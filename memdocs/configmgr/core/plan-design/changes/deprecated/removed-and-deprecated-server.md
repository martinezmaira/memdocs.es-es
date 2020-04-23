---
title: En desuso para servidores de sitio
titleSuffix: Configuration Manager
description: Obtenga información sobre los productos y los sistemas operativos que Configuration Manager ya no admite para los servidores de sitio.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702573"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Elementos eliminados y en desuso de los servidores de sitio de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se describen los productos y los sistemas operativos que dejaron de ser compatibles con los servidores de sitio de Configuration Manager o que dejarán de serlo en una actualización futura (en desuso). Se proporcionan notificaciones anticipadas sobre los cambios futuros que es posible que afecten al uso de Configuration Manager.  

Esta información podría cambiar en el futuro. Puede que no incluya cada característica, producto o sistema operativo en desuso.  

## <a name="server-os"></a>SO de servidor  

|Sistemas operativos|Primer anuncio del desuso|Soporte eliminado|
|-|-|-|
|Windows Server 2008 R2 con SP1|10 de julio de 2015| Versión 1702|
|Windows Server 2008 con SP2|10 de julio de 2015|Versión 1511|

## <a name="sql-server"></a>SQL Server

|Versiones de SQL Server|Primer anuncio del desuso|Soporte eliminado|
|-|-|-|
|SQL Server 2008 R2|10 de julio de 2015|Versión 1702|
|SQL Server 2008|10 de julio de 2015|Versión 1511|

Si tiene que actualizar la versión de SQL Server, se recomienda seguir estos métodos, del más sencillo al más complicado:

1. [Realice una actualización local de SQL Server](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (recomendado).  

2. Instale una nueva versión de SQL Server en un equipo nuevo. Después, para que el servidor de sitio apunte a la nueva instancia de SQL Server, [use la opción de mover la base de datos](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) del programa de instalación de Configuration Manager.  

3. Use [Copia de seguridad y recuperación](../../../servers/manage/backup-and-recovery.md).  

## <a name="next-steps"></a>Pasos siguientes

Vea los siguientes artículos para más información:

- [Elementos eliminados y en desuso](removed-and-deprecated.md)  

- [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle)  

- [Compatibilidad con versiones de la rama actual de Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)  
