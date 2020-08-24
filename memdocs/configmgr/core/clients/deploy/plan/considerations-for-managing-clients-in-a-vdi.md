---
title: Administrar clientes VDI
titleSuffix: Configuration Manager
description: Administre clientes de Configuration Manager en una infraestructura de escritorio virtual (VDI).
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d79edb5ad1a60c5876163281ec5c1d1c17eff0a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692815"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Administración de clientes de Configuration Manager en una infraestructura de escritorio virtual (VDI)

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager admite la instalación del cliente de Configuration Manager en los siguientes escenarios de infraestructura de escritorio virtual (VDI):

- **Máquinas virtuales personales**: la máquina virtual (VM) mantiene los datos y la configuración del usuario de una sesión a otra.

- **Herramientas de Servicios de Escritorio remoto**: hospede varias sesiones de cliente simultáneas en un servidor centralizado. Los usuarios se conectan a una sesión y ejecutan aplicaciones en ese servidor.

- **Máquinas virtuales agrupadas**: la máquina virtual no se conserva de una sesión a otra. Cuando un usuario cierra una sesión, el entorno virtual descarta todos los datos y configuraciones. Las máquinas virtuales agrupadas son útiles cuando no se pueden usar los Servicios de Escritorio remoto. Por ejemplo, si una aplicación necesaria no se puede ejecutar en el servidor de Windows que hospeda las sesiones de cliente.

- **Windows Virtual Desktop**: un servicio de virtualización de escritorio y aplicaciones que se ejecuta en Microsoft Azure. A partir de la versión 1906, use Configuration Manager para administrar estos dispositivos virtuales que ejecutan Windows en Azure.

## <a name="personal-vms"></a>Máquinas virtuales personales

Configuration Manager trata a las máquinas virtuales personales como si fueran equipos físicos. Puede preinstalar el cliente de Configuration Manager en la imagen de máquina virtual o después de aprovisionarlo.

Para más información, consulte [Compatibilidad con entornos de virtualización](../../../plan-design/configs/support-for-virtualization-environments.md).

## <a name="remote-desktop-services"></a>Servicios de Escritorio remoto

No se ha instalado el cliente de Configuration Manager para sesiones de Escritorio Remoto individuales. Instálelo una vez en el servidor que hospeda los Servicios de Escritorio remoto. Puede usar todas las características del cliente de Configuration Manager en el servidor de Servicios de Escritorio Remoto.

Para más información, consulte [Bienvenida a Servicios de Escritorio remoto](/windows-server/remote/remote-desktop-services/welcome-to-rds).

## <a name="pooled-vms"></a>Máquinas virtuales agrupadas

Cuando se retira una máquina virtual agrupada, se pierden todos los cambios realizados por Configuration Manager.

Dado que la máquina virtual podría estar operativa solo durante un breve período de tiempo, es posible que algunas características de Configuration Manager no devuelvan datos de interés. Por ejemplo, inventario de software, inventario de hardware y medición de software. Considere la posibilidad de excluir la máquina virtual agrupada de las tareas del inventario.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

Para más información, vea [Sistemas operativos compatibles con clientes y dispositivos](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="other-considerations"></a>Otras consideraciones

Dado que la virtualización admite la ejecución de varios clientes de Configuration Manager en el mismo equipo físico, muchas operaciones de cliente tienen un retraso aleatorio integrado en acciones programadas. Por ejemplo, inventario de hardware y software, exámenes antimalware, instalaciones de software y exámenes de actualización de software. Este retraso ayuda a distribuir el procesamiento de la CPU y la transferencia de datos en un servidor que tiene varias máquinas virtuales que ejecutan el cliente de Configuration Manager.

A excepción de los clientes de Windows Embedded en modo de servicio, los clientes de Configuration Manager que no están en entornos virtualizados también usan este retraso aleatorio. Este comportamiento ayuda a evitar picos en el ancho de banda de red. También reduce el procesamiento de la CPU en los sistemas de sitio, como el punto de administración y el servidor de sitio. El intervalo de retraso varía según la capacidad de Configuration Manager. Por ejemplo, consulte [Acerca de la configuración de cliente: Deshabilitar selección aleatoria de fecha límite](../about-client-settings.md#disable-deadline-randomization).

Para contribuir al rendimiento del cliente de Configuration Manager en entornos virtuales que admiten varias sesiones de usuario, se deshabilita la directiva de usuario de forma predeterminada. A partir de la versión 1910, puede habilitar la directiva de usuario en este escenario. Para más información, consulte [Acerca de la configuración de cliente: Habilitar la directiva de usuario para varias sesiones de usuario](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions).