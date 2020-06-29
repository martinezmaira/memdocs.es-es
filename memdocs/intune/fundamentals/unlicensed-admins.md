---
title: Suscribirse o iniciar sesión en Microsoft Intune
description: Procedimiento de registro para obtener una suscripción de Microsoft Intune o de inicio de sesión para comenzar una suscripción.
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
ms.openlocfilehash: ae30e03a03b4d690bdaa9e6a4c73da6ab15226f7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095816"
---
# <a name="unlicensed-admins"></a>Administradores sin licencia

Puede conceder acceso al centro de administración de Microsoft Endpoint Manager/Intune a los administradores sin licencias de Intune.

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Administración de inquilinos** > **Licencias de administrador**.
2. Seleccione **Permitir el acceso a administradores sin licencia** > **Sí**.
    >[!WARNING]
    >No se puede deshacer esta configuración después de hacer clic en **Sí**.

3. A partir de ahora, los usuarios que inicien sesión en el centro de administración de Microsoft Endpoint Manager no necesitarán una licencia de Intune. Su ámbito de acceso se definirá mediante los roles que tengan asignados.

Intune admite hasta 350 administradores sin licencia por grupo de seguridad. Los administradores que superen este límite experimentarán un comportamiento imprevisible.




