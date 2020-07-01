---
title: Evaluación de colecciones
titleSuffix: Configuration Manager
description: Obtenga información sobre el proceso, los tipos y los desencadenadores de la evaluación de recopilación. Entienda la jerarquía y el gráfico de la evaluación de recopilación.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: af90154b848ddcd7cbff21917ef122ab10585098
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663865"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Evaluación de recopilación en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager usa la *evaluación de recopilación* para actualizar la pertenencia a la recopilación en función de las reglas de recopilación que define. El tiempo y el ámbito de la evaluación de recopilación difieren según el tipo de evaluación y la configuración del sitio y la recopilación. 

Es importante comprender el comportamiento de la evaluación de recopilación poder tomar las decisiones de diseño de recopilación adecuadas. Para recomendaciones e instrucciones para la evaluación de recopilación, consulte [Procedimientos recomendados para recopilaciones](best-practices-for-collections.md).

## <a name="evaluation-process"></a>Proceso de evaluación

El archivo [colleval.log](https://docs.microsoft.com/mem/configmgr/core/plan-design/hierarchy/log-files#BKMK_ServerLogs) registra cuando el evaluador de recopilación crea, cambia y elimina recopilaciones.

En un alto nivel, cada evaluación y actualización de una recopilación individual sigue estos pasos:

![Proceso de actualización de recopilación de alto nivel](media/high-level-collection-update-process.png)

1. Ejecute la consulta de recopilación.
1. Agregue los sistemas que son miembros directos.
1. Evalúe todas las recopilaciones de *inclusión*.
   
   Si las recopilaciones de inclusión también tienen reglas de consulta o tiene recopilaciones de inclusión o exclusión, también debe evaluarlas. Si las recopilaciones de inclusión son recopilaciones de restricción, evalúe las recopilaciones que hay debajo de ellas. Después de evaluar totalmente el árbol, devuelva los resultados a la recopilación que realiza la llamada.
   
1. Realice una operación lógica `AND` entre los resultados devueltos y la recopilación con restricción.
1. Evalúe las recopilaciones de *exclusión*.
   
   Si las recopilaciones de exclusión también tienen reglas de consulta o tiene recopilaciones de inclusión o exclusión, también debe evaluarlas. Si estas recopilaciones son recopilaciones con restricción, evalúe las recopilaciones que hay debajo de ellas. Después de evaluar totalmente el árbol, devuelva los resultados a la recopilación que realiza la llamada.
   
1. Compare el conjunto de resultados de la evaluación de los miembros directos y las recopilaciones de inclusión con los resultados de la evaluación de las recopilaciones de exclusión.
1. Escriba los cambios en la base de datos y realice las actualizaciones.
1. Desencadene también la actualización de todas las recopilaciones dependientes. Las recopilaciones dependientes son recopilaciones que la recopilación actual limita o que hacen referencia a la recopilación actual mediante reglas de inclusión o exclusión.

## <a name="collection-evaluation-types-and-triggers"></a>Desencadenadores y tipos de evaluación de recopilación

Estos tipos de subprocesos controlan la evaluación de recopilación según el tipo de evaluación:

- **Principal** para actualizaciones de recopilación programadas
- **Auxiliar** para actualizar manualmente recopilaciones con recopilaciones dependientes
- **Única** para actualizar manualmente recopilaciones sin recopilaciones dependientes
- **Rápida** para actualizaciones de recopilación incrementales

En la tabla siguiente se describen los desencadenadores de evaluación de recopilación y los tipos de evaluación correspondientes. 

| Desencadenador | Tipo de evaluación | Descripción |
|---------|-----------------|-------------|
|Manual|Única o Auxiliar|Manual es la evaluación de recopilación con la prioridad más alta. Cuando un administrador solicita una evaluación de recopilación manual, el evaluador de recopilación asigna el subproceso de evaluación disponible siguiente a la evaluación.|
|Programado|Principal|El proceso de evaluación programada es el mismo que el de la evaluación manual, excepto en que la evaluación se basa en tiempo en lugar de basarse en eventos.|
|Almacenamiento provisional|Única o Auxiliar|Todas las recopilaciones dependen directa o indirectamente de **Todos los sistemas** o **Todos los usuarios y grupos de usuarios**. Ambos tipos de recopilaciones hacen una evaluación de recopilación completa todos los días a las 04:00 a.m. Un cambio en cualquiera de estas recopilaciones desencadena las actualizaciones de las recopilaciones dependientes, según un [gráfico de toda la recopilación](#collection-evaluation-graph).
|Incremental|Rápida|La evaluación incremental usa un gráfico de evaluación de recopilación para evaluar y actualizar las recopilaciones dependientes si una actualización de la pertenencia de la recopilación incremental cambia. Configuration Manager supervisa y actualiza objetos de recursos en todas las recopilaciones que están configuradas para actualizaciones incrementales.<br /><br />Si una consulta de recopilación se basa en información que se actualizará más adelante, como el inventario de hardware, Configuration Manager solo agrega o quita el recurso de la recopilación durante la actualización de recopilación programada.|

## <a name="collection-evaluation-graph"></a>Gráfico de evaluación de recopilación

Un *gráfico de evaluación de recopilación* asigna todas las recopilaciones que se relacionan con la recopilación destinada para evaluación. Una evaluación de recopilación implica la recopilación de destino y todas las recopilaciones relacionadas en el gráfico de evaluación de recopilación.

Cuando se inicia la evaluación de recopilación, Configuration Manager crea un gráfico que incluye todas las recopilaciones que podrían necesitar evaluarse como resultado de los cambios en la recopilación de destino, empezando por el nivel más alto del ciclo. A continuación, el evaluador de recopilación se desplaza por el gráfico en orden, evaluando a su vez la pertenencia a la recopilación. Una vez que la recopilación se evalúa por completo, el evaluador de recopilación quita las recopilaciones de nivel inferior que no se ven afectadas por este ciclo del gráfico de evaluación de recopilación.

Si una o varias de las recopilaciones que se van a evaluar tienen una regla de inclusión o exclusión, el evaluador de recopilación agrega al gráfico la recopilación incluida o excluida, junto con cualquier recopilación que la recopilación limite. Si se produce algún cambio durante la evaluación de las recopilaciones de inclusión y exclusión, el gráfico continúa en esa rama antes de volver a la rama principal.

Configuration Manager compila dos tipos de gráficos de evaluación, *incremental* o *total*.

### <a name="incremental-collection-evaluation"></a>Evaluación de recopilación incremental

Cuando cambian los datos de una tabla, un desencadenador SQL inserta una fila en la tabla **CollectionNotifications**. La próxima vez que se active una programación de evaluación de recopilación, realiza una operación `AND` del id. de recurso con la consulta de recopilación existente y desencadena actualizaciones de las recopilaciones que están habilitadas para las recopilaciones *incrementales*.

La evaluación de recopilación incremental ejecuta una consulta por máquina. La configuración de sitio predeterminada para la evaluación de recopilación incremental es cada cinco minutos.

Un gráfico de evaluación de recopilación incremental asigna las recopilaciones a las que se hace referencia solo si están habilitadas para la evaluación incremental. Si una evaluación incremental se limita a una recopilación que no está habilitada para la evaluación incremental, el gráfico evalúa la recopilación en función de la pertenencia existente de la recopilación de restricción. 

Por ejemplo, en el diagrama siguiente se muestran recursos recién detectados que se aplican a todas las recopilaciones. Sin embargo, la evaluación de recopilación solo actualiza las recopilaciones **Todos los servidores** y **Todos los controladores de dominio**. El evaluador de recopilación no evalúa las demás recopilaciones, porque la recopilación **Todos los servidores miembro** no está habilitada para la evaluación incremental.

![Ejemplo de gráfico de evaluación de recopilación incremental](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>Evaluación de recopilación completa

Las evaluaciones de recopilación manuales o programadas crean un gráfico de evaluación de una recopilación *completa* de todas las recopilaciones dependientes. El gráfico incluye todas las recopilaciones que hacen referencia a la recopilación que se está actualizando y las recopilaciones subsiguientes. Configuration Manager continúa evaluando el gráfico siempre que se produzcan actualizaciones en las recopilaciones que se están procesando.

En el diagrama siguiente se muestra cómo una solicitud de actualización de recopilación programada o manual de la recopilación **Todos los servidores** genera un gráfico completo que incluye todas las recopilaciones aplicables. Los recursos nuevos de controlador de dominio y servidor DNS están dentro del ámbito de las consultas de pertenencia de todas las recopilaciones, por lo que se actualizan todas las recopilaciones.

![Ejemplo 1 de gráfico de evaluación de recopilación completa](media/full-collection-evaluation-graph-1.png)

Una evaluación completa no siempre evalúa todas las recopilaciones. El gráfico de evaluación de recopilación solo continúa evaluando recopilaciones dependientes si se produce una actualización en la recopilación actual a la que se hace referencia. Si se actualiza una recopilación actualizada de manera incremental durante evaluaciones incrementales programadas, es posible que las recopilaciones de referencia que no están habilitadas para actualizaciones incrementales no se actualicen. Una evaluación completa no actualiza la recopilación, lo que finaliza el gráfico de evaluación de recopilación y cualquier evaluación de recopilación de referencia para ese ciclo. 

En el ejemplo siguiente, instalar DNS en el servidor existente lo convierte en miembro de la recopilación **Servidores DNS**, pero como no hay actualizaciones de su recopilación **Todos los servidores miembro** de restricción, la evaluación completa no evalúa la recopilación **Servidores DNS**. El ciclo de evaluación incremental siguiente evaluará la recopilación **Servidores DNS**, porque se trata de una recopilación incremental.

![Ejemplo 2 de gráfico de evaluación de recopilación completa](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>Pasos siguientes
- [Cómo crear recopilaciones](create-collections.md)
- [Procedimientos recomendados para recopilaciones](best-practices-for-collections.md)
- [Collection Evaluation Viewer](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer)
- Sesión [ConfigMgrDogs Troubleshoot ConfigMgr 2012](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411) en TechEd Australia
