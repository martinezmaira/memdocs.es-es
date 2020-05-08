---
title: Implementación de Windows to Go
titleSuffix: Configuration Manager
description: Aprenda a aprovisionar Windows To Go en Configuration Manager para crear un área de trabajo de Windows To Go que se inicie desde una unidad externa.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: add0d17205cc82b30f3a88558c690a813239b92a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906926"
---
# <a name="deploy-windows-to-go-with-configuration-manager"></a>Implementación de Windows to Go con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este tema se proporcionan los pasos para aprovisionar Windows To Go en Configuration Manager. Windows To Go es una función empresarial de Windows 8 que habilita la creación de un área de trabajo Windows To Go que se puede arrancar desde una unidad externa conectada mediante USB en equipos que cumplan los requisitos de certificados de Windows 7 o Windows 8, sin tener en cuenta el sistema operativo que se ejecute en el equipo. Las áreas de trabajo de Windows To Go pueden utilizar la misma imagen que usan las empresas en los equipos de escritorio y portátiles, y se puede administrar de la misma manera.  

 Para obtener más información sobre Windows To Go, consulte [Windows To Go: Introducción a las características](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh831833(v=ws.11)).  

## <a name="provision-windows-to-go"></a>Aprovisionar Windows To Go  
 Windows To Go es un sistema operativo almacenado en una unidad externa conectada mediante USB. Puede aprovisionar la unidad de Windows To Go del mismo modo que aprovisiona otras implementaciones de sistema operativo. Sin embargo, como Windows To Go está diseñado para ser una solución de gran movilidad y centrada en el usuario, debe adoptar un enfoque ligeramente diferente para aprovisionar estas unidades.  

 En un nivel alto, Windows To Go es una implementación en dos fases que le permite configurar el dispositivo Windows To Go y preconfigurar contenido para la implementación del sistema operativo. Puede lograr esto con un impacto mínimo en el usuario y un tiempo de inactividad limitado del equipo del usuario. Después de preconfigurar el equipo, debe completar el proceso de aprovisionamiento para asegurarse de que el equipo esté listo para el usuario. El proceso de aprovisionamiento es similar al proceso de implementación de sistema operativo actual. A continuación se enumera el flujo de trabajo general para preconfigurar contenido y aprovisionar Windows To Go:  

