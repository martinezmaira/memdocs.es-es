---
title: Novedades de la versión 1902
titleSuffix: Configuration Manager
description: Obtenga detalles sobre los cambios y las nuevas funcionalidades incorporados en la versión 1902 de la rama actual de Configuration Manager.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f758456ad75c4acde1b050be75d653cc0e1dcfa1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700374"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Novedades de la versión 1902 de la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 1902 de la rama actual de Configuration Manager está disponible como una actualización en consola. Aplique esta actualización a los sitios que ejecuten las versiones 1802, 1806 o 1810. <!-- baseline only statement:-->Al instalar un nuevo sitio, también está disponible como una versión de línea de base. En este artículo se resumen los cambios y las nuevas características de Configuration Manager, versión 1902.  

Revise siempre la lista de comprobación más reciente para instalar esta actualización. Para más información, consulte [Lista de comprobación para la instalación de la actualización 1902](../../servers/manage/checklist-for-installing-update-1902.md). Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).

Para aprovechar al máximo las nuevas características de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Características y sistemas operativos en desuso

Obtenga información sobre los cambios de compatibilidad antes de implementarlos en [Elementos eliminados y en desuso](deprecated/removed-and-deprecated.md).

- Ha cambiado la implementación para compartir contenido de Azure. Use una puerta de enlace de administración de la nube habilitada para el contenido al habilitar la opción de **Permitir a CMG funcionar como un punto de distribución de nube y servir contenido desde Azure Storage**. No podrá crear un punto de distribución en la nube tradicional en el futuro.

La versión 1902 anula la compatibilidad de los siguientes productos:  

