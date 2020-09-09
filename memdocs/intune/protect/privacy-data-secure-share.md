---
title: Uso compartido y seguridad de datos en Intune
titleSuffix: Microsoft Intune
description: Obtenga más información sobre cómo se protegen y comparten los datos personales en Intune.
keywords: privacidad, datos
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 68921fd6-5f50-456c-a3af-83d7bc4b134b
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34e99a53165afdccd5ee9a2f3f190c78f673a507
ms.sourcegitcommit: 15450a1e92d9f67f74ae619ffe192c15948107c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516263"
---
# <a name="data-security-and-sharing-in-intune"></a>Uso compartido y seguridad de datos en Intune


## <a name="data-security"></a>Seguridad de los datos

Microsoft Intune es un componente clave de la oferta de servicio en la nube de Microsoft Enterprise Mobility + Security Suite. Para admitir la [estrategia de gobernanza de datos](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx), todos los servicios en la nube de Microsoft se desarrollan con metodologías de [Microsoft Privacy](https://www.microsoft.com/en-us/trustcenter/privacy) y [Microsoft Security](https://www.microsoft.com/en-us/trustcenter/security/).  

Microsoft Intune sigue las mismas medidas técnicas y organizativas que toman los equipos de servicio de Microsoft Azure para protegerse contra los procesos de vulneración de datos.

Para obtener más información, vea el [Portal de confianza de servicios](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="data-breach-reporting"></a>Informes de vulneración de datos

Cuando se identifica un incidente de seguridad notificable a los clientes (CRSI), los clientes reciben una notificación al respecto. Este proceso incluye trabajar con el equipo de Microsoft 365 para comunicar la notificación de vulneración a los clientes de Microsoft 365 que usan Intune.

## <a name="data-sharing"></a>Uso compartido de datos

Cuando los administradores de inquilinos activan ciertas funcionalidades (por ejemplo, el Programa de inscripción de dispositivos de Apple), Microsoft Intune obtiene consentimiento del administrador para compartir datos con las terceras partes adecuadas. En tal caso, Intune podría compartir los datos personales con:

- Terceros que actúen como agentes de Microsoft.
- Terceros que no actúen como agentes de Microsoft, pero solo cuando los administradores de inquilinos concedan permiso a Intune explícitamente para ello.

Todos los terceros que actúen como agentes de Microsoft se incluyen en la [lista de subcontratistas de servicios en línea](https://aka.ms/Online_Serv_Subcontractor_List).

El uso compartido de datos con estas entidades se realiza para ayudar al cliente y ofrecer soporte técnico, el mantenimiento del servicio y otras operaciones.

Los datos personales de Intune que se mantienen un el servicio de terceros se rigen mediante un contrato del inquilino con dichos terceros. También concede permiso a Intune que transmitir los datos al servicio de terceros.  

Para obtener más información sobre los datos compartidos con terceros determinados, consulte los artículos siguientes:
- [Data que Intune manda a Apple](data-intune-sends-to-apple.md)
- [Datos que Intune manda a Google](data-intune-sends-to-google.md)
- [Datos que Apple manda a Intune](data-apple-sends-to-intune.md)
- [Datos que Google manda a Intune](data-google-sends-to-intune.md)
- [Datos que Jamf Pro manda a Intune](data-jamf-sends-to-intune.md)

### <a name="microsoft-endpoint-configuration-manager-data-sharing"></a>Uso compartido de los datos de Microsoft Endpoint Configuration Manager

Microsoft Intune no comparte ningún dato con Configuration Manager. Configuration Manager es un producto local implementado, administrado y operado directamente por el cliente. Los datos de uso y diagnóstico recopilados por Configuration Manager solo son para mejorar la experiencia de instalación, la calidad y la seguridad de las versiones futuras.

Para más información, consulte [Diagnósticos y datos de uso para Configuration Manager](/configmgr/core/plan-design/diagnostics/diagnostics-and-usage-data). 


## <a name="next-steps"></a>Pasos siguientes

Consulte cómo [visualizar y corregir](privacy-data-view-correct.md) los datos personales en Intune.
