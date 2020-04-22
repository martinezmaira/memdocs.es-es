---
title: Modificación de la infraestructura
titleSuffix: Configuration Manager
description: Realice cambios o adopte medidas que afectan a la infraestructura de Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694363"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Modificar la infraestructura de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de instalar uno o varios sitios, es posible que deba modificar las configuraciones o realizar acciones que afecten a la infraestructura.

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a> Administración del proveedor de SMS

El proveedor de SMS proporciona el punto de contacto administrativo para una o varias consolas de Configuration Manager. Al instalar varios proveedores de SMS, puede proporcionar redundancia a los puntos de contacto para administrar el sitio y la jerarquía.

En cada sitio de Configuration Manager, puede volver a ejecutar el programa de instalación para:

- Agregar una instancia adicional del proveedor de SMS. Cada instancia adicional del proveedor de SMS debe estar en un equipo independiente.

- Eliminar una instancia del proveedor de SMS. Para quitar el último proveedor de SMS en un sitio, debe desinstalar el sitio.

Para supervisar la instalación o la eliminación del proveedor de SMS, consulte el archivo **ConfigMgrSetup.log** en la carpeta raíz del servidor del sitio en el que ha ejecutado el programa de instalación.

Antes de modificar el proveedor de SMS en un sitio, consulte el [Plan para el proveedor de SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md).

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>Administración de la configuración del proveedor de SMS para un sitio  

1. Ejecute el **programa de instalación de Configuration Manager** desde `\BIN\X64\setup.exe` en la carpeta de instalación del sitio de Configuration Manager.

1. En la página **Primeros pasos**, seleccione **Realizar mantenimiento de sitio o restablecer este sitio**.

1. En la página **Mantenimiento del sitio**, seleccione **Modify SMS provider configuration** (Modificar configuración del proveedor de SMS).

1. En la página **Administrar proveedores de SMS**, seleccione una de las siguientes opciones:

    - **Agregue un nuevo proveedor de SMS**: especifique el FQDN de un equipo para hospedar el proveedor de SMS que actualmente no hospeda.

    - **Desinstale el proveedor de SMS especificado**: seleccione el nombre del equipo del que quiere quitar el proveedor de SMS.

    > [!TIP]  
    > Para trasladar el proveedor de SMS entre dos equipos, primero instálelo en el nuevo equipo. Después, quítelo de la ubicación original. No existe ninguna opción para trasladar el proveedor de SMS entre equipos.

Cuando finalice el Asistente para instalación, se completará la configuración del proveedor de SMS. En las **Propiedades** del sitio, en la pestaña **General**, compruebe los equipos que tienen un proveedor de SMS instalado para el sitio.

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a> Administración de la consola de Configuration Manager

Las tareas siguientes le ayudarán a administrar la consola de Configuration Manager:

