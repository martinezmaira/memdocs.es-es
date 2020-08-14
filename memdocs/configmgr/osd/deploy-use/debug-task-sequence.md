---
title: Depurar una secuencia de tareas
titleSuffix: Configuration Manager
description: Use la herramienta de depuración de secuencias de tareas para solucionar los problemas de una secuencia de tareas.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99ed8232a74b038b9b1cde4af257353252454c2b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125158"
---
# <a name="debug-a-task-sequence"></a>Depurar una secuencia de tareas

*Se aplica a: Configuration Manager (rama actual)*

<!--3612274-->

A partir de la versión 1906, el depurador de secuencias de tareas es una nueva herramienta para la solución de problemas. Se implementa una secuencia de tareas en modo de depuración en una pequeña colección. Le permite recorrer la secuencia de tareas de una manera controlada para facilitar la investigación y la resolución de problemas. Actualmente, el depurador se ejecuta en el mismo dispositivo que el motor de secuencia de tareas, no se trata de un depurador remoto.

> [!Note]  
> En esta versión de Configuration Manager, el depurador de secuencias de tareas es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](../../core/servers/manage/pre-release-features.md).  


## <a name="prerequisites"></a>Requisitos previos

- Actualice al cliente de Configuration Manager en el dispositivo de destino.

- Inicie sesión en el dispositivo de destino como usuario en el grupo local de **Administradores**. El depurador solo pueden ejecutarlo administradores.

- Actualice la imagen de arranque asociada a la secuencia de tareas para asegurarse de que tiene la versión más reciente del cliente.


## <a name="start-the-tool"></a>Inicio de la herramienta

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.

1. Seleccione una secuencia de tareas. En el grupo Implementación de la cinta, seleccione **Depurar**.

    > [!Tip]  
    > Como alternativa, establezca la variable **TSDebugMode** en `TRUE` en una colección en la que se haya implementado la secuencia de tareas, o bien en un objeto de equipo en el que también se hayan implementado. Cualquier dispositivo que tenga este conjunto de variables colocará cualquier secuencia de tareas implementada en el modo de depuración.

1. Cree una implementación de depuración. La configuración de la implementación es la misma que la de una implementación de una secuencia de tareas normal. Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md#process).

    > [!Note]  
    > Solo puede seleccionar una colección pequeña para una implementación de depuración. Solo se mostrarán las colecciones de dispositivos con 10 miembros o menos.

A partir de la versión 1910, use la nueva variable de secuencia de tareas **TSDebugOnError** para iniciar automáticamente el depurador cuando la secuencia de tareas devuelva un error.<!-- 5012536 --> Para obtener más información, vea [Variables de secuencia de tareas: TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError).

## <a name="use-the-tool"></a>Uso de la herramienta

Cuando la secuencia de tareas se ejecuta en el dispositivo, se abre la ventana del depurador de secuencia de tareas, como en la captura de pantalla siguiente:

![Captura de pantalla del depurador de secuencia de tareas](media/3612274-tsdebug.png)

El depurador incluye los controles siguientes:

- **Step** (Paso): desde la posición *actual*, ejecute solo el paso siguiente de la secuencia de tareas.  

    > [!Note]  
    > Cuando la secuencia de tareas está en modo de depuración, si un paso devuelve un error irrecuperable, la secuencia de tareas no produce un error normal. Este comportamiento le ofrece la opción de volver a intentar un paso después de realizar un cambio externo.

- **Ejecutar**: desde la posición *actual*, ejecute la secuencia de tareas con normalidad hasta el final o el próximo punto de *interrupción*, o si hay error en un paso. Antes de usar esta acción, asegúrese de establecer los puntos de interrupción con la acción **Establecer interrupción**.

