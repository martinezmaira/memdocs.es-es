---
title: 'Configuración de Wi-Fi para dispositivos Windows 10 en Microsoft Intune: Azure | Microsoft Docs'
description: Agregue o cree el perfil de configuración de Wi-Fi mediante la configuración de Wi-Fi para dispositivos Windows 10 y versiones posteriores en Microsoft Intune. Puede configurar la configuración básica o de nivel empresarial.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.reviewer: tycast
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d47f1e121a5010a17d213d21d3208977e8f75514
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217632"
---
# <a name="add-wi-fi-settings-for-windows-10-and-later-devices-in-intune"></a>Agregar Wi-Fi para dispositivos Windows 10 y versiones posteriores en Intune

Puede crear un perfil con una configuración específica de Wi-Fi y después implementar este perfil en dispositivos Windows 10 y versiones posteriores. Microsoft Intune ofrece muchas características, incluidas la autenticación en la red, con el uso de una clave precompartida, y mucho más.

Ambas se describen en este artículo.

## <a name="before-you-begin"></a>Antes de comenzar

[Creación de un perfil de dispositivo en Microsoft Intune](wi-fi-settings-configure.md).

## <a name="basic-profile"></a>Perfil básico

Los perfiles personales o básicos usan WPA/WPA2 para proteger la conexión Wi-Fi en los dispositivos. Normalmente, WPA/WPA2 se usa en redes domésticas o redes personales. También puede agregar una clave previamente compartida para autenticar la conexión.

- **Tipo de Wi-Fi**: Elija **Básica**. 

- **Nombre de Wi-Fi (SSID)** : abreviatura de identificador de conjunto de servicios. Este valor es el nombre real de la red inalámbrica a la que se conectan los dispositivos. Pero cuando los usuarios eligen la conexión, solo ven el **Nombre de conexión** que configure.

- **Nombre de la conexión**: Escriba un nombre descriptivo para esta conexión Wi-Fi. El texto que escriba es el nombre que ven los usuarios cuando exploran las conexiones disponibles en sus dispositivos.

- **Conectarse automáticamente cuando esté dentro del alcance**: cuando es **Sí**, los dispositivos se conectan automáticamente cuando están en el alcance de esta red. Cuando es **No**, los dispositivos no se conectan automáticamente.

  - **Conectarse a una red con mayor preferencia, si está disponible**: si los dispositivos están en el alcance de una red con mayor preferencia, elija **Sí** para usarla. Haga clic en **No** para usar la red Wi-Fi de este perfil de configuración.

    Por ejemplo, crea una red Wi-Fi **ContosoCorp** y usa **ContosoCorp** dentro de este perfil de configuración. También tiene una red Wi-Fi **ContosoGuest** dentro del alcance. Cuando los dispositivos corporativos estén dentro del alcance, quiere que se conecten automáticamente a **ContosoCorp**. En este escenario, establezca la propiedad **Conectarse a una red con mayor preferencia si está disponible** en **No**.

  - **Conectarse a esta red, incluso aunque no difunda su SSID**: elija **Sí** para que el perfil de configuración se conecte automáticamente a la red, incluso cuando está oculta (es decir, su SSID no se difunde públicamente). Haga clic en **No** si no quiere que este perfil de configuración se conecte a la red oculta.

- **Límite de conexión de uso medido**: un administrador puede elegir cómo se mide el tráfico. Las aplicaciones pueden luego ajustar su comportamiento de tráfico de red según este valor. Las opciones son:

  - **Sin restricciones**: predeterminado. No se mide la conexión y no existen restricciones en el tráfico.
  - **Fijo**: use esta opción si la red está configurada con un límite fijo para el tráfico. Cuando se alcanza este límite, se prohíbe el acceso a la red.
  - **Variable**: use esta opción si el tráfico se cobra por byte (costo por byte).

- **Tipo de seguridad inalámbrica**: escriba el protocolo de seguridad que se usa para autenticar los dispositivos en la red. Las opciones son:
  - **Abierta (sin autenticación)** : use esta opción solo si la red no es segura.
  - **WPA o WPA2-Personal**: una opción más segura y que suele usarse para conectividad mediante Wi-Fi. Para mayor seguridad, también puede escribir una contraseña de clave precompartida o una clave de red.

    - **Clave precompartida** (PSK): Opcional. Se muestra cuando se elige **WPA o WPA2-Personal** como tipo de seguridad. Una vez configurada la red de su organización, también se configuran una contraseña o una clave de red. Escriba esta contraseña o clave de red para el valor PSK. Escriba una cadena de entre 8 y 64 caracteres. Si la contraseña o la clave de red es de 64 caracteres, escriba caracteres hexadecimales.

      > [!IMPORTANT]
      > La PSK es la misma para todos los dispositivos a los que se dirige el perfil. Si la clave está en peligro, cualquier dispositivo puede usarla para conectarse a la red Wi-Fi. Mantenga segura la PSK para evitar el acceso no autorizado.

