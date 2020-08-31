---
title: Novedades de Microsoft Intune (Azure) | Microsoft Docs
titleSuffix: ''
description: Descubra las novedades del portal de Intune Azure
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
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
ms.openlocfilehash: aa6839cef79623b456cd31eec6b894eae7687de3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820279"
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
### Role-based access control
### Scripts

<!-- ########################## -->
## <a name="week-of-august-24-2020-2008-service-release"></a>Semana del 24 de agosto de 2020 (versión del servicio 2008)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322----"></a>Revocación de licencias asociadas revocadas antes de eliminar el token de VPP de Apple<!--6195322  -->
Cuando se elimina un token de VPP de Apple en Microsoft Endpoint Manager, todas las licencias asignadas por Intune asociadas a ese token se revocarán automáticamente antes de la eliminación.

#### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-shows-descriptions----7414768-wnstaged---"></a>Mejora en la página Actualizar configuración del dispositivo de la aplicación Portal de empresa para Android para mostrar descripciones <!-- 7414768 wnstaged -->
En la aplicación Portal de empresa de dispositivos Android, en la página **Actualizar configuración del dispositivo** se muestra la configuración que debe actualizar un usuario para que sea compatible. Los usuarios expanden el problema para ver más información y verán el botón **Resolver**.

Esta experiencia del usuario se ha mejorado. Las opciones enumeradas se expanden de forma predeterminada para mostrar la descripción y el botón **Resolver**, cuando proceda. Anteriormente, los problemas estaban contraídos de forma predeterminada. Este nuevo comportamiento predeterminado reduce el número de clics, por lo que los usuarios pueden resolver los problemas más rápidamente.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631-----"></a>Uso de NetMotion como un tipo de conexión de VPN para dispositivos iOS/iPadOS y macOS<!-- 1333631   -->
Al crear un perfil de VPN, NetMotion está disponible como tipo de conexión VPN (**Dispositivos** > **Configuración de dispositivos** > **Crear perfil** > **iOS/iPadOS** o **macOS** para plataforma > **VPN** para perfil > **NetMotion** para tipo de conexión).

Para obtener más información sobre los perfiles de VPN en Intune, consulte [Creación de perfiles de VPN para conectarse a servidores VPN](../configuration/vpn-settings-configure.md).

Se aplica a:
- iOS/iPadOS
- macOS

#### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024----"></a>Más opciones del protocolo de autenticación extensible protegido (PEAP) para perfiles Wi-Fi de Windows 10<!-- 3805024  -->
En los dispositivos Windows 10, puede crear perfiles de Wi-Fi con el protocolo de autenticación extensible (EAP) para autenticar las conexiones Wi-Fi (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Windows 10 y posteriores** para plataforma > **Wi-Fi** para perfil > **Empresa**).

Al seleccionar EAP protegido (PEAP), hay nuevas opciones de configuración disponibles:
- **Realizar validación del servidor en PEAP fase 1**: En la fase 1 de negociación PEAP, el servidor se comprueba mediante la validación del certificado.
  - **Deshabilitar los mensajes de usuario para la validación del servidor en PEAP fase 1**: en la fase 1 de la negociación de PEAP, no se muestran los mensajes de usuario que soliciten autorizar nuevos servidores PEAP para entidades de certificación de confianza.
- **Requerir enlace criptográfico**: impide las conexiones a servidores PEAP que no utilizan el enlace criptográfico durante la negociación PEAP.

Para ver la configuración que puede realizar, vaya a [Agregar Wi-Fi para dispositivos Windows 10 y versiones posteriores en Intune](../configuration/wi-fi-settings-windows.md).

Se aplica a: 
- Windows 10 y versiones posteriores

#### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576--idstaged---"></a>Configuración del complemento Microsoft Enterprise SSO de macOS<!-- 5627576  idstaged -->
El equipo de Microsoft Azure AD creó una extensión de aplicación de inicio de sesión único (SSO) de redireccionamiento que permite a los usuarios de macOS 10.15 + obtener acceso con un inicio de sesión a las aplicaciones de Microsoft, a las aplicaciones de la organización y a los sitios web que admiten la característica SSO de Apple y que se autentican mediante Azure AD. Con la versión del complemento Microsoft Enterprise SSO, puede configurar la extensión de SSO con el nuevo tipo de extensión de aplicación de Microsoft Azure AD (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** para plataforma > **Características del dispositivo** para perfil > **Extensión de aplicación de inicio de sesión único** > tipo de extensión de aplicación de SSO > **Microsoft Azure AD**).

Para lograr el SSO con el tipo de extensión de aplicación de SSO de Microsoft Azure AD, los usuarios deben instalar la aplicación de Portal de empresa en sus dispositivos macOS e iniciar sesión en ella. 

