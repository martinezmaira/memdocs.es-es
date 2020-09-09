---
title: Administración de DFCI
ms.reviewer: ''
manager: laurawi
description: Con la implementación de Windows AutoPilot e Intune, puede administrar la configuración de UEFI (BIOS) una vez que se ha inscrito mediante la interfaz de configuración de firmware del dispositivo (DFCI).
keywords: AutoPilot, DFCI, UEFI, Windows 10
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 95979a3c53752bb77c31710e20de54dbc2781262
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606617"
---
# <a name="device-firmware-configuration-interface-dfci-management"></a>Administración de la interfaz de configuración de firmware del dispositivo (DFCI)

**Se aplica a**

- Windows 10

Con la implementación de Windows AutoPilot e Intune, puede administrar la configuración de Unified Extensible Firmware Interface (UEFI) una vez que se ha inscrito mediante la interfaz de configuración de firmware del dispositivo (DFCI). DFCI [permite a Windows pasar comandos de administración](/windows/client-management/mdm/uefi-csp) de Intune a UEFI para dispositivos implementados con AutoPilot. Esta funcionalidad permite limitar el control del usuario final de la configuración del BIOS. Por ejemplo, puede bloquear las opciones de arranque para impedir que los usuarios arranquen otro sistema operativo, como uno que no tenga las mismas características de seguridad.

Si un usuario vuelve a instalar una versión anterior de Windows, instala un sistema operativo independiente o formatea el disco duro, no puede invalidar la administración de DFCI. Esta característica también puede impedir que el malware se comunique con los procesos del sistema operativo, incluidos los procesos de sistema operativo elevados. La cadena de confianza de DFCI utiliza criptografía de clave pública y no depende de la seguridad de contraseñas de UEFI local. Este nivel de seguridad impide que los usuarios locales tengan acceso a la configuración administrada desde los menús UEFI del dispositivo.

Para obtener información general sobre las ventajas, los escenarios y los requisitos previos de DFCI, consulte Introducción a la [interfaz de configuración de firmware (DFCI)](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/).

## <a name="dfci-management-lifecycle"></a>Ciclo de vida de administración de DFCI

El ciclo de vida de administración de DFCI incluye los siguientes procesos:
- Integración de UEFI
- Registro de dispositivos
- Creación de perfiles
- Inscripción
- Administración
- Retirada
- Recuperación

Consulte la siguiente figura.

 ![Ciclo de vida](images/dfci.png)

## <a name="requirements"></a>Requisitos

- Se requiere Windows 10, versión 1809 o posterior y un UEFI compatible.
- El fabricante del dispositivo debe tener DFCI agregado a su firmware UEFI en el proceso de fabricación o como una actualización de firmware que instale. Trabaje con los proveedores de dispositivos para determinar los [fabricantes que admiten DFCI](#oems-that-support-dfci)o la versión de firmware necesaria para usar DFCI.
- El dispositivo debe administrarse con Microsoft Intune. Para obtener más información, consulte [inscribir dispositivos Windows en Intune mediante Windows AutoPilot](/intune/enrollment/enrollment-autopilot).
- El dispositivo debe estar registrado para Windows Autopilot por un [asociado de Proveedor de soluciones en la nube (CSP) de Microsoft](https://partner.microsoft.com/membership/cloud-solution-provider) o registrado directamente por el OEM. 

>[!IMPORTANT]
>Los dispositivos registrados manualmente para el piloto automático (por ejemplo, mediante [la importación desde un archivo CSV](/intune/enrollment/enrollment-autopilot#add-devices)) no pueden usar DFCI. Por diseño, la administración de DFCI requiere la atestación externa de la adquisición comercial del dispositivo a través de un OEM o un registro de asociado de CSP de Microsoft en Windows Autopilot. Una vez registrado el dispositivo, el número de serie se muestra en la lista de dispositivos Windows AutoPilot.

## <a name="managing-dfci-profile-with-windows-autopilot"></a>Administración del perfil de DFCI con Windows AutoPilot

Hay cuatro pasos básicos en la administración del perfil de DFCI con Windows AutoPilot:

1. Crear un perfil de AutoPilot
2. Crear un perfil de página de estado de inscripción
3. Creación de un perfil de DFCI
4. Asignación de los perfiles

Consulte [creación de perfiles](/intune/configuration/device-firmware-configuration-interface-windows#create-the-profiles) y [asignación de perfiles y reinicio](/intune/configuration/device-firmware-configuration-interface-windows#assign-the-profiles-and-reboot) para obtener más información.

También puede [cambiar la configuración existente de DFCI](/intune/configuration/device-firmware-configuration-interface-windows#update-existing-dfci-settings) en los dispositivos que están en uso. En el perfil de DFCI existente, cambie la configuración y guarde los cambios. Puesto que el perfil ya está asignado, la nueva configuración de DFCI surte efecto la próxima vez que el dispositivo se sincronice o se reinicie el dispositivo.

## <a name="oems-that-support-dfci"></a>OEM que admiten DFCI

- [Microsoft Surface](/surface/surface-manage-dfci-guide)

Hay otros OEM pendientes.

## <a name="see-also"></a>Consulte también

[Escenarios de Microsoft DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/)<br>
[Windows AutoPilot y dispositivos Surface](/surface/windows-autopilot-and-surface-devices)<br>
