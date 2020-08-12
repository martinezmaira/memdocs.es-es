---
title: Reiniciar dispositivos con Microsoft Intune - Azure | Microsoft Docs
description: Reinicie dispositivos Windows y iOS/iPadOS con Microsoft Intune en Azure Portal con la acción de reinicio remoto.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d68f09c6163ff613e5e4387a0e2d09a5eeea56c4
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051696"
---
# <a name="remotely-restart-devices-with-intune"></a>Reinicio remoto de los dispositivos con Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

La acción de dispositivo **Reiniciar** permite que se reinicie el dispositivo elegido (dentro de 5 minutos). Como al propietario del dispositivo no se le notifica automáticamente del reinicio, podría perder trabajo.

## <a name="supported-platforms"></a>Plataformas admitidas

- Windows: compatible con Windows 8.1 y versiones posteriores
- Dispositivos dedicados de Android Enterprise: compatibles con Android 7.0 y versiones posteriores
- Dispositivos Android Enterprise totalmente administrados: compatibles con Android 6.0 y versiones posteriores
- Dispositivos corporativos de Android Enterprise con un perfil de trabajo: compatibles con Android 8.0 y versiones posteriores
- iOS/iPados: compatible

    > [!Note]  
    > Para usar este comando es necesario que el dispositivo esté supervisado y disponer del derecho de acceso **Bloqueo del dispositivo**. El dispositivo se reinicia inmediatamente. Los dispositivos iOS/iPadOS bloqueados con un código de acceso no se vuelven a unir a una red Wi-Fi después del reinicio. Después del reinicio, el dispositivo podría no comunicarse con el servidor.
- macOS: no compatible
- Dispositivos Android y del perfil de trabajo Android: no compatibles

## <a name="restart-a-device"></a>Reiniciar un dispositivo

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Seleccione **Dispositivos** > **Todos los dispositivos**.
4. En la lista de dispositivos que administra, seleccione un dispositivo > **Reiniciar** > **Sí**.

## <a name="next-steps"></a>Pasos siguientes

- Para ver el estado de la acción de dispositivo **Reiniciar**, seleccione **Dispositivos** > **Acciones de dispositivo**.
