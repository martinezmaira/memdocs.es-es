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
ms.openlocfilehash: 6ecd15ea98ff9fa5ff0ff6ff570e644a8dcf5003
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85503046"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>Directivas de configuración de aplicaciones del marco de configuración de seguridad de Android Enterprise

Como parte del [marco de configuración de seguridad de Android Enterprise](android-configuration-framework.md), debe establecer correctamente las directivas de configuración de aplicaciones para los dispositivos de Android Enterprise.

Los dispositivos de perfil de trabajo de Android Enterprise están concebidos para aislar los datos personales de los de trabajo. Los dispositivos totalmente administrados de Android Enterprise solo están concebidos para datos de trabajo o educativos. Por lo tanto, las aplicaciones de Microsoft implementadas en estos dispositivos deben estar configuradas para no permitir cuentas personales.

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>No permitir cuentas personales de aplicaciones de Microsoft en dispositivos de Android Enterprise

1. Agregue las aplicaciones a Google Play administrado. Para obtener más información, consulte [Incorporación de aplicaciones de Google Play administrado a dispositivos Android Enterprise con Intune](../apps/apps-add-android-for-work.md).
2. Cree una directiva para cada aplicación de Google Play administrado descrita en [Adición de directivas de configuración de aplicaciones para dispositivos Android Enterprise administrados]().
3. Cree la siguiente clave única en cada directiva:

    | Key | Valores |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | Uno o varios; UPN delimitados.<br>Las cuentas permitidas son las únicas cuentas de usuario administradas que define esta clave.<br>En el caso de los dispositivos inscritos en Intune, el token {{userprincipalname}} se puede usar para representar la cuenta de usuario inscrita. |


## <a name="next-steps"></a>Pasos siguientes
Aplique la [configuración de seguridad del perfil de trabajo de Android Enterprise](android-work-profile-security-settings.md) o la [configuración de seguridad totalmente administrada de Android Enterprise](android-fully-managed-security-settings.md).