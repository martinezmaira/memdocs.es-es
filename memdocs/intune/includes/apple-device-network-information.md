---
title: archivo include
description: Archivo de inclusión
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347273"
---
## <a name="apple-device-network-information"></a>Información de red de dispositivos de Apple

|**Se usa para**|**Nombre de host (dirección IP/subred)**|**Protocolo**|**Puerto**|
|------------|-----------|------------|-----------|
|Recuperación y visualización de contenido de los servidores de Apple|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|Comunicación con servidores APNS|#-courier.push.apple.com<br>"#" es un número aleatorio entre 0 y 50.|TCP|5223 y 443|
|Distintas funciones, como acceso a Internet, iTunes Store, App Store de macOS, iCloud, mensajería, etc.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 o 443|

Para obtener más información, vea:

- [Puertos TCP y UDP usados por los productos de software de Apple](https://support.apple.com/HT202944)
- [Acerca de los procesos en segundo plano de iTunes y las conexiones del host para el servidor de iTunes, iOS/iPadOS y macOS](https://support.apple.com/HT201999)
- [Si tus clientes macOS e iOS/iPadOS no reciben notificaciones push de Apple](https://support.apple.com/HT203609)