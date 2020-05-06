---
title: Solución de problemas de BitLocker
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo solucionar problemas con la administración de BitLocker en Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708613"
---
# <a name="troubleshoot-bitlocker"></a>Solución de problemas de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

Use la información de este artículo como ayuda para solucionar problemas con la administración de BitLocker en Configuration Manager.

## <a name="server-error-in-self-service"></a>Error de servidor en autoservicio

Al intentar abrir el portal de autoservicio (`https://webserver.contoso.com/SelfService`) por primera vez, verá el mensaje de error siguiente:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Para corregir este problema, asegúrese de que ha instalado el [requisito previo](../../plan-design/bitlocker-management.md#prerequisites) para **Microsoft ASP.NET MVC 4.0** en el servidor web.

## <a name="see-also"></a>Vea también

Para obtener más información sobre el uso de registros de eventos de BitLocker, vea [Registros de eventos de BitLocker](about-event-logs.md).

Para obtener una lista de los errores conocidos y las posibles causas de las entradas del registro de eventos, vea los artículos siguientes:

- [Registros de eventos de cliente](client-event-logs.md)
- [Registros de eventos de servidor](server-event-logs.md)

Para comprender por qué los clientes se notifican como no conformes con la directiva de administración de BitLocker, consulte [Códigos de no conformidad](non-compliance-codes.md).
