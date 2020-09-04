---
title: Crear medios independientes
titleSuffix: Configuration Manager
description: Use un medio independiente para implementar el sistema operativo en un equipo sin conexión de red.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c8710c50dc2feabebd7e8f0f84ac49b3b0dd35c
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068028"
---
# <a name="create-stand-alone-media"></a>Crear medios independientes

*Se aplica a: Configuration Manager (rama actual)*

Los medios independientes de Configuration Manager contienen todo lo necesario para implementar el sistema operativo en un equipo sin una conexión de red.

Use medios independientes en los siguientes escenarios de implementación de sistema operativo:  

- [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

- [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>Uso

Los medios independientes incluyen la secuencia de tareas que automatiza los pasos para instalar el sistema operativo, además de otros contenidos necesarios Este contenido incluye la imagen de arranque, la imagen del sistema operativo y los controladores de dispositivos. Dado que los medios independientes contienen todo lo necesario para implementar el sistema operativo, requieren más espacio en disco que otros tipos de medios.

Al crear un medio independiente en un sitio de administración central, el cliente recupera su código de sitio asignado de Active Directory. Los medios independientes que se crean en los sitios secundarios asignan automáticamente al cliente el código de sitio para dicho sitio.  


## <a name="prerequisites"></a>Requisitos previos

Antes de crear medios independientes con el Asistente para crear medio de secuencia de tareas, asegúrese de que se cumplen las condiciones siguientes:

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creación de una secuencia de tareas para implementar un sistema operativo

Como parte de los medios independientes, debe especificar la secuencia de tareas para implementar un sistema operativo. Para más información, consulte [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Acciones no compatibles con medios independientes

No se admiten las siguientes acciones en medios independientes:

- El paso [Aplicar controladores automáticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) en la secuencia de tareas. Los medios independientes no admiten la aplicación automática de controladores de dispositivos desde el catálogo de controladores. Use el paso [Aplicar paquete de controladores](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) para que un conjunto especificado de controladores esté disponible en el programa de instalación de Windows.  

- El paso [Descargar contenido de paquete](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) de la secuencia de tareas. La información del punto de administración no está disponible en medios independientes, por lo que se producirá un error en el paso al intentar enumerar las ubicaciones de contenido.  

- Instalación de actualizaciones de software.  

- Instalación de software antes de implementar el sistema operativo.  

- Secuencias de tareas personalizadas para implementaciones sin sistema operativo.  

- Asociación de usuarios con el equipo de destino para admitir la afinidad de dispositivo de usuario.  

- El paquete dinámico se instala a través del paso [Instalar paquetes](../understand/task-sequence-steps.md#BKMK_InstallPackage).  

- La aplicación dinámica se instala a través del paso [Instalar aplicación](../understand/task-sequence-steps.md#BKMK_InstallApplication).

- La opción **Usar paquete de cliente de preproducción cuando esté disponible** del paso de secuencia de tareas **Instalar Windows y Configuration Manager**. Para obtener más información sobre esta configuración, consulte [Instalar Windows y Configuration Manager](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> Podría producirse un error si la secuencia de tareas incluye el paso [Instalar paquete](../understand/task-sequence-steps.md#BKMK_InstallPackage) y usted crea los medios independientes en un sitio de administración central. El sitio de administración central no tiene las directivas de configuración de cliente necesarias. Estas directivas son necesarias para habilitar al agente de distribución de software durante la ejecución de la secuencia de tareas. Es probable que aparezca el siguiente error en el archivo **CreateTsMedia.log**:  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> Para los medios independientes que incluyan un paso **Instalar paquete**, cree los medios independientes en un sitio primario que tenga habilitado el agente de distribución de software.
>
> También puede usar un paso [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) personalizado. Agréguelo después del paso [Instalar Windows y Configuration Manager](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) y antes del primer paso **Instalar paquete**. El paso **Ejecutar línea de comandos** ejecuta el siguiente comando de WMIC para habilitar el agente de distribución de software antes del primer paso Instalar paquete:  
>
> `WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo el contenido asociado con la secuencia de tareas

Distribuya todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Este contenido incluye la imagen de arranque, la imagen de sistema operativo y otros archivos asociados. El asistente recopila la información del punto de distribución al crear los medios.

Su cuenta de usuario necesita al menos acceso de **Lectura** a la biblioteca de contenido en ese punto de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar la unidad USB extraíble

Si usa una unidad USB extraíble, conéctela al equipo donde se ejecuta el Asistente para crear medio de secuencia de tareas. Windows debe identificar la unidad USB como un dispositivo extraíble. El asistente escribe directamente en la unidad extraíble cuando crea los medios.

Los medios independientes utilizan un sistema de archivos FAT32. No se pueden crear medios independientes en una unidad USB extraíble cuyo contenido incluya un archivo de más de 4 GB de tamaño.

### <a name="create-an-output-folder"></a>Crear una carpeta de salida

Antes de ejecutar el Asistente para crear medio de secuencia de tareas para crear medios para un conjunto de CD o DVD, cree una carpeta para los archivos de salida que se crean. Los medios que se crean para un conjunto de CD o DVD se escriben como un archivo .ISO directamente en la carpeta.


## <a name="process"></a>Proceso

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione el nodo **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear medio de secuencia de tareas**. Esta acción inicia el Asistente para crear medio de secuencia de tareas.  

3. En la página **Seleccionar tipo de medio**, especifique las siguientes opciones:  

    - Seleccione **Medio independiente**.  

    - Opcionalmente, si quiere permitir solo que el sistema operativo se implemente sin requerir intervención del usuario, seleccione **Permitir la implementación desatendida de sistema operativo**.  

        > [!IMPORTANT]  
        > Cuando se selecciona esta opción, no se solicita al usuario que proporcione información de configuración de red ni que realice secuencias de tareas opcionales. Si se configura el medio para la protección con contraseña, se seguirá solicitando una contraseña al usuario.  

4. En la página **Tipo de medios**, especifique si el medio es una **unidad USB extraíble** o un **conjunto de CD/DVD**. Luego, configure las siguientes opciones:  

    > [!IMPORTANT]  
    > Los medios usan un sistema de archivos FAT32. No puede crear medios en una unidad USB cuyo contenido incluya un archivo de más de 4 GB de tamaño.  

    - Si selecciona **Unidad USB extraíble**, especifique dónde quiere almacenar el contenido.  

        - **Formatear la unidad USB extraíble (FAT32) y hacerla de arranque** : de forma predeterminada, permita que Configuration Manager prepare la unidad USB. Muchos de los nuevos dispositivos UEFI requieren una partición FAT32 de arranque. Sin embargo, este formato también limita el tamaño de los archivos y la capacidad total de la unidad. Si ya ha formateado y configurado la unidad extraíble, deshabilite esta opción.

    - Si selecciona **Conjunto de CD/DVD**, especifique la capacidad del medio (**Tamaño de medio**) y el nombre y la ruta de acceso del archivo de salida (**Archivo multimedia**). El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: `\\servername\folder\outputfile.iso`  

        Si la capacidad del medio es demasiado pequeña para almacenar todo el contenido, crea varios archivos. A continuación, deberá almacenar el contenido en varios CD o DVD. Si se requieren varios archivos multimedia, Configuration Manager agrega un número de secuencia al nombre de cada archivo de salida que crea.  

        Si implementa una aplicación junto con el sistema operativo y la aplicación no cabe en un solo medio, Configuration Manager almacena la aplicación en varios medios. Cuando se ejecuta el medio independiente, Configuration Manager pide al usuario el siguiente medio en el que se almacena la aplicación.  

        > [!IMPORTANT]  
        > Si selecciona una imagen .iso existente, el Asistente para crear medio de secuencia de tareas elimina la imagen de la unidad o el recurso compartido cuando pasa a la siguiente página del asistente. Se elimina la imagen existente incluso si, a continuación, se cancela al asistente.  

    - **Carpeta de almacenamiento provisional**:<!--1359388-->: el proceso de creación de medios puede requerir una gran cantidad de espacio en disco temporal. De forma predeterminada, esta ubicación es similar a la siguiente ruta de acceso: `%UserProfile%\AppData\Local\Temp`. A partir de la versión 1902, para ofrecer mayor flexibilidad con respecto al almacenamiento de estos archivos temporales, cambie este valor a otra unidad y ruta de acceso.  

    - **Etiqueta de medio**:<!--1359388-->: a partir de la versión 1902, agregue una etiqueta al medio de secuencia de tareas. Esta etiqueta ayuda a identificar mejor el medio después de crearlo. El valor predeterminado es `Configuration Manager`. Este campo de texto aparece en las siguientes ubicaciones:  

        - Si monta un archivo ISO, Windows muestra esta etiqueta como el nombre de la unidad montada  

        - Si aplica formato a una unidad USB, usa los primeros 11 caracteres de la etiqueta como nombre  

        - Configuration Manager escribe un archivo de texto denominado `MediaLabel.txt` en la raíz del medio. De forma predeterminada, el archivo incluye una sola línea de texto: `label=Configuration Manager`. Si personaliza la etiqueta del medio, esta línea usa la etiqueta personalizada en lugar del valor predeterminado.  

    - **Incluir archivo autorun.inf en el medio**:<!-- 4090666 -->: a partir de la versión 1906, Configuration Manager no agrega un archivo autorun.inf de forma predeterminada. Normalmente, los productos antimalware bloquean este archivo. Para obtener más información sobre la característica de ejecución automática de Windows, vea [Creating an AutoRun-enabled CD-ROM Application](/windows/desktop/shell/autoplay) (Creación de una aplicación de CD-ROM con ejecución automática habilitada). Si todavía lo necesita en su escenario, seleccione esta opción para incluir el archivo.  

5. En la página **Seguridad**, especifique las siguientes opciones:

    - **Proteger medio con contraseña:** : escriba una contraseña segura para ayudar a proteger el medio frente al acceso no autorizado. Al especificar una contraseña, el usuario debe proporcionar dicha contraseña para poder usar el medio.  

        > [!IMPORTANT]  
        > Por seguridad, asigne siempre una contraseña para ayudar a proteger el medio.  
        >
        > En un medio independiente, solo se cifran los pasos de la secuencia de tareas y sus variables. No se cifra el contenido restante del medio. No incluya información confidencial en los scripts de la secuencia de tareas. Almacene e implemente la información confidencial mediante el uso de variables de secuencia de tareas.  

    - **Seleccionar el intervalo de fechas de validez de este medio independiente**: establezca fechas de inicio y expiración opcionales en los medios. Esta configuración está deshabilitada de manera predeterminada. Las fechas se comparan con la hora del sistema del equipo antes de que se ejecuten los medios independientes. Cuando la hora del sistema es anterior a la hora de inicio o posterior a la hora de expiración, los medios independientes no se inician. Estas opciones también están disponibles mediante el cmdlet de PowerShell [New-CMStandaloneMedia](/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps).  

6. En la página **CD/DVD independiente**, seleccione la secuencia de tareas que implementa el sistema operativo. Solo se pueden seleccionar esas secuencias de tareas que están asociadas con una imagen de arranque. Compruebe la lista de contenido al que hace referencia la secuencia de tareas.  

    - **Detectar dependencias de aplicación asociadas y agregarlas a este medio**: también agrega contenido a los medios para las dependencias de la aplicación.  

        > [!TIP]  
        > Si no ve las dependencias de aplicación esperadas, anule la selección y, a continuación, vuelva a seleccionar esta opción para actualizar la lista.  

7. En la página **Seleccionar aplicación**, especifique contenido adicional de la aplicación que se incluirá como parte del archivo multimedia.  

8. En la página **Seleccionar paquete**, especifique contenido adicional del paquete que se incluirá como parte del archivo multimedia.  

9. En la página **Seleccionar paquete de controladores**, especifique contenido adicional del paquete de controladores que se incluirá como parte del archivo multimedia.  

10. En la página **Puntos de distribución**, especifique los puntos que contienen el contenido necesario.  

    Configuration Manager solo muestra los puntos de distribución que incluyen el contenido. Antes de continuar, distribuya todo el contenido asociado a la secuencia de tareas en al menos un punto de distribución. Después de distribuir el contenido, actualice la lista de puntos de distribución. Quite los puntos de distribución ya haya seleccionado en esta página, vaya a la página anterior y después regrese a la página **Puntos de distribución**. O bien, reinicie al asistente. Para obtener más información, consulte [Distribuir contenido al que hace referencia una secuencia de tareas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) y [Administración del contenido y de la infraestructura de contenido](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

11. En la página **Personalización**, especifique las siguientes opciones:  

    - Agregue las variables que usa la secuencia de tareas.  

    - **Habilitar comando de preinicio**: Especifique los comandos de preinicio que desee ejecutar antes de que se ejecute la secuencia de tareas. Los comandos de preinicio son un script o un ejecutable que puede interactuar con el usuario en Windows PE antes de que se ejecute la secuencia de tareas. Para obtener más información, consulte [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas).  

        > [!TIP]  
        > Durante la creación de medios, la secuencia de tareas escribe el identificador de paquete y el comando de preinicio, incluidos los valores de las variables de secuencia de tareas, en el archivo de registro **CreateTSMedia.log** en el equipo que ejecuta la consola de Configuration Manager. Puede revisar este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

        Si el comando de preinicio necesita contenido, seleccione la opción **Incluir archivos para el comando de preinicio**.  

12. Complete el asistente.  

Los archivos de medios independientes (.iso) se crean en la carpeta de destino. Si seleccionó **Conjunto de CD/DVD**, copie los archivos de salida en un conjunto de CD o DVD.


## <a name="next-steps"></a>Pasos siguientes

[Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md) (Uso de medios independientes para implementar Windows sin usar la red)
