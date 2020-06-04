---
title: Administración de las opciones de protección de cuentas expuestas a ataques con directivas de seguridad de los puntos de conexión en Microsoft Intune | Microsoft Docs
description: Configure e implemente directivas para los dispositivos administrados con opciones de directiva de protección de cuentas de seguridad de los puntos de conexión en Microsoft Endpoint Manager.
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
ms.openlocfilehash: 6fb5702b7c809c7810004a53d084f19fa94dea9e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431857"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Directiva de protección de cuentas de seguridad de los puntos de conexión en Intune

Use las directivas de seguridad de los puntos de conexión de Intune para la protección de cuentas a fin de proteger la identidad y las cuentas de los usuarios. La directiva de protección de cuentas se centra en las opciones de Windows Hello y Credential Guard, que forma parte de la administración de identidades y del acceso de Windows.

- *Windows Hello para empresas* reemplaza las contraseñas con una autenticación de dos factores sólida en equipos y dispositivos móviles.
- *Credential Guard* ayuda a proteger las credenciales y los secretos que se usan con los dispositivos.

Para obtener más información, consulte [Administración de identidad y acceso](https://docs.microsoft.com/windows/security/identity-protection/) en la documentación de administración de identidades y acceso de Windows.

Encontrará las directivas de seguridad de los puntos de conexión correspondientes a la protección de cuentas en *Administrar*, en el nodo **Seguridad de los puntos de conexión** del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Consulte [Configuración del perfil de protección de cuentas](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-account-protection-profiles"></a>Requisitos previos para perfiles de protección de cuentas

- Windows 10 o posterior

## <a name="account-protection-profiles"></a>Perfiles de protección de cuentas

*Los perfiles de protección de cuentas se encuentran en versión preliminar*.

**Perfiles de Windows 10**:

- **Protección de cuentas** *(versión preliminar)* : la configuración de las directivas de protección de cuentas le ayuda a proteger las credenciales de usuario.

## <a name="next-steps"></a>Pasos siguientes

[Configuración de directivas de seguridad de puntos de conexión](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
