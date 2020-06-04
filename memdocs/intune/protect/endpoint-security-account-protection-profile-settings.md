---
title: Configuración de la directiva de protección de cuentas para la seguridad de los puntos de conexión de Intune | Microsoft Docs
description: Configuración de la directiva de protección de cuentas para la seguridad de los puntos de conexión en Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83432000"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Configuración de la directiva de protección de cuentas para la seguridad de los puntos de conexión en Intune

Vea los parámetros que se pueden configurar en los perfiles de la directiva de *protección de cuentas*, en el nodo seguridad de los puntos de conexión de Intune, como parte de una [directiva de seguridad para los puntos de conexión](../protect/endpoint-security-policy.md).

Perfiles y plataformas compatibles:

- **Windows 10 y versiones posteriores**:
  - Perfil: **Protección de cuentas** *(versión preliminar)*


## <a name="account-protection-profile"></a>Perfil de protección de cuentas

### <a name="account-protection"></a>Protección de cuentas

- **Bloquear Windows Hello para empresas**

  Windows Hello para empresas es un método alternativo para iniciar sesión en dispositivos Windows mediante la sustitución de contraseñas, tarjetas inteligentes y tarjetas inteligentes virtuales.
  - **No configurado** (*valor predeterminado*): los dispositivos aprovisionan Windows Hello para empresas.
  - **Deshabilitado**: los dispositivos aprovisionan Windows Hello para empresas.
  - **Habilitado**: los dispositivos no aprovisionan Windows Hello para empresas para ningún usuario.
  
- **Habilitar para usar claves de seguridad en el inicio de sesión**

  Habilite la clave de seguridad de Windows Hello como credencial de inicio de sesión para todos los equipos del inquilino.
  - **Sin configurar** (*valor predeterminado*).
  - **Sí**

- **Activar Credential Guard**  
  [CSP: []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard usa el hipervisor de Windows para proporcionar protecciones. Credential Guard requiere compatibilidad de hardware para el Arranque seguro y las protecciones DMA. Esta configuración solo se realiza correctamente en los dispositivos que cumplen los requisitos de hardware.
  - **No configurado** (*valor predeterminado*): deshabilite el uso de Credential Guard, que es el valor predeterminado de Windows.
  - **Habilitar con bloqueo UEFI**: habilite Credential Guard y no permita que se deshabilite de forma remota, ya que la configuración persistente de UEFI debe borrarse manualmente.
  - **Habilitar sin bloqueo UEFI**: habilitar Credential Guard y permitir que se apague sin acceso físico a la máquina.

## <a name="next-steps"></a>Pasos siguientes

[Directiva de seguridad para los puntos de conexión para la protección de cuentas](../protect/endpoint-security-account-protection-policy.md)
