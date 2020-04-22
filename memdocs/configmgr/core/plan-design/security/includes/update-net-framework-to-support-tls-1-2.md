---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: b21365d0c355adab6819e13537c1b25316583ec2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704093"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>Determinación de la versión de .NET

En primer lugar, determine las versiones instaladas de .NET. Para obtener más información, consulte el artículo sobre [cómo determinar qué versiones y niveles de Service Pack de Microsoft .NET Framework están instalados](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Instalación de actualizaciones de .NET

Instale las actualizaciones de .NET para poder habilitar la criptografía segura. Algunas versiones de .NET Framework pueden requerir actualizaciones para habilitar la criptografía segura. Use estas instrucciones:

- .NET Framework 4.6.2 y versiones posteriores admite TLS 1.1 y TLS 1.2. Confirme la configuración del Registro, pero no se requiere ningún cambio adicional.

- Actualice .NET Framework 4.6 y versiones anteriores para admitir TLS 1.1 y TLS 1.2. Para obtener más información, vea [Versiones y dependencias de .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Si usa .NET Framework 4.5.1 o 4.5.2 en Windows 8.1 o Windows Server 2012, las actualizaciones importantes y otros detalles también están disponibles en el [Centro de descarga](https://www.microsoft.com/download/details.aspx?id=42883).


### <a name="configure-for-strong-cryptography"></a>Configuración de la criptografía segura

Configure .NET Framework para admitir criptografía segura. Establezca la configuración `SchUseStrongCrypto` del registro en `DWORD:00000001`. Este valor deshabilita el cifrado de flujo RC4 y requiere reiniciar. Para más información sobre esta configuración, consulte el [aviso de seguridad de Microsoft 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Asegúrese de establecer las siguientes claves del Registro en cualquier equipo que se comunique a través de la red con un sistema habilitado para TLS 1.2. Por ejemplo, los clientes de Configuration Manager, los roles de sistema de sitio remoto que no estén instalados en el servidor de sitio y el propio servidor de sitio.

Para las aplicaciones de 32 bits que se ejecutan en sistemas operativos de 32 bits o las de 64 bits que se ejecutan en sistemas operativos de 64 bits, actualice los valores de subclave siguientes:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

En el caso de las aplicaciones de 32 bits que se ejecutan en sistemas operativos de 64 bits, actualice los valores de subclave siguientes:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> El valor `SchUseStrongCrypto` permite a .NET usar TLS 1.1 y TLS 1.2. El valor `SystemDefaultTlsVersions` permite a .NET usar la configuración del sistema operativo. Para obtener más información, consulte [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).
