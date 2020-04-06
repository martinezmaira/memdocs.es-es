---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a807a90cdca18d79e7b92b4efeb56d341da2596
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438729"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>En desarrollo para Microsoft Intune: abril de 2020

Para ayudarle con la preparación y planeación, en esta página se enumeran las actualizaciones y características de la interfaz de usuario de Intune que están en desarrollo, pero que aún no se han publicado. Además de la información de esta página: 

- Si prevemos que tendrá que tomar medidas antes de realizar un cambio, haremos una publicación complementaria en el Centro de mensajes de Office.
- Cuando una característica entra en producción, ya sea una versión preliminar o disponible con carácter general, la descripción de la característica pasa de esta página a [Novedades](whats-new.md).
- Esta página y la página [Novedades](whats-new.md) se actualizan periódicamente. Compruebe si hay actualizaciones adicionales.
- Consulte el [plan de desarrollo de Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) para conocer los plazos de tiempo y los productos estratégicos.

> [!NOTE]
> Esta página refleja las expectativas actuales sobre las capacidades de Intune en una versión futura. Las fechas y las características individuales pueden cambiar. En esta página no se describen todas las características en desarrollo.

**Fuente RSS**: para recibir notificaciones cuando esta página se actualice, copie y pegue la dirección URL siguiente en el lector de fuentes: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Administración de aplicaciones

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Actualización para las directivas de configuración de aplicaciones de Android<!-- 6113334  -->
Las directivas de configuración de aplicaciones de Android se actualizarán para permitir que los administradores seleccionen el tipo de inscripción del dispositivo antes de crear un perfil de configuración de aplicación. La funcionalidad se agregará para tener en cuenta los perfiles de certificado que se basan en el tipo de inscripción (perfil de trabajo o propietario del dispositivo).  Después de su lanzamiento, sucederá lo siguiente:

- Las directivas existentes creadas antes del lanzamiento de esta característica que no tengan ningún perfil de certificado asociado usarán de forma predeterminada el perfil de trabajo y el perfil de propietario del dispositivo para el tipo de inscripción de dispositivos.
- Las directivas existentes creadas antes del lanzamiento de esta característica que tengan perfiles de certificado asociados usarán de forma predeterminada únicamente el perfil de trabajo.
- Si se crea un perfil y se han seleccionado los perfiles de trabajo y de propietario del dispositivo para el tipo de inscripción del dispositivo, no podrá asociar un perfil de certificado a la directiva de configuración de la aplicación.
- Si se crea un perfil y solo se selecciona el perfil de trabajo, se podrán usar las directivas de certificado del perfil de trabajo creadas en la configuración del dispositivo.
- Si se crea un perfil y solo se selecciona el perfil de propietario del dispositivo, se podrán usar las directivas de certificado del propietario del dispositivo creadas en la configuración del dispositivo.

Las directivas existentes no corregirán ni emitirán nuevos certificados.

Además, agregaremos perfiles de configuración de correo electrónico de Gmail y Nine que funcionarán con los tipos de inscripción de perfil de trabajo y de propietario del dispositivo, e incluirán el uso de perfiles de certificado en ambos tipos de configuración de correo electrónico.  Todas las directivas de Gmail o Nine que haya creado en la configuración del dispositivo para perfiles de trabajo seguirán aplicándose al dispositivo, sin necesidad de trasladarlas a las directivas de configuración de aplicaciones.

