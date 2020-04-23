---
title: Operaciones de migración
titleSuffix: Configuration Manager
description: Cree y ejecute trabajos para migrar datos y clientes a la rama actual de Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a93269fc50c7bb39cd47f10e448d30742fc8ab22
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704573"
---
# <a name="operations-for-migrating-to-configuration-manager-current-branch"></a>Operaciones para migrar a la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En una migración de Configuration Manager se pueden migrar datos y clientes después de recopilar correctamente datos de un sitio de origen en una jerarquía de origen admitida. Use la información en las secciones siguientes para crear y ejecutar trabajos de migración para migrar datos y clientes, y después complete el proceso de migración.  

-   [Crear y editar trabajos de migración](#Create_Edit_migration_Jobs)  

-   [Ejecutar trabajos de migración](#Run_Migration_Jobs)  

-   [Actualizar o volver a asignar un punto de distribución compartido](#BKMK_ProcUpgrdSS)  

-   [Supervisar la actividad de migración en el área de trabajo de migración](#Monitor_MIgration)  

-   [Migrar clientes](#BKMK_MigrateClients)  

-   [Finalizar la migración](#Complete_Migration)  

##  <a name="create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Crear y editar trabajos de migración  
 Use los procedimientos siguientes para crear trabajos de migración de datos, editar la lista de exclusión para los trabajos de migración basados en recopilación, configurar puntos de distribución compartidos y editar programaciones de trabajos de migración.  

> [!NOTE]  
>  El siguiente procedimiento para crear un trabajo de migración que migre por recopilaciones se aplica solo a jerarquías de origen que ejecutan una versión compatible de Configuration Manager 2007. El tipo de trabajo de migración basado en la recopilación no está disponible cuando se migra desde una jerarquía de orígenes de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Crear un trabajo de migración para migrar por recopilaciones  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración** y después haga clic en **Trabajos de migración**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear trabajo de migración**.  

4.  En la página **General** del Asistente para crear trabajo de migración, configure lo siguiente y después haga clic en **Aceptar**:  

    -   Especifique un nombre para el trabajo de migración.  

    -   En la lista desplegable **Tipo de trabajo** , seleccione **Migración de recopilación**.  

5.  En la página **Seleccionar recopilaciones**, configure lo siguiente y después haga clic en **Siguiente**:  

    -   Seleccione las recopilaciones que desea migrar.  

    -   Si solo quiere migrar recopilaciones y no los objetos asociados con esas recopilaciones, desactive **Migrar objetos asociados a las recopilaciones especificadas**. Si desactiva esta opción, no se migran los objetos asociados en este trabajo, y puede omitir los pasos 6 y 7.  

6.  En la página **Seleccionar objetos**, desactive cualquier tipo de objeto u objetos disponibles específicos que no quiere migrar. De forma predeterminada, se seleccionan todos los tipos de objetos asociados y objetos disponibles. Elija **Siguiente**.  

7.  En la página **Propiedad de contenido**, asigne la propiedad del contenido de cada sitio de origen enumerado a un sitio de la jerarquía de destino y después haga clic en **Siguiente**.  

8.  En la página **Ámbito de seguridad**, seleccione uno o más ámbitos de seguridad de administración basados en roles para asignarlos a los objetos que se migrarán en este trabajo de migración y después haga clic en **Siguiente**.  

9. En la página **Restricción de recopilación**, configure una recopilación de la jerarquía de destino para limitar el ámbito de cada recopilación enumerada y después haga clic en **Siguiente**. Si no hay ninguna recopilación enumerada, haga clic en **Siguiente**.  

10. En la página **Sustitución de código de sitio**, asigne un código de sitio de la jerarquía de destino para reemplazar el código de sitio de Configuration Manager 2007 para cada recopilación presentada y después haga clic en **Siguiente**. Si no hay ninguna recopilación enumerada, haga clic en **Siguiente**.  

11. En la página **Revisar información**, haga clic en **Guardar en archivo** para guardar la información mostrada para verla más tarde. Cuando esté listo para continuar, haga clic en **Siguiente**.  

12. En la página **Configuración**, especifique cuándo debe ejecutarse el trabajo de migración, seleccione las opciones de configuración adicionales que necesite para este trabajo de migración y después haga clic en **Siguiente**.  

13. Confirme la configuración y finalice el asistente.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Crear un trabajo de migración para migrar por objetos  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración** y después haga clic en **Trabajos de migración**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear trabajo de migración**.  

4.  En la página **General** del Asistente para crear trabajo de migración, configure lo siguiente y después haga clic en **Siguiente**:  

    -   Especifique un nombre para el trabajo de migración.  

    -   En la lista desplegable **Tipo de trabajo** , seleccione **Migración de objeto**.  

5.  En la página **Seleccionar objetos** , seleccione los tipos de objeto que desea migrar. De forma predeterminada, se seleccionan todos los objetos disponibles para cada tipo de objeto que seleccione.  

6.  En la página **Propiedad de contenido**, asigne la propiedad del contenido de cada sitio de origen enumerado a un sitio de la jerarquía de destino y después haga clic en **Siguiente**. Si no hay ningún sitio de origen enumerado, haga clic en **Siguiente**.  

7.  En la página **Ámbito de seguridad**, seleccione uno o más ámbitos de seguridad de administración basados en roles para asignarlos a los objetos de este trabajo de migración y después haga clic en **Siguiente**.  

8.  En la página **Revisar información**, haga clic en **Guardar en archivo** para guardar la información mostrada para verla más tarde. Cuando esté listo para continuar, haga clic en **Siguiente**.  

9. En la página **Configuración**, configure cuándo debe ejecutarse el trabajo de migración y seleccione las opciones de configuración adicionales que necesite para este trabajo de migración. Después, haga clic en **Siguiente**.  

10. Confirme la configuración y finalice el asistente.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Crear un trabajo de migración para migrar objetos modificados  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración** y después haga clic en **Trabajos de migración**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear trabajo de migración**.  

4.  En la página **General** del Asistente para crear trabajo de migración, configure lo siguiente y después haga clic en **Siguiente**:  

    -   Especifique un nombre para el trabajo de migración.  

    -   En la lista desplegable **Tipo de trabajo**, seleccione **Objetos modificados después de la migración**.  

5.  En la página **Seleccionar objetos** , seleccione los tipos de objeto que desea migrar. De forma predeterminada, se seleccionan todos los objetos disponibles para cada tipo de objeto que seleccione.  

6.  En la página **Propiedad de contenido**, asigne la propiedad del contenido de cada sitio de origen enumerado a un sitio de la jerarquía de destino y después haga clic en **Siguiente**. Si no hay ningún sitio de origen enumerado, haga clic en **Siguiente**.  

7.  En la página **Ámbito de seguridad**, seleccione uno o más ámbitos de seguridad de administración basados en roles para asignarlos a los objetos de este trabajo de migración y después haga clic en **Siguiente**.  

8.  En la página **Revisar información**, haga clic en **Guardar en archivo** para guardar la información mostrada para verla más tarde. Cuando esté listo para continuar, haga clic en **Siguiente**.  

9. En la página **Configuración**, configure cuándo debe ejecutarse el trabajo de migración y seleccione las opciones de configuración adicionales que necesite para este trabajo de migración. A diferencia de otros tipos de trabajo de migración, este trabajo de migración debe sobrescribir los objetos migrados anteriormente en la base de datos de Configuration Manager. Elija **Siguiente**.  

10. Confirme la configuración y después finalice el asistente.  

###  <a name="modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a> Modificar la lista de exclusión para la migración  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, haga clic en **Migración** para obtener acceso a la lista de exclusión. También puede acceder a la lista de exclusión a través del nodo **Jerarquía de origen** o **Trabajos de migración** .  

3.  En la pestaña **Inicio**, en el grupo **Migración**, haga clic en **Editar lista de exclusión**.  

4.  En el cuadro de diálogo **Editar lista de exclusión**, seleccione el objeto excluido que quiere quitar de la lista de exclusión y después haga clic en **Quitar**.  

5.  Haga clic en **Aceptar** para guardar los cambios y finalizar la edición. Para cancelar los cambios actuales y restaurar todos los objetos que quitó, haga clic en **Cancelar**y después en **No**. De este modo se cancelará la eliminación de los objetos y se cerrará el cuadro de diálogo **Editar la lista de exclusión** .  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Compartir puntos de distribución de la jerarquía de origen  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración**, haga clic en **Jerarquía de origen** y después seleccione el sitio de origen que quiere configurar.  

3.  En la pestaña **Inicio**, en el grupo **Sitio de origen**, haga clic en **Configurar**.  

4.  En el cuadro de diálogo **Credenciales del sitio de origen**, seleccione **Habilitar uso compartido del punto de distribución para el servidor de sitio de origen** y después haga clic en **Aceptar**.  

5.  Cuando termine el proceso de recopilación de datos, haga clic en **Cerrar**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Cambiar la programación de un trabajo de migración  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración** y después haga clic en **Trabajos de migración**.  

3.  Seleccione el trabajo de migración que quiere cambiar. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  En las propiedades del trabajo de migración, haga clic en la pestaña **Configuración**, cambie el tiempo de ejecución para el trabajo de migración y después haga clic en **Aceptar**.  

##  <a name="run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Ejecutar trabajos de migración  
 Use el procedimiento siguiente para ejecutar un trabajo de migración que aún no ha comenzado.  


1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración** y después haga clic en **Trabajos de migración**.  

3.  Seleccione el trabajo de migración que quiere ejecutar. En la pestaña **Inicio**, en el grupo **Trabajo de migración**, haga clic en **Iniciar**.  

4.  Haga clic en **Sí** para iniciar el trabajo de migración.  

##  <a name="upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a> Actualizar o volver a asignar un punto de distribución compartido  
 Puede actualizar un punto de distribución admitido compartido desde un sitio de origen de Configuration Manager 2007 (o bien volver a asignar un punto de distribución admitido compartido desde un sitio de origen de Configuration Manager) para que sea un punto de distribución en la jerarquía de destino.  

> [!IMPORTANT]  
>  Antes de actualizar un punto de distribución de sucursal de Configuration Manager 2007, debe desinstalar el software de cliente de Configuration Manager 2007 del equipo donde se encuentra el punto de distribución de sucursal. Si el software de cliente de Configuration Manager 2007 está instalado cuando intenta actualizar el punto de distribución, la actualización no se puede realizar y el contenido que se implementó previamente en el punto de distribución de sucursal se quita del equipo.  

> [!CAUTION]  
>  Si actualiza o vuelve a asignar un punto de distribución compartido, el rol de sistema de sitio de punto de distribución y el equipo de sistema de sitio se quitan del sitio de origen y se agregan como punto de distribución al sitio en la jerarquía de destino que seleccione.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Actualizar o volver a asignar un punto de distribución compartido  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración**y después seleccione **Jerarquía de orígenes**.  

3.  Seleccione el sitio al que pertenece el punto de distribución que quiere actualizar, haga clic en la pestaña **Puntos de distribución compartidos** y seleccione el punto de distribución elegible que quiere actualizar o volver a asignar.  

4.  En la pestaña **Punto de distribución** del grupo **Punto de distribución**, haga clic en **Reasignar**.  

5.  Especifique la configuración en el Asistente para reasignar puntos de distribución compartidos como si estuviese instalando un punto de distribución nuevo para la jerarquía de destino, con la adición siguiente:  

    -   En la página **Conversión de contenido**, revise las instrucciones sobre el espacio necesario para convertir el contenido existente. Después, en la página **Configuración de unidad** del asistente, compruebe que la unidad del equipo del punto de distribución seleccionado tiene la cantidad de espacio libre en disco que se necesita.  

6.  Confirme la configuración y después finalice el asistente.  

##  <a name="monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Supervisar la actividad de migración en el área de trabajo de migración  
 Use la consola de Configuration Manager para supervisar la migración.  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración** y después haga clic en **Trabajos de migración**.  

3.  Seleccione el trabajo de migración que quiere supervisar.  

4.  Puede ver los detalles y el estado del trabajo de migración seleccionado en las pestañas correspondientes a **Resumen** y **Objetos en el trabajo**.  

##  <a name="migrate-clients"></a><a name="BKMK_MigrateClients"></a> Migrar clientes  
 Después de migrar datos de clientes entre jerarquías, pero antes de finalizar la migración, planee la migración de los clientes a la jerarquía de destino. La migración de clientes entre jerarquías implica la desinstalación del software cliente Configuration Manager de equipos que están asignados a la jerarquía de origen y, después, la desinstalación del software cliente Configuration Manager de la jerarquía de destino. Si instala el cliente desde la jerarquía de destino también puede asignarlo a un sitio primario en esa jerarquía. Para más información sobre cómo migrar clientes, vea [Planear una estrategia de migración de clientes](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="finish-migration"></a><a name="Complete_Migration"></a> Finalizar la migración  
 Use este procedimiento para finalizar la migración desde la jerarquía de origen.  

1.  En la consola de Configuration Manager, seleccione **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Migración**y después seleccione **Jerarquía de orígenes**.  

3.  Para una jerarquía de origen de Configuration Manager 2007, seleccione un sitio de origen que esté en el nivel inferior de la jerarquía de origen. En el caso de una jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, seleccione el sitio de origen disponible.  

4.  En la pestaña **Inicio**, en el grupo **Limpiar**, haga clic en **Detener la recopilación de datos**.  

5.  Haga clic en **Sí** para confirmar la acción.  

6.  Para una jerarquía de origen de Configuration Manager 2007, antes de continuar con el paso siguiente, repita los pasos 3, 4 y 5. Realice estos pasos en cada sitio de la jerarquía, desde la parte inferior de la jerarquía hasta la parte superior. En el caso de una jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, continúe con el paso siguiente.  

7.  En la pestaña **Inicio**, en el grupo **Limpiar**, haga clic en **Limpiar datos de migración**.  

8.  En el cuadro de diálogo **Limpiar datos de migración**, en la lista desplegable **Jerarquía de origen**, seleccione el código de sitio y el servidor de sitio del sitio de nivel superior de la jerarquía de origen y después haga clic en **Aceptar**.  

9. Haga clic en **Sí** para finalizar el proceso de migración para la jerarquía de origen.  
