---
title: Administración y supervisión de implementaciones por fases
titleSuffix: Configuration Manager
description: Aprenda a administrar y supervisar las implementaciones por fases para el software en Configuration Manager.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 631a2fc3cb7df01eed1a5a6af80dd87f84455bdc
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606348"
---
# <a name="manage-and-monitor-phased-deployments"></a>Administración y supervisión de implementaciones por fases

En este artículo se describe cómo administrar y supervisar las implementaciones por fases. Las tareas de administración incluyen iniciar manualmente la siguiente fase y suspender o reanudar una fase.

En primer lugar, deberá crear una implementación por fases:

- [Aplicación](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  
- [Actualización de software](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Secuencia de tareas](create-phased-deployment-for-task-sequence.md)  

## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> Pasar a la fase siguiente

Cuando se selecciona la opción **Iniciar manualmente la segunda fase de implementación** el sitio no inicia automáticamente la siguiente fase según los criterios de éxito. Debe mover la implementación por fases a la siguiente fase.  

1. Cómo se inicia esta acción varía según el tipo de software implementado:  

    - **Aplicación**: vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.

    - **Actualización de software**: vaya al área de trabajo **Biblioteca de software** y, después, seleccione uno de los nodos siguientes:
        - Actualizaciones de software  
            - **Todas las actualizaciones de software**  
            - **Grupos de actualizaciones de software**
        - Mantenimiento de Windows 10, **Todas las actualizaciones de Windows 10**  
        - Administración de cliente de Office 365, **Actualizaciones de Office 365**  

    - **Secuencia de tareas**: En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione **Secuencias de tareas**.

2. Seleccione el software con la implementación por fases.  

3. En el panel de detalles, cambie a la pestaña **Implementaciones por fases**.  

4. Seleccione la implementación por fases y haga clic en **Pasar a la siguiente fase** en la cinta.  

    ![Clic con el botón derecho en el menú para mostrar acciones en una implementación por fases](media/Suspend-phased-deployment.PNG)

A partir de la versión 2002, use el siguiente cmdlet de Windows PowerShell para esta tarea: [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext).

## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Suspender y reanudar fases

Puede suspender o reanudar manualmente una implementación por fases. Por ejemplo, usted crea una implementación por fases para una secuencia de tareas. Durante la supervisión de la fase de su grupo piloto, observa un gran número de errores. Suspende la implementación por fases para evitar que más dispositivos ejecuten la secuencia de tareas. Después de resolver el problema, reanuda la implementación por fases para continuar con la implementación.

1. Cómo se inicia esta acción varía según el tipo de software implementado:  

    - **Aplicación**: vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.

    - **Actualización de software**: vaya al área de trabajo **Biblioteca de software** y, después, seleccione uno de los nodos siguientes:
        - Actualizaciones de software  
            - **Todas las actualizaciones de software**  
            - **Grupos de actualizaciones de software**
        - Mantenimiento de Windows 10, **Todas las actualizaciones de Windows 10**  
        - Administración de cliente de Office 365, **Actualizaciones de Office 365**  

    - **Secuencia de tareas**: En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione **Secuencias de tareas**. Seleccione una secuencia de tareas existente y después haga clic en **Crear implementación por fases** en la cinta.  

2. Seleccione el software con la implementación por fases.  

3. En el panel de detalles, cambie a la pestaña **Implementaciones por fases**.  

4. Seleccione la implementación por fases y haga clic en **Suspender** o **Reanudar** en la cinta.

> [!NOTE]
> A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](/deployoffice/name-change). Es posible que siga viendo el nombre anterior en el producto y la documentación de Configuration Manager mientras se está actualizando la consola.

A partir de la versión 2002, use los siguientes cmdlets de Windows PowerShell para esta tarea:

- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)

## <a name="monitor"></a><a name="bkmk_monitor"></a> Supervisar
<!--1358577-->

Las implementaciones por fases tienen su propio nodo de supervisión dedicada, lo que facilita la identificación de las implementaciones de este tipo que ha creado y la navegación a la vista de supervisión de implementaciones por fases. En el área de trabajo **Supervisión**, seleccione **Implementaciones por fases** y haga doble clic en una de las implementaciones por fases para ver el estado. <!--3555949-->

![Panel de estado de implementación por fases que muestra el estado de dos fases](media/1358577-phased-deployment-status.png)

Este panel muestra la siguiente información para cada fase de la implementación:  

- **Número total de dispositivos** o **Número total de recursos**: número de dispositivos que abarca esta fase.  

