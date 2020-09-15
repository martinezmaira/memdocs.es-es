---
title: 'En desarrollo: Microsoft Intune'
titleSuffix: ''
description: Características de Microsoft Intune en desarrollo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9ec657e7d2ee83f3f4f54f9a33a5a350faa4229
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564251"
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


<!-- ***********************************************-->
## <a name="device-configuration"></a>Configuración del dispositivo

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Creación de perfiles de certificado de PKCS para dispositivos Android Enterprise totalmente administrados (COBO)<!-- 4839686 -->
Puede crear perfiles de certificado de PKCS para implementar certificados en dispositivos de perfil de trabajo y propietario del dispositivo Android Enterprise (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise > solo propietario del dispositivo** o **Android Enterprise > solo perfil de trabajo** para plataforma > **PKCS** para perfil).

Pronto podrá crear perfiles de certificado PKCS para dispositivos Android Enterprise totalmente administrados. Se requiere el conector de certificado PFX de Intune. Si no usa SCEP y solo usa PKCS, puede quitar el conector NDES después de instalar el nuevo conector PFX. El nuevo conector PFX importa los archivos PFX e implementa los certificados PKCS en todas las plataformas.

Para más información sobre certificados PKCS, consulte [Configuración y uso de certificados PKCS con Intune](../protect/certficates-pfx-configure.md).

Se aplica a:
- Android Enterprise totalmente administrado (COBO)

### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>Compatibilidad con certificados con un tamaño de clave de 4096 bits en dispositivos iOS y macOS<!-- 7659175   -->
Intune pronto admitirá el uso de un tamaño de clave de 4096 bits para los perfiles de certificado SCEP. (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > *seleccione una plataforma* > *Perfil* = **Certificado SCEP**).

La compatibilidad con las claves de 4096 bits se ofrecerá para las siguientes plataformas: 
- iOS 14 y versiones posteriores
- macOS 11 y versiones posteriores    

### <a name="new-setting-for-password-complexity-for-android-10-and-later---7992114----"></a>Nuevo valor para configurar la complejidad de la contraseña para Android 10 y versiones posteriores<!-- 7992114  -->
Con el fin de admitir nuevas opciones para Android 10 y versiones posteriores, vamos a agregar un nuevo valor de configuración denominado **Complejidad de la contraseña** a las directivas *Conformidad de dispositivos* y *Restricciones de dispositivos*. (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Restricciones de dispositivos** y **Dispositivos** > **Directivas de cumplimiento** > **Crear directiva**). Con esta configuración, podrá administrar el grado de seguridad de la contraseña, que tenga en cuenta el tipo de contraseña, la longitud y la calidad. 

Se admitirán los niveles de complejidad siguientes:
- **Ninguno**: sin contraseña.
- **Bajo**: la contraseña cumple uno de los siguientes requisitos:
  - Patrón
  - PIN con secuencias repetidas (4444) u ordenadas (1234, 4321, 2468).
- **Medio**: la contraseña cumple uno de los siguientes requisitos:
  - PIN sin secuencias repetidas (4444) u ordenadas (1234, 4321, 2468), con una longitud de al menos 4.
  - Alfabético, con una longitud de al menos 4.
  - Alfanumérico, con una longitud de al menos 4.
- **Alto**: la contraseña cumple uno de los siguientes requisitos:
  - PIN sin secuencias repetidas (4444) u ordenadas (1234, 4321, 2468), con una longitud de al menos 8.
  - Alfabético, con una longitud de al menos 6.
  - Alfanumérico, con una longitud de al menos 6.

La complejidad de la contraseña no se aplica a los dispositivos Samsung Knox que ejecutan Android 10 y versiones posteriores. En estos dispositivos, los valores de configuración Longitud de la contraseña o Tipo de contraseña invalidan el de Complejidad de la contraseña.

### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355---"></a>Actualización de la versión preliminar COPE: nuevas opciones de configuración para crear requisitos para la contraseña del perfil de trabajo de dispositivos de propiedad corporativa de Android Enterprise con un perfil de trabajo<!--7088355 -->
En el futuro, las opciones de configuración permitirán a los administradores establecer requisitos para la contraseña del perfil de trabajo de dispositivos de propiedad corporativa de Android Enterprise con un perfil de trabajo.  (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** para la plataforma > **Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado** > **Restricciones de dispositivos** para el perfil > **Contraseña del perfil de trabajo**):

