---
title: Procedimientos para habilitar Seguridad de la capa de transporte (TLS) 1.2 en los clientes
titleSuffix: Configuration Manager
description: Información sobre cómo habilitar TLS 1.2 para clientes de Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704113"
---
# <a name="how-to-enable-tls-12-on-clients"></a>Procedimientos para habilitar TLS 1.2 en clientes

*Se aplica a: Configuration Manager (rama actual)*

Al habilitar TLS 1.2 para el entorno de Configuration Manager, asegúrese primero de que los clientes sean compatibles y estén correctamente configurados para usar TLS 1.2 antes de habilitarlo y deshabilitar los protocolos antiguos en los servidores y sistemas de sitios remotos. Hay tres tareas para habilitar TLS 1.2 en los clientes:

- Actualización de Windows y WinHTTP
- Comprobación de que TLS 1.2 está habilitado como protocolo para SChannel en el nivel de sistema operativo
- Actualización y configuración de .NET Framework para admitir TLS 1.2

Para obtener más información sobre las dependencias de características y escenarios específicos de Configuration Manager, vea [Habilitación de TLS 1.2](enable-tls-1-2.md).

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a> Actualización de Windows y WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 y las versiones posteriores de Windows admiten de forma nativa TLS 1.2 para las comunicaciones cliente-servidor a través de WinHTTP. 

Las versiones anteriores de Windows, como Windows 7 o Windows Server 2012, no habilitan TLS 1.1 ni 1.2 de manera predeterminada para las comunicaciones seguras mediante WinHTTP. En el caso de estas versiones anteriores de Windows, instale la [Actualización 3140245](https://support.microsoft.com/help/3140245) para habilitar el valor del Registro siguiente, que se puede establecer para agregar TLS 1.1 y TLS 1.2 a la lista de protocolos seguros predeterminados para WinHTTP. Con la revisión instalada, cree los valores del Registro siguientes:

> [!IMPORTANT]
> Habilite esta configuración en todos los clientes que ejecutan versiones anteriores de Windows *antes*  de habilitar TLS 1.2 y deshabilitar los protocolos antiguos en los servidores de Configuration Manager. En caso contrario, puede dejarlos huérfanos sin darse cuenta.

Compruebe el valor de la configuración del Registro `DefaultSecureProtocols`, por ejemplo:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Si cambia este valor, reinicie el equipo.

El ejemplo anterior muestra el valor de `0xAA0` para el parámetro `DefaultSecureProtocols` de WinHTTP. [KB 3140245: Actualización para habilitar TLS 1.1 y 1.2 como protocolos seguros predeterminados de WinHTTP en Windows](https://support.microsoft.com/help/3140245) muestra el valor hexadecimal de cada protocolo. De forma predeterminada en Windows, este valor es `0x0A0` para habilitar SSL 3.0 y TLS 1.0 para WinHTTP. En el ejemplo anterior se mantienen estos valores predeterminados, y se habilitan también TLS 1.1 y TLS 1.2 para WinHTTP. Esta configuración garantiza que el cambio no interrumpe ninguna otra aplicación que todavía podría depender de SSL 3.0 o TLS 1.0. Puede usar el valor de `0xA00` para habilitar solo TLS 1.1 y TLS 1.2. Configuration Manager admite el protocolo más seguro que Windows negocia entre ambos dispositivos.

 Si desea deshabilitar SSL 3.0 y TLS 1.0 por completo, use el parámetro de los protocolos deshabilitados de SChannel en Windows. Para obtener más información, consulte el artículo sobre [cómo restringir el uso de ciertos algoritmos criptográficos y protocolos en Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> Comprobación de que TLS 1.2 está habilitado como protocolo para SChannel en el nivel de sistema operativo

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> Actualización y configuración de .NET Framework para admitir TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Pasos siguientes

- [Habilitación de TLS 1.2 en servidores y sistemas de sitios remotos](enable-tls-1-2-server.md)
- [Problemas habituales al habilitar TLS 1.2](enable-tls-1-2-troubleshoot.md)

