---
title: Comprobaciones de requisitos previos
titleSuffix: Configuration Manager
description: Referencia de las comprobaciones de requisitos previos específicos para las actualizaciones de Configuration Manager.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5bdf2adbf4ba5f02869ba5058da84ee7738e0ce2
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608069"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Lista de comprobaciones de requisitos previos de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se detallan las comprobaciones de requisitos previos que se ejecutan al instalar o actualizar Configuration Manager. Para obtener más información, vea [Comprobador de requisitos previos](prerequisite-checker.md).  



## <a name="errors"></a>Errores

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Asignaciones de migración activas en el sitio primario de destino

*Se aplica a: sitio de administración central*

No hay ninguna asignación de migración activa en los sitios primarios.

### <a name="active-replica-mp"></a>Módulo de administración de réplica activo

*Se aplica a: sitio primario*

Hay una réplica de punto de administración activa.

### <a name="administrative-rights-on-expand-primary-site"></a>Derechos administrativos en sitios primarios de expansión

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, la cuenta de usuario que ejecuta el programa de instalación tiene derechos de **administrador** en el sitio primario independiente.

### <a name="administrative-rights-on-site-system"></a>Derechos administrativos en el sistema de sitio

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

La cuenta de usuario que ejecuta el programa de instalación de Configuration Manager tiene derechos de **administrador** en el servidor de sitio.

### <a name="administrator-rights-on-central-administration-site"></a>Derechos de administrador en el sitio de administración central

*Se aplica a: sitio primario*

La cuenta de usuario que ejecuta el programa de instalación de Configuration Manager tiene derechos de **administrador** en el servidor de sitio de administración central.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Punto de sincronización de Asset Intelligence no admitido en el sitio primario expandido

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, el rol del punto de sincronización de Asset Intelligence no está instalado en el sitio primario independiente.

### <a name="bits-enabled"></a>BITS habilitado

*Se aplica a: punto de administración*

El Servicio de transferencia inteligente en segundo plano (BITS) está instalado en el punto de administración. Esta comprobación puede fallar por uno de los siguientes motivos:

- BITS no está instalado.  

- El componente de compatibilidad de WMI de IIS 6.0 para IIS 7.0 no está instalado en el servidor o host de IIS remoto.  

- El programa de instalación no ha podido comprobar la configuración de IIS remoto. Los componentes comunes de IIS no están instalados en el servidor de sitio.  

### <a name="case-insensitive-collation-on-sql-server"></a>Intercalación que diferencia entre mayúsculas y minúsculas en SQL Server

*Se aplica a: servidor de base de datos del sitio*

La instalación de SQL Server utiliza una intercalación que diferencia entre mayúsculas y minúsculas, como **SQL_Latin1_General_CP1_CI_AS**.

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Derechos de administración del servidor de sitio de administración central en el sitio primario que se va a expandir

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, la cuenta de equipo del servidor de sitio de administración central tiene derechos de **administrador** en el servidor de sitio primario independiente.

### <a name="client-version-on-management-point-computer"></a>Versión de cliente en el equipo de punto de administración

*Se aplica a: punto de administración*

Va a instalar el punto de administración en un servidor cuya versión no difiere de la del cliente instalado de Configuration Manager.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Cloud Management Gateway en el sitio primario expandido

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, el rol de Cloud Management Gateway no está instalado en el sitio primario independiente.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Conexión a SQL Server en el sitio de administración central

*Se aplica a: sitio primario*

La cuenta de usuario que ejecuta el programa de instalación de Configuration Manager en el sitio primario para unirlo a una jerarquía existente tiene el rol **administrador del sistema** en la instancia de SQL Server para el sitio de administración central.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>La configuración personalizada de agente cliente tiene NAP habilitada

*Se aplica a: sitio primario, sitio de administración central*

No hay ninguna configuración de cliente personalizada que habilite la Protección de acceso a redes (NAP).

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Punto de servicio de almacenamiento de datos en el sitio primario expandido

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, el rol del punto de servicio de almacenamiento de datos no está instalado en el sitio primario independiente.

### <a name="dedicated-sql-server-instance"></a>Instancia de SQL Server dedicada

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

Ha configurado una instancia dedicada de SQL Server para hospedar la base de datos de sitio de Configuration Manager.

Si otro sitio utiliza la instancia, debe seleccionar otra instancia para el nuevo sitio. También puede desinstalar el otro sitio o mover su base de datos a otra instancia de SQL Server.

### <a name="default-client-agent-settings-have-nap-enabled"></a>La configuración predeterminada de agente cliente tiene NAP habilitada

*Se aplica a: sitio primario, sitio de administración central*

La configuración predeterminada de cliente no habilita la Protección de acceso a redes (NAP).

### <a name="domain-membership-error"></a>Pertenencia a dominio (error)

