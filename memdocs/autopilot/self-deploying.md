---
title: Modo autoimplementado de Windows AutoPilot
description: El modo de auto-implementación permite que un dispositivo se implemente con poca interacción del usuario. Este modo está diseñado para implementar Windows 10 como un quiosco, un dispositivo de señal digital o un dispositivo compartido.
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
ms.openlocfilehash: 13b45b972ed17d24efedaa048c0e48ea2f2d90d2
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568611"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Modo autoimplementado de Windows AutoPilot

**Se aplica a: Windows 10, versión 1903 o posterior**

El modo de Autoimplementación de Windows AutoPilot permite implementar un dispositivo con poca interacción del usuario. En el caso de los dispositivos con una conexión Ethernet, no se requiere ninguna interacción del usuario. En el caso de los dispositivos conectados a través de Wi-Fi, el usuario solo debe:
- Elija el idioma, la configuración regional y el teclado.
- Establecer una conexión de red. 

El modo de auto-implementación proporciona lo siguiente:
- Une el dispositivo a Azure Active Directory.
- Inscribe el dispositivo en Intune (u otro servicio MDM) mediante Azure AD para la inscripción automática de MDM.
- Garantiza que todas las directivas, las aplicaciones, los certificados y los perfiles de red se aprovisionan en el dispositivo.
- Usa la página estado de inscripción para impedir el acceso hasta que el dispositivo esté totalmente aprovisionado.

>[!NOTE]
>El modo de auto-implementación no admite Active Directory join ni Unión a Azure AD híbrido. Todos los dispositivos se unirán a Azure Active Directory.

El modo de auto-implementación permite implementar un dispositivo de Windows 10 como un quiosco, un dispositivo de señal digital o un dispositivo compartido.

