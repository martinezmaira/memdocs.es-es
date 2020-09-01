---
title: Novedades de la versión 1906
titleSuffix: Configuration Manager
description: Obtenga detalles sobre los cambios y las nuevas funcionalidades incorporados en la versión 1906 de la rama actual de Configuration Manager.
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3736e5343e10bdfc8d5be8abf79ee27e46749834
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995116"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Novedades de la versión 1906 de la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 1906 de la rama actual de Configuration Manager está disponible como una actualización en consola. Aplique esta actualización a los sitios que ejecuten la versión 1802 o versiones posteriores. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> En este artículo se resumen los cambios y las nuevas características de Configuration Manager, versión 1906.  

Revise siempre la lista de comprobación más reciente para instalar esta actualización. Para más información, consulte [Lista de comprobación para la instalación de la actualización 1906](../../servers/manage/checklist-for-installing-update-1906.md). Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).

Para aprovechar al máximo las nuevas características de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

> [!Tip]  
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>Cambios en los requisitos

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>El cliente de la versión 1906 requiere compatibilidad con la firma de código SHA-2

<!--SCCMDocs-pr#3404-->
Debido a la vulnerabilidad del algoritmo SHA-1 y para estar en línea con los estándares del sector, Microsoft ahora solo firma archivos binarios de Configuration Manager con el algoritmo SHA-2, que es más seguro. Estas versiones del sistema operativo Windows requieren una actualización para admitir la firma de código SHA-2:

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

Para más información, consulte [Requisitos previos para los clientes de Windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2).


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infraestructura del sitio

### <a name="site-server-maintenance-task-improvements"></a>Mejoras en las tareas de mantenimiento del servidor de sitio

<!--3555894-->
Ahora las tareas de mantenimiento del servidor de sitio se pueden ver y editar desde su propia pestaña en la vista de detalles de un servidor de sitio. En la nueva pestaña **Tareas de mantenimiento** se proporciona la información siguiente:

- Si la tarea está habilitada
- La programación de la tarea
- La última hora de inicio
- La última hora de finalización
- Si la tarea se ha completado correctamente

![Nueva pestaña para tareas de mantenimiento en la vista de detalles de un servidor de sitio](./media/3555894-maintenance-tasks.png)

Para obtener más información, vea [Tareas de mantenimiento](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906).

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Supervisión de la actualización de base de datos de actualización de Configuration Manager

<!--4200581-->
Ahora, al aplicar una actualización de Configuration Manager, puede ver el estado de la tarea **Actualizar base de datos de Configuration Manager** en la ventana de estado de la instalación.

- Si se bloquea la actualización de la base de datos, se le proporcionará la advertencia **En curso, requiere atención**.
   - En cmupdate.log se registrará el nombre del programa y el identificador de sesión de SQL que bloquea la actualización de la base de datos.
- Cuando la actualización de la base de datos deje de estar bloqueada, el estado se restablecerá a **En curso** o **Completado**.
   - Cuando la actualización de la base de datos está bloqueada, se realiza una comprobación cada cinco minutos para ver el bloqueo persiste.

   ![Supervisión de la actualización de la base de datos durante la instalación](./media/4200581-database-upgrade-monitoring.png)

Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install).

### <a name="management-insights-rule-for-ntlm-fallback"></a>Regla de Información de administración para la reserva de NTLM

<!--4572953-->
Información de administración incluye una nueva regla que detecta si ha habilitado el método de reserva de autenticación de NTLM menos seguro para el sitio: **La reserva de NTLM está habilitada**.

