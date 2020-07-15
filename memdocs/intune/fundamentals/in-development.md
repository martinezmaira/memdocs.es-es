---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5afca831e2f3cbcda69150adcbbcff996bf99554
ms.sourcegitcommit: 01c1ca337e82c5e8e92153079ed89f79e20bde9e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86157814"
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

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>S/MIME para Outlook en dispositivos iOS y Android Enterprise administrados sin inscripción<!-- 6517155  -->
Podrá habilitar S/MIME para Outlook en dispositivos iOS y Android Enterprise mediante las directivas de configuración de aplicaciones para dispositivos administrados sin inscripción. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones** > **Agregar** > **Aplicaciones administrados**. Además, puede elegir si quiere permitir que los usuarios cambien esta configuración en Outlook. Para más información sobre la configuración de Outlook, consulte [Opciones de configuración de Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>El Portal de empresa de iOS admitirá la Inscripción de dispositivos automatizada de Apple sin afinidad de usuario<!-- 7282707  --> 
Este portal se admitirá en los dispositivos inscritos con la Inscripción de dispositivos automatizada de Apple sin necesidad de un usuario asignado. Un usuario final puede iniciar sesión en el Portal de empresa de iOS para establecerse como usuario primario de un dispositivo iOS o iPad inscrito sin afinidad de dispositivo. Para más información sobre la Inscripción de dispositivos automatizada, consulte [Inscripción automática de dispositivos iOS/iPadOS con Inscripción de dispositivos automatizada de Apple](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Notificaciones de instalación de aplicaciones Win32 y el Portal de empresa<!-- 7485945  -->
Los usuarios finales podrán decidir si las aplicaciones que se muestran en el [Portal de empresa web de Microsoft Intune](https://portal.manage.microsoft.com/) deben abrirse con la aplicación del Portal de empresa o con el Portal de empresa web. Esta opción solo está disponible si el usuario final tiene instalada la aplicación del Portal de empresa e inicia una aplicación del Portal de empresa web fuera de un explorador.

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>El Portal de empresa agrega compatibilidad con las aplicaciones de Configuration Manager<!-- 4297660 -->
El Portal de empresa ahora admite aplicaciones de Configuration Manager. Esta característica permite a los usuarios finales ver las aplicaciones implementadas de Configuration Manager y de Intune en el Portal de empresa de los clientes administrados conjuntamente. Esta compatibilidad ayuda a los administradores a consolidar sus diferentes experiencias del portal de usuario final. Para más información, consulte [Uso de la aplicación Portal de empresa en dispositivos administrados conjuntamente](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuración del dispositivo

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Establecimiento del estado de cumplimiento de dispositivos desde partners de MDM de terceros<!-- 6361689   -->
Los clientes de Microsoft 365 que posean soluciones de MDM de terceros podrán aplicar directivas de acceso condicional para aplicaciones de Microsoft 365 en iOS y Android a través de la integración con el servicio de cumplimiento de dispositivos de Microsoft Intune. Un proveedor de MDM de terceros aprovechará el servicio Cumplimiento de dispositivos de Intune para enviar datos de cumplimiento de dispositivos a Intune. Después, Intune evaluará para determinar si el dispositivo es de confianza y establecerá los atributos de acceso condicional en Azure AD.  A los clientes se les pedirá que establezcan directivas de acceso condicional de Azure AD desde el centro de administración de Microsoft Endpoint Manager o desde el portal de Azure AD.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nueva configuración de VPN para dispositivos Windows 10 y versiones más recientes<!-- 6602122  -->
Cuando se crea un perfil de VPN mediante el tipo de conexión de IKEv2, hay nuevas opciones que puede configurar(**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Windows 10 y posteriores** como plataforma > **VPN** para el perfil > **VPN base**):

- **Túnel de dispositivos**: permite que los dispositivos se conecten automáticamente a una VPN sin necesidad de la interacción del usuario; no es necesario siquiera que el usuario inicie la sesión. Esta característica requiere que se habilite **Always On** y que se usen **certificados de máquina** como método de autenticación.
- Configuración de Cryptography Suite: Configure los algoritmos que se usan para proteger las asociaciones de seguridad IKE y secundarias, que permiten hacer coincidir la configuración de cliente y servidor.

Para ver las opciones que puede configurar, vaya a [Configuración de dispositivos con Windows 10 y Windows Holographic para agregar conexiones VPN mediante Intune](../configuration/vpn-settings-windows-10.md).

Se aplica a:
- Windows 10 y versiones posteriores

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Nuevas características de Managed Home Screen en los dispositivos dedicados del propietario del dispositivo de Android Enterprise (COSU)<!-- 7414175 7133328 7133720 7134873 7135184  -->
En los dispositivos Android Enterprise, los administradores podrán usar perfiles de configuración de dispositivos para personalizar Managed Home Screen en dispositivos dedicados mediante el modo de pantalla completa de varias aplicaciones (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** para la plataforma > **Solo el propietario del dispositivo** > **Restricciones de dispositivo** para el perfil > **Device experience** [Experiencia de dispositivo]).

En concreto, puede:

- Personalizar iconos, cambiar la orientación de la pantalla y mostrar notificaciones de aplicaciones en los iconos de distintivos <!--7414175-->
- Ocultar el punto de entrada de configuración administrada <!--7133328-->
- Acceso más sencillo al menú de depuración <!--7133720-->
- Crear una lista permitida de redes Wi-Fi <!-- 7134873-->
- Acceso más sencillo a la información del dispositivo <!-- 7135184-->

Para más información, consulte [Configuración de dispositivos Android Enterprise para permitir o restringir características](../configuration/device-restrictions-android-for-work.md).

Se aplica a:

- Dispositivos dedicados administrados del propietario del dispositivo Android Enterprise (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscripción de dispositivos

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>Dispositivos corporativos con habilitación personal (versión preliminar)<!--4442275 -->
Intune admitirá dispositivos corporativos de Android con un perfil de trabajo para versiones de sistema operativo Android 8 y posterior. Los dispositivos corporativos con un perfil de trabajo son uno de los escenarios de administración corporativa del conjunto de soluciones de Android Enterprise. Este escenario va destinado a dispositivos de usuario únicos para uso personal y corporativo. Este escenario de propiedad corporativa y con habilitación personal (COPE) ofrece lo siguiente:

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



<!-- ***********************************************-->
## <a name="device-management"></a>Administración de dispositivos

### <a name="device-compliance-logs-now-in-english--6014904---"></a>Registros de cumplimiento de dispositivos ahora en inglés<!--6014904 -->
Los registros de IntuneDeviceComplianceOrg solo tienen enumeraciones para ComplianceState, OwnerType y DeviceHealthThreatLevel. En una actualización futura, estos registros tendrán información en inglés en las columnas.

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

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nueva lógica de combinación para dispositivos Windows 10<!--179048-->
En la actualidad, si un cliente restablece la imagen inicial de un dispositivo y luego lo vuelve a inscribir, aparecerán varios registros para el dispositivo en la consola de administración de Microsoft Endpoint Manager. La nueva lógica de combinación está en desarrollo para combinar estos registros duplicados para dispositivos Windows 10.

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>Actualizaciones de la acción de bloqueo remoto para dispositivos macOS<!--7032805 -->
Las actualizaciones de la acción de bloqueo remoto para dispositivos macOS incluirán:
- El PIN de recuperación se mostrará durante 30 días (en lugar de siete) antes de la eliminación.
- Si un administrador tiene abierto un segundo explorador e intenta volver a desencadenar el comando desde otra pestaña o explorador, Intune permitirá que el comando pase. Sin embargo, el estado de los informes se establecerá como erróneo en lugar de generar un nuevo PIN.
- El administrador no podrá emitir otro comando de bloqueo remoto si el anterior todavía está pendiente o si el dispositivo no se ha vuelto a sincronizar.
Estos cambios están diseñados para impedir que se sobrescriba el PIN correcto después de varios comandos de bloqueo remoto.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Implementación de actualizaciones de software en dispositivos macOS <!-- 3194876 -->
Podrá implementar actualizaciones de software en grupos de dispositivos macOS. Esta característica incluye, entre otras, actualizaciones de archivos críticos, de archivos de configuración y del firmware. Podrá enviar actualizaciones en la siguiente sincronización de dispositivos o seleccionar una programación semanal para implementar actualizaciones dentro o fuera de los períodos que establezca. De esta manera, podrá actualizar los dispositivos fuera de las horas de trabajo estándar o cuando el departamento de soporte técnico tiene a todo el personal ocupado. También obtendrá un informe detallado de todos los dispositivos macOS con actualizaciones implementadas. Puede profundizar en el informe en función de cada dispositivo para ver los estados de determinadas actualizaciones.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>Propiedades adicionales de Data Warehouse v1.0<!-- 6125732   -->
Hay otras propiedades disponibles mediante Intune Data Warehouse v1.0. Las propiedades siguientes se exponen ahora por medio de la entidad [dispositivos](../developer/reports-ref-devices.md#devices):
- `ethernetMacAddress`: identificador de red único de este dispositivo.
- `office365Version`: versión de Office 365 instalada en el dispositivo.

Las propiedades siguientes ahora se exponen por medio de la entidad [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories):
- `physicalMemoryInBytes`: memoria física en bytes.
- `totalStorageSpaceInBytes`: capacidad total de almacenamiento en bytes.

Para obtener más información, vea [API de Data Warehouse de Microsoft Intune](../developer/reports-nav-intune-data-warehouse.md).

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Plantilla de informe de cumplimiento de Power BI V2.0<!-- 636958  -->
Los administradores podrán actualizar la versión de la plantilla de informe de cumplimiento de Power BI de V1.0 a V2.0. En V2.0 se incluirá un diseño mejorado, así como cambios en los cálculos y los datos que se muestran como parte de la plantilla. Para obtener información relacionada, vea [Conexión con el almacenamiento de datos con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Control de acceso basado en roles.

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Compatibilidad de etiquetas de ámbito con directivas de personalización<!--6182440 -->
Podrá asignar etiquetas de ámbito a las directivas de personalización. Para ello, vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Administración de inquilinos**> **Personalización** donde verá las opciones de configuración de **Etiquetas de ámbito**.

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>Cambios de los permisos Asignar perfil y Actualizar perfil<!--7177586 -->
Los permisos de control de acceso basado en rol cambiarán en Asignar perfil y Actualizar perfil:
- Asignar perfil: los administradores con este permiso también podrán asignar los perfiles a los tokens y asignar un perfil predeterminado a un token.
- Actualizar perfil: los administradores con este permiso solo podrán actualizar los perfiles existentes.

<!-- ***********************************************-->
## <a name="security"></a>Seguridad

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Compatibilidad de la directiva de protección de aplicaciones con Symantec Endpoint Security y Check Point Sandblast<!--  4452423, 4731168 -->

En octubre de 2019, la directiva de protección de aplicaciones de Intune agregó la capacidad de usar datos de algunos de nuestros asociados de Microsoft Threat Defense (MTD). Estamos agregando compatibilidad con los siguientes asociados para usar una directiva de protección de aplicaciones que bloquee o elimine de forma selectiva los datos corporativos de los usuarios en función del estado de un dispositivo:

- **Check Point Sandblast** en Android, iOS y iPadOS
- **Symantec Endpoint Security** en Android, iOS y iPadOS

Para más información sobre el uso de la directiva de protección de aplicaciones con asociados de MTD, consulte [Creación de una directiva de protección de aplicaciones de Mobile Threat Defense con Intune](../protect/mtd-app-protection-policy.md).

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>Almacenamiento de la clave de recuperación de un dispositivo macOS cifrado con FileVault antes de inscribirlo en Intune<!--5239424   -->
Pronto, los usuarios finales de un dispositivo macOS que no se cifró mediante la directiva FileVault de Intune, o que se cifró antes de inscribirlo en Intune, no tendrán que descifrar el dispositivo para que Intune pueda volver a cifrarlo. En cambio, el cifrado actual puede permanecer en su lugar y el usuario puede ir al sitio web del Portal de empresa, donde puede elegir *Store recovery key* (Almacenar la clave de recuperación) para enviar la clave de recuperación personal del dispositivo macOS cifrado. Tras el envío de una clave válida, Intune rotará la clave personal para generar una nueva, que permanecerá a disposición del usuario mediante el sitio web del Portal de empresa, el Portal de empresa o de iOS, el Portal de empresa de Android o la aplicación de Intune. Así, los usuarios pueden acceder a esas ubicaciones desde cualquier dispositivo para ver la clave en caso de que se bloquee su dispositivo macOS.

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>Ocultación de la clave de recuperación personal de un usuario de dispositivo durante el cifrado de disco de FileVault de macOS<!--  5475632  -->
Vamos a agregar un nuevo valor llamado *Hide recovery key* (Ocultar la clave de recuperación) a la directiva de cifrado de discos de seguridad de punto de conexión de FileVault (**Seguridad de los puntos de conexión** > **Cifrado de disco** > **Crear perfil** > **macOS** > **FileVault**). Cuando se habilita la nueva configuración, Intune oculta la clave de recuperación personal al usuario del dispositivo macOS durante el cifrado. Ocultar la clave en este momento, puede ayudar a protegerla, ya que los usuarios no podrán anotarla mientras esperan a que el dispositivo se cifre. En cambio, si se necesita recuperación, un usuario siempre puede usar cualquier dispositivo para ver su clave de recuperación personal mediante el sitio web del Portal de empresa de Intune.

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>Vista mejorada de los detalles de base de referencia de seguridad de los dispositivos<!-- 5536846   -->
Estamos trabajando para mejorar la visualización de la configuración de base de referencia de seguridad, cuando profundiza en los detalles de un dispositivo (**Seguridad de los puntos de conexión** > **Dispositivos**).  Para cada base de referencia de seguridad asignada, podrá ver una lista plana de los detalles de cada opción de configuración que incluye las categorías de las opciones de configuración, los nombres de las opciones de configuración y el estado de cada opción de configuración en ese dispositivo.

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>Administración de las ubicaciones de origen de las actualizaciones de definiciones con la directiva antivirus de seguridad de puntos de conexión para dispositivos Windows 10<!-- 6347801  -->  
Vamos a agregar dos nuevas opciones de configuración a la categoría *Actualizaciones* de la directiva antivirus de seguridad de puntos de conexión de dispositivos Windows 10 que puede ayudarlo a administrar la forma en que los dispositivos obtienen definiciones de actualización (**Seguridad de los puntos de conexión** > ** Antivirus** > **Crear directiva** > **Windows 10 y versiones posteriores** > **Microsoft Defender Antivirus**).

Con la nueva configuración, podrá agregar recursos compartidos de archivos UNC como ubicaciones de origen de descarga para las actualizaciones de definiciones, y definir el orden en el que se establece comunicación con las distintas ubicaciones de origen. La nueva configuración administrará los siguientes CSP de Defender:

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>La directiva de detección de puntos de conexión y respuesta para la incorporación de dispositivos de asociación de inquilinos a MDATP se va a mover de la versión preliminar<!-- 7303816   -->
Como parte de la seguridad de los puntos de conexión en Intune, la compatibilidad de las directivas de detección de puntos de conexión y respuesta (EDR) para su uso con dispositivos administrados por Configuration Manager pronto pasará de la versión preliminar a la disponibilidad con carácter general (**Seguridad de los puntos de conexión** > **Detección de puntos de conexión y respuesta** > **Crear directiva** > **Windows 10 y Windows Server**). Al configurar la [asociación de inquilinos para Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md), puede usar las directivas EDR para incorporar dispositivos administrados por Configuration Manager a Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender). 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>Mejoras del nodo de bases de referencia de seguridad<!-- 7433136   -->
Para mejorar la usabilidad del nodo de línea base de seguridad del centro de administración de Endpoint Manager, vamos a quitar la pestaña *Información general* de cada línea base y a abrir la pestaña **Perfil** de las líneas base (**Seguridad de los puntos de conexión** > **Líneas base de seguridad** > *línea base*).

La página *Información general* de cada línea base muestra los gráficos y los iconos que agregan los resultados de la última versión de línea base implementada. Esa información se duplica con respecto a lo que ve si profundiza en una versión para obtener más información. Una vez que se ha quitado la página *Información general*, esos gráficos y detalles agregados seguirán estando disponibles cuando profundice en la versión directamente.  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>Versión preliminar de la herramienta de migración de reglas de firewall<!-- 6423187  -->
Estamos trabajando en la versión preliminar pública de una herramienta basada en PowerShell que migrará las reglas de firewall de Windows Defender. Al instalar y ejecutar la herramienta, se crean automáticamente directivas de reglas de firewall de seguridad de los puntos de conexión para Intune basadas en la configuración actual de un cliente de Windows 10.

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>Nueva configuración del perfil de control de dispositivos de la directiva de reducción de la superficie expuesta a ataques de seguridad de los puntos de conexión<!--7032084 -->
Vamos a agregar varias opciones de configuración para dispositivos Windows 10 al perfil de control de dispositivos para la directiva de reducción de la superficie expuesta a ataques de los puntos de conexión (**Seguridad de los puntos de conexión** > **Reducción de la superficie expuesta a ataques** > **Crear directiva** > **Windows 10 y versiones posteriores** > **Control de dispositivos**). 

La nueva configuración será la misma que la que está disponible actualmente en [Perfiles de restricción de dispositivos](../configuration/device-restrictions-windows-10.md) para *Configuración de dispositivos*. La configuración que se agrega al perfil de *Control de dispositivos* debe incluir varias opciones de configuración de Bluetooth.  


<!-- ***********************************************-->
## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vea también

Consulte [Novedades de Microsoft Intune](whats-new.md) para obtener más información sobre los desarrollos recientes.