- Tipo de contraseña obligatoria
- Longitud mínima de la contraseña
- Número de días hasta que expire la contraseña
- Número de contraseñas requeridas antes de que el usuario pueda reusar una
- Número de errores de inicio de sesión antes de borrar el dispositivo


### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886----"></a>Nuevas opciones de configuración con VPN por aplicación o VPN a petición en dispositivos iOS/iPad y macOS<!-- 7758772 7758837 7758886  -->
- **Impedir que los usuarios deshabiliten la VPN automática**: al crear una conexión **VPN por aplicación** automática o **VPN a petición**, puede obligar a los usuarios a conservar la VPN automática habilitada y en ejecución.
- **Dominios asociados**: al crear una conexión **VPN por aplicación** automática, puede especificar dominios asociados en el perfil de VPN que inicien automáticamente la conexión VPN. 
- **Dominios excluidos**: al crear una conexión **VPN por aplicación** automática, puede crear una lista de dominios que puedan omitir la conexión VPN cuando se conecte la VPN por aplicación.

Puede configurar perfiles de VPN automática en **Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPados** o **macOS** para la plataforma > **VPN** para el perfil > **VPN automática**.

Para obtener más información sobre los dominios asociados, vea [Dominios asociados](../configuration/device-features-configure.md#associated-domains).

Para ver los valores que se pueden configurar, consulte [Configuración de la red privada virtual (VPN) por aplicación para dispositivos iOS/iPadOS](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile).

Se aplica a:
- iOS/iPadOS 14 y versiones más recientes
- macOS Big Sur (macOS 11)

### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356----"></a>Actualización de la versión preliminar COPE: nuevas opciones para configurar el perfil personal de dispositivos de propiedad corporativa de Android Enterprise con un perfil de trabajo<!-- 7086356  -->
En el caso de los dispositivos de propiedad corporativa de Android Enterprise con un perfil de trabajo, hay nuevas opciones de configuración que solo se aplican al perfil personal (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** > para la plataforma **Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado** > **Restricciones de dispositivos** para el perfil > **Perfil personal**):

- **Cámara**: use esta opción para bloquear el acceso a la cámara durante el uso personal.
- **Captura de pantalla**: use esta opción para bloquear las capturas de pantalla durante el uso personal.
- **Permitir que los usuarios habiliten la instalación de aplicaciones de orígenes desconocidos en el perfil personal**: use esta opción para permitir que los usuarios instalen aplicaciones de orígenes desconocidos en el perfil personal. 

Para ver los valores actuales que se pueden configurar, vaya a [Configuración de dispositivos Android Enterprise para permitir o restringir características](../configuration/device-restrictions-android-for-work.md).

### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422----"></a>Bloqueo de clips de aplicación en iOS/iPadOS y aplazamiento de las actualizaciones de software que no sean del sistema operativo en dispositivos macOS<!-- 7518422  -->
Cuando se crean perfiles de restricciones de dispositivos en dispositivos iOS/iPadOS y macOS, hay algunos valores de configuración nuevos:

**iOS/iPadOS 14.0 y versiones posteriores: bloqueo de clips de aplicación**
- Se aplica a iOS/iPadOS 14.0 y versiones posteriores.
- Los dispositivos deben haberse inscrito con la inscripción de dispositivos o con la inscripción de dispositivos automatizada (dispositivos supervisados).
- La opción **Bloquear clips de aplicación** bloquea los clips de aplicación en los dispositivos administrados (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** para la plataforma > **Restricciones de dispositivos** para el perfil > **General**). Cuando se bloquean, los usuarios no pueden agregar ningún clip de aplicación y los clips existentes se quitan del dispositivo.  

**macOS 11 y versiones posteriores: aplazamiento de las actualizaciones de software**
- Se aplica a macOS 11 y versiones posteriores. En dispositivos macOS supervisados, el dispositivo debe tener la inscripción de dispositivos aprobada por el usuario o haberse inscrito a través de la inscripción de dispositivos automatizada.
- La opción **Aplazar las actualizaciones de software** retrasa el momento en que el usuario ve las actualizaciones de software que no sean del sistema operativo (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **macOS** para la plataforma > **Restricciones de dispositivos** para el perfil > **General**). Si se aplazan estas actualizaciones, las actualizaciones recién publicadas no estarán visibles para los usuarios hasta después del período de aplazamiento, que se configura mediante la opción **Retrasar la visibilidad de las actualizaciones de software**. El aplazamiento de las actualizaciones de software que no sean del sistema operativo no afectará a las actualizaciones programadas.
- El valor de configuración **Aplazar las actualizaciones de software** existente se combina con esta nueva opción. Con la nueva opción, se pueden diferir las actualizaciones de software del sistema operativo, así como las que no sean del sistema operativo. Se puede seguir usando la opción **Retrasar la visibilidad de las actualizaciones de software** para establecer el número de días, que se aplicarán a ambas opciones para aplazar las actualizaciones de software.
- El comportamiento de las directivas existentes no cambia ni se elimina, y tampoco se ve afectado. Las directivas existentes se migrarán automáticamente a la nueva opción con la misma configuración.

### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689----"></a>Deshabilitación de la selección aleatoria de direcciones MAC en redes Wi-Fi en dispositivos iOS/iPadOS<!-- 7758689  -->
A partir de iOS/iPadOS 14, de forma predeterminada, los dispositivos presentan una dirección MAC aleatoria al conectarse a una red, en lugar de la dirección MAC física. Este comportamiento se recomienda por cuestiones de privacidad, ya que es más difícil realizar un seguimiento de un dispositivo mediante su dirección MAC. Esta característica también interrumpe las funciones que se basan en una dirección MAC estática, incluido el control de acceso a la red (NAC). 

Puede deshabilitar la selección aleatoria de direcciones MAC en función de la red en los perfiles de Wi-Fi (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOS** > para la plataforma > **Wi-Fi** para el perfil > **Básico** o **Empresa** para el tipo de Wi-Fi).

Para ver las opciones que se pueden configurar actualmente, vaya a [Adición de configuración de Wi-Fi para dispositivos iOS/iPadOS](../configuration/wi-fi-settings-ios.md).

Se aplica a:
- iOS/iPadOS 14 y versiones más recientes

### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>Establecimiento de la unidad de transmisión máxima para las conexiones VPN de IKEv2 en dispositivos iOS/iPadOS<!-- 7758937  -->
A partir de iOS/iPadOS 14 y dispositivos más recientes, se puede configurar una unidad de transmisión máxima (MTU) personalizada al usar conexiones VPN de IKEv2 (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **iOS/iPadOs** para la plataforma > **VPN** para el perfil > IKEv2 para el tipo de conexión).

Para obtener más información sobre las opciones que se pueden configurar, vea [Configuración de IKEv2](../configuration/vpn-settings-ios.md#ikev2-settings).

Se aplica a:
- iOS/iPadOS 14 y versiones más recientes

### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116----"></a>Conexión VPN según la cuenta para perfiles de correo electrónico en dispositivos iOS/iPadOS<!-- 7759116  -->
A partir de iOS/iPadOS 14, el tráfico de correo electrónico de la aplicación de correo nativa se puede enrutar a través de una VPN en función de la cuenta que emplea el usuario. Ahora, se puede especificar un perfil de VPN según la aplicación para usarlo con esta conexión VPN en función de la cuenta.  La conexión VPN según la aplicación se activa automáticamente cuando los usuarios emplean la cuenta de la organización en la aplicación de correo.

Para ver las opciones que se pueden configurar actualmente, vaya a [Incorporación de la configuración de correo electrónico para dispositivos iOS e iPadOS](../configuration/email-settings-ios.md).

Se aplica a:
- iOS/iPadOS 14 y versiones más recientes

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>Uso de NetMotion como tipo de conexión VPN para dispositivos de perfil de trabajo de Android Enterprise<!-- 7764263 -->
Al crear un perfil de VPN, NetMotion está disponible como tipo de conexión VPN (**Dispositivos** > **Configuración de dispositivos** > **Crear perfil** > **perfil de trabajo de Android Enterprise** para la plataforma > **VPN** para el perfil > **NetMotion** para el tipo de conexión).

Para obtener más información sobre los perfiles de VPN en Intune, consulte [Creación de perfiles de VPN para conectarse a servidores VPN](../configuration/vpn-settings-configure.md).

Se aplica a:
- Perfil de trabajo de Android Enterprise

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>Cambios en la configuración de contraseñas en los perfiles de restricción de dispositivos para el administrador de dispositivos Android<!-- 7662279  --> 
Estamos introduciendo algunos cambios en la configuración de contraseñas para las directivas de *restricción de dispositivos* y *cumplimiento* para el *administrador de dispositivos Android*. (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Restricciones de dispositivos** y **Dispositivos** > **Directivas de cumplimiento** > **Crear directiva**). Estos cambios ayudan a Intune a adaptarse a los cambios en Android 10 y versiones posteriores, para asegurarse de que la configuración de contraseñas siga aplicándose a los dispositivos según lo previsto.
 
Los cambios incluyen:
- La eliminación de la opción de nivel superior para **Contraseña**.  
- La configuración se reorganizará en secciones basadas en los dispositivos a los que se apliquen.
- La opción **Longitud mínima de contraseña** se deshabilitará para su uso a menos que **Tipo de contraseña** se configure en un valor al que se le aplique la longitud de contraseña.
- Actualizaciones adicionales de etiquetas y texto de ejemplo.

Estos cambios se aplican a la interfaz de usuario para la configuración y no afectarán a los perfiles existentes. 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Inscripción de dispositivos

### <a name="ending-support-for-ios-11--7327321---"></a>Fin de la compatibilidad con iOS 11<!--7327321 -->
A partir de iOS 14, la inscripción de Intune y la aplicación Portal de empresa serán compatibles con iOS 12 y versiones posteriores. No se admitirán versiones anteriores, pero seguirán recibiendo directivas.

### <a name="ending-support-for-macos-1012--7327326---"></a>Fin de la compatibilidad con macOS 10.12<!--7327326 -->
A partir de macOS 11, la inscripción de Intune y la aplicación Portal de empresa serán compatibles con macOS 10.13 y versiones posteriores. No se admitirán versiones anteriores.


<!-- ***********************************************-->
## <a name="device-management"></a>Administración de dispositivos

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Compatibilidad de scripts de PowerShell con dispositivos BYOD<!-- 1862833  -->
Los scripts de PowerShell admitirán dispositivos registrados de Azure AD en Intune. Para más información sobre PowerShell, vea [Uso de scripts de PowerShell para dispositivos Windows 10 en Intune](../apps/intune-management-extension.md). Esta funcionalidad no es compatible con dispositivos que ejecutan Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics incluirá registros de detalles del dispositivo<!--6014987  -->
Habrá disponibles registros detallados del dispositivo de Intune en **Informes** > **Log Analytics**. Puede correlacionar los detalles del dispositivo para compilar consultas personalizadas y libros de Azure.

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Asociación de inquilinos: ejecución de scripts desde el centro de administración<!--7220536, CM6234688 -->
Podrá incorporar la eficacia de la característica [Ejecutar scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) local de Configuration Manager al centro de administración de Microsoft Endpoint Manager. Permita que otros roles, como el de Departamento de soporte técnico, ejecuten scripts de PowerShell desde la nube en un dispositivo administrado de Configuration Manager individual. Esto proporciona todas las ventajas tradicionales de los scripts de PowerShell que ya se han definido y aprobado por el administrador de Configuration Manager en este nuevo entorno. Para más información, consulte [Technical Preview 2005 para Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Implementación de actualizaciones de software en dispositivos macOS <!-- 3194876 -->
Podrá implementar actualizaciones de software en grupos de dispositivos macOS. Esta característica incluye, entre otras, actualizaciones de archivos críticos, de archivos de configuración y del firmware. Podrá enviar actualizaciones en la siguiente sincronización de dispositivos o seleccionar una programación semanal para implementar actualizaciones dentro o fuera de los períodos que establezca. De esta manera, podrá actualizar los dispositivos fuera de las horas de trabajo estándar o cuando el departamento de soporte técnico tiene a todo el personal ocupado. También obtendrá un informe detallado de todos los dispositivos macOS con actualizaciones implementadas. Puede profundizar en el informe en función de cada dispositivo para ver los estados de determinadas actualizaciones.

### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228---"></a>Actualización de la versión preliminar COPE: restablecimiento de la contraseña del perfil para dispositivos de propiedad corporativa de Android Enterprise con un perfil de trabajo <!--7217228 -->
En el futuro, una acción del administrador permitirá a los administradores restablecer la contraseña del perfil de trabajo de dispositivos de propiedad corporativa de Android Enterprise con un perfil de trabajo.

### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043---"></a>Cambio del nombre de un dispositivo administrado de forma conjunta unido a Azure Active Directory<!--7728043 -->
Se podrá cambiar el nombre de un dispositivo administrado de forma conjunta que esté unido a Azure AD. Para ello, vaya a MEM > **Dispositivos** > **Todos los dispositivos** > elija un dispositivo > **…**  > **Cambiar el nombre del dispositivo**.

### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987---"></a>Compatibilidad con baterías PowerPrecision y PowerPrecision+ para dispositivos Zebra<!--3724987 -->
En la página de detalles del hardware de un dispositivo, podrá ver la siguiente información sobre los dispositivos Zebra que usan baterías PowerPrecision y PowerPrecision+:
- Valoración del estado de mantenimiento según Zebra (solo en baterías PowerPrecision+)
- Número de ciclos de carga completos consumidos
- Fecha de la última sincronización de la última batería que se encontró en el dispositivo
- Número de serie de la última batería que se encontró en el dispositivo

<!-- ***********************************************-->
## <a name="intune-apps"></a>Aplicaciones de Intune

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Entrega unificada de aplicaciones de Azure AD Enterprise y Office Online en el Portal de empresa de Windows<!-- 1817861  -->
En la versión de 2006, anunciamos la [entrega unificada de aplicaciones de Azure AD Enterprise y Office Online en el Portal de empresa](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal). Esta característica se admitirá en el Portal de empresa de Windows. En el panel **Personalización** de Intune, puede seleccionar **Ocultar** o **Mostrar** **Aplicaciones de Azure AD Enterprise** y **Aplicaciones de Office Online** en el Portal de empresa de Windows. Cada usuario final ve todo el catálogo de aplicaciones desde el servicio de Microsoft elegido. De forma predeterminada, cada origen de aplicación adicional se establecerá en **Ocultar**. Para encontrar esta opción de configuración, seleccione **Administración de inquilinos** > **Personalización** en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Para obtener información relacionada, vea [Personalización de las aplicaciones del Portal de empresa de Intune, el sitio web del Portal de empresa y la aplicación de Intune](../apps/company-portal-app.md).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Supervisión y solución de problemas

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Plantilla de informe de cumplimiento de Power BI V2.0<!-- 636958  -->
Los administradores podrán actualizar la versión de la plantilla de informe de cumplimiento de Power BI de V1.0 a V2.0. En V2.0 se incluirá un diseño mejorado, así como cambios en los cálculos y los datos que se muestran como parte de la plantilla. Para obtener información relacionada, vea [Conexión con el almacenamiento de datos con Power BI](../developer/reports-proc-get-a-link-powerbi.md).


### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Informes nuevos y mejorados del Antivirus de Microsoft Defender para Windows 10 y versiones más recientes<!-- 6018169  -->
Vamos a agregar cuatro nuevos informes del Antivirus de Microsoft Defender en Windows 10, en **Seguridad de los puntos de conexión** > **Antivirus**.
- Dos informes operativos: *Dispositivos con malware detectado* y *Estado del agente*.
- Dos informes organizativos: *Malware detectado* y *Estado del agente*.

Por ejemplo, el informe operativo *Estado del agente* mostrará de un vistazo el nombre del dispositivo, el nombre de usuario, el correo electrónico del usuario y el UPN, y si está habilitada la protección en tiempo real y de red. Publicaremos más detalles cuando estos informes estén disponibles para su uso.

Para obtener más información sobre la seguridad de los puntos de conexión en Intune, vea [Administración de la seguridad de puntos de conexión en Microsoft Intune](../protect/endpoint-security.md).

### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics-preview--7200950---"></a>Análisis de GPO locales mediante el análisis de directivas de grupo (versión preliminar)<!--7200950 -->
En **Dispositivos** > **Análisis de directivas de grupo (versión preliminar)** , puede importar objetos de directiva de grupo (GPO) en el centro de administración de Endpoint Manager. Al realizar la importación, Intune analiza automáticamente el GPO y muestra las directivas que tienen una configuración equivalente en Intune. También se muestran los GPO que están en desuso o que ya no son compatibles.

Se aplica a:
- Windows 10 y versiones posteriores

#### <a name="new-windows-10-feature-update-report---6473128----"></a>Nuevo informe de actualizaciones de características de Windows 10<!-- 6473128  -->
El informe de **actualizaciones de características de Windows** proporciona una vista general del cumplimiento de los dispositivos que se establecen como destino mediante una directiva de **actualizaciones de características de Windows 10**. En el [centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Informes** > **Actualizaciones de características de Windows (versión preliminar)**  > **Errores de actualización de características** para ver el resumen de este informe. Para ver los informes de directivas específicas, seleccione la pestaña **Informes** y abra el **informe de actualización de características de Windows**. 

#### <a name="new-windows-10-feature-failures-update-report---6473121-----"></a>Nuevo informe de fallo en la actualización de las características de Windows 10<!-- 6473121   -->
El informe de **errores de actualización de características** proporciona detalles sobre los errores de los dispositivos que se establecen como destino mediante una directiva de **actualizaciones de características de Windows 10** y que han intentado llevar a cabo una actualización. En el [centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Dispositivos** > **Monitor** > **Errores de actualización de características** para ver este informe.

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

### <a name="improved-certificate-deployment-for-android-enterprise----6296499----"></a>Implementación de certificados mejorada para Android Enterprise <!-- 6296499  -->
Los dispositivos que ejecuten perfiles de trabajo de propiedad corporativa, dedicados y totalmente administrados de Android Enterprise pronto podrán usar certificados S/MIME para Outlook sin que el usuario del dispositivo tenga que permitir el acceso. Los certificados S/MIME se implementan mediante el perfil del certificado PKCS importado para la configuración del dispositivo. (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Android Enterprise** >  **Certificado PKCS importado** en la categoría para *Perfil de trabajo de propiedad corporativa, dedicado y totalmente administrado*).

### <a name="tri-state-options-for-settings-are-coming-to-endpoint-security-firewall-policy---6586159-----"></a>Próxima incorporación de opciones de tres estados para la configuración en la directiva de firewall de seguridad de los puntos de conexión<!-- 6586159   -->
Vamos a agregar un tercer estado de configuración para las opciones de las directivas de firewall de seguridad de los puntos de conexión, donde la plataforma (Windows o macOS) puede admitir la opción adicional (**Seguridad de los puntos de conexión** > **Firewall**).

Por ejemplo, si un valor de configuración ofrece actualmente las opciones **No configurado** y **Sí**, si la plataforma lo admite, agregaremos la opción **No**.

### <a name="new-security-baseline-for-office---3150261----"></a>Nueva línea base de seguridad para Office<!-- 3150261  -->
Estamos agregando una nueva línea base de seguridad (**Seguridad de los puntos de conexión** > **Líneas base de seguridad**) para administrar la configuración de *Microsoft Office O365*. La configuración de la línea base incluirá configuraciones para aplicaciones de Office, como *Administración de complementos*, *Administración de MIME* y mucho más.

### <a name="improved-status-details-in-security-baseline-reports---7221051------"></a>Detalles de estado mejorados en los informes de línea base de seguridad<!-- 7221051    -->
Estamos mejorando los detalles de estado que se verán al consultar los resultados de las líneas base de seguridad implementadas. (**Seguridad de los puntos de conexión** > **Líneas base de seguridad** >  *seleccione un tipo de línea base de seguridad, como* **Líneas base de seguridad de Windows 10** > **Perfiles** > *seleccione una instancia de ese perfil para ver el estado* > *seleccione un informe de perfil, como* **Estado del dispositivo**).

Las mejoras modificarán las etiquetas y definiciones comunes que usamos para el estado, a fin de que se ajusten mejor a la intención del estado. Por ejemplo:
- **Matches baseline** (Coincide con la línea base) se actualizará a **Matches default settings** (Coincide con la configuración predeterminada), ya que describe mejor la intención de identificar cuándo una configuración de dispositivo coincide con la configuración de línea base predeterminada (sin modificar).
- **Configuración errónea** se desglosará en detalles más específicos, como **Error**, **Conflicto** y **Pendiente**. Los nuevos estados aportarán coherencia a otras áreas de la consola.

### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374--idstaged---"></a>Permisos de RBAC expandidos para el rol de seguridad de los puntos de conexión<!--7312374  idstaged -->
El rol **Administrador de seguridad de los puntos de conexión** para Intune está recibiendo más permisos de control de acceso basado en rol (RBAC) para tareas remotas. Este rol concede acceso al centro de administración de Microsoft Endpoint Manager y lo pueden usar las personas que administran las características de seguridad y cumplimiento, incluidas las líneas base de seguridad, el cumplimiento de dispositivos, el acceso condicional y la Protección contra amenazas avanzada de Microsoft Defender.

Para ver el permiso de un rol de RBAC de Intune, vaya a (**Administración de inquilinos** > **Roles de Intune** > *seleccione un rol* > **Permisos**).

Entre los permisos ampliados para tareas remotas se incluyen los siguientes:

- Reiniciar ahora
- Bloqueo remoto
- Rotar las claves de BitLocker (versión preliminar)
- Rotar la clave de FileVault
- Sincronizar dispositivos
- Microsoft Defender
- Iniciar una acción de Configuration Manager

### <a name="updates-for-security-baselines---7102146-7103916----"></a>Actualizaciones para líneas base de seguridad<!-- 7102146, 7103916  -->
Pronto publicaremos actualizaciones para las siguientes líneas base de seguridad (**Seguridad de los puntos de conexión** > **Líneas base de seguridad**):
- **Línea base de seguridad de MDM** (Seguridad de Windows 10)
- **Línea de base de ATP de Microsoft Defender**

Las versiones de línea base actualizadas proporcionan compatibilidad con los valores de configuración recientes para ayudarle a mantener las configuraciones que recomiendan los equipos de producto respectivos.

### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503--idstaged----"></a>Uso de los detalles de configuración de la seguridad de los puntos de conexión para identificar el origen de conflictos de directivas en los dispositivos.<!-- 7567503  idstaged  -->
Para contribuir a la resolución de conflictos, pronto podrá explorar los perfiles de línea base de seguridad para ver la *configuración de seguridad de los puntos de conexión* de un dispositivo seleccionado. A partir de ahí, podrá seleccionar las opciones de configuración que muestren *Conflicto* o *Error* y seguir profundizando para ver una lista de detalles, con los perfiles y las directivas que forman parte del conflicto. Si después selecciona una directiva que es el origen de un conflicto, Intune abrirá el panel de información general de la directiva, desde donde podrá revisar o modificar la configuración de la directiva. (**Dispositivos** > *seleccione un dispositivo* > **Configuración de seguridad de los puntos de conexión** > *seleccione un perfil o una línea base* > *seleccione un valor de configuración de la lista de valores aplicados al dispositivo*).

Los siguientes tipos de directivas pueden identificarse como orígenes de conflicto cuando se explora una línea base de seguridad:
- Directiva de configuración de dispositivos
- Directivas de seguridad de puntos de conexión

### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-----"></a>Nuevos detalles de la configuración de seguridad de los puntos de conexión para un dispositivo<!-- 7745029   -->
Estamos agregando nuevos detalles para los dispositivos disponibles para que se puedan visualizar como parte de la configuración de seguridad de los puntos de conexión de un dispositivo. (**Seguridad de los puntos de conexión** > **Líneas base de seguridad** > *línea base seleccionada* > **Perfiles** > *perfil seleccionado* > **Estado del dispositivo** > **Configuración de seguridad de los puntos de conexión**). Nuevos detalles:

- **UPN** (Nombre principal del usuario): el UPN identifica el perfil de seguridad de los puntos de conexión que se ha asignado a un usuario determinado del dispositivo. Es útil para diferenciar entre varios usuarios de un dispositivo y varias entradas de un perfil o línea base que se han asignado al dispositivo. 
- **Peor estado**: este detalle identifica el estado menos favorable para el dispositivo. Cuando este estado es **Correcto**, el dispositivo no tiene conflictos ni errores de directivas.

### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Android 11 ha dejado de usar la implementación de certificados raíz de confianza en dispositivos inscritos por el administrador de dispositivos<!--7662775  -->
Con Android 11, ya no se pueden implementar certificados raíz de confianza en dispositivos inscritos como *Administrador de dispositivos Android*. Este cambio no afecta a los dispositivos Samsung Knox debido a la integración de Intune con la plataforma Knox. En el caso de dispositivos que no son Samsung, los usuarios deben instalar manualmente el certificado raíz de confianza en el dispositivo. 

Con el certificado raíz de confianza instalado manualmente en un dispositivo, puede usar SCEP para aprovisionar certificados en el dispositivo. En este caso, sigue teniendo que crear e implementar una directiva de *certificado de confianza* en el dispositivo y vincularla al perfil del *certificado SCEP*.

- Si el certificado raíz de confianza está en el dispositivo, el perfil de certificado SCEP se instalará correctamente. 
- Si no se encuentra el certificado de confianza, se producirá un error en el perfil de certificado SCEP.

<!-- ***********************************************-->
## <a name="notices"></a>Notificaciones

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vea también

Consulte [Novedades de Microsoft Intune](whats-new.md) para obtener más información sobre los desarrollos recientes.
