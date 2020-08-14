---
title: Captura y restauración de estado de usuario
titleSuffix: Configuration Manager
description: Use secuencias de tareas de Configuration Manager para capturar y restaurar los datos de estado de usuario en escenarios de implementación de sistema operativo.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a1f11c46689b213b795c0d71221728f916a68bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125498"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Creación de una secuencia de tareas para capturar y restaurar el estado de usuario en Configuration Manager

 *Se aplica a: Configuration Manager (rama actual)*

 Use secuencias de tareas de Configuration Manager para capturar y restaurar los datos de estado de usuario en escenarios de implementación de sistema operativo. En estos casos, desea conservar el estado de usuario del sistema operativo actual. Según el tipo de tarea de secuencia de tareas que cree, las etapas de captura y restauración podrían agregarse automáticamente como parte de la secuencia de tareas. En otros escenarios, es posible que deba agregar manualmente las etapas de captura y restauración a la secuencia de tareas. En este artículo se indican las etapas que se deben agregar a una secuencia de tareas existente para capturar y restaurar los datos de estado de usuario.  



## <a name="task-sequence-steps"></a>Pasos de la secuencia de tareas  

Para capturar y restaurar el estado del usuario, agregue los pasos siguientes a la secuencia de tareas:  

- [Solicitar almacén de estado](../understand/task-sequence-steps.md#BKMK_RequestStateStore): en caso de que se almacene el estado de usuario en el punto de migración de estado, necesita este paso.  

- [Capturar estado de usuario](../understand/task-sequence-steps.md#BKMK_CaptureUserState): este paso captura los datos de estado de usuario. A continuación, almacena los datos en el punto de migración de estado o el disco local mediante vínculos físicos.  

- [Restaurar estado de usuario](../understand/task-sequence-steps.md#BKMK_RestoreUserState): este paso restaura los datos de estado de usuario en el equipo de destino. Puede recuperar los datos desde un punto de migración de estado o si tiene un vínculo físico en el disco local.  

- [Liberar almacén de estado](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): en caso de que se almacene el estado de usuario en el punto de migración de estado, necesita este paso. Este paso quita los datos del punto de migración de estado.  


 Utilice los procedimientos siguientes para agregar los pasos de la secuencia de tareas necesarios para capturar y restaurar el estado de usuario. Para obtener más información sobre la creación de secuencias de tareas, vea [Administrar secuencias de tareas para automatizar tareas](manage-task-sequences-to-automate-tasks.md).  



## <a name="capture-the-user-state"></a>Captura del estado del usuario  

 Para agregar pasos a una secuencia de tareas para capturar el estado de usuario, siga estos pasos:

1.  En la lista **Secuencias de tareas** , seleccione una secuencia de tareas y, a continuación, haga clic en **Editar**.  

2.  Si utiliza un punto de migración de estado para almacenar el estado de usuario, agregue el paso **Liberar almacén de estado** a la secuencia de tareas. En el **Editor de secuencia de tareas**, haga clic en **Agregar**. Seleccione **Estado de usuario** y, a continuación, haga clic en **Solicitar almacén de estado**. Configure las propiedades y opciones para este paso y, a continuación, haga clic en **Aplicar**. Para obtener más información acerca de las opciones disponibles, vea [Solicitar almacén de estado](../understand/task-sequence-steps.md#BKMK_RequestStateStore).  

3.  Agregue el paso **Capturar estado de usuario** a la secuencia de tareas. En el **Editor de secuencia de tareas**, haga clic en **Agregar**. Seleccione **Estado de usuario** y, a continuación, haga clic en **Capturar estado de usuario**. Configure las propiedades y opciones para este paso y, a continuación, haga clic en **Aplicar**. Para obtener más información acerca de las opciones disponibles, vea [Capturar estado de usuario](../understand/task-sequence-steps.md#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Cuando se agrega este paso a la secuencia de tareas, también debe establecerse la variable de secuencia de tareas **OSDStateStorePath** para especificar dónde se almacenan los datos de estado de usuario. Si almacena el estado de usuario localmente, no especifique una carpeta raíz, dado que eso puede provocar un error en la secuencia de tareas. Siempre que almacene los datos de usuario localmente, utilice una carpeta o subcarpeta. Para obtener más información sobre las variables de secuencia de tareas, consulte [Task sequence variables](../understand/task-sequence-variables.md#OSDStateStorePath) (Variables de secuencia de tareas).  

4.  Si usa un punto de migración de estado, agregue el paso **Liberar almacén de estado** a la secuencia de tareas. En el **Editor de secuencia de tareas**, haga clic en **Agregar**. Seleccione **Estado de usuario** y, a continuación, haga clic en **Liberar almacén de estado**. Configure las propiedades y opciones para este paso y, a continuación, haga clic en **Aplicar**. Para obtener más información acerca de las opciones disponibles, vea [Liberar almacén de estado](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  La acción de la secuencia de tareas que se ejecuta antes del paso **Liberar almacén de estado** debe finalizar correctamente para que se inicie el paso **Liberar almacén de estado**.  


 Implemente esta secuencia de tareas para capturar el estado de usuario en un equipo de destino. Para más información sobre cómo implementar secuencias de tareas, vea [Deploy a task sequence (Implementar una secuencia de tareas)](deploy-a-task-sequence.md).  



## <a name="restore-the-user-state"></a>Restauración del estado de usuario  

 Para agregar pasos a una secuencia de tareas para restaurar el estado de usuario, siga estos pasos:

1. En la lista **Secuencias de tareas** , seleccione una secuencia de tareas y, a continuación, haga clic en **Editar**.  

2. Agregue el paso **Restaurar estado de usuario** a la secuencia de tareas. En el **Editor de secuencia de tareas**, haga clic en **Agregar**. Seleccione **Estado de usuario** y, a continuación, haga clic en **Restaurar estado de usuario**. Este paso establece una conexión con el punto de migración de estado si es necesario. Configure las propiedades y opciones para este paso y, a continuación, haga clic en **Aplicar**. Para obtener más información acerca de las opciones disponibles, vea [Restaurar estado de usuario](../understand/task-sequence-steps.md#BKMK_RestoreUserState).  

   > [!Important]  
   >  Si usa el paso [Capturar estado de usuario](../understand/task-sequence-steps.md#BKMK_CaptureUserState) con la opción de **Capturar todos los perfiles de usuario mediante opciones estándar**, debe seleccionar la opción **Restaurar perfiles de usuario de equipo local** en el paso **Restaurar estado de usuario**. En caso contrario, se producirá un error en la secuencia de tareas.  

   > [!Note]  
   > Si almacena el estado de usuario mediante el uso de vínculos físicos locales y la restauración no se realiza correctamente, puede eliminar manualmente los vínculos físicos que se crearon para almacenar los datos. La secuencia de tareas puede ejecutar la herramienta USMTUtils para automatizar esta acción con un paso [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine). Si usa USMTUtils para eliminar el vínculo físico, agregue un paso [Reiniciar equipo](../understand/task-sequence-steps.md#BKMK_RestartComputer) después de ejecutar USMTUtils.  

3. Si usa un punto de migración de estado para almacenar el estado de usuario, agregue el paso **Liberar almacén de estado** a la secuencia de tareas. En el **Editor de secuencia de tareas**, haga clic en **Agregar**. Seleccione **Estado de usuario** y, a continuación, haga clic en **Liberar almacén de estado**. Configure las propiedades y opciones para este paso y, a continuación, haga clic en **Aplicar**. Para obtener más información acerca de las opciones disponibles, vea [Liberar almacén de estado](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  La acción de la secuencia de tareas que se ejecuta antes del paso **Liberar almacén de estado** debe finalizar correctamente para que se inicie el paso **Liberar almacén de estado**.  


 Implemente esta secuencia de tareas para restaurar el estado de usuario en un equipo de destino. Para más información sobre la implementación de secuencias de tareas, vea [Deploy a task sequence (Implementar una secuencia de tareas)](deploy-a-task-sequence.md).  



## <a name="next-steps"></a>Pasos siguientes

[Supervisar la implementación de la secuencia de tareas](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
