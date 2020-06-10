---
title: Administración de clientes
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar clientes en Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b9111e3be82424425561e0a664fee955d73ee63
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270827"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Procedimientos para administrar clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Cuando el cliente de Configuration Manager se instala y se asigna correctamente a un sitio, puede ver el dispositivo en el área de trabajo **Activos y compatibilidad** del nodo **Dispositivos** y en una o varias recopilaciones del nodo **Recopilaciones de dispositivos**. Seleccione el dispositivo o una recopilación, y después ejecute operaciones de administración. Pero existen otras formas de administrar el cliente, que es posible que involucren otras áreas de trabajo de la consola o tareas externas a la consola.  

> [!NOTE]  
> Si instala el cliente de Configuration Manager pero todavía no se ha asignado correctamente a un sitio, es posible que no aparezca en la consola. Después de que el cliente se asigne a un sitio, actualice la pertenencia a la recopilación y actualice la vista de consola.  
>
> Un dispositivo también se puede mostrar en la consola cuando el cliente de Configuration Manager no está instalado. Este comportamiento se produce si el sitio detecta un dispositivo, pero el cliente no está instalado ni asignado.
>
> Los dispositivos móviles que se administran mediante el [conector de Exchange Server](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) o [MDM local](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) no instalan el cliente de Configuration Manager.  
>
> Para administrar un dispositivo desde la consola, use la columna **Cliente** del nodo **Dispositivos** para determinar si el cliente está instalado.  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> Administración de clientes desde el nodo **Dispositivos**  

Dependiendo del tipo de dispositivo, es posible que algunas de estas opciones no estén disponibles.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Dispositivos**.  

2. Seleccione uno o más dispositivos y, después, seleccione una de estas tareas de administración de cliente en la cinta. (También puede hacer clic con el botón derecho en el dispositivo).  

### <a name="import-user-device-affinity"></a>Importar afinidad de dispositivo de usuario

Configure las asociaciones entre usuarios y dispositivos, de manera que pueda implementar de manera eficaz el software a los usuarios.  

