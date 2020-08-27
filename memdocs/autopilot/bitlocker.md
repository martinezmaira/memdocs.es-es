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
ms.openlocfilehash: 8ea2e0de96887e8f7d97633a041721462b81d6c8
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908303"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>Establecer el algoritmo de cifrado de BitLocker para dispositivos AutoPilot

**Se aplica a**

-   Windows 10

Con Windows AutoPilot, puede configurar las opciones de cifrado de BitLocker que se aplicarán antes de que se inicie el cifrado automático. Esto garantiza que el algoritmo de cifrado predeterminado no se aplica automáticamente cuando no es el valor deseado. También se pueden entregar otras directivas de BitLocker que se deben aplicar antes del cifrado antes de que se inicie el cifrado de BitLocker automático. 

El algoritmo de cifrado de BitLocker se usa cuando BitLocker se habilita por primera vez y establece la seguridad en la que debe producirse el cifrado de volumen completo. Los algoritmos de cifrado disponibles son: AES-CBC 128-bit, AES-CBC 256-bit, XTS-AES 128 bits o cifrado XTS-AES 256-bit. El valor predeterminado es XTS-AES 128-bit Encryption. Consulte [CSP de BitLocker](/windows/client-management/mdm/bitlocker-csp) para obtener información sobre los algoritmos de cifrado recomendados que se deben usar.

Para asegurarse de que se establece el algoritmo de cifrado de BitLocker deseado antes de que se produzca el cifrado automático en los dispositivos AutoPilot:

1. Configure los [valores del método de cifrado](/intune/endpoint-protection-windows-10#windows-encryption) en el perfil de Endpoint Protection de Windows 10 para el algoritmo de cifrado deseado. 
2. [Asigne la Directiva](/intune/device-profile-assign) a su grupo de dispositivos AutoPilot. 
    - **Importante**: la Directiva de cifrado debe estar asignada a los **dispositivos** del grupo, no a los usuarios.
3. Habilite la página de [Estado de inscripción](enrollment-status.md) de AutoPilot (ESP) para estos dispositivos. 
    - **Importante**: si ESP no está habilitado, la Directiva no se aplicará antes de que se inicie el cifrado.

A continuación se muestra un ejemplo de configuración de cifrado de Windows Microsoft Intune.

   ![Configuración de cifrado de BitLocker](images/bitlocker-encryption.png)

**Nota**: un dispositivo que se cifre automáticamente deberá descifrarse antes de cambiar el algoritmo de cifrado.

La configuración está disponible en configuración de dispositivos-> perfiles-> crear perfil-> Platform = Windows 10 y versiones posteriores, tipo de perfil = Endpoint Protection-> configurar-> cifrado de Windows-> configuración de base de BitLocker, configurar métodos de cifrado = habilitar.

**Nota**: también se recomienda establecer el cifrado de windows-> configuración de windows-> cifrar = **requerir**.

## <a name="requirements"></a>Requisitos

Windows 10, versión 1809 o posterior.

## <a name="see-also"></a>Consulte también

[Información general de BitLocker](/windows/security/information-protection/bitlocker/bitlocker-overview)