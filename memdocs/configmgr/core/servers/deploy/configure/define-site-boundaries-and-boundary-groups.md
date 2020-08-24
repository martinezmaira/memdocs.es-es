---
title: Uso de límites y grupos de límites
titleSuffix: Configuration Manager
description: Utilice los límites y grupos de límites para definir ubicaciones de red y sistemas de sitio accesibles para dispositivos administrados.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 385dc1b2f542c964b52515e755a9202ee951bc5c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126382"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Definir límites de sitio y grupos de límites

*Se aplica a: Configuration Manager (rama actual)*

Los *límites* en Configuration Manager definen las ubicaciones de red en la intranet. Estas ubicaciones incluyen los dispositivos que quiere administrar. Los *grupos de límites* son grupos lógicos de límites que puede configurar.

Una jerarquía puede incluir cualquier número de grupos de límites. Cada grupo de límites puede contener cualquier combinación de los tipos de límites siguientes:  

- Subred IP  
- Nombre de sitio de Active Directory  
- Prefijo IPv6  
- Intervalo de direcciones IP  
- VPN (a partir de la versión 2006)

Los clientes de la intranet evalúan su ubicación de red actual y después usan esa información para identificar los grupos de límites a los que pertenecen.  

Los clientes usan grupos de límites para lo siguiente:  

- **Encontrar un sitio asignado:** los grupos de límites permiten que los clientes encuentre un sitio primario para la asignación del cliente. Este comportamiento también se conoce como la *asignación automática de sitio*.  

- **Encontrar determinados roles de sistema de sitio que puedan usar:** Asocie un grupo de límites con ciertos roles de sistema de sitio. Luego, el sitio proporciona a los clientes esa lista de sistemas de sitio en el grupo de límites. Los clientes usan estos sistemas de sitio para acciones como buscar contenido o un punto de administración cercano.  

Los clientes que están en Internet o que están configurados como clientes solo de Internet no usan la información de límites. Estos clientes no pueden usar la asignación automática de sitio. Pueden descargar contenido de un punto de distribución basado en Internet desde un sitio asignado o un punto de distribución basado en la nube.  

A partir de la versión 1902, puede asociar una instancia de Cloud Management Gateway (CMG) con un grupo de límites. Para más información, consulte el [diseño de jerarquía de CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design).<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a> Recomendaciones

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Use una combinación del mínimo de límites que satisfagan sus necesidades

Use cualquier tipo o tipos de límite que elija y que funcione en el entorno. Para simplificar las tareas de administración, use los tipos de límite que le permiten usar la menor cantidad de límites que puede.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Evite la superposición de límites en la asignación automática de sitio

Aunque cada grupo de límites admite tanto la referencia del sistema de sitio y la asignación de sitio, cree un conjunto independiente de grupos de límites para usarlo solo en la asignación de sitio. Asegúrese de que cada uno de los límites de un grupo de límites no forme parte de otro grupo de límites con una asignación de sitio diferente.

- Un único límite puede incluirse en varios grupos de límites.  

- Los grupos de límites pueden asociarse con un sitio principal diferente para la asignación de sitio  

- En el caso de un límite que es miembro de dos grupos de límites distintos con asignaciones de sitio diferentes, los clientes seleccionan un sitio al cual unirse de manera aleatoria. Este comportamiento podría no ser el adecuado para el sitio al que quiere que se una el cliente. Esta configuración se denomina *superposición de límites*.  

    La superposición de límites no es un problema para la ubicación del contenido. Puede ser una configuración útil que brinde a los clientes ubicaciones de contenido o recursos adicionales que pueden usar.  


## <a name="next-steps"></a>Pasos siguientes

- [Definición de las ubicaciones de red como límites](boundaries.md)

- [Configurar grupos de límites](boundary-groups.md)
