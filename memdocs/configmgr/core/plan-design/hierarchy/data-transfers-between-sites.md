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
ms.openlocfilehash: c3b74ceab892c67abbd56e8cb2a5c123374a92be
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663318"
---
# <a name="data-transfers-between-sites"></a>Transferencias de datos entre sitios

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager usa la *replicación basada en archivos* y la *replicación de base de datos* para transferir distintos tipos de información entre sitios. Obtenga información sobre cómo Configuration Manager mueve datos entre sitios y cómo se puede administrar la transferencia de datos a través de la red.  

## <a name="types-of-replication"></a>Tipos de replicación

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /></a> File-based replication

Configuration Manager usa la replicación basada en archivos para transferir datos basados en archivos entre sitios de la jerarquía. Estos datos incluyen las aplicaciones y los paquetes que quiere implementar en puntos de distribución de sitios secundarios. También controla los registros de datos de detección no procesados que el sitio transfiere a su sitio principal y que posteriormente procesa.  

Para más información, consulte [Replicación basada en archivos](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /></a> Database replication

La replicación de base de datos de Configuration Manager utiliza SQL Server para transferir datos. Utiliza este método para combinar los cambios en su base de datos de sitio con la información de la base de datos de otros sitios de la jerarquía.

Para más información, consulte [Replicación de la base de datos](database-replication.md).

Para ayuda con la solución de problemas de replicación de SQL, consulte [Solución de problemas de replicación de SQL](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Vea también

[Supervisión de la replicación](../../servers/manage/monitor-replication.md)