- **Configuración del proxy de la empresa**: elija la configuración del proxy que se va a usar en la organización. Las opciones son:
  - **Ninguna**: no se ha configurado ningún valor de proxy.
  - **Configurar manualmente**: escriba la **Dirección IP del servidor proxy** y su **Número de puerto**.
  - **Configurar automáticamente**: escriba la dirección URL que apunta a un script de configuración automática de proxy (PAC). Por ejemplo, escriba `http://proxy.contoso.com/proxy.pac`.

## <a name="enterprise-profile"></a>Perfil de empresa

Los perfiles Enterprise usan el Protocolo de autenticación extensible (EAP) para autenticar las conexiones Wi-Fi. EAP se suele usar en empresas, ya que puede utilizar certificados para autenticar y proteger las conexiones, y configurar más opciones de seguridad.

- **Tipo de Wi-Fi**: elija **Empresa**.

- **Nombre de Wi-Fi (SSID)** : abreviatura de identificador de conjunto de servicios. Este valor es el nombre real de la red inalámbrica a la que se conectan los dispositivos. Pero cuando los usuarios eligen la conexión, solo ven el **Nombre de conexión** que configure.

- **Nombre de la conexión**: Escriba un nombre descriptivo para esta conexión Wi-Fi. El texto que escriba es el nombre que ven los usuarios cuando exploran las conexiones disponibles en sus dispositivos.

- **Conectarse automáticamente cuando esté dentro del alcance**: cuando es **Sí**, los dispositivos se conectan automáticamente cuando están en el alcance de esta red. Cuando es **No**, los dispositivos no se conectan automáticamente.
  - **Conectarse a una red con mayor preferencia, si está disponible**: si los dispositivos están en el alcance de una red con mayor preferencia, elija **Sí** para usarla. Haga clic en **No** para usar la red Wi-Fi de este perfil de configuración.

    Por ejemplo, crea una red Wi-Fi **ContosoCorp** y usa **ContosoCorp** dentro de este perfil de configuración. También tiene una red Wi-Fi **ContosoGuest** dentro del alcance. Cuando los dispositivos corporativos estén dentro del alcance, quiere que se conecten automáticamente a **ContosoCorp**. En este escenario, establezca la propiedad **Conectarse a una red con mayor preferencia si está disponible** en **No**.

  - **Conectarse a esta red, incluso aunque no difunda su SSID**: elija **Sí** para que el perfil de configuración se conecte automáticamente a la red, incluso cuando está oculta (es decir, su SSID no se difunde públicamente). Haga clic en **No** si no quiere que este perfil de configuración se conecte a la red oculta.

- **Límite de conexión de uso medido**: un administrador puede elegir cómo se mide el tráfico. Las aplicaciones pueden luego ajustar su comportamiento de tráfico de red según este valor. Las opciones son:

  - **Sin restricciones**: predeterminado. No se mide la conexión y no existen restricciones en el tráfico.
  - **Fijo**: use esta opción si la red está configurada con un límite fijo para el tráfico. Cuando se alcanza este límite, se prohíbe el acceso a la red.
  - **Variable**: use esta opción si el tráfico se cobra por byte.

- **Inicio de sesión único (SSO)** : permite configurar el inicio de sesión único (SSO), donde se comparten las credenciales para el equipo y el inicio de sesión de red Wi-Fi. Las opciones son:
  - **Deshabilitar**: se deshabilita el comportamiento de SSO. El usuario debe autenticarse en la red por separado.
  - **Habilitar antes de que el usuario inicie sesión en el dispositivo**: use SSO para autenticarse en la red justo antes del proceso de inicio de sesión del usuario.
  - **Habilitar después de que el usuario inicie sesión en el dispositivo**: use SSO para autenticarse en la red justo después de que finalice el proceso de inicio de sesión del usuario.
  - **Tiempo máximo para autenticarse antes del tiempo de espera**: escriba el número máximo de segundos que deben transcurrir antes de autenticarse en la red, de 1 a 120 segundos.
  - **Permitir que Windows solicite al usuario credenciales de autenticación adicionales**: si se hace clic en **Sí** se permite que el sistema Windows solicite al usuario credenciales de autenticación adicionales en caso de que el método de autenticación lo requiera. Haga clic en **No** para ocultar estos mensajes.

- **Habilitar almacenamiento en caché de Clave maestra en pares (PMK)** : seleccione **Sí** para almacenar en caché la PMK usada en la autenticación. Este almacenamiento en caché normalmente permite que la autenticación en la red se complete más rápido. Haga clic en **No** para forzar el protocolo de enlace de autenticación al conectarse a la red Wi-Fi cada vez. Para usar el valor **Habilitar la autenticación previa**, seleccione **Sí**.

  - **Tiempo máximo que se almacena en caché una PMK**: escriba el número de minutos que una Clave maestra en pares (PMK) se almacena en caché, de 5 a 1440 minutos.
  - **Número máximo de PMK almacenadas en caché**: escriba el número de claves almacenadas en caché, de 1 a 255.

