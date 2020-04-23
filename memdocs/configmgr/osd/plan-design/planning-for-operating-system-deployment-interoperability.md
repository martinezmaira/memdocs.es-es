---
title: Interoperabilidad de la implementación del sistema operativo
titleSuffix: Configuration Manager
description: Comprenda los problemas de interoperabilidad cuando diferentes sitios de Configuration Manager en una sola jerarquía usan versiones diferentes.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708083"
---
# <a name="plan-for-os-deployment-interoperability"></a>Planificación de la interoperabilidad de la implementación del sistema operativo

*Se aplica a: Configuration Manager (rama actual)*

Si en una misma jerarquía hay varios sitios de Configuration Manager que usan versiones diferentes, no estarán disponibles algunas funciones de Configuration Manager. Normalmente, la funcionalidad de la versión más actual de Configuration Manager no es accesible en sitios o por clientes que ejecutan una versión anterior. Para obtener más información, vea [Interoperabilidad entre diferentes versiones de Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


## <a name="objects"></a>Objetos

Considere los siguientes objetos cuando actualice el sitio de nivel superior de la jerarquía y otros sitios de la jerarquía ejecuten Configuration Manager con una versión anterior:  

### <a name="client-installation-package"></a>Paquete de instalación de cliente  

- El origen predeterminado del paquete de instalación de cliente se actualiza automáticamente. Todos los puntos de distribución de la jerarquía se actualizan con el nuevo paquete de instalación de cliente. Este comportamiento se produce incluso en los puntos de distribución de sitios de la jerarquía que tienen una versión anterior.  

- No se puede asignar nuevos clientes de versión a sitios que todavía no se han actualizado a la nueva versión. Asignación se bloquea en el punto de administración.  

### <a name="boot-images"></a>Imágenes de arranque  

- Si actualiza el sitio de nivel superior a la última versión de Configuration Manager, se actualizan automáticamente las imágenes de arranque predeterminadas (x86 y x64). La actualización usa Windows ADK para Windows 10, que incluye Windows PE 10. Los archivos asociados a las imágenes de arranque predeterminadas se actualizan con la versión de Configuration Manager más reciente de los archivos. El sitio no actualiza automáticamente las imágenes de arranque personalizadas. Deberá actualizar manualmente las imágenes de arranque personalizadas, incluidas las versiones anteriores de Windows PE.  

- Si la jerarquía de sitio contiene sitios con versiones diferentes de Configuration Manager, evite usar medios dinámicos. En su lugar, use medios basados en sitio para ponerse en contacto con un punto de administración específico. Después de actualizar todos los sitios a la misma versión de Configuration Manager, puede volver a usar medios dinámicos.

- Compruebe que las imágenes de arranque de Configuration Manager más recientes incluyan sus personalizaciones. Después, actualice todos los puntos de distribución en los sitios de la versión nueva con la versión más reciente de las nuevas imágenes de arranque.  

### <a name="user-state-migration-tool-usmt"></a>Herramienta de migración de estado de usuario (USMT)  

Si actualiza el sitio de nivel superior a la versión más reciente de Configuration Manager, el paquete de USMT predeterminado también se actualizará automáticamente a esta versión. No se actualizará automáticamente ningún paquete de USMT personalizado. Por tanto, tendrá que actualizarlos manualmente.  

### <a name="new-task-sequence-steps"></a>Nuevas etapas de la secuencia de tareas  

Periódicamente, se introducen nuevas etapas en la secuencia de tareas con las nuevas versiones de Configuration Manager. Al implementar una secuencia de tareas con una nueva etapa en clientes más antiguos, se producirá un error en la etapa de la secuencia de tareas. Antes de implementar una secuencia de tareas con una nueva etapa, asegúrese de que los clientes de la recopilación de destino están actualizados a la nueva versión.  

### <a name="os-deployment-media"></a>Medios de implementación del sistema operativo  

Al actualizar el sitio a una nueva versión, actualice todos los medios con el nuevo paquete de cliente de Configuration Manager. Se incluyen los tipos de medios de arranque, de captura, preconfigurados e independientes.

### <a name="third-party-extensions-to-os-deployment"></a>Extensiones de terceros para la implementación del sistema operativo  

Si dispone de extensiones de terceros para la implementación del sistema operativo y tiene diferentes versiones de los sitios o clientes de Configuration Manager (es decir, una jerarquía mixta), puede haber problemas con las extensiones.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Versión más reciente de los sitios de Configuration Manager en una jerarquía mixta  

Cuando actualiza un sitio a la versión más reciente de Configuration Manager, las secuencias de tareas que hacen referencia al paquete de instalación de cliente predeterminado se inician automáticamente para implementar la versión de cliente de Configuration Manager más reciente.

Las secuencias de tareas que hacen referencia a un paquete de instalación de cliente personalizado siguen implementando la versión del cliente que se encuentra en dicho paquete personalizado. Es probable que los paquetes personalizados incluyan una versión anterior del cliente de Configuration Manager. Para evitar errores en la implementación de la secuencia de tareas, actualice todos los paquetes de instalación de cliente personalizados a la versión más reciente.

Cuando configure una secuencia de tareas para usar un paquete de instalación de cliente personalizado, realice una de las siguientes acciones:

- Actualice la etapa de la secuencia de tareas para usar la versión más reciente de Configuration Manager del paquete de instalación de cliente.
- Actualice el paquete personalizado para usar el origen de instalación de cliente más reciente de Configuration Manager.

> [!IMPORTANT]  
> No implemente secuencias de tareas que hagan referencia al paquete de instalación del cliente de Configuration Manager más reciente en clientes que se encuentren en un sitio de Configuration Manager más antiguo. Cuando se actualizan los clientes asignados a un sitio de Configuration Manager anterior a la última versión de cliente de Configuration Manager, Configuration Manager bloquea la asignación del anterior sitio de Configuration Manager. Estos clientes ya no estarán asignar a ningún sitio. Hasta que asigne el cliente manualmente al sitio de Configuration Manager más reciente o reinstale la versión anterior del cliente de Configuration Manager en el equipo, estos clientes permanecerán sin administrar.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versiones anteriores de Configuration Manager en una jerarquía mixta  

Al actualizar el sitio de administración central a la versión más reciente de Configuration Manager, asegúrese de que las secuencias de tareas de implementación del sistema operativo que implemente no dejen a dichos clientes en un estado sin administrar (por ejemplo, si realiza la implementación en clientes asignados a un sitio de Configuration Manager más antiguo que todavía no ha actualizado a la versión más reciente de Configuration Manager).

Realice una copia de una secuencia de tareas que use para realizar la implementación en clientes en la versión más reciente del sitio de Configuration Manager. Después, modifique la secuencia de tareas para implementarla en clientes de un sitio de Configuration Manager más antiguo. Configure la secuencia de tareas para que haga referencia al paquete de instalación de cliente personalizado que usa el origen de instalación del cliente de Configuration Manager más reciente. Si aún no tiene un paquete de instalación de cliente personalizado que haga referencia al origen de instalación del cliente de Configuration Manager más antiguo, deberá crear uno manualmente.  

> [!Important]  
> A partir de la versión 1902, no se puede implementar un paquete o una secuencia de tareas en una versión de cliente 5.7730 o anterior. Para solucionar esta limitación, actualice el cliente a una versión posterior.<!-- SCCMDocs-pr issue #3493 -->
