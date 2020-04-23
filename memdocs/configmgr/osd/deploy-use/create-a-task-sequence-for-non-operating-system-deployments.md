---
title: Crear una secuencia de tareas para implementaciones que no son de sistema operativo
titleSuffix: Configuration Manager
description: Creación de secuencias de tareas que no son para implementar un sistema operativo, como la distribución de software o la automatización de tareas
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 583a90452fe077057b93150e9cb635fe9269de5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709073"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Crear una secuencia de tareas para implementaciones que no son de sistema operativo

*Se aplica a: Configuration Manager (rama actual)*

Las secuencias de tareas de Configuration Manager se usan para automatizar diferentes clases de tareas del entorno. Estas tareas están diseñadas principalmente y probadas para implementar sistemas operativos. Configuration Manager tiene muchas otras características que deben ser la tecnología principal que use en los siguientes escenarios:

- [Instalación de la aplicación](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > A partir de la versión 2002, puede instalar aplicaciones complejas mediante secuencias de tareas a través del modelo de aplicación. Agregue un tipo de implementación a una aplicación que sea una secuencia de tareas, para instalar o desinstalar la aplicación. Para obtener más información, vea [Creación de aplicaciones Windows](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [Instalación de actualizaciones de software](../../sum/understand/software-updates-introduction.md)

- [Establecimiento de la configuración](../../compliance/understand/ensure-device-compliance.md)

Considere también otras tecnologías de automatización de Microsoft System Center, como [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) y [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

La eficacia de las secuencias de tareas radica en su flexibilidad y en cómo se usan. Se pueden usar para configurar clientes, distribuir software, actualizar controladores, editar estados de usuario y realizar otras tareas independientes de la implementación del sistema operativo. Puede crear una secuencia de tareas personalizada para agregar cualquier número de tareas. En Configuration Manager se admite el uso de secuencias de tareas personalizadas para implementaciones que no son de sistema operativo. Pero si una secuencia de tareas produce resultados incoherentes o no deseados, debe buscar formas de simplificar la operación:

- Usar pasos más sencillos
- Dividir las acciones entre varias secuencias de tareas
- Adoptar un enfoque por fases para crear y probar la secuencia de tareas

Los siguientes pasos pueden usarse en una secuencia de tareas personalizada de una implementación que no es de sistema operativo:  

- [Comprobar preparación](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Conectar a carpeta de red](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Descargar contenido de paquete](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Instalar aplicación](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Instalar paquete](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Instalar actualizaciones de software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Reiniciar equipo](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [Ejecutar script de PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Ejecutar secuencia de tareas](../understand/task-sequence-steps.md#child-task-sequence)  

- [Establecer variables dinámicas](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Establecer variable de secuencia de tareas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  
