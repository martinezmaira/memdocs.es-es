---
title: Almacenamiento de datos
titleSuffix: Configuration Manager
description: Punto de servicio de almacenamiento de datos y base de datos para Configuration Manager
ms.date: 05/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43bb2d1cc85488decf61bce7a3f18aa73bc17bce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692673"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>El punto de servicio de almacenamiento de datos para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--1277922-->
Use el punto de servicio de almacenamiento de datos para almacenar y generar informes de datos históricos a largo plazo para su implementación de Configuration Manager.

> [!Note]  
> En la versión 1910, Configuration Manager habilita esta característica opcional de forma predeterminada, mientras que en la versión 1906 o anteriores no lo hace. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](install-in-console-updates.md#bkmk_options).<!--505213-->  


El almacenamiento de datos admite hasta 2 TB de datos, con marcas de tiempo para el seguimiento de cambios. El almacenamiento de datos guarda datos sincronizando automáticamente la base de datos de sitio de Configuration Manager con la base de datos de almacenamiento de datos. Puede acceder a esta información desde su punto de servicio de informes. Los datos que se sincronizan con la base de datos de almacenamiento de datos se conservan durante tres años. Periódicamente, una tarea integrada quita los datos anteriores a este período.

Los datos que se sincronizan incluyen lo siguiente de los grupos de datos globales y datos de sitio:
- Mantenimiento de infraestructura
- Seguridad
- Cumplimiento
- Malware   
- Implementaciones de software
- Detalles de inventario (en cambio, el historial de inventario no se sincroniza)

Cuando se instala el rol de sistema de sitio, instala y configura la base de datos del almacén de datos. También instala varios informes de forma que pueda buscar fácilmente estos datos y crear informes sobre ellos.

A partir de la versión 1810, puede sincronizar más tablas desde la base de datos de sitio con el almacenamiento de datos. Este cambio permite crear más informes según sus requisitos empresariales.<!--1358870--> 



## <a name="prerequisites"></a>Requisitos previos

- El rol de sistema de sitio de almacenamiento de datos solo es compatible con el sitio de nivel superior de la jerarquía Por ejemplo, un sitio de administración central o un sitio primario independiente.  

- El equipo en el que instale el rol de sistema de sitio necesita .NET Framework 4.5.2 o versiones posteriores.  

- Conceda a la **cuenta de punto de Reporting Services** el permiso **db_datareader** en la base de datos del almacenamiento de datos.  

- Para sincronizar datos con la base de datos del almacén de datos, Configuration Manager usa la cuenta de equipo del rol de sistema de sitio. La cuenta requiere los permisos siguientes:  

    - **Administrator** en el equipo que hospeda la base de datos de almacenamiento de datos.  

    - **DB_Creator** en la base de datos del almacenamiento de datos.  

    - El permiso **DB_owner** o **DB_reader** con permisos de **ejecución**  para la base de datos de sitio de nivel superior.  

- La base de datos de almacenamiento de datos requiere el uso de SQL Server 2012 o una versión posterior. La edición puede ser Standard, Enterprise o Datacenter. No es necesario que la versión de SQL Server para el almacenamiento de datos sea la misma que la del servidor de base de datos del sitio.<!--SCCMDocs issue 662-->  

- La base de datos de almacenamiento admite las siguientes configuraciones de SQL Server:  

    - Una instancia con nombre o predeterminada  

    - Grupo de disponibilidad de SQL Server Always On  

    - Clúster de conmutación por error de SQL Server  

- Si usa [vistas distribuidas](../../plan-design/hierarchy/database-replication.md#bkmk_distviews), debe instalar el punto de servicio de almacenamiento de datos en el mismo servidor que hospeda la base de datos del sitio de administración central.  

Para obtener más información sobre las licencias de SQL Server, vea las [preguntas más frecuentes sobre productos y licencias](../../understand/product-and-licensing-faq.md). <!-- sms500967 -->

La base de datos de almacenamiento de datos debe tener el mismo tamaño que su base de datos de sitio. Aunque en un principio el almacenamiento de datos sea más pequeño, crecerá con el tiempo. <!--SCCMDocs issue 756-->



## <a name="install"></a>Instalar

Cada jerarquía admite una única instancia de este rol y puede encontrarse en cualquier sistema de sitio de ese sitio de nivel superior. El servidor SQL Server que hospeda la base de datos para el almacenamiento puede ser local para el rol de sistema de sitio o remoto. El almacenamiento de datos trabaja con el punto de servicios de informes instalado en el mismo sitio. No es necesario que instale los dos roles de sistema de sitio en el mismo servidor.   

Para instalar el rol, use el **Asistente para agregar roles de sistema de sitio** o el **Asistente para crear servidor de sistema de sitio**. Para más información, consulte [Instalación de roles de sistema de sitio para System Center Configuration Manager](../deploy/configure/install-site-system-roles.md). En la página **Selección de rol de sistema** del asistente, seleccione el rol **Punto de mantenimiento de almacenamiento de datos**. 

Cuando instala el rol, Configuration Manager crea la base de datos de almacenamiento de datos en la instancia de SQL Server que especifique. Si especifica el nombre de una base de datos existente, Configuration Manager no creará ninguna base de datos, sino que utilizará la que especifique. Este proceso es el mismo que cuando se [mueve la base de datos de almacén de datos a un nuevo servidor SQL](#move-the-database).


### <a name="configure-properties"></a>Configuración de propiedades

#### <a name="general-page"></a>Página general

- **Nombre de dominio completo de SQL Server**: Especifique el nombre de dominio completo (FQDN) del servidor que hospeda la base de datos del punto de servicio de almacenamiento de datos.  

- **Nombre de instancia de SQL Server, si corresponde**: Si no usa una instancia predeterminada de SQL Server, especifique la instancia con nombre.  

- **Nombre de la base de datos**: Especifique un nombre para la base de datos de almacenamiento de datos. Configuration Manager creará la base de datos de almacenamiento de datos con este nombre. Si especifica un nombre de base de datos que ya existe en la instancia de SQL Server, Configuration Manager usará esa base de datos.  

- **Puerto de SQL Server utilizado para la conexión**: Especifique el número de puerto TCP/IP que usa el servidor SQL Server que hospeda la base de datos del almacenamiento de datos. El servicio de sincronización del almacenamiento de datos usa este puerto para conectarse a la base de datos de dicho almacenamiento. De forma predeterminada, usa el puerto de SQL Server **1433** para la comunicación.  

- **Cuenta de punto de servicio de almacenamiento de datos**: a partir de la versión 1802, establezca el **nombre de usuario** que use la cuenta de SQL Server Reporting Services al conectarse a la base de datos de almacenamiento de datos.  


#### <a name="synchronization-schedule-page"></a>Página Programación de sincronización
*Se aplica a las versiones 1806 y anteriores*

- **Hora de inicio**: Especifique la hora a la que desea que se inicie la sincronización del almacenamiento de datos.  

- **Patrón de periodicidad**

    - **Diariamente**: permite especificar que la sincronización se ejecute cada día.  

    - **Semanalmente**: permite especificar un solo día cada semana, con una periodicidad semanal para la sincronización.


#### <a name="synchronization-settings-page"></a>Página Configuración de sincronización
*Se aplica a la versión 1810 y posteriores*

- **Configuración personalizada de sincronización de datos**: seleccione la opción para **Seleccionar tablas**. En la ventana Tablas de bases de datos, seleccione los nombres de tabla para sincronizar con la base de datos de almacenamiento de datos. Use el filtro para buscar por nombre o seleccione la lista desplegable para elegir grupos específicos. Haga clic en **Aceptar** cuando haya terminado, para guardar.  

    > [!Note]  
    > No se pueden quitar las tablas que el rol selecciona de forma predeterminada.  

- **Hora de inicio**: Especifique la hora a la que desea que se inicie la sincronización del almacenamiento de datos.  

- **Patrón de periodicidad**

    - **Diariamente**: permite especificar que la sincronización se ejecute cada día.  

    - **Semanalmente**: permite especificar un solo día cada semana, con una periodicidad semanal para la sincronización.



## <a name="reporting"></a>Generación de informes

Después de instalar un punto de servicio de almacenamiento de datos, varios informes pasan a estar disponibles en el punto de servicios de informes del sitio. Si instala el punto de servicio de almacenamiento de datos antes de instalar un punto de servicios de informes, los informes se agregan automáticamente cuando se instale posteriormente el punto de servicios de informes.

> [!WARNING]  
> A partir de la versión 1802, el punto de almacenamiento de datos es compatible con credenciales alternativas.<!--507334--> Si ha actualizado desde una versión anterior de Configuration Manager, debe especificar las credenciales que SQL Server Reporting Services usa para conectarse a la base de datos de almacenamiento de datos. Los informes de almacenamiento de datos no se abren si no agrega las credenciales. 
> 
> Para especificar una cuenta, establezca el **nombre de usuario** para la cuenta del punto de servicio de almacenamiento de datos en las propiedades del rol. Para obtener más información, vea [Configuración de propiedades](#configure-properties). 

El rol de sistema de sitio de almacenamiento de datos incluye los siguientes informes en la categoría **Almacenamiento de datos**:  

- **Implementación de aplicaciones - Histórico**: Vea los detalles de la implementación de aplicaciones para una máquina y una aplicación determinada.  

- **Endpoint Protection y cumplimiento de actualizaciones de software - Historial**: Vea los equipos a los que les faltan actualizaciones de software.  

- **Inventario de hardware general - Histórico**: Vea todo el inventario de hardware para un equipo específico.  

- **Inventario de software general - Histórico**: Vea todo el inventario de software para un equipo específico.  

- **Información general del mantenimiento de infraestructura - Histórico**: Muestra información general del mantenimiento de su infraestructura de Configuration Manager.  

- **Lista de malware detectado - Histórico**: Vea el malware que se ha detectado en la organización.  

- **Resumen de distribución de software - Histórico**: Un resumen de distribución de software para un equipo y anuncio específico.  



## <a name="site-expansion"></a>Expansión de sitios

Antes de instalar un sitio de administración central para expandir un sitio primario independiente existente, primero desinstale el rol de punto de servicio de almacenamiento de datos. Después de instalar el sitio de administración central, puede instalar el rol de sistema de sitio en el sitio de administración central.  

A diferencia de un movimiento de la base de datos del almacenamiento de datos, este cambio produce una pérdida de los datos históricos que se han sincronizado previamente en el sitio primario. No se admite la copia de seguridad de la base de datos desde el sitio principal y su restauración en el sitio de administración central.



## <a name="move-the-database"></a>Mover la base de datos

Use los siguientes pasos para mover la base de datos de almacenamiento de datos a un servidor de SQL Server nuevo:  

1. Use SQL Server Management Studio para realizar una copia de seguridad de la base de datos de almacenamiento de datos. A continuación, restaure esa base de datos a una instancia de SQL Server del nuevo equipo que hospeda el almacenamiento de datos.  

    > [!NOTE]  
    > Después de restaurar la base de datos en el nuevo servidor, asegúrese de que los permisos de acceso de la base de datos son los mismos en la nueva base de datos de almacenamiento de datos que en la base de datos de almacenamiento de datos original.  

2. Use la consola de Configuration Manager para quitar el rol del punto de servicio de almacenamiento de datos del servidor actual.  

3. Vuelva a instalar el punto de servicio de almacenamiento de datos. Especifique el nombre del nuevo servidor de SQL Server y de la instancia que hospeda la base de datos del almacenamiento de datos restaurada.  

4. Después de que se instale el rol de sistema de sitio, se completa el movimiento.  



## <a name="troubleshooting"></a>Solución de problemas 

### <a name="log-files"></a>Archivos de registro 

Use los siguientes registros para investigar problemas con la instalación del punto de servicio de almacenamiento de datos o con la sincronización de datos:

- **DWSSMSI.log** y **DWSSSetup.log**: use estos registros para investigar errores al instalar el punto de servicio de almacenamiento de datos.  

- **Microsoft.ConfigMgrDataWarehouse.log**: use este registro para investigar la sincronización de datos entre la base de datos del sitio y la base de datos de almacenamiento de datos.  


### <a name="set-up-failure"></a>Error de configuración 

Cuando el rol del punto de servicio de almacenamiento de datos es el primero que instala en un servidor remoto, se produce un error en la instalación para el almacenamiento de datos.  

#### <a name="workaround"></a>Solución alternativa 
Asegúrese de que el equipo en el que va a instalar el punto de servicio de almacenamiento de datos ya hospeda al menos otro rol.  


### <a name="synchronization-failed-to-populate-schema-objects"></a>Con la sincronización no se han rellenado los objetos de esquema 

La sincronización genera el siguiente mensaje de error en **Microsoft.ConfigMgrDataWarehouse.log**: `failed to populate schema objects`

#### <a name="workaround"></a>Solución alternativa 
Asegúrese de que la cuenta de equipo del rol de sistema de sitio es **db_owner** en la base de datos del almacenamiento de datos.


### <a name="reports-fail-to-open"></a>No se pueden abrir los informes

Los informes de almacenamiento de datos no se pueden abrir cuando la base de datos del almacenamiento de datos y el punto de servicio de informes se encuentran en diferentes sistemas de sitio.  

#### <a name="workaround"></a>Solución alternativa
Conceda a la **cuenta de punto de Reporting Services** el permiso **db_datareader** en la base de datos del almacenamiento de datos.


### <a name="error-opening-reports"></a>Error al abrir los informes

Al abrir un informe de almacenamiento de datos, se devuelve el siguiente el error:

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>Solución alternativa 
Siga los pasos que se indican a continuación para configurar certificados:

1. En el equipo que hospeda la base de datos del almacenamiento de datos:  

    1. Abra IIS, seleccione **Certificados de servidor** y después haga clic con el botón derecho en **Crear certificado autofirmado**. Después especifique el "nombre descriptivo" del nombre del certificado como **Certificado de identificación de SQL Server del almacenamiento de datos**. Seleccione el almacén de certificados como **Personal**.  

    2. Abra **Administrador de configuración de SQL Server**. En **Configuración de red de SQL Server**, haga clic con el botón derecho para seleccionar **Propiedades** en **Protocolos para MSSQLSERVER**. Cambie a la pestaña **Certificado**, seleccione **Certificado de identificación de SQL Server de almacenamiento de datos** como el certificado y luego guarde los cambios.  

    3. En **Administrador de configuración de SQL Server**, en **Servicios de SQL Server**, reinicie el **Servicio SQL Server**. Si SQL Reporting Services también está instalado en el servidor que hospeda la base de datos de almacén de datos, reinicie también **Reporting Services**.  

    4. Abra Microsoft Management Console (MMC) y agregue el complemento **Certificados**. Seleccione la **cuenta de equipo** del equipo local. Expanda la carpeta **Personal** y seleccione **Certificados**. Exporte el **Certificado de identificación de SQL Server de almacenamiento de datos** como un archivo **DER binario codificado X.509 (.CER)** .  

2. En el equipo que hospeda SQL Server Reporting Services, abra MMC y agregue el complemento **Certificados**. Seleccione **Cuenta de equipo**. En la carpeta **Entidades emisoras raíz de confianza**, importe el **Certificado de identificación de SQL Server de almacenamiento de datos**.  



## <a name="data-flow"></a>Flujo de datos   

![Diagrama que muestra el flujo de datos lógicos entre los componentes de sitio del almacenamiento de datos](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>Sincronización y almacenamiento de datos

| Paso   | Detalles  |
|--------|----------|  
| **1**  | El servidor de sitio transfiere y almacena datos en la base de datos del sitio. |  
| **2**  | Basándose en su programación y configuración, el punto de servicio de almacenamiento de datos obtiene datos de la base de datos del sitio. |  
| **3**  | El punto de servicio de almacenamiento de datos transfiere y almacena una copia de los datos sincronizados en la base de datos de almacenamiento de datos. |  


#### <a name="reporting"></a>Generación de informes

| Paso   | Detalles  |
|--------|----------|  
| **A**  | Mediante informes integrados, un usuario solicita datos. Esta solicitud se pasa al punto de servicios de informes mediante SQL Server Reporting Services. |  
| **B**  | La mayoría de los informes se refieren a información actual y estas solicitudes se ejecutan en la base de datos del sitio. |  
| **C**  | Cuando un informe solicita datos históricos, mediante uno de los informes con una *categoría* de **almacenamiento de datos**, la solicitud se ejecuta en la base de datos de almacenamiento de datos. |  
