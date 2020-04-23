---
title: Collection Evaluation Viewer
titleSuffix: Configuration Manager
description: Use Collection Evaluation Viewer para ver el proceso de evaluación de colecciones de Configuration Manager y solucionar problemas en él.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707893"
---
# <a name="collection-evaluation-viewer"></a>Collection Evaluation Viewer

*Se aplica a: Configuration Manager (rama actual)*

Collection Evaluation Viewer es una de las [herramientas de Configuration Manager](tools.md). Úsela para ver el proceso de evaluación de colecciones en el servidor de sitio primario y solucionar problemas.

La herramienta muestra la siguiente información:  

- Información histórica y actual de las evaluaciones de colecciones completas e incrementales  

- El estado de la cola de evaluación  

- La hora a la que van a finalizar las evaluaciones de colecciones  

- Las colecciones que se están evaluando  

- La hora estimada de inicio y finalización de una evaluación de colecciones  



## <a name="about-collection-evaluation"></a>Acerca de la evaluación de colecciones

El proceso de evaluación de colecciones se ejecuta mediante la evaluación de las reglas de pertenencia de una colección para actualizar sus miembros. El sitio coloca una colección que se está evaluando en una de cuatro colas diferentes:  

- **Cola manual**: para las recopilaciones que un administrador ha seleccionado manualmente para evaluar desde la consola.  

- **Nueva cola**: para nuevas recopilaciones.  

- **Cola completa**: para aquellas recopilaciones a las que se va a realizar una evaluación completa.  

- **Cola incremental**: para recopilaciones con una evaluación incremental.  

Hay cuatro subprocesos que se ejecutan para evaluar las colecciones de las colas anteriores. Cada cola incluye una serie de matrices y cada matriz incluye las colecciones que se van a evaluar. El subproceso que se está ejecutando para la cola selecciona una colección de la matriz y ejecuta la evaluación. La longitud de la cola indica el número de matrices de la cola.



## <a name="requirements"></a>Requisitos

- Ejecutar la herramienta en el servidor de sitio  

- Que un usuario administrativo con el rol **Analista de solo lectura**, como mínimo, ejecute la herramienta  

- El usuario también necesita permiso de **lectura** en la base de datos de sitio en SQL



## <a name="usage"></a>Uso

Ejecute **CEViewer.exe**. El menú principal de la herramienta contiene las siguientes pestañas: 

