---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268797"
---
Use las siguientes definiciones para diferenciar entre piloto y producción:  

- **Piloto**: subconjunto de los dispositivos que quiere validar antes de realizar la implementación en un conjunto más grande. Use Análisis de escritorio para marcar los dispositivos como únicos en el conjunto piloto. Los dispositivos del piloto están listos para actualizarse cuando no haya activos de bloqueo. Un activo de bloqueo está marcado como *crítico* y *no se puede* actualizar.  

- **Production**: todos los demás dispositivos inscritos en Análisis de escritorio que no están en el piloto. Los dispositivos de producción están listos para actualizarse cuando todos los activos estén aprobados. Análisis de escritorio aprueba automáticamente los activos no críticos.  
