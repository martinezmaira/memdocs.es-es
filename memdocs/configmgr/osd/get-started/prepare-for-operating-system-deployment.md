---
title: Preparar la implementación de sistema operativo
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo prepararse para implementaciones de sistema operativo en Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708843"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Preparación para la implementación de SO en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Hay varias cosas que debe hacer en Configuration Manager para poder implementar sistemas operativos. Use los siguientes artículos para prepararse para la implementación del SO:  

-   [Administrar imágenes de arranque](manage-boot-images.md)  

-   [Administración de imágenes del sistema operativo](manage-operating-system-images.md)  

-   [Administración de paquetes de actualización del sistema operativo](manage-operating-system-upgrade-packages.md)  

-   [Administrar controladores](manage-drivers.md)  

-   [Administrar el estado de usuario](manage-user-state.md)  

-   [Preparación para implementaciones en equipos desconocidos](prepare-for-unknown-computer-deployments.md)  

-   [Asociar usuarios a un equipo de destino](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Tamaño de imágenes del SO  

Las imágenes de sistema operativo son de tamaño grande. Por ejemplo, el tamaño de la imagen de Windows 7 es 3 gigabytes o más. El tamaño de la imagen y el número de equipos en que implementa al mismo tiempo el sistema operativo afecta al rendimiento de la red y al ancho de banda disponible. Asegúrese de probar el rendimiento de red. La prueba del impacto mide mejor el efecto que podría tener la implementación de la imagen y el tiempo que lleva completar la implementación. Las actividades de Configuration Manager que afectan al rendimiento de la red incluyen la distribución de la imagen a un punto de distribución, la distribución de la imagen de un sitio a otro y la descarga de la imagen al cliente.  

Asegúrese también de que planea suficiente espacio de almacenamiento en disco en los puntos de distribución que hospedan las imágenes del sistema operativo.  

Para obtener más información, consulte [Consideraciones de planeación adicionales para puntos de distribución](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Tamaño de la caché de cliente  

Cuando los clientes de Configuration Manager descargan contenido, usan automáticamente el servicio de transferencia inteligente en segundo plano (BITS) si está disponible. Cuando implementa una secuencia de tareas que instala un sistema operativo, puede establecer una opción en la implementación de forma que los clientes de Configuration Manager descarguen la imagen completa en una memoria caché local antes de que se ejecute la secuencia de tareas.  

Cuando un cliente de Configuration Manager debe descargar una imagen de sistema operativo pero no hay suficiente espacio en la memoria caché, el cliente puede liberar espacio en su caché. Comprueba los otros paquetes en la memoria caché para determinar si la eliminación de cualquiera de los paquetes más antiguos liberará espacio suficiente para que quepa la imagen. Si la eliminación paquetes no libera suficiente espacio, el cliente no descarga la imagen y se produce un error en la implementación. Este comportamiento puede ocurrir si la memoria caché tiene un paquete grande que está configurado para conservarse en la memoria caché. Si la eliminación de paquetes libera suficiente espacio en disco en la memoria caché, el cliente los elimina y luego descarga la imagen en la caché.  

El tamaño de caché predeterminado en clientes de Configuration Manager puede no ser lo suficientemente grande para la mayoría de las implementaciones de imagen de sistema operativo. Si planea descargar la imagen completa a la caché del cliente, ajuste el tamaño de la caché del cliente en los equipos de destino para acomodar el tamaño de la imagen que va a implementar.  

Para obtener más información, vea [Configurar la caché del cliente](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  


