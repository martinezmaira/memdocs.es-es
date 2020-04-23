---
title: Infraestructura de red
titleSuffix: Configuration Manager
description: Configure firewalls, puertos y dominios para preparar las comunicaciones de Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703093"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Consideraciones sobre la infraestructura de red para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para preparar la red a fin de admitir Configuration Manager, es posible que tenga que configurar algunos componentes de infraestructura. Por ejemplo, abra los puertos del firewall para pasar las comunicaciones que usa Configuration Manager.  

## <a name="ports-and-protocols"></a>Puertos y protocolos

Las distintas características de Configuration Manager usan distintos puertos de red. Algunos puertos son obligatorios y otros los puede personalizar.

La mayoría de las comunicaciones de Configuration Manager usan puertos comunes, como el puerto 80 para HTTP o el puerto 443 para HTTPS. Algunos roles de sistema de sitio permiten usar sitios web y puertos personalizados. Para más información, consulte [Sitios web para servidores de sistema de sitio](websites-for-site-system-servers.md).

Antes de implementar Configuration Manager, identifique los puertos que planea usar y configure los firewalls según sea necesario.

Después de instalar Configuration Manager, si necesita cambiar un puerto, no olvide actualizar los firewalls de los dispositivos y la red. Además, cambie la configuración del puerto en Configuration Manager.

Vea los siguientes artículos para más información:

- [Configurar puertos de comunicación de cliente](../../clients/deploy/configure-client-communication-ports.md)
- [Puertos usados en Configuration Manager](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>Requisitos de acceso a Internet

Algunas características de Configuration Manager se basan en la conectividad de Internet para obtener la funcionalidad completa. Si la organización restringe la comunicación de red con Internet mediante un dispositivo proxy o firewall, asegúrese de permitir los puntos de conexión necesarios.

Para más información, consulte los [requisitos de acceso a Internet](internet-endpoints.md).


## <a name="proxy-servers"></a>Servidores proxy

Puede especificar distintos servidores proxy para los diferentes clientes y servidores de sistema de sitio. Puede realizar estas configuraciones cuando instala un cliente o un rol de sistema de sitio, o bien cambiarlas más adelante en caso de ser necesario.

Para obtener más información, vea [Compatibilidad de servidor proxy](proxy-server-support.md).
