---
title: Recuperación del sitio
titleSuffix: Configuration Manager
description: Obtenga información para recuperar los sitios en Configuration Manager.
ms.date: 06/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e71baef06349a00d49bc7fdc799d078c29939d8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699524"
---
# <a name="recover-a-configuration-manager-site"></a>Recuperar un sitio de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Ejecute una recuperación de sitio de Configuration Manager después de que se produzca un error en un sitio o se pierdan datos de la base de datos de sitio. Reparar y volver a sincronizar datos son las tareas principales de una recuperación de sitio y son necesarias para evitar la interrupción de las operaciones.

Las secciones de este artículo pueden ayudarle a recuperar un sitio de Configuration Manager. Para crear una copia de seguridad, consulte [Copia de seguridad y recuperación](backup-and-recovery.md).

## <a name="considerations-before-recovering-a-site"></a>Consideraciones antes de recuperar un sitio

> [!Important]  
> Esta información se aplica únicamente a escenarios de recuperación del sitio. Si está actualizando la infraestructura local y no recuperando activamente un sitio erróneo, lea la información de los artículos siguientes:
>
> - [Actualizar la infraestructura local](upgrade-on-premises-infrastructure.md)
> - [Modificar la infraestructura](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>Preparación del hardware del servidor

<!-- 2841893 -->

Asegúrese de que las configuraciones existentes no estén presentes en el servidor de sitio. Cualquier configuración anterior puede producir conflictos durante el proceso de recuperación del sitio. Elija una de las opciones siguientes para el hardware del servidor:

- Use un nuevo servidor que cumpla los requisitos generales y de recuperación.

- Formatee los discos y reinstale el sistema operativo en el servidor existente. Asegúrese de que cumple los requisitos generales y de recuperación.

- Reutilice un servidor existente que haya limpiado.

Use uno de los procedimientos siguientes para limpiar un servidor existente:

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>Limpieza de un servidor existente solo para la recuperación del servidor de sitio

1. Elimine las claves de Registro de SMS: `HKLM\Software\Microsoft\SMS`
2. Elimine todas las entradas del Registro que empiecen por `SMS` desde `HKLM\System\CurrentControlSet\Services`. Por ejemplo:
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. Desinstale la consola de Configuration Manager.
4. Reinicie el servidor.
5. Confirme que se han eliminado todas las claves del Registro anteriores.

El servidor ya está listo para el procedimiento de restauración de Configuration Manager.

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>Limpieza de un servidor existente solo para la recuperación de la base de datos del sitio

1. Haga una copia de seguridad de la base de datos del sitio. También puede hacer una copia de seguridad de las demás bases de datos auxiliares, como WSUS.
2. Asegúrese de anotar el nombre de la instancia y el nombre del servidor de SQL.
3. Elimine manualmente la base de datos del sitio desde SQL Server.
4. Reinicie el servidor SQL Server.

El servidor ya está listo para el procedimiento de restauración de Configuration Manager.

#### <a name="clean-an-existing-server-for-full-recovery"></a>Limpieza de un servidor existente para la recuperación completa

1. Haga una copia de seguridad de la base de datos del sitio. También puede hacer una copia de seguridad de las demás bases de datos auxiliares, como WSUS.
2. Haga una copia de la biblioteca de contenido.
3. Elimine manualmente la base de datos del sitio desde SQL Server.
4. Desinstale el sitio de Configuration Manager.
5. Elimine manualmente la carpeta de instalación de Configuration Manager y las demás carpetas de Configuration Manager.
6. Reinicie el servidor.
7. Restaure la biblioteca de contenido y otras bases de datos, como WSUS.

El servidor ya está listo para el procedimiento de restauración de Configuration Manager.

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>Uso de una versión compatible y la misma edición de SQL Server

<!-- SCCMDocs#751 -->

Si es posible, use la misma versión de SQL Server. Sin embargo, es posible restaurar una base de datos a una versión más reciente.

No cambie la edición de SQL Server. No se admite la restauración de una base de datos de sitio de Standard Edition a Enterprise Edition.

Otros requisitos de configuración de SQL Server:

- SQL Server no puede estar establecido en **modo de usuario único**.
- Asegúrese de que los archivos MDF y LDF sean válidos. Al recuperar un sitio, no se realiza ninguna comprobación del estado de los archivos.  

### <a name="sql-server-always-on-availability-groups"></a>Grupos de disponibilidad Always On de SQL Server

Si usa grupos de disponibilidad Always On de SQL Server para hospedar la base de datos de sitio, modifique los planes de recuperación como se indica en [Prepararse para usar SQL Server Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery).

### <a name="database-replicas"></a>Réplicas de base de datos

Después de restaurar una base de datos de sitio que haya configurado para réplicas de base de datos, vuelva a configurar cada réplica. Para poder usar las réplicas de base de datos, vuelva a crear las publicaciones y las suscripciones.

## <a name="determine-your-recovery-options"></a>Determinar las opciones de recuperación

Debe tener en cuenta dos áreas principales para la recuperación del sitio de administración central y del servidor de sitio primario de Configuration Manager: el **servidor de sitio** y la **base de datos de sitio**.
Las secciones siguientes pueden ayudarle a seleccionar las mejores opciones para el escenario de recuperación.

> [!NOTE]  
> Cuando el programa de instalación de Configuration Manager detecta que hay un sitio en el servidor, puede iniciar una recuperación de sitio, pero las opciones de recuperación del servidor de sitio son limitadas. Por ejemplo, si ejecuta el programa de instalación en un servidor de sitio existente, al elegir la recuperación podrá recuperar el servidor de base de datos de sitio, pero la opción de recuperación del servidor de sitio estará deshabilitada.

### <a name="site-server-recovery-options"></a>Opciones de recuperación de servidor de sitio

Inicie el programa de instalación de Configuration Manager a partir de una copia de la carpeta **CD.Latest** creada fuera de la carpeta de instalación de Configuration Manager.  

- Si ejecuta el programa de instalación desde el menú **Inicio** del servidor de sitio, la opción **Recuperar un sitio** no está disponible.  

- Si ha instalado alguna actualización desde la consola de Configuration Manager antes de hacer la copia de seguridad, no puede reinstalar el sitio mediante el programa de instalación desde las siguientes ubicaciones:

  - Medios de instalación
  - Ruta de instalación de Configuration Manager

A continuación, seleccione la opción **Recuperar un sitio** . Cuenta con las siguientes opciones de recuperación para el servidor de sitio con errores:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Recuperar el servidor de sitio mediante una copia de seguridad existente

Use esta opción si tiene una copia de seguridad de Configuration Manager del servidor de sitio anterior al error del sitio. El sitio crea esta copia de seguridad como parte de la tarea de mantenimiento **Copia de seguridad del servidor del sitio**. El sitio se vuelve a instalar y se configura en función del sitio cuya copia de seguridad se había realizado.  

#### <a name="reinstall-the-site-server"></a>Reinstalar el servidor de sitio

Use esta opción si no tiene una copia de seguridad del servidor de sitio. Se vuelve a instalar el servidor de sitio y debe especificar la configuración del sitio tal como lo haría durante una instalación inicial.  

- Use el mismo código de sitio y el mismo nombre de base de datos de sitio que cuando se instaló por primera vez el sitio con errores.  

- Puede volver a instalar el sitio en un nuevo equipo que ejecute una nueva versión del sistema operativo.  

- El servidor debe usar el mismo nombre de host y el mismo nombre de dominio completo (FQDN) que el servidor de sitio original.

### <a name="site-database-recovery-options"></a>Opciones de recuperación de base de datos de sitio

Cuando se ejecuta el programa de instalación de Configuration Manager, existen las siguientes opciones de recuperación de la base de datos de sitio:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Recuperar la base de datos de sitio con un conjunto de copia de seguridad

Use esta opción si tiene una copia de seguridad de Configuration Manager de la base de datos de sitio anterior al error de la base de datos. El sitio crea esta copia de seguridad como parte de la tarea de mantenimiento **Copia de seguridad del servidor del sitio**. En una jerarquía, al restaurar un sitio primario, el proceso de recuperación recupera del sitio de administración central los cambios realizados en la base de datos de sitio después de la última copia de seguridad. Al restaurar el sitio de administración central, el proceso de recuperación recupera estos cambios desde un sitio primario de referencia. Si recupera la base de datos de sitio de un sitio primario independiente, pierde los cambios del sitio desde la última copia de seguridad.  

Cuando se recupera la base de datos de un sitio de una jerarquía, el comportamiento de recuperación es diferente para un sitio de administración central y un sitio primario. El comportamiento también es diferente si la última copia de seguridad está dentro o fuera del período de retención de seguimiento de cambios de SQL Server. Para obtener más información, vea la sección [Escenarios de recuperación de base de datos de sitio](#site-database-recovery-scenarios) de este artículo.  

> [!NOTE]  
> Si selecciona restaurar la base de datos de sitio mediante un conjunto de copia de seguridad, pero la base de datos de sitio ya existe, se produce un error en la recuperación.  

#### <a name="create-a-new-database-for-this-site"></a>Crear una nueva base de datos para este sitio

Use esta opción si no tiene una copia de seguridad de la base de datos de sitio. En una jerarquía, el proceso de recuperación crea una nueva base de datos de sitio. Al restaurar un sitio primario secundario, recupera los datos al replicar desde el sitio de administración central. Al restaurar el sitio de administración central, replica los datos desde un sitio primario de referencia. Esta opción no está disponible cuando se recupera un sitio primario independiente o un sitio de administración central que no tiene sitios primarios.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Usar una base de datos de sitio que se ha recuperado manualmente

Use esta opción si ya ha recuperado la base de datos de sitio de Configuration Manager, pero tiene que completar el proceso de recuperación.  

- Configuration Manager puede recuperar la base de datos de sitio desde cualquiera de los siguientes procesos:  

  - La tarea de mantenimiento de copia de seguridad de Configuration Manager  
  - Una copia de seguridad de base de datos de sitio con Data Protection Manager (DPM)  
  - Otro proceso de copia de seguridad  

    Después de restaurar la base de datos de sitio con un método ajeno a Configuration Manager, ejecute el programa de instalación y seleccione esta opción para completar la recuperación de la base de datos de sitio.  

    > [!NOTE]  
    > Si usa DPM para realizar la copia de seguridad de la base de datos del sitio, emplee los procedimientos de DPM para restaurar la base de datos del sitio en una ubicación determinada antes de continuar con el proceso de restauración en Configuration Manager. Para obtener más información sobre DPM, vea la biblioteca de documentación de [Data Protection Manager](/system-center/dpm).  

- En una jerarquía, al recuperar una base de datos de sitio primario, el proceso de recuperación recupera del sitio de administración central los cambios realizados en la base de datos de sitio después de la última copia de seguridad. Al restaurar el sitio de administración central, el proceso de recuperación recupera estos cambios desde un sitio primario de referencia. Si recupera la base de datos de sitio de un sitio primario independiente, pierde los cambios del sitio desde la última copia de seguridad.  

#### <a name="skip-database-recovery"></a>Omitir recuperación de base de datos

Use esta opción si no se ha producido ninguna pérdida de datos en el servidor de base de datos de sitio de Configuration Manager. Esta opción solo es válida si la base de datos de sitio no está en el mismo equipo que el servidor de sitio que se está recuperando.  

### <a name="sql-server-change-tracking-retention-period"></a>Período de retención de seguimiento de cambios de SQL Server

Configuration Manager habilita el seguimiento de cambios de la base de datos de sitio de SQL Server. El seguimiento de cambios permite a Configuration Manager consultar información sobre los cambios realizados en las tablas de base de datos a partir de un punto concreto en el tiempo. El período de retención especifica cuánto tiempo se conserva la información de seguimiento de cambios. De forma predeterminada, la base de datos de sitio está configurada para tener un período de retención de cinco días. Cuando se recupera una base de datos del sitio, el proceso de recuperación variará en función de si la copia de seguridad pertenece o no al período de retención. Por ejemplo, si se produce un error en SQL Server y la última copia de seguridad se hizo hace siete días, está fuera del período de retención.

Para obtener más información sobre los datos internos de seguimiento de cambios de SQL Server, vea las siguientes entradas de blog del equipo de SQL Server: [Change Tracking Cleanup - part 1](/archive/blogs/sql_server_team/change-tracking-cleanup-part-1) (Limpieza de seguimiento de cambios: Parte 1) y [Change Tracking Cleanup - part 2](/archive/blogs/sql_server_team/change-tracking-cleanup-part-2) (Limpieza de seguimiento de cambios: Parte 2).

### <a name="reinitialization-of-site-or-global-data"></a>Reinicialización de los datos globales o del sitio

El proceso para reinicializar datos globales o del sitio reemplaza los datos existentes de la base de datos del sitio por datos de otra base de datos del sitio. Por ejemplo, si el sitio ABC reinicializa datos desde el sitio XYZ, se producen los siguientes pasos:

- Los datos se copian desde el sitio XYZ al sitio ABC.
- Los datos existentes para el sitio XYZ se quitan de la base de datos del sitio en el sitio ABC.
- Los datos copiados desde el sitio XYZ se insertan en la base de datos del sitio para el sitio ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>Escenario de ejemplo 1: El sitio primario reinicializa los datos globales desde el sitio de administración central

El proceso de recuperación quita los datos globales existentes para el sitio primario de la base de datos del sitio primario, y reemplaza los datos por datos globales copiados desde el sitio de administración central.

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>Escenario de ejemplo 2: El sitio de administración central reinicializa los datos del sitio desde un sitio primario

El proceso de recuperación quita los datos existentes de sitio de ese sitio primario de la base de datos de sitio de administración central. Reemplaza los datos con los datos de sitio copiados del sitio primario. Los datos de sitio de otros sitios primarios no se ven afectados.

### <a name="site-database-recovery-scenarios"></a>Escenarios de recuperación de base de datos de sitio

Una vez restaurada la base de datos de sitio a partir de una copia de seguridad, Configuration Manager intenta restaurar los cambios realizados en los datos globales y de sitio desde la última copia de seguridad de la base de datos. Configuration Manager inicia las siguientes acciones una vez que se restaura la base de datos de sitio a partir de la copia de seguridad:  

#### <a name="recovered-site-is-a-cas"></a>El sitio recuperado es un sitio de administración central

- Copia de seguridad de base de datos dentro del período de retención del seguimiento de cambios  

  - **Datos globales**: los cambios en los datos globales posteriores a la copia de seguridad se replican desde todos los sitios primarios.  

  - **Datos de sitio**: los cambios en los datos del sitio posteriores a la copia de seguridad se replican desde todos los sitios primarios.  

- Copia de seguridad de base de datos anterior al período de retención de seguimiento de cambios  

  - **Datos globales**: El sitio de administración central reinicializa los datos globales desde el sitio primario de referencia, si se especifica. A continuación, el resto de sitios primarios reinicializan los datos globales desde el sitio de administración central. Si no se especifica un sitio de referencia, el resto de sitios primarios reinicializan los datos globales desde el sitio de administración central. Estos datos son lo que se ha restaurado a partir de la copia de seguridad.  

  - **Datos de sitio**: El sitio de administración central reinicializa los datos del sitio desde cada sitio primario.  

#### <a name="recovered-site-is-a-primary-site"></a>El sitio recuperado es un sitio primario

- Copia de seguridad de base de datos dentro del período de retención del seguimiento de cambios  

  - **Datos globales**: Los cambios en los datos globales posteriores a la copia de seguridad se replican desde el sitio de administración central.  

  - **Datos de sitio**: El sitio de administración central reinicializa los datos del sitio desde el sitio primario. Se pierden los cambios posteriores a la copia de seguridad. Los clientes vuelven a generar la mayoría de los datos cuando envían información al sitio primario.  

- Copia de seguridad de base de datos anterior al período de retención de seguimiento de cambios  

  - **Datos globales**: El sitio primario reinicializa los datos globales desde el sitio de administración central.  

  - **Datos de sitio**: El sitio de administración central reinicializa los datos del sitio desde el sitio primario. Se pierden los cambios posteriores a la copia de seguridad. Los clientes vuelven a generar la mayoría de los datos cuando envían información al sitio primario.  

## <a name="site-recovery-procedures"></a>Procedimientos de recuperación de sitio

Use uno de los siguientes procedimientos para recuperar la base de datos de sitio y el servidor de sitio:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Iniciar una recuperación de sitio en el Asistente para instalación

1. Copie la carpeta [CD.Latest](the-cd.latest-folder.md) en una ubicación fuera de la carpeta de instalación de Configuration Manager. Desde la copia de la carpeta CD.Latest, ejecute el Asistente para instalación de Configuration Manager.  

2. En la página **Primeros pasos**, seleccione **Recuperar un sitio** y, a continuación, seleccione **Siguiente**.  

3. Complete el asistente con las opciones apropiadas para la recuperación de sitio que desea completar.  

     - Durante la recuperación, el programa de instalación identifica el puerto de SQL Server Service Broker (SSB) que usa SQL Server. No cambie el valor de este puerto durante la recuperación; de lo contrario, la replicación de datos no funcionará correctamente una vez finalizada la recuperación.  

     - Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager en el Asistente para instalación.  

### <a name="start-an-unattended-site-recovery"></a>Iniciar una recuperación de sitio desatendida

1. Prepare el script de instalación desatendida para las opciones que necesita para la recuperación de sitio. Para obtener más información, vea [Recuperación de sitios desatendida](unattended-recovery.md).  

2. Ejecute el programa de instalación de Configuration Manager mediante la opción de línea de comandos `/script`. Por ejemplo, cree un archivo de inicialización de la instalación **ConfigMgrUnattend.ini**. Guárdelo en el directorio `C:\Temp` del equipo en el que está ejecutando el programa de instalación. Use el comando siguiente:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> Después de recuperar un sitio de administración central, la replicación de algunos datos de sitios secundarios no puede establecerse. Estos datos pueden incluir el inventario de hardware, el inventario de software y los mensajes de estado.
>
> Si se produce este problema, reinicialice **ConfigMgrDRSSiteQueue** para la replicación de base de datos. Use el **Administrador de SQL Server** para ejecutar la consulta siguiente en la base de datos de sitio para el sitio de administración central:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>Tareas posteriores a la recuperación

Tras la recuperación del sitio, se deben tener en cuenta varias tareas posteriores a la recuperación para que la recuperación del sitio esté completa. Consulte las secciones siguientes para obtener información útil acerca de cómo completar el proceso de recuperación del sitio.

### <a name="reenter-user-account-passwords"></a>Volver a especificar las contraseñas de cuentas de usuario

Después de una recuperación del servidor de sitio, vuelva a especificar las contraseñas de las cuentas de usuario del sitio. Estas contraseñas se restablecen durante la recuperación del sitio. Las cuentas se enumeran en la página **Finalizado** del Asistente para instalación una vez completada la recuperación del sitio. La lista también se guarda en `C:\ConfigMgrPostRecoveryActions.html` en el servidor de sitio recuperado.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Volver a especificar las contraseñas de cuentas de usuario después de la recuperación del sitio

1. Abra la consola de Configuration Manager y conéctese con el sitio recuperado.  

2. Vaya al área de trabajo **Administración**, expanda **Seguridad** y luego seleccione **Cuentas**.  

3. Realice los siguientes pasos para cada cuenta a fin de volver a especificar la contraseña:  

     1. Seleccione la cuenta en la lista identificada después de la recuperación del sitio.  

     2. En la cinta, seleccione **Propiedades**.  

     3. En la pestaña **General**, seleccione **Establecer** y luego vuelva a escribir la contraseña de la cuenta.  

     4. Seleccione **Comprobar**, elija el origen de datos apropiado para la cuenta de usuario seleccionada y luego seleccione **Conexión de prueba**. Este paso prueba que la cuenta de usuario se puede conectar al origen de datos y comprueba las credenciales.  

     5. Seleccione **Aceptar** para guardar los cambios de la contraseña y luego **Aceptar** para cerrar la página de propiedades de la cuenta.  

#### <a name="reenter-pxe-passwords"></a>Reintroducción de las contraseñas de PXE

<!-- SCCMDocs#1683 -->

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Puntos de distribución**. Cualquier punto de distribución local en que aparezca **Sí** en la columna **PXE** está habilitado con PXE y es posible que sea necesario escribir su contraseña.

1. Seleccione un punto de distribución habilitado con PXE y seleccione **Propiedades** en la cinta.

1. Cambie a la pestaña **PXE**.

1. Si está habilitada la opción **Requerir una contraseña cuando los equipos usen PXE**, escriba y confirme la contraseña.

1. Seleccione **Aceptar** para guardar y cerrar las propiedades.

Repita este proceso para cualquier otro punto de distribución local habilitado con PXE.

#### <a name="reenter-task-sequence-passwords"></a>Reescritura de las contraseñas de las secuencias de tareas

<!-- SCCMDocs#1683 -->

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione el nodo **Secuencias de tareas**.

1. Seleccione una secuencia de tareas y, a continuación, en la cinta, seleccione **Editar**.

1. Revise los pasos siguientes para volver a escribir contraseñas:

    - **Aplicar configuraciones de Windows**: Si habilita y especifica la contraseña de administrador local, vuelva a escribir y confirme la contraseña.

    - **Aplicar configuración de red**: En la cuenta que tiene permiso para unirse al dominio, seleccione **Establecer**. Escriba y confirme la contraseña y, a continuación, seleccione **Comprobar**.

    - **Capturar imagen de sistema operativo**: En la cuenta empleada para acceder al destino, seleccione **Establecer**. Escriba y confirme la contraseña y, a continuación, seleccione **Comprobar**.

    - **Conexión a la carpeta de red**: En la cuenta usada para conectar una carpeta de red, seleccione **Establecer**. Escriba y confirme la contraseña y, a continuación, seleccione **Comprobar**.

    - **Habilitar BitLocker**: Si usa la opción de administración de claves **TPM y PIN**, vuelva a escribir el PIN.

    - **Unirse a dominio o grupo de trabajo**: En la cuenta que tiene permiso para unirse al dominio, seleccione **Establecer**. Escriba y confirme la contraseña y, a continuación, seleccione **Comprobar**.

    - **Ejecutar línea de comandos**: Si usa la opción para **ejecutar esta etapa como la cuenta siguiente**, seleccione **Establecer**. Escriba y confirme la contraseña y, a continuación, seleccione **Comprobar**.

    - **Ejecutar script de PowerShell**: Si usa la opción para **ejecutar esta etapa como la cuenta siguiente**, seleccione **Establecer**. Escriba y confirme la contraseña y, a continuación, seleccione **Comprobar**.

Repita este proceso para todas las secuencias de tareas.

### <a name="recreate-bootable-media-and-prestaged-media-in-non-pki-environments"></a>Nueva creación de medios de arranque y medios preconfigurados en entornos que no son de PKI

En entornos que no son de PKI, los certificados autofirmados en medios de arranque y medios configurados se basan en las claves de máquina del servidor en el que se crearon los medios. Por esta razón, si el hardware cambia o el sistema operativo se vuelve a instalar como parte de una recuperación, es necesario volver a crear los medios de arranque y los medios preconfigurados que se crearon en ese servidor. Para más información sobre cómo crear medios de arranque y medios preconfigurados, consulte [Crear medios de arranque](../../../osd/deploy-use/create-bootable-media.md) y [Crear medios preconfigurados](../../../osd/deploy-use/create-prestaged-media.md).

### <a name="reenter-sideloading-keys"></a>Volver a especificar las claves de instalación de prueba

Después de una recuperación del servidor de sitio, vuelva a especificar las claves de instalación de prueba de Windows especificadas para el sitio. Estas claves se restablecen durante la recuperación del sitio. Después de volver a especificar las claves de instalación de prueba, el sitio restablece el recuento de la columna **Activaciones usadas** de las claves de instalación de prueba de Windows.

Por ejemplo, antes del error del sitio, el recuento de **Total de activaciones** muestra **100**. El número de claves que han usado los dispositivos, o **Activaciones usadas**, es **90**. Después de la recuperación del sitio, el valor **Total de activaciones** sigue mostrando **100**, pero la columna **Activaciones usadas** muestra de forma incorrecta **0**. Después de que diez nuevos dispositivos usen una clave de instalación de prueba, no queda ninguna clave de instalación de prueba y el dispositivo número 11 no puede aplicar ninguna clave de instalación de prueba.

### <a name="recreate-azure-services"></a>Nueva creación de los servicios de Azure

<!-- SCCMDocs#1022 -->

En la versión 1806 de Configuration Manager, después de la recuperación del sitio, verá el siguiente error en cloudmgr.log:

`Index (zero-based) must be greater than or equal to zero`

Para solucionarlo, [renueve la clave secreta](../deploy/configure/azure-services-wizard.md#bkmk_renew) para cada conexión de inquilino de Azure.

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configuración de SSL para roles de sistema de sitio que usan IIS

Al recuperar sistemas de sitio que ejecutan IIS y que se habían configurado para HTTPS, vuelva a configurar IIS para usar el certificado de servidor web.

### <a name="reinstall-hotfixes"></a>Reinstalar revisiones

Tras una recuperación del sitio, debe reinstalar las [revisiones extraordinarias](updates.md#bkmk_outofband) que se han aplicado al servidor del sitio. Tras la recuperación del sitio, vea la lista de las revisiones instaladas anteriormente en la página **Finalizado** del Asistente para instalación. Esta lista también se guarda en `C:\ConfigMgrPostRecoveryActions.html` en el servidor de sitio recuperado.

### <a name="recover-custom-reports"></a>Recuperar informes personalizados

Algunos clientes crean informes personalizados en SQL Server Reporting Services. Cuando se produce un error en este componente, recupere los informes a partir de una copia de seguridad del servidor de informes. Para obtener más información sobre la restauración de los informes personalizados de Reporting Services, vea [Operaciones de copia de seguridad y restauración de Reporting Services](/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### <a name="recover-content-files"></a>Recuperación de archivos de contenido

La base de datos de sitio realiza un seguimiento de la ubicación en la que el servidor de sitio almacena los archivos de contenido. No se realiza copia de seguridad de los propios archivos de contenido ni se restauran como parte del proceso de copia de seguridad y recuperación. Para recuperar totalmente los archivos de contenido, restaure la biblioteca de contenido y los archivos de origen del paquete en la ubicación original. Hay varios métodos para recuperar los archivos de contenido. El método más sencillo consiste en restaurar los archivos a partir de una copia de seguridad del sistema de archivos del servidor de sitio.

Si no tiene una copia de seguridad del sistema de archivos de los archivos de origen del paquete, cópielos o descárguelos manualmente. Este proceso es similar a la creación original del paquete. Ejecute la siguiente consulta en SQL Server para buscar la ubicación de origen del paquete de todos los paquetes y las aplicaciones: `SELECT * FROM v_Package`. Identifique el sitio de origen del paquete mediante los tres primeros caracteres del identificador del paquete. Por ejemplo, si el identificador del paquete es CEN00001, el código de sitio del sitio de origen es CEN. Cuando restaure los archivos de origen del paquete, se deben restaurar en la misma ubicación en la que se encontraban antes del error.

Si no tiene una copia de seguridad del sistema de archivos que incluya la biblioteca de contenido, tiene las siguientes opciones de restauración:  

- **Importar un archivo de contenido preconfigurado**: en una jerarquía de Configuration Manager, puede crear un archivo de contenido preconfigurado con todos los paquetes y las aplicaciones de otra ubicación. Luego, importe el archivo de contenido preconfigurado para recuperar la biblioteca de contenido en el servidor de sitio.  

- **Actualizar contenido**: Configuration Manager copia el contenido del origen del paquete en la biblioteca de contenido. Para que esta acción finalice correctamente, los archivos de origen del paquete deben estar disponibles en la ubicación original. Realice esta acción en cada paquete y aplicación.

### <a name="recover-custom-software-updates"></a>Recuperar actualizaciones de software personalizadas

Si ha incluido archivos de base de datos de System Center Updates Publisher en el plan de copias de seguridad, puede recuperar las bases de datos si se produce un error en el equipo de Updates Publisher. Para obtener más información sobre Updates Publisher, vea [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

#### <a name="restore-the-updates-publisher-database"></a>Restaurar la base de datos de Updates Publisher

1. Vuelva a instalar Updates Publisher en el equipo recuperado.  

2. Copie el archivo de base de datos **Scupdb.sdf** del destino de copia de seguridad en `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` en el equipo que ejecuta Updates Publisher.  

3. Si más de un usuario ejecuta Updates Publisher en el equipo, copie cada archivo de base de datos en la ubicación del perfil de usuario correspondiente.  

### <a name="user-state-migration-data"></a>Datos de migración de estado de usuario

Como parte de las propiedades de punto de migración de estado, se especifican las carpetas que almacenan datos de estado de usuario. Después de recuperar un punto de migración de estado, restaure manualmente los datos de estado de usuario en el servidor. Restaure en las mismas carpetas donde se almacenaban los datos antes del error.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Regeneración de los certificados para puntos de distribución

Después de restaurar un sitio, **distmgr.log** podría contener la siguiente entrada para uno o varios puntos de distribución: `Failed to decrypt cert PFX data`. Esta entrada indica que el sitio no puede descifrar los datos del certificado de punto de distribución. Para resolver este problema, vuelva a generar o a importar el certificado de los puntos de distribución afectados. Use el cmdlet [Set-CMDistributionPoint](/powershell/module/configurationmanager/set-cmdistributionpoint) de PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Actualizar certificados usados para puntos de distribución basados en la nube

Configuration Manager exige un certificado de administración de Azure para el servidor de sitio para comunicarse con puntos de distribución basados en la nube. Después de una recuperación de sitio, actualice los certificados de los puntos de distribución basados en la nube.

## <a name="recover-a-secondary-site"></a>Recuperar un sitio secundario

Configuration Manager no admite la copia de seguridad de la base de datos en un sitio secundario, pero sí la recuperación mediante la reinstalación del sitio secundario. Se precisa la recuperación de sitio secundario si se produce un error en un sitio secundario de Configuration Manager.

### <a name="requirements"></a>Requisitos

- El servidor debe cumplir todos los requisitos previos del sitio secundario y tener los derechos de seguridad correspondientes configurados.  

- Use la misma ruta de instalación que se usó para el sitio con errores.  

- Use un servidor con la misma configuración que el servidor con errores. Esta configuración incluye su nombre de dominio completo (FQDN).  

- El servidor debe tener la misma configuración de SQL Server que el sitio con errores.  

  - Durante la recuperación de un sitio secundario, Configuration Manager no instala SQL Server Express si no está instalado ya en el equipo.  

  - Use la misma versión de SQL Server y la misma instancia de SQL Server que se usaron para la base de datos del sitio secundario antes del error.  

### <a name="procedure"></a>Procedimiento

Use la acción **Recuperar sitio secundario** del nodo **Sitios** de la consola de Configuration Manager. A diferencia de lo que ocurre con otros tipos de sitios, la recuperación de un sitio secundario no usa un archivo de copia de seguridad. Este proceso reinstala los archivos del sitio secundario en el servidor con errores. Una vez reinstalado el sitio, los datos del sitio secundario se reinicializan a partir del sitio primario.

Durante el proceso de recuperación, Configuration Manager verifica la existencia de la biblioteca de contenido en el servidor de sitio secundario. También comprueba que esté disponible el contenido adecuado. El sitio secundario usa la biblioteca de contenido existente, si esta incluye el contenido adecuado. De lo contrario, para recuperar la biblioteca de contenido de un sitio secundario, redistribuya o preconfigure el contenido en el servidor.

Si tiene un punto de distribución que no está en el servidor del sitio secundario, no es preciso que vuelva a instalar el punto de distribución durante la recuperación del sitio secundario. Después de la recuperación de sitio secundario, el sitio se sincroniza automáticamente con el punto de distribución.

Puede comprobar el estado de la recuperación del sitio secundario mediante la acción **Mostrar estado de instalación** del nodo **Sitios** de la consola de Configuration Manager.