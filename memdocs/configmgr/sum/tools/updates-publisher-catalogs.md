---
title: Administrar catálogos de actualizaciones
titleSuffix: Configuration Manager
description: Administrar catálogos de actualizaciones de software con System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1314e2b4a6adc21b876e6bdbf8b25aa9e4fd3e9a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700133"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Administrar catálogos de actualizaciones de software en Updates Publisher

*Se aplica a: System Center Updates Publisher*

Use el **Área de trabajo** **Catálogos** para administrar catálogos de actualizaciones de software. Esto incluye agregar nuevos catálogos, administrar suscripciones de catálogo existentes e importar información sobre las actualizaciones de un catálogo en el repositorio de Updates Publisher.

Los catálogos de actualizaciones de software contienen información sobre actualizaciones relacionadas que han creado organizaciones distintas a Microsoft. Otras organizaciones incluyen los proveedores de software de terceros y de su propia organización que hayan registrado sus catálogos con Microsoft. Los catálogos de proveedores de software registrados se denominan *catálogos de partner*. Los catálogos que se crean y no están registrados con Microsoft se denominan catálogos de *usuario*.

## <a name="add-software-update-catalogs"></a>Agregar catálogos de actualizaciones de software
Debe agregar un catálogo de actualizaciones a Updates Publisher para poder administrar las actualizaciones que contiene. Cuando agrega un catálogo, Updates Publisher:
-   Crea una suscripción a ese catálogo para así poder buscar actualizaciones en el mismo.
-   Se agrega el catálogo a una lista de la ventana **My Software Update Catalogs** (Mis catálogos de actualizaciones de software) del **área de trabajo Catálogos**.  

La información sobre cada catálogo suscrito está disponible en la consola. Esta información incluye la dirección URL o ubicación de descarga, el nombre de la compañía u organización que crea el catálogo y cuándo se Ha importado o modificado por última vez.

