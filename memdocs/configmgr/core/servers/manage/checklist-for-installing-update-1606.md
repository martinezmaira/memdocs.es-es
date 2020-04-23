---
title: Lista de comprobación de 1606
titleSuffix: Configuration Manager
description: Sepa lo que debe hacer antes de actualizar la versión 1511 o 1602 de Configuration Manager a la versión 1606.
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 95da730a6978c235fcae6a1d05b7984486abdaeb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707413"
---
# <a name="checklist-for-installing-update-1606-for-configuration-manager"></a>Lista de comprobación para la instalación de la actualización 1606 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La versión 1606 de la rama actual de Configuration Manager es una actualización que se puede usar para actualizar desde la versión 1511 o 1602.

Antes de instalar la versión 1606 como una actualización, lea la información siguiente y la lista de comprobación para conocer los pasos necesarios antes del inicio de la actualización.

Para más información sobre las versiones de línea base, vea [Versiones de línea base y versiones de actualización](../../../core/servers/manage/updates.md#bkmk_Baselines) en [Actualizaciones de Configuration Manager](../../../core/servers/manage/updates.md).

## <a name="about-installing-update-1606"></a>Acerca de la instalación de la actualización 1606

Como *actualización*, 1606 solo puede instalarse en el sitio de nivel superior de la jerarquía. Esto significa que, si existe, la instalación se inicia desde el sitio de administración central, o bien desde el sitio principal independiente.  

- Los sitios primarios secundarios realizan la instalación de la actualización automáticamente después de que el sitio de administración central haya terminado de instalarla. Puede usar períodos para tareas administrativas para controlar el momento en que un sitio instala actualizaciones. Antes de la versión 1606, los períodos para tareas administrativas se denominaban ventanas de mantenimiento. Para más información, vea [Ventanas de servicio para servidores de sitio](service-windows.md).  

- Una vez que el sitio principal primario termine de instalar la actualización, tendrá que actualizar manualmente los sitios secundarios desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.  

Cuando el servidor de sitio instala la actualización, los roles de sistema de sitio instalados en el servidor de sitio y aquellos instalados en los equipos remotos se actualizan automáticamente. Por lo tanto, antes de instalar la actualización, asegúrese de que cada servidor de sistema de sitio cumpla los requisitos previos nuevos de funcionamiento con la nueva versión de actualización.  

La primera vez que use una consola de Configuration Manager una vez que la actualización se haya instalado, se le pedirá que actualice esa consola.  Para ello, debe ejecutar el programa de instalación de Configuration Manager en el equipo que hospede la consola y, luego, seleccionar la opción para actualizarla. Se recomienda no retrasar la instalación de la actualización de la consola.

**Problemas conocidos de esta actualización**   
En el estado de la instalación del paquete de actualización se pueden ver los siguientes problemas:
- Al actualizar desde la versión 1602 a la 1606, el paso **Extraer carga de paquete de actualización** muestra el estado **No iniciada**, aun cuando la descarga ha terminado.
- Al actualizar desde la versión 1511 a la 1606, algunos pasos mostrarán el estado **Completado**, pero no el valor de **Hora de la última actualización**.


## <a name="checklist"></a>Lista de comprobación  

**Asegurarse de que todos los sitios ejecutan una versión compatible de Configuration Manager:**  antes de empezar la instalación de la actualización 1606, cada servidor de sitio de la jerarquía debe ejecutar la misma versión de Configuration Manager, ya sea la versión 1511 o 1602.

**Revisar las versiones instaladas de Microsoft .NET en los servidores de sistema de sitio:** cuando un sitio instala la actualización 1606, Configuration Manager instala .NET Framework 4.5.2 de forma automática en todos los equipos que hospeden alguno de los roles de sistema de sitio siguientes (si todavía no está instalado .NET Framework 4.5 o una versión posterior):  

- Punto de proxy de inscripción  

- Punto de inscripción  

- Punto de administración  

- Punto de conexión de servicio  

Esta instalación puede poner el servidor de sistema de sitio en un estado pendiente de reinicio y notificar los errores al visor de estado de los componentes de Configuration Manager. Además, las aplicaciones .NET del servidor pueden presentar errores aleatorios hasta que se reinicia el servidor.  

Para obtener más información, consulte [Requisitos previos de sitio y sistema de sitio para System Center Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

**Revise el estado del sitio y de la jerarquía y compruebe que no hay problemas sin resolver:** Antes de actualizar un sitio, resuelva todos los problemas de funcionamiento para el servidor del sitio, el servidor de base de datos del sitio y los roles del sistema de sitio instalados en los equipos remotos. Una actualización del sitio puede generar errores debido a problemas de funcionamiento existentes.

Para más información, vea [Usar alertas y el sistema de estado de Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

**Revisar la replicación de datos y archivos entre sitios:**  Asegúrese de que la replicación de archivos y base de datos entre sitios funciona y está actualizada. Los retrasos o los trabajos pendientes pueden impedir una actualización correcta y sin problemas.    

Para la replicación de base de datos, puede utilizar Replication Link Analyzer para ayudar a resolver problemas antes de iniciar la actualización. Para obtener más información, vea [Acerca de Replication Link Analyzer](monitor-replication.md#BKMK_RLA).  


**Instalar todas las actualizaciones críticas aplicables de los sistemas operativos en los equipos que hospedan el sitio, el servidor de base de datos del sitio y los roles del sistema de sitio remoto:** Antes de instalar una actualización para Configuration Manager, instale las actualizaciones críticas para cada sistema de sitio aplicable. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los equipos correspondientes antes de iniciar la actualización.  

**Deshabilite las réplicas de la base de datos para los puntos de administración en los sitios primarios:** Configuration Manager no puede actualizar correctamente un sitio primario que tiene habilitada una réplica de base de datos para puntos de administración. Deshabilite la replicación de base de datos antes de instalar una actualización de Configuration Manager.  

Para más información, vea [Réplicas de bases de datos para puntos de administración de Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Establecer los grupos de disponibilidad AlwaysOn de SQL Server en conmutación por error manual:**  
Antes de instalar las actualizaciones, como la versión 1606, asegúrese de que el grupo de disponibilidad esté establecido para la conmutación por error manual. Después de actualizar el sitio, puede restaurar la conmutación por error a automática. Para obtener más información, consulte [SQL Server AlwaysOn para una base de datos de sitio](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Vuelva a configurar los puntos de actualización de software que usan NLB:** Configuration Manager no puede actualizar un sitio que usa un clúster de equilibrio de carga de red (NLB) para hospedar puntos de actualización de software.  

Si utiliza clústeres NLB para puntos de actualización de software, use Windows PowerShell para quitar el clúster NLB.    

Para obtener más información, vea [Planear actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md).  

**Deshabilitar todas las tareas de mantenimiento del sitio en cada sitio mientras dure la instalación de la actualización en ese sitio:** antes de instalar la actualización, deshabilite cualquier tarea de mantenimiento del sitio que pueda estar en ejecución mientras el proceso de actualización esté activo. Esto incluye, entre otras cosas, lo siguiente:  

- Copia de seguridad del servidor del sitio  

- Eliminar operaciones cliente antiguas  

- Eliminar datos de detección antiguos  

Cuando se ejecuta una tarea de mantenimiento de la base de datos de sitio durante la instalación de la actualización, se puede producir un error en la instalación de la actualización. Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de instalar la actualización.  

Para más información, vea [Tareas de mantenimiento de Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) y [Referencia de tareas de mantenimiento de Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Detener el software antivirus en los servidores de Configuration Manager:** antes de actualizar un sitio, asegúrese de que ha detenido el software antivirus en los servidores de Configuration Manager. <!--SMS.503481--> 

**Cree una copia de seguridad de la base de datos del sitio en el sitio de administración central y los sitios primarios:** antes de actualizar un sitio, haga una copia de seguridad de la base de datos del sitio para asegurarse de que dispone de una copia de seguridad preparada para la recuperación ante desastres.   

Para más información, vea [Copia de seguridad y recuperación de Configuration Manager](backup-and-recovery.md).  

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

- You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

- Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

- A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

- Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

- If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**Plan piloto de cliente:** Al instalar una actualización que actualiza el cliente, puede probar esa nueva actualización de cliente en preproducción antes de implementar y actualizar todos los clientes activos.   

Para aprovechar las ventajas de esta opción, antes de comenzar la instalación de la actualización, debe configurar el sitio para que admita las actualizaciones automáticas de preproducción. Para más información, vea [Actualizar clientes](../../../core/clients/manage/upgrade/upgrade-clients.md) y   
[Cómo probar las actualizaciones de cliente en una recopilación de preproducción](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**Planear usar períodos para tareas administrativas para controlar el momento en que los servidores de sitio instalan actualizaciones:** Puede usar períodos para tareas administrativas para definir un período durante el cual se pueden instalar las actualizaciones de un servidor de sitio.

Esto puede ayudarle a controlar el momento en que los sitios de la jerarquía instalan la actualización.
Antes de la versión 1606, los períodos para tareas administrativas se denominaban ventanas de mantenimiento. Para más información, vea [Ventanas de servicio para servidores de sitio](service-windows.md).  

**Ejecutar el comprobador de requisitos previos del programa de instalación**:  antes de instalar la actualización 1606, puede ejecutar el Comprobador de requisitos previos independientemente de la instalación de la actualización. Al instalar la actualización en el sitio, el Comprobador de requisitos previos vuelve a ejecutarse.  

Para más información, vea **Paso 3: Ejecutar el comprobador de requisitos previos antes de instalar una actualización** en el tema [Actualizaciones de Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

> [!IMPORTANT]  
> Cuando se ejecuta el Comprobador de requisitos previos de forma independiente o como parte de la instalación de una actualización, el proceso actualiza algunos archivos de origen del producto que se utilizan para tareas de mantenimiento del sitio. Por lo tanto, después de ejecutar el Comprobador de requisitos previos, pero antes de instalar la actualización 1606, si necesita realizar una tarea de mantenimiento del sitio, ejecute **Setupwpf.exe** (programa de instalación de Configuration Manager) desde la carpeta CD.Latest en el servidor de sitio.  

**Actualizar sitios:** Ya está listo para iniciar la instalación de la actualización de la jerarquía.  
Se recomienda planear la instalación de la actualización fuera del horario comercial habitual de cada sitio, ya que será el momento en que el proceso de instalación de la actualización y sus acciones para volver a instalar los componentes del sitio y los roles de sistema de sitio afectarán menos a las operaciones comerciales.

Para obtener más información, vea [Actualizaciones para Configuration Manager](../../../core/servers/manage/updates.md).  
