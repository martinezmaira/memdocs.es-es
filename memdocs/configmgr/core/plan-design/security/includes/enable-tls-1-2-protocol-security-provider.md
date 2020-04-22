---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704083"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 está habilitado de manera predeterminada. Por tanto, no es necesario modificar estas claves para habilitarlo. Puede realizar cambios en `Protocols` para deshabilitar TLS 1.0 y TLS 1.1 después de seguir el resto de las instrucciones de este artículo y de haber comprobado que el entorno funciona solo con TLS 1.2 habilitado.

Compruebe la configuración de la subclave del Registro `\SecurityProviders\SCHANNEL\Protocols`, tal como se muestra en [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