1.  [Requisitos previos para aprovisionar Windows To Go](#BKMK_Prereqs)  

2.  [Crear medios preconfigurados](#BKMK_CreatePrestagedMedia)  

3.  [Crear un paquete de Windows To Go Creator](#BKMK_CreatePackage)  

4.  [Actualizar la secuencia de tareas para habilitar BitLocker para Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Implementar el paquete de Windows To Go Creator y la secuencia de tareas](#BKMK_Deployments)  

6.  [El usuario ejecuta la herramienta Windows To Go Creator](#BKMK_UserExperience)  

7.  [Configuration Manager configura y crea etapas en la unidad de Windows To Go](#BKMK_ConfigureStageDrive)  

8.  [El usuario inicia sesión en Windows 8](#BKMK_UserLogsIn)  

###  <a name="prerequisites-to-provision-windows-to-go"></a><a name="BKMK_Prereqs"></a> Requisitos previos para aprovisionar Windows To Go  
 Antes de que aprovisione Windows To Go, debe completar las siguientes acciones en Configuration Manager:  

-   **Distribuir una imagen de arranque a un punto de distribución**  

     antes de crear los medios preconfigurados, debe distribuir la imagen de arranque en un punto de distribución.  

    > [!NOTE]  
    >  Las imágenes de arranque se usan para instalar el sistema operativo en los equipos de destino dentro del entorno de Configuration Manager. Contienen una versión de Windows PE que instala el sistema operativo, así como todos los controladores de dispositivo adicionales que fuesen necesarios. Configuration Manager proporciona dos imágenes de arranque: Una para plataformas x86 y otra para plataformas x64. También puede crear sus propias imágenes de arranque. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

-   **Distribuir la imagen de sistema operativo Windows 8 a un punto de distribución**  

     antes de crear los medios preconfigurados, debe distribuir la imagen de sistema operativo Windows 8 en un punto de distribución.  

    > [!NOTE]  
    >  Las imágenes de sistema operativo son archivos con formato .WIM y representan una recopilación comprimida de archivos de referencia y carpetas que se necesitan para instalar y configurar correctamente un sistema operativo en un equipo. Para obtener más información, consulte [Administrar imágenes de sistema operativo](../get-started/manage-operating-system-images.md).  

-   **Crear una secuencia de tareas para implementar Windows 8**  

     debe crear una secuencia de tareas para una implementación de Windows 8 a la que hará referencia al crear los medios preconfigurados. Para obtener más información, vea [Manage task sequences to automate tasks](manage-task-sequences-to-automate-tasks.md) (Administración de secuencias de tareas para automatizar tareas).  

###  <a name="create-prestaged-media"></a><a name="BKMK_CreatePrestagedMedia"></a> Crear medios preconfigurados  
 Los medios preconfigurados contienen la imagen de arranque que se utiliza para iniciar el equipo de destino y la imagen de sistema operativo que se aplica al equipo de destino. Mediante el uso de la imagen de arranque, se puede iniciar el equipo que se aprovisiona con los medios preconfigurados. A continuación, el equipo puede ejecutar una secuencia de tareas de implementación de sistema operativo existente para instalar una implementación completa de sistema operativo. La secuencia de tareas que implementa el sistema operativo no se incluye en el medio.  

 Puede agregar contenido, como aplicaciones y controladores de dispositivos, además de la imagen de sistema operativo y la imagen de arranque durante la fase de preconfiguración. Esto reduce el tiempo que se tarda en implementar un sistema operativo y reduce el tráfico de red porque el contenido ya está en la unidad.  

 Utilice el procedimiento siguiente para crear los medios preconfigurados.  

#### <a name="to-create-prestaged-media"></a>Para crear medios preconfigurados  

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear medio de secuencia de tareas** para iniciar el Asistente para crear medio de secuencia de tareas.  

4. En la página **Seleccionar tipo de medio** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

   -   Seleccione **Medio preconfigurado**.  

   -   Seleccione **Permitir la implementación desatendida de sistema operativo** para arrancar la implementación de Windows To Go sin intervención del usuario.  

       > [!IMPORTANT]  
       >  Cuando utilice esta opción con la variable personalizada SMSTSPreferredAdvertID (configurada más adelante en este procedimiento), no será necesaria la interacción del usuario y el equipo arrancará automáticamente en la implementación de Windows To Go cuando detecte una unidad de Windows To Go. Se seguirá solicitando una contraseña al usuario si el medio está configurado para la protección con contraseña. Si usa la opción **Permitir la implementación desatendida de sistema operativo** sin configurar la variable SMSTSPreferredAdvertID, se producirá un error al implementar la secuencia de tareas.  

5. En la página **Administración de medio** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

   -   Seleccione **Medio dinámico** si desea permitir que un punto de administración redirija el medio a otro punto de administración, según la ubicación del cliente en los límites del sitio.  

   -   Seleccione **Medio basado en sitio** si desea que el medio solo se ponga en contacto con el punto de administración especificado.  

6. En la página **Propiedades de medio**  , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

   -   **Creado por**: especifique la persona que creó el medio.  

   -   **Versión**: especifique el número de versión del medio.  

   -   **Comentario**: escriba una descripción única del uso del medio.  

   -   **Archivo multimedia**: especifique el nombre y la ruta de acceso de los archivos de salida. El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: **\\\nombre de servidor\carpeta\archivo de salida.iso**  

7. En la página **Seguridad** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

   -   Seleccione **Habilitar compatibilidad de equipos desconocida** para permitir que el medio implemente un sistema operativo en un equipo que no esté administrado por Configuration Manager. No hay ningún registro de estos equipos en la base de datos de Configuration Manager. Los equipos desconocidos incluyen los siguientes:  

       -   Un equipo que no tiene instalado el cliente de Configuration Manager  

       -   Un equipo que no se importa en Configuration Manager  

       -   Un equipo que no ha detectado Configuration Manager  

   -   Seleccione **Proteger medio con contraseña** y escriba una contraseña segura para ayudar a proteger el medio frente a un acceso no autorizado. Cuando se especifica una contraseña, el usuario debe proporcionar esa contraseña para utilizar el medio preconfigurado.  

       > [!IMPORTANT]  
       >  Por motivos de seguridad, asigne siempre una contraseña para ayudar a proteger el medio preconfigurado.  

       > [!NOTE]  
       >  Cuando proteja el medio preconfigurado con una contraseña, se pedirá la contraseña al usuario incluso cuando el medio esté configurado con la opción **Permitir la implementación desatendida de sistema operativo** .  

   -   Para comunicaciones HTTP, seleccione **Crear certificado autofirmado de medio**y, a continuación, especifique las fechas de inicio y de expiración del certificado.  

   -   Para comunicaciones HTTPS, seleccione **Importar certificado PKI**y, a continuación, especifique el certificado que desea importar y su contraseña.  

        Para obtener más información sobre este certificado de cliente que se usa para imágenes de arranque, consulte [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificado PKI).  

   -   **Afinidad entre usuario y dispositivo**: para admitir la administración centrada en el usuario en Configuration Manager, especifique cómo quiere que el medio asocie los usuarios con el equipo de destino. Para obtener más información sobre cómo es compatible la implementación de sistema operativo con la afinidad entre usuario y dispositivo, consulte [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md) (Asociar usuarios con un equipo de destino).  

       -   Especifique **Permitir afinidad de dispositivo de usuario con autoaprobación** si desea que el medio asocie automáticamente los usuarios al equipo de destino. Esta funcionalidad se basa en las acciones de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino cuando se implementa el sistema operativo en el equipo de destino.  

       -   Especifique **Permitir afinidad de dispositivo de usuario pendiente de la aprobación del administrador** si desea que el medio asocie los usuarios al equipo de destino después de conceder la aprobación. Esta funcionalidad se basa en el ámbito de la secuencia de tareas que implementa el sistema operativo. En este escenario, la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino, pero espera la aprobación del usuario administrativo antes de implementar el sistema operativo.  

       -   Especifique **No permitir afinidad de dispositivo de usuario** si no desea que el medio asocie usuarios al equipo de destino. En este escenario, la secuencia de tareas no asocia usuarios al equipo de destino cuando se implementa el sistema operativo.  

8. En la página **Secuencia de tareas** , especifique la secuencia de tareas de Windows 8 que creó en la sección anterior.  

9. En la página **Imagen de arranque** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    > [!IMPORTANT]  
    >  La arquitectura de la imagen de arranque que se distribuye debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86. En equipos certificados con Windows 8 en modo EFI, debe utilizar una imagen de arranque x64.  

    -   **Imagen de arranque**: especifique la imagen de arranque para iniciar el equipo de destino.  

    -   **Punto de distribución**: especifique el punto de distribución que hospeda la imagen de arranque. El asistente recupera la imagen de arranque desde el punto de distribución y la escribe en el medio.  

        > [!NOTE]  
        >  El usuario administrativo debe tener permisos de **lectura** en el contenido de la imagen de arranque en el punto de distribución. Para obtener más información, vea [Cuenta de acceso de paquetes](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

    -   Si seleccionó **Medio basado en sitio** en la página **Administración de medio** de este asistente, en el cuadro **Punto de administración** , especifique un punto de administración del sitio primario.  

    -   Si seleccionó **Medio dinámico** en la página **Administración de medio** de este asistente, en el cuadro **Puntos de administración asociados** , especifique los puntos de administración del sitio primario que se usarán y un orden de prioridad para las comunicaciones iniciales.  

10. En la página **Imágenes** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Paquete de imagen**: especifique el paquete que contiene la imagen de sistema operativo de Windows 8.  

    -   **Índice de imagen**: especifique la imagen que desea implementar si el paquete contiene varias imágenes de sistema operativo.  

    -   **Punto de distribución**: especifique el punto de distribución que hospeda el paquete de imágenes de sistema operativo. El asistente recupera la imagen de sistema operativo desde el punto de distribución y la escribe en el medio.  

        > [!NOTE]  
        >  El usuario administrativo debe tener permisos de **lectura** en el contenido de la imagen de sistema operativo en el punto de distribución. Para obtener más información, vea [Cuenta de acceso de paquetes](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

11. En la página **Seleccionar aplicación** , especifique el contenido de aplicación que desee incluir en el archivo multimedia y, a continuación, haga clic en **Siguiente**.  

12. En la página **Seleccionar paquete** , especifique el contenido de paquete adicional que desee incluir en el archivo multimedia y, a continuación, haga clic en **Siguiente**.  

13. En la página **Seleccionar el paquete de controladores** , especifique el contenido del paquete de controladores que desee incluir en el archivo multimedia y, a continuación, haga clic en **Siguiente**.  

14. En la página **Puntos de distribución** , seleccione uno o varios puntos de distribución que contengan el contenido que necesita la secuencia de tareas y, a continuación, haga clic en **Siguiente**.  

15. En la página **Personalización** , especifique la siguiente información y, a continuación, haga clic en **Siguiente**.  

    - **Variables**: Especifique las variables que la secuencia de tareas utiliza para implementar el sistema operativo. Para Windows To Go, utilice la variable SMSTSPreferredAdvertID para seleccionar automáticamente la implementación de Windows To Go mediante el formato siguiente:  

       SMSTSPreferredAdvertID = {*IdImplementación*}, donde IdImplementación es el identificador de implementación asociado a la secuencia de tareas que utilizará para completar el proceso de aprovisionamiento para la unidad de Windows To Go.  

      > [!TIP]  
      >  Cuando utilice esta variable con una secuencia de tareas configurada para su ejecución desatendida (configurada anteriormente en este procedimiento), no será necesaria la interacción del usuario y el equipo arrancará automáticamente en la implementación de Windows To Go cuando detecte una unidad de Windows To Go. Se seguirá solicitando una contraseña al usuario si el medio está configurado para la protección con contraseña.  

    - **Comandos de preinicio**: Especifique los comandos de preinicio que desee ejecutar antes de que se ejecute la secuencia de tareas. Los comandos de preinicio pueden ser un script o ejecutable que puede interactuar con el usuario en Windows PE antes de que se ejecute la secuencia de tareas para instalar el sistema operativo. Configure las opciones siguientes para la implementación de Windows To Go:  

      - **OSDBitLockerPIN**: BitLocker para Windows To Go requiere una frase de contraseña. Establezca la variable **OSDBitLockerPIN** como parte de un comando de preinicio para establecer la frase de contraseña de BitLocker para la unidad de Windows To Go.  

        > [!WARNING]  
        >  Después de habilitar BitLocker para la frase de contraseña, el usuario debe indicar esta frase de contraseña cada vez que el equipo arranque en la unidad de Windows To Go.  

      - **SMSTSUDAUsers**: especifica el usuario primario del equipo de destino. Utilice esta variable para recopilar el nombre de usuario, que, a continuación, se puede utilizar para asociar el usuario y el dispositivo. Para obtener más información, consulte [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md) (Asociar usuarios a un equipo de destino).  

        > [!TIP]  
        >  Para recuperar el nombre de usuario, puede crear un cuadro de entrada como parte del comando de preinicio, pedir que el usuario escriba su nombre de usuario y, a continuación, establecer la variable con el valor. Por ejemplo, puede agregar las siguientes líneas al archivo de script del comando de preinicio:  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Para obtener más información sobre cómo crear un archivo de script para usarlo como comando de preinicio, consulte [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas).  

16. Complete el asistente.  

    > [!NOTE]  
    >  El asistente puede tardar un período prolongado de tiempo en completar el archivo multimedia preconfigurado.  

###  <a name="create-a-windows-to-go-creator-package"></a><a name="BKMK_CreatePackage"></a> Crear un paquete de Windows To Go Creator  
 Como parte de la implementación de Windows To Go, debe crear un paquete para implementar el archivo multimedia preconfigurado. El paquete debe incluir la herramienta que configura la unidad de Windows To Go y extrae el medio preconfigurado en la unidad. Utilice el procedimiento siguiente para crear el paquete de Windows To Go Creator.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Para crear el paquete de Windows To Go Creator  

1. En el servidor para hospedar los archivos del paquete de Windows To Go Creator, cree una carpeta de origen para los archivos de origen del paquete.  

   > [!NOTE]  
   >  La cuenta de equipo del servidor de sitio debe tener permisos de acceso de **lectura** en la carpeta de origen.  

2. Copie el archivo multimedia preconfigurado que creó en la sección [Create prestaged media](#BKMK_CreatePrestagedMedia) en la carpeta de origen del paquete.  

3. Copie la herramienta de Windows To Go Creator (WTGCreator.exe) en la carpeta de origen del paquete. La herramienta Creator está disponible en cualquier servidor de sitio primario en la siguiente ubicación: <*carpeta de instalación de Configuration Manager*>\OSD\Tools\WTG\Creator.  

4. Cree un paquete y un programa con el Asistente para crear paquetes y programas.  

5. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

6. En el área de trabajo **Biblioteca de software** , expanda **Administración de aplicaciones**y, a continuación, haga clic en **Paquetes**.  

7. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear paquete**.  

8. En la página **Paquete** , especifique el nombre y la descripción del paquete. Por ejemplo, escriba **Windows To Go** como nombre del paquete y especifique la descripción **Paquete para configurar una unidad de Windows To Go con Configuration Manager**.  

9. Seleccione **Este paquete contiene archivos de origen**, especifique la ruta de acceso de la carpeta origen del paquete que creó en el paso 1 y, a continuación, haga clic en **Siguiente**.  

10. En la página **Tipo de programa** , seleccione **Programa estándar**y, a continuación, haga clic en **Siguiente**.  

11. En la página **Programa estándar** , especifique lo siguiente:  

    -   **Nombre**: especifique el nombre del programa. Por ejemplo, escriba **Creator** como nombre del programa.  

    -   **Línea de comandos**: escriba **WTGCreator.exe /wim:PrestageName.wim**, donde PrestageName es el nombre del archivo preconfigurado que ha creado y copiado en la carpeta de origen del paquete para el paquete de Windows To Go Creator.  

         Si lo desea, puede agregar las siguientes opciones:  

        -   **enableBootRedirect**: opción de línea de comandos para cambiar las opciones de inicio de Windows To Go para permitir la redirección del arranque. Cuando use esta opción, el equipo arrancará desde una unidad USB sin necesidad de cambiar el orden de arranque en el firmware del equipo ni de hacer que el usuario seleccione una opción de una lista de opciones de arranque durante el inicio. Si se detecta una unidad de Windows To Go, el equipo se arranca en esa unidad.  

    -   **Ejecutar**: especifique **Normal** para ejecutar el programa según los valores predeterminados del sistema y el programa.  

    -   **El programa se puede ejecutar**: especifique si el programa puede ejecutarse solo cuando un usuario inicia sesión.  

    -   **Modo de ejecución**: especifique si el programa se ejecutará con los permisos de los usuarios conectados o con permisos administrativos. La herramienta Windows To Go Creator requiere permisos elevados para su ejecución.  

    -   Seleccione **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**y, a continuación, haga clic en **Siguiente**.  

12. En la página Requisitos, especifique lo siguiente:  

    - **Requisitos de la plataforma**: seleccione las plataformas de Windows 8 aplicables para permitir el aprovisionamiento.  

    - **Espacio en disco estimado**: especifique el tamaño de la carpeta de origen del paquete para Windows To Go Creator.  

    - **Duración máxima permitida de la ejecución (minutos)** : especifica el tiempo máximo que se espera que el programa se ejecute en el equipo cliente. De forma predeterminada, este valor está establecido en 120 minutos.  

      > [!IMPORTANT]  
      >  Si está usando ventanas de mantenimiento para la recopilación en la que se ejecuta este programa, puede producirse un conflicto si la **Duración máxima permitida de la ejecución** es mayor que la ventana de mantenimiento programada. Si el tiempo máximo de ejecución se establece como **Desconocido**, comenzará durante la ventana de mantenimiento, pero seguirá ejecutándose hasta que se complete o se produzca un error después de cerrar la ventana de mantenimiento. Si establece el tiempo de ejecución máximo en un periodo específico (no configurado como Desconocido) que supera la duración de cualquiera de las ventanas de mantenimiento disponibles, no se ejecutará el programa.  

      > [!NOTE]  
      >  Si el valor se configura como **Desconocido**, Configuration Manager establece el tiempo máximo de ejecución permitido en 12 horas (720 minutos).  

      > [!NOTE]  
      >  Si se supera el tiempo de ejecución máximo (ya sea un valor establecido por el usuario o el valor predeterminado), Configuration Manager detiene el programa si se selecciona **Ejecutar con derechos administrativos** y no se selecciona **Permitir a los usuarios ver la instalación del programa e interactuar con la misma** en la página **Programa estándar**.  

      Haga clic en **Siguiente** y complete el asistente.  

###  <a name="update-the-task-sequence-to-enable-bitlocker-for-windows-to-go"></a><a name="BKMK_UpdateTaskSequence"></a> Actualizar la secuencia de tareas para habilitar BitLocker para Windows To Go  
 Windows To Go habilita BitLocker en una unidad externa de arranque sin el uso de TPM. Por lo tanto, debe utilizar una herramienta independiente para configurar BitLocker en la unidad de Windows To Go. Para habilitar BitLocker, debe agregar una acción a la secuencia de tareas después del paso **Instalar Windows y Configuration Manager** paso.  

> [!NOTE]  
>  BitLocker para Windows To Go requiere una frase de contraseña. En el paso [Create prestaged media](#BKMK_CreatePrestagedMedia) , se establece la frase de contraseña como parte de un comando de preinicio mediante la variable OSDBitLockerPIN.  

 Utilice el siguiente procedimiento para actualizar la secuencia de tareas de Windows 8 para habilitar BitLocker para Windows To Go.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Para actualizar la secuencia de tareas de Windows 8 para habilitar BitLocker  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Administración de aplicaciones**y, a continuación, haga clic en **Paquetes**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear paquete**.  

4.  En la página **Paquete** , especifique el nombre y la descripción del paquete. Por ejemplo, escriba **BitLocker for Windows To Go** como el nombre del paquete y especifique **Package to update BitLocker for Windows To Go** como su descripción.  

5.  Seleccione **Este paquete contiene archivos de origen**, especifique la ubicación de la herramienta BitLocker para Windows To Go y, a continuación, haga clic en **Siguiente**. La herramienta BitLocker está disponible en cualquier servidor de sitio primario de Configuration Manager en la siguiente ubicación: <*carpeta de instalación de Configuration Manager*>\OSD\Tools\WTG\BitLocker\.  

6.  En la página **Tipo de programa** , seleccione **No crear un programa**.  

7.  Haga clic en **Siguiente** y complete el asistente.  

8.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

9. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

10. Seleccione la secuencia de tareas de Windows 8 a la que se hace referencia en los medios preconfigurados.  

11. En la pestaña **Inicio** , en el grupo **Secuencia de tareas** , haga clic en **Editar**.  

12. Haga clic en el paso **Instalar Windows y Configuration Manager** , haga clic en **Agregar**, haga clic en **General**y, a continuación, haga clic en **Ejecutar línea de comandos**. El paso Ejecutar línea de comandos se agrega después del paso Instalar Windows y Configuration Manager.  

13. En la pestaña **Propiedades** del paso **Ejecutar línea de comandos** , agregue lo siguiente:  

    1.  **Nombre**: especifique un nombre para la línea de comandos, como **Habilitar BitLocker para Windows To Go**.  

    2.  **Línea de comandos**: i386\osdbitlocker_wtg.exe /Enable /pwd:< *None&#124;AD*>  

         Parámetros:  

        -   /pwd:<None&#124;AD>: especifique el modo de recuperación de contraseña de BitLocker. Este parámetro es necesario si utiliza el parámetro /Enable en la línea de comandos.  

             Seleccione **AD** para configurar el Cifrado de unidad BitLocker para realizar una copia seguridad de la información de recuperación de unidades protegidas con BitLocker en Servicios de dominio de Active Directory (AD DS). La copia de seguridad de contraseñas de recuperación de una unidad protegida con BitLocker permite a los usuarios administrativos recuperar la unidad si está bloqueada. Esto garantiza que los usuarios autorizados siempre podrán tener acceso a datos cifrados que pertenecen a la empresa. Cuando se especifica **None**, el usuario es responsable de mantener una copia de la contraseña de recuperación o la clave de recuperación. Si el usuario pierde dicha información o se olvida de descifrar la unidad antes de salir de la organización, los usuarios administrativos no podrán acceder fácilmente a la unidad.  

        -   /wait:<TRUE&#124;FALSE>: especifique si la secuencia de tareas espera que el cifrado se complete antes de finalizar.  

    3.  Seleccione **Paquete**y, a continuación, especifique el paquete que creó al principio de este procedimiento.  

    4.  En la pestaña **Opciones** , agregue las siguientes condiciones:  

        -   Condición = Variable de secuencia de tareas  

        -   Variable = _SMSTSWTG  

        -   Condición = Igual a  

        -   Valor = True  

    > [!NOTE]  
    >  El paso **Habilitar BitLocker** , que es probable que se produzca después del paso de línea de comandos nuevo, no se utiliza para habilitar BitLocker para Windows To Go. Sin embargo, puede mantener este paso en la secuencia de tareas que se utilizará para las implementaciones de Windows 8 que no utilicen una unidad de Windows To Go.  

###  <a name="deploy-the-windows-to-go-creator-package-and-task-sequence"></a><a name="BKMK_Deployments"></a> Implementar el paquete de Windows To Go Creator y la secuencia de tareas  
 Windows To Go es un proceso de implementación híbrida. Por lo tanto, debe implementar el paquete de Windows To Go Creator y la secuencia de tareas de Windows 8. Utilice los procedimientos siguientes para completar el proceso de implementación.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Para implementar el paquete de Windows To Go Creator  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Administración de aplicaciones**y, a continuación, haga clic en **Paquetes**.  

3.  Seleccione el paquete de Windows To Go que creó en el paso [Crear un paquete de Windows To Go Creator](#BKMK_CreatePackage) .  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

5.  En la página **General** , especifique la siguiente configuración:  

    1.  **Software**: compruebe que el paquete de Windows To Go está seleccionado.  

    2.  **Colección**: haga clic en **Examinar** para seleccionar la colección en la que quiere implementar el paquete de Windows To Go.  

    3.  **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación**: seleccione esta opción si desea almacenar el contenido del paquete en el grupo de puntos de distribución de recopilaciones predeterminado. Si no asocia la recopilación seleccionada con un grupo de puntos de distribución, esta opción no estará disponible.  

6.  En la página **Contenido** , haga clic en **Agregar** y, a continuación, seleccione los puntos de distribución o los grupos de puntos de distribución en los que desee implementar el contenido asociado a este paquete y programa.  

7.  En la página **Configuración de implementación** , seleccione **Disponible** como tipo de implementación y, a continuación, haga clic en **Siguiente**.  

8.  En **Programación**, configure cuándo se implementará o será disponible para dispositivos cliente este paquete y programa.  

     Las opciones de esta página variarán dependiendo de si la acción de la implementación se establece en **Disponible** o **Requerido**.  

9. En la página **Programación**, configure las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    1.  **Programar cuándo estará disponible esta implementación**: especifique la fecha y hora en que el paquete y programa estarán disponibles para su ejecución en el equipo de destino. Cuando seleccione **UTC**, este valor asegura que el paquete y programa están disponibles para varios equipos de destino al mismo tiempo, en lugar de en momentos diferentes, según la hora local de los equipos de destino.  

    2.  **Programar cuándo expirará esta implementación**: especifique la fecha y hora de expiración del paquete y programa en el equipo de destino. Cuando seleccione **UTC**, este valor garantiza que la secuencia de tareas expira en varios equipos de destino al mismo tiempo, en lugar de en momentos diferentes, según la hora local de los equipos de destino.  

10. En la página **Experiencia del usuario** del asistente, especifique la siguiente información:  

    -   **Instalación de software**: permite que el software se instale fuera de las ventanas de mantenimiento configuradas.  

    -   **Reinicio del sistema (si es necesario para completar la instalación)** : permite que un dispositivo se reinicie fuera de las ventanas de mantenimiento configuradas cuando así lo requiera la instalación del software.  

    -   **Dispositivos de Embedded**: Cuando implementa paquetes y programas en dispositivos de Windows Embedded habilitados con filtro de escritura, puede especificar la instalación de paquetes y programas en la superposición temporal y confirmar los cambios más tarde, o puede confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.  

11. En la página **Puntos de distribución** , especifique la siguiente información:  

    -   **Opciones de implementación:** especifique **Descargar contenido desde el punto de distribución y ejecutar localmente**.  

    -   **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: para reducir la carga en la red, seleccione esta opción para permitir que los clientes descarguen contenido de otros clientes en la red que ya han descargado el contenido y lo han almacenado en la memoria caché. Esta opción utiliza Windows BranchCache y se puede utilizar en equipos que ejecutan Windows Vista SP2 y posterior.  

    -   **Permitir a los clientes usar una ubicación de origen de reserva para el contenido**: especifique si desea permitir que los clientes usen un punto de distribución no preferido de reserva como ubicación de origen del contenido si este no está disponible en un punto de distribución preferido.  

12. Complete el asistente.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Para implementar la secuencia de tareas de Windows 8  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  Seleccione la tarea de secuencias de Windows 8 que creó en el paso [Prerequisites to provision Windows To Go](#BKMK_Prereqs) .  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

5.  En la página **General** , especifique la siguiente configuración:  

    1.  **Secuencia de tareas**: compruebe que la secuencia de tareas de Windows 8 esté seleccionada.  

    2.  **Colección**: Haga clic en **Examinar** para seleccionar la recopilación que incluye todos los dispositivos para los que un usuario podría aprovisionar Windows To Go.  

        > [!IMPORTANT]  
        >  Si el medio preconfigurado que creó en la sección [Crear medios preconfigurados](#BKMK_CreatePrestagedMedia) usa la variable SMSTSPreferredAdvertID, puede implementar la secuencia de tareas en la recopilación **Todos los sistemas** y especificar la opción **Solo Windows PE (oculta)** en la página **Contenido** . Como la secuencia de tareas está oculta, solo estará disponible para los medios.  

    3.  **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación**: seleccione esta opción si desea almacenar el contenido del paquete en el grupo de puntos de distribución de recopilaciones predeterminado. Si no asocia la recopilación seleccionada con un grupo de puntos de distribución, esta opción no estará disponible.  

6.  En la página **Configuración de implementación** , configure las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   **Finalidad**: seleccione **Disponible**. Cuando implementa la secuencia de tareas en un usuario, el usuario verá la secuencia de tareas publicada en el catálogo de aplicaciones y podrá solicitarla a petición. Si implementa la secuencia de tareas en un dispositivo, el usuario verá la secuencia de tareas en el Centro de Software y podrá instalarla a petición.  

    -   **Estar disponible para**: especifique si la secuencia de tareas debe estar disponible para medios, el entorno PXE o clientes de Configuration Manager.  

        > [!IMPORTANT]  
        >  Use la opción **Sólo medios y PXE (ocultos)** para implementaciones automatizadas de secuencia de tareas. Seleccione **Permitir la implementación desatendida de sistema operativo** y configure la variable SMSTSPreferredAdvertID como parte del medio preconfigurado para que el equipo arranque automáticamente en la implementación de Windows To Go sin interacción del usuario cuando detecta una unidad de Windows To Go. Para obtener más información acerca de las opciones de medios preconfigurados, consulte la sección [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  En la página **Programación** , configure las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    1.  **Programar cuándo estará disponible esta implementación**: especifique la fecha y la hora en las que la secuencia de tareas estará disponible para su ejecución en el equipo de destino. Cuando se selecciona **UTC**, este valor garantiza que la secuencia de tareas estará disponible en varios equipos de destino al mismo tiempo, en lugar de en momentos diferentes, según la hora local de los equipos de destino.  

    2.  **Programar cuándo expirará esta implementación**: especifique la fecha y la hora de expiración de la secuencia de tareas en el equipo de destino. Cuando seleccione **UTC**, este valor garantiza que la secuencia de tareas expira en varios equipos de destino al mismo tiempo, en lugar de en momentos diferentes, según la hora local de los equipos de destino.  

8.  En la página **Experiencia del usuario** , especifique la siguiente información:  

    -   **Mostrar progreso de la secuencia de tareas**: especifique si el cliente de Configuration Manager debe mostrar el progreso de la secuencia de tareas.  

    -   **Instalación de software**: especifique si el usuario puede instalar software fuera de las ventanas de mantenimiento configuradas después del tiempo programado.  

    -   **Reinicio del sistema (si es necesario para completar la instalación)** : permite que un dispositivo se reinicie fuera de las ventanas de mantenimiento configuradas cuando así lo requiera la instalación del software.  

    -   **Dispositivos de Embedded**: Cuando implementa paquetes y programas en dispositivos de Windows Embedded habilitados con filtro de escritura, puede especificar la instalación de paquetes y programas en la superposición temporal y confirmar los cambios más tarde, o puede confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.  

    -   **Clientes basados en Internet**: especifique si la secuencia de tareas se puede ejecutar en un cliente basado en Internet. Las operaciones que instalan software, como un sistema operativo, no son compatibles con esta configuración. Utilice esta opción solo para secuencias de tareas basadas en scripts que realizan operaciones en el sistema operativo estándar.  

9. En la página **Alertas** , especifique la configuración de alertas que desea establecer para esta implementación de secuencia de tareas y, a continuación, haga clic en **Siguiente**.  

10. En la página **Puntos de distribución** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

    -   **Opciones de implementación**: seleccione **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas**.  

    -   **Cuando no haya disponible ningún punto de distribución local, usar un punto de distribución remoto**: especifique si los clientes pueden utilizar puntos de distribución en redes lentas y poco confiables para descargar el contenido requerido por la secuencia de tareas.  

    -   **Permitir a los clientes usar una ubicación de origen de reserva para el contenido**:
        - *Antes de la versión 1610*, se puede activar la casilla Permitir ubicación de origen de reserva para contenido para permitir a los clientes que están fuera de estos grupos de límites que reviertan y usen el punto de distribución como ubicación de origen para el contenido cuando no estén disponibles otros puntos de distribución.
        - *A partir de la versión 1610*, ya no se puede configurar **Permitir ubicación de origen de reserva para contenido**.  En su lugar, se deben configurar relaciones entre grupos de límites que determinen cuándo puede un cliente empezar a buscar grupos de límites adicionales para una ubicación de origen de contenido válida. 

11. Complete el asistente.  

###  <a name="user-runs-the-windows-to-go-creator"></a><a name="BKMK_UserExperience"></a> El usuario ejecuta la herramienta Windows To Go Creator  
 Después de implementar el paquete de Windows To Go y la secuencia de tareas de Windows 8, Windows To Go Creator está disponible para el usuario. El usuario puede ir al catálogo de software o al Centro de software si se ha implementado Windows To Go Creator en los dispositivos, y ejecutar el programa Windows To Go Creator. Una vez descargado el paquete de Creator, se muestra un icono intermitente en la barra de tareas. Cuando el usuario hace clic en el icono, se muestra un cuadro de diálogo para que el usuario seleccione la unidad de Windows To Go que desea aprovisionar (a menos que se use la opción de línea de comandos /drive). Si la unidad no cumple los requisitos de Windows To Go o no tiene suficiente espacio libre en disco para instalar la imagen, Creator muestra un mensaje de error. El usuario puede comprobar la unidad y la imagen que se aplicarán en la página de confirmación. A medida que Creator configura y preconfigura contenido en la unidad de Windows To Go, muestra un cuadro de diálogo de progreso. Al finalizar la preconfiguración, Creator muestra una solicitud de reinicio del equipo para arrancar en la unidad de Windows To Go.  

> [!NOTE]  
>  Si no habilitó la redirección del arranque como parte de la línea de comandos de Creator en la sección [Crear un paquete de Windows To Go Creator](#BKMK_CreatePackage) , es posible que el usuario deba arrancar manualmente en la unidad de Windows To Go cada vez que se reinicia el sistema.  

###  <a name="configuration-manager-configures-and-stages-the-windows-to-go-drive"></a><a name="BKMK_ConfigureStageDrive"></a> Configuration Manager configura y crea etapas en la unidad de Windows To Go  
 Después de que el equipo reinicie la unidad de Windows To Go, la unidad arrancará en Windows PE y se conectará al punto de administración para obtener la directiva y finalizar la implementación de sistema operativo. Configuration Manager configura y crea etapas en la unidad. Después de que Configuration Manager cree etapas en la unidad, el usuario puede reiniciar el equipo para finalizar el proceso de aprovisionamiento (por ejemplo, unirse a un dominio o instalar aplicaciones). Este proceso es el mismo para todos los medios preconfigurados.  

###  <a name="user-logs-in-to-windows-8"></a><a name="BKMK_UserLogsIn"></a> El usuario inicia sesión en Windows 8  
 Cuando Configuration Manager finaliza el proceso de aprovisionamiento y se muestra la pantalla de bloqueo de Windows 8, el usuario puede iniciar sesión en el sistema operativo.  
