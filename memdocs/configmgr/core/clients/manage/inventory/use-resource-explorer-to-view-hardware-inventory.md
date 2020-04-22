---
title: Cómo usar el Explorador de recursos
titleSuffix: Configuration Manager
description: Use el Explorador de recursos para ver el inventario de hardware en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690103"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Cómo usar el Explorador de recursos para ver el inventario de hardware en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use el Explorador de recursos de Configuration Manager para ver información sobre el inventario de hardware. El sitio recopila esta información de los clientes de la jerarquía.  

> [!Tip]  
>  El Explorador de recursos no muestra ningún dato hasta que se ejecuta un ciclo de inventario de hardware en el cliente al que se conecte.  



## <a name="overview"></a>Introducción

El Explorador de recursos tiene las siguientes secciones relacionadas con el inventario de hardware:  

- **Hardware**: muestra el inventario de hardware más reciente recopilado del dispositivo cliente especificado.  

    - En el nodo **Estado de estación de trabajo** se muestra la hora y fecha del último inventario de hardware del dispositivo.  

- **Historial de hardware**: un historial de los elementos inventariados que han cambiado desde el último ciclo de inventario de hardware.  

    - Expanda un elemento para ver un nodo **Actual** y uno o varios nodos con la fecha histórica. Compare la información del nodo actual con la de uno de los nodos históricos para ver los elementos que han cambiado.  

> [!NOTE]  
> De forma predeterminada, Configuration Manager elimina los datos de inventario de hardware que hayan estado inactivos durante 90 días. Ajuste este número de días en la tarea de mantenimiento del sitio **Eliminar historial de inventario antiguo**. Para obtener más información, vea [Tareas de mantenimiento](../../../servers/manage/maintenance-tasks.md).  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a> Cómo abrir el Explorador de recursos   

1.  En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y haga clic en el nodo **Dispositivos**. También puede seleccionar cualquier colección en el nodo **Recopilaciones de dispositivos**.  

2.  Seleccione un dispositivo. En la cinta, en la pestaña **Inicio** y el grupo **Dispositivos**, haga clic en **Iniciar** y, después, seleccione **Explorador de recursos**.   

> [!Tip]  
> En el Explorador de recursos, haga clic con el botón derecho en un elemento del panel de resultados de la derecha para obtener acciones adicionales. Haga clic en **Propiedades** para ver ese elemento en otro formato.  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a> Uso de valores enteros grandes
<!--1357880-->
En las versiones de Configuration Manager 1802 y anteriores, el inventario de hardware tiene un límite para enteros mayores que 4 294 967 296 (2^32). Este límite puede alcanzarse en atributos como tamaños de unidades de disco duro en bytes. El punto de administración no procesa los valores enteros por encima de este límite, por lo que no se almacena ningún valor en la base de datos. 

A partir de la versión 1806, el límite se ha aumentado a 18.446.744.073.709.551.616 (2^64). 

Para una propiedad con un valor que no cambia, como el tamaño total del disco, no puede ver inmediatamente el valor después de actualizar el sitio. La mayoría del inventario de hardware es un informe diferencial. El cliente envía solamente los valores que cambian. Para solucionar este comportamiento temporalmente, agregue otra propiedad a la misma clase. Esta acción hace que el cliente actualice todas las propiedades de la clase que ha cambiado. 



## <a name="see-also"></a>Vea también

Para obtener información sobre cómo ver el inventario de hardware de los clientes que ejecutan Linux y UNIX, vea [Cómo supervisar clientes para servidores Linux y UNIX](../monitor-clients-for-linux-and-unix-servers.md).  

En el Explorador de recursos también se muestra el Inventario de software. Para obtener más información, vea [Cómo usar el Explorador de recursos para ver el inventario de software](use-resource-explorer-to-view-software-inventory.md).
