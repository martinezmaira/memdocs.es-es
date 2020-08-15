---
title: Requisitos de licencia de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Infórmese sobre los requisitos de licencia para la implementación de Windows AutoPilot.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 911ff589acb5d215931dd4a2e72a05bff760a533
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253363"
---
# <a name="windows-autopilot-licensing-requirements"></a>Requisitos de licencia de Windows AutoPilot

**Se aplica a: Windows 10**

Windows AutoPilot depende de las capacidades específicas disponibles en Windows 10 y Azure Active Directory. También requiere un servicio MDM como Microsoft Intune. Estas funcionalidades pueden obtenerse a través de varias ediciones y programas de suscripción:

Para proporcionar los Azure Active Directory necesarios (características de personalización de marca de empresa y inscripción automática de MDM) y la funcionalidad de MDM, se requiere una de las siguientes suscripciones:
- [Suscripción a Microsoft 365 Empresa Premium](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 suscripción F1 o F3](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 la suscripción Academic a1, a3 o A5](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise suscripción a E3 o E5](https://www.microsoft.com/microsoft-365/enterprise), que incluye todas las características de Windows 10, Office 365 y em + S (Azure ad e Intune).
- [Enterprise Mobility + Security suscripción a E3 o E5](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), que incluye todas las características necesarias de Azure ad e Intune.
- [Intune for Education suscripción](https://docs.microsoft.com/intune-education/what-is-intune-for-education), que incluye todas las características necesarias de Azure ad e Intune.
- [Azure Active Directory Premium P1 o P2](https://azure.microsoft.com/services/active-directory/) y [Microsoft Intune suscripción](https://www.microsoft.com/cloud-platform/microsoft-intune) (o un servicio MDM alternativo).

> [!NOTE]
> Incluso cuando se usa Microsoft 365 suscripciones, todavía es necesario [asignar licencias de Intune a los usuarios](https://docs.microsoft.com/intune/fundamentals/licenses-assign).

Además, también se recomiendan los siguientes elementos (pero no son obligatorios):
- [Microsoft 365 aplicaciones para la empresa](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), que se pueden implementar fácilmente a través de Intune (u otros servicios de MDM).
- [Activación de suscripciones de Windows](https://docs.microsoft.com/windows/deployment/windows-10-enterprise-subscription-activation), para subir automáticamente los dispositivos de Windows 10 Pro a Windows 10 Enterprise.

**Pasos siguientes**

[Requisitos de configuración de Windows AutoPilot](configuration-requirements.md)

