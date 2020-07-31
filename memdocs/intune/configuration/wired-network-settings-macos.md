---
title: Configuración de red cableada para dispositivos macOS en Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Cree o agregue un perfil de configuración de dispositivos de red cableada para dispositivos macOS. Vea las diferentes configuraciones, agregue certificados, elija un tipo de EAP y seleccione un método de autenticación en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1da738611dd5fe114054645170d2b49ef12f0523
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334613"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>Incorporación de la configuración de red cableada para dispositivos macOS en Microsoft Intune

Puede crear un perfil con una configuración específica de red cableada y después implementar este perfil en los dispositivos macOS. Microsoft Intune ofrece muchas características, incluidas la autenticación en la red, agregar un certificado SCEP y muchas más.

En este artículo se describen las opciones que se pueden configurar.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de dispositivos de red cableada](wired-networks-configure.md).

> [!NOTE]
> Estas configuraciones están disponibles para todos los tipos de inscripción. Para más información sobre los tipos de inscripción, consulte [Inscripción de macOS](../enrollment/macos-enroll.md).

## <a name="wired-network"></a>Red cableada

- **Interfaz de red**: Seleccione las interfaces de red del dispositivo al que se aplica el perfil, en función de la prioridad del orden del servicio. Las opciones son:
  
  - **Primera Ethernet activa** (valor predeterminado)
  - **Segunda Ethernet activa**
  - **Tercera Ethernet activa**
  - **Primera Ethernet**
  - **Segunda Ethernet**
  - **Tercera Ethernet**
  - **Cualquier Ethernet**

  Las opciones que tienen la palabra "activa" en el título usan interfaces que funcionan activamente en el dispositivo. Si no hay interfaces activas, se configura la siguiente interfaz según la prioridad del orden del servicio. De forma predeterminada, se selecciona **Primera Ethernet activa**, que también es el valor predeterminado que configura macOS.

- **Tipo de EAP**: seleccione el tipo de Protocolo de autenticación extensible (EAP) para autenticar las conexiones cableadas seguras. Las opciones son:

  - **EAP-FAST**: escriba la **Configuración de las credenciales de acceso protegido (PAC)** . Esta opción usa credenciales de acceso protegido para crear un túnel autenticado entre el cliente y el servidor de autenticación. Las opciones son:
    - **No usar (PAC)**
    - **Usar (PAC)** : si existe un archivo PAC, úselo.
    - **Usar y aprovisionar PAC**: cree y agregue el archivo PAC a los dispositivos.
    - **Usar y aprovisionar PAC anónimamente**: cree y agregue el archivo PAC a los dispositivos sin autenticación en el servidor.

  - **EAP-TLS**: Indique también:

    - **Confianza del servidor** - **Nombres de servidor de certificados**: **agregue** uno o varios nombres comunes usados en los certificados emitidos por la entidad de certificación (CA) de confianza. Al escribir esta información, puede omitir la ventana de confianza dinámica que se muestra en los dispositivos de los usuarios cuando se conectan a esta red.
    - **Certificado raíz para validación del servidor**: seleccione un perfil de certificado raíz de confianza existente. Cuando el cliente se conecta a la red, este certificado se presenta al servidor. Se usa para autenticar la conexión.
    - **Autenticación de cliente** - **Certificados**: seleccione el perfil de certificado de cliente SCEP que también se implementa en el dispositivo. Este certificado es la identidad presentada por el dispositivo al servidor para autenticar la conexión. No se admiten certificados PKCS.
    - **Privacidad de identidad (identidad interna)** : escriba el texto que se envía como respuesta a una solicitud de identidad EAP. Este texto puede ser cualquier valor, como `anonymous`. Durante la autenticación, esta identidad anónima se envía inicialmente, seguida de la identificación real enviada en un túnel seguro.

  - **EAP-TTLS**: Indique también:

    - **Confianza del servidor** - **Nombres de servidor de certificados**: **agregue** uno o varios nombres comunes usados en los certificados emitidos por la entidad de certificación (CA) de confianza. Al escribir esta información, puede omitir la ventana de confianza dinámica que se muestra en los dispositivos de los usuarios cuando se conectan a esta red.
    - **Certificado raíz para validación del servidor**: seleccione un perfil de certificado raíz de confianza existente. Cuando el cliente se conecta a la red, este certificado se presenta al servidor. Se usa para autenticar la conexión.
    - **Autenticación de cliente**: seleccione un **método de autenticación**. Las opciones son:
      - **Nombre de usuario y contraseña**: pide al usuario un nombre de usuario y una contraseña para autenticar la conexión. Indique también:
        - **Método que no es EAP (identidad interna)** : seleccione cómo autenticar la conexión. Asegúrese de elegir el mismo protocolo que está configurado en su red. Las opciones son:
          - **Contraseña no cifrada (PAP)**
          - **Protocolo de autenticación de desafío mutuo (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP versión 2 (MS-CHAP v2)**
      - **Certificados**: seleccione el perfil de certificado de cliente SCEP que también se implementa en el dispositivo. Este certificado es la identidad presentada por el dispositivo al servidor para autenticar la conexión. No se admiten certificados PKCS.
      - **Privacidad de identidad (identidad interna)** : escriba el texto que se envía como respuesta a una solicitud de identidad EAP. Este texto puede ser cualquier valor, como `anonymous`. Durante la autenticación, esta identidad anónima se envía inicialmente, seguida de la identificación real enviada en un túnel seguro.

  - **LEAP**

  - **PEAP**: Indique también:

    - **Confianza del servidor** - **Nombres de servidor de certificados**: **agregue** uno o varios nombres comunes usados en los certificados emitidos por la entidad de certificación (CA) de confianza. Al escribir esta información, puede omitir la ventana de confianza dinámica que se muestra en los dispositivos de los usuarios cuando se conectan a esta red.
    - **Certificado raíz para validación del servidor**: seleccione un perfil de certificado raíz de confianza existente. Cuando el cliente se conecta a la red, este certificado se presenta al servidor. Se usa para autenticar la conexión.
    - **Autenticación de cliente**: seleccione un **método de autenticación**. Las opciones son:
      - **Nombre de usuario y contraseña**: pide al usuario un nombre de usuario y una contraseña para autenticar la conexión.
      - **Certificados**: seleccione el perfil de certificado de cliente SCEP que también se implementa en el dispositivo. Este certificado es la identidad presentada por el dispositivo al servidor para autenticar la conexión. No se admiten certificados PKCS.
      - **Privacidad de identidad (identidad interna)** : escriba el texto que se envía como respuesta a una solicitud de identidad EAP. Este texto puede ser cualquier valor, como `anonymous`. Durante la autenticación, esta identidad anónima se envía inicialmente, seguida de la identificación real enviada en un túnel seguro.

## <a name="next-steps"></a>Pasos siguientes

El perfil se crea, pero puede que no haga nada. Asegúrese de [asignar el perfil](device-profile-assign.md) y [supervisar el estado](device-profile-monitor.md).
