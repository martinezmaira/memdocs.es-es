---
title: Solución de problemas de referencia técnica de implementación de aplicaciones
titleSuffix: Configuration Manager
description: Referencia técnica para la solución de problemas de implementación de aplicaciones en Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688873"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Referencia técnica para la implementación de aplicaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo, aprenderá cómo funcionan las implementaciones de aplicaciones.

## <a name="before-you-begin"></a>Antes de empezar

A la hora de solucionar problemas de las implementaciones de aplicaciones, hay varios elementos que pueden serle útiles para revisar registros de cliente. Estos elementos incluyen:

- Identificador de CI de la aplicación
- Identificador único de la aplicación
- Identificador único del tipo de implementación
- Identificador único de la implementación de la aplicación (también conocido como identificador único de la asignación)
- Objetivo de la implementación de aplicaciones
- Identificador único de contenido
- Identificador y nombre de la recopilación
- Tipo de colección

Para simplificar la solución de problemas, puede ejecutar una consulta SQL similar a la siguiente en la base de datos de Configuration Manager para obtener la información enumerada anteriormente.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> Cuando ejecute esta consulta, **debe** usar el nombre de la aplicación que aparece en la pestaña "Información general" de las propiedades de la aplicación, en lugar de usar el nombre de aplicación localizado que aparece en la pestaña "Centro de software".

## <a name="next-steps"></a>Pasos siguientes

- [Directiva de implementación de aplicaciones](deployment-policy-technical-reference.md)
