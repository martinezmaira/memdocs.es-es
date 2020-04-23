---
title: Introducción a la habilitación de Seguridad de la capa de transporte (TLS) 1.2
titleSuffix: Configuration Manager
description: Introducción a los procedimientos de habilitación de TLS 1.2 para Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5d9d7cea7e5653b338a3eb4adb01d9fded99035e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704063"
---
# <a name="how-to-enable-tls-12"></a>Habilitación de TLS 1.2

*Se aplica a: Configuration Manager (rama actual)*

Seguridad de la capa de transporte (TLS), como Capa de sockets seguros (SSL), es un protocolo de cifrado diseñado para mantener los datos seguros al transferirlos a través de una red. En estos artículos se describen los pasos necesarios para asegurarse de que en la comunicación segura de Configuration Manager se use el protocolo TLS 1.2. También se describen los requisitos de actualización de las características más usadas y la solución de algunos problemas comunes.

## <a name="enabling-tls-12"></a>Habilitación de TLS 1.2

Configuration Manager se basa en varios componentes distintos para garantizar la comunicación segura. El protocolo que se usa para una conexión determinada depende de las funcionalidades de los componentes pertinentes en el lado cliente y servidor. Si un componente no está actualizado o correctamente configurado, es posible que la comunicación use un protocolo más antiguo y menos seguro. Para habilitar correctamente Configuration Manager a fin de admitir TLS 1.2 para todas las comunicaciones seguras, debe habilitar TLS 1.2 para todos los componentes necesarios. Los componentes necesarios dependen del entorno y de las características de Configuration Manager que use.

> [!IMPORTANT]
> Inicie este proceso con los clientes, especialmente las versiones anteriores de Windows. Antes de habilitar TLS 1.2 y deshabilitar los protocolos antiguos en los servidores de Configuration Manager, asegúrese de que todos los clientes admiten TLS 1.2. En caso contrario, los clientes no se podrán comunicar con los servidores y podrían quedar huérfanos.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Tareas para clientes, servidores y sistemas de sitios remotos de Configuration Manager

A fin de habilitar TLS 1.2 en los componentes de los que Configuration Manager depende para la comunicación segura, tendrá que realizar varias tareas en los clientes y en los servidores de sitios.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Habilitación de TLS 1.2 para clientes de Configuration Manager