Updates Publisher puede buscar cambios en las suscripciones automáticamente cada vez que se inicia. Esto se configura como una [Opción avanzada](updates-publisher-options.md#advanced). Una vez configurada, Updates Publisher hace referencia a la información de dirección URL o ubicación de descarga de la suscripción y le alerta cuando hay cambios en el catálogo realizados desde la última vez que se importó al repositorio.

Para buscar manualmente una actualización del catálogo, seleccione el catálogo de la lista **My Software Update Catalogs** (Mis catálogos de actualizaciones de software) y elija **Actualizar** en la cinta de opciones.

Además de agregar catálogos y visualizar información sobre catálogos suscritos, puede:
-  **Editar** información de catálogos de *usuario*.
-  **Eliminar** (quitar)un catálogo de Updates Publisher.
-  **Importar** actualizaciones de un catálogo al repositorio de Updates Publisher. Al importar actualizaciones, se importan todas las actualizaciones contenidas en el catálogo. Puede ver las actualizaciones en el área de trabajo Actualizaciones, donde luego puede seleccionar y publicar actualizaciones en el servidor de actualización.

> [!NOTE]   
> Si se elimina un catálogo de Updates Publisher, el catálogo se quita del repositorio. Esto no afecta a las actualizaciones que se hayan publicado en el servidor de actualización. Para quitar actualizaciones del servidor de actualización que ya no están en el repositorio, vea [Expirar actualizaciones de software sin referencia](updates-publisher-options.md#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Administrar catálogos de actualizaciones
Puede ver la lista de catálogos que ha importado en la ventana **My Software Update Catalogs** (Mis catálogos de actualizaciones de software) del **área de trabajo Catálogos**. En esta área de trabajo puede:

-   **Add a partner catalog** (Agregar un catálogo de partner): use una de las opciones siguientes para buscar nuevos catálogos de partner:

    -   En la consola, vaya a **Updates Workspace** (Área de trabajo Actualizaciones)  > **Introducción**. En la ventana **Introducción**, elija **Add Partner Software Updates Catalogs** (Agregar catálogos de actualizaciones de software de partner).

    -   En la consola, vaya a **Catalogs Workspace** (Área de trabajo Catálogos) > **Mis catálogos**. Luego, en la cinta de opciones, elija **Add Catalogs** (Agregar catálogos).

-   **Add a user catalog** (Agregar catálogo de usuario): en la consola, vaya a **Catalogs Workspace** (Área de trabajo Catálogos) > **Mis catálogos**. Luego, en la cinta de opciones, elija **Add Catalogs** (Agregar catálogos). Además de la ubicación del archivo .cab, debe especificar un Editor, Nombre y Descripción que identifique el catálogo.


-   **Buscar actualizaciones a catálogos**: seleccione uno o más catálogos y luego elija **Actualizar** en la cinta de opciones.

-   **Editar un catálogo de usuario**: seleccione un catalogo de *usuario* y luego elija **Editar** en la cinta de opciones. Luego puede modificar las propiedades definidas por el usuario.

-   **Eliminar catálogos**: seleccione uno o más catálogos y luego elija **Quitar** en la cinta de opciones. Se eliminan el catálogo, la suscripción y las actualizaciones de esos catálogos del repositorio de Updates Publisher.

-   **Agregar actualizaciones de un catálogo al repositorio**: elija **Importar** en la cinta de opciones para iniciar el asistente para **importar catálogos**. Para obtener más información, vea [Importar actualizaciones](#import-updates)

## <a name="import-updates"></a>Importar actualizaciones
Cuando se importa un catálogo, Updates Manager agrega las actualizaciones de ese catálogo al repositorio de Updates Publisher. Una vez importadas las actualizaciones, puede publicarlas en el servidor de actualización para ponerlas a disposición de los dispositivos administrados.

### <a name="to-import-updates"></a>Para importar actualizaciones
1. Para iniciar el asistente para **importar catálogos**, elija **Importar** en la cinta de opciones de una de las áreas de trabajo siguientes:

   -   Área de trabajo Catálogos

   -   Área de trabajo Actualizaciones

2. En la página **Tipo de importación**, seleccione uno o varios catálogos que haya agregado a Updates Publisher o especifique una ruta de acceso a un catálogo que aún no haya agregado como suscripción. Elija **Siguiente** para ver la pantalla de resumen y, cuando esté listo, elija **Siguiente** para iniciar la importación.

3. En la ventana **Security Warning – Catalog Validation** (Advertencia de seguridad: validación de catálogos), revise el certificado del catálogo y, cuando esté listo, elija **Aceptar** para importar las actualizaciones.

   > [!CAUTION]
   > Acepto solo actualizaciones de editores en los que confíe. Las actualizaciones de software de editores que no son de confianza puede dañar los equipos cliente al buscar actualizaciones.
   > 
   >  Si ya no confía en un editor, quítelo de la lista de editores de confianza. Para encontrar más información sobre la aceptación de catálogos, haga clic en **Información** en el cuadro de diálogo **Security Warning – Catalog Validation** (Advertencia de seguridad: validación de catálogos).

   Si opta por aceptar siempre los catálogos de un editor, el editor se agrega a la [lista de publicadores de confianza](updates-publisher-options.md#trusted-publishers). Puede revisar y modificar esta lista como opción de Updates Publisher.

4. La importación omite la importación de una actualización cuando esta se encuentra ya en el repositorio y se cumple alguna de las siguientes condiciones:

   -   La actualización no ha cambiado desde la última vez que se importó.

   -   La actualización se ha modificado y tiene un nuevo hash digital. La edición de una actualización evita que una nueva actualización sobrescriba el original, ya que, de hacerlo, sobrescribiría los cambios que se hubiesen implementado.

5. En la página **Confirmación**, revise los resultados de la importación.

6. Haga clic en **Cerrar** para finalizar el asistente. Ahora puede ver las actualizaciones de este catálogo en el área de trabajo Actualizaciones.

## <a name="next-steps"></a>Pasos siguientes
Entre las acciones comunes que se realizan después de importar actualizaciones, se incluyen:
-   [Administrar actualizaciones](manage-updates-with-updates-publisher.md) en una agrupación, asignarlas e implementarlas en el servidor de actualización.
-   [Crear reglas de aplicabilidad](updates-publisher-applicability-rules.md) que le ayuden a determinar cuándo se implementan las actualizaciones en el servidor de actualización.
