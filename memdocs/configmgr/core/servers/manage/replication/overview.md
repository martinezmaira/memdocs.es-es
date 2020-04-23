---
title: Solución de problemas de replicación de SQL
titleSuffix: Configuration Manager
description: Use estos diagramas para ayudar a comprender y solucionar problemas de la replicación de SQL entre sitios Configuration Manager
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703993"
---
# <a name="troubleshoot-sql-replication"></a>Solución de problemas de replicación de SQL

En una jerarquía de varios sitios, Configuration Manager usa la replicación de SQL para transferir datos entre sitios. Para más información, consulte [Replicación de la base de datos](../../../plan-design/hierarchy/database-replication.md).

Para comprender mejor al solución de problemas con la replicación de SQL, use estos diagramas.

- [Replicación de SQL](sql-replication.md)
- [Configuración de SQL](sql-configuration.md)
- [Rendimiento de SQL](sql-performance.md)
- [Reinicialización de replicación de SQL (reinit)](sql-replication-reinit.md)
- [Reinicialización de datos globales](global-data-reinit.md)
- [Reinicialización de datos de sitio](site-data-reinit.md)
- [Mensaje de que falta reinicialización](reinit-missing-message.md)

Estos diagramas de solución de problemas están interconectados. Use el siguiente diagrama para entender sus relaciones:

![Diagrama de información general del proceso para solucionar problemas de replicación de SQL](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Para más información, vea la siguiente serie de blogs de Soporte técnico de Microsoft:

- [Mecanismos de sincronización de DRS de Configuration Manager](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [Servicio de replicación de datos (DRS) de Configuration Manager 2012 sin límites](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [DRS de Configuration Manager 2012: preguntas más frecuentes sobre la solución de problemas](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [Mecanismos de inicialización de DRS de Configuration Manager 2012](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [Configuration Manager 2012: problemas de certificado de SQL Server Service Broker y DRS](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
