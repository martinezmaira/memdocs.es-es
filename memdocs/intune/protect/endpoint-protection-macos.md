---
title: Configuración de Endpoint Protection en dispositivos macOS con Microsoft Intune | Microsoft Docs
description: Utilice Intune para configurar el uso del firewall integrado en dispositivos macOS para permitir o bloquear aplicaciones específicas, o bien use el modo sigiloso, para utilizar Gatekeeper a fin de determinar dónde se instalan las aplicaciones y para usar el cifrado de disco FileVault.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107499"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Configuración de Endpoint Protection de macOS en Intune

En este artículo se muestran las opciones de Endpoint Protection que se pueden configurar para los dispositivos con macOS. Estas opciones se configuran mediante un perfil de configuración de dispositivo macOS para [Endpoint Protection](endpoint-protection-configure.md) en Intune.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de Endpoint Protection de macOS](endpoint-protection-configure.md).

## <a name="firewall"></a>Firewall

Use el firewall para controlar conexiones por aplicación en lugar de por puerto. La configuración por aplicación permite aprovechar las ventajas de la protección del firewall con más facilidad. También ayuda a evitar que aplicaciones no deseadas tomen el control de los puertos de red que están abiertos para las aplicaciones legítimas.

- **Habilitar firewall**

  Active el uso del firewall en macOS y después configure cómo se administran las conexiones entrantes en el entorno.

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**

