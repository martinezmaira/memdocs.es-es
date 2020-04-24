---
title: Reglas de aplicabilidad
titleSuffix: Configuration Manager
description: Administrar reglas de aplicabilidad para System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53a3aabfe65449723bdb6076486128b76a1a830c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078437"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Administrar reglas de aplicabilidad para Updates Publisher

*Se aplica a: System Center Updates Publisher*

Con Updates Publisher, las reglas de aplicabilidad definen requisitos que han de cumplirse para que un dispositivo pueda instalar una actualización. Las reglas se usan también para determinar si el equipo tiene instalada una actualización. Una regla de aplicabilidad compleja con varios elementos se denomina conjunto de reglas.

Las agrupaciones de actualizaciones no usan reglas de aplicabilidad.

## <a name="overview-of-applicability-rules"></a>Información general sobre las reglas de aplicabilidad
Las reglas de aplicabilidad se administran desde el **espacio de trabajo Reglas**. Cuando se crea una regla, se especifican una o más condiciones. Cuando se especifican varias condiciones, se pueden configurar relaciones entre ellas para que se evalúen consecutivamente o se combinen en instrucciones lógicas **And** u **Or**.

Por ejemplo, el siguiente conjunto de reglas contiene tres reglas. La primera regla comprueba que el archivo *MyFile* existe. La segunda y la tercera comprueban que el idioma del sistema operativo Windows es inglés o japonés.

``` Example
And  
  File '\[PROGRAM\_FILES\] \\Microsoft\\MyFile' exists  
  Or  
    Windows Language is English
    Windows Language is Japanese
```

Todas las actualizaciones requieren como mínimo una regla de aplicabilidad. Las actualizaciones que se importan tienen ya reglas de aplicabilidad aplicadas y, cuando se crean actualizaciones, hay que agregarles una o más reglas. En Updates Publisher, cualquier actualización se puede modificar y expandir en las reglas.

Para ver las reglas que se han creado, seleccione una regla en la lista **My saved rules** (Mis reglas guardadas) del **área de trabajo Reglas**. Las condiciones individuales y las operaciones lógicas de cada regla se muestran en el panel **Applicability Rules** (Reglas de aplicabilidad) de la consola. Las reglas de las actualizaciones que se importan solo se pueden ver y modificar cuando se edita la actualización.

Puede crear reglas de aplicabilidad en dos ubicaciones de Updates Publisher:

-   En el **área de trabajo Reglas** , se crean y **guardan** conjuntos de reglas que pueden usarse más adelante. Al editar o crear una actualización, puede seleccionar **Saved rule** (Regla guardada) como **Tipo de regla** y luego seleccionar en una lista de conjuntos de reglas creados previamente.

-   También puede crear otras reglas en el momento que crea o edita una actualización. Las reglas que cree de esta manera no se guardan para su uso en el futuro.

## <a name="create-applicability-rule"></a>Crear reglas de aplicabilidad
La información siguiente es similar a la correspondiente a cómo se crean reglas desde el asistente para [crear actualizaciones](create-updates-with-updates-publisher.md#use-the-create-update-wizard). Pero, a diferencia del asistente, tiene la posibilidad de guardar los conjuntos de reglas para su uso en el futuro.

1. En el **área de trabajo Reglas**, elija **Crear** para abrir el **Asistente para crear reglas**.

2. Especifique un nombre para la regla y haga clic en ![Nueva regla](media/newrule.png). Se abrirá la página **Applicability Rule** (Regla de aplicabilidad), donde puede configurar reglas.

3. Como **Tipo de regla**, seleccione uno de los siguientes. Las opciones que hay que configurar varían en función de cada tipo:

   - **Archivo**: use esta regla para exigir que un dispositivo tenga un archivo con propiedades que cumplan uno o más criterios que se especifiquen para poder aplicar esta actualización.

   - **Registro**: use este tipo para especificar detalles del Registro que deben estar presentes para que un dispositivo cumpla los requisitos para instalar esta actualización.

   - **Sistema**: esta regla usa detalles del sistema para determinar la aplicabilidad. Puede elegir entre definir una versión de Windows, un idioma de Windows o la arquitectura del procesador, o especificar una consulta WMI que identifique el sistema operativo de los dispositivos.

   - **Windows Installer**: use este tipo de regla para determinar la aplicabilidad en función de un .MSI instalado o una revisión de Windows Installer (.MSP). También puede determinar si determinados componentes o características se instalan como parte del requisito.

     > [!IMPORTANT]   
     > En dispositivos administrados, el nuevo Agente de Windows Update no puede detectar paquetes de instalación de Windows instalados por usuario. Cuando use este tipo de regla, configure reglas de aplicabilidad adicionales, como versiones de archivo o valores de la clave del Registro, para que el paquete de Windows Installer pueda detectarse adecuadamente independientemente del criterio, por usuario o por sistema.

   - **Saved rule** (Regla guardada): esta opción le permite buscar y usar reglas que haya configurado y guardado anteriormente.

4. Continúe agregando y configurando otras reglas que quiera.

5. Use los botones de operaciones lógicas para ordenar y agrupar distintas reglas con el fin de crear comprobaciones de requisitos previos de mayor complejidad.

6. Cuando el conjunto de reglas esté completo, haga clic en **Aceptar** para guardarlo. El conjunto de reglas aparece ahora en la lista **My saved rules** (Mis reglas guardadas).

## <a name="edit-applicability-rule-sets"></a>Editar conjuntos de reglas de aplicabilidad
Para editar una regla de aplicabilidad, seleccione una regla que se haya guardado en la lista **My saved rules** (Mis reglas guardadas) del **área de trabajo Reglas** y elija **Editar** en la cinta de opciones. Se abrirá el asistente para **editar reglas**.

Este asistente**editar reglas** muestra las reglas actuales del conjunto de reglas. Edite las reglas de la misma manera que usa el asistente para **crear reglas** para crear otras reglas. Puede usar este asistente para cambiar el nombre del conjunto de reglas, eliminar reglas, cambiar el orden de reglas y relaciones o agregar nuevas reglas.

Después de realizar cambios, elija **Aceptar** para guardar los cambios y cerrar el asistente.

Para obtener información más detallada sobre cómo usar el asistente para reglas, vea el **paso 7**, la página de aplicabilidad o el asistente para [crear actualizaciones](create-updates-with-updates-publisher.md#use-the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Eliminar reglas de aplicabilidad
Para eliminar una regla de aplicabilidad, seleccione la regla o el conjunto de reglas en la lista **My saved rules** (Mis reglas guardadas) del **área de trabajo Reglas** y elija **Eliminar** en la cinta de opciones. De este modo se quita la regla o el conjunto de reglas guardados de Updates Publisher.

Para eliminar una regla de una actualización concreta, debe [editar la actualización](manage-updates-with-updates-publisher.md#edit-updates-and-bundles).
