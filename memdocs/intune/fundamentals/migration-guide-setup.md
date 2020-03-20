---
title: Configuración básica de Microsoft Intune
description: En este artículo se indican los pasos necesarios para configurar Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60cfa440-0723-4ea0-bacf-3c5d26f9a1d3
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b7784d4ad86e3418259f85ca1c4577d2289dc86
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79358161"
---
# <a name="basic-setup"></a>Configuración básica

Después de evaluar el entorno, ha llegado la hora de configurar Microsoft Intune.

## <a name="external-dependencies-for-an-intune-deployment"></a>Dependencias externas para una implementación de Intune

### <a name="identity"></a>Identidad

Intune exige Azure Active Directory (AAD) como proveedor de agrupaciones de identidades y de usuarios. Más información acerca de:

- [¿Requisitos de identidad?](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview#design-considerations-overview)

- [Requisitos de sincronización de directorios](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements)

- [Multi-Factor Authentication (MFA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks)

- [Planeación de grupos de usuarios y dispositivos](users-add.md)

- [Creación de grupos de usuarios y dispositivos](groups-get-started.md)

Si su organización ya usa Office 365, Intune debe usar el mismo entorno de Azure Active Directory.

### <a name="pki-optional"></a>PKI (opcional)

Si piensa usar autenticación basada en certificados para perfiles de VPN, Wi-Fi o correo electrónico con Intune, tendrá que asegurarse de que tiene una [infraestructura PKI](../protect/certificates-configure.md) compatible y lista para crear e implementar perfiles de certificado. Obtenga más información sobre la configuración de certificados en Intune:

- [Cómo configurar la infraestructura de certificados para SCEP](/intune/certificates-scep-configure).

- [Cómo configurar la infraestructura de certificados para PFX](/intune/certficates-pfx-configure).

## <a name="task-list-for-an-intune-setup"></a>Lista de tareas para una configuración de Intune

### <a name="task-1-intune-subscription"></a>Tarea 1: Suscripción a Intune

Para poder migrar a Intune, necesita primero una [suscripción a Intune](account-sign-up.md).

### <a name="task-2-assign-intune-user-licenses"></a>Tarea 2: Asignación de licencias de usuario de Intune

- Aprenda a [asignar licencias de usuario de Intune](licenses-assign.md).

- Si ha creado un inquilino de Azure Active Directory, aprenda a [crear otros usuarios o a sincronizar un usuario desde su Active Directory (AD) local.](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)

### <a name="task-3-set-your-mdm-authority-to-intune"></a>Tarea 3: Establecer Intune como entidad de MDM

Se recomienda que administre Intune mediante el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Establezca **Intune** como entidad de MDM. El uso de otra entidad de MDM permite a Intune transferir la administración de MDM a consolas de administración de Microsoft alternativas. Estos casos no son frecuentes.

> [!IMPORTANT]
> Si va a transferir la administración de dispositivos móviles a Intune por primera vez, debe establecer Intune como entidad de MDM.

Aprenda a [establecer la entidad de administración de dispositivos móviles](mdm-authority-set.md).

## <a name="next-step"></a>Paso siguiente

Configure las [directivas de administración de dispositivos y aplicaciones](migration-guide-configure-policies.md).
