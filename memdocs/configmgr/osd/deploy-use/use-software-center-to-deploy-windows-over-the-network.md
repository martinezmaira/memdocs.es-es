---
title: Usar Centro de software para implementar Windows a través de la red
titleSuffix: Configuration Manager
description: Implemente un sistema operativo desde el Centro de software para actualizar un equipo existente con una nueva versión de Windows o para actualizar Windows a la versión más reciente.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124608"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usar el Centro de software para implementar Windows a través de la red con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede crear una secuencia de tareas que instale un sistema operativo disponible en el Centro de software. Un usuario puede ejecutar una secuencia de tareas desde el Centro de software en los siguientes escenarios de implementación del sistema operativo:

- [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)

- [Crear una secuencia de tareas para implementaciones que no son de sistema operativo](create-a-task-sequence-for-non-operating-system-deployments.md)

Realice los pasos de uno de esos escenarios de implementación del sistema operativo. Luego siga estas secciones para prepararse para las implementaciones que están disponibles en el Centro de software.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Implementar la secuencia de tareas

Implemente la secuencia de tareas en una colección de destino. Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md).

En la página **Deployment Settings** (Configuración de implementación) de la implementación, en la opción **Make available to the following** (Estar disponible para), seleccione una de las siguientes opciones:

- Solo clientes de Configuration Manager

- Clientes de Configuration Manager, medios y PXE

Configure también si la implementación es necesaria o está disponible:

- Implementación necesaria: las implementaciones necesarias hacen que la secuencia de tareas esté disponible en el Centro de software. Se inicia automáticamente en la fecha límite configurada.

- Implementación disponible: la secuencia de tareas está disponible en el Centro de software y los usuarios pueden instalarla a petición.

Después de crear la implementación, los clientes de la colección de destino mostrarán la secuencia de tareas en el Centro de software.

## <a name="next-steps"></a>Pasos siguientes

[Experiencias de usuario para la implementación de sistemas operativos](../understand/user-experience.md#software-center)
