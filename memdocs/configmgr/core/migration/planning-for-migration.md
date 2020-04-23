---
title: Planeamiento de la migración
titleSuffix: Configuration Manager
description: Obtenga información sobre sitios y jerarquías antes de migrar datos a una jerarquía de destino de la rama actual de Configuration Manager.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702833"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Planeación de la migración a la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de migrar datos a una jerarquía de destino de la rama actual de Configuration Manager, asegúrese de estar familiarizado con las jerarquías y los sitios de Configuration Manager. Para más información sobre los sitios y las jerarquías, vea [Aspectos básicos de Configuration Manager](../../core/understand/fundamentals.md).  

Instale una jerarquía de la rama actual de Configuration Manager que sea la jerarquía de destino para poder migrar datos desde una jerarquía de origen admitida.  

Después de instalar la jerarquía de destino, configure las funciones y características de administración que quiera usar en la jerarquía de destino antes de empezar a migrar los datos.  

Además, tendrá que planear la superposición entre la jerarquía de origen y la jerarquía de destino. Por ejemplo, podría configurar la jerarquía de origen para usar los mismos límites o ubicaciones de red que la jerarquía de destino. Luego podría instalar nuevos clientes en la jerarquía de destino y usar la asignación automática de sitios. En este escenario, debido a que un cliente de Configuration Manager recién instalado puede seleccionar un sitio de cualquier jerarquía al que unirse, el cliente podría asignarse incorrectamente a su jerarquía de origen. Por lo tanto, planee la asignación de cada cliente nuevo en la jerarquía de destino a un sitio específico en dicha jerarquía en lugar de usar la asignación automática de sitios.  

Para más información sobre las asignaciones de sitio, vea [Consideraciones sobre la asignación de sitio de cliente](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) en [Interoperabilidad entre diferentes versiones de Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

Use los siguientes artículos para planear la migración de una jerarquía de origen a una jerarquía de destino de Configuration Manager:

-   [Requisitos previos para la migración](../../core/migration/prerequisites-for-migration.md)  

-   [Listas de comprobación del administrador para planear la migración](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determinar si se migrarán datos a la rama actual de Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planear una estrategia de jerarquía de origen](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Listas de comprobación del administrador para planear la migración](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planear una estrategia de migración de clientes](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planear una estrategia de migración de implementación de contenido](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planear la migración de objetos de Configuration Manager a la rama actual de Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planear la supervisión de la actividad de migración](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planear la finalización de la migración](../../core/migration/planning-to-complete-migration.md)  
