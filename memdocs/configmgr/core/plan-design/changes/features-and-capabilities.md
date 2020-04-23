---
title: Características y funcionalidades
titleSuffix: Configuration Manager
description: Obtenga información sobre las principales funcionalidades de administración de Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5cdd0a9497f07d80813aca5dc169c4d61944e85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706403"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Características y funcionalidades de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se resumen las principales características de administración de Configuration Manager. Cada característica tiene sus propios requisitos previos, y cómo se use cada una de ellas podría influir en el diseño y la implementación de la jerarquía de Configuration Manager. Por ejemplo, si quiere implementar actualizaciones de software en dispositivos de la jerarquía, necesita un rol de sistema de sitio de punto de distribución.  

Para más información sobre cómo planear e instalar Configuration Manager para que admita estas funcionalidades de administración en su entorno, vea [Prepararse para Configuration Manager](../get-ready.md).  

## <a name="co-management"></a>Administración conjunta

La administración conjunta es una de las principales formas de asociar la implementación existente de Configuration Manager a la nube de Microsoft 365. Le permite administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune. La administración conjunta permite asociar a la nube la inversión existente en Configuration Manager mediante la incorporación de nuevas funcionalidades, como el acceso condicional. Para más información, vea [¿Qué es la administración conjunta?](../../../comanage/overview.md)

## <a name="desktop-analytics"></a>Análisis de escritorio

Análisis de escritorio es un servicio basado en la nube que se integra con Configuration Manager. Este servicio proporciona información detallada e inteligente para que pueda tomar decisiones más fundamentadas sobre la preparación de actualizaciones de sus clientes Windows. Combina datos de su organización con datos agregados de millones de dispositivos conectados a servicios en la nube de Microsoft. Para más información, vea [¿Qué es Análisis de escritorio?](../../../desktop-analytics/overview.md)

## <a name="cloud-attached-management"></a>Administración conectada a la nube

Use características como Cloud Management Gateway, los puntos de distribución basados en la nube y Azure Active Directory para administrar los clientes basados en Internet.

Vea los siguientes artículos para más información:

