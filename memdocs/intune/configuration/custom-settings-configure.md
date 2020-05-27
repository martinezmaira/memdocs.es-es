---
title: 'Uso de una configuración de dispositivo personalizada en Microsoft Intune: Azure | Microsoft Docs'
description: Agregue o cree un perfil para usar la configuración personalizada en dispositivos con Windows Phone, Windows 8.1, Windows 10 y versiones posteriores, el administrador de dispositivos Android, Android Enterprise, y macOS e iOS/iPadOS mediante Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ddbb82d3cd5c86ff32917013edd4f16b303678fe
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990102"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Crear un perfil con una configuración personalizada en Intune

Microsoft Intune incluye muchas configuraciones integradas para controlar diversas características de un dispositivo. También puede crear perfiles personalizados, que se crean de forma similar a los perfiles integrados. para usar las configuraciones de dispositivo y las características que no están integradas en Intune. Estos perfiles incluyen características y configuraciones para controlar dispositivos de la organización. Por ejemplo, puede crear un perfil personalizado que establece la misma función para todos los dispositivos iOS/iPadOS.

La configuración personalizada se puede realizar de forma diferente en cada plataforma. Por ejemplo, para controlar características en dispositivos Android y Windows, puede especificar valores de identificador uniforme de recursos de Open Mobile Alliance (OMA-URI). Para dispositivos Apple, puede importar un archivo creado con [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) o [Apple Profile Manager](https://support.apple.com/profile-manager).

Para obtener más información sobre los perfiles de configuración, vea [¿Qué son los perfiles de dispositivo de Microsoft Intune?](device-profiles.md)

En este artículo se muestra cómo crear un perfil personalizado para el administrador de dispositivos Android, Android Enterprise, iOS/iPadOS, macOS y Windows. También puede ver todas las opciones de configuración disponibles para las distintas plataformas.

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Plataforma**: seleccione la plataforma de los dispositivos. Las opciones son:  

        - **Administrador de dispositivos Android**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 y versiones posteriores**
        - **Windows Phone 8.1**

    - **Perfil**: seleccione **Personalizado**.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para la directiva. Asígnele un nombre a las directivas para que pueda identificarlas de manera sencilla más adelante. Por ejemplo, un nombre de directiva válido es **Windows 10: Perfil personalizado que habilita OMA-URI personalizado de AllowVPNOverCellular**.
    - **Descripción**: escriba una descripción para la directiva. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.

7. En **Opciones de configuración**, las opciones que puede configurar serán diferentes, según la plataforma que haya elegido. Elija la plataforma para la configuración detallada:

    - [Administrador de dispositivos Android](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. Seleccione **Siguiente**.
9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione los usuarios o grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente, la configuración **Connectivity/AllowVPNOverCellular** está habilitada. Este valor permite que un dispositivo Windows 10 abra una conexión VPN cuando se encuentre en una red de telefonía móvil.

> [!div class="mx-imgBorder"]
> ![Ejemplo de una directiva personalizada que contiene opciones de VPN en Intune y el Administrador de puntos de conexión](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Pasos siguientes

El perfil se crea, pero puede que todavía no haga nada. Después, [asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).
