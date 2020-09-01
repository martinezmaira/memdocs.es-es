---
title: Novedades de la versión 2006
titleSuffix: Configuration Manager
description: Obtenga detalles sobre los cambios y las nuevas funcionalidades incorporados en la versión 2006 de la rama actual de Configuration Manager.
ms.date: 08/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fc12c81a1ec58d17580b91e21a1ba7d2e0cb0cbc
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819684"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Novedades de la versión 2006 de la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 2006 de la rama actual de Configuration Manager está disponible como una actualización en consola. Aplique esta actualización en los sitios que ejecuten la versión 1810 o versiones posteriores. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->En este artículo se resumen los cambios y las nuevas características de la versión 2006 de Configuration Manager.

Revise siempre la lista de comprobación más reciente para instalar esta actualización. Para más información, vea la [lista de comprobación para la instalación de la actualización 2006](../../servers/manage/checklist-for-installing-update-2006.md). Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

Para aprovechar al máximo las nuevas características de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

> [!TIP]
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Asociación de inquilinos de Microsoft Endpoint Manager

### <a name="tenant-attach-microsoft-defender-antivirus-policies-in-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Asociación de inquilinos: Directivas del Antivirus de Microsoft Defender en el Centro de administración de Microsoft Endpoint Manager.
<!--4812909-->
Ahora puede crear directivas de Antivirus de Microsoft Defender en la consola de Microsoft Endpoint Manager e implementarlas en las recopilaciones de Configuration Manager. Para obtener más información, incluidas las instrucciones detalladas y la configuración disponible, consulte los siguientes artículos:
- [Asociación de inquilinos: incorporación de clientes de Configuration Manager a ATP de Microsoft Defender desde el centro de administración (versión preliminar)](../../../tenant-attach/atp-onboard.md)
- [Asociación de inquilinos: implementación de la directiva de antivirus de seguridad de punto de conexión desde el centro de administración (versión preliminar)](../../../tenant-attach/deploy-antivirus-policy.md)
- [Configuración de la directiva de Antivirus de Microsoft Defender para dispositivos con asociación de inquilinos en Microsoft Intune](../../../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json). 

