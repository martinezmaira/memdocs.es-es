---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7827c85585d630f64ba9c6d342b6275fca506b1d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906974"
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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Compatibilidad con varias cuentas en Portal de empresa para Mac<!-- 5779449  -->
En los dispositivos macOS, ahora Portal de empresa almacena en caché las cuentas de usuario, lo que facilita el inicio de sesión. Los usuarios ya no tienen que iniciar sesión en el Portal de empresa cada vez que inician la aplicación. Además, en el Portal de empresa se mostrará un selector de cuenta si hay varias cuentas de usuario en caché, de modo que los usuarios no tengan que escribir su nombre de usuario. 

### <a name="auto-update-vpp-available-apps---3640511----"></a>Actualización automática de aplicaciones disponibles para VPP<!-- 3640511  -->
Las aplicaciones que se publican como aplicaciones disponibles para el Programa de compras por volumen (PCV) se actualizarán de forma automática cuando se habilita **Actualizaciones automáticas de la aplicación** para el token de PCV. Actualmente, las aplicaciones disponibles para PCV no se actualizan de forma automática. En su lugar, los usuarios finales deben ir al Portal de empresa y volver a instalar la aplicación si hay disponible una versión más reciente. Pero las aplicaciones necesarias actualmente admiten las actualizaciones automáticas.

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>Personalización de acciones de dispositivo de autoservicio en el Portal de empresa<!--4393379  -->
Podrá personalizar las acciones de dispositivo de autoservicio disponibles que se muestran a los usuarios finales en la aplicación Portal de empresa y el sitio web. Para ayudar a evitar acciones de dispositivo no deseadas, podrá configurar estas opciones para la aplicación Portal de empresa si selecciona **Administración de inquilinos** > **Personalización** > **Crear** > **Ocultar características**. Están disponibles las siguientes acciones:
- Ocultar el botón **Quitar** en los dispositivos corporativos de Windows.
- Ocultar el botón **Restablecer** en los dispositivos corporativos de Windows.
- Ocultar el botón **Restablecer** en los dispositivos corporativos de iOS.
- Ocultar el botón **Quitar** en los dispositivos corporativos de iOS.

Para obtener más información, vea [Acciones de dispositivo de autoservicio de usuario desde el Portal de empresa](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Entrega unificada de aplicaciones de Azure AD Enterprise u Office Online en el Portal de empresa<!--4404429 -->
En el Portal de empresa podrá alternar (**Ocultar** o **Mostrar**) la presentación de aplicaciones de Azure AD Enterprise u Office Online. Cada usuario verá todo el catálogo de aplicaciones desde el servicio de Microsoft elegido. De forma predeterminada, cada origen de aplicación adicional se establecerá en **Ocultar**. Esta característica se aplicará en primer lugar en el sitio web del Portal de empresa en la versión 2005 y se espera que en el futuro se admita en los Portales de empresa de Windows, iOS/iPadOS y macOS. Para encontrar esta próxima opción, seleccione **Administración de inquilinos** > **Personalización** en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431). Para obtener información relacionada, vea [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md).

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>Búsqueda en la documentación de Intune desde el Portal de empresa<!-- 1736480 -->
Ahora puede buscar en la documentación de Intune directamente desde la aplicación Portal de empresa para macOS. En la barra de menús, seleccione **Ayuda** > **Buscar** y escriba las palabras clave de la búsqueda para encontrar rápidamente las respuestas a las preguntas.

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Portal de empresa para Android guiará a los usuarios para obtener aplicaciones después de la inscripción del perfil de trabajo <!-- 6103999  -->
Se van a mejorar las instrucciones en la aplicación del Portal de empresa para facilitar a los usuarios la búsqueda e instalación de aplicaciones.  Después de la inscripción en la administración del perfil de trabajo, los usuarios verán un mensaje que les indica que pueden encontrar aplicaciones sugeridas en la versión con distintivo de Google Play. Los usuarios también verán un nuevo vínculo **Obtener aplicaciones** en el cajón de Portal de empresa de la izquierda. Para dejar espacio a estas experiencias nuevas y mejoradas, se quitará la pestaña **APLICACIONES**. 

### <a name="android-company-portal-user-experience---5736084---"></a>Experiencia del usuario del Portal de empresa de Android<!-- 5736084 -->
En la versión 2005 de Portal de empresa de Android, los usuarios finales de dispositivos Android a los que una directiva de protección de aplicaciones emite una advertencia, un bloqueo o un borrado, verán una nueva experiencia de usuario. En lugar de la experiencia de cuadros de diálogo actual, los usuarios finales verán un mensaje de página completa en el que se describe el motivo de la advertencia, el bloqueo o el borrado, y los pasos para corregir el problema. Para obtener más información, vea [Experiencia de protección de aplicaciones para dispositivos Android](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) y [Configuración de directivas de protección de aplicaciones Android en Microsoft Intune](../apps/app-protection-policy-settings-android.md).


