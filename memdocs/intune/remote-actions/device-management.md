---
title: 'Administrar dispositivos con Microsoft Intune: Azure | Microsoft Docs'
description: Revise los dispositivos que administra con Microsoft Intune, incluida la exportación de una lista de dispositivos a formato csv, vea los dispositivos unidos a Azure Active Directory, revise un registro de cambio de acciones en el dispositivo, use TeamViewer Connector para permitir que los administradores de TI solucionen problemas de dispositivos Android de forma remota y vea todas las acciones que se pueden ejecutar en los dispositivos.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/14/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d2412418-d91a-4767-a3d6-bc88bb29caa2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4acb2317ea2147f25ef5b19c7d92ae795df36629
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338115"
---
# <a name="what-is-microsoft-intune-device-management"></a>¿Qué es la administración de dispositivos de Microsoft Intune?

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Como administrador de TI, debe asegurarse de que los dispositivos administrados proporcionan los recursos que necesitan los usuarios para hacer su trabajo y proteger esos datos de posibles riesgos.

La carga de trabajo **Dispositivos** ofrece información detallada sobre los dispositivos que administra y permite realizar tareas remotas en esos dispositivos.

## <a name="get-to-your-devices"></a>Ir a los dispositivos

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Seleccione **Dispositivos**. Esta vista muestra información detallada sobre los dispositivos individuales y lo que se puede hacer con ellos, lo que incluye:

   - **Información general** muestra una instantánea visual de los dispositivos inscritos, cuántos dispositivos usan las diferentes plataformas, etc.
   - **Todos los dispositivos** muestra una lista de los dispositivos inscritos que administra.

     Use la característica **Exportar** para crear una lista .zip de todos los dispositivos, en incrementos de 10 000 (Internet Explorer) o 30 000 (Microsoft Edge y Chrome).

     Seleccione un dispositivo para [ver detalles adicionales](device-inventory.md), como información sobre hardware, las aplicaciones instaladas y las directivas, entre otros.

   - **Dispositivos de Azure AD** muestra una lista de los dispositivos registrados o unidos a Azure Active Directory (Azure AD). Obtenga más información sobre la [administración de dispositivos de Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction).
   - **Acciones de dispositivo** incluye un historial de las acciones remotas realizadas en distintos dispositivos, en el que se incluye la acción, su estado, quién la inició y la hora.

     ![Captura de pantalla de supervisión de acciones de dispositivo](./media/device-management/monitor-device-actions.png)

   - **Registros de auditoría** es un registro de las actividades que generan un cambio en Intune. [Registros de auditoría](../fundamentals/monitor-audit-logs.md) proporciona más detalles.
   - **TeamViewer Connector** es un servicio que permite que los usuarios de dispositivos Android administrados por Intune obtengan asistencia remota de su administrador de TI. Obtenga más información sobre [TeamViewer](teamviewer-support.md).
   - **Ayuda y soporte técnico** proporciona un acceso directo para obtener sugerencias de solución de problemas, solicitar soporte técnico o comprobar el estado de Intune.

## <a name="available-device-actions"></a>Acciones de dispositivo disponibles
Las acciones disponibles dependen de la plataforma y la configuración del dispositivo.

- [Visualización del inventario de dispositivos](device-inventory.md)
- Ejecute las acciones de dispositivo remoto:
  - [Restablecimiento de Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
  - [Rotación de claves de BitLocker](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) (solo Windows)
  - [Eliminar](devices-wipe.md#delete-devices-from-the-intune-portal)
  - [Deshabilitar Bloqueo de activación](device-activation-lock-disable.md) (solo para iOS)
  - [Comienzo de cero](device-fresh-start.md) (solo para Windows)
  - [Examen completo](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (solo Windows 10)
  - [Buscar dispositivo](device-locate.md) (solo para iOS)
  - [Modo perdido](device-lost-mode.md) (solo para iOS)
  - [Examen rápido](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (solo Windows 10)
  - [Control remoto en Android](teamviewer-support.md)
  - [Bloqueo remoto](device-remote-lock.md)
  - [Cambio de nombre de un dispositivo](device-rename.md)
  - [Restablecer el código de acceso](device-passcode-reset.md)
  - [Reiniciar](device-restart.md) (solo para Windows)
  - [Retirar](devices-wipe.md#retire)
  - [Actualizar la inteligencia de seguridad de Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus)
  - [Restablecimiento del PIN de Windows 10](device-windows-pin-reset.md)
  - [Borrar](devices-wipe.md#wipe)
  - [Envío de notificaciones personalizadas](custom-notifications.md#send-a-custom-notification-to-a-single-device) (Android y iOS/iPadOS)
  - [Sincronización del dispositivo](device-sync.md)
- [Acciones masivas de dispositivo](bulk-device-actions.md)

## <a name="next-steps"></a>Pasos siguientes

- En **Todos los dispositivos**, seleccione un dispositivo para ver más detalles sobre ese dispositivo concreto.
- Elija **Acciones de dispositivo** para ver el estado de las acciones realizadas en los dispositivos que administra.
