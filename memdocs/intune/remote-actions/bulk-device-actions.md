---
title: Use acciones masivas del dispositivo en uno con Microsoft Intune.
titleSuffix: ''
description: Use acciones masivas remota del dispositivo.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c1b9a695830380c00900d0fe94ec075b21def0a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989350"
---
# <a name="use-bulk-device-actions"></a>Uso de acciones masivas del dispositivo

Puede usar acciones masivas del dispositivo para las siguientes acciones remotas:
- [Restablecimiento de Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Notificaciones personalizadas](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Eliminar](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Cambiar nombre](device-rename.md)
- [Reiniciar](device-restart.md)
- [Sincronizar](device-sync.md)
- [Eliminación de datos](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Uso de una acción masiva del dispositivo

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Elija **Dispositivos** > **Todos los dispositivos** > **Acciones masivas del dispositivo**.
![Acciones masivas de dispositivo](./media/bulk-device-actions/bulk-device-actions.png)
3. En la página **Acción masiva del dispositivo**, seleccione un **SO** y **Acción del dispositivo**. Algunas acciones de dispositivo tienen opciones adicionales o campos para rellenar. Seleccione **Siguiente**.
4. En la página **Dispositivos**, seleccione entre 1 y 100 dispositivos y, luego, **Siguiente**.
5. En la página **Revisar y crear**, seleccione **Crear**.

## <a name="next-steps"></a>Pasos siguientes
[Información general sobre la administración de dispositivos.](device-management.md)