En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), puede buscar directivas de configuración de aplicaciones. Para ello, seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones**. Para obtener más información sobre las directivas de configuración de aplicaciones, consulte [Directivas de configuración de aplicaciones para Microsoft Intune](../apps/app-configuration-policies-overview.md).

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams ahora se incluye en el conjunto de aplicaciones Office 365 para macOS<!-- 5903936  -->
Los usuarios a los que se les asigne Microsoft Office para macOS en Microsoft Endpoint Manager ahora recibirán Microsoft Teams, además de las aplicaciones de Microsoft Office existentes (Word, Excel, PowerPoint, Outlook y OneNote). Intune reconocerá los dispositivos Mac existentes que tengan instaladas las demás aplicaciones de Office para macOS e intentará instalar Microsoft Teams la próxima vez que el dispositivo se registre con Intune. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), encontrará el **conjunto de aplicaciones de Office 365** para macOS. Para ello, seleccione **Aplicaciones** > **macOS** > **Agregar**. Para obtener más información, vea [Asignación de Office 365 a dispositivos macOS con Microsoft Intune](../apps/apps-add-office365-macos.md).

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>Compatibilidad del panel de personalización con destinatarios de grupo <!-- 4722837  -->
Podrá establecer el destino de la configuración del panel de personalización en grupos de usuarios. En el portal de Intune, seleccione **Aplicaciones cliente** > **Personalización**. Para obtener más información, consulte [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](company-portal-app.md].

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuración del dispositivo

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Perfiles de configuración de dispositivos de red cableada para dispositivos macOS<!-- 3508686  -->
Se va a publicar un nuevo perfil de configuración de dispositivo macOS que configura redes cableadas (**Configuración del dispositivo** > **Perfiles** > **Crear perfil** > **macOS** para plataforma > **Red cableada** para tipo de perfil). Use esta característica para crear perfiles de 802.1x con el fin de administrar redes cableadas e implementarlas en los dispositivos macOS.

Se aplica a:
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>Experiencia de interfaz de usuario mejorada al crear perfiles de configuración en dispositivos iOS/iPadOS y macOS<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
Cuando se crea un perfil para dispositivos iOS/iPadOS o macOS, se actualiza la experiencia en el Centro de administración de Endpoint Manager. Este cambio afecta a los siguientes perfiles de configuración de dispositivos (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS** o **macOS** para plataforma):

- Personalizado: iOS/iPadOS y macOS
- Características del dispositivo: iOS/iPadOS y macOS
- Restricciones de dispositivos: iOS/iPadOS y macOS
- Endpoint Protection: macOS
- Extensiones: macOS
- Archivo de preferencias: macOS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Las opciones y valores de los perfiles de configuración de dispositivos se actualizarán para las plataformas Windows<!-- 4091122 -->
Al crear perfiles de configuración de dispositivos para plataformas Windows (**Dispositivos** > **Perfiles de configuración** >  **Crear perfil** > cualquier opción **Windows** para la plataforma), algunas opciones y sus valores son diferentes del CSP y pueden ser confusos. Los nombres de las opciones y sus valores se actualizarán para que sean más claros.

Se aplica a:

- Perfiles de configuración de dispositivos Windows 10 y versiones posteriores
- Perfiles de configuración de dispositivos Windows Holographic for Business
- Perfiles de configuración de dispositivos Windows 8.1
- Perfiles de configuración de dispositivos Windows Phone 8.1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Configuración de la aplicación ATP de Microsoft Defender para macOS  <!-- 5520115  -->
Pronto podrá configurar las [opciones](../protect/endpoint-protection-macos.md) para la aplicación ATP de Microsoft Defender para dispositivos que ejecuten macOS como parte de un perfil de configuración de dispositivo de protección de puntos de conexión (**Dispositivos** > **Perfiles de configuración** > **Crear perfil**, seleccione **macOS** para *Plataforma* y, después, **Endpoint Protection** para el *Tipo de perfil*). Habrá ocho opciones para la configuración de dispositivos macOS. 

ATP de Microsoft Defender es compatible con macOS 10.13 (High Sierra) y versiones posteriores, y la aplicación [ATP de Microsoft Defender](../apps/apps-advanced-threat-protection-macos.md) se debe implementar en el dispositivo *después* de aplicar esta configuración. Las opciones se deben enviar al dispositivo antes de que se implemente la aplicación. No se admiten las versiones beta de macOS.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nueva configuración de FileVault para la directiva de configuración de dispositivos Endpoint Protection de macOS<!-- 5459801   -->
Se va a agregar una opción nueva a la categoría FileVault dentro de la plantilla [Endpoint Protection de macOS](../protect/endpoint-protection-macos.md): Ocultar clave de recuperación. (**Dispositivos** > **Perfiles de configuración** > **Crear perfil**, seleccione **macOS** para la *Plataforma* y, después, **Endpoint Protection** para el *Tipo de perfil*). Esta opción oculta la clave personal del usuario final durante el cifrado de FileVault 2. Un usuario del dispositivo puede ver su clave de recuperación personal en cualquier momento desde la aplicación Portal de empresa de iOS o desde el sitio web del Portal de empresa para el dispositivo macOS cifrado. Para ver la clave de recuperación personal, puede ir a los detalles del dispositivo y hacer clic en *Obtener clave de recuperación*.

