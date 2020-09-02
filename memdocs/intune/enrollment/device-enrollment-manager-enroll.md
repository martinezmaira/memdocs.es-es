---
title: Inscripción de dispositivos mediante una cuenta de administrador de inscripción de dispositivos
titleSuffix: Microsoft Intune
description: Use la cuenta del administrador de inscripciones de dispositivos para inscribir dispositivos en Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f674cc7b0c7d7314c7152d530cff210319c568df
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913144"
---
# <a name="enroll-devices-in-intune-by-using-a-device-enrollment-manager-account"></a>Inscripción de dispositivos en Intune mediante una cuenta de administrador de inscripción de dispositivos

Puede inscribir hasta 1000 dispositivos móviles con una sola cuenta de Azure Active Directory mediante una cuenta de administrador de inscripción de dispositivos (DEM). DEM es un permiso de Intune que puede aplicarse a una cuenta de usuario de AAD y que permite al usuario inscribir hasta 1000 dispositivos. Una cuenta de DEM es útil en escenarios donde los dispositivos están inscritos y preparados antes de entregarlos a los usuarios de los dispositivos. Intencionadamente, hay un límite de 150 cuentas de administrador de inscripción de dispositivos (DEM) en Microsoft Intune.

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>Limitaciones de los dispositivos que están inscritos con una cuenta DEM

Los dispositivos y las cuentas de los usuarios de DEM inscritos con una cuenta de usuario de DEM tienen las siguientes limitaciones:

- Se debe asignar una cuenta de usuario DEM a una licencia de Intune.
- No se puede realizar el borrado desde el Portal de empresa. Se puede borrar un dispositivo inscrito por una cuenta de usuario de DEM desde Intune en Azure Portal.
- Solo el dispositivo local aparece en el sitio web o en la aplicación de Portal de empresa.
- Las cuentas de usuario de DEM no pueden usar aplicaciones del Programa de Compras por Volumen de Apple (VPP) con licencias de usuario de Apple VPP debido a los requisitos de identificador de Apple por usuario para la administración de aplicaciones.
- No se pueden usar cuentas de DEM al inscribir dispositivos mediante la Inscripción de dispositivos automatizada (ADE) de Apple.
- Los dispositivos pueden instalar aplicaciones de VPP si disponen de licencias de dispositivo de Apple VPP.
- Los dispositivos están bloqueados para el acceso condicional con la excepción de Windows 10 1803+.
- Todos los dispositivos inscritos con cuentas DEM deben tener la licencia correspondiente para que Intune los administre. La licencia puede ser una licencia de usuario de Intune o una licencia de dispositivo de Intune.
- Si va a [inscribir dispositivos de perfil de trabajo Android Enterprise](android-work-profile-enroll.md) mediante una cuenta de administrador de inscripciones de dispositivos (DEM), existe un límite de 10 dispositivos que se pueden inscribir por cuenta.
- No se admite la [inscripción de dispositivos Android Enterprise totalmente administrados](android-fully-managed-enroll.md) con cuentas DEM.
- La aplicación de una restricción de dispositivos de Azure AD a una cuenta DEM le impedirá alcanzar el límite de 1000 dispositivos que la cuenta DEM puede inscribir.

## <a name="enrollment-methods-supported-by-dem-accounts"></a>Métodos de inscripción admitidos por las cuentas DEM

Puede usar los siguientes métodos para inscribir dispositivos mediante cuentas de DEM:

- [Windows Autopilot](../../autopilot/enrollment-autopilot.md):
- [Inscripción masiva de dispositivos Windows](windows-bulk-enroll.md)
- DEM iniciado a través del Portal de empresa

## <a name="add-a-device-enrollment-manager"></a>Agregar un administrador de inscripción de dispositivos

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **Inscribir dispositivos** > **Administradores de inscripciones de dispositivos**.

2. Seleccione **Agregar**.

3. En la hoja **Agregar usuario**, escriba un nombre principal de usuario para el usuario de DEM y seleccione **Agregar**. El usuario DEM se agrega a la lista de usuarios DEM.

## <a name="permissions-required-to-create-dem-accounts"></a>Permisos necesarios para crear cuentas de DEM

Se requieren los roles de administrador global o administrador de servicios de Intune de Azure AD para:
- Asignar permisos de DEM a una cuenta de usuario de Azure AD.
- Ver todos los usuarios de DEM.

Si un usuario no tiene asignado el rol de administrador global o de administrador de servicios de Intune, pero tiene habilitados permisos de lectura para el rol de administradores de inscripción de dispositivos que tiene asignado, solo podrá ver los usuarios de DEM que haya creado.

## <a name="remove-device-enrollment-manager-permissions"></a>Eliminación de los permisos de administrador de inscripción de dispositivos

La eliminación de un administrador de inscripción de dispositivos no afecta a los dispositivos inscritos.

**Eliminación de un administrador de inscripción de dispositivos**

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **Inscribir dispositivos** > **Administradores de inscripciones de dispositivos**.
2. En la hoja **Administradores de inscripción de dispositivos**, seleccione el usuario DEM y **Eliminar**.