Para obtener más información sobre las extensiones de aplicación de SSO de macOS, consulte [Extensión de aplicación de inicio de sesión único](../configuration/device-features-configure.md#single-sign-on-app-extension).

Se aplica a:
- macOS 10.15 y versiones más recientes

#### <a name="prevent-users-from-unlocking-android-enterprise-work-profile-devices-using-face-and-iris-scanning--6069759-idmiss---"></a>Impedir que los usuarios desbloqueen dispositivos de perfil de trabajo de Android Enterprise mediante examen facial y del iris<!--6069759 idmiss -->
Ahora puede evitar que los usuarios usen el examen facial o del iris para desbloquear sus dispositivos administrados de perfil de trabajo, ya sea en el nivel de dispositivo o en el nivel de perfil de trabajo. Esta opción se puede establecer en las secciones **Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** para la plataforma > **Perfil de trabajo > Restricciones de dispositivos** para el perfil > **Configuración del perfil profesional** y **Contraseña**.

Para más información, consulte [Configuración de dispositivos Android Enterprise para permitir o restringir características mediante Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Se aplica a: 
- Perfil de trabajo de Android Enterprise

#### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991----"></a>Uso de extensiones de aplicación de SSO en más aplicaciones iOS/iPadOS con el complemento de Microsoft Enterprise SSO<!-- 7369991  -->
El complemento [Microsoft Enterprise SSO para dispositivos Apple](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) se puede usar con todas las aplicaciones que admiten las extensiones de aplicación SSO. En Intune, esta característica significa que el complemento funciona con aplicaciones móviles iOS/iPadOS que no usan la biblioteca de autenticación de Microsoft (MSAL) para dispositivos Apple. Las aplicaciones no necesitan usar MSAL, pero tienen que autenticarse con puntos de conexión de Azure AD.

Para configurar las aplicaciones de iOS/iPadOS para usar SSO con el complemento, agregue los identificadores de lote de aplicaciones en un perfil de configuración de iOS/iPadOS (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para plataforma > **Características del dispositivo** para perfil > **Extensión de aplicación de inicio de sesión único** > **Microsoft Azure AD** > para tipo de extensión de aplicación de SSO > **Identificadores de lote de las aplicaciones**).

Para ver la configuración actual de la extensión de la aplicación de SSO que puede configurar, vaya a [Extensión de aplicación de inicio de sesión único](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Se aplica a:
- iOS/iPadOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="deploy-endpoint-security-antivirus-policy-to-tenant-attached-devices-preview---5475441----"></a>Implementación de la directiva de antivirus de seguridad de punto de conexión en dispositivos con asociación de inquilinos (versión preliminar)<!-- 5475441  -->
Como versión preliminar, puede implementar la [directiva de antivirus](../protect/endpoint-security-antivirus-policy.md) de seguridad de punto de conexión en los dispositivos que se administran con Configuration Manager. Para hacer posible este escenario, es necesario configurar una asociación de inquilinos entre una versión admitida de Configuration Manager y la suscripción de Intune. Se admiten las siguientes versiones de Configuration Manager:

- Versión 2006 de la rama actual de Configuration Manager

Para más información, consulte los [requisitos de las directivas de seguridad de punto de conexión de Intune](../protect/tenant-attach-intune.md#specific-requirements-for-intune-endpoint-security-policies) para admitir la asociación de inquilinos.

#### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119------"></a>Cambios para las exclusiones de la directiva de antivirus para la seguridad de los puntos de conexión<!--5583940, 6018119    -->
Se han introducido dos cambios en la administración de las listas de exclusión de Antivirus de Microsoft Defender que se configuran como parte de una [directiva de antivirus de seguridad de punto de conexión](../protect/endpoint-security-antivirus-policy.md). Los cambios le ayudan a evitar conflictos entre las distintas directivas y a resolver aquellos relacionados con las listas de exclusión que podrían existir en las directivas previamente implementadas.

Ambos cambios se aplican a la configuración de directiva de los siguientes [proveedores de servicios de configuración de Antivirus de Microsoft Defender](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions) (CSP):

- Defender/ExcludedPaths
- Defender/ExcludedExtensions
- Defender/ExcludedProcesses

Los cambios son:

- Nuevo tipo de perfil: **Exclusiones del Antivirus de Microsoft Defender**: use este nuevo tipo de perfil para Windows 10 y versiones posteriores para definir una directiva que se centre únicamente en las exclusiones del antivirus. Este perfil puede ayudarle a simplificar la administración de las listas de exclusión separándolas de otras configuraciones de directiva.

  Entre las exclusiones que se pueden configurar se incluyen los *procesos*, las *extensiones de archivos* y los *archivos* y *carpetas* de Defender que no quiere que examine Microsoft Defender.

- **Combinación de directivas**: Intune ahora combina la lista de exclusiones que ha definido en perfiles independientes en una única lista de exclusiones que se aplicarán a cada dispositivo o usuario. Por ejemplo, en el caso de un usuario con tres directivas independientes, las listas de exclusión de esas tres directivas se combinan en un único superconjunto de *exclusiones de antivirus de Microsoft Defender*, que se aplican de este modo al usuario.


<!-- ########################## -->
## <a name="week-of-august-17-2020"></a>Semana del 17 de agosto de 2020

### <a name="intune-apps"></a>Aplicaciones de Intune

#### <a name="custom-brand-image-now-displayed-in-the-windows-company-portal-profile-page---4280187---"></a>La imagen de marca personalizada se muestra ahora en la página del perfil del Portal de empresa de Windows<!-- 4280187 -->
Como administrador de Microsoft Intune, puede cargar una imagen de marca personalizada en Intune que se mostrará como imagen de fondo en la página de perfil del usuario en la aplicación del Portal de empresa de Windows. Para más información, consulte [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md#branding).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>El Portal de empresa agrega compatibilidad con las aplicaciones de Configuration Manager<!-- 4297660 -->
El Portal de empresa ahora admite aplicaciones de Configuration Manager. Esta característica permite a los usuarios finales ver las aplicaciones implementadas de Configuration Manager y de Intune en el Portal de empresa de los clientes administrados conjuntamente. Esta compatibilidad ayuda a los administradores a consolidar sus diferentes experiencias del portal de usuario final. Para más información, consulte [Uso de la aplicación Portal de empresa en dispositivos administrados conjuntamente](/mem/configmgr/comanage/company-portal). 

### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="set-device-compliance-state-from-third-party-mdm-providers---6361689---"></a>Establecimiento del estado de cumplimiento del dispositivo desde proveedores de MDM de terceros<!-- 6361689 -->

Intune admite ahora [soluciones MDM de terceros como origen de detalles de cumplimiento de dispositivos](../protect/device-compliance-partners.md). Estos datos de cumplimiento de terceros se pueden usar para aplicar directivas de acceso condicional a aplicaciones de Microsoft 365 en iOS y Android gracias a la integración con Microsoft Intune.  Intune evalúa los detalles de cumplimiento del proveedor de terceros para determinar si un dispositivo es de confianza y, luego, establece los atributos de acceso condicional en Azure AD.  Para continuar, se crearán las directivas de acceso condicional de Azure AD desde el centro de administración de Microsoft Endpoint Manager o el portal de Azure AD.

En esta versión, se admiten los siguientes proveedores de MDM de terceros, como una versión preliminar pública:

- VMWare Workspace ONE UEM (antes conocido como AirWatch)

*Esta actualización se va a implementar en los clientes globalmente. Esta funcionalidad aparecerá la próxima semana.*

<!-- ########################## -->
## <a name="week-of-august-10-2020"></a>Semana del 10 de agosto de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="tenant-attach-install-an-application-from-the-admin-center----in7220536-cm6024389--"></a>Asociación de inquilinos: instalación de una aplicación desde el centro de administración <!-- IN7220536 CM6024389-->
Ahora puede iniciar la instalación de una aplicación en tiempo real para un dispositivo asociado al inquilino desde el centro de administración de Microsoft Endpoint Manager. Para más información, consulte [Asociación de inquilinos: instalación de una aplicación desde el centro de administración](../../configmgr/tenant-attach/applications.md).

<!-- ########################## -->
## <a name="week-of-july-27-2020"></a>Semana del 27 de julio de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="power-bi-compliance-report-template-v20---636958---"></a>Plantilla de informe de cumplimiento de Power BI V2.0<!-- 636958 -->
Las aplicaciones de plantilla de Power BI permiten a los asociados de Power BI compilar aplicaciones de Power BI con poca o ninguna programación e implementarlas en cualquier cliente de Power BI. Los administradores pueden actualizar la versión de la plantilla de informe de cumplimiento de Power BI de V1.0 a V2.0. En V2.0 se incluye un diseño mejorado, así como cambios en los cálculos y datos que se muestran como parte de la plantilla. Para obtener más información, vea [Conexión a Data Warehouse con Power BI](../developer/reports-proc-get-a-link-powerbi.md) y [Actualización de una aplicación de plantilla](https://docs.microsoft.com/power-bi/service-template-apps-install-distribute#update-a-template-app). Además, vea la entrada de blog [Anuncio de una nueva versión del informe de cumplimiento de Power BI con Data Warehouse de Intune](https://aka.ms/new_compliance_report).

<!-- ########################## -->
## <a name="week-of-july-13-2020--2007-service-release"></a>Semana del 13 de julio de 2020 (versión del servicio 2007)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="exchange-on-premises-connector-support---7138486----"></a>Compatibilidad con Exchange On-Premises Connector<!-- 7138486  -->
Intune está retirando la compatibilidad con la característica Exchange On-Premises Connector del servicio Intune a partir de la versión 2007 (julio). En este momento, los clientes existentes con un conector activo podrán continuar con la función actual. Los clientes nuevos y los existentes que no tengan un conector activo ya no podrán crear otros conectores ni administrar dispositivos de Exchange ActiveSync (EAS) desde Intune. En el caso de esos clientes, Microsoft recomienda el uso de la [autenticación moderna híbrida (HMA)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) de Exchange para proteger el acceso a Exchange local. HMA habilita las dos directivas de Intune App Protection (también conocidas como MAM) y el acceso condicional a través de Outlook Mobile para Exchange local.

#### <a name="smime-for-outlook-on-ios-and-android-devices-without-enrollment---6517155---"></a>S/MIME para Outlook en dispositivos iOS y Android sin inscripción<!-- 6517155 -->
Ahora se puede habilitar S/MIME para Outlook en dispositivos iOS y Android mediante la directiva de configuración de aplicaciones para aplicaciones administradas. Esto permite la entrega de directivas independientemente del estado de inscripción de los dispositivos. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** > **Aplicaciones administrados**. Además, puede elegir si quiere permitir que los usuarios cambien esta configuración en Outlook. Sin embargo, para implementar automáticamente certificados de S/MIME en Outlook para iOS y Android, el dispositivo debe estar inscrito. Para obtener información general sobre S/MIME, vea [Información general sobre S/MIME para firmar y cifrar el correo electrónico en Intune](https://docs.microsoft.com/mem/intune/protect/certificates-s-mime-encryption-sign). Para obtener más información sobre las opciones de configuración de Outlook, vea [Opciones de configuración de Microsoft Outlook](../apps/app-configuration-policies-outlook.md) y [Agregar directivas de configuración para aplicaciones administradas sin inscripción de dispositivos](../apps/app-configuration-policies-managed-app.md). Para obtener información sobre S/MIME en Outlook para iOS y Android, vea [Escenarios de S/MIME](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios) y [Claves de configuración: opciones de S/MIME](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122-----"></a>Nueva configuración de VPN para dispositivos Windows 10 y versiones más recientes<!-- 6602122   -->

Cuando se crea un perfil de VPN mediante el tipo de conexión de IKEv2, hay nuevas opciones que puede configurar(**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Windows 10 y posteriores** como plataforma > **VPN** para el perfil > **VPN base**):

- **Túnel de dispositivos**: Permite que los dispositivos se conecten automáticamente a VPN sin necesidad de interacción del usuario, incluido el inicio de sesión del usuario. Esta característica requiere que se habilite **Always On** y que se usen **certificados de máquina** como método de autenticación.
- Configuración de Cryptography Suite: Configure los algoritmos que se usan para proteger las asociaciones de seguridad IKE y secundarias, que permiten hacer coincidir la configuración de cliente y servidor.

Para ver las opciones que puede configurar, vaya a [Configuración de dispositivos con Windows 10 y Windows Holographic para agregar conexiones VPN mediante Intune](../configuration/vpn-settings-windows-10.md).

Se aplica a:

- Windows 10 y versiones posteriores

#### <a name="configure-more-microsoft-launcher-settings-in-a-device-restrictions-profile-on-android-enterprise-devices-cobo---6285001----"></a>Configuración de más opciones de Microsoft Launcher en un perfil de restricciones de dispositivos en dispositivos empresariales Android (COBO)<!-- 6285001  -->

En los dispositivos totalmente administrados de Android Enterprise, se pueden configurar las opciones de Microsoft Launcher mediante el perfil de restricciones de dispositivos (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise**como plataforma > **Solo el propietario del dispositivo** > **Restricciones de dispositivos** > **Experiencia de dispositivo** > **Totalmente administrado**). 

Para ver estas opciones, vaya a [Configuración de dispositivos Android Enterprise para permitir o restringir características mediante Intune](../configuration/device-restrictions-android-for-work.md#device-experience).

También puede establecer la configuración de Microsoft Launcher mediante un [perfil de configuración de aplicaciones](../apps/configure-microsoft-launcher.md).

Se aplica a:

- Dispositivos totalmente administrados del propietario del dispositivo Android Enterprise (COBO)

#### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184---idstaged---"></a>Nuevas características de Managed Home Screen en los dispositivos dedicados del propietario del dispositivo de Android Enterprise (COSU)<!-- 7414175 7133328 7133720 7134873 7135184   idstaged -->

En los dispositivos Android Enterprise, los administradores pueden usar perfiles de configuración de dispositivos para personalizar Managed Home Screen en dispositivos dedicados mediante el modo de pantalla completa de varias aplicaciones (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** para la plataforma > **Solo el propietario del dispositivo** > **Restricciones de dispositivo** para el perfil > **Experiencia de dispositivo** > **Dispositivo dedicado** > **Varias aplicaciones**).

En concreto, puede:

- Personalizar iconos, cambiar la orientación de la pantalla y mostrar notificaciones de aplicaciones en los iconos de notificación <!--7414175-->
- Ocultar el acceso directo a la configuración administrada <!--7133328-->
- Acceder de forma más sencilla al menú de depuración <!--7133720-->
- Crear una lista permitida de redes Wi-Fi <!-- 7134873-->
- Acceso más sencillo a la información del dispositivo <!-- 7135184-->

Para obtener más información, vea [Configuración de dispositivos Android Enterprise para permitir o restringir características](../configuration/device-restrictions-android-for-work.md) y [este blog](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

Se aplica a:

- Dispositivos dedicados administrados del propietario del dispositivo Android Enterprise (COSU)

#### <a name="administrative-templates-updated-for-microsoft-edge-84--7722068--"></a>Plantillas administrativas actualizadas para Microsoft Edge 84<!--7722068-->
Se ha actualizado la configuración de ADMX disponible para Microsoft Edge. Los usuarios finales ahora pueden configurar e implementar la configuración de ADMX nueva agregada en Edge 84. Para obtener más información, vea las [Notas de la versión de Edge 84](https://docs.microsoft.com/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscripción de dispositivos

#### <a name="corporate-owned-personally-enabled-devices-preview--4442275----"></a>Dispositivos corporativos con habilitación personal (versión preliminar)<!--4442275  -->
Intune ahora admite dispositivos corporativos de Android Enterprise con un perfil de trabajo para versiones de sistema operativo Android 8 y posteriores. Los dispositivos corporativos con un perfil de trabajo son uno de los escenarios de administración corporativa del conjunto de soluciones de Android Enterprise. Este escenario va destinado a dispositivos de usuario únicos para uso personal y corporativo. Este escenario de propiedad corporativa y con habilitación personal (COPE) ofrece lo siguiente:

- creación de contenedores de perfiles de trabajo y personales
- control de nivel de dispositivo para los administradores
- garantía para los usuarios finales de que sus datos y aplicaciones personales seguirán siendo privados

La primera versión preliminar pública incluirá un subconjunto de las características que se incluirán en la versión disponible con carácter general. De manera gradual se agregarán características adicionales. Las características que estarán disponibles en la primera versión preliminar incluyen las siguientes:

- Inscripción: los administradores pueden crear varios perfiles de inscripción con tokens únicos que no expiren. La inscripción de dispositivos se puede realizar mediante NFC, la entrada de tokens, el código QR, Zero Touch o Knox Mobile Enrollment.
- Configuración de dispositivos: un subconjunto de los valores de configuración existentes de dispositivos dedicados y totalmente administrados.
- Cumplimiento de dispositivos: las directivas de cumplimiento que están disponibles actualmente para los dispositivos totalmente administrados.
- Acciones de dispositivo: elimine el dispositivo (restablecimiento de fábrica), reinícielo y bloquéelo.  
- Administración de aplicaciones: asignaciones de aplicaciones, configuración de aplicaciones y funcionalidades de informes asociadas 
- Acceso condicional

Para obtener más información sobre la versión preliminar de la propiedad corporativa con perfil de trabajo, vea el [blog de soporte técnico](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805-----"></a>Actualizaciones de la acción de bloqueo remoto para dispositivos macOS<!--7032805   -->
Los cambios de la acción de bloqueo remoto para dispositivos macOS incluyen lo siguiente:
- El PIN de recuperación se muestra durante 30 días (en lugar de 7) antes de la eliminación.
- Si un administrador tiene abierto un segundo explorador e intenta volver a desencadenar el comando desde otra pestaña o explorador, Intune permite que el comando pase. Sin embargo, el estado de los informes se establece como erróneo en lugar de generar un nuevo PIN.
- Al administrador no se le permite emitir otro comando de bloqueo remoto si el anterior todavía está pendiente o si el dispositivo no se ha vuelto a sincronizar.
Estos cambios están diseñados para impedir que se sobrescriba el PIN correcto después de varios comandos de bloqueo remoto.

#### <a name="device-actions-report-differentiates-between-wipe-and-protected-wipe--7118901---"></a>Distinción entre el borrado y el borrado protegido en el informe de acciones de dispositivo<!--7118901 -->
El informe **Acciones de dispositivo** ahora distingue entre las acciones de borrado y de borrado protegido. Para ver el informe, vaya al [centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Supervisar** > **Acciones de dispositivo** (en **Otros**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="microsoft-defender-firewall-rule-migration-tool-preview---6423187-----"></a>Versión preliminar de la herramienta de migración de reglas de firewall de Microsoft Defender<!-- 6423187   -->
Estamos trabajando en la versión preliminar pública de una herramienta basada en PowerShell que migrará las reglas de firewall de Microsoft Defender. Al instalar y ejecutar la herramienta, se crean automáticamente directivas de reglas de firewall de seguridad de los puntos de conexión para Intune basadas en la configuración actual de un cliente de Windows 10. Para obtener más información, vea [Información general sobre la herramienta de migración de reglas de firewall de seguridad de los puntos de conexión](../protect/endpoint-security-firewall-rule-tool.md).

#### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-generally-available---7303816-----"></a>Directiva de detección de puntos de conexión y respuesta para la incorporación de dispositivos de asociación de inquilinos a MDATP disponible de manera general<!-- 7303816   -->
Como parte de la seguridad del punto de conexión en Intune, las [directivas de detección y de puntos de conexión y respuesta (EDR) para su uso con dispositivos que administra Configuration Manager](../protect/endpoint-security-edr-policy.md) ya no se encuentran en *versión preliminar* y ahora están *disponibles de manera general*.

Para usar la directiva de EDR con dispositivos de una versión compatible de Configuration Manager, configure [Asociación de inquilinos para Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md). Después de completar la configuración de asociación de inquilinos, puede implementar las directivas de EDR para incorporar dispositivos que administra Configuration Manager a Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender).

#### <a name="bluetooth-settings-are-available-in-device-control-profiles-for-endpoint-security-attack-surface-reduction-policy---7032084-----"></a>La configuración de Bluetooth está disponible en los perfiles de control de dispositivos de la directiva de reducción de la superficie expuesta a ataques de seguridad de los puntos de conexión <!--7032084   -->
Hemos agregado opciones de configuración para administrar Bluetooth en dispositivos Windows 10 en el [perfil de control de dispositivos](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) para la *directiva de reducción de la superficie expuesta a ataques de seguridad de los puntos de conexión*.  Estas son las mismas opciones de configuración que las que han estado disponibles en los perfiles de restricción de dispositivos para *Configuración del dispositivo*.

#### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801-----"></a>Administración de las ubicaciones de origen de las actualizaciones de definiciones con la directiva antivirus de seguridad de puntos de conexión para dispositivos Windows 10<!-- 6347801   -->  
Hemos agregado dos nuevas opciones de configuración a la categoría *Actualizaciones* de la [directiva antivirus de seguridad del punto de conexión para dispositivos Windows 10](../protect/antivirus-microsoft-defender-settings-windows.md#updates) que pueden ayudar a administrar la forma en la que los dispositivos obtienen definiciones de actualización:

- *Definir recursos compartidos de archivos para descargar actualizaciones de definiciones*
- *Definir orden de los orígenes para descargar actualizaciones de definiciones*

Gracias a las nuevas opciones de configuración, se pueden agregar recursos compartidos de archivos UNC como ubicaciones de origen de descarga para las actualizaciones de definiciones y definir el orden en el que se establece la comunicación con las distintas ubicaciones de origen.

#### <a name="improved-security-baselines-node---7433136------"></a>Nodo mejorado de líneas base de seguridad<!-- 7433136    -->
Hemos realizado algunos cambios para mejorar la facilidad de uso del [nodo de línea base de seguridad](../protect/security-baselines.md) en el centro de administración de Microsoft Endpoint Manager. Ahora, al acceder a **Seguridad de punto de conexión** > **Líneas base de seguridad** y seleccionar un tipo de línea base de seguridad para MDM, se presentará un panel **Perfiles**. En el panel Perfiles, se pueden ver los perfiles que se han creado para ese tipo de línea base.  Anteriormente, la consola presentaba un panel Información general que incluía una acumulación de datos agregados que no siempre coincidía con los detalles que se encontraban en los informes de perfiles individuales.

Sin cambiar, en el panel Perfiles, se puede seleccionar un perfil y explorarlo para ver las propiedades de los perfiles, así como varios informes que están disponibles en *Supervisión*.  Del mismo modo, en el mismo nivel que Perfiles, todavía se puede seleccionar la opción **Versiones** para ver las distintas versiones de ese tipo de perfil que se ha implementado. Al explorar una versión, también obtiene acceso a los informes, de forma similar a los informes de perfil. 

#### <a name="derived-credentials-support-for-windows---4886090-----"></a>Compatibilidad con credenciales derivadas para Windows<!-- 4886090   -->
Ahora se pueden usar credenciales derivadas con sus dispositivos Windows. Esto expandirá la compatibilidad existente para iOS/iPadOS y Android, y estará disponible para los mismos proveedores de credenciales derivados:
- Entrust Datacard
- Intercede
- DISA Purebred

La compatibilidad con Windows incluye el uso de una credencial derivada para la autenticación en perfiles de Wi-Fi o VPN. En el caso de los dispositivos Windows, la credencial derivada se emite desde la aplicación cliente que proporciona el proveedor de credenciales derivadas que se usa.

#### <a name="manage-filevault-encryption-for-devices-that-were-encrypted-by-the-device-user-and-not-by-intune--5239424----"></a>Administración del cifrado de FileVault para dispositivos que ha cifrado el usuario del dispositivo en lugar de Intune<!--5239424  -->
Intune ahora puede [asumir la administración del cifrado de disco de FileVault en un dispositivo macOS que ha cifrado el usuario del dispositivo](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices) en lugar de la directiva de Intune.  En este escenario se requiere lo siguiente:
- El dispositivo debe recibir la directiva de cifrado de disco de Intune que habilita FileVault.
- El usuario del dispositivo debe usar el sitio web del Portal de empresa a fin de cargar la clave de recuperación personal para el dispositivo cifrado en Intune. Para cargar la clave, es necesario selecciona la opción *Almacenar clave de recuperación* para su dispositivo macOS cifrado.

Una vez que el usuario cargue su clave de recuperación, Intune la rotará para confirmar que sea válida. Intune ahora puede administrar la clave y el cifrado como si usara la directiva para cifrar el dispositivo directamente. Si un usuario necesita recuperar su dispositivo, puede acceder a la clave de recuperación mediante cualquier dispositivo desde las ubicaciones siguientes:   
- sitio web del Portal de empresa
- Aplicación Portal de empresa para iOS/iPadOS 
- Aplicación Portal de empresa para Android
- Aplicación de Intune

#### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632--"></a>Ocultación de la clave de recuperación personal de un usuario de dispositivo durante el cifrado de disco de FileVault de macOS<!--  5475632-->
Al usar la directiva de seguridad del punto de conexión para configurar el cifrado de disco de FileVault para macOS, use el valor [**Ocultar clave de recuperación**](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) para impedir la visualización de la *clave de recuperación personal* para el usuario del dispositivo, mientras se cifra el dispositivo. Al ocultar la clave durante el cifrado, puede ayudar a protegerla, ya que los usuarios no podrán anotarla mientras esperan a que el dispositivo se cifre. 

Más adelante, si se necesita la recuperación, un usuario siempre puede usar cualquier dispositivo para ver su clave de recuperación personal mediante el sitio web del Portal de empresa de Intune, el Portal de empresa de iOS/iPadOS, el Portal de empresa de Android o la aplicación de Intune.

#### <a name="improved-view-of-security-baseline-details-for-devices---5536846----"></a>Vista mejorada de los detalles de base de referencia de seguridad de los dispositivos<!-- 5536846  -->
Ahora puede explorar los detalles de un dispositivo para ver la información detallada de configuración de las líneas base de seguridad que se aplican al dispositivo. La configuración aparece en una lista sencilla y plana, que incluye la categoría de configuración, el nombre de la configuración y el estado. Para obtener más información, vea [Visualización de configuraciones de seguridad de los puntos de conexión por dispositivo](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="device-compliance-logs-now-in-english--6014904----"></a>Registros de cumplimiento de dispositivos ahora en inglés<!--6014904  -->
Anteriormente, los registros de DeviceComplianceOrg de Intune solo tenían enumeraciones para ComplianceState, OwnerType y DeviceHealthThreatLevel. Ahora estos registros tienen información en inglés en las columnas.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Control de acceso basado en roles.

#### <a name="assign-profile-and-update-profile-permission-changes--7177586-----"></a>Cambios de los permisos Asignar perfil y Actualizar perfil<!--7177586   -->
Los permisos de control de acceso basado en rol se han cambiado por Asignar perfil y Actualizar perfil para el flujo de inscripción de dispositivo automatizada:

Asignar perfil: los administradores con este permiso también pueden asignar los perfiles a los tokens y asignar un perfil predeterminado a un token para la inscripción de dispositivo automatizada.

Actualizar perfil: los administradores con este permiso pueden actualizar los perfiles existentes solo para la inscripción de dispositivo automatizada.

Para ver estos roles, vaya al [centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Administración de inquilinos** > **Roles** > **Todos los roles** > **Crear** > **Permisos** > **Roles**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Scripting

#### <a name="additional-data-warehouse-v10-properties---6125732----"></a>Propiedades adicionales de Data Warehouse v1.0<!-- 6125732  -->
Hay otras propiedades disponibles mediante Intune Data Warehouse v1.0. Las propiedades siguientes se exponen ahora por medio de la entidad [dispositivos](../developer/reports-ref-devices.md#devices):
- `ethernetMacAddress`: identificador de red único de este dispositivo.
- `office365Version`: versión de Office 365 instalada en el dispositivo.

Las propiedades siguientes ahora se exponen por medio de la entidad [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories):
- `physicalMemoryInBytes`: memoria física en bytes.
- `totalStorageSpaceInBytes`: capacidad total de almacenamiento en bytes.

Para obtener más información, vea [API de Data Warehouse de Microsoft Intune](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## <a name="week-of-july-06-2020"></a>Semana del 6 de julio de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023---"></a>Actualización de iconos de dispositivos en aplicaciones del Portal de empresa y de Intune en Android<!-- 6057023 -->
Hemos actualizado los iconos de dispositivos de las aplicaciones del Portal de empresa y de Intune de los dispositivos Android para crear una apariencia más moderna y en consonancia con el sistema de diseño de Microsoft Fluent. Puede encontrar información relacionada en [Actualizaciones de los iconos de la aplicación del Portal de empresa para iOS o iPadOS y macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscripción de dispositivos

#### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707---"></a>El Portal de empresa de iOS admitirá la Inscripción de dispositivos automatizada de Apple sin afinidad de usuario<!-- 7282707 --> 
El Portal de empresa de iOS ahora se admite en los dispositivos inscritos con la Inscripción de dispositivos automatizada de Apple sin necesidad de un usuario asignado. Un usuario final puede iniciar sesión en el Portal de empresa de iOS para establecerse como usuario primario de un dispositivo iOS o iPad inscrito sin afinidad de dispositivo. Para más información sobre la Inscripción de dispositivos automatizada, consulte [Inscripción automática de dispositivos iOS/iPadOS con Inscripción de dispositivos automatizada de Apple](../enrollment/device-enrollment-program-enroll-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview---7552762---"></a>Asociación de inquilinos: detalles de cliente de ConfigMgr en el centro de administración (versión preliminar)<!-- 7552762 -->

Ahora puede ver los detalles del cliente ConfigMgr, incluidas las recopilaciones, la pertenencia a grupos de límites y la información de cliente en tiempo real para un dispositivo específico en el centro de administración de Microsoft Endpoint Manager. Para más información, consulte [Asociación de inquilinos: detalles de cliente de ConfigMgr en el centro de administración (versión preliminar)](../../configmgr/tenant-attach/client-details.md)

## <a name="week-of-june-22-2020"></a>Semana del 22 de junio de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Nuevas aplicaciones protegidas disponibles para Intune<!-- 7248952 -->
Ya están disponibles las siguientes aplicaciones protegidas:
- BlueJeans Video Conferencing
- Cisco Jabber para Intune
- Tableau Mobile para Intune
- ZERO para Intune

Para obtener más información sobre las aplicaciones protegidas, vea [Aplicaciones protegidas de Microsoft Intune](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>Uso del análisis de puntos de conexión para mejorar la productividad del usuario y reducir los costos de soporte técnico de TI<!-- 5653063 --> 
Durante la semana siguiente se implementará esta característica. El análisis de puntos de conexión tiene como objetivo mejorar la productividad del usuario y reducir los costos de soporte técnico de TI, gracias a la información detallada que se proporciona sobre la experiencia del usuario. La información permite que TI optimice la experiencia del usuario final con soporte técnico proactivo y detecte regresiones a la experiencia del usuario mediante la evaluación del impacto de los cambios de configuración en el usuario. Para más información, consulte [Análisis de puntos de conexión (versión preliminar)](https://aka.ms/uea).

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>Corrección proactiva de los problemas del dispositivo del usuario final mediante paquetes de scripts<!-- 5933328 -->
Puede crear y ejecutar paquetes de scripts en dispositivos de usuario final para buscar y corregir de forma proactiva los principales problemas de soporte técnico de la organización. La implementación de paquetes de scripts le ayudará a reducir las llamadas de soporte técnico. Cree su propio paquete de scripts o implemente uno de los que hemos escrito y usado en nuestro entorno para disminuir las incidencias de soporte técnico. Intune permite ver el estado de los paquetes de scripts implementados y supervisar los resultados de detección y corrección. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Informes** > **Análisis de puntos de conexión** > **Correcciones proactivas**. Para obtener más información, vea [Correcciones proactivas](https://aka.ms/uea_prs).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Uso de ATP de Microsoft Defender en directivas de cumplimiento para Android<!-- 4425686  -->

Ahora puede usar Intune para [incorporar dispositivos Android a Advanced Threat Protection de Microsoft Defender](../protect/advanced-threat-protection-configure.md#onboard-devices) (ATP de Microsoft Defender). Una vez que haya incorporado los dispositivos inscritos, las directivas de cumplimiento para Android podrán usar las señales de *nivel de amenaza* de ATP de Microsoft Defender. Estas son las mismas señales que se podían usar previamente para dispositivos Windows 10.

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563----"></a>Configuración de la protección web de ATP de Defender para dispositivos Android<!-- 6185563  -->

Al usar Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) para dispositivos Android, puede [configurar la protección web de ATP de Microsoft Defender](../protect/advanced-threat-protection-manage-android.md) para deshabilitar la característica de examen de suplantación de identidad (phishing) o impedir que el examen use la VPN.

En función de cómo se inscriba el dispositivo Android con Intune, estarán disponibles las siguientes opciones:

- Administrador de dispositivos Android: use la configuración de OMA-URI personalizada para deshabilitar la característica de protección web o para deshabilitar el uso de VPN solo durante los exámenes.
- Perfil de trabajo de Android Enterprise: use un perfil de configuración de aplicaciones y el diseñador de configuraciones para deshabilitar todas las funciones de protección web.

<!-- ########################## -->
## <a name="week-of-june-15-2020--2006-service-release"></a>Semana del 15 de junio de 2020 (versión del servicio 2006)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>Protección de la transferencia de datos de telecomunicaciones para aplicaciones administradas<!-- 6884491  -->
Cuando se detecta un número de teléfono hipervinculado en una aplicación protegida, Intune comprueba si se ha aplicado una directiva de protección que permita transferir el número a una aplicación de marcador. Puede elegir cómo administrar este tipo de transferencia de contenido cuando se inicia desde una aplicación administrada por directiva. Al crear una directiva de protección de aplicaciones en Microsoft Endpoint Manager, seleccione una opción de aplicación administrada en **Enviar datos de la organización a otras aplicaciones** y, luego, elija una opción en **Transferir datos de telecomunicaciones a**. Para obtener más información sobre esta configuración de protección de datos, vea [Configuración de directivas de protección de aplicaciones Android en Microsoft Intune](../apps/app-protection-policy-settings-android.md) y [Configuración de directivas de protección de aplicaciones de iOS](../apps/app-protection-policy-settings-ios.md). 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>Entrega unificada de aplicaciones de Azure AD Enterprise y Office Online en el Portal de empresa<!-- 7414033  -->
En el panel **Personalización** de Intune, puede seleccionar **Ocultar** o **Mostrar** **Aplicaciones de Azure AD Enterprise** y **Aplicaciones de Office Online** en el Portal de empresa. Cada usuario final ve todo el catálogo de aplicaciones desde el servicio de Microsoft elegido. De forma predeterminada, cada origen de aplicación adicional se establecerá en **Ocultar**. Esta característica se va a aplicar en primer lugar en el sitio web del Portal de empresa y, luego, en el Portal de empresa de Windows. Para encontrar esta opción de configuración, seleccione **Administración de inquilinos** > **Personalización** en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Para obtener información relacionada, vea [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md).

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Mejoras en el Portal de empresa para la experiencia de inscripción de macOS<!-- 6444452  -->
La experiencia de inscripción del Portal de empresa para macOS cuenta con un proceso de inscripción más sencillo que es más coherente con la experiencia de inscripción en el Portal de empresa para iOS. Los usuarios del dispositivo verán:  
- Una interfaz de usuario más elegante.  
- Una lista de comprobación de inscripción mejorada.  
- Instrucciones más claras sobre cómo inscribir sus dispositivos.  
- Mejores opciones de solución de problemas.  

Para más información sobre el Portal de empresa de Intune, consulte [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md).

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>Mejoras en la página Dispositivos de iOS/iPadOS y los portales de empresa de macOS<!-- 6055001 -->
Hemos realizado cambios en la página **Dispositivos** del Portal de empresa para mejorar la experiencia de la aplicación para usuarios de iOS/iPadOS y Mac. Además de crear una apariencia más moderna, hemos reorganizado los detalles del dispositivo en una sola columna con encabezados de sección definidos para que a los usuarios les resulte más fácil ver el estado de los dispositivos. También hemos agregado una mensajería más clara y pasos de solución de problemas para los usuarios cuyos dispositivos no cumplen los requisitos. Para obtener más información sobre el Portal de empresa, vea [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md). Para sincronizar manualmente un dispositivo, vea [Sincronización manual del dispositivo iOS](../user-help/sync-your-device-manually-ios.md).  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>Configuración de la nube para la aplicación Portal de empresa de iOS o iPadOS<!-- 7071303  -->
La nueva configuración de la **nube** para el Portal de empresa de iOS o iPadOS permite a los usuarios redirigir la autenticación hacia la nube adecuada para la organización. De forma predeterminada, la opción está configurada en **Automático**, que dirige la autenticación a la nube que el dispositivo del usuario detecta automáticamente. Si la autenticación de la organización debe redirigirse a una nube distinta de la que se detecta automáticamente (como una pública o de administración pública), los usuarios pueden seleccionar manualmente la nube adecuada si eligen **Configuración** de la aplicación > **Portal de empresa** > **Nube**. Los usuarios solo deben cambiar el valor **Automático** de **Nube** si inician sesión desde otro dispositivo y este no detecta automáticamente la nube adecuada. 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>Tokens duplicados de VPP de Apple<!-- 7101606  -->
Los tokens de VPP de Apple con la misma **Ubicación del token** ahora están marcados como **Duplicados** y se pueden sincronizar de nuevo cuando se ha quitado el token duplicado. Todavía puede asignar y revocar licencias para los tokens marcados como duplicados. Pero es posible que las licencias de las nuevas aplicaciones y los libros comprados no se reflejen una vez que un token se marca como duplicado. Para buscar los tokens de VPP de Apple del inquilino, en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Administración de inquilinos** > **Conectores y tokens** > **Tokens de VPP de Apple**. Para obtener más información relacionada con los tokens VPP, vea [Administración de aplicaciones de iOS y macOS compradas a través del Programa de Compras por Volumen de Apple con Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>Adición de varios certificados raíz para la autenticación EAP-TLS en perfiles de Wi-Fi en dispositivos macOS<!-- 2077871  -->

En los dispositivos macOS, puede crear un perfil de Wi-Fi y seleccionar el tipo de autenticación Protocolo de autenticación extensible (EAP) (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** para la plataforma > **Wi-Fi** para el perfil > **Tipo de Wi-Fi** establecido en Empresa).

Al establecer el **Tipo de EAP** en la autenticación **EAP-TLS**, **EAP-TTLS** o **PEAP**, puede agregar varios certificados raíz. Antes solo se podía agregar un certificado raíz.

Para obtener más información sobre las opciones que se pueden configurar, vea [Incorporación de la configuración de Wi-Fi para dispositivos macOS en Microsoft Intune](../configuration/wi-fi-settings-macos.md).

Se aplica a:
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>Uso de certificados PKCS con perfiles de Wi-Fi en dispositivos Windows 10 y más recientes<!-- 3246388   -->
Puede autenticar los perfiles de Wi-Fi de Windows con certificados SCEP (**Configuración de dispositivo** > **Perfiles** > **Crear perfil** > **Windows 10 y versiones posteriores** para la plataforma > **Wi-Fi** para el tipo de perfil > **Empresa** > **Tipo de EAP**). Ahora puede usar certificados PKCS con los perfiles de Wi-Fi de Windows. Esta característica permite a los usuarios autenticar perfiles de Wi-Fi mediante perfiles de certificado PKCS nuevos o existentes en el inquilino. 

Para obtener más información sobre las opciones de Wi-Fi que se pueden configurar, vea [Agregar Wi-Fi para dispositivos Windows 10 y versiones posteriores en Intune](../configuration/wi-fi-settings-windows.md).

Se aplica a:
- Windows 10 y versiones posteriores

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Perfiles de configuración de dispositivos de red cableada para dispositivos macOS<!-- 3508686  -->
Hay disponible un nuevo perfil de configuración de dispositivos macOS que configura redes cableadas (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** para la plataforma > **Red cableada** para el perfil). Use esta característica para crear perfiles de 802.1x con el fin de administrar redes cableadas e implementarlas en los dispositivos macOS.

Para obtener más información sobre esta característica, vea [Redes cableadas en dispositivos macOS](../configuration/wired-networks-configure.md).

Se aplica a:
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>Uso de Microsoft Launcher como iniciador predeterminado para dispositivos empresariales Android totalmente administrados<!-- 4927976   -->
En los dispositivos del propietario de dispositivos de Android Enterprise, puede configurar Microsoft Launcher como el iniciador predeterminado para dispositivos totalmente administrados (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise**como plataforma > **Propietario del dispositivo** > **restricciones de dispositivos** para el perfil > **Experiencia de dispositivo**). Para configurar el resto de la configuración de Microsoft Launcher, use [directivas de configuración de aplicaciones](../apps/configure-microsoft-launcher.md). 

Además, hay otras actualizaciones de la interfaz de usuario, entre las que se incluyen **Dispositivos dedicados**, cuyo nombre cambia a **Experiencia de dispositivo**.

Para ver los valores que puede restringir, consulte [Configuración de dispositivos Android Enterprise para permitir o restringir características mediante Intune](../configuration/device-restrictions-android-for-work.md). 

Se aplica a:
- Dispositivos totalmente administrados del propietario del dispositivo Android Enterprise (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>Uso de la configuración de modo de aplicación única autónoma para configurar la aplicación de Portal de empresa de iOS con el fin de que sea una aplicación de inicio y cierre de sesión<!-- 7055619   -->
En los dispositivos iOS o iPadOS, puede configurar las aplicaciones para que se ejecuten en el modo de aplicación única autónoma (ASAM). Ahora, la aplicación Portal de empresa admite ASAM y se puede configurar para que sea una aplicación de inicio y cierre de sesión. En este modo, los usuarios deben iniciar sesión en la aplicación Portal de empresa para usar otras aplicaciones y el botón Pantalla principal del dispositivo. Cuando cierran sesión en la aplicación Portal de empresa, el dispositivo vuelve al modo de aplicación única y se bloquea en la aplicación Portal de empresa.

Para configurar el Portal de empresa de modo que esté en ASAM, vaya a **Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para plataforma > **Restricciones de dispositivos** para perfil > **Modo de aplicación única autónoma**.

Para obtener más información, vea [Modo de aplicación única autónoma (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) y [Modo de aplicación única](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (se abre el sitio web de Apple).

Se aplica a:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>Configuración del almacenamiento en caché de contenido en dispositivos macOS<!-- 7106872   -->
En los dispositivos macOS, puede crear un perfil de configuración que configure el almacenamiento en caché de contenido (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** como plataforma > **Características del dispositivo** para tipo de perfil). Use esta configuración para eliminar la caché, permitir la caché compartida, establecer un límite de caché en el disco y mucho más.

Para más información sobre el almacenamiento en caché de contenido, consulte [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (abre el sitio web de Apple).

Para ver los valores que se pueden configurar, vea [Configuración de características de dispositivos macOS en Intune](../configuration/macos-device-features-settings.md).

Se aplica a:
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Agregue una nueva configuración de esquema y busque la configuración de esquema existente con OEMConfig en Android Enterprise.<!-- 6394386   -->
En Intune, puede usar OEMConfig para administrar la configuración de los dispositivos Android Enterprise (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** para plataforma > **OEMConfig** para el perfil). Al usar **Diseñador de configuraciones**, se muestran las propiedades del esquema de la aplicación. Ahora, en **Diseñador de configuraciones**, puede:

- Agregar una nueva configuración al esquema de la aplicación.
- Buscar valores nuevos y existentes en el esquema de la aplicación.

Para más información sobre los perfiles OEMConfig en Intune, consulte [Uso y administración de dispositivos Android Enterprise con OEMConfig en Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Se aplica a:
- Android Enterprise

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>Bloqueo de sesiones temporales de iPad compartidas en dispositivos iPad compartidos<!-- 6613794  -->
En Intune, hay una nueva opción para **bloquear sesiones temporales de iPad compartidas en dispositivos iPad compartidos** (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** como plataforma > **Restricciones de dispositivos** para tipo de perfil > **iPad compartido**). Cuando está habilitada, los usuarios finales no pueden usar la cuenta de invitado. Deben iniciar sesión en el dispositivo con el identificador y la contraseña de Apple administrados. 

Para obtener más información, vea [Configuración de dispositivos iOS e iPadOS para permitir o restringir características](../configuration/device-restrictions-ios.md).

Se aplica a:
- Dispositivos iPad compartidos que ejecutan iOS/iPadOS 13.4 y versiones más recientes

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscripción de dispositivos

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>Los dispositivos de tipo Bring Your Own Device pueden usar la VPN para la implementación<!--5015344  -->
El nuevo botón de alternancia **Omitir comprobación de conectividad del dominio** del perfil de Autopilot le permite implementar dispositivos de Unión a Azure AD híbrido sin acceso a la red corporativa mediante su propio cliente VPN Win32 de terceros. Para ver el nuevo botón de alternancia, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos**  > **Windows** > **Inscripción de Windows** > **Perfiles de implementación** > **Crear perfil** > **Configuración rápida (OOBE)** .

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>Los perfiles de la página de estado de inscripción pueden establecerse en grupos de dispositivos<!--3952138 -->
Antes, los perfiles de la página de estado de inscripción (ESP) solo podían destinarse a grupos de usuarios. Ahora también pueden establecerse en grupos de dispositivos. Para obtener más información, vea [Configuración de una página de estado de inscripción](../enrollment/windows-enrollment-status.md).

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Errores de sincronización de inscripción de dispositivos automatizada<!-- 6988214 -->
Se notificarán nuevos errores para iOS/iPadOS y para dispositivos macOS, incluido lo siguiente:
- Caracteres no válidos en el número de teléfono o si el campo está vacío. 
- Nombre de configuración no válido o vacío en el perfil. 
- Valor de cursor no válido o expirado, o si no se encuentra ningún cursor.
- Token rechazado o expirado. 
- El campo Departamento está vacío o la longitud es demasiado larga. 
- Apple no encuentra el perfil y se debe crear uno nuevo. 
- Se agregará un recuento de los dispositivos de Apple Business Manager eliminados a la página de información general en la que verá el estado de los dispositivos.

#### <a name="shared-ipads-for-business--6367326-----"></a>iPad compartidos para la empresa<!--6367326   -->
Puede usar Intune y Apple Business Manager para configurar de forma fácil y segura un iPad compartido de modo que varios empleados puedan compartir dispositivos. [iPad compartido](https://developer.apple.com/education/shared-ipad/) de Apple proporciona una experiencia personalizada para varios usuarios a la vez que conserva los datos de usuario. Con un identificador de Apple administrado, los usuarios pueden acceder a sus aplicaciones, datos y configuraciones después de iniciar sesión en cualquier iPad compartido de su organización. iPad compartido funciona con identidades federadas.

Para ver esta característica, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **iOS** > **Inscripción de iOS** > **Tokens del programa de inscripción** > **elija un token** > **Perfiles** > **Crear perfil** > **iOS**. En la página **Configuración de administración**, seleccione **Inscribir sin afinidad de usuario** y verá la opción **iPad compartido**.

Requiere iPadOS 13.4 y versiones posteriores. En esta versión se ha agregado compatibilidad con sesiones temporales con iPad compartido para que los usuarios puedan acceder a un dispositivo sin un identificador de Apple administrado. Al cerrar sesión, el dispositivo borra todos los datos de usuario para que esté listo para su uso de forma inmediata, lo que elimina la necesidad de borrarlo. 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Interfaz de usuario actualizada para la inscripción de dispositivos automatizada de Apple<!--7430322 -->
La interfaz de usuario se ha actualizado para reemplazar el Programa de inscripción de dispositivos de Apple por la inscripción de dispositivos automatizada, con el fin de reflejar la terminología de Apple.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>Disponibilidad del PIN de bloqueo remoto de dispositivo para macOS<!--7281557   -->
La disponibilidad de los PIN de bloqueo remoto para dispositivos macOS ha aumentado de 7 a 30 días.

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>Cambio del usuario primario en los dispositivos administrados conjuntamente<!--7319183  -->
Puede cambiar el usuario primario de un dispositivo para dispositivos Windows administrados conjuntamente. Para más información sobre cómo buscarlo y cambiarlo, consulte [Búsqueda del usuario primario de un dispositivo de Intune](../remote-actions/find-primary-user.md). Esta característica se implementará gradualmente a lo largo de las próximas semanas.

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Al establecer el usuario primario de Intune, también se establece la propiedad del propietario de Azure AD.<!--7319227 -->
Esta nueva característica establece automáticamente la propiedad del propietario en los dispositivos unidos a Azure AD híbrido recién inscritos al mismo tiempo que se establece el usuario primario de Intune. Para más información sobre el usuario primario, consulte [Búsqueda del usuario primario de un dispositivo de Intune](../remote-actions/find-primary-user.md).

Se trata de un cambio en el proceso de inscripción y solo se aplica a los dispositivos recién inscritos. En el caso de los dispositivos unidos a Azure AD híbrido existentes, debe actualizar manualmente la propiedad del propietario de Azure AD. Para ello, puede usar la característica [Cambiar el usuario primario](../remote-actions/find-primary-user.md#change-a-devices-primary-user) o [un script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

Cuando los dispositivos Windows 10 se unen a un directorio de Azure Active Directory híbrido, el primer usuario del dispositivo se convierte en el usuario primario de Endpoint Manager.  Actualmente, el usuario no está establecido en el objeto de dispositivo de Azure AD correspondiente. Esto produce una incoherencia al comparar la propiedad de *propietario* de un portal de Azure AD con la propiedad de *usuario primario* en el centro de administración de Microsoft Endpoint Manager. La propiedad de propietario de Azure AD se usa para proteger el acceso a las claves de recuperación de BitLocker. La propiedad no se rellena en los dispositivos unidos a Azure AD híbrido. Esta limitación evita la configuración del autoservicio de recuperación de BitLocker desde Azure AD. Esta próxima característica resuelve esta limitación.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>Ocultación de la clave de recuperación de los usuarios durante el cifrado de FileVault 2 para dispositivos macOS<!-- 5459801  -->
Se ha agregado una opción nueva a la categoría *FileVault* dentro de la plantilla [Endpoint Protection de macOS](../protect/endpoint-protection-macos.md#filevault): **Ocultar clave de recuperación**. Esta opción oculta la clave personal del usuario final durante el cifrado de FileVault 2. 

Para ver la clave de recuperación personal de un dispositivo macOS cifrado, el usuario del dispositivo puede ir a cualquiera de las siguientes ubicaciones y hacer clic en *Obtener clave de recuperación* para el dispositivo macOS: 

- Aplicación Portal de empresa de iOS/iPadOS
- Aplicación de Intune
- Sitio web del portal de empresa
- Aplicación Portal de empresa de Android

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Compatibilidad con certificados de firma S/MIME y cifrado con Outlook en Android totalmente administrado<!--5896415   -->
Ahora puede usar certificados de firma S/MIME y cifrado con Outlook en dispositivos que ejecutan Android Enterprise totalmente administrado.

Esto amplía la compatibilidad agregada el mes pasado para otras versiones de Android (compatibilidad con certificados de firma S/MIME y cifrado con Outlook en Android). Puede aprovisionar estos certificados mediante perfiles de certificado SCEP y PKCS importados.

Para obtener más información, vea [Etiquetado de sensibilidad y protección en Outlook para iOS y Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) en la documentación de Exchange.

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Adición de un vínculo al sitio web de soporte técnico de Portal de empresa en correos electrónicos por incumplimiento<!-- 7225498    -->
Cuando [configure una plantilla de mensaje de notificación](../protect/actions-for-noncompliance.md#create-a-notification-message-template) para enviar notificaciones por correo electrónico en caso de incumplimiento, use la nueva opción **Vínculo al sitio web de Portal de empresa** para incluir automáticamente un vínculo a dicho sitio web. Si establece esta opción en *Habilitar*, los usuarios con dispositivos no compatibles que reciban un correo electrónico basado en esta plantilla pueden usar el vínculo para abrir un sitio web y obtener más información sobre por qué su dispositivo no es compatible. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>Licencias

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>Los administradores ya no necesitan una licencia de Intune para acceder a la consola de administración de Microsoft Endpoint Manager.<!--1335430 -->
Ahora puede establecer una alternancia en todo el inquilino que elimine el requisito de licencia de Intune para que los administradores accedan a la consola de administración de MEM y a las API de grafos de consulta. Una vez que se elimine el requisito de licencia, nunca se puede volver a restablecer. 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>Scripts 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>Disponibilidad de scripts de shell en dispositivos macOS<!-- 7134839  -->
Los scripts de shell para dispositivos macOS ya están disponibles para los clientes de China y de la nube de administración pública. Para obtener más información sobre los scripts de shell, vea [Uso de scripts de shell en dispositivos macOS en Intune](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>Semana del 8 de junio de 2020   

### <a name="app-management"></a>Administración de aplicaciones  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>Actualizaciones de la pantalla informativa en Portal de empresa para iOS/iPadOS <!--7032452 -->
Se ha actualizado una pantalla informativa en Portal de empresa para iOS/iPadOS a fin de explicar mejor lo que un administrador puede ver y hacer en los dispositivos. Estas aclaraciones solo se aplican a los dispositivos corporativos. Solo se ha actualizado el texto; no se han realizado modificaciones reales de lo que el administrador puede ver o hacer en los dispositivos de usuario. Para ver las pantallas actualizadas, vaya a [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](./whats-new-app-ui.md).

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Actualización de la experiencia del usuario final de inicio condicional de la aplicación Android<!-- 5736084 -->
La versión 2006 del Portal de empresa de Android incluye cambios basados en las actualizaciones de la versión 2005. En 2005, implementamos una actualización en la que los usuarios finales de dispositivos Android que son objeto de una advertencia, un bloqueo o un borrado por parte de una directiva de protección de aplicaciones ven un mensaje de página completa en el que se describe el motivo de dicha advertencia, bloqueo o borrado y los pasos para corregir los problemas. En 2006, los nuevos usuarios de aplicaciones Android a los que se asignó a una directiva de protección de aplicaciones seguirán un flujo guiado para corregir los problemas que hacen que el acceso a su aplicación se bloquee. 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>Semana del 25 de mayo de 2020

### <a name="app-management"></a>Administración de aplicaciones

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>Aplicaciones Windows de 32 bits (x86) en dispositivos ARM64<!-- 5477661 -->
Las aplicaciones Windows de 32 bits (x86) implementadas como disponibles en dispositivos ARM64 ahora se mostrarán en el Portal de empresa. Para más información sobre las aplicaciones Windows de 32 bits, consulte [Administración de aplicaciones Win32](../apps/apps-win32-app-management.md).

#### <a name="windows-company-portal-app-icon---7114635---"></a>Icono de la aplicación Portal de empresa de Windows<!-- 7114635 -->
Se actualizó el icono de la aplicación Portal de empresa de Windows. Para más información sobre el Portal de empresa de Intune, consulte [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md).


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>Semana del 18 de mayo de 2020

### <a name="app-management"></a>Administración de aplicaciones  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>Actualización de iconos de la aplicación Portal de empresa para iOS/iPados y macOS<!--6057697 -->
Actualizamos los iconos en Portal de empresa para crear una apariencia más moderna que sea compatible en dispositivos de pantalla doble y se alinee con Microsoft Fluent Design System. Para ver los iconos actualizados, vaya a [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](./whats-new-app-ui.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Uso de la directiva de detección de puntos de conexión y respuesta para incorporar dispositivos a ATP de Defender<!-- 7130165  -->

Use la [directiva de detección de puntos de conexión y respuesta](../protect/endpoint-security-edr-policy.md) (EDR) de Seguridad de los puntos de conexión para incorporar y configurar dispositivos para la implementación de Advanced Threat Protection de Microsoft Defender (ATP de Defender). EDR admite la directiva para dispositivos Windows administrados por Intune (MDM) y una directiva independiente para dispositivos Windows administrados por Configuration Manager. 

Para usar la directiva para dispositivos de Configuration Manager, debe [configurar Configuration Manager para admitir la directiva de EDR](../protect/tenant-attach-intune.md). La configuración incluye:

- Configure Configuration Manager para la *asociación de inquilinos*.
- Instale una actualización en consola para Configuration Manager a fin de habilitar la compatibilidad con las directivas de EDR. Esta actualización solo se aplica a las jerarquías que tienen habilitada la *asociación de inquilinos*.
- Sincronice las colecciones de dispositivos de la jerarquía con el Centro de administración de Microsoft Endpoint Manager.


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>Semana del 11 de mayo de 2020 (versión de servicio 2005)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Administración de aplicaciones

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Personalización de acciones de dispositivo de autoservicio en el Portal de empresa<!--4393379 -->
Puede personalizar las acciones de dispositivo de autoservicio disponibles que se muestran a los usuarios finales en la aplicación Portal de empresa y el sitio web. Para ayudar a evitar acciones de dispositivo no deseadas, puede configurar estas opciones para la aplicación Portal de empresa si selecciona **Administración de inquilinos** > **Personalización**. Están disponibles las siguientes acciones:
- Ocultar el botón **Quitar** en los dispositivos corporativos de Windows.
- Ocultar el botón **Restablecer** en los dispositivos corporativos de Windows.
- Ocultar el botón **Restablecer** en los dispositivos corporativos de iOS.
- Ocultar el botón **Quitar** en los dispositivos corporativos de iOS.
Para obtener más información, vea [Acciones de dispositivo de autoservicio de usuario desde el Portal de empresa](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

#### <a name="auto-update-vpp-available-apps---3640511----"></a>Actualización automática de aplicaciones disponibles para VPP<!-- 3640511  -->
Las aplicaciones que se publican como aplicaciones disponibles para el Programa de compras por volumen (PCV) se actualizarán de forma automática cuando se habilita **Actualizaciones automáticas de la aplicación** para el token de PCV. Anteriormente, las aplicaciones disponibles para VPP no se actualizaban de forma automática, sino que los usuarios finales debían ir al Portal de empresa y volver a instalar la aplicación si había disponible una versión más reciente. Las aplicaciones necesarias siguen admitiendo las actualizaciones automáticas.




#### <a name="android-company-portal-user-experience---5736084----"></a>Experiencia del usuario del Portal de empresa de Android<!-- 5736084  -->
En la versión 2005 de Portal de empresa de Android, los usuarios finales de dispositivos Android a los que una directiva de protección de aplicaciones emite una advertencia, un bloqueo o un borrado, verán una nueva experiencia de usuario. En lugar de la experiencia de cuadros de diálogo actual, los usuarios finales verán un mensaje de página completa en el que se describe el motivo de la advertencia, el bloqueo o el borrado, y los pasos para corregir el problema. Para obtener más información, vea [Experiencia de protección de aplicaciones para dispositivos Android](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) y [Configuración de directivas de protección de aplicaciones Android en Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>Compatibilidad con varias cuentas en el Portal de empresa para macOS<!-- 5779449  -->
En los dispositivos macOS, ahora Portal de empresa almacena en caché las cuentas de usuario, lo que facilita el inicio de sesión. Los usuarios ya no tienen que iniciar sesión en el Portal de empresa cada vez que inician la aplicación. Además, en el Portal de empresa se mostrará un selector de cuenta si hay varias cuentas de usuario en caché, de modo que los usuarios no tengan que escribir su nombre de usuario. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Nuevas aplicaciones protegidas disponibles<!-- 7060934   -->
Ya están disponibles las siguientes aplicaciones protegidas:
- Board Papers
- Breezy for Intune
- Hearsay Relate for Intune
- ISEC7 Mobile Exchange Delegate for Intune
- Lexmark for Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- ServiceNow® Onboarding - Intune
- Smartcrypt for Intune
- Tact for Intune
- Zero - email for attorneys

Para obtener más información sobre las aplicaciones protegidas, vea [Aplicaciones protegidas de Microsoft Intune](../apps/apps-supported-intune-apps.md).

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>Búsqueda en la documentación de Intune desde el Portal de empresa<!-- 1736480   -->
Ahora puede buscar en la documentación de Intune directamente desde la aplicación Portal de empresa para macOS. En la barra de menús, seleccione **Ayuda** > **Buscar** y escriba las palabras clave de la búsqueda para encontrar rápidamente las respuestas a las preguntas.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Configuración del dispositivo

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Mejoras en la compatibilidad de OEMConfig con dispositivos Zebra Technologies<!-- 4184154 -->
Intune es totalmente compatible con todas las características proporcionadas por OEMConfig de Zebra. Los clientes que administran dispositivos Zebra Technologies con Android Enterprise y OEMConfig pueden implementar varios perfiles de OEMConfig en un dispositivo. Los clientes también pueden ver informes completos sobre el estado de los perfiles de OEMConfig de Zebra.

Para obtener más información, vea [Implementación de varios perfiles de OEMConfig en dispositivos Zebra en Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md).

No hay ningún cambio en el comportamiento de OEMConfig para otros OEM.

Se aplica a:
- Android Enterprise
- Dispositivos Zebra Technologies que admiten OEMConfig. Para obtener detalles específicos sobre compatibilidad, póngase en contacto con Zebra.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>Configuración de extensiones del sistema en dispositivos macOS<!-- 6255624 -->
En los dispositivos macOS, puede crear un perfil de extensiones de kernel para configurar opciones en el nivel de kernel (**Dispositivos** > **Perfiles de configuración** > **macOS** para la plataforma > **Extensiones de kernel** para el perfil). Apple va a dejar en desuso las extensiones de kernel y las va a reemplazar por extensiones del sistema en una versión futura.

Las extensiones del sistema se ejecutan en el espacio del usuario y no tienen acceso al kernel. El objetivo es aumentar la seguridad y proporcionar un mayor control al usuario final, a la vez que se limitan los ataques en el nivel de kernel. Tanto las extensiones de kernel como las del sistema permiten a los usuarios instalar extensiones de aplicaciones que amplían las funciones nativas del sistema operativo.

En Intune, puede configurar tanto extensiones de kernel como del sistema (**Dispositivos** > **Perfiles de configuración** > **macOS** para la plataforma > **Extensiones del sistema** para el perfil). Las extensiones de kernel se aplican a la versión 10.13.2 y más recientes. Las extensiones del sistema se aplican a la versión 10.15 y más recientes. Desde macOS 10.15 a macOS 10.15.4, las extensiones de kernel y del sistema se pueden ejecutar en paralelo. 

Para obtener información sobre estas extensiones en dispositivos macOS, vea [Incorporación de extensiones de macOS](../configuration/kernel-extensions-overview-macos.md).

Se aplica a:
- macOS 10.15 y versiones más recientes

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>Configuración de preferencias de privacidad de aplicaciones y procesos en dispositivos macOS<!-- 2934232   --> 
Con el lanzamiento de macOS Catalina 10.15, Apple ha agregado nuevas mejoras de seguridad y privacidad. De forma predeterminada, las aplicaciones y los procesos no pueden acceder a datos específicos sin el consentimiento del usuario. Si los usuarios no proporcionan su consentimiento, es posible que las aplicaciones y los procesos no funcionen. Intune va a agregar compatibilidad con opciones que permiten a los administradores de TI permitir o impedir el consentimiento del acceso a datos en nombre de los usuarios finales en dispositivos que ejecuten macOS 10.14 y versiones posteriores. Estas opciones garantizan que las aplicaciones y los procesos sigan funcionando correctamente y reducen el número de mensajes. 

Para obtener más información sobre las opciones que se pueden administrar, vea [Preferencias de privacidad de macOS](../configuration/device-restrictions-macos.md#privacy-preferences).

Se aplica a:
- macOS 10.14 y versiones posteriores

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Inscripción de dispositivos

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Las restricciones de inscripción admiten etiquetas de ámbito<!--4209550  -->
Ya se pueden asignar etiquetas de ámbito a las restricciones de inscripción. Para ello, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Restricciones de inscripción** > **Crear restricción**. Cree cualquier tipo de restricción y verá la página **Etiquetas de ámbito**. Para obtener más información, consulte [Establecer restricciones de inscripción](../enrollment/enrollment-restrictions-set.md).

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Compatibilidad con Autopilot para dispositivos HoloLens 2<!--6305220  -->
Windows Autopilot ya es compatible con dispositivos HoloLens 2. Para más información sobre el uso de Autopilot para HoloLens, consulte [Windows Autopilot para HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>Uso de la acción de sincronización remota de forma masiva para iOS<!--6440956  idmiss-->
Ya se puede usar la acción de sincronización remota en hasta 100 dispositivos iOS a la vez. Para ver esta característica, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Todos los dispositivos** > **Acciones masivas del dispositivo**. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Reducción del intervalo de sincronización automatizada de dispositivos a 12 horas<!--3077535  -->
En la Inscripción de dispositivos automatizada de Apple, el intervalo de sincronización automatizada de dispositivos entre Intune y Apple Business Manager se ha reducido de 24 a 12 horas. Para obtener más información sobre la sincronización, vea [Sincronización de dispositivos administrados](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Seguridad de dispositivos

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Compatibilidad con credenciales derivadas para DISA Purebred en dispositivos Android<!-- 6939073     -->
Ahora puede usar *DISA Purebred* como proveedor de [credenciales derivadas](../protect/derived-credentials.md) en dispositivos Android Enterprise totalmente administrados. La compatibilidad incluye la recuperación de una credencial derivada de DISA Purebred. Puede usar una credencial derivada para la autenticación de aplicaciones, Wi-Fi, VPN o la firma S/MIME o el cifrado con las aplicaciones que lo admitan. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Envío de notificaciones de inserción como acción en caso de no cumplimiento <!-- 1733150   -->
Ahora puede configurar una [acción en caso de no cumplimiento](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) que envíe una notificación de inserción a un usuario cuando su dispositivo no cumpla las condiciones de una directiva de cumplimiento. La nueva acción es **Enviar notificación push al usuario final** y se admite en dispositivos iOS y Android.

Cuando los usuarios seleccionan la notificación de inserción en su dispositivo, se abre la aplicación Portal de empresa o Intune para mostrar detalles sobre el motivo del no cumplimiento.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Contenido de Seguridad de los puntos de conexión y nuevas características<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

La documentación de [Seguridad de los puntos de conexión](../protect/endpoint-security.md) de Intune ya está disponible. En el nodo Seguridad de los puntos de conexión del Centro de administración de Microsoft Endpoint Manager es posible:

- Crear e implementar directivas de seguridad prioritarias para los dispositivos administrados
- Configurar la integración con Advanced Threat Protection de Microsoft Defender y administrar las tareas de seguridad para ayudar a corregir los riesgos de los dispositivos en riesgo según la identificación del equipo de ATP
- Configurar líneas base de seguridad
- Supervisar el cumplimiento y las directivas de acceso condicional de un dispositivo
- Ver el estado de cumplimiento de todos los dispositivos desde Intune y Configuration Manager cuando Configuration Manager está configurado para la asociación de clientes.

Además de la disponibilidad de contenido, estas son las novedades de Seguridad de los puntos de conexión este mes:

- [**Las directivas de Seguridad de los puntos de conexión**](../protect/endpoint-security-policy.md) **no están** en la ***versión preliminar*** y ya están listas para usarse en entornos de producción, como *disponibles con carácter general*, con dos excepciones:

  - En una nueva *versión preliminar pública*, puede usar el [perfil de **reglas de firewall de Microsoft Defender**](../protect/endpoint-security-firewall-policy.md#firewall-profiles) para la directiva de firewall de Windows 10. Con cada instancia de este perfil, puede configurar hasta 150 reglas de firewall para cumplimentar los perfiles de firewall de Microsoft Defender. 
  - La directiva de seguridad de protección de cuentas permanece en versión preliminar. 

- Ahora puede [**crear un duplicado de directivas de seguridad de puntos de conexión**](../protect/endpoint-security-policy.md#duplicate-a-policy). Los duplicados conservan la configuración de opciones de la directiva original, pero con un nuevo nombre. La nueva instancia de directiva no incluye ninguna asignación a grupos hasta que se edita la nueva instancia de directiva para agregarlas. Puede duplicar las siguientes directivas:
  - Antivirus
  - Cifrado de discos
  - Firewall
  - Detección de puntos de conexión y respuesta
  - Reducción de la superficie expuesta a ataques
  - Protección de cuentas

- Ahora puede [**crear un duplicado de una línea base de seguridad**](../protect/security-baselines.md#duplicate-a-security-baseline). Los duplicados conservan la configuración de opciones de la línea base original, pero con un nuevo nombre. La nueva instancia de línea base no incluye ninguna asignación a grupos hasta que no se edita la nueva instancia de línea de base para agregarlas.

- Hay disponible un nuevo informe de la directiva de antivirus de Seguridad de los puntos de conexión: [**Puntos de conexión incorrectos de Windows 10**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). Este informe es una nueva página que puede seleccionar cuando vea la directiva de antivirus de Seguridad de los puntos de conexión. El informe muestra el estado del antivirus de los dispositivos Windows 10 administrados por MDM.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Compatibilidad con certificados de firma S/MIME y cifrado con Outlook en Android<!-- 7207474  -->
Ahora puede usar certificados de firma S/MIME y cifrado con Outlook en Android. Con esta compatibilidad, puede aprovisionar estos certificados mediante perfiles de certificado SCEP, PKCS y PKCS importados. Se admiten las siguientes plataformas Android:

- Perfil de trabajo de Android Enterprise
- Administrador de dispositivos Android

Pronto va a estar disponible la compatibilidad con dispositivos Android Enterprise totalmente administrados.

Para obtener más información, vea [Etiquetado de sensibilidad y protección en Outlook para iOS y Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) en la documentación de Exchange.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

#### <a name="device-reports-ui-update---6269408---"></a>Actualización de la interfaz de usuario de informes de dispositivos<!-- 6269408 -->
Ahora, el panel de información general de informes proporciona un **Resumen** y una pestaña **Informes**. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Informes** y luego la pestaña **Informes** para ver los tipos de informes disponibles. Para obtener información relacionada, vea [Informes de Intune](../fundamentals/reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Scripting

#### <a name="macos-script-support---6376978----"></a>Compatibilidad con scripts de macOS<!-- 6376978  -->
La compatibilidad con scripts para macOS ya está disponible con carácter general. Además, se ha agregado compatibilidad con los scripts asignados por el usuario y los dispositivos macOS que se han inscrito con Inscripción de dispositivos automatizada de Apple (anteriormente Programa de inscripción de dispositivos). Para obtener más información, vea [Uso de scripts de shell para dispositivos macOS en Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Semana del 4 de mayo de 2020  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Portal de empresa para Android guía a los usuarios para obtener aplicaciones después de la inscripción del perfil de trabajo <!-- 6103999 -->
Hemos mejorado las instrucciones en la aplicación del Portal de empresa para facilitar a los usuarios la búsqueda e instalación de aplicaciones. Después de la inscripción en la administración del perfil de trabajo, los usuarios recibirán un mensaje que explica cómo encontrar aplicaciones sugeridas en la versión con distintivo de Google Play. El último paso de [Inscribir dispositivos con perfil Android](../user-help/enroll-device-android-work-profile.md) se ha actualizado para mostrar el mensaje nuevo. Los usuarios también verán un nuevo vínculo **Obtener aplicaciones** en el cajón de Portal de empresa de la izquierda. Para dejar espacio a estas experiencias nuevas y mejoradas, se quitó la pestaña **APLICACIONES**. Para ver las pantallas actualizadas, vaya a [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Semana del 20 de abril de 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Administración de dispositivos

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager reúne Configuration Manager e Intune en una misma consola. A partir de la versión 2002 de Configuration Manager, puede cargar los dispositivos de Configuration Manager en el servicio en la nube y realizar acciones en ellos en el centro de administración. Para obtener más información, vea [Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
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
Las organizaciones que usan [canales de pruebas cerradas de Google Play para las pruebas de versión preliminar de las aplicaciones](https://support.google.com/googleplay/android-developer/answer/3131213) pueden administrar dichos canales con Intune. Puede asignar de forma selectiva las aplicaciones de línea de negocio publicadas en canales de preproducción de Google Play a grupos piloto para realizar las pruebas. En Intune, puede ver si una aplicación tiene publicado un canal de compilación de pruebas de preproducción, así como asignar ese canal a grupos de dispositivos o de usuarios de Azure AD. Esta característica está disponible para todos los escenarios de Android Enterprise que se admiten actualmente (perfil de trabajo, totalmente administrado y dedicado). En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), puede agregar una aplicación administrada de Google Play. Para ello, seleccione **Aplicaciones** > **Android** > **Agregar**. Para obtener más información, vea [Uso de canales de pruebas cerradas de Google Play administrado](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

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
Para obtener más información, vea el artículo sobre [eliminación de un token de ADE de Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-automated-device-enrollment-token-from-intune).

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

<!-- ########################## -->
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

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Guía para usuarios desde la administración de administradores de dispositivos Android a la administración de perfiles de trabajo<!--5857738   -->
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
Las propiedades adicionales de inventario de dispositivos están disponibles mediante el Almacenamiento de datos de Intune. Las propiedades siguientes ahora se exponen por medio de la colección beta [devices](../developer/reports-ref-devices.md#devices):
- `ethernetMacAddress`: identificador de red único de este dispositivo.
- `model`: modelo del dispositivo.
- `office365Version`: versión de Office 365 instalada en el dispositivo.
- `windowsOsEdition`: versión del sistema operativo.

Las propiedades siguientes ahora se exponen por medio de la colección beta [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories):
- `physicalMemoryInBytes`: memoria física en bytes.
- `totalStorageSpaceInBytes`: capacidad total de almacenamiento en bytes.

Para obtener más información, vea [API de Data Warehouse de Microsoft Intune](../developer/reports-nav-intune-data-warehouse.md).

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

## <a name="whats-new-archive"></a>Archivo de novedades
Para ver los meses anteriores, consulte el [archivo de novedades](whats-new-archive.md).

## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