- **Set Current** (Establecer actual): seleccione un paso en el depurador y, después, seleccione **Set Current**. Esta acción mueve el puntero *actual* a ese paso. Esta acción permite omitir pasos o retroceder.  

    > [!Warning]  
    > El depurador no considera el tipo de paso cuando se cambia la posición actual en la secuencia. Algunos pasos pueden establecer variables de secuencia de tareas que se necesitan para la evaluación de condiciones en pasos posteriores. Si se ejecutan de forma desordenada, algunos pasos pueden producir un error o causar daños importantes en un dispositivo. Use esta opción bajo su responsabilidad.  

- **Set Break** (Establecer punto de interrupción): seleccione un paso en el depurador y, después, seleccione **Set Break**. Esta acción agrega un punto de *interrupción* al depurador. Cuando se **ejecuta** la secuencia de tareas, se detiene en un *punto de interrupción*.  

    - Antes de usar la acción **Ejecutar**, establezca puntos de interrupción.

    - A partir de la versión 1910, si crea un punto de interrupción en el depurador y, a continuación, la secuencia de tareas reinicia el equipo, el depurador mantiene el punto de interrupción después del reinicio.<!-- 5012509 -->

    - En la versión 1906, los puntos de interrupción no se guardan después de que se reinicie el equipo, como con el paso [Reiniciar el equipo](../understand/task-sequence-steps.md#BKMK_RestartComputer). Por ejemplo, si inicia el depurador desde el Centro de software para una secuencia de tareas de creación de imágenes, no establezca interrupciones en la fase de Windows PE. Cuando el equipo se reinicia en Windows PE, el depurador pausa la secuencia de tareas para que pueda establecer interrupciones.

- **Borrar todas las interrupciones**: quita todos los puntos de interrupción.

- **Archivo de registro**: abre el archivo de registro de la secuencia de tareas actual, **smsts.log**, con [CMTrace](../../core/support/cmtrace.md). Puede ver las entradas del registro cuando el motor de secuencia de tareas está "esperando al depurador".

- **Símbolo del sistema cmd**: en Windows PE, abre un símbolo del sistema.

- **Cancelar**: cierra el depurador y produce un error en la secuencia de tareas.

- **Quit** (Salir): desasocia y cierra el depurador, pero la secuencia de tareas continúa ejecutándose con normalidad.

La ventana **Variables de secuencias de tareas** muestra los valores actuales de todas las variables en el entorno de la secuencia de tareas. Para más información, vea [Task sequence variables](../understand/task-sequence-variables.md) (Variables de secuencia de tareas). Si usa el paso [Establecer variable de secuencia de tareas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) con la opción **No mostrar este valor**, el depurador no mostrará el valor de la variable. No se pueden editar los valores de las variables en el depurador.

> [!Note]
> Algunas variables de secuencias de tareas son solo para uso interno y no se incluyen en la documentación de referencia.

El depurador de secuencias de tareas continúa ejecutándose después de un paso [Reiniciar el equipo](../understand/task-sequence-steps.md#BKMK_RestartComputer), pero debe volver a crear los puntos de interrupción. Aunque es posible que la secuencia de tareas no necesite la interacción del usuario, como el depurador sí la requiere, debe iniciar sesión en Windows para continuar. Si no inicia sesión después de una hora para continuar con la depuración, se produce un error en la secuencia de tareas.

También se pasa a una secuencia de tareas secundaria con el paso [Ejecutar secuencia de tareas](../understand/task-sequence-steps.md#child-task-sequence). La ventana del depurador muestra los pasos de la secuencia de tareas secundaria junto con la secuencia de tareas principal.


## <a name="known-issues"></a>Problemas conocidos

Si establece una implementación normal y una implementación de depuración como destino del mismo dispositivo a través de varias implementaciones, es posible que el depurador de la secuencia de tareas no se inicie.


## <a name="see-also"></a>Vea también

- [Acerca de los pasos de la secuencia de tareas](../understand/task-sequence-steps.md)
- [Variables de secuencias de tareas](../understand/task-sequence-variables.md)
- [Uso de variables de secuencias de tareas](../understand/using-task-sequence-variables.md)
- [Implementación de una secuencia de tareas](deploy-a-task-sequence.md)