*Se aplica a: sitio de administración central, sitio primario, sitio secundario, proveedor de SMS, SQL Server*

El equipo de Configuration Manager pertenece a un dominio de Windows.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Punto de Endpoint Protection en el sitio primario expandido

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, el rol del punto de Endpoint Protection no está instalado en el sitio primario independiente.

### <a name="existing-configuration-manager-server-components-on-server"></a>Componentes de servidor de Configuration Manager existentes en el servidor

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

Un servidor de sitio o el rol de sistema de sitio aún no están instalados en el servidor seleccionado para la instalación del sitio.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Sitio primario independiente existente para la versión y el código de sitio

*Se aplica a: sitio primario, sitio de administración central*

El sitio primario que planea expandir es un sitio primario independiente. Tiene la misma versión de Configuration Manager, pero un código de sitio diferente que el sitio de administración central que se va a instalar.

### <a name="firewall-exception-for-sql-server"></a>Excepción de firewall para SQL Server

*Se aplica a: sitio de administración central, sitio primario o sitio secundario, punto de administración*

Firewall de Windows está deshabilitado o existe la excepción correspondiente de Firewall de Windows para SQL Server.

Permite el acceso remoto a Sqlservr.exe o a los puertos TCP necesarios. De forma predeterminada, SQL Server escucha en el puerto TCP 1433 y SQL Server Service Broker (SSB) usa el puerto TCP 4022.

### <a name="free-disk-space-on-site-server"></a>Espacio libre en disco en el servidor de sitio

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

Para instalar el servidor de sitio, debe tener al menos 15 GB de espacio libre en disco. Si instala al proveedor de SMS en el mismo servidor, necesitará 1 GB de espacio libre adicional.

### <a name="iis-service-running"></a>Ejecución del servicio IIS

*Se aplica a: punto de administración, punto de distribución*

IIS está instalado y en ejecución en el servidor para los puntos de administración o distribución.

### <a name="incompatible-collection-references"></a>Referencias a recopilaciones no compatibles

*Se aplica a: sitio de administración central*

Durante una actualización, las recopilaciones solo hacen referencia a otras recopilaciones del mismo tipo.

### <a name="match-collation-of-expand-primary-site"></a>Hacer coincidir la intercalación del sitio primario de expansión

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, la base de datos de sitio para el sitio primario independiente tiene la misma intercalación que la base de datos de sitio en el sitio de administración central.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>Tamaño máximo de replicación de texto para los grupos de disponibilidad Always On de SQL Server

*Se aplica a: servidor de base de datos del sitio*

