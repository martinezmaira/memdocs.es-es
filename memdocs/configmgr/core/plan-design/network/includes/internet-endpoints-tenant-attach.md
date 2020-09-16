---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 27436e7cd782ca910049007d52f37e2d7945f01e
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606249"
---
- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742-->

- `https://dc.services.visualstudio.com` <!--7541816-->

El punto de conexión de servicio realiza una conexión saliente de larga duración con el servicio de notificaciones hospedado en `https://*.manage.microsoft.com`. Compruebe que el proxy usado para el punto de conexión de servicio no agota demasiado rápido el tiempo de espera de las conexiones salientes. Para las conexiones salientes a este punto de conexión de Internet el tiempo recomendado son 3 minutos. <!--7820969-->