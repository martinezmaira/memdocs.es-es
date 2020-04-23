---
title: Referencia de las tareas de mantenimiento
titleSuffix: Configuration Manager
description: Detalles de cada una de las tareas de mantenimiento del sitio de Configuration Manager
ms.date: 03/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9964834bf3a6bfa8e5c0a0bb70039554134490ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708543"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Referencia de las tareas de mantenimiento en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se enumeran los detalles de cada una de las tareas de mantenimiento del sitio de Configuration Manager. Cada entrada especifica los tipos de sitio en los que la tarea está disponible y si está habilitada de forma predeterminada.

Para obtener más información, vea [Configurar tareas de mantenimiento](maintenance-tasks.md#set-up-maintenance-tasks).  

## <a name="tasks"></a>Tareas

### <a name="backup-site-server"></a>Copia de seguridad del servidor del sitio

Use esta tarea para crear una copia de seguridad de su información crítica para restaurar un sitio y la base de datos de Configuration Manager. Para obtener más información, consulte [Hacer una copia de seguridad de un sitio de Configuration Manager](backup-and-recovery.md).  

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|no habilitado.|
|Sitio secundario|No disponible|

### <a name="check-application-title-with-inventory-information"></a>Comprobar título de la aplicación con información de inventario

Utilice esta tarea para mantener la coherencia de los títulos de software entre el inventario de software y el catálogo Asset Intelligence. Para obtener más información, vea [Introducción a Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|Sitio primario|No disponible|
|Sitio secundario|No disponible|

### <a name="clear-undiscovered-clients"></a>Borrar clientes no detectados

> [!Tip]
> También puede ver esta tarea en la consola denominada **Borrar marca de instalación**.

use esta tarea para quitar la marca instalada para los clientes que no envían un registro de detección de latidos durante el período de **nueva detección de cliente**. La marca instalada evita la instalación de inserción automática de clientes en un equipo que puede tener un cliente de Configuration Manager activo.  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|no habilitado.|
|Sitio secundario|No disponible|

### <a name="delete-aged-application-request-data"></a>Eliminar datos antiguos de solicitud de la aplicación

utilice esta tarea para eliminar solicitudes antiguas de la aplicación de la base de datos. Para más información, vea [Crear e implementar una aplicación](../../../apps/get-started/create-and-deploy-an-application.md).  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-application-revisions"></a>Eliminar revisiones antiguas de la aplicación

utilice esta tarea para eliminar revisiones de la aplicación a las que ya no se hace referencia. Para obtener más información, vea [Revisar y sustituir aplicaciones](../../../apps/deploy-use/revise-and-supersede-applications.md).

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-client-download-history"></a>Eliminar historial de descargas de cliente antiguas

use esta tarea para eliminar datos históricos sobre el origen de descarga que usan los clientes. La información del origen de descarga se utiliza para rellenar el [panel Orígenes de datos de cliente](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-client-operations"></a>Eliminar operaciones cliente antiguas

Use esta tarea para eliminar de la base de datos del sitio todos los datos antiguos de las operaciones de cliente. Por ejemplo, estos datos incluyen las siguientes operaciones:

- Notificaciones de cliente vencidas o expiradas, como las solicitudes de descarga de la directiva de equipo o usuario.
- Endpoint Protection, como solicitudes realizadas por un usuario administrativo para que los clientes ejecuten un examen o descarguen definiciones actualizadas.

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-client-presence-history"></a>Historial de presencias de cliente vencidas eliminado
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
Use esta tarea para eliminar la información de historial sobre el estado en línea de los clientes registrado por la notificación del cliente. Elimina la información de los clientes con un estado anterior a la hora especificada. Para obtener más información, vea [Cómo supervisar clientes](../../clients/manage/monitor-clients.md).

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>Eliminar datos antiguos del tráfico de Cloud Management Gateway

Use esta tarea para eliminar de la base de datos del sitio todos los datos antiguos sobre el tráfico que atraviesa [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md). Estos datos incluyen:

- El número de solicitudes
- Bytes de solicitudes totales
- Bytes de respuesta totales
- Número de solicitudes con errores
- Número máximo de solicitudes simultáneas

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-cmpivot-results"></a>Eliminar resultados antiguos de CMPivot

Utilice esta tarea para eliminar de la base de datos del sitio información antigua de los clientes en consultas de CMPivot. Para obtener más información, vea [CMPivot para datos en tiempo real](cmpivot.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-collected-files"></a>Eliminar archivos recopilados antiguos

Utilice esta tarea para eliminar de la base de datos la información antigua acerca de los archivos recopilados. Esta tarea también elimina los archivos recopilados desde la estructura de carpetas del servidor de sitio en el sitio seleccionado. De forma predeterminada, las cinco copias más recientes de los archivos recopilados se almacenan en el servidor de sitio en el directorio de **Inboxes\sinv.box\FileCol**. Para obtener más información, vea [Introducción al inventario de software](../../clients/manage/inventory/introduction-to-software-inventory.md).  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-computer-association-data"></a>Eliminar datos antiguos de asociación de equipos

Utilice esta tarea para eliminar de la base de datos los datos antiguos de asociación de equipos de implementación de sistema operativo. Esta información se usa al restaurar el estado de usuario durante una secuencia de tareas. Para obtener más información, consulte [Manage user state](../../../osd/get-started/manage-user-state.md) (Administrar el estado de usuario).  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-console-connection-data"></a>Eliminar datos de conexión de consola antiguos

Esta tarea elimina datos de la base de datos del sitio acerca de las conexiones de la consola al sitio.<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-delete-detection-data"></a>Eliminar datos antiguos de detección de eliminación

Utilice esta tarea para eliminar datos antiguos de la base de datos creada en las vistas de extracción. Elimina la información de cambios de datos antiguos utilizada por sistemas externos que extraen datos de la base de datos.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-device-wipe-record"></a>Eliminar registro antiguo de borrado de dispositivo

Utilice esta tarea para eliminar de la base de datos los datos antiguos acerca de las acciones de borrado del dispositivo móvil. Para obtener más información, consulte [Protección de los datos con borrado, bloqueo o restablecimiento de contraseña de forma remota](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-discovery-data"></a>Eliminar datos de detección antiguos

utilice esta tarea para eliminar datos de detección antiguos de la base de datos. Estos datos pueden incluir registros de:

- Detección de latidos
- Detección de red
- Métodos de detección de Active Directory: sistema, usuario y grupo

Esta tarea también quita los dispositivos antiguos marcados como retirados. Cuando se ejecuta esta tarea en un sitio, se eliminan los datos asociados a ese sitio, y esos cambios se replican a otros sitios. Para obtener más información, vea [Ejecutar la detección](../deploy/configure/run-discovery.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-distribution-point-usage-stats"></a>Eliminar estadísticas antiguas de uso de punto de distribución

use esta tarea para eliminar de la base de datos los datos vencidos de puntos de distribución que lleven almacenados más tiempo del especificado.  

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-enrolled-devices"></a>Eliminar dispositivos inscritos antiguos

Use esta tarea para eliminar de la base de datos del sitio los datos antiguos sobre dispositivos móviles que no han enviado información al sitio durante un tiempo especificado.

Esta tarea se aplica a los dispositivos que están inscritos con [MDM local](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) de Configuration Manager. Para obtener más información sobre estos dispositivos, vea [Sistemas operativos compatibles con clientes y dispositivos](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|no habilitado.|
|Sitio secundario|No disponible|

### <a name="delete-aged-ep-health-status-history-data"></a>Eliminar datos antiguos del historial de estado de mantenimiento de EP

Utilice esta tarea para eliminar de la base de datos información de estado antigua de Endpoint Protection (EP). Para más información, vea [Cómo supervisar el estado de Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-exchange-partnership"></a>Eliminar asociación de Exchange vencida

> [!Tip]
> > También puede ver esta tarea en la consola denominada **Eliminar dispositivos antiguos administrados por el conector de Exchange Server**.

Utilice esta tarea para eliminar datos antiguos acerca de los dispositivos móviles administrados por el conector de Exchange Server. Este sitio elimina estos datos de acuerdo con el parámetro **Omitir dispositivos móviles que hayan estado inactivos durante más de (días)** en la pestaña **Detección** de las propiedades del conector de Exchange Server. Para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-inventory-history"></a>Eliminar historial de inventario antiguo

Utilice esta tarea para eliminar de la base de datos los datos de inventario almacenados durante más tiempo del especificado. Para obtener más información, vea [Cómo usar el Explorador de recursos para ver el inventario de hardware](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-log-data"></a>Eliminar datos de registro antiguos

Utilice esta tarea para eliminar de la base de datos los datos de registro antiguos utilizados para solucionar problemas. Estos datos no están relacionados con las operaciones de componentes de Configuration Manager.  

> [!IMPORTANT]  
> De forma predeterminada, esta tarea se ejecuta a diario en cada sitio. En un sitio de administración central y en sitios primarios, la tarea elimina los datos más antiguos de 30 días. Al usar SQL Server Express en un sitio secundario, asegúrese de que esta tarea se ejecute todos los días y que elimine los datos que hayan estado inactivos durante siete días.  

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|**Sitio secundario**|Habilitado|

### <a name="delete-aged-metering-data"></a>Eliminar los datos obsoletos de mediciones

Utilice esta tarea para eliminar de la base de datos los datos antiguos acerca de la disponibilidad de software almacenados durante más tiempo del especificado. Para obtener más información, vea [Medición de software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-metering-summary-data"></a>Eliminar los datos obsoletos de resumen de mediciones

Utilice esta tarea para eliminar de la base de datos los datos antiguos de resumen para la medición de software almacenados durante más tiempo del especificado. Para obtener más información, vea [Medición de software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-notification-server-history"></a>Eliminar historial antiguo del servidor de notificaciones

Esta tarea elimina el historial de presencias de cliente vencidas.

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-notification-task-history"></a>Eliminar historial de tareas de notificación vencidas

Utilice esta tarea para eliminar de la base de datos del sitio la información acerca de las tareas de notificación del cliente. Esta tarea se aplica a los datos que no se han actualizado durante un período de tiempo especificado. Para obtener más información, vea [Notificación de cliente](../../clients/manage/client-notification.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-passcode-records"></a>Eliminar registros de códigos de accesos antiguos

Use esta tarea en el sitio de primer nivel de la jerarquía para eliminar datos antiguos sobre restablecimientos de códigos de acceso para dispositivos Windows Phone. Los datos de restablecimiento de código de acceso están cifrados, pero contienen el PIN para dispositivos. De forma predeterminada, esta tarea está habilitada y elimina los datos anteriores a un día.  

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-replication-data"></a>Eliminar datos de replicación vencidos

Use esta tarea para eliminar de la base de datos los datos antiguos sobre la replicación de base de datos entre los sitios de Configuration Manager. Si cambia la configuración de esta tarea de mantenimiento, la configuración se aplica a todos los sitios aplicables en la jerarquía. Para obtener más información, consulte [Supervisión de la replicación de la base de datos](monitor-replication.md).  

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|**Sitio secundario**|Habilitado|

### <a name="delete-aged-replication-summary-data"></a>Eliminar datos de resumen de replicación vencidos

Use esta tarea para eliminar de la base de datos del sitio los datos de resumen de replicación antiguos cuando no se hayan actualizado durante un período de tiempo especificado. Para obtener más información, consulte [Supervisión de la replicación de la base de datos](monitor-replication.md).  

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|**Sitio secundario**|Habilitado|

### <a name="delete-aged-status-messages"></a>Eliminar mensajes de estado antiguos

Utilice esta tarea para eliminar de la base de datos los datos de mensajes de estado antiguos, tal como se configuraron en las reglas de filtro de estado. Para obtener información, consulte [Supervisar el sistema de estado de Configuration Manager](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus).

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-threat-data"></a>Eliminar datos de amenaza antiguos

Utilice esta tarea para eliminar de la base de datos los datos de amenaza antiguos de Endpoint Protection almacenados durante más tiempo del especificado. Para obtener más información, vea [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-unknown-computers"></a>Eliminar equipos desconocidos vencidos

use esta tarea para eliminar información sobre equipos desconocidos de la base de datos del sitio cuando no se ha actualizado durante un período de tiempo especificado. Para obtener más información, consulte [Prepare for unknown computer deployments](../../../osd/get-started/prepare-for-unknown-computer-deployments.md) (Preparación para implementaciones en equipos desconocidos).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-aged-user-device-affinity-data"></a>Eliminar datos antiguos de afinidad de dispositivo del usuario

utilice esta tarea para eliminar datos antiguos de afinidad de dispositivo del usuario de la base de datos. Para obtener más información, vea [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-duplicate-system-discovery-data"></a>Eliminar datos de detección del sistema duplicados

Utilice esta tarea para eliminar de la base de datos del sitio los registros duplicados generados por la detección del sistema.<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|Sitio primario|No disponible|
|Sitio secundario|No disponible|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>Eliminar los registros expirados del paquete de inscripciones MDM en masa

use esta tarea para eliminar certificados antiguos de inscripción masiva y los perfiles correspondientes después de que caduque el certificado de inscripción. Para más información, vea [Crear perfiles de certificado](../../../protect/deploy-use/create-certificate-profiles.md).

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-inactive-client-discovery-data"></a>Eliminar datos de detección de cliente inactivos

Utilice esta tarea para eliminar de la base de datos los datos de detección para clientes inactivos. El sitio marca los clientes como inactivos cuando el cliente se marca como obsoleto y por medio de las configuraciones realizadas para el estado de cliente.

Esta tarea solo funciona en los recursos que son clientes de Configuration Manager. Es diferente de la tarea **Eliminar datos de detección antiguos**, que elimina los registros de datos de detección antiguos. Cuando esta tarea se ejecuta en un sitio, quita los datos de la base de datos en todos los sitios de la jerarquía. Para obtener más información, vea [Cómo configurar el estado de cliente](../../clients/deploy/configure-client-status.md).

> [!IMPORTANT]  
> Si está habilitada, configure esta tarea para que se ejecute con un intervalo mayor que la programación de **detección de latidos**. Esta configuración permite que los clientes activos envíen un registro de detección de latidos para marcar su registro de clientes como activo para que esta tarea no los elimine.  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|no habilitado.|
|Sitio secundario|No disponible|

### <a name="delete-obsolete-alerts"></a>Eliminar alertas obsoletas

Utilice esta tarea para eliminar de la base de datos alertas expiradas almacenadas durante más tiempo del especificado. Para obtener más información, consulte [Usar alertas y el sistema de estado](use-alerts-and-the-status-system.md).

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-obsolete-client-discovery-data"></a>Eliminar datos obsoletos de detección de cliente

utilice esta tarea para eliminar registros de cliente obsoletos de la base de datos. Por lo general, un registro marcado como obsoleto suele reemplazarse por registro más reciente para el mismo cliente. El registro más reciente se convierte en el registro actual del cliente. Para obtener información acerca la detección, consulte [Ejecutar la detección](../deploy/configure/run-discovery.md).

> [!IMPORTANT]  
> Si está habilitada, configure esta tarea para que se ejecute con un intervalo mayor que la programación de detección de latidos. Esta configuración permite al cliente enviar un registro de detección de latidos que establece correctamente el estado obsoleto.  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|no habilitado.|
|Sitio secundario|No disponible|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>Eliminar sitios y subredes obsoletos de detección de bosque

Utilice esta tarea para eliminar datos sobre sitios, subredes y dominios de Active Directory. Quita los datos que el sitio no ha detectado con el método de detección de bosques de Active Directory en los últimos 30 días. Esta tarea elimina los datos de detección, pero no afecta a los límites creados desde estos datos de detección. Para obtener más información, vea [Ejecutar la detección](../deploy/configure/run-discovery.md).

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="delete-orphaned-client-deployment-state-records"></a>Eliminar registros del estado de la implementación del cliente huérfano

use esta tarea para purgar periódicamente la tabla que contiene información de estado de implementación de cliente. Esta tarea limpia los registros asociados con dispositivos obsoletos o retirados.  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="evaluate-collection-members"></a>Evaluar miembros de la recopilación

puede configurar la evaluación de pertenencia a recopilación como componente del sitio. Para obtener más información, vea [Componentes de sitio](../deploy/configure/site-components.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="monitor-keys"></a>Supervisar claves

use esta tarea para supervisar la integridad de las claves principales de la base de datos de Configuration Manager. Una clave principal es una columna o una combinación de columnas que identifica de forma única una fila. La clave distingue la fila de cualquier otra fila de una tabla de base de datos de Microsoft SQL Server.

|||
|---------|---------|
|**Sitio de administración central**|Habilitado|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="rebuild-indexes"></a>Recompilar índices

use esta tarea para recompilar los índices de la base de datos de Configuration Manager. Un índice es una estructura de base de datos que se crea en una tabla de base de datos para acelerar la recuperación de datos. Por ejemplo, buscar en una columna indexada suele ser mucho más rápido que buscar en una columna no indexada.

Para mejorar el rendimiento, los índices de la base de datos de Configuration Manager se actualizan con frecuencia para permanecer sincronizados con los datos que se almacenan en la base de datos y que cambian continuamente. Esta tarea:

- Crea índices en columnas de base de datos con una exclusividad de al menos el 50 %.
- Quita los índices de las columnas que tienen una exclusividad inferior al 50 %.
- Recompila todos los índices existentes que cumplen los criterios de exclusividad de los datos.

|||
|---------|---------|
|**Sitio de administración central**|no habilitado.|
|**Sitio primario**|no habilitado.|
|**Sitio secundario**|no habilitado.|

### <a name="summarize-file-usage-metering-data"></a>Resumir datos de medición de uso de archivos

utilice esta tarea para resumir los datos de varios registros de uso de archivos de disponibilidad de software en un único registro general. El resumen de datos puede comprimir los datos almacenados en la base de datos de Configuration Manager.

Para resumir los datos de medición de software y conservar espacio en disco en la base de datos, use esta tarea con la tarea **Resumir datos de uso mensual de disponibilidad de software**. Para obtener más información, vea [Medición de software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="summarize-installed-software-data"></a>Resumir datos de software instalado

Utilice esta tarea para resumir los datos de la información de software de Asset Intelligence recopilada a través del inventario de hardware para combinar varios registros en un solo registro general. El resumen de datos puede comprimir los datos almacenados en la base de datos de Configuration Manager. Para obtener más información, consulte [Configurar tareas de mantenimiento de Asset Intelligence](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="summarize-monthly-usage-metering-data"></a>Resumir mensualmente los datos de medición de uso

utilice esta tarea para resumir los datos de varios registros de uso mensual de disponibilidad de software en un único registro general. El resumen de datos puede comprimir los datos almacenados en la base de datos de Configuration Manager.

Para resumir los datos de medición de software y conservar espacio en disco en la base de datos, use esta tarea con la tarea **Resumir datos de uso de archivo de disponibilidad de software**. Para obtener más información, vea [Medición de software](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="update-application-available-targeting"></a>Actualizar destinatarios disponibles de la aplicación

use esta tarea para que Configuration Manager actualice la asignación de las implementaciones de directiva y aplicación a los recursos en colecciones. Al implementar directivas o aplicaciones en una colección, Configuration Manager crea una asignación inicial entre los objetos que implemente y los miembros de la recopilación.

Estas asignaciones se almacenan en una tabla para una referencia rápida. Cuando cambia la pertenencia a colecciones, el sitio actualiza estas asignaciones almacenadas para reflejar estos cambios. En cambio, es posible que estas asignaciones no se sincronicen. Por ejemplo, si el sitio no puede procesar correctamente un archivo de notificación, es posible que ese cambio no se refleje en un cambio en las asignaciones. Esta tarea actualiza esa asignación según la pertenencia a la colección actual.  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|

### <a name="update-application-catalog-tables"></a>Actualizar tablas del catálogo de aplicaciones

utilice esta tarea para sincronizar la memoria caché de la base de datos del sitio web del catálogo de aplicaciones con la información más reciente de la aplicación. Si cambia la configuración de esta tarea de mantenimiento, se aplica a todos los sitios primarios en la jerarquía.  

|||
|---------|---------|
|Sitio de administración central|No disponible|
|**Sitio primario**|Habilitado|
|Sitio secundario|No disponible|


## <a name="see-also"></a>Vea también

[Tareas de mantenimiento](maintenance-tasks.md)
