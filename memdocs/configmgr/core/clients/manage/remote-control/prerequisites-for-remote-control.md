---
title: Requisitos previos de control remoto
titleSuffix: Configuration Manager
description: Consulte los requisitos previos del control remoto en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696423"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Requisitos previos del control remoto en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

El control remoto de Configuration Manager tiene dependencias externas y dependencias dentro del producto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Controlador de tarjeta de vídeo del equipo|Asegúrese de que el controlador de vídeo más reciente esté instalado en los equipos cliente para garantizar un rendimiento óptimo del control remoto.|  

 Los dispositivos que ejecutan Windows Embedded, Windows Embedded para punto de servicio (POS) y Windows Fundamentals for Legacy PCs no admiten el visor de control remoto, pero admiten el cliente de control remoto.  

 El control remoto de Configuration Manager no se puede usar para administrar de forma remota los equipos cliente que ejecuten Systems Management Server 2003 o Configuration Manager 2007.  

> [!NOTE]  
>  No hay servicios de Windows son necesarios como una dependencia externa para el control remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemas operativos compatibles con el visor de control remoto  
El Visor de control remoto se admite en todos los sistemas operativos compatibles con la consola de Configuration Manager. Para más información, vea [Configuraciones compatibles con las consolas de Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|El control remoto debe habilitarse para los clientes|De forma predeterminada, el control remoto no está habilitado cuando se instala Configuration Manager. Para más información sobre cómo habilitar y configurar el control remoto, vea [Configuración del control remoto](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Punto de servicios de informes|El rol de sistema de sitio de punto de servicios de informes debe instalarse antes de poder ejecutar informes para el control remoto. Para obtener más información, vea [Introducción a los informes](../../../servers/manage/introduction-to-reporting.md).|  
|Permisos de seguridad para administrar el control remoto|Para acceder a los recursos de la recopilación e iniciar una sesión de control remoto desde la consola de Configuration Manager: permisos **Leer**, **Leer recurso** y **Control remoto** en el objeto **Collection**.<br /><br /> El rol de seguridad **Operador de herramientas remotas** incluye estos permisos, que son necesarios para administrar el control remoto en Configuration Manager.<br /><br /> Para más información, vea [Configurar la administración basada en roles de Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Además, es necesario conceder permisos a los visores permitidos para usar el control remoto mediante la adición de estos usuarios a la lista **Visores permitidos de control remoto y asistencia remota** de la configuración del cliente **Herramientas remotas**.
