---
title: Usar Centro de software para implementar Windows a través de la red
titleSuffix: Configuration Manager
description: Puede implementar un sistema operativo en el Centro de software para actualizar un equipo existente con una nueva versión de Windows o para actualizar Windows a la versión más reciente.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709033"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usar el Centro de software para implementar Windows a través de la red con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede hacer que la secuencia de tareas que instala un sistema operativo en Configuration Manager esté disponible en el Centro de software. Puede implementar un sistema operativo en el Centro de software en los siguientes escenarios de implementación de sistema operativo:

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)

Complete los pasos de uno de los escenarios de implementación de sistema operativo. Luego siga estas secciones para prepararse para las implementaciones que están disponibles en el Centro de software.

## <a name="configure-deployment-settings"></a>Configurar la implementación  
Para que la implementación de sistema operativo esté disponible en el Centro de software, configure la implementación. Puede configurar la implementación en la página **Configuración de implementación** del Asistente para implementar software o en la pestaña **Configuración de implementación** en las propiedades de la implementación. Para la configuración **Estar disponible para** , configure **Solo clientes de Configuration Manager** o **PXE, medios y clientes de Configuration Manager**. Una vez que el sistema implemente el sistema operativo, este aparecerá en el Centro de software para los miembros de la recopilación de destino.

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> Implemente la secuencia de tareas en los equipos.  
Implemente el sistema operativo en una recopilación de destino. Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md). Al implementar sistemas operativos para el Centro de software, puede configurar si la implementación es necesaria o está disponible.

-   **Implementación requerida**: las implementaciones necesarias harán que el sistema operativo esté disponible en el Centro de software, pero se iniciará automáticamente según la programación de asignación configurada.

-   **Implementación disponible**: el sistema operativo estará disponible en el Centro de software y el usuario puede instalarlo a petición.
