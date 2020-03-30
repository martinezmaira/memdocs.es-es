---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220139"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>En desarrollo para Microsoft Intune: marzo de 2020

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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>Modo horizontal admitido en Portal de empresa para iOS<!--6048329  -->
Los usuarios podrán inscribir sus dispositivos, buscar aplicaciones y obtener soporte técnico de TI con la orientación de pantalla que prefieran. La aplicación detectará y ajustará automáticamente las pantallas para ajustarse al modo horizontal o vertical, a menos que los usuarios bloqueen la pantalla en modo vertical.

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Experiencia de inicio de sesión mejorada en la aplicación Portal de empresa para Android<!-- 6103997  -->
Se va a actualizar el diseño de varias pantallas de inicio de sesión en la aplicación Portal de empresa para Android a fin de que la experiencia sea más moderna, sencilla y limpia para los usuarios.

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

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Experiencia de interfaz de usuario mejorada al crear perfiles de configuración de OEMConfig en dispositivos Android Enterprise<!-- 5568645   -->
Al crear o editar un perfil de OEMConfig para dispositivos Android Enterprise, se actualiza la experiencia en el Centro de administración del Administrador de puntos de conexión. La experiencia actualizada proporciona un resumen de los valores que se han configurado de un vistazo. Este cambio afecta al perfil de configuración del dispositivo de OEMConfig (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** para plataforma > **OEMConfig** para tipo de perfil).

Esta característica se aplica a:
- Android Enterprise 

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Las opciones y valores de los perfiles de configuración de dispositivos se actualizarán para las plataformas Windows<!-- 4091122 -->
Al crear perfiles de configuración de dispositivos para plataformas Windows (**Dispositivos** > **Perfiles de configuración** >  **Crear perfil** > cualquier opción **Windows** para la plataforma), algunas opciones y sus valores son diferentes del CSP y pueden ser confusos. Los nombres de las opciones y sus valores se actualizarán para que sean más claros.

Se aplica a:

- Perfiles de configuración de dispositivos Windows 10 y versiones posteriores
- Perfiles de configuración de dispositivos Windows Holographic for Business
- Perfiles de configuración de dispositivos Windows 8.1
- Perfiles de configuración de dispositivos Windows Phone 8.1

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Experiencia de interfaz de usuario mejorada al crear perfiles de restricciones de dispositivo en dispositivos Android y Android Enterprise<!-- 5841361 -->
Al crear un perfil para dispositivos Android o Android Enterprise, se actualizará la experiencia en el Centro de administración del Administrador de puntos de conexión. Este cambio afecta a los perfiles de configuración de dispositivo siguientes (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Administrador de dispositivos Android** o **Android Enterprise** para la plataforma):

- Restricciones de dispositivos: Administrador de dispositivos Android
- Restricciones de dispositivos: Propietario del dispositivo Android Enterprise
- Restricciones de dispositivos: Perfil de trabajo de Android Enterprise

Para obtener más información sobre las restricciones de dispositivos que se pueden configurar, vea [Administrador de dispositivos Android](../configuration/device-restrictions-android.md) y [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Configuración de la aplicación ATP de Microsoft Defender para macOS  <!-- 5520115  -->
Pronto podrá configurar las [opciones](../protect/endpoint-protection-macos.md) para la aplicación ATP de Microsoft Defender para dispositivos que ejecuten macOS como parte de un perfil de configuración de dispositivo de protección de puntos de conexión (**Dispositivos** > **Perfiles de configuración** > **Crear perfil**, seleccione **macOS** para *Plataforma* y, después, **Endpoint Protection** para el *Tipo de perfil*). Habrá ocho opciones para la configuración de dispositivos macOS. 

ATP de Microsoft Defender es compatible con macOS 10.13 (High Sierra) y versiones posteriores, y la aplicación [ATP de Microsoft Defender](../apps/apps-advanced-threat-protection-macos.md) se debe implementar en el dispositivo *después* de aplicar esta configuración. Las opciones se deben enviar al dispositivo antes de que se implemente la aplicación. No se admiten las versiones beta de macOS.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nueva configuración de FileVault para la directiva de configuración de dispositivos Endpoint Protection de macOS<!-- 5459801   -->
Se va a agregar una opción nueva a la categoría FileVault dentro de la plantilla [Endpoint Protection de macOS](../protect/endpoint-protection-macos.md): Ocultar clave de recuperación. (**Dispositivos** > **Perfiles de configuración** > **Crear perfil**, seleccione **macOS** para la *Plataforma* y, después, **Endpoint Protection** para el *Tipo de perfil*). Esta opción oculta la clave personal del usuario final durante el cifrado de FileVault 2. Un usuario del dispositivo puede ver su clave de recuperación personal en cualquier momento desde la aplicación Portal de empresa de iOS o desde el sitio web del Portal de empresa para el dispositivo macOS cifrado. Para ver la clave de recuperación personal, puede ir a los detalles del dispositivo y hacer clic en *Obtener clave de recuperación*.

Esta opción no estará disponible en una directiva creada anteriormente. Tendrá que volver a crear las directivas de FileVault para configurar esta opción y poder usarla. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Configuración del agente de optimización de entrega al descargar contenido de aplicaciones Win32<!-- 5410945  -->
Podrá configurar el agente de optimización de entrega para descargar contenido de aplicaciones Win32 en modo de segundo plano o de primer plano, en función de la asignación. En el caso de las aplicaciones Win32 existentes, el contenido se seguirá descargando en el modo de segundo plano. En el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Aplicaciones** > **Todas las aplicaciones** > *seleccione la aplicación Win32* > **Propiedades**. Seleccione **Editar** junto a **Asignaciones**.  Edite la asignación seleccionando **Incluir** en **Modo**, en la sección **Requerido**.  Verá la nueva configuración en la sección **Configuración de la aplicación** cuando esté disponible. Para obtener más información sobre la Optimización de entrega, vea [Administración de aplicaciones Win32: Optimización de entrega](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Administración de dispositivos

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Cambio del usuario primario para dispositivos Windows <!-- 3794742 -->
Podrá cambiar el usuario primario para dispositivos híbridos de Windows y unidos a Azure AD. Para ello, vaya a **Intune** > **Dispositivos** > **Todos los dispositivos** > elija un dispositivo > **Propiedades** > **Usuario primario**.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Compatibilidad de scripts de PowerShell con dispositivos BYOD<!-- 1862833  -->
Los scripts de PowerShell admitirán dispositivos registrados de Azure AD en Intune. Para más información sobre PowerShell, vea [Uso de scripts de PowerShell para dispositivos Windows 10 en Intune](../apps/intune-management-extension.md). Esta funcionalidad no es compatible con dispositivos que ejecutan Windows 10 Home Edition.

### <a name="new-information-in-device-details---5604099---"></a>Nueva información en los detalles del dispositivo<!-- 5604099 -->
La información siguiente estará en la página **Información general** de los dispositivos:

- Capacidad de almacenamiento (cantidad de almacenamiento físico en el dispositivo)
- Capacidad de memoria (cantidad de memoria física en el dispositivo)

### <a name="script-support-for-macos-devices---4280361----"></a>Compatibilidad con scripts para dispositivos macOS<!-- 4280361  -->
Podrá agregar e implementar scripts en dispositivos macOS. Esta compatibilidad amplía la capacidad de configurar dispositivos macOS más allá de lo que es posible con las funcionalidades de MDM nativas en dispositivos macOS.

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
