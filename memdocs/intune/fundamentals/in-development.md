---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b7f1a4280b409ec4a12c6371fd2e6cba8a571ca
ms.sourcegitcommit: 56a894edd291034510c144c31770cf09e20b2d6c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2020
ms.locfileid: "88048028"
---
# <a name="in-development-for-microsoft-intune"></a>En desarrollo para Microsoft Intune

Para ayudarle con la preparación y planeación, en esta página se enumeran las actualizaciones y características de la interfaz de usuario de Intune que están en desarrollo, pero que aún no se han publicado. Además de la información de esta página: 

- Si prevemos que tendrá que tomar medidas antes de realizar un cambio, haremos una publicación complementaria en el Centro de mensajes de Office.
- Cuando una característica entra en producción, ya sea una versión preliminar o disponible con carácter general, la descripción de la característica pasa de esta página a [Novedades](whats-new.md).
- Esta página y la página [Novedades](whats-new.md) se actualizan periódicamente. Compruebe si hay actualizaciones adicionales.
- Consulte el [plan de desarrollo de Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) para conocer los plazos de tiempo y los productos estratégicos.

> [!NOTE]
> Esta página refleja las expectativas actuales sobre las funciones de Intune en una versión futura. Las fechas y las características individuales pueden cambiar. En esta página no se describen todas las características en desarrollo.

