---
title: Configuración de detección de puntos de conexión y respuesta para la seguridad de puntos de conexión de Intune | Microsoft Docs
description: Configuración de la directiva de detección de puntos de conexión y respuesta para la seguridad de puntos de conexión en Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: e26719bb9bf322e3e4bf11b39911e98788707629
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460423"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Configuración de la directiva de detección de puntos de conexión y respuesta para la seguridad de puntos de conexión en Intune

Vea los parámetros que se pueden configurar en los perfiles de la [directiva de detección de puntos de conexión y respuesta](../protect/endpoint-security-edr-policy.md) en el nodo de seguridad de los puntos de conexión de Intune.

Plataformas y perfiles compatibles:

- **Windows 10 y versiones posteriores**: use esta plataforma para la directiva que implemente en dispositivos administrados con Intune.
  - Perfil: **Detección de puntos de conexión y respuesta (MDM)**

- **Windows 10 y Windows Server**: use esta plataforma para la directiva que implemente en dispositivos administrados mediante Configuration Manager.
  - Perfil: **Detección de puntos de conexión y respuesta (ConfigMgr)**

## <a name="endpoint-detection-and-response-mdm"></a>Detección de puntos de conexión y respuesta (MDM)

**Detección de puntos de conexión y respuesta**:

- **Tipo de paquete de configuración de cliente de ATP de Microsoft Defender**

  Cargue un paquete de configuración firmado que se usará para incorporar el cliente de ATP de Microsoft Defender.

  - **Sin configurar** (*valor predeterminado*).
  - **Blob de incorporación**  
  - **Blob de retirada**  

  Si se establece en *Blob de incorporación*, se pueden configurar las siguientes opciones:

  - **Blob de incorporación de Advanced Threat Protection**  
    Haga clic en **Select onboarding file** (Seleccionar archivo de incorporación) para abrir el panel *Select onboarding File* (Seleccionar archivo de incorporación), donde se especifica un archivo `.onboarding`.

  Si se establece en *Blob de retirada*, se pueden configurar las siguientes opciones:
  
  - **Blob de retirada de Advanced Threat Protection**  
     Haga clic en **Select offboarding file** (Seleccionar archivo de retirada) para abrir el panel *Select offboarding File* (Seleccionar archivo de retirada), donde se especifica un archivo `.offboarding`.

- **Uso compartido de muestras para todos los archivos**  

  Devuelve o establece el parámetro de configuración de uso compartido de muestras de Advanced Threat Protection de Microsoft Defender.  
  - **No configurado** (*valor predeterminado*)
  - **Sí**

- **Frecuencia de informes de telemetría urgentes**

  - **No configurado** (*valor predeterminado*)
  - **Sí**: aumente la frecuencia de informes de telemetría de Advanced Threat Protection de Microsoft Defender.

## <a name="endpoint-detection-and-response-configmgr"></a>Detección de puntos de conexión y respuesta (ConfigMgr)

**Detección de puntos de conexión y respuesta**:

- **Uso compartido de muestras para todos los archivos**  

  Devuelve o establece el parámetro de configuración de uso compartido de muestras de Advanced Threat Protection de Microsoft Defender.  
  - **No configurado** (*valor predeterminado*)
  - **Sí**

- **Frecuencia de informes de telemetría urgentes**

  - **No configurado** (*valor predeterminado*)
  - **Sí**: aumente la frecuencia de informes de telemetría de Advanced Threat Protection de Microsoft Defender.

## <a name="next-steps"></a>Pasos siguientes

[Directiva de seguridad de puntos de conexión para EDR](../protect/endpoint-security-edr-policy.md)
