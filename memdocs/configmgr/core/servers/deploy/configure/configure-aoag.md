---
title: Configuración de los grupos de disponibilidad
titleSuffix: Configuration Manager
description: Configuración y administración de grupos de disponibilidad Always On de SQL Server con Configuration Manager
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12753b3800b3b304bd13c992b57d22bf9e1bfad8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704803"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configuración de grupos de disponibilidad AlwaysOn de SQL Server para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la información de este artículo para configurar y administrar los grupos de disponibilidad que use con Configuration Manager.

Antes de empezar:  

- Familiarícese con la información de [Preparación para usar grupos de disponibilidad AlwaysOn de SQL Server con Configuration Manager](sql-server-alwayson-for-a-highly-available-site-database.md).
- Familiarícese con la documentación de SQL Server que explica el uso de grupos de disponibilidad y los procedimientos relacionados. Esta información es necesaria para completar los siguientes escenarios.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> Creación y configuración de un grupo de disponibilidad

Utilice el procedimiento siguiente para crear un grupo de disponibilidad y, a continuación, mover una copia de la base de datos de sitio a ese grupo de disponibilidad.

1. Use el siguiente comando para detener el sitio de Configuration Manager:

    `preinst.exe /stopsite`

    Para más información, vea [Herramienta de mantenimiento de jerarquía](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Cambie el modelo de copia de seguridad de la base de datos de sitio de **SENCILLA** a **COMPLETA**:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Los grupos de disponibilidad solo admiten el modelo de copia de seguridad COMPLETA. Para más información, vea [Ver o cambiar el modelo de recuperación de una base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Use SQL Server para crear una copia de seguridad completa de la base de datos de sitio. Elija una de las siguientes opciones:

    - **Será miembro del grupo de disponibilidad**: Si utiliza este servidor como miembro de la réplica principal inicial del grupo de disponibilidad, no es necesario restaurar una copia de la base de datos del sitio en este u otro servidor del grupo. La base de datos ya se encuentra en la réplica principal. SQL Server replica la base de datos en las réplicas secundarias en un paso posterior.  

    - **No será miembro del grupo de disponibilidad**: Restaure una copia de la base de datos de sitio en el servidor que hospedará la réplica principal del grupo.

    Para más información, vea los siguientes artículos en la documentación de SQL Server:

    - [Crear una copia de seguridad completa de base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Restauración de una copia de seguridad de la base de datos con SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Si planea pasar de un grupo de disponibilidad a una base de datos independiente en una réplica existente, primero quite la base de datos del grupo de disponibilidad.

4. En el servidor que hospedará la réplica principal inicial del grupo, use el [Asistente para nuevo grupo de disponibilidad](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) para crear el grupo de disponibilidad. En el asistente:

    - En la página **Seleccionar base de datos**, elija la base de datos para el sitio de Configuration Manager.  

    - En la página **Especificar réplicas** , configure lo siguiente:

        - **Réplicas:** especifique los servidores que hospedarán las réplicas secundarias.

        - **Agente de escucha**: Especifique el **Nombre DNS del agente de escucha** como un nombre DNS completo; por ejemplo, `<listener_server>.fabrikam.com`. Al configurar Configuration Manager para usar la base de datos en el grupo de disponibilidad, se usa este nombre.

    - En la página **Seleccionar sincronización de datos iniciales** seleccione **Completa**. Una vez que el asistente cree el grupo de disponibilidad, hace una copia de seguridad del registro de transacciones y la base de datos principal. Después, los restaurará en cada servidor que hospede una réplica secundaria

        > [!Note]  
        > Si no usa este paso, restaure una copia de la base de datos del sitio en cada servidor que hospeda una réplica secundaria. Después, combine manualmente esa base de datos con el grupo.

5. Compruebe la configuración en cada réplica:

    1. Asegúrese de que la cuenta del equipo del servidor del sitio forme parte del grupo de **administradores locales** de cada equipo que sea miembro del grupo de disponibilidad.  

    2. Ejecute el [script de verificación](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites) para confirmar que la base de datos de sitio de cada réplica está configurada correctamente.

    3. Si hay que ajustar parámetros en las réplicas secundarias, antes de continuar, debe conmutar por error manualmente la réplica principal en la secundaria. porque solo puede configurar la base de datos de una réplica principal. Para más información, vea [Realización de una conmutación por error manual planeada de un grupo de disponibilidad (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) en la documentación de SQL Server.

6. Una vez que todas las réplicas cumplan los requisitos, el grupo de disponibilidad estará listo para su uso con Configuration Manager.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> Configuración de un sitio para usar el grupo de disponibilidad

Después de [crear y configurar el grupo de disponibilidad](#bkmk_create), utilice el mantenimiento del sitio de Configuration Manager para configurar el sitio de manera que utilice la base de datos que el grupo de disponibilidad hospeda.

No se admite la instalación de un sitio nuevo con su base de datos en un grupo de disponibilidad. Por ejemplo, si usa los medios de la base de referencia, instale el sitio mediante una sola instancia de SQL Server. Una vez instalado el sitio, mueva la base de datos del sitio al grupo de disponibilidad.

1. Ejecute el **programa de instalación de Configuration Manager**: `\BIN\X64\setup.exe` desde la carpeta de instalación del sitio de Configuration Manager.

2. En la página **Introducción**, seleccione **Realizar mantenimiento de sitio o restablecer este sitio** y, después, seleccione **Siguiente**.

3. Seleccione **Modificar configuración de SQL Server** y, después, haga clic en **Siguiente**.

4. Vuelva a configurar lo siguiente en la base de datos del sitio:

    - **Nombre de SQL Server**: escriba el nombre virtual del *agente de escucha* de grupo de disponibilidad. Configuró el agente de escucha al crear el grupo de disponibilidad. El nombre virtual debe ser un nombre DNS completo, como `<Listener_Server>.fabrikam.com`.  

    - **Instancia:** para especificar la instancia predeterminada para el *agente de escucha* del grupo de disponibilidad, este valor debe estar en blanco. Si la base de datos del sitio actual se ejecuta en una instancia con nombre, borre la instancia con nombre actual.

    - **Base de datos:** deje el nombre tal y como aparece. Este es el nombre de la base de datos del sitio actual.

5. Después de proporcionar la información de la nueva ubicación de la base de datos, complete el programa de instalación con los procesos y las configuraciones habituales.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> Miembros de la réplica sincrónica  

Si la base de datos de sitio está hospedada en un grupo de disponibilidad, utilice los procedimientos siguientes para agregar o quitar miembros de la réplica sincrónica. Para más información sobre el tipo y el número de réplicas admitidos, vea [Configuraciones de grupo de disponibilidad](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations).

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a> Adición de un nuevo miembro de réplica sincrónica

<!--3127336-->
A partir de la versión 1906, ejecute el programa de instalación de Configuration Manager para agregar un nuevo miembro de réplica sincrónica.

1. Agregue una réplica secundaria con los procedimientos de SQL Server.

    1. [Agregue una réplica secundaria a un grupo de disponibilidad Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. Vea el estado en SQL Management Studio. Espere a que el grupo de disponibilidad vuelva al estado completo.

1. Ejecute el programa de instalación de Configuration Manager y seleccione la opción para modificar el sitio.

1. Especifique el nombre de la escucha de grupo de disponibilidad como nombre de la base de datos. Si el cliente de escucha usa un puerto de red no estándar, especifíquelo también. Esta acción hace que el programa de instalación se asegure de que todos los nodos están configurados correctamente. También inicia un proceso de recuperación de la base de datos.

El programa de instalación de Configuration Manager usa la operación de movimiento de la base de datos SQL y se asegura de que los nodos están configurados correctamente.

Para más información sobre cómo realizar este proceso manualmente en la versión 1902 o versiones anteriores, vea [ConfigMgr 1702: agregar un nodo nuevo (réplica secundaria) a un grupo de disponibilidad AlwaysOn existente de SQL](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960).

### <a name="remove-a-replica-member"></a>Eliminación de un miembro de la réplica

A partir de la versión 1906, puede usar el programa de instalación de Configuration Manager para quitar un miembro de la réplica. Use el mismo procedimiento para [agregar un nuevo miembro de réplica sincrónica](#bkmk_sync-add).

Para más información sobre cómo realizar este proceso manualmente en la versión 1902 o versiones anteriores, vea [Quitar una réplica secundaria de un grupo de disponibilidad](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server).  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> Réplicas asincrónicas

Puede usar una réplica asincrónica en el grupo de disponibilidad que use con Configuration Manager. No es necesario ejecutar los scripts de configuración necesarios para configurar una réplica sincrónica, ya que no se admite una réplica asincrónica para la base de datos del sitio.

### <a name="configure-an-asynchronous-commit-replica"></a>Configuración de una réplica de confirmación asincrónica

Para más información, vea [Adición de una réplica secundaria a un grupo de disponibilidad Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Uso de la réplica asincrónica para la recuperación del sitio

Use la réplica asincrónica para recuperar la base de datos del sitio.

1. Detenga el sitio primario activo para evitar que se realicen escrituras adicionales en la base de datos del sitio. Para detener el sitio, use la [herramienta de mantenimiento de jerarquías](../../manage/hierarchy-maintenance-tool-preinst.exe.md): `preinst.exe /stopsite`

1. Una vez detenido el sitio, use una réplica asincrónica en lugar de una [base de datos recuperada manualmente](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a> Detención del uso de un grupo de disponibilidad

Utilice el procedimiento siguiente cuando ya no desee hospedar la base de datos de sitio en un grupo de disponibilidad. Con este proceso, moverá la base de datos de sitio de nuevo a una sola instancia de SQL Server.

1. Para detener el sitio de Configuration Manager, use el siguiente comando: `preinst.exe /stopsite`. Para más información, vea [Herramienta de mantenimiento de jerarquía](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Use SQL Server para crear una copia de seguridad completa de la base de datos de sitio desde la réplica principal. Para más información, vea [Crear una copia de seguridad completa de base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. Utilice SQL Server para restaurar la copia de seguridad de la base de datos de sitio en el servidor que hospedará la base de datos de sitio. Para más información, vea [Restauración de la copia de seguridad de una base de datos con SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > Si el servidor de la réplica principal del grupo de disponibilidad hospedará la única instancia de la base de datos del sitio, omita este paso.

4. En el servidor que hospedará la base de datos del sitio, cambie el modelo de copia de seguridad de la base de datos del sitio de **COMPLETA** a **SENCILLA**. Para más información, vea [Ver o cambiar el modelo de recuperación de una base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. Ejecute el **programa de instalación de Configuration Manager**: `\BIN\X64\setup.exe` desde la carpeta de instalación del sitio de Configuration Manager.

6. En la página **Introducción**, seleccione **Realizar mantenimiento de sitio o restablecer este sitio** y, después, seleccione **Siguiente**.  

7. Seleccione **Modificar configuración de SQL Server** y, después, haga clic en **Siguiente**.  

8. Vuelva a configurar lo siguiente en la base de datos del sitio:

    - **Nombre de SQL Server:** escriba el nombre del servidor que hospeda ahora la base de datos de sitio.

    - **Instancia:** especifique la instancia con nombre que hospeda la base de datos del sitio. Si la base de datos se encuentra en la instancia predeterminada, deje este campo en blanco.

    - **Base de datos:** deje el nombre tal y como aparece. Este es el nombre de la base de datos del sitio actual.

9. Después de proporcionar la información de la nueva ubicación de la base de datos, complete el programa de instalación con los procesos y las configuraciones habituales. Cuando finaliza la instalación, el sitio se reinicia y comienza a utilizar la nueva ubicación de la base de datos.

10. Para limpiar los servidores que eran miembros del grupo de disponibilidad, siga las instrucciones de [Quitar un grupo de disponibilidad (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server).