- Linux y UNIX como cliente. El anuncio del desuso se realizó con la [versión 1802](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infraestructura del sitio

### <a name="client-health-dashboard"></a>Panel de mantenimiento del cliente

<!--3599209-->
Se implementan actualizaciones de software y se usan otras aplicaciones para proteger el entorno, pero estas implementaciones solo llegan a clientes correctos. Los clientes incorrectos de Configuration Manager afectan negativamente al cumplimiento general. ¿Considera que determinar el estado del cliente puede resultar complicado según el denominador "número total de dispositivos que deben estar en el ámbito de administración"? Por ejemplo, si detecta todos los sistemas de Active Directory, incluso si algunos de esos registros son para máquinas retiradas, este proceso aumenta el denominador.

Ahora puede ver un panel con información sobre el estado de los clientes de Configuration Manager en su entorno. Allí puede ver el estado del cliente, el estado de escenario y errores comunes. Filtre la vista por varios atributos distintos para ver los posibles problemas con las versiones del sistema operativo y de cliente.

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Expanda **Estado del cliente** y seleccione el nodo **Panel de mantenimiento del cliente**.

![Captura de pantalla del panel de mantenimiento del cliente](media/3599209-client-health-dashboard.png)

Para obtener más información, vea [Cómo supervisar clientes](../../clients/manage/monitor-clients.md#bkmk_health).

### <a name="new-management-insight-rules"></a>Nuevas reglas de conclusiones de administración

La característica de conclusiones de administración tiene las siguientes reglas nuevas:

- Varias reglas con recomendaciones sobre la administración de colecciones. Use esta información para simplificar la administración y mejorar el rendimiento. Revise estas nuevas reglas en el grupo **Colecciones**.<!--3555752-->  

- **Actualice los clientes a una regla de la versión de Windows 10** admitida del grupo **Administración simplificada**. Esta regla informa sobre los clientes que ejecutan una versión de Windows 10 que ya no se admite. También incluye a los clientes con una versión de Windows 10 que se acerca al final del servicio (tres meses).<!--3897268-->  

Para obtener más información, vea [Información de administración](../../servers/manage/management-insights.md).

### <a name="improvement-to-enhanced-http"></a>Optimización de HTTP mejorado

<!--3798957-->

Ahora puede habilitar HTTP mejorado por sitio primario o para el sitio de administración central.

En las propiedades del sitio de administración central, seleccione la opción **Usar los certificados generados por Configuration Manager para sistemas de sitios HTTP**. Este valor de configuración solo se aplica a los roles de sistema de sitio del sitio de administración central. No es una configuración global para la jerarquía.

Para más información, vea [HTTP mejorado](../hierarchy/enhanced-http.md).

### <a name="improvement-to-setup-prerequisites"></a>Mejoras de los requisitos previos del programa de instalación

Al instalar o actualizar a la versión 1902, el programa de instalación de Configuration Manager ahora incluye la siguiente comprobación de requisitos previos:

- **Reinicio del sistema pendiente en la instancia remota de SQL Server**: esta comprobación de requisitos previos es similar a la regla **Reinicio del sistema pendiente**, pero comprueba un servidor SQL remoto. Para obtener más información, consulte la [Lista de comprobaciones de requisitos previos](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Administración conectada a la nube

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Detención del servicio en la nube cuando se supera el umbral

<!--3735092-->
Configuration Manager ahora puede detener un servicio de Cloud Management Gateway (CMG) cuando la transferencia de datos total supera el límite. La instancia de CMG siempre ha tenido alertas para desencadenar notificaciones cuando el uso alcanza niveles críticos o de advertencia. Para lograr reducir los costos de Azure inesperados debido a un pico de uso, esta nueva opción desactiva el servicio en la nube.

Para más información, consulte [Stop CMG when it exceeds threshold](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop) (Detener CMG cuando se supere el umbral).

### <a name="use-azure-resource-manager-for-cloud-services"></a>Uso de Azure Resource Manager para servicios en la nube

<!--3605704-->
A partir de la versión 1810, la implementación clásica de servicios en Azure ya no se usa en Configuration Manager. Esta versión es la última que admite la creación de estas implementaciones de Azure.

Las implementaciones existentes seguirán funcionando. A partir de esta versión de la rama actual, Azure Resource Manager es el único mecanismo de implementación para las nuevas instancias del punto de distribución de nube y la puerta de enlace de administración de la nube.

Para más información, consulte [Azure Resource Manager para Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Adición de una puerta de enlace de administración de la nube a grupos de límites

<!--3640932-->
Ahora puede asociar una puerta de enlace de administración de la nube con un grupo de límites. Esta configuración permite a los clientes predeterminar o recurrir a dicha puerta de enlace para la comunicación con el cliente de acuerdo con las relaciones de grupo de límites. Este comportamiento es especialmente útil en escenarios de sucursales y VPN. Puede dirigir el tráfico de clientes lejos de los enlaces WAN caros y lentos para utilizar vínculos de Internet más rápidos a Microsoft Azure.

Para más información, consulte el [diseño de la jerarquía de CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design) y [configure Cloud Management Gateway](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Administración en tiempo real

### <a name="run-cmpivot-from-the-central-administration-site"></a>Ejecución de CMPivot desde el sitio de administración central

<!--3610960-->
Configuration Manager ahora admite la ejecución CMPivot desde el sitio de administración central en una jerarquía. El sitio primario sigue controlando la comunicación con el cliente. Al ejecutar CMPivot desde el sitio de administración central, se comunica con el sitio primario a través del canal de suscripción de mensajes de alta velocidad. Esta comunicación no depende de la replicación SQL estándar entre sitios.

Para obtener más información, vea [CMPivot para datos en tiempo real](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1902).

### <a name="edit-or-copy-powershell-scripts"></a>Edición o copia de scripts de PowerShell

<!--3705507-->
Ahora puede **editar** o **copiar** un script de PowerShell existente que se usa con la característica Ejecutar scripts. En lugar de volver a crear un script que necesita cambiar, ahora puede editarlo directamente. Ambas acciones utilizan la misma experiencia de asistente que cuando se crea un nuevo script. Cuando edita o copia un script, Configuration Manager no mantiene el estado de aprobación.

Para más información, consulte [Ejecutar scripts](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit).


## <a name="content-management"></a><a name="bkmk_content"></a> Administración de contenido

### <a name="distribution-point-maintenance-mode"></a>Modo de mantenimiento del punto de distribución

<!--3555754-->

Ahora puede establecer un punto de distribución en modo de mantenimiento. Habilite el modo de mantenimiento cuando vaya a instalar actualizaciones de software o realizar cambios de hardware en el servidor.

Mientras el punto de distribución está en modo de mantenimiento, presenta estos comportamientos:

- El sitio no distribuye contenido a este punto de distribución.  

- Los puntos de administración no devuelvan la ubicación de este punto de distribución a los clientes.

- Cuando se actualiza el sitio, todavía se actualiza un punto de distribución en modo de mantenimiento.

- Las propiedades del punto de distribución son de solo lectura. Por ejemplo, no se puede cambiar el certificado ni agregar grupos de límites.  

- Cualquier tarea programada, como la validación de contenido, se sigue ejecutando en la misma programación.

Para más información sobre esta característica, consulte [Modo de mantenimiento](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint).

Para más información sobre cómo automatizar este proceso con el SDK de Configuration Manager, consulte artículo sobre el [método SetDPMaintenanceMode en la clase SMS_DistributionPointInfo](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="client-management"></a><a name="bkmk_client"></a> Administración de clientes

### <a name="client-provisioning-mode-timeout"></a>Tiempo de espera del modo de aprovisionamiento de cliente

<!--3197824-->
La secuencia de tareas establece una marca de tiempo cuando coloca el cliente en modo de aprovisionamiento. Un cliente en modo de aprovisionamiento comprueba cada 60 minutos la duración de tiempo transcurrido desde la marca de tiempo. Si ha estado en modo de aprovisionamiento durante más de 48 horas, el cliente sale del modo de aprovisionamiento automáticamente y reinicia el proceso.

Para más información, consulte [Modo de aprovisionamiento](../../../osd/understand/provisioning-mode.md).

### <a name="view-first-screen-only-during-remote-control"></a>Visualización de la primera pantalla solo durante el control remoto

<!--3231732-->
Cuando se conecta a un cliente con dos o más monitores, puede ser difícil verlos todos en el visor del control remoto de Configuration Manager. Un operador de herramientas remoto puede elegir ahora entre ver **todas las pantallas** o solo la **primera pantalla**.

Para obtener más información, vea [Cómo administrar de forma remota un equipo cliente de Windows](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="specify-a-custom-port-for-peer-wakeup"></a>Especificación de un puerto personalizado para reactivación del mismo nivel

<!--3605925-->
Ahora puede especificar un número de puerto personalizado para el proxy de reactivación. En la configuración de cliente, en el grupo **Administración de energía**, establezca la configuración de **Número de puerto de Wake On LAN (UDP)** .  

Para obtener más información, vea [Cómo configurar Wake on LAN](../../clients/deploy/configure-wake-on-lan.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Administración de aplicaciones

### <a name="improvements-to-application-approvals-via-email"></a>Mejoras de las aprobaciones de aplicación por correo electrónico

<!--3594063-->
En esta versión se incluyen mejoras en la característica para recibir notificaciones por correo electrónico para las solicitudes de aplicación. Los usuarios siempre podían agregar un comentario a la solicitud desde el Centro de software. Este comentario se muestra en la solicitud de aplicación en la consola de Configuration Manager. Ahora el comentario también se muestra en el correo electrónico. La inclusión de este comentario en el correo electrónico ayuda a los aprobadores a tomar una decisión más acertada para aprobar o denegar la solicitud.

Para más información, consulte [Notificaciones por correo electrónico](../../../apps/deploy-use/app-approval.md#bkmk_email-approve).

### <a name="improvements-to-package-conversion-manager"></a>Mejoras del Administrador de conversión de paquetes

<!-- SCCMDocs-pr issue #3357 -->
Esta versión incluye las siguientes mejoras del [Administrador de conversión de paquetes](../../../apps/pcm/package-conversion-manager.md):

- Análisis de paquetes programado que se ejecuta cada 7 días de forma predeterminada
- Cmdlets de PowerShell para analizar y convertir paquetes
- Mejoras y correcciones de errores generales


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementación del sistema operativo

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Estado de progreso durante la secuencia de tareas de actualización local

<!--3747129-->
Ahora verá una barra de progreso más detallada durante una secuencia de tareas de actualización local de Windows 10. Esta barra muestra el progreso de la configuración de Windows, que por lo demás es silenciosa durante la secuencia de tareas. Los usuarios tienen ahora cierta visibilidad del progreso subyacente. Esto ayuda con la preocupación de que el proceso de actualización se suspenda debido a la falta de indicación de progreso.  

![Ejemplo de progreso de la secuencia de tareas con el progreso de la actualización de Windows](media/3747129-installation-progress.png)

Esta característica funciona con cualquier versión admitida de Windows 10 y únicamente con la secuencia de tareas de actualización local.

### <a name="improvements-to-task-sequence-media-creation"></a>Mejoras en la creación de medios de secuencia de tareas

<!--3556027, fka 1359388-->
Esta versión incluye varias mejoras para ayudarle a crear y administrar medios de secuencia de tareas. Para más información, vea los siguientes artículos sobre los tipos de medios específicos:

- [Crear medios independientes](../../../osd/deploy-use/create-stand-alone-media.md)
- [Crear medios preconfigurados](../../../osd/deploy-use/create-prestaged-media.md)
- [Crear medios de arranque](../../../osd/deploy-use/create-bootable-media.md)
- [Crear medios de captura](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>Especificar almacenamiento temporal

Al crear medios de secuencia de tareas, personaliza la ubicación que usa el sitio para el almacenamiento temporal de datos. Este proceso puede requerir mucho espacio de unidad temporal. Este cambio proporciona mayor flexibilidad para elegir dónde almacenar estos archivos temporales.

En el **Asistente para crear medio de secuencia de tareas**, especifique una ubicación para la **carpeta de almacenamiento provisional**. De forma predeterminada, esta ubicación es similar a la siguiente ruta de acceso: `%UserProfile%\AppData\Local\Temp`.

#### <a name="add-a-label-to-the-media"></a>Agregar una etiqueta a los medios

Ahora puede agregar una etiqueta a los medios de secuencia de tareas. Esta etiqueta ayuda a identificar mejor el medio después de crearlo. En el **Asistente para crear medio de secuencia de tareas**, especifique una **etiqueta de medio**.

### <a name="import-a-single-index-of-an-os-image"></a>Importación de un índice único de una imagen de sistema operativo

<!--3719699-->
Al importar un archivo de imagen de Windows (WIM) en Configuration Manager, ahora puede especificar que se importe automáticamente un índice único en lugar de todos los índices de la imagen en el archivo. Esta opción ofrece estas ventajas:

- Archivo de imagen más pequeño  
- Instalación sin conexión más rápida  
- Optimización del mantenimiento de imágenes, para un archivo de imagen más pequeño tras una instalación sin conexión

Al importar una imagen del sistema operativo, seleccione la opción **Extraer un índice de imágenes específico del archivo WIM especificado**. Después, seleccione el índice de imagen en la lista.  

Para más información, consulte [Agregar una imagen de sistema operativo](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages).

### <a name="optimized-image-servicing"></a>Servicio de imágenes optimizado

<!--3555951-->
Al aplicar actualizaciones de software a una imagen de sistema operativo, puede usar una nueva opción para optimizar los resultados que consiste en quitar cualquier actualización reemplazada. La optimización de la instalación sin conexión solo se aplica a imágenes con un índice único.

Cuando se cree una programación para actualizar una imagen de sistema operativo, seleccione la opción **Quitar las actualizaciones reemplazadas después de actualizar la imagen**.

Para más información, vea [Aplicar las actualizaciones de software a una imagen](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase).

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Mejoras del paso de secuencia de tareas Ejecutar script de PowerShell

<!--3556028, fka 1359389-->
El paso de secuencia de tareas **Ejecutar script de PowerShell** incluye ahora las siguientes mejoras:  

- Ahora puede escribir directamente código de Windows PowerShell en este paso. Este cambio permite ejecutar comandos de PowerShell durante una secuencia de tareas sin necesidad de crear y distribuir un paquete con el script.

- cuando se elige la opción **Especificar un script de PowerShell**, haga clic en **Editar script**. En la nueva ventana de script de PowerShell se proporcionan las acciones siguientes:  

    - Editar el script directamente  

    - Abrir un script existente desde un archivo  

    - Ir a un script aprobado existente en Configuration Manager

- Guardar la salida del script en una variable de secuencia de tareas personalizada  

- Para incluir los parámetros del script en el registro de la secuencia de tareas, establezca la variable de secuencia de tareas **OSDLogPowerShellParameters** en **TRUE**. De forma predeterminada, los parámetros no están en el registro.  

- Otras mejoras que proporcionan una funcionalidad similar a la del paso [Ejecutar línea de comandos](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine). Por ejemplo, especifique credenciales de usuario alternativas o especifique un tiempo de espera.

> [!Important]  
> Para aprovechar esta nueva característica de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

Para más información, vea [Ejecutar script de PowerShell](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

### <a name="other-improvements-to-os-deployment"></a>Otras mejoras en la implementación del sistema operativo

<!--3633146,3641475,3654172,3734270-->
Esta versión incluye las siguientes mejoras en la implementación del sistema operativo:

- Hay una nueva acción predeterminada **Ver** en las secuencias de tareas. <!--3633146-->  

- La ventana del cuadro de diálogo de error de secuencia de tareas muestra ahora más información. Muestra el nombre del paso de la secuencia de tareas donde se produjo el error. <!--3641475-->  

- Al establecer la variable de secuencia de tareas **OSDDoNotLogCommand** en True, ahora también se oculta la línea de comandos del paso Ejecutar línea de comandos en el archivo de registro. Antes solo se enmascaraba el nombre del programa en el paso Instalar paquete en el archivo smsts.log.<!--3654172-->  

- Cuando se habilita un respondedor PXE en un punto de distribución sin Servicio de implementación de Windows, ahora puede ser en el mismo servidor que el servicio DHCP. <!--3734270--> Para más información, consulte [Configurar al menos un punto de distribución para aceptar solicitudes del entorno PXE](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


## <a name="software-center"></a><a name="bkmk_userxp"></a> Centro de software

### <a name="replace-toast-notifications-with-dialog-window"></a>Reemplazo de las notificaciones del sistema por una ventana de cuadro de diálogo

<!--3555947-->
A veces los usuarios no ven la notificación del sistema de Windows sobre un reinicio o una implementación necesaria. Entonces no ven la experiencia de posponer el recordatorio. Este comportamiento puede conducir a una mala experiencia de usuario cuando el cliente llega a una fecha límite.

Ahora, si es necesario reiniciar las implementaciones o se requieren cambios de software, tiene la opción de utilizar una ventana de diálogo más intrusiva.

Para más información, vea [Planeamiento del centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

### <a name="configure-user-device-affinity-in-software-center"></a>Configuración de la afinidad entre usuario y dispositivo en el Centro de software

<!--3485366-->
Con las [mejoras en la infraestructura del Centro de software](whats-new-in-version-1806.md#software-center-infrastructure-improvements) a partir de la versión 1806, los roles de servidor de sitio del catálogo de aplicaciones ya no son necesarios para la mayoría de los escenarios. Algunos clientes todavía pueden depender del catálogo de aplicaciones para permitir que los usuarios establezcan su dispositivo primario para la afinidad de dispositivo del usuario.

Ahora los usuarios pueden establecer su dispositivo primario en el Centro de software. Esta acción hace que sean usuarios primarios del dispositivo en Configuration Manager.

Para obtener más información, vea [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="configure-default-views-in-software-center"></a>Configuración de vistas predeterminadas en el Centro de software

<!--3612112-->
Esta versión de Configuration Manager contiene más información sobre cómo personalizar el Centro de software:

- Establecimiento del diseño predeterminado de las aplicaciones, como iconos o una lista  

    - Si un usuario cambia esta configuración, el Centro de software mantiene la preferencia del usuario en el futuro.  

- Configuración del filtro de aplicación predeterminado, ya sea todas o solo las aplicaciones necesarias  

    - Centro de software siempre usa la configuración predeterminada. Los usuarios pueden cambiar este filtro, pero el Centro de software no conserva sus preferencias.

Especifique estos valores en el grupo de configuración de cliente **Centro de software**.

Para más información, vea [Acerca de la configuración de cliente](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults).


## <a name="software-updates"></a><a name="bkmk_sum"></a> Actualizaciones de software

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Especificación de la prioridad de las actualizaciones de características en el mantenimiento de Windows 10

<!--3734525-->
Ajuste la prioridad con la que los clientes instalan una actualización de características a través de [Mantenimiento de Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md). De forma predeterminada, los clientes ahora instalan las actualizaciones de características con mayor prioridad de procesamiento.

Use la configuración de cliente para configurar esta opción. En el grupo **Actualizaciones de software**, configure esta opción: **Especificación de la prioridad de subproceso para las actualizaciones de características**.

Para más información, vea [Acerca de la configuración de cliente](../../clients/deploy/about-client-settings.md#software-updates).


## <a name="office-management"></a><a name="bkmk_o365"></a> Administración de Office

### <a name="redirect-windows-known-folders-to-onedrive"></a>Redirección de carpetas conocidas de Windows a OneDrive

<!--3556021-->
Utilice Configuration Manager para mover las carpetas conocidas de Windows a OneDrive para la Empresa. Estas carpetas incluyen Escritorio, Documentos e Imágenes. Para simplificar las actualizaciones de Windows 10, implemente esta configuración en los clientes de Windows 7 antes de implementar una secuencia de tareas.

Para más información sobre esta característica de OneDrive para la Empresa, consulte [Redirigir y mover las carpetas conocidas de Windows a OneDrive](/onedrive/redirect-known-folders).

Primero, [busque el identificador de inquilino de Office 365](/onedrive/find-your-office-365-tenant-id). Luego, implemente la versión de cliente de sincronización de OneDrive 18.111.0603.0004 o una versión posterior. Para más información, vea [Implementar aplicaciones de OneDrive con Configuration Manager](/onedrive/deploy-on-windows).  

Para crear e implementar un perfil de OneDrive para la Empresa, en la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Expanda **Configuración de cumplimiento** y seleccione el nodo **Perfiles de OneDrive para la Empresa**.  

Para más información, consulte la sección sobre redirección de carpetas conocidas de Windows a OneDrive en el artículo [OneDrive for Business Profiles](../../../compliance/deploy-use/onedrive-profile.md) (OneDrive for Business Profiles).

### <a name="integration-for-office-365-proplus-readiness"></a>Integración para la preparación de Office 365 ProPlus

<!--3735402-->
Use Configuration Manager para identificar los dispositivos con una confianza alta que estén listos para actualizar a Office 365 ProPlus. La integración proporciona conclusiones sobre los posibles problemas de compatibilidad con los complementos y las macros de Office usados en su entorno. Después, use Configuration Manager para implementar Office en los dispositivos que estén listos.

El panel de administración de clientes existente de Office 365 ahora incluye un nuevo icono, **Office 365 ProPlus Upgrade Readiness**.

Para más información, consulte [Panel de administración del cliente de Office 365](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness).

### <a name="additional-languages-for-office-365-updates"></a>Idiomas adicionales para las actualizaciones de Office 365

<!--3555955-->
Configuration Manager ahora es compatible con todos los idiomas admitidos para las actualizaciones de cliente de Office 365. El flujo de trabajo de actualización ahora separa los 38 idiomas de **Windows Update** de los numerosos idiomas de la **actualización de cliente de Office 365**.

Para más información, consulte [Administración de las actualizaciones de Office 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang).

### <a name="office-products-on-lifecycle-dashboard"></a>Productos de Office en el panel de ciclo de vida

<!--3556026-->
El panel de ciclo de vida de los productos ahora incluye información sobre las versiones instaladas de Office 2003 hasta Office 2016. Los datos aparecen después de que el sitio ejecute la tarea de resumen del ciclo de vida, que es cada 24 horas.

Para más información, vea [Uso del panel de ciclo de vida del producto](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


## <a name="phased-deployments"></a><a name="bkmk_pod"></a> Implementaciones por fases

### <a name="dedicated-monitoring-for-phased-deployments"></a>Supervisión dedicada para implementaciones por fases

<!--3555949-->
Las implementaciones por fases ahora tienen su propio nodo de supervisión dedicado. Con este nodo es más fácil identificar las implementaciones por fases que creó y, después, ir a la vista de supervisión de la implementación por fases. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Implementaciones por fases**. Se muestra la lista de implementaciones por fases.

Para más información, vea la [vista de supervisión de implementaciones por fases](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor).

### <a name="improvement-to-phased-deployment-success-criteria"></a>Mejora de los criterios de éxito para la implementación por fases

<!--3555946-->
Especifique criterios adicionales para el éxito de una fase en una implementación por fases. En lugar de solamente un porcentaje, este criterio ahora también puede ser el número de dispositivos implementados correctamente. Esta opción es útil cuando el tamaño de la colección es variable y tiene un número específico de dispositivos que deben implementarse correctamente para poder pasar a la siguiente fase.

Cree una implementación por fases para una secuencia de tareas, actualización de software o aplicación. En la página de configuración del asistente, seleccione la siguiente opción como criterios de éxito de la primera fase: **Número de dispositivos implementados correctamente**.

Para más información, vea [Crear implementaciones por fases](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Consola de Configuration Manager

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a> Mejoras en la consola de Configuration Manager

<!--3594151-->
Según los comentarios de clientes recibidos en la cumbre Midwest Management Summit (MMS) Desert Edition de 2018, en esta versión se incluyen las mejoras siguientes de la consola de Configuration Manager:

- Maximizar la ventana del Registro del explorador de los métodos de detección de aplicaciones
- Ir a la colección desde una implementación de aplicación
- Quitar contenido del estado de supervisión
- Ordenación de las vistas por valores enteros en el nodo **Implementaciones** del área de trabajo **Supervisión**
- Mover la advertencia de un número de resultados elevado

Para más información, vea [Sugerencias de la consola de Configuration Manager](../../servers/manage/admin-console-tips.md).

### <a name="configuration-manager-console-notifications"></a>Notificaciones de la consola de Configuration Manager

<!--3556016, fka 1318035-->
Para estar esté mejor informado y poder realizar la acción adecuada, la consola de Configuration Manager ahora le notifica los siguientes eventos:

- Cuando hay una actualización disponible para el propio Configuration Manager
- Cuando se producen eventos de ciclo de vida y mantenimiento en el entorno

Esta notificación es una barra en la parte superior de la ventana de la consola, debajo de la cinta. Reemplaza a la experiencia anterior cuando había disponibles actualizaciones de Configuration Manager. Estas notificaciones en consola aún muestran información crítica, pero no interfieren con el trabajo en la consola. No se pueden descartar las notificaciones críticas. La consola muestra todas las notificaciones en una nueva área de notificación de la barra de título.

Para más información, vea [Notificaciones de la consola de Configuration Manager](../../servers/manage/admin-console-notifications.md).

### <a name="confirmation-of-console-feedback"></a>Confirmación de comentarios de la consola

<!--3556010-->
Al enviar [comentarios](../../understand/find-help.md#product-feedback) en la consola de Configuration Manager, ahora se muestra un mensaje de confirmación. Este mensaje incluye un **identificador de comentario** que puede enviar a Microsoft como identificador de seguimiento.

Para obtener más información, vea [Comentarios sobre el producto](../../understand/find-help.md#bkmk_feedbackid).

### <a name="view-recently-connected-consoles"></a>Consulta de las consolas conectadas recientemente

<!--3699367-->
Ahora puede ver las conexiones más recientes de la consola de Configuration Manager. La vista incluye las conexiones activas y aquellas consolas que se conectaron recientemente. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Seguridad** y seleccione el nodo **Conexiones de la consola**.

Para obtener más información, vea [Uso de la consola de Configuration Manager](../../servers/manage/admin-console.md#bkmk_viewconnected).

### <a name="in-console-documentation-dashboard"></a>Panel de documentación en consola

<!--3556019, fka 1357546-->
Hay un nuevo nodo de **documentación** en la nueva área de trabajo **Comunidad**. Este nodo incluye información actualizada acerca de los artículos de soporte técnico y la documentación de Configuration Manager.

Para obtener más información, vea [Uso de la consola de Configuration Manager](../../servers/manage/admin-console.md#bkmk_doc-dashboard).

### <a name="search-device-views-using-mac-address"></a>Vistas de búsqueda de dispositivos mediante dirección MAC

<!--3600878-->
Ahora puede buscar una dirección MAC en la vista de un dispositivo de la consola de Configuration Manager. Esta propiedad es útil para los administradores de implementaciones de sistema operativo durante la solución de problemas de implementaciones de PXE. Cuando vea una lista de dispositivos, agregue la columna **Dirección MAC** a la vista. Use el campo de búsqueda para agregar los criterios de búsqueda de **Dirección MAC**.

Para más información, vea [Sugerencias de la consola de Configuration Manager](../../servers/manage/admin-console-tips.md).

### <a name="use-net-47-for-improved-console-accessibility"></a>Uso de .NET 4.7 para mejorar la accesibilidad de la consola

<!-- SCCMDocs-pr issue #3228 -->
Para mejorar las características de accesibilidad de la consola de Configuration Manager, actualice .NET a la versión 4.7 o posterior en el equipo que ejecuta la consola.

Para obtener la información, vea [Características de accesibilidad de Configuration Manager](../../understand/accessibility-features.md).

### <a name="changes-to-console-setup-process"></a>Cambios realizados en el proceso de instalación de la consola

<!-- 3612513 -->
Se requieren nuevos componentes para instalar la consola de Configuration Manager. Si crea un paquete para instalar la consola en otros equipos, asegúrese de que el paquete incluya los siguientes archivos:

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

Al instalar o actualizar el servidor de sitio, copia estos archivos de instalación y los paquetes de idioma admitidos para el sitio en la subcarpeta **Tools\ConsoleSetup**. Para obtener más información, consulte [Instalar la consola de Configuration Manager](../../servers/deploy/install/install-consoles.md).


## <a name="other-updates"></a>Otras actualizaciones

Además de nuevas características, esta versión también incluye cambios adicionales como, por ejemplo, correcciones de errores. Para obtener más información, consulte [Resumen de cambios en la rama actual de Configuration Manager, versión 1902](https://support.microsoft.com/help/4498910).

Para más información sobre los cambios en los cmdlets de Windows PowerShell para Configuration Manager, consulte las [notas de la versión de PowerShell 1902](/powershell/sccm/1902-release-notes?view=sccm-ps).

El paquete acumulativo de actualizaciones siguiente (4500571) está disponible en la consola desde el 17 de junio de 2019: [Paquete acumulativo de actualizaciones de la rama actual de Configuration Manager, versión 1902](https://support.microsoft.com/help/4500571).

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

Cuando esté listo para instalar esta versión, consulte [Instalación de actualizaciones para Configuration Manager](../../servers/manage/updates.md) y [Lista de comprobación para la instalación de la actualización 1902](../../servers/manage/checklist-for-installing-update-1902.md).

> [!TIP]  
> Para instalar un sitio nuevo, use una versión de línea de base de Configuration Manager.  
>
> Más información acerca de:    
> - [Instalación de nuevos sitios](../../servers/deploy/install/installing-sites.md)  
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)  

Para saber los problemas conocidos e importantes, vea las [Notas de la versión](../../servers/deploy/install/release-notes.md).

Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).