- **Bloquear todas las conexiones entrantes**

  Bloquee todas las conexiones entrantes excepto las necesarias para los servicios básicos de Internet, como DHCP, Bonjour e IPSec. Esta característica también bloquea todos los servicios de uso compartido, como Uso compartido de archivos y Pantalla compartida. Si usa servicios de uso compartido, mantenga este valor como *No configurado*.

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**

  Al establecer *Bloquear todas las conexiones entrantes* en *No configurado*, puede configurar qué aplicaciones pueden o no recibir conexiones entrantes.

  **Aplicaciones permitidas**: configure una lista de las aplicaciones con permiso para recibir conexiones entrantes.

  - **Agregar aplicaciones por id. de agrupación**: escriba el [id. de agrupación](../configuration/bundle-ids-built-in-ios-apps.md) de la aplicación. El sitio web de Apple tiene una lista de [aplicaciones de Apple integradas](https://support.apple.com/HT208094).
  - **Agregar aplicación de la tienda**: seleccione una aplicación de la tienda que haya agregado previamente a Intune. Para más información, vea [Agregar aplicaciones a Microsoft Intune](../apps/apps-add.md).

  **Aplicaciones bloqueadas**: configure una lista de las aplicaciones que tienen bloqueadas las conexiones entrantes.

  - **Agregar aplicaciones por id. de agrupación**: escriba el [id. de agrupación](../configuration/bundle-ids-built-in-ios-apps.md) de la aplicación. El sitio web de Apple tiene una lista de [aplicaciones de Apple integradas](https://support.apple.com/HT208094).
  - **Agregar aplicación de la tienda**: seleccione una aplicación de la tienda que haya agregado previamente a Intune. Para más información, vea [Agregar aplicaciones a Microsoft Intune](../apps/apps-add.md).

- **Habilitar el modo sigiloso**

  Habilite el modo sigiloso para impedir que el equipo responda a solicitudes de sondeo. El dispositivo sigue respondiendo a las solicitudes entrantes de las aplicaciones autorizadas. Las solicitudes inesperadas, como ICMP (ping), se ignoran.

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**

## <a name="gatekeeper"></a>Equipo selector

- **Permitir aplicaciones descargadas desde estas ubicaciones**

  Limitar las aplicaciones que puede iniciar un dispositivo, en función de dónde se hayan descargado las aplicaciones. El fin es proteger los dispositivos frente al malware y permitir únicamente aplicaciones de orígenes de confianza.

  - **Sin configurar** (*valor predeterminado*).
  - **Mac App Store**
  - **Mac App Store y desarrolladores identificados**
  - **Cualquier ubicación**

- **No permitir que el usuario invalide Gatekeeper**

  Impide que los usuarios invaliden el valor del equipo selector y que presionen Control+clic para instalar una aplicación. Si está habilitado, los usuarios pueden presionar Control+clic en cualquier aplicación e instalarla.

  - **No configurado** (*valor predeterminado*): los usuarios pueden presionar la tecla Control y hacer clic para instalar aplicaciones.
  - **Sí**: impide que los usuarios usen la combinación de la tecla Control y hacer clic para instalar aplicaciones.

## <a name="filevault"></a>FileVault

Para obtener más información sobre la configuración de FileVault de Apple, vea [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) en el contenido para desarrolladores de Apple.

> [!IMPORTANT]
> A partir de macOS 10.15, la configuración de FileVault requiere la inscripción de MDM aprobada por el usuario.

- **Habilitación de FileVault**  

  Puede *habilitar* el cifrado de disco completo mediante XTS-AES 128 con FileVault en dispositivos que ejecuten macOS 10.13 y versiones posteriores.

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**

  Cuando *Habilitar FileVault* se establece en *Sí*, se pueden configurar los valores siguientes:

  - **Tipo de clave de recuperación**

    Las claves de recuperación de *Clave personal* se crean para los dispositivos. Configure las opciones siguientes para la clave personal.

  - **Descripción de la ubicación secundaria de la clave de recuperación personal**

    Especifique un mensaje breve para el usuario en el que se explique cómo y dónde puede recuperar su clave de recuperación personal. Este texto se inserta en el mensaje que el usuario ve en la pantalla de inicio de sesión cuando se le solicita que escriba su clave de recuperación personal en caso de que se haya olvidado una contraseña.

  - **Rotación de clave de recuperación personal**

    Especifique la frecuencia con la que se rotará la clave de recuperación personal para un dispositivo. Puede seleccionar el valor predeterminado, que es **No configurado**, o un valor de **1** a **12** meses.

  - **Ocultar clave de recuperación**

    Elija ocultar la clave personal de un usuario del dispositivo durante el cifrado de FileVault 2.

    - **No configurado** (*valor predeterminado*): la clave personal es visible para el usuario del dispositivo durante el cifrado.
    - **Sí**: la clave personal se oculta al usuario del dispositivo durante el cifrado.

    Después del cifrado, los usuarios del dispositivo pueden ver su clave de recuperación personal para un dispositivo macOS cifrado desde las ubicaciones siguientes:
    - Aplicación Portal de empresa de iOS/iPadOS
    - Aplicación de Intune
    - Sitio web del Portal de empresa
    - Aplicación del portal de la compañía de Android

    Para ver la clave, desde la aplicación o el sitio web, vaya a los detalles del dispositivo macOS cifrado y seleccione *Obtener la clave de recuperación*.

  - **Deshabilitar mensaje al cerrar sesión**

    Evite el mensaje en el que se solicita al usuario que habilite FileVault cuando cierre la sesión.  Cuando se establece en Deshabilitar, al cerrar la sesión el mensaje está deshabilitado y, en su lugar, se le solicita cuando el usuario inicia sesión.

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: se deshabilita el mensaje al cerrar sesión.

  - **Número de veces que se permite omitir**

    Establece el número de veces que un usuario puede pasar por alto los mensajes para habilitar FileVault antes de que sea necesario para iniciar sesión.

    - **No configurado**: se requiere cifrado en el dispositivo antes de que se permita el siguiente inicio de sesión.
    - **0**: se requiere que los dispositivos se cifren la próxima vez que un usuario inicie sesión en el dispositivo.
    - De **1** a **10**: permite al usuario omitir el mensaje de 1 a 10 veces antes de requerir el cifrado en el dispositivo.
    - **No hay límite, avisar siempre**: se solicita al usuario que habilite FileVault, pero el cifrado nunca es necesario.

    El valor predeterminado de esta opción depende de la configuración de *Deshabilitar mensaje al cerrar sesión*. Cuando la opción *Deshabilitar mensaje al cerrar sesión* se establece en **No configurado**, este valor se establece de forma predeterminada en **No configurado**. Cuando *Deshabilitar mensaje al cerrar sesión* se establece en **Sí**, el valor predeterminado es **1** y el valor **No configurado** no es una opción.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](../configuration/device-profile-assign.md) y [supervise el estado](../configuration/device-profile-monitor.md).

También puede configurar Endpoint Protection en [dispositivos con Windows 10 y otros más recientes](endpoint-protection-windows-10.md).
