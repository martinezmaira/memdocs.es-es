---
title: Novedades de la versión 2002
titleSuffix: Configuration Manager
description: Obtenga detalles sobre los cambios y las nuevas funcionalidades incorporados en la versión 2002 de la rama actual de Configuration Manager.
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 38ea77e44b1d1754d80d0ec902929f5de620c063
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993342"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Novedades de la versión 2002 de la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 2002 de la rama actual de Configuration Manager está disponible como una actualización en consola. Aplique esta actualización en los sitios que ejecuten la versión 1810 o versiones posteriores. <!-- baseline only statement:-->Al instalar un nuevo sitio, también está disponible como una versión de línea de base. En este artículo se resumen los cambios y las nuevas características de la versión 2002 de Configuration Manager.

Revise siempre la lista de comprobación más reciente para instalar esta actualización. Para obtener más información, vea la [lista de comprobación para la instalación de la actualización 2002](../../servers/manage/checklist-for-installing-update-2002.md). Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).

Para aprovechar al máximo las nuevas características de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

> [!TIP]
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Asociación de inquilinos de Microsoft Endpoint Manager

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Sincronización de dispositivos y acciones de dispositivo
<!--3555758-->
Microsoft Endpoint Manager es una solución integrada para administrar todos los dispositivos. Microsoft reúne Configuration Manager e Intune en una única consola denominada **centro de administración de Microsoft Endpoint Manager**. A partir de esta versión, puede cargar los dispositivos de Configuration Manager en el servicio en la nube y realizar acciones desde la hoja **Dispositivos** del centro de administración.

Para obtener más información, vea el artículo [Asociación de inquilinos de Microsoft Endpoint Manager](../../../tenant-attach/device-sync-actions.md).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infraestructura del sitio

### <a name="remove-a-central-administration-site"></a>Eliminación de un sitio de administración central
<!-- 3607277 -->

Si su jerarquía consta de un sitio de administración central (CAS) y de un único sitio primario secundario, ahora puede quitar el CAS. Esta acción simplifica la infraestructura de Configuration Manager a un único sitio primario independiente. Elimina las complejidades de la replicación de sitio a sitio y centra sus tareas de administración en un único sitio primario.

Para obtener más información, vea [Eliminación del CAS](../../servers/deploy/install/remove-central-administration-site.md).

### <a name="new-management-insight-rules"></a>Nuevas reglas de conclusiones de administración

Esta versión incluye las siguientes reglas de conclusiones de administración:

- Nueve reglas en el grupo **Configuration Manager Assessment**, cortesía del soporte técnico Premier de Microsoft Azure de ingeniería de campo. Estas reglas son un ejemplo de las muchas comprobaciones más que proporciona el soporte técnico Premier de Microsoft Azure en el centro de servicios.<!-- 3607758 -->

  - La detección de grupos de seguridad de Active Directory está configurada para ejecutarse con demasiada frecuencia.
  - La detección de sistemas de Active Directory está configurada para ejecutarse con demasiada frecuencia.
  - La detección de usuarios de Active Directory está configurada para ejecutarse con demasiada frecuencia.
  - Recopilaciones limitadas a Todos los sistemas o Todos los usuarios.
  - La detección de latidos está deshabilitada.
  - Consultas de recopilaciones de larga duración habilitadas para las actualizaciones incrementales.
  - Reducir el número de aplicaciones y paquetes en los puntos de distribución.
  - Problemas de instalación del sitio secundario.
  - Actualizar todos los sitios a la misma versión.

- Dos reglas adicionales en el grupo de **Cloud Services** para ayudarle a configurar el sitio con el fin de agregar comunicación HTTPS segura:<!-- 6268489 -->

  - Sitios que no tienen una configuración correcta de HTTPS.
  - Dispositivos no cargados en Azure AD.

Para obtener más información, vea [Información de administración](../../servers/manage/management-insights.md).

### <a name="improvements-to-administration-service"></a>Mejoras en el servicio de administración