### <a name="install-applications-from-the-admin-center"></a>Instalación de aplicaciones desde el centro de administración
<!--7518897, 6024389-->
Puede iniciar la instalación de una aplicación en tiempo real para un dispositivo asociado al inquilino desde el centro de administración de Microsoft Endpoint Manager. A partir de la versión 2006 de Configuration Manager, la lista de aplicaciones disponibles para el dispositivo también incluye las aplicaciones implementadas en el usuario que ha iniciado la sesión en el dispositivo actualmente. Para más información, consulte [Asociación de inquilinos: instalación de una aplicación desde el centro de administración](../../../tenant-attach/applications.md).  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a> Importación de la aplicación de Azure AD creada anteriormente durante la incorporación de la asociación de inquilino
<!--6479246-->
Durante una nueva incorporación, un administrador puede especificar una aplicación creada anteriormente durante la incorporación a la asociación de inquilino. Para obtener más información, vea [Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> Análisis de puntos de conexión

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>Recopilación de datos del análisis de puntos de conexión habilitada de forma predeterminada
<!--7065447, 7741111-->
La configuración del cliente **Habilitar recopilación de datos del análisis de puntos de conexión** ahora está habilitada de forma predeterminada. Esta configuración permite que los puntos de conexión administrados envíen datos, como información sobre el rendimiento de inicio, al servidor de sitio de Configuration Manager. Este cambio solo afecta a la recopilación de datos locales. Los datos del análisis de punto de conexión no se cargan en el centro de administración de Microsoft Endpoint Manager hasta que se [habilita la carga de datos en Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload). El nuevo valor predeterminado se aplica a la configuración de cliente predeterminada y a la configuración de cliente personalizada creada después de actualizar a la versión 2006.

- Si actualiza de la versión 2002 a la versión 2006, se conservan los valores de configuración de cliente personalizados existentes. El valor predeterminado de **Habilitar recopilación de datos del análisis de puntos de conexión** en la versión 2002 de Configuration Manager es **No**.
- Si va a actualizar a la versión 2006 desde la versión 1910 o anterior de Configuration Manager, todas las configuraciones de cliente personalizadas preexistentes que contengan el grupo de configuración **Agente de equipo** heredarán el nuevo valor predeterminado de **Sí** para **Habilitar recopilación de datos del análisis de puntos de conexión**.

Para más información, vea [Configuración de la recopilación de datos del análisis de puntos de conexión en Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infraestructura del sitio

### <a name="vpn-boundary-type"></a> Tipo de límite de VPN

<!--7020519-->

Para simplificar la administración de clientes remotos, ahora puede crear un nuevo tipo de límite para las VPN. Anteriormente, tenía que crear límites para clientes VPN basados en la dirección IP o subred. Esta configuración podría resultar difícil o no posible debido a la configuración de la subred o al diseño de la VPN.

Ahora, cuando un cliente envía una solicitud de ubicación, incluye información adicional sobre su configuración de red. En función de esta información, el servidor determina si el cliente se encuentra en una VPN.

Para más información, vea [Definición de límites](../../servers/deploy/configure/boundaries.md).

### <a name="management-insights-to-optimize-for-remote-workers"></a>Información de administración para optimizar a los trabajadores remotos

<!--6982226-->

Esta versión agrega un nuevo grupo de información de administración, **Optimización para trabajos remotos**. Esta información lo ayudará a crear experiencias mejores para los trabajadores remotos y reducir la carga en su infraestructura. La información de esta versión se centra principalmente en la VPN:

- **Definir grupos de límites de VPN**
- **Configurar preferencia por orígenes de contenido en la nube de los clientes conectados a VPN**
- **Deshabilitar el uso compartido de contenido punto a punto para clientes conectados VPN**

Para obtener más información, vea [Información de administración](../../servers/manage/management-insights.md).

### <a name="improved-support-for-windows-virtual-desktop"></a> Compatibilidad mejorada con Windows Virtual Desktop

<!--6527576-->

La plataforma de **sesión múltiple de Windows 10 Enterprise** está disponible en la lista de versiones de sistema operativo admitidas en objetos con reglas de requisitos o listas de aplicabilidad.

Para obtener más información sobre la compatibilidad de Configuration Manager con Windows Virtual Desktop, consulte [Versiones de SO admitidas para clientes y dispositivos](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>Los clientes de la intranet pueden usar un punto de actualización de software de CMG
<!--7102873-->
Ahora, los clientes de la intranet pueden acceder al punto de actualización de software de una CMG cuando se asigna a un grupo de límites. Para obtener más información, vea [Configuración de grupos de límites](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Administración conectada a la nube

### <a name="use-the-company-portal-app-on-co-managed-devices"></a> Uso de la aplicación Portal de empresa en dispositivos administrados conjuntamente

<!--CMADO-3601237,INADO-4297660-->

El Portal de empresa es ahora la experiencia del portal de aplicaciones multiplataforma para Microsoft Endpoint Manager. Mediante la configuración de los dispositivos administrados conjuntamente para usar también el Portal de empresa, puede proporcionar una experiencia de usuario coherente en todos los dispositivos.

Para más información, consulte [Uso de la aplicación Portal de empresa en dispositivos administrados conjuntamente](../../../comanage/company-portal.md).

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>Uso de Microsoft Azure China 21Vianet para la administración conjunta
<!--7133238-->
Ahora puede seleccionar la nube de Azure China como su entorno de Azure al habilitar la administración conjunta. Para más información, consulte [cómo habilitar la administración conjunta](../../../comanage/how-to-enable.md).

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Notificación de expiración de clave secreta de aplicación de Azure AD

<!--6386392-->

Si configura los servicios de Azure para que se conecten a su sitio mediante la nube, la consola de Configuration Manager muestra ahora las notificaciones para las siguientes circunstancias:

- Una o más claves secretas de la aplicación de Azure AD expirarán pronto.
- Una o más claves secretas de la aplicación de Azure AD han expirado.

Para más información, vea [Renovar clave secreta](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="desktop-analytics"></a>Análisis de escritorio

Para más información sobre los cambios mensuales en el servicio en la nube de Análisis de escritorio, vea [Novedades de Análisis de escritorio](../../../desktop-analytics/whats-new.md).

#### <a name="change-to-diagnostic-data-labels"></a>Cambio a etiquetas de datos de diagnóstico

<!-- 7363467 -->

Para adaptarse mejor a los requisitos de Análisis de escritorio para los datos de diagnóstico de Windows, esta configuración tiene nuevas etiquetas:

| Versión 2006 y posteriores | Versión 2002 y anteriores |
|---------|---------|
| Requerido | Básico |
| Opcional (limitado) | Mejorado (limitado) |
| N/D | Mejorada |
| Opcional | Completo |

Si configuró previamente algún dispositivo en el nivel **Mejorado**, al actualizar a la versión 2006, se revertirá a **Opcional (limitado)** . Como consecuencia, se envían menos datos a Microsoft. Este cambio no debe afectar a lo que se ve en Análisis de escritorio.

Para obtener más información, consulte [Habilitación del uso compartido de datos en Análisis de escritorio](../../../desktop-analytics/enable-data-sharing.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Administración en tiempo real

### <a name="improvements-to-cmpivot"></a>Mejoras en CMPivot
<!--6518631-->
Se han realizado las siguientes mejoras en CMPivot:

- Convergencia de CMPivot desde la consola y CMPivot independiente.
- Ejecución de CMPivot desde un dispositivo individual o varios dispositivos sin tener que seleccionar o crear una recopilación.
- Desde los resultados de la consulta de CMPivot, puede seleccionar un dispositivo individual o varios dispositivos y, a continuación, iniciar una instancia de CMPivot independiente con el ámbito de la selección.

Para más información, vea [CMPivot a partir de la versión 2006](../../servers/manage/cmpivot-changes.md#bkmk_2006).

## <a name="client-management"></a><a name="bkmk_client"></a> Administración de clientes

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a> Instalación y actualización del cliente en una conexión de uso medido

<!--6976145-->

Anteriormente, si el dispositivo estaba conectado a una red de uso medido, los nuevos clientes no se instalaban. Los clientes existentes solo se actualizaban si se permitía toda la comunicación del cliente. En el caso de los dispositivos que se mueven con frecuencia en una red de uso medido, estarían sin administrar o en una versión de cliente anterior. A partir de esta versión, puede instalar y actualizar el cliente cuando se establece el valor de cliente **Comunicación de clientes en conexiones a Internet de uso medido** en **Permitir** o **Limitar**. Con esta configuración, puede permitir que el cliente se mantenga actualizado, pero la comunicación del cliente se sigue administrando en una red de uso medido.

Para definir el comportamiento de una nueva instalación de cliente, hay un nuevo valor de ccmsetup, **/AllowMetered**. Cuando se permite la comunicación de cliente en una red de uso medido para ccmsetup, esta descarga el contenido, se registra en el sitio y descarga la directiva inicial. Cualquier comunicación de cliente posterior sigue la configuración del valor de cliente de esa directiva.

Vea los siguientes artículos para más información:

- [Acerca de la configuración de cliente](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [Acerca de los parámetros y propiedades de instalación de cliente](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>Mejoras en la administración de los reinicios de los dispositivos

<!--3601213-->

Configuration Manager proporciona muchas opciones para administrar los reinicios y las notificaciones de reinicio del dispositivo. Ahora puede definir la configuración de un cliente para impedir que los dispositivos se reinicien automáticamente cuando una implementación lo requiera. Esta configuración ofrece más control en situaciones únicas. De forma predeterminada, la configuración de cliente **Configuration Manager puede forzar el reinicio de un dispositivo** está habilitada, por lo que Configuration Manager puede seguir forzando el reinicio de los dispositivos. Esta configuración solo se aplica a aplicaciones, actualizaciones de software e implementaciones de paquetes que requieren un reinicio.

Para más información, vea [Notificaciones de reinicio del dispositivo](../../clients/deploy/device-restart-notifications.md).

## <a name="application-management"></a><a name="bkmk_app"></a> Administración de aplicaciones

### <a name="improvements-to-available-apps-via-cmg"></a>Mejoras en las aplicaciones disponibles a través de CMG

<!--6935376-->
En esta versión se corrige un problema con la autenticación del centro de software y Azure Active Directory (Azure AD). Para un cliente detectado como en la intranet pero que se comunica a través de Cloud Management Gateway (CMG), el Centro de software anteriormente usaría la autenticación de Windows. Al intentar obtener la lista de aplicaciones disponibles para el usuario, se produciría un error. Ahora usa la identidad de Azure Active Directory (Azure AD) para los dispositivos unidos a Azure AD. Estos dispositivos pueden estar unidos a la nube o a híbrido.

Para más información, vea [Implementación de aplicaciones disponibles para el usuario](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).

### <a name="microsoft-365-apps-for-enterprise"></a>Aplicaciones de Microsoft 365 para empresas
<!--6298093-->
El nombre de Office 365 ProPlus se ha cambiado por Aplicaciones de Microsoft 365 para empresas el 21 de abril de 2020. A partir de la versión 2006, se han realizado los cambios siguientes:

- La consola de Configuration Manager se ha actualizado para reflejar el nombre nuevo.
  - Este cambio también incluye nombres de canal de actualización para Aplicaciones de Microsoft 365.
- Se ha agregado una notificación de banner a la consola para que le notifique si una o varias reglas de implementación automática hacen referencia a nombres de canal obsoletos en los criterios de **Título** para las actualizaciones de Aplicaciones de Microsoft 365.

Para más información, vea [Nombres de canales para Aplicaciones de Microsoft 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) y [Panel de preparación de Aplicaciones de Microsoft 365](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementación del sistema operativo

### <a name="task-sequence-media-support-for-cloud-based-content"></a> Compatibilidad de medios de secuencia de tareas para contenido basado en la nube

<!--6209223-->

Los medios de secuencia de tareas ahora pueden descargar contenido basado en la nube. Por ejemplo, puede enviar una llave USB a un usuario remoto para restablecer la imagen inicial de su dispositivo. O una oficina que tiene un servidor de entorno PXE local, pero quiere que los dispositivos den la máxima prioridad posible a los servicios en la nube. En lugar de sobrecargar la WAN para descargar el contenido de la implementación de un sistema operativo de gran tamaño, los medios de arranque y las implementaciones del entorno PXE ahora pueden obtener contenido de orígenes basados en la nube. Por ejemplo, una instancia de Cloud Management Gateway (CMG) que se habilita para compartir contenido.

> [!NOTE]
> El dispositivo sigue necesitando una conexión de intranet al punto de administración.

Para más información, vea [Usar medios de arranque para implementar Windows a través de la red](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

### <a name="improvements-to-task-sequences-via-cmg"></a> Mejoras en las secuencias de tareas a través de CMG

Esta versión incluye las siguientes mejoras para implementar secuencias de tareas en dispositivos que se comunican a través de una puerta de enlace de administración en la nube (CMG):

- Compatibilidad con la implementación de sistema operativo<!--6997525-->: con una secuencia de tareas que usa una imagen de arranque para implementar un sistema operativo, puede implementarlo en un dispositivo que se comunique a través de CMG. El usuario debe iniciar la secuencia de tareas desde el Centro de Software. Para más información, vea [Planificación de Cloud Management Gateway: especificaciones](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications).

- En esta versión se corrigen los dos [problemas conocidos](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg) de la rama actual de Configuration Manager, versión 2002.<!-- 6983320 --> Ahora puede ejecutar una secuencia de tareas en un dispositivo que se comunique a través de CMG en las siguientes circunstancias:

  - Un dispositivo de grupo de trabajo que se ha registrado con un [token de registro en masa](../../clients/deploy/deploy-clients-cmg-token.md).

  - Ha configurado el sitio para [HTTP mejorado](../hierarchy/enhanced-http.md) y el punto de administración es HTTP.

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>Mejoras en los pasos de secuencia de tareas de BitLocker

<!--6995601-->

Ahora puede especificar el modo de cifrado de disco en los pasos de la secuencia de tareas **Habilitar BitLocker** y **Tener en servicio BitLocker**. De forma predeterminada, los pasos siguen usando el método de cifrado predeterminado para la versión del sistema operativo.

El paso **Habilitar BitLocker** también incluye ahora un parámetro **Omitir este paso para equipos que no tengan TPM o cuando TPM no esté habilitado**. Cuando se habilita esta opción, el paso registra un error en un dispositivo sin un TPM o un TPM que no se inicializa, y la secuencia de tareas continúa. Esta configuración facilita la administración del comportamiento de la secuencia de tareas en los dispositivos que no son totalmente compatibles con BitLocker.

Para más información, vea [Pasos de la secuencia de tareas](../../../osd/understand/task-sequence-steps.md).

### <a name="management-insight-rules-for-os-deployment"></a>Reglas de información de administración para la implementación de SO

<!--6982275-->

Cuando el tamaño de la directiva de secuencia de tareas supera los 32 MB, el cliente no puede procesar la directiva de gran tamaño. En consecuencia, el cliente no puede ejecutar la implementación de la secuencia de tareas. Para ayudar a administrar el tamaño de la directiva de las secuencias de tareas, esta versión incluye la siguiente información de administración:

- **Las secuencias de tareas de gran tamaño pueden contribuir a superar el tamaño máximo de la directiva**.

- **El tamaño total de la directiva para las secuencias de tareas supera el límite de la directiva**.

> [!TIP]
> Estas reglas se encuentran en un nuevo grupo para **Implementación de sistema operativo**. La regla existente para **Imágenes de arranque no utilizadas** ahora también está en este grupo.

Para más información, vea [Información de administración](../../servers/manage/management-insights.md#operating-system-deployment).

### <a name="improvements-to-os-deployment"></a>Mejoras en la implementación del sistema operativo

Esta versión incluye las siguientes mejoras adicionales en la implementación del sistema operativo:

- Use una variable de secuencia de tareas para especificar el destino del paso [Formatear y crear particiones en el disco](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Esta nueva opción de variable admite secuencias de tareas más complejas con comportamientos dinámicos. Por ejemplo, un script personalizado puede detectar el disco y establecer la variable en función del tipo de hardware. A continuación, puede usar varias instancias de este paso para configurar diferentes tipos de hardware y particiones.<!--6610288-->

- El paso [Comprobar preparación](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) incluye ahora una comprobación para determinar si el dispositivo usa UEFI. También incluye una nueva variable de secuencia de tareas de solo lectura, **_TS_CRUEFI**.<!--6452769-->

- Si habilita la [ventana de progreso de la secuencia de tareas](../../../osd/understand/user-experience.md#task-sequence-progress) para mostrar información de progreso más detallada, ahora no cuenta los pasos habilitados en un grupo deshabilitado. Este cambio permite que la estimación del progreso sea más precisa.<!--6448412-->

- Anteriormente, durante una secuencia de tareas para actualizar un dispositivo a Windows 10, se abrió una ventana del símbolo del sistema durante una de las fases finales de configuración de Windows. La ventana estaba en la parte superior de la configuración rápida (OOBE) de Windows y los usuarios podían interactuar con ella para interrumpir el proceso de actualización. Ahora, los scripts SetupCompleteTemplate.cmd y SetupRollbackTemplate.cmd de Configuration Manager incluyen un cambio para ocultar esta ventana del símbolo del sistema.<!--2837795-->

- Algunos clientes crean interfaces de secuencia de tareas personalizadas mediante el método **IProgressUI::ShowMessage**, pero no devuelven un valor para la respuesta del usuario. Esta versión agrega el método [IProgressUI::ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md). Este nuevo método es similar al existente, pero también incluye una nueva variable de resultado entero, **pResult**.<!--6448458-->

## <a name="protection"></a>Protección

### <a name="cmg-support-for-endpoint-protection-policies"></a>Compatibilidad de CMG con las directivas de protección de los puntos de conexión

<!--4773948-->

Mientras que Cloud Management Gateway (CMG) tiene directivas de protección de puntos de conexión compatibles, los dispositivos requerían acceso a los controladores de dominio locales. A partir de esta versión, los clientes que se comunican a través de CMG pueden aplicar inmediatamente directivas de Endpoint Protection sin una conexión activa a Active Directory.

Para más información, vea [Compatibilidad de CMG con características de Configuration Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features).

### <a name="bitlocker-management-support-for-hierarchies"></a>Compatibilidad de la administración de BitLocker con jerarquías

<!-- 5925693 -->

Ahora, puede instalar el portal de autoservicio de BitLocker y el sitio web de administración y supervisión en el sitio de administración central.

Para más información, vea [Configuración de los portales de BitLocker](../../../protect/deploy-use/bitlocker/setup-websites.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Consola de Configuration Manager

### <a name="community-hub-and-github"></a>GitHub y Centro de comunidad
<!--3555935, 3555936, deep link included 4224406-->

*(Se incorporó por primera vez en junio de 2020)*

La comunidad de administradores de TI ha desarrollado multitud de conocimientos con el paso de los años. En lugar de reinventar elementos como scripts e informes desde cero, hemos creado un **Centro de comunidad** de Configuration Manager donde compartirlos. Al aprovechar el trabajo de los demás, puede ahorrarse horas de trabajo. El Centro de comunidad fomenta la creatividad mediante la creación de otros trabajos y con otras personas que se basan en los suyos. GitHub ya tiene procesos y herramientas en todo el sector diseñados para el uso compartido. Ahora, el Centro de comunidad aprovechará esas herramientas directamente en la consola de Configuration Manager como piezas fundamentales para impulsar esta nueva comunidad. Para la versión inicial, el contenido disponible en el Centro de comunidad solo será cargado por Microsoft. 

Para más información, consulte [Centro de comunidad y GitHub](../../servers/manage/community-hub.md).

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Vínculos directos a elementos del Centro de comunidad
<!--4224406-->
Puede desplazarse fácilmente hasta los elementos del nodo Centro de comunidad de la consola de Configuration Manager, y hacer referencia a ellos, con un vínculo directo. Para más información, vea [Vínculos directos a elementos del Centro de comunidad](../../servers/manage/community-hub.md#bkmk_deeplink).

### <a name="notifications-from-microsoft"></a>Notificaciones de Microsoft
<!--3953121-->
Ahora puede optar por recibir notificaciones de Microsoft en la consola de Configuration Manager. Estas notificaciones le ayudan a mantenerse informado acerca de los cambios o las actualizaciones de características, los cambios en Configuration Manager y los servicios asociados y los problemas que requieren una acción para solucionarse.

Para más información, vea [Configuración de un sitio para recibir mensajes desde Microsoft](../../servers/manage/admin-console-notifications.md#bkmk_msft).

### <a name="power-bi-sample-reports"></a>Informes de ejemplo de Power BI
<!--5679791-->

*(Se incorporó por primera vez en junio de 2020)*

Al integrar Power BI Report Server con los informes de Configuration Manager, ahora hay disponibles informes de Power BI de ejemplo. Descargue e instale los siguientes informes de ejemplo:

- Estado de compatibilidad de las actualizaciones de software
- Estado de implementación de actualizaciones de software

Para más información, vea [Instalación de informes de ejemplo de Power BI](../../servers/manage/powerbi-sample-reports.md).

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> Sistemas operativos en desuso

Obtenga información sobre los cambios de compatibilidad antes de implementarlos en [Elementos eliminados y en desuso](deprecated/removed-and-deprecated.md).

Tal como se anunció por primera vez en la versión 1906, la versión 2006 anula la compatibilidad con las siguientes versiones de sistema operativo cliente:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise

## <a name="other-updates"></a>Otras actualizaciones

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

Para obtener más información sobre los cambios en los cmdlets de Windows PowerShell relativos a Configuration Manager, vea las [notas de la versión de PowerShell 2006](/powershell/sccm/2006-release-notes?view=sccm-ps).

Para obtener más información sobre los cambios en la API REST del servicio de administración, consulte las [notas de la versión del servicio de administración](../../../develop/adminservice/release-notes.md#bkmk_2006).

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4556203).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Pasos siguientes

En este momento, la versión 2006 se ha lanzado para el anillo de actualización inicial. Para instalar esta actualización, debe indicar su consentimiento para participar. Para más información, consulte [Círculo de actualizaciones inicial](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring).

<!-- As of May 11, 2020, version 2006 is globally available for all customers to install. -->

Cuando esté listo para instalar esta versión, vea cómo [instalar actualizaciones para Configuration Manager](../../servers/manage/updates.md) y la [lista de comprobación para la instalación de la actualización 2006](../../servers/manage/checklist-for-installing-update-2006.md).

> [!TIP]
> Para instalar un sitio nuevo, use una versión de línea de base de Configuration Manager.
>
> Más información acerca de:
>
> - [Instalación de nuevos sitios](../../servers/deploy/install/installing-sites.md)
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)

Para conocer los problemas conocidos e importantes, vea las [Notas de la versión](../../servers/deploy/install/release-notes.md).

Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).