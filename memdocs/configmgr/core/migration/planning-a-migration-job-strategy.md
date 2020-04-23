---
title: Planeamiento de trabajos de migración
titleSuffix: Configuration Manager
description: Use trabajos de migración para configurar los datos que quiera migrar al entorno de la rama actual de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87aac20a2ac70e843bf17982375c92804de2b20e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702853"
---
# <a name="plan-a-migration-job-strategy-in-configuration-manager"></a>Planear una estrategia de trabajo de migración en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use trabajos de migración para configurar los datos específicos que quiera migrar al entorno de la rama actual de Configuration Manager. Los trabajos de migración identifican los objetos que planea migrar y se ejecutan en el sitio de nivel superior en la jerarquía de destino. Puede configurar uno o varios trabajos de migración por cada sitio de origen. Esto le permite migrar todos los objetos al mismo tiempo o subconjuntos limitados de datos con cada trabajo.  

 Puede crear trabajos de migración después de que Configuration Manager recopile correctamente datos de uno o varios sitios de la jerarquía de origen. Puede migrar datos en cualquier secuencia de los sitios de origen en que se recopilaron los datos. Con un sitio de origen de Configuration Manager 2007, solo puede migrar datos desde el sitio donde se creó un objeto. Con sitios de origen que ejecutan System Center 2012 Configuration Manager o posterior, todos los datos que puede migrar están disponibles en el sitio de nivel superior de la jerarquía de origen.  

 Antes de migrar clientes entre jerarquías, asegúrese de que se han migrado los objetos que utilizan los clientes y que estos objetos están disponibles en la jerarquía de destino. Por ejemplo, cuando migra desde una jerarquía de origen de Configuration Manager 2007 SP2, es posible que reciba un anuncio de contenido implementado en una recopilación personalizada que contiene un cliente. En este escenario, se recomienda migrar la recopilación, el anuncio y el contenido asociado antes de migrar el cliente. Estos datos no se pueden asociar al cliente en la jerarquía de destino si el contenido, la recopilación y el anuncio no se migran antes de migrar el cliente. Si un cliente no se asocia a los datos relacionados con un anuncio y contenido ejecutado anteriormente, el cliente puede recibir la oferta de contenido para instalar en la jerarquía de destino, lo que puede no ser necesario. Cuando el cliente se migra después de migrar los datos, el cliente se asocia al contenido y al anuncio, y, a menos que el anuncio sea recurrente, no recibirá de nuevo la oferta de este contenido para el anuncio migrado.  

 Algunos objetos requieren más que la migración de datos de la jerarquía de origen a la jerarquía de destino. Por ejemplo, para migrar correctamente actualizaciones de software para sus clientes en la jerarquía de destino, debe implementar un punto de actualización de software activo, configurar el catálogo de productos y sincronizar el punto de actualización de software con Windows Server Update Services (WSUS) en la jerarquía de destino.  

##  <a name="types-of-migration-jobs"></a><a name="Types_of_Migration"></a> Tipos de trabajos de migración  
 Configuration Manager admite los siguientes tipos de trabajos de migración. Cada tipo de trabajo está diseñado para ayudar a definir los objetos que se pueden incluir en ese trabajo.  

 **Migración de recopilación** (solo se admite al migrar desde Configuration Manager 2007 SP2): Migre los objetos que estén relacionados con las recopilaciones que seleccione. De forma predeterminada, la migración de una recopilación incluye todos los objetos asociados a los miembros de la recopilación. Puede excluir instancias de objetos específicos al usar un trabajo de migración de recopilación.  

 **Migración de objetos**: Migre los objetos individuales que seleccione. Seleccione solo los datos específicos que desee migrar.  

 **Migración de objetos migrados anteriormente**: migre objetos que migró anteriormente, cuando se hayan actualizado en la jerarquía de origen después de que se hubieran migrado por última vez.  

###  <a name="objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a> Objetos que puede migrar  
 No todos los objetos se pueden migrar con un tipo específico de trabajo de migración. La lista siguiente identifica el tipo de objetos que puede migrar con cada tipo de trabajo de migración.  

> [!NOTE]  
>  Los trabajos de migración de recopilación solo están disponibles al migrar objetos desde una jerarquía de origen de Configuration Manager 2007 SP2.  

 **Tipos de trabajo que puede usar para migrar cada objeto**  

