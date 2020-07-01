---
title: Creación de una secuencia de tareas de actualización de SO
titleSuffix: Configuration Manager
description: Use una secuencia de tareas para actualizar automáticamente de Windows 7 o una versión posterior a Windows 10
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ad36978f3f3dc5207068a65d76bf8f5c7c3078c
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383247"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Crear una secuencia de tareas para actualizar un SO en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use secuencias de tareas en Configuration Manager para actualizar automáticamente un SO en un equipo de destino. Esta actualización puede ser desde Windows 7 o una versión posterior a Windows 10, o desde Windows Server 2012 o posterior a Windows Server 2016. Cree una secuencia de tareas que haga referencia al paquete de actualización de sistema operativo y cualquier otro contenido para instalar, como aplicaciones o actualizaciones de software. La secuencia de tareas para actualizar un SO es parte del escenario de [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md).  


## <a name="prerequisites"></a>Requisitos previos

Antes de crear la secuencia de tareas, se deben aplicar los requisitos siguientes:

### <a name="required"></a>Requerido

- El [paquete de actualización del SO](../get-started/manage-operating-system-upgrade-packages.md) debe estar disponible en la consola de Configuration Manager.  

- Al actualizar a Windows Server 2016, seleccione la opción **Omitir cualquier mensaje de compatibilidad descartable** en el paso de secuencia de tareas Actualizar sistema operativo. En caso contrario, se produce un error en la actualización.  

### <a name="required-if-used"></a>Necesario (si se usa)  

- Las [actualizaciones de software](../../sum/get-started/synchronize-software-updates.md) deben estar sincronizadas en la consola de Configuration Manager.  

- Las [aplicaciones](../../apps/deploy-use/create-applications.md) deben agregarse a la consola de Configuration Manager.  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a> Crear una secuencia de tareas para actualizar un sistema operativo  

Para actualizar el sistema operativo en los clientes, puede crear una secuencia de tareas y seleccionar **Actualizar un sistema operativo desde el paquete de actualización** en el Asistente para crear secuencia de tareas. El asistente agrega los pasos de secuencia de tareas para actualizar el sistema operativo, aplica actualizaciones de software e instala aplicaciones.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear secuencia de tareas**.  

3. En la página **Crear nueva secuencia de tareas** del Asistente para creación de secuencia de tareas, seleccione **Actualizar un sistema operativo desde un paquete de actualización** y luego elija **Siguiente**.  

4. En la página **Información de secuencia de tareas**, especifique la siguiente configuración:  

    - **Nombre de la secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

    - **Descripción**: de manera opcional, especifique una descripción.  

