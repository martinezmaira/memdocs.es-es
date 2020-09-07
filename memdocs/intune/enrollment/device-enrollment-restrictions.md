---
title: Restricciones de inscripción de dispositivos para el maco de configuración de seguridad de Android Enterprise
titleSuffix: Microsoft Intune
description: Restricciones de inscripción de dispositivos para el maco de configuración de seguridad de Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/02/2020
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
ms.openlocfilehash: 618be398d963e0a796ad9be7e8810201fc5e12f5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995099"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Restricciones de inscripción de dispositivos de Android Enterprise

Antes de inscribir los dispositivos para el [marco de configuración de la seguridad de Android Enterprise](android-configuration-framework.md), las organizaciones deben configurar las restricciones adecuadas. Estas restricciones garantizan que los usuarios solo puedan inscribir:

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
Consulte [Inscribir dispositivos totalmente administrados](android-fully-managed-enroll.md#enroll-the-fully-managed-devices) para asegurarse de que la organización admita la inscripción de dispositivos totalmente administrados de Android Enterprise. 

## <a name="conditional-access-policies"></a>Directivas de acceso condicional
Las organizaciones pueden usar directivas de acceso condicional de Azure AD para asegurarse de que los usuarios solo puedan acceder al contenido profesional o educativo en dispositivos Android inscritos. Para ello, necesitará una directiva de acceso condicional destinada a todos los usuarios potenciales. Encontrará más información sobre la creación de esta directiva en [Uso obligatorio de dispositivos administrados para el acceso a aplicaciones en la nube mediante el acceso condicional](/azure/active-directory/conditional-access/require-managed-devices). 

Siga los pasos descritos en el [escenario relativo a la obligatoriedad de la inscripción para dispositivos iOS y Android](/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices), que garantiza que solo los dispositivos móviles inscritos conformes se puedan conectar a los puntos de conexión de Microsoft 365.

## <a name="next-steps"></a>Pasos siguientes

[Establecimiento de directivas de configuración de aplicaciones](android-app-configuration-policies.md)