- [Conectar](#bkmk_connect): establece la conexión inicial con el servidor de sitio primario y SQL Server.  

- [Evaluación completa](#bkmk_full-eval): muestra información detallada sobre todas las evaluaciones completas anteriores.   

- [Evaluación incremental](#bkmk_incremental-eval): muestra información detallada sobre todas las evaluaciones incrementales anteriores.  

- [Todas las colas](#bkmk_all-q): resume las evaluaciones de recopilaciones actuales de las cuatro colas.  

- [Cola manual](#bkmk_manual-q): muestra información detallada sobre la evaluación de recopilación actual de la cola manual.  

- [Nueva cola](#bkmk_new-q): muestra información detallada sobre la evaluación de recopilación actual de la nueva cola.  

- [Cola completa](#bkmk_full-q): muestra información detallada sobre la evaluación de recopilación actual de la cola completa.  

- [Cola incremental](#bkmk_incremental-q): muestra información detallada sobre la evaluación de recopilación actual de la cola incremental.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a> Pestaña Conectar

Esta pestaña permite establecer la conexión inicial con el servidor de sitio primario. La herramienta también establece una conexión con el servidor de SQL Server que hospeda la base de datos de sitio.

Las conexiones al servidor de sitio primario y los servidores de SQL Server usan las credenciales del usuario con la sesión iniciada. No se admiten conexiones con el sitio de administración central ni con un sitio secundario. Ningún proceso de evaluación de colecciones se ejecuta en esos sitios.

Una vez que la herramienta establece correctamente una conexión, se ve una notificación en la parte inferior de Collection Evaluation Viewer que confirma la conexión de la herramienta con SQL Server. 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a> Pestaña Evaluación completa

Muestra información detallada sobre las evaluaciones de colecciones completas anteriores. Hay ocho columnas:  

- **Nombre de recopilación**: nombre de la recopilación.  

- **Identificador de sitio**: identificador de sitio de la recopilación.   

- **Tiempo de ejecución**: tiempo que ha tardado en ejecutarse la última evaluación de recopilación, en segundos.  

- **Hora de finalización de la última evaluación**: cuándo se ha completado la última evaluación de recopilación.  

- **Hora de la próxima evaluación**: cuándo se inicia la próxima evaluación completa.  

- **Cambios de miembros**: cambios de miembros en la última evaluación de recopilación. Estos cambios son más (miembros agregados) o menos (miembros quitados).  

- **Hora del último cambio de miembro**: hora más reciente en que se ha producido un cambio de pertenencia en la evaluación de recopilación.  

- **Porcentaje**: porcentaje de tiempo de evaluación de esta recopilación en relación con el tiempo de evaluación total (todas las recopilaciones).  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a> Pestaña Evaluación incremental

Muestra información detallada sobre las evaluaciones de colecciones incrementales anteriores. Hay siete columnas:  

- **Nombre de recopilación**: nombre de la recopilación.  

- **Identificador de sitio**: identificador de sitio de la recopilación.   

- **Tiempo de ejecución**: tiempo que ha tardado en ejecutarse la última evaluación de recopilación, en segundos.  

- **Hora de finalización de la última evaluación**: cuándo se ha completado la última evaluación de recopilación.  

- **Cambios de miembros**: cambios de miembros en la última evaluación de recopilación. Estos cambios son más (miembros agregados) o menos (miembros quitados).  

- **Hora del último cambio de miembro**: hora más reciente en que se ha producido un cambio de pertenencia en la evaluación de recopilación.  

- **Porcentaje**: porcentaje de tiempo de evaluación de esta recopilación en relación con el tiempo de evaluación total (todas las recopilaciones).  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a> Pestaña Todas las colas

Resume las evaluaciones de colecciones actuales de las cuatro colas. Hay seis secciones:  

- **Resumen**: muestra el número total de recopilaciones y la longitud de la cola de todas las recopilaciones de las cuatro colas.  

- **Evaluación en ejecución**: indica qué recopilación se está evaluando en cada cola y cuánto tiempo se ha ejecutado.  

- **Actualización manual**: muestra un breve resumen de las recopilaciones que se están evaluando, la hora de finalización estimada y el orden de la evaluación de la cola manual.  

- **Nueva recopilación**: muestra un breve resumen de las recopilaciones que se están evaluando, la hora de finalización estimada y el orden de la evaluación de la cola de la nueva recopilación.  

- **Evaluación completa**: muestra un breve resumen de las recopilaciones que se están evaluando, la hora de finalización estimada y el orden de la evaluación de la cola de evaluación completa.  

- **Evaluación incremental**: muestra un breve resumen de las recopilaciones que se están evaluando, la hora de finalización estimada y el orden de la evaluación de la cola de evaluación incremental.  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a> Pestaña Cola manual

Muestra información sobre la evaluación de colecciones manual que se está evaluando. El orden en la lista es el orden en el que se va a evaluar la colección. Hay cuatro columnas:  

- **Nombre de recopilación**: nombre de la recopilación.  

- **Identificador de sitio**: identificador de sitio de la recopilación.   

- **Hora de finalización estimada**: cuándo se estima que se complete la evaluación.  

- **Tiempo de ejecución estimado**: duración estimada de ejecución de la evaluación en formato día:hora:minuto:segundo.  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a> Pestaña Nueva cola

Muestra información actual sobre la nueva evaluación de colecciones que se está evaluando. El orden en la lista es el orden en el que se va a evaluar la colección. Hay cuatro columnas:  

- **Nombre de recopilación**: nombre de la recopilación.  

- **Identificador de sitio**: identificador de sitio de la recopilación.   

- **Hora de finalización estimada**: cuándo se estima que se complete la evaluación.  

- **Tiempo de ejecución estimado**: duración estimada de ejecución de la evaluación en formato día:hora:minuto:segundo.  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a> Pestaña Cola completa

Muestra información sobre la evaluación de colecciones completa que se está evaluando. El orden en la lista es el orden en el que se va a evaluar la colección. Hay cuatro columnas:  

- **Nombre de recopilación**: nombre de la recopilación.  

- **Identificador de sitio**: identificador de sitio de la recopilación.   

- **Hora de finalización estimada**: cuándo se estima que se complete la evaluación.  

- **Tiempo de ejecución estimado**: duración estimada de ejecución de la evaluación en formato día:hora:minuto:segundo.  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a> Pestaña Cola incremental

Muestra información sobre la evaluación de colecciones incremental que se está evaluando. El orden en la lista es el orden en el que se va a evaluar la colección. Hay cuatro columnas:  

- **Nombre de recopilación**: nombre de la recopilación.  

- **Identificador de sitio**: identificador de sitio de la recopilación.   

- **Hora de finalización estimada**: cuándo se estima que se complete la evaluación.  

- **Tiempo de ejecución estimado**: duración estimada de ejecución de la evaluación en formato día:hora:minuto:segundo.  



