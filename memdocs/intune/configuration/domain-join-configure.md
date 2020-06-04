---
title: Configuración de un perfil de unión a un dominio para Windows 10 en Microsoft Intune - Azure | Microsoft Docs
description: Cree un perfil de configuración de dispositivo de unión a un dominio para dispositivos híbridos unidos a Azure AD. Use este perfil para implementar información de dominio de Active Directory local en dispositivos aprovisionados con Windows AutoPilot y Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 211722a02183d3b86525468f907d4093331d9de6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988431"
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

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
    - **Perfil**: seleccione **Unión a un dominio (versión preliminar)** .

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para la directiva. Asígnele un nombre a las directivas para que pueda identificarlas de manera sencilla más adelante. Por ejemplo, un nombre de directiva válido es **Windows 10: Perfil de unión a un dominio que incluye información de dominio local para inscribir dispositivos unidos a AD híbridos con Windows AutoPilot**.
    - **Descripción**: escriba una descripción para la directiva. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.
7. En **Opciones de configuración**, escriba las siguientes propiedades:

    - **Prefijo de nombre de equipo**: escriba un prefijo para el nombre del dispositivo. Los nombres de equipo tienen una longitud de 15 caracteres. Después del prefijo, los 15 caracteres restantes se generan de forma aleatoria.
    - **Nombre de dominio**: escriba el nombre de dominio completo (FQDN) al que se van a unir los dispositivos. Por ejemplo, escriba `americas.corp.contoso.com.`.
    - **Unidad organizativa** (opcional): Escriba la ruta de acceso completa ([nombre distintivo](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) que lleva a la unidad organizativa (OU) donde se van a crear las cuentas de equipo. Por ejemplo, escriba `"CN=Users,DC=Contoso,DC=com"`. Si no especifica un valor, se usa un contenedor de objetos de equipo conocido.

      Para obtener más información y consejos sobre esta configuración, vea [Implementación de dispositivos unidos a Azure AD híbridos](../enrollment/windows-autopilot-hybrid.md).

8. Seleccione **Siguiente**.

9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione los usuarios o el grupo de usuarios que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

Ya está listo para [implementar dispositivos unidos a Azure AD híbridos mediante Intune y Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Pasos siguientes

Después de [asignar](device-profile-assign.md) el perfil, [supervise su estado](device-profile-monitor.md).

[Implementación de dispositivos unidos a Azure AD híbridos mediante Intune y Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).
