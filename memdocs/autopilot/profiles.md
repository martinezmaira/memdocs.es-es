---
title: Configuración de perfiles de AutoPilot
description: Obtenga información sobre cómo configurar perfiles de dispositivo para la implementación de Windows AutoPilot.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
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
ms.openlocfilehash: dddabd1408a3f00c472ae787f201f3998c323482
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606566"
---
# <a name="configure-autopilot-profiles"></a>Configuración de perfiles de AutoPilot

**Se aplica a**

-  Windows 10

Debe aplicar un perfil de configuración a cada dispositivo que use el servicio de implementación de Windows AutoPilot. El perfil debe especificar el comportamiento de implementación exacto del dispositivo. Para obtener procedimientos detallados sobre cómo configurar las opciones de perfil y registrar dispositivos, consulte [registrar dispositivos](add-devices.md#registering-devices).

## <a name="profile-settings"></a>Configuración del perfil

Están disponibles las siguientes opciones de perfil:

-  **Omitir las páginas de configuración de registro de Cortana, OneDrive y OEM**. Todos los dispositivos registrados con AutoPilot omitirán automáticamente estas páginas durante el proceso de la experiencia rápida (OOBE).

-  Se **configura automáticamente para el trabajo o la escuela**. Todos los dispositivos registrados con AutoPilot se consideran automáticamente dispositivos de trabajo o escuela, por lo que esta pregunta no aparecerá durante el proceso de OOBE.

-  **Experiencia de inicio de sesión con la personalización de marca de empresa**. En lugar de presentar una página de inicio de sesión de Azure AD genérica, todos los dispositivos registrados con AutoPilot presentarán una página de inicio de sesión personalizada. En esta página se muestra el nombre de la organización, el logotipo y el texto de ayuda adicional, tal y como se ha configurado en Azure AD. Consulte [Agregar personalización de marca de empresa a su directorio](/azure/active-directory/customize-branding#add-company-branding-to-your-directory) para personalizar esta configuración.

-  **Omitir la configuración de privacidad**. Esta configuración de Perfil de AutoPilot opcional permite a las organizaciones no preguntar sobre la configuración de privacidad durante el proceso de OOBE. Esta configuración suele ser deseable para que la organización pueda configurar estas opciones a través de Intune u otra herramienta de administración.

-  **Deshabilite la creación de cuentas de administrador local en el dispositivo**. Las organizaciones pueden decidir si el usuario que configura el dispositivo debe tener acceso de administrador una vez completado el proceso.

-  **Omitir contrato de licencia para el usuario final (CLUF)**. En Windows 10 versión 1709 y versiones posteriores, las organizaciones pueden decidir omitir la página del CLUF presentada durante el proceso de OOBE. Omitir la página del CLUF significa que las organizaciones aceptan los términos del CLUF para sus usuarios.

-  **Deshabilite las características del consumidor de Windows**. En Windows 10 versión 1803 y versiones posteriores, las organizaciones pueden deshabilitar las características del consumidor de Windows. Cuando se deshabilitan las características del consumidor de Windows, el dispositivo no instala automáticamente ninguna aplicación Microsoft Store adicional cuando el usuario inicia sesión por primera vez en el dispositivo. Para obtener más información, consulte la [documentación de MDM](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures).

## <a name="related-topics"></a>Temas relacionados

[Descarga de perfiles](troubleshooting.md#profile-download)<br>
[Registro de dispositivos](add-devices.md)
