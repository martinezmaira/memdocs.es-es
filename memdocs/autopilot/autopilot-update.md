---
title: Actualización de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Actualización de Windows AutoPilot
keywords: AutoPilot, actualizar, Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: a677dec0d722f0ef17a8c16248a41dea1b0be947
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068125"
---
# <a name="windows-autopilot-update"></a>Actualización de Windows AutoPilot

**Se aplica a**

- Windows 10, versión 1903

Windows AutoPilot Update instala las últimas características y correcciones del piloto automático en los dispositivos AutoPilot de la organización. Los dispositivos no se mueven a la versión más reciente del sistema operativo Windows. Con la actualización AutoPilot, puede mantener la versión actual del sistema operativo de los dispositivos y seguir sacando provecho de las nuevas características y correcciones de errores de AutoPilot.

El proceso de actualización de Windows AutoPilot se produce después de la comprobación de actualizaciones críticas de la [revisión de Windows Zero Day (ZDP)](/windows-hardware/customize/desktop/windows-updates-during-oobe) . Durante el proceso de actualización, los dispositivos comprueban Windows Update para una nueva actualización del piloto automático. Si hay una actualización de AutoPilot disponible, el dispositivo descarga e instala la actualización y, a continuación, se reinicia automáticamente. Consulte el ejemplo siguiente.

 ![AutoPilot Update 1](images/update1.png)<br>
 ![AutoPilot Update 2](images/update2.png)<br>
 ![AutoPilot Update 3](images/update3.png)

En el diagrama siguiente se muestra una orquestación de implementación de Windows AutoPilot típica durante la ejecución rápida (OOBE) con el nuevo nodo de actualización de Windows AutoPilot.

 ![Flujo de actualización de AutoPilot](images/update-flow.png)

## <a name="release-cadence"></a>Cadencia de lanzamientos

- Cuando hay una actualización de AutoPilot disponible, normalmente se publica el cuarto martes del mes. La actualización podría publicarse en una semana diferente si se produce una excepción.
- También se publicará un artículo de Knowledge base (KB) para documentar los cambios que se incluyen en la actualización.

Para obtener una lista de las actualizaciones publicadas, consulte historial de actualizaciones de [AutoPilot](windows-autopilot-whats-new.md#windows-autopilot-update-history).

## <a name="see-also"></a>Consulte también

[Windows Update durante OOBE](/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Novedades de Windows AutoPilot](windows-autopilot-whats-new.md)<br>