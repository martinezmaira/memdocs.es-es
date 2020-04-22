---
title: Administración de actualizaciones
titleSuffix: Configuration Manager
description: Administrar las actualizaciones que se implementan y crean con System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2cb1d1547c23357adbaa26e649e4e22a78e0f39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700193"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Administrar actualizaciones de software en Updates Publisher

*Se aplica a: System Center Updates Publisher*     

En System Center Updates Publisher, use el **área de trabajo Actualizaciones** para administrar actualizaciones y agrupaciones de software que haya importado al repositorio.  

Entre las tareas de administración se incluyen la duplicación, edición y expiración o reactivación de actualizaciones y agrupaciones, además de la asignación de actualizaciones y agrupaciones a publicaciones. También puede exportar catálogos personalizados para su uso con otras instalaciones de Updates Publisher.

Para obtener actualizaciones que pueda administrar:
-  [Agregue un catalogo de actualizaciones](updates-publisher-catalogs.md#add-software-update-catalogs) a su instalación de Updates Publisher.
-  [Importe](updates-publisher-catalogs.md#import-updates) las actualizaciones de ese catálogo al repositorio.

También puede [crear sus propias actualizaciones](create-updates-with-updates-publisher.md).



## <a name="create-a-duplicate-of-an-update"></a>Crear duplicados de una actualización
Puede crear duplicados, o copias, de actualizaciones que se encuentren en el repositorio. Luego, puede modificar la copia en lugar de modificar la actualización original. No puede crear copias de agrupaciones de actualizaciones.

Para crear una copia, seleccione una actualización en el **área de trabajo Actualizaciones** y luego elija **Duplicar**. La copia de la actualización aparecerá en la misma ubicación del área de trabajo Actualizaciones con *Copia de* agregado al nombre.

Una nueva copia que se cree tiene un estado de **Unexpired** (Vigente), pero, si no, conserva la configuración del original.

## <a name="edit-updates-and-bundles"></a>Editar actualizaciones y agrupaciones
Puede seleccionar actualizaciones y agrupaciones que se encuentren en el repositorio para modificarlas.

En el **área de trabajo Actualizaciones**, seleccione una actualización o agrupación y luego elija **Editar** en la pestaña **Inicio** para abrir el asistente de edición. Las actualizaciones y agrupaciones tienen asistentes independientes pero estrechamente relacionados que presentan las mismas opciones que los asistentes para [crear actualizaciones](create-updates-with-updates-publisher.md#use-the-create-update-wizard) o [crear agrupaciones](create-updates-with-updates-publisher.md#use-the-create-bundle-wizard).

Al editar, puede cambiar los detalles disponibles sobre la actualización o agrupación para poder usarlos en su entorno. Por ejemplo, puede editar las reglas de aplicabilidad o prioridad o cambiar el idioma. También puede cambiar el producto y proveedor para mover la actualización o agrupación a una carpeta personalizada con el fin de agrupar actualizaciones para su propio uso.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Asignar actualizaciones y agrupaciones a una publicación
Puede seleccionar actualizaciones y agrupaciones en el **área de trabajo Actualizaciones** y luego elegir **Asignar** en la pestaña **Inicio** de la cinta de opciones para agregarlas a una publicación. Se inicia el asistente para **Assign Software Updates** (Asignar actualizaciones de software).
-  Vea [Publicar actualizaciones y agrupaciones](#publish-updates-and-bundles-from-the-updates-workspace) para obtener información sobre cómo seleccionar y publicar actualizaciones y agrupaciones como una única tarea.
-  Vea [Administrar publicaciones](updates-publisher-publications.md) para obtener información sobre cómo administrar grupos de actualizaciones y agrupaciones como un único objeto. Después de asignar actualizaciones a una publicación, puede administrar esa publicación que, a su vez, incluye todas las actualizaciones asignadas.

Cuando asigna actualizaciones a una publicación:

-   Puede incluir actualizaciones y agrupaciones expiradas y sin expirar en la misma publicación.

-   Especifique el tipo de publicación:

    -   **Full Content** (Contenido completo): se publica todo el contenido de la actualización en el servidor WSUS. Incluye los metadatos y los archivos binarios de la actualización.

    -   **Solo metadatos**: solo se publican los metadatos; no se publican los archivos binarios de la actualización. Podría elegir esta opción cuando quiera recopilar datos de cumplimiento.

    -   **Automático**: este modo solo está disponible cuando Updates Publisher se ha conectado a Configuration Manager [vea la opción [ConfigMgr Server](updates-publisher-options.md#configmgr-server) (Servidor de ConfigMgr)].

    Con este tipo, Updates Publisher consulta Configuration Manager para determinar si las actualizaciones o agrupaciones se deben publicar con el contenido completo o solo con los metadatos. El contenido completo de una actualización solo se publica cuando la actualización cumple las condiciones de **Requested client count threshold** (Umbral de cuenta de clientes solicitados) y **Package source size threshold** (Umbral de tamaño de origen del paquete), que se especifiquen en la página **ConfigMgr Server** (Servidor de ConfigMgr) de opciones de Updates Publisher.

-   Seleccione una publiación:

    -   Use **Assign software update to existing publications** (Asignar actualización de software a publicaciones existentes) cuando ya haya creado la publicación que quiera usar. Esta opción no está disponible hasta que no exista como mínimo una publicación.

    -   Use **Assign software update to a new publication** (Asignar actualización de software a una nueva publicación) cuando no tenga una publicación adecuada. Se creará una publicación con el nombre que especifique.

Después de asignar actualizaciones a una publicación, puede usar el **área de trabajo Publicaciones** para [publicar](updates-publisher-publications.md#publish-publications) o [exportar](updates-publisher-publications.md#export-a-publication) la publicación como grupo.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publicar actualizaciones y agrupaciones desde el área de trabajo Actualizaciones
Cuando publica actualizaciones y agrupaciones, Updates Publisher agrega información sobre esas actualizaciones y agrupaciones (metadatos) y, posiblemente, los archivos binarios de las actualizaciones (contenido completo), a un servidor de actualización para la implementación en dispositivos.

Para tener la posibilidad de publicar, debe configurar la opción [Servidor de actualización](updates-publisher-options.md#update-server) de Updates Publisher. Para abrir esta opción de configuración, vaya a **Área de trabajo Actualizaciones** &gt;**Información general** y seleccione **Configure WSUS and Signing Certificate** (Configurar certificado de firma y WSUS). También puede ir a la página Servidor de actualización en las opciones de Updates Publisher.

Hay dos maneras de publicar actualizaciones y agrupaciones:
-   Directamente desde el área de trabajo Actualizaciones. (Vea el procedimiento siguiente, *Para publicar actualizaciones y agrupaciones*).
-   Como una [publicación](updates-publisher-publications.md#publish-publications) desde el área de trabajo Publicaciones.  

> [!NOTE]   
> Updates Publisher solo puede publicar actualizaciones cuyo tamaño sea de 375 megabytes (MB) o menos.

### <a name="to-publish-updates-and-bundles"></a>Para publicar actualizaciones y agrupaciones
1.  Vaya a **Updates Workspace** (Área de trabajo Actualizaciones) y seleccione una o varias actualizaciones y agrupaciones que quiera publicar. Luego elija **Publicar** en la pestaña **Inicio** de la cinta de opciones.

2.  En la página **Seleccionar** del asistente para **publicación**, seleccione cómo quiere publicar las actualizaciones. Las opciones son las mismas que para [asignar actualizaciones](#assign-updates-and-bundles-to-a-publication): **Full Content** (Contenido completo), **Solo metadatos** o **Automático**.

    También puede firmar todas las actualizaciones con un nuevo certificado de publicación.

3.  Complete el asistente.

Si la publicación no se lleva a cabo, se le ofrece un vínculo al archivo UpdatesPublisher.log que puede proporcionar más información.

## <a name="export-updates"></a>Exportar actualizaciones
Puede exportar actualizaciones y agrupaciones desde el repositorio de Updates Publisher para crear un catálogo de actualizaciones personalizado. Después, puede [agregar](updates-publisher-catalogs.md#add-software-update-catalogs) y luego [importar](updates-publisher-catalogs.md#import-updates) ese catálogo a otra instancia de Updates Publisher. (También puede [exportar actualizaciones como una publicación](updates-publisher-publications.md#export-a-publication)).

Para exportar directamente, vaya a **Updates Workspace** (Área de trabajo Actualizaciones)  > **Todas las actualizaciones de software** y seleccione una o más actualizaciones y agrupaciones. No puede exportar una carpeta de proveedor o producto, pero puede seleccionar una carpeta y luego elegir las actualizaciones de la carpeta que quiera exportar.

Con una o varias actualizaciones seleccionadas, elija **Exportar** en la pestaña **Inicio** de la cinta de opciones e indique una ruta de acceso y un nombre de archivo para la exportación del catálogo.

Tendrá la posibilidad de exportar (incluir) actualizaciones de software dependientes.

## <a name="delete-updates-and-bundles"></a>Eliminar actualizaciones y agrupaciones
Puede eliminar actualizaciones y agrupaciones de actualizaciones para quitarlas del repositorio de Updates Publisher.

Vaya a **Updates Workspace** (Área de trabajo Actualizaciones)  > **Todas las actualizaciones de software** y seleccione una o más actualizaciones individuales. Elija **Eliminar** en la pestaña **Inicio** de la cinta de opciones.

-   Si la selección solo contiene actualizaciones o agrupaciones que no se han publicado o que han expirado, se le pedirá que confirme la eliminación antes de quitarlas.

-   Si la selección incluye una actualización o agrupación que se ha publicado y aún no ha expirado, recibirá una advertencia. Debe hacer que esas actualizaciones [expiren](updates-publisher-publications.md#expire-or-reactivate-updates-and-bundles) y publicar ese cambio antes de eliminarlas del repositorio.  

Si elimina una actualización o agrupación de un proveedor y luego la importa de nuevo al catálogo, la actualización se restaura en el repositorio.

## <a name="manage-vendor-and-product-folders"></a>Administrar carpetas de proveedor y producto
Para ver una lista de proveedores, así como los productos de cada proveedor para el que haya importado o creado actualizaciones, vaya a **Updates Workspace** (Área de trabajo Actualizaciones)  > **Introducción** > **Todas las actualizaciones de software**.

Las carpetas de proveedores y productos las crea automáticamente Updates Publisher cuando se usa un asistente para importar o crear una actualización o agrupación de software. También puede crear estas carpetas manualmente.

-   Para crear una carpeta de proveedor, en el panel de navegación del **área de trabajo Actualizaciones**, haga clic con el botón derecho en **Todas las actualizaciones de software** y elija **Crear proveedor**.

-   Para crear una carpeta de producto en una carpeta de proveedor, haga clic con el botón derecho en esta carpeta y elija **Crear producto**.

Además de crear carpetas, puede cambiarle el nombre a cualquier carpeta de proveedor o producto del repositorio o eliminarla. Para ello, haga clic con el botón derecho en la carpeta y elija la opción que quiera, **Cambiar nombre** o **Eliminar**. Al eliminar una carpeta se quitan todas las actualizaciones y agrupaciones de esa carpeta y sus carpetas de producto del repositorio de Updates Publisher.

Puede mover actualizaciones entre carpetas de proveedor y producto, incluidas las creadas por usted. Para mover una actualización o agrupación a otra carpeta, debe seleccionar la actualización o agrupación y luego, **Editar**. Después, puede reasignar el proveedor y el producto en la página **Información** del asistente para editar actualizaciones. Cuando el asistente para **editar actualizaciones** termine, el cambio se aplica y la actualización se mueve a la nueva carpeta.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Ver el XML de una actualización o agrupación
Puede seleccionar una sola actualización o agrupación en el **área de trabajo Actualizaciones** y luego elegir **Ver XML** para mostrar la estructura XML de la actualización. No existe la posibilidad de modificar directamente la estructura XML.
