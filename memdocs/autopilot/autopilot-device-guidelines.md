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
ms.openlocfilehash: 326901cef5b337a505d85dc6c5706109ad9cbc1f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908546"
---
# <a name="windows-autopilot-device-guidelines"></a>Instrucciones para dispositivos Windows AutoPilot

**Se aplica a**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>Directrices de procedimientos recomendados de hardware y firmware para Windows AutoPilot

Todos los dispositivos usados con Windows AutoPilot deben cumplir los [requisitos mínimos de hardware](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) para Windows 10.  

Las siguientes prácticas recomendadas garantizan que los dispositivos se puedan aprovisionar fácilmente como parte del proceso de implementación de Windows AutoPilot: 
- Asegúrese de que el TPM 2,0 está habilitado y en un buen estado (no en **modo de funcionalidad reducida**) en los dispositivos diseñados para el modo de Autoimplementación de Windows AutoPilot.
- El OEM aprovisiona información de tupla única (SmbiosSystemManufacturer, SmbiosSystemProductName, SmbiosSystemSerialNumber) o PKID + SmbiosSystemSerialNumber en los [campos de SMBIOS](/windows-hardware/drivers/bringup/smbios) por especificación de Microsoft (fabricante, nombre de producto y número de serie almacenados en el tipo de SMBIOS 1 04H, tipo 1 05H y tipo 1 07H).
- El OEM carga los hashes de hardware 4K obtenidos mediante la herramienta OA3 RS3 + se ejecutan en modo auditoría en el sistema operativo completo a Microsoft a través del informe CBR antes de enviar los dispositivos a un cliente o un socio de canal AutoPilot.
- Microsoft requiere que los controladores de envío de OEM se publiquen en Windows Update dentro de los 30 días siguientes a la presentación de los CBR. El firmware del sistema y las actualizaciones de controladores se publican en Windows Update dentro de 14 días.
- El OEM garantiza que el PKID aprovisionado en el SMBIOS se pasa al canal.

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>Directrices de prácticas recomendadas de software para Windows AutoPilot

- El dispositivo Windows AutoPilot debe preinstalarse solo con controladores de imagen más de Windows 10.
- Puede preinstalar la versión con licencia de Office, como [Microsoft 365 aplicaciones para empresas](/deployoffice/about-office-365-proplus-in-the-enterprise).
- A menos que el cliente lo solicite explícitamente, no se debe incluir ningún otro software preinstalado.
  - Por directiva de OEM, las características de Windows 10, incluidas las aplicaciones integradas, no se deben deshabilitar ni quitar.

## <a name="related-topics"></a>Temas relacionados

[Consentimiento de cliente de Windows AutoPilot](registration-auth.md)<br>
[Guía del escenario de sustitución de la placa base](autopilot-mbr.md)<br>