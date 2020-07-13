---
title: Administradores sin licencia en Microsoft Intune
description: Obtenga información sobre cómo conceder a los administradores sin licencia permiso para acceder a Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6dcd41377234bbb1b40e513f16c3393d763b17f
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088197"
---
# <a name="unlicensed-admins"></a>Administradores sin licencia

Puede conceder acceso al centro de administración de Microsoft Endpoint Manager/Intune a los administradores sin licencias de Intune.

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Administración de inquilinos** > **Roles** > **Licencias de administrador**.
2. Seleccione **Permitir el acceso a administradores sin licencia** > **Sí**.
    >[!WARNING]
    >No se puede deshacer esta configuración después de hacer clic en **Sí**.

3. A partir de ahora, los usuarios que inicien sesión en el centro de administración de Microsoft Endpoint Manager no necesitarán una licencia de Intune. Su ámbito de acceso se definirá mediante los roles que tengan asignados.

Intune admite hasta 350 administradores sin licencia por grupo de seguridad y solo se aplica a los miembros directos. Los administradores que superen este límite experimentarán un comportamiento imprevisible.




