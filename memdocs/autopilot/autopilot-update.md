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
ms.openlocfilehash: 34db88c53cdd7db46c126f15bb60a7fd2941a627
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757370"
---
# <a name="windows-autopilot-update"></a>Actualización de Windows AutoPilot

**Se aplica a**

-   Windows 10, versión 1903

La actualización de Windows AutoPilot le permite obtener las últimas características de AutoPilot y las correcciones de problemas críticos sin necesidad de pasar a la versión más reciente del sistema operativo Windows. Con la actualización de AutoPilot, las organizaciones pueden mantener su versión actual del sistema operativo y seguir beneficiándose de las nuevas características y correcciones de errores de AutoPilot.
 
Durante el proceso de implementación de AutoPilot, la actualización de Windows AutoPilot se ha agregado como un nuevo nodo después de la comprobación de actualizaciones críticas de la [revisión de Windows Zero Day (ZDP)](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe) . Durante el proceso de actualización, los dispositivos de Windows AutoPilot acceden a Windows Update para comprobar si hay una nueva actualización AutoPilot.  Si hay una actualización de AutoPilot disponible, el dispositivo descargará e instalará la actualización y, a continuación, se reiniciará automáticamente. Consulte el ejemplo siguiente.

   ![AutoPilot Update 1](images/update1.png)<br>
   ![AutoPilot Update 2](images/update2.png)<br>
   ![AutoPilot Update 3](images/update3.png)

En el diagrama siguiente se muestra una orquestación de implementación de Windows AutoPilot típica durante la ejecución rápida (OOBE) con el nuevo nodo de actualización de Windows AutoPilot.

   ![Flujo de actualización de AutoPilot](images/update-flow.png)

## <a name="release-cadence"></a>Cadencia de lanzamientos

- Cuando hay una actualización de AutoPilot disponible, normalmente se publica el cuarto martes del mes. La actualización se puede liberar en una semana diferente si se produce una excepción.
- También se publicará un artículo de Knowledge base (KB) para documentar los cambios que se incluyen en la actualización.

Para obtener una lista de las actualizaciones publicadas, consulte historial de actualizaciones de [AutoPilot](windows-autopilot-whats-new.md#windows-autopilot-update-history).

## <a name="see-also"></a>Consulte también

[Windows Update durante OOBE](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Novedades de Windows AutoPilot](windows-autopilot-whats-new.md)<br>