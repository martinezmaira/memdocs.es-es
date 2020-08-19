---
title: Configuración de correo electrónico de Microsoft Intune para Windows Phone 8.1
titleSuffix: ''
description: Conozca la configuración de Intune que puede usar para configurar las conexiones de correo electrónico en dispositivos que ejecutan Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5bd00f12ab0f015c6408e2bbc934e1320c7540e
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146155"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>Configuración de perfiles de correo electrónico en Microsoft Intune para dispositivos que ejecutan Windows Phone 8.1

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

En este artículo, se muestran las opciones de configuración de perfiles de correo electrónico que puede configurar para los dispositivos que ejecutan Windows Phone 8.1.

>[!IMPORTANT]
>Los perfiles de correo electrónico de Windows Phone 8.1 también se aplican a los dispositivos Windows 10.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de correo electrónico de Windows Phone 8.1](email-settings-configure.md).

## <a name="email-settings"></a>Configuración de correo electrónico

- **Servidor de correo electrónico**: escriba el nombre de host del servidor de Exchange. Por ejemplo, escriba `outlook.office365.com`.
- **Nombre de la cuenta**: indique el nombre para mostrar en la cuenta de correo electrónico. Este nombre se muestra en los dispositivos de los usuarios.
- **Atributo de nombre de usuario de AAD**: este nombre es el atributo que Intune obtiene de Azure Active Directory (AAD). Intune genera dinámicamente el nombre de usuario que usa este perfil. Las opciones son:
  - **Nombre principal de usuario**: obtiene el nombre, como `user1` o `user1@contoso.com`.
  - **Dirección SMTP principal**: obtiene el nombre en formato de dirección de correo electrónico, como `user1@contoso.com`.
  - **Nombre de cuenta sAM**: requiere el dominio, como `domain\user1`. Indique también:
    - **Origen de nombre de dominio del usuario**: Las opciones son:
      - **AAD** (Azure Active Directory): escriba **Atributo de nombre de dominio del usuario de ADD**. elija si quiere obtener el atributo **Nombre de dominio completo** o **Nombre de NetBIOS** del usuario.
      - **Personalizado**: escriba **Nombre de dominio personalizado que se usará**. escriba un valor que Intune use como nombre de dominio, como `contoso.com` o `contoso`.

- **Atributo de dirección de correo electrónico de AAD**: Intune obtiene este atributo de Azure Active Directory (AAD). elija el modo en que se genera la dirección de correo electrónico para el usuario. Las opciones son:
  - **Nombre principal de usuario**: usa el nombre principal completo como dirección de correo electrónico, por ejemplo, `user1@contoso.com` o `user1`.
  - **Dirección SMTP principal**: usa la dirección SMTP principal para iniciar sesión en Exchange, por ejemplo, `user1@contoso.com`.

## <a name="security-settings"></a>Configuración de seguridad

- **SSL**: **Habilitar** usa la comunicación de Capa de sockets seguros (SSL) al enviar y recibir correos electrónicos y al comunicarse con el servidor de Exchange. **Deshabilitar** no requiere SSL.

## <a name="synchronization-settings"></a>Configuración de sincronización

- **Cantidad de correo electrónico para sincronizar**: elija el número de días de correo electrónico que quiere sincronizar. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Seleccione **Ilimitado** para sincronizar todo el correo electrónico disponible.
- **Programación de sincronización**: seleccione una programación para que los dispositivos sincronicen datos de Exchange Server. También puede seleccionar **Conforme llegan los mensajes**, que sincroniza los datos tan pronto como llegan. O bien, seleccione **Manual** para que el usuario del dispositivo inicie la sincronización.

## <a name="content-sync-settings"></a>Configuración de la sincronización de contenido

- **Tipo de contenido para sincronizar**: Seleccione los tipos de contenido que quiere sincronizar con los dispositivos:
  - **Contactos**: **Activado** sincroniza los contactos. **Desactivado** no sincroniza automáticamente los contactos. Los usuarios sincronizan manualmente.
  - **Calendario**: **Activado** sincroniza el calendario. **Desactivado** no sincroniza automáticamente el calendario. Los usuarios sincronizan manualmente.
  - **Tareas**: **Activado** sincroniza las tareas. **Desactivado** no sincroniza automáticamente las tareas. Los usuarios sincronizan manualmente.

## <a name="next-steps"></a>Pasos siguientes

También puede configurar las opciones de correo electrónico en [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md) y [Windows 10](email-settings-windows-10.md).

[Configuración de las opciones de correo electrónico en Intune](email-settings-configure.md)
