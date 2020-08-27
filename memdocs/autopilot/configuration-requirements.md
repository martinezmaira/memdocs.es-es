---
title: Requisitos de configuración de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Infórmese sobre los requisitos de configuración para la implementación de Windows AutoPilot.
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
ms.openlocfilehash: 8731532ff052c626514d9f1a80e3a93c0cbde6dc
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908323"
---
# <a name="windows-autopilot-configuration-requirements"></a>Requisitos de configuración de Windows AutoPilot

**Se aplica a: Windows 10**

Antes de poder usar Windows AutoPilot, es necesario realizar algunas tareas de configuración para admitir los escenarios comunes de la prueba piloto. 

- Configure Azure Active Directory la inscripción automática. Para obtener Microsoft Intune, consulte [habilitación de la inscripción automática de Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment) para obtener más información. Si usa otro servicio MDM, póngase en contacto con el proveedor para obtener las direcciones URL específicas o la configuración necesaria para esos servicios.
- Configure Azure Active Directory la personalización de marca personalizada. Para mostrar una página de inicio de sesión específica de la organización, debe configurar Azure Active Directory con las imágenes y el texto que desea mostrar. Para obtener más información, consulte [Inicio rápido: agregar personalización de marca de empresa a la página de inicio de sesión en Azure ad](/azure/active-directory/fundamentals/customize-branding). Los elementos clave para AutoPilot incluyen el "logotipo cuadrado", "texto de la página de inicio de sesión" y Azure Active Directory nombre de inquilino. El nombre del inquilino se configura por separado en las propiedades del inquilino de Azure AD.
- Opcional: para pasar automáticamente de Windows 10 Pro a Windows 10 Enterprise, habilite la [activación](/windows/deployment/windows-10-enterprise-subscription-activation)de la suscripción de Windows.

Los escenarios específicos tendrán requisitos adicionales. Por lo general, hay dos tareas específicas:

- Registro de dispositivos. Los dispositivos deben agregarse a Windows AutoPilot para admitir la mayoría de los escenarios de Windows AutoPilot. Para obtener más información, consulte [Agregar dispositivos a Windows AutoPilot](add-devices.md).
- Configuración del perfil. Una vez que se han agregado dispositivos a Windows AutoPilot, es necesario aplicar un perfil de configuración a cada dispositivo. Consulte [configuración de perfiles de AutoPilot](profiles.md) para más información.  Microsoft Intune puede automatizar esta asignación de perfil. Para obtener más información, consulte [crear un grupo de dispositivos AutoPilot](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) y [asignar un perfil de implementación AutoPilot a un grupo de dispositivos](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group).

Para obtener más información, consulte [escenarios de Windows AutoPilot](windows-Autopilot-scenarios.md).

Para ver un tutorial sobre algunos de estos pasos relacionados, consulte este vídeo:

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


No hay ningún requisito de hardware adicional para usar Windows 10 AutoPilot, más allá de los [requisitos para ejecutar Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

**Pasos siguientes**

[Información general de Windows AutoPilot](windows-autopilot.md)