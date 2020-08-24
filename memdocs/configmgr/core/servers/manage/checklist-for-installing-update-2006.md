---
title: Lista de comprobación de 2006
titleSuffix: Configuration Manager
description: Sepa lo que debe hacer antes de actualizar a la versión 2006 de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6d359306-69ae-4873-ba90-964b6ae51d79
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a3c66863e7768c5ca90151bf85d61aa1e3a0e17
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129613"
---
# <a name="checklist-for-installing-update-2006-for-configuration-manager"></a>Lista de comprobación para la instalación de la actualización 2006 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Si usa la rama actual de Configuration Manager, puede instalar la actualización en consola de la versión 2006 a fin de actualizar la jerarquía desde una versión anterior. <!-- baseline only statement:Version 2006 is also available as [baseline media](updates.md#bkmk_Baselines), so you can use the installation media to install the first site of a new hierarchy.-->

Para obtener la actualización de la versión 2006, debe usar un punto de conexión de servicio en el sitio de nivel superior de la jerarquía. Este rol de sistema de sitio puede realizarse en el modo en línea o sin conexión. Para descargar la actualización cuando el punto de conexión de servicio está desconectado, [use la herramienta de conexión de servicio](use-the-service-connection-tool.md).<!-- SCCMDocs#1946 -->

Después de que su jerarquía descargue el paquete de actualización de Microsoft, búsquelo en la consola. En el área de trabajo **Administración**, seleccione el nodo **Actualizaciones y mantenimiento**.