Esta opción no estará disponible en una directiva creada anteriormente. Tendrá que volver a crear las directivas de FileVault para configurar esta opción y poder usarla. 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Envío de notificaciones de inserción como acción de no cumplimiento <!-- 1733150   -->
En el caso de las plataformas iOS y Android, agregaremos una nueva acción de no cumplimiento que enviará una notificación de inserción de aplicación a través de la aplicación Portal de empresa. Los usuarios pueden hacer clic en las notificaciones, que iniciarán la aplicación Portal de empresa, donde se mostrará el motivo al que se debe el estado de no cumplimiento. Los administradores podrán configurar esta nueva acción de no cumplimiento en el Centro de administración de Microsoft Endpoint Manager. Para ello, hay que ir a **Dispositivos** > **Directivas de cumplimiento** > **Crear directiva** y seleccionar la *Acción* para enviar una notificación de inserción de aplicación.

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Pruebas de versión preliminar para aplicaciones de Google Play administrado<!-- 2681933  -->
Las organizaciones que usan [canales de prueba cerrados de Google Play para las pruebas de versión preliminar de las aplicaciones](https://support.google.com/googleplay/android-developer/answer/3131213) podrán administrar dichos canales con Intune. Podrá asignar de forma selectiva las aplicaciones de línea de negocio publicadas en canales de preproducción de Google Play a grupos piloto para realizar las pruebas. En Intune, también podrá ver si una aplicación tiene publicada en ella un canal de compilación de prueba de preproducción, así como asignar ese canal a grupos de dispositivos o usuarios de AAD. Esta característica está disponible para todos los escenarios de Android Enterprise que se admiten actualmente (perfil de trabajo, totalmente administrado y dedicado). En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), puede agregar una aplicación administrada de Google Play. Para ello, seleccione **Aplicaciones** > **Android** > **Agregar**. Para obtener más información, consulte [Incorporación de aplicaciones de Google Play administrado a dispositivos Android Enterprise con Intune](../apps/apps-add-android-for-work.md).

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>Administración de la configuración de S/MIME para Outlook en Android<!-- 6517085   -->
Podrá usar las directivas de configuración de aplicaciones para administrar la configuración de S/MIME para Outlook en los dispositivos que ejecutan Android Enterprise. También podrá elegir si quiere permitir que los usuarios del dispositivo habiliten o deshabiliten S/MIME en la configuración de Outlook. Si quiere usar la directiva de configuración de aplicaciones para Android, en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), vaya a **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** > **Dispositivos administrados**.

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>Opciones adicionales en los perfiles de SSO y de extensión de la aplicación de SSO en dispositivos iOS/iPadOS<!-- 6504155  -->
En dispositivos iOS/iPadOS, puede hacer lo siguiente:

- En los perfiles de SSO (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para la plataforma > **Características de los dispositivos** para el perfil > **Inicio de sesión único**), establezca el nombre de la entidad de seguridad de Kerberos en el nombre de cuenta del administrador de cuentas de seguridad (SAM) en perfiles de SSO. 
- En los perfiles de extensión de la aplicación de SSO (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para la plataforma > **Características del dispositivo** para el perfil > **Extensión de aplicación de inicio de sesión único**) puede configurar la extensión de Microsoft Azure AD de iOS/iPadOS con menos clics si usa un nuevo tipo de extensión de la aplicación de SSO. Puede habilitar la extensión de Azure AD para dispositivos compartidos y enviarle a la extensión datos específicos de esta.

Se aplica a:
- iOS/iPadOS 13.0 y versiones posteriores