Puede usar el [Explorador quiosco](https://www.microsoft.com/p/kiosk-browser/9ngb5s5xg2kp?rtc=1&activetab=pivot:overviewtab) al configurar un dispositivo de pantalla completa. Esta aplicación se basa en Microsoft Edge y se puede usar para crear una experiencia de exploración personalizada y administrada por MDM.

Puede automatizar completamente la configuración del dispositivo combinando el modo de autodeploing con las directivas de MDM. Use las directivas de MDM para crear una cuenta local configurada para iniciar sesión automáticamente. Para obtener más información, consulte:
- [Simplificación de la administración de quioscos con Windows 10](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/simplifying-kiosk-management-for-it-with-windows-10/ba-p/187691).
- [Configure un quiosco o un inicio de sesión digital en Intune u otro servicio MDM](/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service).

>[!NOTE]
>El modo de auto-implementación no asocia actualmente un usuario con el dispositivo (ya que no se especifica ningún identificador de usuario ni contraseña como parte del proceso). Como resultado, es posible que algunas funcionalidades de Azure AD e Intune (como la recuperación de BitLocker, la instalación de aplicaciones desde el Portal de empresa o el acceso condicional) no estén disponibles para un usuario que inicie sesión en el dispositivo. Para obtener más información, consulte [escenarios y capacidades de Windows AutoPilot](windows-autopilot-scenarios.md) y [configuración del algoritmo de cifrado de BitLocker para dispositivos AutoPilot](bitlocker.md).

![La experiencia del usuario con el modo de Autoimplementación de Windows AutoPilot](images/self-deploy-welcome.png)

## <a name="requirements"></a>Requisitos

El modo de auto-implementación usa el hardware de TPM 2,0 del dispositivo para autenticar el dispositivo en el inquilino de Azure AD de una organización. Por lo tanto, los dispositivos sin TPM 2,0 no se pueden usar con este modo. Los dispositivos también deben admitir la atestación de dispositivo de TPM. Todos los dispositivos Windows nuevos deben cumplir estos requisitos.

>[!IMPORTANT]
>Si intenta realizar una implementación de modo de implementación automática en un dispositivo que no admite TPM 2,0 o en una máquina virtual, se producirá un error en el proceso al comprobar el dispositivo con un error de tiempo de espera de 0x800705B4 (no se admiten los TPM virtuales de Hyper-V). Tenga en cuenta también que se requiere la versión 1903 o posterior de Windows para usar el modo de implementación automática debido a problemas con la atestación del dispositivo de TPM en Windows 10, versión 1809. Dado que Windows 10 Enterprise 2019 LTSC se basa en Windows 10 versión 1809, el modo de Autoimplementación no se admite también en Windows 10 Enterprise 2019 LTSC. Consulte [problemas conocidos de Windows AutoPilot](known-issues.md) para revisar otros errores y soluciones conocidos.

Puede mostrar un logotipo específico de la organización y el nombre de la organización durante el proceso de AutoPilot. Para ello, Azure AD la personalización de marca de empresa debe configurarse con las imágenes y el texto que desea mostrar. Consulte [Inicio rápido: agregar personalización de marca de empresa a la página de inicio de sesión en Azure ad](/azure/active-directory/fundamentals/customize-branding) para obtener más detalles. 

## <a name="step-by-step"></a>Paso a paso

Para realizar la implementación en modo de implementación automática de Windows AutoPilot, deben realizarse los siguientes pasos de preparación:

1. Cree un perfil AutoPilot para el modo de auto-implementación con la configuración que desee. En Microsoft Intune, este modo se elige explícitamente al crear el perfil. No es posible crear un perfil en el Microsoft Store para la empresa o el centro de partners para el modo de auto-implementación.
2. Si usa Intune, cree un grupo de dispositivos en Azure Active Directory y asigne el perfil de AutoPilot a ese grupo. Asegúrese de que el perfil se ha asignado al dispositivo antes de intentar implementar ese dispositivo.
3. Arranque el dispositivo, conectándolo a Wi-Fi, si es necesario, y espere a que se complete el proceso de aprovisionamiento.

## <a name="validation"></a>Validación

Al usar Windows AutoPilot para implementar en modo de implementación automática, se debe observar la siguiente experiencia del usuario final:

-  Una vez conectado a una red, se descargará el perfil AutoPilot.
- Si está conectado a Ethernet y el perfil AutoPilot está configurado para omitirlos, no se mostrarán las siguientes páginas: idioma, configuración regional y distribución del teclado. De lo contrario, se requieren pasos manuales:
  -  Si hay varios idiomas preinstalados en Windows 10, el usuario debe elegir un idioma.
  -  El usuario debe elegir una configuración regional y una distribución del teclado y, opcionalmente, una segunda distribución del teclado.
-  Si se conecta a través de Ethernet, no se espera ningún mensaje de red. Si no hay ninguna conexión Ethernet disponible y Wi-Fi está integrado, el usuario debe conectarse a una red inalámbrica.
-  Windows 10 comprobará si hay actualizaciones de OOBE críticas y, si hay alguna disponible, se instalarán automáticamente (si es necesario, se reiniciarán).
-  El dispositivo se unirá Azure Active Directory.
-  Después de unirse Azure Active Directory, el dispositivo se inscribe en Intune (u otros servicios MDM configurados).
-  Se mostrará la [Página estado de inscripción](enrollment-status.md) .
-  En función de la configuración del dispositivo implementada, el dispositivo hará lo siguiente:
  -  Permanece en la pantalla de inicio de sesión, donde cualquier miembro de la organización puede iniciar sesión especificando sus credenciales de Azure AD.
  -  Inicie sesión automáticamente como una cuenta local para los dispositivos configurados como pantalla completa o de señalización digital.

>[!NOTE]
>La implementación de directivas de EAS mediante el modo de auto-implementación para implementaciones de quiosco producirá un error en la funcionalidad de inicio de sesión automático. 

En caso de que los resultados observados no coincidan con estas expectativas, consulte la documentación de [solución de problemas de Windows AutoPilot](troubleshooting.md) .
