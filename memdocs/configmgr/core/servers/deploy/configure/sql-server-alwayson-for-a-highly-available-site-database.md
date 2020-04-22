---
title: SQL Server Always On
titleSuffix: Configuration Manager
description: Planeamiento para usar grupos de disponibilidad AlwaysOn de SQL Server con Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9e2e4e85d9fb6a1ab34af8760e0ac61d6e4fab4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700893"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparación para usar grupos de disponibilidad AlwaysOn de SQL Server con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use este artículo para preparar Configuration Manager para usar grupos de disponibilidad AlwaysOn de SQL Server. Esta característica proporciona una solución de alta disponibilidad y recuperación ante desastres para la base de datos.  

Configuration Manager admite el uso de grupos de disponibilidad:

- En sitos primarios y el sitio de administración central.
- De forma local, o en Microsoft Azure.

Al utilizar grupos de disponibilidad en Microsoft Azure, puede aumentar aún más la disponibilidad de la base de datos de sitio mediante *conjuntos de disponibilidad de Azure*. Para más información sobre los conjuntos de disponibilidad de Azure, consulte [Administrar la disponibilidad de las máquinas virtuales](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
> Antes de continuar, familiarícese con la configuración de SQL Server y los grupos de disponibilidad de SQL Server. La siguiente información hace referencia a la biblioteca de documentación y los procedimientos de SQL Server.


## <a name="supported-scenarios"></a>Escenarios admitidos

Los siguientes escenarios son compatibles con el uso de grupos de disponibilidad con Configuration Manager. Para obtener más información y conocer los procedimientos para cada uno de ellos, consulte [Configuración de grupos de disponibilidad AlwaysOn de SQL Server para Configuration Manager](configure-aoag.md).

- [Crear un grupo de disponibilidad para su uso con Configuration Manager](configure-aoag.md#bkmk_create)  
- [Configuración de un sitio para usar el grupo de disponibilidad](configure-aoag.md#bkmk_configure)  
- [Agregar o quitar a miembros de la réplica sincrónica de un grupo de disponibilidad que hospeda una base de datos de sitio](configure-aoag.md#bkmk_sync)  
- [Configuración o recuperación de un sitio a partir de réplicas de confirmación asincrónicas](configure-aoag.md#bkmk_async)  
- [Sacar una base de datos de sitio de un grupo de disponibilidad a una instancia predeterminada o con nombre de un servidor SQL Server independiente](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos se aplican a todos los escenarios. Si hubiera requisitos previos adicionales para un escenario concreto, se detallarán con ese escenario.

### <a name="configuration-manager-accounts-and-permissions"></a>Cuentas y permisos de Configuration Manager

#### <a name="installation-account"></a>Cuenta de instalación

La cuenta que utilice para ejecutar el programa de instalación de Configuration Manager debe cumplir los requisitos siguientes:

- Debe ser miembro del grupo de **administradores** locales en cada equipo que sea miembro del grupo de disponibilidad.
- Debe ser **Administrador del sistema** en cada instancia de SQL Server que hospeda la base de datos de sitio.

#### <a name="site-server-to-replica-member-access"></a>Acceso del miembro del servidor de sitio a la réplica

La cuenta del equipo del servidor del sitio debe formar parte del grupo de **administradores locales** de cada equipo que sea miembro del grupo de disponibilidad.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Version

Cada réplica del grupo de disponibilidad debe ejecutar una versión de SQL Server que sea compatible con su versión de Configuration Manager. Si SQL Server lo admite, distintos nodos del grupo de disponibilidad pueden ejecutar distintas versiones de SQL Server. Para más información, vea [Versiones de SQL Server compatibles con Configuration Manager](../../../plan-design/configs/support-for-sql-server-versions.md).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Edición

Use una edición *Enterprise* de SQL Server.

#### <a name="account"></a>Cuenta

Cada instancia de SQL Server puede ejecutarse en una cuenta de usuario de dominio (**cuenta de servicio**) o a una que no sea de dominio. Cada réplica de un grupo puede tener una configuración diferente.

- Utilice una cuenta con los mínimos permisos posibles. Para obtener más información, consulte [Consideraciones de seguridad para una instalación de SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Para obtener más información sobre la configuración de cuentas de servicio y permisos de SQL Server, consulte [Configurar los permisos y las cuentas de servicio de Windows](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Para usar una cuenta que no es de dominio, debe utilizar certificados. Para obtener más información, consulte [Usar certificados para un extremo de creación de reflejo de la base de datos (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Para más información, vea [Crear un punto de conexión de creación de reflejo de la base de datos para grupos de disponibilidad AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="database"></a>Capa

#### <a name="configure-the-database-on-a-new-replica"></a>Configuración de la base de datos en una nueva réplica

Configure la base de datos de cada réplica con los parámetros siguientes:  

- Habilite la **integración con CLR**:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Para obtener más información, consulte [Introducción a la integración con CLR de SQL Server](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Establezca el **Tamaño de replicación de texto máximo** en `2147483647`:  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Establezca el propietario de la base de datos en *Cuenta SA*. No es necesario habilitar esta cuenta.

- Ponga en **ACTIVADO** el parámetro **DE CONFIANZA**:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Para obtener más información, consulte la [Propiedad de base de datos TRUSTWORTHY](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).

- Habilite **Service Broker**:  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > No se puede habilitar la opción Service Broker en una base de datos que ya forma parte de un grupo de disponibilidad. Tendrá que habilitar esa opción antes de agregarla al grupo de disponibilidad.<!-- SCCMDocs#1432 -->

- Configure la prioridad de Service Broker:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Establezca estas configuraciones solo en una réplica principal. Para configurar una réplica secundaria, provoque primero una conmutación por error de la primaria a la secundaria. Esta acción convierte a la secundaria en la nueva réplica principal.

#### <a name="database-verification-script"></a>Script de verificación de la base de datos

Ejecute el script de SQL siguiente para comprobar las configuraciones de base de datos para las réplicas principal y secundaria. Para solucionar un problema en una réplica secundaria, cambie esa réplica secundaria para que sea la réplica principal.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Configuraciones de grupo de disponibilidad

#### <a name="replica-members"></a>Miembros de réplica

- El grupo de disponibilidad debe tener, al menos, una réplica principal.  

- Use el mismo número y tipo de réplicas en un grupo de disponibilidad que admita la versión de SQL Server.

- Se puede utilizar la réplica de confirmación asincrónica para recuperar una réplica sincrónica. Para obtener más información, vea [Opciones de recuperación de base de datos de sitio](../../manage/recover-sites.md#site-database-recovery-options).  

    > [!Warning]  
    > Configuration Manager no admite la *conmutación por error* para usar la réplica de confirmación asincrónica como la base de datos de sitio. Para obtener más información, consulte [Conmutación por error y modos de conmutación por error (grupos de disponibilidad AlwaysOn)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

Configuration Manager no valida el estado de la réplica de confirmación asincrónica para confirmar que está actualizada. El uso de una réplica de confirmación asincrónica como base de datos de sitio puede poner en riesgo la integridad del sitio y los datos. Por diseño, puede que esta réplica no esté sincronizada. Para más información, vea [Información general de los grupos de disponibilidad AlwaysOn (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Cada miembro de la réplica debe tener las siguiente configuración:

- Usa la *instancia predeterminada* o una *instancia con nombre*  

- La opción **Conexiones del rol principal** está establecida en **Permitir todas las conexiones**  

- La opción **Secundaria legible** está establecida en **Sí**.  

- Está habilitada para la **conmutación por error manual**

    > [!Note]
    > En la versión 1902 y versiones anteriores, debe configurar todos los grupos de disponibilidad en SQL Server para la conmutación por error manual. Esta configuración es necesaria incluso si no hospeda la base de datos del sitio.
    >
    > A partir de la versión 1906, Configuration Manager admite el uso de las réplicas sincrónicas del grupo de disponibilidad cuando se establece en **Conmutación automática por error**. Establezca la **conmutación por error manual** en estos casos:
    >
    > - Cuando se ejecuta el programa de instalación de Configuration Manager para especificar el uso de la base de datos del sitio en el grupo de disponibilidad.  
    > - Instala cualquier actualización en Configuration Manager. (No solo las actualizaciones que se aplican a la base de datos de sitio).  

- Todos los miembros necesitan el mismo [modo de propagación](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).<!-- SCCMDocs-pr#3899 --> La instalación de Configuration Manager incluye una comprobación de requisitos previos para verificar esta configuración al crear una base de datos mediante la instalación o recuperación.

    > [!Note]  
    > Cuando el programa de instalación crea la base de datos y se configura la propagación **automática**, el grupo de disponibilidad debe tener permisos para crear la base de datos. Este requisito se aplica a una nueva base de datos o a una recuperación. Para más información, vea [Propagación automática para la réplica secundaria](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security).<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Ubicación del miembro de réplica

Hospede todas las réplicas en un grupo de disponibilidad en el entorno local o bien en Microsoft Azure. No se admite un escenario en el que un grupo incluya un miembro en el entorno local y otro en Azure.

El programa de instalación de Configuration Manager necesita conectarse a cada réplica. Si configura un grupo de disponibilidad en Azure y el grupo está detrás de un equilibrador de carga interno o externo, abra estos puertos predeterminados:

- Asignador de extremos de RPC: **TCP 135**

- SQL Server Service Broker: **TCP 4022**  

- SQL a través de TCP: **TCP 1433**

Una vez completado el programa de instalación de Configuration Manager, los siguientes puertos deben mantenerse abiertos para Configuration Manager:  

- SQL Server Service Broker: **TCP 4022**  

- SQL a través de TCP: **TCP 1433**  

Puede usar puertos personalizados para estas configuraciones. Use los mismos puertos personalizados por el punto de conexión y en todas las réplicas del grupo de disponibilidad.

#### <a name="listener"></a>Agente de escucha

El grupo de disponibilidad debe tener al menos un *agente de escucha de grupo de disponibilidad*. Al configurar Configuration Manager para usar la base de datos de sitio en el grupo de disponibilidad, usa el nombre virtual de este agente de escucha. Aunque un grupo de disponibilidad puede contener varios agentes de escucha, Configuration Manager solo puede usar uno. Para obtener más información, consulte [Crear o configurar un agente de escucha del grupo de disponibilidad (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Rutas de acceso de archivo

Al ejecutar el programa de instalación de Configuration Manager para configurar un sitio para que use la base de datos en un grupo de disponibilidad, cada servidor de réplica secundario debe tener una ruta de acceso de archivo de SQL Server idéntica a la ruta de acceso para los archivos de base de datos del sitio que se encuentran en la réplica principal actual. Si no existe una ruta de acceso idéntica, se producirá un error en el programa de instalación al agregar la instancia para el grupo de disponibilidad como nueva ubicación de la base de datos del sitio.  

La cuenta de servicio de SQL Server local debe tener permiso de **Control total** para esta carpeta.

Los servidores de réplica secundaria solo requieren esta ruta de acceso de archivo mientras utilizan el programa de instalación de Configuration Manager para especificar la instancia de base de datos del grupo de disponibilidad. Una vez que completa la configuración de la base de datos de sitio en el grupo de disponibilidad, puede eliminar la ruta de acceso de los servidores de réplicas secundarias sin usar.

Por ejemplo, considere el siguiente escenario:

- Crea un grupo de disponibilidad que utiliza tres servidores SQL Server.  

- El servidor de réplica principal es una nueva instalación de SQL Server 2014. De forma predeterminada, almacena los archivos .MDF y .LDF de la base de datos en `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- Ha actualizado los servidores de réplica secundaria a SQL Server 2014 desde versiones anteriores. Con la actualización, estos servidores mantienen la ruta de acceso a los archivos original para almacenar los archivos de base de datos: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.  

- Antes de mover la base de datos de sitio a este grupo de disponibilidad, cree la siguiente ruta de acceso a los archivos en cada servidor de réplica secundaria: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. Esta ruta de acceso es un duplicado de la ruta de acceso en uso en la réplica principal, incluso si las réplicas secundarias no utilizan esta ubicación de archivo.  

- A continuación, concede a la cuenta de servicio de SQL Server de cada réplica secundaria control total de acceso a la ubicación del archivo recién creada en el servidor.  

- Ahora puede ejecutar correctamente el programa de instalación de Configuration Manager para configurar el sitio para que use la base de datos del sitio del grupo de disponibilidad.  

#### <a name="multi-subnet-failover"></a>Conmutación por error de múltiples subredes

<!-- SCCMDocs-pr#3734 -->
A partir de la versión 1906, puede habilitar la [palabra clave de la cadena de conexión MultiSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) en SQL Server. También debe agregar manualmente los siguientes valores al registro de Windows en el servidor del sitio:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> El uso de la [alta disponibilidad del servidor del sitio](site-server-high-availability.md) y SQL Server Always On con conmutación por error de múltiples subredes no proporciona todas las funcionalidades de la conmutación automática por error para los escenarios de recuperación ante desastres.

Si necesita crear un grupo de disponibilidad con un miembro en una ubicación remota, priorice en función de la latencia de red más baja. La alta latencia de red puede provocar errores de replicación.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos

Las siguientes limitaciones se aplican a todos los escenarios.

### <a name="unsupported-sql-server-options-and-configurations"></a>Opciones y configuraciones de SQL Server que no son compatibles

- **Grupos de disponibilidad básica**: introducidos con la edición SQL Server 2016 Standard, los grupos de disponibilidad básica no admiten el acceso de lectura a réplicas secundarias. La configuración requiere este acceso. Para obtener más información, consulte [Grupos de disponibilidad básica (grupos de disponibilidad AlwaysOn)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Instancia del clúster de conmutación por error**: las instancias del clúster de conmutación por error no son compatibles con las réplicas usadas junto con Configuration Manager. Para obtener más información, consulte [Instancias de clúster de conmutación por error de AlwaysOn (SQL Server)](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: En la versión 1902 y versiones anteriores, no se permite usar un grupo de disponibilidad con Configuration Manager en una configuración de varias subredes. Tampoco puede usar la cadena de conexión de palabra clave [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover).

    Para admitir esta configuración, actualice Configuration Manager a la versión 1906 o una versión posterior. Para más información, consulte el requisito previo de [conmutación por error de múltiples subredes](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover).

### <a name="sql-servers-that-host-additional-availability-groups"></a>Servidores SQL Server que hospedan grupos de disponibilidad adicionales

<!--SCCMDocs issue 649-->
Cuando en SQL Server se hospedan uno o varios grupos de disponibilidad además del grupo que se usa para Configuration Manager, necesita una configuración específica en el momento de ejecutar el programa de instalación de Configuration Manager. Esta configuración también se necesita para instalar una actualización para Configuration Manager. Cada réplica de cada grupo de disponibilidad debe tener las siguientes configuraciones:

- Conmutación por error manual  
- Permitir cualquier conexión de solo lectura  

> [!Note]
> En la versión 1902 y versiones anteriores, debe configurar todos los grupos de disponibilidad en SQL Server para la conmutación por error manual. Esta configuración es necesaria incluso si no hospeda la base de datos del sitio.
>
> A partir de la versión 1906, Configuration Manager admite el uso de las réplicas sincrónicas del grupo de disponibilidad cuando se establece en **Conmutación automática por error**. Establezca la **conmutación por error manual** en estos casos:
>
> - Cuando se ejecuta el programa de instalación de Configuration Manager para especificar el uso de la base de datos del sitio en el grupo de disponibilidad.  
> - Instala cualquier actualización en Configuration Manager. (No solo las actualizaciones que se aplican a la base de datos de sitio).  

### <a name="unsupported-database-use"></a>Uso de base de datos no admitido

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager admite solo la base de datos de sitio en un grupo de disponibilidad

Configuration Manager no admite las bases de datos siguientes en un grupo de disponibilidad de SQL Server Always On:  

- Base de datos de informes  
- Base de datos WSUS  

#### <a name="pre-existing-database"></a>Base de datos existente previamente

no puede usar la nueva base de datos que ha creado en la réplica. Cuando configure un grupo de disponibilidad, restaure una copia de una base de datos de Configuration Manager existente en la réplica principal.  

#### <a name="distributed-views"></a>Vistas distribuidas

<!-- SCCMDocs-pr#3792 -->
En la versión 1902 y versiones anteriores, si hospeda la base de datos del sitio en un grupo de disponibilidad de SQL Server Always On, no puede habilitar las [vistas distribuidas](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) para la replicación de base de datos. Para admitir esta configuración, actualice a la versión 1906 o una versión posterior.


### <a name="setup-errors-in-configmgrsetuplog"></a>Errores de instalación en ConfigMgrSetup.log

Al ejecutar el programa de instalación de Configuration Manager para mover una base de datos de sitio a un grupo de disponibilidad, este intenta procesar los roles de la base de datos en las réplicas secundarias del grupo de disponibilidad. El archivo **ConfigMgrSetup.log** muestra el error siguiente:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Es seguro omitir estos errores.

### <a name="site-expansion"></a>Expansión de sitios

<!--SCCMDocs issue 568-->
Si configura la base de datos de sitio para que un sitio primario independiente use Always On de SQL, no puede expandir el sitio para que incluya un sitio de administración central. Si intenta este proceso, se produce un error. Para expandir el sitio, quite temporalmente la base de datos del sitio principal desde el grupo de disponibilidad.

No es necesario realizar ningún cambio en la configuración al agregar un sitio secundario.


## <a name="changes-for-site-backup"></a>Cambios para la copia de seguridad del sitio

### <a name="backup-database-files"></a>Copia de seguridad de archivos de base de datos
  
Cuando una base de datos de sitio utiliza un grupo de disponibilidad, ejecute la tarea de mantenimiento del **Servidor del sitio de copia de seguridad** integrada para realizar una copia de seguridad de los archivos y las configuraciones comunes de Configuration Manager. No use los archivos .MDF o .LDF creados por esa copia de seguridad. Realice en su lugar realizar copias de seguridad directas de los archivos de la base de datos mediante SQL Server.

### <a name="transaction-log"></a>Registro de transacciones  

Configure el modelo de recuperación de la base de datos de sitio en **Completo**. Esta configuración es un requisito para el uso de Configuration Manager en un grupo de disponibilidad. Planee la supervisión y el mantenimiento del tamaño del registro de transacciones de la base de datos de sitio. En el modelo de recuperación completa, las transacciones no están protegidas hasta que se realiza una copia de seguridad completa de la base de datos o el registro de transacciones. Para obtener más información, consulte [Realizar copias de seguridad y restaurar bases de datos de SQL Server](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).


## <a name="changes-for-site-recovery"></a>Cambios para la recuperación del sitio

Utilice la opción de recuperación del sitio **Omitir recuperación de base de datos (use esta opción si la base de datos de sitio no se vio afectada)** si al menos un nodo del grupo de disponibilidad sigue funcionando.

A partir de la versión 1906, la recuperación del sitio puede volver a crear la base de datos en un grupo AlwaysOn de SQL. Este proceso funciona tanto con la inicialización manual como con la automática.<!-- SCCMDocs-pr#3846 -->

En la versión 1902 o en versiones anteriores, cuando se pierden todos los nodos de un grupo de disponibilidad, debe volver a crear el grupo de disponibilidad para recuperar el sitio. Configuration Manager no puede volver a generar o restaurar el nodo de disponibilidad. Vuelva a crear el grupo, restaure la copia de seguridad y vuelva a configurar SQL. Luego, use la opción de recuperación del sitio **Omitir recuperación de base de datos (use esta opción si la base de datos del sitio no se vio afectada)** .

Para obtener más información, vea [Copia de seguridad y recuperación](../../manage/backup-and-recovery.md).


## <a name="changes-for-reporting"></a>Cambios para la notificación

### <a name="install-the-reporting-service-point"></a>Instalación del punto de servicios de informes

El punto de servicios de informes no admite el uso del nombre virtual del agente de escucha del grupo de disponibilidad. Tampoco admite el hospedaje de su base de datos en un grupo de disponibilidad Always On de SQL Server.  

- De forma predeterminada, la instalación del punto de servicios de informes establece el **Nombre de servidor de base de datos de sitio** en el nombre virtual que se especifica como el agente de escucha. Cambie esta opción para especificar un nombre de equipo y una instancia de una réplica del grupo de disponibilidad.  

- Para descargar los informes y para aumentar la disponibilidad cuando un nodo de la réplica está sin conexión, considere la posibilidad de instalar puntos de servicios de informes adicionales en cada nodo de réplica. Luego, configure cada punto de servicios de informes para que use su propio nombre de equipo. Cuando se instala un punto de servicios de informes en cada réplica del grupo de disponibilidad, los informes siempre pueden conectarse a un servidor de punto de informes activo.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Cambio del punto de servicios de informes que utiliza la consola

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y seleccione el nodo **Informes**.

1. En la cinta de opciones, seleccione **Opciones de informes**.  

1. En el cuadro de diálogo Opciones de informes, seleccione el punto de servicios de informes que desea utilizar.  


## <a name="next-steps"></a>Pasos siguientes

En este artículo se describen los requisitos previos, las limitaciones y los cambios en las tareas comunes que Configuration Manager requiere cuando se usan grupos de disponibilidad. Para conocer los procedimientos para instalar y configurar el sitio para usar grupos de disponibilidad, consulte [Configuración de grupos de disponibilidad](configure-aoag.md).
