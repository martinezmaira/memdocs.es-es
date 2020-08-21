---
title: Actualizar la infraestructura local
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo actualizar la infraestructura, como SQL Server y el sistema operativo de sistemas de sitio.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7efc775199a34a66a8cd4a83b85baccd4a3ab5cb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699490"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Actualizar la infraestructura local compatible con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la información de este artículo para ayudarle a actualizar la infraestructura del servidor que ejecuta Configuration Manager.  

- Si quiere *actualizar* desde una versión anterior a Configuration Manager, rama actual, vea [Actualizar a Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md).  

- Si quiere *actualizar* la infraestructura de Configuration Manager, rama actual, a una nueva versión, vea [Actualizaciones para Configuration Manager](updates.md).  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Actualización del sistema operativo de los sistemas de sitio  

Configuration Manager admite la actualización local del sistema operativo del servidor que hospeda un servidor de sitio y de cualquier rol de sistema de sitio en las situaciones siguientes:  

- Si Configuration Manager sigue admitiendo el nivel de Service Pack de Windows resultante, admite una actualización local a un Service Pack de Windows Server posterior.  

- Actualización local desde:  

    - Windows Server 2016 para Windows Server 2019  

    - Windows Server 2012 R2 para Windows Server 2019  

    - Windows Server 2012 R2 para Windows Server 2016  

    - Windows Server 2012 para Windows Server 2016  

    - Windows Server 2012 a Windows Server 2012 R2  

    - Windows Server 2008 R2 a Windows Server 2012 R2  

Para actualizar un servidor, use los procedimientos de actualización que proporciona el SO al que se va a actualizar. Vea los siguientes artículos:  

- [Windows Server Upgrade Center](https://aka.ms/upgradecenter)  

- [Upgrade and conversion options for Windows Server 2016](/windows-server/get-started/supported-upgrade-paths) (Opciones de actualización y conversión de Windows Server 2016)  

- [Upgrade Options for Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)) (Opciones de actualización de Windows Server 2012 R2)  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> Actualizar Windows Server 2016 o 2019

Use los pasos que se describen en esta sección para cualquiera de los escenarios de actualización siguientes:  

- Actualice Windows Server 2012 R2 o Windows Server 2016 a Windows Server 2019  

- Actualice Windows Server 2012 o Windows Server 2012 R2 a Windows Server 2016  

#### <a name="before-upgrade"></a>Antes de la actualización

- (Windows Server 2012 o Windows Server 2012 R2): Quite el cliente de System Center Endpoint Protection (SCEP). Ahora Windows Server tiene Windows Defender integrado, que reemplaza al cliente SCEP. La presencia del cliente SCEP puede impedir la actualización a Windows Server.  

- Quite el rol de WSUS del servidor si está instalado. Puede mantener el SUSDB y readjuntarlo una vez que se vuelva a instalar WSUS.  

- Si va a actualizar el sistema operativo del servidor de sitio, asegúrese de que la [replicación basada en archivos](../../plan-design/hierarchy/file-based-replication.md) es correcta para el sitio. Compruebe todas las bandejas de entrada en busca de trabajos pendientes, tanto en sitios de envío como en sitios de recepción. Si hay muchos trabajos de replicación bloqueados o pendientes, espere hasta que desaparezca.<!-- SCCMDocs#1792 -->
    - En el sitio de envío, revise el archivo **sender.log**.
    - En el sitio de recepción, revise el archivo **despooler.log**.

#### <a name="after-upgrade"></a>Después de la actualización

- Asegúrese de que Windows Defender está habilitado, establecido para el inicio automático y en ejecución.  

- Asegúrese de que se ejecutan los siguientes servicios de Configuration Manager:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Asegúrese de que los servicios de **activación de procesos de Windows** y de **WWW/W3svc** están habilitados y configurados para el inicio automático. El proceso de actualización deshabilita estos servicios, así que asegúrese de que se ejecuten en los siguientes roles de sistema de sitio:  

    - Servidor de sitio  

    - Punto de administración  

    - Punto de servicio web del catálogo de aplicaciones  

    - Punto de sitios web del catálogo de aplicaciones  

- Asegúrese de que cada servidor que hospeda un rol de sistema de sitio sigan cumpliendo todos los [requisitos previos](../../plan-design/configs/site-and-site-system-prerequisites.md). Por ejemplo, puede que tenga que volver a instalar BITS, WSUS, o configurar valores específicos de IIS.  

- Después de restaurar los requisitos previos que falten, reinicie el servidor una vez más para asegurarse de que los servicios se hayan iniciado y estén operativos.  

