---
title: Bloquear dispositivos con Microsoft Intune - Azure | Microsoft Docs
description: Use la acción de bloqueo remoto de Microsoft Intune para bloquear un dispositivo protegido por un PIN o contraseña.
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
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 220a2ac92d46c1279d4498c8673e2ceef28c470f
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462055"
---
# <a name="remotely-lock-devices-with-intune"></a>Bloqueo remoto de dispositivos con Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

La acción de dispositivo **Bloqueo remoto** bloquea el dispositivo. Para desbloquear el dispositivo, el propietario debe introducir su código de acceso. Puede bloquear de forma remota los dispositivos que dispongan de PIN o contraseña. Los dispositivos que no tienen PIN o contraseña no se pueden bloquear de forma remota.

## <a name="supported-platforms"></a>Plataformas compatibles

**Bloqueo remoto** es compatible con las siguientes plataformas:

- Android
- Dispositivos de quiosco de Android Enterprise
- Dispositivos de perfil de trabajo Android Enterprise
- Dispositivos totalmente administrados de Android Enterprise
- Dispositivos Android Enterprise de propiedad corporativa con perfil de trabajo
- iOS
- macOS
- Windows 10 Mobile
- Windows Phone 8.1 y versiones posteriores

**Bloqueo remoto** no es compatible con:
- Windows 10 Escritorio

> [!NOTE]
> Para los dispositivos MacOS, establezca un PIN de recuperación de 6 dígitos. Una vez bloqueado el dispositivo, en **Información general del dispositivo** se muestra el PIN hasta que se envía otra acción de dispositivo. Asegúrese de anotar el PIN, ya que solo estará disponible durante 30 días después de enviar el comando de bloqueo remoto. Una vez transcurridos los 30 días, Intune ya no dispondrá del PIN. Además, verá un estado de error en los informes si inicia este comando de nuevo para el mismo dispositivo mientras el PIN original no se ha usado para desbloquear correctamente el dispositivo. Solo debe enviar este comando una vez, anotar el PIN y, hasta que lo use para entrar en el dispositivo macOS correctamente, no intentar enviar este comando al mismo dispositivo.


## <a name="remote-lock-a-device"></a>Bloquear de forma remota un dispositivo

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Seleccione **Dispositivos** > **Todos los dispositivos**.
4. En la lista de dispositivos, seleccione un dispositivo y, luego, seleccione la acción **Bloqueo remoto**.

## <a name="next-steps"></a>Pasos siguientes

- Para ver el estado de esta acción, seleccione **Microsoft Intune** > **Dispositivos** > **Acciones de dispositivo**. 
- Consulte [Acciones disponibles](device-management.md) para ver más acciones para administrar los dispositivos.