Para obtener más información, vea [Información de administración](../../servers/manage/management-insights.md#security).

### <a name="improvements-to-support-for-sql-always-on"></a>Mejoras en la compatibilidad con Always On de SQL

- Agregue una réplica sincrónica nueva desde la configuración<!--3127336-->: ahora puede agregar un nuevo nodo de réplica secundaria a un grupo de disponibilidad AlwaysOn de SQL existente. En lugar de un proceso manual, use el programa de instalación de Configuration Manager para realizar este cambio. Para más información, consulte [Configuración de grupos de disponibilidad AlwaysOn de SQL Server](../../servers/deploy/configure/configure-aoag.md#bkmk_sync).

- Conmutación por error de múltiples subredes<!-- SCCMDocs-pr#3734 -->: Ahora puede habilitar la [palabra clave MultiSubnetFailover y características asociadas](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) en SQL Server. También debe configurar manualmente el servidor de sitio. Para más información, consulte el requisito previo de [conmutación por error de múltiples subredes](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover).

- Compatibilidad con vistas distribuidas<!-- SCCMDocs-pr#3792 -->: la base de datos del sitio se puede hospeda en un grupo de disponibilidad AlwaysOn de SQL Server y es posible habilitar vínculos de replicación de base de datos para usar las [vistas distribuidas](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep).

    > [!Note]  
    > Este cambio no se aplica a los clústeres de SQL Server.

- La recuperación del sitio puede volver a crear la base de datos en un grupo Always On de SQL. Este proceso funciona tanto con la inicialización manual como la automática.<!-- SCCMDocs-pr#3846 -->

- Comprobaciones de los requisitos previos para una instalación nueva:<!-- SCCMDocs-pr#3899 -->  

    - Todos los grupos de disponibilidad SQL deben tener el mismo modo de inicialización.
    - Las réplicas del grupo de disponibilidad de SQL deben estar en buen estado.

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Administración conectada a la nube

### <a name="azure-active-directory-user-group-discovery"></a>Detección de grupos de usuarios de Azure Active Directory

<!--3611956-->

Ahora puede descubrir grupos de usuarios y miembros de esos grupos desde Azure Active Directory (Azure AD). Los usuarios que se encuentran en los grupos de Azure AD que el sitio no haya detectado anteriormente se agregan como recursos de usuario en Configuration Manager. Cuando el grupo es un grupo de seguridad, se crea un registro de recurso de grupo de usuarios. Esta es una [característica de versión preliminar](../../servers/manage/pre-release-features.md) y debe estar habilitada.

Para más información, consulte [Configurar métodos de detección](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco).

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>Sincronización de los resultados de pertenencia a recopilaciones con grupos de Azure Active Directory

<!--3607475-->

Ahora puede habilitar la sincronización de las pertenencias a recopilaciones con un grupo de Azure Active Directory (Azure AD). Esta sincronización es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](../../servers/manage/pre-release-features.md).

La sincronización permite usar las reglas de agrupación locales existentes en la nube mediante la creación de pertenencias a grupos de Azure AD en función de los resultados de la pertenencia a recopilaciones. Solo los dispositivos con un registro de Azure Active Directory se reflejan en el grupo de Azure AD. Se admiten tanto los dispositivos unidos a Azure Active Directory como los unidos a Azure HD híbrido.

Para más información, vea [Create collections](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) (Crear recopilaciones).


## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Análisis de escritorio

### <a name="readiness-insights-for-desktop-apps"></a>Información sobre la preparación de aplicaciones de escritorio

<!-- 4021225 -->

Ahora puede obtener información más detallada para las aplicaciones de escritorio, incluidas las aplicaciones de línea de negocio. El anterior kit de herramientas de App Health Analyzer ahora está integrado con el cliente de Configuration Manager. Esta integración simplifica la implementación y la capacidad de administración de la información sobre preparación de las aplicaciones en el portal de Análisis de escritorio.

Para más información, consulte [Evaluación de compatibilidad en el Análisis de escritorio](../../../desktop-analytics/compat-assessment.md#advanced-insights).


### <a name="dalogscollector-tool"></a>Herramienta DALogsCollector

<!--4622989-->
Use la herramienta DesktopAnalyticsLogsCollector.ps1 desde el directorio de instalación de Configuration Manager para ayudar a solucionar problemas con Análisis de escritorio. Ejecuta algunos pasos básicos para solucionar problemas y recopila los registros pertinentes en un solo directorio de trabajo.

Para más información, consulte [Recopilador de registros](../../../desktop-analytics/log-collector.md).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Administración en tiempo real

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>Incorporación de combinaciones, operadores adicionales y agregadores en CMPivot

<!--4054074-->

Para CMPivot, ahora tiene más operadores aritméticos, agregadores y la posibilidad de agregar combinaciones de consulta como el uso conjunto de Registro y Archivo.

Para obtener más información, vea [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1906).

### <a name="cmpivot-standalone"></a>CMPivot independiente

<!--3555890, 4619340, 4692885 -->

Ahora puede usar CMPivot como una aplicación independiente. CMPivot independiente es una **característica de versión preliminar** y solo está disponible en inglés. Ejecútelo fuera de la consola de Configuration Manager para ver el estado en tiempo real de los dispositivos en su entorno. Este cambio le permite usar CMPivot en un dispositivo sin instalar primero la consola.

Puede compartir la eficacia de CMPivot con otras personas, como administradores del departamento de soporte técnico o seguridad, que no tienen la consola instalada en su equipo. Estas otras personas pueden usar CMPivot para consultar Configuration Manager junto con las otras herramientas que usan tradicionalmente. Al compartir estos datos de administración enriquecidos, pueden trabajar juntos para resolver proactivamente los problemas empresariales de los roles.

Para más información, consulte [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) y [Características de versión preliminar](../../servers/manage/pre-release-features.md#bkmk_table).

### <a name="added-permissions-to-the-security-administrator-role"></a>Permisos agregados al rol Administrador de seguridad

<!--4683130-->

Se han agregado los permisos siguientes al rol [**Administrador de seguridad**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) integrado de Configuration Manager:

- Lectura en script SMS
- Ejecución de CMPivot en colección
- Lectura en Informe de inventario

Para obtener más información, vea [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot_secadmin1906).


## <a name="content-management"></a><a name="bkmk_content"></a> Administración de contenido

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>Datos de descarga de la Optimización de entrega en el panel de orígenes de datos de cliente

<!--3555759-->
Ahora el panel de orígenes de datos de cliente incluye datos de [Optimización de entrega](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). Este panel ayuda a comprender desde dónde obtienen el contenido los clientes en el entorno.

Para más información, consulte [Panel de orígenes de datos de cliente](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>Uso del punto de distribución como servidor de caché en la red para la optimización de entrega

<!--3555764-->
Ya puede instalar el servidor de caché en la red de Optimización de distribución en los puntos de distribución. Al almacenar en caché este contenido de forma local, los clientes pueden beneficiarse de la característica de Optimización de entrega y, además, puede ayudar a proteger los vínculos WAN.

Este servidor de caché actúa como una caché transparente a petición para el contenido descargado mediante la Optimización de entrega. Use la configuración de cliente para asegurarse de que este servidor se ofrezca únicamente a los miembros del grupo de límites de Configuration Manager local.

Para más información, consulte el artículo sobre la [caché en la red de optimización de entrega en Configuration Manager](../hierarchy/microsoft-connected-cache.md).


## <a name="client-management"></a><a name="bkmk_client"></a> Administración de clientes

### <a name="support-for-windows-virtual-desktop"></a>Compatibilidad con Windows Virtual Desktop

<!--3556025-->
[Windows Virtual Desktop](/azure/virtual-desktop/) es una característica en versión preliminar de Microsoft Azure y Microsoft 365. Ahora puede usar Configuration Manager para administrar estos dispositivos virtuales que ejecutan Windows en Azure.

Al igual que un servidor de terminal, estos dispositivos virtuales permiten varias sesiones de usuario activas simultáneas. Para facilitar el rendimiento del cliente, ahora en Configuration Manager se deshabilitan las directivas de usuario en todos los dispositivos que admiten estas sesiones de usuario múltiples. Aunque habilite las directivas de usuario, el cliente las deshabilita de forma predeterminada en estos dispositivos, que incluyen Windows Virtual Desktop y servidores de terminal.

Para más información, consulte [Versiones de sistemas operativos compatibles para clientes y dispositivos](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers).

### <a name="support-center-onetrace-preview"></a>Centro de soporte técnico OneTrace (versión preliminar)

<!--3555962-->
OneTrace es un nuevo visor de registros del Centro de soporte técnico. Funciona de forma similar a CMTrace, con las mejoras siguientes:

- Una vista con pestañas.
- Ventanas acoplables.
- Funciones de búsqueda mejoradas.
- Capacidad de habilitar filtros sin salir de la vista del registro.
- Sugerencias de la barra de desplazamiento para identificar rápidamente clústeres de errores.
- Apertura de registro rápida para archivos de gran tamaño

![Captura de pantalla del visor de registros OneTrace](./media/3555962-onetrace.png)

Para más información, consulte [Centro de soporte técnico OneTrace](../../support/support-center-onetrace.md).

### <a name="configure-client-cache-minimum-retention-period"></a>Configuración del período de retención mínimo de caché de cliente

<!--4485509-->
Ahora puede especificar el tiempo mínimo que el cliente de Configuration Manager mantendrá el contenido almacenado en caché. Esta configuración de cliente define el tiempo mínimo que el agente de Configuration Manager debe esperar para quitar contenido de la memoria caché en caso de que se necesite más espacio. En el grupo **Configuración de caché de cliente** de la configuración cliente, establezca la opción siguiente: **Minimum duration before cached content can be removed (minutes)** (Duración mínima antes de que se pueda quitar contenido almacenado en caché (minutos)).

> [!Note]  
> En el mismo grupo de configuración de cliente, la opción existente para **Habilitar el cliente de Configuration Manager en el SO completo para compartir contenido** ahora se denomina **Habilitar como origen de caché del mismo nivel**. El comportamiento de la configuración no cambia.  

Para obtener más información, vea [Configuración de la memoria caché del cliente](../../clients/deploy/about-client-settings.md#client-cache-settings).


## <a name="co-management"></a><a name="bkmk_comgmt"></a> Administración conjunta

### <a name="improvements-to-co-management-auto-enrollment"></a>Mejoras en la inscripción automática de la administración conjunta

- Un nuevo dispositivo administrado de forma conjunta ahora se inscribe automáticamente en el servicio Microsoft Intune en función de su token de *dispositivo* de Azure Active Directory (Azure AD). No es necesario esperar a que un usuario inicie sesión en el dispositivo para iniciar la inscripción automática. Este cambio ayuda a reducir el número de dispositivos con el [estado de inscripción](../../../comanage/how-to-monitor.md#co-management-enrollment-status) *Inicio de sesión de usuario pendiente*.<!-- 4454491 -->

- Para clientes que ya tienen dispositivos inscritos en la administración conjunta, los dispositivos nuevos ahora se inscriben de manera inmediata una vez que cumplen con los requisitos previos. Por ejemplo, una vez que el dispositivo se une a Azure AD y que se instala el cliente de Configuration Manager.<!--4321130-->

Para más información, consulte [Habilitación de la administración conjunta](../../../comanage/how-to-enable.md).

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>Varios grupos piloto para las cargas de trabajo de administración conjunta

<!--3555750-->
Ahora puede configurar diferentes colecciones piloto para cada una de las cargas de trabajo de administración conjunta. Usar diferentes colecciones piloto permite adoptar un enfoque más específico al cambiar las cargas de trabajo.

- En la pestaña **Habilitación**, ahora puede especificar una colección **Inscripción automática de Intune**.
    - La colección **Inscripción automática de Intune** debe contener todos los clientes que quiera incorporar a la administración conjunta. En esencia, se trata de un superconjunto de todas las demás colecciones de almacenamiento provisional.

- En la pestaña **Almacenamiento provisional**, en lugar de usar una colección piloto para todas las cargas de trabajo, ahora puede elegir una colección individual para cada carga de trabajo.

    ![La pestaña Almacenamiento provisional de Administración conjunta permite elegir una colección para cada carga de trabajo](./media/3555750-co-management-staging-tab.png)

Estas opciones también están disponibles cuando se habilita la administración conjunta por primera vez.

Para más información, consulte [Habilitación de la administración conjunta](../../../comanage/how-to-enable.md).

### <a name="co-management-support-for-government-cloud"></a>Compatibilidad con la administración para la nube de administración pública.

<!--4075452-->
Los clientes del gobierno de EE. UU. ahora pueden usar la administración conjunta con la nube de administración pública de EE. UU. (portal.azure.us). Para más información, consulte [Habilitación de la administración conjunta](../../../comanage/how-to-enable.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Administración de aplicaciones

### <a name="filter-applications-deployed-to-devices"></a>Filtrado de aplicaciones implementadas en dispositivos

<!--4451056-->
Las categorías de usuario para las implementaciones de aplicaciones dirigidas al dispositivo ahora se muestran como filtros en el Centro de software. Especifique una **categoría usuario** para una aplicación en la página **Centro de software** de sus propiedades. Después, abra la aplicación en el Centro de software y examine los filtros disponibles.

Para más información, vea [Especificar manualmente la información de la aplicación](../../../apps/deploy-use/create-applications.md#bkmk_manual-app).

### <a name="application-groups"></a>Grupos de aplicaciones

<!--3555907-->
Cree un grupo de aplicaciones que puede enviar a una colección de usuarios o dispositivos como una sola implementación. Los metadatos que especifique sobre el grupo de aplicaciones se ven en el Centro de software como una sola entidad. Puede ordenar las aplicaciones en el grupo para que el cliente las instale en un orden específico.

Es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](../../servers/manage/pre-release-features.md).

Para más información, consulte [Crear grupos de aplicaciones](../../../apps/deploy-use/create-app-groups.md).

### <a name="retry-the-install-of-pre-approved-applications"></a>Reintento de la instalación de aplicaciones aprobadas previamente

<!--4336307-->
Ahora puede volver a intentar la instalación de una aplicación que haya aprobado previamente para un usuario o dispositivo. La opción de aprobación es solo para las implementaciones disponibles. Si el usuario desinstala la aplicación, o si se produce un error en el proceso de instalación inicial, Configuration Manager no vuelve a evaluar su estado y reinstalarla. Esta característica permite que un técnico de soporte técnico intente volver a instalar la aplicación rápidamente para un usuario que llame para obtener ayuda.

Para obtener más información, vea [Aprobar aplicaciones](../../../apps/deploy-use/app-approval.md).

### <a name="install-an-application-for-a-device"></a>Instalación de una aplicación para un dispositivo

<!--4402180-->
Desde la consola de Configuration Manager, ahora puede instalar aplicaciones en un dispositivo en tiempo real. Esta característica puede ayudar a reducir la necesidad de colecciones independientes para cada aplicación.

Para más información, consulte [Instalación de aplicaciones para un dispositivo](../../../apps/deploy-use/install-app-for-device.md).

### <a name="improvements-to-app-approvals"></a>Mejoras en las aprobaciones de aplicaciones

<!--4224910-->
En esta versión se incluyen las mejoras siguientes en las aprobaciones de aplicaciones:

- Si aprueba una solicitud de aplicación en la consola y después la deniega, ahora la puede volver a aprobar. Después de que apruebe la aplicación, se vuelve a instalar en el cliente.  

- En la consola de Configuration Manager, área de trabajo **Biblioteca de software**, en **Administración de aplicaciones**, el nombre del nodo **Solicitudes de aprobación** se cambia a **Solicitudes de aplicación**.<!-- SCCMDocs-pr#4028 -->

- Hay un nuevo método WMI, **DeleteInstance**, para quitar una solicitud de aprobación de aplicación. Esta acción no desinstala la aplicación en el dispositivo. Si todavía no está instalada, el usuario no puede instalar la aplicación desde el Centro de software.

- Llame a la API **CreateApprovedRequest** para crear una solicitud aprobada previamente para una aplicación en un dispositivo. Para evitar la instalación automática de la aplicación en el cliente, establezca el parámetro **AutoInstall** en `FALSE`. El usuario verá la aplicación en el Centro de software, pero se instalará de forma automática.

Para obtener más información, vea [Aprobar aplicaciones](../../../apps/deploy-use/app-approval.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementación del sistema operativo

### <a name="task-sequence-debugger"></a>Depurador de secuencia de tareas

<!--3612274-->
El depurador de secuencia de tareas es una nueva herramienta para la solución de problemas. Se implementa una secuencia de tareas en modo de depuración en una colección de un dispositivo. Le permite recorrer la secuencia de tareas de una manera controlada para facilitar la investigación y la resolución de problemas.

![Captura de pantalla del depurador de secuencia de tareas](./media/3612274-tsdebug.png)

Es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](../../servers/manage/pre-release-features.md).

Para más información, consulte [Depurar una secuencia de tareas](../../../osd/deploy-use/debug-task-sequence.md).

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>Limpieza del contenido de la aplicación de la caché de cliente durante la secuencia de tareas

<!--4485675-->
En el paso de secuencia de tareas **Instalar aplicación**, ahora puede eliminar el contenido de la aplicación desde la caché de cliente después de que se ejecute el paso.

Para más información, consulte [Acerca de los pasos de la secuencia de tareas](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication).

> [!Important]  
> Actualice el cliente de destino a la versión más reciente para admitir esta nueva característica.

### <a name="reclaim-sedo-lock-for-task-sequences"></a>Reclamo de bloqueo de SEDO para secuencias de tareas

<!--3699337-->
Si la consola de Configuration Manager deja de responder, podría quedarse bloqueado y no poder realizar más cambios en una secuencia de tareas. Cuando intente obtener acceso a una secuencia de tareas bloqueada, ahora podrá **descartar los cambios** y seguir editando el objeto.

Para más información, vea [Uso del editor de secuencias de tareas](../../../osd/understand/task-sequence-editor.md#bkmk_sedo).

### <a name="pre-cache-driver-packages-and-os-images"></a>Imágenes de sistema operativo y paquetes de controladores de caché previa

<!--4224642-->
La caché previa de la secuencia de tareas ahora incluye tipos de contenido adicionales. El contenido de la caché previa anteriormente solo se aplicaba a los paquetes de actualizaciones del sistema operativo. Ahora puede usar el almacenamiento en caché previa para disminuir el consumo de ancho de banda de:

- Imágenes de SO
- Paquetes de controladores
- Paquetes

Para obtener más información, vea [Configuración del contenido de la caché previa](../../../osd/deploy-use/configure-precache-content.md).

### <a name="improvements-to-os-deployment"></a>Mejoras en la implementación del sistema operativo

Esta versión incluye las siguientes mejoras en las implementaciones del sistema operativo:

- Use los dos cmdlets de PowerShell siguientes para crear y editar el paso [Ejecutar secuencia de tareas](../../../osd/understand/task-sequence-steps.md#child-task-sequence):<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- Ahora resulta más sencillo editar las variables cuando se ejecuta una secuencia de tareas. Después de seleccionar una secuencia de tareas en la ventana del Asistente para secuencia de tareas, la página para editar las variables de secuencia de tareas incluye un botón **Editar**.<!-- 4668846 --> Para obtener más información, consulte [How to use task sequence variables](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz) (Uso de variables de secuencia de tareas).

- El paso de la secuencia de tareas **Deshabilitar BitLocker** tiene un contador de reinicio nuevo. Use esta opción para especificar el número de reinicios para mantener BitLocker deshabilitado. Este cambio lo ayuda a simplificar la secuencia de tareas. Puede usar un solo paso, en lugar de agregar varias instancias de este paso. <!--4512937--> Para obtener más información, consulte [Deshabilitar BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker).

- Use la variable de la secuencia de tareas nueva **SMSTSRebootDelayNext** con la variable [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) existente. Si desea que los reinicios posteriores se realicen con un tiempo de espera distinto al primero, defina esta variable nueva con un valor diferente en segundos. <!--4447680--> Para más información, consulte [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext).

- La secuencia de tareas establece una variable de solo lectura nueva **_SMSTSLastContentDownloadLocation**. Esta variable contiene la última ubicación donde la secuencia de tareas ha descargado o intentado descargar el contenido. Inspeccione esta variable en lugar de analizar los registros de cliente.<!-- 2840337 -->

- Al crear medios de secuencia de tareas, Configuration Manager no agrega un archivo autorun.inf. Normalmente, los productos antimalware bloquean este archivo. Aun así, si es necesario para su escenario, puede incluir el archivo.<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>Mejoras en PXE

La opción 82 durante el protocolo de enlace DHCP de PXE ahora es compatible con el respondedor PXE sin WDS. La opción 82 no es compatible con WDS.


## <a name="software-center"></a><a name="bkmk_userxp"></a> Centro de software

### <a name="improvements-to-software-center-tab-customizations"></a>Mejoras en las personalizaciones de la pestaña Centro de software

<!--4063773-->
Ahora puede agregar hasta cinco pestañas personalizadas en el Centro de software. También puede modificar el orden en que aparecen estas pestañas en el Centro de software.

Para obtener más información, vea [Acerca de la configuración de cliente](../../clients/deploy/about-client-settings.md#software-center).

### <a name="software-center-infrastructure-improvements"></a>Mejoras de la infraestructura del Centro de software

<!--3555950-->

Esta versión incluye las siguientes mejoras de la infraestructura del Centro de software:

- El Centro de software ahora se comunica con un punto de administración para las aplicaciones destinadas a los usuarios, si existen. Ya no usa el catálogo de aplicaciones. Este cambio facilita la eliminación del catálogo de aplicaciones del sitio.

- Anteriormente, el Centro de software elegía el primero punto de administración de la lista de servidores disponibles. A partir de esta versión, usa el mismo punto de administración que el cliente. Este cambio permite al Centro de software usar el mismo punto de administración del sitio primario asignado que el cliente.

> [!Important]  
> Estas mejoras iterativas del Centro de software y el punto de administración son para retirar los roles de catálogo de aplicaciones.
>
> - La experiencia del usuario de Silverlight no se admite a partir de la versión 1806 de la rama actual.
> - A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones.
> - La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  

Para más información, consulte [Eliminación del catálogo de aplicaciones](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat) y [Planeamiento del Centro de software](../../../apps/plan-design/plan-for-software-center.md).

### <a name="redesigned-notification-for-newly-available-software"></a>Notificación rediseñada para el software recién disponible

<!--3555904-->
La notificación **Hay nuevo software disponible** solo se mostrará una vez por usuario para una determinada aplicación y revisión. El usuario ya no verá la notificación cada vez que inicie sesión. Solo verá otra notificación para una aplicación si ha cambiado o si se reimplementó.

Para más información, vea [Crear e implementar una aplicación](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience).

### <a name="more-frequent-countdown-notifications-for-restarts"></a>Notificaciones de cuenta regresiva más frecuentes para reinicios

<!--3976435-->

Ahora un reinicio pendiente se recordará con más frecuencia a los usuarios finales mediante notificaciones de cuenta regresiva intermitentes. Puede definir el intervalo de las notificaciones intermitentes en **Configuración de cliente** en la página **Reinicio de equipo**. Cambie el valor de **Especifique la duración de repetición para las notificaciones de cuenta regresiva de reinicio de equipo (minutos)** para configurar la frecuencia con que el usuario recibe un recordatorio respecto de un reinicio pendiente hasta que se produzca la notificación de cuenta regresiva final.

Además, el valor máximo de **Mostrar una notificación temporal al usuario que indique el intervalo antes de que el usuario se desconecte o el equipo se inicie (minutos)** ha aumentado de 1440 minutos (24 horas) a 20160 minutos (2 semanas).

Para más información, consulte [Notificaciones de reinicio del dispositivo](../../clients/deploy/device-restart-notifications.md) y [Acerca de la configuración de cliente](../../clients/deploy/about-client-settings.md#computer-restart).

### <a name="direct-link-to-custom-tabs-in-software-center"></a>Vínculo directo a pestañas personalizadas en el Centro de software

<!--4655176-->

Ahora puede proporcionar a los usuarios un vínculo directo a una [pestaña personalizada](../../clients/deploy/about-client-settings.md#software-center-tab-visibility) en el Centro de software.

Use el siguiente formato de dirección URL para abrir el Centro de software en una pestaña determinada:

`softwarecenter:page=CustomTab1`

La cadena `CustomTab1` es la primera pestaña personalizada en orden.

Por ejemplo, escriba esta dirección URL en la ventana **Ejecutar** de Windows.

También puede usar esta sintaxis para abrir pestañas predeterminadas en el Centro de software:

|Línea de comandos  |Pestaña  |
|---------|---------|
|`AvailableSoftware`|Aplicaciones|
|`Updates`|Actualizaciones|
|`OSD`|Sistemas operativos|
|`InstallationStatus`|Estado de la instalación|
|`Compliance`|Cumplimiento de dispositivos|
|`Options`|Options|

Para más información, consulte [Visibilidad de las pestañas del Centro de software](../../clients/deploy/about-client-settings.md#software-center-tab-visibility).

## <a name="software-updates"></a><a name="bkmk_sum"></a> Actualizaciones de software

### <a name="additional-options-for-wsus-maintenance"></a>Opciones adicionales para el mantenimiento de WSUS

<!--4110109-->
Ahora tiene tareas de mantenimiento de WSUS adicionales que Configuration Manager puede ejecutar para mantener en buen estado los puntos de actualización de sofware. El mantenimiento de WSUS se produce después de cada sincronización. Además de rechazar las actualizaciones expiradas en WSUS, Configuration Manager ahora puede:

- Quitar las actualizaciones obsoletas de la base de datos de WSUS.
- Agregar índices no agrupados a la base de datos de WSUS para mejorar el rendimiento de la limpieza de WSUS.

Para obtener más información, vea [Mantenimiento de las actualizaciones de software](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906).

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>Configuración del tiempo de ejecución máximo predeterminado para las actualizaciones de software

<!--3734426-->

Ahora puede especificar la cantidad máxima de tiempo de la que dispone una instalación de actualización de software. Puede especificar los elementos siguientes en la pestaña **Duración máxima de la ejecución** en el punto de actualización de software:

- **Duración máxima de la ejecución para actualizaciones de características de Windows (minutos)** .
- **Duración máxima de la ejecución para actualizaciones de Office 365 y las actualizaciones que no son de características para Windows (minutos)** .

Para obtener más información, vea [Planear actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime).

### <a name="configure-dynamic-update-during-feature-updates"></a>Configurar la actualización dinámica durante las actualizaciones de características

<!--4062619-->

Use una configuración de cliente nueva para configurar [Actualización dinámica](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) durante la instalación de actualizaciones de características de Windows 10. La actualización dinámica instala paquetes de idioma, características a petición, controladores y actualizaciones acumulativas durante la instalación de Windows al dirigir al cliente a descargar estas actualizaciones de Internet.

Para más información, consulte [Configuración de cliente de actualizaciones de software](../../clients/deploy/about-client-settings.md#software-updates) y [Administración de Windows como servicio](../../../osd/deploy-use/manage-windows-as-a-service.md).

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Nueva categoría de producto Windows 10, versión 1903 y posteriores

<!--4682946-->

**Windows 10, versión 1903 y posteriores** se ha agregado a Microsoft Update como un producto propio en lugar de formar parte del producto **Windows 10** como en las versiones anteriores. Este cambio le obligaba a realizar una serie de pasos manuales para asegurarse de que los clientes veían estas actualizaciones. Se ha intentado reducir el número de pasos manuales que debe seguir para el nuevo producto.

Cuando actualice a la versión 1906 de Configuration Manager y tenga seleccionado el producto **Windows 10** para la sincronización, las siguientes acciones tendrán lugar de forma automática:

- El producto **Windows 10, versión 1903 y posteriores** se agrega para la sincronización.
- Las reglas de implementación automática que contienen el producto **Windows 10** se actualizarán para incluir **Windows 10, versión 1903 y posteriores**.
- Los planes de mantenimiento se actualizan para incluir el producto **Windows 10, versión 1903 y posteriores**.

Para más información, consulte [Configurar las clasificaciones y los productos que va a sincronizar](../../../sum/get-started/configure-classifications-and-products.md), [Planes de mantenimiento](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) y [Reglas de implementación automática](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

### <a name="drill-through-required-updates"></a>Obtención de detalles de actualizaciones necesarias

<!--4224414-->
Ahora se pueden obtener detalles de las estadísticas de compatibilidad para ver qué dispositivos requieren una actualización de software específica. Para ver la lista de dispositivos, necesita permiso para ver las actualizaciones y las colecciones a las que pertenecen los dispositivos. Para profundizar en la lista de dispositivos, seleccione el hipervínculo **Ver las actualizaciones necesarias** junto al gráfico circular en la pestaña **Resumen** para una actualización. Si hace clic en el hipervínculo, irá a un nodo temporal en **Dispositivos**, donde podrá ver los dispositivos que requieren la actualización.

El hipervínculo **Ver las actualizaciones necesarias** está disponible en estas ubicaciones:

   - **Biblioteca de software** > **Actualizaciones de software** > **Todas las actualizaciones de software**
   - **Biblioteca de software** > **Mantenimiento de Windows 10** > **Todas las actualizaciones de Windows 10**
   - **Biblioteca de software** > **Administración de clientes de Office 365** > **Actualizaciones de Office 365**

Para más información, consulte [Supervisar actualizaciones de software](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates), [Administración de Windows como servicio](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates) y [Administrar actualizaciones de Aplicaciones de Microsoft 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


## <a name="office-management"></a><a name="bkmk_o365"></a> Administración de Office

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Panel de Upgrade Readiness para Office 365 ProPlus

<!--4021125-->

Para ayudar a determinar qué dispositivos están listos para actualizar a Aplicaciones de Microsoft 365 para empresas, hay un nuevo panel de preparación. Incluye el icono de **Upgrade Readiness para Office 365 ProPlus** que se publicó en la versión 1902 de la rama actual de Configuration Manager. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de clientes de Office 365** y seleccione el nodo **Upgrade Readiness para Office 365 ProPlus**.

Para más información sobre el panel, los requisitos previos y el uso de estos datos, consulte [Integración para la preparación de Office 365 ProPlus](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).


## <a name="protection"></a><a name="bkmk_protect"></a> Protección

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Criterios de confianza de archivos de Protección de aplicaciones de Windows Defender

<!--3555858-->

Hay una nueva configuración de directiva que permite a los usuarios confiar en archivos que normalmente se abren en Protección de aplicaciones de Windows Defender (WDAG). Tras completarse correctamente, los archivos se abrirán en el dispositivo de host en lugar de hacerlo en WDAG.

Para más información, consulte [Creación e implementación de directivas de Protección de aplicaciones de Windows Defender](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Consola de Configuration Manager

### <a name="role-based-access-for-folders"></a>Acceso basado en roles para carpetas

<!--3600867-->

Ahora puede establecer los ámbitos de seguridad en las carpetas. Si tiene acceso a un objeto de la carpeta pero no a la carpeta, no podrá ver el objeto. De forma similar, si tiene acceso a una carpeta pero no a un objeto incluido en su interior, no verá ese objeto. Haga clic con el botón derecho en una carpeta, elija **Establecer ámbitos de seguridad** y, luego, elija los ámbitos de seguridad que quiere aplicar.

Para más información, vea [Sugerencias de la consola de Configuration Manager](../../servers/manage/admin-console-tips.md) y [Configuración de la administración basada en roles](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder).

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Incorporación de una columna GUID de SMBIOS a los nodos de recopilación de dispositivos y dispositivos

<!--4526580-->
Tanto en el nodo **Dispositivos** como en el nodo **Recopilaciones de dispositivos**, ahora puede agregar una columna nueva para **GUID de SMBIOS**. Este valor es el mismo que la propiedad **GUID de BIOS** de la clase de recurso del sistema. Es un identificador único para el hardware del dispositivo.

### <a name="administration-service-support-for-security-nodes"></a>Compatibilidad del servicio de administración con los nodos de seguridad

<!--4223683-->
Ahora puede permitir que algunos nodos de la consola de Configuration Manager usen el servicio de administración. Este cambio permite que la consola se comunique con el proveedor de SMS a través de HTTPS en lugar de WMI.

Para más información, consulte [Servicio de administración](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).

> [!Note]
> A partir de la versión 1906, la pestaña **Comunicación de equipo cliente** en las propiedades del sitio ahora se denomina **Communication Security** (Seguridad de la comunicación).<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>Pestaña Colecciones en el nodo Dispositivos

<!--4616810-->
En el área de trabajo **Activos y compatibilidad**, vaya al nodo **Dispositivos** y seleccione un dispositivo. En el panel de detalles, cambie a la nueva pestaña **Colecciones**. En esta pestaña se enumeran las colecciones que incluyen este dispositivo.

> [!Note]  
> - Esta pestaña no está actualmente disponible en un subnodo de dispositivos bajo el nodo **Recopilaciones de dispositivos**. Por ejemplo, cuando selecciona la opción **Mostrar miembros** en una colección.
> - Es posible que esta pestaña no se rellene como se esperaba para algunos usuarios. Para ver la lista completa de colecciones a las que pertenece un dispositivo, debe tener el rol de seguridad **Administrador total**. Este es un problema conocido. <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>Pestaña Secuencias de tareas en el nodo Aplicaciones

<!--4616810-->
Vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones**, vaya al nodo **Aplicaciones** y seleccione una aplicación. En el panel de detalles, cambie a la nueva pestaña **Secuencias de tareas**. En esta pestaña se enumeran las secuencias de tareas que hacen referencia a esta aplicación.

### <a name="show-collection-name-for-scripts"></a>Mostrar el nombre de la recopilación para los scripts

<!--4616810-->
En el área de trabajo **Supervisión**, seleccione el nodo **Estado del script**. Ahora se muestra el **Nombre de la recopilación** además el identificador.

### <a name="real-time-actions-from-device-lists"></a>Acciones en tiempo real desde las listas de dispositivos

<!--4616810-->
Hay varias maneras de mostrar una lista de dispositivos en el nodo **Dispositivos** del área de trabajo **Activos y compatibilidad**.

- En el área de trabajo **Activos y compatibilidad**, seleccione el nodo **Recopilaciones de dispositivos**. Seleccione una recopilación de dispositivos y elija la acción **Mostrar miembros**. Esta acción abre un subnodo del nodo **Dispositivos** con una lista de dispositivos para esa colección.  

  - Al seleccionar el subnodo de la recopilación, ahora se puede iniciar **CMPivot** desde el grupo Recopilación de la cinta.  

- En el área de trabajo **Supervisión**, seleccione el nodo **Implementaciones**. Seleccione una implementación y elija la acción **Ver estado** en la cinta. En el panel de estado de la implementación, haga doble clic en el total de recursos para obtener los detalles de una lista de dispositivos.  

  - Al seleccionar un dispositivo en esta lista, ahora se puede iniciar **CMPivot** y **Ejecutar scripts** desde el grupo Dispositivo de la cinta.  

### <a name="order-by-program-name-in-task-sequence"></a>Ordenar por nombre de programa en la secuencia de tareas

<!--4616810-->
En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en el nodo **Secuencias de tareas**. Edite una secuencia de tareas y seleccione o agregue el paso [Instalar paquete](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage). Si un paquete tiene más de un programa, ahora en la lista desplegable los programas se ordenan alfabéticamente.

### <a name="correct-names-for-client-operations"></a>Nombres correctos para las operaciones de cliente

<!--4616810-->
En el área de trabajo **Supervisión**, seleccione **Operaciones de cliente**. La operación para **Cambiar al siguiente punto de actualización de software** ahora tiene el nombre correcto.


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Características y sistemas operativos en desuso

Obtenga información sobre los cambios de compatibilidad antes de implementarlos en [Elementos eliminados y en desuso](deprecated/removed-and-deprecated.md).

La versión 1906 anula la compatibilidad de las características siguientes:  

- No es posible instalar nuevos roles de catálogo de aplicaciones. Los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Para más información, consulte [Planeamiento del centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).

La versión 1906 pone en desuso la compatibilidad de los siguientes productos:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>Otras actualizaciones

A partir de esta versión las características siguientes dejarán de estar en versión preliminar:

- [Servicio de administración Proveedor de SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Administración del control de aplicaciones de Windows Defender](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Además de nuevas características, esta versión también incluye cambios adicionales como, por ejemplo, correcciones de errores. Para obtener más información, consulte [Resumen de cambios en la rama actual de Configuration Manager, versión 1906](https://support.microsoft.com/help/4514258).

Para más información sobre los cambios en los cmdlets de Windows PowerShell para Configuration Manager, consulte las [notas de la versión de PowerShell 1906](/powershell/sccm/1906-release-notes?view=sccm-ps).

El siguiente paquete acumulativo de actualizaciones (4517869) está disponible en la consola desde el 1 de octubre de 2019: [Paquete acumulativo de actualizaciones de la rama actual de Configuration Manager, versión 1906](https://support.microsoft.com/help/4517869).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Pasos siguientes

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
A partir del 16 de agosto de 2019, la versión 1906 está disponible globalmente para que todos los clientes puedan instalarla.

Cuando esté listo para instalar esta versión, consulte [Instalación de actualizaciones para Configuration Manager](../../servers/manage/updates.md) y [Lista de comprobación para la instalación de la actualización 1906](../../servers/manage/checklist-for-installing-update-1906.md).

> [!TIP]  
> Para instalar un sitio nuevo, use una versión de línea de base de Configuration Manager.  
>
> Más información acerca de:
>
> - [Instalación de nuevos sitios](../../servers/deploy/install/installing-sites.md)  
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)  

Para saber los problemas conocidos e importantes, vea las [Notas de la versión](../../servers/deploy/install/release-notes.md).

Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).