- Si va a actualizar el servidor de sitio primario, [ejecute un restablecimiento del sitio](modify-your-infrastructure.md#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problema conocido de consolas remotas de Configuration Manager

Después de actualizar el servidor de sitio o una instancia del proveedor de SMS, no podrá conectarse con la consola de Configuration Manager. Para evitar este problema, restaure de forma manual los permisos del grupo de **administradores de SMS** en WMI. Los permisos deben establecerse en el servidor de sitio y en cada servidor remoto que hospeda una instancia del proveedor de SMS:

1. En los servidores aplicables, abra Microsoft Management Console (MMC), agregue el complemento de **Control WMI** y, luego, seleccione **Equipo local**.  

2. En MMC, abra las **Propiedades** de **Control WMI (local)** y seleccione la pestaña **Seguridad**.  

3. Expanda el árbol por debajo de la raíz, seleccione el nodo **SMS** y, luego, elija **Seguridad**.  Asegúrese de que el grupo **Administradores de SMS** tiene los permisos siguientes:  

    - Habilitar cuenta  

    - Llamada remota habilitada  

4. En la pestaña **Seguridad**, en el nodo **SMS**, seleccione el nodo **sitio_&lt;CódigoDeSitio** y, después, elija **Seguridad**. Asegúrese de que el grupo **Administradores de SMS** tiene los permisos siguientes:  

    - Ejecutar métodos  

    - Escritura de proveedor  

    - Habilitar cuenta  

    - Llamada remota habilitada  

5. Guarde los permisos para restaurar el acceso de la consola de Configuration Manager.  

#### <a name="known-issue-for-remote-site-systems"></a>Problema conocido relativo a los sistemas de sitios remotos

Tras actualizar un servidor que aloja un sistema de sitio remoto, es posible que valor `Software\Microsoft\SMS` no figure en la siguiente clave del Registro: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`.

Si no aparece tras actualizar Windows en el servidor, agréguelo manualmente. De lo contrario, al cargar archivos a los buzones del servidor de sitio, puede haber problemas con los roles de los sistemas de sitios.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Actualizar Windows Server 2012 R2

Al hacer la actualización de Windows Server 2008 R2 o Windows Server 2012 a Windows Server 2012 R2, se aplican las condiciones siguientes:

#### <a name="before-upgrade"></a>Antes de la actualización

- En Windows Server 2012: Quite el rol de WSUS del servidor si está instalado. Puede mantener el SUSDB y readjuntarlo una vez que se vuelva a instalar WSUS.  

- En Windows Server 2008 R2: Antes de actualizar a Windows Server 2012 R2, debe desinstalar WSUS 3.2 del servidor. Puede mantener el SUSDB y readjuntarlo una vez que se vuelva a instalar WSUS. Para más información, vea [Windows Server Update Services Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality) (Introducción a Windows Server Update Services).  

- Si va a actualizar el sistema operativo del servidor de sitio, asegúrese de que la [replicación basada en archivos](../../plan-design/hierarchy/file-based-replication.md) es correcta para el sitio. Compruebe todas las bandejas de entrada en busca de trabajos pendientes, tanto en sitios de envío como en sitios de recepción. Si hay muchos trabajos de replicación bloqueados o pendientes, espere hasta que desaparezca.<!-- SCCMDocs#1792 -->
    - En el sitio de envío, revise el archivo **sender.log**.
    - En el sitio de recepción, revise el archivo **despooler.log**.

#### <a name="after-upgrade"></a>Después de la actualización

- El proceso de actualización deshabilita los servicios de implementación de Windows. Asegúrese de que este servicio se inicia y ejecuta en los siguientes roles de sistema de sitio:  

    - Servidor de sitio  

    - Punto de administración  

    - Punto de servicio web del catálogo de aplicaciones  

    - Punto de sitios web del catálogo de aplicaciones  

- Asegúrese de que los servicios de **activación de procesos de Windows** y de **WWW/W3svc** están habilitados y configurados para el inicio automático. El proceso de actualización deshabilita estos servicios, así que asegúrese de que se ejecuten en los siguientes roles de sistema de sitio:  

    - Servidor de sitio  

    - Punto de administración  

    - Punto de servicio web del catálogo de aplicaciones  

    - Punto de sitios web del catálogo de aplicaciones  

- Asegúrese de que cada servidor que hospeda un rol de sistema de sitio sigan cumpliendo todos los [requisitos previos](../../plan-design/configs/site-and-site-system-prerequisites.md). Por ejemplo, puede que tenga que volver a instalar BITS, WSUS, o configurar valores específicos de IIS.  

    Después de restaurar los requisitos previos que falten, reinicie el servidor una vez más para asegurarse de que los servicios se hayan iniciado y estén operativos.  

### <a name="unsupported-upgrade-scenarios"></a>Escenarios de actualización no compatibles

Con frecuencia, se pregunta sobre los siguientes escenarios de actualización de Windows Server, pero no son compatibles con Configuration Manager:  

- Windows Server 2008 a Windows Server 2012 o posterior  

- Windows Server 2008 R2 a Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Actualizar el sistema operativo de los clientes  

Configuration Manager admite una actualización local del SO para los clientes de Configuration Manager en las situaciones siguientes:  

- Si Configuration Manager admite el nivel de Service Pack resultante, admite una actualización local a un Service Pack de Windows posterior.  

- Actualización inmediata de Windows desde una versión compatible a Windows 10. Para más información, consulte [Actualizar Windows a la versión más reciente](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Actualizaciones de mantenimiento desde una compilación a otra de Windows 10. Para obtener más información, consulte [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md) (Administrar Windows como servicio).  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> Actualizar SQL Server  

Configuration Manager admite una actualización local de SQL Server en el servidor de base de datos del sitio.

Para más información sobre las versiones de SQL Server compatibles con Configuration Manager, consulte [Versiones de SQL Server compatibles con System Center Configuration Manager](../../plan-design/configs/support-for-sql-server-versions.md).  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Actualizar la versión del Service Pack de SQL Server

Si Configuration Manager sigue admitiendo el nivel de Service Pack resultante de SQL Server, admite la actualización local de SQL Server a un Service Pack posterior.

Si tiene más de un sitio de Configuration Manager en una jerarquía, cada sitio puede ejecutar una versión de Service Pack de SQL Server diferente. No hay ninguna limitación en el orden en el que los sitios actualizan la versión del Service Pack de SQL Server.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Actualización a una nueva versión de SQL Server

Configuration Manager es compatible con la actualización local de SQL Server a las siguientes versiones:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Esto incluye la actualización de SQL Server Express a una versión más reciente en los sitios secundarios.

Al actualizar la versión de SQL Server que hospeda la base de datos de sitio, debe actualizar la versión de SQL Server que se usa en los sitios en el siguiente orden:

1. Actualice primero SQL Server en el sitio de administración central.  

2. Actualice los sitios secundarios antes de actualizar un sitio primario principal de un sitio secundario.  

3. Actualice los sitios primarios principales en último lugar. Estos sitios incluyen tanto los sitios primarios secundarios, que informan a un sitio de administración central, como los sitios primarios independientes, que están en el sitio de nivel superior de una jerarquía.  

### <a name="sql-server-cardinality-estimation-level"></a>Nivel de estimación de cardinalidad de SQL Server

Al actualizar una base de datos del sitio a partir de una versión anterior de SQL Server, la base de datos conserva su nivel existente de estimación de cardinalidad (CE) de SQL si se encuentra en el mínimo permitido para esa instancia de SQL Server. La actualización de SQL Server con una base de datos en un nivel de compatibilidad inferior al nivel permitido establece automáticamente la base de datos en el nivel de compatibilidad más bajo que permite SQL Server.

En la tabla siguiente se identifican los niveles de compatibilidad recomendados para las bases de datos del sitio de Configuration Manager:

|Versión de SQL Server | Niveles de compatibilidad admitidos | Nivel recomendado |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Para identificar el nivel de compatibilidad de la estimación de cardinalidad de SQL Server en uso para la base de datos del sitio, ejecute la siguiente consulta SQL en el servidor de base de datos del sitio:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

Para obtener más información sobre los niveles de compatibilidad de CE de SQL y cómo establecerlos, consulte [Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).

Para más información sobre la actualización de SQL Server, consulte los siguientes artículos de SQL Server:  

- [Actualización a SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Actualización a SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Actualización a SQL Server 2014](/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para actualizar SQL Server en el servidor de base de datos del sitio  

1. Detenga todos los servicios de Configuration Manager del sitio.  

2. Actualice SQL Server a una versión compatible.  

3. Reinicie los servicios de Configuration Manager.  

> [!NOTE]  
> Cuando cambia la edición de SQL Server en uso en el sitio de administración central de Standard a Enterprise o Datacenter, la partición de la base de datos no cambia. Esta partición de la base de datos limita el número de clientes que admite la jerarquía.