<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuración del dispositivo

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

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>Configuración de extensiones del sistema en dispositivos macOS<!-- 6255624  -->
En los dispositivos macOS, puede crear un perfil de extensiones de kernel para configurar opciones en el nivel de kernel (**Dispositivos** > **Perfiles de configuración** > **macOS** para la plataforma > **Extensiones de kernel** para el perfil). En última instancia, Apple va a dejar en desuso las extensiones de kernel y las va a reemplazar por extensiones del sistema en una versión futura. Las extensiones del sistema se ejecutan en el espacio del usuario y no proporcionan acceso al kernel. El objetivo es aumentar la seguridad y proporcionar un mayor control al usuario final, a la vez que se limitan los ataques en el nivel de kernel. Tanto las extensiones de kernel como las del sistema permiten a los usuarios instalar extensiones de aplicaciones que amplían las funciones nativas del sistema operativo.

En Intune, puede configurar tanto extensiones de kernel como del sistema (**Dispositivos** > **Perfiles de configuración** > **macOS** para la plataforma > **Extensiones del sistema** para el perfil). Las extensiones de kernel se aplican a la versión 10.13.2 y más recientes. Las extensiones del sistema se aplican a la versión 10.15 y más recientes. Desde macOS 10.15 a macOS 10.15.4, las extensiones de kernel y del sistema se pueden ejecutar en paralelo. 

Para obtener información sobre las extensiones de kernel en dispositivos macOS, vea [Adición de extensiones de kernel de macOS](../configuration/kernel-extensions-overview-macos.md).

