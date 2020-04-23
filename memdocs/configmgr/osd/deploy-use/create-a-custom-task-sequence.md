---
title: Crear una secuencia de tareas personalizada
titleSuffix: Configuration Manager
description: Edite una secuencia de tareas personalizada en Configuration Manager para agregar pasos a la secuencia de tareas.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9107e9787cf7f12cab624101c37344ea20684112
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704203"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Creación de una secuencia de tareas personalizada con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Cuando se crea una secuencia de tareas personalizada en Configuration Manager, no contiene ningún paso de secuencia de tareas. Después de crear la secuencia de tareas, edítela y agregue los pasos de secuencia de tareas que necesite.  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a> Crear una secuencia de tareas personalizada

Use el procedimiento siguiente para crear una secuencia de tareas personalizada:

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear secuencia de tareas**. Esta acción inicia el Asistente para crear secuencia de tareas.  

1. En la página **Crear una nueva secuencia de tareas** , seleccione **Crear una nueva secuencia de tareas personalizada**.  

1. En la página **Información de secuencia de tareas**, especifique lo siguiente:

    - Un nombre para la secuencia de tareas
    - Una descripción de la secuencia de tareas
    - Una imagen de arranque opcional para que la use la secuencia de tareas

Después de completar el Asistente para crear secuencia de tareas, Configuration Manager agrega la secuencia de tareas personalizada al nodo **Secuencias de tareas**. Ahora puede editar esta secuencia de tareas y agregar pasos.  

## <a name="see-also"></a>Vea también

Para obtener una lista de los pasos de secuencia de tareas disponibles, vea [Pasos de la secuencia de tareas](../understand/task-sequence-steps.md).  

Para obtener más información sobre cómo editar una secuencia de tareas, vea [Uso del editor de secuencias de tareas](../understand/task-sequence-editor.md).  

La mayoría de las veces, usará secuencias de tareas para automatizar tareas de implementación de sistema operativo, pero puede crear una secuencia de tareas personalizada para automatizar diversos tipos de tareas. Para obtener más información, vea [Crear una secuencia de tareas para implementaciones que no son de sistema operativo](create-a-task-sequence-for-non-operating-system-deployments.md).

A partir de la versión 2002, instale aplicaciones complejas mediante secuencias de tareas a través del modelo de aplicación. Agregue un tipo de implementación a una aplicación que sea una secuencia de tareas, para instalar o desinstalar la aplicación. Para obtener más información, vea [Creación de aplicaciones Windows](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

## <a name="next-steps"></a>Pasos siguientes

[Implementar la secuencia de tareas](deploy-a-task-sequence.md)
