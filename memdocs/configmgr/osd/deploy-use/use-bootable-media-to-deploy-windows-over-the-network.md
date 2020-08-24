---
title: Usar medios de arranque para implementar Windows a través de la red
titleSuffix: Configuration Manager
description: Use implementaciones de medios de arranque en Configuration Manager para implementar el sistema operativo al iniciar el equipo de destino.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124763"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usar medios de arranque para implementar Windows a través de la red con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los medios de arranque solo incluyen la imagen de arranque y un puntero a la secuencia de tareas. La imagen del sistema operativo y otro contenido al que se hace referencia se descargan de la red. Dado que el medio de arranque no contiene mucho contenido, puede actualizar la secuencia de tareas y la mayoría del contenido sin tener que reemplazar el medio.

Implemente sistemas operativos a través de la red con medios de arranque en los escenarios siguientes:

- [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)

- [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md)

Realice los pasos de uno de los escenarios de implementación del sistema operativo y, luego, use las secciones siguientes para usar medios de arranque para implementar el sistema operativo.

## <a name="configure-deployment-settings"></a>Configurar la implementación

Cuando use medios de arranque para iniciar el proceso de implementación del sistema operativo, configure la implementación de secuencias de tareas para que el sistema operativo esté disponible para los medios. Establezca esta opción en la página **Deployment Settings** (Configuración de implementación) de la implementación. Para el valor **Estar disponible para**, seleccione una de las opciones siguientes:

- Clientes de Configuration Manager, medios y PXE

- Solo medios y PXE

- Sólo medios y PXE (ocultos)

Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="create-the-bootable-media"></a>Crear medios de arranque

Cuando cree medios de arranque, especifique si se trata de una unidad flash USB o de un conjunto de CD o DVD. El equipo que inicia el medio debe admitir la opción que elija como unidad de arranque. Para obtener más información, consulte [Crear medios de arranque](create-bootable-media.md).

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a> Instalación del sistema operativo desde un medio de arranque

Para instalar el sistema operativo, inserte el medio de arranque y, luego, encienda el equipo.

## <a name="support-for-cloud-based-content"></a>Compatibilidad con contenido basado en la nube

<!--6209223-->

A partir de la versión 2006, el medio de arranque puede descargar contenido de la nube. Por ejemplo, puede enviar una llave USB a un usuario remoto para restablecer la imagen inicial de su dispositivo. O una oficina que tiene un servidor de entorno PXE local, pero quiere que los dispositivos den la máxima prioridad posible a los servicios en la nube. En lugar de sobrecargar la WAN para descargar el contenido de la implementación de un sistema operativo de gran tamaño, los medios de arranque y las implementaciones del entorno PXE ahora pueden obtener contenido de orígenes basados en la nube. Por ejemplo, una instancia de Cloud Management Gateway (CMG) que se habilita para compartir contenido.

> [!NOTE]
> El dispositivo sigue necesitando una conexión de intranet al punto de administración.

Cuando se ejecuta la secuencia de tareas, se descarga el contenido de los orígenes basados en la nube. Revise el archivo **smsts.log** en el cliente.

### <a name="prerequisites"></a>Requisitos previos

- Habilite la configuración de cliente siguiente en el grupo **Cloud Services**: **Permitir acceso al punto de distribución de nube**. Asegúrese de que la configuración de cliente está implementada en los clientes de destino. Para más información, consulte [Acerca de la configuración de cliente: Dispositivos de nube](../../core/clients/deploy/about-client-settings.md#cloud-services).

- Para el grupo de límites en el que se encuentra el cliente:

  - Asocie los sistemas de sitio del punto de distribución de nube o de CMG habilitados para contenido. Para más información, vea [Configuración de un grupo de límites](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config).

  - Habilite la siguiente opción: **Preferir los orígenes basados en la nube frente a los orígenes locales**. Para más información, vea [Opciones de grupo de límites para descargas del mismo nivel](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Distribuya el contenido al que hace referencia la secuencia de tareas a la instancia de CMG habilitada para contenido o un punto de distribución en la nube.

## <a name="next-steps"></a>Pasos siguientes

[Experiencias de usuario para la implementación de sistemas operativos](../understand/user-experience.md#task-sequence-wizard)
