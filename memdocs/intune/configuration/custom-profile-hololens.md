---
title: 'Uso del Control de aplicaciones de Windows Defender en dispositivos HoloLens 2 en Microsoft Intune: Azure | Microsoft Docs'
description: Configure el CSP Control de aplicaciones de Windows Defender (WDAC) para permitir o impedir que las aplicaciones se abran en dispositivos HoloLens 2 en Microsoft Intune. Use PowerShell y un perfil de configuración personalizado.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d2d19b03253725bde7b0ee27f3c94b42adb5917
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990133"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Uso de WDAC y Windows PowerShell para permitir o bloquear aplicaciones en dispositivos HoloLens 2 con Microsoft Intune

Los dispositivos Microsoft HoloLens 2 admiten el [CSP Control de aplicaciones de Windows Defender (WDAC)](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp), que reemplaza al [CSP de AppLocker](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).

Con Windows PowerShell y Microsoft Intune, puede usar el CSP WDAC para permitir o bloquear que se abran aplicaciones específicas en dispositivos Microsoft HoloLens 2. Por ejemplo, puede que quiera permitir o impedir que la aplicación Cortana se abra en los dispositivos HoloLens 2 de la organización.

Esta característica se aplica a:

- Dispositivos HoloLens 2 que ejecutan Windows Holographic for Business

El CSP WDAC se basa en la [característica Control de aplicaciones de Windows Defender (WDAC)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). También puede [usar varias directivas de WDAC](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

En este artículo se muestra cómo:

1. Usar Windows PowerShell para crear directivas de WDAC.
2. Usar Windows PowerShell para convertir las reglas de directiva de WDAC en XML, actualizar el XML y convertirlo en un archivo binario.
3. En Microsoft Intune, crear un [perfil de configuración de dispositivos personalizado](custom-settings-windows-holographic.md), agregar este archivo binario de directiva de WDAC y aplicar la directiva a los dispositivos HoloLens 2.

En Intune, debe crear un perfil de configuración personalizado para usar el CSP Control de aplicaciones de Windows Defender (WDAC). 

Siga los pasos de este artículo como una plantilla para permitir o denegar que determinadas aplicaciones se abran en dispositivos HoloLens 2.

## <a name="prerequisites"></a>Requisitos previos

- Estar familiarizado con Windows PowerShell.
- Iniciar sesión en Intune como miembro del:

  - Rol de Intune **Administrador de directivas y perfiles** o **Administrador de roles de Intune**

    O BIEN

  - Rol de Azure AD **Administrador global** o **Administrador de servicios de Intune**

  En [Control de acceso basado en rol (RBAC) con Intune](../fundamentals/role-based-access-control.md) encontrará más información.

- Cree un grupo de usuarios o de dispositivos con sus dispositivos HoloLens 2. Para obtener más información, vea [Grupos de usuarios frente a grupos de dispositivos](device-profile-assign.md#user-groups-vs-device-groups).

## <a name="example"></a>Ejemplo

En este ejemplo se usa Windows PowerShell para crear una directiva de Control de aplicaciones de Windows Defender (WDAC). La directiva impide que se abran determinadas aplicaciones. Después, use Intune para implementar la directiva en dispositivos HoloLens 2.

1. En el equipo de escritorio, abra la aplicación de **Windows PowerShell**.
2. Obtenga información sobre el paquete de aplicación instalado en el equipo de escritorio:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Por ejemplo, escriba:

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Después, confirme que el paquete tiene atributos de aplicación:

    ```powershell
    $package1
    ```

    Verá atributos similares a los siguientes detalles de aplicación:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Cree una directiva de WDAC y agregue el paquete de aplicación a la regla DENY:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Repita los pasos 2 y 3 para cualquier otra aplicación a la que quiera aplicar DENY:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Por ejemplo, escriba:

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Convierta la directiva de WDAC en **newPolicy.xml**:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Para establecer como destino todas las versiones de una aplicación, en newPolicy.xml, asegúrese de que `PackageVersion="65535.65535.65535.65535"` se encuentra en el nodo Deny:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    Para `PackageFamilyNameRules`, puede usar las versiones siguientes:

    - **Permitir**: escriba `PackageVersion, 0.0.0.0`, que significa "permitir esta versión y versiones superiores".
    - **Denegar**: escriba `PackageVersion, 65535.65535.65535.65535`, que significa "denegar esta versión y versiones anteriores".

6. Combine **newPolicy.xml** con la directiva predeterminada que se encuentra en el equipo de escritorio. En este paso se crea **mergedPolicy.xml**. Por ejemplo, permita que se ejecuten Windows, los controladores firmados por WHQL y las aplicaciones firmadas de Store:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Deshabilite la regla del **Modo de auditoría** en **mergedPolicy.xml**. Al realizar la combinación, el modo de auditoría se activa automáticamente:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Habilite la regla **InvalidateEAs en un reinicio** en **mergedPolicy.xml**:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Para obtener más información sobre estas reglas, vea [Comprender las reglas de directivas de WDAC y las reglas de archivos](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Convierta **mergedPolicy.xml** a formato binario. En este paso se crea **compiledPolicy.bin**. Agregará este archivo binario **compiledPolicy.bin** a Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Cree un perfil de configuración de dispositivo personalizado en Intune:

    1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), cree un perfil de configuración de dispositivos personalizado de Windows 10.

        Para conocer los pasos específicos, vea [Creación de un perfil personalizado mediante OMA-URI en Intune](custom-settings-configure.md).

    2. Cuando cree el perfil, especifique la configuración siguiente:

      - **OMA-URI**: escriba `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`. Reemplace `<PolicyGUID>` por el nodo PolicyTypeID en el archivo **mergedPolicy.xml** que creó en el paso 6.

        Siguiendo nuestro ejemplo, especifique `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076`.

        El GUID de la directiva **debe coincidir** con el nodo PolicyTypeID del archivo **mergedPolicy.xml** (creado en el paso 6).

      - **Tipo de datos**: establézcalo en **Base64 (archivo)** . Convierte automáticamente el archivo de bin a Base64.
      - **Archivo de certificado**: Cargue el archivo binario **compiledPolicy.bin** (creado en el paso 9).

      La configuración tiene un aspecto similar a la siguiente:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Agregue un OMA-URI personalizado para configurar el CSP ApplicationControl en Microsoft Intune.":::

11. Cuando el perfil esté [asignado](device-profile-assign.md) al grupo HoloLens 2, compruebe el estado del perfil. Una vez que el perfil se haya aplicado correctamente, reinicie los dispositivos HoloLens 2.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

[Más información sobre los perfiles personalizados de Intune](custom-settings-configure.md).
