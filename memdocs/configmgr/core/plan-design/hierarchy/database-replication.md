---
title: Replicación de base de datos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo la replicación de base de datos de Configuration Manager utiliza SQL Server para transferir datos en la jerarquía.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b495b02-c966-4eb3-92b9-52ebbf5c38ae
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d1a2c8baa349e6499aa483f947d94f7459357be4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703603"
---
# <a name="database-replication"></a>Replicación de base de datos

*Se aplica a: Configuration Manager (rama actual)*

La replicación de base de datos de Configuration Manager utiliza SQL Server para transferir datos. Utiliza este método para combinar los cambios en su base de datos de sitio con la información de la base de datos de otros sitios de la jerarquía.

Tenga en cuenta los puntos siguientes sobre la replicación de base de datos:

- Todos los sitios comparten la misma información.  

- Cuando instala un sitio en una jerarquía, Configuration Manager establece automáticamente la replicación de base de datos entre el sitio nuevo y su sitio primario.  

- Cuando finaliza la instalación del sitio, se inicia automáticamente la replicación de base de datos.  

Si se agrega un nuevo sitio a una jerarquía, Configuration Manager crea una base de datos genérica en el nuevo sitio. El sitio primario crea una instantánea de los datos pertinentes en su base de datos. A continuación, transfiere la instantánea al nuevo sitio mediante la [replicación basada en archivos](file-based-replication.md). De este modo, el nuevo sitio usa un programa de copia masiva (BCP) de SQL Server para cargar la información en su copia local de la base de datos de Configuration Manager. Después de cargar la instantánea, cada sitio lleva a cabo la replicación de base de datos con el otro sitio.  

Para replicar datos entre sitios, Configuration Manager usa su propio servicio de replicación de base de datos. El servicio de replicación de base de datos usa el seguimiento de cambios de SQL Server para supervisar los cambios en la base de datos del sitio local. Luego, replica los cambios en los demás sitios mediante SQL Server Service Broker (SSB). De forma predeterminada, este proceso usa el puerto TCP 4022.  


## <a name="replication-groups"></a>Grupos de replicación

Configuration Manager agrupa los datos replicados mediante la replicación de base de datos en grupos de replicación diferentes. Cada grupo de replicación tiene una programación de replicación independiente y fija. El sitio usa esta programación para determinar la frecuencia con que replica los cambios en otros sitios.  

Por ejemplo, un cambio en una configuración de administración basada en roles se replica rápidamente en otros sitios. Con este comportamiento se garantiza que el otro sitio puede aplicar rápidamente estos cambios. Un cambio de configuración de menor prioridad, como una solicitud para instalar un sitio secundario nuevo, se replica con menos urgencia. Una solicitud de nuevo sitio puede tardar varios minutos en llegar al sitio primario de destino.  


## <a name="settings"></a>Configuración

Puede modificar la siguiente configuración para la replicación de base de datos:  

- **Vínculos de replicación de base de datos**: Controle cuándo el tráfico específico cruza la red.  

- **Vistas distribuidas**: cuando un sitio de administración central (CAS) solicita los datos del sitio seleccionados, puede acceder directamente a los datos desde la base de datos en un sitio primario secundario.  

- **Programaciones**: especifique cuándo se usa un vínculo de replicación y cuándo se replican distintos tipos de datos del sitio.  

- **Resumen**: Cambie la configuración de resumen de datos sobre el tráfico de red que cruza los vínculos de replicación. De forma predeterminada, el resumen se produce cada 15 minutos. Se usa en informes para la replicación de base de datos.  

- **Umbrales de replicación de base de datos**: defina cuándo el sitio informa vínculos como degradados o erróneos. También puede configurar en qué momento Configuration Manager genera alertas relativas a los vínculos de replicación que tienen un estado de degradado o con error.  


## <a name="types-of-data"></a>Tipos de datos

