---
title: 'Actualización a Windows Holographic for Business en Microsoft Intune: Azure | Microsoft Docs'
description: Actualice a Windows 10 Holographic for Business mediante un perfil de configuración de dispositivo en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d561d2682cf90d5d7075640c260d8f21c8b891b1
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556122"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Actualización de dispositivos que ejecutan Windows Holographic a Windows Holographic for Business

En Microsoft Intune se incluyen varias opciones de configuración para ayudarle a administrar y proteger sus dispositivos. En este artículo se describen las opciones de configuración para actualizar los dispositivos Windows Holographic a Windows Holographic for Business.

Como parte de su solución de administración de dispositivos móviles (MDM), use estas configuraciones para actualizar sus dispositivos Windows Holographic. Para Microsoft HoloLens, puede adquirir Commercial Suite para obtener la licencia necesaria para la actualización. Para obtener más información, consulte [Desbloquear las funcionalidades de Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Como administrador de Intune, puede crear y asignar estas opciones de configuración a los dispositivos.

Para más información sobre esta característica, consulte [Uso de un perfil de configuración para actualizar Windows 10 o cambiar del modo S en Intune](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Antes de comenzar

[Cree una actualización de edición de Windows 10 y el perfil de configuración de dispositivo de cambio de modo](edition-upgrade-configure-windows-10.md#create-the-profile).

Al crear una actualización de edición de Windows 10 y el perfil de configuración de dispositivo de cambio de modo, hay más opciones de configuración de las que se enumeran en este artículo. La configuración de este artículo es compatible con dispositivos Windows Holographic for Business.

## <a name="edition-upgrade"></a>Actualización de la edición

- **Edición a la que actualizar**: seleccione **Windows 10 Holographic for Business**.
- **Archivo de licencia**: busque y seleccione el archivo de licencia XML que se le proporcionó.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="En Intune, escriba el nombre del archivo XML que incluye la información de la licencia de Holographic for Business.":::

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede crear perfiles de actualización de edición para dispositivos [Windows 10 y posteriores](edition-upgrade-windows-settings.md).