- [Actualización de Windows y WinHTTP en Windows 8.0, Windows Server 2012 (no R2) y versiones anteriores](enable-tls-1-2-client.md#bkmk_winhttp)
- [Comprobación de que TLS 1.2 está habilitado como protocolo para SChannel en el nivel de sistema operativo](enable-tls-1-2-client.md#bkmk_protocol)
- [Actualización y configuración de .NET Framework para admitir TLS 1.2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Habilitación de TLS 1.2 para servidores y sistemas de sitios remotos de Configuration Manager

- [Comprobación de que TLS 1.2 está habilitado como protocolo para SChannel en el nivel de sistema operativo](enable-tls-1-2-server.md#bkmk_protocol)
- [Actualización y configuración de .NET Framework para admitir TLS 1.2](enable-tls-1-2-server.md#bkmk_net)
- [Actualización de SQL Server y SQL Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [Actualización de Windows Server Update Services (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Características y dependencias de escenario

En esta sección se describen las dependencias para características y escenarios específicos de Configuration Manager. Para determinar los pasos siguientes, busque los elementos que son de aplicación para su entorno.

|Característica o un escenario|Tareas de actualización|
|--- |--- |
|Servidores de sitio (central, principal o secundario)| - [Actualice .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> - Compruebe la configuración de la criptografía segura.|
|Servidor de base de datos del sitio|[Actualice SQL Server y sus componentes cliente](enable-tls-1-2-server.md#bkmk_sql).|
|Servidores de sitio secundario|[Actualice SQL Server y sus componentes cliente](enable-tls-1-2-server.md#bkmk_sql) a una versión compatible de SQL Express.|
|Roles de sistema de sitio| - [Actualice .NET Framework](enable-tls-1-2-server.md#bkmk_net) y compruebe la configuración de la criptografía segura. <br/> - [Actualice SQL Server y sus componentes cliente](enable-tls-1-2-server.md#bkmk_sql) en roles que lo necesitan, como [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client).|
|Punto de servicios de informes|- [Actualice .NET Framework](enable-tls-1-2-server.md#bkmk_net) en el servidor de sitio, los servidores de SQL Reporting Services y cualquier equipo que tenga la consola.<br/> - Reinicie el servicio SMS_Executive según sea necesario.|
|Punto de actualización de software|[Actualice WSUS](enable-tls-1-2-server.md#bkmk_wsus).|
|Puerta de enlace de administración en la nube|[Exigir TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Consola de Configuration Manager| - [Actualice .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - Compruebe la configuración de la criptografía segura.|
|Cliente de Configuration Manager con roles de sistema de sitio HTTPS|[Actualice Windows para admitir TLS 1.2 para las comunicaciones cliente-servidor mediante WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp).|
|Centro de software| - [Actualice .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - Compruebe la configuración de la criptografía segura.|
|Clientes de Windows 7| *Antes* de habilitar TLS 1.2 en cualquier componente del servidor, [actualice Windows para admitir TLS 1.2 para las comunicaciones cliente-servidor mediante WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp). Si habilita TLS 1.2 en componentes de servidor en primer lugar, puede dejar huérfanas las versiones anteriores de los clientes.|

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="why-use-tls-12-with-configuration-manager"></a>¿Por qué usar TLS 1.2 con Configuration Manager?

TLS 1.2 es más seguro que los protocolos criptográficos anteriores, como SSL 2.0, SSL 3.0, TLS 1.0 y TLS 1.1. Esencialmente, TLS 1.2 hace que los datos que se transfieren por la red sean más seguros.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>¿Dónde usa Configuration Manager protocolos de cifrado como TLS 1.2?

Básicamente, hay cinco áreas en las que Configuration Manager usa protocolos de cifrado como TLS 1.2:

- Comunicaciones de cliente con roles de servidor de sitio basados en IIS cuando el rol está configurado para usar HTTPS. Algunos ejemplos de estos roles son los puntos de distribución, los puntos de actualización de software y los puntos de administración.
- Punto de administración, SMS Executive y comunicaciones del proveedor de SMS con SQL. Configuration Manager siempre cifra las comunicaciones SQL.
- Servidor de sitio a comunicaciones de WSUS, si WSUS está configurado para usar HTTPS.
- Consola de Configuration Manager para SQL Reporting Services (SSRS), si SSRS está configurado para usar HTTPS.
- Cualquier conexión a servicios basados en Internet. Algunos ejemplos son Cloud Management Gateway (CMG), la sincronización del punto de conexión de servicio y la sincronización de metadatos de actualización desde Microsoft Update.

### <a name="what-determines-which-encryption-protocol-is-used"></a>¿Qué determina el protocolo de cifrado que se usa?

HTTPS siempre negociará la versión más alta del protocolo compatible con el cliente y el servidor en una conversación cifrada. Al establecer una conexión, el cliente envía un mensaje al servidor con el protocolo más alto disponible. Si el servidor admite la misma versión, envía un mensaje con esa versión. Esta versión negociada es la que se usa para la conexión. Si el servidor no admite la versión presentada por el cliente, el mensaje del servidor especificará la versión más alta que pueda usar. Para obtener más información sobre el protocolo de enlace TLS, vea [Establecimiento de una sesión segura mediante TLS](https://docs.microsoft.com/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>¿Qué determina la versión del protocolo que pueden usar el cliente y el servidor?

Por lo general, los elementos siguientes pueden determinar la versión del protocolo que se usa:

- La aplicación puede determinar qué versiones de protocolo específicas se van a negociar.
  - El procedimiento recomendado consiste en evitar la codificación rígida de versiones de protocolo específicas en el nivel de aplicación y seguir la configuración definida en el nivel de protocolo del componente y del sistema operativo.
  - Configuration Manager sigue este procedimiento recomendado.
- En el caso de las aplicaciones escritas con .NET Framework, las versiones de protocolo predeterminadas dependen de la versión de la plataforma en la que se hayan compilado.  
  - De forma predeterminada, las versiones de .NET anteriores a la 4.6.3 no incluían TLS 1.1 y 1.2 en la lista de protocolos para la negociación.
- Las aplicaciones que usan WinHTTP para comunicaciones HTTPS, como el cliente de Configuration Manager, dependen de la versión del sistema operativo, el nivel de revisión y la configuración para la compatibilidad con la versión del protocolo.


## <a name="additional-resources"></a>Recursos adicionales

- [Referencia técnica de controles criptográficos](cryptographic-controls-technical-reference.md)
- Para obtener más información, consulte [Procedimientos recomendados sobre la seguridad de la capa de transporte (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).
- [KB 3135244: Compatibilidad con TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

## <a name="next-steps"></a>Pasos siguientes

- [Habilitación de TLS 1.2 en clientes](enable-tls-1-2-client.md)
- [Habilitación de TLS 1.2 en los servidores de sitios](enable-tls-1-2-server.md)
