---
title: Lista de comprobación de 1710 | Configuration Manager
titleSuffix: Configuration Manager
description: Sepa lo que debe hacer antes de actualizar a la versión 1710 de Configuration Manager.
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e8ab8ca-41ef-467a-943b-a115d88cafe0
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fd3e067577a7f89c02727ccd490ef6d1eb26ca98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707753"
---
# <a name="checklist-for-installing-update-1710-for-configuration-manager"></a>Lista de comprobación para la instalación de la actualización 1710 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Si usa la rama actual de Configuration Manager, puede instalar la actualización en consola de la versión 1710 a fin de actualizar la jerarquía desde una versión anterior.

Para obtener la actualización de la versión 1710, debe usar un rol de sistema de sitio de punto de conexión del servicio en el sitio de nivel superior de su jerarquía. Esto puede realizarse en el modo en línea o sin conexión. Después de que su jerarquía descargue el paquete de actualización de Microsoft, lo podrá encontrar en la consola, en **Administración &gt; Información general &gt; Cloud Services &gt; Actualizaciones y mantenimiento**.

-   Cuando la actualización aparezca como **Disponible**, ya está lista para instalarse. Antes de instalar la versión 1710, revise la siguiente información [sobre la instalación de la actualización 1710](#about-installing-update-1710) y la [lista de comprobación](#checklist) de las configuraciones que deben realizarse antes de iniciar la actualización.

-   Si la actualización se muestra como **Descargando** y no cambia, revise los archivos **hman.log** y **dmpdownloader.log** para ver los errores.

    -   Si el registro dmpdownloader.log indica que el proceso de dmpdownloader está suspendido y a la espera de un intervalo antes de comprobar las actualizaciones, puede reiniciar el servicio **SMS_Executive** en el servidor de sitio para reiniciar la descarga de los archivos de redistribución de la actualización.

    -   Otro problema común de descarga se produce cuando la configuración del servidor proxy impide descargas desde `silverlight.dlservice.microsoft.com` y `download.microsoft.com`.

Para obtener más información sobre la instalación de actualizaciones, consulte [Actualizaciones y servicio en la consola](updates.md#bkmk_inconsole).

Para más información sobre las versiones de la rama actual, vea [Versiones de línea de base y versiones de actualización](updates.md#bkmk_Baselines) en [Actualizaciones de Configuration Manager](updates.md).

## <a name="about-installing-update-1710"></a>Acerca de la instalación de la actualización 1710

**Sitios:**  
La actualización 1710 se instala en el sitio de primer nivel de la jerarquía. Esto significa que, si existe, la instalación se inicia desde el sitio de administración central, o bien desde el sitio principal independiente. Después de instalar la actualización en el sitio de nivel superior, los sitios secundarios tienen el siguiente comportamiento de actualización:

-   Los sitios primarios secundarios inician la instalación de la actualización automáticamente después de que el sitio de administración central termine de instalarla. Puede usar períodos para tareas administrativas para controlar el momento en que un sitio instala la actualización. Para más información, vea [Ventanas de servicio para servidores de sitio](service-windows.md).

-   Una vez que el sitio principal primario termine de instalar la actualización, tendrá que actualizar manualmente cada sitio secundario desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.

**Roles de sistema de sitio:**  
Cuando un servidor de sitio instala la actualización, los roles de sistema de sitio instalados en el equipo del servidor de sitio y aquellos instalados en los equipos remotos se actualizan automáticamente. Antes de instalar la actualización, asegúrese de que cada servidor de sistema de sitio cumpla los requisitos previos de funcionamiento con la nueva versión de la actualización.

**Consolas de Configuration Manager:**    
La primera vez que use una consola de Configuration Manager una vez que la actualización haya terminado, se le pedirá que actualice esa consola. Para ello, debe ejecutar el programa de instalación de Configuration Manager en el equipo que hospeda la consola y, luego, seleccionar la opción para actualizarla. Se recomienda no retrasar la instalación de la actualización de la consola.

> [!IMPORTANT]  
> Cuando instala una actualización en el sitio de administración central, tenga en cuenta las siguientes limitaciones y retrasos que existen hasta que todos los sitios primarios secundarios también completan la instalación de la actualización:    
> - **Las actualizaciones de cliente** no se inician. Esto incluye las actualizaciones automáticas de los clientes y los clientes de preproducción. Además, no se puede promover a los clientes de preproducción a producción hasta que el último sitio completa la instalación de la actualización. Después de que el último sitio completa la instalación de la actualización, las actualizaciones de cliente comenzarán en función de las opciones de configuración.   
> - Las **nuevas características** habilitadas con la actualización no están disponibles. Esto es para evitar que la replicación de datos relacionados con esa característica se envíe a un sitio que no ha instalado aún la compatibilidad para esta característica. Después de que todos los sitios primarios instalan la actualización, la característica estará disponible para su uso.   
> - Los **vínculos de replicación** entre el sitio de administración central y los sitios primarios secundarios se muestran como no actualizados. Esto se muestra en el estado de instalación del paquete de actualización como estado completado con la advertencia Supervisando inicialización de replicación. En el nodo Supervisión de la consola, se muestra como *El vínculo en configuración*.


## <a name="checklist"></a>Lista de comprobación

**Asegurarse de que todos los sitios ejecutan una versión de Configuration Manager que admite la actualización a 1710:**    
Para poder iniciar la instalación de la actualización 1710, cada servidor de sitio de la jerarquía debe ejecutar la misma versión de Configuration Manager. Para actualizar a 1710, debe usar la versión 1610, 1702 o 1706.

**Revisar el estado de Software Assurance o de los derechos de suscripción equivalentes:**    
Debe tener un contrato de Software Assurance (SA) activo para instalar la actualización 1710. Al instalar esta actualización, en la pestaña **Licencias** se ofrece la opción de confirmar la **Fecha de expiración de Software Assurance**.

Este es un valor opcional que puede especificar como un recordatorio útil de la fecha de expiración de la licencia. Esta fecha está visible cuando se instalan las actualizaciones futuras. Puede que haya especificado este valor anteriormente durante la configuración o instalación de una actualización, o en la pestaña **Licencias** de la **Configuración de jerarquía** de la consola de Configuration Manager.

Para más información, vea [Licencias y ramas de Configuration Manager](../../understand/learn-more-editions.md).

**Revisar las versiones instaladas de Microsoft .NET en los servidores de sistema de sitio:** cuando un sitio instala esta actualización, Configuration Manager instala .NET Framework 4.5.2 de forma automática en todos los equipos que hospeden alguno de los roles de sistema de sitio siguientes, si todavía no está instalado .NET Framework 4.5 o una versión posterior:

-   Punto de proxy de inscripción
-   Punto de inscripción
-   Punto de administración
-   Punto de conexión de servicio

Esta instalación puede poner el servidor de sistema de sitio en un estado pendiente de reinicio y notificar los errores al visor de estado de los componentes de Configuration Manager. Además, las aplicaciones .NET del servidor pueden experimentar errores aleatorios hasta que se reinicie el servidor.

Para obtener más información, consulte [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).

**Revisar la versión de Windows Assessment and Deployment Kit (ADK) para Windows 10**: Windows 10 ADK debe tener la versión 1703 o posterior. Para obtener más información sobre las versiones de Windows ADK admitidas, consulte [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Si es necesario actualizar Windows ADK, hágalo antes de comenzar la actualización de Configuration Manager. Esto garantiza que las imágenes de arranque predeterminadas se actualicen automáticamente a la última versión de Windows PE. (Las imágenes de arranque personalizadas deben actualizarse manualmente).

Si actualiza el sitio antes que Windows ADK, consulte [Actualización de puntos de distribución con la imagen](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image) para conocer las mejoras aplicadas a este proceso en la versión 1710 de Configuration Manager.

**Revise el estado del sitio y de la jerarquía y compruebe que no hay problemas sin resolver:** Antes de actualizar un sitio, resuelva todos los problemas de funcionamiento para el servidor del sitio, el servidor de base de datos del sitio y los roles del sistema de sitio instalados en los equipos remotos. Una actualización del sitio puede generar errores debido a problemas de funcionamiento existentes.

Para más información, vea [Usar alertas y el sistema de estado de Configuration Manager](use-alerts-and-the-status-system.md).

**Revisar la replicación de datos y archivos entre sitios:**    
Asegúrese de que la replicación de archivos y base de datos entre sitios funciona y está actualizada. Los retrasos o los trabajos pendientes pueden impedir una actualización correcta y sin problemas.
Para la replicación de base de datos, puede utilizar Replication Link Analyzer para ayudar a resolver problemas antes de iniciar la actualización.

Para más información, vea [Replication Link Analyzer](monitor-replication.md#BKMK_RLA) en el tema [Supervisión de la replicación de base de datos](monitor-replication.md#BKMK_RLA).

**Instale todas las actualizaciones críticas aplicables de los sistemas operativos en los equipos que hospedan el sitio, el servidor de base de datos del sitio y los roles del sistema de sitio remoto:** Antes de instalar una actualización para Configuration Manager, instale las actualizaciones críticas para cada sistema de sitio aplicable. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los equipos correspondientes antes de iniciar la actualización.

**Deshabilitar las réplicas de la base de datos para los puntos de administración en los sitios primarios:**    
Configuration Manager no puede actualizar correctamente un sitio primario que tiene habilitada una réplica de base de datos para puntos de administración. Deshabilite la replicación de base de datos antes de instalar una actualización de Configuration Manager.

Para más información, vea [Réplicas de bases de datos para puntos de administración de Configuration Manager](../deploy/configure/database-replicas-for-management-points.md).

**Establecer los grupos de disponibilidad AlwaysOn de SQL Server en la conmutación por error manual:**    
Si utiliza un grupo de disponibilidad, asegúrese de que dicho grupo está establecido para la conmutación por error manual antes de iniciar la instalación de la actualización. Después de actualizar el sitio, puede restaurar la conmutación por error a automática. Para obtener más información, consulte [SQL Server AlwaysOn para una base de datos de sitio](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Volver a configurar los puntos de actualización de software que usan NLB:**    
<!-- Support for NLBs is fully removed with 1702. When 1702 is no longer in support, this statement can drop -->
Configuration Manager no puede actualizar un sitio que usa un clúster de equilibrio de carga de red (NLB) para hospedar puntos de actualización de software.

Si utiliza clústeres NLB para puntos de actualización de software, use Windows PowerShell para quitar el clúster NLB.
Para obtener más información, vea [Planear actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md).

**Deshabilitar todas las tareas de mantenimiento del sitio en cada sitio mientras dure la instalación de la actualización en ese sitio:**    
Antes de instalar la actualización, deshabilite cualquier tarea de mantenimiento del sitio que pueda estar en ejecución mientras el proceso de actualización esté activo. Esto incluye, entre otras cosas, lo siguiente:

-   Copia de seguridad del servidor del sitio
-   Eliminar operaciones cliente antiguas
-   Eliminar datos de detección antiguos

Cuando se ejecuta una tarea de mantenimiento de la base de datos de sitio durante la instalación de la actualización, se puede producir un error en la instalación de la actualización. Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de instalar la actualización.

Para más información, vea [Tareas de mantenimiento de Configuration Manager](maintenance-tasks.md) y [Referencia de tareas de mantenimiento de Configuration Manager](reference-for-maintenance-tasks.md).

**Detener el software antivirus en los servidores de Configuration Manager:** antes de actualizar un sitio, asegúrese de que ha detenido el software antivirus en los servidores de Configuration Manager. <!--SMS.503481--> 

**Cree una copia de seguridad de la base de datos del sitio en el sitio de administración central y los sitios primarios:** antes de actualizar un sitio, haga una copia de seguridad de la base de datos del sitio para asegurarse de que dispone de una copia de seguridad preparada para la recuperación ante desastres.

Para más información, vea [Copia de seguridad y recuperación de Configuration Manager](backup-and-recovery.md).

**Plan piloto de cliente:**    
Al instalar una actualización que actualiza el cliente, puede probar esa nueva actualización de cliente en preproducción antes de implementar y actualizar todos los clientes activos.

Para aprovechar las ventajas de esta opción, debe configurar el sitio para que admita las actualizaciones automáticas de preproducción antes de comenzar la instalación de la actualización.

Para obtener más información, vea [Actualizar clientes](../../clients/manage/upgrade/upgrade-clients.md) y [Cómo probar las actualizaciones de cliente en una recopilación de preproducción](../../clients/manage/upgrade/test-client-upgrades.md).

**Planear usar períodos para tareas administrativas para controlar el momento en que los servidores de sitio instalan actualizaciones:**    
Use períodos para tareas administrativas para definir un período durante el cual se pueden instalar las actualizaciones de un servidor de sitio.

Esto puede ayudarle a controlar el momento en que los sitios de la jerarquía instalan la actualización. Para más información, vea [Ventanas de servicio para servidores de sitio](service-windows.md).

**Ejecutar el Comprobador de requisitos previos del programa de instalación:**    
Cuando la actualización aparece en la consola como **Disponible**, puede ejecutar de manera independiente el Comprobador de requisitos previos antes de instalar la actualización. (Al instalar la actualización en el sitio, el Comprobador de requisitos previos vuelve a ejecutarse).

Para ejecutar una comprobación de requisitos previos desde la consola, vaya a **Administración > Información general > Cloud Services > Actualizaciones y mantenimiento**. Luego, haga clic con el botón derecho en **Paquete de actualización 1710 de Configuration Manager** y, después, elija **Ejecutar comprobación de requisitos previos**.

Para más información sobre cómo iniciar y supervisar la comprobación de requisitos previos, consulte **Paso 3: Ejecutar el comprobador de requisitos previos antes de instalar una actualización** en el tema [Instalar actualizaciones en consola para Configuration Manager](install-in-console-updates.md).

> [!IMPORTANT]  
> Cuando se ejecuta el Comprobador de requisitos previos de forma independiente o como parte de la instalación de una actualización, el proceso actualiza algunos archivos de origen del producto que se utilizan para tareas de mantenimiento del sitio. Por lo tanto, después de ejecutar el Comprobador de requisitos previos, pero antes de instalar la actualización, si necesita realizar una tarea de mantenimiento del sitio, ejecute **Setupwpf.exe** (programa de instalación de Configuration Manager) desde la carpeta CD.Latest en el servidor de sitio.

**Actualizar sitios:**    
Ya está listo para iniciar la instalación de la actualización de la jerarquía. Para más información sobre la instalación de la actualización, consulte [Instalación de actualizaciones en la consola](install-in-console-updates.md#bkmk_install).

Se recomienda planear la instalación de la actualización fuera del horario comercial habitual de cada sitio, ya que será el momento en que el proceso de instalación de la actualización y sus acciones para volver a instalar los componentes del sitio y los roles de sistema de sitio afectarán menos a las operaciones comerciales.

Para obtener más información, vea [Actualizaciones para Configuration Manager](updates.md).

## <a name="post-update-checklist"></a>Lista de comprobación posterior a la actualización
Revise las acciones siguientes que deben realizarse una vez finalizada la instalación de la actualización.
1. Asegúrese de que la replicación de sitio a sitio está activa. En la consola, consulte **Supervisión** > **Jerarquía de sitios** y **Supervisión** > **Replicación de base de datos** para obtener indicaciones sobre problemas o una confirmación de que los vínculos de replicación están activos.
2. Asegúrese de que cada servidor de sitio y rol de sistema de sitio se ha actualizado a la versión 1710. En la consola, puede agregar la columna opcional **Versión** a la presentación de algunos nodos, como **Sitios** y **Puntos de distribución**.

   Cuando sea necesario, un rol de sistema de sitio se reinstalará automáticamente para actualizar a la nueva versión. Considere la posibilidad de reiniciar los sistemas de sitio remoto que no se actualizan correctamente.
3. Vuelva a configurar réplicas de base de datos para los puntos de administración de los sitios primarios que deshabilitó antes de iniciar la actualización.
4. Vuelva a configurar las tareas de mantenimiento de base de datos que deshabilitó antes de iniciar la actualización.
5. Si ha configurado el proyecto piloto del cliente antes de instalar la actualización, actualice los clientes en función del plan que ha creado.
