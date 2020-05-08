---
title: Creación de un perfil de Wi-Fi para dispositivos en Microsoft Intune - Azure | Microsoft Docs
description: Consulte estos pasos para crear un perfil de configuración de dispositivos Wi-Fi en Microsoft Intune. Cree perfiles para el administrador de dispositivos Android, Android Enterprise, modo de pantalla completa de Android, iOS, iPadOS, macOS, Windows 10 y versiones posteriores, y Windows Holographic for Business. Use estos perfiles para crear una conexión Wi-Fi para usar certificados, elegir un tipo de EAP, seleccionar un método de autenticación, habilitar un proxy y mucho más.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1ff20db13a87faea41d262da5742a428ec4d28f
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587291"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Adición y uso de la configuración de Wi-Fi en los dispositivos en Microsoft Intune

Wi-Fi es una red inalámbrica que muchos dispositivos móviles utilizan para acceder a la red. Microsoft Intune incluye configuraciones Wi-Fi integradas que se pueden implementar en usuarios y dispositivos de su organización. Este grupo de configuración se conoce como un "perfil" y se puede asignar a distintos usuarios y grupos. Una vez asignado, los usuarios acceden a la red Wi-Fi de la organización sin tener que configurarla ellos mismos.

Por ejemplo, instale una nueva red Wi-Fi denominada Contoso Wi-Fi. Después, quiere configurar todos los dispositivos iOS/iPadOS para conectarse a esta red. Este es el proceso:

1. Cree un perfil de Wi-Fi que contenga la configuración para conectarse a la red inalámbrica Contoso Wi-Fi.
2. Asigne el perfil a un grupo que incluya todos los usuarios de los dispositivos iOS/iPadOS.
3. En sus dispositivos, los usuarios encuentran la nueva red Contoso Wi-Fi en la lista de redes inalámbricas. Pueden conectarse a ella fácilmente con el método de autenticación de su elección.

En este artículo se enumeran los pasos para crear un perfil Wi-Fi. También incluye vínculos que describen las distintas configuraciones para cada plataforma.

## <a name="supported-device-platforms"></a>Plataformas de dispositivos compatibles

Los perfiles de Wi-Fi admiten las siguientes plataformas de dispositivo:

- Android 4 y versiones posteriores
- Quiosco de Android y Android Enterprise
- iOS 8.0 y versiones posteriores
- IPadOS 13.0 y versiones más recientes
- macOS X 10.11 y versiones más recientes
- Windows 10 y versiones posteriores, Windows 10 Mobile y Windows Holographic for Business

> [!NOTE]
> Para dispositivos que ejecutan Windows 8.1, puede importar una configuración de Wi-Fi que se haya exportado anteriormente desde otro dispositivo.

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
      - **Windows 8.1 y versiones posteriores**

    - **Perfil**: Seleccione **Wi-Fi**.

      > [!TIP]
      >
      > - Para dispositivos **Android Enterprise** que se ejecutan como un dispositivo dedicado (quiosco), elija **Solo el propietario del dispositivo** > **Wi-Fi**.
      > - Para **Windows 8.1 y versiones posteriores**, puede elegir **Importación de Wi-Fi**. Esta opción le permite importar la configuración de Wi-Fi como archivo XML exportado previamente de otro dispositivo.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil sería **Perfil WiFi para toda la empresa**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.
7. En **Opciones de configuración**, las opciones que puede configurar serán diferentes, según la plataforma que haya elegido. Seleccione la plataforma en la configuración detallada:

    - [Administrador de dispositivos Android](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), incluidos los dispositivos dedicados
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 y versiones posteriores](wi-fi-settings-windows.md)
    - [Windows 8.1 y versiones posteriores](wi-fi-settings-import-windows-8-1.md), incluido Windows Holographic for Business

8. Seleccione **Siguiente**.
9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione el usuario o los grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

> [!TIP]
> Si usa la autenticación basada en certificados para el perfil de Wi-Fi, implemente el perfil de Wi-Fi, el de certificado y el perfil raíz de confianza en los mismos grupos para asegurarse de que cada dispositivo pueda reconocer la legitimidad de la entidad de certificación.  Para obtener más información, vea [Procedimiento para configurar certificados con Microsoft Intune](../protect/certificates-configure.md).


## <a name="next-steps"></a>Pasos siguientes

Se crea el perfil, pero no hacen nada. Después, [asigne este perfil](device-profile-assign.md) y [supervise su estado](device-profile-monitor.md).

[Problemas de perfiles Wi-Fi en Intune](troubleshoot-wi-fi-profiles.md).
