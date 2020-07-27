---
title: Configuración de la inscripción de Intune para dispositivos corporativos de Android Enterprise con un perfil de trabajo
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo inscribir dispositivos corporativos de Android Enterprise con un perfil de trabajo en Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4934115915c41d696258aa54ee8f4b7c84d1809c
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465026"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>Configuración de la inscripción de Intune para dispositivos corporativos de Android Enterprise con un perfil de trabajo

Los dispositivos corporativos de Android Enterprise con un perfil de trabajo son dispositivos de un único usuario diseñados para su uso corporativo y personal.

Los usuarios finales pueden separar sus datos profesionales y personales con la garantía de que sus datos y aplicaciones personales seguirán siendo privados. Los administradores pueden controlar algunos valores y características para todo el dispositivo, como los siguientes:

- Establecer los requisitos para la contraseña del dispositivo
- Controlar el Bluetooth y la itinerancia de datos
- Configurar la protección frente al restablecimiento de fábrica

Con Intune es más fácil implementar aplicaciones y configuraciones en dispositivos corporativos de Android Enterprise con un perfil de trabajo. Para más detalles sobre Android Enterprise, consulte [Requisitos para usar dispositivos Android en una empresa](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="device-requirements"></a>Requisitos de los dispositivos

Para poder administrarlos como dispositivos de perfil de trabajo corporativos de Android Enterprise, estos deben cumplir los requisitos siguientes:

- Sistema operativo Android, versión 8.0 y posteriores.
- Los dispositivos deben ejecutar una versión de Android que tenga conectividad con Servicios de Google para móviles (GMS). Los dispositivos deben tener GMS disponible y deben ser capaces de conectarse a GMS.

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>Configuración de la administración de dispositivos corporativos de Android Enterprise con un perfil de trabajo

Para configurar la administración de dispositivos corporativos de Android Enterprise con un perfil de trabajo, siga estos pasos:

1. Para prepararse para administrar dispositivos móviles, debe [establecer la entidad de administración de dispositivos móviles (MDM) en **Microsoft Intune**](../fundamentals/mdm-authority-set.md) para obtener instrucciones. Este elemento solo se establece una vez, la primera vez que configura Intune para la administración de dispositivos móviles.
2. [Conecte su cuenta de inquilino de Intune a su cuenta de Google Play administrada](connect-intune-android-enterprise.md).
3. [Cree un perfil de inscripción](#create-an-enrollment-profile).
4. [Cree un grupo de dispositivos](#create-a-device-group).
5. [Inscriba los dispositivos corporativos de perfil de trabajo](#enroll-the-corporate-owned-work-profile-devices).

### <a name="create-an-enrollment-profile"></a>Crear un perfil de inscripción

> [!NOTE]
> Los tokens de los dispositivos corporativos con un perfil de trabajo no expirarán automáticamente. Si un administrador decide revocar un token, el perfil asociado no se mostrará en **Dispositivos** > **Android** > **Inscripción en Android** > **Dispositivos corporativos con un perfil de trabajo (versión preliminar)** . Para ver todos los perfiles asociados con tokens activos e inactivos, haga clic en **Filtro** y active las casillas de los estados de directiva "activo" e "inactivo". 

Se debe crear un perfil de inscripción para que los usuarios puedan inscribir dispositivos corporativos de perfil de trabajo. Al crear el perfil, obtiene un token de inscripción (cadena aleatoria) y un código QR. Según el sistema operativo Android y la versión del dispositivo, puede usar el token o un código QR para [inscribir el dispositivo dedicado](#enroll-the-corporate-owned-work-profile-devices).

1. Inicie sesión en el [centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y elija **Dispositivos** > **Android** > **Inscripción en Android** > **Dispositivos corporativos con un perfil de trabajo (vista preliminar)** .
2. Elija **Crear perfil** y rellene los campos.
    - **Nombre**: escriba el nombre que va a usar al asignar el perfil al grupo de dispositivos dinámicos.
    - **Descripción**: agregue una descripción del perfil (opcional).
3. Elija **Siguiente**.
5. En la página **Revisar y crear**, elija **Crear** para crear la directiva.

### <a name="create-a-device-group"></a>Creación de un grupo de dispositivos

Puede dirigir las aplicaciones y directivas a grupos de dispositivos dinámicos o asignados. Puede configurar grupos de dispositivos dinámicos de Azure AD para que los dispositivos que están inscritos con un perfil de inscripción determinado se rellenen automáticamente. Para ello, siga estos pasos:

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y elija **Grupos** > **Todos los grupos** > **Nuevo grupo**.
2. En la hoja **Grupo**, rellene los campos obligatorios, como se indica a continuación:
    - **Tipo de grupo**: Seguridad
    - **Nombre de grupo**: escriba un nombre intuitivo (como Dispositivos de fábrica 1)
    - **Tipo de pertenencia**: dispositivo dinámico
3. Elija **Agregar una consulta dinámica**.
4. En la hoja **Reglas de pertenencia dinámica**, rellene los campos del modo siguiente:
    - **Agregar regla de pertenencia dinámica**: regla simple
    - **Add devices where** (Agregar dispositivos aquí): enrollmentProfileName
    - En el cuadro central, elija **Igual a**.
    - En el último campo, escriba el nombre del perfil de inscripción que creó anteriormente.
    Para más información sobre las reglas de pertenencia dinámica, vea [Reglas de pertenencia dinámica a grupos de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Elija **Agregar consulta** > **Crear**.

### <a name="revoke-tokens"></a>Revocación de tokens

puede hacer que el token o el código QR expire inmediatamente. A partir de este momento, el código QR o token ya no se puede usar. Puede usar esta opción si:
  - comparte accidentalmente el código QR o token con un tercero no autorizado,
  - finaliza todas las inscripciones y ya no necesita el token o código QR.

La revocación de un código QR o token no tendrá ningún efecto en los dispositivos que ya estén inscritos.

1. Inicie sesión en el [centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y elija **Dispositivos** > **Android** > **Inscripción en Android** > **Dispositivos corporativos con un perfil de trabajo (vista preliminar)** .
2. Elija el perfil con el que quiera trabajar.
3. Elija **Token**.
5. Para revocar el token, elija **Revocar token** > **Sí**.

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>Inscripción de los dispositivos corporativos de perfil de trabajo

Los usuarios ahora pueden [inscribir los dispositivos corporativos de perfil de trabajo](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> La aplicación **Microsoft Intune** se instalará automáticamente durante la inscripción de un dispositivo corporativo con un perfil de trabajo.  Esta aplicación es necesaria para la inscripción y no se puede desinstalar. 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>Administración de aplicaciones en dispositivos corporativos de Android Enterprise de perfil de trabajo

Solo las aplicaciones que tienen el tipo de asignación [establecido en obligatorio](../apps/apps-deploy.md#assign-an-app) se pueden instalar en dispositivos corporativos de perfil de trabajo de Android Enterprise. Las aplicaciones se instalan desde Google Play Store administrado del mismo modo que en los dispositivos de perfil de trabajo Android Enterprise.

Cuando el desarrollador de aplicaciones publica una actualización en Google Play, las aplicaciones se actualizan automáticamente en los dispositivos administrados.

Para quitar una aplicación de dispositivos corporativos de perfil de trabajo de Android Enterprise, puede realizar una de las acciones siguientes:
- Eliminar la implementación obligatoria de la aplicación.
- Crear una implementación de desinstalación de la aplicación.

## <a name="next-steps"></a>Pasos siguientes
- [Implementar aplicaciones Android](../apps/apps-deploy.md)
- [Agregar directivas de configuración de Android](../configuration/device-profiles.md)
