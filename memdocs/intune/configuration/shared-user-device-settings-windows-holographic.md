---
title: 'Configuración para dispositivos compartidos con Windows Holographic for Business: Microsoft Intune (Azure) | Microsoft Docs'
description: Agregue y use Windows Holographic for Business para configurar dispositivos compartidos o que varios usuarios empleen en Microsoft Intune. Consulte una lista de las opciones de configuración de administración de cuentas y qué hacen en los dispositivos, incluido Microsoft HoloLens.
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
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88b7f41b873697a7ec34bd1fc2f1098384ab1c18
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915728"
---
# <a name="windows-holographic-for-business-settings-to-manage-shared-devices-using-intune"></a>Opciones de configuración de Windows Holographic for Business para administrar dispositivos compartidos con Intune

Es posible que varios usuarios empleen dispositivos con Windows Holographic, como Microsoft HoloLens. Los dispositivos con varios usuarios se denominan dispositivos compartidos y son parte de las soluciones de la administración de dispositivos móviles (MDM).

Con Microsoft Intune, los usuarios pueden iniciar sesión en estos dispositivos compartidos con una cuenta de invitado. Al usar el dispositivo, solamente tendrán acceso a las características que permita.

En este artículo se describen las opciones de configuración que usa en un perfil de configuración de dispositivos con Windows Holographic for Business. Tras crear el perfil en Intune, implementará o asignará el perfil en los grupos de dispositivos de su organización. También puede asignar este perfil a un grupo de dispositivos con distintos tipos de dispositivo y versiones del SO.

Para obtener más información sobre esta característica de Intune, vea [Control access, accounts, and power features on shared PC or multi-user devices](shared-user-device-settings.md) (Control del acceso, las cuentas y las características de energía en dispositivos con varios usuarios o equipos compartidos). Para obtener más información sobre el CSP de Windows, vea [AccountManagement CSP](/windows/client-management/mdm/accountmanagement-csp) (CSP de AccountManagement).

## <a name="before-your-begin"></a>Antes de empezar

[Cree un perfil de configuración de dispositivo multiusuario compartido de Windows 10](shared-user-device-settings.md).

Al crear un perfil de configuración de dispositivo de usuario compartido de Windows 10, hay más opciones de configuración de las que se enumeran en este artículo. La configuración de este artículo es compatible con dispositivos Windows Holographic for Business.

## <a name="shared-multi-user-device-settings"></a>Configuración de dispositivos compartidos con varios usuarios

> [!NOTE]
> Los dispositivos que ejecutan Windows Holographic for Business, incluido Microsoft HoloLens, solo admiten las opciones de configuración de **Administración de cuentas**. El hecho de configurar cualquier otra de las opciones de Intune, incluida **Modo de PC compartido**, no tendrá ningún efecto sobre estos dispositivos.

- **Administración de cuentas**: elija si las cuentas se eliminan automáticamente. Las opciones son:
  - **Sin configurar** (valor predeterminado): elimina automáticamente las cuentas locales que crean los invitados, así como las de AD y Azure AD. Cuando un usuario cierre sesión en el dispositivo, o cuando se ejecute el mantenimiento del sistema, estas cuentas se eliminarán.

    Indique también:

    - **Eliminación de cuenta**: elija cuándo se eliminarán las cuentas:
      - **Umbral de espacio de almacenamiento**
      - **Umbral de espacio de almacenamiento y umbral de inactividad**
      - **Inmediatamente después de cerrar sesión**

    Indique también:

    - **Iniciar umbral de eliminación (%)** : indique un porcentaje (de 0 a 100) de espacio en disco. Cuando el espacio de almacenamiento o en disco sea inferior al valor indicado, las cuentas en caché se eliminarán. Se eliminan las cuentas continuamente para recuperar espacio en disco. Las cuentas que lleven más tiempo inactivas serán las primeras en eliminarse.
    - **Detener umbral de eliminación (%)** : indique un porcentaje (de 0 a 100) de espacio en disco. Cuando el espacio de almacenamiento o en disco alcance el valor indicado, la eliminación se detendrá.

  - **Deshabilitar**: las cuentas locales, de AD y de Azure AD que crean los invitados permanecen en el dispositivo y no se eliminan.

## <a name="next-steps"></a>Pasos siguientes

- [Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).
- Vea la configuración del dispositivo de usuario compartido para [Windows 10 y versiones más recientes](shared-user-device-settings-windows.md).