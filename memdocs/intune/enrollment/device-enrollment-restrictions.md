---
title: Restricciones de inscripción de dispositivos para el maco de configuración de seguridad de Android Enterprise
titleSuffix: Microsoft Intune
description: Restricciones de inscripción de dispositivos para el maco de configuración de seguridad de Android Enterprise.
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
ms.openlocfilehash: d26040c5a009a9c3877abbc25512e317f584f114
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85503031"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Restricciones de inscripción de dispositivos de Android Enterprise

Antes de inscribir los dispositivos para el [marco de configuración de la seguridad de Android Enterprise](), las organizaciones deben configurar las restricciones adecuadas. Estas restricciones garantizan que los usuarios solo puedan inscribir:
- dispositivos aprobados.
- un número de dispositivos especificado.
- dispositivos con las plataformas especificadas.
- dispositivos con los sistemas operativos especificados.
- dispositivos de los fabricantes especificados.

Para más información sobre las restricciones de inscripción de dispositivos, consulte [Establecer restricciones de inscripción](enrollment-restrictions-set.md).

## <a name="work-profile-basic-level-1-security-restrictions"></a>Restricciones de seguridad básica (nivel 1) del perfil de trabajo

En el caso de la seguridad básica del perfil de trabajo de Android Enterprise (nivel 1), se deben implementar las siguientes restricciones de dispositivos:

| Tipo | Plataforma | Version | Permite dispositivos personales |
|--------|--------|--------|--------|
| Android Enterprise | Allow | Android 5.0 y versiones posteriores.<p>Microsoft recomienda configurar la versión principal mínima de Android para que coincida con las versiones de Android compatibles con las aplicaciones de Microsoft. Los OEM y los dispositivos que se adhieren a los requisitos recomendados de Android Enterprise deben ser compatibles con la versión de publicación actual y una actualización posterior.   Actualmente, Android recomienda Android 8.0 y versiones posteriores para los profesionales que trabajan con datos. Para más información, consulte [Requisitos de Android Enterprise Recommended](https://www.android.com/enterprise/recommended/requirements/). | Sí |
| Administrador de dispositivos Android| Bloquear | Todas las versiones | Sí |

## <a name="work-profile-high-level-3-security-restrictions"></a>Restricciones de seguridad alta (nivel 3) del perfil de trabajo
En el caso de la seguridad alta del perfil de trabajo de Android Enterprise (nivel 3), se deben implementar las siguientes restricciones de dispositivos:

| Tipo | Plataforma | Version | Permite dispositivos personales |
|--------|--------|--------|--------|
| Android Enterprise | Allow | Android 8.0 y versiones posteriores | Sí |
| Administrador de dispositivos Android| Bloquear | Todas las versiones | Sí |

## <a name="fully-managed-security-restrictions"></a>Restricciones de seguridad totalmente administrada
Asegúrese de que la organización admita la inscripción de dispositivos totalmente administrados de Android Enterprise, para lo cual debe revisar la inscripción totalmente administrada de Android Enterprise. 

## <a name="next-steps"></a>Pasos siguientes

[Establecimiento de directivas de configuración de aplicaciones](android-app-configuration-policies.md)
