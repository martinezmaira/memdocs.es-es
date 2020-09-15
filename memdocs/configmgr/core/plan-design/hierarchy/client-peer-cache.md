---
title: Caché del mismo nivel de cliente
titleSuffix: Configuration Manager
description: Use la caché del mismo nivel de cliente para las ubicaciones de origen al implementar contenido con Configuration Manager.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d0bd136278053ded38d0d6ed4cfe4059ffe3037
ms.sourcegitcommit: 0ec6d8dabb14f20b1d84f7b503f1b03aac2a30d4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2020
ms.locfileid: "89479321"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Caché del mismo nivel para clientes de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--1101436-->
La caché del mismo nivel se usa para ayudar a administrar la implementación de contenido en clientes en ubicaciones remotas. El almacenamiento en caché del mismo nivel es una solución integrada de Configuration Manager que permite a los clientes compartir contenido con otros clientes directamente desde su caché local.   

> [!Note]  
> En la versión 1906, Configuration Manager habilita esta característica opcional de forma predeterminada, mientras que en la versión 1902 o anteriores no lo hace. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  



## <a name="overview"></a>Introducción

Definiciones:  

- **Cliente de caché del mismo nivel**: cualquier cliente de Configuration Manager que descarga contenido desde el mismo nivel.  

- **Origen de la caché del mismo nivel**: cliente de Configuration Manager que se habilita para la caché del mismo nivel y que tiene contenido para compartir con otros clientes.  

