---
title: Establecer el algoritmo de cifrado de BitLocker para dispositivos AutoPilot
ms.reviewer: ''
manager: laurawi
description: Microsoft Intune proporciona un conjunto completo de opciones de configuración para administrar BitLocker en dispositivos Windows 10.
keywords: AutoPilot, BitLocker, cifrado, 256 bits, Windows 10
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
ms.openlocfilehash: f72410d0570e1b9ebbc324f26a288100e744f422
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056994"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>Establecer el algoritmo de cifrado de BitLocker para dispositivos AutoPilot

**Se aplica a**

-  Windows 10

Con Windows AutoPilot, puede configurar las opciones de cifrado de BitLocker para que se apliquen antes de que se inicie el cifrado automático. Esta configuración garantiza que el algoritmo de cifrado predeterminado no se aplica automáticamente. También se pueden aplicar otras directivas de BitLocker antes de que se inicie el cifrado automático de BitLocker. 

El algoritmo de cifrado de BitLocker se usa cuando BitLocker se habilita por primera vez. El algoritmo establece la intensidad del cifrado de volumen completo. Los algoritmos de cifrado disponibles son: AES-CBC 128-bit, AES-CBC 256-bit, XTS-AES 128 bits o cifrado XTS-AES 256-bit. El valor predeterminado es XTS-AES 128-bit Encryption. Consulte [CSP de BitLocker](/windows/client-management/mdm/bitlocker-csp) para obtener información sobre los algoritmos de cifrado recomendados que se deben usar.

Para asegurarse de que el algoritmo de cifrado de BitLocker que desea está establecido antes de que se produzca el cifrado automático en los dispositivos AutoPilot:

1. Establezca la [configuración del método de cifrado](/intune/endpoint-protection-windows-10#windows-encryption) en el perfil de Endpoint Protection de Windows 10 en el algoritmo de cifrado que desee. 
2. [Asigne la Directiva](/intune/device-profile-assign) a su grupo de dispositivos AutoPilot. La Directiva de cifrado debe estar asignada a los **dispositivos** del grupo, no a los usuarios.
3. Habilite la página de [Estado de inscripción](enrollment-status.md) de AutoPilot (ESP) para estos dispositivos. Si el ESP no está habilitado, la Directiva no se aplicará antes de que se inicie el cifrado.

A continuación se muestra un ejemplo de configuración de cifrado de Windows Microsoft Intune.

![Configuración de cifrado de BitLocker](images/bitlocker-encryption.png)

Los dispositivos que se cifren automáticamente deberán descifrarse antes de cambiar el algoritmo de cifrado.

La configuración está disponible en perfiles de **configuración de dispositivos**  >  **Profiles**  >  **crear perfil**  >  **plataforma** = Windows 10 y versiones posteriores, tipo de perfil = Endpoint Protection > **configurar**el  >  **cifrado de Windows**  >  **configuración base de BitLocker**, configurar métodos de cifrado = habilitar.

También se recomienda establecer la configuración de Windows de **cifrado de Windows**  >  **Windows Settings**  >  **cifrar** = requerir.

## <a name="requirements"></a>Requisitos

Windows 10, versión 1809 o posterior.

## <a name="next-steps"></a>Pasos siguientes

[Información general de BitLocker](/windows/security/information-protection/bitlocker/bitlocker-overview)