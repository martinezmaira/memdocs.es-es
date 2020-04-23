---
title: Usar medios de arranque para implementar Windows a través de la red
titleSuffix: Configuration Manager
description: Use implementaciones de medios de arranque en Configuration Manager para implementar el sistema operativo al iniciar el equipo de destino.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709243"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usar medios de arranque para implementar Windows a través de la red con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede implementar el sistema operativo cuando el equipo de destino se inicia con una implementación de medios de arranque. Los medios contienen un puntero a la secuencia de tareas, la imagen del sistema operativo y otro contenido requerido de la red. Cuando se inicia el equipo de destino, el equipo recupera los elementos a los que hace referencia el puntero. Una vez que los medios de arranque liberan contenido, puede actualizar el destino sin tener que reemplazarlo en los medios.

Puede implementar sistemas operativos a través de la red mediante multidifusión en los siguientes escenarios de implementación de sistema operativo:

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md)  

Complete los pasos de uno de los escenarios de implementación de sistema operativo y luego use las secciones siguientes para usar medios de arranque para implementar el sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurar la implementación  
Cuando use medios de arranque para iniciar el proceso de implementación del sistema operativo, configure la implementación para que el sistema operativo esté disponible para los medios. Puede configurar esta opción en la página **Configuración de implementación** del Asistente para implementar software o en la pestaña **Configuración de implementación** en las propiedades de la implementación. Para la opción de configuración **Estar disponible para** , configure uno de los siguientes:

-   Clientes de Configuration Manager, medios y PXE

-   Solo medios y PXE

-   Sólo medios y PXE (ocultos)

## <a name="create-the-bootable-media"></a>Crear medios de arranque
Puede especificar si el medio de arranque es una unidad flash USB o un conjunto de CD/DVD. El equipo que inicia el medio debe admitir la opción que elija como unidad de arranque. Para obtener más información, consulte [Crear medios de arranque](create-bootable-media.md).  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Instalar el sistema operativo desde un medio de arranque  
Inserte el medio de arranque en una unidad de arranque en el equipo y luego vuelva a encenderlo para instalar el sistema operativo.
