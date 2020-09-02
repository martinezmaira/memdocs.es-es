---
title: Capacidades de Intune por método de inscripción para dispositivos Windows
titleSuffix: Microsoft Intune
description: Capacidades por método de inscripción para dispositivos Windows
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/21/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 701794ba476f87aaf079e39c834f3e8e3f2c280d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913892"
---
# <a name="intune-enrollment-method-capabilities-for-windows-devices"></a>Capacidades de Intune por método de inscripción para dispositivos Windows
[!INCLUDE[azure_portal](../includes/azure_portal.md)]

Hay varios métodos para inscribir los dispositivos de los recursos en Intune. Cada método tiene diferentes procedimientos recomendados y funciones, como se muestra en estas tablas.

## <a name="best-practices-by-enrollment-method"></a>Procedimientos recomendados por método de inscripción
| **Best practices** (Procedimientos recomendados) | **[Unido a Azure AD](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Unido a Azure AD con AutoPilot (modo controlado por el usuario)](../../autopilot/enrollment-autopilot.md)** |**[Unido a Azure AD con AutoPilot (modo de implementación automática)](../../autopilot/enrollment-autopilot.md)** |**[Masivo](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Administración conjunta](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Uso frecuente en EDU|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Se pueden usar dispositivos como dispositivos compartidos|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Los dispositivos personales deben acceder a los recursos de la empresa|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Mantenimiento automático de aplicaciones|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>Capacidades por método de inscripción

| **Capacidades** | **[Unido a Azure AD](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Unido a Azure AD con AutoPilot (modo controlado por el usuario)](../../autopilot/enrollment-autopilot.md)** |**[Unido a Azure AD con AutoPilot (modo de implementación automática)](../../autopilot/enrollment-autopilot.md)** |**[Masivo](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Administración conjunta](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Conditional Access                                      |![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)\*\*|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|
|El usuario se asocia con el dispositivo                    |![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|
|Necesita Azure AD Premium                               |![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|
|El dispositivo puede evaluar recursos protegidos por la entidad de certificación             |![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|
|Los usuarios no deben ser administradores en sus dispositivos               |![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Capacidad de configurar la experiencia de instalación de dispositivos        |![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Capacidad de inscribir dispositivos sin interacción del usuario      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|
|Capacidad de ejecutar scripts de PowerShell                       |![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/checkmark.png)\*| 
|Admite la inscripción automática después de unirse a un dominio de AD      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|
|Admite la inscripción automática después de unirse a Hybrid Azure AD|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|
|Admite la inscripción automática después de unirse a Azure AD       |![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![Marca de verificación](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|

\* Las cargas de trabajo de aplicaciones cliente en Configuration Manager deben moverse a Intune piloto o a Intune.

\** [Los dispositivos están bloqueados para el acceso condicional con la excepción de Windows 10 1803+.](device-enrollment-manager-enroll.md)

## <a name="next-steps"></a>Pasos siguientes

[Configuración de la inscripción para Windows](windows-enroll.md)