-   **Anuncios** (disponibles para migrar desde sitios de origen de Configuration Manager 2007 compatibles)  

    -   Migración de recopilación  


-   **Catálogo Asset Intelligence**  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Requisitos de hardware de Asset Intelligence**  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Lista de software de Asset Intelligence**  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Límites**  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Líneas de base de configuración**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Elementos de configuración**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Ventanas de mantenimiento**  

    -   Migración de recopilación  


-   **Imágenes de arranque de implementación de sistema operativo**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Paquetes de controladores de implementación de sistema operativo**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Controladores de implementación de sistema operativo**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Imágenes de implementación de sistema operativo**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Paquetes de implementación de sistema operativo**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Paquetes de distribución de software**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Reglas de disponibilidad de software**  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Paquetes de implementación de actualizaciones de software**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Plantillas de implementación de actualización de software**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Implementaciones de actualización de software**  

    -   Migración de recopilación  


-   **Listas de actualizaciones de software**  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Secuencias de tareas**  

    -   Migración de recopilación  

    -   Migración de objeto  

    -   Migración de objeto migrado anteriormente  

-   **Paquetes de aplicaciones virtuales**  

    -   Migración de recopilación  

    -   Migración de objeto  

    > [!IMPORTANT]  
    >  Aunque puede migrar un paquete de aplicación virtual con la migración de objeto, los paquetes no se pueden migrar con el tipo de trabajo de migración de **Migración de objeto migrado anteriormente**. En su lugar, debe eliminar el paquete de aplicación virtual migrado del sitio de destino y, a continuación, crear un nuevo trabajo de migración para migrar la aplicación virtual.  

##  <a name="general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a> Planeamiento general de todos los trabajos de migración  
 Use al Asistente para crear trabajo de migración con el fin de crear un trabajo de migración para migrar objetos a la jerarquía de destino. El tipo de trabajo de migración que cree determina qué objetos están disponibles para migrar. Puede crear y usar varios trabajos de migración para migrar datos desde el mismo sitio de origen o desde varios sitios de origen. El uso de un tipo de trabajo de migración no anula el uso de un tipo diferente de trabajo de migración.  

 Después de ejecutar correctamente un trabajo de migración, su estado aparece como **Completado** y no se puede ejecutar de nuevo. Sin embargo, puede crear un nuevo trabajo de migración para migrar cualquiera de los objetos que se migraron en el trabajo original. Este nuevo trabajo de migración también puede incluir objetos nuevos. Al crear trabajos de migración adicionales, los objetos que se migraron previamente muestran el estado de **Migrado**. Puede seleccionar estos objetos para migrarlos otra vez pero, a menos que el objeto se haya actualizado en la jerarquía de origen, no es necesario migrar de nuevo estos objetos. Si el objeto se actualizó en la jerarquía de origen después de su migración original, puede identificar ese objeto cuando use el tipo de trabajo de migración de **Objetos modificados después de la migración**.  

 Puede eliminar un trabajo de migración antes de ejecutarlo. Pero, una vez completado un trabajo de migración, este permanece visible en la consola de Configuration Manager y no se puede eliminar. Cada trabajo de migración completado o no ejecutado todavía permanece visible en la consola de Configuration Manager hasta que se complete el proceso de migración y se limpien los datos de migración.  

> [!NOTE]  
>  Después de completar la migración mediante la acción **Limpiar datos de migración**, puede volver a configurar la misma jerarquía como la jerarquía de origen actual para restaurar la visibilidad de los objetos migrados anteriormente.  

 Para ver los objetos incluidos en cualquier trabajo de migración en la consola de Configuration Manager, seleccione el trabajo de migración y después haga clic en la pestaña **Objetos en el trabajo**.  

 Utilice la información de las secciones siguientes como ayuda para planear todos los trabajos de migración.  

### <a name="data-selection"></a>Selección de datos  
 Cuando cree un trabajo de migración de recopilación, debe seleccionar una o más recopilaciones. Después de seleccionar las recopilaciones, el Asistente para crear trabajo de migración muestra los objetos asociados a las recopilaciones. De forma predeterminada, se migran todos los objetos asociados a las recopilaciones seleccionadas, pero puede desactivar los objetos que no quiera migrar con ese trabajo. Cuando desactiva un objeto que tiene objetos dependientes, también se desactivan esos objetos dependientes. Todos los objetos desactivados se agregan a una lista de exclusión. Los objetos que aparecen en una lista de exclusión se quitan de la selección automática en futuros trabajos de migración. Debe editar manualmente la lista de exclusión para quitar los objetos que desee que se seleccionen automáticamente para la migración en los trabajos de migración que se creen en el futuro.  

