---
title: Usar multidifusión para implementar Windows a través de la red
titleSuffix: Configuration Manager
description: Use multidifusión en su entorno de Configuration Manager para que varios equipos puedan descargar simultáneamente la imagen del sistema operativo.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124712"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usar multidifusión para implementar Windows a través de la red con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La multidifusión es un método de optimización de red que puede usar cuando es probable que varios clientes descarguen la misma imagen del sistema operativo al mismo tiempo. Cuando se usa la multidifusión, varios equipos descargan a la vez la imagen del sistema operativo, ya que el punto de distribución la distribuye mediante multidifusión. Este comportamiento es lo contrario a que cada cliente descargue una copia de la imagen a través de una conexión independiente desde el punto de distribución.

Implemente sistemas operativos a través de la red mediante multidifusión en los siguientes escenarios de implementación del sistema operativo:

- [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)

Realice los pasos de uno de estos escenarios de implementación del sistema operativo. A continuación, use las secciones siguientes para admitir la multidifusión.

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a> Configuración de puntos de distribución para multidifusión

Para usar multidifusión, configure al menos un punto de distribución que la admita. Para obtener más información, vea [Instalación y configuración de puntos de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

Para consultar una lista de los puertos necesarios para admitir la multidifusión, vea [Puertos](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).

## <a name="prepare-an-os-image-for-multicast"></a>Preparación de una imagen del sistema operativo para multidifusión

Debe configurar la imagen del sistema operativo para que admita multidifusión. Para más información, consulte [Preparación de la imagen de sistema operativo para implementaciones de multidifusión](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Implementar la secuencia de tareas

Implemente el sistema operativo en una recopilación de destino. Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="next-steps"></a>Pasos siguientes

[Experiencias de usuario para la implementación de sistemas operativos](../understand/user-experience.md)