5. En la página **Actualizar el sistema operativo de Windows**, especifique la siguiente configuración:  

    - **Paquete de actualización**: especifique el paquete de actualización que contenga los archivos de origen de actualización del sistema operativo. Compruebe que ha seleccionado el paquete de actualización correcto examinando la información del panel **Propiedades**. Para más información, vea [Administrar paquetes de actualización de sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

    - **Índice de ediciones**: si hay varios índices de edición del sistema operativo disponibles en el paquete, seleccione el índice de la edición deseada. De forma predeterminada, el asistente selecciona el primer índice.  

    - **Clave de producto**: especifique la clave de producto de Windows para el sistema operativo que quiera instalar. Puede especificar claves de licencia por volumen codificadas o claves de producto estándar. Si usa una clave de producto estándar, separe cada grupo de cinco caracteres por un guion (`-`). Por ejemplo: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. Si se trata de una actualización de una edición de licencia por volumen, la clave de producto puede no ser necesaria.  

        > [!Note]  
        > Esta clave de producto puede ser una clave de activación múltiple (CAM) o una clave de licencias por volumen genérica (CLVG). Las CLVG también se conocen como claves de configuración de cliente del servicio de administración de claves (SAC). Para obtener más información, consulte [Plan para la activación por volumen](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obtener una lista de claves de configuración de cliente KMS, consulte el [Apéndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) de la Guía de activación de Windows Server.

    - **Omitir cualquier mensaje de compatibilidad descartable**: seleccione esta opción si va a actualizar a Windows Server 2016. Si no selecciona esta configuración, la secuencia de tareas no se completará, ya que el programa de instalación de Windows espera a que el usuario seleccione **Confirmar** en un cuadro de diálogo de compatibilidad de aplicaciones de Windows.  

6. En la página **Incluir actualizaciones**, especifique si se van a instalar las actualizaciones de software necesarias, todas o ninguna. A continuación, seleccione **Siguiente**. Si especifica que se instalen las actualizaciones, Configuration Manager instala solo las destinadas a las colecciones a las que pertenece el equipo de destino.  

7. En la página **Instalar aplicaciones**, especifique las aplicaciones que desee instalar en el equipo de destino y seleccione **Siguiente**. Si selecciona más de una aplicación, especifique también si la secuencia de tareas debe continuar si se produce un error en la instalación de una aplicación específica.  

8. Complete el asistente.  

> [!Important]  
> Cuando se ejecuta la secuencia de tareas en un dispositivo, el cliente de Configuration Manager crea varios scripts para controlar el comportamiento de la secuencia de tareas en distintos escenarios. Cuando se completa la secuencia de tareas, el cliente no quita estos scripts hasta que se reinicia el equipo. Estos archivos de script no contienen información confidencial.  

La plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 incluye grupos adicionales con las acciones recomendadas que se agregarán antes y después del proceso de actualización. Estas acciones son comunes entre muchos clientes que están actualizando correctamente los dispositivos a Windows 10. Para obtener más información, vea los pasos de secuencia de tareas recomendados [para preparar la actualización](#recommended-task-sequence-steps-to-prepare-for-upgrade) y [para el procesamiento posterior](#recommended-task-sequence-steps-for-post-processing).

A partir de la versión 1806, esta plantilla de secuencia de tareas también incluye un grupo con las acciones recomendadas que se deben agregar en caso de error del proceso de actualización. Estas acciones facilitan la solución de problemas. Para obtener más información, consulte [Pasos de la secuencia de tareas recomendados para errores](#recommended-task-sequence-steps-on-failure).<!--1358500-->  


## <a name="configure-pre-cache-content"></a>Configuración del contenido de la caché previa

<!--1021244-->
La característica de caché previa para las implementaciones disponibles de secuencias de tareas permite que los clientes descarguen el contenido del paquete de actualización del sistema operativo relevante antes de que un usuario instale la secuencia de tareas.  

Para obtener más información, vea [Configuración del contenido de la caché previa](configure-precache-content.md).


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Pasos de secuencia de tareas recomendados para preparación para actualización

La plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 incluye grupos adicionales con las acciones recomendadas que se agregarán antes del proceso de actualización. Estas acciones del grupo **Preparación para actualización** son comunes entre muchos clientes que están actualizando correctamente los dispositivos a Windows 10. Si tiene una secuencia de tareas existente que aún no tiene estas acciones, agréguelas manualmente a la secuencia de tareas en el grupo **Preparar para actualización**.  

### <a name="battery-checks"></a>Comprobaciones de la batería

agregue pasos a este grupo para comprobar si el equipo usa la batería o una conexión por cable. Esta acción requiere un script o utilidad personalizado a fin de realizar la comprobación.

#### <a name="battery-check-example"></a>Ejemplo de comprobación de la batería

Use WbemTest y conéctese al espacio de nombres `root\cimv2`. Después, ejecute la siguiente consulta:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

Si devuelve algún resultado, el dispositivo se está ejecutando con batería. En caso contrario, el dispositivo está conectado a la red por cable.  

### <a name="networkwired-connection-checks"></a>Comprobaciones de conexión por cable o red

agregue pasos a este grupo para comprobar si el equipo está conectado a una red y no está usando una conexión inalámbrica. Esta acción requiere un script o utilidad personalizado a fin de realizar la comprobación.

#### <a name="network-check-example"></a>Ejemplo de comprobación de red

Use WbemTest y conéctese al espacio de nombres `root\cimv2`. Después, ejecute la siguiente consulta:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

Si se devuelve algún resultado, el dispositivo esta funcionando con una conexión Wi-Fi. En caso contrario, el dispositivo está conectado a la red por cable.

### <a name="remove-incompatible-applications"></a>Eliminación de aplicaciones no compatibles

agregue pasos a este grupo para quitar las aplicaciones no compatibles con esta versión de Windows 10. El método para desinstalar una aplicación es diferente en cada situación.  

Si la aplicación usa Windows Installer, copie la línea de comandos de **Desinstalar programa** desde la pestaña **Programas** en las propiedades del tipo de implementación de Windows Installer de la aplicación. Luego, agregue un paso para **Ejecutar línea de comandos** a este grupo con la línea de comandos de desinstalar programa. Por ejemplo:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>Eliminación de controladores no compatibles

agregue pasos a este grupo para quitar los controladores no compatibles con esta versión de Windows 10.  

### <a name="removesuspend-third-party-security"></a>Eliminación o suspensión de seguridad de terceros

agregue pasos a este grupo para quitar o suspender programas de seguridad de terceros, como antivirus.  

Si utiliza un programa de cifrado de disco de otro fabricante, indique su controlador de cifrado al programa de instalación de Windows con la [opción de línea de comandos](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers) `/ReflectDrivers`. Agregue un paso para [establecer la variable de secuencia de tareas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) a la secuencia de tareas en este grupo. Establezca la variable de secuencia de tareas en **OSDSetupAdditionalUpgradeOptions**. Establezca el valor en `/ReflectDrivers` con la ruta de acceso al controlador. Esta [variable de secuencia de tareas](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) anexa la línea de comandos del programa de instalación de Windows utilizada por la secuencia de tareas. Para obtener las instrucciones adicionales sobre este proceso, póngase en contacto con su proveedor de software.  

### <a name="download-package-content-task-sequence-step"></a>Paso de la secuencia de tareas Descargar contenido de paquete  

Use el paso [Descargar contenido de paquete](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) antes del paso **Actualizar sistema operativo** en los siguientes escenarios:  

- Use una única secuencia de tareas de actualización para las plataformas x86 y x64. Incluya dos pasos **Descargar contenido de paquete** en el grupo **Preparación para actualización**. Establezca condiciones en cada paso para detectar la arquitectura del cliente. Esta condición hace que el paso solo descargue el paquete de actualización de sistema operativo adecuado. Configure todos los pasos **Descargar contenido de paquete** para que usen la misma variable, y use la variable para la ruta de los medios en el paso **Actualizar sistema operativo** .  

- Para descargar dinámicamente un paquete de controladores aplicables, use dos pasos **Descargar contenido de paquete** con condiciones para detectar el tipo de hardware adecuado para cada paquete de controlador. Configure los pasos **Descargar contenido de paquete** para que usen la misma variable. Después, use esa variable para el valor **Contenido preconfigurado** de la sección de controladores del paso **Actualizar sistema operativo**.  

    > [!NOTE]  
    > Configuration Manager agrega un sufijo numérico al nombre de variable. Por ejemplo, si especifica `%mycontent%` como variable personalizada, el cliente almacena todo el contenido al que se hace referencia en esta ubicación. Cuando se hace referencia a la variable en un paso posterior, como **Actualizar sistema operativo**, se usa con un sufijo numérico. En este ejemplo, `%mycontent01%` o `%mycontent02%`, donde el número se corresponde al orden en el que el paso **Descargar contenido de paquete** muestra este contenido específico.  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>Pasos de la secuencia de tareas recomendados para posprocesamiento

Después de crear la secuencia de tareas, agregue pasos adicionales al grupo **Posprocesamiento** de la secuencia de tareas.  

> [!NOTE]  
> Esta secuencia de tareas no es lineal. Hay condiciones en los pasos que pueden afectar a los resultados de la secuencia de tareas. Este comportamiento depende de si actualiza correctamente el equipo cliente, o bien de si tiene que revertir el equipo cliente al sistema operativo original.  

La plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 incluye grupos adicionales con las acciones recomendadas que se agregarán después del proceso de actualización. Estas acciones del grupo **Posprocesamiento** son comunes entre muchos clientes que están actualizando correctamente los dispositivos a Windows 10. Si tiene una secuencia de tareas existente que aún no tiene estas acciones, agréguelas manualmente a la secuencia de tareas en el grupo **Posprocesamiento**.  

### <a name="apply-setup-based-drivers"></a>Aplicación de controladores basados en la instalación

agregue pasos a este grupo para instalar controladores de instalación (.exe) a partir de paquetes.  

### <a name="installenable-third-party-security"></a>Instalación y habilitación de seguridad de terceros

agregue pasos a este grupo para instalar o habilitar programas de seguridad de terceros, como antivirus.  

### <a name="set-windows-default-apps-and-associations"></a>Establecimiento de aplicaciones predeterminadas de Windows y asociaciones

agregue pasos a este grupo para establecer las aplicaciones predeterminadas de Windows y las asociaciones de archivos.

1. Prepare un equipo de referencia con las asociaciones de aplicaciones deseadas.
1. Ejecute la siguiente línea de comandos para exportar:  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. Agregue el archivo XML a un paquete.
1. Agregue un paso [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) en este grupo. Especifique el paquete que contiene el archivo XML y, a continuación, especifique la siguiente línea de comandos:  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

Para obtener más información, consulte [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations) (Exportación o importación de asociaciones de aplicaciones predeterminadas).

### <a name="apply-customizations-and-personalization"></a>Aplicación de personalizaciones

agregue pasos a este grupo para aplicar personalizaciones al menú Inicio, como la organización de los grupos de programas. Para obtener más información, consulte [Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen) (Personalización de la pantalla Inicio).  


## <a name="optional-task-sequence-steps-for-rollback"></a>Pasos de secuencia de tareas opcionales para la reversión  

Cuando se produce algún problema con el proceso de actualización después de reiniciar el equipo, el programa de instalación de Windows revierte el sistema al SO anterior. La secuencia de tareas continúa después con cualquier paso en el grupo **Reversión**. Después de crear la secuencia de tareas, agregue pasos opcionales en este grupo según sea necesario. Por ejemplo, revierta los cambios realizados en el sistema en el grupo Preparación para actualización, como desinstalar el software incompatible.


## <a name="recommended-task-sequence-steps-on-failure"></a>Pasos de la secuencia de tareas recomendados para errores

<!--1358500-->
A partir de la versión 1806, la plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 incluye un grupo para **Ejecutar acciones en caso de error**. Este grupo incluye las acciones recomendadas para agregar en caso de que se produzca un error en el proceso de actualización. Estas acciones facilitan la solución de problemas.

### <a name="collect-logs"></a>Recopilación de registros

para recopilar registros del cliente, agregue pasos en este grupo.  

- Una práctica común consiste en copiar los archivos de registro en un recurso compartido de red. Para establecer esta conexión, use el paso [Conectar a carpeta de red](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

- Para llevar a cabo la operación de copia, utilice una utilidad o script personalizado con el paso [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) o [Ejecutar script de PowerShell Script](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript).  

- Los archivos para recopilar podrían incluir los siguientes registros:  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- Para más información sobre setupact.log y otros registros de instalación de Windows, vea [Windows Setup Log files](https://docs.microsoft.com/windows/deployment/upgrade/log-files) (Archivos de registro de instalación de Windows).  

- Para obtener más información sobre registros de cliente de Configuration Manager, vea [Registros de cliente de Configuration Manager](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs).  

- Para obtener más información sobre **_SMSTSLogPath** y otras variables útiles, vea [Task sequence variables](../understand/task-sequence-variables.md) (Variables de secuencia de tareas).  

### <a name="run-diagnostic-tools"></a>Ejecución de herramientas de diagnóstico

para ejecutar herramientas de diagnóstico adicionales, agregue pasos en este grupo. Automatice estas herramientas para recopilar información adicional del sistema justo después del error.  

Una de estas herramientas es Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Es una herramienta de diagnóstico independiente para obtener detalles sobre el motivo de que una actualización de Windows 10 se haya realizado incorrectamente.  

- En Configuration Manager, [cree un paquete](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) para la herramienta.  

- Agregue un paso [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) a este grupo de la secuencia de tareas. Use la opción **Paquete** para hacer referencia a la herramienta. La siguiente cadena es una **línea de comandos** de ejemplo:  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`  

> [!TIP]
> Use siempre la versión más reciente de SetupDiag para contar con la funcionalidad y las correcciones más recientes de los problemas conocidos. Para más información, consulte [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag).

## <a name="additional-recommendations"></a>Otras recomendaciones

### <a name="windows-documentation"></a>Documentación de Windows

Consulte la documentación de Windows para [solucionar los errores de actualización de Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). En este artículo también se incluye información detallada sobre el proceso de actualización.  

### <a name="check-minimum-disk-space"></a>Comprobación del espacio mínimo en disco

En el paso predeterminado **Comprobar preparación**, habilite **Garantizar espacio libre mínimo en disco (MB)** . Establezca el valor en al menos **16384** (16 GB) para un paquete de actualización de sistema operativo de 32 bits, o **20480** (20 GB) para 64 bits.  

### <a name="retry-downloading-policy"></a>Reintento de descarga de la directiva

Use la [variable de secuencia de tareas](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) **SMSTSDownloadRetryCount** para intentar descargar de nuevo la directiva. En este momento, el cliente lo reintenta de manera predeterminada dos veces; esta variable está configurada en dos (2). Si los clientes no utilizan una conexión de red intranet por cable, una mayor cantidad de reintentos ayudará al cliente a obtener la directiva. El uso de esta variable no tiene ningún efecto secundario, además del retraso que implica la imposibilidad de descargar la directiva.<!--501016--> Aumente también la variable **SMSTSDownloadRetryDelay** desde el valor predeterminado de 15 segundos.  

### <a name="perform-an-inline-compatibility-assessment"></a>Realización de una evaluación de compatibilidad en línea

1. Agregue un segundo paso para **actualizar el sistema operativo** al principio del grupo **Preparar para la actualización**.  

    1. Póngale el nombre *Evaluación de actualización*.
    1. Especifique el mismo paquete de actualización y, a continuación, habilite la opción **Realizar examen de compatibilidad del programa de instalación de Windows sin iniciar la actualización**.
    1. Habilite **Continuar después de un error** en la pestaña Opciones.  

1. Inmediatamente después de este paso de *Evaluación de actualización*, agregue otro paso **Ejecutar línea de comandos**. Especifique la siguiente línea de comandos:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

1. En la pestaña **Opciones** , agregue la siguiente condición:

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

Este código de retorno es el equivalente decimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que es un examen de compatibilidad en el que no se detecta ningún problema. Si el paso *Evaluación de actualización* se realiza correctamente y devuelve este código, la secuencia de tareas omite este paso. En caso contrario, si el paso de la evaluación devuelve cualquier otro código de retorno, este paso produce un error en la secuencia de tareas con el código de retorno del examen de compatibilidad del programa de instalación de Windows. Para obtener más información sobre **_SMSTSOSUpgradeActionReturnCode**, vea [Task sequence variables](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode) (Variables de secuencia de tareas).

Para obtener más información, consulte [Actualizar el sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS).  

### <a name="convert-from-bios-to-uefi"></a>Conversión de BIOS a UEFI

Si desea cambiar el dispositivo de BIOS a UEFI durante esta secuencia de tareas, consulte [Conversión de BIOS a UEFI durante una actualización local](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).  

### <a name="manage-bitlocker"></a>Administración de BitLocker

<!--SCCMDocs issue #494-->
Si usa el cifrado de disco BitLocker, en ese caso, de forma predeterminada el programa de instalación de Windows la suspende automáticamente durante la actualización. A partir de Windows 10, versión 1803, el programa de instalación de Windows incluye el parámetro de línea de comandos `/BitLocker` para controlar este comportamiento. Si los requisitos de seguridad exigen mantener el cifrado de disco activo en todo momento, utilice la [variable de secuencia de tareas](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) **OSDSetupAdditionalUpgradeOptions** en el grupo **Preparar para actualización** para incluir `/BitLocker TryKeepActive`. Para más información, consulte [Opciones de la línea de comandos del programa de instalación de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### <a name="remove-default-apps"></a>Eliminación de aplicaciones predeterminadas

<!--SCCMDocs issue #526-->
Algunos clientes quitan las aplicaciones predeterminadas aprovisionadas en Windows 10. Por ejemplo, la aplicación Bing El Tiempo o la Microsoft Solitaire Collection. En algunas situaciones, estas aplicaciones vuelven después de actualizar Windows 10. Para obtener más información, vea [How to keep apps removed from Windows 10 (Cómo mantener las aplicaciones eliminadas en Windows 10)](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update).

Agregue un paso **Ejecutar línea de comandos** a la secuencia de tareas en el grupo **Preparar para actualización**. Especifique una línea de comandos similar al ejemplo siguiente:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