Para obtener más información sobre el uso del inicio de sesión único en dispositivos iOS/iPadOS, consulte la introducción a la [extensión de aplicación de inicio de sesión único](../configuration/device-features-configure.md#single-sign-on-app-extension) y la [lista de opciones de inicio de sesión único](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscripción de dispositivos

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Los dispositivos de tipo Bring Your Own Device pueden usar la VPN para la implementación<!--5015344 -->
El nuevo botón de alternancia **Omitir comprobación de conectividad del dominio** del perfil de Autopilot le permite implementar dispositivos de Unión a Azure AD híbrido sin acceso a la red corporativa mediante su propio cliente VPN Win32 de terceros. Para ver el nuevo botón de alternancia, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos**  > **Windows** > **Inscripción de Windows** > **Perfiles de implementación** > **Crear perfil** > **Configuración rápida (OOBE)** .

<!-- ***********************************************-->
## <a name="device-management"></a>Administración de dispositivos

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Compatibilidad de scripts de PowerShell con dispositivos BYOD<!-- 1862833  -->
Los scripts de PowerShell admitirán dispositivos registrados de Azure AD en Intune. Para más información sobre PowerShell, vea [Uso de scripts de PowerShell para dispositivos Windows 10 en Intune](../apps/intune-management-extension.md). Esta funcionalidad no es compatible con dispositivos que ejecutan Windows 10 Home Edition.

### <a name="script-support-for-macos-devices---4280361----"></a>Compatibilidad con scripts para dispositivos macOS<!-- 4280361  -->
Podrá agregar e implementar scripts en dispositivos macOS. Esta compatibilidad amplía la capacidad de configurar dispositivos macOS más allá de lo que es posible con las funcionalidades de MDM nativas en dispositivos macOS.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics incluirá registros de detalles del dispositivo<!--6014987  -->
Habrá disponibles registros detallados del dispositivo de Intune en **Informes** > **Log Analytics**. Puede correlacionar los detalles del dispositivo para compilar consultas personalizadas y libros de Azure.

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>Notificaciones de inserción al cambiar el tipo de propiedad del dispositivo<!-- 5575875  -->
Podrá configurar una notificación de inserción para enviársela a los usuarios del Portal de empresa de Android e iOS cuando el tipo de propiedad del dispositivo cambie de personal a corporativo como gesto de cortesía en respeto de su privacidad. Para encontrar esta opción en Microsoft Endpoint Manager, seleccione **Administración de inquilinos** > **Personalización**. Para obtener más información sobre cómo afecta la propiedad del dispositivo a los usuarios finales, vea [Cambiar la propiedad del dispositivo](../enrollment/corporate-identifiers-add.md#change-device-ownership).

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Seguridad

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Compatibilidad con credenciales derivadas en dispositivos Android totalmente administrados<!--4839592-->
Se van a poder usar credenciales derivadas en dispositivos Android Enterprise totalmente administrados. Se va a incluir compatibilidad para recuperar una credencial derivada de Entrust Datacard, Intercede y DISA Purebred. Se va a poder usar una credencial derivada para la autenticación de aplicaciones, Wi-Fi, VPN o la firma o el cifrado S/MIME en las aplicaciones que lo admitan.

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Configuración de preferencias de privacidad para dispositivos macOS<!-- 2934232 --> 
Con el lanzamiento de macOS Catalina 10.15, Apple ha agregado nuevas mejoras de seguridad y privacidad. De forma predeterminada, las aplicaciones y los procesos no pueden acceder a datos específicos sin el consentimiento del usuario. Si los usuarios no proporcionan su consentimiento, es posible que las aplicaciones y los procesos no funcionen. Intune va a agregar compatibilidad con opciones que permiten a los administradores de TI permitir o impedir el consentimiento del acceso a datos en nombre de los usuarios finales en dispositivos que ejecuten macOS 10.14 y versiones posteriores. Estas opciones garantizarán que las aplicaciones y los procesos sigan funcionando correctamente y reducirán el número de mensajes que experimentan los usuarios finales.

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Texto y etiquetas actualizados de la interfaz de usuario para la configuración del perfil de Endpoint Protection de Windows 10<!-- 5983747 -->
Se va a actualizar el texto de varias opciones que se configuran como perfiles de configuración de dispositivos Windows 10 para facilitar la comprensión del uso y los resultados previstos de las opciones.

Las opciones que se van a actualizar incluyen perfiles de configuración de dispositivos Windows 10 para:

- [Restricciones de dispositivos](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Antivirus de Microsoft Defender  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Antivirus de Microsoft Defender

Las opciones que se admiten con Intune no se van a cambiar. Esta actualización es solo para el texto de la interfaz de usuario del Centro de administración del Administrador de puntos de conexión de Microsoft.

<!-- ***********************************************-->
## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vea también

Consulte [Novedades de Microsoft Intune](whats-new.md) para obtener más información sobre los desarrollos recientes.



