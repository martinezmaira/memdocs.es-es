---
title: 'Actualización de Windows 10 y configuración del modo S en Microsoft Intune: Azure | Microsoft Docs'
description: Vea una lista de todas las configuraciones y lo que hacen al actualizar una edición de Windows 10 en un dispositivo o habilite el modo de S en un dispositivo con un perfil de configuración de dispositivo en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d050139ae017f5800670518a41d75fba469ceac
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146480"
---
# <a name="windows-10-and-newer-device-settings-to-upgrade-editions-or-enable-s-mode-in-intune"></a>Configuración de dispositivos Windows 10 (y versiones posteriores) para actualizar ediciones o habilitar el modo S en Intune

En Microsoft Intune se incluyen varias opciones de configuración para ayudarle a administrar y proteger sus dispositivos. En este artículo se enumeran y describen las opciones de configuración para actualizar ediciones o habilitar el modo S en dispositivos Windows 10. Dichas opciones de configuración se crean en un perfil de configuración de actualización de Intune y se insertan o implementan en los dispositivos.

Como parte de su solución de administración de dispositivos móviles (MDM), use estas opciones de configuración para controlar las opciones de edición y del modo S para los dispositivos Windows 10.

Para más información sobre esta característica, consulte [Uso de un perfil de configuración para actualizar Windows 10 o cambiar del modo S en Intune](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Antes de comenzar

[Cree el perfil](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Actualización de la edición

- **Edición a la que actualizar**: seleccione la edición de Windows 10 a la que va a actualizar. Los dispositivos de destino de esta directiva se actualizan a la edición que elija.
- **Clave de producto**: escriba la clave de producto que recibió de Microsoft. Después de crear la directiva con la clave de producto, la clave no se puede actualizar y se oculta por motivos de seguridad. Para cambiar la clave de producto, escriba toda la clave de nuevo.
- **Archivo de licencia**: en **Windows 10 Holographic for Business**, elija **Examinar** para seleccionar el archivo de licencia que recibió de Microsoft. Este archivo de licencia incluye información de licencia de las ediciones a las que está actualizando los dispositivos.

## <a name="mode-switch"></a>Modificador de modo

- **Desactivación del modo S**: desactiva el modo S en el dispositivo. Las opciones son:

  - **Sin configuración**: Intune no cambia ni actualiza esta configuración. De forma predeterminada, el dispositivo en modo S podría permanecer en modo S. Un usuario final puede desactivar el modo S en el dispositivo.
  - **Mantener en modo S**: Impide que el usuario final pueda desactivar el modo S en el dispositivo.
  - **Cambiar**: Permite a los usuarios desactivar el modo S en el dispositivo.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede crear perfiles de actualización de edición para dispositivos [Windows Holographic for Business](holographic-upgrade.md).
