---
title: Procedimientos recomendados para las colecciones
titleSuffix: Configuration Manager
description: Obtenga recomendaciones para configurar recopilaciones y la evaluación de recopilación en Configuration Manager.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b1bc72a3691e4a6f47c29a5a91ef11c92f0f7e7c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693291"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Procedimientos recomendados para recopilaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Algunas de las instrucciones para la administración de recopilaciones pueden ser contradictorias. Por ejemplo, por motivos de rendimiento, debe limitar el número de recopilaciones que se actualizan con frecuencia. Pero actualizar las recopilaciones con frecuencia resulta práctico, ya que la mayor parte de la funcionalidad de Configuration Manager depende de las recopilaciones. Cuando diseñe y configure recopilaciones y la evaluación de recopilación, considere cuidadosamente tanto los requisitos de negocio como los impactos en el rendimiento.

Use los procedimientos recomendados siguientes para las recopilaciones de Configuration Manager.  

## <a name="configure-maintenance-window-for-updates"></a>Configurar la ventana de mantenimiento para actualizaciones

Puede configurar ventanas de mantenimiento para que las colecciones de dispositivos restrinjan las horas a las que Configuration Manager puede instalar software en estos dispositivos. Si configura una ventana de mantenimiento demasiado pequeña, es posible que el cliente no pueda instalar las actualizaciones de software críticas, lo que hace que el cliente sea vulnerable a los problemas que la actualización mitiga.

Consideraciones importantes que se deben tener en cuenta al planear las ventanas de mantenimiento:

- El tiempo de ejecución máximo de actualización de software predeterminado es de 60 minutos.
- Cuando Configuration Manager calcula si una actualización puede instalarse, se agregan cinco minutos al tiempo de ejecución máximo para tener en cuenta el reinicio.
- La duración restante de una ventana de mantenimiento debe ser mayor que el tiempo de ejecución máximo de la actualización de software más cinco minutos.

## <a name="avoid-frequent-collection-evaluation"></a>Evitar la evaluación de recopilación frecuente

Una evaluación de recopilación completa no solo evalúa la recopilación de destino, sino también las recopilaciones que la recopilación limita si se produce una actualización. Además, una recopilación sin programación se sigue evaluando si la recopilación de restricción se actualiza. Por lo tanto, es posible que algunas recopilaciones se evalúen con más frecuencia de lo esperado.

En un entorno de Configuration Manager ocupado, puede mejorar el rendimiento de la evaluación de recopilación si se reducen las programaciones para evitar evaluaciones de recopilación repetidas. En un árbol profundo, puede disminuir la frecuencia de evaluación de recopilación a medida que las recopilaciones descienden más profundamente en el árbol, ya que las evaluaciones de recopilación de nivel superior también desencadenarán evaluaciones de recopilación de nivel inferior.

## <a name="understand-the-collection-evaluation-graph"></a>Entender el gráfico de evaluación de recopilación

