---
title: Actualización a Windows 10
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar Configuration Manager para actualizar un sistema operativo de Windows 7 o una versión posterior a Windows 10.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a9ed8e1ece27117993761a3ce52c462e94e9f79a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124780"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Actualización de Windows a la última versión con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se proporcionan los pasos de Configuration Manager para actualizar el sistema operativo de un equipo. Puede elegir entre distintos métodos de implementación, como medios independientes o el Centro de software. El escenario de actualización local tiene las características siguientes:  

- Actualiza el sistema operativo a Windows 10 o Windows Server 2016 y versiones posteriores.

- Conserva las aplicaciones, la configuración y los datos de usuario en el equipo.

- No tiene dependencias externas, como Windows ADK.

- Es más rápido y resistente que las implementaciones de SO tradicionales.

> [!Note]  
> La secuencia de tareas de actualización en contexto de Windows 10 ahora admite la implementación en los clientes basados en Internet que se administran a través de [Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md). Esta función permite a los usuarios remotos actualizar con mayor facilidad a Windows 10 sin necesidad de conectarse a la intranet. Para obtener más información, vea [Implementar una actualización local de Windows 10 a través de CMG](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->


## <a name="supported-versions"></a>Versiones admitidas

### <a name="upgrade-version"></a>Versión de actualización

Cree solo paquetes de actualización del sistema operativo para actualizar a las siguientes versiones del sistema operativo:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>Versión original

Los dispositivos deben ejecutar una de las siguientes versiones del sistema operativo para tener como destino una secuencia de tareas de actualización del sistema operativo:

#### <a name="windows-client"></a>Cliente de Windows

- Windows 7
- Windows 8.1
- Una versión anterior de Windows 10. Por ejemplo, se puede actualizar Windows 10 de la versión 1809 a la versión 1903.  

Para obtener más información, vea [Rutas de actualización de Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths).

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- Una versión anterior de Windows Server 2016.
- Una versión anterior de Windows Server 2019.

Para obtener más información sobre las rutas de actualización compatibles con Windows Server, vea [Rutas de actualización compatibles con Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) y [Centro de actualización de Windows Server](https://aka.ms/upgradecenter).


## <a name="plan"></a><a name="BKMK_Plan"></a> Plan  

### <a name="task-sequence-requirements-and-limitations"></a>Limitaciones y requisitos de la secuencia de tareas

Revise los siguientes requisitos y limitaciones de la secuencia de tareas para actualizar un sistema operativo y asegurarse de que satisface sus necesidades:  

- Agregue solo los pasos de secuencia de tareas que están relacionados con la tarea principal de actualización del sistema operativo. Estos pasos incluyen principalmente la instalación de paquetes, aplicaciones o actualizaciones. Use también los pasos que ejecutan líneas de comandos, PowerShell o establecen variables dinámicas.  

- Revise los controladores y las aplicaciones que están instalados en los equipos. Antes de implementar la secuencia de tareas de actualización, asegúrese de que los controladores son compatibles con Windows 10.  

Las tareas siguientes no son compatibles con la actualización local. Requieren que se usen las implementaciones de SO tradicionales:  

- Cambiar la pertenencia a dominios del equipo o actualizar el grupo de administradores locales.  

- Implementar un cambio fundamental en el equipo, como:

  - Cambiar las particiones de disco.
  - Cambiar la arquitectura del sistema de x86 a x64.
  - Implementar UEFI. (Para obtener más información sobre una opción posible, vea [Conversión de BIOS a UEFI durante una actualización local](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)).
  - Modificar el idioma del sistema operativo base.  

- Tiene requisitos personalizados, como el uso de una imagen base personalizada, el uso de cifrado de disco de terceros o requerir operaciones de WinPE sin conexión.  

### <a name="infrastructure-requirements"></a>Requisitos de la infraestructura  

El único requisito previo para el escenario de actualización es tener un punto de distribución disponible. Distribuya el paquete de actualización de SO y todos los paquetes que se incluyan en la secuencia de tareas. Para obtener más información, consulte [Instalar o modificar un punto de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).


## <a name="configure"></a><a name="BKMK_Configure"></a> Configurar  

### <a name="prepare-the-os-upgrade-package"></a>Preparar el paquete de actualización de SO  

El paquete de actualización de Windows 10 contiene los archivos de origen necesarios para actualizar el sistema operativo en el equipo de destino. El paquete de actualización debe coincidir en la edición, la arquitectura y el idioma con los clientes que actualice. Para más información, vea [Administrar paquetes de actualización de sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Crear una secuencia de tareas para actualizar el sistema operativo  

Siga los pasos que aparecen en [Creación de una secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) con el objetivo de automatizar la actualización del sistema operativo.  

> [!NOTE]  
> Para crear una secuencia de tareas con el objetivo de actualizar un sistema operativo a Windows 10, normalmente se siguen los pasos descritos en [Creación de una secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md). La secuencia de tareas incluye el paso **Actualizar sistema operativo**, así como pasos adicionales recomendados y grupos para controlar el proceso de actualización integral.
>
> Puede crear una secuencia de tareas personalizada y agregar el paso [Actualizar SO](../understand/task-sequence-steps.md#BKMK_UpgradeOS). Este paso es el único necesario para actualizar el sistema operativo a Windows 10. Si elige este método, agregue también el paso [Reiniciar equipo](../understand/task-sequence-steps.md#BKMK_RestartComputer) después del paso **Actualizar sistema operativo** para completar la actualización. Asegúrese de usar la opción **El sistema operativo predeterminado instalado actualmente** para reiniciar el equipo con el sistema operativo instalado y no con Windows PE.  


## <a name="deploy"></a><a name="BKMK_Deploy"></a> Implementar  

Para implementar el sistema operativo, use uno de los métodos de implementación siguientes:  

- [Usar Centro de software para implementar Windows a través de la red](use-software-center-to-deploy-windows-over-the-network.md)  

- [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md) (Uso de medios independientes para implementar Windows sin usar la red)  

  > [!IMPORTANT]  
  > Cuando use medios independientes, debe incluir una imagen de arranque en la secuencia de tareas. Esta configuración hace que la secuencia de tareas esté disponible en el Asistente para crear medio de secuencia de tareas.


## <a name="monitor"></a>Supervisión  

Para supervisar la implementación de la secuencia de tareas con el objetivo de actualizar el sistema operativo, vea [Supervisar implementaciones del sistema operativo](monitor-operating-system-deployments.md).  