- Cuando la actualización aparezca como **Disponible**, ya está lista para instalarse. Antes de instalar la versión 2006, revise la siguiente información [relativa a la instalación de la actualización 2006](#about-installing-update-2006) y la [lista de comprobación](#checklist) para ver las configuraciones que se deben realizar antes de iniciar la actualización.

- Si la actualización se muestra como **Descargando** y no cambia, revise los archivos **hman.log** y **dmpdownloader.log** para ver los errores.

  - El archivo dmpdownloader.log puede indicar que el proceso de dmpdownloader está esperando un intervalo antes de comprobar las actualizaciones. Reinicie el servicio **SMS_Executive** en el servidor de sitio para reiniciar la descarga de los archivos de redistribución de la actualización.

  - Otro problema común de descarga se produce cuando la configuración del servidor proxy impide descargas desde `silverlight.dlservice.microsoft.com`, `download.microsoft.com` y `go.microsoft.com`.

Para obtener más información sobre la instalación de actualizaciones, consulte [Actualizaciones y servicio en la consola](updates.md#bkmk_inconsole).

Para más información sobre las versiones de la rama actual, vea [Versiones de línea de base y versiones de actualización](updates.md#bkmk_Baselines).

## <a name="about-installing-update-2006"></a>Acerca de la instalación de la actualización 2006

### <a name="sites"></a>Sitios

Instale la actualización 2006 en el sitio de nivel superior de la jerarquía. Inicie la instalación desde el sitio de administración central (CAS), o bien desde el sitio principal independiente. Después de instalar la actualización en el sitio de nivel superior, los sitios secundarios tienen el siguiente comportamiento de actualización:

- Los sitios primarios secundarios inician la instalación de la actualización automáticamente después de que el sitio de administración central termine de instalarla. Puede usar períodos para tareas administrativas para controlar el momento en que un sitio instala la actualización. Para más información, vea [Ventanas de servicio para servidores de sitio](service-windows.md).

- Una vez que el sitio principal primario termine de instalar la actualización, actualice manualmente cada sitio secundario desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.

### <a name="site-system-roles"></a>Roles de sistema de sitio

Cuando un servidor de sitio instala la actualización, actualiza automáticamente todos los roles de sistema de sitio. Estos roles están en el servidor de sitio o instalados en servidores remotos. Antes de instalar la actualización, asegúrese de que cada servidor de sistema de sitio cumpla los requisitos previos actuales con la nueva versión de la actualización.

### <a name="configuration-manager-consoles"></a>Consolas de Configuration Manager

La primera vez que use una consola de Configuration Manager una vez que la actualización haya terminado, se le pedirá que actualice esa consola. También puede ejecutar el programa de instalación de Configuration Manager en el equipo que hospede la consola y seleccionar la opción para actualizarla. Instale la actualización en la consola tan pronto como sea posible. Para obtener más información, consulte [Instalar la consola de Configuration Manager](../deploy/install/install-consoles.md).

> [!IMPORTANT]  
> Cuando instala una actualización en el sitio de administración central, tenga en cuenta las siguientes limitaciones y retrasos que existen hasta que todos los sitios primarios secundarios también completan la instalación de la actualización:
>
> - **Las actualizaciones de cliente** no se inician. Esto incluye las actualizaciones automáticas de los clientes y los clientes de preproducción. Además, no se puede promover a los clientes de preproducción a producción hasta que el último sitio completa la instalación de la actualización. Después de que el último sitio complete la instalación de la actualización, las actualizaciones de cliente comenzarán en función de las opciones de configuración.
> - Las **nuevas características** habilitadas con la actualización no están disponibles. Este comportamiento es para evitar la replicación de datos del sitio de administración central relacionados con esa característica en un sitio que no ha instalado aún la compatibilidad con esa característica. Después de que todos los sitios primarios instalen la actualización, la característica estará disponible para su uso.
> - Los **vínculos de replicación** entre el sitio de administración central y los sitios primarios secundarios se muestran como no actualizados. Este estado se muestra en el estado de instalación de la actualización como *completado con la advertencia* Supervisando inicialización de replicación. En el área de trabajo **Supervisión** de la consola, este estado se muestra como *El vínculo en configuración*.

### <a name="early-update-ring"></a>Anillo de actualización inicial

<!-- SCCMDocs#1397 -->

<!-- As of May 11, 2020, version 2006 is globally available for all customers to install. If you previously opted in to the early update ring, watch for an update to this current branch version. -->

En este momento, la versión 2006 se ha lanzado para el anillo de actualización inicial. Para instalar esta actualización, debe indicar su consentimiento para participar. El siguiente script de PowerShell agrega la jerarquía o sitio primario independiente al anillo de actualización inicial de la versión 2006:

[Script de participación en la versión 2006](https://go.microsoft.com/fwlink/?linkid=2099733) <!-- This fwlink points to the script package on the Download Center, don't change the link here! Make any changes to the fwlink target -->

Microsoft firma el script digitalmente y lo agrupa dentro de un archivo ejecutable autoextraíble.

> [!NOTE]
> La actualización de la versión 2006 solo es válida en sitios que ejecutan la versión 1810 u otra posterior.

Para participar en el anillo de actualización inicial:

1. Abra Windows PowerShell y **Ejecutar como administrador**.
1. Ejecute el script **EnableEarlyUpdateRing2006.ps1** con la siguiente sintaxis:

    `EnableEarlyUpdateRing2006.ps1 <SiteServer_Name> | SiteServer_IP>`

    Donde `SiteServer` hace referencia al sitio de administración central o al servidor de sitio primario independiente. Por ejemplo: `EnableEarlyUpdateRing2006.ps1 cmprimary01`

1. Compruebe si hay actualizaciones. Para obtener más información, consulte [Obtención de actualizaciones disponibles](install-in-console-updates.md#get-available-updates).

Ahora, la actualización de la versión 2006 debería estar disponible en la consola.

> [!IMPORTANT]
> Este script solo agrega el sitio al anillo de actualización inicial de la versión 2006. No se trata de un cambio permanente.

## <a name="checklist"></a>Lista de comprobación

### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Todos los sitios ejecutan una versión admitida de Configuration Manager

Para poder iniciar la instalación de la actualización 2006, cada servidor de sitio de la jerarquía debe ejecutar la misma versión de Configuration Manager. Para actualizar a 2006, debe usar la versión 1810 o una posterior.

### <a name="review-the-status-of-your-product-licensing"></a>Revisar el estado de la licencia de producto

Debe tener un contrato de Software Assurance (SA) activo o derechos de suscripción equivalentes para instalar esta actualización. Al actualizar el sitio, la página **Licencias** ofrece la opción de confirmar la **Fecha de expiración de Software Assurance**.

Este valor es opcional. Puede especificarlo como un recordatorio útil de la fecha de expiración de la licencia. Esta fecha está visible cuando se instalan las actualizaciones futuras. Puede que haya especificado anteriormente este valor durante la configuración o instalación de una actualización. También puede especificar este valor en la consola de Configuration Manager. En el área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione **Sitios**. Seleccione **Configuración de jerarquía** en la cinta de opciones y cambie a la pestaña **Licencias**.

Para obtener más información, vea [Licencias y ramas](../../understand/learn-more-editions.md).

### <a name="review-microsoft-net-versions"></a>Revisar las versiones de .NET de Microsoft

Cuando un sitio instala esta actualización, si el requisito mínimo de .NET Framework 4.5 no está instalado, Configuration Manager instala automáticamente .NET Framework 4.5.2. Cuando este requisito previo no está instalado, el sitio lo instala en cada servidor que hospeda uno de los siguientes roles de sistema de sitio:

- Punto de administración
- Punto de conexión de servicio
- Punto de proxy de inscripción
- Punto de inscripción

Esta instalación puede poner el servidor de sistema de sitio en un estado pendiente de reinicio y notificar los errores al visor de estado de los componentes de Configuration Manager. Además, las aplicaciones .NET del servidor pueden experimentar errores aleatorios hasta que reinicie el servidor.

Para obtener más información, vea  [Requisitos previos de sitio y sistema de sitio](../../plan-design/configs/site-and-site-system-prerequisites.md).

### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Revisar la versión de Windows ADK para Windows 10

La versión de Assessment and Deployment Kit (ADK) para Windows 10 debe ser compatible con la versión 2006 de Configuration Manager. Para obtener más información sobre las versiones de Windows ADK admitidas, consulte [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Si es necesario actualizar Windows ADK, hágalo antes de comenzar la actualización de Configuration Manager. Esto garantiza que las imágenes de arranque predeterminadas se actualicen automáticamente a la última versión de Windows PE. Actualice manualmente las imágenes de arranque personalizadas después de actualizar el sitio.

Si actualiza el sitio antes que Windows ADK, vea [Actualización de puntos de distribución con la imagen](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

### <a name="review-sql-server-native-client-version"></a>Revisión de la versión de SQL Server Native Client

Instale una versión mínima de SQL Server 2012 Native Client, que incluya compatibilidad con TLS 1.2. Para obtener más información, consulte [Lista de comprobaciones de requisitos previos](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Revisar el estado del sitio y de la jerarquía en busca de problemas sin resolver

La actualización del sitio puede generar errores debido a problemas de funcionamiento existentes. Antes de actualizar un sitio, resuelva todos los problemas de funcionamiento de los siguientes sistemas:  

- El servidor de sitio  
- El servidor de base de datos del sitio  
- Roles de sistema de sitio remoto en otros servidores

Para obtener más información, vea  [Usar alertas y el sistema de estado](use-alerts-and-the-status-system.md).

### <a name="review-file-and-data-replication-between-sites"></a>Revisar la replicación de datos y archivos entre sitios

Asegúrese de que la replicación de archivos y bases de datos entre sitios funciona y está actualizada. Los retrasos o los trabajos pendientes pueden impedir una actualización correcta.

#### <a name="database-replication"></a>Replicación de base de datos

Para la [replicación de base de datos](../../plan-design/hierarchy/database-replication.md), para ayudar a resolver problemas antes de iniciar la actualización, utilice **Replication Link Analyzer** (RLA). Para obtener más información, consulte [Supervisión de la replicación de la base de datos](monitor-replication.md).

Use RLA para responder a las siguientes preguntas:

- ¿Está la replicación por grupo en buen estado?
- ¿Hay algún vínculo degradado?
- ¿Hay algún error?

Si hay un trabajo pendiente, espere hasta que desaparezca. Si el trabajo pendiente es grande, como millones de registros, el vínculo se encuentra en mal estado. Antes de actualizar el sitio, resuelva el problema de replicación. Si necesita más ayuda, póngase en contacto con el Soporte técnico de Microsoft.<!-- 2838129 -->

#### <a name="file-based-replication"></a>replicación basada en archivos

Para la [replicación basada en archivos](../../plan-design/hierarchy/file-based-replication.md), compruebe todas las bandejas de entrada en busca de trabajos pendientes, tanto en sitios de envío como en sitios de recepción. Si hay muchos trabajos de replicación bloqueados o pendientes, espere hasta que desaparezca.<!-- SCCMDocs#1792 -->

- En el sitio de envío, revise el archivo **sender.log**.
- En el sitio de recepción, revise el archivo **despooler.log**.

### <a name="install-all-applicable-critical-windows-updates"></a>Instale todas las actualizaciones de Windows críticas aplicables

Antes de instalar una actualización para Configuration Manager, instale las actualizaciones críticas del sistema operativo para cada sistema de sitio aplicable. Estos servidores incluyen el servidor de sitio, el servidor de base de datos de sitio y los roles de sistema de sitio remoto. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los servidores correspondientes antes de iniciar la actualización.

### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Deshabilite las réplicas de la base de datos para los puntos de administración en los sitios primarios

Configuration Manager no puede actualizar correctamente un sitio primario que tiene habilitada una réplica de base de datos para puntos de administración. Antes de instalar una actualización de Configuration Manager deshabilite la replicación de base de datos.

Para obtener más información, vea [Réplicas de bases de datos para puntos de administración ](../deploy/configure/database-replicas-for-management-points.md).

### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Establecer los grupos de disponibilidad AlwaysOn de SQL Server en conmutación por error manual

Si usa un grupo de disponibilidad, asegúrese de que está establecido para la conmutación por error manual antes de iniciar la instalación de la actualización. Después de actualizar el sitio, puede restaurar la conmutación por error a automática. Para obtener más información, vea  [Prepararse para usar SQL Server Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="disable-site-maintenance-tasks-at-each-site"></a>Deshabilitar las tareas de mantenimiento de sitio en cada sitio

Antes de instalar la actualización, deshabilite cualquier tarea de mantenimiento del sitio que pueda estar en ejecución mientras el proceso de actualización esté activo. Por ejemplo, entre otros:

- Copia de seguridad del servidor del sitio
- Eliminar operaciones cliente antiguas
- Eliminar datos de detección antiguos

Cuando se ejecuta una tarea de mantenimiento de la base de datos de sitio durante la instalación de la actualización, se puede producir un error en la instalación de la actualización. Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de instalar la actualización.

Para obtener más información, vea  [Tareas de mantenimiento](maintenance-tasks.md)  y [Referencia de las tareas de mantenimiento](reference-for-maintenance-tasks.md).

### <a name="temporarily-stop-any-antivirus-software"></a>Detener temporalmente cualquier software antivirus

Antes de actualizar un sitio, detenga el software antivirus en los servidores de Configuration Manager. El software antivirus puede bloquear algunos archivos que deben actualizarse, lo que provoca que la actualización no pueda llevarse a cabo. <!--SMS.503481-->

### <a name="create-a-backup-of-the-site-database"></a>Crear una copia de seguridad de la base de datos de sitio

Antes de actualizar el sitio, haga una copia de seguridad de la base de datos del sitio en el sitio de administración central y los sitios primarios. Esta copia de seguridad garantiza la disponibilidad de una copia de seguridad correcta para su uso para la recuperación ante desastres.

Para obtener más información, vea  [Hacer una copia de seguridad de sitios](backup-and-recovery.md).

### <a name="back-up-customized-files"></a>Copia de seguridad de archivos personalizados

Si usted o un producto de terceros personaliza cualquier archivo de configuración Configuration Manager, guarde una copia de las personalizaciones.

Pongamos por ejemplo que agrega entradas personalizadas al archivo **osdinjection.xml** en la carpeta `bin\X64` del directorio de instalación de Configuration Manager. Después de actualizar Configuration Manager, estas personalizaciones no se conservan. Es necesario volver a aplicar las personalizaciones.

### <a name="plan-for-client-piloting"></a>Plan piloto de cliente

Al instalar una actualización del sitio que también actualiza el cliente, pruebe esa nueva actualización del cliente en preproducción antes de actualizar todos los clientes de producción. Para usar esta opción, configure el sitio para que admita las actualizaciones automáticas de preproducción antes de comenzar la instalación de la actualización.

Para obtener más información, vea  [Actualizar clientes](../../clients/manage/upgrade/upgrade-clients.md)  y [Probar actualizaciones de cliente en una recopilación de preproducción](../../clients/manage/upgrade/test-client-upgrades.md).

### <a name="plan-to-use-service-windows"></a>Planear el uso de períodos para tareas administrativas

Para definir un período durante el cual se pueden instalar las actualizaciones de un servidor de sitio para ventanas de servicio. Esto puede ayudarle a controlar el momento en que los sitios de la jerarquía instalan la actualización. Para obtener más información, vea  [Ventanas de servicio para servidores de sitio](service-windows.md).

### <a name="review-supported-extensions"></a>Revisar extensiones compatibles

<!--SCCMdocs#587-->
Si amplía Configuration Manager con otros productos de Microsoft o de asociados de Microsoft, confirme que son compatibles con la versión 2006. Para ello, consulte al proveedor del producto. Por ejemplo, vea las [notas de la versión](../../../mdt/release-notes.md) de Microsoft Deployment Toolkit.

### <a name="remove-intune-subscription-hybrid-mdm"></a>Quitar la suscripción a Intune (MDM híbrida)

<!-- SCCMDocs-pr#4253 -->
La oferta de servicio de MDM híbrida se retirará a partir del 1 de septiembre de 2019. Si el sitio de Configuration Manager tenía una suscripción de Microsoft Intune, deberá quitarla. Para más información, vea [Quitar MDM híbrida](../../../mdm/understand/what-happened-to-hybrid.md#remove-hybrid-mdm).

### <a name="run-the-setup-prerequisite-checker"></a>Ejecutar el Comprobador de requisitos previos del programa de instalación

Cuando la actualización aparece en la consola como **Disponible**, puede ejecutar el Comprobador de requisitos previos antes de instalar la actualización. (Al instalar la actualización en el sitio, el Comprobador de requisitos previos vuelve a ejecutarse).

Para ejecutar una comprobación de requisitos previos desde la consola, vaya al área de trabajo **Administración** y seleccione **Actualizaciones y mantenimiento**. Seleccione el paquete de actualización **Configuration Manager 2006** y haga clic en **Ejecutar comprobación de requisitos previos** en la cinta.

Para obtener más información, consulte **Ejecutar el comprobador de requisitos previos antes de instalar una actualización** en [Antes de instalar una actualización de la consola](install-in-console-updates.md#bkmk_beforeinstall).

> [!IMPORTANT]  
> Cuando se ejecuta el comprobador de requisitos previos, el proceso actualiza algunos archivos de origen del producto que se utilizan para tareas de mantenimiento del sitio. Por tanto, después de ejecutar el comprobador de requisitos previos, pero antes de instalar la actualización, si necesita realizar una tarea de mantenimiento del sitio, ejecute  **Setupwpf.exe**  (programa de instalación de Configuration Manager) desde la carpeta CD.Latest en el servidor de sitio.

### <a name="update-sites"></a>Actualizar sitios

Ya tiene todo listo para iniciar la instalación de la actualización de la jerarquía. Para obtener más información sobre la instalación de la actualización, consulte [Instalación de actualizaciones en la consola](install-in-console-updates.md#bkmk_install).

Es posible que planee instalar la actualización fuera de las horas comerciales normales. Determine cuándo tendrá menos efecto el proceso en sus operaciones empresariales. Si instala la actualización y sus acciones, se vuelven a instalar los componentes de sitio y los roles de sistema de sitio.

Para obtener más información, vea  [Actualizaciones para Configuration Manager](updates.md).

## <a name="post-update-checklist"></a>Lista de comprobación posterior a la actualización

Después de las actualizaciones de sitio, use la siguiente lista de comprobación para completar tareas y configuraciones comunes.

### <a name="confirm-version-and-restart-if-necessary"></a>Confirme la versión y reinicie (si es necesario).

Asegúrese de que cada servidor de sitio y cada rol de sistema de sitio está actualizado a la versión 2006. En la consola, agregue la columna **Versión** a los nodos **Sitios** y **Puntos de distribución** en el área de trabajo **Administración**. Cuando sea necesario, un rol de sistema de sitio se reinstalará automáticamente para actualizar a la nueva versión.

Considere la posibilidad de reiniciar los sistemas de sitio remoto que no se actualizan correctamente. Revise la infraestructura del sitio y asegúrese de que los servidores de sitios y los servidores de sistema de sitio remoto aplicables se han reiniciado correctamente. Normalmente, los servidores de sitio se reinician solo si Configuration Manager instala .NET como un requisito previo para un rol de sistema de sitio.

### <a name="confirm-site-to-site-replication-is-active"></a>Confirmar que la replicación de sitio a sitio está activa

En la consola de Configuration Manager, vaya a las ubicaciones siguientes para ver el estado y asegurarse de que la replicación esté activa:  

- Área de trabajo **Supervisión**, nodo **Jerarquía de sitios**  

- Área de trabajo **Supervisión**, **nodo Replicación de base de datos**  

Vea los siguientes artículos para más información:  

- [Supervisar la infraestructura de la jerarquía y replicación](monitor-hierarchy.md)
- [Información sobre Replication Link Analyzer](monitor-replication.md#BKMK_RLA)  

### <a name="update-configuration-manager-consoles"></a>Actualizar consolas de Configuration Manager

Actualice todas las consolas de Configuration Manager remotas a la misma versión. Se le pedirá que actualice la consola:  

- Cuando abre la consola.  

- Cuando se desplaza a un nuevo nodo en la consola.  

### <a name="reconfigure-database-replicas-for-management-points"></a>Volver a configurar réplicas de base de datos para puntos de administración

Después de actualizar un sitio primario, vuelva a configurar la réplica de base de datos de los puntos de administración que desinstaló antes de actualizar el sitio. Para obtener más información, vea [Réplicas de bases de datos para puntos de administración ](../deploy/configure/database-replicas-for-management-points.md).  

### <a name="reconfigure-sql-server-alwayson-availability-groups"></a>Volver a configurar los grupos de disponibilidad AlwaysOn de SQL Server

Si usa un grupo de disponibilidad, restablezca la configuración de conmutación por error en automática. Para obtener más información, consulte [SQL Server AlwaysOn para una base de datos de sitio](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).<!-- SCCMDocs #1366 -->

### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Volver a configurar las tareas de mantenimiento deshabilitadas

Si ha deshabilitado las [tareas de mantenimiento](maintenance-tasks.md) de bases de datos en un sitio antes de instalar la actualización, vuelva a configurar esas tareas. Use la misma configuración que había antes de la actualización.  

### <a name="update-clients"></a>Actualización de clientes

Actualice los clientes de acuerdo con el plan que ha creado, especialmente si ha configurado el proyecto piloto del cliente antes de instalar la actualización. Para obtener más información, consulte [How to upgrade clients for Windows computers (Cómo actualizar clientes para equipos Windows)](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

### <a name="third-party-extensions"></a>Extensiones de terceros

Si usa extensiones en Configuration Manager, actualícelas a la última versión para admitir la versión 2006 de Configuration Manager.

### <a name="update-custom-boot-images-and-media"></a>Actualización de medios e imágenes de arranque personalizados

<!--SCCMDocs issue 775-->

Use la acción **Actualizar puntos de distribución** para cualquier imagen de arranque que emplee, ya sea una imagen de arranque personalizada o predeterminada. Esta acción garantiza que los clientes puedan usar la versión más reciente. Incluso si no hay una nueva versión de Windows ADK, los componentes de cliente de Configuration Manager pueden cambiar con una actualización. Si no actualiza los medios y las imágenes de arranque, se puede producir un error en las implementaciones de secuencia de tareas en los dispositivos.

Al actualizar el sitio, Configuration Manager actualiza automáticamente las imágenes de arranque *predeterminadas*. No distribuye automáticamente el contenido actualizado en puntos de distribución. Use la acción **Actualizar puntos de distribución** en las imágenes de arranque específicas cuando esté listo para distribuir contenido a través de la red.

Tras actualizar el sitio, actualice manualmente las imágenes de arranque *personalizadas*. Esta acción actualiza la imagen de arranque con los componentes de cliente más recientes si fuera necesario, vuelve a cargarla opcionalmente con la versión actual de Windows PE y redistribuye el contenido a los puntos de distribución.

Para obtener más información, vea [Actualización de puntos de distribución con la imagen](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).
