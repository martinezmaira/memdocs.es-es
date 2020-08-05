---
title: Novedades de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Lea noticias y recursos sobre las últimas actualizaciones y versiones anteriores de Windows AutoPilot.
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
ms.openlocfilehash: d54377222f2e4ef3776e5a765d730f1e1ab38e37
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757013"
---
# <a name="windows-autopilot-whats-new"></a>Windows AutoPilot: novedades

**Se aplica a**

-   Windows 10

## <a name="windows-autopilot-update-history"></a>Historial de actualizaciones de Windows AutoPilot

Están disponibles las siguientes [actualizaciones de Windows AutoPilot](autopilot-update.md) . **Nota**: las actualizaciones se descargan y aplican automáticamente durante el proceso de implementación de Windows AutoPilot. 

Todavía no hay actualizaciones disponibles. Vuelva aquí para obtener más información.

## <a name="new-in-windows-10-version-2004"></a>Novedad de Windows 10, versión 2004

Con esta versión, puede configurar la Unión híbrida [basada en](user-driven.md) Windows autopilot Azure Active Directory la combinación con la compatibilidad con VPN. Esta compatibilidad también se ha trasladado a Windows 10, versión 1909 y 1903.

Si establece la configuración de idioma en el perfil AutoPilot y el dispositivo está conectado a Ethernet, todos los escenarios omitirán ahora las páginas idioma, configuración regional y teclado. En versiones anteriores, esto solo era compatible con los perfiles de auto-implementación.

## <a name="new-in-windows-10-version-1903"></a>Novedad de Windows 10, versión 1903

La [implementación de Windows AutoPilot para la guante blanca](white-glove.md) es nueva en la versión 1903 de Windows 10. Vea el siguiente vídeo:

<br>

> [!VIDEO https://www.youtube.com/embed/nE5XSOBV0rI]

También novedad en esta versión de Windows:
- La página de estado de inscripción (ESP) de Intune ahora realiza el seguimiento de las extensiones de administración de Intune.
- [Cortana VoiceOver y reconocimiento de voz durante Oobe](windows-autopilot-scenarios.md#cortana-voiceover-and-speech-recognition-during-oobe) está deshabilitado de forma predeterminada para todas las SKU de Windows 10 Pro y Enterprise.
- [Windows AutoPilot se actualiza automáticamente durante Oobe](windows-autopilot-scenarios.md#windows-autopilot-is-self-updating-during-oobe). A partir de las actualizaciones funcionales y críticas del piloto de Windows 10, versión 1903, se iniciará la descarga automática durante OOBE.
- Windows AutoPilot establecerá el nivel de datos de diagnóstico en completo en la versión 1903 de Windows 10 y versiones posteriores durante OOBE. 

## <a name="new-in-windows-10-version-1809"></a>Novedad de Windows 10, versión 1809

El [modo de Autoimplementación de](self-deploying.md) Windows AutoPilot permite una experiencia de aprovisionamiento de dispositivos de toque cero. Simplemente encienda el dispositivo, conéctelo a Ethernet y el dispositivo esté configurado por completo con Windows AutoPilot. Esta capacidad de auto-implementación elimina la necesidad actual de que un usuario final interactúe presionando el botón "siguiente" durante el proceso de implementación. 

Puede utilizar el modo de Autoimplementación de Windows AutoPilot para registrar el dispositivo en un inquilino de AAD, inscribirse en el proveedor de MDM de su organización y aprovisionar directivas y aplicaciones, todo ello sin necesidad de autenticación de usuario o interacción del usuario. 

>[!NOTE]
>Se requiere Windows 10, versión 1903 o posterior para usar el modo de implementación automática debido a problemas con la atestación de dispositivo de TPM en Windows 10, versión 1809.

## <a name="related-topics"></a>Temas relacionados

[Novedades de Microsoft Intune](https://docs.microsoft.com/intune/whats-new)<br>
[Novedades de Windows 10](https://docs.microsoft.com/windows/whats-new/)