**Fuente RSS**: para recibir notificaciones cuando esta página se actualice, copie y pegue la dirección URL siguiente en el lector de fuentes: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Este artículo se actualizó por última vez en la fecha que aparece bajo el título anterior.**

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

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Actualización de iconos de dispositivos en aplicaciones del Portal de empresa y de Intune en Android<!-- 6057023  -->
Vamos a actualizar los iconos de dispositivos de las aplicaciones del Portal de empresa y de Intune de los dispositivos Android para crear una apariencia más moderna y en consonancia con el sistema de diseño de Microsoft Fluent. Puede encontrar información relacionada en [Actualizaciones de los iconos de la aplicación del Portal de empresa para iOS o iPadOS y macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>El Portal de empresa de iOS admitirá la Inscripción de dispositivos automatizada de Apple sin afinidad de usuario<!-- 7282707  --> 
Este portal se admitirá en los dispositivos inscritos con la Inscripción de dispositivos automatizada de Apple sin necesidad de un usuario asignado. Un usuario final puede iniciar sesión en el Portal de empresa de iOS para establecerse como usuario primario de un dispositivo iOS o iPad inscrito sin afinidad de dispositivo. Para más información sobre la Inscripción de dispositivos automatizada, consulte [Inscripción automática de dispositivos iOS/iPadOS con Inscripción de dispositivos automatizada de Apple](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>El Portal de empresa de Windows agrega compatibilidad con las aplicaciones de Configuration Manager<!-- 4297660 -->
El Portal de empresa de Windows ahora admite aplicaciones de Configuration Manager. Esta característica permite a los usuarios finales ver las aplicaciones implementadas de Configuration Manager y de Intune en el Portal de empresa de Windows de los clientes administrados conjuntamente. Esta compatibilidad ayuda a los administradores a consolidar sus diferentes experiencias del portal de usuario final. Para más información, consulte [Uso de la aplicación Portal de empresa en dispositivos administrados conjuntamente](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuración del dispositivo

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Establecimiento del estado de cumplimiento de dispositivos desde partners de MDM de terceros<!-- 6361689   -->
Los clientes de Microsoft 365 que posean soluciones de MDM de terceros podrán aplicar directivas de acceso condicional para aplicaciones de Microsoft 365 en iOS y Android a través de la integración con el servicio de cumplimiento de dispositivos de Microsoft Intune. Un proveedor de MDM de terceros aprovechará el servicio Cumplimiento de dispositivos de Intune para enviar datos de cumplimiento de dispositivos a Intune. Después, Intune evaluará para determinar si el dispositivo es de confianza y establecerá los atributos de acceso condicional en Azure AD.  A los clientes se les pedirá que establezcan directivas de acceso condicional de Azure AD desde el centro de administración de Microsoft Endpoint Manager o desde el portal de Azure AD.

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Creación de perfiles de certificado de PKCS para dispositivos Android Enterprise totalmente administrados (COBO)<!-- 4839686 -->
Puede crear perfiles de certificado de PKCS para implementar certificados en dispositivos de perfil de trabajo y propietario del dispositivo Android Enterprise (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise > solo propietario del dispositivo** o **Android Enterprise > solo perfil de trabajo** para plataforma > **PKCS** para perfil).

Pronto podrá crear perfiles de certificado PKCS para dispositivos Android Enterprise totalmente administrados. Se requiere el conector de certificado PFX de Intune. Si no usa SCEP y solo usa PKCS, puede quitar el conector NDES después de instalar el nuevo conector PFX. El nuevo conector PFX importa los archivos PFX e implementa los certificados PKCS en todas las plataformas.

Para más información sobre certificados PKCS, consulte [Configuración y uso de certificados PKCS con Intune](../protect/certficates-pfx-configure.md).

Se aplica a:
- Android Enterprise totalmente administrado (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631---"></a>Uso de NetMotion como un tipo de conexión VPN para iOS/iPadOS y dispositivos macOS<!-- 1333631 -->
Al crear un perfil de VPN, NetMotion está disponible como tipo de conexión VPN (**Dispositivos** > **Configuración de dispositivos** > **Crear perfil** > **iOS/iPadOS** o **macOS** para plataforma > **VPN** para perfil > **NetMotion** para tipo de conexión).

Para obtener más información sobre los perfiles de VPN en Intune, consulte [Creación de perfiles de VPN para conectarse a servidores VPN](../configuration/vpn-settings-configure.md).

Se aplica a:
- iOS/iPadOS
- macOS

### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024---"></a>Más opciones del protocolo de autenticación extensible protegido (PEAP) para perfiles Wi-Fi de Windows 10<!-- 3805024 -->
En los dispositivos Windows 10, puede crear perfiles de Wi-Fi con el protocolo de autenticación extensible (EAP) para autenticar las conexiones Wi-Fi (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Windows 10 y posteriores** para plataforma > **Wi-Fi** para perfil > **Empresa**). Al seleccionar EAP protegido (PEAP), hay nuevas opciones de configuración disponibles:

- **Realizar validación del servidor en PEAP fase 1**: en la fase 1 de la negociación de PEAP, los dispositivos validan el certificado y comprueban el servidor.
  - **Deshabilitar los mensajes de usuario para la validación del servidor en PEAP fase 1**: en la fase 1 de la negociación de PEAP, no se muestran los mensajes de usuario que soliciten autorizar nuevos servidores PEAP para entidades de certificación de confianza.
- **Requerir enlace criptográfico**: impide las conexiones a servidores PEAP que no utilizan el enlace criptográfico durante la negociación PEAP.

Para ver la configuración que puede configurar actualmente, vaya a [Agregar Wi-Fi para dispositivos Windows 10 y versiones posteriores en Intune](../configuration/wi-fi-settings-windows.md).

Se aplica a: 
- Windows 10 y versiones posteriores

### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576---"></a>Configuración del complemento Microsoft Enterprise SSO de macOS<!-- 5627576 -->
El equipo de Microsoft Azure AD creó una extensión de aplicación de inicio de sesión único (SSO) de redireccionamiento que permite a los usuarios de macOS 10.15 + obtener acceso con un inicio de sesión a las aplicaciones de Microsoft, a las aplicaciones de la organización y a los sitios web que admiten la característica SSO de Apple y que se autentican mediante Azure AD. Con la versión del complemento Microsoft Enterprise SSO, puede configurar la extensión de SSO con el nuevo tipo de extensión de aplicación de Microsoft Azure AD (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** para plataforma > **Características del dispositivo** para perfil > **Extensión de aplicación de inicio de sesión único** > tipo de extensión de aplicación de SSO > **Microsoft Azure AD**).

Para lograr el SSO con el tipo de extensión de aplicación de SSO de Microsoft Azure AD, los usuarios deben instalar la aplicación de Portal de empresa en sus dispositivos macOS e iniciar sesión en ella. 

Para obtener más información sobre las extensiones de aplicación de SSO de macOS, consulte [Extensión de aplicación de inicio de sesión único](../configuration/device-features-configure.md#single-sign-on-app-extension).

Se aplica a:
- macOS 10.15 y versiones más recientes

### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991---"></a>Uso de extensiones de aplicación de SSO en más aplicaciones iOS/iPadOS con el complemento de Microsoft Enterprise SSO<!-- 7369991 -->
El complemento [Microsoft Enterprise SSO para dispositivos Apple](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) se puede usar con todas las aplicaciones que admiten las extensiones de aplicación SSO. En Intune, esta característica significa que el complemento funciona con aplicaciones móviles iOS/iPadOS que no usan la biblioteca de autenticación de Microsoft (MSAL) para dispositivos Apple. Las aplicaciones no necesitan usar MSAL, pero tienen que autenticarse con puntos de conexión de Azure AD.

Para configurar las aplicaciones de iOS/iPadOS para usar SSO con el complemento, agregue los identificadores de lote de aplicaciones en un perfil de configuración de iOS/iPadOS (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para plataforma > **Características del dispositivo** para perfil > **Extensión de aplicación de inicio de sesión único** > **Microsoft Azure AD** > para tipo de extensión de aplicación de SSO > **Identificadores de lote de las aplicaciones**).

Para ver la configuración actual de la extensión de la aplicación de SSO que puede configurar, vaya a [Extensión de aplicación de inicio de sesión único](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Se aplica a:
- iOS/iPadOS

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## <a name="device-management"></a>Administración de dispositivos

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Compatibilidad de scripts de PowerShell con dispositivos BYOD<!-- 1862833  -->
Los scripts de PowerShell admitirán dispositivos registrados de Azure AD en Intune. Para más información sobre PowerShell, vea [Uso de scripts de PowerShell para dispositivos Windows 10 en Intune](../apps/intune-management-extension.md). Esta funcionalidad no es compatible con dispositivos que ejecutan Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics incluirá registros de detalles del dispositivo<!--6014987  -->
Habrá disponibles registros detallados del dispositivo de Intune en **Informes** > **Log Analytics**. Puede correlacionar los detalles del dispositivo para compilar consultas personalizadas y libros de Azure.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Asociación de inquilinos: escala de tiempo del dispositivo en el centro de administración<!--7220536, CM7141381 -->
Cuando Configuration Manager sincroniza un dispositivo con Microsoft Endpoint Manager de Microsoft a través de una asociación de inquilinos, podrá ver una escala de tiempo de eventos. Esta escala de tiempo muestra la actividad pasada en el dispositivo que puede ayudarle a solucionar problemas. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Asociación de inquilinos: instalación de una aplicación desde el centro de administración<!-- 7220536, CM6024389 -->
Ahora podrá iniciar la instalación de una aplicación en tiempo real para un dispositivo asociado al inquilino desde el centro de administración de Microsoft Endpoint Management. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Asociación de inquilinos: CMPivot desde el centro de administración<!--7220536, CM6024392 -->
Podrá incorporar la eficacia de [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) al centro de administración de Microsoft Endpoint Manager. Permita que otros roles, como el de Departamento de soporte técnico, puedan iniciar consultas en tiempo real desde la nube en un dispositivo individual administrado por ConfigMgr y devolver los resultados al centro de administración. Esto proporciona todas las ventajas tradicionales de CMPivot, permitiendo a los administradores de TI y a otros roles designados evaluar rápidamente el estado de los dispositivos en su entorno y tomar medidas. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Asociación de inquilinos: ejecución de scripts desde el centro de administración<!--7220536, CM6234688 -->
Podrá incorporar la eficacia de la característica [Ejecutar scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) local de Configuration Manager al centro de administración de Microsoft Endpoint Manager. Permita que otros roles, como el de Departamento de soporte técnico, ejecuten scripts de PowerShell desde la nube en un dispositivo administrado de Configuration Manager individual. Esto proporciona todas las ventajas tradicionales de los scripts de PowerShell que ya se han definido y aprobado por el administrador de Configuration Manager en este nuevo entorno. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Implementación de actualizaciones de software en dispositivos macOS <!-- 3194876 -->
Podrá implementar actualizaciones de software en grupos de dispositivos macOS. Esta característica incluye, entre otras, actualizaciones de archivos críticos, de archivos de configuración y del firmware. Podrá enviar actualizaciones en la siguiente sincronización de dispositivos o seleccionar una programación semanal para implementar actualizaciones dentro o fuera de los períodos que establezca. De esta manera, podrá actualizar los dispositivos fuera de las horas de trabajo estándar o cuando el departamento de soporte técnico tiene a todo el personal ocupado. También obtendrá un informe detallado de todos los dispositivos macOS con actualizaciones implementadas. Puede profundizar en el informe en función de cada dispositivo para ver los estados de determinadas actualizaciones.

### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322---"></a>Revocación de licencias asociadas revocadas antes de eliminar el token de VPP de Apple<!--6195322 -->
En una actualización futura, cuando se elimina un token de VPP de Apple en Microsoft Endpoint Manager, todas las licencias asignadas a Intune asociadas a ese token se revocarán automáticamente antes de la eliminación.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Plantilla de informe de cumplimiento de Power BI V2.0<!-- 636958  -->
Los administradores podrán actualizar la versión de la plantilla de informe de cumplimiento de Power BI de V1.0 a V2.0. En V2.0 se incluirá un diseño mejorado, así como cambios en los cálculos y los datos que se muestran como parte de la plantilla. Para obtener información relacionada, vea [Conexión con el almacenamiento de datos con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Seguridad

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Compatibilidad de la directiva de protección de aplicaciones con Symantec Endpoint Security y Check Point Sandblast<!--  4452423, 4731168 -->

En octubre de 2019, la directiva de protección de aplicaciones de Intune agregó la capacidad de usar datos de algunos de nuestros asociados de Microsoft Threat Defense (MTD). Estamos agregando compatibilidad con los siguientes asociados para usar una directiva de protección de aplicaciones que bloquee o elimine de forma selectiva los datos corporativos de los usuarios en función del estado de un dispositivo:

- **Check Point Sandblast** en Android, iOS y iPadOS
- **Symantec Endpoint Security** en Android, iOS y iPadOS

Para más información sobre el uso de la directiva de protección de aplicaciones con asociados de MTD, consulte [Creación de una directiva de protección de aplicaciones de Mobile Threat Defense con Intune](../protect/mtd-app-protection-policy.md).

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>ATP de Microsoft Defender crea una tarea de seguridad de Endpoint Manager con detalles de la vulnerabilidad<!-- 5568193  -->
La administración de amenazas y vulnerabilidades (TVM) de ATP de Microsoft Defender detecta una configuración de seguridad incorrecta en los dispositivos. Los administradores usan esta información para actualizar los dispositivos vulnerables.

Pronto, ATP de Microsoft Defender podrá generar una tarea de seguridad de Endpoint Manager (**Endpoint Manager** > **Seguridad de los puntos de conexión** > **Tareas de seguridad**) con los detalles de la vulnerabilidad y mostrar los dispositivos afectados. Los administradores de TI pueden aceptar la tarea de seguridad e implementar la configuración necesaria. 

Para más información sobre cómo las tareas de seguridad, vea [Uso de Intune para corregir las vulnerabilidades que identifica ATP de Microsoft Defender](../protect/atp-manage-vulnerabilities.md).

### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119----"></a>Cambios para las exclusiones de la directiva de antivirus para la seguridad de los puntos de conexión<!--5583940, 6018119  -->
Vamos a introducir dos cambios para administrar las listas de exclusión del antivirus de Microsoft Defender que se configuran como parte de una directiva de antivirus de seguridad de los puntos de conexión. (**Seguridad de los puntos de conexión** > **Antivirus** > **Crear directiva** > **Windows 10 y versiones posteriores** para plataforma). Estos dos cambios ayudan a evitar conflictos entre las directivas, y las directivas existentes que estuvieran en conflicto dejarán de estarlo para la lista de exclusiones:

- En primer lugar, vamos a agregar un nuevo tipo de perfil para Windows 10 y versiones posteriores: **Exclusiones del antivirus de Microsoft Defender**.  Este nuevo tipo de perfil incluye solo la configuración para especificar una lista de *procesos*, *extensiones de archivos* y *archivos* y *carpetas* que no quiere que analice Microsoft Defender. Esto puede ayudarle a simplificar la administración de las listas de exclusión separándolas de otras configuraciones de directiva.
- El segundo cambio es que la lista de exclusiones que se define en distintos perfiles se combinará en una única lista de exclusiones para cada dispositivo o usuario, en función de las directivas individuales que se aplican a un usuario o dispositivo específico. Por ejemplo, si el destino es un usuario con tres directivas independientes, las listas de exclusión de esas tres directivas se combinan en un único superconjunto de exclusiones del antivirus de Microsoft Defender, que se aplican de este modo al usuario. Esta combinación incluye las listas de exclusiones del nuevo tipo de perfil que se estaban agregando, así como las directivas existentes que se hubieran configurado en un perfil *Antivirus de Microsoft Defender*.



<!-- ***********************************************-->
## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vea también

Consulte [Novedades de Microsoft Intune](whats-new.md) para obtener más información sobre los desarrollos recientes.
