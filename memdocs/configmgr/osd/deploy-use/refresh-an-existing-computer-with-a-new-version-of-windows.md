---
title: Actualización del sistema operativo de un equipo existente
titleSuffix: Configuration Manager
description: Puede usar varios métodos en Configuration Manager para la partición y el formato de un equipo existente, así como para instalar un nuevo sistema operativo en el equipo.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9582d6840e1f750d53504da4e8e7f6bf54f44965
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708413"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Actualizar un equipo existente con una nueva versión de Windows

*Se aplica a: Configuration Manager (rama actual)*

Use Configuration Manager para la partición y el formato de un equipo existente, y después instale un sistema operativo nuevo. Este proceso se denomina a veces *restablecimiento de la imagen inicial* o *instalación desde cero*. Para este escenario, puede elegir entre muchos métodos de implementación diferentes, como PXE, el medio de arranque o el Centro de software. También puede usar un punto de migración de estado para almacenar la configuración y, después, restaurarla en el nuevo sistema operativo.

Para elegir el escenario de implementación de sistema operativo adecuado, vea [Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="plan"></a><a name="BKMK_Plan"></a> Plan  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Planeación e implementación de los requisitos de infraestructura

Hay varios requisitos de infraestructura que se deben cumplir para poder implementar un sistema operativo. Algunos de estos requisitos incluyen Windows ADK, la Herramienta de migración de estado de usuario (USMT) y Servicios de implementación de Windows (WDS). Para más información, vea [Requisitos de infraestructura para la implementación de SO en Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="install-a-state-migration-point"></a>Instalación de un punto de migración de estado

Si quiere capturar la configuración de un equipo existente y después restaurarla en el sistema operativo nuevo, considere la posibilidad de usar un punto de migración de estado. Para obtener más información, consulte [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints) (Punto de migración de estado).  

## <a name="configure"></a><a name="BKMK_Configure"></a> Configurar  

### <a name="prepare-a-boot-image"></a>Preparar una imagen de arranque

Las imágenes de arranque inician un equipo en un entorno de Windows PE. Windows PE es un sistema operativo mínimo con servicios y componentes limitados. Desde Windows PE, Configuration Manager puede instalar un sistema operativo Windows completo en el equipo.

Vea los siguientes artículos para más información:

- [Administrar imágenes de arranque](../get-started/manage-boot-images.md)

- [Personalizar imágenes de arranque](../get-started/customize-boot-images.md)

- [Distribución de contenido](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Preparación de una imagen del sistema operativo

La imagen del sistema operativo contiene los archivos necesarios para instalar el sistema operativo en el equipo de destino.

Vea los siguientes artículos para más información:

- [Administración de imágenes del sistema operativo](../get-started/manage-operating-system-images.md)

- [Distribución de contenido](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creación de una secuencia de tareas para implementar un sistema operativo

Use una secuencia de tareas para automatizar la instalación del sistema operativo. Según el método de implementación que elija, puede haber consideraciones adicionales para la secuencia de tareas.

Vea los siguientes artículos para más información:

- [Creación de una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md)

- [Administrar el estado de usuario](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a> Implementar

- Para implementar el sistema operativo, use uno de los métodos de implementación siguientes:  

  - [Usar PXE para implementar Windows a través de la red](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Usar multidifusión para implementar Windows a través de la red](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Crear una imagen para un OEM en fábrica o en un almacén local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md) (Uso de medios independientes para implementar Windows sin usar la red)  

  - [Usar medios de arranque para implementar Windows a través de la red](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Usar Centro de software para implementar Windows a través de la red](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Supervisión  

Para más información, vea [Supervisar las implementaciones de sistema operativo en System Center Configuration Manager](monitor-operating-system-deployments.md).  

> [!Note]
> Al restablecer la imagen inicial de un dispositivo UEFI, Administración de arranque de Windows crea una entrada en el cargador de arranque. Este comportamiento es más evidente cuando se restablece la imagen inicial de un dispositivo de forma repetida, como en un entorno de prueba o un laboratorio para alumnos. Por lo general, no afecta al rendimiento ni al uso del dispositivo. Si la lista es demasiado grande, es posible que algunos dispositivos de hardware específicos encuentren problemas funcionales. Por ejemplo, la imposibilidad de arrancar en una unidad USB externa o de seleccionar la entrada de arranque actual de la lista. Use el comando **bcdedit** de Windows para borrar las entradas de arranque sin usar. Para obtener más información, vea [BCDEdit/deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
