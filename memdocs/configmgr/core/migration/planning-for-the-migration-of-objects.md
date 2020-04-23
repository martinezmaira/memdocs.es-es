---
title: Migración de objetos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo planear la migración de objetos entre jerarquías en un entorno de la rama actual de Configuration Manager.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9777fb12a2d63a990587386ac33cb2749bf19a4e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702823"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Planear la migración de objetos de Configuration Manager a la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Con la rama actual de Configuration Manager, se pueden migrar muchos de los distintos objetos que están asociados con diferentes características que se encuentran en un sitio de origen.

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a> Plan para migrar actualizaciones de software  
 Puede migrar objetos de actualización de software, como paquetes de actualización de software e implementaciones de actualización de software.  

 Para migrar satisfactoriamente objetos de actualización de software, primero debe configurar la jerarquía de destino con configuraciones que coincidan con el entorno de jerarquía de origen. Esto requiere las siguientes acciones:  

-   Implementar un punto de actualización de software activo en la jerarquía de destino  

-   Configurar el catálogo de productos e idiomas para que coincida con la configuración de la jerarquía de origen  

-   Sincronizar el punto de actualización de software en la jerarquía de destino con Windows Server Update Services (WSUS)  

A la hora de migrar actualizaciones de software, tenga en cuenta lo siguiente:  

-   Se puede producir un error en la migración de objetos de actualización de software si no se ha sincronizado la información de la jerarquía de destino para que coincida con la configuración de la jerarquía de origen.  

    > [!WARNING]  
    >  Configuration Manager no permite usar la herramienta WSUSutil para sincronizar datos entre una jerarquía de origen y una de destino.  

-   No se pueden migrar actualizaciones personalizadas publicadas mediante System Center Updates Publisher. En su lugar, las actualizaciones personalizadas se deben volver a publicar en la jerarquía de destino.  

Cuando migre desde una jerarquía de origen de Configuration Manager 2007, el proceso de migración modificará algunos objetos de actualización de software al formato en uso en la jerarquía de destino. Utilice la tabla siguiente como ayuda para planear la migración de objetos de actualización de software de Configuration Manager 2007.  

|Objeto de Configuration Manager 2007|Nombre del objeto después de la migración|  
|-----------------------------------|---------------------------------|  
|Listas de actualizaciones de software|Las listas de actualizaciones de software se convierten en grupos de actualizaciones de software.|  
|Implementaciones de actualización de software|Las implementaciones de actualización de software se convierten en grupos de implementaciones y actualizaciones.<br /><br /> Después de migrar la implementación de una actualización de software desde Configuration Manager 2007, debe habilitarla en la jerarquía de destino para implementarla.|  
|Paquetes de actualización de software|Los paquetes de actualización de software continúan siendo paquetes de actualización de software.|  
|Plantillas de actualización de software|Las plantillas de actualización de software continúan siendo plantillas de actualización de software.<br /><br /> El valor **Duración** de las plantillas de implementación de Configuration Manager 2007 no se migra.|  

Al migrar objetos desde una jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, los objetos de las actualizaciones de software no se modifican.  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a> Plan para migrar contenido  
 Puede migrar contenido de una jerarquía de origen compatible a la jerarquía de destino. Para una jerarquía de origen de Configuration Manager 2007, este contenido incluye paquetes y programas de distribución de software y aplicaciones virtuales, como Microsoft Application Virtualization (App-V). En las jerarquías de origen de System Center 2012 Configuration Manager y de la rama actual de Configuration Manager, este contenido incluye aplicaciones y aplicaciones virtuales de App-V. Cuando se migra contenido entre jerarquías, son los archivos de origen comprimidos los que se migran a la jerarquía de destino.  

