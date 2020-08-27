---
title: Conflictos de directivas de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Infórmese sobre los problemas conocidos que pueden producirse durante la implementación de Windows AutoPilot.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
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
ms.openlocfilehash: 23c5c9c0fd025279f1c97b6f19673f9e8b527adb
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907983"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows AutoPilot: conflictos de directivas

**Se aplica a**

- Windows 10

Hay un número significativo de configuraciones de directiva disponibles para Windows 10, como directivas de MDM nativas y configuración de directiva de grupo (con respaldo de ADMX). Algunos de ellos pueden provocar problemas en ciertos escenarios de Windows AutoPilot como resultado de la forma en que cambian el comportamiento de Windows 10. Si encuentra alguno de estos problemas, quite la Directiva en cuestión para resolver el problema.

<table>
<th>Directiva<th>Más información

<tr><td width="50%">Restricción de dispositivo/ <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">Directiva de contraseñas</a></td>
<td>Cuando ciertas <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">directivas de DeviceLock</a>, como la longitud mínima de la contraseña y la complejidad de la contraseña, o cualquier configuración de directiva de grupo similar (incluida la que deshabilite el inicio de sesión automático) se aplican a un dispositivo y el dispositivo se reinicia durante la página de estado de inscripción (ESP) del dispositivo, el inicio de sesión automático de la configuración rápida (OOBE) o el inicio de  Esto es especialmente cierto en escenarios quioscos en los que las contraseñas se generan automáticamente.</td>

<tr><td width="50%"><a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Comportamiento de petición de elevación de administrador</a> y línea de base de seguridad de Windows 10
<br>Línea de base de seguridad de Windows 10/ <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">requerir el modo de aprobación de administrador para administradores</a></td>
<td>Al modificar la configuración del control de cuentas de usuario (UAC) durante la configuración de la aplicación mediante la página de estado de inscripción de dispositivos (ESP), es posible que se produzcan más solicitudes de UAC, especialmente si el dispositivo se reinicia después de aplicar estas directivas, lo que permite que surtan efecto.  Para solucionar este problema, las directivas se pueden destinar a los usuarios en lugar de a los dispositivos para que se apliquen posteriormente en el proceso.</td>

<tr><td width="50%">Restricciones de dispositivos/nube y almacenamiento/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">ayudante para el inicio de sesión de la cuenta Microsoft</a></td>
<td>Si se establece esta directiva en "deshabilitado", se deshabilitará el servicio ayudante para el inicio de sesión de Microsoft (wlidsvc).  Windows AutoPilot requiere este servicio para obtener el perfil de Windows AutoPilot.</td>

</table>

## <a name="related-topics"></a>Temas relacionados

[Solución de problemas de Windows AutoPilot](troubleshooting.md)