---
title: Lista de comprobación de 1602
titleSuffix: Configuration Manager
description: Sepa lo que debe hacer antes de actualizar la versión 1511 de Configuration Manager a la versión 1602.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b330c4049dce06b1e47d1088993b09ec16e724a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700263"
---
# <a name="checklist-for-installing-update-1602-for-configuration-manager"></a>Lista de comprobación para la instalación de la actualización 1602 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de actualizar de la versión 1511 a la versión 1602 de Configuration Manager, revise la información y la lista de comprobación siguientes para conocer los pasos que hay que realizar antes de iniciar la actualización.  

 **Acerca de cómo instalar la actualización 1602:**  

 La actualización 1602 solo puede instalarse en el sitio de primer nivel de la jerarquía. Esto significa que, si existe, la instalación se inicia desde el sitio de administración central, o bien desde el sitio principal independiente.  

-   Los sitios primarios secundarios realizan la instalación de la actualización automáticamente después de que el sitio de administración central termine de instalarla. Puede utilizar ventanas de mantenimiento para controlar el momento en que un sitio instala actualizaciones. A partir de la versión de la actualización 1602, las ventanas de mantenimiento han pasado a denominarse *períodos para tareas administrativas*. Para más información, vea [Ventanas de servicio para servidores de sitio](service-windows.md).  

-   Una vez que el sitio principal primario termine de instalar la actualización, tendrá que actualizar manualmente los sitios secundarios desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.  

Cuando el servidor de sitio instala la actualización, los roles de sistema de sitio instalados en el servidor de sitio y aquellos instalados en los equipos remotos se actualizan automáticamente. Por lo tanto, antes de instalar la actualización, asegúrese de que cada servidor de sistema de sitio cumpla los requisitos previos nuevos de funcionamiento con la nueva versión de la actualización.  

La primera vez que use una consola de Configuration Manager una vez que la actualización haya terminado, se le pedirá que actualice dicha consola. Para ello, debe ejecutar el programa de instalación de Configuration Manager en el equipo que hospede la consola y seleccionar la opción para actualizarla. Se recomienda no retrasar la instalación de la actualización de la consola.  

 **Lista de comprobación:**  

 **Asegurarse de que todos los sitios ejecutan una versión compatible de Configuration Manager:**  Cada servidor de sitio de la jerarquía debe ejecutar la versión 1511 de Configuration Manager antes de iniciar la instalación de la actualización 1602.  

 **Revisar las versiones instaladas de Microsoft .NET en los servidores de sistema de sitio:** cuando un sitio instala la actualización 1602, Configuration Manager instala .NET Framework 4.5.2 de forma automática en todos los equipos que hospeden alguno de los roles de sistema de sitio siguientes (si todavía no está instalado .NET Framework 4.5 o una versión posterior):  

-   Punto de proxy de inscripción  

-   Punto de inscripción  

-   Punto de administración  

-   Punto de conexión de servicio  

