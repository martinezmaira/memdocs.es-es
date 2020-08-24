---
title: Implementar actualizaciones de software
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar de forma manual o automática las actualizaciones de software en la consola de Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: a6e27e2d03983fdf627016d0e3b41aaa378afe29
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693478"
---
# <a name="deploy-software-updates"></a>Implementar actualizaciones de software  

*Se aplica a: Configuration Manager (rama actual)*

La fase de implementación de actualizaciones de software es el proceso de implementar actualizaciones de software. Independientemente de cómo implemente las actualizaciones de software, el sitio:
- Agrega las actualizaciones a un grupo de actualizaciones de software
- Distribuye el contenido de actualización a puntos de distribución
- Implementa el grupo de actualizaciones en los clientes  

Después de crear la implementación, el sitio envía una directiva de actualización de software a los clientes de destino. Los clientes descargan los archivos de contenido de actualización de software desde un origen de contenido en su caché local. Los clientes en Internet descargan siempre el contenido desde el servicio en la nube de Microsoft Update. Las actualizaciones de software están disponibles para su instalación por parte del cliente.   

> [!Tip]  
>  Si un punto de distribución no está disponible, los clientes en la intranet también pueden descargar actualizaciones de software desde Microsoft Update.  

> [!NOTE]  
>  A diferencia de otros tipos de implementación, todas las actualizaciones de software se descargan en la caché del cliente. Esto es independiente del tamaño máximo de caché configurado en el cliente. Para obtener más información sobre la configuración de la memoria caché de cliente, vea [Configurar la caché del cliente para clientes de Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Si configura una implementación de actualizaciones de software requeridas, las actualizaciones de software se instalan automáticamente en la fecha límite programada. El usuario del equipo cliente puede programar o iniciar la instalación de las actualizaciones de software antes de que se cumpla la fecha límite. Tras el intento de instalación, los equipos cliente devuelven mensajes de estado al servidor de sitio para notificar si la instalación de las actualizaciones de software se completó correctamente. Para obtener más información sobre las implementaciones de actualización de software, consulte [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows) (Flujos de trabajo de implementación de actualizaciones de software).  

Hay tres escenarios principales en cuanto a la implementación de actualizaciones de software: 
- [Implementación manual](#BKMK_ManualDeployment)  
- [Implementación automática](#bkmk_auto)  
- [Implementación por fases](#bkmk_phased)  

Normalmente, primero implementa manualmente las actualizaciones de software para crear una línea de base en los clientes. A partir de ahí, administra las actualizaciones de software mediante la implementación automática o por fases.  

> [!Note]  
> No se puede usar una regla de implementación automática con una implementación por fases.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Implementar actualizaciones de software manualmente
Seleccione las actualizaciones de software en la consola de Configuration Manager e inicie manualmente el proceso de implementación. Normalmente usa este método de implementación para:  

- Actualizar los clientes con las actualizaciones de software requeridas antes de crear reglas de implementación automática que administren las implementaciones mensuales  

- Implementar actualizaciones de software fuera de banda  


En la lista siguiente se indica el flujo de trabajo general de la implementación manual de las actualizaciones de software:  

1. Filtre las actualizaciones de software que utilicen requisitos específicos. Por ejemplo, podría especificar criterios para la recuperación de todas las actualizaciones de software de seguridad o imprescindibles que se requieran en más de 50 clientes.  

2. Cree un grupo de actualizaciones de software que contenga las actualizaciones de software.  

3. Descargue el contenido de las actualizaciones de software en el grupo de actualizaciones de software.  

4. Implemente manualmente el grupo de actualizaciones de software.  

Para obtener más información y pasos detallados, vea [Implementar actualizaciones de software manualmente](manually-deploy-software-updates.md).

> [!Note]
> - A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](/deployoffice/name-change). Es posible que siga viendo referencias al nombre anterior en la consola de Configuration Manager y la documentación complementaria mientras se está actualizando la consola.
> - Cuando implemente manualmente las actualizaciones de cliente de Aplicaciones de Microsoft 365, búsquelas en el nodo **Actualizaciones de Office 365** bajo **Administración de clientes de Office 365** del área de trabajo **Biblioteca de software**. 

## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a> Implementar actualizaciones de software automáticamente

Configure la implementación automática de las actualizaciones de software mediante una regla de implementación automática (ADR). Este método de implementación es común para actualizaciones de software mensuales (lo que suele conocerse como "Patch Tuesday") y para la administración de actualizaciones de definiciones. Defina los criterios para que una ADR automatice el proceso de implementación. En la lista siguiente se indica el flujo de trabajo general para implementar automáticamente las actualizaciones de software:  

1.  Cree una ADR que especifique la configuración de implementación.  

2.  El sitio agrega actualizaciones de software a un grupo de actualizaciones de software.  

3.  El sitio implementa el grupo de actualizaciones de software en los clientes de la recopilación de destino.  

En primer lugar, determine la estrategia de implementación de actualización de software automática. Por ejemplo, podría crear la ADR para que inicialmente seleccione una recopilación de destino de clientes de prueba. Después de comprobar que el grupo de prueba ha instalado correctamente las actualizaciones de software, agregue una nueva implementación a la regla. También podría cambiar la colección de destino en la implementación existente a otra que incluya un conjunto de clientes mayor. Tenga en cuenta los siguientes comportamientos cuando decida qué estrategia utilizará:  

- Puede modificar las propiedades de los objetos de actualización de software que crea la ADR.   

- La ADR implementa automáticamente las actualizaciones de software a los clientes cuando los agrega a la colección de destino.  

- Cuando usted o la ADR agrega nuevas actualizaciones de software al grupo de actualizaciones de software, el sitio las implementa automáticamente en los clientes de la colección de destino.  

- Habilite o deshabilite las implementaciones en cualquier momento para la ADR.  


Después de crear una ADR, agregue implementaciones adicionales a la regla. Esta acción le ayuda a administrar la complejidad de la implementación de varias actualizaciones en diferentes recopilaciones. Cada nueva implementación ofrece todas las funcionalidades y la experiencia completa de supervisión de la implementación.  

Todas las implementaciones nuevas que agregue:  

- Usan el mismo grupo y paquete de actualizaciones que la ADR crea la primera vez que se ejecuta  
- Pueden tener como objetivo otra colección  
- Admiten propiedades de implementación únicas, como:  
  -   Hora de activación  
  -   Fecha límite  
  -   Experiencia del usuario  
  -   Alertas independientes para cada implementación  


Para obtener más información y pasos detallados, vea [Implementar actualizaciones de software automáticamente](automatically-deploy-software-updates.md)



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a> Implementación de actualizaciones de software por fases

<!--1358146-->
A partir de la versión 1810, cree implementaciones por fases de actualizaciones de software. Las Implementaciones por fases permiten organizar un lanzamiento de software coordinado y secuencial según criterios y grupos personalizables.

Para más información, vea [Crear implementaciones por fases](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).

