---
title: Introducción a las consultas
titleSuffix: Configuration Manager
description: Cree y ejecute consultas para buscar objetos en una jerarquía de Configuration Manager que coincidan con los criterios de consulta.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694573"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Introducción a las consultas en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede crear y ejecutar consultas para buscar objetos en una jerarquía de Configuration Manager que coincidan con los criterios de consulta. Estos objetos incluyen elementos, como tipos específicos de equipos o grupos de usuarios. Las consultas pueden devolver la mayoría de los tipos de objetos de Configuration Manager, que incluyen sitios, recopilaciones, aplicaciones y datos de inventario.  

## <a name="query-creation-overview"></a>Información general sobre la creación de consultas

 Al crear una consulta, debe especificar un mínimo de dos parámetros: donde quiere buscar y lo que quiere buscar. Por ejemplo, para averiguar la cantidad de espacio en disco duro que está disponible en todos los equipos de un sitio de Configuration Manager, puede crear una consulta para buscar la clase de atributos **Disco lógico** y el atributo **Espacio libre (MB)** para el espacio disponible en disco.  

 Después de crear una consulta inicial, puede especificar criterios adicionales de consulta. Por ejemplo, puede especificar que los resultados de la consulta solo incluyan los equipos que estén asignados a un sitio especificado. También puede modificar cómo se muestran los resultados para que pueda verlos en el orden que prefiera. Por ejemplo, puede especificar que los resultados se ordenen según la cantidad de espacio libre en disco en orden ascendente o descendente.  

 Cuando se crea una consulta, Configuration Manager la almacena y se muestra en el nodo **Consultas** del área de trabajo **Supervisión**. Desde esta ubicación, puede crear consultas y ejecutar, actualizar y administrar las consultas existentes.  

 También puede importar una consulta en una regla de consulta de una recopilación de Configuration Manager. Para obtener más información, vea [Creación de recopilaciones](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Pasos siguientes

 [Cómo crear consultas](../../../core/servers/manage/create-queries.md)
