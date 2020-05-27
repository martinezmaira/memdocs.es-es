---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764210"
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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Portal de empresa para Android guiará a los usuarios para obtener aplicaciones después de la inscripción del perfil de trabajo <!-- 6103999  -->
Se van a mejorar las instrucciones en la aplicación del Portal de empresa para facilitar a los usuarios la búsqueda e instalación de aplicaciones.  Después de la inscripción en la administración del perfil de trabajo, los usuarios verán un mensaje que les indica que pueden encontrar aplicaciones sugeridas en la versión con distintivo de Google Play. Los usuarios también verán un nuevo vínculo **Obtener aplicaciones** en el cajón de Portal de empresa de la izquierda. Para dejar espacio a estas experiencias nuevas y mejoradas, se quitará la pestaña **APLICACIONES**. 

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuración del dispositivo

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Las opciones y valores de los perfiles de configuración de dispositivos se actualizarán para las plataformas Windows<!-- 4091122 -->
Al crear perfiles de configuración de dispositivos para plataformas Windows (**Dispositivos** > **Perfiles de configuración** >  **Crear perfil** > cualquier opción **Windows** para la plataforma), algunas opciones y sus valores son diferentes del CSP y pueden ser confusos. Los nombres de las opciones y sus valores se actualizarán para que sean más claros.

Se aplica a:

- Perfiles de configuración de dispositivos Windows 10 y versiones posteriores
- Perfiles de configuración de dispositivos Windows Holographic for Business
- Perfiles de configuración de dispositivos Windows 8.1
- Perfiles de configuración de dispositivos Windows Phone 8.1

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nueva configuración de FileVault para la directiva de configuración de dispositivos Endpoint Protection de macOS<!-- 5459801   -->
Se va a agregar una opción nueva a la categoría FileVault dentro de la plantilla [Endpoint Protection de macOS](../protect/endpoint-protection-macos.md): Ocultar clave de recuperación. (**Dispositivos** > **Perfiles de configuración** > **Crear perfil**, seleccione **macOS** para la *Plataforma* y, después, **Endpoint Protection** para el *Tipo de perfil*). Esta opción oculta la clave personal del usuario final durante el cifrado de FileVault 2. Un usuario del dispositivo puede ver su clave de recuperación personal en cualquier momento desde la aplicación Portal de empresa de iOS o desde el sitio web del Portal de empresa para el dispositivo macOS cifrado. Para ver la clave de recuperación personal, puede ir a los detalles del dispositivo y hacer clic en *Obtener clave de recuperación*.

Esta opción no estará disponible en una directiva creada anteriormente. Tendrá que volver a crear las directivas de FileVault para configurar esta opción y poder usarla. 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscripción de dispositivos

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Los dispositivos de tipo Bring Your Own Device pueden usar la VPN para la implementación<!--5015344 -->
Es posible que esta característica se retrase.

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


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplicación de las directivas en Seguridad de los puntos de conexión<!-- 5892558   -->
Podrá seleccionar una directiva que haya creado en el nodo Seguridad de los puntos de conexión del Centro de administración de Microsoft Endpoint Manager y, después, duplicarla para crear una copia.  Entre las directivas que podrá duplicar se incluyen las que cree para: 

- Antivirus
- Cifrado de discos
- Firewall
- Detección de puntos de conexión y respuesta
- Reducción de la superficie expuesta a ataques
- Protección de cuentas

La duplicación realizará una copia de la directiva original, a la que puede cambiar el nombre y editar. La copia no incluirá las asignaciones de la original.

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Nuevo perfil de directiva de firewall de seguridad de los puntos de conexión<!-- 5653324   -->
Como versión preliminar, se va a agregar un perfil adicional para Windows 10 y versiones posteriores a la directiva de firewall de Seguridad de los puntos de conexión de Intune (**Seguridad de los puntos de conexión** > **Firewall** > **Crear directiva** > seleccione **Windows 10 y versiones posteriores**). 

Cada instancia de este nuevo perfil admite hasta 150 *reglas de Firewall de Microsoft Defender* personalizadas. El perfil de reglas de Firewall de Microsoft Defender permite definir reglas de firewall de Windows granulares para permitir o bloquear puertos y aplicaciones en Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vea también

Consulte [Novedades de Microsoft Intune](whats-new.md) para obtener más información sobre los desarrollos recientes.