- **Habilitar la autenticación previa**: la autenticación previa permite que el perfil se autentique en todos los puntos de acceso para la red del perfil antes de conectarse. Al moverse entre puntos de acceso, la autenticación previa vuelva a conectar al usuario o los dispositivos más rápidamente. Haga clic en **Sí** para que el perfil se autentique en todos los puntos de acceso para esta red que estén dentro del alcance. Haga clic en **No** para requerir que el usuario o dispositivo se autentique por separado en cada punto de acceso.

  Para usar esta opción, establezca **Habilitar almacenamiento en caché de Clave maestra en pares (PMK)** en **Sí**.

  - **Número máximo de intentos de autenticación previa**: escriba el número de intentos de autenticación previa, de 1 a 16.

- **Tipo de EAP**: elija el tipo de Protocolo de autenticación extensible (EAP) para autenticar las conexiones inalámbricas seguras. Las opciones son:

  - **EAP-SIM**
  - **EAP-TLS**
  - **EAP-TTLS**
  - **EAP protegido** (PEAP)

    **Configuración adicional de EAP-TLS, EAP-TTLS y PEAP**:

    > [!NOTE]
    > Solo se admiten los perfiles de certificado SCEP y PKCS cuando se usa un tipo de EAP.

    - **Confianza del servidor**  

      **Nombres de servidor de certificados**: se usan con los tipos de EAP **EAP-TLS**, **EAP-TTLS** o **PEAP**. Escriba uno o más nombres comunes usados en los certificados emitidos por la entidad de certificación (CA) de confianza. Si escribe esta información, puede omitir el cuadro de diálogo de confianza dinámica que se muestra en los dispositivos de los usuarios cuando se conectan a esta red Wi-Fi.  

      **Certificado raíz para validación del servidor**: se usan con los tipos de EAP **EAP-TLS**, **EAP-TTLS** o **PEAP**. Seleccione el perfil de certificado raíz de confianza que se usa para autenticar la conexión.  

      **Privacidad de identidad (identidad externa)** : se usa con el tipo de EAP **PEAP**. Escriba el texto que se envía como respuesta a una solicitud de identidad EAP. Este texto puede ser cualquier valor. Durante la autenticación, esta identidad anónima se envía inicialmente, seguida de la identificación real enviada en un túnel seguro.  

    - **Autenticación de cliente**

      **Certificado de cliente para la autenticación del cliente (certificado de identidad)** : se usa con el tipo de EAP **EAP-TLS**. Seleccione el perfil de certificado que se usa para autenticar la conexión.

      **Método de autenticación**: se usa con el tipo de EAP **EAP-TTLS**. Seleccione el método de autenticación para la conexión:  

      - **Certificados**: seleccione el certificado de cliente que es el certificado de identidad presentado al servidor.
      - **Nombre de usuario y contraseña**: escriba un **Método que no sea EAP (identidad interna)** para la autenticación. Las opciones son:

        - **Contraseña no cifrada (PAP)**
        - **Desafío mutuo (CHAP)**
        - **Microsoft CHAP (MS-CHAP)**
        - **Microsoft CHAP versión 2 (MS-CHAP v2)**

      **Privacidad de identidad (identidad externa)** : se usa con el tipo de EAP **EAP-TTLS**. Escriba el texto que se envía como respuesta a una solicitud de identidad EAP. Este texto puede ser cualquier valor. Durante la autenticación, esta identidad anónima se envía inicialmente, seguida de la identificación real enviada en un túnel seguro.

- **Configuración del proxy de la empresa**: elija la configuración del proxy que se va a usar en la organización. Las opciones son:
  - **Ninguna**: no se ha configurado ningún valor de proxy.
  - **Configurar manualmente**: escriba la **Dirección IP del servidor proxy** y su **Número de puerto**.
  - **Configurar automáticamente**: escriba la dirección URL que apunta a un script de configuración automática de proxy (PAC). Por ejemplo, escriba `http://proxy.contoso.com/proxy.pac`.

- **Exigir que el perfil de Wi-Fi sea compatible con el Estándar federal de procesamiento de información (FIPS)** : elija **Sí** al validarlo con el estándar FIPS 140-2. Este estándar es necesario para todas las agencias del gobierno federal de Estados Unidos que usan sistemas de seguridad basados en criptografía para proteger la información confidencial pero sin clasificar que se almacena digitalmente. Haga clic en **No** para que no sea compatible con FIPS.

## <a name="use-an-imported-settings-file"></a>Usar un archivo de configuración importado

Para cualquier configuración que no esté disponible en Intune, puede exportar la configuración de Wi-Fi desde otro dispositivo Windows. Esta exportación crea un archivo XML con toda la configuración. Después, importe este archivo en Intune y úselo como el perfil de Wi-Fi. Vea [Exportación e importación de la configuración de Wi-Fi para dispositivos Windows](wi-fi-settings-import-windows-8-1.md).

## <a name="next-steps"></a>Pasos siguientes

Se crea el perfil, pero no hacen nada. A continuación, [asigne este perfil](device-profile-assign.md).

## <a name="more-resources"></a>Más recursos

- Vea las opciones disponibles para [Windows 8.1](wi-fi-settings-import-windows-8-1.md).
- [Introducción a la configuración de Wi-Fi](wi-fi-settings-configure.md), incluidas otras plataformas.
