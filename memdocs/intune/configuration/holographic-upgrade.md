---
title: Actualizar a Windows Holographic for Business
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo actualizar dispositivos que ejecuten Windows Holographic a Windows Holographic for Business
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e809a888fc2696e54540ee6baa2271d7340579
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361060"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Actualización de dispositivos que ejecutan Windows Holographic a Windows Holographic for Business

En Microsoft Intune se incluyen varias opciones de configuración para ayudarle a administrar y proteger sus dispositivos. En este artículo se describen las opciones de configuración para actualizar los dispositivos Windows Holographic a Windows Holographic for Business. Dichas opciones de configuración se crean en un perfil de configuración de actualización de Intune y se insertan o implementan en los dispositivos.

Como parte de su solución de administración de dispositivos móviles (MDM), use estas configuraciones para actualizar sus dispositivos Windows Holographic. Para Microsoft HoloLens, puede adquirir Commercial Suite para obtener la licencia necesaria para la actualización. Para obtener más información, consulte [Desbloquear las funcionalidades de Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Para más información sobre esta característica, consulte [Uso de un perfil de configuración para actualizar Windows 10 o cambiar del modo S en Intune](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de dispositivo](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Actualización de la edición

- **Edición a la que actualizar**: seleccione **Windows 10 Holographic for Business**.
- **Archivo de licencia**: busque y seleccione el archivo de licencia XML que se le proporcionó.

  ![Escriba el nombre de archivo XML que incluye Holographic para la información de licencia empresarial](./media/holographic-upgrade/Holographic-edition-upgrade.png)
 
## <a name="next-steps"></a>Pasos siguientes

El perfil se crea, pero puede que todavía no haga nada. Asegúrese de [asignar el perfil](device-profile-assign.md) y [supervise su estado](device-profile-monitor.md).

También puede crear perfiles de actualización de edición para dispositivos [Windows 10 y posteriores](edition-upgrade-windows-settings.md).
