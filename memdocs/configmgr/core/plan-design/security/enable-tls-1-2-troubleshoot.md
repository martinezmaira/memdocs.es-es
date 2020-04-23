---
title: Problemas habituales al habilitar Seguridad de la capa de transporte (TLS) 1.2
titleSuffix: Configuration Manager
description: Se describen problemas habituales al habilitar Seguridad de la capa de transporte (TLS) 1.2.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704073"
---
# <a name="common-issues-when-enabling-tls-12"></a>Problemas habituales al habilitar TLS 1.2

En este artículo se proporcionan consejos para solucionar los problemas comunes que se producen al habilitar la compatibilidad con TLS 1.2 en Configuration Manager.

## <a name="unsupported-platforms"></a>Plataformas no compatibles

Las siguientes plataformas de cliente son compatibles con Configuration Manager, pero no se admiten en un entorno de TLS 1.2:

- Windows CE
- Apple OS X
- Dispositivos Windows 10 administrados con MDM local

## <a name="reports-dont-show-in-the-console"></a>Los informes no se muestran en la consola

Si los informes no se muestran en la consola de Configuration Manager, asegúrese de actualizar el equipo en el que está ejecutando la consola. [Actualice .NET Framework](enable-tls-1-2-client.md#bkmk_net) y habilite la criptografía segura.

## <a name="fips-security-policy-enabled"></a>Directiva de seguridad FIPS habilitada

Si habilita la configuración de directiva de seguridad FIPS para el cliente o un servidor, la negociación de Secure Channel (Schannel) puede provocar que utilicen TLS 1.0. Este comportamiento se produce incluso si deshabilita el protocolo en el Registro.

Para investigar esto, habilite el registro de eventos del canal seguro y, luego, revise los eventos de Schannel en el registro del sistema. Para obtener más información, consulte el artículo sobre [cómo restringir el uso de ciertos algoritmos criptográficos y protocolos en Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="sql-server-communication-failure"></a>Error de comunicación de SQL Server

Si se produce algún error de comunicación de SQL Server y se devuelve un error **SslSecurityError**, compruebe la siguiente configuración:

- [Actualice .NET Framework](enable-tls-1-2-server.md#bkmk_net) y habilite la criptografía segura en cada equipo
- [Actualice SQL Server](enable-tls-1-2-server.md#bkmk_sql) en el servidor host
- [Actualice los componentes del cliente SQL](enable-tls-1-2-server.md#bkmk_sql-client) en todos los sistemas que se comunican con SQL. Por ejemplo, los servidores de sitio, el proveedor de SMS y los servidores del rol de sitio.

## <a name="configuration-manager-client-communication-failures"></a>Errores de comunicación del cliente de Configuration Manager

Si el cliente de Configuration Manager no se comunica con los roles de sitio, compruebe que [actualizó Windows](enable-tls-1-2-client.md#bkmk_winhttp) para admitir TLS 1.2 para la comunicación cliente/servidor mediante el uso de WinHTTP. Los roles de sitio comunes incluyen puntos de distribución, puntos de administración y puntos de migración de estado.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>El punto de servicios de informes devuelve un error inesperado

Si el punto de servicios de informes no configura los informes, revise el registro **SRSRP.log** para ver la entrada de error siguiente:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Para solucionar este problema, siga estos pasos:

1. [Actualice .NET Framework](enable-tls-1-2-client.md#bkmk_net) y habilite la criptografía segura en todos los equipos pertinentes.

1. Después de instalar las actualizaciones, reinicie el servicio SMS_Executive.

## <a name="application-catalog-doesnt-initialize"></a>El catálogo de aplicaciones no se inicializa

> [!Important]  
> La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910. Para más información, consulte [Características en desuso y eliminadas](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Si el catálogo de aplicaciones no se inicializa, revise el archivo **ServicePortalWebSite.svclog** para ver la entrada de error siguiente:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Para solucionar este problema, siga estos pasos:

1. [Actualice .NET Framework](enable-tls-1-2-client.md#bkmk_net) y habilite la criptografía segura en todos los equipos pertinentes.

1. En la carpeta `%WinDir%\System32\InetSrv` del servidor del catálogo de aplicaciones, cree un archivo **W2SP.exe.config** con el contenido siguiente:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Este es el archivo predeterminado que se crea si la aplicación se compiló con .NET Framework 4.6.3.

1. Use la seguridad de transporte HTTPS para los roles del catálogo de aplicaciones.

    > [!Important]
    > Cuando se usa la seguridad de mensajes HTTP para los roles del catálogo de aplicaciones, WCF se codifica de forma rígida para que solo use SSL 3.0 y TLS 1.0. Esto evita el uso de TLS 1.2.

1. Si hizo alguna modificación, reinicie el equipo.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>El Centro de software o el explorador no se puede comunicar con el catálogo de aplicaciones

> [!Important]  
> La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910. Para más información, consulte [Características en desuso y eliminadas](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

El mejor método para que el Centro de Software funcione con las aplicaciones disponibles para el usuario en un sitio habilitado para TLS 1.2 es quitar la función del catálogo de aplicaciones. A continuación, deje que el Centro de software se comunique directamente con un punto de administración. Para más información, consulte [Eliminación del catálogo de aplicaciones](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).

Si tiene que resolver errores de comunicación entre el catálogo de aplicaciones y el Centro de software, compruebe las condiciones siguientes:

- [Actualice .NET Framework](enable-tls-1-2-client.md#bkmk_net) y habilite la criptografía segura en cada equipo.

- Después de realizar los cambios, reinicie todos los equipos afectados.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Errores de carga del punto de conexión del servicio

Si el punto de conexión del servicio no carga datos a SCCMConnectedService, [actualice .NET Framework](enable-tls-1-2-server.md#bkmk_net) y habilite la criptografía segura en cada equipo. No olvide reiniciar los equipos una vez hechos los cambios.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>La consola de Configuration Manager muestra el cuadro de diálogo de incorporación a Intune

Si el cuadro de diálogo de incorporación a Intune aparece cuando la consola intenta conectarse al portal de Intune, [actualice .NET Framework](enable-tls-1-2-client.md#bkmk_net) y habilite la criptografía segura en cada equipo. No olvide reiniciar los equipos una vez hechos los cambios.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>La consola de Configuration Manager muestra un error al iniciar sesión en Azure

Al intentar crear aplicaciones en Azure Active Directory (Azure AD), si el cuadro de diálogo de incorporación a los servicios de Azure presenta un error inmediatamente después de que se selecciona **Iniciar sesión**, [actualice .NET Framework](enable-tls-1-2-server.md#bkmk_net) y habilite la criptografía segura. No olvide reiniciar los equipos una vez hechos los cambios.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Servicios en la nube de Configuration Manager y TLS 1.2

Las máquinas virtuales de Azure usadas por la puerta de enlace de administración en la nube y por los puntos de distribución en la nube admiten TLS 1.2. Las versiones de cliente admitidas usan automáticamente TLS 1.2.

El registro **SMSAdminui.log** puede contener un error similar al ejemplo siguiente:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

En el registro de eventos del sistema, el identificador de evento 36874 de SChannel podría registrarse con la descripción siguiente: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Recursos adicionales

- Para obtener más información, consulte [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).
- [KB 3135244: Compatibilidad con TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).
- [Referencia técnica de controles criptográficos](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Pasos siguientes

- [Habilitación de TLS 1.2 en clientes](enable-tls-1-2-client.md)
- [Habilitación de TLS 1.2 en servidores y sistemas de sitios remotos](enable-tls-1-2-server.md)

