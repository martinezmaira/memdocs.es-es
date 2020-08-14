---
title: Portal de autoservicio de BitLocker
titleSuffix: Configuration Manager
description: Cómo usar el portal de autoservicio de usuario en Configuration Manager para la recuperación de BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ad1f79bb439e0a426229680960092a5f0d8fb3c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129246"
---
# <a name="bitlocker-self-service-portal"></a>Portal de autoservicio de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

Después de [instalar el portal de autoservicio de BitLocker](setup-websites.md), si BitLocker bloquea el dispositivo de un usuario, este puede obtener acceso de forma independiente a sus equipos. El portal de autoservicio no requiere asistencia alguna por parte del personal del departamento de soporte técnico.

[![Captura de pantalla del portal de autoservicio predeterminado de BitLocker](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> Para obtener una clave de recuperación del portal de autoservicio, el usuario debe haber iniciado sesión correctamente en el equipo al menos una vez. Este inicio de sesión debe ser local en el dispositivo, no en una sesión remota. De lo contrario, debe ponerse en contacto con el departamento de soporte técnico para recuperar las claves. Un administrador del departamento de soporte técnico puede usar el [sitio web de administración y supervisión](helpdesk-portal.md) para solicitar la clave de recuperación.

BitLocker puede bloquear el dispositivo en las siguientes situaciones:

- El usuario ha olvidado la contraseña o el PIN de BitLocker.

- Ha habido un cambio en los archivos del sistema operativo, en BIOS o en el Módulo de plataforma segura (TPM) del dispositivo.

Para solicitar la clave de recuperación de BitLocker desde el portal de autoservicio:

1. Cuando BitLocker bloquea un dispositivo, muestra la pantalla de recuperación de BitLocker durante el inicio. Anote el identificador de 32 dígitos de la clave de recuperación de BitLocker.

1. En otro equipo, vaya al portal de autoservicio en el explorador web, por ejemplo, `https://webserver.contoso.com/SelfService`.

1. Lea y acepte el aviso.

1. En el campo **Id. de la clave de recuperación**, escriba los primeros ocho dígitos del identificador de la clave de recuperación de BitLocker. Si coincide con varias claves, escriba los 32 dígitos.

1. Elija una de las siguientes opciones como **Motivo** de esta solicitud:

    - BIOS/TPM modificados
    - Archivos del sistema operativo modificados
    - PIN/frase de contraseña perdidos

1. Seleccione **Obtener clave**. En el portal de autoservicio se mostrará la **clave de recuperación de BitLocker** de 48 dígitos.

1. Escriba este código de 48 dígitos en la pantalla de recuperación de BitLocker del equipo.

> [!NOTE]
> Puede que se agote el tiempo de espera del portal de autoservicio de BitLocker después de un período de inactividad. Por ejemplo, después de cinco minutos, es posible que vea una advertencia de tiempo de espera con un contador de 60 segundos.
>
> ![Advertencia de tiempo de espera del portal de autoservicio de BitLocker](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Si no reacciona a la cuenta atrás, la sesión expirará.
>
> ![Página de sesión expirada en el portal de autoservicio de BitLocker](media/bitlocker-self-service-portal-session-expired.png)
