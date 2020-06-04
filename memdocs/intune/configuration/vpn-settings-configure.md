---
title: 'Incorporación de una configuración de VPN a dispositivos iOS en Microsoft Intune: Azure | Microsoft Docs'
description: En el administrador de dispositivos Android, Android Enterprise, iOS, iPadOS, macOS y Windows, use la configuración integrada para crear conexiones de red privada virtual (VPN) en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c92220fabf8d1cb2a34ac702dd4157ef848762b
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990262"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Creación de perfiles de VPN para conectarse a servidores VPN en Intune

Las redes privadas virtuales (VPN) ofrecen a los usuarios acceso remoto seguro a la red de la empresa. Los dispositivos usan un perfil de conexión VPN para iniciar una conexión con el servidor VPN. Los **perfiles de VPN** en Microsoft Intune asignan la configuración de VPN en los usuarios y los dispositivos de la organización. Use esta configuración para que los usuarios puedan conectarse de forma fácil y segura a la red de la organización.

Por ejemplo, quiere configurar todos los dispositivos iOS/iPadOS con las opciones de configuración necesarias para conectarse a un recurso compartido de archivos de la red de la empresa. Cree un perfil de VPN que incluya estas opciones de configuración. Después, asigne este perfil a todos los usuarios que tengan dispositivos iOS/iPadOS. Los usuarios verán la conexión VPN en la lista de redes disponibles y podrán conectarse con un esfuerzo mínimo.

> [!NOTE]
> Puede usar [directivas de configuración personalizadas](custom-settings-configure.md) de Intune para crear perfiles de VPN para las siguientes plataformas:
>
> * Android 4 y versiones posteriores
> * Dispositivos inscritos que ejecutan Windows 8.1 y versiones posteriores
> * Windows Phone 8.1 y versiones posteriores
> * Dispositivos inscritos que ejecutan Windows 10 Escritorio
> * Windows 10 Mobile
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>Tipos de conexión VPN

Puede crear perfiles de VPN mediante los siguientes tipos de conexión:

- Automático
  - Windows 10

- Check Point Capsule VPN
  - Administrador de dispositivos Android
  - Perfiles de trabajo de Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Cisco AnyConnect
  - Administrador de dispositivos Android
  - Perfiles de trabajo de Android Enterprise
  - Propietario del dispositivo Android Enterprise (totalmente administrado)
  - iOS/iPadOS
  - macOS

- Cisco (IPsec)
  - iOS/iPadOS

- SSO de Citrix
  - Administrador de dispositivos Android
  - Perfiles de trabajo de Android Enterprise: uso de la [directiva de configuración de aplicaciones](../apps/app-configuration-policies-use-android.md)
  - Propietario del dispositivo Android Enterprise (totalmente administrado): uso de la [directiva de configuración de aplicaciones](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- VPN personalizada
  - iOS/iPadOS
  - macOS

  Cree perfiles de VPN personalizados usando la configuración de URI de [Crear un perfil con una configuración personalizada](custom-settings-configure.md).

- F5 Access
  - Administrador de dispositivos Android
  - Perfiles de trabajo de Android Enterprise
  - Propietario del dispositivo Android Enterprise (totalmente administrado)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Perfiles de trabajo de Android Enterprise: uso de la [directiva de configuración de aplicaciones](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Administrador de dispositivos Android
  - Perfiles de trabajo de Android Enterprise
  - Propietario del dispositivo Android Enterprise (totalmente administrado)
  - iOS/iPadOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- SonicWall Mobile Connect
  - Administrador de dispositivos Android
  - Perfiles de trabajo de Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Zscaler
  - Perfiles de trabajo de Android Enterprise: uso de la [directiva de configuración de aplicaciones](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS

> [!IMPORTANT]
> Para poder usar perfiles de VPN asignados a un dispositivo, debe instalar la aplicación VPN aplicable al perfil. Para ayudarle a asignar la aplicación con Intune, consulte [¿Qué es la administración de aplicaciones de Microsoft Intune?](../apps/app-management.md).  

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Plataforma**: seleccione la plataforma de los dispositivos. Las opciones son:
      - **Administrador de dispositivos Android**
      - **Android Enterprise** > **Solo el propietario del dispositivo**
      - **Android Enterprise** > **Solo perfil de trabajo**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 y versiones posteriores**
      - **Windows 8.1 y versiones posteriores**
      - **Windows Phone 8.1**
    - **Perfil**: seleccione **VPN**.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil sería **Perfil de VPN de toda la empresa**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.
7. En **Opciones de configuración**, las opciones que puede configurar serán diferentes, según la plataforma que haya elegido. Seleccione la plataforma en la configuración detallada:

    - [Administrador de dispositivos Android](vpn-settings-android.md)
    - [Android Enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (incluido Windows Holographic for Business)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. Seleccione **Siguiente**.
9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione el usuario o los grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

## <a name="secure-your-vpn-profiles"></a>Protección de los perfiles de VPN

Los perfiles de VPN pueden utilizar diferentes tipos de conexiones y protocolos de diferentes fabricantes. Estas conexiones suelen protegerse con los siguientes métodos.

### <a name="certificates"></a>Certificados

Al crear el perfil de VPN, elija un perfil de certificado SCEP o PKCS que haya creado previamente en Intune. Este perfil se conoce como “certificado de identidad”. Se usa para autenticar con un perfil de certificado de confianza (o un *certificado raíz*) que se crea para que el dispositivo del usuario pueda conectarse. El certificado de confianza se asigna al equipo que autentica la conexión VPN, por lo general, el servidor de VPN.

Si usa la autenticación basada en certificados para el perfil de VPN, implemente el perfil de VPN, el de certificado y el perfil raíz de confianza en los mismos grupos. Esta asignación garantiza que cada dispositivo pueda reconocer la legitimidad de la entidad de certificación.

Para más información sobre cómo crear y usar perfiles de certificado en Intune, consulte [How to configure certificates with Microsoft Intune](../protect/certificates-configure.md) (Configuración de certificados con Microsoft Intune).

> [!NOTE]
> No se admiten los certificados agregados con el tipo de perfil del **certificado PKCS importado** para la autenticación de VPN. Se admiten los certificados agregados mediante el tipo de perfil de los **certificados PKCS** para la autenticación de VPN.


### <a name="user-name-and-password"></a>Nombre de usuario y contraseña

El usuario se autentica en el servidor de VPN proporcionando el nombre de usuario y contraseña.

## <a name="next-steps"></a>Pasos siguientes

Se crea el perfil, pero todavía no hace nada. Después, [asigne el perfil](device-profile-assign.md) a algunos dispositivos y [supervise su estado](device-profile-monitor.md).

También puede crear y usar instancias de VPN por aplicación en dispositivos de [administrador de dispositivos Android/Android Enterprise](android-pulse-secure-per-app-vpn.md) y [iOS/iPadOS](vpn-setting-configure-per-app.md).
