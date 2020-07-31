---
title: 'Perfil de VPN personalizado por aplicación para el administrador de dispositivos Android en Microsoft Intune: Azure | Microsoft Docs'
description: Use un perfil personalizado para perfiles de VPN por aplicación en el administrador de dispositivos Android con los tipos de conexión Pulse Secure o Citrix VPN en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c8e09b6010f7fc846fd81281053eaaa722e5ef4
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262802"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Use un perfil personalizado de Microsoft Intune para crear un perfil de VPN por aplicación para dispositivos Android

Puede crear un perfil de VPN por aplicación para dispositivos Android 5.0 y versiones posteriores administrados con Intune. Primero, cree un perfil de VPN que use el tipo de conexión Pulse Secure o Citrix. Después, cree una directiva de configuración personalizada que asocie el perfil de VPN con las aplicaciones específicas.

Esta característica se aplica a:

- Administrador de dispositivos Android

Para usar una VPN por aplicación en dispositivos Android Enterprise, use una [directiva de configuración de aplicaciones](../apps/app-configuration-vpn-ae.md). Las directivas de configuración de aplicaciones admiten más aplicaciones cliente VPN. En dispositivos Android Enterprise, puede seguir los pasos de este artículo. Sin embargo, no se recomienda, y solo está limitado a las conexiones VPN de Pulse Secure y Citrix.

Después de asignar la directiva al dispositivo Android o a los grupos de usuarios, los usuarios deben iniciar el cliente de la VPN Pulse Secure o Citrix. El cliente de VPN permite entonces el tráfico solo desde las aplicaciones especificadas para usar la conexión VPN abierta.

> [!NOTE]
>
> Para el administrador de dispositivos Android, solo se admite el tipo de conexión Pulse Secure y Citrix. En dispositivos Android Enterprise, use una [directiva de configuración de aplicaciones](../apps/app-configuration-vpn-ae.md).

## <a name="step-1-create-a-vpn-profile"></a>Paso 1: Crear un perfil de VPN

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Plataforma**: Seleccione **Administrador de dispositivos Android**.
    - **Perfil**: seleccione **VPN**.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil es **Perfil de VPN por aplicación del administrador de dispositivos Android en toda la empresa**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.
7. En **Opciones de configuración**, configure las opciones que quiera en el perfil:

    - [Configuración de VPN para dispositivos del administrador de dispositivos Android](vpn-settings-android.md).

    Anote el valor de **Nombre de la conexión** que especificó al crear el perfil de VPN. Este nombre será necesario en el paso siguiente. En este ejemplo, el nombre de la conexión es **MyAppVpnProfile**.

8. Seleccione **Siguiente** y continúe creando el perfil. Para más información, consulte [Crear perfiles de VPN](vpn-settings-configure.md#create-the-profile).

## <a name="step-2-create-a-custom-configuration-policy"></a>Paso 2: Crear una directiva de configuración personalizada

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para el perfil personalizado. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil es **Perfil de VPN de Android de OMA-URI personalizado en toda la compañía**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.
    - **Plataforma**: Seleccione **Administrador de dispositivos Android**.
    - **Tipo de perfil**: seleccione **Personalizado**.

4. Elija **Configuración** > **Configurar**.
5. En el panel **Configuración OMA-URI personalizada**, elija **Agregar**.
    - **Nombre**: escriba un nombre para la configuración.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.
    - **OMA-URI**: escriba `./Vendor/MSFT/VPN/Profile/*Name*/PackageList`, donde *Nombre* es el nombre de la conexión que anotó en el paso 1. En este ejemplo, la cadena es `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`.
    - **Tipo de datos**: escriba **Cadena**.
    - **Valor**: escriba una lista separada por punto y coma de los paquetes que se van a asociar con el perfil. Por ejemplo, si quiere que Excel y el explorador Google Chrome usen la conexión VPN, escriba `com.microsoft.office.excel;com.android.chrome`.

    :::image type="content" source="./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png" alt-text="Directiva personalizada de VPN por aplicación del administrador de dispositivos Android en Microsoft Intune":::

### <a name="set-your-blocked-and-allowed-app-list-optional"></a>Configuración de la lista de aplicaciones bloqueadas y permitidas (opcional)

Use el valor **BLACKLIST** para escribir una lista de aplicaciones que *no puedan* usar la conexión VPN. Todas las demás aplicaciones se conectan a través de la VPN. También, use el valor **WHITELIST** para especificar una lista de aplicaciones que *puedan* usar la conexión VPN. Las aplicaciones que no están en la lista no se conectan a través de la VPN.

1. En el panel **Configuración OMA-URI personalizada**, elija **Agregar**.
2. Proporcione un nombre de configuración.
3. En **OMA-URI**, escriba `./Vendor/MSFT/VPN/Profile/*Name*/Mode`, donde *Name* es el nombre del perfil de VPN que anotó en el paso 1. En nuestro ejemplo, la cadena es `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`.
4. En **Tipo de datos**, escriba **Cadena**.
5. En **Valor**, escriba **BLACKLIST** o **WHITELIST**.

## <a name="step-3-assign-both-policies"></a>Paso 3: Asignar ambas directivas

[Asigne ambos perfiles de dispositivo](device-profile-assign.md) a los usuarios o dispositivos necesarios.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener una lista de todos los valores de configuración de VPN del administrador de dispositivos Android, consulte [Configuración de dispositivos Android para configurar VPN](vpn-settings-android.md).
- Para más información sobre la configuración de VPN e Intune, consulte [Configuración de VPN en Microsoft Intune](vpn-settings-configure.md).
