---
title: Referencia del archivo de registro
titleSuffix: Configuration Manager
description: Una referencia de todos los archivos de registro del cliente, el servidor y los componentes dependientes de Configuration Manager.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36ab89f1e9988adc167bf69ff7d9f53b02bbe10f
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166549"
---
# <a name="log-file-reference"></a>Referencia del archivo de registro

*Se aplica a: Configuration Manager (rama actual)*

En Configuration Manager, los componentes de cliente y servidor de sitio registran información de proceso en archivos de registro individuales. Se puede usar la información de estos archivos de registro para facilitar la solución de los problemas que puedan producirse. De forma predeterminada, Configuration Manager habilita el registro para los componentes de cliente y servidor.

Para más información general sobre los archivos de registro de Configuration Manager, vea [Acerca de los archivos de registro](about-log-files.md). Dicho artículo incluye información sobre las herramientas que se deben usar, cómo configurar los registros y dónde encontrarlos.

En las secciones siguientes se proporcionan detalles sobre los diferentes archivos de registro disponibles. Supervise los registros de cliente y servidor de Configuration Manager para obtener detalles de operaciones y vea información de los errores para solucionar los problemas.  

- [Archivos de registro de cliente](#BKMK_ClientLogs)  

  - [Operaciones de cliente](#BKMK_ClientOpLogs)  

  - [Instalación de cliente](#BKMK_ClientInstallLog)  

  - [Cliente para Linux y UNIX](#BKMK_LogFilesforLnU)  

  - [Cliente para equipos Mac](#BKMK_LogfilesforMac)  

- [Archivos de registro del servidor](#BKMK_ServerLogs)  

  - [Servidor de sitio y sistemas de sitio](#BKMK_SiteSiteServerLog)  

  - [Instalación del servidor del sitio](#BKMK_SiteInstallLog)

  - [Punto de servicio de almacenamiento de datos](#BKMK_DataWarehouse)

  - [Punto de estado de reserva](#BKMK_FSPLog)  

  - [Punto de administración](#BKMK_MPLog)  

  - [Punto de conexión de servicio](#BKMK_WITLog)  

  - [Punto de actualización de software](#BKMK_SUPLog)  

- [Archivos de registro por funcionalidad](#BKMK_FunctionLogs)  

  - [Administración de aplicaciones](#BKMK_AppManageLog)  

  - [Asset Intelligence](#BKMK_AILog)  

  - [Copia de seguridad y recuperación](#BKMK_BnRLog)  

  - [Inscripción de certificado](#BKMK_CertificateEnrollment)

  - [Notificación de cliente](#BKMK_BGB)

  - [Puerta de enlace de administración en la nube](#cloud-management-gateway)

  - [Configuración de cumplimiento y acceso a los recursos de la compañía](#BKMK_CompSettingsLog)  

  - [Consola de Configuration Manager](#BKMK_ConsoleLog)  

  - [Administración de contenido](#BKMK_ContentLog)  

  - [Análisis de escritorio](#desktop-analytics)

  - [Detección](#BKMK_DiscoveryLog)  

  - [Endpoint Protection](#BKMK_EPLog)  

  - [Extensiones](#BKMK_Extensions)  

  - [Inventario](#BKMK_InventoryLog)  

  - [Migración](#BKMK_MigrationLog)  

  - [Dispositivos móviles](#BKMK_MDMLog)  

  - [Implementación del sistema operativo](#BKMK_OSDLog)  

  - [Administración de energía](#BKMK_PowerMgmtLog)  

  - [Control remoto](#BKMK_RCLog)  

  - [Generación de informes](#BKMK_ReportLog)  

  - [Administración basada en roles](#BKMK_RBALog)  

  - [Medición de software](#BKMK_MeteringLog)  

  - [Actualizaciones de software](#BKMK_SU_NAPLog)  

  - [Wake On LAN](#BKMK_WOLLog)  

  - [Mantenimiento de Windows 10](#BKMK_WindowsServicingLog)

  - [Agente de Windows Update](#BKMK_WULog)  

  - [Servidor WSUS](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a> Archivos de registro de cliente

En las siguientes secciones se indican los archivos de registro relacionados con las operaciones de cliente y la instalación de cliente.  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a> Operaciones de cliente

En la siguiente tabla se muestran los archivos de registro del cliente de Configuration Manager.  

|Nombre del registro|Descripción|  
|--------------|-----------------|  
|ADALOperationProvider.log|Información sobre las solicitudes de token de autenticación de cliente con la biblioteca de autenticación de Azure Active Directory (Azure AD) (ADAL).|
|BitLockerManagementHandler.log|Registra información sobre las directivas de administración de BitLocker.|
|CAS.log|Servicio de acceso a contenido. Mantiene la caché del paquete local en el cliente.|  
|Ccm32BitLauncher.log|Registra las acciones para iniciar aplicaciones en el cliente marcadas como *Ejecutar en modo de 32 bits*.|  
|CcmEval.log|Registra las actividades de evaluación de estado de cliente de Configuration Manager y los detalles de los componentes necesarios para el cliente de Configuration Manager.|  
|CcmEvalTask.log|Registra las actividades de evaluación de estado de cliente de Configuration Manager iniciadas por la tarea programada de evaluación.|  
|CcmExec.log|Registra actividades del cliente y el servicio de host de agente SMS Este archivo de registro también incluye información acerca de cómo habilitar y deshabilitar el proxy de reactivación.|  
|CcmMessaging.log|Registra actividades relacionadas con la comunicación entre el cliente y los puntos de administración.|  
|CCMNotificationAgent.log|Registra actividades relacionadas con las operaciones de notificación de cliente.|  
|Ccmperf.log|Registra actividades relacionadas con el mantenimiento y la captura de datos relacionados con los contadores de rendimiento de cliente.|  
|CcmRestart.log|Registra la actividad de reinicio del servicio de cliente.|  
|CCMSDKProvider.log|Registra actividades de las interfaces SDK de cliente.|  
|ccmsqlce.log|Registra actividades para la edición de SQL Compact que usa el cliente. Normalmente, este registro solo se usa cuando se habilita el registro de depuración o hay un problema con el componente. La tarea de mantenimiento del cliente (ccmeval) suele corregir de forma automática los problemas con este componente.|
|CertificateMaintenance.log|Mantiene los certificados para servicios de dominio de Active Directory y los puntos de administración.|  
|CIDownloader.log|Registra detalles acerca de las descargas de definiciones de elementos de configuración.|  
|CITaskMgr.log|Registra las tareas para cada aplicación y tipo de implementación, como las acciones de descarga de contenido e instalación o desinstalación.|  
|ClientAuth.log|Registra la actividad de autenticación y firma del cliente.|  
|ClientIDManagerStartup.log|Crea y mantiene el GUID de cliente e identifica tareas durante la asignación y el registro de clientes.|  
|ClientLocation.log|Registra tareas relacionadas con la asignación de sitios de cliente.|  
|CMHttpsReadiness.log|Registra los resultados de ejecución de la herramienta de evaluación de preparación de HTTPS de Configuration Manager. Esta herramienta comprueba si los equipos tienen un certificado de autenticación de cliente de infraestructura de clave pública (PKI) que se pueda usar con Configuration Manager.|  
|CmRcService.log|Registra información del servicio de control remoto.|  
|CoManagementHandler.log|Se utiliza para solucionar problemas de administración conjunta en el cliente.|
|ContentTransferManager.log|Programa el Servicio de transferencia inteligente en segundo plano (BITS) o el Bloque de mensajes del servidor (SMB) para descargar paquetes u acceder a ellos.|  
|DataTransferService.log|Registra todas las comunicaciones de BITS para el acceso de directiva o paquete.|  
|DeltaDownload.log|Registra información sobre la descarga de actualizaciones rápidas y actualizaciones descargadas mediante Optimización de entrega.|  
|Diagnostics.log|Registra el estado de las acciones de diagnóstico de cliente.|
|EndpointProtectionAgent|Registra información sobre la instalación del cliente de System Center Endpoint Protection y la aplicación de directivas antimalware en el cliente.|  
|execmgr.log|Registra detalles acerca de los paquetes y las secuencias de tareas que se ejecutan en el cliente.|  
|ExpressionSolver.log|Registra detalles sobre los métodos de detección mejorada que se usan cuando el registro detallado o de depuración está activado.|  
|ExternalEventAgent.log|Registra el historial de detección de malware de Endpoint Protection y eventos relacionados con el estado de cliente.|  
|FileBITS.log|Registra todas las tareas de acceso de paquetes SMB.|  
|FileSystemFile.log|Registra la actividad del proveedor de Instrumental de administración de Windows (WMI) para la recopilación de archivos e inventario de software.|  
|FSPStateMessage.log|Registra la actividad para los mensajes de estado que el cliente envía al punto de estado de reserva.|  
|InternetProxy.log|Registra la actividad de uso y la configuración de proxy de red del cliente.|  
|InventoryAgent.log|Registra actividades de acciones de inventario de hardware, inventario de software y detección de latido en el cliente.|  
|LocationCache.log|Registra la actividad de uso y mantenimiento de la caché de ubicación del cliente.|  
|LocationServices.log|Registra la actividad del cliente para la localización de puntos de administración, puntos de actualización de software y puntos de distribución.|  
|M365AHandler.log|Información sobre la directiva de configuración del Análisis de escritorio|
|MaintenanceCoordinator.log|Registra la actividad de tareas de mantenimiento generales del cliente.|  
|Mifprovider.log|Registra la actividad del proveedor de WMI de archivos de formato de información (MIF) de administración.|  
|mtrmgr.log|Supervisa todos los procesos de disponibilidad de software.|  
|PolicyAgent.log|Registra las solicitudes de las directivas que se hayan realizado mediante el servicio de transferencia de datos.|  
|PolicyAgentProvider.log|Registra los cambios de directiva.|  
|PolicyEvaluator.log|Registra los detalles acerca de la evaluación de directivas en los equipos cliente, incluidas las directivas de las actualizaciones de software.|  
|PolicyPlatformClient.log|Registra el proceso de corrección y cumplimiento para todos los proveedores ubicados en \Archivos de programa\Microsoft Policy Platform, excepto el proveedor de archivos.|  
|PolicySdk.log|Registra actividades de interfaces SDK de sistemas de directivas.|  
|Pwrmgmt.log|Registra información acerca de cómo habilitar o deshabilitar y configurar las opciones del cliente de proxy de reactivación.|  
|PwrProvider.log|Registra las actividades del proveedor de administración de energía (PWRInvProvider) hospedado en el servicio WMI. En todas las versiones compatibles de Windows, el proveedor enumera la configuración actual en los equipos durante el inventario de hardware, y aplica la configuración del plan de energía.|  
|SCClient_&lt;*dominio*\>@&lt;*nombreUsuario*\>_1.log|Registra la actividad del Centro de software para el usuario especificado en el equipo cliente.|  
|SCClient_&lt;*dominio*\>@&lt;*nombreUsuario*\>_2.log|Registra la actividad histórica del Centro de software para el usuario especificado en el equipo cliente.|  
|Scheduler.log|Registra las actividades de las tareas programadas para todas las operaciones de cliente.|  
|SCNotify_&lt;*dominio*\>@&lt;*nombreUsuario*\>_1.log|Registra la actividad para informar a los usuarios acerca del software para el usuario especificado.|  
|SCNotify_&lt;*dominio*\>@&lt;*nombreUsuario*\>_1-&lt;*fecha_hora*>.log|Registra la información histórica de notificación de los usuarios acerca del software para el usuario especificado.|  
|setuppolicyevaluator.log|Registra la creación de directivas de configuración e inventario en WMI.|  
|SleepAgent_&lt;*dominio*\>@SYSTEM_0.log|Archivo de registro principal para el proxy de reactivación.|  
|smscliui.log|Registra el uso del cliente de Configuration Manager en el Panel de control.|  
|SrcUpdateMgr.log|Registra la actividad para las aplicaciones instaladas de Windows Installer que se actualizan con ubicaciones de origen de punto de distribución actual.|  
|StatusAgent.log|Registra mensajes de estado creados por los componentes de cliente.|  
|SWMTRReportGen.log|Genera un informe de datos de uso recopilados por el agente de disponibilidad. Estos datos se registran en Mtrmgr.log.|  
|UserAffinity.log|Registra detalles acerca de la afinidad de dispositivo de usuario.|  
|VirtualApp.log|Registra información específica de la evaluación de los tipos de implementación de Application Virtualization (App-V).|  
|Wedmtrace.log|Registra las operaciones relacionadas con escribir filtros en los clientes de Windows Embedded.|  
|wakeprxy-install.log|Registra la información de instalación cuando los clientes reciben la opción de configuración de cliente para activar un proxy de reactivación.|  
|wakeprxy-uninstall.log|Registra información sobre cómo desinstalar el proxy de reactivación cuando los clientes reciben la opción de configuración de cliente para desactivar el proxy de reactivación, si ya se había activado anteriormente.|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a> Instalación de cliente

En la tabla siguiente se muestran los archivos de registro que contienen información relacionada con la instalación del cliente de Configuration Manager.  

|Nombre del registro|Descripción|  
|--------------|-----------------|  
|ccmsetup.log|Registra tareas de ccmsetup.exe de instalación, actualización y eliminación de cliente. Puede utilizarse para solucionar problemas de instalación de cliente.|  
|ccmsetup-ccmeval.log|Registra tareas de ccmsetup.exe de corrección y estado de cliente.|  
|CcmRepair.log|Registra las actividades de reparación del agente de cliente.|  
|client.msi.log|Registra las tareas de instalación realizadas por client.msi. Puede usarse para solucionar problemas de instalación o eliminación de cliente.|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a> Cliente para Linux y UNIX

> [!Important]  
> A partir de la versión 1902, Configuration Manager no admite clientes Linux o UNIX.
>
> Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

El cliente de Configuration Manager para Linux y UNIX registra información en los archivos de registro siguientes:  

> [!TIP]
> Use CMTrace para ver los archivos de registro del cliente de UNIX y Linux.

|Nombre del registro|Detalles|
|-------------------|-----------------------------------------------------------------|
|Scxcm.log| Archivo de registro para el servicio central del cliente de Configuration Manager para Linux y UNIX (ccmexec.bin). Este archivo de registro contiene información acerca de la instalación y las operaciones en curso de ccmexec.bin. De forma predeterminada, este archivo de registro se encuentra en **/var/opt/microsoft/scxcm.log**. Para cambiar la ubicación del archivo de registro, edite **/opt/microsoft/configmgr/etc/scxcm.conf** y cambie el campo **PATH**. No es necesario reiniciar el equipo cliente o el servicio para que el cambio surta efecto. Puede establecer el nivel de registro en una de cuatro opciones distintas. |
| Scxcmprovider.log |Archivo de registro del servicio CIM del cliente de Configuration Manager para Linux y UNIX (omiserver.bin). Este archivo de registro contiene información acerca de las operaciones en curso de nwserver.bin. Este registro se encuentra en `/var/opt/microsoft/configmgr/scxcmprovider.log`. Para cambiar la ubicación del archivo de registro, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** y cambie el campo **PATH**. No es necesario reiniciar el equipo cliente o el servicio para que el cambio surta efecto. Puede establecer el nivel de registro en una de tres opciones.|

Ambos archivos de registro admiten varios niveles de registro:  

- **scxcm.log**. Para cambiar el nivel de registro, edite **/opt/microsoft/configmgr/etc/scxcm.conf** y cambie cada instancia de la etiqueta **MODULE** por el nivel de registro que quiera:  

  - ERROR: Indica problemas que requieren atención.  

  - WARNING: Indica posibles problemas en las operaciones de cliente.  

  - INFO: Registro más detallado que indica el estado de varios eventos en el cliente.  

  - TRACE: Registro detallado que normalmente se usa para diagnosticar problemas.  

- **scxcmprovider.log**. Para cambiar el nivel de registro, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** y cambie cada instancia de la etiqueta **MODULE** por el nivel de registro que quiera:  

  - ERROR: Indica problemas que requieren atención.  

  - WARNING: Indica posibles problemas en las operaciones de cliente.

  - INFO: Registro más detallado que indica el estado de varios eventos en el cliente.  

En condiciones normales de funcionamiento, use el nivel de registro ERROR. Este nivel de registro crea el archivo de registro más pequeño. A medida que el nivel de registro aumenta de ERROR a WARNING, INFO y TRACE, se crea un archivo de registro mayor, ya que se escriben más datos en el archivo.  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a> Administrar archivos de registro para el cliente UNIX y Linux

El cliente para Linux y UNIX no limita el tamaño máximo de los archivos de registro del cliente. Tampoco copia automáticamente el contenido de sus archivos .log en otro archivo, como en un archivo .lo_. Si desea controlar el tamaño máximo de los archivos de registro, implemente un proceso para administrar los archivos de registro independiente del cliente de Configuration Manager para Linux y UNIX.  

Por ejemplo, puede usar el comando estándar de Linux y UNIX **logrotate** para administrar el tamaño y la rotación de los archivos de registro de cliente. El cliente de Configuration Manager para Linux y UNIX tiene una interfaz que permite a **logrotate** indicar al cliente la finalización de la rotación del registro, lo que permite al cliente reanudar el registro en el archivo de registro.  

Para obtener información acerca de **logrotate**, consulte la documentación de las distribuciones de Linux y UNIX que utiliza.  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a> Cliente para equipos Mac

El cliente de Configuration Manager para equipos Mac registra la información en los archivos de registro siguientes en el equipo Mac:  

|Nombre del registro|Detalles|Ubicación|
|--------------|-------------|-------------|
|CCMClient-&lt;*fecha_hora*>.log|Registra actividades relacionadas con operaciones de cliente de Mac, como la administración de aplicaciones, el inventario y el registro de errores.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent-&lt;*fecha_hora*>.log|Registra información relacionada con las operaciones de cliente, como las operaciones de inicio y cierre de sesión de usuario, y la actividad del equipo Mac.| `~/Library/Logs`|  
|CCMNotifications-&lt;*fecha_hora*>.log|Registra las actividades relacionadas con las notificaciones de Configuration Manager que se muestran en el equipo Mac.| `~/Library/Logs`|  
|CCMPrefPane-&lt;*fecha_hora*>.log|Registra las actividades relacionadas con el cuadro de diálogo de preferencias de Configuration Manager en el equipo Mac, como el estado general y el registro de errores.| `~/Library/Logs`|  

El archivo de registro **SMS_DM.log** del servidor de sistema de sitio además registra la comunicación entre equipos Mac y el punto de administración que está configurado para dispositivos móviles y equipos Mac.  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a> Archivos de registro del servidor

En las siguientes secciones se indican los archivos de registro que se encuentran en el servidor de sitio o que están relacionados con determinados roles de sistema de sitio.  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a> Servidor del sitio y sistemas de sitio

En la tabla siguiente se incluyen los archivos de registro que se encuentra en los servidores de sistema de sitio y en el servidor de sitio de Configuration Manager.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Registra la actividad de procesamiento de inscripción.|Servidor de sitio|  
|ADForestDisc.log|Registra acciones de detección de bosques de Active Directory.|Servidor de sitio|  
|adminservice.log|Graba las acciones para la API REST del servicio de administración del proveedor de SMS.|Equipo con el proveedor de SMS|
|ADService.log|Registra la creación de cuentas y los detalles del grupo de seguridad en Active Directory.|Servidor de sitio|  
|adsgdis.log|Registra acciones de detección de grupos de Active Directory.|Servidor de sitio|  
|adsysdis.log|Registra acciones de detección de sistema de Active Directory.|Servidor de sitio|  
|adusrdis.log|Registra acciones de detección de usuarios de Active Directory.|Servidor de sitio|  
|BusinessAppProcessWorker.log|Registra el procesamiento de aplicaciones de Microsoft Store para Empresas.|Servidor de sitio|
|ccm.log|Registra las actividades de instalación de inserción de cliente.|Servidor de sitio|  
|CertMgr.log|Registra actividades de certificado de comunicaciones dentro de sitios.|Servidor de sistema de sitio|  
|chmgr.log|Registra las actividades del administrador de mantenimiento del cliente.|Servidor de sitio|  
|Cidm.log|Registra los cambios realizados en la configuración de cliente por el administrador de datos de instalación de cliente (CIDM).|Servidor de sitio|  
|CollectionAADGroupSyncWorker.log | A partir de la versión 2002, archivo de registro para la sincronización de los resultados de pertenencia a colecciones con Azure Active Directory. En la versión 1910 y anteriores, el registro de esta característica se combinaba en SMS_AZUREAD_DISCOVERY_AGENT.log. | Servidor de sitio|
|colleval.log|Registra los detalles acerca de la creación, cambio y eliminación de recopilaciones por parte del Evaluador de recopilaciones.|Servidor de sitio|  
|compmon.log|Registra el estado de los subprocesos de componente supervisados del servidor de sitio.|Servidor de sistema de sitio|  
|compsumm.log|Registra tareas del generador de resumen de estado de componente.|Servidor de sitio|  
|ComRegSetup.log|Registra los resultados de la instalación inicial del registro de COM para un servidor de sitio.|Servidor de sistema de sitio|  
|dataldr.log|Registra información sobre el procesamiento de archivos MIF y el inventario de hardware en la base de datos de Configuration Manager.|Servidor de sitio|  
|ddm.log|Registra actividades del administrador de datos de detección.|Servidor de sitio|  
|despool.log|Registra las transferencias de comunicaciones de sitio a sitio entrantes.|Servidor de sitio|  
|distmgr.log|Registra detalles acerca de las actualizaciones de información, la creación, la compresión y la replicación de datos de paquetes. También puede incluir otras actividades del componente del administrador de distribución. Por ejemplo, la instalación de un punto de distribución, los intentos de conexión y la instalación de componentes. Para obtener más información sobre otras funciones que usan este registro, vea [Punto de conexión de servicio](#BKMK_WITLog) e [Implementación de sistema operativo](#BKMK_OSDLog).|Servidor de sitio|  
|EPCtrlMgr.log|Registra información sobre la sincronización de información de amenazas de malware desde el servidor de rol de sistema de sitio de Endpoint Protection en la base de datos de Configuration Manager.|Servidor de sitio|  
|EPMgr.log|Registra el estado del rol de sistema de sitio de Endpoint Protection.|Servidor de sistema de sitio|  
|EPSetup.log|Proporciona información sobre la instalación del rol de sistema de sitio de Endpoint Protection.|Servidor de sistema de sitio|  
|EnrollSrv.log|Registra actividades del proceso de servicio de inscripción.|Servidor de sistema de sitio|  
|EnrollWeb.log|Registra actividades del proceso de sitio web de inscripción.|Servidor de sistema de sitio|  
|fspmgr.log|Registra las actividades del rol de sistema de sitio de punto de estado de reserva.|Servidor de sistema de sitio|  
|hman.log|Registra información sobre los cambios de configuración de sitio y la publicación de información de sitio en Servicios de dominio de Active Directory.|Servidor de sitio|  
|Inboxast.log|Registra los archivos que se mueven del punto de administración a la carpeta INBOXES correspondiente en el servidor de sitio.|Servidor de sitio|  
|inboxmgr.log|Registra actividades de transferencia de archivos entre las carpetas de bandeja de entrada.|Servidor de sitio|  
|inboxmon.log|Registra el procesamiento de archivos de la bandeja de entrada y las actualizaciones de contador de rendimiento.|Servidor de sitio|  
|invproc.log|Registra el reenvío de archivos MIF de un sitio secundario a su sitio primario.|Servidor de sitio|  
|migmctrl.log|Registra información sobre las acciones de migración que implican trabajos de migración, puntos de distribución compartidos y actualizaciones de puntos de distribución.|Sitio de nivel superior de la jerarquía de Configuration Manager y cada sitio primario secundario. En una jerarquía de varios sitios primarios, use el archivo de registro creado en el sitio de administración central.|  
|mpcontrol.log|Registra el registro del punto de administración en el Servicio de nombres de Internet de Windows (WINS). Registra la disponibilidad del punto de administración cada 10 minutos.|Servidor de sistema de sitio|  
|mpfdm.log|Registra las acciones del componente de punto de administración que mueve los archivos de cliente a la carpeta INBOXES correspondiente en el servidor de sitio.|Servidor de sistema de sitio|  
|mpMSI.log|Registra los detalles sobre la instalación de un punto de administración.|Servidor de sitio|  
|MPSetup.log|Registra el proceso empaquetador de instalación de punto de administración.|Servidor de sitio|  
|netdisc.log|Registra acciones de detección de redes.|Servidor de sitio|  
|NotiCtrl.log|Notificaciones de solicitud de la aplicación.|Servidor de sitio|  
|ntsvrdis.log|Registra la actividad de detección de servidores de sistema de sitio.|Servidor de sitio|  
|Objreplmgr|Registra el procesamiento de notificaciones de cambio de objeto para la replicación.|Servidor de sitio|  
|offermgr.log|Registra actualizaciones de anuncio.|Servidor de sitio|  
|offersum.log|Registra el resumen de mensajes de estado de implementación.|Servidor de sitio|  
|OfflineServicingMgr.log|Registra actividades de aplicación de actualizaciones a archivos de imagen de sistema operativo.|Servidor de sitio|  
|outboxmon.log|Registra el procesamiento de archivos de la bandeja de salida y las actualizaciones de contador de rendimiento.|Servidor de sitio|  
|PerfSetup.log|Registra los resultados de la instalación de contadores de rendimiento.|Servidor de sistema de sitio|  
|PkgXferMgr.log|Registra las acciones del componente SMS_Executive que se encarga de enviar contenido desde un sitio primario a un punto de distribución remoto.|Servidor de sitio|  
|policypv.log|Registra las actualizaciones de las directivas de cliente para reflejar cambios de configuraciones o implementaciones de cliente.|Servidor de sitio primario|  
|rcmctrl.log|Registra las actividades de replicación de base de datos entre los sitios de la jerarquía.|Servidor de sitio|  
|replmgr.log|Registra la replicación de archivos entre los componentes de servidor de sitio y el componente de programador.|Servidor de sitio|  
|ResourceExplorer.log|Registra errores, advertencias e información sobre la ejecución del Explorador de recursos.|Equipo que ejecuta la consola de Configuration Manager|  
|RESTPROVIDERSetup.log|Instalación de la API REST del servicio de administración del proveedor de SMS.|Equipo con el proveedor de SMS|
|ruleengine.log|Registra detalles acerca de las reglas de implementación automática de identificación, descarga de contenido y creación de grupos de actualizaciones de software e implementación.|Servidor de sitio|  
|schedule.log|Registra detalles acerca de la replicación de archivos y trabajos de sitio a sitio.|Servidor de sitio|  
|sender.log|Registros los archivos que se transfieren mediante la replicación basada en archivos entre sitios.|Servidor de sitio|  
|sinvproc.log|Registra información acerca del procesamiento de datos de inventario de software en la base de datos del sitio.|Servidor de sitio|  
|sitecomp.log|Registra detalles sobre el mantenimiento de los componentes de sitio instalados en todos los servidores de sistema de sitio en el sitio.|Servidor de sitio|  
|sitectrl.log|Registra cambios de configuración de sitio realizados en objetos de control de sitio en la base de datos.|Servidor de sitio|  
|sitestat.log|Registra el proceso de supervisión de disponibilidad y espacio en disco de todos los sistemas de sitio.|Servidor de sitio|
|SMS_AZUREAD_DISCOVERY_AGENT.log| Archivo de registro para la detección de usuarios y grupos de usuarios de Azure Active Directory (Azure AD). En la versión 1910 y anteriores, también se incluía la sincronización de los resultados de la pertenencia a colecciones en Azure AD.| Servidor de sitio|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Archivo de registro del componente que sincroniza las aplicaciones de Microsoft Store para Empresas.|Servidor de sitio|
|SMS_ISVUPDATES_SYNCAGENT.log| Archivo de registro para la sincronización de actualizaciones de software de terceros.| Actualización de software de nivel superior de la jerarquía de Configuration Manager.|
|SMS_OrchestrationGroup.log| Archivo de registro para grupos de orquestaciones|Servidor de sitio|
|SMS_PhasedDeployment.log| Archivo de registro de las implementaciones por fases|Sitio de nivel superior de la jerarquía de Configuration Manager|
|SMS_REST_PROVIDER.log|Estado de mantenimiento del servicio para la API de REST del servicio de administración del proveedor de SMS, incluida información de certificado.|Equipo con el proveedor de SMS|
|SmsAdminUI.log|Registra la actividad de consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SMSAWEBSVCSetup.log|Registra las actividades de instalación del servicio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|smsbkup.log|Registra el resultado de la salida del proceso de copia de seguridad de sitio.|Servidor de sitio|  
|smsdbmon.log|Registra los cambios de la base de datos.|Servidor de sitio|  
|SMSENROLLSRVSetup.log|Registra las actividades de instalación del servicio web de inscripción.|Servidor de sistema de sitio|  
|SMSENROLLWEBSetup.log|Registra las actividades de instalación de sitio web de inscripción.|Servidor de sistema de sitio|  
|smsexec.log|Registra el procesamiento de todos los subprocesos de componente de servidor de sitio.|Servidor de sitio o servidor de sistema de sitio|  
|SMSFSPSetup.log|Registra mensajes generados por la instalación de un punto de estado de reserva.|Servidor de sistema de sitio|  
|SMSPORTALWEBSetup.log|Registra las actividades de instalación del sitio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|SMSProv.log|Registra el acceso del proveedor de WMI a la base de datos del sitio.|Equipo con el proveedor de SMS|  
|srsrpMSI.log|Registra resultados detallados del proceso de instalación del punto de notificación desde la salida de MSI.|Servidor de sistema de sitio|  
|srsrpsetup.log|Registra los resultados del proceso de instalación del punto de notificación.|Servidor de sistema de sitio|  
|statesys.log|Registra el procesamiento de mensajes de sistema de estado.|Servidor de sitio|  
|statmgr.log|Registra la escritura de todos los mensajes de estado en la base de datos.|Servidor de sitio|  
|swmproc.log|Registra el procesamiento de archivos y configuraciones de disponibilidad.|Servidor de sitio|  

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a> Instalación del servidor del sitio

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la instalación de sitios.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Registra actividades de instalación y evaluación de componente de requisito previo.|Servidor de sitio|  
|ConfigMgrSetup.log|Registra resultados detallados del programa de instalación de servidor de sitio.|Servidor de sitio|  
|ConfigMgrSetupWizard.log|Registra información relacionada con la actividad del Asistente para instalación.|Servidor de sitio|  
|SMS_BOOTSTRAP.log|Registra información sobre el progreso del inicio del proceso de instalación de sitio secundario. Los detalles del proceso de instalación figuran en ConfigMgrSetup.log.|Servidor de sitio|  
|smstsvc.log|Registra información sobre la instalación, el uso y la eliminación de un servicio de Windows. Windows usa este servicio para probar la conectividad de red y los permisos entre servidores. Usa la cuenta de equipo del servidor que crea la conexión.|Registros de servidor de sistema de sitio y servidor de sitio|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a> Punto de servicio de Data Warehouse

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el punto de servicio del almacenamiento de datos.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|DWSSMSI.log|Registra mensajes generados por la instalación de un punto de servicio de almacenamiento de datos.|Servidor de sistema de sitio|  
|DWSSSetup.log|Registra mensajes generados por la instalación de un punto de servicio de almacenamiento de datos.|Servidor de sistema de sitio|  
|Microsoft.ConfigMgrDataWarehouse.log|Registra información acerca de la sincronización de datos entre la base de datos de sitio y la base de datos de almacenamiento de datos.|Servidor de sistema de sitio|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a> Punto de estado de reserva

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el punto de estado de reserva.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Registra detalles acerca de las comunicaciones con el punto de estado de reserva de los clientes heredados de dispositivo móvil y los equipos cliente.|Servidor de sistema de sitio|  
|fspMSI.log|Registra mensajes generados por la instalación de un punto de estado de reserva.|Servidor de sistema de sitio|  
|fspmgr.log|Registra las actividades del rol de sistema de sitio de punto de estado de reserva.|Servidor de sistema de sitio|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a> Punto de administración

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el punto de administración.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Registra actividades de mensajes de cliente en el extremo.|Servidor de sistema de sitio|  
|MP_CliReg.log|Registra la actividad de registro de cliente procesada por el punto de administración.|Servidor de sistema de sitio|  
|MP_Ddr.log|Registra la conversión de registros XML.ddr de clientes y luego los copia en el servidor de sitio.|Servidor de sistema de sitio|  
|MP_Framework.log|Registra las actividades de los componentes principales del punto de administración y del marco de cliente.|Servidor de sistema de sitio|  
|MP_GetAuth.log|Registra la actividad de autorización de cliente.|Servidor de sistema de sitio|  
|MP_GetPolicy.log|Registra las actividades de solicitud de directiva de equipos cliente.|Servidor de sistema de sitio|  
|MP_Hinv.log|Registra detalles acerca de la conversión de registros XML de inventario de hardware de clientes y los copia en el servidor de sitio.|Servidor de sistema de sitio|  
|MP_Location.log|Registra actividades de respuesta y solicitud de ubicación de clientes.|Servidor de sistema de sitio|  
|MP_OOBMgr.log|Registra las actividades de punto de administración relacionadas con la recepción de una OTP de un cliente.|Servidor de sistema de sitio|  
|MP_Policy.log|Registra la comunicación de directivas.|Servidor de sistema de sitio|  
|MP_Relay.log|Registra la transferencia de archivos recopilados del cliente.|Servidor de sistema de sitio|  
|MP_Retry.log|Registra procesos de reintento de inventario de hardware.|Servidor de sistema de sitio|  
|MP_Sinv.log|Registra detalles acerca de la conversión de registros XML de inventario de software de clientes y los copia en el servidor de sitio.|Servidor de sistema de sitio|  
|MP_SinvCollFile.log|Registra los detalles acerca de la recopilación de archivos.|Servidor de sistema de sitio|  
|MP_Status.log|Registra detalles acerca de la conversión de archivos XML.svf de mensaje de estado de clientes y los copia en el servidor de sitio.|Servidor de sistema de sitio|
|mpcontrol.log|Registra el registro del punto de administración en WINS. Registra la disponibilidad del punto de administración cada 10 minutos.|Servidor de sitio|  
|mpfdm.log|Registra las acciones del componente de punto de administración que mueve los archivos de cliente a la carpeta INBOXES correspondiente en el servidor de sitio.|Servidor de sistema de sitio|  
|mpMSI.log|Registra los detalles sobre la instalación de un punto de administración.|Servidor de sitio|  
|MPSetup.log|Registra el proceso empaquetador de instalación de punto de administración.|Servidor de sitio|  
|UserService.log|Graba las solicitudes de usuario del Centro de software, recuperando o instalando aplicaciones disponibles para el usuario desde el servidor.|Servidor de sistema de sitio|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a> Punto de conexión de servicio

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el punto de conexión de servicio.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Registra información de cuenta de proxy y de certificado.|Servidor de sitio|  
|colleval.log|Registra los detalles acerca de la creación, cambio y eliminación de recopilaciones por parte del Evaluador de recopilaciones.|Sitio primario y sitio de administración central|  
|Cloudusersync.log|Registra la habilitación de licencia de usuarios.|Equipo con el punto de conexión de servicio|  
|dataldr.log|Registra información sobre el procesamiento de archivos MIF.|Servidor de sitio|  
|ddm.log|Registra actividades del administrador de datos de detección.|Servidor de sitio|  
|distmgr.log|Registra detalles acerca de las solicitudes de distribución de contenido.|Servidor de sitio de nivel superior|  
|Dmpdownloader.log|Registra detalles sobre las descargas desde Microsoft Intune.|Equipo con el punto de conexión de servicio|  
|Dmpuploader.log|Registra detalles relacionados con la carga de cambios de base de datos en Microsoft Intune.|Equipo con el punto de conexión de servicio|  
|hman.log|Registra información acerca del reenvío de mensajes.|Servidor de sitio|  
|MSfBSyncWorker.log|Registra información sobre la comunicación con Microsoft Store para Empresas.|Equipo con el punto de conexión de servicio|
|objreplmgr.log|Registra el procesamiento de directivas y asignaciones.|Servidor de sitio primario|  
|policypv.log|Registra la generación de directivas de todas las directivas.|Servidor de sitio|  
|outgoingcontentmanager.log|Registra el contenido cargado en Microsoft Intune.|Equipo con el punto de conexión de servicio|  
|sitecomp.log|Registra los detalles de la instalación del de punto de conexión de servicio.|Servidor de sitio|  
|SmsAdminUI.log|Registra la actividad de consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SMS_CLOUDCONNECTION.log|Registra información sobre los servicios en la nube.|Equipo con el punto de conexión de servicio|
|SMSProv.log|Registra las actividades del proveedor de SMS. Las actividades de la consola de Configuration Manager usan el proveedor de SMS.|Equipo con el proveedor de SMS|  
|SrvBoot.log|Registra los detalles sobre el servicio de instalador de punto de conexión de servicio.|Equipo con el punto de conexión de servicio|  
|Statesys.log|Registra el procesamiento de mensajes de administración de dispositivos móviles.|Sitio primario y sitio de administración central|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a> Punto de actualización de software

En la tabla siguiente se indican los archivos de registro que contienen información relacionada con el punto de actualización de software.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Registra detalles sobre la replicación de archivos de notificación de actualizaciones de software de un sitio primario a sitios secundarios.|Servidor de sitio|  
|PatchDownloader.log|Registra detalles sobre el proceso de descarga de actualizaciones de software del origen de actualizaciones al destino de descarga en el servidor de sitio.|Al descargar las actualizaciones manualmente, este archivo está en el directorio `%temp%` del equipo en el que usa la consola. Para las reglas de implementación automática, si el cliente de Configuration Manager está instalado en el servidor de sitio, este archivo está en el servidor de sitio en `%windir%\CCM\Logs`.|  
|ruleengine.log|Registra detalles acerca de las reglas de implementación automática de identificación, descarga de contenido y creación de grupos de actualizaciones de software e implementación.|Servidor de sitio|
|SMS_ISVUPDATES_SYNCAGENT.log| Archivo de registro para la sincronización de actualizaciones de software de terceros.| Actualización de software de nivel superior de la jerarquía de Configuration Manager.|
|SUPSetup.log|Registra detalles acerca de la instalación de un punto de actualización de software. Cuando se completa la instalación del punto de actualización de software, **Installation was successful** se escribe en este archivo de registro.|Servidor de sistema de sitio|  
|WCM.log|Registra los detalles sobre la configuración del punto de actualización de software y las conexiones con el servidor WSUS para las clasificaciones, idiomas y categorías de actualizaciones suscritas.|Servidor de sitio que se conecta al servidor WSUS|  
|WSUSCtrl.log|Registra los detalles acerca de la configuración, la conectividad de base de datos y el estado del servidor WSUS para el sitio.|Servidor de sistema de sitio|  
|wsyncmgr.log|Registra detalles sobre el proceso de sincronización de actualizaciones de software.|Servidor de sistema de sitio|  
|WUSSyncXML.log|Registra detalles sobre la herramienta de inventario para el proceso de sincronización de Microsoft Updates.|Equipo cliente configurado como host de sincronización para la herramienta de inventario para Microsoft Updates|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a> Archivos de registro por funcionalidad

En las secciones siguientes se muestran archivos de registro relacionados con las funciones de Configuration Manager.  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a> Administración de aplicaciones

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la administración de aplicaciones.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Registra los detalles sobre el estado actual y previsto de las aplicaciones, su aplicabilidad, los tipos de implementación, las dependencias y si se cumplieron los requisitos.|Cliente|  
|AppDiscovery.log|Registra los detalles sobre la detección de aplicaciones en equipos cliente.|Cliente|  
|AppEnforce.log|Registra detalles acerca de las medidas de cumplimiento (instalar y desinstalar) que las aplicaciones llevan a cabo en el cliente.|Cliente|  
|AppGroupHandler.log|A partir de la versión 1906, la información de detección y ejecución para los grupos de aplicaciones.|Cliente|
|awebsctl.log|Registra actividades de supervisión del rol de sistema de sitio de punto de servicio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|awebsvcMSI.log|Registra información detallada de instalación del rol de sistema de sitio de punto de servicio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|BusinessAppProcessWorker.log|Registra el procesamiento de aplicaciones de Microsoft Store para Empresas.|Servidor de sitio|
|CCMSDKProvider.log|Registra las actividades del SDK de administración de aplicaciones.|Cliente|  
|colleval.log|Registra los detalles acerca de la creación, cambio y eliminación de recopilaciones por parte del Evaluador de recopilaciones.|Servidor de sistema de sitio|  
|ConfigMgrSoftwareCatalog.log|Registra la actividad del catálogo de aplicaciones, que incluye el uso de Silverlight.|Cliente|  
|MSfBSyncWorker.log|Registra información sobre la comunicación con Microsoft Store para Empresas.|Equipo con el punto de conexión de servicio|
|NotiCtrl.log|Notificaciones de solicitud de la aplicación.|Servidor de sitio|  
|portlctl.log|Registra las actividades de supervisión del rol de sistema de sitio de punto de sitios web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|portlwebMSI.log|Registra la actividad de instalación de MSI del rol de sitio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|PrestageContent.log|Registra detalles sobre el uso de la herramienta ExtractContent.exe en un punto de distribución preconfigurado remoto. Esta herramienta extrae el contenido que ha sido exportado a un archivo.|Servidor de sistema de sitio|  
|ServicePortalWebService.log|Registra la actividad del servicio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|ServicePortalWebSite.log|Registra la actividad del sitio web del catálogo de aplicaciones.|Servidor de sistema de sitio|  
|SettingsAgent.log|La ejecución de aplicaciones específicas, la orquestación de registros de evaluación del grupo de aplicaciones y los detalles de las directivas de administración conjunta.|Cliente|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Archivo de registro del componente que sincroniza las aplicaciones de Microsoft Store para Empresas.|Servidor de sitio|
|SMS_CLOUDCONNECTION.log|Registra información sobre los servicios en la nube.|Equipo con el punto de conexión de servicio|
|SMSdpmon.log|Registra los detalles acerca de la tarea programada de supervisión de estado de punto de distribución configurada en un punto de distribución.|Servidor de sitio|  
|SoftwareCatalogUpdateEndpoint.log|Registra actividades para administrar la dirección URL del catálogo de aplicaciones que se muestra en el Centro de software.|Cliente|  
|SoftwareCenterSystemTasks.log|Registra actividades relacionadas con la validación de componente de requisito previo del Centro de software.|Cliente|  

#### <a name="packages-and-programs"></a>Paquetes y programas

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la implementación de paquetes y programas.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|colleval.log|Registra los detalles acerca de la creación, cambio y eliminación de recopilaciones por parte del Evaluador de recopilaciones.|Servidor de sitio|  
|execmgr.log|Registra los detalles acerca de los paquetes y las secuencias de tareas que se ejecutan.|Cliente|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a> Asset Intelligence

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con Asset Intelligence.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Registra las actividades de las acciones de inventario de Asset Intelligence.|Cliente|  
|aikbmgr.log|Registra los detalles acerca del procesamiento de archivos XML de la bandeja de entrada para la actualización del catálogo Asset Intelligence.|Servidor de sitio|  
|AIUpdateSvc.log|Registra la interacción del punto de sincronización de Asset Intelligence con el servicio en la nube.|Servidor de sistema de sitio|  
|AIUSMSI.log|Registra detalles sobre la instalación del rol de sistema de sitio de punto de sincronización de Asset Intelligence.|Servidor de sistema de sitio|  
|AIUSSetup.log|Registra detalles sobre la instalación del rol de sistema de sitio de punto de sincronización de Asset Intelligence.|Servidor de sistema de sitio|  
|ManagedProvider.log|Registra detalles acerca de la detección de software con una etiqueta de identificación de software asociada. También registra actividades relacionadas con el inventario de hardware.|Servidor de sistema de sitio|  
|MVLSImport.log|Registra detalles acerca del procesamiento de archivos de licencia importados.|Servidor de sistema de sitio|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a> Copia de seguridad y recuperación

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con acciones de copia de seguridad y de recuperación, incluidos el restablecimiento de sitio y los cambios en el proveedor de SMS.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Registra información sobre tareas del programa de instalación y de recuperación cuando Configuration Manager recupera un sitio mediante una copia de seguridad.|Servidor de sitio|  
|smsbkup.log|Registra los detalles acerca de la actividad de la copia de seguridad del sitio.|Servidor de sitio|  
|smssqlbkup.log|Registra la salida del proceso de copia de seguridad de la base de datos del sitio cuando se instala SQL Server en un servidor que no es el servidor del sitio.|Servidor de base de datos del sitio|  
|Smswriter.log|Registra información sobre el estado de Configuration Manager VSS Writer utilizado por el proceso de copia de seguridad.|Servidor de sitio|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a> Inscripción de certificado

En la tabla siguiente se incluyen los archivos de registro de Configuration Manager que contienen información relacionada con la inscripción de certificados. La inscripción de certificados usa el punto de registro de certificados y el módulo de directivas de Configuration Manager en el servidor que ejecuta el servicio de inscripción de dispositivos de red (NDES).  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|Crp.log|Registra actividades de inscripción.|Punto de registro de certificados|  
|Crpctrl.log|Registra el estado operativo del punto de registro de certificado.|Punto de registro de certificados|  
|Crpsetup.log|Registra detalles sobre la instalación y configuración del punto de registro de certificado.|Punto de registro de certificados|  
|Crpmsi.log|Registra detalles sobre la instalación y configuración del punto de registro de certificado.|Punto de registro de certificados|  
|NDESPlugin.log|Registra actividades de inscripción de certificado y verificación de desafío.|Módulo de directivas de Configuration Manager y el servicio de inscripción de dispositivos de red|  

Junto con los archivos de registro de Configuration Manager, revise los registros de aplicaciones de Windows en el Visor de eventos del servidor que ejecuta el Servicio de inscripción de dispositivos de red y el servidor en el que se hospeda el punto de registro de certificado. Por ejemplo, busque mensajes del origen **NetworkDeviceEnrollmentService**.

También puede utilizar los siguientes archivos de registro:  

- Archivos de registro de IIS para el Servicio de inscripción de dispositivos de red: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- Archivos de registro de IIS para el punto de registro de certificados: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- Archivo de registro de directiva de inscripción de dispositivos de red: **mscep.log**  

    > [!NOTE]  
    > Este archivo se encuentra en la carpeta del perfil de la cuenta de NDES, por ejemplo, en C:\Users\SCEPSvc. Para más información sobre cómo habilitar los registros de NDES, vea la sección [Habilitar registros](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) de la wiki de NDES.  

### <a name="client-notification"></a><a name="BKMK_BGB"></a> Notificación de cliente

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la notificación de cliente.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Registra detalles sobre actividades del servidor de sitio relacionadas con tareas de notificación de cliente y procesamiento en línea, y archivos de estado de tarea.|Servidor de sitio|  
|BGBServer.log|Registra las actividades del servidor de notificación, como la comunicación entre cliente y servidor y las tareas de inserción en clientes. También registra información sobre la generación de archivos de estado de tareas y en línea que se enviarán al servidor del sitio.|Punto de administración|  
|BgbSetup.log|Registra las actividades del proceso empaquetador de instalación de servidor de notificaciones durante la instalación y desinstalación.|Punto de administración|  
|bgbisapiMSI.log|Registra los detalles sobre la instalación y desinstalación del servidor de notificaciones.|Punto de administración|  
|BgbHttpProxy.log|Registra las actividades del proxy HTTP de notificación cuando retransmite mensajes de clientes que utilizan HTTP a y desde el servidor de notificaciones.|Cliente|  
|CCMNotificationAgent.log|Registra actividades del agente de notificación, por ejemplo, la comunicación entre cliente y servidor e información sobre las tareas recibidas y enviadas a otros agentes cliente.|Cliente|  

### <a name="cloud-management-gateway"></a>Puerta de enlace de administración en la nube

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la puerta de enlace de administración en la nube.

|Nombre del registro|Descripción|Equipo con el archivo de registro|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Registra detalles sobre la implementación del servicio de puerta de enlace de administración en la nube, el estado del servicio en curso y datos de uso asociados con el servicio. Para configurar el nivel de registro, edite el valor de **Nivel de registro** en la siguiente clave del Registro: `HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|La carpeta *installdir* en el servidor de sitio primario o CAS.|
|CMGSetup.log <sup>[Nota 1](#bkmk_note1)</sup>|Registra detalles sobre la segunda fase de la implementación de Cloud Management Gateway (implementación local en Azure). Para configurar el nivel de registro, use la opción **Nivel de seguimiento** (**Información** (predeterminada), **Detallado**, **Error**) en la pestaña **Azure Portal\Configuración de servicios en la nube**.|**%approot%\logs** en el servidor de Azure o la carpeta SMS/Registros en el servidor de sistema de sitio|
|CMGService.log <sup>[Nota 1](#bkmk_note1)</sup>|Registra detalles sobre el componente principal del servicio Cloud Management Gateway en Azure. Para configurar el nivel de registro, use la opción **Nivel de seguimiento** (**Información** (predeterminada), **Detallado**, **Error**) en la pestaña **Azure Portal\Configuración de servicios en la nube**.|**%approot%\logs** en el servidor de Azure o la carpeta SMS/Registros en el servidor de sistema de sitio|
|SMS_Cloud_ProxyConnector.log|Registra detalles sobre la configuración de conexiones entre el servicio de puerta de enlace de administración en la nube y el punto de conexión de la puerta de enlace de administración en la nube.|Servidor de sistema de sitio|
|CMGContentService.log <sup>[Nota 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->Al habilitar una instancia de CMG para que también sirva contenido del almacenamiento de Azure, este registro almacena los detalles de ese servicio.|**%approot%\logs** en el servidor de Azure o la carpeta SMS/Registros en el servidor de sistema de sitio|

- Para solucionar problemas con implementaciones, use **CloudMgr.log** y **CMGSetup.log**
- Para solucionar problemas de estado del servicio, utilice **CMGService.log** y **SMS_Cloud_ProxyConnector.log**.
- Para solucionar problemas de tráfico de cliente, utilice **CMGHttpHandler.log**, **CMGService.log** y **SMS_Cloud_ProxyConnector.log**.

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a> Nota 1: Registros sincronizados desde Azure

Se trata de archivos de registro locales de Configuration Manager que el administrador de servicio en la nube sincroniza desde Azure Storage cada cinco minutos. Cloud Management Gateway inserta registros en Azure Storage cada cinco minutos. Por tanto, el retraso máximo es de 10 minutos. Los modificadores detallados afectan a los registros locales y remotos. Los nombres de archivo reales incluyen el nombre de servicio y el identificador de instancia de rol. Por ejemplo, CMG-*NombreDeServicio*-*IDInstanciaDeRol*-CMGSetup.log

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a> Configuración de cumplimiento y acceso a los recursos de la compañía

En la tabla siguiente se muestran los archivos de registro que contienen información relacionada con la configuración de cumplimiento y el acceso a los recursos de la compañía.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Registra detalles sobre el proceso de corrección y cumplimiento de configuraciones de cumplimiento, actualizaciones de software y administración de aplicaciones.|Cliente|  
|CITaskManager.log|Registra información acerca de la programación de tareas de elemento de configuración.|Cliente|  
|DCMAgent.log|Registra información de alto nivel acerca de la evaluación, notificación de conflictos y corrección de elementos de configuración y aplicaciones.|Cliente|  
|DCMReporting.log|Registra información acerca de resultados de plataforma de directiva de informes en mensajes de estado de elementos de configuración.|Cliente|  
|DcmWmiProvider.log|Registra información sobre la lectura de synclets de elemento de configuración de WMI.|Cliente|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Consola de Configuration Manager

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la consola de Configuration Manager.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Registra la instalación de la consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SmsAdminUI.log|Registra información acerca del funcionamiento de la consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SMSProv.log|Registra las actividades del proveedor de SMS. Las actividades de la consola de Configuration Manager usan el proveedor de SMS.|Servidor de sitio o servidor de sistema de sitio|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a> Administración de contenido

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la administración de contenido.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Registra detalles de un determinado punto de distribución basado en la nube, como información acerca del acceso a almacenamiento y contenido.|Servidor de sistema de sitio|  
|CloudMgr.log|Registra detalles sobre el aprovisionamiento de contenido, la recopilación de estadísticas de ancho de banda y almacenamiento, y las acciones iniciadas por el administrador para detener o iniciar el servicio de nube que ejecuta un punto de distribución basado en la nube.|Servidor de sistema de sitio|  
|DataTransferService.log|Registra todas las comunicaciones de BITS para el acceso de directiva o paquete. Los puntos de distribución de extracción también usan este registro para la administración de contenido.|Equipo configurado como punto de distribución de extracción|  
|PullDP.log|Registra los detalles sobre el contenido que el punto de distribución de extracción transfiere de puntos de distribución de origen.|Equipo configurado como punto de distribución de extracción|  
|PrestageContent.log|Registra los detalles sobre el uso de la herramienta ExtractContent.exe en un punto de distribución preconfigurado remoto. Esta herramienta extrae el contenido que ha sido exportado a un archivo.|Rol de sistema de sitio|  
|SMSdpmon.log|Registra detalles sobre tareas programadas de supervisión de estado de punto de distribución configuradas en un punto de distribución.|Rol de sistema de sitio|  
|smsdpprov.log|Registra detalles acerca de la extracción de archivos comprimidos recibidos de un sitio primario. El proveedor de WMI del punto de distribución remoto genera este registro.|Equipo de punto de distribución que no comparte ubicación con el servidor del sitio|  
|smsdpusage.log|Registra los detalles sobre el smsdpusage.exe que se ejecuta y recopila datos para el informe de resumen de uso de los puntos de distribución.|Rol de sistema de sitio|  

### <a name="desktop-analytics"></a>Análisis de escritorio

Use los archivos de registro siguientes para ayudar a solucionar problemas con el Análisis de escritorio integrado con Configuration Manager.

Los archivos de registro en el punto de conexión de servicio están en este directorio: `%ProgramFiles%\Configuration Manager\Logs\M365A`.
Los archivos de registro en el cliente de Configuration Manager están en este directorio: `%WinDir%\CCM\logs`.

| Registro | Descripción |Equipo con el archivo de registro|
|---------|---------|---------|
| M365ADeploymentPlanWorker.log | Información sobre la sincronización del plan de implementación desde el servicio en la nube del Análisis de escritorio a Configuration Manager local |Punto de conexión de servicio|
| M365ADeviceHealthWorker.log | Información sobre la carga del estado del dispositivo desde Configuration Manager a la nube de Microsoft |Punto de conexión de servicio|
| M365AHandler.log | Información sobre la directiva de configuración del Análisis de escritorio |Cliente|
| M365AUploadWorker.log | Información sobre la carga de la colección y el dispositivo desde Configuration Manager a la nube de Microsoft |Punto de conexión de servicio|
| SmsAdminUI.log | Información sobre la actividad de la consola de Configuration Manager, como la configuración de los servicios en la nube de Azure  |Punto de conexión de servicio|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a> Detección

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la detección.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Registra acciones de detección de grupos de seguridad de Active Directory.|Servidor de sitio|  
|adsysdis.log|Registra acciones de detección de sistema de Active Directory.|Servidor de sitio|  
|adusrdis.log|Registra acciones de detección de usuarios de Active Directory.|Servidor de sitio|  
|ADForestDisc.log|Registra acciones de detección de bosques de Active Directory.|Servidor de sitio|  
|ddm.log|Registra actividades del administrador de datos de detección.|Servidor de sitio|  
|InventoryAgent.log|Registra actividades de acciones de inventario de hardware, inventario de software y detección de latido en el cliente.|Cliente|  
|netdisc.log|Registra acciones de detección de redes.|Servidor de sitio|  

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con Endpoint Protection.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Registra detalles sobre la instalación del cliente de Endpoint Protection y la aplicación de directiva antimalware en el cliente.|Cliente|  
|EPCtrlMgr.log|Registra detalles sobre la sincronización de información de amenazas de malware del servidor de rol de Endpoint Protection con la base de datos de Configuration Manager.|Servidor de sistema de sitio|  
|EPMgr.log|Supervisa el estado del rol de sistema de sitio de Endpoint Protection.|Servidor de sistema de sitio|  
|EPSetup.log|Proporciona información sobre la instalación del rol de sistema de sitio de Endpoint Protection.|Servidor de sistema de sitio|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a> Extensiones

En la siguiente tabla se enumeran los archivos de registro que contienen información relacionada con las extensiones.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Registra información sobre la descarga de extensiones de Microsoft y la instalación y desinstalación de todas las extensiones.|Equipo que ejecuta la consola de Configuration Manager|  
|FeatureExtensionInstaller.log|Registra información sobre la instalación y desinstalación de extensiones individuales cuando están habilitadas o deshabilitadas en la consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  
|SmsAdminUI.log|Registra la actividad de consola de Configuration Manager.|Equipo que ejecuta la consola de Configuration Manager|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a> Inventario

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con los datos de inventario de procesamiento.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Registra información sobre el procesamiento de archivos MIF y el inventario de hardware en la base de datos de Configuration Manager.|Servidor de sitio|  
|invproc.log|Registra el reenvío de archivos MIF de un sitio secundario a su sitio primario.|Servidor de sitio secundario|  
|sinvproc.log|Registra información acerca del procesamiento de datos de inventario de software en la base de datos del sitio.|Servidor de sitio|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a> Medición

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la disponibilidad.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Supervisa todos los procesos de disponibilidad de software.|Cliente|  
|SWMTRReportGen.log|Genera un informe de datos de uso recopilados por el agente de disponibilidad. Estos datos se registran en Mtrmgr.log.|Cliente|
|swmproc.log|Registra el procesamiento de archivos y configuraciones de disponibilidad.|Servidor de sitio|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a> Migración

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la migración.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Registra información acerca de las acciones de migración que implican trabajos de migración, puntos de distribución compartidos y actualizaciones de puntos de distribución.|Sitio de nivel superior de la jerarquía de Configuration Manager y cada sitio primario secundario. En una jerarquía de varios sitios primarios, utilice el archivo de registro creado en el sitio de administración central.|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a> Dispositivos móviles

En las secciones siguientes se incluyen los archivos de registro que contienen información relacionada con la administración de dispositivos móviles.  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a> Inscripción

En la tabla siguiente se incluyen los registros que contienen información relacionada con la inscripción de dispositivos móviles.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Registra la comunicación entre puntos de administración habilitados para dispositivos móviles y los extremos de punto de administración.|Servidor de sistema de sitio|  
|dmpmsi.log|Registra los datos de Windows Installer para la configuración de un punto de administración habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DMPSetup.log|Registra la configuración del punto de administración cuando está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|enrollsrvMSI.log|Registra los datos de Windows Installer para la configuración de un punto de inscripción.|Servidor de sistema de sitio|  
|enrollmentweb.log|Registra la comunicación entre dispositivos móviles y el punto de proxy de inscripción.|Servidor de sistema de sitio|  
|enrollwebMSI.log|Registra los datos de Windows Installer para la configuración de un punto de proxy de inscripción.|Servidor de sistema de sitio|  
|enrollmentservice.log|Registra la comunicación entre un punto de proxy de inscripción y un punto de inscripción.|Servidor de sistema de sitio|  
|SMS_DM.log|Registra la comunicación entre dispositivos móviles, equipos Mac y el punto de administración habilitado para dispositivos móviles y equipos Mac.|Servidor de sistema de sitio|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Conector de Exchange Server

Los registros siguientes contienen información relacionada con el conector de Exchange Server.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Registra las actividades y el estado del conector de Exchange Server.|Servidor de sitio|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a> Herencia de dispositivo móvil

En la tabla siguiente se incluyen los registros que contienen información relacionada con el cliente heredado de dispositivo móvil.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Registra detalles acerca de datos de inscripción de certificados en clientes heredados de dispositivos móviles.|Cliente|  
|DMCertResp.htm|Registra la respuesta HTML del servidor de certificados cuando el programa de inscripción de cliente heredado de dispositivos móviles solicita un certificado PKI.|Cliente|  
|DmClientHealth.log|Registra los GUID de todos los clientes heredados de dispositivos móviles que se comunican con el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmClientRegistration.log|Registra las solicitudes y respuestas de registro a y desde clientes heredados de dispositivos móviles.|Servidor de sistema de sitio|  
|DmClientSetup.log|Registra datos de instalación de cliente para clientes heredados de dispositivos móviles.|Cliente|  
|DmClientXfer.log|Registra datos de transferencia de clientes para clientes heredados de dispositivos móviles y para implementaciones de ActiveSync.|Cliente|  
|DmCommonInstaller.log|Registra la instalación de archivos de transferencia de cliente para configurar archivos de transferencia de cliente heredado de dispositivos móviles.|Cliente|  
|DmInstaller.log|Registra si DMInstaller llama correctamente a DmClientSetup, y si sale de DmClientSetup correcta o incorrectamente para clientes heredados de dispositivos móviles.|Cliente|  
|DmpDatastore.log|Registra todas las conexiones de base de datos de sitio y las consultas realizadas por el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpDiscovery.log|Registra todos los datos de detección de los clientes heredados de dispositivos móviles en el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpHardware.log|Registra los datos de inventario de hardware de los clientes heredados de dispositivos móviles en el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpIsapi.log|Registra la comunicación de cliente heredado de dispositivos móviles con un punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|dmpmsi.log|Registra los datos de Windows Installer para la configuración de un punto de administración habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DMPSetup.log|Registra la configuración del punto de administración cuando está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpSoftware.log|Registra los datos de distribución de software de los clientes heredados de dispositivos móviles en el punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmpStatus.log|Registra los datos de mensajes de estado de los clientes de dispositivos móviles en un punto de administración que está habilitado para dispositivos móviles.|Servidor de sistema de sitio|  
|DmSvc.log|Registra la comunicación de clientes heredados de dispositivos móviles con un punto de administración que está habilitado para dispositivos móviles.|Cliente|  
|FspIsapi.log|Registra detalles acerca de las comunicaciones con el punto de estado de reserva de los clientes heredados de dispositivo móvil y los equipos cliente.|Servidor de sistema de sitio|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a> Implementación del sistema operativo

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la implementación del sistema operativo.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CAS.log|Registra los detalles cuando se encuentran puntos de distribución de contenido al que se hace referencia.|Cliente|  
|ccmsetup.log|Registra tareas de ccmsetup de instalación, actualización y eliminación de cliente. Puede utilizarse para solucionar problemas de instalación de cliente.|Cliente|  
|CreateTSMedia.log|Registra los detalles de creación de medios de secuencia de tareas.|Equipo que ejecuta la consola de Configuration Manager|  
|Dism.log|Registra acciones de instalación del controlador o acciones de aplicación de actualizaciones para el mantenimiento sin conexión.|Servidor de sistema de sitio|  
|distmgr.log|Registra detalles sobre la configuración para habilitar un punto de distribución de Medio de ejecución anterior al inicio (PXE).|Servidor de sistema de sitio|  
|DriverCatalog.log|Registra los detalles acerca de los controladores de dispositivo que se han importado en el catálogo de controladores.|Servidor de sistema de sitio|  
|mcsisapi.log|Registra información de respuestas de solicitud de cliente y de transferencia de paquetes mediante multidifusión.|Servidor de sistema de sitio|  
|mcsexec.log|Registra acciones de comprobación de estado, espacio de nombres, creación de sesiones y comprobación de certificados.|Servidor de sistema de sitio|  
|mcsmgr.log|Registra cambios en la configuración, el modo de seguridad y la disponibilidad.|Servidor de sistema de sitio|  
|mcsprv.log|Registra la interacción del proveedor de multidifusión con los Servicios de implementación de Windows (WDS).|Servidor de sistema de sitio|  
|MCSSetup.log|Registra los detalles acerca de la instalación del rol del servidor de multidifusión.|Servidor de sistema de sitio|  
|MCSMSI.log|Registra los detalles acerca de la instalación del rol del servidor de multidifusión.|Servidor de sistema de sitio|  
|Mcsperf.log|Registra los detalles acerca de las actualizaciones de contador de rendimiento de multidifusión.|Servidor de sistema de sitio|  
|MP_ClientIDManager.log|Registra las respuestas de punto de administración a las solicitudes de identificador de cliente que las secuencias de tareas inician desde el entorno PXE o medios de arranque.|Servidor de sistema de sitio|  
|MP_DriverManager.log|Registra las respuestas de puntos de administración a las solicitudes de acciones de secuencias de tareas de aplicación automática de controladores.|Servidor de sistema de sitio|  
|OfflineServicingMgr.log|Registra detalles de los planes de mantenimiento sin conexión y de las acciones de aplicación de actualizaciones en archivos Windows Imaging Format (WIM) de sistema operativo.|Servidor de sistema de sitio|  
|Setupact.log|Registra los detalles acerca de los registros de instalación y SysPrep de Windows. Para obtener más información, consulte [Archivos de registro](https://docs.microsoft.com/windows/deployment/upgrade/log-files).|Cliente|  
|Setupapi.log|Registra los detalles acerca de los registros de instalación y SysPrep de Windows.|Cliente|  
|Setuperr.log|Registra los detalles acerca de los registros de instalación y SysPrep de Windows.|Cliente|  
|smpisapi.log|Registra los detalles acerca de las acciones de restauración y captura de estado de cliente, así como información sobre umbrales.|Cliente|  
|Smpmgr.log|Registra los detalles acerca de los resultados de las comprobaciones de estado de punto de migración de estado y los cambios de configuración.|Servidor de sistema de sitio|  
|smpmsi.log|Registra los detalles de instalación y configuración acerca del punto de migración de estado.|Servidor de sistema de sitio|  
|smpperf.log|Registra las actualizaciones de contador de rendimiento de punto de migración de estado.|Servidor de sistema de sitio|  
|smspxe.log|Registra detalles sobre las respuestas a los clientes que usan arranque PXE y detalles sobre la expansión de archivos e imágenes de arranque.|Servidor de sistema de sitio|  
|smssmpsetup.log|Registra los detalles de instalación y configuración acerca del punto de migración de estado.|Servidor de sistema de sitio|
| SMS_PhasedDeployment.log| Archivo de registro de las implementaciones por fases|Sitio de nivel superior de la jerarquía de Configuration Manager|
|Smsts.log|Registra las actividades de secuencia de tareas.|Cliente|  
|TSAgent.log|Registra el resultado de las dependencias de secuencia de tareas antes de iniciar una secuencia de tareas.|Cliente|  
|TaskSequenceProvider.log|Registra los detalles sobre las secuencias de tareas cuando se importan, exportan o editan.|Servidor de sistema de sitio|  
|loadstate.log|Registra los detalles acerca de la Herramienta de migración de estado de usuario (USMT) y la restauración de los datos de estado de usuario.|Cliente|  
|scanstate.log|Registra los detalles acerca de la Herramienta de migración de estado de usuario (USMT) y la captura de los datos de estado de usuario.|Cliente|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a> Administración de energía

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la administración de energía.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|Registra detalles sobre las actividades de administración de energía en el equipo cliente, que incluyen la supervisión y la aplicación de configuración por el agente cliente de administración de energía.|Cliente|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a> Control remoto

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el control remoto.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Registra los detalles acerca de la actividad del visor de control remoto.|En el equipo que ejecuta el visor de control remoto, en la carpeta %temp%.|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a> Generación de informes

En la tabla siguiente se incluyen los archivos de registro de Configuration Manager que contienen información relacionada con la generación de informes.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Registra información acerca de la actividad y el estado del punto de servicios de informes.|Servidor de sistema de sitio|  
|srsrpMSI.log|Registra resultados detallados del proceso de instalación del punto de servicios de informes desde la salida de MSI.|Servidor de sistema de sitio|  
|srsrpsetup.log|Registra los resultados del proceso de instalación del punto de servicios de informes.|Servidor de sistema de sitio|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a> Administración basada en roles

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con la administración basada en roles.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|hman.log|Registra información sobre los cambios de configuración de sitio y la publicación de información de sitio en Servicios de dominio de Active Directory.|Servidor de sitio|  
|SMSProv.log|Registra el acceso del proveedor de WMI a la base de datos del sitio.|Equipo con el proveedor de SMS|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a> Medición de software

En la tabla siguiente se indican los archivos de registro que contienen información relacionada con las mediciones de software.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Supervisa todos los procesos de disponibilidad de software.|Servidor de sitio|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a> Actualizaciones de software

En la tabla siguiente se indican los archivos de registro que contienen información relacionada con las actualizaciones de software.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|AlternateHandler.log|Registra los detalles cuando el cliente llama a la interfaz COM de hacer clic y ejecutar de Office para descargar e instalar las actualizaciones de cliente de Aplicaciones de Microsoft 365 para empresas. Es similar al uso de WuaHandler cuando llama a la API del agente de Windows Update para descargar e instalar las actualizaciones de Windows.<!-- SCCMDocs#888 -->|Cliente|
|Ccmperf.log|Registra actividades relacionadas con el mantenimiento y la captura de datos relacionados con los contadores de rendimiento de cliente.|Cliente|
|DeltaDownload.log|Registra información sobre la descarga de actualizaciones rápidas y actualizaciones descargadas mediante Optimización de entrega.|Cliente|  
|PatchDownloader.log|Registra detalles sobre el proceso de descarga de actualizaciones de software del origen de actualizaciones al destino de descarga en el servidor de sitio.|Cuando las actualizaciones se descargan de forma manual, este archivo de registro se encontrará en el directorio %temp% del usuario que ejecuta la consola en el equipo en el que se ejecute la consola. Para las reglas de implementación automática, este archivo de registro se encontrará en el servidor del sitio en %windir%\CCM\Logs si el cliente de Configuration Manager está instalado en el servidor del sitio.|  
|PolicyEvaluator.log|Registra los detalles acerca de la evaluación de directivas en los equipos cliente, incluidas las directivas de las actualizaciones de software.|Cliente|  
|RebootCoordinator.log|Registra los detalles acerca de la coordinación de reinicios del sistema en los equipos cliente después de que se instalan las actualizaciones de software.|Cliente|  
|ScanAgent.log|Registra los detalles acerca de cómo examinar las solicitudes de actualización de software, la ubicación de WSUS y acciones relacionadas.|Cliente|  
|SdmAgent.log|Registra detalles sobre cómo realizar un seguimiento de la corrección y la compatibilidad. Pero en el archivo de registro de actualizaciones de software, Updateshandler.log, se proporcionan detalles más informativos sobre cómo instalar las actualizaciones de software necesarias a efectos de compatibilidad. Este archivo de registro se comparte con la configuración de compatibilidad.|Cliente|  
|ServiceWindowManager.log|Registra los detalles acerca de la evaluación de las ventanas de mantenimiento.|Cliente|
|SMS_ISVUPDATES_SYNCAGENT.log| Archivo de registro para la sincronización de actualizaciones de software de terceros.| Actualización de software de nivel superior de la jerarquía de Configuration Manager.|
|SMS_OrchestrationGroup.log| Archivo de registro para grupos de orquestaciones|Servidor de sitio|
|SmsWusHandler.log|Registra los detalles sobre el proceso de análisis de la herramienta de inventario para Microsoft Update.|Cliente|  
|StateMessage.log|Registra detalles sobre los mensajes de estado de actualizaciones de software que se crean y envían al punto de administración.|Cliente|  
|SUPSetup.log|Registra detalles acerca de la instalación de un punto de actualización de software. Cuando se completa la instalación del punto de actualización de software, **Installation was successful** se escribe en este archivo de registro.|Servidor de sistema de sitio|  
|UpdatesDeployment.log|Registra los detalles acerca de las implementaciones en el cliente, incluidas la activación, evaluación y aplicación de las actualizaciones de software. En el registro detallado se muestra información adicional acerca de la interacción con la interfaz de usuario del cliente.|Cliente|  
|UpdatesHandler.log|Registra información sobre el análisis de compatibilidad de actualizaciones de software y la descarga e instalación de actualizaciones de software en el cliente.|Cliente|  
|UpdatesStore.log|Registra los detalles acerca del estado de compatibilidad de las actualizaciones de software evaluadas durante el ciclo de análisis de compatibilidad.|Cliente|  
|WCM.log|Registra detalles sobre la configuración del punto de actualización de software y las conexiones con el servidor WSUS para las clasificaciones, idiomas y categorías de actualizaciones suscritas.|Servidor de sitio|  
|WSUSCtrl.log|Registra los detalles acerca de la configuración, la conectividad de base de datos y el estado del servidor WSUS para el sitio.|Servidor de sistema de sitio|  
|wsyncmgr.log|Registra detalles sobre el proceso de sincronización de actualizaciones de software.|Servidor de sitio|  
|WUAHandler.log|Registra detalles acerca del agente de Windows Update en el cliente cuando busca actualizaciones de software.|Cliente|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a> Wake On LAN

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el uso de Wake On LAN.  

> [!NOTE]  
> Si complementa Wake on LAN con el uso de un proxy de reactivación, esta actividad se registra en el cliente. Por ejemplo, vea CcmExec.log y SleepAgent_<*dominio*\>@SYSTEM_0.log en la sección [Operaciones de cliente](#BKMK_ClientOpLogs) de este artículo.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Registra los detalles acerca de los clientes a los que se deben enviar paquetes de reactivación, el número de paquetes de reactivación enviados y el número de paquetes de reactivación que se reintentaron.|Servidor de sitio|  
|wolmgr.log|Registra los detalles sobre los procedimientos de reactivación, como la reactivación de implementaciones configuradas para Wake on LAN.|Servidor de sitio|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a> Mantenimiento de Windows 10

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el mantenimiento de Windows 10.  
El servicio utiliza la misma infraestructura y el mismo proceso que las actualizaciones de software. Para otros registros aplicables al escenario de servicio, consulte [Actualizaciones de software](#BKMK_SU_NAPLog).

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|CBS.log|Registra los errores de servicio relacionados con los cambios en las actualizaciones de Windows o en los roles y características.|Cliente|
|DISM.log|Registra todas las acciones mediante DISM. Si es necesario, DISM.log apuntará a CBS.log para obtener más detalles.|Cliente|
|setupact.log|Archivo de registro principal para la mayoría de los errores que se producen durante el proceso de instalación de Windows. El archivo de registro se encuentra en la carpeta %windir%\$Windows.~BT\sources\panther.|Cliente|

Para más información, consulte el artículo sobre [archivos de registro relacionados con los servicios en línea](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files).

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a> Agente de Windows Update

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el agente de Windows Update.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Registra detalles sobre la conexión del agente de Windows Update con el servidor WSUS y recupera las actualizaciones de software para evaluar el cumplimiento y determinar si hay actualizaciones de los componentes del agente.|Cliente|  

Para más información, consulte el artículo sobre los [archivos de registro de Windows Update](https://docs.microsoft.com/windows/deployment/update/windows-update-logs).

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a> Servidor WSUS

En la tabla siguiente se incluyen los archivos de registro que contienen información relacionada con el servidor WSUS.  

|Nombre del registro|Descripción|Equipo con el archivo de registro|  
|--------------|-----------------|----------------------------|  
|Change.log|Registra detalles sobre la información de base de datos del servidor WSUS que ha cambiado.|Servidor WSUS|  
|SoftwareDistribution.log|Registra detalles sobre las actualizaciones de software que se sincronizan del origen de actualizaciones configurado a la base de datos del servidor de WSUS.|Servidor WSUS|  

Estos archivos de registro se encuentran en la carpeta `%ProgramFiles%\Update Services\LogFiles`.

## <a name="see-also"></a>Vea también

- [Acerca de los archivo de registro](about-log-files.md)

- [Centro de soporte técnico OneTrace](../../support/support-center-onetrace.md)

- [Visor de archivos de registro del Centro de soporte técnico](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
