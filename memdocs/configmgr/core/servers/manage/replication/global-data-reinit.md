---
title: Reinicialización de datos globales
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar la solución de problemas de reinicialización de la replicación de SQL para datos globales en una jerarquía de Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694303"
---
# <a name="troubleshoot-global-data-reinit"></a>Solución de problemas de reinicialización de datos globales

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](../../../plan-design/hierarchy/database-replication.md).

Use el siguiente diagrama para iniciar la solución de problemas de reinicialización (reinit) de la replicación de SQL para datos globales en una jerarquía de Configuration Manager:

![Diagrama para solucionar problemas de reinicialización de datos globales](media/global-data-reinit.svg)

## <a name="queries"></a>Consultas

En este diagrama se usan las siguientes consultas:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Comprobar si la replicación del sitio no ha finalizado la reinicialización

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Obtener el GUID de seguimiento y el estado desde el sitio primario

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Obtener el GUID de seguimiento y el estado desde CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>Comprobar el estado de la solicitud para el identificador de seguimiento

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Pasos siguientes

- [Mensaje de que falta reinicialización](reinit-missing-message.md)
