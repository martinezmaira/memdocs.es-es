---
title: Migración de datos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo transferir datos desde una jerarquía de origen a una jerarquía de destino de Configuration Manager.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701753"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Migrar datos entre jerarquías en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Utilice la migración para transferir datos desde una jerarquía de origen compatible a la jerarquía de destino de Configuration Manager (rama actual). Al migrar datos desde una jerarquía de origen:  

- Acceda a los datos de las bases de datos de sitio de la infraestructura de origen y luego transfiera los datos a su entorno actual.  

- La migración no cambia los datos de la jerarquía de origen, sino que detecta los datos y almacena una copia en la base de datos de la jerarquía de destino.  

Tenga en cuenta los siguientes aspectos al planear su estrategia de migración:  

- Puede migrar una infraestructura existente de Configuration Manager 2007 SP2 a Configuration Manager (rama actual).  

- Puede migrar algunos de los datos compatibles (o todos) desde un sitio de origen.  

- Puede migrar los datos desde un sitio de origen único a varios sitios de la jerarquía de destino.  

- Puede mover datos desde varios sitios de origen a un único sitio de la jerarquía de destino.  


En el vídeo siguiente se analizan y muestran dos [escenarios de migración](#BKMK_MigrationScenarios) habituales. También se indican opciones para incluir Microsoft Azure en los planes de migración.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a> Conceptos  

 Configuration Manager usa los siguientes conceptos y términos durante la migración.  

#### <a name="source-hierarchy"></a>Jerarquía de origen
Una jerarquía que ejecuta una versión compatible de Configuration Manager y que tiene los datos que se van a migrar. Cuando se configura la migración, se identifica la jerarquía de origen al especificar el sitio de nivel superior de una jerarquía de origen. Después de especificar una jerarquía de origen, el sitio de nivel superior de la jerarquía de destino recopila datos de la base de datos del sitio de origen designado para identificar los datos que desea migrar. 

Para obtener más información, consulte [Jerarquías de origen](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Sitios de origen
Son los sitios en la jerarquía de origen que tienen los datos que puede migrar a su jerarquía de destino. 

Para obtener más información, consulte [Sitios de origen](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Jerarquía de destino
Una jerarquía de Configuration Manager (rama actual) en la que se ejecuta la migración para importar datos de una jerarquía de origen.

#### <a name="data-gathering"></a>Recopilación de datos
Es el proceso continuo de identificar la información en una jerarquía de origen que se pueden migrar a la jerarquía de destino. Configuration Manager comprueba la jerarquía de origen según una programación. Este proceso identifica cambios en la información de la jerarquía de origen que se migró anteriormente y que puede querer actualizar en la jerarquía de destino.

Para obtener más información, consulte [Recopilación de datos](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Trabajos de migración
El proceso de configuración de los objetos que se desea migrar y la posterior administración de la migración de dichos objetos a la jerarquía de destino.

Para obtener más información, consulte [Planear una estrategia de trabajo de migración](planning-a-migration-job-strategy.md).

#### <a name="client-migration"></a>Migración de clientes
El proceso de transferencia de información que los clientes usan desde la base de datos del sitio de origen hasta la base de datos de la jerarquía de destino. Esta migración de datos va seguida de una actualización del software cliente de dispositivos a la versión del software cliente de la jerarquía de destino.

Para obtener más información, consulte [Planear una estrategia de migración de clientes](planning-a-client-migration-strategy.md).

#### <a name="shared-distribution-points"></a>Puntos de distribución compartidos
Los puntos de distribución de la jerarquía de origen que Configuration Manager comparte con la jerarquía de destino durante la migración.

Durante la migración, los clientes asignados a sitios en la jerarquía de destino pueden obtener contenido de los puntos de distribución compartidos.

Para obtener más información, consulte[Compartir puntos de distribución entre jerarquías de origen y de destino](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Supervisión de la migración
Es el proceso de supervisión de las actividades de migración. Debe supervisar el progreso y la correcta finalización de la migración desde el nodo **Migración** en el área de trabajo **Administración**.

Para obtener más información, consulte [Planear la supervisión de la actividad de migración](planning-to-monitor-migration-activity.md).

#### <a name="stop-gathering-data"></a>Detener la recopilación de datos
Es el proceso de detener la recopilación de datos de sitios de origen. Cuando ya no hay datos de una jerarquía de origen que quiere migrar, o si quiere pausar las actividades relacionadas con la migración, puede configurar la jerarquía de destino para que deje de recopilar datos de la jerarquía de origen.

Para obtener más información, consulte [Recopilación de datos](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Limpiar datos de migración
Es el proceso de finalización de la migración de una jerarquía de origen mediante la eliminación de la información sobre la migración de la base de datos de las jerarquías de destino.

Para obtener más información, consulte [Planear la finalización de la migración](planning-to-complete-migration.md).



## <a name="typical-workflow"></a>Flujo de trabajo típico  

Para configurar un flujo de trabajo para la migración:

1.  Especifique una jerarquía de origen compatible.  

2.  Configure la recopilación de datos. La recopilación de datos permite a Configuration Manager recopilar información sobre los datos que se pueden migrar desde la jerarquía de origen.  

     Configuration Manager automáticamente repite el proceso para recopilar datos según una programación simple hasta que detenga el proceso de recopilación de datos. De forma predeterminada, el proceso de recopilación de datos se repite cada cuatro horas para que Configuration Manager pueda identificar cambios en los datos de la jerarquía de origen. La recopilación de datos también es necesaria para compartir puntos de distribución.  

3.  Cree trabajos de migración para migrar datos entre la jerarquía de origen y la jerarquía de destino.  

4.  Puede detener la recopilación de datos en cualquier momento con la acción **Detener la recopilación de datos**. Cuando se detiene la recopilación de datos, Configuration Manager deja de identificar cambios en los datos de la jerarquía de origen y no podrá seguir compartiendo puntos de distribución. Normalmente, se usa esta acción cuando ya no va a migrar datos o a compartir puntos de distribución de la jerarquía de origen.  

5.  Opcionalmente, después de detener la recopilación de datos de todos los sitios de la jerarquía de origen, puede limpiar los datos de migración con la acción **Limpiar datos de migración**. Esta acción elimina datos históricos de migración de una jerarquía de origen de la base de datos de la jerarquía de destino.  

Después de migrar los datos, si ya no necesita la jerarquía de origen para administrar los dispositivos de su entorno, puede retirar dicha jerarquía y dicha infraestructura.  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a>Escenarios  

 Configuration Manager admite los siguientes escenarios de migración:
- [Migración de jerarquías de Configuration Manager 2007](#bkmk_2007)  
- [Migración desde Configuration Manager 2012 o desde otra jerarquía de Configuration Manager](#bkmk_2012)

> [!NOTE]  
>  La expansión de una jerarquía que tiene un sitio independiente a una jerarquía que tiene un sitio de administración central no se considera una migración. Para obtener información sobre la expansión de jerarquías, consulte [Expandir un sitio primario independiente](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a> Migración de jerarquías de Configuration Manager 2007  

 Cuando usa la migración para migrar datos desde Configuration Manager 2007, puede mantener la inversión en la infraestructura de sitio existente y obtener las ventajas siguientes:  

#### <a name="site-database-improvements"></a>Mejoras de la base de datos del sitio
La base de datos de Configuration Manager (rama actual) es totalmente compatible con Unicode.

#### <a name="database-replication-between-sites"></a>Replicación de base de datos entre sitios
La replicación en Configuration Manager (rama actual) se basa en Microsoft SQL Server. Este comportamiento mejora el rendimiento de la transferencia de datos entre sitios.

#### <a name="user-centric-management"></a>Administración centrada en el usuario
Los usuarios son el centro de las tareas de administración de Configuration Manager (rama actual). Por ejemplo, puede distribuir software a un usuario incluso si no conoce el nombre del dispositivo para ese usuario. Además, Configuration Manager proporciona a los usuarios un mayor control sobre el software que se instala en los dispositivos y cuándo se instala dicho software.

#### <a name="hierarchy-simplification"></a>Simplificación de la jerarquía
Configuration Manager (rama actual) le permite crear una jerarquía de sitio más sencilla. Esta mejora se debe a la introducción del tipo de sitio de administración central y a los cambios efectuados en el comportamiento de los sitios primarios y secundarios. Configuration Manager (rama actual) usa menos ancho de banda y necesita menos servidores que en las versiones anteriores.

#### <a name="role-based-administration"></a>Administración basada en roles
Este modelo de seguridad central de Configuration Manager (rama actual) ofrece seguridad y administración a nivel de jerarquía según sus requisitos administrativos y empresariales.

> [!NOTE]  
>  Debido a los cambios de diseño que se introdujeron en System Center 2012 Configuration Manager, no puede actualizar Configuration Manager 2007 a Configuration Manager (rama actual). Se admite la actualización in situ de System Center 2012 Configuration Manager a Configuration Manager (rama actual).  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a> Migración desde Configuration Manager 2012 o desde otra jerarquía de Configuration Manager  
 El proceso de migración de datos de una jerarquía de System Center 2012 Configuration Manager o Configuration Manager es el mismo. Este proceso incluye la migración de datos de varias jerarquías de origen en una única jerarquía de destino. Puede aplicar este proceso cuando su compañía adquiera recursos adicionales que ya estén administrados por Configuration Manager. Además, puede migrar datos de un entorno de prueba a un entorno de producción de Configuration Manager. Este proceso le permite mantener su inversión en el entorno de prueba de Configuration Manager.  



## <a name="see-also"></a>Vea también  

-   [Planear la migración a Configuration Manager](planning-for-migration.md)  

-   [Configurar jerarquías de origen y sitios de origen para la migración](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operaciones de migración](operations-for-migration.md)  

-   [Seguridad y privacidad de la migración](security-and-privacy-for-migration.md)  

-   [Comenzar a usar Configuration Manager](../servers/deploy/start-using.md)
