---
title: 'Configuración y características de dispositivos en Microsoft Intune: Azure | Microsoft Docs'
description: Información general de los distintos perfiles de dispositivo de Microsoft Intune. Obtenga información sobre GPO, las características, restricciones, correo electrónico, Wi-Fi, VPN, educación, certificados, actualización de Windows 10, BitLocker y Microsoft Defender, Windows Information Protection, plantillas administrativas y opciones de configuración de dispositivos personalizadas en el centro de administración de Microsoft Endpoint Manager. Use estos perfiles para administrar y proteger los datos y los dispositivos de su compañía.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/20/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 61053fff9d28193c8f4fc1731f72fe0052aba154
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820500"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Aplicación de la configuración y características en dispositivos con perfiles de dispositivos Microsoft Intune

Microsoft Intune incluye valores de configuración y características que puede habilitar o deshabilitar en distintos dispositivos dentro de su organización. Estas características y opciones de configuración se agregan a los "perfiles de configuración". Puede crear perfiles para otros dispositivos y plataformas, como iOS/iPadOS, administrador de dispositivos Android, Android Enterprise y Windows. Luego, use Intune para aplicar o "asignar" el perfil a los dispositivos.

Como parte de la solución de administración de dispositivos móviles (MDM), use estos perfiles de configuración para completar distintas tareas. Estos son algunos ejemplos de perfiles:

- En dispositivos Windows 10, use una plantilla de perfil que bloquee los controles ActiveX en Internet Explorer.
- En dispositivos iOS/iPadOS y macOS, permita que los usuarios usen impresoras AirPrint en la organización.
- Permita o impida el acceso a Bluetooth en el dispositivo.
- Cree un perfil Wi-Fi o VPN que proporcione a distintos dispositivos acceso a su servidor VPN dentro de su red corporativa.
- Administre las actualizaciones de software, incluido el momento de la instalación.
- Ejecute un dispositivo Android como dispositivo de pantalla completa dedicado que pueda ejecutar una o varias aplicaciones.

En este artículo se proporciona información general de los distintos tipos de perfiles que puede crear. Use estos perfiles para habilitar o deshabilitar algunas características en los dispositivos.

## <a name="administrative-templates"></a>Plantillas administrativas

Las [plantillas administrativas](administrative-templates-windows.md) incluyen cientos de opciones que puede configurar para Internet Explorer, Microsoft Edge, OneDrive, Escritorio remoto, Word, Excel y otros programas de Office. Estas plantillas proporcionan a los administradores una vista simplificada de las configuraciones similares a una directiva de grupo, pero que están basadas por completo en la nube.

Esta característica es compatible con:

- Windows 10 y versiones posteriores

## <a name="certificates"></a>Certificados

Los [certificados](../protect/certificates-configure.md) configuran certificados PKCS, SCEP y de confianza que están asignados a los dispositivos. Estos certificados autentican perfiles de correo electrónico, VPN y Wi-Fi.

Esta característica es compatible con:

- Administrador de dispositivos Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1
- Windows 10 y versiones posteriores

## <a name="custom-profile"></a>Perfil personalizado

La [configuración personalizada](custom-settings-configure.md) permite que los administradores asignen la configuración del dispositivo que no está integrada en Intune. En dispositivos Android, puede escribir valores de OMA-URI. Para dispositivos iOS/iPadOS, puede importar un archivo de configuración creado en Apple Configurator.

Esta característica es compatible con:

- Administrador de dispositivos Android
- Android Enterprise
- iOS/iPadOS
- macOS

## <a name="delivery-optimization"></a>Optimización de entrega

[Optimización de distribución](delivery-optimization-windows.md) proporciona una mejor experiencia para distribuir las actualizaciones de software. Esta configuración reemplaza la configuración **Actualizaciones de software** > **Círculo de actualizaciones de Windows 10**.

Use estas opciones para controlar cómo se descargan las actualizaciones de software a los dispositivos de la organización. Por ejemplo, puede permitir que los usuarios obtengan sus propias actualizaciones u obtengan actualizaciones a través de los servicios en la nube de Optimización de distribución en un perfil de dispositivo.

Esta característica es compatible con:

- Windows 10 y versiones posteriores

## <a name="derived-credential"></a>Credencial derivada

