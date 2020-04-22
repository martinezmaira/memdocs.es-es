---
title: Supervisión de la jerarquía
titleSuffix: Configuration Manager
description: Aprenda a supervisar la infraestructura en Configuration Manager mediante el área de trabajo Supervisión de la consola.
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66fc6744ef7d1aaf90a5e7339cc9a5174c0d33f6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694403"
---
# <a name="monitor-the-hierarchy"></a>Supervisión de la jerarquía

*Se aplica a: Configuration Manager (rama actual)*

Para supervisar la jerarquía en Configuration Manager, use el área de trabajo **Supervisión** en la consola de Configuration Manager.  

> [!NOTE]  
> La excepción a esta ubicación es al migrar los sitios. Se ha supervisado este proceso en el nodo **Migración** del área de trabajo **Administración**. Para más información, vea [Operaciones para migrar a la rama actual de Configuration Manager](../../migration/operations-for-migration.md).  

Junto con el uso de la consola de Configuration Manager para la supervisión, use las siguientes características:

- [Introducción a los informes](introduction-to-reporting.md)
- [Archivos de registro](../../plan-design/hierarchy/log-files.md).  

Al supervisar los sitios, busque signos que indiquen problemas que requiera que realice una acción. Por ejemplo:  

- Un trabajo pendiente de archivos en servidores de sitios y sistemas de sitio.  

- Mensajes de estado que indican un error o un problema.  

- Error en la comunicación dentro de un sitio.  

- Mensajes de error y de advertencia en el registro de eventos del sistema en servidores.  

- Mensajes de error y de advertencia en el registro de errores de Microsoft SQL Server.  

- Sitios o clientes que no han informado del estado desde hace tiempo.  

- Respuesta lenta de la base de datos de SQL Server.  

- Indicios de errores de hardware.  

Si las tareas de supervisión revelan cualquier síntoma de problema, investigue el origen del problema. A continuación, repárelo rápidamente para minimizar el riesgo de un error del sitio.  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a> Supervisión de tareas comunes de administración

Configuration Manager proporciona supervisión integrada desde la propia consola de Configuration Manager.

### <a name="alerts"></a>Alertas

Para más información, vea [Supervisar alertas](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts).  

### <a name="compliance-settings"></a>Configuración de cumplimiento

Para obtener más información, consulte [How to monitor compliance settings](../../../compliance/deploy-use/monitor-compliance-settings.md) (Cómo supervisar la configuración de cumplimiento).

### <a name="content"></a>Content

Para más información sobre la supervisión de contenido, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../deploy/configure/manage-content-and-content-infrastructure.md).  

Para información sobre la supervisión de los tipos específicos de contenido:

