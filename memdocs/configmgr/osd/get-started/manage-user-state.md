---
title: Administrar el estado de usuario
titleSuffix: Configuration Manager
description: Configuration Manager usa la Herramienta de migración de estado de usuario para capturar y restaurar los datos de estado de usuario en escenarios de implementación de sistema operativo.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4975f67c84c2354d13457981ac90ba4481d292f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697592"
---
# <a name="manage-user-state-in-configuration-manager"></a>Administración del estado de usuario en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede usar secuencias de tareas de Configuration Manager para capturar y restaurar los datos de estado de usuario en los escenarios de implementación de sistema operativo donde quiere conservar el estado de usuario del sistema operativo actual. Por ejemplo:  

- Implementaciones donde desea capturar el estado de usuario de un equipo para restaurarlo en otro equipo.  

- Implementaciones de actualizaciones donde desea capturar y restaurar el estado de usuario en el mismo equipo.  

Configuration Manager usa la Herramienta de migración de estado de usuario (USMT) 10.0 para administrar la migración de datos de estado de usuario de un equipo de origen a un equipo de destino una vez completada la instalación del sistema operativo. Para más información acerca de escenarios de migración habituales de USMT 10.0, consulte  [Escenarios de migración habituales](/windows/deployment/usmt/usmt-common-migration-scenarios).

En las secciones siguientes obtendrá ayuda para la captura y la restauración de datos de usuario.

## <a name="store-user-state-data"></a><a name="BKMK_StoringUserData"></a> Almacenar datos de estado de usuario

 Al capturar el estado de usuario, puede almacenar los datos de estado de usuario en el equipo de destino o en un punto de migración de estado. Para almacenar el estado de usuario en un punto de migración de estado de usuario, debe usar un servidor de sistema de sitio de Configuration Manager que hospede el rol de sistema de sitio de punto de migración de estado. Para almacenar el estado de usuario en el equipo de destino, debe configurar la secuencia de tareas para almacenar los datos localmente mediante vínculos.

> [!NOTE]
> Los vínculos que se utilizan para almacenar el estado de usuario localmente se conocen como vínculos físicos. Los vínculos físicos constituyen una característica de USMT 10.0 que busca en el equipo si hay archivos y configuración de usuario y, después, crea un directorio de vínculos físicos a esos archivos. Los vínculos físicos, a continuación, se utilizan para restaurar los datos del usuario después de implementado el nuevo sistema operativo.

> [!IMPORTANT]
> No se puede utilizar un punto de migración de estado y emplear vínculos físicos para almacenar los datos de estado de usuario al mismo tiempo.

Cuando se captura la información del estado del usuario, esta información se puede almacenar de una de las siguientes maneras:  

- Puede guardar los datos de estado de usuario de forma remota mediante la configuración de un punto de migración de estado. La secuencia de tareas de **captura** envía los datos al punto de migración de estado. A continuación, una vez implementado el sistema operativo, la secuencia de tareas de **restauración** recupera los datos y restaura el estado de usuario en el equipo de destino.  

- Puede almacenar los datos de estado de usuario localmente en una ubicación específica. En este escenario, la secuencia de tareas de **captura** copia los datos de usuario en una ubicación específica del equipo de destino. A continuación, una vez implementado el sistema operativo, la secuencia de tareas de **restauración** recupera los datos del usuario desde esa ubicación.  

- Puede especificar vínculos físicos que pueden utilizarse para restaurar los datos del usuario a su ubicación original. En este escenario, los datos de estado de usuario permanecen en la unidad cuando se quita el sistema operativo antiguo. A continuación, una vez implementado el sistema operativo, la secuencia de tareas de **restauración** usa los vínculos físicos para restaurar los datos de estado de usuario a su ubicación original.  

### <a name="store-user-data-on-a-state-migration-point"></a><a name="BKMK_UserDataSMP"></a> Almacenar datos de usuario en un punto de migración de estado

 Para almacenar los datos de estado de usuario en un punto de migración de estado, debe realizar lo siguiente:  

