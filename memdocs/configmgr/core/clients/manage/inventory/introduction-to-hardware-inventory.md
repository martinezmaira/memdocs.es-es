---
title: 'Inventario de hardware '
titleSuffix: Configuration Manager
description: Obtenga una introducción al inventario de hardware en Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695413"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Introducción al inventario de hardware en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use el inventario de hardware en Configuration Manager para recopilar información sobre la configuración del hardware de dispositivos cliente en su organización. Para recopilar el inventario de hardware, debe seleccionar la opción **Habilitar inventario de hardware en clientes** en la configuración de cliente.  

 Después de habilitar el inventario de hardware y de que el cliente ejecute un ciclo de inventario de hardware, el cliente envía la información a un punto de administración en el sitio del cliente. Después, el punto de administración reenvía la información de inventario al servidor de sitio de Configuration Manager, que almacena la información de inventario en la base de datos del sitio. El inventario de hardware se ejecuta en los clientes según la programación que especifique en la configuración de cliente.  
## <a name="view-hardware-inventory"></a>Ver el inventario de hardware 

 Puede usar varios métodos para ver los datos de inventario de hardware que Configuration Manager recopila, por ejemplo:  

- [Crear consultas que devuelven los dispositivos que se basan en una configuración de hardware específica.](../../../../core/servers/manage/introduction-to-queries.md)  

- [Crear recopilaciones basadas en consultas en función de una configuración de hardware específica.](../../../../core/clients/manage/collections/introduction-to-collections.md) Las pertenencias a recopilación basadas en consultas se actualizan automáticamente según una programación. Puede usar recopilaciones para varias tareas, que incluyen la implementación de software.

- [Ejecutar informes que muestran detalles específicos acerca de las configuraciones de hardware de su organización.](../../../servers/manage/introduction-to-reporting.md)

- [Use el Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) para ver información detallada sobre el inventario de hardware que se recopila de los dispositivos cliente.

Cuando se ejecuta el inventario de hardware en un dispositivo cliente, los primeros datos de inventario que el cliente devuelve son siempre un inventario completo. Los datos de inventario posteriores contienen solo la información de inventario diferencial. El servidor de sitio procesa la información diferencial del inventario en el orden recibido. Si falta información diferencial para un cliente, el servidor de sitio rechaza la información diferencial adicional e indica al cliente que ejecute un ciclo de inventario completo.  

 Configuration Manager proporciona compatibilidad limitada con equipos de arranque dual. Configuration Manager puede detectar equipos de arranque dual, pero solo devuelve información de inventario del sistema operativo que está activo cuando se ejecuta el ciclo de inventario.  

> [!NOTE]  
>  Para más información sobre cómo usar el inventario de hardware con clientes que ejecutan Linux y UNIX, vea [Inventario de hardware para Linux y UNIX](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Inventario ampliado de hardware con Configuration Manager  
 Además del inventario de hardware integrado en Configuration Manager, también puede usar uno de estos métodos para ampliar el inventario de hardware y recopilar más información:  

- Puede habilitar, deshabilitar, agregar y quitar clases de inventario de hardware personalizado de la consola de Configuration Manager.  
- Use archivos NOIDMIF para recopilar información sobre los dispositivos cliente que Configuration Manager no puede inventariar. Por ejemplo, podría desea recopilar información número de dispositivos activos que sólo existe como una etiqueta en el dispositivo. Inventario NOIDMIF se asocia automáticamente con el dispositivo de cliente que se recopilaron de.  
- Use archivos IDMIF para recopilar información sobre los activos que no están asociados con un cliente de Configuration Manager, por ejemplo, proyectores, fotocopiadoras e impresoras de red.


## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo usar estos métodos para ampliar el inventario de hardware de Configuration Manager, vea [Cómo configurar el inventario de hardware](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
