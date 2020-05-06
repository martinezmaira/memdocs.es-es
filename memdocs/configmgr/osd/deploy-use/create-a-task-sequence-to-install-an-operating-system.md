---
title: Crear una secuencia de tareas para instalar un sistema operativo
titleSuffix: Configuration Manager
description: Use secuencias de tareas de Configuration Manager para instalar automáticamente una imagen de SO y otro contenido en un equipo de destino.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e1b298856edea3f81cab2e9cd5ab75af49dff51
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707313"
---
# <a name="create-a-task-sequence-to-install-an-os"></a>Crear una secuencia de tareas para instalar un sistema operativo

*Se aplica a: Configuration Manager (rama actual)*

Use secuencias de tareas en Configuration Manager para instalar automáticamente una imagen de SO en un equipo de destino. Cree una secuencia de tareas que haga referencia a la imagen de arranque que se usa para iniciar el equipo de destino, la imagen de SO que quiere instalar en el equipo de destino y cualquier otro contenido adicional (por ejemplo, otras aplicaciones o actualizaciones de software) que quiera instalar. A continuación, implemente la secuencia de tareas en la recopilación que contiene el equipo de destino.  

## <a name="create-a-task-sequence-to-install-an-os"></a><a name="BKMK_InstallOS"></a> Creación de una secuencia de tareas para instalar un sistema operativo

Hay muchos escenarios para implementar un sistema operativo en los equipos del entorno. En la mayoría de los casos, cree una secuencia de tareas y seleccione **Instalar un paquete de imágenes existente** en el Asistente para crear secuencia de tareas. Esta opción crea una secuencia de tareas que instala el sistema operativo, migra la configuración de usuario, aplica las actualizaciones de software e instala las aplicaciones.

### <a name="prerequisites"></a>Requisitos previos

Antes de crear una secuencia de tareas para instalar un sistema operativo, se deben instaurar los requisitos siguientes:

#### <a name="required"></a>Requerido

- Una [imagen de arranque](../get-started/manage-boot-images.md)  

- Una [imagen de sistema operativo](../get-started/manage-operating-system-images.md)  

#### <a name="required-if-used"></a>Necesario (si se usa)

- Sincronizar [actualizaciones de software](../../sum/get-started/synchronize-software-updates.md)  

- Agregar [aplicaciones](../../apps/deploy-use/create-applications.md)  

### <a name="process-to-create-a-task-sequence-that-installs-an-os"></a>Proceso para crear una secuencia de tareas que instale un sistema operativo  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione el nodo **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear secuencia de tareas**. Esta acción inicia el Asistente para crear secuencia de tareas.  

3. En la página **Crear nueva secuencia de tareas**, seleccione **Instalar un paquete de imágenes existente** y luego elija **Siguiente**.  

4. En la página **Información de secuencia de tareas**, especifique la siguiente configuración:  

    - **Nombre de la secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

    - **Descripción**: especifique una descripción de lo que la secuencia de tareas hace.  

    - **Imagen de arranque**: Especifique la imagen de arranque que la secuencia de tareas usa para instalar el sistema operativo en el equipo de destino. La imagen de arranque contiene una versión de Windows PE, además de los controladores de dispositivo adicionales necesarios. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        > La arquitectura de la imagen de arranque debe ser compatible con la arquitectura de hardware del equipo de destino.  

