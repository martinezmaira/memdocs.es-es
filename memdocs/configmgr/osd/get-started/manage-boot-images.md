---
title: Administrar imágenes de arranque
titleSuffix: Configuration Manager
description: En Configuration Manager, aprenda a administrar las imágenes de arranque de Windows PE que se usan durante una implementación de sistema operativo.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 74b8b0f29172140a19c402c79b7ea9b7339cf3e5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697643"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Administración de imágenes de arranque con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Una imagen de arranque de Configuration Manager es una imagen de [Windows PE](/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) que se usa durante la implementación de un sistema operativo. Las imágenes de arranque se usan para iniciar un equipo en WinPE. Este sistema operativo mínimo contiene servicios y componentes limitados. Configuration Manager usa WinPE para preparar el equipo de destino para la instalación de Windows.

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a> Imágenes de arranque predeterminadas

Configuration Manager proporciona dos imágenes de arranque predeterminadas: Una para plataformas x86 y otra para plataformas x64. Estas imágenes se almacenan en las carpetas *x64* o *i386* del siguiente recurso compartido de archivos en el servidor de sitio: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\`. Las imágenes de arranque predeterminadas se actualizan o se vuelven a generar según la acción que realice.

Tenga en cuenta los comportamientos siguientes de cualquiera de las acciones descritas para las imágenes de arranque predeterminadas:

- Los objetos de controlador de origen deben ser válidos. Estos objetos incluyen los archivos de origen del controlador. Si los objetos no son válidos, el sitio no agrega los controladores a las imágenes de arranque.  

- No se modifican las imágenes de arranque que no estén basadas en las imágenes de arranque predeterminadas, incluso si usan la misma versión de Windows PE.  

- Vuelva a distribuir las imágenes de arranque modificadas en los puntos de distribución.  

- Vuelva a crear los medios que usen las imágenes de arranque modificadas.  

- Si no quiere que las imágenes de arranque predeterminadas o personalizadas se actualicen automáticamente, no las almacene en la ubicación predeterminada.  

> [!NOTE]
> La herramienta de registro de Configuration Manager (**CMTrace**) se agrega a todas las imágenes de arranque en la **Biblioteca de software**. Cuando esté en Windows PE, inicie la herramienta escribiendo `cmtrace` desde el símbolo del sistema.
>
> CMTrace es el visor predeterminado para los archivos de registro de Windows PE.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Uso de las actualizaciones y el mantenimiento para instalar la última versión de Configuration Manager

Al actualizar la versión de Windows Assessment and Deployment Kit (ADK), y después usar las actualizaciones para instalar la última versión de Configuration Manager, el sitio regenera las imágenes de arranque predeterminadas. Esta actualización incluye la nueva versión de WinPE de Windows ADK actualizado y la versión nueva del cliente de Configuration Manager, los controladores y las personalizaciones. El sitio no modifica las imágenes de arranque personalizadas.

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Actualización desde Configuration Manager 2012 a la rama actual

Al actualizar Configuration Manager 2012 a la rama actual, el sitio regenera las imágenes de arranque predeterminadas. Esta actualización incluye la versión nueva de WinPE de Windows ADK actualizado y la versión nueva del cliente de Configuration Manager. Todas las personalizaciones de imagen de arranque permanecen sin cambios. El sitio no modifica las imágenes de arranque personalizadas.

### <a name="update-distribution-points-with-the-boot-image"></a>Actualización de puntos de distribución con la imagen

Cuando se usa la acción **Actualizar puntos de distribución** del nodo **Imágenes de arranque** en la consola, el sitio actualiza la imagen de arranque de destino con los componentes de cliente, los controladores y las personalizaciones.

Puede volver a cargar la imagen de arranque con la versión más reciente de WinPE desde el directorio de instalación de Windows ADK. En la página **General** del Asistente para actualizar puntos de distribución se proporciona la información siguiente:

- La versión actual de Windows ADK instalada en el servidor de sitio
- La versión actual del cliente de producción
- La versión de Windows ADK de WinPE en la imagen de arranque.
- La versión del cliente de Configuration Manager en la imagen de arranque

Si las versiones de la imagen de arranque no están actualizadas, use la opción de **Volver a cargar esta imagen de arranque con la versión de Windows PE actual desde Windows ADK**.

> [!Important]  
> Esta acción está disponible para las imágenes de arranque personalizada y predeterminada. Durante este proceso para volver a cargar la imagen de arranque, el sitio no conserva las personalizaciones manuales realizadas fuera de Configuration Manager. Estas personalizaciones incluyen las extensiones de terceros. Esta opción vuelve a generar la imagen de arranque con la versión más reciente de WinPE y la versión más reciente del cliente. Solo las configuraciones que especifique en las propiedades de la imagen de arranque se vuelven a aplicar. <!--SCCMDocs issue #1283-->

En el nodo **Imágenes de arranque** también se incluye una columna nueva para (**Versión del cliente**). Use esta columna para ver rápidamente la versión del cliente de Configuration Manager en cada imagen de arranque.

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a> Personalización de una imagen de arranque  

Cuando una imagen de arranque se basa en una versión de WinPE desde la versión admitida de Windows ADK, puede personalizar o [modificar una imagen de arranque](#BKMK_ModifyBootImages), desde la consola. Al actualizar un sitio e instalar una nueva versión de Windows ADK, las imágenes de arranque personalizadas no se actualizan con la nueva versión de Windows ADK. Si esto ocurre, no podrá personalizar las imágenes de arranque en la consola de Configuration Manager. Pero continuarán funcionando como lo hacían antes de la actualización.  

Si una imagen de arranque se basa en otra versión de Windows ADK instalada en un sitio, debe personalizar las imágenes de arranque. Use otro método para personalizar estas imágenes de arranque, como la herramienta de línea de comandos Administración y mantenimiento de imágenes de implementación (DISM). DISM forma parte de Windows ADK. Para obtener más información, consulte [Customize boot images](customize-boot-images.md) (Personalización de imágenes de arranque).  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a> Incorporación de una imagen de arranque  

Durante la instalación de sitio, Configuration Manager agrega automáticamente imágenes de arranque basadas en una versión de WinPE desde la versión admitida de Windows ADK. Según la versión de Configuration Manager, puede agregar imágenes de arranque basadas en una versión de WinPE desde la versión admitida de Windows ADK. Se produce un error al intentar agregar una imagen de arranque que contiene una versión no admitida de WinPE. En la lista siguiente se muestran las versiones de Windows ADK y WinPE que se admiten actualmente:

- Versión de Windows ADK: Windows ADK para Windows 10

- Versiones de Windows PE para imágenes de arranque personalizables desde la consola de Configuration Manager: Windows PE 10

- Versiones admitidas de Windows PE para imágenes de arranque *que no se pueden personalizar* desde la consola de Configuration Manager

  - Windows PE3.1<sup>[Nota 1](#bkmk_note1)</sup>

  - Windows PE 5

Por ejemplo, use la consola de Configuration Manager para personalizar las imágenes de arranque basadas en Windows PE 10 desde Windows ADK para Windows 10. Para una imagen de arranque basada en Windows PE 5, personalícela desde otro equipo con la versión de DISM de Windows ADK para Windows 8. Después, agregue la imagen de arranque personalizada a la consola de Configuration Manager. Vea los siguientes artículos para más información:

- [Personalizar imágenes de arranque](customize-boot-images.md)
- [Compatibilidad con Windows 10 ADK](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [Plataformas compatibles de DISM](/windows-hardware/manufacture/desktop/dism-supported-platforms)

<a name="bkmk_note1"></a>

> [!NOTE]
> **Nota 1: Compatibilidad con Windows PE 3.1**
>
> Solo se puede agregar una imagen de arranque a Configuration Manager si se basa en Windows PE *versión 3.1*. Actualice el AIK de Windows para Windows 7 (basado en Windows PE 3.0) con el complemento de AIK de Windows para Windows 7 SP1 (basado en Windows PE 3.1). Descargue el complemento de AIK de Windows para Windows 7 SP1 en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Imágenes de arranque**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Agregar imagen de arranque**. Esta acción inicia el Asistente para agregar una imagen de arranque.  

3. En la página **Origen de datos**, especifique las siguientes opciones:  

    - En el cuadro **Ruta de acceso** , especifique la ruta de acceso del archivo WIM de imagen de arranque. La ruta de acceso especificada debe ser una ruta de acceso de red válida con el formato UNC. Por ejemplo: `\\ServerName\ShareName\BootImageName.wim`

    - Seleccione la imagen de arranque de la lista desplegable **Imagen de arranque** . Si el archivo WIM contiene varias imágenes de arranque, seleccione la imagen apropiada.  

4. En la página **General**, especifique las siguientes opciones:  

    - En el cuadro **Nombre** , especifique un nombre único para la imagen de arranque.  

    - En el cuadro **Versión** , especifique un número de versión para la imagen de arranque.  

    - En el cuadro **Comentario**, especifique una descripción breve sobre cómo utiliza la imagen de arranque.  

5. Complete el asistente.  

La imagen de arranque aparece ahora en el nodo **Imagen de arranque**. Antes de usar la imagen de arranque para implementar un sistema operativo, distribúyala a los puntos de distribución.

> [!Tip]  
> En el nodo **Imagen de arranque** de la consola, en la columna **Tamaño (KB)** se muestra el tamaño descomprimido de cada imagen de arranque. Cuando el sitio envía una imagen de arranque a través de la red, envía una copia comprimida. Esta copia normalmente es más pequeña que el tamaño que se muestra en la columna **Tamaño (KB)** .  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a> Distribuir imágenes de arranque  

Las imágenes de arranque se distribuyen a los puntos de distribución de la misma forma en que se reparte otro tipo de contenido. Antes de implementar un sistema operativo o crear medios, distribuya la imagen de arranque al menos a un punto de distribución.

Para conocer los pasos de distribución de una imagen de arranque, consulte [Distribuir contenido](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

Para usar PXE para implementar un sistema operativo, considere los aspectos siguientes antes de distribuir la imagen de arranque:  

- Configure el punto de distribución para aceptar solicitudes PXE.  
- Distribuya una imagen de arranque x86 y x64 habilitada para PXE a un punto de distribución habilitado para PXE como mínimo.  
- Configuration Manager distribuye las imágenes de arranque a la carpeta **RemoteInstall** en el punto de distribución habilitado para PXE.  
  
Para obtener más información sobre el uso de PXE para implementar sistemas operativos, consulte [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a> Modificación de una imagen de arranque  

Agregue o quite controladores de dispositivo para la imagen, o edite las propiedades de la imagen de arranque. Los controladores que agregue o quite pueden incluir controladores de red o almacenamiento. Tenga en cuenta los siguientes factores al modificar imágenes de arranque:  

- Antes de agregar controladores a la imagen de arranque, impórtelos y habilítelos en el catálogo de controladores de dispositivo.  

- Al modificar una imagen de arranque, dicha imagen no cambia ninguno de los paquetes asociados a los que hace referencia.  

- Después de realizar cambios en una imagen de arranque, **actualícela** en los puntos de distribución que ya la tienen. Este proceso hace que la versión más reciente de la imagen de arranque esté disponible para los clientes. Para obtener más información, vea [Administrar el contenido distribuido](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="modify-the-properties-of-a-boot-image"></a>Modificación de las propiedades de una imagen de arranque  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Imágenes de arranque**.  

2. Seleccione la imagen de arranque que desee modificar.  

3. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.  

4. Defina cualquiera de las siguientes opciones para cambiar el comportamiento de la imagen de arranque:  

#### <a name="images"></a>Imágenes

En la pestaña **Imágenes**, si cambia las propiedades de la imagen de arranque mediante una herramienta externa, seleccione **Recargar**.  

#### <a name="drivers"></a>Controladores

En la pestaña **Controladores**, agregue los controladores de dispositivo de Windows que WinPE necesita para arrancar. Tenga en cuenta los aspectos siguientes cuando agregue controladores de dispositivo:  

- Asegúrese de que los controladores que se agregan a la imagen de arranque coinciden con la arquitectura de la imagen de arranque.  

- Para mostrar solo los controladores para la arquitectura de la imagen de arranque, seleccione **Ocultar controladores que no coincidan con la arquitectura de la imagen de arranque**. La arquitectura del controlador se basa en la arquitectura que se indica en el archivo INF del fabricante.  

- WinPE ya viene con muchos controladores integrados. Agregue solo los controladores de almacenamiento y de red que no estén incluidos en WinPE.  

- Agregue solo controladores de red y almacenamiento a la imagen de arranque, a menos que existan requisitos para otros controladores en WinPE.  

- Para mostrar solo los controladores de almacenamiento y de red, seleccione **Ocultar los controladores que no sean de almacenamiento o red (para imágenes de arranque)** . Esta opción también oculta otros controladores que no suelen ser necesarios para las imágenes de arranque, como un controlador de vídeo o de módem.  

- Para ocultar los controladores que no tengan una firma digital válida, seleccione **Ocultar los controladores que no estén firmados digitalmente**.  

> [!NOTE]  
> Importe los controladores de dispositivos en el catálogo de controladores antes de agregarlos a una imagen de arranque. Para más información sobre cómo importar controladores de dispositivo, consulte [Manage drivers](manage-drivers.md) (Administración de controladores).  

#### <a name="customization"></a>Personalización

En la pestaña **Personalización** , seleccione cualquiera de las siguientes opciones:  

- Seleccione la opción **Habilitar comando de preinicio** para especificar que se ejecute un comando antes de que se ejecute la secuencia de tareas. Cuando habilite esta opción, especifique también la línea de comandos que se va a ejecutar y los archivos de compatibilidad requeridos por el comando.  

    > [!WARNING]  
    > Agregue `cmd /c` al principio de la línea de comandos. Si no se especifica `cmd /c`, el comando no se cierra después de ejecutarse. La implementación sigue a la espera de que finalice el comando y no se iniciará ningún otro comando o acción que se hayan configurado.  

    > [!TIP]  
    > Durante la creación de los medios de secuencia de tareas, el asistente escribe el identificador de paquete y la línea de comandos de preinicio en el archivo **CreateTSMedia.log**. Esta información incluye el valor de las variables de secuencia de tareas. Este registro se encuentra en el equipo que ejecuta la consola de Configuration Manager. Revise este archivo de registro para comprobar los valores de las variables de secuencia de tareas.  

- Defina los valores de **Fondo de Windows PE** para especificar si quiere usar el fondo predeterminado de WinPE o un fondo personalizado.  

- Configure el **espacio de desecho de Windows PE(MB)** , que es el almacenamiento temporal (unidad RAM) usado por WinPE. Por ejemplo, cuando se ejecuta una aplicación en WinPE y necesita escribir archivos temporales, WinPE redirige los archivos al espacio de desecho en la memoria para simular la presencia de un disco duro. De forma predeterminada, esta cantidad es de 512 MB para los dispositivos con más de 1 GB de RAM, en caso contrario, el valor predeterminado es 32 MB.  

- Seleccione **Habilitar compatibilidad de comando (solo prueba)** para abrir un símbolo del sistema mediante la tecla **F8** mientras se implementa la imagen de arranque. Esta opción es útil para solucionar problemas mientras se prueba la implementación. No se recomienda el uso de esta configuración en una implementación de producción por motivos de seguridad.  

- **Establecer la distribución del teclado predeterminada en WinPE**: <!--4910348-->A partir de la versión 1910, configure la distribución del teclado predeterminada para una imagen de arranque. Si selecciona un idioma distinto de es-es, Configuration Manager sigue incluyéndolo en las configuraciones regionales disponibles. En el dispositivo, el diseño de teclado inicial es la configuración regional seleccionada, pero el usuario puede cambiar el dispositivo a es-es si es necesario.

> [!Tip]
> Use el cmdlet [Set-CMBootImage](/powershell/module/configurationmanager/set-cmbootimage?view=sccm-ps) de PowerShell para configurar estas opciones desde un script.

#### <a name="optional-components"></a>Componentes opcionales

En la pestaña **Componentes opcionales**, especifique los componentes agregados a Windows PE para su uso con Configuration Manager. Para obtener más información sobre los componentes opcionales, vea [WinPE: agregar paquetes (referencia de los componentes opcionales)](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Los siguientes componentes son necesarios para Configuration Manager y siempre se agregan a las imágenes de arranque:

- Scripting (WinPE-Scripting)
- Startup (WinPE-SecureStartup)
- Network (WinPE-WDS-Tools)
- Scripting (WinPE-WMI)

La lista **Componentes** muestra los elementos adicionales que se agregan a esta imagen de arranque. Para agregar más componentes, seleccione el asterisco dorado. Para quitar un componente, selecciónelo en la lista y, a continuación, seleccione la X roja.

Los clientes usan habitualmente los siguientes componentes:

- Microsoft .NET (WinPE-NetFX): Este componente es un requisito previo para PowerShell. Es uno de los componentes opcionales de mayor tamaño.  
- Windows PowerShell (WinPE-PowerShell): Este componente requiere .NET y agrega compatibilidad limitada con PowerShell. Si ejecuta scripts de PowerShell personalizados durante la fase de WinPE de la secuencia de tareas, agregue este componente. Hay otros componentes que pueden ser necesarios para otros cmdlets de PowerShell.
- HTML (WinPE-HTA): Si ejecuta aplicaciones HTML personalizadas durante la fase de WinPE de la secuencia de tareas, agregue este componente.

Para obtener más información acerca de cómo agregar idiomas, consulte [Configurar varios idiomas ](#BKMK_BootImageLanguage).

#### <a name="data-source"></a>origen de datos

En la pestaña **Origen de datos** , actualice cualquiera de las siguientes opciones:  

- Para cambiar el archivo de origen de la imagen de arranque, establezca **Ruta de acceso de la imagen** e **Índice de imágenes**.  

- Para crear una programación para cuando el sitio actualice la imagen de arranque, seleccione **Actualizar puntos de distribución en una programación**.  

- Si no quiere que el contenido de este paquete deje la caché de cliente para hacer sitio a otro contenido, seleccione **Conservar contenido en caché de cliente**.  

- Para especificar que el sitio solo distribuya los archivos cambiados cuando actualice el paquete de imagen de arranque en el punto de distribución, seleccione **Habilitar replicación diferencial binaria** (BDR). Esta configuración minimiza el tráfico de red entre sitios. La BDR es especialmente útil cuando el paquete de imagen de arranque es grande y los cambios son relativamente pequeños.  

- Si la imagen de arranque se usa en una implementación habilitada para PXE, seleccione **Implementar esta imagen de arranque desde el punto de distribución habilitado con PXE**. Para más información, vea [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).  

#### <a name="data-access"></a>Acceso a datos

En la pestaña **Acceso a datos**, puede establecer la configuración del recurso compartido de paquete. Si es necesario en su entorno, establezca la opción en **Copiar el contenido de este paquete en un recurso compartido de paquete en los puntos de distribución**. A continuación, tiene la opción adicional de **usar un nombre personalizado para el recurso compartido de paquete** y especificar el **nombre del recurso compartido** personalizado. Se requiere espacio en disco adicional en los puntos de distribución si se habilita esta opción. Se aplica a todos los puntos de distribución que reciben esta imagen de arranque.

#### <a name="distribution-settings"></a>Configuración de distribución

En la pestaña **Configuración de distribución** , seleccione cualquiera de las siguientes opciones:  

- En la lista **Prioridad de distribución**, especifique el nivel de prioridad. Configuration Manager usa esta lista de prioridad cuando el sitio distribuye varios paquetes en el mismo punto de distribución.  

- Si quiere habilitar la distribución de contenido a petición en puntos de distribución preferidos, seleccione **Habilitar para distribución a petición**. Cuando se habilita esta opción, si un cliente solicita el contenido del paquete y el contenido no está disponible en ningún punto de distribución, el punto de administración distribuye el contenido. Para obtener más información, vea [Distribución de contenido a petición](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

- Para especificar cómo quiere que el sitio distribuya la imagen de arranque en los puntos de distribución habilitados para el contenido preconfigurado, establezca la **Configuración de punto de distribución preconfigurado**. Para más información sobre el contenido preconfigurado, consulte [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) (Preconfigurar el contenido).  

#### <a name="content-locations"></a>Ubicaciones de contenido

En la pestaña **Ubicaciones de contenido**, seleccione el punto de distribución o el grupo de puntos de distribución y use las siguientes acciones:  

- **Validar**: Compruebe la integridad del paquete de imagen de arranque en el punto de distribución o el grupo de puntos de distribución seleccionado.  

- **Redistribuir**: Distribuya de nuevo la imagen de arranque en el punto de distribución o el grupo de puntos de distribución seleccionado.  

- **Quitar**: Elimine la imagen de arranque del punto de distribución o el grupo de puntos de distribución seleccionado.  

#### <a name="security"></a>Seguridad

En la pestaña **Seguridad**, vea los usuarios administrativos que tienen permisos para este objeto.

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a> Configurar una imagen de arranque de PXE  

Para poder usar una imagen de arranque para una implementación basada en PXE, configure la imagen de arranque para que se implemente desde un punto de distribución habilitado con PXE.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Imágenes de arranque**.  

2. Seleccione la imagen de arranque que desee modificar.  

3. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.  

4. En la pestaña **Origen de datos** , seleccione **Implementar esta imagen de arranque desde el punto de distribución habilitado con PXE**. Para más información, vea [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a> Configurar varios idiomas

> [!TIP]
> A partir de la versión 1910, configure la distribución de teclado predeterminada en las propiedades de una imagen de arranque. Para obtener más información, vea [Personalización](#customization).<!--4910348-->

Las imágenes de arranque son independientes del idioma. Esta funcionalidad permite usar una imagen de arranque para mostrar el texto de la secuencia de tareas en varios idiomas en WinPE. Incluya la compatibilidad de idioma adecuada de la pestaña **Componentes opcionales** de la imagen de arranque. Después, establezca la variable de secuencia de tareas correspondiente para indicar el idioma que se va a mostrar. El idioma del sistema operativo implementado es independiente del idioma de WinPE. El idioma que WinPE muestra al usuario se determina de la manera siguiente:  

- Cuando un usuario ejecuta la secuencia de tareas desde un sistema operativo existente, Configuration Manager utiliza automáticamente el idioma configurado para el usuario. Cuando la secuencia de tareas se ejecuta automáticamente como resultado de una fecha límite de implementación obligatoria, Configuration Manager utiliza el idioma del sistema operativo.  

- Para las implementaciones de sistema operativo que usan PXE o medios, establezca el valor del identificador de idioma en la variable **SMSTSLanguageFolder** como parte de un comando de preinicio. Cuando el equipo arranca WinPE, los mensajes se muestran en el idioma que especificó en la variable. Si se produce un error al tener acceso al archivo de recursos de idioma en la carpeta especificada, o bien no se establece la variable, WinPE muestra los mensajes en el idioma predeterminado.  

    > [!NOTE]  
    > Si protege el medio con una contraseña, el texto que solicita la contraseña al usuario siempre se muestra en el idioma de WinPE.  

Use el procedimiento siguiente para establecer el idioma de WinPE de las implementaciones de sistema operativo iniciadas por un medio o por PXE.  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Establecimiento del idioma de Windows PE de una implementación de sistema operativo iniciada por un medio o por PXE  

1. Compruebe que el archivo de recursos de secuencia de tareas correcto (tsres.dll) se encuentra en la carpeta de idioma correspondiente en el servidor de sitio antes de actualizar la imagen de arranque. Por ejemplo, el archivo de recursos del idioma inglés se encuentra en la siguiente ubicación: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Como parte de su comando de preinicio, configure la variable de entorno **SMSTSLanguageFolder** con el identificador de idioma correspondiente. El identificador de idioma no debe especificarse con un formato hexadecimal sino mediante el formato decimal. Por ejemplo, para establecer el Id. de idioma en inglés, especifique el valor decimal **1033**, no el valor hexadecimal 00000409 del nombre de carpeta.