- [Administración de clientes en Internet](../../clients/manage/manage-clients-internet.md)
- [Planeación de Azure Active Directory](../security/plan-for-security.md#bkmk_planazuread)
- [Servicios de Azure](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>Administración en tiempo real

Use CMPivot para consultar inmediatamente los dispositivos conectados a Internet, luego fíltrelos y agrupe los datos para obtener información más detallada. Use también la consola de Configuration Manager para administrar e implementar scripts de Windows PowerShell en los clientes. Para más información, vea [CMPivot](../../servers/manage/cmpivot.md) y [Creación y ejecución de scripts de PowerShell](../../../apps/deploy-use/create-deploy-scripts.md).

## <a name="application-management"></a>Administración de aplicaciones

Ayuda a crear, administrar, implementar y supervisar aplicaciones relativas a diversos dispositivos que administre. Implemente, actualice y administre Office 365 desde la consola de Configuration Manager. Configuration Manager se integra además con Microsoft Store para Empresas y Educación para ofrecer aplicaciones basadas en la nube. Para más información, vea [Introducción a la administración de aplicaciones](../../../apps/understand/introduction-to-application-management.md).

## <a name="os-deployment"></a>Implementación del sistema operativo

Implemente una actualización local de Windows 10, o capture e implemente imágenes de sistema operativo. La implementación de imágenes puede usar PXE, la multidifusión o un medio de arranque. También puede ayudar a volver a implementar dispositivos existentes mediante Windows AutoPilot. Para más información, vea [Introducción a la implementación de sistema operativo](../../../osd/understand/introduction-to-operating-system-deployment.md).  

## <a name="software-updates"></a>Actualizaciones de software

Administre, implemente y supervise las actualizaciones de software de la organización. Integre con Optimización de distribución de Windows y otras tecnologías de almacenamiento en caché del mismo nivel para ayudar a controlar el uso de la red. Para obtener más información, vea [Introducción a las actualizaciones de software](../../../sum/understand/software-updates-introduction.md).  

## <a name="company-resource-access"></a>Acceso a los recursos de la empresa

Permite conceder a los usuarios de la organización acceso a los datos y las aplicaciones desde ubicaciones remotas. Esta característica engloba perfiles de Wi-Fi, VPN, correo electrónico y certificado. Para más información, vea [Protección de los datos y de la infraestructura de sitios](../../../protect/understand/protect-data-and-site-infrastructure.md).

## <a name="compliance-settings"></a>Configuración de cumplimiento

Ayuda a evaluar, controlar y corregir el cumplimiento de la configuración de los dispositivos cliente de la organización. Además, puede usar la configuración de cumplimiento para configurar una serie de características y opciones de seguridad en los dispositivos que administra. Para más información, vea [Garantizar el cumplimiento de dispositivos](../../../compliance/understand/ensure-device-compliance.md).  

## <a name="endpoint-protection"></a>Endpoint Protection

Proporciona seguridad, antimalware y administración de Firewall de Windows en los equipos de la organización. Esta área incluye la administración y la integración con las siguientes características del conjunto de aplicaciones de Windows Defender:

- Antivirus de Windows Defender
- Protección contra amenazas avanzada de Microsoft Defender
- Windows Defender Exploit Guard
- Protección de aplicaciones de Windows Defender
- Control de aplicaciones de Windows Defender
- Firewall de Windows Defender

Para obtener más información, vea [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

## <a name="inventory"></a>Tema de

Ayuda a identificar y supervisar los recursos.

### <a name="hardware-inventory"></a>Inventario de hardware

Recopila información detallada sobre el hardware de los dispositivos de la organización. Para obtener más información, vea [Introducción al inventario de hardware](../../clients/manage/inventory/introduction-to-hardware-inventory.md).  

### <a name="software-inventory"></a>Inventario de software

Recopila y proporciona información sobre los archivos que se almacenan en los equipos cliente de la organización. Para obtener más información, vea [Introducción al inventario de software](../../clients/manage/inventory/introduction-to-software-inventory.md).  

### <a name="asset-intelligence"></a>Asset Intelligence

Proporciona herramientas para recopilar datos de inventario y supervisar el uso de la licencia de software en la organización. Para obtener más información, vea [Introducción a Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

## <a name="on-premises-mobile-device-management"></a>Administración local de dispositivos móviles

Inscribe y administra dispositivos usando la infraestructura de Configuration Manager local con la funcionalidad de administración integrada en las plataformas de dispositivos (en la administración al uso se emplea un cliente de Configuration Manager instalado por separado). Actualmente, esta característica permite administrar dispositivos Windows 10 Enterprise y Windows 10 Mobile. Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="power-management"></a>Administración de energía

Administre y supervise el consumo de energía de los equipos cliente de la organización. Configure planes de energía y use Wake on LAN para realizar el mantenimiento fuera del horario comercial. Para obtener más información, consulte [Introduction to power management](../../clients/manage/power/introduction-to-power-management.md) (Introducción a la administración de energía).  

## <a name="remote-control"></a>Control remoto

Proporciona herramientas para administrar de forma remota los equipos cliente desde la consola de Configuration Manager. Para obtener más información, vea [Introducción al control remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).  

## <a name="reporting"></a>Generación de informes

Use funciones avanzadas de informes de SQL Server Reporting Services desde la consola de Configuration Manager. Esta característica proporciona cientos de informes predeterminados. Para obtener más información, vea [Introducción a los informes](../../servers/manage/introduction-to-reporting.md).  

## <a name="software-metering"></a>Disponibilidad de software

Supervise y recopile datos de uso de software de los clientes de Configuration Manager. Puede usar estos datos para saber si el software se usa después de instalarlo. Para más información, consulte [Medición de software en System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  
