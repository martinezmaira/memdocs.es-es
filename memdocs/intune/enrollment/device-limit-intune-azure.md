---
title: Distinción de las restricciones de límite de dispositivos entre Intune y Azure
titleSuffix: ''
description: Se explican las diferencias entre las restricciones de límite de dispositivos de Intune y las de Azure AD.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63c9d9e4752e4b0d317667162255e368fc5a099c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908561"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Distinción de las restricciones de límite de dispositivos entre Intune y Azure AD

Las restricciones de límite de dispositivos se pueden configurar de dos maneras:
- Con una inscripción de Intune
- Con una unión de Azure Active Directory (AD) o un registro de Azure AD

En este artículo se explica cuándo se aplican estos límites en función de la configuración existente.

## <a name="intune-device-limit-restrictions"></a>Restricción de límite de dispositivos de Intune

Con las restricciones de límite de dispositivos de Intune se establece un número máximo de dispositivos que un usuario puede controlar (el máximo es 15). Para configurar este **Límite de dispositivo**, vaya a [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Restricciones de inscripción**. Para más información, vea [Creación de una restricción de límite de dispositivos](enrollment-restrictions-set.md#create-a-device-limit-restriction).

## <a name="azure-device-limit-restriction"></a>Restricción de límite de dispositivos de Azure

Las restricciones de límite de dispositivos de Azure establecen el número máximo de dispositivos que Azure AD une o que Azure AD registra. Para establecer el **Número máximo de dispositivos por usuario**, vaya a Azure Portal > **Azure Active Directory** > **Dispositivos**. Para más información, vea [Configuración de dispositivo](/azure/active-directory/devices/device-management-azure-portal).

## <a name="settings-applied-based-on-user-affinity"></a>Configuración aplicada según la afinidad de usuario

Si tiene establecidas restricciones de límite de dispositivos tanto de Intune como de Azure, la siguiente tabla muestra qué es lo que se aplica en función de la configuración de afinidad del usuario.

| Plataforma de dispositivo | Afinidad de usuario | Se aplica Azure | Se aplica Intune |
| ----- | ----- | ----- | ----- | ----- |
| Perfil de trabajo de Android Enterprise | Sí | Sí | Sí|
| Dispositivo Android Enterprise dedicado | No | No | No |
| Android Enterprise totalmente administrado | Sí | Sí | Sí |
| Administrador de dispositivos Android | Sí | Sí | Sí |
| DEM de administrador de dispositivos Android | No | | No | 
| BYOD de iOS/macOS | Sí | Sí | Sí |
| Inscripción de dispositivo automatizada (ADE) de iOS/macOS | Sí | Sí | Sí |
| ADE de iOS/macOS | No | Sí | No |
| BYOD de Windows | Sí | Sí | Sí |
| Solo Windows MD | | Sí | Sí |
| Unión de Windows Azure AD| Sí | Sí | No |
| Windows Autopilot | Sí | Sí | No |
| Unión a Azure AD híbrida de Windows | No | No | Sí |
| Administración conjunta de Windows | No | Sí | No |
| DEM de Windows | No | Sí | No |
| Inscripción en masa de Windows | No | Sí | No |


## <a name="android-and-ios-devices"></a>Dispositivos iOS y Android

### <a name="ios-or-android-devices-example-1"></a>Ejemplo 1 de dispositivos iOS o Android

- La opción **Número máximo de dispositivos por usuario** de Azure está establecida en 3.
- La opción **Límite de dispositivos** de Intune está establecida en 5.
 
**Resultado:** el número máximo se establece por usuario. Por ejemplo, si hay tres dispositivos de Intune inscritos, el registro de Azure de un cuarto dispositivo generará un error, debido a la opción que limita el número de registros de dispositivos.

### <a name="ios-or-android-devices-example-2"></a>Ejemplo 2 de dispositivos iOS o Android

- La opción **Número máximo de dispositivos por usuario** de Azure está establecida en 20.
- La opción **Límite de dispositivos** de Intune está establecida en 2.

**Resultado:** se pueden registrar e inscribir correctamente dos dispositivos. La inscripción de Intune de cualquier dispositivo extra se bloqueará. La ADE sin afinidad de usuario está restringida por los límites de registro de dispositivos de Azure, aunque no esté asociada a un usuario.

## <a name="windows-devices"></a>Dispositivos Windows

No se aplican restricciones de límite de dispositivos de Intune en los siguientes tipos de inscripción de Windows:
- Inscripciones con administración conjunta
- Inscripciones de objetos de directiva de grupo (GPO)
- Inscripciones de unión de Azure AD
- Inscripciones de unión de Azure AD masiva
- Inscripciones de AutoPilot
- Inscripciones del administrador de inscripciones de dispositivos

No se pueden aplicar restricciones de límite de dispositivos en estos tipos de inscripción porque se consideran escenarios de dispositivos compartidos. Para estos tipos de inscripción se pueden establecer límites estrictos en Azure Active Directory.

Respecto a la restricción de límite de dispositivos en Azure, la opción **Número máximo de dispositivos por usuario** se aplica a los dispositivos que están unidos a Azure AD o registrados en Azure AD. Esta opción no se aplica a los dispositivos unidos a Azure AD híbridos.

### <a name="windows-10-example-1"></a>Ejemplo 1 de Windows 10

- La opción **Número máximo de dispositivos por usuario** de Azure está establecida en 5.
- La opción **Límite de dispositivos** de Intune está establecida en 3.
- Los dispositivos son dispositivos unidos a Azure AD híbridos e inscritos automáticamente (configurados con GPO).

**Resultado:** dado que la inscripción se inserta a través de un GPO, el límite de registro de dispositivos de Azure es irrelevante,  al igual que la restricción de límite de dispositivos de Intune.

### <a name="windows-10-example-2"></a>Ejemplo 2 de Windows 10

- La opción **Número máximo de dispositivos por usuario** de Azure está establecida en 5.
- La opción **Límite de dispositivos** de Intune está establecida en 2.
- Los dispositivos están unidos a un dominio local y se han inscrito a través de **Configuración** > **Obtener acceso a trabajo o escuela** > **Conectar**.

**Resultado:** solo se pueden inscribir dos dispositivos antes de que se bloqueen. Se puede registrar un máximo de cinco dispositivos.


## <a name="next-steps"></a>Pasos siguientes

- [Creación de una restricción de límite de dispositivos en Azure](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Configuración de las opciones de dispositivo en Azure](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [Más información sobre el registro y la unión a un dominio](/azure/active-directory/devices/overview#getting-devices-in-azure-ad)