5. En la página **Instalar Windows**, especifique la siguiente configuración:  

    - **Paquete de imagen**: especifique el paquete que contiene la imagen de SO que desea instalar. Para más información, vea [Administrar imágenes de SO](../get-started/manage-operating-system-images.md).  

    - **Imagen**: si el paquete de imágenes de sistema operativo contiene varias imágenes, especifique el índice de la que quiera instalar.  

    - **Particionar y formatear el equipo de destino antes de instalar el sistema operativo**: especifique si desea que la secuencia de tareas particione y formatee el equipo de destino antes de que instale el SO.  

    - **Clave de producto**: especifique la clave de producto de Windows, si es necesario. Puede especificar claves de licencia por volumen codificadas y claves de producto estándar. Si utiliza una clave de producto no codificada, cada grupo de cinco caracteres debe estar separado por un guion (`-`). Por ejemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    - **Modo de licencia de servidor**: especifique que la licencia de servidor es **Por puesto**, **Por servidor**, o bien que no se especifica ninguna licencia. Si la licencia de servidor es **Por servidor**, especifique también el número máximo de conexiones de servidor.  

    - Especifique cómo se va a controlar la cuenta de administrador del sistema operativo nuevo:  

        - **Generar la contraseña de la cuenta de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas (recomendado)** : Windows deshabilita la cuenta de administrador local después de que la secuencia de tareas implemente la imagen de sistema operativo.  

        - **Habilitar la cuenta y especificar la contraseña de administrador local**: Windows usa la misma contraseña para la cuenta de administrador local en todos los equipos en los que la secuencia de tareas implementa esta imagen de SO.  

6. En la página **Configurar red**, especifique la siguiente configuración:  

    - **Unirse a un grupo de trabajo**: agregue el equipo de destino a un grupo de trabajo.  

    - **Unirse a un dominio**: agregue el equipo de destino a un dominio. En **Dominio**, especifique el nombre del dominio.  

        > [!IMPORTANT]  
        > Puede examinar para localizar los dominios del bosque local, pero debe especificar el nombre de dominio para un bosque remoto.  

        También puede especificar una unidad organizativa (UO) en el campo **Unidad organizativa de dominio**. Este valor es opcional y especifica el nombre distintivo LDAP X.500 de la unidad organizativa. Si todavía no existe, Windows crea la cuenta de equipo en esta unidad organizativa.  

    - **Cuenta**: el nombre de usuario y la contraseña de la cuenta que tenga permisos para unirse al dominio especificado. Por ejemplo: *dominio\usuario* o *%variable%* .  

        > [!IMPORTANT]  
        > Si planea migrar la configuración del dominio o la configuración del grupo de trabajo, especifique las credenciales de dominio apropiadas.  

7. En la página **Instalar Configuration Manager**, especifique el paquete de cliente de Configuration Manager que quiere instalar en el equipo de destino. También puede incluir propiedades de instalación.  

8. En la página **Migración de estado**, especifique la información siguiente:  

    - **Capturar configuración de usuario**: la secuencia de tareas captura el estado de usuario. Para más información sobre cómo capturar y restaurar el estado de usuario, vea [Manage user state (Administrar el estado de usuario)](../get-started/manage-user-state.md).  

    - **Capturar configuración de red**: la secuencia de tareas captura la configuración de red del equipo de destino. Captura la pertenencia del dominio o del grupo de trabajo, además de la configuración del adaptador de red.  

    - **Capturar configuración de Microsoft Windows**: la secuencia de tareas captura la configuración de Windows del equipo de destino antes de instalar la imagen de sistema operativo. Captura el nombre de equipo, el nombre de usuario registrado y de organización, y la configuración de zona horaria.  

9. En la página **Incluir actualizaciones**, especifique si desea instalar las actualizaciones de software necesarias, todas las actualizaciones de software o ninguna. Si especifica que se instalen las actualizaciones de software, Configuration Manager instala solo las que se destinan a las colecciones a las que pertenece el equipo de destino.  

10. En la página **Instalar aplicaciones**, especifique las aplicaciones que desee instalar en el equipo de destino. Si especifica varias aplicaciones, también puede especificar que la secuencia de tareas continúe si se produce un error en la instalación de una aplicación específica.  

11. Complete el asistente.  

Ahora puede implementar la secuencia de tareas en una recopilación de equipos. Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md).


## <a name="pre-cache-content"></a>Caché previa de contenido

<!--4224642-->
A partir de la versión 1906, puede habilitar este tipo de secuencia de tareas para almacenar el contenido en una caché previa. La característica de caché previa para las implementaciones disponibles de secuencias de tareas permite que los clientes descarguen el contenido pertinente antes de que un usuario instale la secuencia de tareas.  