Descubra cómo funciona el gráfico de evaluación de recopilación para que pueda diseñar una estructura de recopilación adecuada. No confíe en que la evaluación de recopilación completa actualizará siempre todas las recopilaciones. Si se actualiza una recopilación actualizada de manera incremental según una programación, es posible que las recopilaciones de referencia que no están habilitadas para actualizaciones incrementales no se actualicen. Como es probable que se produzcan actualizaciones durante las evaluaciones incrementales, es posible que una evaluación completa no actualice la recopilación, lo que finaliza el gráfico de evaluación de recopilación para ese ciclo. En ese caso, no se produce ninguna evaluación de la recopilación de referencia. Para más información, consulte [Gráfico de evaluación de recopilación](collection-evaluation.md#collection-evaluation-graph).

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a> Limitar las actualizaciones incrementales

Habilitar actualizaciones incrementales para muchas recopilaciones podría provocar retrasos en la evaluación. Es mejor limitar el número de recopilaciones actualizadas de manera incremental a 200. El número exacto depende de:

- El número total de recopilaciones
- La frecuencia con la que se agregan y cambian recursos nuevos en la jerarquía
- El número de clientes en una jerarquía
- La complejidad de las reglas de pertenencia de la recopilación en una jerarquía

Si el ciclo de evaluación incremental tarda más que la frecuencia de actualización configurada, Configuration Manager procesa evaluaciones de recopilación de manera constante, lo que podría impactar el rendimiento del sistema. Reduzca el número de recopilaciones actualizadas de manera incremental o aumente el tiempo entre los ciclos de evaluación incremental.

Dados los posibles impactos de las recopilaciones incrementales, es importante tener una directiva o un procedimiento para crear las recopilaciones y asignar las programaciones de actualización. Algunos ejemplos de consideraciones sobre directivas pueden ser:

- Use solo actualizaciones incrementales para las recopilaciones que se usan para el ámbito de seguridad, la configuración del cliente y las ventanas de mantenimiento. Estas actualizaciones de recopilación afectan el comportamiento del cliente y al acceso a los recursos.
- En el caso de las aplicaciones sin aprobación de licencias, anuncie las aplicaciones a las recopilaciones existentes y use condiciones globales para restringir la disponibilidad.
- Describa los períodos adecuados para otras recopilaciones que tienen programadas actualizaciones de recopilación completa.

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>Evitar la evaluación de árboles grandes desde el CAS

En un entorno de Configuration Manager, el sitio de administración central (CA) no evalúa la pertenencia de la recopilación. Los sitios principales son los únicos sitios que evalúan recopilaciones. Los sitios secundarios actúan como servidores proxy que usan solo los datos que replican desde el sitio principal.

Para solicitar una actualización de recopilación, el CA envía una solicitud a cada sitio principal. Los sitios principales evalúan la recopilación y devuelven los resultados al CA. Los resultados de la evaluación de recopilación solo aparecen después de que todas las instrucciones de evaluación de recopilación se replican a todos los sitios, todos los sitios evalúan todas las recopilaciones y todos los datos se devuelven al CAS y se consolidan.

En el diagrama siguiente se muestra el flujo cuando el CAS solicita una actualización de recopilación manual:

![Actualización de recopilación manual desde un CA](media/manual-collection-update-from-cas.png)

Una actualización de recopilación desde un CA con varios sitios principales puede llevar mucho tiempo. Si una recopilación no se evalúa a tiempo, resulta tentador repetir la solicitud.

Una vez que un subproceso de evaluación de recopilación comienza y carga el gráfico de evaluación, la evaluación continúa hasta que el gráfico de evaluación de recopilación está vacío. Luego, el subproceso finaliza y está disponible para la evaluación siguiente. Sin embargo, si otro ciclo de evaluación de recopilación se pone en cola mientras el subproceso evalúa las recopilaciones, el subproceso se reinicia de inmediato para intentar una evaluación del ciclo "perdido".

Cada método de evaluación se ejecuta en su propio subproceso. Es posible que dentro del subproceso, Configuration Manager intente representar gráficamente la misma recopilación más de una vez. A continuación, Configuration Manager quita la segunda solicitud y las subsiguientes.

Para evitar estos escenarios, evite las evaluaciones de recopilación manuales de árboles grandes, especialmente al trabajar desde el CA con varios sitios.

## <a name="consider-collection-depth-and-cross-referencing"></a>Considerar la profundidad de la recopilación y las referencias cruzadas

Para lograr un equilibrio entre los requisitos de negocio y el rendimiento, es importante comprender la estructura de recopilación que se crea y sus dependencias de otras recopilaciones. Si crea una recopilación con reglas que hacen referencia a una o varias recopilaciones que también hacen referencia a otras recopilaciones, se evalúan todas esas recopilaciones para crear la pertenencia de la recopilación.

Las reglas de recopilación de inclusión y exclusión de Configuration Manager hacen que las recopilaciones de referencia sean más sencillas que escribir una consulta WQL personalizada. Pero si el uso de recopilaciones de inclusión y exclusión genera una baja en el alto rendimiento, puede usar en su lugar el método de consulta WQL:

Inclusión:

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

Exclusión:

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>Usar CEViewer para supervisar la evaluación de recopilación

Puede usar [Collection Evaluation Viewer (CEViewer)](../../../support/ceviewer.md) para supervisar cuántas recopilaciones se evalúan y cuánto tarda cada recopilación en actualizarse. CEViewer está en la carpeta *CD.Latest* del servidor de sitio.

Para realizar manualmente una comprobación similar con SQL, puede usar la consulta siguiente:

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```