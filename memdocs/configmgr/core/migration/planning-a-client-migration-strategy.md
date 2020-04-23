---
title: Planeamiento de migración de clientes
titleSuffix: Configuration Manager
description: Obtenga información sobre las tareas de migración de clientes de una jerarquía de origen a una jerarquía de destino de la rama actual de Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704563"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>Planeación de una estrategia de migración de clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para migrar clientes de la jerarquía de origen a una jerarquía de destino de la rama actual de Configuration Manager, debe realizar dos tareas. Debe migrar los objetos asociados con el cliente y volver a instalar o asignar los clientes de la jerarquía de origen a la jerarquía de destino. Migre los objetos primero para que estén disponibles cuando se migren los clientes. Los objetos asociados con el cliente se migran mediante trabajos de migración. Para más información sobre cómo migrar los objetos asociados con el cliente, vea [Planear una estrategia de migración de clientes](../../core/migration/planning-a-migration-job-strategy.md).  

 Utilice las siguientes secciones para planear la migración de clientes a la jerarquía de destino.  

-   [Planear la migración de clientes a la jerarquía de destino](#Planning_for_Client_Agent_Migration)  

-   [Planear el control de los datos mantenidos en los clientes durante la migración](#Planning_for_Client_Data_Migration)  

-   [Planear los datos de cumplimiento y de inventario durante la migración](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> Planear la migración de clientes a la jerarquía de destino  
 Cuando se migran clientes de una jerarquía de origen, se actualiza el software cliente en el equipo cliente para coincidir con la versión del producto de la jerarquía de destino.  

-   **Una jerarquía de origen de Configuration Manager 2007:** cuando migre clientes desde una jerarquía de origen que ejecute una versión compatible de Configuration Manager, el software cliente se actualizará a la versión del cliente para la jerarquía de destino.  

-   **Una jerarquía de origen de System Center 2012 Configuration Manager o posteriores:** Cuando se migran clientes entre jerarquías con la misma versión del producto, el software cliente no cambia ni se actualiza. En su lugar, el cliente se reasignará desde la jerarquía de origen a un sitio en la jerarquía de destino.  

    > [!NOTE]  
    >  Si no se admite la migración de la versión del producto de una jerarquía a la jerarquía de destino, actualice todos los sitios y los clientes de la jerarquía de origen a una versión del producto admitida. Después de actualizar la jerarquía de origen a una versión admitida del producto, puede realizar la migración entre jerarquías. Para más información, vea la sección [Versiones de Configuration Manager admitidas para la migración](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) en [Requisitos previos para la migración](../../core/migration/prerequisites-for-migration.md).  

Utilice la siguiente información para planear la migración de clientes:  

-   Para actualizar o volver a asignar clientes desde el sitio de origen al sitio de destino, puede utilizar cualquier método de implementación de cliente compatible con la implementación de clientes en la jerarquía de destino. Los métodos de implementación de cliente típicos incluyen instalación de inserción de cliente, distribución de software, directiva de grupo e instalación de cliente basada en actualizaciones de software. Para obtener más información, vea [Métodos de instalación de cliente en System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Asegúrese de que el dispositivo que ejecuta el software cliente en la jerarquía de origen cumple los requisitos mínimos de hardware y ejecuta un sistema operativo admitido por la versión de Configuration Manager en la jerarquía de destino.  

-   Antes de migrar un cliente, ejecute un trabajo de migración para migrar la información que usará el cliente en la jerarquía de destino.  

-   Los clientes que actualizan conservan su historial de ejecución para las implementaciones. Esto evita que las implementaciones se vuelvan a ejecutar innecesariamente en la jerarquía de destino.  

    -   Para los clientes de Configuration Manager 2007, se mantiene el historial de ejecución de anuncios.  

    -   En el caso de los clientes de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, el historial de ejecución de implementaciones se conserva.  

-   Puede migrar clientes de los sitios de la jerarquía de origen en cualquier orden que elija. Pero considere la posibilidad de migrar un número limitado de clientes en fases, en lugar de migrar grandes cantidades de clientes de una sola vez. Una migración por fases reduce los requisitos de ancho de banda de red y el procesamiento del servidor cuando cada cliente recién actualizado envía sus datos de cumplimiento y el inventario completo iniciales a su sitio asignado.  

-   Al migrar clientes de Configuration Manager 2007 se desinstala el software cliente existente del equipo cliente y se instala el nuevo software cliente.  

-   Configuration Manager no puede migrar un cliente de Configuration Manager 2007 que tenga el cliente de App-V instalado, a no ser que la versión del cliente de App-V sea 4.6 SP1 o superior.  

Puede supervisar el proceso de migración del cliente en el nodo **Migración** del área de trabajo **Administración** en la consola de Configuration Manager.  

Tras migrar el cliente a la jerarquía de destino, no podrá administrar ese dispositivo con su jerarquía de origen y deberá considerar la posibilidad de quitar el cliente de la jerarquía de origen. Aunque no sea un requisito a la hora de migrar jerarquías, puede servir para evitar la identificación de un cliente migrado en un informe de jerarquía de origen, o un recuento incorrecto de recursos entre las dos jerarquías durante la migración. Por ejemplo, cuando un cliente migrado permanece en la base de datos del sitio de origen, puede ejecutar un informe de actualizaciones de software que identifique de forma incorrecta el equipo como un recurso sin administrar cuando está administrado actualmente por la jerarquía de destino.  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a> Planear el control de los datos mantenidos en los clientes durante la migración  
Cuando migre un cliente desde su jerarquía de origen a la jerarquía de destino, parte de la información se mantiene en el dispositivo, mientras que otra no está disponible en el dispositivo después de la migración.  

La información siguiente se conserva en el dispositivo cliente:  

-   El identificador único (GUID), que asocia un cliente con su información en la base de datos de Configuration Manager.  

-   El historial de implementaciones o de anuncios, que impide que los clientes vuelvan a ejecutar innecesariamente anuncios o implementaciones en la jerarquía de destino.  

La información siguiente no se conserva en el dispositivo cliente:  

-   Los archivos en la caché del cliente. Si el cliente requiere estos archivos para instalar el software, el cliente los descarga de nuevo desde la jerarquía de destino.  

-   Información de la jerarquía de origen sobre los anuncios o las implementaciones que no se han ejecutado todavía. Si desea que el cliente ejecute los anuncios o las implementaciones después de migrar, debe volver a implementarlos en el cliente en la jerarquía de destino.  

-   Información acerca del inventario. El cliente vuelve a enviar esta información a su sitio asignado en la jerarquía de destino después de que el cliente migre y se hayan generado los nuevos datos de cliente.  

-   Datos de cumplimiento de normas. El cliente vuelve a enviar esta información a su sitio asignado en la jerarquía de destino después de que el cliente migre y se hayan generado los nuevos datos de cliente.  

Cuando se migra un cliente, no se mantiene la información que se almacena en el Registro del cliente de Configuration Manager ni la ruta de acceso de archivos. Después de la migración, vuelva a aplicar esta configuración. Los valores de configuración típicos incluyen lo siguiente:  

-   Planes de energía  

-   Configuración de registro  

-   Configuración de directivas locales  

Además, es posible que tenga que volver a instalar algunas aplicaciones.  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Planear los datos de cumplimiento y de inventario durante la migración  
No se guardan los datos de cumplimiento de normas ni el inventario de cliente al migrar un cliente a la jerarquía de destino. En su lugar, esta información se vuelve a crear en la jerarquía de destino cuando un cliente envía primero su información a su sitio asignado. Para ayudar a reducir los requisitos de ancho de banda de red y el procesamiento de servidor resultantes, es mejor que migre un número pequeño de clientes en fases en lugar de migrar una gran cantidad de clientes de una sola vez.  

 Además, no puede migrar las personalizaciones del inventario de hardware de una jerarquía de origen. Debe introducirlas en la jerarquía de destino independientemente de la migración. Para más información sobre cómo ampliar el inventario de hardware, vea [Cómo configurar el inventario de hardware](../../core/clients/manage/inventory/configure-hardware-inventory.md).  
