---
title: Administración de publicaciones
titleSuffix: Configuration Manager
description: Administrar grupos de actualizaciones de software como una publicación con System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e3dedef9ffe785ce7127fc371030cfd990d70e38
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608375"
---
# <a name="manage-publications-in-updates-publisher"></a>Administrar publicaciones en Updates Publisher

*Se aplica a: System Center Updates Publisher*

Puede usar publicaciones para administrar grupos de actualizaciones y agrupaciones como un único objeto. Esto incluye publicar las actualizaciones en un servidor de administración y exportar la publicación como un grupo para su uso con otra instalación de Updates Publisher.

## <a name="create-publications"></a>Crear publicaciones
Las publicaciones se crean de dos maneras:

-   Cuando administre actualizaciones y agrupaciones en el **área de trabajo Actualizaciones**, puede [asignarlas](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) a una nueva publicación que se cree en ese momento.

-   En el **área de trabajo Publicaciones**, puede usar el botón **Crear** de la pestaña **Publicación** de la cinta de opciones. Este método le permite crear una publicación para su uso en el futuro. Más adelante, cuando asigne actualizaciones, puede usar esta publicación.

## <a name="rename-a-publication"></a>Cambiar el nombre de una publicación
Para cambiar el nombre de una publicación, seleccione la publicación desde el **área de trabajo Publicaciones** y luego, en la pestaña **Publicación** de la cinta de opciones, elija **Editar**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Cambiar el tipo de publicación de actualizaciones de una publicación
En el **área de trabajo Publicaciones**, puede modificar el **tipo de publicación** de actualizaciones y agrupaciones que se hayan asignado a una publicación.

1. Seleccione la publicación que contiene las actualizaciones que quiere modificar y luego seleccione una o más actualizaciones o agrupaciones de la lista **Todas &lt;nombre de publicación> actualizaciones de miembro**.

2. Luego, en la pestaña **Inicio**, elija una de las opciones siguientes. Las opciones disponibles varían según el tipo de publicación de las actualizaciones que haya seleccionado.

   -   **Automática**
   -   **Full Content** (Contenido completo)
   -   **Solo metadatos**

Después de realizar un cambio, puede que tenga que actualizar la vista de publicación para ver los nuevos valores.

Para obtener información sobre los distintos tipos de publicación, vea [Asignar actualizaciones y agrupaciones a una publicación](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Cuando establece el tipo de publicación de una agrupación, todas las actualizaciones de software de esa agrupación se publican con el tipo de publicación de la agrupación.

## <a name="remove-updates-from-a-publication"></a>Quitar actualizaciones de una publicación
Para quitar actualizaciones o agrupaciones de una publicación, seleccione la publicación que quiere modificar en el **área de trabajo Publicaciones** y luego, las actualizaciones y agrupaciones que quiere quitar. Luego, en la pestaña **Inicio** de la cinta de opciones, elija **Quitar**.

Una vez quitadas de una publicación, las actualizaciones siguen disponibles en el repositorio de Updates Publisher.

## <a name="publish-publications"></a>Publicar publicaciones
Cuando publica actualizaciones y agrupaciones, Updates Publisher agrega información sobre esas actualizaciones y agrupaciones (metadatos) y, posiblemente, los archivos binarios de las actualizaciones (contenido completo), a un servidor de actualización para la implementación en dispositivos.

Para tener la posibilidad de publicar, debe configurar la opción [Servidor de actualización](updates-publisher-options.md#update-server) de Updates Publisher. Para abrir esta opción de configuración, vaya a **Área de trabajo Actualizaciones** &gt;**Información general** y seleccione **Configure WSUS and Signing Certificate** (Configurar certificado de firma y WSUS). También puede ir a la página Servidor de actualización en las opciones de Updates Publisher.

> [!NOTE]   
> Updates Publisher solo puede publicar actualizaciones cuyo tamaño sea de 375 megabytes (MB) o menos.

### <a name="to-publish-a-publication"></a>Para publicar una publicación

1. Vaya al **área de trabajo Publicaciones** y seleccione una publicación que contenga el grupo de actualizaciones y agrupaciones que quiere publicar o exportar. Luego elija **Publicar** en la pestaña **Inicio** de la cinta de opciones.

2. En la página **Seleccionar** del **Asistente para publicación** puede elegir firmar todas las actualizaciones con un nuevo certificado de publicación, pero no cambiar el tipo de publicación.

3. Complete el asistente.

   Si la publicación no se lleva a cabo, se le ofrece un vínculo al archivo UpdatesPublisher.log que puede proporcionar más información.

## <a name="export-a-publication"></a>Exportar una publicación
Puede exportar una publicación desde el repositorio de Updates Publisher. Al hacerlo, exporta las actualizaciones y agrupaciones que están asignadas a esa publicación y crea un catálogo de actualizaciones. Después, puede [agregar](updates-publisher-catalogs.md#add-software-update-catalogs) y luego [importar](updates-publisher-catalogs.md#import-updates) ese catálogo a otra instancia de Updates Publisher. También puede [exportar actualizaciones](manage-updates-with-updates-publisher.md#export-updates) que no formen parte de una publicación.

Para exportar una publicación, vaya al **área de trabajo Publicaciones** y seleccione la publicación que contiene las actualizaciones que quiere exportar. Solo pude seleccionar una publicación a la vez.

Con la publicación seleccionada, elija **Exportar** en la pestaña **Inicio** de la cinta de opciones e indique una ruta de acceso y un nombre de archivo para la exportación del catálogo.

También tendrá la posibilidad de exportar (incluir) actualizaciones de software dependientes como parte de la exportación.

## <a name="delete-a-publication"></a>Eliminación de una publicación
Para cambiar el nombre de una publicación, seleccione la publicación en el **área de trabajo Publicaciones** y luego elija **Editar** en la pestaña **Publicación** de la cinta de opciones.

Una vez quitada una publicación de Updates Publisher, las actualizaciones que estaban en la publicación siguen disponibles en el repositorio de Updates Publisher.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Expirar o reactivar actualizaciones y agrupaciones
Puede usar el **área de trabajo Actualizaciones** para seleccionar y luego hacer que expiren o reactivar actualizaciones y agrupaciones. Puede hacer expirar y reactivar actualizaciones y agrupaciones cuantas veces quiera.

-   **Para hacer que expiren actualizaciones o agrupaciones**, seleccione una o varias actualizaciones o agrupaciones que no hayan expirado en área de trabajo Actualizaciones y luego elija **Expirar** en la pestaña **Inicio**. La actualización o agrupación puede reactivarse hasta que se publique como expirada en Configuration Manager.

    Para poder quitar (eliminar) una actualización o agrupación personalizada de Configuration Manager, debe hacerla expirar y luego publicar ese estado de expirado en Configuration Manager. Una vez expiradas las actualizaciones o agrupaciones en Configuration Manager, ya no puede implementar ni reactivar la actualización o agrupación.

-   **Para reactivar actualizaciones o agrupaciones**, seleccione una o varias actualizaciones que hayan expirado en área de trabajo Actualizaciones y luego elija **Reactivar** en la pestaña **Inicio** de la cinta de opciones. Si la actualización expirada se publicó anteriormente como expirada en Configuration Manager, no puede reactivarse.
