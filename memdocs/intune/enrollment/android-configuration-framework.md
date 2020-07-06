---
title: Marco de trabajo de configuración de seguridad de Android Enterprise
titleSuffix: Microsoft Intune
description: Conozca las restricciones y los valores de configuración sugeridos para seguridad básica y alta de dispositivos Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85503034"
---
# <a name="android-enterprise-security-configuration-framework"></a>Marco de trabajo de configuración de seguridad de Android Enterprise

El marco de configuración de seguridad de Android Enterprise consta de una serie de recomendaciones de configuración de las directivas de configuración y cumplimiento de los dispositivos. Estas recomendaciones le ayudan a adaptar la protección de seguridad de los dispositivos móviles de la organización a sus necesidades específicas.

Las organizaciones preocupadas por la seguridad buscan formas de garantizar la protección de los datos corporativos de dispositivos móviles. Un método que se usa para proteger esos datos es mediante la inscripción de dispositivos. La inscripción de dispositivos ayuda a las organizaciones a:
- implementar directivas de cumplimiento (como la seguridad de PIN, la validación de jailbreak/root, etc.).
- implementar directivas de configuración (como Wi-Fi, certificados y VPN).
- administrar el ciclo de vida de la aplicación.

Para configurar un escenario de seguridad completo, Microsoft introdujo una nueva taxonomía para las [configuraciones de seguridad de Windows 10](https://aka.ms/secconframework). Intune emplea una taxonomía similar para su marco de configuración de seguridad de Android Enterprise. Incluyen la configuración recomendada del cumplimiento y las restricciones de los dispositivos para la seguridad básica, mejorada y alta. Esta taxonomía se explica en los artículos siguientes:

1. [Metodología de implementación del marco de Android Enterprise](framework-deployment-methodology.md): una metodología recomendada para implementar el marco de configuración de seguridad.
2. [Restricciones de la inscripción de dispositivos Android](device-enrollment-restrictions.md): restricciones de dispositivos previas a la inscripción para dispositivos Android Enterprise.
3. [Establecimiento de directivas de configuración de aplicaciones para dispositivos Android Enterprise](android-app-configuration-policies.md): Configure las aplicaciones de los dispositivos para que no permitan cuentas personales.
4. [Configuración de seguridad del perfil de trabajo de Android Enterprise](android-work-profile-security-settings.md): opciones de configuración específicas para la seguridad básica y alta en los dispositivos de perfil de trabajo.
5. [Configuración de seguridad totalmente administrada de Android Enterprise](android-fully-managed-security-settings.md): opciones de configuración específicas para la seguridad básica, mejorada y alta en dispositivos totalmente administrados.

## <a name="android-enterprise-enrollment-modes"></a>Modos de inscripción de Android Enterprise

Con Android 5.0, Google introdujo Android Enterprise, que incluye dos modos de inscripción. El marco de trabajo de configuración de seguridad de Android Enterprise proporciona recomendaciones para ambos modos.
- [Dispositivos totalmente administrados (propietario del dispositivo)](android-fully-managed-enroll.md): corporativos que están asociados con un solo usuario. Estos dispositivos son exclusivamente para trabajar, no para uso personal.
- [Perfil de trabajo (propietario del perfil)](android-work-profile-enroll.md): normalmente, para dispositivos personales en los que los responsables de TI quieren establecer un límite claro entre los datos de trabajo y los personales. Las directivas controladas por TI garantizan que los datos de trabajo no se pueden transferir al perfil personal.


## <a name="next-steps"></a>Pasos siguientes

[Metodología de implementación del marco de Android Enterprise](framework-deployment-methodology.md)