- **Estado**: indica el estado actual de esta fase. Cada fase puede tener uno de los siguientes estados:  

  - **Implementación creada**: la implementación por fases creó una implementación del software en la colección para esta fase. Los clientes son destinos activos con este software.  

  - **En espera**: la fase anterior aún no ha alcanzado los criterios de idoneidad para que la implementación continúe en esta fase.  

  - **Suspendida**: un administrador ha suspendido la implementación.  

- **Progreso**: estados de implementación con códigos de color de los clientes. Por ejemplo: Correcto, En curso, Error, Requisitos no cumplidos y Desconocido.

### <a name="success-criteria-tile"></a>Icono Criterios de éxito

Use el menú desplegable **Fase de selección** para cambiar la vista al icono **Criterios de éxito**. Este icono compara el **Objetivo de la fase** con el cumplimiento actual de la implementación. Con la configuración predeterminada, el objetivo de esta fase es 95 %. Este valor significa que la implementación necesita un cumplimiento del 95 % para pasar a la siguiente fase.

En este ejemplo, el objetivo de la fase es el 65 % y el cumplimiento actual es del 66,7 %. La implementación por fases se mueve automáticamente a la segunda fase, porque la primera fase cumple los criterios de éxito.  

   ![Ejemplo de icono de criterios de éxito del estado de la implementación por fases donde el objetivo es un 65 %.](media/pod-status-success-criteria-tile.png)

El objetivo de esta fase es el mismo que el **Porcentaje de éxito de la implementación** en la Configuración de fase de la *siguiente* fase. Para que la implementación por fases inicie la fase siguiente, esa segunda fase define los criterios de éxito de la primera fase. Para ver esta configuración:

1. Vaya al objeto de implementación por fases en el software y abra Propiedades de implementación por fases.  

2. Cambie a la pestaña **Fases**. Seleccione **Fase 2** y haga clic en **Ver**.  

3. En la ventana Propiedades de la fase, cambie a la pestaña **Configuración de fase**.  

4. Vea el valor de **Porcentaje de éxito de la implementación** en el grupo *Criterios de éxito de la fase anterior*.  

Por ejemplo, las siguientes propiedades son para la misma fase que el icono de criterio de éxito que se muestra anteriormente, donde el criterio es el 65 %:  

![Pestaña de configuración de fase en las propiedades de fase](media/phase-properties-phase-settings.png)

## <a name="powershell"></a>PowerShell

Use los siguientes cmdlets de Windows PowerShell para administrar implementaciones por fases:

### <a name="automatically-create-phased-deployments"></a>Crear automáticamente implementaciones por fases

- [New-CMApplicationAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmapplicationautophaseddeployment)
- [New-CMSoftwareUpdateAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdateautophaseddeployment)
- [New-CMTaskSequenceAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequenceautophaseddeployment)

### <a name="manually-create-phased-deployments"></a>Crear manualmente implementaciones por fases

- [New-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/new-cmsoftwareupdatephase)
- [New-CMSoftwareUpdateManualPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatemanualphaseddeployment)
- [New-CMTaskSequencePhase](/powershell/module/configurationmanager/new-cmtasksequencephase)
- [New-CMTaskSequenceManualPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequencemanualphaseddeployment)

### <a name="get-existing-phased-deployment-objects"></a>Obtener objetos de implementación por fases existentes

- [Get-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/get-cmapplicationphaseddeployment)
- [Get-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/get-cmsoftwareupdatephaseddeployment)
- [Get-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/get-cmtasksequencephaseddeployment)
- [Get-CMPhase](/powershell/module/configurationmanager/get-cmphase)

### <a name="monitor-phased-deployment-status"></a>Supervisar el estado de implementación por fases

- [Get-CMPhasedDeploymentStatus](/powershell/module/configurationmanager/get-cmphaseddeploymentstatus)

### <a name="manage-existing-phased-deployments"></a>Administrar implementaciones por fases existentes

- [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)
- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)

### <a name="modify-existing-phased-deployments"></a>Modificar implementaciones por fases existentes

- [Set-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/set-cmapplicationphaseddeployment)
- [Set-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/set-cmsoftwareupdatephase)
- [Set-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/set-cmsoftwareupdatephaseddeployment)
- [Set-CMTaskSequencePhase](/powershell/module/configurationmanager/set-cmtasksequencephase)
- [Set-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/set-cmtasksequencephaseddeployment)
- [Remove-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/remove-cmapplicationphaseddeployment)
- [Remove-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/remove-cmsoftwareupdatephaseddeployment)
- [Remove-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/remove-cmtasksequencephaseddeployment)
