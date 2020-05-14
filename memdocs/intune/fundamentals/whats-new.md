---
title: Novedades de Microsoft Intune (Azure) | Microsoft Docs
titleSuffix: ''
description: Descubra las novedades del portal de Intune Azure
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/04/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b3c8287d9b5ca2d46094d04ee2179128bead4a8
ms.sourcegitcommit: 0dafd513a59afe592b5cfe2a80b6288020dc5bf0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2020
ms.locfileid: "82991738"
---
# <a name="whats-new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Obtenga información sobre las novedades que se producen cada semana en Microsoft Intune en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). También puede encontrar [notificaciones importantes](#notices), [versiones anteriores](whats-new-archive.md) e información sobre [cómo se publican las actualizaciones del servicio de Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> El lanzamiento de cada [actualización mensual](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) puede tardar hasta tres días y se realizará en el orden siguiente:
>
> - Día 1: Asia Pacífico (APAC)
> - Día 2: Europa, Oriente Medio y África (EMEA)
> - Día 3: América del Norte
> - Día 4+: Intune for Government
>
> Es posible que algunas características se implementen durante varias semanas y que no estén disponibles para todos los clientes la primera semana.
>
> Revise la [página En desarrollo](in-development.md) para ver una lista de las características que aparecerán en una versión próxima.

**Fuente RSS**: reciba notificaciones cuando esta página se actualice copiando y pegando la siguiente dirección URL en su lector de fuentes: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot

