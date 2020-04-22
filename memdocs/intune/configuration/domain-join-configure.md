---
title: Configuración de un perfil de unión a un dominio para Windows 10 en Microsoft Intune - Azure | Microsoft Docs
description: Cree un perfil de configuración de dispositivo de unión a un dominio para dispositivos híbridos unidos a Azure AD. Use este perfil para implementar información de dominio de Active Directory local en dispositivos aprovisionados con Windows AutoPilot y Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "79364401"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Configuración de una unión a dominio para dispositivos híbridos unidos a Azure AD en Microsoft Intune

Muchos entornos usan una instancia local de Active Directory (AD). Cuando los dispositivos unidos a un dominio de AD se unen también Azure AD, se les denomina dispositivos unidos a Azure AD híbridos. Con Windows AutoPilot, puede [inscribir dispositivos unidos a Azure AD híbridos](../enrollment/windows-autopilot-hybrid.md) en Intune. Para inscribirlos, necesitará también un perfil de configuración de **unión a un dominio**.

Un perfil de configuración de **unión a un dominio** configura la información de dominio de la instancia local de Active Directory. Cuando los dispositivos se aprovisionan (normalmente, sin conexión), este perfil implementa los detalles de dominio de AD para que los dispositivos sepan a qué dominio local deben unirse. Si no se crea un perfil de unión a un dominio, es posible que estos dispositivos no puedan implementarse.

Esta característica se aplica a:

- Windows 10 y versiones posteriores
- Dispositivos unidos a Azure AD híbridos
- Implementación híbrida con AutoPilot+Intune

En este artículo se explica cómo crear un perfil de unión a un dominio de una implementación de AutoPilot híbrida. También puede ver la configuración disponible.

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para la directiva. Asígnele un nombre a las directivas para que pueda identificarlas de manera sencilla más adelante. Por ejemplo, un nombre de directiva válido es **Windows 10: Perfil de unión a un dominio que incluye información de dominio local para inscribir dispositivos unidos a AD híbridos con Windows AutoPilot**.
    - **Descripción**: escriba una descripción para la directiva. Esta configuración es opcional pero recomendada.
    - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
    - **Tipo de perfil**: seleccione **Unión a un dominio (versión preliminar)** .

4. Seleccione **Configuración**. Escriba las propiedades siguientes:

    - **Prefijo de nombre de equipo**: escriba un prefijo para el nombre del dispositivo. Los nombres de equipo tienen una longitud de 15 caracteres. Después del prefijo, los 15 caracteres restantes se generan de forma aleatoria.
    - **Nombre de dominio**: escriba el nombre de dominio completo (FQDN) al que se van a unir los dispositivos. Por ejemplo, escriba `americas.corp.contoso.com.`.
    - **Unidad organizativa** (opcional): Escriba la ruta de acceso completa ([nombre distintivo](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) que lleva a la unidad organizativa (OU) donde se van a crear las cuentas de equipo. Por ejemplo, escriba `"CN=Users,DC=Contoso,DC=com"`. Si no especifica un valor, se usa un contenedor de objetos de equipo conocido.

      Para obtener más información y consejos sobre esta configuración, vea [Implementación de dispositivos unidos a Azure AD híbridos](../enrollment/windows-autopilot-hybrid.md).

5. Cuando haya terminado, seleccione **Aceptar** > **Crear** para guardar los cambios.

El perfil se crea y se muestra en la lista de perfiles. Ya está listo para [implementar dispositivos unidos a Azure AD híbridos mediante Intune y Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Pasos siguientes

Una vez creado el perfil, está listo para asignarlo. Después, [asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

[Implementación de dispositivos unidos a Azure AD híbridos mediante Intune y Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).
