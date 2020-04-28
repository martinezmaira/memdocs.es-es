---
title: Cuentas utilizadas
titleSuffix: Configuration Manager
description: Identifique y administre los grupos y las cuentas de Windows y los objetos de SQL que se usan en Configuration Manager.
ms.date: 10/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6808fed9fa9aaf894e3975066eb7707880b7948
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073422"
---
# <a name="accounts-used-in-configuration-manager"></a>Cuentas que se usan en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la información siguiente para identificar las cuentas y los grupos de Windows y los objetos de SQL que se usan en Configuration Manager, cómo se usan y cualquier requisito.  

- [Grupos de Windows que crea y usa Configuration Manager](#bkmk_groups)  
  - [ConfigMgr_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [ConfigMgr_DViewAccess](#configmgr_dviewaccess)  
  - [Usuarios del control remoto de ConfigMgr](#configmgr-remote-control-users)  
  - [Administradores de SMS](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_&lt;código_de_sitio\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;código_de_sitio\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;código_de_sitio\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_&lt;código_de_sitio\>](#bkmk_filerepl)  

- [Cuentas que usa Configuration Manager](#bkmk_accounts)
  - [Cuenta de detección de grupos de Active Directory](#active-directory-group-discovery-account)  
  - [Cuenta de detección de sistemas de Active Directory](#active-directory-system-discovery-account)  
  - [Cuenta de detección de usuarios de Active Directory](#active-directory-user-discovery-account)  
  - [Cuenta de bosque de Active Directory](#active-directory-forest-account)  
  - [Cuenta de punto de registro de certificado](#certificate-registration-point-account)  
  - [Cuenta de captura de imagen de sistema operativo](#capture-os-image-account)  
  - [Cuenta de instalación de inserción de cliente](#client-push-installation-account)  
  - [Cuenta de conexión de punto de inscripción](#enrollment-point-connection-account)  
  - [Cuenta de conexión de Exchange Server](#exchange-server-connection-account)  
  - [Cuenta de conexión del punto de administración](#management-point-connection-account)  
  - [Cuenta de conexión de multidifusión](#multicast-connection-account)  
  - [Cuenta de acceso a la red](#network-access-account)  
  - [Cuenta de acceso de paquetes](#package-access-account)  
  - [Cuenta de punto de Reporting Services](#reporting-services-point-account)  
  - [Cuentas de visores permitidos de herramientas remotas](#remote-tools-permitted-viewer-accounts)  
  - [Cuenta de instalación del sitio](#site-installation-account)
  - [Cuenta de instalación del sistema de sitio](#site-system-installation-account)  
  - [Cuenta de servidor proxy de sistema de sitio](#site-system-proxy-server-account)  
  - [Cuenta de conexión del servidor SMTP](#smtp-server-connection-account)  
  - [Cuenta de conexión de punto de actualización de software](#software-update-point-connection-account)  
  - [Cuenta de sitio de origen](#source-site-account)  
  - [Cuenta de base de datos del sitio de origen](#source-site-database-account)  
  - [Cuenta de unión de dominio de secuencia de tareas](#task-sequence-domain-join-account)  
  - [Cuenta de conexión de carpeta de red de secuencia de tareas](#task-sequence-network-folder-connection-account)  
  - [Cuenta de ejecución de secuencia de tareas](#task-sequence-run-as-account)  

- [Objetos de usuario que Configuration Manager usa en SQL](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Roles de base de datos que Configuration Manager usa en SQL](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a> Grupos de Windows que crea y usa Configuration Manager  

Configuration Manager crea automáticamente y, en muchos casos, mantiene automáticamente los siguientes grupos de Windows:  

> [!NOTE]  
> Cuando Configuration Manager crea un grupo en un equipo que es miembro del dominio, el grupo es un grupo de seguridad local. Si el equipo es un controlador de dominio, el grupo es un grupo local de dominio. Este tipo de grupo se comparte entre todos los controladores de dominio del dominio.  


### <a name="configmgr_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a> ConfigMgr_CollectedFilesAccess

Configuration Manager usa este grupo para conceder acceso para ver los archivos recopilados por el inventario de software.  

Para obtener más información, vea [Introducción al inventario de software](../../clients/manage/inventory/introduction-to-software-inventory.md).

#### <a name="type-and-location"></a>Tipo y ubicación
Este grupo es un grupo de seguridad local creado en el servidor de sitio primario.

Cuando se desinstala un sitio, este grupo no se quita automáticamente. Elimínelo de forma manual después de desinstalar un sitio.

#### <a name="membership"></a>Pertenencia
Configuration Manager administra automáticamente la pertenencia al grupo. Entre los miembros se incluyen usuarios administrativos que tienen concedido el permiso **Ver archivos recopilados** en el objeto asegurable **Recopilación** desde un rol de seguridad asignado.

#### <a name="permissions"></a>Permisos
De forma predeterminada, este grupo tiene el permiso **Lectura** en la siguiente carpeta del servidor de sitio: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`.  


### <a name="configmgr_dviewaccess"></a><a name="configmgr_dviewaccess"></a>ConfigMgr_DViewAccess  

Se trata de un grupo de seguridad local que Configuration Manager crea en el servidor de base de datos del sitio o en el servidor de réplica de base de datos para un sitio primario secundario. El sitio lo crea cuando se usan vistas distribuidas para la replicación de base de datos entre los sitios de una jerarquía. Contiene el servidor de sitio y las cuentas de equipo de SQL Server del sitio de administración central.

Para obtener más información, vea [Transferencias de datos entre sitios](data-transfers-between-sites.md).


### <a name="configmgr-remote-control-users"></a>Usuarios del control remoto de ConfigMgr  

Las herramientas remotas de Configuration Manager usan este grupo para almacenar las cuentas y los grupos que se configuran en la lista **Visores permitidos**. El sitio asigna esta lista a cada cliente.  

Para obtener más información, vea [Introducción al control remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).

#### <a name="type-and-location"></a>Tipo y ubicación
Se trata de un grupo de seguridad local creado en el cliente de Configuration Manager cuando el cliente recibe una directiva que habilita las herramientas remotas.

Después de deshabilitar las herramientas remotas para un cliente, este grupo no se quita automáticamente. Elimínelo de forma manual después de deshabilitar las herramientas remotas.

#### <a name="membership"></a>Pertenencia
De forma predeterminada, no hay ningún miembro en este grupo. Al agregar usuarios a la lista **Visores permitidos**, se agregan automáticamente a este grupo.

Use la lista **Visores permitidos** para administrar la pertenencia a este grupo en lugar de agregar usuarios o grupos directamente.

Además de ser un visor permitido, un usuario administrativo debe tener el permiso **Control remoto** en el objeto **Collection**. Asigne este permiso mediante el rol de seguridad **Operador de herramientas remotas**.  

#### <a name="permissions"></a>Permisos
De forma predeterminada, este grupo no tiene permisos para ninguna ubicación en el equipo. Solo se usa para contener la lista **Visores permitidos**.  


### <a name="sms-admins"></a>Administradores de SMS  

Configuration Manager usa este grupo para conceder acceso al proveedor de SMS a través de WMI. Se necesita acceso al proveedor de SMS para ver y modificar objetos en la consola de Configuration Manager.  

> [!NOTE]  
> La configuración de administración basada en roles de un usuario administrativo determina qué objetos puede ver y administrar cuando usa la consola de Configuration Manager.  

Para más información, vea [Plan for the SMS Provider](plan-for-the-sms-provider.md) (Planear el proveedor de SMS).

#### <a name="type-and-location"></a>Tipo y ubicación
Se trata de un grupo de seguridad local que se crea en cada equipo que tenga un proveedor de SMS. 

Cuando se desinstala un sitio, este grupo no se quita automáticamente. Elimínelo de forma manual después de desinstalar un sitio.

#### <a name="membership"></a>Pertenencia
Configuration Manager administra automáticamente la pertenencia al grupo. De forma predeterminada, cada usuario administrativo en una jerarquía y la cuenta de equipo del servidor de sitio son miembros del grupo **Administradores de SMS** en cada equipo de proveedor de SMS de un sitio.

#### <a name="permissions"></a>Permisos
Puede ver y configurar los permisos y derechos del grupo de administradores de SMS con el complemento de MMC **Control WMI**. De forma predeterminada, se concede **Habilitar cuenta** y **Llamada remota habilitada** a este grupo en el espacio de nombres de WMI `Root\SMS`. Los usuarios autenticados tienen los permisos **Ejecutar métodos**, **Escritura de proveedor** y **Habilitar cuenta**.

Cuando use una consola de Configuration Manager, configure permisos de DCOM de **activación remota** en el equipo de servidor de sitio y en el proveedor de SMS. Conceda estos derechos al grupo **Administradores de SMS**. Esta acción simplifica la administración en lugar de conceder estos derechos directamente a los usuarios o grupos. Para obtener más información, vea [Configuración de permisos de DCOM para consolas remotas de Configuration Manager](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;código_de_sitio\>  
 
Los puntos de administración remotos con respecto al servidor de sitio usan este grupo para conectarse a la base de datos del sitio. Este grupo proporciona un acceso de punto de administración a las carpetas de bandeja de entrada en el servidor de sitio y la base de datos del sitio.  

#### <a name="type-and-location"></a>Tipo y ubicación
Se trata de un grupo de seguridad local que se crea en cada equipo que tenga un proveedor de SMS.

Cuando se desinstala un sitio, este grupo no se quita automáticamente. Elimínelo de forma manual después de desinstalar un sitio.

#### <a name="membership"></a>Pertenencia
Configuration Manager administra automáticamente la pertenencia al grupo. De forma predeterminada, la pertenencia incluye las cuentas de equipo de equipos remotos que tienen un punto de administración para el sitio.

#### <a name="permissions"></a>Permisos
De forma predeterminada, este grupo tiene los permisos de **Lectura**, **Lectura y ejecución** y **Mostrar el contenido de la carpeta** para la carpeta siguiente en el servidor de sitio: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Este grupo tiene el permiso adicional para **Escribir** en subcarpetas por debajo de la carpeta **inboxes**, en la que el punto de administración escribe datos de cliente.


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;código_de_sitio\>  
 
Los equipos del proveedor de SMS remotos usan este grupo para conectarse al servidor de sitio.  

#### <a name="type-and-location"></a>Tipo y ubicación
Este grupo es un grupo de seguridad local creado en el servidor de sitio.

Cuando se desinstala un sitio, este grupo no se quita automáticamente. Elimínelo de forma manual después de desinstalar un sitio.

#### <a name="membership"></a>Pertenencia
Configuration Manager administra automáticamente la pertenencia al grupo. De forma predeterminada, la pertenencia incluye la cuenta de equipo o una cuenta de usuario de dominio. Usa esta cuenta para conectarse al servidor de sitio desde cada proveedor de SMS remoto.

#### <a name="permissions"></a>Permisos
De forma predeterminada, este grupo tiene los permisos de **Lectura**, **Lectura y ejecución** y **Mostrar el contenido de la carpeta** para la carpeta siguiente en el servidor de sitio: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Este grupo tiene los permisos adicionales de **Escritura** y **Modificar** en las subcarpetas por debajo de inboxes. El proveedor de SMS requiere acceso a estas carpetas.

Este grupo también tiene el permiso **Lectura** para las subcarpetas del servidor de sitio por debajo de `C:\Program Files\Microsoft Configuration Manager\OSD\Bin`. 

También tiene los permisos siguientes para las subcarpetas por debajo de `C:\Program Files\Microsoft Configuration Manager\OSD\boot`:
- **Lectura**  
- **Lectura y ejecución**  
- **Mostrar el contenido de la carpeta**  
- **Escritura**  
- **Modificar**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;código_de_sitio\>  

El componente de administrador de envío de archivos en equipos de sistema de sitio remoto de Configuration Manager usa este grupo para conectarse al servidor de sitio.  

#### <a name="type-and-location"></a>Tipo y ubicación
Este grupo es un grupo de seguridad local creado en el servidor de sitio.

Cuando se desinstala un sitio, este grupo no se quita automáticamente. Elimínelo de forma manual después de desinstalar un sitio.

#### <a name="membership"></a>Pertenencia
Configuration Manager administra automáticamente la pertenencia al grupo. De forma predeterminada, la pertenencia incluye la cuenta de equipo o la cuenta de usuario de dominio. Usa esta cuenta para conectarse al servidor de sitio desde cada sistema de sitio remoto que ejecuta el Administrador de envío de archivos.

#### <a name="permissions"></a>Permisos
De forma predeterminada, este grupo tiene los permisos de **Lectura**, **Lectura y ejecución** y **Mostrar el contenido de la carpeta** para la carpeta siguiente y sus subcarpetas en el servidor de sitio: `C:\Program Files\Microsoft Configuration Manager\inboxes`. 

Este grupo tiene los permisos adicionales de **Escritura** and **Modificar** en la carpeta siguiente del servidor de sitio: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`.


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;código_de_sitio\>  
Configuration Manager usa este grupo para habilitar la replicación basada en archivos entre sitios de una jerarquía. Por cada sitio remoto que transfiere archivos directamente a este sitio, este grupo contiene cuentas configuradas como **cuenta de replicación de archivos**.  

#### <a name="type-and-location"></a>Tipo y ubicación
Este grupo es un grupo de seguridad local creado en el servidor de sitio.

#### <a name="membership"></a>Pertenencia
Cuando se instala un sitio nuevo como secundario de otro, Configuration Manager agrega automáticamente la cuenta de equipo del nuevo servidor de sitio al grupo en el servidor de sitio primario. Configuration Manager también agrega la cuenta de equipo del sitio primario al grupo en el nuevo servidor de sitio. Si especifica otra cuenta para las transferencias basadas en archivos, agregue dicha cuenta a este grupo en el servidor de sitio de destino.

Cuando se desinstala un sitio, este grupo no se quita automáticamente. Elimínelo de forma manual después de desinstalar un sitio.

#### <a name="permissions"></a>Permisos
De forma predeterminada, este grupo tiene **Control total** en la carpeta siguiente: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`.



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a> Cuentas que usa Configuration Manager  

Puede configurar las cuentas siguientes para Configuration Manager.  


### <a name="active-directory-group-discovery-account"></a>Cuenta de detección de grupos de Active Directory  

El sitio usa la **cuenta de detección de grupos de Active Directory** para detectar los objetos siguientes desde las ubicaciones en Active Directory Domain Services que especifique:
- Grupos de seguridad locales, globales y universales
- La pertenencia a estos grupos
- La pertenencia dentro de grupos de distribución
  - Los grupos de distribución no se detectan como recursos de grupo

Esta cuenta puede ser una cuenta de equipo del servidor de sitio que ejecute la detección o una cuenta de usuario de Windows. Debe tener permiso de acceso de **Lectura** en las ubicaciones de Active Directory que se especifiquen para la detección.  

Para obtener más información, vea [Detección de grupos de Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Cuenta de detección de sistemas de Active Directory  

El sitio usa la **cuenta de detección de sistemas de Active Directory** para detectar equipos desde las ubicaciones en Active Directory Domain Services que especifique.  

Esta cuenta puede ser una cuenta de equipo del servidor de sitio que ejecute la detección o una cuenta de usuario de Windows. Debe tener permiso de acceso de **Lectura** en las ubicaciones de Active Directory que se especifiquen para la detección.  

Para obtener más información, vea [Detección de sistemas de Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Cuenta de detección de usuarios de Active Directory  
 
El sitio usa la **cuenta de detección de usuarios de Active Directory** para detectar cuentas de usuario desde las ubicaciones en Active Directory Domain Services que especifique.  

Esta cuenta puede ser una cuenta de equipo del servidor de sitio que ejecute la detección o una cuenta de usuario de Windows. Debe tener permiso de acceso de **Lectura** en las ubicaciones de Active Directory que se especifiquen para la detección.  

Para obtener más información, vea [Detección de usuario de Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Cuenta de bosque de Active Directory  

El sitio usa la **cuenta de bosque de Active Directory** para detectar la infraestructura de red en bosques de Active Directory. Los sitios de administración central y los sitios primarios también la usan para publicar datos de sitio de Active Directory Domain Services en un bosque.  

> [!NOTE]  
> Los sitios secundarios siempre utilizan la cuenta de equipo del servidor de sitio secundario para publicar en Active Directory.  

Para detectar y publicar en bosques que no son de confianza, la cuenta de bosque de Active Directory debe ser una cuenta global. Si no se usa la cuenta de equipo del servidor de sitio, solo se puede seleccionar una cuenta global.  

Esta cuenta debe tener permisos de **lectura** en cada bosque de Active Directory donde desee detectar infraestructura de red.  

Esta cuenta debe tener permisos **Control total** en el contenedor de **administración de sistema** y todos sus objetos secundarios en cada bosque de Active Directory donde quiera publicar datos del sitio. Para más información, vea [Preparar Active Directory para la publicación de sitios](../network/extend-the-active-directory-schema.md).  

Para obtener más información, vea [Detección de bosques de Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Cuenta de punto de registro de certificado  

El punto de registro de certificado usa la **cuenta de punto de registro de certificado** para conectarse a la base de datos de Configuration Manager. Usa su cuenta de equipo de forma predeterminada, pero en su lugar puede configurar una cuenta de usuario. Cuando el punto de registro de certificado esté en un dominio que no sea de confianza en el servidor del sitio, debe especificar una cuenta de usuario. Esta cuenta solo requiere acceso de **lectura** a la base de datos del sitio, ya que el sistema de mensajes de estado controla las tareas de escritura.  

Para obtener más información, vea [Introducción a los perfiles de certificado](../../../protect/deploy-use/introduction-to-certificate-profiles.md).


### <a name="capture-os-image-account"></a>Cuenta de captura de imagen de sistema operativo  

Cuando se captura una imagen de sistema operativo, Configuration Manager usa la **cuenta de captura de imagen de sistema operativo** para acceder a la carpeta en la que se almacenan las imágenes capturadas. Si agrega el paso **Capturar imagen de sistema operativo** a una secuencia de tareas, esta cuenta será necesaria.  

La cuenta debe tener permisos de **Lectura** y **Escritura** en el recurso compartido de red donde se almacenan las imágenes capturadas.  

Si cambia la contraseña de la cuenta en Windows, actualice la secuencia de tareas con la contraseña nueva. El cliente de Configuration Manager recibirá la nueva contraseña la próxima vez que descargue la directiva de cliente.  

Si necesita usar esta cuenta, cree una cuenta de usuario de dominio. Concédale los permisos mínimos para acceder a los recursos de red necesarios, y úsela para todas las secuencias de tareas de captura.  

> [!IMPORTANT]  
> No asigne permisos de inicio de sesión interactivo a esta cuenta.  
>   
> No use la cuenta de acceso a la red para esta cuenta.  

Para obtener más información, vea [Crear una secuencia de tareas para capturar un sistema operativo](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).


### <a name="client-push-installation-account"></a>Cuenta de instalación de inserción de cliente  

Cuando se implementan clientes mediante el método de instalación de inserción de cliente, el sitio usa la **cuenta de instalación de inserción de cliente** para conectarse a los equipos e instalar el software de cliente de Configuration Manager. Si no especifica esta cuenta, el servidor de sitio intenta usar su cuenta de equipo.  

Esta cuenta debe ser miembro del grupo **Administradores** locales de los equipos cliente de destino. Esta cuenta no requiere derechos de **Administrador de dominio**.  

Puede especificar más de una cuenta de instalación de inserción de cliente. Configuration Manager prueba cada una por turnos hasta que una es correcta.  

> [!TIP]  
> Si tiene un entorno de Active Directory de gran tamaño y necesita cambiar esta cuenta, siga los pasos siguientes para coordinar la actualización de esta cuenta de forma más eficaz: 
> 1. Cree una cuenta con otro nombre.   
> 2. Agregue la nueva cuenta a la lista de cuentas de instalación de inserción de cliente en Configuration Manager.  
> 3. Deje tiempo suficiente para que Active Directory Domain Services pueda replicar la nueva cuenta.  
> 4. Después, quite la cuenta antigua de Configuration Manager y Active Directory Domain Services.  

> [!IMPORTANT]  
> No conceda a esta cuenta el derecho para iniciar sesión de forma local.  

Para obtener más información, vea [Instalación de inserción de cliente](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Cuenta de conexión de punto de inscripción  

El punto de inscripción usa la **cuenta de conexión de punto de inscripción** para conectarse a la base de datos de sitio de Configuration Manager. Usa su cuenta de equipo de forma predeterminada, pero en su lugar puede configurar una cuenta de usuario. Cuando el punto de inscripción esté en un dominio que no sea de confianza en el servidor del sitio, debe especificar una cuenta de usuario. Esta cuenta requiere acceso de **lectura** y **escritura** a la base de datos del sitio.  

Para obtener más información, vea [Instalación de roles de sistema de sitio para la MDM local](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).


### <a name="exchange-server-connection-account"></a>Cuenta de conexión de Exchange Server  

El servidor de sitio usa la **cuenta de conexión de Exchange Server** para conectarse al servidor Exchange especificado. Usa esta conexión para buscar y administrar dispositivos móviles que se conectan a Exchange Server. Esta cuenta requiere los cmdlets de PowerShell de Exchange que proporcionan los permisos necesarios para el equipo de Exchange Server. Para obtener más información acerca de los cmdlets, consulte [Instalación y configuración de Exchange Conector](../../../mdm/deploy-use/install-configure-exchange-connector.md).  


### <a name="management-point-connection-account"></a>Cuenta de conexión del punto de administración  

El punto de administración usa la **cuenta de conexión del punto de administración** para conectarse a la base de datos de sitio de Configuration Manager. Usa esta conexión para enviar y recuperar información para los clientes. El punto de administración usa su cuenta de equipo de forma predeterminada, pero en su lugar puede configurar una cuenta de usuario. Cuando el punto de administración esté en un dominio que no sea de confianza en el servidor del sitio, debe especificar una cuenta de usuario.  

Cree la cuenta como una cuenta local con derechos reducidos en el equipo que ejecuta Microsoft SQL Server.  

> [!IMPORTANT]  
> No conceda derechos de inicio de sesión interactivo a esta cuenta.  


### <a name="multicast-connection-account"></a>Cuenta de conexión de multidifusión  

Los puntos de distribución habilitados para la multidifusión usan la **cuenta de conexión de multidifusión** para leer información de la base de datos del sitio. El servidor usa su cuenta de equipo de forma predeterminada, pero en su lugar puede configurar una cuenta de usuario. Cuando la base de datos del sitio esté en un bosque que no sea de confianza, debe especificar una cuenta de usuario. Por ejemplo, si el centro de datos tiene una red perimetral en un bosque que no sea ni el servidor del sitio ni la base de datos del sitio, use esta cuenta para leer la información de multidifusión desde la base de datos del sitio.  

Si necesita esta cuenta, créela como una cuenta local con derechos reducidos en el equipo que ejecuta Microsoft SQL Server.  

> [!IMPORTANT]  
> No conceda derechos de inicio de sesión interactivo a esta cuenta.  

Para obtener más información, consulte [Usar multidifusión para implementar Windows a través de la red](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).


### <a name="network-access-account"></a>Cuenta de acceso a la red  

Los equipos cliente usan la **cuenta de acceso a la red** cuando no pueden usar su cuenta de equipo local para acceder a contenido en los puntos de distribución. Esto se aplica principalmente a los equipos y clientes del grupo de trabajo de dominios que no son de confianza. Esta cuenta también se usa durante la implementación del sistema operativo, cuando el equipo que lo instala no tiene aún una cuenta de equipo en el dominio.  

> [!Important]  
> La cuenta de acceso a la red nunca se usa como contexto de seguridad para ejecutar programas, instalar actualizaciones de software ni ejecutar secuencias de tareas. Solo se utiliza para acceder a recursos de la red.  

En primer lugar, un cliente de Configuration Manager intenta usar su cuenta de equipo para descargar el contenido. Si se produce un error, prueba de forma automática la cuenta de acceso a la red.  

A partir de la versión 1806, un grupo de trabajo o un cliente unido a Azure AD pueden acceder de forma segura a contenido desde puntos de distribución sin necesidad de una cuenta de acceso a la red. Este comportamiento incluye escenarios de implementación de sistema operativo con una secuencia de tareas que se ejecuta desde el medios de arranque, PXE o el Centro de software. Para obtener más información, vea [HTTP mejorado](enhanced-http.md).<!--1358228,1358278-->

> [!Note]  
> Si habilita **HTTP mejorado** para que no se requiera la cuenta de acceso a la red, el punto de distribución debe ejecutar Windows Server 2012 o una versión posterior. <!--SCCMDocs-pr issue #2696-->
>  
> Actualice los clientes al menos a la versión 1806 antes de habilitar esta funcionalidad. Si solo permite conexiones de **HTTP mejorado**, los clientes más antiguos no se podrán autenticar con este método, por lo que no podrán descargar el paquete de actualización de cliente desde un punto de distribución. <!--vso2841213-->   

#### <a name="permissions"></a>Permisos

Conceda a esta cuenta los permisos adecuados mínimos en el contenido que el cliente necesita para tener acceso al software. La cuenta debe tener el permiso **Tener acceso a este equipo desde la red** en el punto de distribución. Puede configurar hasta 10 cuentas de acceso a la red por cada sitio.  

Cree la cuenta en cualquier dominio que proporcione el acceso necesario a los recursos. La cuenta de acceso a la red siempre debe incluir un nombre de dominio. No se admite la seguridad de paso a través para esta cuenta. Si tiene puntos de distribución en varios dominios, cree la cuenta en un dominio de confianza.  

> [!TIP]  
> Para evitar bloqueos de cuentas, no cambie la contraseña de una cuenta de acceso a la red existente. En su lugar, cree otra cuenta y configúrela en Configuration Manager. Cuando transcurra el tiempo suficiente para que todos los clientes reciban los detalles de la cuenta nueva, quite la cuenta antigua de las carpetas compartidas de red y elimine la cuenta.  

> [!IMPORTANT]  
> No conceda derechos de inicio de sesión interactivo a esta cuenta.  
>   
> No conceda a esta cuenta el derecho de unir equipos al dominio. Si tiene que unir equipos al dominio durante una secuencia de tareas, use la [cuenta de unión de dominio de secuencia de tareas](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Configuración de la cuenta de acceso a la red  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Después, seleccione el sitio.  

2.  En el grupo **Configuración** de la cinta, haga clic en **Configurar componentes de sitio** y después en **Distribución de software**.  

3.  Haga clic en la pestaña **Cuenta de acceso a la red**. Configure una o varias cuentas y, después, elija **Aceptar**.  


### <a name="package-access-account"></a>Cuenta de acceso de paquetes  

Una **cuenta de acceso de paquetes** permite establecer permisos NTFS para especificar los usuarios y grupos de usuarios que pueden acceder a contenido de paquetes en los puntos de distribución. De forma predeterminada, Configuration Manager solo concede acceso a las cuentas de acceso genérico **Usuario** y **Administrador**. Puede controlar el acceso de los equipos cliente mediante el uso de grupos o cuentas de Windows adicionales. Los dispositivos móviles siempre recuperan el contenido del paquete de forma anónima, por lo que no usan cuentas de acceso de paquetes.  

De forma predeterminada, cuando Configuration Manager copia los archivos de contenido en un punto de distribución, concede acceso de **Lectura** al grupo **Usuarios** local y **Control total** al grupo de **Administradores** local. Los permisos reales necesarios dependen del paquete. Si tiene clientes en grupos de trabajo o en bosques que no son de confianza, estos clientes usan la cuenta de acceso a la red para acceder al contenido del paquete. Asegúrese de que la cuenta de acceso a la red tenga permisos para el paquete mediante las cuentas de acceso de paquetes definidas.  

Utilice las cuentas en un dominio que pueda acceder a los puntos de distribución. Si crea o modifica la cuenta después de crear el paquete, tendrá que redistribuirlo. La actualización del paquete no cambia los permisos NTFS del paquete.  

No es necesario agregar la cuenta de acceso a la red como una cuenta de acceso de paquetes, ya que la pertenencia al grupo **Usuarios** la agrega de forma automática. Restringir la cuenta de acceso de paquetes solo a la cuenta de acceso a la red no impide que los clientes accedan al paquete.  

#### <a name="manage-package-access-accounts"></a>Administración de cuentas de acceso de paquetes  

1.  En la consola de Configuration Manager, elija **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software**, determine el tipo de contenido para el que desea administrar cuentas de acceso y siga los pasos indicados:  

    - **Aplicación**: expanda **Administración de aplicaciones**, haga clic en **Aplicaciones** y, luego, seleccione la aplicación para la que se van a administrar cuentas de acceso.  

    - **Paquete**: expanda **Administración de aplicaciones**, haga clic en **Paquetes** y, luego, seleccione el paquete para el que se van a administrar cuentas de acceso.  

    - **Paquetes de implementación de actualizaciones de software**: expanda **Actualizaciones de software**, haga clic en **Paquetes de implementación** y, después, seleccione el paquete de implementación para el que se van a administrar cuentas de acceso.  

    - **Paquete de controladores**: expanda **Sistemas operativos**, haga clic en **Paquetes de controladores** y, luego, seleccione el paquete de controladores para el que se van a administrar cuentas de acceso.  

    - **Imagen del sistema operativo**: expanda **Sistemas operativos**, haga clic en **Imágenes de sistema operativo** y, después, seleccione la imagen de sistema operativo para la que se van a administrar cuentas de acceso.  

    - **Paquete de actualización del sistema operativo**: expanda **Sistemas operativos**, haga clic en **Paquetes de actualización del sistema operativo** y, después, seleccione el paquete de actualización de sistema operativo para el que se van a administrar cuentas de acceso.  

    - **Imagen de arranque**: expanda **Sistemas operativos**, haga clic en **Imágenes de arranque** y, luego, seleccione la imagen de arranque para la que se van a administrar cuentas de acceso.  

3.  Haga clic con el botón derecho en el objeto seleccionado y, luego, elija **Administrar cuentas de acceso**.  

4.  En el cuadro de diálogo **Agregar cuenta** , especifique el tipo de cuenta al que se le concederá acceso al contenido y, a continuación, especifique los derechos de acceso asociados a la cuenta.  

    > [!NOTE]  
    > Cuando se agrega un nombre de usuario para la cuenta y Configuration Manager encuentra tanto una cuenta de usuario local como una cuenta de usuario de dominio con ese nombre, este establece derechos de acceso para la cuenta de usuario de dominio.  


### <a name="reporting-services-point-account"></a>Cuenta de punto de Reporting Services  
 
SQL Server Reporting Services usa la **cuenta de punto de Reporting Services** para recuperar los datos de informes de Configuration Manager de la base de datos del sitio. La cuenta de usuario y la contraseña de Windows especificadas se cifran y almacenan en la base de datos de SQL Server Reporting Services.  

> [!NOTE]  
> La cuenta que especifique debe tener permisos de **Inicio de sesión local** en el equipo que hospeda la base de datos de SQL Reporting Services.

> [!NOTE]  
> A la cuenta se le conceden automáticamente todos los derechos necesarios al agregarse al rol smsschm_users de SQL Database en la base de datos de ConfigMgr.

Para obtener más información, vea [Introducción a los informes](../../servers/manage/introduction-to-reporting.md).


### <a name="remote-tools-permitted-viewer-accounts"></a>Cuentas de visores permitidos de herramientas remotas  

Las cuentas que especifique como **Visores permitidos** para el control remoto son una lista de usuarios a los que se permite el uso de funcionalidades de herramientas remotas en los clientes.  

Para obtener más información, vea [Introducción al control remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).


### <a name="site-installation-account"></a>Cuenta de instalación del sitio
<!--SCCMDocs issue #572-->
Use una cuenta de usuario de dominio para iniciar sesión en el servidor en el que se ejecuta el programa de instalación de Configuration Manager y se instala un sitio nuevo.

Esta cuenta requiere los permisos siguientes:  

- **Administrador** en los siguientes servidores:
    - El servidor de sitio  
    - Cada servidor que hospeda la base de datos del sitio  
    - Cada instancia del Proveedor de SMS para el sitio  

- **Administrador del sistema** en la instancia de SQL Server que hospeda la base de datos del sitio  

El programa de instalación de Configuration Manager agrega automáticamente esta cuenta al grupo [Administradores de SMS](#sms-admins).

Después de la instalación, esta cuenta es el único usuario con derechos para la consola de Configuration Manager. Si tiene que quitar esta cuenta, asegúrese de agregar primero sus derechos a otro usuario.

Al expandir un sitio independiente para incluir un sitio de administración central, esta cuenta requiere los derechos de administración basada en roles **Administrador total** o **Administrador de infraestructura** en el sitio primario independiente.


### <a name="site-system-installation-account"></a>Cuenta de instalación del sistema de sitio  

El servidor de sitio usa la **cuenta de instalación del sistema de sitio** para instalar, reinstalar, desinstalar y configurar sistemas de sitio. Si configura el sistema de sitio de modo que exija al servidor de sitio iniciar conexiones con este sistema, Configuration Manager también usa esta cuenta para extraer datos del sistema de sitio después de la instalación del sistema de sitio y cualquier rol. Cada sistema de sitio puede tener una cuenta de instalación distinta, pero solo se puede configurar una cuenta de instalación para administrar todos los roles en ese sistema de sitio.  

Esta cuenta requiere permisos administrativos locales en los sistemas de sitio de destino. Además, esta cuenta debe **Tener acceso a este equipo desde la red** en la directiva de seguridad en los sistemas de sitio de destino.  

> [!TIP]  
> Si tiene muchos controladores de dominio y estas cuentas se usan en varios dominios, antes de configurar el sistema de sitio, compruebe que Active Directory las haya replicado.  
>   
> Al especificar una cuenta local en cada sistema de sitio que se va a administrar, esta configuración es más segura que usar cuentas de dominio. Limita los daños que los atacantes pueden producir si la seguridad de la cuenta se ve comprometida. Aunque las cuentas de dominio son más fáciles de administrar. Tenga en cuenta el equilibrio entre la seguridad y una administración eficaz.  


### <a name="site-system-proxy-server-account"></a>Cuenta de servidor proxy de sistema de sitio
<!--SCCMDocs issue #648-->
Los roles de sistema de sitio siguientes usan la **cuenta de servidor proxy de sistema de sitio** para obtener acceso a Internet a través de un servidor proxy o firewall que requiera acceso autenticado:

- Punto de sincronización de Asset Intelligence
- Conector de Exchange Server
- Punto de conexión de servicio
- Punto de actualización de software

> [!IMPORTANT]  
> Especifique una cuenta que tenga los mínimos permisos posibles en el servidor proxy o firewall correspondiente.  

Para obtener más información, vea [Compatibilidad de servidor proxy](../network/proxy-server-support.md).


### <a name="smtp-server-connection-account"></a>Cuenta de conexión del servidor SMTP  

El servidor de sitio usa la **cuenta de conexión del servidor SMTP** para enviar alertas por correo electrónico cuando el servidor SMTP requiere acceso autenticado.  

> [!IMPORTANT]  
> Especifique una cuenta que tenga los mínimos permisos posibles para enviar mensajes de correo electrónico.  

Para obtener más información, consulte [Usar alertas y el sistema de estado](../../servers/manage/use-alerts-and-the-status-system.md).


### <a name="software-update-point-connection-account"></a>Cuenta de conexión de punto de actualización de software  

El servidor de sitio usa la **cuenta de conexión de punto de actualización de software** para los dos servicios de actualización de software siguientes:  

- Windows Server Update Services (WSUS), que configura opciones como las definiciones de producto, las clasificaciones y la configuración ascendente.  

- Administrador de sincronización de WSUS, que solicita la sincronización a un servidor WSUS ascendente o a Microsoft Update.  

La [cuenta de instalación del sistema de sitio](#site-system-installation-account) puede instalar componentes para las actualizaciones de software, pero no puede realizar funciones específicas de actualización de software en el punto de actualización de software. Si no puede usar la cuenta de equipo del servidor de sitio para esta funcionalidad porque el punto de actualización de software está en un bosque que no es de confianza, debe especificar esta cuenta además de la cuenta de instalación del sistema de sitio.  

Esta cuenta debe ser un administrador local en el equipo donde se instala WSUS. También debe formar parte del grupo **Administradores de WSUS** local.  

Para obtener más información, vea [Planear actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md).


### <a name="source-site-account"></a>Cuenta de sitio de origen  

El proceso de migración usa la **cuenta de sitio de origen** para acceder al proveedor de SMS del sitio de origen. Esta cuenta requiere permisos de **Leer** en objetos de sitio en el sitio de origen para obtener datos de trabajos de migración.  

Si tiene puntos de distribución de Configuration Manager 2007 o sitios secundarios con puntos de distribución colocados, al actualizarlos a puntos de distribución de Configuration Manager (rama actual), esta cuenta también debe tener permisos **Eliminar** para la clase **Sitio**. Este permiso sirve para quitar correctamente el punto de distribución del sitio de Configuration Manager 2007 durante la actualización.  

> [!NOTE]  
> La cuenta de sitio de origen y la [cuenta de base de datos del sitio de origen](#source-site-database-account) se identifican como **Administrador de migraciones** en el nodo **Cuentas** del área de trabajo **Administración** en la consola de Configuration Manager.  

Para más información, vea [Migración de datos entre jerarquías](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Cuenta de base de datos del sitio de origen  

El proceso de migración usa la **cuenta de base de datos del sitio de origen** para acceder a la base de datos de SQL Server del sitio de origen. Para obtener datos de la base de datos de SQL Server del sitio de origen, la cuenta de base de datos del sitio de origen debe tener los permisos para **Leer** y **Ejecutar** en la base de datos de SQL Server del sitio de origen.  

Si usa la cuenta de equipo de Configuration Manager (rama actual), asegúrese de que se cumpla lo siguiente para esta cuenta:  
  
- Es un miembro del grupo de seguridad **Usuarios COM distribuidos** en el mismo dominio que el sitio de Configuration Manager 2007.  
- Es un miembro del grupo de seguridad **Administradores de SMS**.  
- Tiene el permiso **Lectura** para todos los objetos de Configuration Manager 2007.  

> [!NOTE]  
> La cuenta de sitio de origen y la [cuenta de base de datos del sitio de origen](#source-site-database-account) se identifican como **Administrador de migraciones** en el nodo **Cuentas** del área de trabajo **Administración** en la consola de Configuration Manager.  

Para más información, vea [Migración de datos entre jerarquías](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Cuenta de unión de dominio de secuencia de tareas 

El programa de instalación de Windows usa la **cuenta de unión de dominio de secuencia de tareas** para unir un equipo creado recientemente con una imagen a un dominio. Esta cuenta es necesaria para el paso de secuencia de tareas [Unirse a dominio o grupo de trabajo](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) con la opción **Unirse a un dominio**. Esta cuenta también se puede configurar con el paso [Aplicar configuración de red](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings), pero no es necesario.  

Esta cuenta requiere el derecho **Unión a dominio** en el dominio de destino.  

> [!TIP]  
> Cree una cuenta de usuario de dominio con los permisos mínimos para unirse al dominio, y úsela para todas las secuencias de tareas.  

> [!IMPORTANT]  
> No asigne permisos de inicio de sesión interactivo a esta cuenta.  
>   
> No use la cuenta de acceso a la red para esta cuenta.  


### <a name="task-sequence-network-folder-connection-account"></a>Cuenta de conexión de carpeta de red de secuencia de tareas  

El motor de secuencia de tareas usa la **cuenta de conexión de carpeta de red de secuencias de tareas** para conectarse a una carpeta compartida en la red. Esta cuenta es necesaria para el paso de secuencia de tareas [Conectar a carpeta de red](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

Esta cuenta requiere permisos de acceso a la carpeta compartida especificada. Debe ser una cuenta de usuario de dominio.  

> [!TIP]  
> Cree una cuenta de usuario de dominio con los permisos mínimos para acceder a los recursos de red necesarios, y úsela para todas las secuencias de tareas.  

> [!IMPORTANT]  
> No asigne permisos de inicio de sesión interactivo a esta cuenta.  
>   
> No use la cuenta de acceso a la red para esta cuenta.  


### <a name="task-sequence-run-as-account"></a>Cuenta de ejecución de secuencia de tareas  

El motor de secuencias de tareas usa la **cuenta de ejecución de secuencias de tareas** para ejecutar líneas de comandos o scripts de PowerShell con credenciales distintas a las de la cuenta del sistema local. Esta cuenta es necesaria para los pasos de la secuencia de tareas [Ejecutar línea de comandos](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) y [Ejecutar script de PowerShell](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) con la opción **Ejecutar este paso como la cuenta siguiente** seleccionada.  

Configure la cuenta para que tenga los permisos mínimos necesarios para ejecutar la línea de comandos especificada en la secuencia de tareas. La cuenta requiere derechos de inicio de sesión interactivo. Normalmente requiere la capacidad de instalar software y acceder a recursos de red. Para la tarea Ejecutar script de PowerShell, esta cuenta requiere permisos de administrador local. 

> [!IMPORTANT]  
> No use la cuenta de acceso a la red para esta cuenta.  
>   
> Nunca convierta la cuenta en administrador de dominio.  
>   
> No configure nunca perfiles móviles para esta cuenta. Cuando la secuencia de tareas se ejecuta, descarga el perfil móvil para la cuenta. Esto deja el perfil vulnerable al acceso en el equipo local.  
>   
> Limite el ámbito de la cuenta. Por ejemplo, cree otras cuentas de ejecución de secuencia de tareas para cada secuencia de tareas. Después, si una cuenta se pone en peligro, solo estarán en peligro los equipos cliente a los que esa cuenta tenga acceso.  
>   
> Si la línea de comandos requiere acceso administrativo al equipo, considere la posibilidad de crear una cuenta de administrador local solo para esta cuenta en todos los equipos que ejecuten la secuencia de tareas. Elimine la cuenta cuando ya no la necesite.  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a> Objetos de usuario que Configuration Manager usa en SQL 
<!--SCCMDocs issue #1160-->
Configuration Manager automáticamente crea y mantiene los siguientes objetos de usuario en SQL.  Estos objetos se encuentran en la base de datos de Configuration Manager, en Seguridad/Usuarios.  

> [!IMPORTANT]  
>  Modificar o quitar estos objetos puede provocar problemas drásticos dentro de un entorno de Configuration Manager.  Se recomienda no realizar ningún cambio en estos objetos.


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

Este objeto se usa para ejecutar consultas en el contexto de solo lectura.  Este objeto se usa con varios procedimientos almacenados.


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

Este objeto se usa para proporcionar permisos para las instrucciones SQL dinámicas.


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

Este objeto se usa para realizar ejecuciones de SQL Reporting.  El siguiente procedimiento almacenado se usa con esta función: spSRExecQuery.


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Roles de base de datos que Configuration Manager usa en SQL
<!--SCCMDocs issue #1160-->
Configuration Manager automáticamente crea y mantiene los objetos de rol siguientes en SQL. Estos roles proporcionan acceso a procedimientos almacenados, tablas, vistas y funciones específicos para llevar a cabo las acciones necesarias de cada rol con el fin de recuperar o insertar datos en la base de datos de ConfigMgr y desde esta. Estos objetos se encuentran en la base de datos de Configuration Manager, en Seguridad/Roles/Roles de base de datos.

> [!IMPORTANT]  
> Modificar o quitar estos objetos puede provocar problemas drásticos dentro de un entorno de Configuration Manager.  Se recomienda no realizar ningún cambio en estos objetos.

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Importación de Licencias por volumen de Asset Intelligence. ConfigMgr concede este permiso a las cuentas de usuario basadas en el acceso de RBA para poder importar la licencia por volumen que se va a usar con Asset Intelligence.  Esta cuenta la podría agregar un rol total de administrador o un rol de Administrador de activos.

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Sincronización de actualización de Asset Intelligence. ConfigMgr concede a la cuenta de equipo que hospeda el punto de sincronización de Asset Intelligence acceso para obtener los datos del proxy de Asset Intelligence y para ver los datos de IA pendientes para su carga.

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

Administración fuera de banda. Este rol lo usa el rol de AMT de Configuration Manager para recuperar datos en dispositivos que admiten AMT de Intel.

> [!NOTE]  
> Este rol está en desuso en las versiones más recientes de ConfigMgr.

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

Compatibilidad con el Servicio de inscripción de dispositivos de red (SCEP) del Punto de registro de certificados. ConfigMgr concede permisos a la cuenta de equipo del sistema de sitio que admite el Punto de registro de certificados para la compatibilidad de SCEP con la firma y renovación de certificados.

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

Compatibilidad de PFX con el Punto de registro de certificados. ConfigMgr concede permisos a la cuenta de equipo del sistema de sitio que admite el Punto de registro de certificados configurado para la compatibilidad de PFX con la firma y renovación.

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

Punto de administración de dispositivos. ConfigMgr concede este permiso a la cuenta de equipo de un Punto de administración con la opción "Permitir que los dispositivos móviles y el equipo Mac usen este punto de administración", la capacidad para proporcionar compatibilidad con dispositivos inscritos en MDM.

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

Punto de conexión de servicio. ConfigMgr concede este permiso a la cuenta de equipo que hospeda el Punto de conexión de servicio para recuperar y proporcionar datos de telemetría, administrar servicios en la nube y recuperar actualizaciones del servicio.

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

Vistas distribuidas. Configuration Manager concede este permiso a la cuenta de equipo de los Servidores de sitio primarios del CAS cuando se selecciona la opción de vistas distribuidas de SQL Server en las propiedades del vínculo de replicación.

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

Almacenamiento de datos. ConfigMgr concede este permiso a la cuenta de equipo que hospeda el rol de Almacenamiento de datos.

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 Punto de inscripción. ConfigMgr concede este permiso a la cuenta de equipo que hospeda el Punto de inscripción para permitir la inscripción de dispositivos a través de MDM.

### <a name="smsdbrole_extract"></a>smsdbrole_extract

Proporciona acceso a todas las vistas extendidas de esquema.

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

Servicio de Administrador de jerarquía. ConfigMgr concede permisos a esta cuenta para administrar los mensajes de estado de conmutación por error y las transacciones de agente de SQL Server entre sitios en una jerarquía.

> [!NOTE]  
> El rol smdbrole_WebPortal es miembro de este rol de forma predeterminada.

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

Servicio multidifusión. ConfigMgr concede este permiso a la cuenta de equipo del Punto de distribución que admite la multidifusión.

### <a name="smsdbrole_mp"></a>smsdbrole_MP

Punto de administración. ConfigMgr concede este permiso a la cuenta de equipo que hospeda el rol de Punto de administración para proporcionar compatibilidad con los clientes de ConfigMgr.

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

Punto de administración de Microsoft BitLocker Administration And Monitoring. ConfigMgr concede este permiso a la cuenta de equipo que hospeda el Punto de administración que administra MBAM en un entorno.

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

Solicitud de aplicación de Punto de administración. ConfigMgr concede este permiso a la cuenta de equipo que hospeda el Punto de administración que admite las solicitudes de aplicación basadas en el usuario.

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

Proveedor de SMS. Configuration Manager concede este permiso a la cuenta de equipo que hospeda un rol de Proveedor de SMS.  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

Servidor de sitio. ConfigMgr concede este permiso a la cuenta de equipo que hospeda el sitio primario o CAS.

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

Punto de actualización de software. ConfigMgr concede este permiso a la cuenta de equipo que hospeda el Punto de actualización de software para trabajar con actualizaciones de terceros.

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

Punto de sitio web del catálogo de aplicaciones. Configuration Manager concede permiso a la cuenta de equipo que hospeda el Punto de sitio web del catálogo de aplicaciones para proporcionar una implementación de aplicación basada en el usuario.

### <a name="smsschm_users"></a>smsschm_users

Acceso a informes de usuario. ConfigMgr concede acceso a la cuenta usada para la cuenta de Punto de servicios de informes con el fin de permitir el acceso a las vistas de informes de SMS y, de este modo, mostrar los datos de informes de Configuration Manager.  Los datos se restringen aún más con el uso de RBA.