- Para modificar el idioma que se muestra en la consola de Configuration Manager, consulte la sección [Administración del idioma de la consola de Configuration Manager](#BKMK_ManageConsoleLanguages).

- Para instalar más consolas, vea [Instalación de la consola de Configuration Manager](../deploy/install/install-consoles.md).

- Para configurar los permisos de DCOM para habilitar consolas remotas desde el servidor de sitio, consulte la sección [Configuración de permisos de DCOM para consolas remotas de Configuration Manager](#BKMK_ConfigDCOMforRemoteConsole).

- Para modificar los permisos administrativos a fin de limitar lo que los usuarios pueden ver y hacer en la consola, consulte [Modificar el ámbito administrativo de un usuario administrativo](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser).

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a> Administración del idioma de la consola de Configuration Manager

Durante la instalación del servidor de sitio, los archivos de instalación de la consola de Configuration Manager y los paquetes de idioma compatibles con el sitio se copian en la subcarpeta `\Tools\ConsoleSetup` de la ruta de instalación de Configuration Manager en el servidor de sitio.

- Cuando inicia la instalación de la consola de Configuration Manager desde esta carpeta en el servidor de sitio, la consola de Configuration Manager y los archivos de paquetes de idioma admitidos se copian en el equipo.

- Cuando un paquete de idioma está disponible para la configuración de idioma actual del equipo, la consola de Configuration Manager se abre en dicho idioma.

- Si el paquete de idioma asociado no está disponible para la consola de Configuration Manager, esta se abre en inglés (Estados Unidos).

Por ejemplo, imagine que instala la consola de Configuration Manager desde un servidor de sitio que admite inglés, alemán y francés. Si abre la consola de Configuration Manager en un equipo con francés como idioma configurado, la consola se abre en francés. Si abre la consola de Configuration Manager en un equipo con japonés como idioma configurado, la consola se abre en inglés porque el paquete de idioma japonés no está disponible.  

Cada vez que se abre la consola de Configuration Manager:

- Determina el idioma configurado para el equipo.
- Comprueba si hay un paquete de idioma asociado disponible para la consola de Configuration Manager.
- Abre la consola con el paquete de idioma adecuado.

Si opta por abrir la consola de Configuration Manager en inglés, independientemente del idioma configurado en el equipo, quite los archivos del paquete de idioma del equipo, o bien cámbieles el nombre.

Utilice los siguientes procedimientos para iniciar la consola de Configuration Manager en inglés, independientemente de la configuración regional establecida en el equipo.  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Instalación de la versión solo en inglés de la consola de Configuration Manager en equipos  

1. En el Explorador de Windows, vaya a `\Tools\ConsoleSetup\LanguagePack` en la ruta de instalación de Configuration Manager.

1. Cambie el nombre de los archivos **.msp** y **.mst** . Por ejemplo, puede cambiar **&lt;nombre archivo\>.MSP** a **&lt;nombre archivo\>.MSP.deshabilitado**.

1. Instale la consola de Configuration Manager en el equipo.

    > [!IMPORTANT]
    > Cuando se configuran idiomas de servidor nuevos para el servidor de sitio, los archivos .msp y .mst se copian de nuevo en la carpeta **LanguagePack**. Debe repetir este procedimiento cada vez que instala una consola de Configuration Manager solo en inglés.  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Deshabilitación temporal de un idioma de la consola en una instalación de la consola de Configuration Manager

1. En el equipo que ejecuta la consola de Configuration Manager, cierre la consola de Configuration Manager.

1. En el Explorador de Windows, examine &lt;*ConsoleInstallationPath*>\Bin\ en el equipo de la consola de Configuration Manager.  

1. Cambie el nombre de la carpeta de idioma del idioma que está configurado en el equipo. Por ejemplo, si el idioma configurado para el equipo era el alemán, puede cambiar el nombre de la carpeta **de** a **de.deshabilitado**.  

1. Para abrir la consola de Configuration Manager en el idioma configurado para el equipo, cambie el nombre de la carpeta al nombre original. Por ejemplo, cambie el nombre de **de.dehabilitado** a **de**.  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configuración de permisos de DCOM para consolas remotas

La cuenta de usuario que ejecuta la consola de Configuration Manager requiere permiso para acceder a la base de datos del sitio mediante el proveedor de SMS. Sin embargo, un usuario administrativo que usa una consola remota de Configuration Manager también requiere permisos de DCOM de **Activación remota** en:

- El equipo de servidor de sitio

- Cada equipo que hospede una instancia del proveedor de SMS

El grupo de seguridad denominado **Administradores de SMS** concede acceso al proveedor de SMS en un equipo y también puede usarse para conceder los permisos de DCOM necesarios. Este grupo es local en el equipo cuando el proveedor de SMS se ejecuta en un servidor miembro. Es un grupo local de dominio cuando el proveedor de SMS se ejecuta en un controlador de dominio.

> [!IMPORTANT]
> La consola de Configuration Manager usa WMI para conectarse con el proveedor de SMS, y WMI usa internamente DCOM. Si la consola de Configuration Manager se ejecuta en un equipo distinto del equipo del proveedor de SMS, requiere permisos para activar un servidor de DCOM en el equipo del proveedor de SMS. De forma predeterminada, la activación remota solo se concede a los miembros del grupo de administradores integrados.
>
> Si permite que el grupo de administradores de SMS tenga el permiso de activación remota, un miembro de este grupo podría intentar ataques de DCOM contra el equipo del proveedor de SMS. Esta configuración también aumenta la superficie expuesta a ataques del equipo. Para mitigar esta amenaza, debe supervisar cuidadosamente la pertenencia al grupo de administradores de SMS.

Use el procedimiento siguiente para configurar cada sitio de administración central (CAS), servidor de sitio primario y cada equipo en donde está instalado el proveedor de SMS para conceder acceso remoto a la consola de Configuration Manager a usuarios administrativos.

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Configuración de permisos de DCOM para conexiones remotas de la consola de Configuration Manager

1. Como administrador del equipo de destino, ejecute `Dcomcnfg.exe` para abrir **Servicios de componentes**.

1. Expanda **Servicios de componentes**, expanda **Equipos** y seleccione **Mi PC**. En el menú **Acción**, seleccione **Propiedades**.

1. En la ventana de **Propiedades de Mi PC**, cambie a la pestaña **Seguridad COM**. En la sección **Permisos de inicio y activación**, seleccione **Editar límites**.

1. En la ventana **Permisos de inicio y activación**, seleccione **Agregar**.

1. En la ventana **Select Users, Computers, Service Accounts, or Groups** (Seleccionar usuarios, equipos, cuentas de servicio o grupos), en el campo **Escriba los nombres de objeto que desea seleccionar**, escriba `SMS Admins` y seleccione **Aceptar**.

   > [!TIP]
   > Para ubicar el grupo de administradores de SMS, es posible que tenga que cambiar la configuración de **Desde esta ubicación**. Este grupo es local en el equipo cuando el proveedor de SMS se ejecuta en un servidor miembro, y es un grupo local de dominio cuando el proveedor de SMS se ejecuta en un controlador de dominio.

1. En la sección **Permisos para administradores de SMS**, para permitir la activación remota, seleccione la columna **Permitir** para la fila **Activación remota**.

1. Seleccione **Aceptar** para guardar los cambios y cerrar todas las ventanas.

El equipo ya está configurado para permitir el acceso remoto a la consola de Configuration Manager a los miembros del grupo de administradores de SMS.

Repita este procedimiento en cada equipo del proveedor de SMS que pueda admitir consolas remotas de Configuration Manager.

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a> Modificación de la configuración de la base de datos del sitio

Después de instalar un sitio, puede modificar la configuración de la base de datos del sitio y el servidor de base de datos del sitio. Ejecute el programa de instalación de Configuration Manager en un servidor CAS o en un servidor de sitio primario para realizar cambios. Puede mover la base de datos del sitio a una nueva instancia de SQL Server en el mismo equipo o a otro equipo que ejecute una versión compatible de SQL Server. Estos cambios no se admiten para la configuración de la base de datos en sitios secundarios.

Para obtener más información acerca de los límites de compatibilidad, consulte [Directiva de soporte técnico para los cambios de la base de datos manualmente en un entorno de Configuration Manager](https://support.microsoft.com/kb/3106512).  

> [!NOTE]
> Al modificar la configuración de la base de datos de un sitio, Configuration Manager reinicia o vuelve a instalar servicios de Configuration Manager en el servidor de sitio y en servidores de sistema de sitio remoto que se comunican con la base de datos.

### <a name="modify-the-database-configuration"></a>Modificación de la configuración de la base de datos

Ejecute el programa de instalación de Configuration Manager en el servidor de sitio y seleccione la opción **Realizar mantenimiento de sitio o restablecer este sitio**. Después, seleccione la opción **Modificar configuración de SQL Server**. Puede cambiar las siguientes configuraciones de base de datos del sitio:

- El servidor basado en Windows que aloja la base de datos.

- La instancia de SQL Server en uso en un servidor que aloja la base de datos de SQL Server.

- Nombre de la base de datos.

- Puerto de SQL Server en uso por Configuration Manager.

- Puerto de SQL Server Service Broker en uso por Configuration Manager.

### <a name="move-the-site-database"></a>Traslado de la base de datos del sitio

Si mueve la base de datos del sitio, revise también la configuración siguiente:

- Si mueve la base de datos del sitio a un nuevo equipo, agregue la cuenta de equipo del servidor del sitio al grupo **Administradores locales** del equipo que ejecuta SQL Server. Si usa un clúster de SQL Server para la base de datos del sitio, agregue la cuenta de equipo al grupo **Administradores locales** de cada equipo de nodo de clúster de Windows Server.

- Al mover la base de datos a una nueva instancia de SQL Server, o a un nuevo equipo de SQL Server, habilite la integración con Common Language Runtime (CLR). Use **SQL Server Management Studio** para conectarse a la instancia de SQL Server que hospeda la base de datos del sitio. Después, ejecute el siguiente procedimiento almacenado como una consulta: `sp_configure 'clr enabled',1; reconfigure`.

- Asegúrese de que el nuevo servidor de SQL Server tiene acceso a la ubicación de copia de seguridad. Cuando use una ruta UNC para almacenar la copia de seguridad de base de datos del sitio, después de mover la base de datos a un nuevo servidor, asegúrese de que la cuenta de equipo del nuevo servidor de SQL Server tiene permisos de **escritura** en la ubicación UNC. Esta configuración incluye el movimiento a un grupo de disponibilidad AlwaysOn de SQL Server o a un clúster de SQL Server.

> [!IMPORTANT]
> Antes de mover una base de datos que tenga una o más réplicas de base de datos para puntos de administración, quite las réplicas de la base de datos. Después de completar el traslado de la base de datos, se pueden reconfigurar las réplicas de la base de datos. Para obtener más información, vea [Réplicas de bases de datos para puntos de administración ](../deploy/configure/database-replicas-for-management-points.md).

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a> Administración del SPN para el servidor de base de datos del sitio

Puede elegir la cuenta que ejecuta los servicios de SQL para la base de datos del sitio:

- Cuando los servicios se ejecutan con la cuenta de sistema del equipo, el nombre de entidad de seguridad de servicio (SPN) se registra automáticamente.

- Cuando los servicios se ejecutan con una cuenta de usuario local de dominio, deberá registrar manualmente el SPN. El SPN permite que los clientes SQL y otros sistemas de sitio se autentiquen con Kerberos. Sin la autenticación Kerberos, podrían producirse errores de comunicación con la base de datos.

Para obtener más información sobre los SPN y las conexiones con Kerberos, consulte [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections).

Registre un SPN para la cuenta de servicio SQL Server del servidor de base de datos del sitio mediante la herramienta **Setspn**. Ejecute Setspn como administrador de dominio en un equipo del mismo dominio que SQL Server.

Los procedimientos siguientes son ejemplos de cómo administrar el SPN para la cuenta de servicio de SQL Server. Para obtener más información sobre Setspn, consulte [Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\)).

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>Creación manual de un SPN de usuario de dominio para la cuenta de servicio de SQL Server

1. Abra un símbolo del sistema como administrador.

1. Escriba un comando válido para crear el SPN para el nombre NetBIOS y el FQDN:

    > [!IMPORTANT]
    > Cuando cree un SPN para SQL Server en clúster, especifique el nombre virtual del clúster de SQL Server como el nombre de equipo de SQL Server.

    - Nombre NetBIOS: `setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        Por ejemplo: `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - FQDN: `setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        Por ejemplo: `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > El comando para registrar un SPN para una instancia con nombre de SQL Server es el mismo que se usa para registrar un SPN para una instancia predeterminada. La única excepción es que el número de puerto debe coincidir con el puerto usado por la instancia con nombre.

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>Comprobación de si el SPN de usuario de dominio está registrado correctamente

1. Abra un símbolo del sistema como administrador.

1. Escriba este comando: `setspn -L <domain\SQL service account>`

    Por ejemplo: `setspn -L contoso\sqlservice`

1. Revise el **ServicePrincipalName** que se ha registrado. Asegúrese de que ha creado un SPN válido para SQL Server.

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Cambio de la cuenta de servicio de SQL Server de sistema local a una cuenta de usuario de dominio

1. Cree o seleccione una cuenta de usuario de sistema local o de dominio que desee utilizar como cuenta de servicio de SQL Server.

1. Abra **Administrador de configuración de SQL Server**.

1. Seleccione **Servicios de SQL Server** y abra **SQL Server&lt;NOMBRE DE INSTANCIA\>** .

1. Cambie a la pestaña **Iniciar sesión**. Seleccione **Esta cuenta** y escriba el nombre de usuario y la contraseña de la cuenta de usuario de dominio del paso 1.

1. Confirme el cambio de la cuenta de servicio y reinicie el servicio SQL Server.

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a> Ejecutar un restablecimiento de sitio

Cuando se ejecuta un restablecimiento de sitio en un sitio primario o CAS, el sitio:

- Vuelve a aplicar los permisos de registro y archivo de Configuration Manager predeterminados.

- Reinstala todos los componentes y roles del sistema de sitio.

Los sitios secundarios no admiten un restablecimiento de sitio.

Puede restablecer manualmente un sitio. También pueden ejecutarse automáticamente después de modificar la configuración del sitio. Por ejemplo:

- Si se ha producido un cambio en las cuentas usadas por los componentes de Configuration Manager, considere la posibilidad de realizar un restablecimiento de sitio manual. Esta acción garantiza que los componentes del sitio se actualicen para usar los detalles de la nueva cuenta.

- Si modifica los idiomas de cliente o servidor en un sitio, Configuration Manager ejecuta automáticamente un restablecimiento de sitio. El sitio requiere un restablecimiento para usar los nuevos idiomas.

> [!NOTE]
> Un restablecimiento de sitio no restablece los permisos de acceso a objetos que no son de Configuration Manager.

### <a name="what-happens-during-a-site-reset"></a>¿Qué sucede durante un restablecimiento de sitio?

Cuando se ejecuta un restablecimiento de sitio:

1. El programa de instalación se detiene y reinicia el servicio **SMS_SITE_COMPONENT_MANAGER** y los componentes de subproceso del servicio **SMS_EXECUTIVE** .

1. El programa de instalación quita y vuelve a crear la carpeta de recurso compartido del sistema de sitio y el componente **SMS Executive** en el equipo local y en los equipos de sistema de sitio remoto.

1. El programa de instalación reinicia el servicio **SMS_SITE_COMPONENT_MANAGER**, que instala los servicios **SMS_EXECUTIVE** y **SMS_SQL_MONITOR**.

El restablecimiento de sitio restaura los objetos siguientes:

- Las claves del Registro **SMS** o **NAL** y todas las subclaves predeterminadas bajo estas claves.

- El árbol de directorio de archivos de Configuration Manager y los archivos o subdirectorios predeterminados en este árbol de directorio de archivos.

### <a name="prerequisites-for-site-reset"></a>Requisitos previos para el restablecimiento de sitio

La cuenta que use para el restablecimiento de sitio deberá tener los permisos siguientes:

- Para restablecer el CAS:

  - Un **Administrador local** en el servidor de CAS.

  - Privilegios equivalentes al rol de seguridad **Administrador total** de administración basada en roles.

- Para restablecer un sitio primario:

  - Un **Administrador local** en el servidor de sitio primario.

  - Privilegios equivalentes al rol de seguridad **Administrador total** de administración basada en roles.
  
  - Si el sitio primario está en una jerarquía con un CAS, esta cuenta también debe ser un **Administrador local** en el servidor de CAS.

### <a name="limitations-for-a-site-reset"></a>Limitaciones para un restablecimiento del sitio

Si la jerarquía está configurada para admitir la [prueba de actualizaciones de cliente en una recopilación de preproducción](../../clients/manage/upgrade/test-client-upgrades.md), no puede usar un restablecimiento del sitio para cambiar los paquetes de idioma de servidor o cliente de los sitios.

### <a name="run-a-site-reset"></a>Ejecutar un restablecimiento de sitio

1. Inicie el programa de instalación de Configuration Manager en el servidor de sitio mediante uno de los métodos siguientes:

    - En el menú **Inicio**, seleccione **Programa de instalación de Configuration Manager**.

    - En el directorio de *medios de instalación* de Configuration Manager, abra `\SMSSETUP\BIN\X64\setup.exe`. Asegúrese de que esta versión sea la misma que la versión del sitio.

    - En el directorio en el que está *instalado* Configuration Manager, abra `\BIN\X64\setup.exe`.

1. En la página **Primeros pasos**, seleccione **Realizar mantenimiento de sitio o restablecer este sitio**.

1. En la página **Mantenimiento del sitio**, seleccione **Reset site with no configuration changes** (Restablecer el sitio sin cambios de configuración).

1. Seleccione **Sí** para iniciar el restablecimiento de sitio.

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a> Administración de paquetes de idioma en un sitio

Después de instalar un sitio, puede cambiar los paquetes de idioma de servidor y cliente que se usan.

### <a name="server-language-packs"></a>Paquetes de idioma de servidor

*Se aplica a: Instalaciones de la consola de Configuration Manager, nuevas instalaciones de roles de sistema de sitio aplicables*

Después de actualizar los paquetes de idioma de servidor en un sitio, puede agregar compatibilidad para los paquetes de idioma en consolas de Configuration Manager.

Para agregar compatibilidad con un paquete de idioma de servidor en una consola de Configuration Manager, instale la consola de Configuration Manager desde la carpeta **ConsoleSetup** en un servidor de sitio que incluya el paquete de idioma que quiere usar. Si la consola de Configuration Manager ya está instalada, desinstálela para permitir que la nueva instalación identifique la lista actual de paquetes de idioma admitidos.

### <a name="client-language-packs"></a>Paquetes de idioma de cliente

Los cambios en los paquetes de idioma de cliente actualizan los archivos de origen de instalación de cliente. Las nuevas instalaciones y actualizaciones de cliente agregan compatibilidad con la lista actualizada de idiomas de cliente.

Después de actualizar los paquetes de idioma de cliente en un sitio, instale cada cliente que usará los paquetes de idioma mediante los archivos de origen que incluyen los paquetes de idioma de cliente.

Para obtener más información sobre los idiomas de cliente y servidor compatibles con Configuration Manager, vea [Paquetes de idioma](../deploy/install/language-packs.md).

### <a name="modify-the-supported-language-packs-at-a-site"></a>Modificación de los paquetes de idioma compatibles en un sitio

1. Inicie el programa de instalación de Configuration Manager en el servidor de sitio mediante uno de los métodos siguientes:

    - En el menú **Inicio**, seleccione **Programa de instalación de Configuration Manager**.

    - En el directorio de *medios de instalación* de Configuration Manager, abra `\SMSSETUP\BIN\X64\setup.exe`. Asegúrese de que esta versión sea la misma que la versión del sitio.

    - En el directorio en el que está *instalado* Configuration Manager, abra `\BIN\X64\setup.exe`.

1. En la página **Primeros pasos**, seleccione **Realizar mantenimiento de sitio o restablecer este sitio**.

1. En la página **Mantenimiento del sitio**, seleccione **Modify language configuration** (Modificar la configuración de idioma).

1. En la página **Requisitos previos**, seleccione una de las siguientes opciones:

    - **Download required files** (Descargar los archivos requeridos): adquiera actualizaciones de paquetes de idioma.

    - **Use previously downloaded files** (Usar archivos descargados anteriormente): use archivos descargados anteriormente que incluyan los paquetes de idioma que quiere agregar al sitio.

1. En la página **Selección de idioma de servidor**, seleccione los idiomas de servidor que admite el sitio.

1. En la página **Selección de idioma de cliente**, seleccione los idiomas de cliente que admite el cliente.

1. Complete el asistente para modificar la compatibilidad de idioma en el sitio.

    > [!NOTE]
    > Configuration Manager inicia un restablecimiento del sitio. Este proceso vuelve a instalar todos los roles de sistema de sitio en el sitio.

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a> Modificación del umbral de alerta del servidor de bases de datos

De forma predeterminada, Configuration Manager genera alertas cuando en un servidor de base de datos de sitio queda poco espacio libre en disco:

- Se genera una advertencia cuando el espacio libre en disco es de 10 GB o menos.
- Se genera una alerta crítica cuando el espacio libre en disco es de 5 GB o menos.

Puede modificar estos valores o deshabilitar las alertas para cada sitio:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.

1. Seleccione el sitio que quiere configurar. En la cinta, seleccione **Propiedades**.

1. Cambie a la pestaña **Alerta** y edite la configuración.

## <a name="uninstall-sites-and-hierarchies"></a>Desinstalar sitios y jerarquías

Es posible que tenga que desinstalar un rol de sistema de sitio, un sitio o una jerarquía de Configuration Manager. Para obtener más información, vea [Desinstalación de roles, sitios y jerarquías](../deploy/install/uninstall-sites-and-hierarchies.md).

A partir de la versión 2002, también puede quitar el CAS de una jerarquía, pero debe conservar el sitio primario. Para obtener más información, vea [Eliminación del CAS](../deploy/install/remove-central-administration-site.md).
