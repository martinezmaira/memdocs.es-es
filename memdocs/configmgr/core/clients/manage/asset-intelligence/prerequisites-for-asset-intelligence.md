---
title: Requisitos previos de Asset Intelligence
titleSuffix: Configuration Manager
description: Obtenga los requisitos previos de Asset Intelligence en Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dfed0f2c2e8149abb05d4b21047d4d494f034e53
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695013"
---
# <a name="prerequisites-for-asset-intelligence-in-configuration-manager"></a>Requisitos previos de Asset Intelligence en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Asset Intelligence en Configuration Manager tiene dependencias externas y dependencias dentro del producto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  
 La tabla siguiente proporciona las dependencias de Asset Intelligence que son externas a Configuration Manager.  

|Dependencia|Más información|  
|----------------|----------------------|  
|Auditoría de requisitos previos de eventos de inicio de sesión correctos|Cuatro informes de Asset Intelligence muestran información recopilada de los registros de eventos de seguridad de Windows en los equipos cliente. Si la configuración del registro de eventos de seguridad no está establecida para registrar todos los eventos de inicio de sesión correctos, estos informes no contienen datos incluso aunque se haya habilitado la clase de informes de inventario de hardware correspondiente.<br /><br /> Los siguientes informes de Asset Intelligence dependen de la información recopilada del registro de eventos de seguridad de Windows:<br /><br /> - Hardware 03A - Usuarios del equipo primario<br />- Hardware 03B - Equipos para un usuario primario específico de la consola<br />- Hardware 04A - Equipos compartidos (multiusuario)<br />- Hardware 05A - Usuarios de la consola en un equipo específico<br /><br /> Para habilitar el Agente cliente de inventario de hardware a fin de inventariar la información necesaria para admitir estos informes, primero se debe modificar la configuración del registro de eventos de seguridad de Windows en los clientes para que registren todos los eventos de inicio de sesión correctos y habilitar la clase de informe de inventario de hardware **SMS_SystemConsoleUser** . Para obtener más información sobre cómo modificar la configuración del registro de eventos de seguridad para registrar todos los eventos de inicio de sesión correctos, consulte [Habilitar la auditoría de eventos de inicio de sesión correctos](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  La clase de informe de inventario de hardware **SMS_SystemConsoleUser** conserva los datos de eventos de inicio de sesión correctos de solo los 90 días anteriores del registro de eventos de seguridad, independientemente de la longitud del registro. Si el registro de eventos de seguridad tiene menos de 90 días de datos, se lee todo el registro.  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependencias internas en Configuration Manager  
 La tabla siguiente proporciona las dependencias de Asset Intelligence que son internas a Configuration Manager.  

|Dependencia|Más información|  
|----------------|----------------------|  
|Requisitos previos del agente cliente|Los informes de Asset Intelligence dependen de la información de cliente que se obtiene a través de informes de inventario de hardware y software de cliente. Para obtener la información necesaria para todos los informes de Asset Intelligence, deben habilitarse los siguientes agentes cliente:<br /><br /> - Agente cliente de inventario de hardware<br />- Agente cliente de medición de software|  
|Dependencias de agente cliente de inventario de hardware|Para recopilar los datos de inventario necesarios para algunos informes de Asset Intelligence, el Agente cliente de inventario de hardware debe estar habilitado. Además, algunas clases de informes de inventario de hardware de las que dependen los informes de Asset Intelligence deben habilitarse en equipos de servidor de sitio primario.<br /><br /> Para más información sobre cómo habilitar el Agente cliente de inventario de hardware, vea [Cómo ampliar el inventario de hardware](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Dependencias de Agente cliente de medición de software|Los datos de diversos informes de software de Asset Intelligence dependen del Agente cliente de medición de software. Para más información sobre cómo habilitar el Agente cliente de medición de software, vea [Supervisión del uso de aplicaciones a través de la medición de software](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Los siguientes informes de software de Asset Intelligence dependen del Agente cliente de medición de software para proporcionar datos:<br /><br /> - Software 07A - Programas ejecutables usados recientemente por recuento de equipos<br />- Software 07B - Equipos que han usado recientemente un ejecutable especificado<br />- Software 07C - Programas ejecutables usados recientemente en un equipo especificado<br />- Software 08A - Ejecutables usados recientemente por recuento de usuarios<br />- Software 08B - Usuarios que han usado recientemente un programa ejecutable especificado<br />- Software 08C - Programas ejecutables usados recientemente por un usuario especificado|  
|Requisitos previos de la clase de informes de inventario de hardware de Asset Intelligence|Los informes de Asset Intelligence en Configuration Manager dependen de clases de informes de inventario de hardware específicas. Hasta que se habilitan las clases de informes de inventario de hardware y los clientes han informado su inventario de hardware basado en estas clases de informes, los informes de Asset Intelligence asociados no contienen ningún dato. Puede habilitar las clases de informes de inventario de hardware siguientes para admitir los requisitos de informes de Asset Intelligence:<br /><br /> -   SMS_SystemConsoleUsage<sup>1</sup><br />-   SMS_SystemConsoleUser<sup>1</sup><br />-   SMS_InstalledSoftware<br />-   SMS_AutoStartSoftware<br />-   SMS_BrowserHelperObject<br />-   Win32_USBDevice<br />-   SMS_InstalledExecutable<br />-   SMS_SoftwareShortcut<br />-   SoftwareLicensingService<br />-   SoftwareLicensingProduct<br />-   SMS_SoftwareTag<br /><br /> <sup>1</sup> De forma predeterminada, las clases de informes de inventario de hardware de Asset Intelligence **SMS_SystemConsoleUsage** y **SMS_SystemConsoleUser** están habilitadas.<br /><br /> Las clases de informes de inventario de hardware de Asset Intelligence se pueden editar en el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, desde el nodo **Asset Intelligence**. Para más información, vea la sección [Habilitar las clases de informes de inventario de hardware de Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) del tema [Configurar Asset Intelligence en Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).|  
|Punto de servicios de informes|El rol de sistema de sitio de punto de servicios de informes debe instalarse antes de que puedan mostrarse los informes de actualizaciones de software. Para obtener más información sobre la creación de un punto de servicios de informes, consulte [Configuración de informes en Configuration Manager](https://go.microsoft.com/fwlink/p/?LinkId=232661).|  
