---
title: Configuración de correo electrónico para dispositivos Windows 10 en Microsoft Intune - Azure | Microsoft Docs
description: Cree un perfil de correo electrónico de configuración de dispositivos que use servidores de Exchange y recupere los atributos de Azure Active Directory. También puede habilitar SSL y sincronizar el correo electrónico y los programas en dispositivos Windows 10 con Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa861a266f89b82fdd2d6e73d30fdc2e58da33b4
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086902"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>Configuración de perfiles de correo electrónico para dispositivos que ejecutan Windows 10 en Microsoft Intune.

Use la configuración del perfil de correo electrónico para configurar la aplicación Correo en los dispositivos que ejecutan Windows 10 y versiones posteriores.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree el perfil](email-settings-configure.md).

## <a name="email-settings"></a>Configuración de correo electrónico

- **Servidor de correo electrónico**: escriba el nombre de host del servidor de Exchange. Por ejemplo, escriba `outlook.office365.com`.
- **Nombre de la cuenta**: indique el nombre para mostrar en la cuenta de correo electrónico. Este nombre se muestra en los dispositivos de los usuarios.
- **Atributo de nombre de usuario de AAD**: este nombre es el atributo que Intune obtiene de Azure Active Directory (AAD). Intune genera dinámicamente el nombre de usuario que usa este perfil. Las opciones son:
  - **Nombre principal de usuario**: obtiene el nombre, como `user1` o `user1@contoso.com`.
  - **Dirección SMTP principal**: obtiene el nombre en formato de dirección de correo electrónico, como `user1@contoso.com`.
  - **Nombre de cuenta sAM**: requiere el dominio, como `domain\user1`. Indique también:  
    - **Origen de nombre de dominio del usuario**: elija **AAD** (Azure Active Directory) o **Personalizar**.

      Si quiere obtener los atributos de **AAD**, escriba:
      - **Atributo de nombre de dominio del usuario de ADD**: elija si quiere obtener el atributo **Nombre de dominio completo** o el **Nombre NetBIOS** del usuario.

      Si quiere usar los atributos **Personalizados**, escriba:
      - **Nombre de dominio personalizado que se usará**: escriba un valor que Intune use como nombre de dominio, como `contoso.com` o `contoso`.

- **Atributo de dirección de correo electrónico de AAD**: Intune obtiene este atributo de Azure Active Directory (AAD). elija el modo en que se genera la dirección de correo electrónico para el usuario. Las opciones son:
  - **Nombre principal de usuario**: usa el nombre principal completo como dirección de correo electrónico, por ejemplo, `user1@contoso.com` o `user1`.
  - **Dirección SMTP principal**: usa la dirección SMTP principal para iniciar sesión en Exchange, por ejemplo, `user1@contoso.com`.

### <a name="security"></a>Seguridad

- **SSL**: **Habilitar** usa la comunicación de Capa de sockets seguros (SSL) al enviar y recibir correos electrónicos y al comunicarse con el servidor de Exchange. **Deshabilitar** no requiere SSL.

### <a name="synchronization"></a>Sincronización

- **Cantidad de correo electrónico para sincronizar**: elija el número de días de correo electrónico que quiere sincronizar. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Seleccione **Ilimitado** para sincronizar todo el correo electrónico disponible.
- **Programación de sincronización**: seleccione una programación para que los dispositivos sincronicen datos de Exchange Server. También puede seleccionar **Conforme llegan los mensajes**, que sincroniza los datos tan pronto como llegan. O bien, seleccione **Manual** para que el usuario del dispositivo inicie la sincronización.

### <a name="content-sync"></a>Sincronización de contenido

- **Tipo de contenido para sincronizar**: Seleccione los tipos de contenido que quiere sincronizar con los dispositivos:
  - **Contactos**: **Activado** sincroniza los contactos. **Desactivado** no sincroniza automáticamente los contactos. Los usuarios sincronizan manualmente.
  - **Calendario**: **Activado** sincroniza el calendario. **Desactivado** no sincroniza automáticamente el calendario. Los usuarios sincronizan manualmente.
  - **Tareas**: **Activado** sincroniza las tareas. **Desactivado** no sincroniza automáticamente las tareas. Los usuarios sincronizan manualmente.

## <a name="next-steps"></a>Pasos siguientes

También puede configurar las opciones de correo electrónico en [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md) y [iOS/iPadOS](email-settings-ios.md). 

[Configuración de las opciones de correo electrónico en Intune](email-settings-configure.md)
