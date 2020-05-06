---
title: Creación de perfiles de VPN
titleSuffix: Configuration Manager
description: Aprenda a crear perfiles de VPN en Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694253"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Creación de perfiles de VPN en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager admite varios tipos de conexión VPN. Para más información sobre los tipos de conexión disponibles para las distintas plataformas de dispositivos, consulte [Perfiles de VPN](vpn-profiles.md).

En el caso de conexiones VPN de terceros, distribuya la aplicación VPN antes de implementar el perfil de VPN. Si no implementa la aplicación, se les pedirá a los usuarios que lo hagan cuando intenten conectarse a la VPN. Para obtener más información, consulte [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implementar aplicaciones).

## <a name="create-a-vpn-profile"></a>Crear un perfil de VPN

1. Vaya al área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la empresa** y seleccione **Perfiles de VPN**.

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, elija **Crear perfil de VPN**.

1. En la página **General** del Asistente para crear perfil de VPN, especifique la información siguiente:

    - **Nombre**: escriba un nombre único para identificar el perfil de VPN en la consola.

        > [!NOTE]
        > No use estos caracteres en el nombre del perfil de VPN: `\/:*?<>|; `. El perfil de VPN de Windows no admite estos caracteres especiales.

    - **Descripción**: si quiere, escriba una descripción para proporcionar más información sobre el perfil de VPN.

    - **Tipo de perfil de VPN**: seleccione la plataforma adecuada.

        Si selecciona la plataforma **Windows 8.1**, también puede **Importar desde archivo**. Esta acción importa información del perfil de VPN desde un archivo XML. Si selecciona esta opción, el resto del asistente se simplifica a la páginas siguientes: **Plataformas compatibles** e **Importar perfil de VPN**.

1. En la página **Plataformas compatibles**, seleccione las versiones de sistema operativo compatibles con este perfil de VPN.

1. En la página **Conexión**, especifique esta información:

    - **Tipo de conexión**: elija el tipo de conexión VPN. Para más información sobre los tipos compatibles, consulte [Perfiles de VPN](vpn-profiles.md).

    - **Lista de servidores**: agregue un nuevo servidor que se usará para la conexión VPN. Según el tipo de conexión, puede agregar uno o más servidores VPN y especificar cuál es el servidor predeterminado.

    - **Omitir la VPN al conectarse a la red de la compañía**: configure los clientes para que no usen la VPN cuando estén dentro de la red interna. Si es necesario, especifique un nombre DNS específico para la conexión.

1. En la página **Método de autenticación** del asistente, elija un método compatible con el tipo de conexión. La configuración y las opciones disponibles en esta página varían en función del tipo de conexión seleccionado. Para más información, consulte [Referencia del método de autenticación](#bkmk_auth).

1. En la página **Configuración de proxy**, si la VPN usa un servidor proxy, seleccione una de las opciones según corresponda para su entorno. A continuación, proporcione la información de configuración para el proxy.

1. La página **Aplicaciones** solo se aplica a los perfiles de Windows 10. Agregue aplicaciones de escritorio y universales que se conecten automáticamente a esta VPN. El tipo de aplicación determina el identificador de la aplicación:

    - Para una *aplicación de escritorio*, proporcione la ruta de acceso al archivo de la aplicación.

    - Para una *aplicación universal*, proporcione el nombre de familia de paquete (PFN). Para obtener información sobre cómo buscar el PFN de una aplicación, consulte [Find a package family name for per-app VPN](find-a-pfn-for-per-app-vpn.md) (Buscar un nombre de familia de paquete para VPN por aplicación).

    También puede configurar una opción para que **solo las aplicaciones de la lista puedan usar esta VPN**.

    > [!IMPORTANT]
    > Proteja todas las listas de aplicaciones asociadas que se compilan para configurar una VPN por aplicación. Si un usuario no autorizado modifica la lista y usted la importa a la lista de aplicaciones de VPN por aplicación, podría autorizar el acceso a VPN a aplicaciones que no deberían tener acceso.

1. La página **Límites** solo se aplica a los perfiles de Windows 10 para configurar los límites de la VPN. Puede agregar estas opciones:

    - **Reglas de tráfico de red**: defina qué protocolos, puertos local y remoto e intervalos de direcciones se van a habilitar para la conexión VPN.  

        > [!Note]
        > Si no se crea ninguna regla de tráfico de red, se habilitan todos los protocolos, puertos e intervalos de direcciones. Una vez creada una regla, la conexión VPN solo usa los protocolos, puertos e intervalos de direcciones que especifique en esa regla o en reglas adicionales.

    - **Nombres y servidores DNS**: los servidores DNS que usa la conexión VPN una vez que el dispositivo establece la conexión.

    - **Rutas**: las rutas de red que usan la conexión VPN. La creación de más de 60 rutas puede producir un error en la directiva.

1. Complete el asistente.

El nuevo perfil de VPN se muestra en el nodo **Perfiles de VPN** en el área de trabajo **Activos y compatibilidad** .

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a> Referencia del método de autenticación

Los métodos de autenticación de VPN disponibles dependen del tipo de conexión:

### <a name="certificates"></a>Certificados

Si el certificado de cliente se autentica en un servidor RADIUS, como un Servidor de directivas de redes, establezca el nombre alternativo del firmante del certificado en el nombre principal de usuario.

Tipos de conexión admitidos:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- VPN móvil de punto de comprobación

### <a name="username-and-password"></a>Nombre de usuario y contraseña

Tipos de conexión admitidos:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- VPN móvil de punto de comprobación

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

Tipos de conexión admitidos:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>EAP (PEAP) protegido de Microsoft

Tipos de conexión admitidos:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Contraseña segura de Microsoft (EAP-MSCHAP v2)

Tipos de conexión admitidos:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Tarjeta inteligente u otro certificado

Tipos de conexión admitidos:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Tipos de conexión admitidos:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Usar certificados de equipo

Tipos de conexión admitidos:

- IKEv2

### <a name="additional-authentication-options"></a>Opciones de autenticación adicionales

Si la versión del cliente Windows lo admite, la opción de **Configurar** el método de autenticación está disponible. Esta opción abre la ventana de propiedades de Windows para configurar el método de autenticación.

En función de las opciones que seleccione, se le podría solicitar que especifique más información, por ejemplo:

- **Recordar las credenciales de usuario en cada inicio de sesión**: las credenciales de usuario se recuerdan para que los usuarios no tengan que escribirlas cada vez que se conecten.  

- **Seleccionar un certificado de cliente para autenticación de cliente**: seleccione un perfil de certificado SCEP de cliente creado previamente para autenticar la conexión VPN. Para obtener más información, vea [Crear perfiles de certificado PFX](create-certificate-profiles.md).

## <a name="next-steps"></a>Pasos siguientes

- En el caso de conexiones VPN de terceros, distribuya la aplicación VPN antes de implementar el perfil de VPN. Si no implementa la aplicación, se les pedirá a los usuarios que lo hagan cuando intenten conectarse a la VPN. Para obtener más información, consulte [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implementar aplicaciones).

- Implemente el perfil de VPN. Para obtener más información, vea [Cómo implementar perfiles](deploy-wifi-vpn-email-cert-profiles.md).
