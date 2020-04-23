---
title: Transferencias de datos entre sitios
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703623"
---
# <a name="data-transfers-between-sites"></a>Transferencias de datos entre sitios

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager usa la *replicación basada en archivos* y la *replicación de base de datos* para transferir distintos tipos de información entre sitios. Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.  

## <a name="types-of-replication"></a>Tipos de replicación

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /> Replicación basada en archivos

Configuration Manager usa la replicación basada en archivos para transferir datos basados en archivos entre sitios de la jerarquía. Estos datos incluyen las aplicaciones y los paquetes que quiere implementar en puntos de distribución de sitios secundarios. También controla los registros de datos de detección no procesados que el sitio transfiere a su sitio principal y que posteriormente procesa.  

Para más información, consulte [Replicación basada en archivos](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /> Replicación de base de datos

La replicación de base de datos de Configuration Manager utiliza SQL Server para transferir datos. Utiliza este método para combinar los cambios en su base de datos de sitio con la información de la base de datos de otros sitios de la jerarquía.

Para más información, consulte [Replicación de la base de datos](database-replication.md).

Para ayuda con la solución de problemas de replicación de SQL, consulte [Solución de problemas de replicación de SQL](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Vea también

[Supervisión de la replicación](../../servers/manage/monitor-replication.md)
