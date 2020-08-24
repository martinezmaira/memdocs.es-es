---
title: Configuración de los portales de BitLocker
titleSuffix: Configuration Manager
description: Instalación de los componentes de administración de BitLocker para el portal de autoservicio y el sitio web de administración y supervisión
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1b07d30c7a593ec0bd70e6c330c57364186f2c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697269"
---
# <a name="set-up-bitlocker-portals"></a>Configuración de los portales de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

Para usar los siguientes componentes de administración de BitLocker en Configuration Manager, primero debe instalarlos:

- Portal de autoservicio del usuario
- Sitio web de administración y supervisión (portal de soporte técnico)

Puede instalar los portales en un servidor de sitio existente o en el servidor del sistema de sitio con IIS instalado, o bien usar un servidor web independiente para hospedarlos.

> [!NOTE]
> A partir de la versión 2006, puede instalar el portal de autoservicio de BitLocker y el sitio web de administración y supervisión en el sitio de administración central.<!-- 5925693 -->
>
> En la versión 2002 y anteriores, instale solo el portal de autoservicio y el sitio web de administración y supervisión con una base de datos de sitio primario. En una jerarquía, instale estos sitios web para cada sitio primario.

Antes de empezar, confirme los [requisitos previos](../../plan-design/bitlocker-management.md#prerequisites) de estos componentes.

## <a name="run-the-script"></a>Ejecución del script

En el servidor web de destino, realice las siguientes acciones:

> [!NOTE]
> Dependiendo del diseño del sitio, puede que tenga que ejecutar el script varias veces. Por ejemplo, ejecute el script en el punto de administración para instalar el sitio web de administración y supervisión. A continuación, ejecútelo de nuevo en un servidor web independiente para instalar el portal de autoservicio.

1. Copie los siguientes archivos de `SMSSETUP\BIN\X64` en la carpeta de instalación de Configuration Manager del servidor de sitio en una carpeta local del servidor de destino:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Ejecute PowerShell como administrador y, luego, ejecute el script de manera similar a la línea de comandos siguiente:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Por ejemplo,

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > En esta línea de comandos de ejemplo se utilizan todos los parámetros posibles para mostrar su uso. Ajuste el uso de acuerdo con los requisitos de su entorno.

Después de la instalación, acceda a los portales a través de las direcciones URL siguientes:

- Portal de autoservicio: `https://webserver.contoso.com/SelfService`
- Sitio web de administración y supervisión: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Microsoft recomienda el uso de HTTPS, pero no es obligatorio. Para obtener más información, vea [Configuración de SSL en IIS](/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="script-usage"></a>Uso del script

Este proceso usa un script de PowerShell, MBAMWebSiteInstaller.ps1, para instalar estos componentes en el servidor web. Acepta los parámetros siguientes:

- `-SqlServerName <ServerName>` (obligatorio): el nombre de dominio completo del servidor de base de datos del sitio.

- `-SqlInstanceName <InstanceName>`: el nombre de instancia de SQL Server de la base de datos del sitio primario. Si SQL usa la instancia predeterminada, no incluya este parámetro.

- `-SqlDatabaseName <DatabaseName>` (obligatorio): el nombre de la base de datos del sitio principal, por ejemplo, `CM_ABC`.

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: la dirección URL del servicio web del punto de servicio de informes del sitio primario. Es el valor **Web Service URL** (Dirección URL del servicio web) en **Administrador de configuración de Reporting Services**.

    > [!NOTE]
    > Este parámetro es para instalar el **informe de auditoría de recuperación** que está vinculado desde el sitio web de administración y supervisión. De forma predeterminada, Configuration Manager incluye los otros informes de administración de BitLocker.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Por ejemplo, `contoso\BitLocker help desk users`. Un grupo de usuarios de dominio cuyos miembros tienen acceso a las áreas **Administrar TPM** y **Recuperación de unidad** del sitio web de administración y supervisión. Al usar estas opciones, este rol tiene que rellenar todos los campos, incluidos el dominio y el nombre de la cuenta del usuario.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Por ejemplo, `contoso\BitLocker help desk admins`. Un grupo de usuarios de dominio cuyos miembros tienen acceso a todas las áreas de recuperación del sitio web de administración y supervisión. Al ayudar a los usuarios a recuperar sus unidades, este rol solo debe escribir la clave de recuperación.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Por ejemplo, `contoso\BitLocker report users`. Un grupo de usuarios de dominio cuyos miembros tienen acceso de solo lectura al área **Informes** del sitio web de administración y supervisión.

    > [!NOTE]
    > El script del instalador no crea los grupos de usuarios de dominio que especifique en los parámetros **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName** y **-MbamReportUsersGroupName**. Antes de ejecutar el script, asegúrese de crear estos grupos.
    >
    > Al especificar los parámetros **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName** y **-MbamReportUsersGroupName**, asegúrese de especificar el nombre de dominio y el nombre de grupo. Use el formato `"domain\user_group"`. No excluya el nombre de dominio. Si el nombre de dominio o el nombre de grupo contiene espacios o caracteres especiales, escriba el parámetro entre comillas (`"`).

- `-SiteInstall Both`: especifique los componentes que se van a instalar. Hay varias opciones válidas:
  - `Both`: instale varios componentes.
  - `HelpDesk`: instale solo el sitio web de administración y supervisión
  - `SSP`: instale solo el portal de autoservicio.

- `-IISWebSite`: el sitio web donde el script instala las aplicaciones web de MBAM. De manera predeterminada, usa el sitio web predeterminado de IIS. Cree el sitio web personalizado antes de usar este parámetro.

- `-InstallDirectory`: La ruta de acceso donde el script instala los archivos de aplicación web. De forma predeterminada, esta ruta de acceso es `C:\inetpub`. Cree el directorio personalizado antes de usar este parámetro.

- `-Uninstall`: desinstala los sitios del portal web del departamento de ayuda de administración de BitLocker/autoservicio en un servidor web en el que se han instalado previamente.

## <a name="verify"></a>Comprobar

Use los registros siguientes para la supervisión y solución de problemas:

- Registros de eventos de Windows en **Microsoft-Windows-MBAM-Web**. Para obtener más información, vea [Registros de eventos de BitLocker](../../tech-ref/bitlocker/about-event-logs.md) y [Registros de eventos del servidor](../../tech-ref/bitlocker/server-event-logs.md).

- Los registros de seguimiento de cada componente se encuentran en las siguientes ubicaciones predeterminadas:

  - Portal de autoservicio: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Sitio web de administración y supervisión: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Para obtener más información acerca de la solución de problemas, vea [Solución de problemas de BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

## <a name="next-steps"></a>Pasos siguientes

[Personalización del portal de autoservicio](customize-self-service-portal.md)

Para obtener más información sobre el uso de los componentes que instaló, consulte los siguientes artículos:

- [Sitio web de administración y supervisión de BitLocker](helpdesk-portal.md)
- [Portal de autoservicio de BitLocker](self-service-portal.md)