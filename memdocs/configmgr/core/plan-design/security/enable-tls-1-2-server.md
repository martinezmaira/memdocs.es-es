---
title: Habilitación de Seguridad de la capa de transporte (TLS) 1.2 en los servidores y sistemas de sitios remotos
titleSuffix: Configuration Manager
description: Información sobre cómo habilitar TLS 1.2 para servidores de sitios de Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704103"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>Procedimientos para habilitar TLS 1.2 en los servidores y sistemas de sitios remotos

*Se aplica a: Configuration Manager (rama actual)*

Al habilitar TLS 1.2 para el entorno de Configuration Manager, empiece primero por [habilitar TLS 1.2 para los clientes](enable-tls-1-2-client.md). Después, habilite TLS 1.2 en los servidores y sistemas de sitios remotos. Por último, pruebe las comunicaciones entre el cliente y el sistema de sitios antes de deshabilitar potencialmente los protocolos antiguos en el lado servidor. Las tareas siguientes son necesarias para habilitar TLS 1.2 en los servidores y sistemas de sitios remotos:

- Comprobación de que TLS 1.2 está habilitado como protocolo para SChannel en el nivel de sistema operativo
- Actualización y configuración de .NET Framework para admitir TLS 1.2
- Actualización de SQL Server y componentes cliente
- Actualización de Windows Server Update Services (WSUS)

Para obtener más información sobre las dependencias de características y escenarios específicos de Configuration Manager, vea [Habilitación de TLS 1.2](enable-tls-1-2.md). 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> Comprobación de que TLS 1.2 está habilitado como protocolo para SChannel en el nivel de sistema operativo

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> Actualización y configuración de .NET Framework para admitir TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a> Actualización de SQL Server y componentes cliente

Microsoft SQL Server 2016 y versiones posteriores admiten TLS 1.1 y TLS 1.2. Las versiones anteriores y las bibliotecas dependientes pueden requerir actualizaciones. Para más información, consulte [KB 3135244: Compatibilidad con TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Los servidores de sitio secundario deben usar al menos SQL Server 2016 Express con Service Pack 2 (13.2.50.26) o posterior.

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a> SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) también describe los requisitos de los componentes cliente de SQL Server.

No olvide actualizar también SQL Server Native Client al menos a la versión SQL 2012 SP4 (11.*.7001.0). A partir de la versión 1810, este requisito es una [comprobación de requisitos previos (advertencia)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Configuration Manager usa SQL Server Native Client en los siguientes roles de sistema de sitio:

- Servidor de base de datos del sitio
- Servidor de sitio: sitio de administración central, sitio primario o sitio secundario
- Punto de administración
- Punto de administración de dispositivos
- Punto de migración de estado
- Proveedor de SMS
- Punto de actualización de software
- Punto de distribución habilitado con multidifusión
- Punto de servicio de actualización de Asset Intelligence
- Punto de servicios de informes
- Servicio web del catálogo de aplicaciones
- Punto de inscripción
- Punto de Endpoint Protection
- Punto de conexión de servicio
- Punto de registro de certificados
- Punto de servicio de almacenamiento de datos


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a> Actualización de Windows Server Update Services (WSUS)

Para admitir TLS 1.2 en versiones anteriores de WSUS, instale la siguiente actualización en el servidor WSUS:

- En el servidor WSUS que ejecuta Windows Server 2012, instale la [actualización 4022721](https://support.microsoft.com/help/4022721) o una acumulativa posterior.
- En el servidor WSUS que ejecuta Windows Server 2012 R2, instale la [actualización 4022720](https://support.microsoft.com/help/4022720) o una acumulativa posterior.

A partir de Windows Server 2016, TLS 1.2 se admite de forma predeterminada para WSUS.  Las actualizaciones de TLS 1.2 solo son necesarias en los servidores Windows Server 2012 y Windows Server 2012 R2 WSUS.

## <a name="next-steps"></a>Pasos siguientes

- [Problemas habituales al habilitar TLS 1.2](enable-tls-1-2-troubleshoot.md)
