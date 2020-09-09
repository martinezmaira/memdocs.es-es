---
title: Novedades de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Lea noticias y recursos sobre las últimas actualizaciones y versiones anteriores de Windows AutoPilot.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
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
ms.openlocfilehash: 736e01696cf503b63762c32a9acee3cb68c1e241
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606559"
---
# <a name="windows-autopilot-whats-new"></a>Windows AutoPilot: novedades

**Se aplica a**

- Windows 10

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
- Windows AutoPilot establecerá el nivel de datos de diagnóstico en Full durante OOBE en los dispositivos que ejecutan Windows 10, versión 1903 o posterior. 

## <a name="new-in-windows-10-version-1809"></a>Novedad de Windows 10, versión 1809

El [modo de Autoimplementación de](self-deploying.md) Windows AutoPilot es un proceso de aprovisionamiento de dispositivos sin interacción. Simplemente encienda el dispositivo, conéctese a Ethernet y AutoPilot configura automáticamente el dispositivo. Los usuarios finales no tienen que presionar el botón "siguiente" durante el proceso de implementación. 

Puede usar el modo de Autoimplementación de Windows AutoPilot para registrar el dispositivo en un inquilino de AAD, inscribirse en el proveedor de MDM de la organización y aprovisionar directivas y aplicaciones. No se requiere autenticación de usuario ni interacción del usuario.

>[!NOTE]
>Se requiere Windows 10, versión 1903 o posterior para usar el modo de implementación automática debido a problemas con la atestación de dispositivo de TPM en Windows 10, versión 1809.

## <a name="related-topics"></a>Temas relacionados

[Novedades de Microsoft Intune](/intune/whats-new)<br>
[Novedades de Windows 10](/windows/whats-new/)