### <a name="site-ownership-for-migrated-content"></a>Propiedad del sitio para el contenido migrado  
 Cuando migra contenido para las implementaciones, debe asignar el objeto de contenido a un sitio en la jerarquía de destino. Este sitio, a continuación, se convierte en el propietario de ese contenido en la jerarquía de destino. Aunque el sitio de nivel superior de su jerarquía de destino es el sitio que migra realmente los metadatos del contenido, es el sitio asignado que accede a los archivos de origen originales del contenido en la red.  

 Para minimizar el ancho de banda de red que se utiliza durante la migración, considere la posibilidad de transferir propiedad del contenido al sitio más cercano disponible. Dado que la información sobre el contenido se comparte de forma global en Configuration Manager, estará disponible en cada sitio.  

 La información sobre el contenido se comparte en todos los sitios de la jerarquía de destino mediante la replicación de base de datos. Pero cualquier contenido que asigne a un sitio primario y que luego implemente en puntos de distribución en otros sitios primarios se transfiere mediante la replicación basada en archivos. Esta transferencia se dirige al sitio de administración central y, a continuación, a cada sitio primario adicional. Si centraliza paquetes que planea distribuir en varios sitios primarios antes o durante la migración cuando asigne un sitio como propietario de contenido, puede reducir las transferencias de datos en redes de ancho de banda bajo.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Ámbitos de seguridad de administración basada en roles para los datos migrados  
 Cuando migre datos a una jerarquía de destino, debe asignar uno o varios ámbitos de seguridad de administración basada en roles a los objetos cuyos datos se migran. Esto garantiza que solo los usuarios administrativos adecuados tienen acceso a estos datos después de su migración. Los ámbitos de seguridad que especifique se definen mediante el trabajo de migración y se aplican a cada objeto que se migra con ese trabajo. Si necesita aplicar ámbitos de seguridad diferentes a diferentes conjuntos de objetos y quiere asignar esos ámbitos durante la migración, debe migrar los diferentes conjuntos de objetos mediante diferentes trabajos de migración.  

 Antes de configurar un trabajo de migración, revise cómo funciona la administración basada en roles en Configuration Manager. Si es necesario, configure uno o varios ámbitos de seguridad para los datos que migra con el fin de controlar quién tendrá acceso a los objetos migrados en la jerarquía de destino.  

 Para más información sobre los ámbitos de seguridad y la administración basada en roles, vea [Conceptos básicos de la administración basada en roles de Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Revisar las acciones de migración  
 Cuando configure un trabajo de migración, el Asistente para crear trabajo de migración mostrará una lista de acciones que debe ejecutar para asegurar una migración correcta y una lista de acciones que Configuration Manager lleva a cabo durante la migración de los datos seleccionados. Revise esta información detenidamente para comprobar el resultado esperado.  

### <a name="schedule-migration-jobs"></a>Programar trabajos de migración  
 De forma predeterminada, un trabajo de migración se ejecuta inmediatamente después de crearlo. Pero puede especificar cuándo se ejecutará el trabajo de migración al crear el trabajo o al editar las propiedades del mismo. Puede programar la ejecución del trabajo de migración de esta forma:  

-   Ejecutar el trabajo ahora  

-   Ejecutar el trabajo a una hora de inicio específica  

-   No ejecutar el trabajo  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Especificar la resolución de conflictos para los datos migrados  
 De forma predeterminada, los trabajos de migración no sobrescriben datos en la base de datos de destino a menos que configure el trabajo de migración para omitir o sobrescribir los datos que se migraron anteriormente a la base de datos de destino.  

##  <a name="plan-for-collection-migration-jobs"></a><a name="About_Collection_Migration"></a> Planear trabajos de migración de recopilación  
 Los trabajos de migración de recopilaciones solo están disponibles cuando se migran datos de una jerarquía de origen que ejecuta una versión admitida de Configuration Manager 2007. Debe especificar una o más recopilaciones para la migración al migrar por recopilación. Para cada recopilación que se especifica, el trabajo de migración selecciona automáticamente todos los objetos relacionados para la migración. Por ejemplo, si selecciona una recopilación específica de usuarios, se identifican los miembros de la recopilación y puede migrar las implementaciones asociadas a esa recopilación. Si lo desea, puede seleccionar otros objetos de implementación asociados a esos miembros para la migración. Todos estos elementos seleccionados se agregan a la lista de objetos que se pueden migrar.  

 Cuando una recopilación se migra, Configuration Manager también migra las configuraciones de la recopilación (como las ventanas de mantenimiento y variables de la recopilación), pero no las configuraciones de la recopilación para el aprovisionamiento del cliente de AMT.  

 Use la información en las secciones siguientes para obtener información sobre las configuraciones adicionales que pueden corresponder a trabajos de migración basados en la recopilación.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Excluir objetos de trabajos de migración de recopilación  
 Puede excluir determinados objetos de un trabajo de migración de recopilación. Si excluye un determinado objeto de un trabajo de migración de recopilación, el objeto se agrega a una lista de exclusión global que tiene todos los objetos excluidos de los trabajos de migración creados para cualquier sitio de origen en la jerarquía de origen actual. Los objetos en la lista de exclusión siguen estando disponibles para la migración en futuros trabajos, pero no se incluyen automáticamente cuando se crea un nuevo trabajo de migración basado en recopilación.  

 Puede editar la lista de exclusión para quitar objetos previamente excluidos. Después de quitar un objeto de la lista de exclusión, se selecciona automáticamente cuando se especifica una recopilación asociada durante la creación de un nuevo trabajo de migración.  

### <a name="unsupported-collections"></a>Recopilaciones no admitidas  
 Configuration Manager puede migrar todas las recopilaciones de dispositivo o de usuario predeterminadas, y la mayoría de recopilaciones personalizadas de una jerarquía de origen de Configuration Manager 2007. Pero Configuration Manager no puede migrar recopilaciones que contienen usuarios y dispositivos en la misma recopilación.  

 No se pueden migrar las siguientes recopilaciones:  

-   Una recopilación que tiene usuarios y dispositivos.  

-   Una recopilación que tiene una referencia a una recopilación de otro tipo de recurso. Por ejemplo, una recopilación basada en dispositivo que tiene una recopilación secundaria o un vínculo a una recopilación basada en usuario. En este ejemplo, solo se migra la recopilación de nivel superior.  

-   Una recopilación que tiene una regla para incluir equipos desconocidos. La recopilación se migra, pero la regla para incluir equipos desconocidos no se migra.  

### <a name="empty-collections"></a>Recopilaciones vacías  
 Una recopilación vacía es una recopilación que no dispone de recursos asociados. Cuando Configuration Manager migra una recopilación vacía, la convierte en una carpeta organizativa que no tiene usuarios ni dispositivos. La carpeta se crea con el nombre de la recopilación vacía en el nodo **Recopilaciones de usuarios** o **Recopilaciones de dispositivos** en el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager.  

### <a name="linked-collections-and-subcollections"></a>Recopilaciones secundarias y recopilaciones vinculadas  
 Cuando migra recopilaciones vinculadas a otras recopilaciones o que tienen recopilaciones secundarias, Configuration Manager crea una carpeta en el nodo **Recopilaciones de usuarios** o **Recopilaciones de dispositivos**, además de las recopilaciones y recopilaciones secundarias vinculadas.  

### <a name="collection-dependencies-and-include-objects"></a>Dependencias de recopilaciones e inclusión de objetos  
 Cuando se especifica una recopilación para la migración en el Asistente para crear trabajo de migración, las recopilaciones dependientes se seleccionan automáticamente para incluirlas en el trabajo. Este comportamiento garantiza que todos los recursos necesarios están disponibles después de la migración.  

 Por ejemplo: se selecciona una recopilación para dispositivos que ejecutan Windows 10 y que se denomina **Win_10**. Esta recopilación se limita a una recopilación que tiene todos los sistemas operativos de cliente y que se denomina **Todos_Clientes**. La recopilación **Todos_Clientes** se seleccionará automáticamente para la migración.  

### <a name="collection-limiting"></a>Restricción de recopilación  
 Con la rama actual de Configuration Manager, las recopilaciones son datos globales y se evalúan en cada sitio de la jerarquía. Por lo tanto, planee cómo limitar el ámbito de una recopilación después de su migración. Durante la migración, puede identificar una recopilación de la jerarquía de destino que usará para limitar el ámbito de la recopilación que se está migrando a fin de que la recopilación migrada no incluya miembros no anticipados.  

 Por ejemplo, en Configuration Manager 2007, las recopilaciones se evalúan en el sitio que las crea y en los sitios secundarios. Se puede implementar un anuncio a solo un sitio secundario, lo que puede limitar el ámbito de ese anuncio a ese sitio secundario. En comparación, con la rama actual de Configuration Manager, las recopilaciones se evalúan en todos los sitios y después se evalúan los anuncios asociados en relación con cada sitio. La restricción de la recopilación le permite limitar los miembros de la recopilación en función de otra recopilación para evitar la adición de miembros inesperados a la recopilación.  

### <a name="site-code-replacement"></a>Reemplazo de código de sitio  
 Cuando migra una recopilación que tiene criterios que identifican un sitio de Configuration Manager 2007, debe especificar un determinado sitio de la jerarquía de destino. Esto garantiza que la recopilación migrada permanece operativa en su jerarquía de destino y su ámbito no se incrementa.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Especificar el comportamiento de anuncios migrados  
 De forma predeterminada, los trabajos de migración basados en recopilaciones deshabilitan los anuncios que migran a la jerarquía de destino. Esto incluye todos los programas que están asociados con el anuncio. Cuando crea un trabajo de migración basado en recopilación que tiene anuncios, verá la opción **Habilitar programas para la implementación en Configuration Manager después de migrar un anuncio** en la página **Configuración** del Asistente para crear trabajo de migración. Si selecciona esta opción, los programas asociados con los anuncios se habilitan después de su migración. Como práctica recomendada, no seleccione esta opción. En su lugar, habilite los programas después de migrarlos cuando pueda comprobar los clientes que los recibirán.  

> [!NOTE]  
>  Verá la opción **Habilitar programas para la implementación en Configuration Manager después de migrar un anuncio** solo cuando crea un trabajo de migración basado en una recopilación y si el trabajo de migración contiene anuncios.  

 Para habilitar un programa después de la migración, desactive **Deshabilitar este programa en equipos en los que esté anunciado** en la pestaña **Opciones avanzadas** de las propiedades del programa.  

##  <a name="plan-for-object-migration-jobs"></a><a name="About_Object_Migration"></a> Planear trabajos de migración de objetos  
 A diferencia de la migración de recopilaciones, debe seleccionar cada objeto y la instancia del objeto que se va a migrar. Puede seleccionar objetos individuales (como anuncios de una jerarquía de Configuration Manager 2007, una publicación de una jerarquía de System Center 2012 Configuration Manager o una jerarquía de la rama actual de Configuration Manager) para agregarlos a la lista de objetos que quiere migrar en relación con un determinado trabajo de migración. El trabajo de migración de objeto no migra al sitio de destino los objetos que no se agregan a la lista de migración.  

 Los trabajos de migración basados en objetos no tienen ninguna configuración adicional que se deba planear además de la aplicable a todos los trabajos de migración.  

##  <a name="plan-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a> Planear trabajos de migración de objetos migrados previamente  
 Si un objeto que ya se ha migrado a la jerarquía de destino se actualiza en la jerarquía de origen, puede migrarlo de nuevo mediante el tipo de trabajo **Objetos modificados después de la migración** . Por ejemplo, al cambiar el nombre o actualizar los archivos de origen de un paquete en la jerarquía de origen, la versión de paquete se incrementa en la jerarquía de origen. Después del incremento de la versión del paquete, el paquete se puede identificar para la migración mediante este tipo de trabajo.  

 Este tipo de trabajo es similar al tipo de migración de objeto, excepto que cuando se seleccionan objetos para la migración, solo puede seleccionar los que se actualizaron después de que un trabajo de migración anterior los migró.   

 Cuando se selecciona este tipo de trabajo, el comportamiento de resolución de conflictos en la página **Configuración** del Asistente para crear trabajo de migración se configura para sobrescribir los objetos migrados anteriormente. Esta configuración no se puede modificar.  

> [!NOTE]  
>  Este trabajo de migración puede identificar objetos que la jerarquía de origen actualiza automáticamente y objetos actualizados por usuarios administrativos.  
