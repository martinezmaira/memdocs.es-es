---
title: Conflictos de directivas de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Infórmese sobre los conflictos de directivas que se pueden producir durante la implementación de Windows AutoPilot.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: mtniehaus
ms.author: mniehaus
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 1f839f128dc869f7c9a4619237de0c33a21d66e1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606582"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows AutoPilot: conflictos de directivas

**Se aplica a**

- Windows 10

Hay un número significativo de configuraciones de directiva disponibles para Windows 10, entre las que se incluyen:
- Directivas MDM nativas
- Configuración de directiva de grupo (con respaldo de ADMX)

Algunas configuraciones de Directiva pueden causar problemas en algunos escenarios de Windows AutoPilot. Estos problemas pueden surgir debido a la manera en que las directivas cambian el comportamiento de Windows 10. Si encuentra alguno de estos problemas, quite la Directiva en cuestión para resolver el problema.

<table>
<th>Directiva<th>Más información

<tr><td width="50%">Restricción de dispositivo/ <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">Directiva de contraseñas</a></td>
<td>El inicio de sesión automático de la experiencia rápida (OOBE) o del escritorio del usuario puede producir un error cuando se reinicia un dispositivo durante la página de estado de inscripción de dispositivos (ESP). Este error puede producirse cuando se aplican determinadas <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">directivas de DeviceLock</a> a un dispositivo. Estas directivas pueden incluir:<ul><li>Longitud mínima de la contraseña y complejidad de la contraseña</li><li>Cualquier configuración de directiva de grupo similar (incluida cualquier que deshabilite el inicio de sesión automático)</li></ul>
Este posible error es especialmente cierto en escenarios quioscos en los que se generan automáticamente contraseñas.</td>

<tr><td width="50%"><a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Comportamiento de petición de elevación de administrador</a> y línea de base de seguridad de Windows 10
<br>Línea de base de seguridad de Windows 10/ <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">requerir el modo de aprobación de administrador para administradores</a></td>
<td>Pueden aparecer más mensajes al modificar la configuración de control de cuentas de usuario (UAC) durante la OOBE mediante la página de estado de inscripción de dispositivos (ESP). Es más probable que se produzcan más solicitudes si el dispositivo se reinicia después de aplicar las directivas. Para solucionar este problema, las directivas se pueden destinar a los usuarios en lugar de a los dispositivos para que se apliquen posteriormente en el proceso.</td>

<tr><td width="50%">Restricciones de dispositivos/nube y almacenamiento/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">ayudante para el inicio de sesión de la cuenta Microsoft</a></td>
<td>Si se establece esta directiva en "deshabilitado", se deshabilitará el servicio ayudante para el inicio de sesión de Microsoft (wlidsvc). Windows AutoPilot requiere este servicio para obtener el perfil de Windows AutoPilot.</td>

</table>

## <a name="related-topics"></a>Temas relacionados

[Solución de problemas de Windows AutoPilot](troubleshooting.md)
