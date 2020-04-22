---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697853"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a> Las secuencias de tareas no están disponibles para entorno PXE o elementos multimedia

<!--5578298-->
Si implementa una secuencia de tareas para entorno PXE o elementos multimedia (USB o DVD), el cliente no recibe la directiva. En **smsts.log** aparece el mensaje siguiente:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Solución alternativa

Inicie la secuencia de tareas desde el Centro de Software.