Para obtener más información, vea [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="import-computer-information"></a>Importar información del equipo

Inicie el **Asistente para importar información de equipo** para importar información del equipo nuevo a la base de datos de Configuration Manager. Puede importar varios equipos mediante un archivo, o bien especificar información para un único equipo.

### <a name="add-selected-items"></a>Agregar elementos seleccionados

Se muestran las opciones siguientes:

- **Agregar elementos seleccionados a la recopilación de dispositivos existente**: Abre el cuadro de diálogo **Seleccionar recopilación** . Seleccione la recopilación a la que quiera agregar este dispositivo. El dispositivo se incluye en esta recopilación mediante una regla de pertenencia **Directa**.  

- **Agregar elementos seleccionados a la nueva recopilación de dispositivos**: abre el **Asistente para crear recopilación de dispositivos**, donde puede crear una recopilación. La recopilación seleccionada se incluye en esta recopilación mediante una regla de pertenencia **Directa**.  

Para obtener más información, vea [Creación de recopilaciones](collections/create-collections.md).

### <a name="install-client"></a>Instalar cliente

Se abre el **Asistente para la instalación de cliente**. Este asistente usa la instalación de inserción de cliente para instalar o reinstalar un cliente de Configuration Manager en el dispositivo seleccionado.

> [!TIP]  
> Hay muchas maneras diferentes de instalar el cliente de Configuration Manager. Aunque el asistente Inserción del cliente ofrece un método de instalación de cliente cómodo desde la consola, este método tiene muchas dependencias y no es adecuado para todos los entornos. Para más información sobre las dependencias, vea [Requisitos previos para la implementación de clientes en equipos Windows](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation). Para más información sobre los otros tipos de instalación de clientes, vea [Métodos de instalación de cliente](../deploy/plan/client-installation-methods.md).

Para más información, vea [Cómo instalar clientes de Configuration Manager mediante la inserción de cliente](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

### <a name="run-script"></a>Ejecutar script

Abre el asistente **Ejecutar el script** para ejecutar un script de PowerShell en el dispositivo seleccionado.

Para obtener más información, consulte [Creación y ejecución de scripts de PowerShell](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="install-application"></a>Instalación de la aplicación

Instale una aplicación en un dispositivo en tiempo real. Esta característica puede ayudar a reducir la necesidad de colecciones independientes para cada aplicación.

Para más información, consulte [Instalación de aplicaciones para un dispositivo](../../../apps/deploy-use/install-app-for-device.md).

### <a name="reassign-site"></a>Reasignar el sitio

Reasigne uno o más clientes, incluidos dispositivos móviles administrados, a otro sitio primario en la jerarquía. Puede reasignar los clientes de forma individual o seleccionar más de uno para reasignarlos de forma masiva.  

### <a name="client-settings---resultant-client-settings"></a>Configuración de cliente: configuración de cliente resultante

Cuando se implementan varias configuraciones de cliente en el mismo dispositivo, el establecimiento de prioridades y la combinación de configuraciones son complejos. Use esta opción para ver el conjunto resultante de la configuración de cliente implementada en este dispositivo.

Para obtener más información, vea [Cómo configurar el cliente](../deploy/configure-client-settings.md).

### <a name="start"></a>Start

- Ejecute el **Explorador de recursos** para ver la información de inventario de hardware y software de un cliente de Windows. Vea los siguientes artículos para más información:

  - [Cómo usar el Explorador de recursos para ver el inventario de hardware](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [Cómo usar el Explorador de recursos para ver el inventario de software](inventory/use-resource-explorer-to-view-software-inventory.md)

- Administre el dispositivo de forma remota mediante **Control remoto**, **Asistencia remota** o **Cliente de Escritorio remoto**. Para obtener más información, vea [Cómo administrar de forma remota un equipo cliente de Windows](remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="approve"></a>Aprobar

Cuando el cliente se comunica con los sistemas de sitio mediante HTTP y un certificado autofirmado, debe aprobar estos clientes para identificarlos como equipos de confianza. De forma predeterminada, la configuración del sitio aprueba automáticamente los clientes del mismo bosque de Active Directory, bosques de confianza e inquilinos conectados de Azure Active Directory (Azure AD).<!-- MEMDocs#318 -->. Este comportamiento predeterminado significa que no es necesario aprobar cada cliente de forma manual. Apruebe manualmente los equipos del grupo de trabajo de confianza y cualquier otro equipo de confianza que no esté aprobado.

> [!IMPORTANT]  
> Aunque algunas funciones de administración puedan funcionar para los clientes no aprobados, este es un escenario no compatible para Configuration Manager.  

No tiene que aprobar clientes que se comunican siempre con sistemas de sitio mediante HTTPS, o bien clientes que usan un certificado PKI al comunicarse con sistemas de sitio mediante HTTP. Estos clientes establecen confianza mediante el uso de los certificados PKI.

### <a name="block-or-unblock"></a>Bloquear o desbloquear

Bloquee un cliente que ya no sea de confianza. El bloqueo impide que el cliente reciba la directiva y evita que los sistemas de sitio se comuniquen con el cliente.  

> [!IMPORTANT]  
> El bloqueo de un cliente solo impide la comunicación del cliente con sistemas de sitio de Configuration Manager. No evita la comunicación con otros dispositivos. Cuando el cliente se comunica con sistemas de sitio mediante HTTP en lugar de HTTPS, existen algunas limitaciones de seguridad.  

También puede desbloquear a un cliente que está bloqueado.

Para obtener más información, vea [Determinar si bloquear clientes](../deploy/plan/determine-whether-to-block-clients.md).

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>Borrar implementaciones de PXE requeridas

Puede realizar de nuevo una implementación del entorno PXE requerida. Para ello, borre el estado de la última implementación del entorno PXE asignada a un equipo o a una recopilación de Configuration Manager. Esta acción restablece el estado de la implementación, y vuelve a instalar las implementaciones requeridas más recientes.

Para más información, vea [Use PXE to deploy Windows over the network](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).

### <a name="client-notification"></a>Notificación de cliente

Para obtener más información, vea [Notificación de cliente](client-notification.md#client-notification).

### <a name="endpoint-protection"></a>Endpoint Protection

Para obtener más información, vea [Notificación de cliente](client-notification.md#endpoint-protection).

### <a name="edit-primary-users"></a>Editar usuarios primarios

Vea los usuarios de este dispositivo en los últimos 90 días, o bien especifique los usuarios primarios de este dispositivo.

Para obtener más información, vea [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="wipe-a-mobile-device"></a>Borrar un dispositivo móvil

Puede borrar dispositivos móviles compatibles con el comando de borrado. Esta acción elimina permanentemente todos los datos en el dispositivo móvil, incluida la configuración personal y los datos personales. Normalmente, esta acción restablece el dispositivo móvil a sus valores predeterminados de fábrica. Borre un dispositivo móvil cuando ya no sea de confianza. Por ejemplo, en caso de pérdida o robo del dispositivo.  

> [!TIP]  
> Compruebe la documentación del fabricante para obtener más información acerca de cómo el dispositivo móvil procesa un comando de borrado remoto.  

Se suele producir un retraso hasta que el dispositivo móvil recibe el comando de borrado:  

- Si el dispositivo móvil está inscrito por Configuration Manager, el cliente recibe el comando cuando descarga su directiva de cliente.

- Si el dispositivo móvil está administrado por el conector de Exchange Server, recibe el comando cuando se sincroniza con Exchange.  

Para supervisar la recepción en el dispositivo del comando de borrado, use la columna **Estado de borrado**. Hasta que el dispositivo no envíe una confirmación de borrado a Configuration Manager, puede cancelar el comando de borrado.  

### <a name="retire-a-mobile-device"></a>Retirar un dispositivo móvil

La opción **Retirar** solo se admite en dispositivos móviles inscritos mediante MDM local.  

Para más información, vea [Protección de los datos mediante la eliminación remota, el bloqueo remoto o el restablecimiento de código de acceso](../../../mdm/deploy-use/wipe-lock-reset-devices.md).

### <a name="change-ownership"></a>Cambiar la propiedad

Si un dispositivo no está unido a un dominio y no tiene el cliente de Configuration Manager instalado, use esta opción para cambiar la propiedad a **Compañía** o **Personal**.  

Puede usar este valor en requisitos de aplicaciones para controlar las implementaciones y para controlar la cantidad de inventario que se recopila de los dispositivos de los usuarios.  

Puede que necesite agregar la columna **Propietario del dispositivo** a la vista haciendo clic con el botón derecho en cualquier encabezado de columna y seleccionándola.

### <a name="delete"></a>Eliminar

> [!WARNING]  
> No elimine un cliente si quiere desinstalar el cliente de Configuration Manager o quitarlo de una recopilación.  

La acción **Eliminar** elimina de forma manual el registro de cliente de la base de datos de Configuration Manager. Use esta acción solo para solucionar un problema. Si elimina el objeto, pero el cliente sigue instalado y se comunica con el sitio, Detección de latido vuelve a crear el registro del cliente. Vuelve a aparecer en la consola de Configuration Manager, aunque se pierden el historial del cliente y todas las asociaciones anteriores.  
> [!NOTE]  
> Cuando se elimina un cliente de dispositivo móvil inscrito por Configuration Manager, esta acción también revoca el certificado PKI emitido. Después, el punto de administración rechaza este certificado, incluso si IIS no comprueba la lista de revocación de certificados (CRL).
>
> Cuando elimina estos clientes, no se revocan los certificados en los clientes heredados de dispositivos móviles.

Para desinstalar el cliente, vea [Desinstalar el cliente de Configuration Manager](#BKMK_UninstalClient).  

Para asignar el cliente a un nuevo sitio primario, vea [Cómo asignar clientes a un sitio en Configuration Manager](../deploy/assign-clients-to-a-site.md).

Para quitar el cliente de una recopilación, vuelva a configurar las propiedades de la recopilación. Para obtener más información, vea [Cómo administrar colecciones](collections/manage-collections.md).

### <a name="refresh"></a>Actualizar

Actualice la vista de la consola con los datos más recientes de la base de datos. Por ejemplo, si un dispositivo aparece en la lista de la detección, pero no se muestra como instalado. Después de instalar el cliente y asegurarse de que está asignado al sitio, seleccione **Actualizar**.

### <a name="properties"></a>Propiedades

Vea las implementaciones y los datos de detección destinados al cliente.

También puede configurar variables que usan las secuencias de tareas para implementar un sistema operativo en el dispositivo. Para más información, vea [Creación de variables de secuencia de tareas para dispositivos y recopilaciones](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Administración de clientes desde el nodo **Recopilaciones de dispositivos**

Muchas de las tareas que están disponibles para los dispositivos en el nodo **Dispositivos** también lo están en las colecciones. La consola aplica automáticamente la operación en todos los dispositivos aptos de la recopilación. Esta acción en una recopilación completa genera paquetes de red adicionales y aumenta el uso de la CPU en el servidor del sitio.  

Tenga en cuenta las preguntas siguientes antes de ejecutar tareas de nivel de recopilación. Una vez que se haya iniciado, no puede detener la tarea desde la consola.

- ¿Cuántos dispositivos hay en la recopilación?
- ¿Los dispositivos están conectados mediante conexiones de red de ancho de banda reducido?
- ¿Cuánto tiempo tarda esta tarea en completarse para todos los dispositivos?

Para obtener más información, vea [Cómo administrar colecciones](collections/manage-collections.md).


## <a name="restart-clients"></a>Reinicio de clientes

Use la consola de Configuration Manager para identificar los clientes que precisan un reinicio. Después, use una acción de notificación de cliente para reiniciarlos.

> [!Tip]
> Habilite la actualización de cliente automática para mantener a los clientes actualizados con menos esfuerzo. Para obtener más información, vea [Usar una actualización de cliente automática](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

Para identificar los dispositivos pendientes de reinicio, vaya al área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager y seleccione el nodo **Dispositivos**. Después, puede ver el estado de cada dispositivo en el panel de detalles en una nueva columna denominada **Reinicio pendiente**. Cada dispositivo tiene uno o varios de los valores siguientes:

- **No**: no hay ningún reinicio pendiente
- **Configuration Manager**: este valor proviene del componente de coordinador de reinicio de cliente (RebootCoordinator.log)
- **Cambiar nombre de archivo**: este valor proviene de una operación de cambio de nombre de archivo pendiente notificada por Windows (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
- **Windows Update**: este valor proviene de la notificación de Windows Update Agent de un reinicio pendiente necesario para una o varias actualizaciones (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **Agregar o quitar características**: este valor proviene del servicio basado en componentes de Windows que notifica que la adición o eliminación de una característica de Windows requiere un reinicio (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending)

### <a name="create-the-client-notification-to-restart-a-device"></a>Creación de la notificación de cliente para reiniciar un dispositivo

1. Seleccione el dispositivo que quiera reiniciar dentro de una recopilación en el nodo **Recopilaciones de dispositivos** de la consola.
2. En la cinta, seleccione **Notificación de cliente** y luego **Reiniciar**. Se abre una ventana de información sobre el reinicio. Seleccione **Aceptar** para confirmar la solicitud de reinicio.

Cuando el cliente recibe la notificación de un **Centro de software**, se abre la ventana de notificación para informar al usuario sobre el reinicio. De forma predeterminada, el reinicio se produce al cabo de 90 minutos. Puede modificar la hora de reinicio en la [configuración de cliente](../deploy/configure-client-settings.md). La configuración para el comportamiento del reinicio se encuentra en la pestaña [Reinicio de equipo](../deploy/about-client-settings.md#computer-restart) de la configuración predeterminada.


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a> Configuración de la caché de cliente

La caché del cliente almacena los archivos temporales para el momento en que los clientes instalen aplicaciones y programas. Las actualizaciones de software también usan la caché de cliente, pero siempre intentan descargar a la caché independientemente de la configuración de tamaño. Configure las opciones de caché, como el tamaño y ubicación, al instalar manualmente el cliente, al usar la instalación de inserción de cliente o después de la instalación.

Puede especificar el tamaño de la carpeta de caché mediante la configuración del cliente en la consola de Configuration Manager. Para obtener más información, vea [Configuración de la memoria caché del cliente](../deploy/about-client-settings.md#client-cache-settings).

La ubicación predeterminada de la caché de cliente de Configuration Manager es `%windir%\ccmcache` y el espacio en disco predeterminado es 5120 MB.  

> [!IMPORTANT]  
> No cifre la carpeta que se usa para la caché de cliente. Configuration Manager no puede descargar contenido en una carpeta cifrada.  

### <a name="about-the-client-cache"></a>Acerca de la caché de cliente  

El cliente de Configuration Manager descarga el contenido del software necesario en cuanto recibe la implementación, pero espera el tiempo programado para ejecutar la implementación. Cuando llega el momento programado, el cliente de Configuration Manager comprueba si el contenido está disponible en la caché. Si el contenido está en la caché y es la versión correcta, el cliente usa el contenido almacenado en caché. Cuando cambia la versión requerida del contenido, o bien si el cliente elimina el contenido para hacer sitio a otro paquete, el cliente descarga de nuevo el contenido en la caché.  

Si el cliente trata de descargar el contenido de un programa o aplicación cuyo tamaño es mayor que el de la caché, se produce un error de implementación debido a la falta de espacio en la caché. El cliente genera el mensaje de estado 10050 de tamaño de caché insuficiente. Si aumenta el tamaño de caché más adelante, el resultado es el siguiente:  

- Para un programa necesario: el cliente no reintenta descargar el contenido de forma automática. Vuelva a implementar el paquete y el programa en el cliente.  
- Para una aplicación requerida: el cliente vuelve a intentar descargar el contenido automáticamente cuando descarga su directiva de cliente.  

Si el cliente intenta descargar un paquete cuyo tamaño es inferior al de la caché, pero la caché está llena, se reintentan todas las implementaciones *requeridas* hasta que:

- La caché disponga de espacio
- Se agote el tiempo de espera de la descarga
- Se alcance el límite de número de reintentos

Si después aumenta el tamaño de la caché, el cliente intenta volver a descargar el paquete durante el próximo intervalo de reintento. El cliente intenta descargar el contenido cada cuatro horas hasta un máximo de 18 veces.  

El contenido en caché no se elimina de forma automática. Permanece en la caché al menos durante un día después de que el cliente use ese contenido. Si configura las propiedades del paquete con la opción para conservar el contenido de la caché del cliente, el cliente no lo elimina automáticamente. Si los paquetes descargados en las últimas 24 horas ocupan el espacio de la caché y el cliente debe descargar paquetes nuevos, puede aumentar el tamaño de la caché u optar por eliminar el contenido conservado en la caché.  

Utilice los procedimientos siguientes para configurar la caché del cliente durante la instalación manual del cliente, o después de instalar el cliente.  

### <a name="configure-the-cache-during-manual-client-installation"></a>Configuración de la caché durante la instalación manual del cliente  

Ejecute el comando CCMSetup.exe desde la ubicación de origen de instalación y especifique las siguientes propiedades necesarias, que han de estar separadas por espacios:  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > Use la configuración de tamaño de caché disponible en **Configuración de cliente** en la consola de Configuration Manager en lugar de SMSCACHESIZE. Para obtener más información, vea [Configuración de la memoria caché del cliente](../deploy/about-client-settings.md#client-cache-settings).

Para obtener más información sobre estas propiedades de línea de comandos para CCMSetup.exe, vea [Acerca de las propiedades de instalación de clientes](../deploy/about-client-installation-properties.md).

### <a name="configure-the-cache-during-client-push-installation"></a>Configuración de la caché durante la instalación de inserción de cliente  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Seleccione el sitio adecuado. En la pestaña **Inicio** de la cinta, en el grupo **Configuración**, seleccione **Configuración de instalación de cliente** y después **Instalación de inserción de cliente**. Cambie a la pestaña **Propiedades de instalación**.  

3. Especifique las siguientes propiedades, separadas por espacios:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > Use la configuración de tamaño de caché disponible en **Configuración de cliente** en la consola de Configuration Manager en lugar de SMSCACHESIZE. Para obtener más información, vea [Configuración de la memoria caché del cliente](../deploy/about-client-settings.md#client-cache-settings).

     Para obtener más información sobre estas propiedades de línea de comandos para CCMSetup.exe, vea [Acerca de las propiedades de instalación de clientes](../deploy/about-client-installation-properties.md).  

### <a name="configure-the-cache-on-the-client-computer"></a>Configuración de la caché en el equipo cliente  

1. En el equipo cliente, abra el panel de control de **Configuration Manager**.  

2. Cambie a la pestaña **Caché**. Establezca las propiedades de espacio y ubicación. La ubicación predeterminada es `%windir%\ccmcache`.  

3. Para eliminar los archivos de la carpeta de caché, pulse **Eliminar archivos**.  

### <a name="configure-client-cache-size-in-client-settings"></a>Configuración del tamaño de la caché de cliente en la configuración de cliente

Ajuste el tamaño de la carpeta de caché de cliente sin tener que volver a instalar el cliente. Use la configuración de tamaño de caché disponible en **Configuración de cliente** en la consola de Configuration Manager. Para obtener más información, vea [Configuración de la memoria caché del cliente](../deploy/about-client-settings.md#client-cache-settings).


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a> Desinstalación del cliente

Puede desinstalar el software cliente de Configuration Manager de un equipo mediante **CCMSetup.exe** con la propiedad **/Uninstall**. Ejecute CCMSetup.exe en un equipo individual desde el símbolo del sistema, o bien implemente un paquete para desinstalar el cliente de una recopilación de equipos.  

> [!NOTE]  
> No puede desinstalar al cliente de Configuration Manager desde un dispositivo móvil. Si debe quitar el cliente de Configuration Manager de un dispositivo móvil, debe borrar el dispositivo y, de esta forma, se eliminan todos los datos del dispositivo móvil.  

1. Abra un símbolo del sistema de Windows como administrador. Cambie la carpeta a la ubicación en la que se encuentra CCMSetup.exe, por ejemplo: `cd %windir%\ccmsetup`.

2. Ejecute el comando siguiente: `CCMSetup.exe /uninstall`.

> [!TIP]  
> El proceso de desinstalación no muestra ningún resultado en la pantalla. Para comprobar que el cliente se desinstala correctamente, vea el siguiente archivo de registro: `%windir%\ccmsetup\logs\CCMSetup.log`  
>
> Si tiene que esperar a que se complete el proceso de desinstalación antes de hacer algo más, ejecute `Wait-Process CCMSetup` en PowerShell. Este comando puede pausar un script hasta que se complete el proceso de CCMSetup.


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a> Administración de registros en conflicto

Configuration Manager usa el identificador de hardware para tratar de identificar los clientes que puedan estar duplicados y alertarle de los registros en conflicto. Por ejemplo, si reinstala un equipo, el identificador de hardware sería el mismo, pero el GUID que usa Configuration Manager es posible que cambie.  

Configuration Manager resuelve automáticamente los conflictos mediante la autenticación de Windows de la cuenta del equipo o un certificado PKI de un origen de confianza. Cuando Configuration Manager no puede resolver el conflicto de identificadores de hardware duplicados, una configuración de jerarquía determina el comportamiento.

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>Cambio de la configuración de la jerarquía para administrar los registros en conflicto  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.

1. En la cinta, seleccione **Configuración de jerarquía**.

1. Cambie a la pestaña **Aprobación de cliente y registros conflictivos** y seleccione una de las opciones siguientes:

    - **Resolver automáticamente los registros conflictivos**
    - **Resolver manualmente los registros conflictivos**

### <a name="manually-resolve-conflicting-records"></a>Resolver manualmente los registros conflictivos  

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado del sistema** y seleccione el nodo **Registros en conflicto**.  

1. Seleccione uno o más registros en conflicto y, después, pulse **Registros en conflicto**.  

1. Seleccione una de las siguientes opciones:  

    - **Combinar**: para combinar el registro recién detectado con el registro de cliente existente.  

    - **Nuevo**: para crear un registro de cliente en conflicto.  

    - **Bloquear**: para crear un registro de cliente en conflicto, pero marcarlo como bloqueado.  


## <a name="manage-duplicate-hardware-identifiers"></a>Administrar identificadores de hardware duplicados

Puede proporcionar una lista de identificadores de hardware que Configuration Manager ignora en el registro de clientes y el arranque PXE. Esta lista ayuda a resolver dos problemas comunes:

1. Muchos dispositivos nuevos no incluyen un puerto Ethernet incorporado. Los técnicos usan un adaptador de USB a Ethernet para establecer una conexión con cable para la implementación del sistema operativo. Estos adaptadores se suelen compartir debido a su costo y su facilidad de uso general. En el sitio se usa la dirección MAC de este adaptador para identificar el dispositivo. Por tanto, la reutilización del adaptador se vuelve problemática sin acciones de administrador adicionales entre cada implementación. Para volver a usar el adaptador en este escenario, excluya su dirección MAC.

2. Aunque el atributo SMBIOS debe ser único, algunos dispositivos de hardware especiales tienen identificadores duplicados. Excluya este identificador duplicado y use la dirección MAC única de cada dispositivo como base.

Use el proceso siguiente para agregar identificadores de hardware a fin de que Configuration Manager los omita:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.

2. En la pestaña **Inicio** de la cinta, en el grupo **Sitios**, seleccione **Configuración de jerarquía**.

3. Cambie a la pestaña **Aprobación de cliente y registros conflictivos**. Para agregar nuevos identificadores de hardware, seleccione **Agregar** en la sección **Identificadores de hardware duplicados**.

> [!TIP]
> A partir de la versión 1910, use los siguientes cmdlets de PowerShell para automatizar la administración de identificadores de hardware duplicados:<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a> Inicio de la recuperación de la directiva

Un cliente de Configuration Manager descarga su directiva de cliente en una programación que se configura como una configuración de cliente. También puede iniciar la recuperación de la directiva a petición desde el cliente. Por ejemplo, para situaciones de solución de problemas o de prueba.  

- [Notificación de cliente](#bkmk_policy-notify)
- [Panel de control del cliente](#bkmk_policy-manual)
- [Centro de soporte técnico](#bkmk_policy-support)
- [Un script](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a> Inicio de la recuperación de directivas de cliente mediante la notificación de cliente  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione **Dispositivos**.  

1. Seleccione el dispositivo para el que quiera descargar la directiva. En la pestaña **Inicio** de la cinta, en el grupo **Dispositivo**, seleccione **Notificación de cliente** y después **Descargar directiva de equipo**.  

    > [!NOTE]  
    > También puede usar la notificación de cliente para iniciar la recuperación de directivas para todos los dispositivos de una colección.  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a> Inicio de la recuperación de la directiva de cliente desde el panel de control del cliente de Configuration Manager

1. Abra el panel de control de **Configuration Manager** en el equipo.  

2. Cambie a la pestaña **Acciones**. Seleccione **Ciclo de evaluación y recuperación de directivas de equipo** para iniciar la directiva de equipo y, después, seleccione **Ejecutar ahora**.  

3. Seleccione **Aceptar** para confirmar el mensaje.  

4. Repita los pasos anteriores para cualquier otra acción. Por ejemplo, **Ciclo de evaluación y recuperación de directivas de usuario** para la configuración de cliente del usuario.  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a> Inicio de la recuperación de la directiva de cliente con el Centro de soporte técnico

Use el Centro de soporte técnico para solicitar y ver la directiva de cliente. Para más información, vea [Referencia del Centro de soporte técnico](../../support/support-center-ui-reference.md#bkmk_support-policy).

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a> Inicio de la recuperación de la directiva de cliente mediante script  

1. Abra un editor de scripts, como el Bloc de notas o Windows PowerShell ISE.  

2. Copie e inserte el siguiente código de PowerShell de ejemplo<!-- SCCMDocs#1591 --> en el archivo:  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > Para más información sobre los identificadores de programación, vea [Identificadores de mensaje](../../support/send-schedule-tool.md#bkmk_sendschedule-guids).

3. Guarde el archivo con una extensión .ps1.  

4. Ejecute el script en el cliente.
