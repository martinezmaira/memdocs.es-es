---
title: Listas de comprobación de migración
titleSuffix: Configuration Manager
description: Use listas de comprobación del administrador como ayuda para planear una estrategia de migración a la rama actual de Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e406a2b7674815bb3313200ba850baa249f17ebc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701813"
---
# <a name="administrator-checklists-for-migration-planning-in-configuration-manager"></a>Listas de comprobación del administrador para planear la migración en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use las siguientes listas de comprobación del administrador como ayuda para planear la estrategia de migración a la rama actual de Configuration Manager.

##  <a name="administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a> Lista de comprobación de administrador para la planeación de la migración  
 Utilice la siguiente lista de comprobación para la planeación de los pasos de la migración.  

-   **Evalúe el entorno actual:**  

     Identifique los requisitos empresariales existentes que se satisfacen mediante la jerarquía de origen y elabore planes para continuar cumpliendo los requisitos en la jerarquía de destino.  

-   **Revise la funcionalidad y los cambios disponibles con la versión de Configuration Manager que usa y emplee la información para diseñar la jerarquía de destino:**  

    Para más información, vea [Aspectos básicos de Configuration Manager](../../core/understand/fundamentals.md) y [Novedades](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Determine el modelo de seguridad administrativa que se usará para la administración basada en roles:**  

    Para más información, vea [Conceptos básicos de la administración basada en roles para Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Evalúe la red y la topología de Active Directory:** Revise la estructura de dominio y topología de red existentes, y tenga en cuenta su efecto en tareas de migración y diseño de jerarquía.  

-   **Finalice el diseño de la jerarquía de destino:**  

    Decida sobre la selección de ubicación de un sitio de administración central, los sitios primarios, los sitios secundarios y las opciones de distribución de contenido.  

-   **Asigne la jerarquía a los equipos que va a usar para los sitios y los servidores de sitio en la jerarquía de destino:**  

    Identifique los equipos que servidores de sistema de sitio y sitios usarán en la jerarquía de destino y, después, asegúrese de que tienen la capacidad suficiente para satisfacer los requisitos operativos existentes y futuros.  

-   **Planee la estrategia de migración de objetos:**  

    Planee usar los trabajos de migración disponibles para migrar varios tipos de objetos, como límites de sitios, recopilaciones, anuncios e implementaciones. Para más información, vea [Tipos de trabajos de migración](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) en [Planear una estrategia de trabajo de migración](../../core/migration/planning-a-migration-job-strategy.md).  

    Configuration Manager migra solo los objetos seleccionados. Los objetos que no se migran y que son necesarios en la jerarquía de destino deben volver a crearse en la jerarquía de destino.  

    Los objetos que se pueden migrar se muestran al configurar trabajos de migración.  

-   **Planee la estrategia de migración de clientes:**  

    Use un enfoque controlado para limitar el ancho de banda de red y los requisitos de procesamiento del servidor al migrar los clientes a la jerarquía de destino. Para más información sobre cómo planear una estrategia de migración de cliente, vea [Planear una estrategia de migración de clientes](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Prepare un plan para los datos de cumplimiento e inventario:**  

    Configuration Manager no admite la migración de inventario de hardware, inventario de software o datos de cumplimiento de administración de configuración deseada para actualizaciones de software o clientes.  

    En vez de ello, después de que el cliente se migra al nuevo sitio en la jerarquía de destino y recibe la directiva para estas configuraciones, el cliente envía esta información a su sitio asignado. Esta acción rellena la base de datos del sitio de destino con datos actualizados de cumplimiento y de inventario.  

-   **Prepare un plan para la finalización de la migración desde la jerarquía de origen:**  

    Decida cuándo se migrarán los objetos y los clientes. Al finalizar la migración, puede planear la retirada de los servidores de sitio en la jerarquía de origen.  

##  <a name="administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a> Lista de comprobación de administrador para la migración de jerarquías  
Utilice la siguiente lista de comprobación para planear una jerarquía de destino antes de iniciar la migración.  

-   **Identifique los equipos que se van a usar en la jerarquía de destino:**  

    Configuration Manager no admite una actualización inmediata desde la infraestructura de Configuration Manager 2007. En su lugar, se usa la migración para mover datos de Configuration Manager 2007 a la rama actual de Configuration Manager. Esto exige usar una implementación en paralelo e instalar Configuration Manager en los nuevos equipos.  

    Del mismo modo, al migrar desde otra jerarquía de Configuration Manager, debe instalar una nueva jerarquía de destino que sea una implementación en paralelo a la jerarquía de origen.  

-   **Cree la jerarquía de destino:**  

    Para preparar la migración, instale y configure una jerarquía de destino de Configuration Manager que incluya un sitio primario. Por ejemplo:  

    -   Instale un sitio de administración central y, después, instale al menos un sitio primario secundario.  

    -   Instale un sitio primario independiente si no piensa usar un sitio de administración central.  

-   **Si quiere migrar información relacionada con actualizaciones de software, configure un punto de actualización de software en la jerarquía de destino y sincronice las actualizaciones de software:**  

    Debe configurar y sincronizar las actualizaciones de software en la jerarquía de destino antes de poder migrar información de actualizaciones de software de la jerarquía de origen.  


-   **Instale y configure roles de sistema de sitio adicionales en la jerarquía de destino:**  

    Configure los sistemas de sitio y los roles de sistema de sitio adicionales que necesite.  

-   **Compruebe la funcionalidad operativa de la jerarquía de destino:**  

    Compruebe lo siguiente:  

    -   Si la jerarquía de destino incluye varios sitios, confirme que la replicación de base de datos funciona entre los sitios. La replicación de base de datos no es aplicable en sitios primarios independiente.  

    -   Compruebe que todos los roles de sistema de sitio instalados están operativos.  

    -   Compruebe que los clientes de Configuration Manager que instala en la jerarquía de destino pueden comunicarse correctamente con su sitio asignado.  


##  <a name="administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a> Lista de comprobación de administrador para la migración  
Utilice la siguiente lista de comprobación para migrar datos de la jerarquía de origen a la jerarquía de destino.  

-   **Habilite la migración en la jerarquía de destino:**  

    Configure una jerarquía de origen especificando el sitio de nivel superior de la jerarquía de origen. Para más información sobre cómo especificar el sitio de origen, vea [Planear una estrategia de jerarquía de origen](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Si la jerarquía de origen ejecuta Configuration Manager 2007 SP2, seleccione y configure sitios adicionales en la jerarquía de origen:**  

    Debe configurar credenciales de recopilación de datos para cada sitio adicional de la jerarquía de origen de Configuration Manager 2007 SP2 del que quiera recopilar datos. Cuando se configura cada sitio de origen, el proceso de recopilación de datos se inicia de inmediato y continúa durante el periodo de migración hasta que se detenga la recopilación de datos del sitio correspondiente. La recopilación de datos garantiza poder migrar, desde la jerarquía de origen, objetos que se actualizaron o agregaron después de un proceso de recopilación de datos anterior.

    > [!NOTE]  
    >  Si la jerarquía de origen ejecuta System Center 2012 Configuration Manager o versiones posteriores, no es necesario configurar sitios de origen adicionales.  

-   **Configure el uso compartido de puntos de distribución:**  

    Puede compartir puntos de distribución entre las dos jerarquías para hacer que el contenido de los objetos que migra esté disponible para los clientes en la jerarquía de destino. Esto garantiza que el mismo contenido sigue estando disponible para los clientes de ambas jerarquías, y que puede mantener el contenido hasta que detenga la recopilación de datos y finalice la migración.  

    Para más información sobre los puntos de distribución compartidos, vea [Compartir puntos de distribución entre jerarquías de origen y de destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) en [Planear una estrategia de migración de implementación de contenido](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Cree y ejecute trabajos de migración para migrar objetos asociados a los clientes en la jerarquía de origen:**  

    Cree trabajos de migración para migrar objetos entre jerarquías. Las configuraciones necesarias para cada trabajo de migración pueden variar según los datos que el trabajo migra.  

    Por ejemplo, independientemente del trabajo de migración que se utiliza, al migrar contenido debe asignar la administración del contenido a un sitio en la jerarquía de destino. El sitio asignado tendrá acceso a la ubicación original del archivo de origen de contenido, y será responsable de distribuir el contenido a los puntos de distribución en la jerarquía de destino.  

    Para más información, vea [Crear y editar trabajos de migración para Configuration Manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) en [Operaciones para migrar a la rama actual de Configuration Manager](../../core/migration/operations-for-migration.md).  

-   **Migre los clientes a la jerarquía de destino:**  

    El proceso de migración de los clientes depende de su escenario de migración:  

    -   Al migrar clientes con una versión de cliente distinta a la de la jerarquía de destino, debe actualizar el software cliente. La actualización exige la eliminación del cliente de Configuration Manager actual seguida de la instalación de la nueva versión de cliente que coincide con el sitio de destino.  

    -   Al migrar clientes que tienen una versión de cliente que coincide con la versión de la jerarquía de destino, el cliente no se actualiza ni reinstala. En vez de ello, el cliente se asigna a un sitio primario en la jerarquía de destino.  

    Al migrar un cliente a la jerarquía de destino, el cliente se asocia con los datos migrados anteriormente a esa jerarquía de destino.  

    Para obtener más información, consulte [Planear una estrategia de migración de clientes](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Actualice o vuelva a asignar puntos de distribución compartidos:**  

    Cuando ya no tenga que admitir clientes en la jerarquía de origen, puede actualizar puntos de distribución compartidos desde un sitio de origen de Configuration Manager 2007 o reasignar puntos de distribución compartidos desde un sitio de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager. Cuando se actualiza o se reasigna un punto de distribución, el rol de sistema de sitio se transfiere a un sitio primario en la jerarquía de destino y se quita el punto de distribución del sitio de origen en la jerarquía de origen. Cuando se actualiza o se reasigna un punto de distribución compartido, el contenido permanece en el equipo del punto de distribución y no es necesario volver a implementar el contenido en los nuevos puntos de distribución en la jerarquía de destino.  

    También puede actualizar un punto de distribución de Configuration Manager 2007 que comparte ubicación con un servidor de sitio secundario. De esta manera se quita el sitio secundario y solo hay un punto de distribución en la jerarquía de destino.  

    Para más información sobre los puntos de distribución compartidos, vea [Compartir puntos de distribución entre jerarquías de origen y de destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) en [Planear una estrategia de migración de implementación de contenido](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Finalizar la migración:**  

    Después de migrar los datos y los clientes de todos los sitios en la jerarquía de origen, y de actualizar los puntos de distribución correspondientes, puede finalizar la migración. Para finalizar la migración, detenga la recopilación de datos de los sitios de origen en la jerarquía de origen. A continuación, puede quitar la información de migración que no necesite y retirar la infraestructura de la jerarquía de origen. Para obtener más información, consulte [Planear la finalización de la migración](../../core/migration/planning-to-complete-migration.md).  