- [Supervisar aplicaciones](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Supervisar paquetes y programas](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Supervisar el contenido de las actualizaciones de software](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [Supervisar el contenido de las implementaciones del sistema operativo](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Endpoint Protection

Para más información, vea [Cómo supervisar el estado de Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).  

### <a name="os-deployment"></a>Implementación del sistema operativo

Para más información, vea [Supervisar las implementaciones de sistema operativo en System Center Configuration Manager](../../../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="monitor-power-management"></a>Supervisión de la administración de energía

Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](../../clients/manage/power/monitor-and-plan-for-power-management.md).  

### <a name="monitor-software-metering"></a>Supervisión de la medición de software

Para más información, consulte [Medición de software en System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

### <a name="monitor-software-updates"></a>Supervisar actualizaciones de software

Para obtener más información, consulte [Monitor software updates](../../../sum/deploy-use/monitor-software-updates.md) (Supervisión de las actualizaciones de software).  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a> Supervisión de jerarquías de sitio

El nodo **Jerarquía del sitio** del área de trabajo **Supervisión** proporciona una visión general de la jerarquía de Configuration Manager y de los vínculos entre sitios. Puede utilizar dos vistas:  

- **Diagrama de jerarquía**: muestra la jerarquía como un mapa topológico simplificado que solo muestra la información esencial. Para más información, consulte [Diagrama de jerarquía](#hierarchy-diagram).  

- **Vista geográfica**: presenta los sitios en un mapa geográfico que muestra las ubicaciones de sitios que configure. Para más información, consulte [Vista geográfica](#geographical-view).  

Use el nodo **Jerarquía del sitio** para supervisar el estado de cada sitio. Supervise también los vínculos de replicación entre sitios y su relación con factores externos, como una ubicación geográfica.  

El estado del sitio y el estado del vínculo entre sitios se replican como datos de sitio y no como datos globales. Cuando conecte la consola de Configuration Manager a un sitio primario secundario, no podrá ver el estado del sitio ni del vínculo para otros sitios primarios ni para sus sitios secundarios. Por ejemplo, en una jerarquía con varios sitios primarios, cuando conecta la consola a un sitio primario, puede ver el estado de los sitios secundarios, el sitio primario y el sitio de administración central. Desde esta vista, no puede ver el estado de otros sitios debajo del sitio de administración central.  

Para controlar la visualización en el nodo **Jerarquía del sitio**, use la acción **Definir configuración**. La jerarquía Replica la configuración que se configura en este nodo.  

### <a name="hierarchy-diagram"></a>Diagrama de jerarquía

El diagrama de jerarquía muestra los sitios en un mapa de topología. Seleccione un sitio y vea un resumen de mensajes de estado de ese sitio. Obtener detalles para ver los mensajes de estado y acceda a las **propiedades** del sitio.  

Para ver el estado de alto nivel para un vínculo de sitio o de replicación entre sitios, pause el puntero del mouse sobre el objeto. El estado del vínculo de replicación no se replica globalmente. Para ver el vínculo de replicación entre todos los sitios primarios de una jerarquía, conecte la consola al sitio de administración central.  

Las siguientes opciones modifican el diagrama de jerarquía:  

#### <a name="groups"></a>Grupos

Configure el número de sitios primarios y secundarios que desencadenan un cambio en el diagrama de jerarquía. Este cambio en la visualización combina los sitios en un solo objeto. Después, verá el número total de sitios y un resumen de alto nivel de mensajes de estado y estado de sitio. Las configuraciones de grupo no afectan a la vista geográfica.  

#### <a name="favorite-sites"></a>Sitios favoritos

Especifique los sitios individuales como sitios favoritos. Un icono de estrella identifica un sitio favorito en el diagrama de jerarquía. Los sitios favoritos no se combinan con otros sitios cuando se utilizan grupos. Siempre se muestran de forma individual.  

### <a name="geographical-view"></a>Vista geográfica

La vista geográfica muestra la ubicación de cada sitio en un mapa geográfico. Solo muestra los sitios que configure con una ubicación. Cuando seleccione un sitio en esta vista, muestra los vínculos de replicación a sitios primarios o secundarios. A diferencia de la vista Diagrama de jerarquía, en esta vista no puede mostrar mensajes de estado del sitio ni detalles del vínculo de replicación.  

> [!NOTE]  
> Para usar la vista geográfica, el equipo al que se conecte la consola de Configuration Manager deberá tener instalado Internet Explorer y poder acceder a Mapas de Bing mediante el protocolo HTTP.  

La siguiente opción modifica la vista geográfica:  

#### <a name="site-location"></a>Ubicación del sitio

Especifique una ubicación geográfica para cada sitio mediante uno de los siguientes tipos:

- Una dirección
- Un nombre de lugar como el nombre de una ciudad
- Por las coordenadas de latitud y longitud

Por ejemplo, para usar la latitud y longitud de Redmond (Washington, EE.UU.), especifique **N 47 40 26.3572 O 122 7 17.4432** como ubicación del sitio. No es necesario especificar los símbolos de grado, minutos o segundos de la latitud ni la longitud. Configuration Manager usa Mapas de Bing para mostrar la ubicación en la vista geográfica. A continuación, puede ver la jerarquía con las ubicaciones geográficas. Esta vista proporciona información sobre los problemas regionales que pueden afectar a sitios específicos o a la replicación entre sitios.  

Cuando se especifica una ubicación, puede utilizar el cuadro **Ubicación** para buscar un sitio específico en la jerarquía. Con el sitio seleccionado, introduzca la ubicación como nombre de la ciudad o dirección postal en la columna **Ubicación** . Configuration Manager utiliza Mapas de Bing para resolver la ubicación.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>Pasos siguientes

[Supervisión de la replicación de base de datos](monitor-replication.md)
