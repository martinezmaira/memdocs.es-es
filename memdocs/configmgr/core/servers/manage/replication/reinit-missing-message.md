---
title: Mensaje de que falta reinicialización
titleSuffix: Configuration Manager
description: Use este diagrama para iniciar la solución de problemas de un mensaje que falta con la reinicialización de la replicación de SQL en Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703983"
---
# <a name="reinit-missing-message"></a>Mensaje de que falta reinicialización

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](../../../plan-design/hierarchy/database-replication.md).

Use el siguiente diagrama para iniciar la solución de problemas de un mensaje que falta con la reinicialización de la replicación de SQL (reinit):

![Diagrama para solucionar problemas de un mensaje que falta relacionado con la reinicialización](media/reinit-missing-message.svg)

## <a name="queries"></a>Consultas

En este diagrama se usan las siguientes consultas:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Comprobar si la replicación del sitio no ha finalizado la reinicialización

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>Obtener el GUID de seguimiento y el estado desde el sitio del suscriptor

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>Obtener el GUID de seguimiento y el estado desde el sitio de publicación

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Acciones correctivas

### <a name="version-1902-and-later"></a>Versión 1902 y posteriores

Para detectar el problema y reinicializar, ejecute [Replication Link Analyzer](../monitor-replication.md#BKMK_RLA).

### <a name="version-1810-and-earlier"></a>Versión 1810 y anteriores

Ejecute la siguiente consulta SQL para obtener `ReplicationGroupID`:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

A continuación, use el método `InitializeData` en la clase WMI `SMS_ReplicationGroup` con los valores siguientes:

- ReplicationGroupID: de la consulta SQL anterior
- SiteCode1: sitio primario
- SiteCode2: sitio secundario

Para más información, consulte [Método InitializeData en la clase SMS_ReplicationGroup](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md).

#### <a name="example"></a>Ejemplo

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Pasos siguientes

- [Reinicialización de replicación de SQL (reinit)](sql-replication-reinit.md)