Las [credenciales derivadas](../protect/derived-credentials.md) son certificados en tarjetas inteligentes que pueden autenticar, firmar y cifrar. En Intune, se pueden crear perfiles con estas credenciales para usarlas en aplicaciones, perfiles de correo electrónico y conexión a VPN, S/MIME y Wi-Fi.

Esta característica es compatible con:

- Android Enterprise
- iOS/iPadOS

## <a name="device-features"></a>Características del dispositivo

Las [características del dispositivo](device-features-configure.md) controlan las características de dispositivos iOS/iPadOS y macOS, como AirPrint, las notificaciones y los mensajes de la pantalla de bloqueo.

Esta característica es compatible con:

- iOS/iPadOS
- macOS

## <a name="device-firmware-configuration-interface"></a>Device firmware configuration interface (Interfaz de configuración de firmware de dispositivos)

[Device firmware configuration interface](device-firmware-configuration-interface-windows.md) (DFCI) permite a los administradores habilitar o deshabilitar valores de UEFI (BIOS) mediante Intune. Use estos valores para mejorar la seguridad en el nivel de firmware, que normalmente es más resistente a los ataques malintencionados.

Esta característica es compatible con:

- Windows 10 1809 y versiones posteriores en firmware compatible

## <a name="device-restrictions"></a>Restricciones de dispositivos

Las [restricciones de dispositivos](device-restrictions-configure.md) controlan la seguridad, el hardware, el uso compartido de datos y otras opciones de configuración de los dispositivos. Por ejemplo, cree un perfil de restricción de dispositivos que impida que los usuarios de dispositivos iOS/iPadOS utilicen la cámara del dispositivo. 

Esta característica es compatible con:

- Administrador de dispositivos Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 y versiones posteriores
- Windows 10 Team

## <a name="domain-join"></a>Unión a un dominio

[Unión a un dominio](domain-join-configure.md) configura la información de dominio de Active Directory local. Esta información se implementa en los dispositivos híbridos unidos a Azure AD cuando se aprovisiona con Windows Autopilot e Intune. Este perfil indica a los dispositivos el dominio y la unidad organizativa que se van a unir.

Esta característica es compatible con:

- Windows 10 y versiones posteriores

## <a name="edition-upgrade-and-mode-switch"></a>Actualización de edición y conmutador de modo

Las [actualizaciones de la edición de Windows 10](edition-upgrade-configure-windows-10.md) actualizan automáticamente dispositivos que ejecutan algunas versiones de Windows 10 a una edición más reciente.

Esta característica es compatible con:

- Windows 10 y versiones posteriores

## <a name="education"></a>Education