Use la configuración de cliente para habilitar a los clientes para que sean orígenes de caché del mismo nivel. No es necesario habilitar los clientes de caché del mismo nivel. Cuando se habilitan los clientes para ser orígenes de caché del mismo nivel, el punto de administración los incluye en la lista de orígenes de ubicación de contenido.<!--510397--> Para obtener más información sobre este proceso, vea [Operaciones](#operations).  

Un origen de caché del mismo nivel debe ser miembro del grupo de límites actual del cliente de caché del mismo nivel. El punto de administración no incluye los orígenes de caché del mismo nivel de un grupo de límites vecino en la lista de orígenes de contenido que proporciona al cliente. Solo incluye los puntos de distribución de un grupo de límites vecino. Para más información acerca de los grupos de límites actuales y vecinos, vea [Grupos de límites](../../servers/deploy/configure/boundary-groups.md).<!--SCCMDocs issue 685-->  

El cliente de Configuration Manager usa la caché del mismo nivel para proporcionar a otros clientes todos los tipos de contenido en la caché. Este contenido incluye archivos de Aplicaciones de Microsoft 365 para empresas y archivos de instalación rápida.<!--SMS.500850-->  

La caché del mismo nivel no reemplaza el uso de otras soluciones como Optimización de distribución o Windows BranchCache. La caché del mismo nivel funciona junto con otras soluciones. Estas tecnologías le proporcionan más opciones para extender las soluciones tradicionales de implementación de contenido, como los puntos de distribución. La caché del mismo nivel es una solución personalizada que no depende de BranchCache. Si no habilita o usa BranchCache, la caché del mismo nivel sigue funcionando.  

> [!Note]  
> A partir de la versión 1802, Windows BranchCache siempre está habilitado en las implementaciones. Se ha quitado la opción **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**.<!--SCCMDocs issue 539--> Si el punto de distribución lo admite, y está habilitado en la configuración del cliente, los clientes usan BranchCache. Para más información, consulte [Configurar BranchCache](../../clients/deploy/about-client-settings.md#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Operaciones

Para habilitar la caché del mismo nivel, implemente la [configuración de cliente](#bkmk_settings) en una colección. Después, los miembros de esa colección actúan como un origen de la caché del mismo nivel para otros clientes en el mismo grupo de límites.  

- Un cliente que actúa como origen de contenido del mismo nivel envía una lista de contenido almacenado en caché disponible a su punto de administración mediante mensajes de estado. Un cliente de origen de contenido del mismo nivel también envía un mensaje de estado al punto de administración cuando quita contenido de la memoria caché local.

   > [!NOTE]
   > Vea [Mensajes de estado en Configuration Manager](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map) para obtener la lista de mensajes de estado de origen de contenido del mismo nivel aplicables, en concreto los que tienen los identificadores de mensaje de estado 7200, 7201, 7202 y 7203.

- Otro cliente en el mismo grupo de límites solicita una ubicación de contenido al punto de administración. El servidor devuelve la lista de posibles orígenes de contenido. En esta lista se incluyen todos los orígenes de caché del mismo nivel que tienen contenido y están en línea. También se incluyen los puntos de distribución y otras ubicaciones de origen de contenido de ese grupo de límites. Para obtener más información, vea [Content source priority](fundamental-concepts-for-content-management.md#content-source-priority) (Prioridad de los orígenes de contenido).  

- Como es habitual, el cliente que busca el contenido selecciona un origen de la lista proporcionada. Después, el cliente intenta obtener el contenido.  

A partir de la versión 1806, los grupos de límites incluyen valores de configuración adicionales para ofrecerle mayor control sobre la distribución de contenido en su entorno. Para más información, vea [Opciones de grupo de límites para descargas del mismo nivel](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Si el cliente reserva el contenido en un grupo de límites vecino, el punto de administración no agrega los orígenes de caché del mismo nivel del grupo de límites vecino a la lista de ubicaciones de origen de contenido potenciales.  

Solo se eligen los clientes más adecuados como orígenes de caché del mismo nivel. Evalúe la idoneidad del cliente en función de atributos como el tipo de chasis, el espacio en disco y la conectividad de red. Para obtener más información que pueda ayudar a seleccionar los mejores clientes para la caché del mismo nivel, vea [este blog de un consultor de Microsoft](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801).


### <a name="limited-access-to-a-peer-cache-source"></a>Acceso limitado al origen de caché del mismo nivel  

Un origen de caché del mismo nivel rechaza las solicitudes de contenido cuando cumple alguna de las condiciones siguientes en el momento en que un elemento del mismo nivel solicita contenido:  

- Modo de batería baja  

- La carga del procesador supera el 80 %  

- E/S de disco tiene un valor *AvgDiskQueueLength* superior a 10  

- No hay más conexiones disponibles para el equipo  

> [!Tip]  
> Configure estas opciones mediante la clase WMI del servidor de configuración de cliente para la característica de origen del mismo nivel (*SMS_WinPEPeerCacheConfig*) en el SDK de Configuration Manager.  

Cuando el origen de caché del mismo nivel rechaza una solicitud del contenido, el cliente de caché del mismo nivel continúa buscando el contenido en la lista de ubicaciones de origen de contenido.   



## <a name="requirements"></a>Requisitos

- La caché del mismo nivel admite todas las versiones de Windows que aparecen en [Sistemas operativos compatibles con dispositivos y clientes](../configs/supported-operating-systems-for-clients-and-devices.md). Los sistemas operativos que no son Windows no se admiten como orígenes de caché del mismo nivel ni clientes de caché del mismo nivel.  

- Un origen de caché del mismo nivel debe ser un cliente de Configuration Manager unido a un dominio. Pero un cliente que no esté unido a un dominio puede obtener contenido de un origen de caché del mismo nivel unido a un dominio.  

- Los clientes solo pueden descargar contenido desde los orígenes de caché del mismo nivel de su grupo de límites actual.  

- No se necesita una [cuenta de acceso a la red](accounts.md#network-access-account), con la siguiente excepción:  

  - Una cuenta de acceso a la red se configura en el sitio cuando un cliente habilitado para la caché del mismo nivel ejecuta una secuencia de tareas desde el Centro de software, y se reinicia en una imagen de arranque. Cuando el dispositivo está en Windows PE, usa la cuenta de acceso a la red para obtener contenido del origen de caché del mismo nivel.  

  - Cuando es necesario, el origen de caché del mismo nivel usa la cuenta de acceso a la red para autenticar las solicitudes de descarga de los elementos del mismo nivel. Esta cuenta solo requiere permisos de usuario de dominio para este propósito.  

- Con la versión 1802 y anteriores, el último envío de detección de latidos del cliente determina el límite actual de un origen de contenido de caché del mismo nivel. Es posible que un cliente que se desplace a otro grupo de límites siga siendo miembro de su grupo de límites anterior a efectos de la caché del mismo nivel. Este comportamiento da lugar a que se le ofrezca al cliente un origen de caché del mismo nivel que no está en su ubicación de red inmediata. No habilite los clientes móviles como origen de caché del mismo nivel.<!--SCCMDocs issue 641-->  

  > [!Important]  
  > A partir de la versión 1806, Configuration Manager es más eficaz a la hora de determinar si un origen de caché del mismo nivel se ha movido a otra ubicación. Este comportamiento garantiza que el punto de administración lo ofrezca como un origen de contenido a los clientes en la nueva ubicación y no en la ubicación antigua. Si usa la característica de caché del mismo nivel con orígenes de caché del mismo nivel en itinerancia, después de actualizar el sitio a la versión 1806, actualice también todos los orígenes de caché del mismo nivel a la última versión de cliente. El punto de administración no incluye estos orígenes de caché del mismo nivel en la lista de ubicaciones de contenido hasta que se actualicen al menos a la versión 1806.<!--SCCMDocs issue 850-->  

- Antes de intentar la descarga de contenido, el punto de administración valida en primer lugar si el origen de caché del mismo nivel está en línea.<!--sms.498675--> Esta validación se produce a través del "canal rápido" para la notificación de cliente, que usa el puerto TCP 10123.<!--511673-->  

> [!Note]  
> Para aprovechar las nuevas características de Configuration Manager, primero actualice los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a> Configuración de cliente de caché del mismo nivel

Para obtener más información sobre las opciones de cliente de caché del mismo nivel, vea [Configuración de la memoria caché del cliente](../../clients/deploy/about-client-settings.md#client-cache-settings). 

Para obtener más información sobre cómo configurar estas opciones, vea [Cómo configurar el cliente](../../clients/deploy/configure-client-settings.md).

En los clientes que admiten la caché del mismo nivel que usan el Firewall de Windows, Configuration Manager configura los puertos de firewall que se especifiquen en la configuración de cliente.



## <a name="partial-download-support"></a><a name="bkmk_parts"></a> Compatibilidad de descarga parcial
<!--1357346-->
A partir de la versión 1806, los orígenes de caché del mismo nivel de cliente ahora pueden dividir el contenido en partes. Estas partes reducen al mínimo la transferencia de red para usar menos WAN. El punto de administración proporciona un seguimiento más detallado de las partes de contenido e intenta eliminar más de una descarga del mismo contenido por grupo de límites. 


### <a name="example-scenario"></a>Escenario de ejemplo

Contoso tiene un único sitio primario con dos grupos de límites: oficina central y sucursal. Hay una relación de reserva de 30 minutos entre los grupos de límites. El punto de administración y el punto de distribución del sitio solo están en el límite de oficina central. La ubicación de la sucursal no tiene ningún punto de distribución local. Dos de los cuatro clientes de la sucursal están configurados como orígenes de caché del mismo nivel. 

![Diagrama de configuración de red descrita para el escenario de ejemplo](media/1357346-peer-cache-source-parts.png)

1. Su destino es una implementación con contenido para los cuatro clientes de la sucursal. Solo ha distribuido el contenido en el punto de distribución.  

2. El cliente 3 y el cliente 4 no tienen un origen local para la implementación. El punto de administración indica a los clientes que esperen 30 minutos antes de recurrir al grupo de límites remoto.  

3. El cliente 1 (PCS1) es el primer origen de caché del mismo nivel que actualiza la directiva con el punto de administración. Dado que este cliente está habilitado como un origen de caché del mismo nivel, el punto de administración le indica que inicie inmediatamente la descarga de la parte A desde el punto de distribución.  

4. Cuando el cliente 2 (PCS2) se pone en contacto con el punto de administración, como la parte A ya está en curso pero aún no se ha completado, el punto de administración indica que se inicie inmediatamente la descarga de la parte B desde el punto de distribución.  

5. PCS1 termina la descarga de la parte A y notifica inmediatamente al punto de administración. Como la parte B ya está en curso pero aún no se ha completado, el punto de administración le indica que empiece la descarga de la parte C desde el punto de distribución.  

6. PCS2 termina la descarga de la parte B y notifica inmediatamente al punto de administración. El punto de administración le indica que empiece a descargar la parte D desde el punto de distribución.  

7. PCS1 termina la descarga de la parte C y notifica inmediatamente al punto de administración. El punto de administración le informa de que ya no hay más partes disponibles en el punto de distribución remoto. El punto de administración le indica que descargue la parte B desde su elemento del mismo nivel local, PCS2.  

8. Este proceso continúa hasta que ambos orígenes de la memoria caché del mismo nivel de cliente obtienen todos los elementos el uno del otro. El punto de administración da prioridad a las partes procedentes del punto de distribución remoto antes de indicar a los orígenes de la memoria caché del mismo nivel que descarguen partes del elemento del mismo nivel local.  

9. El cliente 3 es el primero que actualiza la directiva después de expirar el período de reserva de 30 minutos. Ahora vuelve a comprobar con el punto de administración, que informa al cliente de que hay nuevos orígenes locales. En lugar de descargar el contenido por completo desde el punto de distribución a través de la WAN, descarga el contenido en su totalidad desde uno de los orígenes de caché del mismo nivel de cliente. Los clientes dan prioridad a los orígenes del mismo nivel local. 

> [!Note]  
> Si el número de orígenes de caché del mismo nivel de cliente es mayor que el número de partes de contenido, el punto de administración indica a los orígenes de caché del mismo nivel adicionales que esperen el tiempo de reserva, como un cliente normal. 


### <a name="configure-partial-download"></a>Configurar la descarga parcial

1. Configure los [grupos de límites](../../servers/deploy/configure/boundary-groups.md) y los orígenes de caché del mismo nivel de la forma normal.  

2. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda el nodo **Configuración del sitio** y haga clic en **Sitios**. Haga clic en **Configuración de jerarquía** en la cinta de opciones.  

3. En la pestaña **General**, habilite la opción **Configure client peer cache sources to divide content into parts** (Configurar orígenes de caché del mismo nivel de cliente para que dividan el contenido en partes).  

4. Cree una implementación requerida con contenido.  

   > [!Note]  
   > Esta característica solo funciona cuando el cliente descarga el contenido en segundo plano, como con una implementación requerida. Las descargas a petición, como cuando el usuario instala una implementación disponible en el Centro de software, se comportan como de costumbre.  

Para ver cómo controlan la descarga de contenido en partes, vea el **ContentTransferManager.log** en el origen de caché del mismo nivel de cliente y el **MP_Location.log** en el punto de administración.  



## <a name="guidance-for-cache-management"></a>Instrucciones para la administración de la caché
<!--510645-->
La caché del mismo nivel se basa en la caché del cliente de Configuration Manager para compartir contenido. Tenga en cuenta los aspectos siguientes para administrar la caché de cliente en su entorno:  

- La caché de cliente de Configuration Manager no es como la biblioteca de contenido de un punto de distribución. Aunque el contenido que se distribuye se administra en un punto de distribución, el cliente de Configuration Manager administra de forma automática el contenido en su caché. Hay configuraciones y métodos para ayudar a controlar el contenido que está en la caché de un origen de caché del mismo nivel. Para obtener más información, vea [Configurar la caché del cliente para clientes de Configuration Manager](../../clients/manage/manage-clients.md#BKMK_ClientCache).  

- El mantenimiento y el tamaño de caché normal se aplica a los orígenes de caché del mismo nivel. Para obtener más información, vea [Configurar el tamaño de la caché de cliente](../../clients/deploy/about-client-settings.md#configure-client-cache-size). Tenga en cuenta el tamaño del contenido más grande como los paquetes de actualización del sistema operativo o los archivos de actualización rápida de Windows 10. Compare la necesidad de este contenido con el espacio en disco disponible en los orígenes de caché del mismo nivel.  

- El cliente de origen de caché del mismo nivel actualiza la última vez a la que se hizo referencia al contenido en caché cuando un elemento del mismo nivel lo descarga. El cliente usa esta marca de tiempo cuando mantiene de forma automática su caché, y primero quita el contenido antiguo. Por tanto, debe esperar para quitar el contenido que los clientes de caché de mismo nivel descargan con más frecuencia, si lo hacen.  

- Si es necesario, durante una secuencia de tareas de implementación de sistema operativo, use la variable **SMSTSPreserveContent** para conservar el contenido en la caché del cliente. Para más información, vea [Task sequence variables](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent) (Variables de secuencia de tareas).  

- Si es necesario, al crear el software siguiente, use la opción **Conservar contenido en la memoria caché del cliente**:  
  - Aplicaciones
  - Paquetes
  - Imágenes de SO
  - Paquetes de actualización del sistema operativo
  - Imágenes de arranque



## <a name="monitoring"></a>monitoring   

Para ayudarle a entender el uso de la caché del mismo nivel, vea el panel **Orígenes de datos de cliente**. Para obtener más información, vea [Panel de orígenes de datos de cliente](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

Además, use los informes para ver el uso de la caché del mismo nivel. En la consola, vaya al área de trabajo **Supervisión**, expanda **Informes** y haga clic en el nodo **Informes**. Todos los informes siguientes tienen un tipo de **contenido de distribución de software**:  

1.  **Rechazo del contenido de origen de la caché del mismo nivel**: frecuencia con que los orígenes de la caché del mismo nivel de un grupo de límites rechazan una solicitud de contenido.  

    > [!Note]  
    > **Problema conocido**<!--486652-->: al explorar en profundidad resultados como *MaxCPULoad* o *MaxDiskIO*, es posible que reciba un error que sugiere que no se pueden encontrar el informe o los detalles. Como solución alternativa, use los otros dos informes en los que se muestran los resultados directamente.  

2. **Rechazo del contenido de origen de la caché del mismo nivel según la condición**: muestra los detalles de rechazo de un tipo de rechazo o grupo de límites específico. 

    > [!Note]  
    > **Problema conocido**<!--486652-->: no puede seleccionar entre los parámetros disponibles y, en su lugar, debe escribirlos manualmente. Escriba los valores de *Nombre del grupo de límites* y *Tipo de rechazo* tal como se muestra en el informe **Rechazo del contenido de origen de la caché del mismo nivel**. Por ejemplo, para *Tipo de rechazo* puede escribir *MaxCPULoad* o *MaxDiskIO*.  

3. **Detalles del rechazo del contenido de origen de la caché del mismo nivel**: muestra el contenido que el cliente solicitaba cuando se rechazó.  

    > [!Note]  
    > **Problema conocido**<!--486652-->: no puede seleccionar entre los parámetros disponibles y, en su lugar, debe escribirlos manualmente. Escriba el valor para *Tipo de rechazo* como se muestra en el informe **Rechazo del contenido de origen de la caché del mismo nivel**. Después, escriba el *Id. del recurso* para el origen de contenido sobre el que quiera obtener más información. 
    > 
    > Para buscar el identificador de recurso del origen de contenido:  
    > 
    > 1. Busque el nombre de equipo que se muestra como *Origen de caché del mismo nivel* en los resultados del informe **Rechazo del contenido de origen de la caché del mismo nivel por condición**.  
    > 
    > 2. Vaya al área de trabajo **Activos y compatibilidad**, haga clic en el nodo **Dispositivos** y busque el nombre de ese equipo. Utilice el valor de la columna de identificador de recurso.  

