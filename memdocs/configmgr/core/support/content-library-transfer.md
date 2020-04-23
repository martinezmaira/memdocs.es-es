---
title: Herramienta Content Library Transfer
titleSuffix: Configuration Manager
description: Use la herramienta Content Library Transfer para transferir contenido de una unidad de disco a otra en un punto de distribución de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703443"
---
# <a name="content-library-transfer-tool"></a>Herramienta Content Library Transfer

*Se aplica a: Configuration Manager (rama actual)*

La herramienta Content Library Transfer es una de las [herramientas de Configuration Manager](tools.md). Transfiere contenido de una unidad de disco a otra. La herramienta está diseñada para ejecutarse en sistemas de sitio de punto de distribución. Admite puntos de distribución ubicados en un sitio o en sistemas de sitio remoto.  

La herramienta es útil para el escenario en que la unidad de disco que hospeda la biblioteca de contenido se llena. En primer lugar, agregue o identifique otro disco duro con espacio suficiente para hospedar la biblioteca de contenido. Luego use **ContentLibraryTransfer.exe** para transferir el contenido del disco duro antiguo lleno a la unidad nueva vacía.
 
Una vez completada la transferencia, el contenido es accesible a los equipos cliente desde la nueva ubicación.



## <a name="usage"></a>Uso 

Ejecute **ContentLibraryTransfer.exe** como usuario con permisos administrativos en el punto de distribución. 

#### <a name="syntax"></a>Sintaxis 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Ejemplo
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Limitaciones

- Ejecute la herramienta localmente en el punto de distribución. No se puede ejecutar desde un equipo remoto.  

- Úsela únicamente cuando los clientes no estén accediendo de forma activa al punto de distribución. Si ejecuta la herramienta mientras los clientes están accediendo al contenido, la biblioteca de contenido de la unidad de destino puede tener datos incompletos. Se puede producir un error en la transferencia de datos que dé lugar a una biblioteca de contenido completamente inutilizable.  

- No distribuya contenido al punto de distribución mientras se ejecuta la herramienta. Si ejecuta la herramienta mientras se está escribiendo contenido en el punto de distribución, la biblioteca de contenido de la unidad de destino puede tener datos incompletos. Se puede producir un error en la transferencia de datos que dé lugar a una biblioteca de contenido completamente inutilizable.



## <a name="see-also"></a>Vea también

- [Conceptos básicos de la administración de contenido](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [La biblioteca de contenido](../plan-design/hierarchy/the-content-library.md)