<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Semana del 4 de mayo de 2020  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Portal de empresa para Android guía a los usuarios para obtener aplicaciones después de la inscripción del perfil de trabajo <!-- 6103999 -->
Hemos mejorado las instrucciones en la aplicación del Portal de empresa para facilitar a los usuarios la búsqueda e instalación de aplicaciones. Después de la inscripción en la administración del perfil de trabajo, los usuarios recibirán un mensaje que explica cómo encontrar aplicaciones sugeridas en la versión con distintivo de Google Play. El último paso de [Inscribir dispositivos con perfil Android](../user-help/enroll-device-android-work-profile.md) se ha actualizado para mostrar el mensaje nuevo. Los usuarios también verán un nuevo vínculo **Obtener aplicaciones** en el cajón de Portal de empresa de la izquierda. Para dejar espacio a estas experiencias nuevas y mejoradas, se quitó la pestaña **APLICACIONES**. Para ver las pantallas actualizadas, vaya a [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Semana del 20 de abril de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### <a name="device-management"></a>Administración de dispositivos

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758-idready---"></a>Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo<!-- 6317104, CM3555758 idready -->
Microsoft Endpoint Manager reúne Configuration Manager e Intune en una misma consola. A partir de la versión 2002 de Configuration Manager, puede cargar los dispositivos de Configuration Manager en el servicio en la nube y realizar acciones en ellos en el centro de administración. Para obtener más información, vea [Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo](../../configmgr/tenant-attach/device-sync-actions.md). 

### <a name="app-management"></a>Administración de aplicaciones

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Cambio del nombre de Microsoft Office 365 ProPlus<!-- 6368143 -->
El nombre de Microsoft Office 365 ProPlus se va a cambiar por **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). En nuestra documentación, normalmente se hace referencia a este producto como Aplicaciones de Microsoft 365. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), puede encontrar el conjunto de aplicaciones si selecciona **Aplicaciones** > **Windows** > **Agregar**. Para obtener más información sobre cómo agregar aplicaciones, vea [Incorporación de aplicaciones a Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>Semana del 13 de marzo de 2020 (versión del servicio 2004)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Administración de la configuración de S/MIME para Outlook en dispositivos Android Enterprise<!-- 6517085   -->
Podrá usar las directivas de configuración de aplicaciones para administrar la configuración de S/MIME para Outlook en los dispositivos que ejecutan Android Enterprise. También puede elegir si quiere permitir que los usuarios del dispositivo habiliten o deshabiliten S/MIME en la configuración de Outlook. Si quiere usar las directivas de configuración de aplicaciones para Android, en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), vaya a **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** > **Dispositivos administrados**. Para obtener más información sobre la configuración de Outlook, vea [Opciones de configuración de Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Pruebas de versión preliminar para aplicaciones de Google Play administrado<!-- 2681933  -->
Las organizaciones que usan [canales de pruebas cerradas de Google Play para las pruebas de versión preliminar de las aplicaciones](https://support.google.com/googleplay/android-developer/answer/3131213) pueden administrar dichos canales con Intune. Puede asignar de forma selectiva las aplicaciones de línea de negocio publicadas en canales de preproducción de Google Play a grupos piloto para realizar las pruebas. En Intune, también puede ver si una aplicación tiene publicado un canal de compilación de pruebas de preproducción, así como asignar ese canal a grupos de dispositivos o de usuarios de AAD. Esta característica está disponible para todos los escenarios de Android Enterprise que se admiten actualmente (perfil de trabajo, totalmente administrado y dedicado). En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), puede agregar una aplicación administrada de Google Play. Para ello, seleccione **Aplicaciones** > **Android** > **Agregar**. Para obtener más información, vea [Uso de canales de pruebas cerradas de Google Play administrado](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams ahora se incluye en el conjunto de aplicaciones Office 365 para macOS<!-- 5903936  -->
Los usuarios a los que se les asigne Microsoft Office para macOS en Microsoft Endpoint Manager ahora recibirán Microsoft Teams, además de las aplicaciones de Microsoft Office existentes (Word, Excel, PowerPoint, Outlook y OneNote). Intune reconocerá los dispositivos Mac existentes que tengan instaladas las demás aplicaciones de Office para macOS e intentará instalar Microsoft Teams la próxima vez que el dispositivo se registre con Intune. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), encontrará el **conjunto de aplicaciones de Office 365** para macOS. Para ello, seleccione **Aplicaciones** > **macOS** > **Agregar**. Para obtener más información, vea [Asignación de Office 365 a dispositivos macOS con Microsoft Intune](../apps/apps-add-office365-macos.md).

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Actualización para las directivas de configuración de aplicaciones de Android<!-- 6113334  -->
Las directivas de configuración de aplicaciones de Android se han actualizado para permitir que los administradores seleccionen el tipo de inscripción del dispositivo antes de crear un perfil de configuración de aplicación. La funcionalidad se agregará para tener en cuenta los perfiles de certificado que se basan en el tipo de inscripción (perfil de trabajo o propietario del dispositivo).  En esta actualización se ofrece lo siguiente:

1. Si se crea un perfil y se han seleccionado los perfiles de trabajo y de propietario del dispositivo para el tipo de inscripción del dispositivo, no podrá asociar un perfil de certificado a la directiva de configuración de la aplicación.
2. Si se crea un perfil y solo se selecciona el perfil de trabajo, se podrán usar las directivas de certificado del perfil de trabajo creadas en la configuración del dispositivo.
3. Si se crea un perfil y solo se selecciona el perfil de propietario del dispositivo, se podrán usar las directivas de certificado del propietario del dispositivo creadas en la configuración del dispositivo. 

> [!IMPORTANT]
> Las directivas existentes creadas antes del lanzamiento de esta característica (versión de abril de 2020: 2004) que no tengan ningún perfil de certificado asociado usarán de forma predeterminada los perfiles de trabajo y de propietario del dispositivo para el tipo de inscripción del dispositivo. Además, las directivas existentes creadas antes del lanzamiento de esta característica que tengan perfiles de certificado asociados usarán de forma predeterminada únicamente el perfil de trabajo.

Además, agregamos perfiles de configuración de correo electrónico de Gmail y Nine que funcionarán con los tipos de inscripción de perfil de trabajo y de propietario del dispositivo, e incluirán el uso de perfiles de certificado en ambos tipos de configuración de correo electrónico.  Todas las directivas de Gmail o Nine que haya creado en la configuración del dispositivo para perfiles de trabajo seguirán aplicándose al dispositivo, sin necesidad de trasladarlas a las directivas de configuración de aplicaciones.

En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), puede buscar directivas de configuración de aplicaciones. Para ello, seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones**. Para obtener más información sobre las directivas de configuración de aplicaciones, consulte [Directivas de configuración de aplicaciones para Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Notificaciones de inserción al cambiar el tipo de propiedad del dispositivo<!-- 5575875 -->
Se puede configurar una notificación de inserción para enviársela a los usuarios del Portal de empresa de Android y de iOS como gesto de cortesía hacia su privacidad cuando el tipo de propiedad del dispositivo cambie de Personal a Corporativo. Esta notificación de inserción se establece como desactivada de forma predeterminada. Para encontrar esta opción en Microsoft Endpoint Manager, seleccione **Administración de inquilinos** > **Personalización**. Para obtener más información sobre cómo afecta la propiedad del dispositivo a los usuarios finales, vea [Cambiar la propiedad del dispositivo](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Compatibilidad del panel de personalización con destinatarios de grupo<!-- 4722837  -->
Puede establecer el destino de la configuración en el panel **Personalización** en grupos de usuarios. Para encontrar estas opciones en Intune, vaya al [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431) y seleccione **Administración de inquilinos** > **Personalización**. Para obtener más información sobre la personalización, vea [Personalización de las aplicaciones del Portal de empresa de Intune, sitio web del Portal de empresa y aplicación de Intune](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>Se admiten varias reglas de VPN a petición "Evaluar cada intento de conexión" en iOS, iPadOS y macOS<!-- 6424615  -->
La experiencia del usuario de Intune permite agregar varias reglas de VPN a petición en el mismo perfil de VPN con la acción **Evaluar cada intento de conexión** (**Dispositivos** > **Perfiles de configuración** > **Crear perfiles** > **iOS/iPadOS** o **macOS** > para la plataforma > **VPN** para el perfil > **VPN automática** > **A petición**).

Solo se respetaba la primera regla de la lista. Este comportamiento se ha corregido e Intune evalúa todas las reglas de la lista. Cada regla se evalúa en el orden en que aparece en la lista de reglas a petición.

> [!NOTE]
> Si tiene perfiles de VPN existentes que usan estas reglas de VPN a petición, la corrección se aplica la próxima vez que cambie el perfil de VPN. Por ejemplo, realice un cambio menor, como cambiar el nombre de la conexión, y guarde el perfil.
>
> Si usa certificados SCEP para la autenticación, este cambio hace que se vuelvan a emitir los certificados para este perfil de VPN.

Se aplica a:
- iOS/iPadOS
- macOS

Para obtener más información sobre los perfiles de VPN, vea [Crear perfiles de VPN](../configuration/vpn-settings-configure.md).

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>Opciones adicionales en los perfiles de SSO y de extensión de la aplicación de SSO en dispositivos iOS/iPadOS<!-- 6504155   -->

En dispositivos iOS/iPadOS, puede hacer lo siguiente:
- En los perfiles de SSO (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para la plataforma > **Características de los dispositivos** para el perfil > **Inicio de sesión único**), establezca el nombre de la entidad de seguridad de Kerberos en el nombre de cuenta del administrador de cuentas de seguridad (SAM) en perfiles de SSO. 
- En los perfiles de extensión de la aplicación de SSO (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para la plataforma > **Características del dispositivo** para el perfil > **Extensión de aplicación de inicio de sesión único**) puede configurar la extensión de Microsoft Azure AD de iOS/iPadOS con menos clics si usa un nuevo tipo de extensión de la aplicación de SSO. Puede habilitar la extensión de Azure AD para dispositivos en modo de dispositivo compartido y enviarle a la extensión datos específicos de esta.

Se aplica a:
- iOS/iPadOS 13.0 y versiones posteriores

Para obtener más información sobre el uso del inicio de sesión único en dispositivos iOS/iPadOS, consulte la introducción a la [extensión de aplicación de inicio de sesión único](../configuration/device-features-configure.md#single-sign-on-app-extension) y la [lista de opciones de inicio de sesión único](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscripción de dispositivos

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Eliminación del token de inscripción de dispositivos automatizada de Apple cuando el perfil predeterminado está presente<!--6393220 -->
Anteriormente, no se podía eliminar un perfil predeterminado, lo que implicaba que no se podía eliminar el token de inscripción de dispositivos automatizada asociado. Ahora, puede eliminar el token cuando:
- No haya dispositivos asignados al token
- Haya un perfil predeterminado presente. Para ello, elimine el perfil predeterminado y, luego, el token asociado.
Para obtener más información, vea el artículo sobre [eliminación de un token de ADE de Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-ade-token-from-intune).

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Compatibilidad ampliada con dispositivos de Inscripción de dispositivos automatizada de Apple y Apple Configurator 2, perfiles y tokens<!--3542402 -->
Para ayudar a las organizaciones y los departamentos de TI distribuida, Intune admite ahora hasta 1000 perfiles de inscripción por token, 2000 tokens de inscripción de dispositivos automatizada (anteriormente conocida como DEP) por cuenta de Intune y 75 000 dispositivos por token. No hay ningún límite específico para dispositivos por perfil de inscripción más allá del número máximo de dispositivos por token.

Intune ahora admite hasta 1000 perfiles de Apple Configurator 2.

Para obtener más información, vea [Volumen admitido](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Cambios en la entrada de columna de la página Todos los dispositivos<!--6967616 -->
En la página **Todos los dispositivos**, las entradas de la columna **Administrado por** han cambiado:
- Ahora se muestra *Intune* en lugar de *MDM*
- Ahora se muestra *Con administración conjunta* en lugar de *Agente de MDM/ConfigMgr*

Los valores de exportación no han cambiado.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>Información de versión de Trusted Platform Manager (TPM) ahora en la página Hardware de dispositivo<!--6224914 idmiss -->
Ahora puede ver el número de versión de TPM en la página de hardware de un dispositivo ([Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > elegir un dispositivo > **Hardware** > buscar en **Revestimiento de hardware del sistema**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>Recopilación de registros para mejorar la solución de problemas de scripts asignados a dispositivos macOS<!-- 6359853  -->
Ahora puede recopilar registros para una mejor solución de problemas de scripts asignados a dispositivos macOS. Puede recopilar registros de hasta 60 MB (comprimidos) o 25 archivos, lo que ocurra primero. Para obtener más información, vea [Solución de problemas de directivas de script del shell en macOS mediante la recopilación de registros](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Seguridad

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Credenciales derivadas para aprovisionar dispositivos Android Enterprise totalmente administrados con certificados<!--4839592    -->
Intune ahora admite el uso de [credenciales derivadas](../protect/derived-credentials.md) como método de autenticación para dispositivos Android. Las credenciales derivadas son una implementación de la norma 800-157 del National Institute of Standards and Technology (NIST) relativa a la implementación de certificados en dispositivos. Nuestra compatibilidad con Android amplía nuestra compatibilidad con dispositivos que ejecutan iOS/iPadOS.

Las credenciales derivadas se basan en el uso de una tarjeta de verificación de identidad personal (PIV) o una tarjeta de acceso común (CAC), como una tarjeta inteligente. Para obtener una credencial derivada para un dispositivo móvil, los usuarios comienzan en la aplicación Microsoft Intune y siguen un flujo de trabajo de inscripción que es único para el proveedor que usen. Un requisito común a todos los proveedores es usar una tarjeta inteligente en un equipo para autenticarse en el proveedor de las credenciales derivadas. Tras ello, dicho proveedor emite un certificado para el dispositivo que viene derivado de la tarjeta inteligente del usuario.

Las credenciales derivadas se usan como método de autenticación de los perfiles de configuración de dispositivos de VPN y Wi-Fi. También se pueden usar para la autenticación de aplicaciones y el cifrado y la firma S/MIME de las aplicaciones que lo admiten.

Intune admite ahora los siguientes proveedores de credenciales derivadas con Android:
- Entrust Datacard
- Intercede

Un tercer proveedor, DISA Purebred, estará disponible para Android en una versión futura.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Línea de base de seguridad de Microsoft Edge ya está disponible con carácter general<!--6586139 -->

*Esta nueva línea de base se va a implementar en los inquilinos durante las próximas semanas. Esperamos que todos los inquilinos tengan esta nueva línea de base a principios de mayo.*

Ya está disponible una nueva versión de la característica [Línea de base de seguridad de Microsoft Edge](../protect/security-baselines.md#available-security-baselines) y se publica como disponible con carácter general (GA). La línea de base de Edge anterior estaba en versión preliminar.  La nueva versión de línea de base corresponde a abril de 2020 (Edge versión 80 y posteriores). 

Con el lanzamiento de esta nueva línea de base, ya no podrá crear perfiles basados en las versiones de línea de base anteriores, pero puede seguir usando los perfiles que haya creado con esas versiones. También puede optar por [actualizar los perfiles existentes para usar la versión de línea de base más reciente](../protect/security-baselines.md#change-the-baseline-version-for-a-profile). 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>Semana del 6 de abril de 2020

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>Nueva configuración de script de shell para dispositivos macOS<!-- 6884363 -->
Al configurar scripts de shell para dispositivos macOS, ahora puede configurar las siguientes opciones nuevas: 
- Ocultar las notificaciones de scripts en los dispositivos
- Frecuencia del script
- Número máximo de reintentos en caso de error del script

Para obtener más información, vea [Uso de scripts de shell para dispositivos macOS en Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Semana del 30 de marzo de 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Dirección URL nueva para el Centro de administración de Microsoft Endpoint Manager<!-- 3704810 -->
En consonancia con el anuncio del año pasado relativo a Microsoft Endpoint Manager en Ignite, hemos cambiado la dirección URL del Centro de administración de Microsoft Endpoint Manager (anteriormente Administración de dispositivos de Microsoft 365) a [https://endpoint.microsoft.com](https://endpoint.microsoft.com). La dirección URL del centro de administración anterior ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) continuará funcionando, pero se recomienda empezar a acceder al Centro de administración de Microsoft Endpoint Manager con la dirección URL nueva.

Para obtener más información, vea [Simplificación de las tareas de TI mediante el Centro de administración de Microsoft Endpoint Manager](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### <a name="app-management"></a>Administración de aplicaciones  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>Modo horizontal admitido en Portal de empresa para iOS<!--6048329  -->   
Los usuarios ahora pueden inscribir sus dispositivos, buscar aplicaciones y obtener soporte técnico de TI con la orientación de pantalla que prefieran. La aplicación detectará y ajustará automáticamente las pantallas para ajustarse al modo horizontal o vertical, a menos que los usuarios bloqueen la pantalla en modo vertical.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>Compatibilidad con scripts para dispositivos macOS (Versión preliminar pública)<!-- 4280361  -->
Se podrán agregar e implementar scripts en dispositivos macOS. Esta compatibilidad amplía la capacidad de configurar dispositivos macOS más allá de lo que es posible con las funcionalidades de MDM nativas en dispositivos macOS. Para obtener más información, vea [Uso de scripts de shell para dispositivos macOS en Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>Semana del 24 de marzo de 2020

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Experiencia de interfaz de usuario mejorada al crear perfiles de restricciones de dispositivo en dispositivos Android y Android Enterprise<!-- 5841361 -->
Al crear un perfil para dispositivos Android o Android Enterprise, se actualizará la experiencia en el Centro de administración de Microsoft Endpoint Manager. Este cambio afecta a los perfiles de configuración de dispositivo siguientes (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Administrador de dispositivos Android** o **Android Enterprise** para la plataforma):

- Restricciones de dispositivos: Administrador de dispositivos Android
- Restricciones de dispositivos: Propietario del dispositivo Android Enterprise
- Restricciones de dispositivos: Perfil de trabajo de Android Enterprise

Para obtener más información sobre las restricciones de dispositivos que se pueden configurar, vea [Administrador de dispositivos Android](../configuration/device-restrictions-android.md) y [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>Experiencia de interfaz de usuario mejorada al crear perfiles de configuración en dispositivos iOS/iPadOS y macOS<!-- 5569002 5568997 -->
Al crear un perfil para dispositivos iOS o macOS, se actualizará la experiencia en el Centro de administración de Microsoft Endpoint Manager. Este cambio afecta a los siguientes perfiles de configuración de dispositivos (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** o **macOS** para plataforma):

- Personalizado: iOS/iPadOS y macOS
- Características del dispositivo: iOS/iPadOS y macOS
- Restricciones de dispositivos: iOS/iPadOS y macOS
- Endpoint Protection: macOS
- Extensiones: macOS
- Archivo de preferencias: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>Opción Ocultar en la configuración del usuario en características del dispositivo en dispositivos macOS<!-- 6524869 -->

Al crear un perfil de dispositivo de configuración de características en dispositivos macOS, hay una nueva opción **Ocultar en la configuración del usuario** (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** para plataforma > **Características del dispositivo** para perfil > **Elementos de inicio de sesión**).

Esta característica establece la marca de verificación ocultar de una aplicación en la lista de aplicaciones de elementos de inicio de sesión **Usuarios y grupos** en dispositivos macOS. Los perfiles existentes muestran este valor en la lista como sin configurar. Para configurar esta opción, los administradores pueden actualizar los perfiles existentes.

Cuando se establece en **Ocultar**, la casilla ocultar está activada para la aplicación y los usuarios no pueden cambiarla. También oculta la aplicación a los usuarios después de que estos inicien sesión en sus dispositivos.

> [!div class="mx-imgBorder"]
> ![Ocultar aplicaciones en dispositivos macOS después de que los usuarios inicien sesión en el dispositivo en Microsoft Intune y Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Para obtener más información sobre los parámetros que se pueden configurar, vea [Configuración de características de dispositivos macOS](../configuration/macos-device-features-settings.md).

Esta característica se aplica a:

- macOS

## <a name="week-of-march-16-2020-2003-service-release"></a>Semana del 16 de marzo de 2020 (versión del servicio 2003)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>Actualizaciones del Portal de empresa de iOS y macOS<!-- 5779439, 5780234  -->
El panel Perfil del Portal de empresa en macOS e iOS se ha actualizado para incluir el botón Cerrar sesión. Además, se han realizado mejoras de la interfaz de usuario en el panel Perfil en el Portal de empresa para macOS. Para más información sobre Portal de empresa, vea [Configuración de la aplicación Portal de empresa de Microsoft Intune](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Cambio del destino de clips web a Microsoft Edge en dispositivos iOS<!-- 5455276   -->
Los clips web recién implementados (aplicaciones web ancladas) en los dispositivos iOS que se necesitan para abrirse en un explorador protegido se abrirán en Microsoft Edge en lugar de en Intune Managed Browser. Debe cambiar el destino de los clips web existentes para asegurarse de que se abran en Microsoft Edge en lugar de en Managed Browser. Para obtener más información, consulte [Administración del acceso web mediante Microsoft Edge con Microsoft Intune](../apps/manage-microsoft-edge.md) y [Agregar aplicaciones web a Microsoft Intune](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Uso de la herramienta de diagnóstico de Intune con Microsoft Edge para Android<!-- 4735244  -->
Microsoft Edge para Android ahora está integrado con la herramienta de diagnóstico de Intune. De forma similar a la experiencia en Microsoft Edge para iOS, al escribir "about:intunehelp" en la barra de dirección URL (el cuadro de dirección) de Microsoft Edge en el dispositivo se iniciará la herramienta de diagnóstico de Intune. Esta herramienta proporcionará registros detallados. Los usuarios pueden recibir la solicitud de recopilar y enviar estos registros a su departamento de informática, o bien ver los registros de MAM para aplicaciones específicas.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Actualización de la marca y la personalización de Intune<!-- 5236032  -->
Hemos actualizado el panel de Intune que se denominaba "Personalización de marca y personalización" con mejoras, como las siguientes:

- Se va a cambiar el nombre del panel a **Personalización**.
- Se va a mejorar la organización y el diseño de las opciones.
- Se va a mejorar el texto y la información sobre herramientas de las opciones.

Para encontrar estas opciones en Intune, vaya al [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431) y seleccione **Administración de inquilinos** > **Personalización**. Para obtener información sobre la personalización existente, vea [Configuración de la aplicación Portal de empresa de Microsoft Intune](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Clave de recuperación cifrada personal del usuario<!-- 6273943  -->
Hay una nueva característica de Intune disponible que permitirá a los usuarios recuperar su clave de recuperación de **FileVault** cifrada personal para dispositivos Mac a través de la aplicación Portal de empresa de Android o la aplicación de Intune de Android. Hay un vínculo en la aplicación Portal de empresa y en la aplicación de Intune que abrirá un explorador Chrome en el Portal de empresa web, donde el usuario puede ver la clave de recuperación de **FileVault** necesaria para acceder a sus dispositivos Mac. Para obtener más información sobre el cifrado, vea [Uso del cifrado de dispositivos con Intune](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>Optimización de inscripción de dispositivos dedicados <!-- 6114580  -->
Estamos optimizando la inscripción para dispositivos dedicados de Android Enterprise y facilitando la aplicación de certificados SCEP asociados a Wi-Fi a dispositivos dedicados inscritos antes del 22 de noviembre de 2019. En el caso de las nuevas inscripciones, la aplicación de Intune se seguirá instalando, pero los usuarios finales ya no tendrán que realizar el paso para **habilitar el agente de Intune** durante la inscripción. La instalación se realizará en segundo plano automáticamente y los certificados SCEP asociados a Wi-Fi se pueden implementar y establecer sin interacción del usuario final.  

Estos cambios se implementarán por fases a lo largo del mes de marzo, a medida que se implemente el back-end de servicio de Intune. Todos los inquilinos tendrán este nuevo comportamiento hasta el final de marzo. Para ver información relacionada, consulte [Compatibilidad con certificados de SCEP en dispositivos dedicados de Android Enterprise](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Nueva experiencia del usuario al crear plantillas administrativas en dispositivos Windows<!--5096036 -->
A raíz de los comentarios de los clientes y nuestro cambio a la nueva experiencia de pantalla completa de Azure, hemos vuelto a generar la experiencia de perfil de plantillas administrativas con una vista de carpeta. No hemos realizado cambios en ninguna configuración o perfil existente. Por lo tanto, los perfiles existentes seguirán siendo los mismos y se podrán usar en la nueva vista. Todavía puede desplazarse por todas las opciones de configuración seleccionando **Toda la configuración** y usando la búsqueda. La vista de árbol se divide por configuraciones de equipo y usuario. Encontrará la configuración de Windows, Office y Edge en sus carpetas asociadas.  

Se aplica a:
- Windows 10 y versiones posteriores

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>Uso permanente de Always On por parte de los perfiles de VPN con conexiones VPN IKEv2 con dispositivos iOS/iPadOS<!-- 1947932   -->
En dispositivos iOS/iPadOS, puede crear un perfil de VPN que use una conexión IKEv2 (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para plataforma > **VPN** para tipo de perfil). Ahora puede configurar AlwaysOn con IKEv2. Cuando los perfiles de VPN IKEv2 están configurados, se conectan automáticamente y permanecen conectados (o se vuelven a conectar rápidamente) a la VPN. Permanecen conectados incluso al moverse entre redes o al reiniciar dispositivos.

En iOS/iPadOS, la VPN de Always On está limitada a perfiles de IKEv2.

Para ver la configuración IKEv2 que puede establecer, vaya a [Incorporación de VPN en dispositivos iOS en Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Se aplica a:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Eliminación de agrupaciones y matrices de agrupaciones en perfiles de configuración de dispositivos OEMConfig en dispositivos Android Enterprise<!-- 5550355   -->
En los dispositivos Android Enterprise, puede crear y actualizar perfiles de OEMConfig (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** para plataforma > **OEMConfig** para tipo de perfil). Los usuarios pueden ahora eliminar agrupaciones y matrices de agrupaciones mediante el **Diseñador de configuraciones** de Intune.

Para obtener más información sobre los perfiles OEMConfig, vea [Uso y administración de dispositivos Android Enterprise con OEMConfig en Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Se aplica a:
- Android Enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>Configuración de la extensión de aplicación de inicio de sesión único de Microsoft Azure AD en iOS/iPadOS<!-- 5672534   -->
El equipo de Microsoft Azure AD creó una extensión de aplicación de inicio de sesión único (SSO) de redireccionamiento que permite a los usuarios de iOS/iPadOS 13.0+ obtener acceso a aplicaciones y sitios web de Microsoft con un inicio de sesión. Todas las aplicaciones que anteriormente tenían autenticación asincrónica con la aplicación Microsoft Authenticator seguirán recibiendo SSO con la nueva extensión de SSO. Con la versión de la extensión de aplicación de SSO de Azure AD, puede configurar la extensión de SSO con el tipo de extensión de aplicación de SSO de redireccionamiento (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPad** para la plataforma > **Características del dispositivo** para el tipo de perfil > **Extensión de aplicación de inicio de sesión único**).

Se aplica a:
- iOS 13.0 y versiones más recientes
- IPadOS 13.0 y versiones más recientes

Para obtener más información sobre las extensiones de aplicación de SSO de iOS, consulte [Extensión de aplicación de inicio de sesión único](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>La opción de modificación de la configuración de confianza de aplicaciones empresariales se ha quitado de los perfiles de restricción de dispositivos iOS/iPadOS.<!-- 6225131   -->
En los dispositivos iOS/iPadOS puede crear un perfil de restricciones de dispositivo (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para la plataforma > **Restricciones de dispositivos** para el tipo de perfil). Apple ha quitado la opción **Modificación de la configuración de confianza de aplicaciones empresariales**, y también se ha quitado de Intune. Si usa actualmente esta configuración en un perfil, no tiene ningún impacto y se quita de los perfiles existentes. Esta opción también se ha quitado de los informes en Intune.

Se aplica a:
- iOS/iPadOS

Para ver los valores que puede restringir, vaya a [Configuración de dispositivos iOS e iPadOS para permitir o restringir características](../configuration/device-restrictions-ios.md).

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Solución de problemas: Cambio de la notificación de directiva de MAM pendiente a icono informativo<!--6348954 -->
El icono de notificación de una directiva de MAM pendiente en la hoja de solución de problemas se ha cambiado a un icono informativo.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Actualización de la interfaz de usuario al configurar la directiva de cumplimiento<!-- 3961639    -->

Hemos actualizado la interfaz de usuario para [crear directivas de cumplimiento](../protect/create-compliance-policy.md#create-the-policy) en el Administrador de puntos de conexión de Microsoft (**Dispositivos** > **Directivas de cumplimiento** > **Directivas** > **Crear directiva**). Tenemos una nueva experiencia de usuario que proporciona la misma configuración y los mismos detalles que ha usado anteriormente. La nueva experiencia sigue un proceso similar a un asistente para crear una directiva de cumplimiento e incluye una página en la que puede agregar *Asignaciones* a la directiva, y una página *Revisar y crear* en la que puede revisar la configuración antes de crear la directiva.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Retirar dispositivos no compatibles<!-- 1827291       -->
Hemos agregado una nueva acción para dispositivos no compatibles que puede agregar a cualquier directiva para [retirar el dispositivo no compatible](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance).  La nueva acción, **Retirar el dispositivo no compatible**, da como resultado la eliminación de todos los datos de la compañía del dispositivo, y también quita el dispositivo de la administración de Intune.  Esta acción se ejecuta cuando se alcanza el valor configurado en días y, en ese momento, el dispositivo se puede retirar. El valor mínimo es 30 días.  Se requerirá la aprobación explícita del administrador de TI para retirar los dispositivos mediante la sección *Retirada de los dispositivos no compatibles*, donde los administradores pueden retirar todos los dispositivos que cumplan los requisitos.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Compatibilidad con WPA y WPA2 en perfiles de Wi-Fi Empresarial de iOS<!--6215273   -->
[Los perfiles de Wi-Fi de empresa para iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) admiten ahora el campo *Tipo de seguridad*. En *Tipo de seguridad*, puede seleccionar**WPA Enterprise** o **WPA/WPA2 Enterprise** y, a continuación, especificar una selección para el *tipo de EAP*.  (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** y seleccione **iOS/iPad** para *Plataforma* y **Wi-Fi** para *Perfil*). 

Las nuevas opciones de empresa son similares a las que están disponibles para un perfil de Wi-Fi básico para iOS.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Nueva experiencia de usuario para perfiles de certificado, correo electrónico, VPN y Wi-Fi<!-- 5615208   -->
Se ha actualizado la [experiencia del usuario](../configuration/device-profile-create.md) en el Centro de administración del Administrador de puntos de conexión (**Dispositivos** > **Perfiles de configuración** > **Crear perfil**) para crear y modificar los siguientes tipos de perfil. La nueva experiencia presenta las mismas opciones que antes, pero usa una experiencia similar a un asistente que no requiere tanto desplazamiento horizontal. Con la nueva experiencia no tendrá que modificar las configuraciones existentes.

- Credencial derivada
- Correo electrónico
- Certificado PKCS
- Certificado PKCS importado
- Certificado SCEP
- Certificado de confianza
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscripción de dispositivos

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Configuración de la disponibilidad de la inscripción en Portal de empresa para iOS y Android<!-- 4260128  -->
Puede configurar si la inscripción de dispositivos en el Portal de empresa en dispositivos iOS y Android está disponible con mensajes o sin mensajes o no está disponible para los usuarios. Para encontrar estas opciones en Intune, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y seleccione **Administración de inquilinos** > **Personalización** > **Editar** > **Inscripción de dispositivos**.  

La compatibilidad con la configuración de inscripción de dispositivos requiere que los usuarios finales tengan estas versiones del Portal de empresa:
-    Portal de empresa en iOS: versión 4.4 o posterior
-    Portal de empresa en Android: versión 5.0.4715.0 o posterior

Para obtener más información sobre la personalización existente del Portal de empresa, vea [Configuración de la aplicación Portal de empresa de Microsoft Intune](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Nuevo informe de Android en la página de información general de dispositivos Android<!-- 5435435   -->
Hemos agregado un informe a la consola de administración del Administrador de puntos de conexión de Microsoft en la página de información general de dispositivos Android, en la que se muestra el número de dispositivos Android inscritos en cada solución de administración de dispositivos. En este gráfico (como en el de la consola de Azure) se muestra la cantidad de dispositivos inscritos de perfil de trabajo, totalmente administrados, dedicados y de administrador de dispositivos. Para ver el informe, elija **Dispositivos** > **Android** > **Información general**.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738---wnstaged--"></a>Guía para usuarios desde la administración de administradores de dispositivos Android a la administración de perfiles de trabajo<!--5857738   wnstaged-->
Se va a publicar una nueva opción de cumplimiento para la plataforma de administrador de dispositivos Android. Esta opción permite hacer que un dispositivo no sea compatible si se administra con el administrador de dispositivos.

En estos dispositivos no compatibles, en la página **Actualizar configuración del dispositivo**, los usuarios verán el mensaje **Mover a la nueva configuración de administración de dispositivos**. Si pulsa el botón **Resolver**, se les guiará por lo siguiente:

1. Anulación de la inscripción desde la administración de administradores de dispositivos
2. Inscripción en la administración de perfiles de trabajo
3. Resolución de problemas de cumplimiento 
 
En un esfuerzo por cambiar a la administración de dispositivos moderna, más completa y segura, Google va a reducir la compatibilidad con el administrador de dispositivos en las nuevas versiones de Android.  Intune solo puede proporcionar compatibilidad completa con dispositivos Android administrados por el administrador de dispositivos que ejecuten Android 10 y versiones posteriores hasta el segundo trimestre de 2020. Los dispositivos administrados por el administrador de dispositivos (menos Samsung) que ejecuten Android 10 o versiones posteriores después de este periodo ya no se podrán administrar de forma completa. En concreto, los dispositivos afectados no recibirán nuevos requisitos de contraseña.

Para obtener más información acerca de esta configuración, consulte [Transferencia de dispositivos Android desde el administrador de dispositivos a la administración de perfiles de trabajo](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Ahora, el almacenamiento de datos proporciona la dirección MAC.<!-- 6123680  -->
El almacenamiento de datos de Intune proporciona la dirección MAC como una nueva propiedad (`EthernetMacAddress`) en la entidad `device` para permitir que los administradores se correspondan entre el usuario y la dirección Mac del host. Esta propiedad ayuda a llegar a usuarios específicos y a solucionar los incidentes que se producen en la red. Los administradores también pueden usar esta propiedad en [Informes de Power BI](../developer/reports-proc-get-a-link-powerbi.md) para generar informes más completos. Para obtener más información, vea la entidad de [dispositivo](../developer/intune-data-warehouse-collections.md#devices) en el Almacenamiento de datos de Intune.

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Propiedades de inventario de dispositivos de almacenamiento de datos adicionales<!-- 6125732  -->
Las propiedades adicionales de inventario de dispositivos están disponibles mediante el Almacenamiento de datos de Intune. Las propiedades siguientes se exponen ahora a través de la colección de [dispositivos](../developer/intune-data-warehouse-collections.md#devices):
- "Model": el modelo del dispositivo.
- "Office365Version": la versión de Office 365 instalada en el dispositivo.
- "PhysicalMemoryInBytes": memoria física en bytes.
- `TotalStorageSpaceInBytes`: capacidad total de almacenamiento en bytes.

Para obtener más información, vea [API de Almacenamiento de datos de Intune](../developer/reports-nav-intune-data-warehouse.md) y la entidad de [dispositivos](../developer/intune-data-warehouse-collections.md#devices) de Almacenamiento de datos de Intune.

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Actualización del flujo de trabajo de ayuda y soporte técnico para admitir servicios adicionales<!-- 5654170   -->
Hemos actualizado la página de ayuda y soporte técnico en el centro de administración del Administrador de puntos de conexión de Microsoft, donde ahora [elige el tipo de administración que usa](../fundamentals/get-support.md#options-to-access-help-and-support). Con este cambio podrá seleccionar de entre los tipos de administración siguientes:

- Configuration Manager (incluye Análisis de escritorio)
- Intune
- Administración conjunta

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Seguridad

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Uso de una versión preliminar de las directivas centradas en el administrador de seguridad como parte de la seguridad del punto de conexión<!--6131401  -->
Como versión preliminar pública, se han agregado varios grupos de directivas nuevos en el nodo de seguridad del punto de conexión en el centro de administración de puntos de conexión de Microsoft. Como administrador de seguridad, puede usar estas nuevas directivas para centrarse en aspectos específicos de la seguridad de los dispositivos con el fin de administrar grupos discretos de configuración relacionada sin la sobrecarga del cuerpo de directivas de configuración de dispositivos, más grande.

A excepción de la nueva *directiva antivirus para el antivirus de Microsoft Defender* (consulte a continuación), la configuración de cada una de estas nuevas directivas y perfiles en versión preliminar es la misma que ya ha configurado hoy a través de los [perfiles de configuración de dispositivos](../configuration/device-profile-create.md).

Estos son los nuevos tipos de directivas que se encuentran en versión preliminar y sus tipos de perfil disponibles:

- **Antivirus (versión preliminar)** :
  - macOS:
    - **Antivirus**: administre la [configuración de directivas antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) para macOS para administrar [ATP de Microsoft Defender para Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

  - Windows 10 y versiones posteriores:
    - **Antivirus de Microsoft Defender**: administre la [configuración de directivas antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) para protección en la nube, exclusiones del antivirus, correcciones, opciones de análisis, etc.

      El perfil antivirus para el *antivirus de Microsoft Defender* es una excepción que introduce una nueva instancia de la configuración que se encuentra como parte de un perfil de restricción de dispositivos. Estas nuevas opciones de configuración del antivirus:

        - Son las mismas opciones que se encuentran en las restricciones de dispositivos, pero admiten una tercera opción de configuración que no está disponible cuando se configura como una restricción de dispositivo.
        - Se aplican a los dispositivos que se administran conjuntamente con Configuration Manager, cuando el [control deslizante de carga de trabajo de administración conjunta](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) para Endpoint Protection está establecido en Intune.

     Planean usar el nuevo perfil *Antivirus* > *Antivirus de Microsoft Defender* en lugar de configurarlos a través de un perfil de restricción de dispositivos.

  - **Experiencia de seguridad de Windows**: administre la configuración de seguridad de Windows que los usuarios finales pueden ver en el centro de seguridad de Microsoft Defender y las notificaciones que reciben. Estos valores no se modifican respecto a los disponibles como perfil de Endpoint Protection en la configuración de dispositivos.

- **Cifrado de disco (versión preliminar)** :
  - macOS:
    - **FileVault**
  - Windows 10 y versiones posteriores:
    - **BitLocker**
- **Firewall (versión preliminar)** :
  - macOS:
    - **Firewall de macOS**
  - Windows 10 y versiones posteriores:
    - **Firewall de Microsoft Defender**
- **Detección de puntos de conexión y respuesta (versión preliminar)** :
  - Windows 10 y versiones posteriores: -**Windows 10 Intune**
- **Reducción de la superficie expuesta a ataques (versión preliminar)** :
  - Windows 10 y versiones posteriores:
    - **Aislamiento de aplicaciones y navegador**
    - **Protección web**
    - **Control de la aplicación**
    - **Reglas de reducción de la superficie expuesta a ataques**
    - **Control de dispositivos**
    - **Protección contra vulnerabilidades**
- **Protección de cuentas (versión preliminar)** :
  - Windows 10 y versiones posteriores:
    - **Protección de cuentas**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Semana del 9 de marzo de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Configuración del agente de optimización de entrega al descargar contenido de aplicaciones Win32<!-- 5410945 -->

El agente de optimización de distribución se puede configurar para descargar contenido de aplicaciones Win32 en primer o segundo plano en función de la asignación. En el caso de las aplicaciones Win32 existentes, el contenido se seguirá descargando en el modo de segundo plano. En el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Aplicaciones** > **Todas las aplicaciones** > *seleccione la aplicación Win32* > **Propiedades**. Seleccione **Editar** junto a **Asignaciones**.  Edite la asignación seleccionando **Incluir** en **Modo**, en la sección **Requerido**.  Verá la nueva configuración en la sección **Configuración de la aplicación**. Para obtener más información sobre la Optimización de entrega, vea [Administración de aplicaciones Win32: Optimización de entrega](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Cambio del usuario primario para dispositivos Windows<!-- 3794742   -->
Puede cambiar el usuario primario de dispositivos híbridos de Windows y unidos a Azure AD. Para ello, vaya a **Intune** > **Dispositivos** > **Todos los dispositivos** > elija un dispositivo > **Propiedades** > **Usuario primario**. Para más información, vea [Cambio del usuario principal de un dispositivo](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

También se ha creado un nuevo permiso RBAC (Dispositivos administrados/Establecer usuario primario) para esta tarea. El permiso se ha agregado a diversos roles integrados como, por ejemplo, Departamento de soporte técnico, Administrador educativo y Administrador de seguridad de puntos de conexión.

Esta característica se está implementando en los clientes de forma global en su versión preliminar. Debería verla en las próximas semanas.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Semana del 2 de marzo de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager reúne Configuration Manager e Intune en una misma consola. A partir de la versión 2002.2 de Technical Preview de Configuration Manager, se pueden cargar dispositivos de Configuration Manager en el servicio en la nube y realizar acciones en ellos en el centro de administración. Para más información, vea de [Características de la versión 2002.2 de Technical Preview de Configuration Manager](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Revise el [artículo de Technical Preview de Configuration Manager](https://docs.microsoft.com/configmgr/core/get-started/technical-preview) antes de instalar esta actualización. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.

#### <a name="bulk-remote-actions--4576882--"></a>Acciones remotas en masa<!--4576882-->
Ahora puede emitir comandos en masa para las siguientes acciones remotas: reiniciar, cambiar el nombre, restablecer Autopilot, borrar y eliminar. Para ver las nuevas acciones en masa, vaya al [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Todos los dispositivos** > **Acciones en masa**.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Lista de todos los dispositivos búsqueda, ordenación y filtro mejorados<!--6179023-->
La lista Todos los dispositivos se ha mejorado para optimizar el rendimiento, la búsqueda, la ordenación y el filtrado. Para más información, vea [esta sugerencia de soporte técnico](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### <a name="app-management"></a>Administración de aplicaciones  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Experiencia de inicio de sesión mejorada en la aplicación Portal de empresa para Android    
Hemos actualizado el diseño de varias pantallas de inicio de sesión en la aplicación Portal de empresa para Android a fin de que la experiencia sea más moderna, sencilla y limpia para los usuarios. Para comprobar las mejoras, vea [Novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui).

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Semana del 24 de febrero de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>mejoras en la experiencia del usuario del Portal de empresa de macOS<!-- 5568987 -->
Se han realizado mejoras en la experiencia de inscripción de dispositivos macOS y en la aplicación Portal de empresa para Mac. Verá las siguientes mejoras:
- Mejora de la experiencia de Microsoft **AutoUpdate** durante la inscripción que garantizará que los usuarios tengan la versión más reciente del Portal de empresa.
- Paso de comprobación de cumplimiento mejorado durante la inscripción.
- Compatibilidad con los identificadores de incidentes copiados, por lo que los usuarios pueden enviar los errores más rápido desde sus dispositivos al equipo de soporte técnico de su empresa.

Para obtener más información sobre la inscripción y la aplicación Portal de empresa aplicación para Mac, vea [Inscripción del dispositivo macOS mediante la aplicación Portal de empresa](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Ahora las directivas de protección de aplicaciones para Better Mobile admiten iOS e iPadOS<!-- 6224512  -->

En octubre de 2019, la directiva de protección de aplicaciones de Intune agregó la capacidad de usar datos de nuestros asociados de Microsoft Threat Defense. Con esta actualización, ahora puede usar una directiva de protección de aplicaciones para bloquear o borrar de forma selectiva los datos corporativos de los usuarios en función del estado de un dispositivo mediante Better Mobile en iOS e iPadOS.  Para más información, consulte [Creación de una directiva de protección de aplicaciones de Mobile Threat Defense con Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Las exportaciones de la lista Todos los dispositivos ahora en formato CSV comprimido<!--6343117-->
Ahora las exportaciones de la página **Dispositivos** > **Todos los dispositivos** están en formato CSV comprimido.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Semana del 17 de febrero de 2020 (versión del servicio 2002)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>Aplicación Advanced Threat Protection (ATP) de Microsoft Defender para macOS<!-- 5424618 -->
Intune proporciona una manera sencilla de implementar la aplicación Advanced Threat Protection (ATP) de Microsoft Defender para macOS en dispositivos Mac administrados. Para obtener más información, vea [Adición de ATP de Microsoft Defender en dispositivos macOS con Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) y [Protección contra amenazas avanzada de Microsoft Defender para Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Habilitación del control de acceso a la red (NAC) con la VPN de Cisco AnyConnect en dispositivos iOS<!-- 4860111  -->
En los dispositivos iOS, puede crear un perfil de VPN y usar tipos de conexión diferentes, entre los que se incluyen Cisco AnyConnect (**Configuración de dispositivo** > **Perfiles** > **Crear perfil** > **iOS** para la plataforma > **VPN** para el tipo de perfil > **Cisco AnyConnect** para el tipo de conexión).

Puede habilitar el control de acceso a la red (NAC) con Cisco AnyConnect. Para usar esta característica,:

1. En la [Guía del administrador del motor de Cisco Identity Services](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html), siga los pasos de **Configuración de Microsoft Intune como servidor MDM** para configurar el motor de Cisco Identity Services (ISE) en Azure.
2. En el perfil de configuración de dispositivos de Intune, seleccione la opción **Habilitar el control de acceso a la red (NAC)** .

Para ver las opciones de VPN disponibles, vaya a [Configuración de VPN en dispositivos iOS](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscripción de dispositivos

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Número de serie en la página del certificado push MDM de Apple<!--5947765  -->
Ahora en la página del certificado push MDM de Apple se muestra el número de serie. El número de serie es necesario para recuperar el acceso al certificado de extracción MDM de Apple si se pierde el acceso al id. de Apple que creó el certificado. Para ver el número de serie, vaya a **Dispositivos** > **iOS** > **Inscripción de iOS** > **Certificado push MDM de Apple**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Nuevas opciones de programación de actualización para insertar actualizaciones del sistema operativo en dispositivos iOS/iPadOS inscritos<!--5879689  -->
Puede elegir entre las opciones siguientes al programar las actualizaciones del sistema operativo para dispositivos iOS/iPadOS. Estas opciones se aplican a los dispositivos que usaron los tipos de inscripción Apple Business Manager o Apple School Manager.
- Actualización en la siguiente inserción
- Actualización durante la hora programada
- Actualización fuera de la hora programada

En las dos últimas opciones, puede crear varias ventanas de tiempo.

Para ver las nuevas opciones, vaya a MEM > **Dispositivos** >  **iOS** > **Directivas de actualización para iOS/iPadOS** > **Crear perfil**.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Elección de las actualizaciones de iOS/iPadOS que se van a insertar en los dispositivos inscritos<!--5879689  -->
Puede elegir una actualización específica de iOS/iPadOS (excepto para la más reciente) para insertarla en los dispositivos inscritos mediante Apple Business Manager o Apple School Manager. Estos dispositivos deben tener una directiva de configuración de dispositivos establecida para retrasar la visibilidad de las actualizaciones de software durante un número determinado de días. Para ver esta característica, vaya a MEM > **Dispositivos** >  **iOS** > **Directivas de actualización para iOS/iPadOS** > **Crear perfil**.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Mejora de la experiencia de informes de Intune<!-- 3791418   -->
Intune ahora proporciona una experiencia de informes mejorada, con nuevos tipos de informes, una mejor organización de informes, vistas más centradas y una funcionalidad de informes más eficiente, así como datos más coherentes y precisos. La experiencia de informes pasará de la versión preliminar pública a GA (disponibilidad general). Además, la versión de GA proporcionará compatibilidad para la localización, correcciones de errores, mejoras de diseño y datos de cumplimiento de dispositivos agregados en los mosaicos del [Centro de administración de Microsoft Endpoint Manager ](https://go.microsoft.com/fwlink/?linkid=2109431).

Los nuevos tipos de informe se centran en la información siguiente:

- **Operativo**: proporciona registros nuevos con un enfoque de estado negativo. 
- **Organizativo**: proporciona un resumen más amplio del estado general.
- **Histórico**: proporciona patrones y tendencias a lo largo de un período de tiempo.
- **Especialista**: le permite usar datos sin procesar para crear sus propios informes personalizados.

El primer conjunto de informes nuevos se centra en el cumplimiento de los dispositivos. Para obtener más información, vea [Blog:marco de creación de informes de Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) e [Informes de Intune](reports.md).

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Consolidación de la ubicación de las líneas de base de seguridad en la interfaz de usuario<!-- 6177074   -->
Se han consolidado las rutas de acceso para encontrar [líneas de base de seguridad](../protect/security-baselines.md) en el Centro de administración del Administrador de puntos de conexión de Microsoft mediante la eliminación de *Líneas de base de seguridad* de varias ubicaciones de la interfaz de usuario. Para buscar líneas de base de seguridad, ahora se usa la ruta de acceso siguiente:  **Seguridad de los puntos de conexión** > **Líneas de base de seguridad**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>Compatibilidad ampliada con certificados PKCS importados<!-- 6044197  -->
Se ha ampliado la compatibilidad con el uso de [certificados PKCS importados](../protect/certificates-imported-pfx-configure.md#supported-platforms) para admitir *dispositivos Android Enterprise totalmente administrados*. Por lo general, la importación de certificados PFX se usa para escenarios de cifrado S/MIME, donde los certificados de cifrado de un usuario son necesarios en todos sus dispositivos para que se pueda realizar el descifrado del correo electrónico.

Las siguientes plataformas admiten la importación de certificados PFX:

- Android: Administrador de dispositivos
- Android Enterprise: Totalmente administrado
- Android Enterprise: Perfil de trabajo
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Visualización de la configuración de seguridad de los puntos de conexión para dispositivos<!-- 6206460  -->
Se ha actualizado el nombre de la opción en el Centro de administración del Administrador de puntos de conexión de Microsoft para ver las [configuraciones de seguridad de los puntos de conexión que se aplican a un dispositivo específico](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). Se ha cambiado el nombre de esta opción por **Configuración de seguridad de los puntos de conexión** porque muestra las líneas base de seguridad aplicables y las directivas adicionales creadas fuera de las líneas de base de seguridad. Esta opción antes se denominaba *Líneas de base de seguridad*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Control de acceso basado en roles.

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Próximos cambios en la interfaz de usuario de roles de Intune<!--5801612   -->
La interfaz de usuario del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Administración de inquilinos** > **Roles** se ha mejorado con un diseño más sencillo e intuitivo. Esta experiencia proporciona la misma configuración y los mismos detalles que se usan ahora, pero la nueva experiencia emplea un proceso similar a un asistente.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>Semana del 17 de febrero de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="microsofts-new-office-app---5859926---"></a>Nueva aplicación de Office de Microsoft<!-- 5859926 -->
La nueva aplicación de Office de Microsoft ya está disponible con carácter general para su descarga y uso. La aplicación de Office es una experiencia consolidada en la que los usuarios pueden trabajar en Word, Excel y PowerPoint en una sola aplicación. Puede dirigirse a la aplicación con una directiva de protección de aplicaciones para asegurarse de que los datos a los que se accede están protegidos.

Para obtener más información, vea [Procedimiento para habilitar las directivas de protección de aplicaciones de Intune con la aplicación de Office en versión preliminar para dispositivos móviles](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>Semana del 10 de febrero de 2020

### <a name="windows-7-ends-extended-support--3042987---"></a>Finalización del soporte extendido de Windows 7<!--3042987 -->
El 14 de enero de 2020 finalizó el soporte extendido de Windows 7. En Intune ha quedado en desuso el soporte para los dispositivos que ejecutan Windows 7 al mismo tiempo. La asistencia técnica y las actualizaciones automáticas que ayudan a proteger su equipo ya no están disponibles. Se debe actualizar a Windows 10. Para más información, vea la [entrada de blog sobre el plan de cambios](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Microsoft Edge versión 77 y posteriores en dispositivos con Windows 10<!-- 5843584 -->
Intune ahora admite la desinstalación de la versión 77 y posteriores de Microsoft Edge en dispositivos con Windows 10. Para obtener más información, consulte [Adición de Microsoft Edge para Windows 10 a Microsoft Intune](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>Pantalla quitada del Portal de empresa, inscripción del perfil de trabajo de Android<!--6103987 -->
La pantalla **¿Cuál es el paso siguiente?** se ha quitado del flujo de inscripción del perfil de trabajo de Android en el Portal de empresa para simplificar la experiencia del usuario. Vaya a [Inscripción con el perfil de trabajo de Android](../user-help/enroll-device-android-work-profile.md) para ver el flujo de inscripción del perfil de trabajo de Android actualizado.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Rendimiento mejorado de la aplicación Portal de empresa<!-- 6178652 -->
La aplicación Portal de empresa se ha actualizado para admitir un rendimiento mejorado en los dispositivos que usan procesadores ARM64, como Surface Pro X. Anteriormente, el Portal de empresa operaba en un modo ARM32 emulado. Ahora, en la versión 10.4.7080.0 y en versiones posteriores, la aplicación Portal de empresa se compila de forma nativa para ARM64. Para más información sobre la aplicación Portal de empresa, consulte [Configuración de la aplicación Portal de empresa de Microsoft Intune](../apps/company-portal-app.md).

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>Semana del 27 de enero de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>Compatibilidad de Intune con el canal de implementación adicional de Microsoft Edge versión 77 para macOS<!-- 5983950  -->
Microsoft Intune ahora admite el canal de implementación **estable** para la aplicación Microsoft Edge para macOS. El canal **estable** es el canal recomendado para la implementación de Microsoft Edge en general en entornos empresariales. Se actualiza cada seis semanas y cada versión incorpora mejoras del canal **beta**. Además de canales **estable** y **beta**, Intune admite un canal de **desarrollo**. La versión preliminar pública ofrece los canales estable y de desarrollo para la versión 77 y posteriores de Microsoft Edge para macOS. Las actualizaciones automáticas del explorador están activadas de forma predeterminada. Para obtener más información, consulte [Adición de Microsoft Edge a dispositivos macOS con Microsoft Intune](../apps/apps-edge-macos.md).

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>Retirada de Intune Managed Browser<!--5728447 -->
Se va a retirar Intune Managed Browser. Use Microsoft Edge para la experiencia de explorador de Intune protegida. 

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>Semana del 20 de enero de 2020 (versión del servicio 2001)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>Cambio en la experiencia del usuario al agregar aplicaciones a Intune<!-- 4705829   -->
Verá una nueva experiencia de usuario al agregar aplicaciones a través de Intune. Esta experiencia proporciona la misma configuración y los mismos detalles que ha usado anteriormente, pero la nueva experiencia emplea un proceso similar a un asistente antes de agregar una aplicación a Intune. Esta nueva experiencia también proporciona una página de revisión antes de agregar la aplicación. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Aplicaciones** > **Todas las aplicaciones** > **Agregar**. Para más información, vea [Agregar aplicaciones a Microsoft Intune](../apps/apps-add.md).

#### <a name="require-win32-apps-to-restart----5622282-----"></a>Requisito de reinicio de las aplicaciones Win32 <!-- 5622282   -->
Puede requerir que una aplicación Win 32 se reinicie después de una instalación correcta. Además, puede elegir el tiempo (el período de gracia) que transcurrirá antes de que se produzca el reinicio.

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>Cambio en la experiencia del usuario al configurar aplicaciones en Intune<!-- 4207990   -->
Verá una nueva experiencia de usuario al crear directivas de configuración de aplicaciones en Intune. Esta experiencia proporciona la misma configuración y los mismos detalles que ha usado anteriormente, pero la nueva experiencia emplea un proceso similar a un asistente antes de agregar una directiva a Intune. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar**. Para obtener más información, vea [Directivas de configuración de aplicaciones para Microsoft Intune](../apps/app-configuration-policies-overview.md). 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>Compatibilidad de Intune con el canal de implementación adicional de Microsoft Edge para Windows 10<!-- 5861774 -->
Microsoft Intune ahora admite el canal de implementación adicional **estable** para la aplicación Microsoft Edge (versión 77 y posteriores) para Windows 10. El canal **estable** es el canal recomendado para la implementación de Microsoft Edge para Windows 10 en general en entornos empresariales. Este canal se actualiza cada seis semanas y cada versión incorpora mejoras del canal **beta**. Además de canales **estable** y **beta**, Intune admite un canal de **desarrollo**. Para obtener más información, vea [Microsoft Edge para Windows 10 - Configuración de aplicaciones](../apps/apps-windows-edge.md#configure-app-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>Mejor experiencia de interfaz de usuario al configurar la interfaz de usuario del conector local de Exchange ActiveSync<!-- 5695492   -->
Hemos actualizado para experiencia para [configurar el conector local de Exchange ActiveSync](../protect/exchange-connector-install.md). La experiencia actualizada usa un solo panel para configurar, editar y resumir los detalles de los conectores locales.

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>Adición de configuración de proxy automática a perfiles de Wi-Fi para perfiles de trabajo de Android Enterprise<!-- 4490822   -->
En los dispositivos de perfil de trabajo de Android Enterprise, puede crear perfiles de Wi-Fi. Al elegir el tipo Wi-Fi Enterprise, también puede especificar el tipo de protocolo de autenticación extensible (EAP) que se usa en la red Wi-Fi.

Ahora, al elegir el tipo de empresa, también puede especificar la configuración de proxy automática, incluida una dirección URL del servidor proxy, como `proxy.contoso.com`.

Para ver la configuración de Wi-Fi actual que puede establecer, vaya a [Incorporación de la configuración de Wi-Fi en Microsoft Intune para dispositivos que ejecutan Android Enterprise y el Quiosco de Android](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only).

Se aplica a:
- Perfil de trabajo de Android Enterprise

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscripción de dispositivos

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>Bloqueo de las inscripciones de Android por el fabricante del dispositivo<!--5197392  -->
Puede bloquear la inscripción de dispositivos en función del fabricante del dispositivo. Esta característica se aplica al administrador de dispositivos Android y los dispositivos de perfil de trabajo de Android Enterprise. Para ver las restricciones de inscripción, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Restricciones de inscripción**.

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>Mejoras en la interfaz de usuario para Crear un perfil de tipo de inscripción en iOS/iPadOS<!-- 6055005 -->
Para la inscripción de usuarios de iOS/iPadOS, se ha simplificado la página **Crear un perfil de tipo de inscripción** **Configuración** para mejorar el proceso de elección del **Tipo de inscripción** manteniendo la misma funcionalidad. Para ver la interfaz de usuario nueva, vaya a la página [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **iOS** > **Inscripción de iOS** > **Tipos de inscripción** > **Crear perfil** > **Configuración**. Para obtener más información, consulte [Creación de un perfil de inscripción de usuario en Intune](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="new-information-in-device-details---4471759-5604099----"></a>Nueva información en los detalles del dispositivo<!-- 4471759 5604099  -->
La siguiente información está ahora en la página de **información general** para dispositivos:
- Capacidad de memoria (cantidad de memoria física en el dispositivo)
- Capacidad de almacenamiento (cantidad de almacenamiento físico en el dispositivo) 
- Arquitectura de CPU

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>Cambio de nombre de la acción remota Omisión del bloqueo de activación de iOS a Deshabilitación del bloqueo de activación <!--5904591  -->
Se ha cambiado el nombre de la acción remota **Omisión del bloqueo de activación** a **Deshabilitación del bloqueo de activación**. Para obtener más información, consulte [Deshabilitación del bloqueo de activación de iOS con Intune](../remote-actions/device-activation-lock-disable.md).

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>Compatibilidad con la implementación de actualizaciones de características de Windows 10 para dispositivos AutoPilot<!-- 5948137   -->
Intune ahora admite dispositivos registrados con AutoPilot mediante [implementaciones de actualizaciones de características de Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates).

Las directivas de actualización de características de Windows 10 no se pueden aplicar durante la configuración rápida (OOBE) de Autopilot y solo se aplican en el primer análisis de Windows Update una vez que el dispositivo haya finalizado el aprovisionamiento (que suele ser un día).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Informes de implementación de Windows Autopilot (versión preliminar) <!-- 3856172   -->
Un nuevo informe detalla cada dispositivo implementado mediante Windows Autopilot. Para más información, vea [Informe de implementaciones de Autopilot](../enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Control de acceso basado en roles.

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>Nuevo rol de Administrador de seguridad de los puntos de conexión integrado en Intune<!--4253397   -->
Hay un nuevo rol integrado de Intune disponible: el administrador de seguridad de los puntos de conexión. Este nuevo rol concede a los administradores acceso completo al nodo del administrador de puntos de conexión en Intune y acceso de solo lectura a otras áreas. El rol es una expansión del rol "Administrador de seguridad" de Azure AD. Si actualmente solo tiene administradores globales como roles, no es necesario realizar ningún cambio. Si usa roles y desea la granularidad que proporciona el Administrador de seguridad de puntos de conexión, asigne ese rol cuando esté disponible. Para más información acerca de roles integrados, vea [Control de acceso basado en rol](role-based-access-control.md).

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>Semana del 6 de enero de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>Compatibilidad de S/MIME con Microsoft Outlook para iOS<!-- 2669398 -->
Intune admite la entrega de certificados de cifrado y firma S/MIME que se pueden usar con Outlook para iOS en dispositivos iOS. Para más información, consulte [Etiquetado de sensibilidad y protección en Outlook para iOS y Android](https://aka.ms/omsmime).

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>Almacenamiento en caché del contenido de la aplicación Win32 mediante el servidor de caché con conexión de Microsoft<!-- 6030314 -->
Puede instalar un servidor de caché con conexión de Microsoft en los puntos de distribución de Configuration Manager para almacenar en caché el contenido de la aplicación Win32 de Intune. Para más información, consulte [Caché con conexión de Microsoft en Configuration Manager - Compatibilidad con aplicaciones Win32 de Intune](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Control de acceso basado en roles.

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Los perfiles de plantillas administrativas de Windows 10 (ADMX) ahora admiten etiquetas de ámbito <!--5137390 -->
Ahora puede asignar etiquetas de ámbito a los perfiles de plantilla administrativa (ADMX). Para ello, vaya a **Intune** > **Dispositivos** > **Perfiles de configuración** > elija un perfil de plantillas administrativas en la lista > **Propiedades** > **Etiquetas de ámbito**. Para más información sobre las etiquetas de ámbito, vea [Asignar etiquetas de ámbito a otros objetos](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>Semana del 30 de diciembre de 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>Recuperación de una clave de recuperación personal desde dispositivos macOS con cifrado de MEM<!-- 4851745 -->
Los usuarios finales pueden recuperar su clave de recuperación personal (clave de FileVault) mediante la aplicación Portal de empresa de iOS. El dispositivo que tiene la clave de recuperación personal se debe inscribir en Intune y cifrar con FileVault a través de Intune. Con la aplicación Portal de empresa de iOS, un usuario final puede recuperar su clave de recuperación personal en su dispositivo macOS cifrado haciendo clic en **Obtener clave de recuperación**. También puede recuperar la clave de recuperación en Intune si selecciona **Dispositivos** > *el dispositivos macOS cifrado e inscrito* > **Obtener clave de recuperación**. Para más información sobre FileVault, consulte [Cifrado de FileVault para macOS](../protect/encrypt-devices.md#filevault-encryption-for-macos).

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>Aplicaciones de VPP con licencia de usuario de iOS y iPadOS<!-- 5619268 -->
En el caso de los dispositivos iOS y iPadOS inscritos por el usuario, los usuarios finales ya no verán las aplicaciones de VPP con licencia de dispositivo recién creadas implementadas como disponibles. Sin embargo, los usuarios finales seguirán viendo todas las aplicaciones de VPP con licencia de usuario en el Portal de empresa. Para más información relacionada con las aplicaciones VPP, vea [Administración de aplicaciones de iOS y macOS compradas a través del Programa de Compras por Volumen de Apple con Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>Semana del 23 de diciembre de 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>Aviso: La compatibilidad de Windows 10 1703 (RS2) finalizará <!-- 5026679 -->
A partir del 9 de octubre de 2018, finalizó la compatibilidad de Windows 10 1703 (RS2) con la plataforma de Microsoft para las ediciones Home, Pro y Pro for Workstations. En el caso de las ediciones Windows 10 Enterprise y Education, la compatibilidad de Windows 10 1703 (RS2) con la plataforma finalizó el 8 de octubre de 2019. A partir del 26 de diciembre de 2019, actualizaremos la versión mínima de la aplicación Portal de empresa de Windows a Windows 10 1709 (RS3). Los equipos que ejecutan versiones anteriores a 1709 dejarán de recibir las versiones actualizadas de la aplicación desde Microsoft Store. Comunicamos anteriormente este cambio a los clientes que administran versiones anteriores de Windows 10 a través del centro de mensajes. Para más información, consulte [Hoja de datos del ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>Semana del 16 de diciembre de 2019

### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Actualizaciones de Plantillas administrativas para dispositivos Windows 10 <!-- 5941568 -->

Puede usar plantillas ADMX en Microsoft Intune para controlar y administrar la configuración de Microsoft Edge, Office y Windows. Las Plantillas administrativas en Intune realizaron estas actualizaciones en la configuración de las directivas:

- Se agregó compatibilidad con las versiones 78 y 79 de Microsoft Edge.
- Incluye los archivos ADMX del 11 de noviembre de 2019 en [Archivos de Plantillas administrativas (ADMX/ADML) y la Herramienta de personalización de Office para Office 365 ProPlus, Office 2019 y Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

Para más información sobre las plantillas ADMX en Intune, consulte [Usar plantillas de Windows 10 para configurar opciones de directiva de grupo en Microsoft Intune](../configuration/administrative-templates-windows.md).

Se aplica a:

- Windows 10 y versiones posteriores

## <a name="week-of-december-9-2019-1912-service-release"></a>Semana del 9 de diciembre de 2019 (versión del servicio 1912)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>Migración a Microsoft Edge para escenarios de exploración administrados<!-- 5173762 -->
A medida que se acerca la retirada de Intune Managed Browser, se han realizado cambios en las directivas de protección de aplicaciones para simplificar los pasos necesarios para trasladar a los usuarios a Edge. Se han actualizado las opciones de la configuración de directiva de protección de aplicaciones **Restringir la transferencia de contenido web con otras aplicaciones** para que sea una de las siguientes:

- Cualquier aplicación
- Intune Managed Browser
- Microsoft Edge
- Explorador no administrado 

Al seleccionar **Microsoft Edge**, los usuarios finales verán que la mensajería de acceso condicional les notifica que Microsoft Edge es necesario para escenarios de exploración administrados. Se les pedirá que descarguen e inicien sesión en Microsoft Edge con sus cuentas de AAD, si todavía no lo han hecho.  Este será el equivalente a tener como destino las aplicaciones habilitadas para MAM con la configuración de la aplicación `com.microsoft.intune.useEdge` establecida en **true**. Las directivas de protección de aplicaciones existentes en las que se usaba la opción **Exploradores administrados por directivas** ahora tendrán **Intune Managed Browser** seleccionado y no verá ningún cambio de comportamiento. Esto significa que los usuarios verán mensajes para usar Microsoft Edge si ha establecido la opción de configuración de la aplicación **useEdge** en **true**. Animamos a todos los clientes que aprovechan los escenarios de exploración administrados para actualizar sus directivas de protección de aplicaciones con **Restringir la transferencia de contenido web con otras aplicaciones** para asegurarse de que los usuarios vean las instrucciones adecuadas para realizar la transición a Microsoft Edge, con independencia de la aplicación desde la que inicien los vínculos. 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>Configuración del contenido de las notificaciones de una aplicación para las cuentas de organización<!-- 2576686  -->
Las directivas de protección de aplicaciones (APP) de Intune en dispositivos iOS y Android permiten controlar el contenido de las notificaciones de una aplicación para las cuentas de organización. Puede seleccionar una opción (permitir, bloquear datos de la organización o bloqueado) para especificar cómo se muestran las notificaciones de las cuentas de la organización para la aplicación seleccionada. Esta característica requiere compatibilidad de las aplicaciones y puede que no esté disponible para todas las aplicaciones habilitadas para la aplicación. Outlook para iOS versión 4.15.0 (o posterior) y Outlook para Android 4.83.0 (o posterior) serán compatibles con esta configuración. La configuración está disponible en la consola, pero la funcionalidad entrará en vigor después del 16 de diciembre de 2019. Consulte [¿Qué son las directivas de protección de aplicaciones?](../apps/app-protection-policy.md) para obtener más información sobre APP.

#### <a name="microsoft-app-icons-update--4677605----"></a>Actualización de los iconos de las aplicaciones de Microsoft<!--4677605  -->
Se han actualizado los iconos que se usan para las aplicaciones de Microsoft en el panel de la aplicación objetivo para las directivas de protección de aplicaciones y las directivas de configuración de aplicaciones.

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>Requerir el uso de teclados aprobados en Android<!--4761794  -->
Como parte de una directiva de protección de aplicaciones, puede especificar la configuración [**Teclados aprobados**](../apps/app-protection-policy-settings-android.md#data-protection) para administrar los teclados Android que se pueden usar con aplicaciones Android administradas. Cuando un usuario abra la aplicación administrada y aún no use un teclado aprobado para esa aplicación, se le pedirá que cambie a uno de los teclados aprobados que ya están instalados en el dispositivo. Si es necesario, verá un vínculo para descargar un teclado aprobado en Google Play Store, que puede instalar y configurar. El usuario solo puede editar campos de texto en una aplicación administrada cuando su teclado activo no sea uno de los teclados aprobados.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>Experiencia de inicio de sesión único actualizada para aplicaciones y sitios web en dispositivos iOS, iPadOS y macOS<!-- 4999578  -->
Intune agregó una configuración de inicio de sesión único (SSO) para dispositivos iOS, iPadOS y macOS. Ahora puede configurar las extensiones de aplicación de SSO de redireccionamiento escritas por su organización o por el proveedor de identidades. Use estas opciones para configurar una experiencia de inicio de sesión único sin problemas para aplicaciones y sitios web que usan métodos de autenticación modernos, como OAuth y SAML2. 

Estas nuevas opciones expanden la configuración anterior de las extensiones de aplicación SSO y la extensión Kerberos integrada de Apple (**Dispositivos** > **Configuración del dispositivo** > **Perfiles** > **Crear perfil** > **iOS/iPadOS** o **macOS** para el tipo de plataforma > **Características del dispositivo** para el tipo de perfil). 

Para ver todas las opciones de la extensión de aplicación SSO que puede configurar, vaya a [SSO en iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) y [SSO en macOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Se aplica a:

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>Actualizamos dos opciones de restricción de dispositivos para dispositivos iOS e iPados para corregir su comportamiento<!-- 5701352    -->
En los dispositivos iOS, puede crear los perfiles de restricción de dispositivos **Permitir actualizaciones móviles de PKI** y **Bloqueo del modo restringido de USB** (**Dispositivos** > **Configuración del dispositivo** > **Perfiles** > **Crear perfil** > **iOS/iPadOS** para la plataforma > **Restricciones de dispositivos** para el tipo de perfil). Antes de esta versión, la configuración de la interfaz de usuario y las descripciones de las siguientes opciones no eran correctas, algo que ahora se corrigió. A partir de esta versión, el comportamiento de la configuración es el siguiente:

**Bloquear actualizaciones móviles de PKI**: **Bloquear** impide que los usuarios reciban actualizaciones de software, a menos que el dispositivo esté conectado a un equipo. **No configurado** (valor predeterminado): permite que un dispositivo reciba actualizaciones de software sin estar conectado a un equipo.
- Anteriormente, esta configuración le permitía configurarla como: **Permitir**, que permite a los usuarios recibir actualizaciones de software sin tener que conectar los dispositivos a un equipo.
**Permitir accesorios USB con el dispositivo bloqueado**: **Permitir** permite que los accesorios USB intercambien datos con un dispositivo que ha estado bloqueado durante más de una hora. **No configurado** (valor predeterminado) no actualiza el modo restringido de USB en el dispositivo y los accesorios USB no podrán transferir datos del dispositivo si están bloqueados durante más de una hora.
- Anteriormente, esta configuración le permitía configurarla como: **Bloquear** para deshabilitar el modo restringido de USB en los dispositivos supervisados.

Para más información sobre los valores que puede configurar, consulte [Configuración de dispositivos iOS e iPadOS para permitir o restringir características mediante Intune](../configuration/device-restrictions-ios.md).

Esta característica se aplica a:

- OS/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Perfiles de configuración de dispositivos de red cableada para dispositivos macOS<!-- 3508686  -->
   > [!NOTE]
   > Esta característica se ha retrasado, pero se publicará pronto.

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>Impedir que los usuarios configuren las credenciales de certificado en el almacén de claves administrado en dispositivos propietarios de dispositivos Android Enterprise<!-- 3311998 -->
En dispositivos propietarios de dispositivos Android Enterprise, puede establecer una nueva configuración que impide que los usuarios configuren sus credenciales de certificado en el almacén de claves administrado (**Configuración del dispositivo** > **Perfiles** > **Crear perfil** > **Android Enterprise** para la plataforma > **Solo el propietario del dispositivo > Restricciones de dispositivos** para el tipo de perfil > **Users + Accounts** [Usuarios y cuentas]).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="protected-wipe-action-now-available--51150000---"></a>La acción de borrado protegido ya está disponible<!--51150000 -->
Ahora tiene la opción de usar la acción Borrar dispositivo para realizar el borrado protegido de un dispositivo. Los borradores protegidos equivalen a los borrados estándar, salvo que no se pueden eludir apagando el dispositivo. Un borrado protegido seguirá intentando restablecer el dispositivo hasta que se complete de forma correcta. En algunas configuraciones, esta acción puede hacer que el dispositivo no se pueda reiniciar. Para más información, consulte [Retirada o borrado de los dispositivos](../remote-actions/devices-wipe.md).

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>Dirección MAC de Ethernet de un dispositivo agregada a la página Información general del dispositivo<!--5562275 -->
Ahora puede ver la dirección MAC de Ethernet de un dispositivo en la página de detalles del dispositivo (**Dispositivos** > **Todos los dispositivos** > elija un dispositivo > **Información general**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>Experiencia mejorada en un dispositivo compartido cuando se habilitan las directivas de acceso condicional basadas en el dispositivo<!-- 1734096  -->
Mejoramos la experiencia en un dispositivo compartido con varios usuarios a los que se les aplica la directiva de acceso condicional basada en los dispositivos mediante la comprobación de la evaluación de cumplimiento más reciente para el usuario al aplicar la directiva. Para más información, consulte estos artículos de información general:
- [Información general de Azure sobre el Acceso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Información general sobre el cumplimiento de los dispositivos de Intune](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>Uso de perfiles de certificado PKCS para aprovisionar dispositivos con certificados<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
Ahora puede usar perfiles de certificado PKCS para emitir certificados a *dispositivos* que ejecuten Android for Work, iOS/iPadOS y Windows, cuando estén asociados a perfiles como los de Wi-Fi y VPN. Anteriormente, estas tres plataformas solo admitían certificados basados en el usuario, con la compatibilidad basada en dispositivos limitada a macOS.

> [!NOTE]
> No se admiten los perfiles de certificado PKCS con perfiles Wi-FI. En su lugar, use perfiles de certificado SCEP cuando use un [tipo EAP](../configuration/wi-fi-settings-windows.md#enterprise-profile).

Para usar un certificado basado en dispositivos, al [crear un perfil de certificado PKCS](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) para las plataformas admitidas, seleccione **Configuración**. Ahora verá el valor de **Tipo de certificado**, que admite las opciones de dispositivo o usuario.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="centralized-audit-logs--5603185-5697164---"></a>Registros de auditoría centralizados<!--5603185, 5697164 -->
Una nueva experiencia de registros de auditoría centralizados ahora recopila los registros de auditoría de todas las categorías en una sola página. Puede filtrar los registros para obtener los datos que está buscando. Para ver los registros de auditoría, vaya a **Administración de inquilinos** > **Registros de auditoría**. 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>Información de etiqueta de ámbito incluida en los detalles de la actividad de registro de auditoría<!--5763534 -->
Los detalles de la actividad de registro de auditoría ahora incluyen información de etiqueta de ámbito (para los objetos de Intune que admiten etiquetas de ámbito). Para más información sobre los registros de auditoría, consulte [Uso de registros de auditoría para realizar un seguimiento de los eventos y supervisarlos](monitor-audit-logs.md).

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>Semana del 2 de diciembre de 2019

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>Nueva licencia de administración conjunta de Microsoft Endpoint Configuration Manager<!--5027281-->
Los clientes de Configuration Manager con Software Assurance pueden obtener la administración conjunta de Intune para equipos con Windows 10 sin tener que comprar una licencia de Intune adicional para la administración conjunta. Los clientes ya no necesitan asignar licencias de Intune y EMS individuales a los usuarios finales para la administración conjunta de Windows 10.
- Los dispositivos administrados por Configuration Manager e inscritos en la administración conjunta tienen casi los mismos derechos que los equipos administrados por MDM de Intune independiente. Pero después de restablecerlos, no se pueden volver a aprovisionar con Autopilot.
- Los dispositivos Windows 10 inscritos en Intune mediante otros medios requieren licencias completas de Intune.
- Los dispositivos de otras plataformas siguen requiriendo licencias de Intune completas.

Para más información, vea [Términos de Licencia](https://www.microsoft.com/en-us/Licensing/product-licensing/products).

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>Semana del 18 de noviembre de 2019 (versión del servicio 1911)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>Actualización de la interfaz de usuario al borrar datos de la aplicación de forma selectiva<!-- 4102028 -->
La interfaz de usuario para borrar selectivamente los datos de la aplicación en Intune se ha actualizado. Los cambios de la UI son:
- Una experiencia más sencilla, dado el uso de un formato de tipo asistente condensado dentro de un panel.
- Una actualización del flujo de creación para incluir asignaciones.
- Una página de resumen de todos los elementos establecidos al ver las propiedades, antes de crear una nueva directiva o al editar una propiedad. Además, al editar las propiedades, el resumen solo mostrará una lista de elementos de la categoría de propiedades que se están editando.

Para obtener más información, consulte [Borrado solo de datos corporativos de aplicaciones administradas por Intune](../apps/apps-selective-wipe.md).

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>Compatibilidad con el teclado de terceros de iOS y iPadOS<!-- 4922950 -->
En marzo de 2019, anunciamos el fin del la compatibilidad del parámetro de la directiva de protección de aplicaciones de iOS "Teclados de terceros". La característica está de vuelta en Intune con compatibilidad tanto con iOS como con iPadOS. Para habilitar esta configuración, visite la pestaña **Protección de datos** de una directiva de protección de aplicaciones iOS/iPadOS nueva o existente y busque la opción **Teclados de terceros** en **Transferencia de datos**.

El comportamiento de esta configuración de directiva difiere ligeramente de la implementación anterior. En las aplicaciones de varias identidades que usan la versión de SDK 12.0.16 y versiones posteriores que son el destino de directivas de protección de aplicaciones con esta opción configurada en **Bloquear**, los usuarios finales no podrán elegir los teclados de terceros en sus cuentas personales y de organización. Las aplicaciones que usan versiones de SDK 12.0.12 y anteriores seguirán mostrando el comportamiento documentado en la entrada de blog que lleva por título [Problema conocido: Los teclados de terceros no se bloquean en iOS para cuentas personales](https://aka.ms/3rdparty_iOS_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>Requerimiento de administración de Jamf a grupos de usuarios de macOS<!-- 4061739  --> 
Puede dirigirse a grupos específicos de usuarios cuyos [dispositivos macOS serán administrados por Jamf](../protect/conditional-access-integrate-jamf.md). Esto le permite aplicar la integración de cumplimiento de Jamf a un subconjunto de dispositivos macOS mientras que otros dispositivos se administran mediante Intune. Si ya usa la integración de Jamf, la integración se destinará a todos los usuarios de manera predeterminada.

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>Nueva configuración de Exchange ActiveSync al crear un perfil de configuración de dispositivo de correo electrónico en dispositivos iOS<!-- 4892824   --> 
En dispositivos iOS/iPadOS, puede configurar la conectividad del correo electrónico en un perfil de configuración de dispositivos (**Configuración de dispositivos** > **Perfiles** > **Crear perfil** > **iOS/iPadOS** como plataforma > **Correo electrónico** para tipo de perfil). 

Hay nuevas opciones de configuración de Exchange ActiveSync disponibles, entre las que se incluyen:
- **Datos de Exchange para sincronizar**: elija los servicios de Exchange que se sincronizarán (o cuya sincronización se bloqueará) con el calendario, los contactos, los recordatorios, las notas y el correo electrónico.
- **Permitir a los usuarios cambiar la configuración de sincronización**: permita (o impida) a los usuarios cambiar la configuración de sincronización para estos servicios en sus dispositivos.  

Para obtener más información sobre esta configuración, vaya a [Incorporación de la configuración de correo electrónico para dispositivos iOS en Microsoft Intune](../configuration/email-settings-ios.md). 

Se aplica a:

- iOS 13.0 y versiones más recientes
- IPadOS 13.0 y versiones más recientes

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>Evitación de que los usuarios agreguen cuentas personales de Google a dispositivos Android Enterprise dedicados y totalmente administrados<!-- 5353228   -->
En los dispositivos Android Enterprise dedicados y totalmente administrados, hay una nueva opción que impide que los usuarios creen cuentas de Google personales (**Configuración de dispositivos** > **Perfiles** > **Crear perfil** > **Android Enterprise** para plataforma > **Solo el propietario del dispositivo > Restricciones de dispositivos** para tipo de perfil > **configuración de Usuarios y cuentas** > **Cuentas personales de Google**).

Para ver los valores que puede configurar, vaya a [Configuración de dispositivos Android Enterprise para permitir o restringir características mediante Intune](../configuration/device-restrictions-android-for-work.md).

Se aplica a:

- Dispositivos totalmente administrados de Android Enterprise
- Dispositivos Android Enterprise dedicados

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>Eliminación del parámetro de registro del servidor para los comandos de Siri en el perfil de restricciones de dispositivos de iOS/iPadOS <!-- 5468501   -->
En dispositivos iOS y iPadOS, el parámetro **Registro del servidor para los comandos de Siri** se ha quitado de la consola de administración de Microsoft Endpoint Manager (**Configuración de dispositivo** > **Perfiles** > **Crear perfil** > **iOS/iPadOS** para plataforma &gt; **Restricciones de dispositivos** para tipo de perfil &gt; **Aplicaciones integradas**). 

Esta configuración no tiene ningún efecto en los dispositivos. Para quitar el parámetro de los perfiles existentes, abra el perfil, realice cualquier cambio y, a continuación, guarde el perfil. El perfil se actualiza y la configuración se elimina de los dispositivos.

Para ver todos los valores que puede configurar, vea [Configuración de dispositivos iOS y iPadOS para permitir o restringir características mediante Intune](../configuration/device-restrictions-ios.md).

Se aplica a:

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Actualizaciones de características de Windows 10 (versión preliminar pública)<!-- 2384877 -->
Ahora puede implementar [actualizaciones de características de Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) en dispositivos Windows 10. Las actualizaciones de características de Windows 10 son una nueva directiva de actualización de software que establece la versión de Windows 10 que desea que se instale y permanezca en los dispositivos. Puede usar este nuevo tipo de directiva junto con los anillos de actualización de Windows 10 existentes.

Los dispositivos que reciben la directiva de actualizaciones de características de Windows 10 instalarán la versión especificada de Windows y, a continuación, permanecerán con esa versión hasta que se edite o se quite la directiva. Los dispositivos que ejecutan una versión posterior de Windows permanecen en su versión actual. Los dispositivos que se encuentran en una versión específica de Windows pueden seguir instalando actualizaciones de calidad y seguridad para esa versión desde los anillos de actualización de Windows 10.

Este nuevo tipo de directiva comienza a implementarse en los inquilinos esta semana. Si esta directiva todavía no está disponible para el inquilino, lo estará pronto.

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>Adición y cambio de información clave en archivos PLIST para aplicaciones macOS<!-- 4736278 -->
En los dispositivos macOS, ahora puede crear un perfil de configuración de dispositivos que cargue un archivo de lista de propiedades (. plist) asociado a una aplicación o el dispositivo (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** para la plataforma > **Archivo de preferencias** para el tipo de perfil).

Solo algunas aplicaciones admiten preferencias administradas, y es posible que estas aplicaciones no le permitan administrar toda la configuración. Asegúrese de cargar un archivo de lista de propiedades que configure los valores del canal del dispositivo, no la configuración del canal del usuario.

Para obtener más información sobre esta característica, consulte [Adición de un archivo de lista de propiedades a dispositivos macOS mediante Microsoft Intune](../configuration/preference-file-settings-macos.md).

Se aplica a:

- dispositivos macOS con 10.7 y versiones más recientes

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>Edición del valor de nombre de dispositivo para dispositivos Autopilot<!-- 2640074 -->
Puede editar el valor del nombre de dispositivo para los dispositivos Autopilot unidos a Azure AD.  Para obtener más información, consulte [Edición de atributos de dispositivo Autopilot](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>Edición del valor de etiqueta de grupo para dispositivos Autopilot<!-- 4816775   -->
Puede editar el valor Etiqueta de grupo para dispositivos Autopilot. Para obtener más información, consulte [Edición de atributos de dispositivo Autopilot](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="updated-support-experience---5012398---"></a>Experiencia de soporte técnico actualizada<!-- 5012398 -->

A partir de hoy, se está implantando en los inquilinos una experiencia actualizada y simplificada en la consola para [obtener ayuda y soporte técnico para Intune](get-support.md). Si esta experiencia todavía no está disponible para usted, lo estará pronto.

Se ha mejorado la búsqueda en la consola, los comentarios de incidencias comunes y el flujo de trabajo que se usa para ponerse en contacto con el servicio de soporte técnico. Al abrir una incidencia de soporte técnico, verá estimaciones en tiempo real de cuándo pueda esperar una devolución de llamada o una respuesta por correo electrónico; los clientes de soporte técnico Premier y Unified pueden especificar fácilmente la gravedad de su incidencia con el fin de obtener soporte técnico más rápido.

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>Mejora de la experiencia de informes de Intune (versión preliminar pública) <!-- 3791418 -->
Intune ahora proporciona una experiencia de informes mejorada, con nuevos tipos de informes, una mejor organización de informes, vistas más centradas y una funcionalidad de informes más eficiente, así como datos más coherentes y precisos. Los nuevos tipos de informe se centran en lo siguientes aspectos:

- **Operativo**: proporciona registros nuevos con un enfoque de estado negativo. 
- **Organizativo**: proporciona un resumen más amplio del estado general.
- **Histórico**: proporciona patrones y tendencias a lo largo de un período de tiempo.
- **Especialista**: le permite usar datos sin procesar para crear sus propios informes personalizados.

El primer conjunto de informes nuevos se centra en el cumplimiento de los dispositivos. Para obtener más información, vea [Blog:marco de creación de informes de Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) e [Informes de Intune](reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Control de acceso basado en roles.

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>Duplicación de roles personalizados o integrados <!-- 1081938   -->
Ahora puede copiar tanto roles integrados como roles personalizados. Para obtener más información, vea [Copia de un rol](../fundamentals/create-custom-role.md#copy-a-role).

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>Nuevos permisos para el rol de administrador escolar <!-- 5621805  -->  
Se han agregado dos nuevos permisos, **Asignar perfil** y **Sincronizar dispositivo**, al rol de administrador escolar > **Permisos** > **Programas de inscripción**. El permiso de sincronizar perfil permite a los administradores de grupos sincronizar dispositivos Windows Autopilot. El permiso de asignar perfil les permite eliminar perfiles de inscripción de Apple iniciados por el usuario. También les concede permiso para administrar las asignaciones de dispositivos Autopilot y las asignaciones del perfil de implementación de Autopilot. Para obtener una lista de todos los permisos de administrador de grupo y administrador escolar, consulte [Asignación de un grupo de administración](https://docs.microsoft.com/intune-education/group-admin-delegate).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Seguridad

#### <a name="bitlocker-key-rotation---2564951----"></a>Rotación de clave de BitLocker<!-- 2564951  -->
Puede usar una acción de dispositivo de Intune para [rotar de forma remota las claves de recuperación de BitLocker](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) para dispositivos administrados que ejecutan la versión 1909 o posterior de Windows. Para que se puedan rotar las claves de recuperación, los dispositivos deben configurarse para admitir la rotación de claves de recuperación.  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>Actualizaciones en la inscripción de dispositivos dedicada para admitir la implementación de certificados de dispositivos SCEP <!-- 5198878  -->
Intune ahora admite la implementación de certificados de dispositivos SCEP en dispositivos Android Enterprise dedicados para permitir el acceso basado en certificados a los perfiles de Wi-Fi. La aplicación Microsoft Intune debe estar presente en el dispositivo para que funcione la implementación. Como resultado, hemos actualizado la experiencia de inscripción para dispositivos Android Enterprise dedicados. Las nuevas inscripciones siguen empezando de la misma manera (con QR, NFC, sin interacción o con identificador de dispositivo) pero ahora tienen un paso que requiere que los usuarios instalen la aplicación Intune. Los dispositivos existentes comenzarán a instalar la aplicación automáticamente de manera gradual.

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>Registros de auditoría de Intune para colaboración de negocio a negocio<!--5670211 -->
La colaboración de negocio a negocio (B2B) le permite compartir de forma segura las aplicaciones y los servicios de la empresa con usuarios invitados de cualquier otra organización, manteniendo al mismo tiempo el control sobre sus propios datos corporativos. Intune ahora admite registros de auditoría para usuarios invitados de B2B. Por ejemplo, cuando los usuarios invitados realizan cambios, Intune podrá capturar estos datos a través de registros de auditoría. Para obtener más información, consulte [¿Qué es el acceso de usuarios invitados en Azure Active Directory B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>Semana del 11 de noviembre de 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>Experiencia mejorada de inscripción de macOS en el Portal de empresa <!-- 5074349  -->  
La experiencia de inscripción del Portal de empresa para macOS cuenta con un proceso de inscripción más sencillo que es más coherente con la experiencia de inscripción en el Portal de empresa para iOS. Los usuarios del dispositivo ahora ven lo siguiente:  

- Una interfaz de usuario más elegante.  
- Una lista de comprobación de inscripción mejorada.  
- Instrucciones más claras sobre cómo inscribir sus dispositivos.  
- Mejores opciones de solución de problemas.  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>Aplicaciones web iniciadas desde la aplicación Portal de empresa de Windows<!-- 5030972 -->
Los usuarios finales ahora pueden iniciar aplicaciones web directamente desde la aplicación Portal de empresa de Windows. Los usuarios finales pueden seleccionar la aplicación web y, a continuación, elegir la opción **Abrir en el explorador**. La dirección URL web publicada se abre directamente en un explorador web. Esta funcionalidad se implementará durante la próxima semana. Para más información sobre las aplicaciones web, consulte[Agregar aplicaciones web a Microsoft Intune](../apps/web-app.md).  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Nueva columna de tipo de asignación en el Portal de empresa para Windows 10 <!-- 5459950  -->
Se ha cambiado el nombre de la columna Portal de empresa > **Aplicaciones instaladas** > **Tipo de asignación** a **Requerida por la organización**.  En esa columna, los usuarios verán un valor de **Sí** o **No** para indicar si una aplicación es obligatoria o es opcional para su organización. La razón de estos cambios es la confusión que despertaba en los usuarios de los dispositivos el concepto de aplicaciones disponibles. Los usuarios pueden obtener más información sobre cómo instalar aplicaciones en el Portal de empresa en [Instalar y compartir aplicaciones en el dispositivo](../user-help/install-apps-cpapp-windows.md). Para obtener más información sobre cómo configurar la aplicación Portal de empresa para sus usuarios, vea [Configuración de la aplicación Portal de empresa de Microsoft Intune](../apps/company-portal-app.md).  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>Semana del 4 de noviembre de 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Las líneas de base de seguridad se admiten en Microsoft Azure Government<!-- 4062552 -->

Las instancias de Intune que se hospedan en *Microsoft Azure Government* ahora pueden usar [líneas base de seguridad](../protect/security-baselines.md) para ayudarle a proteger sus usuarios y dispositivos.

## <a name="whats-new-archive"></a>Archivo de novedades
Para ver los meses anteriores, consulte el [archivo de novedades](whats-new-archive.md).

## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