Configuration Manager clasifica principalmente los datos que replica como *datos globales* o *datos del sitio*. Cuando se produce la replicación de base de datos, el sitio transfiere los cambios a los datos globales y a los datos del sitio a través del vínculo de replicación de base de datos. Los datos globales se replican a un sitio primario o secundario. Los datos de sitio solo se replican en un sitio primario. Un tercer tipo de datos, los *datos locales*, no se replica a otros sitios. Los datos locales son información que los demás sitios no necesitan.  

### <a name="global-data"></a>Datos globales

Los datos globales son objetos creados por el administrador que se replican a todos los sitios de la jerarquía. Los sitios secundarios solo reciben un subconjunto de los datos globales, como los datos de proxy globales. Puede crear datos globales en el sitio CAS y el sitio primario. Este tipo incluye los datos siguientes:

- Implementaciones de software
- Actualizaciones de software
- Definiciones de colección
- Ámbitos de seguridad de administración basada en roles

### <a name="site-data"></a>Datos del sitio

Los datos del sitio son información operativa creada por los sitios primarios de Configuration Manager y sus clientes asignados. Los datos del sitio se replican al sitio CAS, pero no a otros sitios primarios. Los datos del sitio solo son visibles en el sitio CAS y en el sitio primario donde se originan los datos. Solo puede modificar los datos del sitio en el sitio primario donde los creó. Este tipo incluye los datos siguientes:

- Inventario de hardware
- Mensajes de estado
- Alertas
- Los resultados de las colecciones basadas en consultas

Todos los datos del sitio se replican en el sitio CAS. El sitio CAS realiza la administración y la generación de informes para toda la jerarquía de sitios.  


## <a name="database-replication-links"></a><a name="bkmk_Dblinks"></a> Vínculos de replicación de base de datos

Cuando se instala un nuevo sitio en una jerarquía, Configuration Manager crea automáticamente un vínculo de replicación de base de datos entre el sitio primario y el nuevo sitio. Crea un vínculo único para conectar ambos sitios.  

Para controlar la transferencia de datos a través del vínculo de replicación, cambie la configuración de cada vínculo. Cada vínculo de replicación es compatible con configuraciones independientes. Cada vínculo de replicación de base de datos incluye estos controles:  

- Detener la replicación de los datos del sitio seleccionados desde un sitio primario al sitio CAS. Esta acción hace que el CAS pueda acceder directamente a estos datos desde la base de datos del sitio primario.  

- Programar la transferencia de los datos del sitio seleccionados desde un sitio primario secundario al sitio CAS.

- Definir la configuración que determina cuándo un vínculo de replicación de base de datos tiene un estado degradado o erróneo.

- Especificar cuándo se generan alertas para un vínculo de replicación con errores.

- Especificar la frecuencia con que Configuration Manager resume los datos sobre el tráfico de replicación que usa el vínculo de replicación. Usa estos datos en los informes.

Para configurar un vínculo de replicación de base de datos, en la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Seleccione el nodo **Replicación de base de datos** y edite las propiedades del vínculo. Este nodo también está en el área de trabajo **Administración**, en el nodo **Configuración de jerarquía**. Edite un vínculo de replicación desde el sitio primario o el sitio secundario del vínculo de replicación.  

