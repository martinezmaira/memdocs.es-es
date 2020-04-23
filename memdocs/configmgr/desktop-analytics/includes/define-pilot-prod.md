---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708223"
---
Use las siguientes definiciones para diferenciar entre piloto y producción:  

- **Piloto**: subconjunto de los dispositivos que quiere validar antes de realizar la implementación en un conjunto más grande. Use Análisis de escritorio para marcar los dispositivos como únicos en el conjunto piloto. Los dispositivos del piloto están listos para actualizarse cuando no haya activos de bloqueo. Un activo de bloqueo está marcado como *crítico* y *no se puede* actualizar.  

- **Production**: todos los demás dispositivos inscritos en Análisis de escritorio que no están en el piloto. Los dispositivos de producción están listos para actualizarse cuando todos los activos estén aprobados. Análisis de escritorio aprueba automáticamente los activos no críticos.  