<!-- 5728365 -->

El servicio de administración es una API REST del proveedor de SMS. Anteriormente, había que implementar una de las siguientes dependencias:

- Habilitar HTTP mejorado para todo el sitio
- Enlazar de forma manual un certificado basado en PKI al IIS en el servidor que hospeda el rol de proveedor de SMS

A partir de esta versión, el servicio de administración usa automáticamente el certificado autofirmado del sitio. Este cambio ayuda a reducir la fricción para facilitar el uso del servicio de administración. El sitio siempre genera este certificado. La configuración de sitio HTTP mejorado en **Usar los certificados generados por Configuration Manager para sistemas de sitios HTTP** solo controla si los sistemas de sitio lo usan o no. Ahora, el servicio de administración omite esta configuración del sitio porque siempre usa el certificado del sitio, incluso si ningún otro sistema de sitio usa HTTP mejorado. Todavía puede usar un certificado de autenticación de servidor basado en PKI.

Para obtener más información, consulte los siguientes artículos nuevos:

- [¿Qué es el servicio de administración?](../../../develop/adminservice/overview.md)
- [Cómo configurar el servicio de administración](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Compatibilidad del proxy con la detección y la sincronización de grupos de Azure Active Directory

<!-- 5913817 -->

La configuración de proxy del sistema de sitio, incluida la autenticación, ahora se usa en:

- La detección de usuarios de Azure Active Directory (Azure AD).
- La detección de grupos de usuarios de Azure AD.
- La sincronización de los resultados de la pertenencia a recopilaciones con grupos de Azure Active Directory.

Para obtener más información, vea [Compatibilidad de servidor proxy](../network/proxy-server-support.md#bkmk_other).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Administración conectada a la nube

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>Mensaje de estado crítico que indica que hay errores de conexión del servidor con los puntos de conexión necesarios

<!-- 5566763 -->

Si el sitio de Configuration Manager no se puede conectar a los puntos de conexión necesarios para un servicio en la nube, genera un mensaje de estado crítico con el identificador 11488. Cuando el servidor de sitio no se puede conectar con el servicio, el estado del componente SMS_SERVICE_CONNECTOR cambia a crítico. Consulte el estado detallado en el nodo Estado del componente de la consola de Configuration Manager.

### <a name="token-based-authentication-for-cloud-management-gateway"></a>Autenticación basada en tokens para Cloud Management Gateway

<!-- 5686290 -->

Cloud Management Gateway (CMG) admite muchos tipos de clientes, pero, incluso con un protocolo HTTP mejorado, estos clientes requieren un certificado de autenticación de cliente. Este requisito de certificado puede ser difícil de aprovisionar en clientes basados en Internet que no se suelen conectar a la red interna, no consiguen conectar con Azure Active Directory (Azure AD) y no disponen de ningún método para instalar un certificado emitido con PKI.

Configuration Manager amplía la compatibilidad de su dispositivo con los métodos siguientes:

- Registro de un solo token en la red interna
- Creación de un token de registro masivo para dispositivos basados en Internet

Para obtener más información, vea [Autenticación basada en tokens para CMG](../../clients/deploy/deploy-clients-cmg-token.md).

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Características basadas en la nube de Microsoft Endpoint Configuration Manager

<!--5834830-->

Cuando haya nuevas características basadas en la nube disponibles en el centro de administración de Microsoft Endpoint Manager u otros servicios en la nube asociados para la instalación local de Configuration Manager, puede seleccionar estas nuevas características en la consola de Configuration Manager. Para obtener más información sobre la habilitación de características en la consola de Configuration Manager, vea [Habilitar características opcionales de las actualizaciones](../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Análisis de escritorio

Para más información sobre los cambios mensuales en el servicio en la nube de Análisis de escritorio, vea [Novedades de Análisis de escritorio](../../../desktop-analytics/whats-new.md).

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>El panel Estado de la conexión muestra los problemas de conexión del cliente

Use el panel Estado de la conexión de Análisis de escritorio que hay en Configuration Manager para supervisar el estado de conectividad de los clientes. Ahora le ayuda identificar más fácilmente los problemas de configuración del proxy de clientes en dos áreas:

- **Comprobaciones de conectividad del punto de conexión**: Si los clientes no se pueden conectar a un punto de conexión necesario, verá una alerta de configuración en el panel. Explore en profundidad para ver los puntos de conexión a los que los clientes no pueden conectarse debido a problemas de configuración del proxy.<!-- 4963230 -->

- **Estado de conectividad**: Si sus clientes usan un servidor proxy para acceder al servicio en la nube de Análisis de escritorio, Configuration Manager ahora muestra los problemas de autenticación del proxy que tienen los clientes. Explore en profundidad para ver los clientes que no se pueden inscribir debido a problemas de autenticación del proxy.<!-- 4963383 -->

Para más información, consulte [Supervisión del estado de conexión](../../../desktop-analytics/monitor-connection-health.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Administración en tiempo real

### <a name="improvements-to-cmpivot"></a>Mejoras en CMPivot

<!-- 5870934 -->

Se ha facilitado la navegación por las entidades CMPivot. Ahora puede buscar entidades CMPivot. También se han agregado nuevos iconos para que pueda diferenciar fácilmente las entidades y los tipos de objeto de entidad.

Para obtener más información, vea [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_2002).

## <a name="content-management"></a><a name="bkmk_content"></a> Administración de contenido

### <a name="exclude-certain-subnets-for-peer-content-download"></a>Exclusión de determinadas subredes para la descarga de contenido del mismo nivel

<!-- 3555777 -->

Los grupos de límites incluyen la opción siguiente para las descargas del mismo nivel: **Durante las descargas del mismo nivel, use solo elementos del mismo nivel dentro de la misma subred**. Si habilita esta opción, la lista de ubicaciones de contenido del punto de administración solo incluye orígenes del mismo nivel que se encuentran en la misma subred y el mismo grupo de límites que el cliente. En función de la configuración de su red, ahora puede excluir ciertas subredes para que no coincidan. Por ejemplo, en el caso de que quiera incluir un límite, pero excluir una subred de VPN específica.

Para obtener más información, consulte las [opciones de grupo de límites](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

### <a name="proxy-support-for-microsoft-connected-cache"></a>Compatibilidad del proxy con la Caché conectada de Microsoft

<!-- 5856396 -->

Si su entorno usa un servidor proxy no autenticado para el acceso a Internet, ahora cuando habilita un punto de distribución de Configuration Manager para la Caché conectada de Microsoft, puede comunicarse a través del proxy. Para más información, vea [Caché de conexión de Microsoft](../hierarchy/microsoft-connected-cache.md).

## <a name="client-management"></a><a name="bkmk_client"></a> Administración de clientes

### <a name="client-log-collection"></a>Recopilación de registros de cliente

<!-- 4226618 -->

Ahora puede desencadenar un dispositivo cliente para cargar sus registros de cliente en el servidor del sitio mediante el envío de una acción de notificación de cliente desde la consola de Configuration Manager.

Para obtener más información, consulte [Notificación de cliente](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="wake-up-a-device-from-the-central-administration-site"></a>Reactivación de un dispositivo desde el sitio de administración central

<!-- 6030715 -->

En el nodo Dispositivos o Recopilaciones de dispositivos del sitio de administración central (CAS), ahora puede usar la acción de notificación del cliente para reactivar dispositivos. Anteriormente, esta acción solo estaba disponible desde un sitio primario.

Para obtener más información, vea [Cómo configurar Wake on LAN](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810).

### <a name="improvements-to-support-for-arm64-devices"></a>Mejoras de compatibilidad con dispositivos ARM64

<!--5954175-->

La plataforma **Todo Windows 10 (ARM64)** está disponible en la lista de versiones de sistema operativo admitidas en objetos con reglas de requisitos o listas de aplicabilidad.

> [!NOTE]
> Si previamente ha seleccionado la plataforma de nivel superior **Windows 10**, esta acción ha seleccionado automáticamente **Todo Windows 10 (64 bits)** y **Todo Windows 10 (32 bits)** . Esta nueva plataforma no se selecciona automáticamente. Si quiere agregar **Todo Windows 10 (ARM64)** , selecciónelo manualmente en la lista.

Para obtener más información sobre la compatibilidad de Configuration Manager con dispositivos ARM64, vea [Windows 10 en ARM64](../configs/support-for-windows-10.md#bkmk_arm64).

### <a name="track-configuration-item-remediations"></a>Seguimiento de las correcciones de elementos de configuración
<!--4261411-->
Ahora puede **realizar un seguimiento del historial de correcciones cuando se admita** en las reglas de cumplimiento de los elementos de configuración. Cuando se habilita esta opción, cualquier corrección que se produzca en el cliente para el elemento de configuración generará un mensaje de estado. El historial se almacena en la base de datos de Configuration Manager.

Para obtener más información, consulte el artículo [Creación de elementos de configuración personalizados para equipos de escritorio y servidores de Windows administrados con el cliente de Configuration Manager](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track).

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a> Administración de aplicaciones

### <a name="microsoft-edge-management-dashboard"></a>Panel de administración de Microsoft Edge

<!-- 3871913 -->

El panel de administración de Microsoft Edge le proporciona información sobre el uso de Microsoft Edge y otros exploradores. En este panel, puede hacer lo siguiente:

- Ver cuántos dispositivos tienen instalado Microsoft Edge
- Vea cuántos clientes tienen instaladas versiones diferentes de Microsoft Edge
- Ver los exploradores instalados en todos los dispositivos
- Ver el explorador preferido en cada dispositivo

En el área de trabajo Biblioteca de software, haga clic en Administración de Microsoft Edge para ver el panel. Para cambiar la colección de los datos del gráfico, haga clic en Examinar y elija otra colección. De forma predeterminada, la lista desplegable incluye las cinco colecciones más grandes. Al seleccionar una colección que no está en la lista, la colección recién seleccionada pasa a ocupar la parte inferior de la lista desplegable.

Para obtener más información, vea el artículo [Administración de Microsoft Edge](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash).

### <a name="improvements-to-microsoft-edge-management"></a>Mejoras en la administración de Microsoft Edge

<!-- 4561024 -->

Ahora puede crear una aplicación de Microsoft Edge que esté configurada para recibir actualizaciones automáticas en lugar de deshabilitar las actualizaciones automáticas. Este cambio le permite elegir administrar las actualizaciones de Microsoft Edge con Configuration Manager o permitir que Microsoft Edge se actualice automáticamente. Al crear la aplicación, seleccione la opción para permitir que Microsoft Edge actualice automáticamente la versión del cliente en el dispositivo del usuario final en la página de configuración de Microsoft Edge.

Para obtener más información, vea el artículo [Administración de Microsoft Edge](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate).

### <a name="task-sequence-as-an-app-model-deployment-type"></a>Secuencia de tareas como un tipo de implementación de modelo de aplicación

<!-- 3555953 -->

Ahora puede instalar aplicaciones complejas mediante secuencias de tareas a través del modelo de aplicación. Agregue un tipo de implementación a una aplicación que sea una secuencia de tareas, para instalar o desinstalar la aplicación. Esta característica proporciona los comportamientos siguientes:

- Mostrar la secuencia de tareas de aplicación con un icono en el Centro de software. Un icono facilita a los usuarios buscar e identificar la secuencia de tareas de aplicación.

- Definir metadatos adicionales para la secuencia de tareas de aplicación, incluida información localizada.

Para obtener más información, vea [Creación de aplicaciones Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementación del sistema operativo

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>Arranque de una secuencia de tareas inmediatamente después del registro del cliente

<!-- 5526972 -->

Al instalar y registrar un nuevo cliente de Configuration Manager, y también implementar una secuencia de tareas en él, es difícil determinar cuánto tiempo después del registro se ejecutará la secuencia de tareas. En esta versión se introduce una nueva propiedad de instalación de cliente que puede usar para iniciar una secuencia de tareas en un cliente después de que se registre correctamente en el sitio.

Para obtener más información, vea [Acerca de los parámetros y propiedades de instalación de cliente: PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts).

### <a name="improvements-to-check-readiness-task-sequence-step"></a>Mejoras en el paso de la secuencia de tareas “Comprobar preparación”

<!-- 6005561 -->

Ahora puede comprobar más propiedades del dispositivo en el paso de la secuencia de tareas **Comprobar preparación**. Use este paso en una secuencia de tareas para comprobar que el equipo de destino cumpla los requisitos previos.

- Arquitectura del sistema operativo actual
- Versión de SO mínima
- Versión de SO máxima
- Versión mínima del cliente
- Idioma del sistema operativo actual
- Alimentación de CA conectada
- El adaptador de red está conectado y no es inalámbrico

Para obtener más información, vea [Pasos de la secuencia de tareas: Comprobar preparación](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness).

### <a name="improvements-to-task-sequence-progress"></a>Mejoras en el progreso de secuencias de tareas

<!-- 5932692 -->

La ventana de progreso de la secuencia de tareas ahora incluye las mejoras siguientes:

- Puede habilitarla para que muestre el número de paso actual, el número total de pasos y el porcentaje completado.
- Se ha aumentado el ancho de la ventana para proporcionar más espacio de modo que se vea mejor el nombre de la organización en una sola línea.

Para obtener más información, vea el artículo [Experiencias de usuario para la implementación de sistemas operativos](../../../osd/understand/user-experience.md#task-sequence-progress).

### <a name="improvements-to-os-deployment"></a>Mejoras en la implementación del sistema operativo

Esta versión incluye las siguientes mejoras en las implementaciones del sistema operativo:

- El entorno de secuencias de tareas incluye una nueva variable de solo lectura, `_TSSecureBoot`.<!--5842295--> Use esta variable para determinar el estado de arranque seguro en un dispositivo habilitado para UEFI. Para obtener más información, consulte la sección [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot).

- Establezca variables de secuencia de tareas para configurar el contexto de usuario para los pasos **Ejecutar línea de comandos** y **Ejecutar script PowerShell**.<!-- 5573175 --> Para obtener más información, vea las secciones sobre las variables [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) y [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser).

- En el paso **Ejecutar script PowerShell**, ahora puede establecer la propiedad **Parámetros** en una variable.<!-- 5690481 --> Para más información, vea [Ejecutar script de PowerShell](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- Ahora, el respondedor PXE de Configuration Manager envía mensajes de estado al servidor de sitio. Este cambio facilita la solución de problemas de las implementaciones de sistemas operativos que usan este servicio.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> Actualizaciones de software

### <a name="orchestration-groups"></a>Grupos de orquestaciones

<!-- 3098816 -->

Cree un grupo de orquestaciones para controlar mejor la implementación de las actualizaciones de software en los dispositivos. Muchos administradores de servidores deben administrar cuidadosamente las actualizaciones de cargas de trabajo específicas y automatizar los comportamientos entre ellas.

Un grupo de orquestaciones ofrece la flexibilidad de actualizar los dispositivos en función de un porcentaje, un número específico o un orden explícito. También puede ejecutar un script de PowerShell antes y después de que los dispositivos ejecuten la implementación de actualización.

Los miembros de un grupo de orquestaciones pueden ser cualquier cliente de Configuration Manager, no solo servidores. Las reglas del grupo de orquestaciones se aplican a los dispositivos de todas las implementaciones de actualizaciones de software en cualquier colección que contenga un miembro del grupo de orquestaciones. Se siguen aplicando otros comportamientos de implementación. Por ejemplo, las ventanas de mantenimiento y las programaciones de implementación.

Para obtener más información, consulte el artículo [Grupos de orquestaciones](../../../sum/deploy-use/orchestration-groups.md).

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>Evaluación de las actualizaciones de software después de una actualización de la pila de servicio

<!-- 4639943 -->

Ahora Configuration Manager detecta si una actualización de la pila de servicio (SSU) forma parte de una instalación de varias actualizaciones. Cuando se detecta una SSU, se instala en primer lugar. Después de instalar la SSU, se ejecuta un ciclo de evaluación de actualizaciones de software para instalar las actualizaciones restantes. Este cambio permite instalar una actualización acumulativa dependiente después de la actualización de la pila de servicio. No es necesario reiniciar el dispositivo entre instalaciones ni tampoco crear una ventana de mantenimiento adicional. Las SSU se instalan en primer lugar solo para instalaciones no iniciadas por el usuario. Por ejemplo, si un usuario inicia una instalación de varias actualizaciones desde el centro de software, es posible que la SSU no se instale primero.

Para obtener más información, vea [Planear actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu).

### <a name="microsoft-365-updates-for-disconnected-software-update-points"></a>Actualizaciones de Microsoft 365 para puntos de actualización de software desconectados

<!-- 4065163 -->

Puede usar una nueva herramienta para importar actualizaciones de Microsoft 365 desde un servidor de WSUS conectado a Internet en un entorno de Configuration Manager desconectado. Anteriormente, cuando exportaba e importaba metadatos de software actualizado en entornos desconectados, no podía implementar actualizaciones de Microsoft 365. Las actualizaciones de Microsoft 365 requieren metadatos adicionales descargados de una API de Office y la red CDN de Office, lo cual no es posible en entornos desconectados.

Para más información, vea [Sincronización de actualizaciones de Microsoft 365 desde un punto de actualización de software desconectado](../../../sum/get-started/synchronize-office-updates-disconnected.md).

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a> Protección

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Expansión de la incorporación de Protección contra amenazas avanzada (ATP) de Microsoft Defender
 
<!-- 5229962 -->
Configuration Manager ha ampliado su compatibilidad con la incorporación de dispositivos a ATP de Microsoft Defender. Para obtener más información, consulte [Protección contra amenazas avanzada de Microsoft Defender (ATP)](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Incorporación de clientes Configuration Manager a ATP de Microsoft Defender a través del Centro de administración de Microsoft Endpoint Manager
<!--5691658-->
Ahora puede implementar directivas de incorporación de respuesta y detección de puntos de conexión de ATP de Microsoft Defender (EDR) en clientes administrados de Configuration Manager. Estos clientes no requieren inscripción en Azure AD o MDM y la directiva está destinada a colecciones de Configuration Manager en lugar de a grupos de Azure AD.

Esta funcionalidad permite a los clientes administrar la incorporación de Intune MDM y del cliente de EDR/ATP de Configuration Manager desde una sola experiencia de administración: el Centro de administración de Microsoft Endpoint Manager. Para obtener más información, consulte [Directiva de detección y respuesta de puntos de conexión para la seguridad de puntos de conexión en Intune](../../../../intune/protect/endpoint-security-edr-policy.md).

> [!Important]
> Necesitará el paquete acumulativo de revisiones, [KB4563473](https://support.microsoft.com/help/4563473), instalado en el entorno para esta característica.

### <a name="improvements-to-bitlocker-management"></a>Mejoras en la administración de BitLocker

- La directiva de administración de BitLocker ahora incluye opciones de configuración adicionales, incluidas directivas para unidades fijas y extraíbles.<!-- 5925683 --> Para obtener más información, vea [Referencia de la configuración de BitLocker](../../../protect/tech-ref/bitlocker/settings.md).

- En la rama actual de Configuration Manager, versión 1910, para integrar el servicio de recuperación de BitLocker se necesita un punto de administración habilitado para HTTPS. La conexión HTTPS es necesaria para cifrar las claves de recuperación en la red desde el cliente de Configuration Manager al punto de administración. La configuración del punto de administración y de todos los clientes para HTTPS puede resultar complicada para muchos clientes.

    A partir de esta versión, el requisito de HTTPS es para el sitio web de IIS que hospeda el servicio de recuperación, no para todo el rol de punto de administración. Este cambio reduce los requisitos de certificado, pero sigue cifrando las claves de recuperación en tránsito.<!-- 5925660 --> Para obtener más información, consulte el artículo [Cifrado de los datos de recuperación](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md).

## <a name="reporting"></a><a name="bkmk_report"></a> Generación de informes

### <a name="integrate-with-power-bi-report-server"></a>Integración con Power BI Report Server

<!-- 3721603 -->

Ahora puede integrar Power BI Report Server con informes de Configuration Manager. Esta integración proporciona una visualización moderna y un mejor rendimiento. Además, la consola admite informes de Power BI de manera similar a como ya ocurre con SQL Server Reporting Services.

Para obtener más información, vea [Integración con Power BI Report Server](../../servers/manage/powerbi-report-server.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Consola de Configuration Manager

### <a name="show-boundary-groups-for-devices"></a>Visualización de los grupos de límites de los dispositivos

<!--6521835-->

Para ayudarle a solucionar mejor los problemas de comportamiento de los dispositivos con grupos de límites, ahora puede ver los grupos de límites de dispositivos específicos. En el nodo **Dispositivos**, o cuando se muestran los miembros de una **Colección de dispositivos**, agregue la nueva columna **Grupos de límites** a la vista de lista.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary).

### <a name="send-a-smile-improvements"></a>Mejoras en la opción Enviar una sonrisa

<!-- 5891852 -->

Al usar las opciones Enviar una sonrisa o Enviar una desaprobación, se crea un mensaje de estado en el momento de enviar los comentarios. Con esta mejora se proporciona un registro de lo siguiente:

- Momento en el que se han enviado los comentarios
- Quién ha enviado los comentarios
- Identificador de los comentarios
- Si los comentarios se han enviado correctamente o no

Los mensajes de estado con el identificador 53900 significan que los comentarios se han enviado correctamente; en cambio, si el identificador es el 53901, significa que no se han podido enviar.

Para obtener más información, vea [Comentarios sobre el producto](../../understand/find-help.md#BKMK_1806Feedback).

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>Búsqueda de elementos de configuración y líneas base de configuración en todas las subcarpetas

<!--5891241-->

De forma similar a las mejoras de versiones anteriores, ahora se puede usar la opción de búsqueda **Todas las subcarpetas** de los nodos **Elementos de configuración** y **Líneas base de configuración**.

### <a name="community-hub"></a>Centro de la comunidad

<!--3555935, 3555936-->

*(Se incorporó por primera vez en junio de 2020)*

La comunidad de administradores de TI ha desarrollado multitud de conocimientos con el paso de los años. En lugar de reinventar elementos como scripts e informes desde cero, hemos creado un **Centro de comunidad** de Configuration Manager donde compartirlos. Al aprovechar el trabajo de los demás, puede ahorrarse horas de trabajo. El Centro de comunidad fomenta la creatividad mediante la creación de otros trabajos y con otras personas que se basan en los suyos. GitHub ya tiene procesos y herramientas en todo el sector diseñados para el uso compartido. Ahora, el Centro de comunidad aprovechará esas herramientas directamente en la consola de Configuration Manager como piezas fundamentales para impulsar esta nueva comunidad. Para la versión inicial, el contenido disponible en el Centro de comunidad solo será cargado por Microsoft.

Para más información, consulte [Centro de comunidad y GitHub](../../servers/manage/community-hub.md).

## <a name="tools"></a><a name="bkmk_tools"></a> Herramientas

### <a name="onetrace-log-groups"></a>Grupos de registros de OneTrace

<!-- 5559993 -->

OneTrace ahora admite grupos de registros personalizables, de forma similar a la característica del Centro de soporte técnico. Los grupos de registros permiten abrir todos los archivos de registro de un único escenario. Actualmente, OneTrace incluye grupos para los siguientes escenarios:

- Administración de aplicaciones
- Configuración de cumplimiento (también llamada Administración de configuración deseada)
- Actualizaciones de software

Para obtener más información, consulte [Centro de soporte técnico OneTrace](../../support/support-center-onetrace.md).

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a> Mejoras para extender y migrar un sitio local a Microsoft Azure
<!--5665775, 6307931-->
La herramienta para extender y migrar un sitio local a Microsoft Azure ahora permite aprovisionar varios roles de sistema de sitio en una sola máquina virtual de Azure. Puede agregar roles de sistema de sitio después de que se haya completado la implementación inicial de la máquina virtual de Azure.

Para más información, vea [Extensión y migración de un sitio local a Microsoft Azure](../../support/azure-migration-tool.md#bkmk_add_role).

## <a name="other-updates"></a>Otras actualizaciones

A partir de esta versión, las características siguientes dejarán de estar en [versión preliminar](../../servers/manage/pre-release-features.md):

- [Detección de grupos de usuarios de Azure Active Directory](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Sincronización de los resultados de pertenencia a recopilaciones con Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [CMPivot independiente](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [Aplicaciones cliente para dispositivos administrados conjuntamente](../../../comanage/workloads.md#client-apps) (antes denominadas *aplicaciones móviles para dispositivos administrados conjuntamente*)<!-- 1357892/3600959 -->

Para obtener más información sobre los cambios en los cmdlets de Windows PowerShell relativos a Configuration Manager, vea las [notas de la versión de PowerShell 2002](/powershell/sccm/2002-release-notes?view=sccm-ps).

Para obtener más información sobre los cambios en la API REST del servicio de administración, consulte las [notas de la versión del servicio de administración](../../../develop/adminservice/release-notes.md#bkmk_2002).

Además de nuevas características, esta versión también incluye cambios adicionales como, por ejemplo, correcciones de errores. Para más información, vea [Resumen de cambios en la rama actual de Configuration Manager, versión 2002](https://support.microsoft.com/help/4556203).

El paquete acumulativo de actualizaciones siguiente (4560496) está disponible en la consola desde el 15 de julio de 2020: [Paquete acumulativo de actualizaciones para Microsoft Endpoint Configuration Manager, versión 2002](https://support.microsoft.com/help/4560496).

### <a name="hotfixes"></a>Revisiones

Se ofrecen estas revisiones adicionales para solucionar problemas específicos:

| Id. | Título | Fecha | En la consola |
|---------|---------|---------|---------|
| [4575339](https://support.microsoft.com/help/4575339) | Los dispositivos aparecen dos veces en el centro de administración de Microsoft Endpoint Configuration Manager. | 23 de julio de 2020 | No |
| [4575774](https://support.microsoft.com/help/4575774) | Error del cmdlet New-CMTSStepPrestartCheck en la versión 2002 de Configuration Manager. | 24 de julio de 2020 | No |
| [4576782](https://support.microsoft.com/help/4576782) | Se agota el tiempo de espera de la hoja de la aplicación en el Centro de administración de Microsoft Endpoint Manager | 11 de agosto de 2020 | No |

<!--
> [!NOTE]
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Pasos siguientes

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

A partir del 11 de mayo de 2020, la versión 2002 está disponible globalmente para que todos los clientes puedan instalarla.

Cuando esté listo para instalar esta versión, vea cómo [instalar actualizaciones para Configuration Manager](../../servers/manage/updates.md) y la [lista de comprobación para la instalación de la actualización 2002](../../servers/manage/checklist-for-installing-update-2002.md).

> [!TIP]
> Para instalar un sitio nuevo, use una versión de línea de base de Configuration Manager.
>
> Más información acerca de:
>
> - [Instalación de nuevos sitios](../../servers/deploy/install/installing-sites.md)
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)

Para conocer los problemas conocidos e importantes, vea las [Notas de la versión](../../servers/deploy/install/release-notes.md).

Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).