En [Configuración de los ajustes de educación de Windows 10 en Microsoft Intune](education-settings-configure.md) se configuran opciones para la [aplicación Take a Test de Windows](https://docs.microsoft.com/education/windows/take-tests-in-windows-10). Al configurar estas opciones, no puede ejecutar ninguna otra aplicación en el dispositivo hasta que se complete la prueba.

En [Configuración del entorno educativo: iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) se usa la aplicación Classroom de iOS/iPadOS para guiar el aprendizaje y controlar los dispositivos de los alumnos en el aula. Puede configurar dispositivos iPad para que muchos alumnos puedan compartir un solo dispositivo.

## <a name="email"></a>Correo electrónico

La [configuración de correo electrónico](email-settings-configure.md) crea, asigna y supervisa la configuración de correo electrónico de Exchange ActiveSync en los dispositivos. Los perfiles de correo electrónico ayudan en la coherencia, reducen las llamadas al soporte técnico y permiten a los usuarios finales acceder al correo electrónico de la empresa en sus dispositivos personales sin necesidad de ninguna configuración por su parte. 

Esta característica es compatible con:

- Administrador de dispositivos Android
- Android Enterprise
- iOS/iPadOS
- Windows 10 y versiones posteriores

## <a name="endpoint-protection"></a>Endpoint Protection

[Endpoint Protection](../protect/endpoint-protection-configure.md) configura los valores de BitLocker y Microsoft Defender para dispositivos Windows 10. Además, configura el firewall, la puerta de enlace y otros recursos en dispositivos macOS.

Para incorporar Advanced Threat Protection de Microsoft Defender (WDATP) a Microsoft Intune, consulte [Configuración de los puntos de conexión mediante las herramientas de Administración de dispositivos móviles (MDM)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

Esta característica es compatible con:

- macOS
- Windows 10 y versiones posteriores

## <a name="esim-cellular---public-preview"></a>Telefonía móvil eSIM: versión preliminar pública

Los [perfiles de telefonía móvil eSIM](esim-device-configuration.md) permiten que los administradores configuren planes de datos móviles en los dispositivos administrados para el acceso a Internet y datos. Tras obtener los códigos de activación del operador de telefonía móvil, use Intune para importarlos y, después, asignarlos a los dispositivos compatibles con eSIM.

Esta característica es compatible con:

- Windows 10 Fall Creators Update y versiones posteriores

## <a name="extensions"></a>Extensiones

[las extensiones del sistema macOS y las extensiones de kernel](kernel-extensions-overview-macos.md) permiten a los administradores agregar características o programas que amplían las funciones nativas del sistema operativo. Configure estas opciones para confiar en todas las extensiones de un desarrollador o partner específico o para permitir extensiones específicas.

Esta característica es compatible con:

- macOS

## <a name="identity-protection"></a>Protección de identidad

[Protección de identidad](../protect/identity-protection-configure.md) controla la experiencia de Windows Hello para empresas en dispositivos Windows 10. Configure estas opciones para que Windows Hello para empresas esté disponible para los usuarios y dispositivos, y para especificar los requisitos de PIN y gestos para los dispositivos.  

Esta característica es compatible con:  

- Windows 10 y versiones posteriores
- Windows Holographic for Business  

## <a name="kiosk"></a>Pantalla completa

En el perfil de [configuración de pantalla completa](kiosk-settings.md) se configura un dispositivo para ejecutar una aplicación o ejecutar varias aplicaciones. También puede personalizar otras características en el quiosco, como un menú de inicio y un explorador web.

Esta característica es compatible con:

- Windows 10 y versiones posteriores

La configuración de pantalla completa también está disponible como restricciones de dispositivos para [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience) e [iOS/iPadOS](device-restrictions-ios.md#kiosk).

## <a name="mx-profile-zebra"></a>Perfil de MX (Zebra)

Las [Extensiones de movilidad (MX)](android-zebra-mx-overview.md) expanden la configuración integrada de Intune para personalizar o agregar más opciones de configuración específicas de los dispositivos Zebra. Los dispositivos Zebra se suelen usar en fábricas y en entornos de venta al por menor. Si tiene cientos o miles de dispositivos Zebra, puede usar Intune para configurarlos y administrarlos.

Esta característica es compatible con:

- Administrador de dispositivos Android

## <a name="microsoft-defender-atp"></a>ATP de Microsoft Defender

[Advanced Threat Protection (ATP) de Microsoft Defender](../protect/advanced-threat-protection.md) se integra con Intune para supervisar y ayudar a proteger los dispositivos. Establezca los niveles de riesgo y determine qué sucede si los dispositivos superan ese nivel. Cuando se combina con el acceso condicional, se puede ayudar a evitar actividades malintencionadas en la organización.

Esta característica es compatible con:

- Windows 10 y versiones posteriores

## <a name="oemconfig"></a>OEMConfig

En los dispositivos Android Enterprise, [OEMConfig](android-oem-configuration-overview.md) es un estándar que permite que los OEM (fabricantes de equipos originales) y los EMM (administración de movilidad empresarial) compilen y admitan características específicas de OEM de manera estandarizada. Con OEMConfig, un OEM crea un esquema que define las características de administración específicas suyas y lo inserta en una aplicación cargada en Google Play. Intune lee el esquema de la aplicación y permite que los administradores de Intune configuren los valores en el esquema.

Esta característica es compatible con:

- Android Enterprise (OEMConfig)

## <a name="powershell-scripts"></a>Scripts de PowerShell

Los [scripts de PowerShell](../apps/intune-management-extension.md) usan la extensión de administración de Intune para cargar los scripts de PowerShell en Intune y, luego, los ejecutan en los dispositivos. Consulte también lo que se necesita para usar una extensión, cómo agregarla a Intune y otra información importante.

Esta característica es compatible con:

- Windows 10 y versiones posteriores
- Windows Holographic for Business

## <a name="preference-file"></a>Archivo de preferencia

Los [archivos de preferencia](preference-file-settings-macos.md) en dispositivos macOS incluyen información sobre las aplicaciones. Por ejemplo, se pueden usar los archivos de preferencia para controlar la configuración del explorador web, personalizar las aplicaciones y mucho más.

Esta característica es compatible con:

- macOS

## <a name="shared-multi-user-device"></a>Dispositivos multiusuario compartidos

En [Windows 10](shared-user-device-settings-windows.md) y [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) se incluyen opciones de configuración para administrar dispositivos con varios usuarios, que también se conocen como dispositivos o equipos compartidos. Cuando un usuario inicie sesión en el dispositivo, seleccione si quiere que este pueda cambiar las opciones de suspensión o guardar archivos en el dispositivo. En otro ejemplo, para ahorrar espacio, puede crear un perfil que elimine las credenciales inactivas de los dispositivos Windows HoloLens.

Estas opciones de configuración de los dispositivos multiusuario compartidos permiten a un administrador controlar algunas de las características del dispositivo y administrar dichos dispositivos compartidos mediante Intune.

Esta característica es compatible con:

- Windows 10 y versiones posteriores
- Windows Holographic for Business

## <a name="update-policies"></a>Directivas de actualización

En [Directivas de actualización de iOS/iPadOS](../protect/software-updates-ios.md) se muestra cómo crear y asignar directivas de iOS/iPadOS para instalar actualizaciones de software en los dispositivos iOS/iPadOS. También puede revisar el estado de la instalación.

Para actualizar las directivas en dispositivos con Windows, vea [Optimización de entrega](delivery-optimization-windows.md). 

Esta característica es compatible con:

- iOS/iPadOS

## <a name="vpn"></a>VPN

La [configuración de VPN](vpn-settings-configure.md) asigna perfiles de VPN a usuarios y dispositivos de la organización para que puedan conectarse a la red de forma fácil y segura. 

Las redes privadas virtuales (VPN) ofrecen a los usuarios un acceso remoto seguro a la red de la empresa. Dispositivos que usan un perfil de conexión VPN para iniciar una conexión con el servidor VPN. 

Esta característica es compatible con: 

- Administrador de dispositivos Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1
- Windows 10 y versiones posteriores

## <a name="wi-fi"></a>Wi-Fi

La [configuración de Wi-Fi](wi-fi-settings-configure.md) asigna valores de configuración de red inalámbrica a los usuarios y los dispositivos. Al asignar un perfil de Wi-Fi, los usuarios obtienen acceso a su red Wi-Fi corporativa sin tener que configurarla ellos mismos. 

Esta característica es compatible con:

- Administrador de dispositivos Android
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1 (solo importación)
- Windows 10 y versiones posteriores

## <a name="wired-networks"></a>Redes cableadas

Las [redes cableadas](wired-networks-configure.md) permiten crear y administrar conexiones cableadas de 802.1x para equipos de escritorio macOS. En el perfil, seleccione la interfaz de red, los tipos de EAP aceptados y escriba la configuración de confianza del servidor, incluidos los certificados PKCS y SCEP.

Al asignar el perfil, los usuarios de equipos de escritorio macOS obtienen acceso a la red cableada corporativa sin tener que configurarla ellos mismos.

Esta característica es compatible con:

- macOS

## <a name="zebra-mobility-extensions-mx"></a>Zebra Mobility Extensions (MX)

[Zebra Mobility Extensions (MX)](android-zebra-mx-overview.md) permite que los administradores usen y administren dispositivos Zebra en Intune. Puede crear perfiles de StageNow con la configuración y, luego, usar Intune para asignar e implementar estos perfiles a sus dispositivos Zebra. El artículo [Registros y problemas comunes de StageNow](android-zebra-mx-logs-troubleshoot.md) es un excelente recurso para solucionar problemas con los perfiles y ver algunos posibles problemas que surjan al usar StageNow.

Esta característica es compatible con:

- Administradores de dispositivos Android (Mobility Extensions)

## <a name="manage-and-troubleshoot"></a>Supervisión y solución de problemas

[Administre los perfiles](device-profile-monitor.md) para comprobar el estado de los dispositivos y los perfiles asignados. También ayudan a resolver conflictos mediante la visualización de la configuración que provoca un conflicto y los perfiles que incluyen esta configuración. El artículo [Problemas comunes y sus soluciones](device-profile-troubleshoot.md) ayuda a los administradores a trabajar con los perfiles. Describe lo que sucede cuando se elimina un perfil, lo que hace que se envíen notificaciones a los dispositivos y mucho más.

## <a name="next-steps"></a>Pasos siguientes

Elija la plataforma y empiece a trabajar.