1. [Configure a state migration point](#BKMK_StateMigrationPoint) para almacenar los datos de estado de usuario.  

1. [Create a computer association](#BKMK_ComputerAssociation) entre el equipo de origen y el equipo de destino. Debe crear esta asociación para capturar el estado de usuario en el equipo de origen.  

1. [Cree una secuencia de tareas para capturar y restaurar el estado del usuario](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). En concreto, debe agregar las siguientes etapas de secuencia de tareas para capturar los datos de usuario de un equipo, almacenarlos en un punto de migración de estado y restaurarlos en un equipo:  

    - [Solicitar almacén de estado](../understand/task-sequence-steps.md#BKMK_RequestStateStore) para solicitar acceso a un punto de migración de estado al capturar el estado de un equipo o restaurar el estado en un equipo.  

    - [Capturar estado de usuario](../understand/task-sequence-steps.md#BKMK_CaptureUserState) para capturar y almacenar los datos de estado de usuario en el punto de migración de estado.  

    - [Restaurar estado de usuario](../understand/task-sequence-steps.md#BKMK_RestoreUserState) para recuperar el estado de usuario en el equipo de destino mediante la recuperación de los datos desde un punto de migración de estado de usuario.  

    - [Liberar almacén de estado	](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) para notificar al punto de migración de estado que la acción de captura o restauración se completó.  

### <a name="store-user-data-locally"></a><a name="BKMK_UserDataDestination"></a> Almacenar datos de usuario localmente

 Para almacenar los datos de estado de usuario localmente, debe hacer lo siguiente:  

- [Cree una secuencia de tareas para capturar y restaurar el estado del usuario](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). En concreto, debe agregar las siguientes etapas de secuencia de tareas para capturar los datos de usuario de un equipo y restaurarlos en un equipo mediante vínculos físicos:

  - [Capturar estado de usuario](../understand/task-sequence-steps.md#BKMK_CaptureUserState) para capturar y almacenar los datos de estado de usuario en una carpeta local mediante vínculos físicos.  

  - [Restaurar estado de usuario](../understand/task-sequence-steps.md#BKMK_RestoreUserState) para restaurar el estado de usuario en el equipo de destino mediante la recuperación de los datos a través de vínculos físicos.  

    > [!NOTE]
    > Los datos de estado de usuario que hacen referencia a los vínculos físicos permanecen en el equipo después de que la secuencia de tareas elimina el sistema operativo anterior. Se trata de los datos que se utilizan para restaurar el estado de usuario cuando se implementa el nuevo sistema operativo.  

## <a name="configure-a-state-migration-point"></a><a name="BKMK_StateMigrationPoint"></a> Configure a state migration point

El punto de migración de estado almacena los datos de estado de usuario que se capturan en un equipo y se restauran en otro. Sin embargo, cuando se captura la configuración de usuario para la implementación de sistema operativo en el mismo equipo, como una implementación en la que se actualice el sistema operativo en el equipo de destino, puede almacenar los datos en el mismo equipo mediante vínculos físicos o en un punto de migración de estado. En algunas implementaciones, al crear el almacén de estado, Configuration Manager crea automáticamente una asociación entre el almacén de estado y el equipo de destino. Puede utilizar los métodos siguientes para configurar un punto de migración de estado para almacenar los datos de estado de usuario:  

- Use el **Asistente para crear servidor de sistema de sitio** para crear un nuevo servidor de sistema de sitio para el punto de migración de estado.  

- Use el **Asistente para agregar roles de sistema de sitio** para agregar un punto de migración de estado a un servidor existente.  

  Al utilizar estos asistentes, deberá proporcionar la siguiente información para el punto de migración de estado:  

- Las carpetas para almacenar los datos de estado de usuario.  

- El número máximo de clientes que pueden almacenar datos en el punto de migración de estado.  

- Seleccione el espacio libre mínimo para que el punto de migración de estado almacene datos de estado de usuario.  

- La directiva de eliminación para el rol. Puede especificar que los datos de estado de usuario se eliminen inmediatamente después de ser restaurados en un equipo o después de un número específico de días tras haber sido restaurados en un equipo.  

- Si el punto de migración de estado responde solo a solicitudes de restauración de datos de estado de usuario. Cuando se habilita esta opción, no se puede utilizar el punto de migración de estado para almacenar datos de estado de usuario.  

  Para obtener más información sobre el punto de migración de estado y las etapas para configurarlo, consulte [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints) (Punto de migración de estado).  

## <a name="create-a-computer-association"></a><a name="BKMK_ComputerAssociation"></a> Create a computer association

Cree una asociación de equipos para definir una relación entre un equipo de origen y un equipo de destino cuando instale un sistema operativo en hardware nuevo y quiera capturar y restaurar la configuración de datos de usuario. El equipo de origen es un equipo existente administrado por Configuration Manager. Cuando se implementa el nuevo sistema operativo en el equipo de destino, el equipo de origen contiene el estado de usuario que se migra al equipo de destino.  

> [!NOTE]  
> No se admite para crear una asociación de equipos entre equipos situados en un sitio primario de Configuration Manager con equipos que se encuentran en un sitio secundario. Las asociaciones de equipos son específicas de un sitio y no se replican.  

### <a name="to-create-a-computer-association"></a>Para crear una asociación de equipo

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

1. En el área de trabajo **Activos y compatibilidad** , haga clic en **Migración de estado de usuario**.  

1. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear asociación de equipo**.  

1. En la pestaña **Asociación de equipo** del cuadro de diálogo **Propiedades de asociación de equipos** , especifique el equipo de origen que tiene el estado de usuario para capturar y el equipo de destino en el que se restaurarán los datos de estado de usuario.  

1. En la pestaña **Cuentas de usuario** , especifique las cuentas de usuario para migrar al equipo de destino. Especifique una de las siguientes opciones:  

    - **Capturar y restaurar todas las cuentas de usuario**: esta configuración captura y restaura todas las cuentas de usuario. Use esta opción para crear varias asociaciones en el mismo equipo de origen.  

    - **Capturar todas las cuentas de usuario y restaurar cuentas especificadas**: Esta configuración captura todas las cuentas de usuario en el equipo de origen y solo restaura las cuentas que se especifiquen en el equipo de destino. Además, puede utilizar esta opción cuando desee crear varias asociaciones con el mismo equipo de origen.  

    - **Capturar y restaurar cuentas de usuario especificadas**: Esta configuración captura y restaura solo las cuentas que se especifiquen. No es posible crear varias asociaciones con el mismo equipo de origen cuando se selecciona esta opción.  

## <a name="restore-user-state-data-when-an-operating-system-deployment-fails"></a><a name="BKMK_MigrationFails"></a> Restaurar datos de estado de usuario si se produce un error de implementación de sistema operativo

Si se produce un error de implementación de sistema operativo, use la característica LoadState de USMT 10.0 para recuperar los datos de estado de usuario que se capturaron durante el proceso de implementación. Se incluyen los datos que se almacenan en un punto de migración de estado o los datos que se guardan localmente en el equipo de destino. Para obtener más información acerca de esta característica de USMT, consulte [Sintaxis de LoadState](/windows/deployment/usmt/usmt-loadstate-syntax).