---
title: Selección del contenido para migrar
titleSuffix: Configuration Manager
description: Obtenga información sobre qué datos puede y no puede migrar a la rama actual de Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701773"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Determinar si se migrarán datos a la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En la rama actual de Configuration Manager, la migración proporciona un proceso para transferir los datos y las configuraciones que ha creado desde versiones compatibles de Configuration Manager a la nueva jerarquía.  Puede usarlo también para lo siguiente:  

-   Combinar varias jerarquías en una.  

-   Mover los datos y las configuraciones desde una implementación de laboratorio a la implementación de producción.

-   Mover los datos y la configuración desde una versión anterior de Configuration Manager (como Configuration Manager 2007), que no tiene una ruta de acceso de actualización a la rama actual de Configuration Manager, o bien desde System Center 2012 Configuration Manager (que admite una ruta de acceso de actualización a la rama actual de Configuration Manager).  

Con la excepción del rol de sistema de sitio de punto de distribución y los equipos que hospedan puntos de distribución, no se pueden compartir infraestructuras (que incluyen sitios, roles de sistema de sitio o equipos que hospedan un rol de sistema de sitio), migraciones o transferencias entre jerarquías.  

 Aunque no se puede migrar la infraestructura de servidor, se pueden migrar clientes de Configuration Manager entre jerarquías. La migración de clientes implica la migración, de la jerarquía de origen a la jerarquía de destino, de los datos que utilizan los clientes y, a continuación, la instalación o reasignación del software cliente para que el cliente informe a la nueva jerarquía.

Después de instalar un cliente en la nueva jerarquía y de que el cliente envíe sus datos, su identificador de Configuration Manager exclusivo ayuda a Configuration Manager a asociar los datos que se migraron previamente con cada equipo cliente.  

 La función que la migración proporciona ayuda a mantener las inversiones que ha realizado en las configuraciones e implementaciones, mientras aprovecha al máximo los cambios principales del producto (que se incorporaron por primera vez en System Center 2012 Configuration Manager y continuaron en Configuration Manager). Estos cambios incluyen una jerarquía de Configuration Manager simplificada que usa menos sitios y recursos, y un procesamiento mejorado que proviene del código de 64 bits nativo que ejecuta hardware de 64 bits.  

 Para más información sobre las versiones de Configuration Manager que la migración admite, vea [Requisitos previos para la migración](../../core/migration/prerequisites-for-migration.md).  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a> Datos que se pueden migrar a la rama actual de Configuration Manager

La migración puede migrar la mayoría de los objetos entre jerarquías de Configuration Manager compatibles. Las instancias migradas de algunos objetos desde una versión compatible de Configuration Manager 2007 deben modificarse de acuerdo con el esquema de System Center 2012 Configuration Manager y el formato de objetos.

Estas modificaciones no afectan a los datos de la base de datos del sitio de origen. Los objetos que se migran desde una versión compatible de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager no requieren ninguna modificación.  

Los siguientes objetos se pueden migrar según la versión de Configuration Manager de la jerarquía de origen. Algunos objetos, como las consultas, no se migran. Si desea seguir utilizando estos objetos que no se migran, debe volver a crearlos en la nueva jerarquía. Otros objetos, incluidos algunos datos de cliente, se vuelven a crear automáticamente en la jerarquía nueva cuando se administran clientes en dicha jerarquía.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>Objetos que se pueden migrar desde System Center 2012 Configuration Manager o desde la rama actual de Configuration Manager

-   Aplicaciones para System Center 2012 Configuration Manager y versiones posteriores  

-   Entorno virtual de App-V desde System Center 2012 Configuration Manager y versiones posteriores  

-   Personalizaciones de Asset Intelligence  

-   Límites  

-   Recopilaciones: para migrar recopilaciones desde una versión compatible de System Center 2012 Configuration Manager o desde la rama actual de Configuration Manager, se usa un trabajo de migración de objeto.  

-   Configuración de cumplimiento:  

    -   Líneas de base de configuración  

    -   Elementos de configuración  

-   Implementaciones  

-   Implementación de sistema operativo:  

    -   Imágenes de arranque  

    -   Paquetes de controladores  

    -   Controladores  

    -   Imágenes  

    -   Paquetes  

    -   Secuencias de tareas  

-   Resultados de la búsqueda: criterios de búsqueda guardados  

-   Actualizaciones de software:  

    -   Implementaciones  

    -   Paquetes de implementación  

    -   Plantillas  

    -   Listas de actualizaciones de software  

-   Paquetes de distribución de software  

-   Reglas de disponibilidad de software  

-   Paquetes de aplicaciones virtuales  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Objetos que puede migrar desde Configuration Manager 2007 SP2

-   Anuncios  

-   Aplicaciones para System Center 2012 Configuration Manager y versiones posteriores  

-   Entorno virtual de App-V desde System Center 2012 Configuration Manager y versiones posteriores  

-   Personalizaciones de Asset Intelligence  

-   Límites  

-   Recopilaciones: puede migrar recopilaciones desde una versión compatible de Configuration Manager 2007 con un trabajo de migración de recopilaciones.  

-   Configuración de compatibilidad (llamada administración de configuración deseada en Configuration Manager 2007):  

    -   Líneas de base de configuración  

    -   Elementos de configuración  

-   Implementación de sistema operativo:  

    -   Imágenes de arranque  

    -   Paquetes de controladores  

    -   Controladores  

    -   Imágenes  

    -   Paquetes  

    -   Secuencias de tareas  

-   Resultados de la búsqueda: Carpetas de búsqueda  

-   Actualizaciones de software:  

    -   Implementaciones  

    -   Paquetes de implementación  

    -   Plantillas  

    -   Listas de actualizaciones de software  

-   Paquetes de distribución de software  

-   Reglas de disponibilidad de software  

-   Paquetes de aplicaciones virtuales  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a> Datos que no se pueden migrar a la rama actual de Configuration Manager

No se pueden migrar los siguientes tipos de objetos:  

-   Información de aprovisionamiento de cliente de AMT  

-   Archivos en clientes, incluidos:  

    -   Datos del historial e inventario de cliente  

    -   Archivos en la caché del cliente  

-   Consultas  

-   Instancias y derechos de seguridad de Configuration Manager 2007 para el sitio y los objetos  

-   Informes de Configuration Manager 2007 de SQL Server Reporting Services  

-   Informes web de Configuration Manager 2007  

-   Informes de System Center 2012 Configuration Manager y de la rama actual de Configuration Manager  

-   Administración basada en roles de System Center 2012 Configuration Manager y de la rama actual de Configuration Manager:  

    -   Roles de seguridad  

    -   Ámbitos de seguridad  