### <a name="packages-and-programs"></a>Paquetes y programas  
 Cuando se migran paquetes y programas, no se modifican por la migración. Pero antes de migrarlos, debe configurar cada paquete para usar una ruta de acceso de convención de nomenclatura universal (UNC) para su ubicación de archivo de origen. Como parte de la configuración para migrar paquetes y programas, es necesario asignar un sitio en la jerarquía de destino para administrar este contenido. El contenido no se migra desde el sitio asignado, pero después de la migración, el sitio asignado accede a la ubicación del archivo de origen original mediante la asignación de UNC.  

 Una vez migrados el paquete y el programa a la jerarquía de destino, y mientras la migración de la jerarquía de origen permanece activa, puede poner el contenido a disposición de los clientes en esa jerarquía mediante un punto de distribución compartido. Para utilizar un punto de distribución compartido, el contenido debe permanecer accesible en el punto de distribución del sitio de origen. Para más información sobre los puntos de distribución compartidos, vea [Compartir puntos de distribución entre jerarquías de origen y de destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) en [Planear una estrategia de migración de implementación de contenido](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 En cuanto al contenido migrado, si la versión del contenido cambia en la jerarquía de origen o en la de destino, los clientes ya no podrán acceder al mismo desde el punto de distribución compartido en la jerarquía de destino. En este escenario, debe volver a migrar el contenido para restaurar una versión coherente del paquete entre la jerarquía de origen y la jerarquía de destino. Esta información se sincroniza durante el ciclo de recopilación de datos.  

> [!TIP]  
>  Por cada paquete que vaya a migrar, actualice el paquete en la jerarquía de destino. Esto puede evitar problemas al implementar el paquete en puntos de distribución en la jerarquía de destino. Pero cuando se actualiza un paquete en el punto de distribución en la jerarquía de destino, los clientes de dicha jerarquía ya no podrán adquirir ese paquete desde un punto de distribución compartido. Para actualizar un paquete en la jerarquía de destino, en la consola de Configuration Manager, vaya a la biblioteca de software, haga clic con el botón derecho en el paquete y, luego, seleccione **Actualizar puntos de distribución**. Realice esta acción por cada paquete que haya migrado.  

> [!TIP]  
> Use el Administrador de conversión de paquetes para convertir paquetes y programas en aplicaciones de Configuration Manager. Para más información, vea [Administrador de conversión de paquetes](../../apps/pcm/package-conversion-manager.md).  

### <a name="virtual-applications"></a>Aplicaciones virtuales  
Si migra paquetes App-V desde un sitio compatible con Configuration Manager 2007, el proceso de migración los convierte en aplicaciones en la jerarquía de destino. Además, de acuerdo con los anuncios existentes para el paquete App-V, los siguientes tipos de implementación se crean en la jerarquía de destino:  

-   Si no hay ningún anuncio, se crea un tipo de implementación que utiliza la configuración predeterminada del tipo de implementación.  

-   Si existe un anuncio, se crea un tipo de implementación que utiliza la misma configuración que la del anuncio de Configuration Manager 2007.  

-   Si existen varios anuncios, se crea un tipo de implementación para cada anuncio de Configuration Manager 2007, con la misma configuración que la del anuncio.  

> [!IMPORTANT]  
>  Si migra un paquete App-V de Configuration Manager 2007 previamente migrado, se produce un error en la migración porque los paquetes de aplicaciones virtuales no admiten el comportamiento de sobrescritura de migración. En este escenario debe eliminar el paquete de la aplicación virtual migrado de la jerarquía de destino y, a continuación, crear un nuevo trabajo de migración para migrar la aplicación virtual.  

> [!NOTE]  
>  Una vez migrado el paquete de App-V, puede usar el Asistente para actualizar contenido para cambiar la ruta de origen de los tipos de implementación de App-V. Para más información sobre cómo actualizar el contenido relativo a un tipo de implementación, vea Administración de tipos de implementaciones en [Tareas de administración de aplicaciones de Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

Si migra desde una jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, además de las aplicaciones y los tipos de implementación de App-V, puede migrar objetos al entorno virtual de App-V. Para más información sobre los entornos de App-V, vea [Implementar aplicaciones virtuales de App-V](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Anuncios  
Puede migrar anuncios desde un sitio de origen compatible con Configuration Manager 2007 a la jerarquía de destino mediante migración basada en recopilación. Si actualiza un cliente, éste conservará el historial de anuncios previamente ejecutados para evitar que el cliente vuelva a ejecutar los anuncios migrados.  

> [!NOTE]  
>  No puede migrar los anuncios de paquetes virtuales. Se trata de una excepción de la migración de anuncios.  

### <a name="applications"></a>Aplicaciones  
 Puede migrar las aplicaciones a una jerarquía de destino desde una jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager que sea compatible. Si reasigna a un cliente de la jerarquía de origen a la jerarquía de destino, el cliente conserva el historial de las aplicaciones previamente instaladas para impedir que vuelva a ejecutar una aplicación migrada.  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a> Plan para migrar recopilaciones  
 Puede migrar los criterios de las recopilaciones de una jerarquía de origen compatible de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager. Para ello, utilice una tarea de migración basada en objetos. Cuando se migra una recopilación, se migran las reglas de la misma y no la información acerca de los miembros de la recopilación ni la información o los objetos relacionados con los miembros de la recopilación.  

 La migración de objetos de recopilación no se admite si se migra desde una jerarquía de origen de Configuration Manager 2007.  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a> Plan para migrar implementaciones de sistema operativo  
Puede migrar los siguientes objetos de implementación de sistema operativo de una jerarquía de origen compatible:  

-   Imágenes y paquetes de sistema operativo. La ruta de origen de imágenes de arranque se actualiza en la ubicación de la imagen predeterminada para Windows Administrative Installation Kit (Windows AIK) en el sitio de destino. Los siguientes son los requisitos y las limitaciones de la migración de imágenes y paquetes de sistema operativo:  

    -   Para migrar satisfactoriamente archivos de imagen, la cuenta de equipo del servidor del proveedor de SMS para el sitio de alto nivel de las jerarquías de destino debe tener permisos de **Lectura** y **Escritura** de los archivos de origen de la imagen de la ubicación Windows AIK de los sitios de origen.  

    -   Cuando migre un paquete de instalación de sistema operativo, asegúrese de que la configuración del paquete en el sitio de origen indica la carpeta que tiene el archivo WIM, y no el archivo WIM mismo. Si el paquete de instalación indica el archivo WIM, se producirá un error en la migración del paquete de instalación.  

    -   Cuando se migra un paquete de imagen de arranque desde un sitio de origen de Configuration Manager 2007, el identificador del paquete no se mantiene en el sitio de destino. El resultado es que los clientes de la jerarquía de destino no pueden utilizar paquetes de imagen de arranque disponibles en los puntos de distribución compartidos.  

-   Secuencias de tareas. Cuando se migra una secuencia de tareas que tiene una referencia a un paquete de instalación de cliente, la referencia se sustituye por una referencia al paquete de instalación del cliente de la jerarquía de destino.  

    > [!NOTE]  
    >  Si migra una secuencia de tareas, es posible que Configuration Manager migre objetos no necesarios en la jerarquía de destino. Entre estos objetos se incluyen imágenes de arranque y paquetes de instalación de cliente de Configuration Manager 2007.  

-   Controladores y paquetes de controladores. Al migrar paquetes de controladores, la cuenta de equipo del proveedor de SMS en la jerarquía de destino debe tener control total sobre el origen del paquete.

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a> Plan para migrar la administración de configuración deseada  
Puede migrar elementos de configuración y líneas de base de configuración.  

> [!NOTE]  
>  Los elementos de configuración no interpretados de jerarquías de origen de Configuration Manager 2007 no se admiten para la migración. No puede migrar o importar estos elementos de configuración a la jerarquía de destino. Para más información sobre los elementos de configuración no interpretados, vea Uninterpreted configuration items (Elementos de configuración no interpretados) en el tema [About Configuration Items in Desired Configuration Management (Acerca de los elementos de configuración en la administración de configuración deseada)](https://go.microsoft.com/fwlink/?LinkId=103846) de la biblioteca de documentación de Configuration Manager 2007.  

Puede importar paquetes de configuración de Configuration Manager 2007. El proceso de importación convierte automáticamente los paquetes de configuración para que sean compatibles con la rama actual de Configuration Manager.  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a> Plan para migrar límites  
 Puede migrar los límites entre las jerarquías. Al migrar límites de Configuration Manager 2007, cada límite del sitio de origen se migra al mismo tiempo y se agrega a un nuevo grupo de límites que se crea en la jerarquía de destino. Cuando se migran límites de una jerarquía de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, cada límite seleccionado se agrega a un nuevo grupo de límites en la jerarquía de destino.  

 Cada grupo de límites creado automáticamente está habilitado para la ubicación de contenido pero no para la asignación de sitios. De esta manera se evita la superposición de límites para la asignación de sitios entre las jerarquías de origen y de destino. Migrar de un sitio de origen de Configuration Manager 2007 contribuye a evitar que los nuevos clientes de Configuration Manager 2007 instalados se asignen incorrectamente a la jerarquía de destino. De forma predeterminada, los clientes de la rama actual de Configuration Manager no se asignan automáticamente a los sitios de Configuration Manager 2007.  

 Durante la migración, si comparte un punto de distribución con la jerarquía de destino, los límites que estén asociados con el punto de distribución automáticamente se migran a la jerarquía de destino. En la jerarquía de destino, la migración crea un nuevo grupo de límites de solo lectura para cada punto de distribución compartido. Si cambia los límites del punto de distribución en la jerarquía de origen, el grupo de límites en la jerarquía de destino se actualiza con estos cambios durante el siguiente ciclo de obtención de datos.  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a> Plan para migrar informes  
Configuration Manager no admite la migración de informes. En vez de ello, utilice el generador de informes de SQL Server Reporting Services para exportar informes de la jerarquía de origen y, a continuación, impórtelos a la jerarquía de destino.  

> [!NOTE]  
>  Como hay cambios de esquemas en los informes entre Configuration Manager 2007 y la rama actual de Configuration Manager, debe probar todos los informes que importe desde una jerarquía de Configuration Manager 2007 para asegurarse de que funciona según lo esperado.  

Para obtener más información sobre los informes, consulte [Introducción a los informes](../servers/manage/introduction-to-reporting.md).  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a> Plan para migrar carpetas organizativas y de búsqueda  
 Puede migrar las carpetas organizativas y las carpetas de búsqueda de una jerarquía de origen admitida a una jerarquía de destino. Además, desde una jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, se pueden migrar los criterios de una búsqueda guardada a una jerarquía de destino.  

 De forma predeterminada, el proceso de migración conserva las estructuras de carpeta administrativa y de búsqueda de objetos y recopilaciones al migrar. Pero en el Asistente para crear nuevo trabajo de migración, en la página **Configuración**, puede configurar un trabajo de migración para que no migre la estructura organizativa de objetos mediante la desactivación de la casilla correspondiente. Las estructuras organizativas de las recopilaciones siempre se conservan.  

 Las carpetas de búsqueda que contienen aplicaciones virtuales son una excepción a esta regla. Cuando se migra un paquete de App-V, el paquete de App-V se transforma en una aplicación en Configuration Manager. Después de la migración de la carpeta de búsqueda solo se encuentran los paquetes restantes. La carpeta de búsqueda no puede encontrar un paquete de App-V debido a la conversión en aplicación cuando migra.  

 Cuando se migra una búsqueda guardada de la jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, se migran los criterios de búsqueda y no la información del resultado de esta. La migración de una búsqueda guardada no es aplicable desde un sitio de origen de Configuration Manager 2007.  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a> Plan para migrar personalizaciones de Asset Intelligence  
 Puede migrar las personalizaciones de Asset Intelligence de una jerarquía de origen admitida a una jerarquía de destino. No hay cambios significativos en la estructura de las personalizaciones de Asset Intelligence entre Configuration Manager 2007 y la rama actual de Configuration Manager.  

> [!NOTE]  
> La rama actual de Configuration Manager no admite la migración de objetos de Asset Intelligence de un sitio de Configuration Manager 2007 que usa Asset Intelligence Service 2.0 (AIS 2.0).  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a> Plan para migrar personalizaciones de reglas de disponibilidad de software  
 No hay ningún cambio significativo en la medición de software entre Configuration Manager 2007 y la rama actual de Configuration Manager. Puede migrar las reglas de disponibilidad de software de una jerarquía de origen admitida a una jerarquía de destino.  

 De manera predeterminada, las reglas de disponibilidad de software que se migran a una jerarquía de destino no están asociadas a un sitio en la jerarquía de destino, sino que se aplican a todos los clientes en la jerarquía. Para aplicar una regla de disponibilidad de software a clientes de un determinado sitio, debe editar la regla de disponibilidad después de su migración.  
