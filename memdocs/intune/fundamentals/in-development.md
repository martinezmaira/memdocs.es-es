---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5562ef1eaa1cc98e3f5a654e90e4779e228768b6
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311210"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>Mejoras en la página Dispositivos de iOS/iPadOS y los portales de empresa de macOS<!-- 6055001  -->
Hemos realizado varias mejoras en la experiencia del usuario de la página **Dispositivos** de la aplicación Portal de empresa para iOS/iPadOS y Mac. Hemos renovado la página **Dispositivos** para tener un espíritu más moderno y una mejor organización de la información del dispositivo. Mediante el uso de una sola columna con encabezados de sección definidos, los usuarios de iOS/iPadOS y macOS de la organización podrán comprobar fácilmente el estado de sus dispositivos para asegurarse de que están seguros y mantienen el acceso a los recursos de su organización. Además, hemos agregado una mensajería más clara y pasos adicionales de solución de problemas para los usuarios cuyos dispositivos no cumplen los requisitos. Para más información sobre el Portal de empresa de Intune, consulte [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md).

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Mejoras en el Portal de empresa para la experiencia de inscripción de macOS<!-- 6444452  -->
La experiencia de inscripción del Portal de empresa para macOS cuenta con un proceso de inscripción más sencillo que es más coherente con la experiencia de inscripción en el Portal de empresa para iOS. Los usuarios del dispositivo verán:  
- Una interfaz de usuario más elegante.  
- Una lista de comprobación de inscripción mejorada.  
- Instrucciones más claras sobre cómo inscribir sus dispositivos.  
- Mejores opciones de solución de problemas.  

Para más información sobre el Portal de empresa de Intune, consulte [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md).

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>Uso de la configuración de modo de aplicación única autónoma para configurar el Portal de empresa de iOS con el fin de que sea una aplicación de inicio y cierre de sesión<!-- 7055619  -->
Podrá configurar el Portal de empresa de iOS para usar el modo de aplicación única autónoma (ASAM). Puede usar la configuración de ASAM en la consola de Microsoft Endpoint Manager para configurar el Portal de empresa de iOS para entrar y salir del modo de aplicación única al cerrar la sesión e iniciarla. Cuando el Portal de empresa está en ASAM, los usuarios no podrán usar ninguna otra aplicación o el botón de inicio del dispositivo hasta que inicien sesión en el Portal de empresa. Al cerrar sesión, el Portal de empresa volverá a estar en modo de aplicación única. 

