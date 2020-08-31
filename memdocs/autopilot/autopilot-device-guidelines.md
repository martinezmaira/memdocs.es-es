---
title: Instrucciones para dispositivos Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Obtenga información acerca de los procedimientos recomendados de hardware, firmware y software para la implementación de Windows AutoPilot.
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
ms.openlocfilehash: eb591206ad61878bc2637bf1a10c2a1cec17ddba
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057367"
---
# <a name="windows-autopilot-device-guidelines"></a>Instrucciones para dispositivos Windows AutoPilot

**Se aplica a**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>Directrices de procedimientos recomendados de hardware y firmware para Windows AutoPilot

Todos los dispositivos que usan Windows AutoPilot deben cumplir los [requisitos mínimos de hardware](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) para Windows 10.  

Las siguientes prácticas recomendadas garantizan que los dispositivos se puedan aprovisionar fácilmente como parte del proceso de implementación de Windows AutoPilot: 
- TPM 2,0 está habilitado y en un estado correcto (no en **modo de funcionalidad reducida**) en los dispositivos diseñados para el modo de Autoimplementación de Windows AutoPilot.
- El OEM debe proporcionar cualquiera de los siguientes datos en los [campos de SMBIOS](/windows-hardware/drivers/bringup/smbios). La información debe seguir las especificaciones de Microsoft (fabricante, nombre de producto y número de serie almacenado en el tipo de SMBIOS 1 04h, escriba 1 05h y escriba 1 07H).
    - Información de tupla única (SmbiosSystemManufacturer, SmbiosSystemProductName, SmbiosSystemSerialNumber)
    - PKID + SmbiosSystemSerialNumber
- Antes de enviar dispositivos a un cliente o un asociado de canal de AutoPilot, el OEM debe cargar los hashes de hardware 4K en Microsoft mediante el informe CBR. Los hashes se deben recopilar mediante la herramienta OA3 RS3 + ejecutar en modo auditoría en el sistema operativo completo.
- Microsoft requiere que los controladores de envío de OEM se publiquen en Windows Update en un plazo de 30 días a partir de la fecha de envío CBR. El firmware del sistema y las actualizaciones de controladores se publican en Windows Update dentro de 14 días.
- El OEM garantiza que el PKID aprovisionado en el SMBIOS se pasa al canal.

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>Directrices de prácticas recomendadas de software para Windows AutoPilot

- El dispositivo Windows AutoPilot debe preinstalarse solo con controladores de imagen más de Windows 10.
- Puede preinstalar la versión con licencia de Office, como [Microsoft 365 aplicaciones para empresas](/deployoffice/about-office-365-proplus-in-the-enterprise).
- A menos que el cliente lo solicite explícitamente, no se debe incluir ningún otro software preinstalado.
  - Por directiva de OEM, las características de Windows 10, incluidas las aplicaciones integradas, no se deben deshabilitar ni quitar.

## <a name="next-steps"></a>Pasos siguientes

[Consentimiento de cliente de Windows AutoPilot](registration-auth.md)<br>
[Guía del escenario de sustitución de la placa base](autopilot-mbr.md)<br>