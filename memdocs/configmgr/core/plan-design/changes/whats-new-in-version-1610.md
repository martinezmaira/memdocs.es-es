---
title: Nueva versión 1610
titleSuffix: Configuration Manager
description: Conozca en detalle los cambios y las nuevas funciones introducidas en la versión 1610 de Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d154dc0ba681a37ebb2155bfa1bcdb6d8734965f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073966"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Novedades de la versión 1610 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 1610 de la rama actual de Configuration Manager está disponible como actualización en consola para los sitios instalados previamente que ejecutan las versiones 1511, 1602 o 1606.


> [!TIP]  
> Para instalar un sitio nuevo, debe usar una versión de línea base de Configuration Manager.  
>
> Más información acerca de:    
> - [Instalación de nuevos sitios](https://technet.microsoft.com/library/mt590197.aspx)  
> - [Instalación de actualizaciones en los sitios](https://technet.microsoft.com/library/mt607046.aspx)  
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)

En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1610 de Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Supervisión en la consola del estado de la instalación de actualización  
A partir de la versión 1610, cuando instale un paquete de actualizaciones y supervise la instalación en la consola, hay una fase nueva: **Postinstalación**. En esta fase se incluye el estado de las tareas como el reinicio de los servicios clave y la inicialización de la supervisión de replicación. (Esta fase no está disponible en la consola hasta que el sitio se actualice a la versión 1610). Para obtener más información sobre el estado de la instalación de actualización, consulte [Install in-console updates (Instalación de actualizaciones en la consola)](../../servers/manage/install-in-console-updates.md#bkmk_install).


## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir a clientes de la actualización automática
Puede excluir clientes de Windows de la actualización con las versiones nuevas del software cliente. Para hacer esto, incluya los equipos cliente en una colección que sea específica para excluirse de la actualización. Los clientes de la colección excluida omiten las solicitudes para actualizar el software cliente.  Para obtener más información, consulte [Exclude Windows clients from upgrades (Excluir clientes Windows de las actualizaciones)](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Mejoras en los grupos de límites
La versión 1610 presenta cambios importantes en los grupos de límites y en su funcionamiento con los puntos de distribución. Estos cambios pueden simplificar el diseño de la infraestructura de contenido, a la vez que proporcionan más control sobre cómo y cuándo usan la reserva los clientes para buscar puntos de distribución adicionales como ubicaciones de origen de contenido. Esto incluye tanto puntos de distribución locales como basados en la nube.
Estas mejoras reemplazan conceptos y comportamientos con los que puede que esté familiarizado, como la configuración de puntos de distribución para que sean rápidos o lentos. El nuevo modelo será más fácil de configurar y mantener. Estos cambios también constituyen la base para futuros cambios que mejorarán otros roles de sistema de sitio que asocia a los grupos de límites.

Cuando actualiza a la versión 1610, la actualización convierte las configuraciones de los grupos de límites actuales para ajustarse al nuevo modelo, de modo que estos cambios no afecten a las configuraciones de distribución de contenido existentes.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](../../servers/deploy/configure/boundary-groups.md).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Almacenamiento en caché del mismo nivel para la distribución de contenido en los clientes
A partir de la versión 1610, el **almacenamiento en caché del mismo nivel** de cliente le ayuda a administrar la implementación de contenido en los clientes en ubicaciones remotas. El almacenamiento en caché del mismo nivel es una solución integrada de Configuration Manager para que los clientes compartan contenido con otros clientes directamente desde su caché local.

Después de implementar la configuración de cliente que habilita el almacenamiento en caché del mismo nivel en una colección, los miembros de esa colección pueden actuar como origen de contenido del mismo nivel para otros clientes en el mismo grupo de límites.

También puede usar el nuevo panel **Orígenes de datos de cliente** para entender el uso de los orígenes de contenido del almacenamiento en caché del mismo nivel en su entorno.

> [!TIP]  
> Con la versión 1610, el panel de orígenes de datos de cliente y la caché del mismo nivel son funciones de la versión preliminar. Para habilitarlos, vea [Uso de características de la versión preliminar a partir de las actualizaciones](../../servers/manage/install-in-console-updates.md#bkmk_prerelease).

Para obtener más información, consulte [Caché del mismo nivel para clientes de Configuration Manager](../hierarchy/client-peer-cache.md) y [Panel de orígenes de datos de cliente](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar varios puntos de distribución compartidos al mismo tiempo
Ahora puede usar la opción **Reasignar punto de distribución** para que Configuration Manager procese en paralelo la reasignación de un máximo de 50 puntos de distribución compartidos al mismo tiempo. Antes de esta versión, los puntos de distribución reasignados se procesaban de uno en uno. Para obtener más información, consulte [Migrate multiple shared distribution points at the same time (Migrar varios puntos de distribución compartidos al mismo tiempo)](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Puerta de enlace de administración en la nube para administrar los clientes basados en Internet

La puerta de enlace de administración en la nube proporciona una manera sencilla de administrar clientes de Configuration Manager en Internet. El servicio de puerta de enlace de administración en la nube, que se implementa en Microsoft Azure y exige una suscripción de Azure, se conecta a la infraestructura local de Configuration Manager con un nuevo rol denominado punto de conexión de la puerta de enlace de administración en la nube. Una vez implementado y configurado por completo, los clientes pueden comunicarse con los roles del sistema de sitio local de Configuration Manager y con los puntos de distribución basados en la nube independientemente de si están conectados en la red privada interna o en Internet. Para obtener más información y ver cómo la puerta de enlace de administración en la nube se compara con la administración de cliente basada en Internet, consulte [Manage clients on the Internet (Administrar clientes en Internet)](../../clients/manage/manage-clients-internet.md).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Mejoras en la directiva de actualización de la edición de Windows 10
En esta versión se han realizado las siguientes mejoras en este tipo de directiva:

- Ahora puede usar la directiva de actualización de la edición con equipos Windows 10 que ejecuten el cliente de Configuration Manager además de con equipos Windows 10 inscritos en Microsoft Intune.
- Puede actualizar desde Windows 10 Professional a cualquiera de las plataformas del asistente compatibles con el hardware.

## <a name="manage-hardware-identifiers"></a>Administrar identificadores de hardware
Ahora puede proporcionar una lista de identificadores de hardware que Configuration Manager debe omitir en el registro de clientes y el arranque PXE. Esto ayuda a resolver dos problemas comunes:

1. Muchos dispositivos, como Surface Pro 3, no incluyen un puerto Ethernet incorporado. Generalmente, se usa un adaptador de USB a Ethernet para establecer una conexión por cable para la implementación de un sistema operativo. Sin embargo, suele tratarse de adaptadores compartidos debido a su costo y su facilidad de uso general. Dado que la dirección MAC de este adaptador se usa para identificar el dispositivo, resulta problemático volver a usar el adaptador si no se realizan acciones de administrador adicionales entre cada implementación. Ahora, en la versión 1610 de Configuration Manager, puede excluir la dirección MAC de este adaptador para que se pueda volver a usar fácilmente en este escenario.
2. Se supone que el identificador de SMBIOS es un identificador de hardware único, pero algunos dispositivos de hardware especiales se crean con identificadores duplicados. Puede que este problema no sea tan habitual como el escenario del adaptador de USB a Ethernet descrito anteriormente, pero puede solucionarlo usando la lista de identificadores de hardware excluidos.

Para obtener más información, consulte [Manage duplicate hardware identifiers (Administrar identificadores de hardware duplicados)](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Mejoras en la integración de la Tienda Windows para empresas con Configuration Manager
Cambios de esta versión:
- Anteriormente, solo se podían implementar aplicaciones gratuitas de la Tienda Windows para empresas. Configuration Manager ahora además admite la implementación de aplicaciones con licencia en línea de pago (solo para dispositivos inscritos en Intune).
- Ahora puede iniciar una sincronización inmediata entre la Tienda Windows para empresas y Configuration Manager.
- Ahora puede modificar la clave secreta de cliente que ha obtenido de Azure Active Directory.
- Puede eliminar una suscripción de la tienda.

Para más información, vea [Administración de aplicaciones desde la Tienda Windows para empresas con Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronización de directivas para dispositivos inscritos en Intune
Ahora puede solicitar la sincronización de directivas para un dispositivo inscrito en Intune desde la consola de Configuration Manager, en lugar de hacerlo desde la aplicación de portal de empresa en el propio dispositivo. La información del estado de la solicitud de sincronización está disponible como una columna nueva en las vistas del dispositivo, denominada **Remote Sync State (Estado de la sincronización remota)** . La información también está disponible en la sección de datos de detección del cuadro de diálogo **Propiedades** de cada dispositivo.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Usar la configuración de cumplimiento para configurar las opciones de Windows Defender
Ahora puede establecer la configuración de cliente de Windows Defender en equipos Windows 10 inscritos en Intune mediante el uso de elementos de configuración de la consola de Configuration Manager.
Para más información, vea la sección **Windows Defender** de [Crear elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).



## <a name="general-improvements-to-software-center"></a>Mejoras generales en el Centro de software
- Ahora los usuarios pueden solicitar aplicaciones del Centro de software, así como del catálogo de aplicaciones.
- Mejoras para ayudar a los usuarios a comprender qué software es nuevo y relevante.

## <a name="new-columns-in-device-collection-views"></a>Columnas nuevas en las vistas de colección de dispositivos
Ahora puede mostrar columnas para **IMEI** y **Número de serie** (para dispositivos iOS) en las vistas de colección de dispositivos.

## <a name="customizable-branding-for-software-center-dialogs"></a>Cuadros de diálogo personalizables de personalización de marca del Centro de software
La personalización de marca del Centro de software se presentó en la versión 1602 de Configuration Manager. En la versión 1610, esa marca se ha ampliado ahora a todos los cuadros de diálogo asociados para proporcionar una experiencia más coherente a los usuarios del Centro de software.

La personalización de marca del Centro de software se aplica conforme a las siguientes reglas:

- Si no está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de organización especificado en la configuración de cliente **Agente de equipo** **Nombre de organización mostrado en el Centro de software**. Para obtener instrucciones, vea [Cómo establecer la configuración del cliente](../../clients/deploy/configure-client-settings.md).

- Si está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de la organización y el color especificados en las propiedades del rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones. Para más información, vea [Configuration options for Application Catalog website point (Opciones de configuración del punto de sitios web del catálogo de aplicaciones)](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

- Si una suscripción de Microsoft Intune está configurada y conectada al entorno de Configuration Manager, el Centro de software mostrará el nombre de la organización, el color y el logotipo de la empresa especificados en las propiedades de la suscripción de Intune.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Período de gracia de cumplimiento para implementaciones de actualizaciones de software y aplicaciones requeridas
En algunos casos, es posible que quiera dar más tiempo a los usuarios para instalar las implementaciones de aplicaciones o las actualizaciones de software necesarias más allá de los plazos que ha establecido. Por ejemplo, esto puede resultar necesario cuando un equipo ha estado apagado durante un largo período de tiempo y tiene que instalar muchas implementaciones de aplicaciones o actualizaciones. Por ejemplo, si un usuario final acaba de volver de vacaciones, es posible que tenga que esperar bastante mientras se instalan las implementaciones de aplicaciones vencidas. Para solucionar este problema, puede definir un período de gracia de cumplimiento mediante la implementación de la configuración de cliente de Configuration Manager en una colección. 

Para configurar el período de gracia, haga lo siguiente:
1. En la página **Agente de equipo** de la configuración de cliente, configure la nueva propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** con un valor entre **1** y **120** horas.
2. En una nueva implementación de aplicación obligatoria o en las propiedades de una implementación existente, en la página **Programación**, active la casilla **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario** hasta el período de gracia definido en la configuración del cliente. Todas las implementaciones que tengan activada esta casilla y que estén destinadas a dispositivos en los que también haya implementado la configuración de cliente usarán el período de gracia de cumplimiento.

Si configura un período de gracia de cumplimiento y activa la casilla de verificación, una vez que se llegue a la fecha límite de instalación de la aplicación, esta se instalará en la primera ventana que no sea de empresa configurada por el usuario hasta ese período de gracia. No obstante, el usuario puede abrir el Centro de software e instalar la aplicación en cualquier momento que quiera. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas. Se han agregado opciones similares al asistente para la implementación de actualizaciones de software, al asistente para reglas de implementación automática y a las páginas de propiedades.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Funcionalidad mejorada en cuadros de diálogo sobre el software necesario
Cuando un usuario recibe software obligatorio, desde el valor **Posponer y volver a recordármelo en:** , puede seleccionar las siguientes opciones en la lista desplegable: 
- **Más adelante**. Especifica que las notificaciones se programan según la configuración de notificación establecida en la configuración de agente de cliente.
- **Hora fija**. Especifica que la notificación se programará para mostrarse de nuevo después del tiempo seleccionado (por ejemplo, en 30 minutos).

![Página Agente de equipo de Configuración de agente de cliente](media/client-notification-settings.png)

El tiempo máximo de aplazamiento se basa en los valores de notificación definidos en la configuración de agente de cliente. Por ejemplo, si la opción **La fecha límite de la implementación es de más de 24 horas. Recordar al usuario cada (horas)** de la página Agente de equipo se configura para 10 horas y pasan más de 24 antes de la fecha límite, el usuario vería un conjunto de opciones para posponer de hasta 10 horas, pero nunca más. Cuando se acerca la fecha límite, hay menos opciones disponibles, en consonancia con la configuración de agente de cliente correspondiente a cada componente de la escala de tiempo de implementación.

Además, en una implementación de alto riesgo, como una secuencia de tareas que implementa un sistema operativo, la experiencia de notificación del usuario es ahora más intrusiva. En lugar de una notificación transitoria en la barra de tareas, cada vez que se notifica al usuario que se necesita mantenimiento de software crítico, aparece un cuadro de diálogo como el siguiente en el equipo del usuario:

![Cuadro de diálogo Software requerido](media/client-toast-notification.png)


Para obtener más información:
- [Settings to manage high-risk deployments (Configuración para administrar implementaciones de alto riesgo)](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Cómo configurar el cliente](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Panel de actualizaciones de software
Use el nuevo panel de actualizaciones de software para ver el estado de cumplimiento actual de los dispositivos de la organización y analizar rápidamente los datos para ver los dispositivos que están en riesgo. Para ver el panel, vaya a **Supervisión** > **Información general** > **Seguridad** > **Software Updates Dashboard (Panel de actualizaciones de software)** .

Para obtener detalles, vea [Monitor software updates (Supervisar actualizaciones de software)](../../../sum/deploy-use/monitor-software-updates.md).


## <a name="improvements-to-the-application-request-process"></a>Mejoras en el proceso de solicitud de aplicaciones
Después de aprobar una aplicación para la instalación, puede denegar la solicitud. Para ello, haga clic en **Denegar** en la consola de Configuration Manager. Antes, este botón aparecía atenuado tras la aprobación.

Esta acción no provoca que la aplicación se desinstale de ningún dispositivo. En cambio, impide que los usuarios instalen copias nuevas de la aplicación desde el Centro de software.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamaño del contenido en las reglas de implementación automática
Ahora se puede filtrar por el tamaño del contenido de las actualizaciones de software en las reglas de implementación automática. Por ejemplo, para descargar solo las actualizaciones de software de menos de 2 MB, puede establecer el filtro **Tamaño del contenido (KB)** en **< 2048**. Con este filtro se evita que las actualizaciones de software de gran tamaño se descarguen automáticamente, lo que ofrece un mantenimiento simplificado de nivel inferior de Windows cuando el ancho de banda de la red es limitado. Si desea obtener información detallada, consulte:
- [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager y mantenimiento simplificado de Windows en sistemas operativos de nivel inferior)
- [Implementar actualizaciones de software automáticamente](../../../sum/deploy-use/automatically-deploy-software-updates.md)

Para configurar el campo **Tamaño del contenido (KB)** , realice una de las siguientes acciones:
- Cuando cree una regla de implementación automática, en el Asistente para crear regla de implementación automática, vaya a la página **Actualizaciones de software**.
- En las propiedades de una regla de implementación automática existente, vaya a la pestaña **Actualizaciones de software**.

## <a name="office-365-client-management-dashboard"></a>Panel de administración de clientes de Office 365
El panel de administración de clientes de Office 365 ahora está disponible en la consola de Configuration Manager. Para ver el panel, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.

El panel muestra gráficos para lo siguiente:

- Número de clientes de Office 365
- Versiones de cliente de Office 365
- Idiomas de cliente de Office 365
- Canales de cliente de Office 365     

Para obtener información, consulte [Administración de actualizaciones de Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI
Ahora puede personalizar una secuencia de tareas de implementación de sistema operativo con una nueva variable, TSUEFIDrive, para que el paso **Reiniciar el equipo** prepare una partición FAT32 en la unidad de disco duro para la transición a UEFI. En el procedimiento siguiente se proporciona un ejemplo de cómo crear pasos de secuencia de tareas para preparar la unidad de disco duro para la conversión de BIOS en UEFI. Para obtener más información, consulte [Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Mejoras en el paso de secuencia de tareas: Prepare ConfigMgr Client for Capture  
El paso Preparar el cliente de Configuration Manager quitará por completo el cliente de Configuration Manager en lugar de quitar solo la información de clave. Cuando la secuencia de tareas implementa la imagen capturada del sistema operativo, se instala un nuevo cliente de Configuration Manager cada vez. Para obtener más información, consulte [Task sequence steps (Pasos de la secuencia de tareas)](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Gráficos de directivas cumplimiento de Intune
Ahora puede obtener una vista rápida del cumplimiento general de los dispositivos y de las principales razones del incumplimiento con los nuevos gráficos del área de trabajo **Supervisión** de la consola de Configuration Manager. Puede hacer clic en una sección del gráfico para explorar en profundidad una lista de los dispositivos de esa categoría. Para obtener más información, consulte [Monitor the compliance policy (Supervisar la directiva de cumplimiento)](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integración de Lookout en las implementaciones híbridas para proteger los dispositivos iOS y Android
Microsoft se está integrando en la solución de protección de amenazas móviles de Lookout para proteger los dispositivos móviles iOS y Android mediante la detección de malware y aplicaciones de riesgo, entre otros, en los dispositivos. La solución de Lookout le ayuda a determinar el nivel de amenaza, que es configurable. Puede crear una regla de directivas de cumplimiento en Configuration Manager para determinar el cumplimiento de dispositivo basándose en la evaluación de riesgos mediante Lookout. Con las directivas de acceso condicional, puede permitir o bloquear el acceso a los recursos empresariales basándose en el estado de cumplimiento del dispositivo.

Se solicitará a los usuarios de dispositivos iOS no compatibles que se inscriban. Necesitarán instalar la aplicación Lookout for Work en sus dispositivos, activar la aplicación y corregir las amenazas que se mencionan en la aplicación Lookout for Work para obtener acceso a los datos de la empresa.


## <a name="new-compliance-settings-for-configuration-items"></a>Nueva configuración de cumplimiento para elementos de configuración
Hay muchas opciones nuevas que se pueden usar en los elementos de configuración de varias plataformas de dispositivo. Son opciones que existían con anterioridad en Microsoft Intune en una configuración independiente y que ahora están disponibles al usar Intune con Configuration Manager.
Para más información, vea [Elementos de configuración para dispositivos administrados sin el cliente de Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-settings-for-android-devices"></a>Nuevas opciones para dispositivos Android
#### <a name="password-settings"></a>Configuración de contraseña
- **Recordar el historial de contraseñas**
- **Permitir desbloqueo mediante huellas digitales**

#### <a name="security-settings"></a>Configuración de seguridad
- **Requerir cifrado en tarjetas de almacenamiento**
- **Permitir captura de pantalla**
- **Permitir el envío de datos de diagnóstico**

#### <a name="browser-settings"></a>Configuración del explorador
- **Permitir explorador web**
- **Permitir autorrelleno**
- **Permitir bloqueador de elementos emergentes**
- **Permitir cookies**
- **Permitir Active scripting**

#### <a name="app-settings"></a>Configuración de aplicaciones
- **Permitir Google Play Store**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos
- **Permitir almacenamiento extraíble**
- **Permitir tethering Wi-Fi**
- **Permitir geolocalización**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir itinerancia de voz**
- **Permitir itinerancia de datos**
- **Permitir mensajería SMS/MMS**
- **Permitir asistente de voz**
- **Permitir marcación por voz**
- **Permitir copiar y pegar**

### <a name="new-settings-for-ios-devices"></a>Nuevas opciones para dispositivos iOS
#### <a name="password-settings"></a>Configuración de contraseña
- **Número de caracteres complejos necesarios en la contraseña**
- **Permitir contraseñas sencillas**
- **Minutos de inactividad antes de que se requiera la contraseña**
- **Recordar el historial de contraseñas**

### <a name="new-settings-for-mac-os-x-devices"></a>Nuevas opciones para dispositivos Mac OS X
#### <a name="password-settings"></a>Configuración de contraseña
- **Número de caracteres complejos necesarios en la contraseña**
- **Permitir contraseñas sencillas**
- **Recordar el historial de contraseñas**
- **Minutos de inactividad antes de que se active el protector de pantalla**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nuevas opciones para dispositivos Windows 10 Escritorio y Mobile
#### <a name="password-settings"></a>Configuración de contraseña
- **Número mínimo de conjuntos de caracteres**
- **Recordar el historial de contraseñas**
- **Requerir una contraseña cuando el dispositivo vuelva de un estado de inactividad**

#### <a name="security-settings"></a>Configuración de seguridad
- **Requerir cifrado en el dispositivo móvil**
- **Permitir cancelar suscripción manualmente**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos
- **Permitir VPN sobre móvil**
- **Permitir itinerancia de VPN sobre móvil**
- **Permitir restablecer teléfono**
- **Permitir conexión USB**
- **Permitir a Cortana**
- **Permitir notificaciones del centro de actividades**

### <a name="new-settings-for-windows-10-team-devices"></a>Nuevas opciones para dispositivos Windows 10 Team
#### <a name="device-settings"></a>Configuración del dispositivo
- **Habilitar Visión operativa de Azure**
- **Habilitar proyección inalámbrica de Miracast**
- **Seleccione la información sobre la reunión que se muestra en la pantalla de inicio de sesión**
- **URL de imagen de fondo de pantalla de bloqueo**

### <a name="new-settings-for-windows-81-devices"></a>Nuevas opciones para dispositivos Windows 8.1
#### <a name="applicability-settings"></a>Configuración de la aplicación
- **Aplicar todas las configuraciones a Windows 10**

#### <a name="password-settings"></a>Configuración de contraseña
- **Tipo de contraseña requerida**
- **Número mínimo de conjuntos de caracteres**
- **Longitud mínima de la contraseña**
- **Número de errores de inicio de sesión consecutivos permitidos antes de que se borre el dispositivo**
- **Minutos de inactividad antes de que se apague la pantalla**
- **Expiración de la contraseña (días)**
- **Recordar el historial de contraseñas**
- **Impedir la reutilización de contraseñas anteriores**
- **Permitir contraseña de imagen y PIN**

#### <a name="browser-settings"></a>Configuración del explorador
- **Permitir la detección automática de redes de intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Nuevas opciones para dispositivos Windows Phone 8.1
#### <a name="applicability-settings"></a>Configuración de la aplicación
- **Aplicar todas las configuraciones a Windows 10**

#### <a name="password-settings"></a>Configuración de contraseña
- **Número mínimo de conjuntos de caracteres**
- **Permitir contraseñas sencillas**
- **Recordar el historial de contraseñas**

#### <a name="device-capability-settings"></a>Configuración de las capacidades de los dispositivos
- **Permitir conexión automática a zonas Wi-Fi gratuitas**