Esta instalación puede poner el servidor de sistema de sitio en un estado pendiente de reinicio y notificar errores en el visor de estado de componentes de Configuration Manager. Además, las aplicaciones .NET del servidor pueden experimentar errores aleatorios hasta que se reinicie el servidor.  

 Para obtener más información, consulte [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  

 **Revise el estado del sitio y de la jerarquía y compruebe que no hay problemas sin resolver:** Antes de actualizar un sitio, resuelva todos los problemas de funcionamiento para el servidor del sitio, el servidor de base de datos del sitio y los roles del sistema de sitio instalados en los equipos remotos. Una actualización del sitio puede generar errores debido a problemas de funcionamiento existentes.  

Para más información, vea [Usar alertas y el sistema de estado de Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Revisar la replicación de datos y archivos entre sitios:**  Asegúrese de que la replicación de archivos y base de datos entre sitios funciona y está actualizada. Los retrasos o los trabajos pendientes pueden impedir una actualización correcta y sin problemas.    

Para la replicación de base de datos, puede utilizar Replication Link Analyzer para ayudar a resolver problemas antes de iniciar la actualización.    

 Para obtener más información, vea [Acerca de Replication Link Analyzer](monitor-replication.md#BKMK_RLA).  

 **Instalar todas las actualizaciones críticas aplicables de los sistemas operativos en los equipos que hospedan el sitio, el servidor de base de datos del sitio y los roles del sistema de sitio remoto:** Antes de instalar una actualización para Configuration Manager, instale las actualizaciones críticas para cada sistema de sitio aplicable. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los equipos correspondientes antes de iniciar la actualización.  

 **Deshabilite las réplicas de la base de datos para los puntos de administración en los sitios primarios:** Configuration Manager no puede actualizar correctamente un sitio primario que tiene habilitada una réplica de base de datos para puntos de administración. Deshabilite la replicación de base de datos antes de:  

-   Crear una copia de seguridad de la base de datos del sitio para probar la actualización de la base de datos.  

-   Instalar una actualización de Configuration Manager.  

Para más información, vea [Réplicas de bases de datos para puntos de administración de Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Vuelva a configurar los puntos de actualización de software que usan NLB:** Configuration Manager no puede actualizar un sitio que usa un clúster de equilibrio de carga de red (NLB) para hospedar puntos de actualización de software.  Si utiliza clústeres NLB para puntos de actualización de software, use Windows PowerShell para quitar el clúster NLB.    

 Para obtener más información, vea [Planear actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md).  

 **Deshabilitar todas las tareas de mantenimiento del sitio en cada sitio mientras dure la instalación de la actualización en ese sitio:** antes de instalar la actualización, deshabilite cualquier tarea de mantenimiento del sitio que pueda estar en ejecución mientras el proceso de actualización está activo. Entre estas tareas se incluyen las siguientes:  

-   Copia de seguridad del servidor del sitio  

-   Eliminar operaciones cliente antiguas  

-   Eliminar datos de detección antiguos  

Cuando se ejecuta una tarea de mantenimiento de la base de datos de sitio durante la instalación de la actualización, se puede producir un error en la instalación de la actualización. Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de que se haya instalado la actualización.  

 Para más información, vea [Tareas de mantenimiento de Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) y [Referencia de tareas de mantenimiento de Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Detener el software antivirus en los servidores de Configuration Manager:** antes de actualizar un sitio, asegúrese de que ha detenido el software antivirus en los servidores de Configuration Manager. <!--SMS.503481--> 

 **Cree una copia de seguridad de la base de datos del sitio en el sitio de administración central y los sitios primarios:** antes de actualizar un sitio, haga una copia de seguridad de la base de datos del sitio para asegurarse de que dispone de una copia de seguridad preparada para la recuperación ante desastres.   

Para más información, vea [Copia de seguridad y recuperación de Configuration Manager](backup-and-recovery.md).  

 **Realizar una copia de seguridad de un archivo Configuration.mof personalizado:** si usa un archivo Configuration.mof personalizado para definir clases de datos que se usan con el inventario de hardware, cree una copia de seguridad de este archivo antes de actualizar el sitio. Tras la actualización, restaure este archivo al sitio de la versión 1602. Al actualizar un sitio, se sobrescribe el archivo actual con la versión original (predeterminada) del archivo. Para más información sobre cómo usar este archivo, vea [Cómo ampliar el inventario de hardware](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Probar la actualización de la base de datos en una copia de la última copia de seguridad de la base de datos del sitio:** Antes de actualizar un sitio primario o un sitio de administración central de Configuration Manager, pruebe el proceso de actualización de la base de datos del sitio en una copia de la base de datos del sitio.  

-   Debe probar el proceso de actualización de base de datos del sitio porque, al actualizar un sitio, la base de datos del sitio podría modificarse.  

-   Aunque no es necesario actualizar la base de datos de prueba, puede identificar problemas de actualización antes de que la de producción se vea afectada.  

-   Una actualización incorrecta de la base de datos, podría inutilizar la base de datos del sitio, en cuyo caso podría requerirse una recuperación del sitio para recuperar la funcionalidad.  

-   Aunque se trate de una base de datos de sitio compartida entre varios sitios de una jerarquía, planee la prueba de la base de datos en cada uno de los sitios correspondientes antes de actualizar el sitio.  

-   Si utiliza réplicas de base de datos para puntos de administración en un sitio primario, deshabilite la replicación antes de crear la copia de seguridad de la base de datos del sitio.  

Configuration Manager no admite la realización de copias de seguridad de sitios secundarios ni la actualización de prueba de una base de datos de un sitio secundario.   
No ejecute una actualización de base de datos de prueba en la base de datos del sitio de producción. Esta acción actualiza la base de datos del sitio y podría inutilizar el sitio. Para más información, vea [Paso 2: ejecutar el comprobador de requisitos previos antes de instalar una actualización](install-in-console-updates.md#bkmk_step2) de **Antes de instalar una actualización en la consola**.  

 **Plan piloto de cliente:** Al instalar una actualización que actualiza el cliente, puede probar esa nueva actualización de cliente en preproducción antes de implementar y actualizar todos los clientes activos.   

 Para aprovechar las ventajas de esta opción, debe configurar el sitio para que admita las actualizaciones automáticas de preproducción antes de comenzar la instalación de la actualización. Para más información, vea [Actualizar clientes](../../../core/clients/manage/upgrade/upgrade-clients.md) y   
[Cómo probar las actualizaciones de cliente en una recopilación de preproducción](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planear usar ventanas de mantenimiento para controlar el momento en que los servidores de sitio instalan actualizaciones:** puede usar las ventanas de mantenimiento para definir un período durante el cual se pueden instalar las actualizaciones de un servidor de sitio. Esto puede ayudarle a controlar el momento en que los sitios de la jerarquía instalan la actualización.   

A partir de la versión de la actualización 1602, las ventanas de mantenimiento han pasado a denominarse *períodos para tareas administrativas*. Para más información, vea [Ventanas de servicio para servidores de sitio](service-windows.md).  

 **Ejecutar el comprobador de requisitos previos del programa de instalación**:  antes de instalar la actualización 1602, puede ejecutar el Comprobador de requisitos previos independientemente de la instalación de la actualización. Al instalar la actualización en el sitio, el Comprobador de requisitos previos vuelve a ejecutarse.  

Para más información, vea **Paso 3: Ejecutar el comprobador de requisitos previos antes de instalar una actualización** en el tema [Actualizaciones de Configuration Manager](../../../core/servers/manage/updates.md).  

> [!IMPORTANT]  
>  Cuando se ejecuta el Comprobador de requisitos previos de forma independiente o como parte de la instalación de una actualización, el proceso actualiza algunos archivos de origen del producto que se utilizan para tareas de mantenimiento del sitio. Por lo tanto, después de ejecutar el Comprobador de requisitos previos, pero antes de instalar la actualización 1602, si necesita realizar una tarea de mantenimiento del sitio, ejecute **Setupwfe.exe** (programa de instalación de Configuration Manager) desde la carpeta CD.Latest en el servidor de sitio.  

 **Actualizar sitios:** Ya está listo para iniciar la instalación de la actualización de la jerarquía. Se recomienda planear la instalación de la actualización fuera del horario comercial habitual de cada sitio, ya que será el momento en que el proceso de instalación de la actualización y sus acciones para volver a instalar los componentes del sitio y los roles de sistema de sitio afectarán menos a las operaciones comerciales.

Para obtener más información, vea [Actualizaciones para Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Vea también  
 [Actualizaciones para Configuration Manager](../../../core/servers/manage/updates.md)
