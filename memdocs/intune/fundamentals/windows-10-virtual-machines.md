---
title: Uso de máquinas virtuales Windows 10 con Microsoft Intune
titleSuffix: ''
description: Directrices para el uso de máquinas virtuales Windows 10 con Microsoft Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 944b3d98dc59dcae69f72fef5dfdb1793701f67a
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126158"
---
# <a name="using-windows-10-virtual-machines-with-intune"></a>Uso de máquinas virtuales Windows 10 con Intune

Intune admite la administración de máquinas virtuales que ejecutan Windows 10 Enterprise con algunas limitaciones. La administración de Intune no depende de la administración de Windows Virtual Desktop de la misma máquina virtual ni interfiere con este proceso.

Al administrar máquinas virtuales Windows 10 con Intune, tenga en cuenta los puntos siguientes:

- La sesión múltiple de Windows 10 Enterprise (Enterprise para dispositivos virtuales), tal y como se usa en Windows Virtual Desktop, no admite actualmente la administración de Intune.

## <a name="enrollment"></a>Inscripción
- No se recomienda administrar máquinas virtuales de host de sesión a petición con Intune. Cada máquina virtual creada debe inscribirse. Además, la eliminación periódica de máquinas virtuales dejará registros de dispositivos huérfanos en Intune hasta que se [limpien](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules). 
- Los tipos de implementación automática de Windows AutoPilot y White Glove no se admiten porque requieren un Módulo de plataforma segura (TPM) físico. 
- La inscripción en la experiencia rápida (OOBE) no se admite en máquinas virtuales a las que solo se pueda acceder mediante RDP (como es el caso de las máquinas virtuales hospedadas en Azure). Esta restricción significa lo siguiente:
    - Windows Autopilot y la OOBE comercial no se admiten.
    - No se admiten las opciones de página de estado de inscripción para las directivas de contexto de dispositivo.


## <a name="configuration"></a>Configuración
Intune no admite ninguna configuración que use un Módulo de plataforma segura o administración de hardware, lo que incluye:
- [Configuración de BitLocker](../configuration/device-profiles.md#endpoint-protection)
- [Configuración de la interfaz de configuración de firmware del dispositivo](../configuration/device-profiles.md#device-firmware-configuration-interface)

## <a name="reporting"></a>Generación de informes
Intune detecta automáticamente las máquinas virtuales y las notifica como "máquina virtual" en **Dispositivos** > **Todos los dispositivos** > elija un dispositivo > campo **Información general** > **Modelo**. 

Las máquinas virtuales desasignadas pueden contribuir a los informes de dispositivos no conformes porque no pueden [registrarse con el servicio Intune](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="retirement"></a>Retirada
Si solo tiene acceso RDP, no use la [acción de borrado](../remote-actions/devices-wipe.md#wipe). La acción de borrado eliminará la configuración de RDP de la máquina virtual e impedirá que se vuelva a conectar.


