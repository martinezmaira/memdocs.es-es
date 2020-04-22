---
title: Sitios de copia de seguridad
titleSuffix: Configuration Manager
description: Obtenga información para realizar copias de seguridad de los sitios ante la posibilidad de un error o pérdida de datos en Configuration Manager.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 824eaeb939249e1bcc2ed21d5815a0a72dc54797
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700273"
---
# <a name="back-up-a-configuration-manager-site"></a>Hacer una copia de seguridad de un sitio de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Prepare enfoques de copia de seguridad y recuperación para evitar la pérdida de datos. En los sitios de Configuration Manager, un enfoque de copia de seguridad y recuperación puede ayudar a recuperar sitios y jerarquías más rápidamente y con la mínima pérdida de datos.  

Las secciones de este artículo pueden ayudarle a realizar copias de seguridad de los sitios. Para recuperar un sitio, consulte [Recovery for Configuration Manager](recover-sites.md) (Recuperación para Configuration Manager).  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> Los dos métodos de copia de seguridad que se admiten en la recuperación de sitios de Configuration Manager son:
>
> - Una copia de seguridad en estado correcto de la tarea de mantenimiento **Copia de seguridad del servidor del sitio**
> - Una copia de seguridad de base de datos de sitio recuperada manualmente


## <a name="considerations-before-creating-a-backup"></a>Aspectos que debe tener en cuenta antes de crear una copia de seguridad  

-   Si usa un grupo de disponibilidad Always On de SQL Server para hospedar la base de datos del sitio: modifique los planes de copia de seguridad y recuperación, como se describe en [Preparación para usar grupos de disponibilidad AlwaysOn de SQL Server](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup).  

-   Configuration Manager puede recuperar la base de datos de sitio desde la tarea de copia de seguridad de Configuration Manager. También puede usar una copia de seguridad de la base de datos de sitio creada con otro proceso.   

     Por ejemplo, puede restaurar la base de datos de sitio a partir de una copia de seguridad creada como parte de un plan de mantenimiento de Microsoft SQL Server. También puede usar una copia de seguridad creada con Data Protection Manager para hacer una copia de seguridad de la base de datos de sitio.  

-   A partir de la versión 1806, instale un servidor de sitio adicional en modo *pasivo*. El servidor de sitio en modo pasivo se suma al servidor de sitio existente en modo *activo*. Un servidor de sitio en modo pasivo está disponible para uso inmediato, cuando sea necesario. Para obtener más información, vea [Alta disponibilidad de servidor de sitio](../deploy/configure/site-server-high-availability.md). Aunque este rol no elimina la necesidad de planear y realizar las operaciones de copia de seguridad y recuperación, reduce considerablemente el esfuerzo necesario para recuperar un sitio en caso necesario.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Uso de Data Protection Manager para realizar copias de seguridad de la base de datos del sitio
Puede usar System Center Data Protection Manager (DPM) para hacer una copia de seguridad de la base de datos de sitio de Configuration Manager.

