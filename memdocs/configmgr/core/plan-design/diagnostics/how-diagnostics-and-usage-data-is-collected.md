---
title: Recopilación de datos de diagnóstico
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688473"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Recopilación de datos de diagnóstico y uso mediante Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para recopilar los datos de uso y diagnóstico para Configuration Manager, cada sitio primario ejecuta consultas de SQL Server con carácter semanal. En una jerarquía de varios sitio, los datos se replican en el sitio de administración central.  

En el sitio de nivel superior de una jerarquía, el punto de conexión de servicio envía esta información cuando busca actualizaciones. El modo del punto de conexión de servicio determina cómo se transfieren los datos:

- **En línea**: Una vez a la semana, el punto de conexión del servicio envía datos de diagnóstico y uso automáticamente al servicio en la nube.

- **Sin conexión**: Se transfieren manualmente los datos de diagnóstico y uso con la [herramienta de conexión de servicio](../../servers/manage/use-the-service-connection-tool.md).

Para obtener más información, consulte [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md) (Sobre el punto de conexión del servicio).

> [!div class="nextstepaction"]
> [Visualización de datos de diagnóstico y uso](view-diagnostics-and-usage-data.md)
