---
title: 'Uso de una configuración de dispositivo personalizada en Microsoft Intune: Azure | Microsoft Docs'
description: Agregue o cree un perfil para usar la configuración personalizada en dispositivos con Windows Phone, Windows 8.1, Windows 10 y versiones posteriores, el administrador de dispositivos Android, Android Enterprise, y macOS e iOS/iPadOS mediante Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084000"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Crear un perfil con una configuración personalizada en Intune

Microsoft Intune incluye muchas configuraciones integradas para controlar diversas características de un dispositivo. También puede crear perfiles personalizados, que se crean de forma similar a los perfiles integrados. para usar las configuraciones de dispositivo y las características que no están integradas en Intune. Estos perfiles incluyen características y configuraciones para controlar dispositivos de la organización. Por ejemplo, puede crear un perfil personalizado que establece la misma función para todos los dispositivos iOS/iPadOS.

La configuración personalizada se puede realizar de forma diferente en cada plataforma. Por ejemplo, para controlar características en dispositivos Android y Windows, puede especificar valores de identificador uniforme de recursos de Open Mobile Alliance (OMA-URI). Para dispositivos Apple, puede importar un archivo creado con [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) o [Apple Profile Manager](https://support.apple.com/profile-manager).

Para obtener más información sobre los perfiles de configuración, vea [¿Qué son los perfiles de dispositivo de Microsoft Intune?](device-profiles.md)

En este artículo se muestra cómo crear un perfil personalizado para el administrador de dispositivos Android, Android Enterprise, iOS/iPadOS, macOS y Windows. También puede ver todas las opciones de configuración disponibles para las distintas plataformas.

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para la directiva. Asígnele un nombre a las directivas para que pueda identificarlas de manera sencilla más adelante. Por ejemplo, un nombre de directiva válido es **Windows 10: Perfil personalizado que habilita OMA-URI personalizado de AllowVPNOverCellular**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.
    - **Plataforma**: seleccione la plataforma de los dispositivos. Las opciones son:

      - **Administrador de dispositivos Android**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 y versiones posteriores**
      - **Windows 8.1 y versiones posteriores**

    - **Tipo de perfil**: seleccione **Personalizado**.

4. La configuración es diferente para cada plataforma. Para ver la configuración de una plataforma concreta, elija la plataforma:

    - [Administrador de dispositivos Android](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. Cuando termine, seleccione **Crear perfil** > **Crear**.

El perfil se crea y se muestra en la lista de perfiles (**Configuración del dispositivo** > **Perfiles**).

## <a name="next-steps"></a>Pasos siguientes

Una vez creado el perfil, está listo para asignarlo. Después, [asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).