Para obtener más información, vea [Configuración del contenido de la caché previa](configure-precache-content.md).


## <a name="example-task-sequence"></a><a name="BKMK_InstallExistingOSImageTSExample"></a> Secuencia de tareas de ejemplo

Use la tabla siguiente como guía para crear una secuencia de tareas que implemente un sistema operativo mediante una imagen de sistema operativo existente. La tabla ayuda a decidir la secuencia general de los pasos de la secuencia de tareas y cómo organizar y estructurar los pasos de la secuencia de tareas en grupos lógicos. La secuencia de tareas que cree puede ser diferente a la de este ejemplo y puede contener más o menos pasos y grupos de secuencias de tareas.  

> [!NOTE]  
> Use al Asistente para crear la secuencia de tareas para crear esta secuencia de tareas.  
>
> Cuando se usa el Asistente para crear secuencia de tareas para crear esta nueva secuencia de tareas, algunos de los nombres de paso son diferentes de lo serían si agrega manualmente estos pasos a una secuencia de tareas existente de la secuencia de tareas.

|Grupo o paso de secuencia de tareas|Descripción|  
|---------------------------------|-----------------|  
|Capturar archivos y configuraciones - **(nuevo grupo de secuencia de tareas)**|Crear un grupo de secuencia de tareas. Un grupo de secuencia de tareas mantiene pasos similares de secuencia de tareas para una mejor organización y un control de errores.<br /><br /> Este grupo contiene los pasos necesarios para capturar archivos y configuraciones del sistema operativo de un equipo de referencia.|  
|Capturar configuración de Windows|Utilice este paso de la secuencia de tareas para identificar la configuración de Microsoft Windows para capturar desde el equipo de referencia. Puede capturar el nombre de equipo, usuario e información de la organización y la configuración de zona horaria.|  
|Capturar configuración de red|Utilice este paso de la secuencia de tareas para capturar a la configuración de red del equipo de referencia. Puede capturar a la pertenencia de grupo de trabajo o dominio del equipo de referencia y el adaptador de red, información de configuración.|  
|Capturar archivos de usuario y configuraciones: **(nuevo subgrupo de secuencia de tareas)**|Crear un grupo de secuencia de tareas dentro de un grupo de secuencia de tareas. Este subgrupo contiene los pasos necesarios para capturar los datos de estado de usuario. De forma similar al grupo inicial que agregó, este subgrupo mantiene pasos de secuencia de tareas parecidos para una mejor organización y control de errores.|  
|Almacenamiento de información de estado de usuario de solicitud|Utilice este paso de la secuencia de tareas para solicitar acceso a un punto de migración de estado donde se almacenan los datos de estado de usuario. Puede configurar este paso de la secuencia de tareas para capturar o restaurar la información de estado de usuario.|  
|Capturar archivos de usuario y configuración|Use este paso de la secuencia de tareas para usar la herramienta de migración de estado de usuario (USMT) para capturar el estado de usuario y la configuración del equipo de referencia que recibirá la secuencia de tareas asociada a este paso de la tarea. Puede capturar las opciones estándar o configurar qué opciones desea capturar.|  
|Almacenamiento de información de estado de usuario de la versión|Utilice este paso de la secuencia de tareas para notificar el estado del punto de migración que la acción de captura o la restauración está completa.|  
|Instalar el sistema operativo: **(nuevo grupo de secuencia de tareas)**|Cree otro subgrupo de secuencia de tareas. Este subgrupo contiene los pasos necesarios para instalar y configurar el entorno Windows PE.|  
|Reiniciar en Windows PE|Utilice este paso de la secuencia de tareas para especificar las opciones de reinicio del equipo de destino que recibe esta secuencia de tareas. Este paso mostrará un mensaje al usuario indicando que se reiniciará el equipo para que pueda continuar la instalación.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSInWinPE** de solo lectura. Si el valor asociado es igual a **false** sigue el paso de la secuencia de tareas.|  
|Disco de partición 0|Este paso especifica las acciones necesarias para formatear el disco duro del equipo de destino. El número de disco predeterminado es **0**.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSClientCache** de solo lectura. Este paso se ejecuta si la caché de cliente de Configuration Manager no existe.|  
|Aplicar sistema operativo|Utilice este paso de la secuencia de tareas para instalar la imagen de sistema operativo en el equipo de destino. Este paso primero elimina todos los archivos del volumen, salvo los archivos de control específicos de Configuration Manager. A continuación, aplica todas las imágenes de volumen incluidas en el archivo WIM al volumen de disco secuencial correspondiente en el equipo de destino. Puede especificar un **sysprep** archivo de respuesta y también configurar qué partición de disco se utiliza para la instalación.|  
|Aplicar configuraciones de Windows|Utilice este paso de la secuencia de tareas para configurar la información de configuración de la configuración de Windows para el equipo de destino. Puede aplicar la configuración de windows es usuarios e información organizativa, información de clave de producto o licencia, zona horaria y la contraseña de administrador local.|  
|Aplicar configuración de red|Utilice este paso de la secuencia de tareas para especificar la información de configuración de red o grupo de trabajo del equipo de destino. También puede especificar si el equipo utiliza un servidor DHCP o puede asignar estáticamente la información de dirección IP.|  
|Aplicar controladores del dispositivo|Utilice este paso de la secuencia de tareas para instalar a controladores como parte de la implementación de sistema operativo. Para permitir que el Programa de instalación de Windows busque todas las categorías de controladores existentes, seleccione **Considerar controladores de todas las categorías** o, para limitar las categorías de controlador en las que busca el Programa de instalación de Windows, seleccione **Limitar la coincidencia de controladores a los controladores de las categorías seleccionadas**.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSMediaType** de solo lectura. Este paso de secuencia de tareas se ejecuta solo si el valor de la variable no es igual a **FullMedia**.|  
|Aplicar paquete de controladores|Utilice este paso de la secuencia de tareas para hacer que todos los controladores de dispositivo en un paquete de controladores disponibles para su uso por el programa de instalación de Windows.|  
|Instalar sistema operativo: **(nuevo grupo de secuencia de tareas)**|Cree otro subgrupo de secuencia de tareas. Este subgrupo contiene los pasos necesarios para configurar el sistema operativo instalado.|  
|Instalar Windows y Configuration Manager|Use este paso de secuencia de tareas para instalar el software cliente de Configuration Manager. Configuration Manager instala y registra el GUID del cliente de Configuration Manager. Puede asignar los parámetros de instalación necesarios en la ventana **Propiedades de instalación** .|  
|Instalar actualizaciones|Utilice este paso de secuencia de tareas para especificar cómo se instalan las actualizaciones de software en el equipo de destino. No se evalúa si hay actualizaciones de software aplicables al equipo de destino hasta que se ejecuta este paso de secuencia de tareas. En ese momento, se evalúa si existen actualizaciones de software para el equipo de destino similares a las de cualquier otro cliente administrado de Configuration Manager.<br /><br /> Este paso usa la variable de secuencia de tareas **_SMSTSMediaType** de solo lectura. Este paso de secuencia de tareas se ejecuta solo si el valor de la variable no es igual a **FullMedia**.|  
|Restaurar configuración y archivos de usuario **(nuevo subgrupo de secuencia de tareas)**|Cree otro subgrupo de secuencia de tareas. Este subgrupo contiene los pasos necesarios para restaurar los archivos de usuario y la configuración.|  
|Almacenamiento de información de estado de usuario de solicitud|Utilice este paso de la secuencia de tareas para solicitar acceso a un punto de migración de estado donde se almacenan los datos de estado de usuario.|  
|Restaurar archivos de usuario y configuración|Utilice este paso de la secuencia de tareas para ejecutar la herramienta de migración de estado de usuario (USMT) para restaurar el estado de usuario y la configuración en un equipo de destino.|  
|Almacenamiento de información de estado de usuario de la versión|Use este paso de secuencia de tareas para notificar al punto de migración de estado que los datos de estado de usuario ya no son necesarios.|  
