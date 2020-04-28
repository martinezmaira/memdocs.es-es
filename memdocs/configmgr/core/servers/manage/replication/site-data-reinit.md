---
title: Reinicialización de datos de sitio
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar la solución de problemas de reinicialización de la replicación de SQL para datos de sitio en una jerarquía de Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078604"
---
# <a name="troubleshoot-site-data-reinit"></a>Solución de problemas de reinicialización de datos de sitio

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](../../../plan-design/hierarchy/database-replication.md).

Use el siguiente diagrama para iniciar la solución de problemas de reinicialización (reinit) de la replicación de SQL para datos de sitio en una jerarquía de Configuration Manager:

![Diagrama para solucionar problemas de reinicialización de datos de sitio](media/site-data-reinit.svg)

## <a name="queries"></a>Consultas

En este diagrama se usan las siguientes consultas:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Comprobar si la replicación del sitio no ha finalizado la reinicialización

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Obtener el GUID de seguimiento y el estado desde CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Obtener el GUID de seguimiento y el estado desde el sitio primario

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Comprobar que el sitio primario no está en modo de mantenimiento

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>Comprobar el estado de la solicitud para el identificador de seguimiento

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Pasos siguientes

- [Mensaje de que falta reinicialización](reinit-missing-message.md)
- [Reinicialización de datos globales](global-data-reinit.md)