Cree un nuevo grupo de protección en DPM para el equipo de la base de datos de sitio. En la página **Seleccionar miembros del grupo** del asistente Crear nuevo grupo de protección, seleccione el servicio SMS Writer en la lista de orígenes de datos. Luego seleccione la base de datos de sitio como un miembro apropiado. Para obtener más información sobre DPM, vea la biblioteca de documentación de [Data Protection Manager](https://docs.microsoft.com/system-center/dpm).  

> [!IMPORTANT]  
>  Configuration Manager no admite la copia de seguridad de DPM para un clúster de SQL Server que use una instancia con nombre. Sí admite la copia de seguridad de DPM en un clúster de SQL Server que use la instancia predeterminada de SQL Server.  

Después de restaurar la base de datos de sitio, siga los pasos del programa de instalación para recuperar el sitio. Para usar la base de datos de sitio cuya copia de seguridad ha realizado con Data Protection Manager, seleccione la opción de recuperación para **usar una base de datos de sitio que se ha recuperado manualmente**.  



## <a name="backup-maintenance-task"></a>Tarea de mantenimiento de copia de seguridad
Puede automatizar la copia de seguridad de sitios de Configuration Manager mediante la programación de la tarea de mantenimiento predefinida Copia de seguridad del servidor del sitio. Esta tarea tiene las siguientes características:

-   Se ejecuta según una programación
-   Realiza copias de seguridad de la base de datos del sitio
-   Realiza copias de seguridad de claves de registro específicas
-   Realiza copias de seguridad de carpetas y archivos específicos
-   Realiza copias de seguridad de la carpeta [CD.Latest](the-cd.latest-folder.md)   

Planee una ejecución de la tarea de copia de seguridad del sitio predeterminada como mínimo cada cinco días. Esta programación se debe a que Configuration Manager usa un *período de retención de seguimiento de cambios de SQL Server* de cinco días. Para obtener más información, vea [SQL Server change tracking retention period](recover-sites.md#sql-server-change-tracking-retention-period) (Período de retención de seguimiento de cambios de SQL Server).

Para simplificar el proceso de copia de seguridad, puede crear un archivo **AfterBackup.bat**. Este script ejecuta automáticamente acciones posteriores a la copia de seguridad después de que la tarea de copia de seguridad finalice correctamente. Use el archivo AfterBackup.bat para archivar la instantánea de copia de seguridad en una ubicación segura. También puede usar el archivo AfterBackup.bat para copiar archivos en la carpeta de copia de seguridad o para iniciar otras tareas de copia de seguridad.  

Puede realizar una copia de seguridad de un sitio de administración central y de un sitio primario. Los sitios secundarios o los servidores de sistema de sitio no tienen tareas de copia de seguridad.

Cuando se ejecuta el servicio de copia de seguridad de Configuration Manager, sigue las instrucciones definidas en el archivo de control de copia de seguridad: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`. Puede modificar el archivo de control de copia de seguridad para cambiar el comportamiento del servicio de copia de seguridad.  
> [!NOTE]
> Las modificaciones de **Smsbkup.ctl** se aplicarán después de reiniciar el servicio SMS_SITE_VSS_WRITER en el servidor de sitio.

La información del estado de copia de seguridad del sitio se escribe en el archivo **Smsbkup.log** . Este archivo se crea en la carpeta de destino que se especifica en las propiedades de la tarea de mantenimiento Copia de seguridad del servidor del sitio.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Para habilitar la tarea de mantenimiento de copia de seguridad de sitio  
1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2.  Seleccione el sitio para el que quiere habilitar la tarea de mantenimiento de copia de seguridad de sitio.  

3.  Haga clic en **Tarea de mantenimiento de sitio** en la cinta de opciones.  

4.  Seleccione la tarea **Copia de seguridad del servidor del sitio** y haga clic en **Editar**.  

5.  Seleccione la opción para **habilitar esta tarea**. Haga clic en **Definir rutas de acceso** para especificar el destino de la copia de seguridad. Dispone de las siguientes opciones:  

    > [!IMPORTANT]  
    >  Con el fin de evitar la manipulación de los archivos de copia de seguridad, almacene los archivos en una ubicación segura. La ruta de acceso de copia de seguridad más segura es una unidad local, donde puede establecer los permisos de archivos NTFS en la carpeta. Configuration Manager no cifra los datos de copia de seguridad que se almacenan en la ruta de acceso de copia de seguridad.  

    -   **Unidad local en servidor de sitio para los datos y la base de datos del sitio**: especifica que la tarea almacene los archivos de copia de seguridad para el sitio y la base de datos del sitio en la ruta especificada en la unidad de disco local del servidor de sitio. Cree la carpeta local antes de que se ejecute la tarea de copia de seguridad. La cuenta Sistema local del servidor de sitio debe tener permisos de archivos NTFS de **escritura** en la carpeta local para la copia de seguridad del servidor de sitio. La cuenta Sistema local del equipo con SQL Server debe tener permisos NTFS de **escritura** en la carpeta para la copia de seguridad de la base de datos de sitio.  

    -   **Ruta de acceso de red (nombre UNC) para los datos y la base de datos del sitio**: especifica que la tarea almacene los archivos de copia de seguridad del sitio y de la base de datos del sitio en la ruta de red especificada. Cree el recurso compartido antes de que se ejecute la tarea de copia de seguridad. La cuenta de equipo del servidor de sitio debe tener permisos NTFS y de uso compartido de **escritura** en la carpeta de red compartida. Si SQL Server está instalado en otro equipo, la cuenta de equipo de SQL Server debe tener los mismos permisos.  

    -   **Unidades locales en el servidor de sitio y SQL Server**: la tarea almacena los archivos de copia de seguridad para la base de datos de sitio en la ruta especificada en la unidad local del servidor de sitio. La tarea almacena los archivos de copia de seguridad para la base de datos de sitio en la ruta de acceso especificada en la unidad local del servidor de base de datos de sitio. Cree las carpetas locales antes de que se ejecute la tarea de copia de seguridad. La cuenta de equipo del servidor de sitio debe tener permisos de NTFS de **escritura** en la carpeta que se crea en el servidor de sitio. La cuenta de equipo del servidor de SQL Server debe tener permisos de NTFS de **escritura** en la carpeta que se crea en el servidor de la base de datos del sitio. Esta opción solo está disponible cuando la base de datos de sitio no está instalada en el servidor de sitio.  

    > [!NOTE]  
    > La opción de desplazarse al destino de copia de seguridad solo está disponible si se especifica la ruta de acceso de red del destino de copia de seguridad.  
    >  
    > El nombre de la carpeta o el nombre del recurso compartido que se usan para el destino de copia de seguridad no admiten caracteres Unicode.  

6.  Configure una programación para la tarea de copia de seguridad del sitio. Considere la posibilidad de programar la copia de seguridad fuera del horario de trabajo activo. Si tiene una jerarquía, considere la posibilidad de una programación que se ejecute al menos dos veces por semana. Si se produce un error en el sitio, esta programación garantiza la máxima retención de datos.  

    Cuando se ejecuta la consola de Configuration Manager en el mismo servidor de sitio que se está configurando para la copia de seguridad, la tarea de copia de seguridad usa la hora local para la programación. Cuando se ejecuta la consola de Configuration Manager desde otro equipo, la tarea de copia de seguridad usa la hora universal coordinada (UTC) para la programación.  

7.  Elija si quiere crear una alerta en caso de error de la tarea de copia de seguridad. Cuando se selecciona, Configuration Manager crea una alerta crítica para el error de copia de seguridad. Puede ver estas alertas en el nodo **Alertas** del área de trabajo **Supervisión**.  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Comprobar que la tarea de mantenimiento Copia de seguridad del servidor del sitio se está ejecutando  

-   Compruebe la marca de tiempo en los archivos de la carpeta de destino de la copia de seguridad que creó la tarea. Compruebe que la marca de tiempo se actualiza a la hora de la última ejecución programada.  

-   Vaya al nodo **Estado del componente** del área de trabajo **Supervisión**. Revise los mensajes de estado de **SMS_SITE_BACKUP**. Cuando termina correctamente la copia de seguridad de sitio, aparece el id. de mensaje **5035**. Este mensaje indica que la copia de seguridad de sitio se ha completado sin errores.  

-   Cuando configure la tarea de copia de seguridad para crear una alerta si se produce un error, busque las alertas de error de copia de seguridad en el nodo **Alertas** del área de trabajo **Supervisión**.  

-   Abra el Explorador de Windows en el servidor de sitio y vaya a `<ConfigMgrInstallationFolder>\Logs`. Revise **Smsbkup.log** en busca de errores y advertencias. Cuando termina correctamente la copia de seguridad de sitio, el registro muestra `Backup completed` con el id. de mensaje `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Si se produce un error en la tarea de mantenimiento de copia de seguridad, reinicie la tarea de copia de seguridad. Para ello, detenga y reinicie el servicio de Windows **SMS_SITE_BACKUP**.  



## <a name="archive-the-backup-snapshot"></a>Archivo de la instantánea de copia de seguridad  
La tarea de copia de seguridad crea una instantánea de copia de seguridad la primera vez que se ejecuta. Puede usar esta instantánea para recuperar el servidor de sitio si se produce un error. Cuando la tarea de copia de seguridad se ejecuta de nuevo conforme a la programación, crea una nueva instantánea de copia de seguridad que sobrescribe la instantánea anterior. Como resultado, el sitio solo tiene una instantánea de copia de seguridad y no hay forma de recuperar una instantánea de copia de seguridad anterior.  

Conserve varios archivos de la instantánea de copia de seguridad por los siguientes motivos:  

-   Es común que se produzcan errores en los medios de copia de seguridad, que estén en una ubicación incorrecta o que solo incluyan una copia de seguridad parcial. La recuperación de un sitio primario independiente con errores desde una copia de seguridad antigua es mejor que una recuperación sin ninguna copia de seguridad. En el caso de un servidor de sitio de una jerarquía, la copia de seguridad debe estar en el período de retención de seguimiento de cambios de SQL Server, o no es necesaria.  

-   La existencia de daños en el sitio puede pasar desapercibida durante varios ciclos de copia de seguridad. Es posible que tenga que usar una instantánea de copia de seguridad anterior al momento en que el sitio resultó dañado. Este motivo se aplica a un sitio primario independiente y a los sitios de una jerarquía en la que la copia de seguridad está en el período de retención de seguimiento de cambios de SQL Server.  

-   El sitio podría no tener ninguna instantánea de copia de seguridad en absoluto. Por ejemplo, si se produce un error en la tarea de mantenimiento Copia de seguridad del servidor del sitio. Dado que la tarea de copia de seguridad elimina la instantánea de copia de seguridad anterior antes de empezar a realizar la copia de seguridad de los datos actuales, no habrá ninguna instantánea de copia de seguridad válida.  



## <a name="using-the-afterbackupbat-file"></a>Uso del archivo AfterBackup.bat  
Después de realizar la copia de seguridad del sitio correctamente, la tarea de copia de seguridad automáticamente intenta ejecutar un script denominado **AfterBackup.bat**. Cree manualmente el archivo AfterBackup.bat en el servidor de sitio en `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box`. Si hay un archivo AfterBackup.bat en la carpeta correcta, se ejecuta automáticamente después de que termine la tarea de copia de seguridad.

El archivo AfterBackup.bat permite archivar la instantánea de copia de seguridad al final de cada operación de copia de seguridad. Puede realizar automáticamente otras tareas posteriores a la copia de seguridad que no formen parte de la tarea de mantenimiento Copia de seguridad del servidor del sitio. El archivo AfterBackup.bat integra las operaciones de archivo y copia de seguridad, por lo que garantiza que se archiva cada nueva instantánea de copia de seguridad.

Si el archivo AfterBackup.bat no está presente, la tarea de copia de seguridad lo omite sin que se vea afectada la operación de copia de seguridad. Para comprobar que la tarea de copia de seguridad ha ejecutado correctamente el script, vaya al nodo **Estado del componente** del área de trabajo **Supervisión** y revise los mensajes de estado de **SMS_SITE_BACKUP**. Si la tarea inicia correctamente el archivo de comandos AfterBackup.bat, aparece el id. de mensaje **5040**.  

> [!TIP]  
>  Para archivar los archivos de copia de seguridad del servidor de sitio con AfterBackup.bat, debe usar una herramienta de comandos de copiado en el archivo por lotes. Un ejemplo de este tipo de herramienta es [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy), en Windows Server. Por ejemplo, cree el archivo AfterBackup.bat con el siguiente comando: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Aunque el uso previsto de AfterBackup.bat es archivar instantáneas de copia de seguridad, puede crear un archivo AfterBackup.bat para ejecutar otras tareas al término de cada operación de copia de seguridad.  



##  <a name="supplemental-backup-tasks"></a>Tareas de copia de seguridad adicionales  
La tarea de mantenimiento Copia de seguridad del servidor del sitio proporciona una instantánea de copia de seguridad de los archivos del servidor de sitio y la base de datos de sitio. Hay otros elementos de los que no se realiza copia de seguridad que debe tener en cuenta al crear la estrategia de copia de seguridad. Use estas secciones como ayuda para completar la estrategia de copia de seguridad de Configuration Manager.  

### <a name="back-up-custom-reports"></a>Copia de seguridad de informes personalizados   
Si modifica informes personalizados predefinidos o creados en SQL Server Reporting Services, cree una copia de seguridad de los archivos de base de datos del servidor de informes. La copia de seguridad del servidor de informes debe incluir los siguientes componentes:
- Los archivos de origen de los informes y los modelos
- Claves de cifrado
- Las extensiones o los ensamblados personalizados
- Los archivos de configuración
- Las vistas personalizadas de SQL Server usadas en los informes personalizados
- Los procedimientos almacenados personalizados  

> [!IMPORTANT]  
>  Cuando Configuration Manager se actualiza a una versión más reciente, los nuevos informes podrían sobrescribir los informes predefinidos. Si modifica un informe predefinido, asegúrese de realizar una copia de seguridad y luego restáurela en Reporting Services.  

Para obtener más información sobre la copia de seguridad de los informes personalizados en Reporting Services, vea [Operaciones de copia de seguridad y restauración de Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Copia de seguridad de archivos de contenido  
La biblioteca de contenido de Configuration Manager es la ubicación donde se almacenan todos los archivos de contenido de todas las implementaciones de software. La biblioteca de contenido se encuentra en el servidor de sitio y en cada punto de distribución. La tarea de mantenimiento Copia de seguridad del servidor del sitio no realiza una copia de seguridad de la biblioteca de contenido ni de los archivos de origen del paquete. Cuando se produce un error en el servidor de sitio, la información sobre la biblioteca de contenido se restaura en la base de datos de sitio, pero el usuario debe restaurar la biblioteca de contenido y los archivos de origen del paquete.  

-   La biblioteca de contenido debe restaurarse para poder redistribuir el contenido a los puntos de distribución. Cuando se inicia la redistribución de contenido, Configuration Manager copia los archivos de la biblioteca de contenido del servidor de sitio en los puntos de distribución. Para obtener más información, vea [La biblioteca de contenido](../../plan-design/hierarchy/the-content-library.md).  

-   Los archivos de origen del paquete deben restaurarse para poder actualizar el contenido de los puntos de distribución. Cuando se inicia una actualización de contenido, Configuration Manager copia los archivos nuevos o modificados del origen del paquete en la biblioteca de contenido. Luego copia los archivos en los puntos de distribución asociados. Ejecute la siguiente consulta de SQL Server en la base de datos de sitio para buscar la ubicación del origen del paquete de todos los paquetes y aplicaciones: `SELECT * FROM v_Package`. Puede identificar el sitio del origen del paquete mediante los tres primeros caracteres del identificador del paquete. Por ejemplo, si el identificador del paquete es CEN00001, el código de sitio del sitio de origen es CEN. Cuando restaure los archivos de origen del paquete, debe hacerlo en la misma ubicación en la que se encontraban antes del error.  

Compruebe que ha incluido la biblioteca de contenido y los archivos del origen del paquete en la copia de seguridad del sistema de archivos del servidor de sitio.  

### <a name="back-up-custom-software-updates"></a>Copia de seguridad de actualizaciones de software personalizadas  
System Center Updates Publisher es una herramienta independiente que permite administrar actualizaciones de software personalizadas. Updates Publisher usa una base de datos local para el repositorio de actualizaciones de software. Si usa Updates Publisher para administrar las actualizaciones de software personalizadas, determine si tiene que incluir la base de datos de Updates Publisher en el plan de copias de seguridad. Para obtener más información, vea [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).  

Use el siguiente procedimiento para realizar una copia de seguridad de la base de datos de Updates Publisher.  

#### <a name="back-up-the-updates-publisher-database"></a>Copia de seguridad de la base de datos de Updates Publisher  

1.  En el equipo que ejecuta Updates Publisher, busque el archivo de base de datos de Updates Publisher, **Scupdb.sdf**, en `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`. Hay un archivo de base de datos diferente para cada usuario que ejecuta Updates Publisher.  

2.  Copie el archivo de base de datos en el destino de la copia de seguridad. Por ejemplo, si el destino de copia de seguridad es `E:\ConfigMgr_Backup`, podría copiar el archivo de base de datos de Updates Publisher en `E:\ConfigMgr_Backup\SCUP`.  

    > [!TIP]  
    >  Si hay más de un archivo de base de datos en un equipo, considere la posibilidad de almacenar el archivo en una subcarpeta que indique el perfil de usuario asociado al archivo de base de datos. Por ejemplo, podría tener un archivo de base de datos en `E:\ConfigMgr_Backup\SCUP\User1` y otro en `E:\ConfigMgr_Backup\SCUP\User2`.  



## <a name="user-state-migration-data"></a>Datos de migración de estado de usuario  
Puede usar secuencias de tareas de Configuration Manager para capturar y restaurar los datos de estado de usuario en escenarios de implementación de sistema operativo. Las propiedades del punto de migración de estado indican las carpetas que almacenan los datos de estado de usuario. No se realiza copia de seguridad de estos datos como parte de la tarea de mantenimiento Copia de seguridad del servidor del sitio. Como parte del plan de copias de seguridad, debe realizar manualmente la copia de seguridad de las carpetas que especifique para almacenar los datos de migración de estado de usuario.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Determinar las carpetas usadas para almacenar datos de migración de estado de usuario  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Servidores y roles del sistema de sitios**.  

2.  Seleccione el sistema de sitio que hospeda el rol de migración de estado. Luego seleccione **Punto de migración de estado** en el panel **Roles del sistema de sitio**.  

3.  Haga clic en **Propiedades** de la cinta.  

4.  Las carpetas donde se almacenan los datos de migración de estado de usuario se enumeran en la sección **Detalles de la carpeta** de la pestaña **General**.  



## <a name="about-the-sms-writer-service"></a>Acerca del servicio SMS Writer  
SMS Writer es un servicio que interactúa con el Servicio de instantáneas de volumen (VSS) de Windows durante el proceso de copia de seguridad. Para que la copia de seguridad del sitio de Configuration Manager se complete correctamente, el servicio SMS Writer se debe estar ejecutando.  

### <a name="process"></a>Proceso  
1. SMS Writer se registra con el servicio VSS y se enlaza a sus interfaces y eventos. 
2. Cuando VSS difunde eventos o envía notificaciones específicas a SMS Writer, SMS Writer responde a la notificación y toma las medidas oportunas. 
3. SMS Writer lee el archivo de control de copia de seguridad **smsbkup.ctl** que se encuentra en `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` y determina los archivos y los datos de los que se va a hacer una copia de seguridad. 
4. SMS Writer compila metadatos, que constan de varios componentes, incluidos datos específicos de la clave del Registro SMS y las subclaves. 
    a. Envía los metadatos a VSS cuando se le solicitan. 
    b. Luego, VSS envía los metadatos a la aplicación solicitante, el Administrador de copias de seguridad de Configuration Manager. 
5. El Administrador de copias de seguridad selecciona los datos de los que se va a hacer copia de seguridad y los envía a SMS Writer mediante VSS. 
6. El servicio SMS Writer realiza los pasos apropiados para prepararse para la copia de seguridad. 
7. Posteriormente, cuando VSS está listo para realizar la instantánea: a. Envía un evento b. SMS Writer detiene todos los servicios de Configuration Manager c. Se asegura de que las actividades de Configuration Manager estén detenidas mientras se crea la instantánea. 
8. Una vez completada la instantánea, SMS Writer reinicia los servicios y las actividades.

El servicio SMS Writer se instala automáticamente. Debe ejecutarse cuando la aplicación VSS solicite una copia de seguridad o restauración.  

### <a name="writer-id"></a>Identificador de escritor  
El identificador de escritor de SMS Writer es **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Permisos  
El servicio SMS Writer debe ejecutarse bajo la cuenta Sistema local.  

### <a name="volume-shadow-copy-service"></a>Servicio de instantáneas de volumen  
El servicio VSS es un conjunto de API de COM que implementan un marco para permitir la realización de copias de seguridad de volumen mientras se siguen escribiendo aplicaciones de un sistema en los volúmenes. El servicio VSS proporciona una interfaz coherente que permite la coordinación entre aplicaciones de usuario que actualizan datos en el disco (el servicio SMS Writer) y otras que realizan copias de seguridad de aplicaciones (el servicio Administrador de actualizaciones). Para obtener más información, vea [Volume Shadow Copy Service](https://go.microsoft.com/fwlink/p/?LinkId=241968) (Servicio de instantáneas de volumen).  



## <a name="next-steps"></a>Pasos siguientes
Después de crear una copia de seguridad, practique la [recuperación del sitio](recover-sites.md) con esa copia de seguridad. Esta práctica puede ayudarle a familiarizarse con el proceso de recuperación antes de que necesite depender de él. También puede ayudar a confirmar que la copia de seguridad se ha realizado correctamente para el fin previsto.  
