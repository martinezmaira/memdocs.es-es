---
title: 'Agregar Endpoint Protection de macOS en Microsoft Intune: Azure | Microsoft Docs'
description: En los dispositivos macOS, use el equipo selector para determinar dónde se pueden instalar las aplicaciones, incluidas las de Mac App Store. Además, habilite o configure un firewall para permitir aplicaciones concretas, bloquear otras, usar el modo sigiloso e incluso bloquear determinados tipos de conexiones entrantes mediante Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e857cdd7028851f14f607739ba7e37c744fa2f1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359458"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Configuración de Endpoint Protection de macOS en Intune  

En este artículo se muestran las opciones de Endpoint Protection que se pueden configurar para los dispositivos con macOS. Estas opciones se configuran mediante un perfil de configuración de dispositivo macOS para [Endpoint Protection](endpoint-protection-configure.md) en Intune.  

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de Endpoint Protection de macOS](endpoint-protection-configure.md).

## <a name="gatekeeper"></a>Equipo selector  

- **Permitir aplicaciones descargadas desde estas ubicaciones**  
  Limitar las aplicaciones que puede iniciar un dispositivo, en función de dónde se hayan descargado las aplicaciones. El fin es proteger los dispositivos frente al malware y permitir únicamente aplicaciones de orígenes de confianza.  

  - **No configurado**.  
  - **Mac App Store**  
  - **Mac App Store y desarrolladores identificados**  
  - **Cualquier ubicación**  

  **Valor predeterminado**: No configurado  

- **El usuario puede invalidar Gatekeeper**  
  Impide que los usuarios invaliden el valor del equipo selector y que presionen Control+clic para instalar una aplicación. Si está habilitado, los usuarios pueden presionar Control+clic en cualquier aplicación e instalarla.  
 
  - **No configurado**: los usuarios pueden presionar la tecla Control y hacer clic para instalar aplicaciones.  
  - **Bloquear**: impide que los usuarios usen la combinación tecla Control y hacer clic para instalar aplicaciones.  

  **Valor predeterminado**: No configurado  

## <a name="firewall"></a>Firewall  

Use el firewall para controlar conexiones por aplicación en lugar de por puerto. La configuración por aplicación permite aprovechar las ventajas de la protección del firewall con más facilidad. También ayuda a evitar que aplicaciones no deseadas tomen el control de los puertos de red que están abiertos para las aplicaciones legítimas.  

**General**
- **Firewall**  
  Habilite el firewall para configurar la administración de las conexiones entrantes en el entorno.  
  - **No configurado**.  
  - **Habilitar**  

  **Valor predeterminado**: No configurado  

- **Conexiones entrantes**  
  Bloquee todas las conexiones entrantes excepto las necesarias para los servicios básicos de Internet, como DHCP, Bonjour e IPSec. Esta característica también bloquea todos los servicios de uso compartido, como Uso compartido de archivos y Pantalla compartida. Si usa servicios de uso compartido, mantenga este valor como *No configurado*.  
  - **No configurado**.  
  - **Bloquear**  

  **Valor predeterminado**: No configurado  

**Permita o bloquee conexiones entrantes de aplicaciones concretas.**  

  - **Aplicaciones permitidas**  
    Seleccione las aplicaciones a las que de forma explícita se permite recibir conexiones entrantes.  

  - **Aplicaciones bloqueadas**  
    Seleccione las aplicaciones que deben bloquear conexiones entrantes.  

  - **Modo sigiloso**  
    Habilite el modo sigiloso para impedir que el equipo responda a solicitudes de sondeo. El dispositivo sigue respondiendo a las solicitudes entrantes de las aplicaciones autorizadas. Las solicitudes inesperadas, como ICMP (ping), se ignoran.  
    - **No configurado**.  
    - **Habilitar**  

    **Valor predeterminado**: No configurado  

## <a name="filevault"></a>FileVault  
Para obtener más información sobre la configuración de FileVault de Apple, vea [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) en el contenido para desarrolladores de Apple. 

> [!IMPORTANT]  
> A partir de macOS 10.15, la configuración de FileVault requiere la inscripción de MDM aprobada por el usuario. 

- **FileVault**  
  Puede *habilitar* el cifrado de disco completo mediante XTS-AES 128 con FileVault en dispositivos que ejecuten macOS 10.13 y versiones posteriores.  
  - **No configurado**.  
  - **Habilitar**  

  **Valor predeterminado**: No configurado  

  - **Tipo de clave de recuperación**  
    Las claves de recuperación de *Clave personal* se crean para los dispositivos. Configure las opciones siguientes para la clave personal.  

    - **Ubicación de la clave de recuperación personal**: especifique un mensaje breve para el usuario que explique cómo y dónde puede recuperar su clave de recuperación personal. Este texto se inserta en el mensaje que el usuario ve en la pantalla de inicio de sesión cuando se le pide que escriba su clave de recuperación personal en caso de que se haya olvidado una contraseña.  

    - **Rotación de clave de recuperación personal**: especifique la frecuencia con la que se rotará la clave de recuperación personal para un dispositivo. Puede seleccionar el valor predeterminado, que es **No configurado**, o un valor de **1** a **12** meses.  

  - **Deshabilitar mensaje al cerrar sesión**  
    Evite el mensaje en el que se solicita al usuario que habilite FileVault cuando cierre la sesión.  Cuando se establece en Deshabilitar, al cerrar la sesión el mensaje está deshabilitado y, en su lugar, se le solicita cuando el usuario inicia sesión.  
    - **No configurado**.  
    - **Deshabilitar**: deshabilite el mensaje al cerrar sesión.

    **Valor predeterminado**: No configurado  

  - **Número de veces que se permite omitir**  
  Establece el número de veces que un usuario puede pasar por alto los mensajes para habilitar FileVault antes de que sea necesario para iniciar sesión. 

    - **No configurado**: se requiere cifrado en el dispositivo antes de que se permita el siguiente inicio de sesión.  
    - De **1** a **10**: permite al usuario omitir el mensaje de 1 a 10 veces antes de requerir el cifrado en el dispositivo.  
    - **No hay límite, avisar siempre**: se solicita al usuario que habilite FileVault, pero el cifrado nunca es necesario.  
 
    **Valor predeterminado**: *Varía*: cuando la opción *Deshabilitar mensaje al cerrar sesión* está establecida en **No configurado**, este valor se establece de forma predeterminada en **No configurado**. Cuando *Deshabilitar mensaje al cerrar sesión* se establece en **Deshabilitar**, el valor predeterminado es **1** y el valor **No configurado** no es una opción.

Para obtener más información sobre FileVault con Intune, vea [Claves de recuperación de FileVault](encryption-monitor.md#filevault-recovery-keys).

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](../configuration/device-profile-assign.md) y [supervise el estado](../configuration/device-profile-monitor.md).

También puede configurar Endpoint Protection en [dispositivos con Windows 10 y otros más recientes](endpoint-protection-windows-10.md).
