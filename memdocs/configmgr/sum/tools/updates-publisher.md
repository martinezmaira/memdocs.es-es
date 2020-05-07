---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usar System Center Updates Publisher para administrar actualizaciones personalizadas
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700033"
---
# <a name="system-center-updates-publisher"></a>Editor de actualizaciones de System Center

*Se aplica a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) es una herramienta independiente que permite a proveedores de software independientes o desarrolladores de aplicaciones de línea de negocio administrar actualizaciones personalizadas. Esta actualización personalizada incluye actualizaciones que tienen dependencias, como controladores y agrupaciones de actualizaciones.

Con Updates Publisher, puede:

-   Importar actualizaciones de catálogos externos (catálogos de actualizaciones que no sean de Microsoft).
-   Modificar definiciones de actualización, incluidos metadatos de implementación y aplicabilidad.
-   Exportar actualizaciones a catálogos externos.
-   Publicar actualizaciones en un servidor de actualización.

Después de publicar actualizaciones en un servidor de actualización, puede usar Configuration Manager para detectar esas actualizaciones e implementarlas en los dispositivos administrados.

## <a name="workspaces"></a>Áreas de trabajo
Al abrir Updates Publisher, se abre de manera predeterminada en el nodo Introducción del *área de trabajo Actualizaciones*.

![Updates Publisher](media/console1.png)


Updates Publisher tiene cuatro áreas de trabajo que ayudan a organizarlo.


**Área de trabajo Actualizaciones:** use este área de trabajo para [crear](create-updates-with-updates-publisher.md) y [administrar](manage-updates-with-updates-publisher.md) actualizaciones de software y agrupaciones de actualizaciones. Esta área de trabajo incluye asignar actualizaciones y agrupaciones a una publicación, publicarlas y exportarlas a otro repositorio de Updates Publisher.

**Área de trabajo Publicaciones:** en esta área de trabajo se [administran las publicaciones](updates-publisher-publications.md). Una publicación es un grupo de actualizaciones que se crea para simplificar la exportación y publicación de las actualizaciones.

La administración de publicaciones incluye publicar actualizaciones en un servidor para que sus clientes pueden encontrarlas e instalarlas, exportar actualizaciones y agrupaciones para su uso con otras instalaciones de Updates Publisher o modificar el contenido o los detalles de una publicación.

**Área de trabajo Reglas:** aquí puede [administrar reglas de aplicabilidad](updates-publisher-applicability-rules.md) que puede guardar y luego usar con actualizaciones que implemente. Hay dos tipos de informes:

-   Reglas instalables: estas reglas ayudan a determinar si un cliente debe instalar una actualización.
-   Reglas instaladas: estas reglas comprueban si una actualización está ya instalada.

**Área de trabajo Catálogos:** use este espacio de trabajo para agregar y [administrar catálogos de actualizaciones de software](updates-publisher-catalogs.md). Esta área de trabajo incluye la importación de actualizaciones de software desde esos catálogos al repositorio de Updates Publisher.

## <a name="whats-new-in-system-center-updates-publisher"></a>Novedades de System Center Updates Publisher

>[!NOTE] 
> La última versión de System Center Updates Publisher se publicó el 6 de noviembre de 2019. Para obtener más información, vea la sección [Historial de versiones](#release-history).

Hay un nuevo modo de creación de System Center Updates Publisher para ayudarle a crear las actualizaciones. Al habilitar el modo de creación, se agrega un **Área de trabajo Categorías** a la pantalla de inicio. También se agrega un botón **Detectoid** nuevo al **Área de trabajo Actualizaciones** cuando se habilita el modo de creación.

### <a name="to-enable-authoring-mode"></a>Para habilitar el modo de creación

1. En la esquina superior izquierda de la consola, haga clic en la pestaña **Propiedades** de **Updates Publisher** y elija **Opciones**.
1. Vaya a las opciones **Creación**.
1. Active la casilla **Habilitar modo de creación**.

![Habilitación del modo de creación para Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Acerca del área de trabajo de categorías

El área de trabajo Categorías permite a los autores de actualizaciones organizar las que están relacionadas. Por ejemplo, si es un OEM, es posible que quiera organizar las actualizaciones en función de modelos o líneas de productos. Puede definir varias categorías y categorías secundarias, pero no categorías descendientes de las secundarias, ya que está limitado a dos niveles.

![Captura de pantalla del área de trabajo Categorías](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Asignación de una actualización a una categoría

Después de crear la actualización, puede asignarla a una categoría si la selecciona y hace clic en el botón **Clasificar**. También puede hacer clic con el botón derecho en la actualización y seleccionar **Clasificar**.

![Captura de pantalla de la clasificación de una actualización](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>Acerca de detectoids

Una vez que se ha habilitado el modo de creación, puede crear detectoids para las actualizaciones. Los detectoids son útiles cuando se tienen varias actualizaciones que usan la misma regla (o un conjunto de reglas) para determinar la aplicabilidad. En esos casos, tendría que crear un detectoid y asignarlo como requisito previo para una actualización. Puede asignar varios detectoids a una actualización que haya creado.


### <a name="create-a-detectoid"></a>Creación de un detectoid

1. Abra **Updates Workspace** (Área de trabajo Actualizaciones).
1. En la cinta, haga clic en el botón **Detectoid**.
1. Siga las indicaciones del asistente para crear el detectoid.



![Actualización de los requisitos previos mediante un detectoid](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>Historial de versiones

- [2019 RTW, versión 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Fecha de publicación: 6 de noviembre de 2019
- [Versión del paquete acumulativo de actualizaciones 6.0.283.0 de KB4462765](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Fecha de publicación: 7 de septiembre de 2018
- [2017 RTW versión 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Fecha de publicación: 26 de marzo de 2018


## <a name="next-steps"></a>Pasos siguientes
Para empezar, primero [instale](install-updates-publisher.md) y luego [configure opciones](updates-publisher-options.md) de Updates Publisher.