> [!TIP]  
> Es posible editar los vínculos de replicación de base de datos desde el nodo **Replicación de base de datos** en cualquier área de trabajo. Sin embargo, cuando usa el nodo **Replicación de base de datos** en el área de trabajo **Supervisión**, también puede ver el estado de la replicación de base de datos. También proporciona acceso a la herramienta [Replication Link Analyzer](../../servers/manage/monitor-replication.md#BKMK_RLA). Use esta herramienta para ayudar a investigar los problemas con la replicación de base de datos.  

Para más información sobre cómo configurar vínculos de replicación, consulte [Controles de replicación de base de datos del sitio](#BKMK_DBRepControls). Para más información sobre cómo supervisar la replicación, consulte [Supervisión de replicación de base de datos](../../servers/manage/monitor-replication.md).  


## <a name="distributed-views"></a><a name="bkmk_distviews"></a> Vistas distribuidas  

A través de las vistas distribuidas, cuando hace una solicitud al sitio CAS para los datos del sitio seleccionados, accede directamente a la base de datos del sitio primario secundario. Este acceso directo reemplaza la necesidad de replicar los datos del sitio desde el sitio primario al sitio CAS. Dado que cada vínculo de replicación es independiente de otros vínculos de replicación, se pueden usar las vistas distribuidas en los vínculos de replicación elegidos. No se pueden usar vistas distribuidas entre un sitio primario y un sitio secundario.  

Las vistas distribuidas proporcionan las ventajas siguientes:  

- Reducir la carga de la CPU para procesar los cambios de base de datos en el sitio CAS y el sitio primario.

- Reducir la cantidad de datos que se transfieren a través de la red al sitio CAS.

- Mejora del rendimiento de SQL Server que hospeda la base de datos del sitio CAS

- Reducir el espacio en disco que usa la base de datos del sitio CAS.

Considere la posibilidad de las vistas distribuidas cuando haya un sitio primario ubicado cerca del sitio CAS en la red, con los dos sitios siempre encendidos y siempre conectados. Las vistas distribuidas reemplazan la replicación de los datos seleccionados entre los sitios con conexiones directas entre los servidores SQL Server en cada sitio. Los sitios CAS establecen una conexión directa cada vez que se solicitan estos datos.

El sitio solicita los datos de las vistas distribuidas en estos escenarios de ejemplo:

- Cuando ejecuta informes o consultas.
- Cuando ve información en el Explorador de recursos.
- Cuando se realiza la evaluación de recopilación de las recopilaciones que incluyen reglas basadas en los datos del sitio.

De forma predeterminada, las vistas distribuidas están desactivadas para cada vínculo de replicación. Cuando activa las vistas distribuidas, puede seleccionar los datos del sitio que no se replican en el sitio CAS a través de ese vínculo. El sitio CAS accede directamente a estos datos desde la base de datos del sitio primario secundario que comparte el vínculo. Puede configurar los siguientes tipos de datos de sitio para las vistas distribuidas:  

- Datos de **inventario de hardware** de clientes.
- Datos de **inventario y de disponibilidad de software** de clientes.
- **Mensajes de estado** de clientes, el sitio primario y todos los sitios secundarios.

Cuando ve datos en la consola de Configuration Manager o en informes, las operaciones de las vistas distribuidas son invisibles para el usuario. Cuando se solicitan datos que están habilitados para las vistas distribuidas, el servidor de base de datos del sitio CAS accede directamente la base de datos del sitio primario secundario para recuperar la información.

Por ejemplo, se usa una consola de Configuration Manager conectada a CAS. Se solicita información sobre el inventario de hardware desde dos sitios primarios: ABC y XYZ. El inventario de hardware se habilitó solamente para las vistas distribuidas en el sitio ABC. El sitio CAS recupera la información de inventario para los clientes XYZ de su propia base de datos. El sitio CAS recupera la información de inventario para los clientes ABC directamente desde la base de datos en el sitio ABC. Esta información aparece en la consola de Configuration Manager o en un informe sin que se identifique el origen.  

Si un vínculo de replicación tiene un tipo de datos habilitado para las vistas distribuidas, el sitio primario secundario no replica esos datos en el sitio CAS. Cuando se desactivan las vistas distribuidas para un tipo de datos, el sitio primario secundario reanuda la replicación de los datos normal en el sitio CAS. Antes de que estos datos estén disponibles en el sitio CAS, los grupos de replicación para estos datos se deben reinicializar entre el sitio primario y el sitio CAS. Una vez que se desinstale un sitio primario que tenga activadas las vistas distribuidas, el sitio CAS deberá completar la reinicialización de sus datos antes de que se pueda acceder a los datos que se habilitó para las vistas distribuidas en el sitio CAS.  

> [!IMPORTANT]  
> Cuando se usan las vistas distribuidas en cualquier vínculo de replicación en la jerarquía de sitios, antes de desinstalar cualquier sitio primario, desactive las vistas distribuidas de todos los vínculos de replicación. Para obtener más información, consulte [Desinstalar un sitio primario configurado con vistas distribuidas](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews).  

### <a name="prerequisites-and-limitations-for-distributed-views"></a>Requisitos previos y limitaciones para las vistas distribuidas  

- Use solamente las vistas distribuidas en los vínculos de replicación entre un sitio CAS y un sitio primario.

- El sitio CAS debe usar la edición SQL Server Enterprise. El sitio primario no tiene este requisito.

- El sitio CAS solo puede tener una instancia del proveedor de SMS. Instale esa instancia única en el servidor de base de datos del sitio. Esta configuración admite la autenticación de Kerberos. La instancia de SQL Server en el sitio CAS necesita Kerberos para acceder a la instancia de SQL Server en el sitio primario secundario. No hay limitaciones en el proveedor de SMS del sitio primario secundario.

- Solo puede instalar un punto de servicios de informes en el sitio CAS. Instale SQL Server Reporting Services en el servidor de base de datos del sitio. Esta configuración admite la autenticación de Kerberos. La instancia de SQL Server en el sitio CAS necesita Kerberos para acceder a la instancia de SQL Server en el sitio primario secundario.

- No puede hospedar la base de datos del sitio en un [clúster de SQL Server](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).

- En la versión 1902 y versiones anteriores, no puede hospedar la base de datos del sitio en un [grupo de disponibilidad AlwaysOn de SQL Server](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md). Para admitir esta configuración, actualice a la versión 1906 o una versión posterior.<!-- SCCMDocs-pr#3792 -->

- La cuenta de equipo del servidor de bases de datos del sitio CAS requiere permisos de **lectura** en la base de datos del sitio primario.

> [!IMPORTANT]  
> Las vistas distribuidas y las [programaciones](#BKMK_schedules) de replicación de datos son configuraciones mutuamente exclusivas para un vínculo de replicación de base de datos.  


## <a name="schedule-transfers-of-site-data"></a><a name="BKMK_schedules"></a> Programación de transferencias de datos del sitio

Para ayudarlo a controlar el ancho de banda de red que se usa para replicar los datos del sitio desde un sitio primario secundario al sitio CAS, programe cuándo se usará un vínculo de replicación. A continuación, especifique cuándo se replican los distintos tipos de los datos del sitio. Es posible controlar cuándo el sitio primario va a replicar los mensajes de estado, el inventario y los datos de disponibilidad. Los vínculos de replicación de base de datos del sitio secundarios no son compatibles con programaciones para datos del sitio. No es posible programar la transferencia de los datos globales.  

Cuando se configura una programación del vínculo de replicación de base de datos, puede restringir la transferencia de los datos del sitio seleccionados desde el sitio primario al sitio CAS. También puede configurar distintas horas para replicar distintos tipos de datos del sitio.  

> [!IMPORTANT]  
> Las [vistas distribuidas](#bkmk_distviews) y las programaciones para los momentos en que se pueden replicar los datos son configuraciones mutuamente exclusivas para un vínculo de replicación de base de datos.  


## <a name="summarization-of-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> Resumen del tráfico  

Cada sitio resume regularmente los datos relativos al tráfico de red que cruza los vínculos de replicación de base de datos para el sitio. El sitio usa datos resumidos en los informes para la replicación de base de datos. Ambos sitios de un vínculo de replicación resumen el tráfico de red que recorre el vínculo de replicación. El servidor de base de datos del sitio resume los datos. Una vez que se resumen los datos, la información se replica a los otros sitios como datos globales.  

De forma predeterminada, el resumen se produce cada 15 minutos. Para modificar la frecuencia de resumen del tráfico de red, edite el **Intervalo de resumen** en las propiedades del vínculo de replicación de base de datos. La frecuencia de resumen afecta a la información que se ve en los informes sobre la replicación de base de datos. Puede elegir un intervalo de entre 5 a 60 minutos. Al aumentar la frecuencia de resumen, aumenta la carga de procesamiento en el servidor SQL Server de cada sitio del vínculo de replicación.  

## <a name="database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> Umbrales de replicación de base de datos

Los umbrales de replicación de base de datos definen cuando Configuration Manager informa del estado de un vínculo de replicación de base de datos como degradado o erróneo. De manera predeterminada, establece un vínculo como *degradado* cuando un grupo de replicación no puede completar la replicación durante doce intentos consecutivos. Establece el vínculo como *erróneo* cuando cualquier grupo de replicación no se puede replicar durante veinticuatro intentos consecutivos.  

Puede especificar valores predeterminados para el estado degradado o erróneo. Si ajusta estos valores, puede supervisar de manera más segura el estado de la replicación de base de datos a través de los vínculos.  

Uno o varios grupos de replicación no puedan replicar mientras que otros grupos de replicación se siguen replicando de manera correcta. Planee revisar el estado de replicación de un vínculo cuando se notifique por primera como degradado.

Considere la posibilidad de modificar los valores de reintento para el estado de degradado o con errores del vínculo en las situaciones siguientes:

- Hay retrasos periódicos para grupos de replicación específicos y su retraso no es un problema

- El vínculo de red entre sitios tiene poco ancho de banda disponible

Si aumenta el número de reintentos antes de que el sitio establezca el vínculo en degradado o con errores, se pueden eliminar los avisos falsos para los problemas conocidos. Esta acción permite realizar un seguimiento más preciso del estado del vínculo.  

Para comprender la frecuencia con la que se produce la replicación de ese grupo, debe tener en cuenta el intervalo de sincronización de replicación para cada grupo de replicación. Para ver el **intervalo de sincronización** de los grupos de replicación, vaya al área de trabajo **Supervisión** en la consola de Configuration Manager. En el nodo **Replicación de base de datos**, seleccione la pestaña **Detalle de la replicación** de un vínculo de replicación.  

Para más información sobre cómo supervisar la replicación de bases de datos, incluido cómo ver el estado de una replicación, consulte [Supervisión de la replicación de base de datos](../../servers/manage/monitor-replication.md).  


## <a name="site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> Controles de replicación de base de datos de sitio  

Para ayudarlo a controlar el ancho de banda de red que se usa para la replicación de base de datos, cambie la configuración de cada base de datos de sitio. Las opciones solo se aplican a la base de datos de sitio en la que se configuran las opciones. Las opciones siempre se usan cuando el sitio replica cualquier dato mediante replicación de base de datos en otro sitio.  

Puede modificar estos controles de replicación para cada base de datos de sitio:  

- El puerto SSB.  

- El período de tiempo de espera antes de que los errores de replicación provoquen que el sitio reinicialice su copia de la base de datos de sitio.  

- Comprima los datos que un sitio replica. Solamente comprime para transferirse entre sitios y no para almacenarse en la base de datos de cada sitio.  

Para cambiar la configuración de los controles de replicación de una base de datos de sitio, edite las propiedades de la base de datos en la consola de Configuration Manager, en el nodo **Replicación de base de datos**. Este nodo aparece en el nodo **Configuración de jerarquía** del área de trabajo **Administración** y también aparece en el área de trabajo **Supervisión**. Para editar las propiedades de la base de datos de sitio, seleccione el vínculo de replicación entre los sitios y, después, abra las **Propiedades de base de datos primaria** o las **Propiedades de base de datos secundaria**.  

> [!TIP]  
> Es posible configurar los controles de replicación de base de datos desde el nodo **Replicación de base de datos** en cualquier área de trabajo. No obstante, cuando se usa el nodo **Replicación de base de datos** en el área de trabajo **Supervisión**, también se puede ver el estado de la replicación de base de datos para un vínculo de replicación y acceder a la herramienta Replication Link Analyzer para investigar problemas de replicación.  


## <a name="see-also"></a>Vea también

[Supervisión de la replicación](../../servers/manage/monitor-replication.md)

[Solución de problemas de replicación de SQL](../../servers/manage/replication/overview.md)