Cuando se usa Always On de SQL Server, el valor del **tamaño máximo de replicación de texto** debe estar configurado correctamente. Para obtener más información, vea [Preparación para usar grupos de disponibilidad AlwaysOn de SQL Server con Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Conector de Microsoft Intune en el sitio primario expandido

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, el rol de Microsoft Intune Connector no está instalado en el sitio primario independiente.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Biblioteca registrada de compresión diferencial remota (RDC) de Microsoft

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

La biblioteca de RDC está registrada en el servidor de sitio de Configuration Manager.

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

Comprueba la versión de Windows Installer.

Cuando se produce un error en esta comprobación, significa que el programa de instalación no pudo comprobar la versión o que la versión instalada no cumple el requisito mínimo de Windows Installer 4.5.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Versión mínima de .NET Framework para la consola de Configuration Manager

*Se aplica a: consola de Configuration Manager*

Microsoft .NET Framework 4.0 está instalado en el equipo de la consola de Configuration Manager.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Versión mínima de .NET Framework para el servidor de sitio de Configuration Manager

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

.NET Framework 3.5 está instalado o habilitado en el servidor de sitio de Configuration Manager.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Versión mínima de .NET Framework para la instalación de SQL Server Express Edition para el sitio secundario de Configuration Manager

*Se aplica a: sitio secundario*

.NET Framework 4.0 está instalado o habilitado en el servidor de sitio secundario de Configuration Manager. SQL Server Express requiere esta versión.

### <a name="parent-database-collation"></a>Intercalación de base de datos primaria

*Se aplica a: sitio primario, sitio secundario*

La intercalación de base de datos de sitio coincide con la intercalación de base de datos de sitio primario. Todos los sitios de una jerarquía deben utilizar la misma intercalación de base de datos.

### <a name="parent-site-replication-status"></a>Estado de replicación del sitio primario

*Se aplica a: sitio primario, sitio de administración central*

El estado de replicación del sitio primario es **Replicación activa** (estado **125**).

### <a name="pending-system-restart"></a>Reinicio del sistema pendiente

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

Antes de ejecutar el programa de instalación, otro programa requiere que el servidor se reinicie.

A partir de la versión 1810, esta comprobación es más resistente. Para ver si el equipo está en estado de reinicio pendiente, comprueba las siguientes ubicaciones del Registro:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>FQDN primario

*Se aplica a: sitio de administración central, sitio primario, sitio secundario, servidor de base de datos del sitio*

El nombre NetBIOS del equipo coincide con el nombre de host local en el nombre de dominio completo (FQDN).

### <a name="read-only-domain-controller"></a>Controlador de dominio de solo lectura

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

Los servidores de base de datos de sitio y servidores de sitio secundario no se admiten en un controlador de dominio de solo lectura (RODC).

Para obtener más información, vea el artículo del Soporte técnico de Microsoft sobre los [problemas al instalar SQL Server en un controlador de dominio](https://support.microsoft.com/help/2032911).

### <a name="required-sql-server-collation"></a>Intercalación de SQL Server requerida

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

La instancia de SQL Server está configurada para usar la intercalación **SQL_Latin1_General_CP1_CI_AS**.

Si la base de datos de sitio de Configuration Manager ya está instalada, esta comprobación también se aplica a la base de datos. Para obtener información sobre cómo cambiar las intercalaciones de base de datos y la instancia de SQL Server, vea [SQL collation and unicode support](/sql/relational-databases/collations/collation-and-unicode-support) (Compatibilidad con la intercalación y Unicode de SQL).

Si usa un sistema operativo chino y necesita compatibilidad con GB18030, esta comprobación no se aplica. Para obtener más información sobre cómo habilitar la compatibilidad con GB18030, vea [Compatibilidad internacional](../../../plan-design/hierarchy/international-support.md).

### <a name="server-service-is-running"></a>El servicio de servidor se está ejecutando

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

El servicio de servidor se ha iniciado y se está ejecutando.

### <a name="setup-source-folder"></a>Carpeta del origen de la instalación

*Se aplica a: sitio secundario*

La cuenta de equipo del sitio secundario tiene los siguientes permisos para el recurso compartido y la carpeta de origen del programa de instalación:

- Permisos de **lectura** del sistema de archivos NTFS  

- Permisos de **lectura** de los recursos compartidos  

> [!Note]  
> Si usa recursos compartidos administrativos, por ejemplo, C$ y D$, la cuenta de equipo del sitio secundario debe ser un **administrador** del servidor.  

### <a name="setup-source-version"></a>Versión de origen del programa de instalación

*Se aplica a: sitio secundario*

La versión de Configuration Manager de la carpeta de origen especificada para la instalación del sitio secundario coincide con la versión de Configuration Manager del sitio primario.

### <a name="site-code-in-use"></a>Código de sitio en uso

*Se aplica a: sitio primario*

El código de sitio especificado aún no se usa en la jerarquía de Configuration Manager. Especifique un código de sitio único para este sitio.

### <a name="site-server-computer-account-administrative-rights"></a>Derechos administrativos de la cuenta de equipo del servidor de sitio

*Se aplica a: sitio primario, servidor de base de datos del sitio*

La cuenta de equipo del servidor de sitio tiene derechos de **administrador** en SQL Server y el punto de administración.

### <a name="site-server-fqdn-length"></a>Longitud del FQDN del servidor de sitio

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

Longitud del FQDN del servidor de sitio.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Servidor de sitio en modo pasivo en el sitio primario expandido

*Se aplica a: sitio de administración central*

Al expandir un sitio primario a una jerarquía, el rol de servidor de sitio en modo pasivo no está instalado en el sitio primario independiente.

### <a name="sms-provider-in-same-domain-as-site-server"></a>El proveedor de SMS en el mismo dominio que el servidor de sitio

*Se aplica a: proveedor de SMS*

Cualquier instancia del proveedor de SMS está en el mismo dominio que el servidor de sitio.

### <a name="software-update-point-in-nlb-configuration"></a>Punto de actualización de software en la configuración de NLB

*Se aplica a: Punto de actualización de software*

El sitio no usa el equilibrio de carga de red (NLB) con ninguna ubicación virtual para los puntos de actualización de software activos.

### <a name="software-update-point-using-a-load-balancer"></a>Punto de actualización de software con equilibrador de carga

*Se aplica a: Punto de actualización de software*

Configuration Manager no admite los puntos de actualización de software en los equilibradores de carga de red (NLB) o de hardware (HLB).

### <a name="sql-server-always-on-availability-groups"></a>Grupos de disponibilidad Always On de SQL Server

*Se aplica a: servidor de base de datos del sitio*

Al usar Always On de SQL Server, debe cumplir los requisitos mínimos para hospedar un grupo de disponibilidad. Para obtener más información, vea [Preparación para usar grupos de disponibilidad AlwaysOn de SQL Server con Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>Grupo de disponibilidad de SQL Server configurado para secundarias legibles

*Se aplica a: servidor de base de datos del sitio*

Al usar Always On de SQL Server, compruebe el estado de lectura secundaria de las réplicas del grupo de disponibilidad.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>Grupo de disponibilidad de SQL Server configurado para la conmutación por error manual

*Se aplica a: servidor de base de datos del sitio*

Al usar Always On de SQL Server, las réplicas del grupo de disponibilidad se configuran para la conmutación por error manual.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>Réplicas del grupo de disponibilidad de SQL Server en la instancia predeterminada

*Se aplica a: servidor de base de datos del sitio*

Al usar Always On de SQL Server, las réplicas del grupo de disponibilidad se encuentran en la instancia predeterminada.

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>Todos los grupos de disponibilidad de SQL deben tener el mismo modo de propagación

<!-- SCCMDocs-pr#3899 -->
*Se aplica a: servidor de base de datos del sitio*

A partir de la versión 1906, al usar SQL Server Always On, debe configurar las réplicas del grupo de disponibilidad con el mismo [modo de propagación](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).

### <a name="sql-availability-group-replicas-must-be-healthy"></a>Las réplicas del grupo de disponibilidad de SQL deben estar en buen estado

<!-- SCCMDocs-pr#3899 -->
*Se aplica a: servidor de base de datos del sitio*

A partir de la versión 1906, al usar Always On de SQL Server, las réplicas del grupo de disponibilidad presentan un estado correcto.

### <a name="sql-server-configuration-for-site-upgrade"></a>Configuración de SQL Server para la actualización de sitio

*Se aplica a: servidor de base de datos del sitio*

El servidor SQL Server cumple los requisitos mínimos para la actualización del sitio. Para obtener más información, vea [Versiones de SQL Server compatibles](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="sql-server-edition"></a>Edición de SQL Server

*Se aplica a: servidor de base de datos del sitio*

SQL Server del sitio no es SQL Server Express.

### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express en el sitio secundario

*Se aplica a: sitio secundario*

SQL Server Express puede instalarse correctamente en el servidor de sitio secundario.

### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server en el servidor de sitio secundario

*Se aplica a: sitio secundario*

SQL Server está instalado en el servidor de sitio secundario. No se puede instalar SQL Server en un sistema de sitio remoto para un sitio secundario.

> [!Warning]  
> Esta comprobación solo se aplica cuando se selecciona que el programa de instalación utilice una instancia existente de SQL Server.  

### <a name="sql-server-service-running-account"></a>Cuenta de ejecución de servicio SQL Server

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

La cuenta de inicio de sesión del servicio SQL Server no es una cuenta de usuario local ni **SERVICIO LOCAL**.

Configure el servicio SQL Server para utilizar una cuenta de dominio válida, **SERVICIO DE RED** o **SISTEMA LOCAL**.

### <a name="sql-server-site-database-consistency"></a>Coherencia de la base de datos del sitio de SQL Server

*Se aplica a: servidor de base de datos del sitio*

Compruebe la coherencia de la base de datos.

### <a name="sql-server-sysadmin-rights"></a>Derechos de administrador del sistema de SQL Server

*Se aplica a: servidor de base de datos del sitio*

La cuenta de usuario que ejecuta el programa de instalación de Configuration Manager tiene el rol **administrador del sistema** en la instancia de SQL Server que ha seleccionado para la instalación de la base de datos del sitio. También se producen errores en esta comprobación cuando el programa de instalación no puede acceder a la instancia de SQL Server para comprobar los permisos.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Derechos de administrador del sistema de SQL Server para el sitio de referencia

*Se aplica a: servidor de base de datos del sitio*

La cuenta de usuario que ejecuta el programa de instalación de Configuration Manager tiene el rol **administrador del sistema** en la instancia de rol de SQL Server que ha seleccionado como base de datos del sitio de referencia. Se requieren los permisos del rol **administrador del sistema** de SQL Server para modificar la base de datos de sitio.

### <a name="sql-server-tcp-port"></a>Puerto TCP de SQL Server

*Se aplica a: servidor de base de datos del sitio*

TCP está habilitado para la instancia de SQL Server y está configurado para usar un puerto estático.

### <a name="sql-server-version"></a>Versión de SQL Server

*Se aplica a: servidor de base de datos del sitio*

Una versión compatible de SQL Server está instalada en el servidor de base de datos de sitio especificado.

Para obtener más información, vea [Support for SQL Server versions](../../../plan-design/configs/support-for-sql-server-versions.md) (Versiones de SQL Server compatibles).

### <a name="unsupported-os-for-configuration-manager-console"></a>Sistema operativo no admitido para la consola de Configuration Manager

*Se aplica a: consola de Configuration Manager*

Instala la consola de Configuration Manager en equipos que ejecutan una versión de sistema operativo compatible.

Para obtener más información, vea [Sistemas operativos compatibles con consolas de System Center Configuration Manager](../../../plan-design/configs/supported-operating-systems-consoles.md).

### <a name="unsupported-os-for-site-server"></a>Sistema operativo no compatible con el servidor de sitio

*Se aplica a: sitio de administración central, sitio primario, sitio secundario, consola de Configuration Manager, punto de administración, punto de distribución*

El servidor ejecuta una versión de sistema operativo compatible.

Para obtener más información, vea [Sistemas operativos compatibles con servidores de sistema de sitio de Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Rol de sistema de sitio no admitido: punto de servicio fuera de banda

*Se aplica a: sitio primario*

El rol de sistema de sitio de punto de servicio fuera de banda no está instalado.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Rol de sistema de sitio no admitido: punto de validación de mantenimiento del sistema

*Se aplica a: sitio primario*

El rol de sistema de sitio de punto de validación de mantenimiento del sistema no está instalado.

### <a name="unsupported-upgrade-path"></a>Ruta de actualización no compatible

*Se aplica a: sitio primario, sitio de administración central*

Todos los servidores de sitio de la jerarquía tienen la versión mínima de Configuration Manager necesaria para la actualización.

### <a name="usmt-installed"></a>USMT instalado

*Se aplica a: sitio de administración central, sitio primario (solo independiente)*

El componente Herramienta de migración de estado de usuario (USMT) de Windows Assessment and Deployment Kit (ADK) para Windows está instalado.

### <a name="validate-fqdn-of-sql-server"></a>Validar el FQDN de SQL Server

*Se aplica a: servidor de base de datos del sitio*

Ha especificado un FQDN válido para el equipo con SQL Server.

### <a name="verify-central-administration-site-version"></a>Comprobar la versión del sitio de administración central

*Se aplica a: sitio primario*

El sitio de administración central tiene la misma versión que Configuration Manager.

### <a name="verify-database-consistency"></a>Comprobar la coherencia de la base de datos

*Se aplica a: sitio primario, sitio de administración central*

Comprueba la coherencia de la base de datos del sitio en SQL Server.  

### <a name="windows-deployment-tools-installed"></a>Las herramientas de implementación de Windows están instaladas

*Se aplica a: proveedor de SMS*

El componente de herramientas de implementación de Windows ADK está instalado.

### <a name="windows-failover-cluster"></a>Clúster de conmutación por error de Windows

*Se aplica a: servidor de sitio, punto de administración, punto de distribución*

El servidor con el servidor de sitio, punto de administración o los roles de punto de distribución no forma parte de un clúster de Windows.

A partir de la versión 1810, el proceso de instalación de Configuration Manager ya no impide la instalación del rol de servidor de sitio en un equipo con el rol de Windows para clústeres de conmutación por error. SQL Always On requiere este rol, por lo que anteriormente no se podía colocar la base de datos del sitio en el servidor de sitio. Con este cambio, puede crear un sitio de alta disponibilidad con menos servidores usando SQL Always On y un servidor de sitio en modo pasivo. Para obtener más información, vea [High availability options](../configure/high-availability-options.md) (Opciones de alta disponibilidad). <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE instalado

*Se aplica a: proveedor de SMS*

El componente de entorno de preinstalación de Windows (PE) del ADK de Windows está instalado.



## <a name="warnings"></a>Advertencias

### <a name="active-directory-domain-functional-level"></a>Nivel funcional del dominio de Active Directory

*Se aplica a: sitio primario, sitio de administración central*

El nivel funcional de dominio y de bosque de Active Directory es como mínimo Windows Server 2008 R2. Para obtener más información, consulte [Compatibilidad con los dominios de Active Directory](../../../plan-design/configs/support-for-active-directory-domains.md).

### <a name="administrative-rights-on-distribution-point"></a>Derechos administrativos en el punto de distribución

*Se aplica a: punto de distribución*

La cuenta de usuario que ejecuta el programa de instalación tiene derechos de **administrador** en el punto de distribución.

### <a name="administrative-rights-on-management-point"></a>Derechos administrativos en el punto de administración

*Se aplica a: punto de administración, punto de distribución*

La cuenta de equipo del servidor de sitio tiene derechos de **administrador** en el punto de administración y distribución.

### <a name="administrative-share-site-system"></a>Recurso compartido administrativo (sistema de sitio)

*Se aplica a: punto de administración*

Los recursos compartidos administrativos necesarios se encuentran en el equipo de sistema de sitio.

### <a name="application-compatibility"></a>Compatibilidad de aplicaciones

*Se aplica a: sitio primario, sitio de administración central*

Las aplicaciones actuales son compatibles con el esquema de la aplicación.

### <a name="backlogged-inboxes"></a>Bandejas de entrada pendientes

*Se aplica a: sitio primario, sitio de administración central*

El servidor de sitio procesa las bandejas de entrada críticas de manera oportuna. Las bandejas de entrada no contienen archivos cuya antigüedad sea superior a un día.

Comprueba las siguientes carpetas de bandeja de entrada:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Para resolver esta advertencia, compruebe si se están ejecutando los componentes del sistema de sitio de programador y el procesador de paquetes.

### <a name="bits-installed"></a>BITS instalado

*Se aplica a: punto de administración*

El Servicio de transferencia inteligente en segundo plano (BITS) está instalado y habilitado en IIS.

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>Comprobar si el sitio usa el conector de servicio en la nube de Upgrade Readiness

*Se aplica a: sitio primario, sitio de administración central*

El servicio Upgrade Readiness se retiró el 31 de enero de 2020. Para más información, consulte [KB 4521815: Windows Analytics se retirará el 31 de enero de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Análisis de escritorio es la evolución de Windows Analytics. Vea [¿Qué es Análisis de escritorio?](../../../../desktop-analytics/overview.md) para obtener más información.

Si su sitio de Configuration Manager estaba conectado con Upgrade Readiness, tiene que quitarlo y volver a configurar los clientes. Para obtener más información, vea [Quitar la conexión con Upgrade Readiness](../../../clients/manage/upgrade-readiness.md#bkmk_remove).

Si pasa por alto esta advertencia sobre los requisitos previos, el programa de instalación de Configuration Manager quita automáticamente el conector de Upgrade Readiness.<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>Cloud Management Gateway requiere autenticación basada en tokens o un punto de administración HTTPS

*Se aplica a: Cloud Management Gateway* 

Con algunas versiones de Configuration Manager, no puede usar un punto de administración de HTTP con Cloud Management Gateway (CMG). Configure la instancia de CMG para HTTPS, o configure el sitio para HTTP mejorado. Para obtener más información, consulte [Plan for cloud management gateway (Plan para la puerta de enlace de administración en la nube)](../../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="configuration-for-sql-server-memory-usage"></a>Configuración de uso de memoria de SQL Server

*Se aplica a: servidor de base de datos del sitio*

SQL Server está configurado para un uso ilimitado de memoria. Configure la memoria de SQL Server para que tenga un límite máximo.

### <a name="distribution-point-package-version"></a>Versión de paquete de punto de distribución

*Se aplica a: Puntos de distribución*

Todos los puntos de distribución del sitio tienen la versión más reciente de los paquetes de distribución de software.

### <a name="domain-membership-warning"></a>Pertenencia a dominio (advertencia)

*Se aplica a: punto de administración, punto de distribución*

El equipo de Configuration Manager pertenece a un dominio de Windows.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Excepción de firewall para SQL Server (sitio primario independiente)

*Se aplica a: sitio primario (solo independiente)*

Firewall de Windows está deshabilitado o existe la excepción correspondiente de Firewall de Windows para SQL Server.

Permite el acceso remoto a Sqlservr.exe o a los puertos TCP necesarios. De forma predeterminada, SQL Server escucha en el puerto TCP 1433 y Server Service Broker (SSB) usa el puerto TCP 4022.

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Excepción de firewall para SQL Server para el punto de administración

*Se aplica a: punto de administración*

Firewall de Windows está deshabilitado o existe la excepción correspondiente de Firewall de Windows para SQL Server.

### <a name="iis-https-configuration"></a>Configuración HTTPS de IIS

*Se aplica a: punto de administración, punto de distribución*

El sitio web de IIS tiene enlaces para el protocolo de comunicación HTTPS.

Si instala roles de sitio que requieran el protocolo HTTPS, debe configurar los enlaces del sitio de IIS en el servidor especificado con un certificado PKI (infraestructura de clave pública) válido.

### <a name="invalid-discovery-records"></a>Registros de detección no válidos

*Se aplica a: sitio de administración central*

Hay registros de detección que ya no son válidos. Estos registros se van a marcar para su eliminación.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60)

*Se aplica a: sitio de administración central, sitio primario, sitio secundario, consola de Configuration Manager, punto de administración, punto de distribución*

Comprueba que la versión MSXML 6.0, u otra posterior, está instalada.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>La Protección de acceso a redes (NAP) ya no es compatible

*Se aplica a: sitio primario*

No hay actualizaciones de software habilitadas para NAP.

### <a name="ntfs-drive-on-site-server"></a>Unidad NTFS en servidor de sitio

*Se aplica a: sitio primario*

La unidad de disco se debe formatear con el sistema de archivos NTFS. Para mayor seguridad, instale los componentes de servidor de sitio en unidades de disco formateadas con el sistema de archivos NTFS.

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a> Actualizaciones de directivas de elementos de configuración pendientes

<!--SCCMDocs-pr issue 2814-->

*Se aplica a: sitio primario*

A partir de la versión 1806, puede que se le muestre esta advertencia al actualizar desde la versión 1706 o versiones posteriores si tiene varias implementaciones de aplicaciones y al menos una de estas requiere aprobación.

Tiene dos opciones:  

- Ignorar la advertencia y continuar con la actualización. Esta acción provoca un procesamiento más intensivo en el servidor del sitio durante la actualización, ya que se deberán procesar las directivas. También puede que aumente la carga del procesador en el punto de administración tras la actualización.  

- Revisar una de las aplicaciones que no tenga ningún requisito, o bien un requisito específico del SO. Preprocese una parte de la carga del servidor del sitio en ese momento. Revise **objreplmgr.log** y, después, supervise el procesador del punto de administración. Tras completar el procesamiento, actualice el sitio. Aún deberá realizarse parte del procesamiento tras la actualización, pero este será inferior al procesamiento necesario si se ignora la advertencia.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Reinicio pendiente del sistema en la instancia remota de SQL Server

*Se aplica a: Instancia remota de SQL Server, versión 1902 y posteriores*

Antes de ejecutar el programa de instalación, otro programa requiere que el servidor se reinicie.

Para ver si el equipo está en estado de reinicio pendiente, comprueba las siguientes ubicaciones del Registro:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 en el servidor de sitio

*Se aplica a: sitio primario con el conector de Exchange*

Windows PowerShell 2.0, o una versión posterior, está instalado en el servidor de sitio para Configuration Manager Exchange Connector.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>Conexión remota con WMI en el sitio secundario

*Se aplica a: sitio secundario*

El programa de instalación puede establecer una conexión remota con WMI en el servidor de sitio secundario.

### <a name="schema-extensions"></a>Extensiones de esquema

*Se aplica a: sitio primario, sitio de administración central*

El esquema de Active Directory se ha extendido. Si se ha extendido, la versión de las extensiones del esquema que se han usado.

Configuration Manager no requiere extensiones del esquema de Active Directory para instalar el servidor de sitio. Pero Microsoft las recomienda para el uso completo de todas las características de Configuration Manager. Para obtener más información sobre las ventajas de la extensión de esquema, vea [Preparar Active Directory para la publicación de sitios](../../../plan-design/network/extend-the-active-directory-schema.md).

### <a name="share-name-in-package"></a>Nombre de recurso compartido en el paquete

*Se aplica a: sitio primario, sitio de administración central*

Los paquetes no tienen caracteres no válidos en el nombre del recurso compartido, como `#`.

### <a name="site-system-to-sql-server-communication"></a>Sistema de sitio para la comunicación de SQL Server

*Se aplica a: sitio secundario, punto de administración*

La cuenta que ha configurado para ejecutar el servicio SQL Server para la instancia de base de datos del sitio tiene un nombre de entidad de seguridad de servicio (SPN) en Servicios de dominio de Active Directory. Registre un SPN válido en Active Directory para admitir la autenticación Kerberos.

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a> Limpieza del seguimiento de cambios de SQL Server

*Se aplica a: servidor de base de datos del sitio*

A partir de la versión 1810, compruebe si la base de datos del sitio tiene algún trabajo pendiente de datos de seguimiento de cambios de SQL.<!--SCCMDocs-pr issue 3023-->  

Haga manualmente esta comprobación ejecutando un procedimiento de diagnóstico almacenado en la base de datos. En primer lugar, cree una [conexión de diagnóstico](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators) a la base de datos de sitio. El método más sencillo consiste en usar el editor de consultas del Motor de base de datos de SQL Server Management Studio y conectarse a `admin:<instance name>`.

En una ventana de consulta de conexión de administrador dedicada, ejecute los siguientes comandos:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

En función del tamaño de la base de datos y del trabajo pendiente, este procedimiento almacenado puede tardar de unos minutos a varias horas. Al completar la consulta, verá dos secciones de datos relacionados con el trabajo pendiente. Primero consulte **CT_Days_Old**. Este valor indica la antigüedad (días) de la entrada más antigua en la tabla syscommittab. El valor predeterminado de Configuration Manager es de cinco días. No cambie este valor predeterminado. En periodos de grandes volúmenes de procesamiento de datos o replicación, la entrada más antigua en syscommittab puede tener más de cinco días. Si este valor es superior a los siete días, ejecute una limpieza manual de los datos de seguimiento de los cambios.  

Para limpiar los datos de seguimiento de los cambios, ejecute el siguiente comando en la conexión de administración dedicada:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Este comando inicia una limpieza de syscommittab y de todas las tablas del lado asociado. Su ejecución puede tardar de varios minutos a varias horas. Para supervisar su progreso, consulte la vista **vLogs**. Para ver el progreso actual, ejecute la consulta siguiente:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

Cuando se instala un sitio nuevo, Configuration Manager instala de forma automática SQL Server Native Client como un componente redistribuible. Después de instalar el sitio, Configuration Manager no actualiza SQL Server Native Client. La actualización de SQL Server Native Client podría requerir un reinicio, lo que puede afectar al proceso de instalación de sitio.

Esta comprobación garantiza que el servidor de sitio tiene una versión compatible de SQL Native Client. La comprobación de requisitos previos no comprueba la versión de SQL Native Client en los sistemas de sitio remotos.

La versión mínima es SQL 2012 SP4 (`11.*.7001.0`). Esta versión de SQL Native Client es compatible con TLS 1.2. Vea los siguientes artículos para más información:

- [Compatibilidad con TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Cómo habilitar TLS 1.2 para Configuration Manager](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager usa SQL Server Native Client en los siguientes roles de sistema de sitio:<!-- SCCMDocs issue 1150 -->

- Servidor de base de datos del sitio
- Servidor de sitio: sitio de administración central, sitio primario o sitio secundario
- Punto de administración
- Punto de administración de dispositivos
- Punto de migración de estado
- Proveedor de SMS
- Punto de actualización de software
- Punto de distribución habilitado con multidifusión
- Punto de servicio de actualización de Asset Intelligence
- Punto de servicios de informes
- Servicio web del catálogo de aplicaciones
- Punto de inscripción
- Punto de Endpoint Protection
- Punto de conexión de servicio
- Punto de registro de certificados
- Punto de servicio de almacenamiento de datos

### <a name="sql-server-process-memory-allocation"></a>Asignación de memoria de proceso de SQL Server

*Se aplica a: servidor de base de datos del sitio*

SQL Server reserva un mínimo de 8 GB de memoria para el sitio de administración central y el sitio primario, y un mínimo de 4 GB de memoria para el sitio secundario.

Para obtener más información, vea [Cómo configurar las opciones de memoria con SQL Server Management Studio](/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-).

> [!NOTE]  
> Esta comprobación no se aplica a SQL Server Express en un sitio secundario. Esta edición está limitada a 1 GB de memoria reservada.  

### <a name="sql-server-security-mode"></a>Modo de seguridad de SQL Server

*Se aplica a: servidor de base de datos del sitio*

SQL Server está configurado para la seguridad de autenticación de Windows.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Versión de sistema operativo del sistema de sitio no admitida para la actualización

*Se aplica a: sitio primario, sitio secundario*

Los roles de sistema de sitio que no son puntos de distribución se instalan en servidores que ejecutan Windows Server 2012 o una versión posterior.

Para obtener más información, vea [Sistemas operativos compatibles con servidores de sistema de sitio de Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

> [!NOTE]  
> Esta comprobación no puede resolver el estado de los roles de sistema de sitio instalados en Azure o del almacenamiento en la nube usado por Microsoft Intune. Omita las advertencias para estos roles como falsos positivos.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>La actualización del kit de herramientas de evaluación no es compatible

*Se aplica a: sitio primario, sitio de administración central*

La actualización del kit de herramientas de evaluación no está instalada. Para más información, consulte [Características en desuso y eliminadas](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Comprobar los permisos de servidor de sitio para publicar en Active Directory

*Se aplica a: sitio de administración central, sitio primario o sitio secundario*

La cuenta de equipo del servidor de sitio tiene permisos de **Control total** en el contenedor **System Management** en el dominio de Active Directory.

Para más información, vea [Preparar Active Directory para la publicación de sitios](../../../plan-design/network/extend-the-active-directory-schema.md).

> [!NOTE]  
> Si ha comprobado manualmente los permisos, puede omitir esta advertencia.

### <a name="windows-remote-management-winrm-v11"></a>Administración remota de Windows (WinRM) v1.1

*Se aplica a: sitio primario, consola de Configuration Manager*

WinRM 1.1 está instalado en el servidor de sitio primario o en el equipo de la consola de Configuration Manager para ejecutar la consola de administración fuera de banda.

WinRM se instala automáticamente con todas las versiones de Windows admitidas actualmente. Para más información, vea [Instalación y configuración de Administración remota de Windows](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### <a name="wsus-on-site-server"></a>WSUS en servidor de sitio

*Se aplica a: sitio primario, sitio de administración central*

Hay una versión compatible de Windows Server Update Services (WSUS) instalada en el servidor de sitio.

Cuando se utiliza un punto de actualización de software en un servidor distinto al servidor del sitio, debe instalar la consola de administración de WSUS en el servidor de sitio. Para obtener más información sobre WSUS, vea [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).