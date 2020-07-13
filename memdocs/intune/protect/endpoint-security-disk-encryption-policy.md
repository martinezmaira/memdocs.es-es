---
title: Administración de las opciones de firewall con directivas de seguridad de los puntos de conexión en Microsoft Intune | Microsoft Docs
description: Configure e implemente directivas para los dispositivos administrados con la directiva de firewall de seguridad de los puntos de conexión en Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 3e01e54eb6e74c8139c266d677a6406554119273
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972084"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Directiva de antivirus para la seguridad de los puntos de conexión en Intune

Los perfiles de cifrado de disco de seguridad de los puntos de conexión se centran únicamente en las opciones que son relevantes para un método de cifrado integrado de dispositivos, como FileVault o BitLocker. Este método permite a los administradores de seguridad administrar fácilmente las opciones de cifrado de disco sin tener que desplazarse por numerosas opciones que no tienen nada que ver.

Aunque se puede establecer la misma configuración de dispositivos mediante perfiles de *Endpoint Protection* para la configuración de dispositivos, los perfiles de configuración de dispositivos incluyen más categorías de configuración. Esta configuración no guarda relación con el cifrado de discos y podría entorpecer la tarea de establecer únicamente el cifrado de discos en el entorno.

Encontrará las directivas de seguridad de los puntos de conexión para el cifrado de discos en *Administrar*, en el nodo **Seguridad de los puntos de conexión** del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

## <a name="prerequisites-for-disk-encryption-policy"></a>Requisitos previos de la directiva de cifrado de disco

- **macOS**: macOS 10.13 o versiones posteriores
- **Windows**: requiere Windows 10 o posterior

## <a name="disk-encryption-profiles"></a>Perfiles de cifrado de disco

**Perfiles de macOS**:

- **FileVault**: FileVault proporciona cifrado de disco completo integrado para dispositivos macOS.

  Administración de [Configuración de FileVault](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) para macOS.

  Para crear un perfil de FileVault, consulte el artículo sobre el [uso del cifrado de discos FileVault para macOS](../protect/encrypt-devices-filevault.md).

**Perfiles de Windows 10**:

- **BitLocker**: Cifrado de unidad BitLocker es una característica de protección de datos que se integra con el sistema operativo y resuelve las amenazas de robo o exposición de datos de los equipos perdidos, robados o retirados de forma inapropiada.

  Administración de [Configuración de BitLocker](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) para Windows 10.

  Para crear un perfil de BitLocker, consulte el artículo sobre el [uso del cifrado de discos de BitLocker para Windows 10](../protect/encrypt-devices.md).

## <a name="manage-device-encryption"></a>Administración del cifrado de dispositivos

Después de implementar la directiva para cifrar un disco de dispositivo, consulte los artículos siguientes para obtener información sobre cómo administrar el cifrado:

- [Administración de BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [Administración de FileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Supervisión del cifrado de dispositivos](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Pasos siguientes

- [Para crear un perfil de FileVault](../protect/encrypt-devices-filevault.md#create-endpoint-security-policy-for-filevault)
- [Para crear un perfil de BitLocker](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