Se aplica a:
- macOS 10.15 y versiones más recientes

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscripción de dispositivos

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Los dispositivos de tipo Bring Your Own Device pueden usar la VPN para la implementación<!--5015344 -->
Es posible que esta característica se retrase.

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>Reducción del intervalo de sincronización automatizada de dispositivos a 12 horas<!--3077535 -->
Para la Inscripción de dispositivo automatizada de Apple, el intervalo de sincronización automatizada de dispositivos entre Intune y Apple Business Manager se reducirá de 24 a 12 horas. Para obtener más información sobre la sincronización, vea [Sincronización de dispositivos administrados](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Compatibilidad con Autopilot para dispositivos Hololens 2<!--6305220-->
Windows Autopilot será compatible con dispositivos Hololens 2. Para obtener más información sobre el uso de Autopilot en Intune, vea [Inscripción de dispositivos Windows en Intune con Windows Autopilot](../enrollment/enrollment-autopilot.md).

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>Las restricciones de inscripción admitirán etiquetas de ámbito<!--4209550 -->
Podrá asignar etiquetas de ámbito a las restricciones de inscripción. Para ello, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **Restricciones de inscripción** > **Crear restricción**. Cree cualquier tipo de restricción y verá la página **Etiquetas de ámbito**.

### <a name="shared-ipads-for-business--6367326---"></a>iPad compartidos para la empresa<!--6367326 -->
Podrá usar Intune y Apple Business Manager para configurar de forma fácil y segura un iPad compartido para que varios empleados puedan compartir dispositivos. [iPad compartido](https://developer.apple.com/education/shared-ipad/) de Apple proporciona una experiencia personalizada para varios usuarios a la vez que conserva los datos de usuario. Con un identificador de Apple administrado, los usuarios pueden acceder a sus aplicaciones, datos y configuraciones después de iniciar sesión en cualquier iPad compartido de su organización. iPad compartido funciona con identidades federadas.

Para ver esta característica, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **iOS** > **Inscripción de iOS** > **Tokens del programa de inscripción** > elija un token** > **Perfiles** > **Crear perfil** > **iOS**. En la página **Configuración de administración**, seleccione **Inscribir sin afinidad de usuario** y verá la opción **iPad compartido**.

**Se aplica a:** iPadOS 13.4 y versiones posteriores. En esta versión se ha agregado compatibilidad con sesiones temporales con iPad compartido para que los usuarios puedan acceder a un dispositivo sin un identificador de Apple administrado. Al cerrar sesión, el dispositivo borra todos los datos de usuario para que esté listo para su uso de forma inmediata, lo que elimina la necesidad de borrarlo. 

<!-- ***********************************************-->
## <a name="device-management"></a>Administración de dispositivos

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Compatibilidad de scripts de PowerShell con dispositivos BYOD<!-- 1862833  -->
Los scripts de PowerShell admitirán dispositivos registrados de Azure AD en Intune. Para más información sobre PowerShell, vea [Uso de scripts de PowerShell para dispositivos Windows 10 en Intune](../apps/intune-management-extension.md). Esta funcionalidad no es compatible con dispositivos que ejecutan Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics incluirá registros de detalles del dispositivo<!--6014987  -->
Habrá disponibles registros detallados del dispositivo de Intune en **Informes** > **Log Analytics**. Puede correlacionar los detalles del dispositivo para compilar consultas personalizadas y libros de Azure.


### <a name="macos-script-support---6376978----"></a>Compatibilidad con scripts de macOS<!-- 6376978  -->
La compatibilidad con scripts para macOS ya está disponible con carácter general. Además, se agregará compatibilidad con los scripts asignados por el usuario y los dispositivos macOS que se hayan inscrito con Inscripción de dispositivo automatizada de Apple (anteriormente Programa de inscripción de dispositivos). Para obtener más información, vea [Uso de scripts de shell para dispositivos macOS en Intune](../apps/macos-shell-scripts.md).

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Plantilla de informe de cumplimiento de Power BI V2.0<!-- 636958  -->
Los administradores podrán actualizar la versión de la plantilla de informe de cumplimiento de Power BI de V1.0 a V2.0. En V2.0 se incluirá un diseño mejorado, así como cambios en los cálculos y datos que se muestran como parte de la plantilla. Para obtener información relacionada, vea [Conexión con el almacenamiento de datos con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Seguridad

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Compatibilidad con credenciales derivadas para DISA Purebred en dispositivos Android<!--4839592 -->
Podrá usar *DISA Purebred* como un proveedor de [credenciales derivadas](../protect/derived-credentials.md) en dispositivos Android Enterprise totalmente administrados (**Administración de inquilinos** > **Conectores y tokens** > **Credenciales derivadas**). Se va a incluir compatibilidad para recuperar una credencial derivada de DISA Purebred. Se va a poder usar una credencial derivada para la autenticación de aplicaciones, Wi-Fi, VPN o la firma o el cifrado S/MIME en las aplicaciones que lo admitan. 

En abril, Intune agregó compatibilidad con *Entrust Datacard* y *Intercede* como proveedores de credenciales derivadas. 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Configuración de preferencias de privacidad para dispositivos macOS<!-- 2934232 --> 
Con el lanzamiento de macOS Catalina 10.15, Apple ha agregado nuevas mejoras de seguridad y privacidad. De forma predeterminada, las aplicaciones y los procesos no pueden acceder a datos específicos sin el consentimiento del usuario. Si los usuarios no proporcionan su consentimiento, es posible que las aplicaciones y los procesos no funcionen. Intune va a agregar compatibilidad con opciones que permiten a los administradores de TI permitir o impedir el consentimiento del acceso a datos en nombre de los usuarios finales en dispositivos que ejecuten macOS 10.14 y versiones posteriores. Estas opciones garantizarán que las aplicaciones y los procesos sigan funcionando correctamente y reducirán el número de mensajes que experimentan los usuarios finales.


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplicación de las directivas en Seguridad de los puntos de conexión<!-- 5892558   -->
Podrá seleccionar una directiva que haya creado en el nodo Seguridad de los puntos de conexión del Centro de administración de Microsoft Endpoint Manager y, después, duplicarla para crear una copia.  Entre las directivas que podrá duplicar se incluyen las que cree para: 

- Antivirus
- Cifrado de discos
- Firewall
- Detección de puntos de conexión y respuesta
- Reducción de la superficie expuesta a ataques
- Protección de cuentas

La duplicación realizará una copia de la directiva original, a la que puede cambiar el nombre y editar. La copia no incluirá las asignaciones de la original.

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Envío de notificaciones de inserción como acción de no cumplimiento <!-- 1733150   -->
En el caso de las plataformas iOS y Android, se va a agregar una nueva acción de no cumplimiento que enviará una notificación de inserción de aplicación a través de la aplicación Portal de empresa. Los usuarios pueden hacer clic en las notificaciones, que iniciarán la aplicación Portal de empresa, donde se mostrará el motivo del estado de no cumplimiento. Los administradores podrán configurar esta nueva acción de no cumplimiento en el Centro de administración de Microsoft Endpoint Manager. Para ello, hay que ir a **Dispositivos** > **Directivas de cumplimiento** > **Crear directiva** y seleccionar la *Acción* para enviar una notificación de inserción de aplicación. 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Nuevo perfil de directiva de firewall de seguridad de los puntos de conexión<!-- 5653324   -->
Como versión preliminar, se va a agregar un perfil adicional para Windows 10 y versiones posteriores a la directiva de firewall de Seguridad de los puntos de conexión de Intune (**Seguridad de los puntos de conexión** > **Firewall** > **Crear directiva** > seleccione **Windows 10 y versiones posteriores**). 

Cada instancia de este nuevo perfil admite hasta 150 *reglas de Firewall de Microsoft Defender* personalizadas. El perfil de reglas de Firewall de Microsoft Defender permite definir reglas de firewall de Windows granulares para permitir o bloquear puertos y aplicaciones en Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vea también

Consulte [Novedades de Microsoft Intune](whats-new.md) para obtener más información sobre los desarrollos recientes.



