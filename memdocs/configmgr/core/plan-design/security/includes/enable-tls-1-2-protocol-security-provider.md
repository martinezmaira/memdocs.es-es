---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: f14713431c71c1f3625d13ea4be1d919b072e273
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704530"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 está habilitado de manera predeterminada. Por tanto, no es necesario modificar estas claves para habilitarlo. Puede realizar cambios en `Protocols` para deshabilitar TLS 1.0 y TLS 1.1 después de seguir el resto de las instrucciones de este artículo y de haber comprobado que el entorno funciona solo con TLS 1.2 habilitado.

Compruebe la configuración de la subclave del Registro `\SecurityProviders\SCHANNEL\Protocols`, tal como se muestra en [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).