Para configurar el Portal de empresa para que esté en ASAM en Microsoft Endpoint Manager, seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**. Seleccione **iOS/iPadOS** como plataforma y seleccione **Restricciones de dispositivos** como perfil. En la pestaña **Opciones de configuración**, seleccione **Modo de aplicación única autónoma**. Establezca el **nombre de la aplicación** en `Company Portal` y establezca el **identificador de lote de aplicaciones** en `com.app.CompanyPortal`. Para más información, consulte [Modo de aplicación única autónoma (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) y [Modo de aplicación única](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuración del dispositivo

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Establecimiento del estado de cumplimiento de dispositivos desde partners de MDM de terceros<!-- 6361689   -->
Pronto podrá permitir el estado de cumplimiento de los dispositivos iOS o Android administrados por partners de la administración de dispositivos móviles (MDM) de terceros en Azure Active Directory (Azure AD).

Cuando Intune está configurado para la compatibilidad con los partners, los datos de cumplimiento de los dispositivos administrados por el partners de MDM de terceros se envían a Intune para la evaluación de cumplimiento. Los resultados se pasan a Azure AD, donde se usan los datos de cumplimiento para aplicar las directivas de acceso condicional para esos dispositivos.

Pronto se incluirán los siguientes asociados:
- VMware WorkspaceONE (conocido anteriormente como AirWatch)

Para habilitar un asociado de cumplimiento de dispositivos, usará un nuevo nodo en el centro de administración de Microsoft Endpoint Manager: **Administración de inquilinos** > **Conectores y tokens** > **Administración de cumplimiento de partners**, donde seleccionará **Agregar partner de cumplimiento**.

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Adición de un vínculo al sitio web de soporte técnico de Portal de empresa en correos electrónicos por incumplimiento<!-- 7225498    -->
Estamos agregando una nueva configuración a la plantilla de notificación de correo electrónico que agregará el vínculo al sitio web del Portal de empresa a las notificaciones de correo electrónico que se envían a los usuarios de dispositivos no compatibles. (**Seguridad de punto de conexión** > **Conformidad de dispositivos** > **Notificaciones** > **Crear notificación**).  Los usuarios que reciben un correo electrónico debido a que tienen un dispositivo no compatible pueden usar el vínculo para abrir un sitio web y obtener más información sobre por qué su dispositivo no es compatible.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nueva configuración de FileVault para la directiva de configuración de dispositivos Endpoint Protection de macOS<!-- 5459801   -->
Se va a agregar una opción nueva a la categoría FileVault dentro de la plantilla [Endpoint Protection de macOS](../protect/endpoint-protection-macos.md): Ocultar clave de recuperación. (**Dispositivos** > **Perfiles de configuración** > **Crear perfil**, seleccione **macOS** para la *Plataforma* y, después, **Endpoint Protection** para el *Tipo de perfil*). Esta opción oculta la clave personal del usuario final durante el cifrado de FileVault 2. Un usuario del dispositivo puede ver su clave de recuperación personal en cualquier momento desde la aplicación Portal de empresa de iOS o desde el sitio web del Portal de empresa para el dispositivo macOS cifrado. Para ver la clave de recuperación personal, puede ir a los detalles del dispositivo y hacer clic en *Obtener clave de recuperación*.

Esta opción no estará disponible en una directiva creada anteriormente. Tendrá que volver a crear las directivas de FileVault para configurar esta opción y poder usarla. 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>Configuración del almacenamiento en caché de contenido en dispositivos macOS<!-- 7106872 -->
En los dispositivos macOS, puede crear un perfil de configuración que configure el almacenamiento en caché de contenido (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** como plataforma > **Características del dispositivo** para tipo de perfil). Use esta configuración para eliminar la caché, permitir la caché compartida, establecer un límite de caché en el disco y mucho más.

Para más información sobre el almacenamiento en caché de contenido, consulte [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (abre el sitio web de Apple).

Para ver los valores que puede configurar actualmente, consulte [Configuración de características de dispositivos macOS en Intune](../configuration/macos-device-features-settings.md).

Se aplica a:
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nueva configuración de VPN para dispositivos Windows 10 y versiones más recientes<!-- 6602122  -->
Cuando se crea un perfil de VPN mediante el tipo de conexión de IKEv2, hay nuevas opciones que puede configurar(**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Windows 10 y posteriores** como plataforma > **VPN** para el perfil > **VPN base**):

- **Túnel de dispositivos**: Permite que los dispositivos se conecten automáticamente a VPN sin necesidad de interacción del usuario, incluido el inicio de sesión del usuario. Esta característica requiere que se habilite **Always On** y que se usen **certificados de máquina** como método de autenticación.
- Configuración de Cryptography Suite: Configure los algoritmos que se usan para proteger las asociaciones de seguridad IKE y secundarias, que permiten hacer coincidir la configuración de cliente y servidor.

Para ver las opciones que puede configurar, vaya a [Configuración de dispositivos con Windows 10 y Windows Holographic para agregar conexiones VPN mediante Intune](../configuration/vpn-settings-windows-10.md).

Se aplica a:
- Windows 10 y versiones posteriores

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>Bloqueo de sesiones temporales de iPad compartidas en dispositivos iPad compartidos<!-- 6613794 -->
En Intune, hay una nueva opción para **bloquear sesiones temporales de iPad compartidas en dispositivos iPad compartidos** (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** como plataforma > **Restricciones de dispositivos** para tipo de perfil > **iPad compartido**). Cuando está habilitada, los usuarios finales no pueden usar la cuenta de invitado. Deben iniciar sesión en el dispositivo con el identificador y la contraseña de Apple administrados. 

Para más información sobre los valores que puede configurar, consulte [Configuración de dispositivos iOS e iPadOS para permitir o restringir características mediante Intune](../configuration/device-restrictions-ios.md).

Se aplica a:
- Dispositivos iPad compartidos que ejecutan iOS/iPadOS 13.4 y versiones más recientes

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>Uso de Microsoft Launcher como iniciador predeterminado para dispositivos empresariales Android totalmente administrados<!-- 4927976  -->
En los dispositivos del propietario de dispositivos de Android Enterprise, puede configurar Microsoft Launcher como el iniciador predeterminado para dispositivos totalmente administrados (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise**como plataforma > **Propietario del dispositivo** > **restricciones de dispositivos** para el perfil > **Experiencia de dispositivo**). Para configurar el resto de la configuración de Microsoft Launcher, use directivas de configuración de aplicaciones. 

Además, hay otras actualizaciones de la interfaz de usuario, entre las que se incluyen **Dispositivos dedicados**, cuyo nombre cambia a **Experiencia de dispositivo**.

Para ver los valores que puede restringir, consulte [Configuración de dispositivos Android Enterprise para permitir o restringir características mediante Intune](../configuration/device-restrictions-android-for-work.md). 

Se aplica a:
- Dispositivos totalmente administrados del propietario del dispositivo Android Enterprise (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>Agregue una nueva configuración de esquema y busque la configuración de esquema existente con OEMConfig en Android Enterprise.<!-- 6394386  -->
En Intune, puede usar OEMConfig para administrar la configuración de los dispositivos Android Enterprise (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** para plataforma > **OEMConfig** para el perfil). Al usar **Diseñador de configuraciones**, se muestran las propiedades del esquema de la aplicación. Ahora, en **Diseñador de configuraciones**, puede:
- Agregar una nueva configuración al esquema de la aplicación.
- Buscar valores nuevos y existentes en el esquema de la aplicación.

Para más información sobre los perfiles OEMConfig en Intune, consulte [Uso y administración de dispositivos Android Enterprise con OEMConfig en Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Se aplica a:
- Android Enterprise

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscripción de dispositivos

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Errores de sincronización de inscripción de dispositivos automatizada<!-- 6988214 -->
Se notificarán nuevos errores para iOS/iPadOS y para dispositivos macOS, incluido lo siguiente:
- Caracteres no válidos en el número de teléfono o si el campo está vacío. 
- Nombre de configuración no válido o vacío en el perfil. 
- Valor de cursor no válido o expirado, o si no se encuentra ningún cursor.
- Token rechazado o expirado. 
- El campo Departamento está vacío o la longitud es demasiado larga. 
- Apple no encuentra el perfil y se debe crear uno nuevo. 
- Se agregará un recuento de los dispositivos de Apple Business Manager eliminados a la página de información general en la que verá el estado de los dispositivos.

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Los dispositivos de tipo Bring Your Own Device pueden usar la VPN para la implementación<!--5015344 -->
Es posible que esta característica se retrase.

### <a name="shared-ipads-for-business--6367326---"></a>iPad compartidos para la empresa<!--6367326 -->
Podrá usar Intune y Apple Business Manager para configurar de forma fácil y segura un iPad compartido para que varios empleados puedan compartir dispositivos. [iPad compartido](https://developer.apple.com/education/shared-ipad/) de Apple proporciona una experiencia personalizada para varios usuarios a la vez que conserva los datos de usuario. Con un identificador de Apple administrado, los usuarios pueden acceder a sus aplicaciones, datos y configuraciones después de iniciar sesión en cualquier iPad compartido de su organización. iPad compartido funciona con identidades federadas.

Para ver esta característica, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivos** > **iOS** > **Inscripción de iOS** > **Tokens del programa de inscripción** > elija un token > **Perfiles** > **Crear perfil** > **iOS**. En la página **Configuración de administración**, seleccione **Inscribir sin afinidad de usuario** y verá la opción **iPad compartido**.

**Se aplica a:** iPadOS 13.4 y versiones posteriores. En esta versión se ha agregado compatibilidad con sesiones temporales con iPad compartido para que los usuarios puedan acceder a un dispositivo sin un identificador de Apple administrado. Al cerrar sesión, el dispositivo borra todos los datos de usuario para que esté listo para su uso de forma inmediata, lo que elimina la necesidad de borrarlo. 

<!-- ***********************************************-->
## <a name="device-management"></a>Administración de dispositivos

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>Cambio del usuario primario en los dispositivos administrados conjuntamente<!--7319183 -->
Podrá cambiar el usuario primario de un dispositivo para dispositivos Windows administrados conjuntamente. Para más información sobre cómo buscarlo y cambiarlo, consulte [Búsqueda del usuario primario de un dispositivo de Intune](../remote-actions/find-primary-user.md).

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Compatibilidad de scripts de PowerShell con dispositivos BYOD<!-- 1862833  -->
Los scripts de PowerShell admitirán dispositivos registrados de Azure AD en Intune. Para más información sobre PowerShell, vea [Uso de scripts de PowerShell para dispositivos Windows 10 en Intune](../apps/intune-management-extension.md). Esta funcionalidad no es compatible con dispositivos que ejecutan Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics incluirá registros de detalles del dispositivo<!--6014987  -->
Habrá disponibles registros detallados del dispositivo de Intune en **Informes** > **Log Analytics**. Puede correlacionar los detalles del dispositivo para compilar consultas personalizadas y libros de Azure.

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Al establecer el usuario primario de Intune, también se establece la propiedad del propietario de Azure AD.<!--7319227 -->
Esta próxima característica establece automáticamente la propiedad del propietario en los dispositivos unidos a Azure AD híbrido recién inscritos al mismo tiempo que se establece el usuario primario de Intune. Para más información sobre el usuario primario, consulte [Búsqueda del usuario primario de un dispositivo de Intune](../remote-actions/find-primary-user.md).

Se trata de un cambio en el proceso de inscripción y solo se aplica a los dispositivos recién inscritos. En el caso de los dispositivos unidos a Azure AD híbrido existentes, debe actualizar manualmente la propiedad del propietario de Azure AD. Para ello, puede usar la característica [Cambiar el usuario primario](../remote-actions/find-primary-user.md#change-a-devices-primary-user) o [un script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

Cuando los dispositivos Windows 10 se unen a un directorio de Azure Active Directory híbrido, el primer usuario del dispositivo se convierte en el usuario primario de Endpoint Manager.  Actualmente, el usuario no está establecido en el objeto de dispositivo de Azure AD correspondiente. Esto produce una incoherencia al comparar la propiedad de *propietario* de un portal de Azure AD con la propiedad de *usuario primario* en el centro de administración de Microsoft Endpoint Manager. La propiedad de propietario de Azure AD se usa para proteger el acceso a las claves de recuperación de BitLocker. La propiedad no se rellena en los dispositivos unidos a Azure AD híbrido. Esta limitación evita la configuración del autoservicio de recuperación de BitLocker desde Azure AD. Esta próxima característica resuelve esta limitación.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Asociación de inquilinos: escala de tiempo del dispositivo en el centro de administración<!--7220536, CM7141381 -->
Cuando Configuration Manager sincroniza un dispositivo con Microsoft Endpoint Manager de Microsoft a través de una asociación de inquilinos, podrá ver una escala de tiempo de eventos. Esta escala de tiempo muestra la actividad pasada en el dispositivo que puede ayudarle a solucionar problemas. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Asociación de inquilinos: instalación de una aplicación desde el centro de administración<!-- 7220536, CM6024389 -->
Ahora podrá iniciar la instalación de una aplicación en tiempo real para un dispositivo asociado al inquilino desde el centro de administración de Microsoft Endpoint Management. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Asociación de inquilinos: CMPivot desde el centro de administración<!--7220536, CM6024392 -->
Podrá incorporar la eficacia de [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) al centro de administración de Microsoft Endpoint Manager. Permita que otros roles, como el de Departamento de soporte técnico, puedan iniciar consultas en tiempo real desde la nube en un dispositivo individual administrado por ConfigMgr y devolver los resultados al centro de administración. Esto proporciona todas las ventajas tradicionales de CMPivot, permitiendo a los administradores de TI y a otros roles designados evaluar rápidamente el estado de los dispositivos en su entorno y tomar medidas. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Asociación de inquilinos: ejecución de scripts desde el centro de administración<!--7220536, CM6234688 -->
Podrá incorporar la eficacia de la característica [Ejecutar scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) local de Configuration Manager al centro de administración de Microsoft Endpoint Manager. Permita que otros roles, como el de Departamento de soporte técnico, ejecuten scripts de PowerShell desde la nube en un dispositivo administrado de Configuration Manager individual. Esto proporciona todas las ventajas tradicionales de los scripts de PowerShell que ya se han definido y aprobado por el administrador de Configuration Manager en este nuevo entorno. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nueva lógica de combinación para dispositivos Windows 10<!--179048-->
En la actualidad, si un cliente restablece la imagen inicial de un dispositivo y luego lo vuelve a inscribir, aparecerán varios registros para el dispositivo en la consola de administración de Microsoft Endpoint Manager. La nueva lógica de combinación está en desarrollo para combinar estos registros duplicados para dispositivos Windows 10.

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>Disponibilidad del pin de bloqueo remoto para dispositivos macOS<!--7281557-->
La disponibilidad de los pin de bloqueo remoto para dispositivos macOS aumentará de 7 a 30 días.

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
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vea también

Consulte [Novedades de Microsoft Intune](whats-new.md) para obtener más información sobre los desarrollos recientes.
