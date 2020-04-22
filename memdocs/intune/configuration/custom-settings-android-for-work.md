---
title: 'Agregar una configuración personalizada para dispositivos Android Enterprise en Microsoft Intune: Azure | Microsoft Docs'
description: Agregar o crear un perfil personalizado para dispositivos Android Enterprise en Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4724d6e5-05e5-496c-9af3-b74f083141f8
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 827b5eb8b65aa59212b9ef990def3c5f191baf7c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "79334436"
---
# <a name="use-custom-settings-for-android-enterprise-devices-in-microsoft-intune"></a>Uso de una configuración personalizada para dispositivos Android Enterprise en Microsoft Intune

Con Microsoft Intune, puede agregar o crear una configuración personalizada para los dispositivos de perfil de trabajo de Android Enterprise mediante un "perfil personalizado". Los perfiles personalizados son una característica de Intune diseñada para agregar una configuración de dispositivo y características que no están integradas Intune.

Los perfiles personalizados de Android Enterprise usan la configuración OMA-URI (identificador uniforme de recursos de Open Mobile Alliance) para controlar las características en dispositivos Android. Esta configuración la suelen usar los fabricantes de dispositivos móviles para controlar estas características.

Intune admite el siguiente número limitado de perfiles personalizados de Android Enterprise:

- ./Vendor/MSFT/WiFi/Profile/SSID/Settings: Algunos ejemplos de [creación de un perfil de Wi-Fi con una clave precompartida](wi-fi-profile-shared-key.md).
- ./Vendor/MSFT/VPN/Profile/Name/PackageList: Algunos ejemplos de [creación de un perfil de VPN por aplicación](android-pulse-secure-per-app-vpn.md).
- ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste: Vea los [ejemplos](#example) de este artículo. Esta configuración también está disponible en la interfaz de usuario. Para más información, consulte [Configuración de dispositivos Android Enterprise para permitir o restringir características](device-restrictions-android-for-work.md).

Si necesita configuración adicional, vea [OEMConfig para Android Enterprise](android-oem-configuration-overview.md).

En este artículo se muestra cómo crear un perfil personalizado para dispositivos Android Enterprise. También se proporciona un ejemplo de un perfil personalizado que bloquea las acciones de copiar y pegar.

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba los valores siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil es **perfil personalizado de Android Enterprise**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.
    - **Plataforma**: seleccione **Android Enterprise**.
    - **Tipo de perfil**: seleccione **Personalizado**.

4. En **Configuración OMA-URI personalizada**, seleccione **Agregar**. Escriba los valores siguientes:

    - **Nombre**: escriba un nombre único para la configuración OMA-URI, de modo que pueda encontrarla fácilmente.
    - **Descripción**: escriba una descripción con información general sobre la configuración y otros detalles importantes.
    - **OMA-URI**: escriba la configuración OMA-URI que quiere usar.
    - **Tipo de datos**: seleccione el tipo de datos que se va a usar para esta configuración OMA-URI. Las opciones son:

      - String
      - Cadena (archivo XML)
      - Fecha y hora
      - Integer
      - Punto flotante
      - Boolean
      - Base64 (archivo)

    - **Valor**: escriba el valor de datos que quiere asociar con la configuración OMA-URI especificada. El valor depende del tipo de datos que ha seleccionado. Por ejemplo, si selecciona **Fecha y hora**, seleccione el valor en un selector de fecha.

    Después de agregar algunos valores de configuración, puede seleccionar **Exportar**. Haga clic en **Exportar** para crear una lista de todos los valores agregados en un archivo de valores separados por comas (.csv).

5. Haga clic en **Aceptar** para guardar los cambios. Continúe agregando más valores según sea necesario.
6. Cuando termine, seleccione **Aceptar** > **Crear** para crear el perfil de Intune. Una vez hecho, el perfil aparece en la lista **Dispositivos - Perfiles de configuración**.

## <a name="example"></a>Ejemplo

En este ejemplo, creará un perfil personalizado que restringe las acciones de copiar y pegar entre aplicaciones profesionales y aplicaciones personales en dispositivos Android Enterprise.

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba los valores siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, escriba **bloque ent de android copiar pegar perfil personalizado**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.
    - **Plataforma**: seleccione **Android Enterprise**.
    - **Tipo de perfil**: seleccione **Personalizado**.

4. En **Configuración OMA-URI personalizada**, seleccione **Agregar**. Escriba los valores siguientes:

    - **Nombre**: escriba algo parecido a `Block copy and paste`.
    - **Descripción**: escriba algo parecido a `Blocks copy/paste between work and personal apps`.
    - **OMA-URI**: escriba `./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste`.
    - **Tipo de datos**: seleccione **Booleano** para que el valor de esta configuración OMA-URI sea **True** o **False**.
    - **Valor**: seleccione **True**.

5. Después de especificar la configuración, el entorno debería tener un aspecto similar a la imagen siguiente:

    ![Bloquee las acciones de copiar y pegar para un perfil de trabajo Android.](./media/custom-settings-android-for-work/custom-policy-afw-copy-paste.png)

Cuando asigna este perfil a los dispositivos Android Enterprise que administra, las acciones de copiar y pegar estarán bloqueadas entre las aplicaciones de los perfiles profesional y personal.

## <a name="next-steps"></a>Pasos siguientes

Se crea el perfil, pero todavía no hace nada. Después, [asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

Cree un [perfil personalizado en dispositivos Android](custom-settings-android.md).
