---
title: Parámetros y propiedades de instalación de cliente
titleSuffix: Configuration Manager
description: Obtenga información sobre los parámetros y propiedades de la línea de comandos de ccmsetup para instalar el cliente de Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 518954457ba58656aeb1986689a3cf74ce918c02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693613"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Acerca de los parámetros y propiedades de instalación de cliente en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use el comando CCMSetup.exe para instalar el cliente de Configuration Manager. Si proporciona *parámetros* de instalación de cliente en la línea de comandos, modificarán el comportamiento de la instalación. Si proporciona *propiedades* de instalación de cliente en la línea de comandos, modificarán la configuración inicial del agente cliente instalado.

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> Acerca de CCMSetup.exe

El comando CCMSetup.exe descarga los archivos necesarios para instalar el cliente desde un punto de administración o una ubicación de origen. Es posible que estos archivos incluyan:  

- El paquete de Windows Installer client.msi que instala el software cliente

- Requisitos previos del cliente

- Actualizaciones y correcciones para el cliente de Configuration Manager

> [!NOTE]
> No se puede instalar client.msi directamente.  

CCMSetup.exe proporciona *parámetros* de línea de comandos para personalizar la instalación. Los parámetros van precedidos de una barra diagonal (`/`) y, por convención, están en minúsculas. Puede especificar el valor de un parámetro en caso necesario mediante el uso de dos puntos (`:`) inmediatamente seguidos del valor. Para obtener más información, vea [Parámetros de línea de comandos de CCMSetup.exe](#ccmsetupexe-command-line-parameters).

También puede proporcionar *propiedades* en la línea de comandos de CCMSetup.exe para modificar el comportamiento de client.msi. Las propiedades, por convención, van en mayúsculas. Puede especificar un valor para una propiedad mediante el uso de un signo igual (`=`) inmediatamente seguido del valor. Para obtener más información, vea [Propiedades de Client.msi](#clientMsiProps).

> [!IMPORTANT]  
> Especifique los parámetros de CCMSetup antes de especificar propiedades para client.msi.  

CCMSetup.exe y los archivos auxiliares se encuentran en el servidor de sitio en la carpeta **Client** de la carpeta de instalación de Configuration Manager. Configuration Manager comparte esta carpeta con la red en el recurso compartido del sitio. Por ejemplo, `\\SiteServer\SMS_ABC\Client`.

En el símbolo del sistema, el comando CCMSetup.exe utiliza el formato siguiente:  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

Por ejemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

Este ejemplo hace lo siguiente:  

- Especifica al punto de administración denominado SMSMP01 que solicite una lista de puntos de distribución para descargar los archivos de instalación de cliente.  

- Especifica que la instalación debe detenerse si ya existe una versión del cliente en el equipo.  

- Indica a client.msi que asigne el cliente al código del sitio S01.  

- Indica a client.msi que use el punto de estado de reserva denominado SMSFP01.  

> [!TIP]  
> Si un valor de parámetro tiene espacios, póngalo entre comillas.  

Si amplía el esquema de Active Directory para Configuration Manager, el sitio publica muchas propiedades de instalación de cliente en Active Directory Domain Services. El cliente de Configuration Manager lee dichas propiedades automáticamente. Para obtener más información, vea [Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="ccmsetupexe-command-line-parameters"></a>Parámetros de línea de comandos de CCMSetup.exe

### <a name=""></a><a name="bkmk_help"></a> /?

Muestra los parámetros de línea de comandos disponibles para ccmsetup.exe.  

Ejemplo: `ccmsetup.exe /?`

### <a name="source"></a>/source

Especifica la ubicación de descarga de archivos. Use una ruta de acceso local o UNC. El dispositivo descarga los archivos mediante el protocolo de bloque de mensajes del servidor (SMB). Para usar **/source**, la cuenta de usuario de Windows para la instalación de cliente debe tener permisos de **lectura** para la ubicación.

> [!TIP]  
> Puede usar el parámetro **/source** más de una vez en una línea de comandos para especificar ubicaciones de descarga alternativas.  

Ejemplo: `ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/mp

Especifica un punto de administración de origen al que se van a conectar los equipos. Los equipos usan dicho punto de administración para encontrar el punto de distribución más cercano para los archivos de instalación. Si no hay ningún punto de distribución o los equipos no pueden descargar los archivos desde los puntos de distribución después de cuatro horas, descargan los archivos desde el punto de administración especificado.  

> [!IMPORTANT]  
> Este parámetro especifica un punto de administración inicial para que los equipos busquen un origen de descarga. Puede ser cualquier punto de administración en cualquier sitio. No *asigna* el cliente al punto de administración especificado.

Los equipos descargan los archivos a través de una conexión HTTP o HTTPS, dependiendo de la configuración del rol de sistema de sitio para las conexiones de cliente. La descarga también puede usar la limitación de BITS, si se configura. Si configura todos los puntos de distribución y puntos de administración solo para conexiones cliente HTTPS, compruebe que el equipo cliente tenga un certificado de cliente válido.  

Puede usar el parámetro de línea de comandos **/mp** para especificar más de un punto de administración. Si el equipo no puede conectarse al primero, prueba con el siguiente de la lista especificada. Cuando especifique varios puntos de administración, separe los valores con puntos y comas.

Si el cliente se conecta a un punto de administración mediante HTTPS, especifica el FQDN, no el nombre del equipo. El valor debe coincidir con el **nombre del firmante** o el **nombre alternativo del firmante** del certificado PKI del punto de administración. Aunque Configuration Manager admita el uso de un nombre de equipo en el certificado para conexiones en la intranet, se recomienda el uso de un FQDN.

Ejemplo con el nombre de equipo: `ccmsetup.exe /mp:SMSMP01`  

Ejemplo con el FQDN: `ccmsetup.exe /mp:smsmp01.contoso.com`  

Este parámetro también puede especificar la dirección URL de una instancia de Cloud Management Gateway (CMG). Use esta dirección URL para instalar el cliente en un dispositivo basado en Internet. Para obtener el valor de este parámetro, siga los pasos siguientes:

- Cree una instancia de CMG. Para más información, vea [Configurar una instancia de CMG](../manage/cmg/setup-cloud-management-gateway.md).
- En un cliente activo, abra un símbolo del sistema de Windows PowerShell como administrador.
- Ejecute el comando siguiente:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Anexe el prefijo `https://` para usarlo con el parámetro **/mp**.

Ejemplo para cuando use la dirección URL de la instancia de Cloud Management Gateway: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`.

> [!Important]
> Cuando especifique la dirección URL de una instancia de Cloud Management Gateway para el parámetro **/mp**, debe comenzar con `https://`.

### <a name="regtoken"></a>/regtoken

<!--5686290-->

A partir de la versión 2002, use este parámetro para proporcionar un token de registro masivo. Los dispositivos basados en Internet usan este token en el proceso de registro a través de una instancia de Cloud Management Gateway (CMG). Para obtener más información, vea [Autenticación basada en tokens para CMG](deploy-clients-cmg-token.md).

Cuando use este parámetro, incluya también los siguientes parámetros y propiedades:

- [ **/mp**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

La línea de comandos que hay a continuación incluye el resto de las propiedades y los parámetros necesarios:

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

Si CCMSetup.exe no puede descargar los archivos de instalación, use este parámetro para especificar el intervalo de reintentos en minutos. CCMSetup continúa intentándolo hasta que alcanza el límite especificado en el parámetro [ **/downloadtimeout**](#downloadtimeout).

Ejemplo: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Este parámetro impide que CCMSetup se ejecute como un servicio, algo que hace de forma predeterminada. Cuando CCMSetup se ejecuta como un servicio, se ejecuta en el contexto de la cuenta de sistema local del equipo. Esta cuenta podría no disponer de los derechos suficientes para tener acceso a los recursos de red necesarios para la instalación. Con **/noservice**, CCMSetup.exe se ejecuta en el contexto de la cuenta de usuario usada para iniciar la instalación.

Ejemplo: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Especifica que CCMSetup debe ejecutarse como un servicio que usa la cuenta de sistema local.  

> [!TIP]
> Si usa un script para ejecutar CCMSetup.exe con el parámetro **/service**, CCMSetup.exe se cierra después del inicio del servicio. Es posible que no proporcione los detalles de la instalación correctamente.

Ejemplo: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Use este parámetro para desinstalar el cliente de Configuration Manager. Para obtener más información, consulte [Desinstalación del cliente](../manage/manage-clients.md#BKMK_UninstalClient).

Ejemplo: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Si ya hay instalada una versión del cliente, este parámetro especifica que la instalación del cliente debe detenerse.  

Ejemplo: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

Use este parámetro para exigir que el equipo se reinicie si es necesario para completar la instalación. Si no especifica este parámetro, CCMSetup se cierra cuando es necesario reiniciar. Después, continúa tras el siguiente reinicio manual.

Ejemplo: `CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

Cuando el dispositivo descargue los archivos de instalación del cliente a través de una conexión HTTP, use este parámetro para especificar la prioridad de la descarga. Especifique uno de los siguientes valores posibles:

- `FOREGROUND`

- `HIGH`

- `NORMAL` (valor predeterminado)

- `LOW`

Ejemplo: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

Si CCMSetup no puede descargar los archivos de instalación del cliente, este parámetro especifica el tiempo de espera máximo en minutos. Después de este tiempo de espera, CCMSetup deja de intentar descargar los archivos de instalación. El valor predeterminado es **1440** minutos (un día).

Use el parámetro [ **/retry**](#retry) para especificar el intervalo entre reintentos.

Ejemplo: `ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

Especifique este parámetro para que el cliente use un certificado de autenticación de cliente PKI. Si no incluye este parámetro, o si el cliente no encuentra un certificado válido, usa una conexión HTTP con un certificado autofirmado.

Ejemplo: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> En algunos escenarios, no será necesario especificar este parámetro, pero siga usando un certificado de cliente. Por ejemplo, la instalación de cliente basada en inserciones de cliente y actualizaciones de software. Use este parámetro cuando instale manualmente un cliente y use el parámetro **/mp** con un punto de administración habilitado para HTTPS.
>
> Especifique también este parámetro cuando instale un cliente para comunicarse solo a través de Internet. Use la propiedad **CCMALWAYSINF=1** junto con las propiedades para el punto de administración basado en Internet (**CCMHOSTNAME**) y el código de sitio (**SMSSITECODE**). Para obtener más información sobre la administración de clientes basada en Internet, vea [Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

### <a name="nocrlcheck"></a>/NoCRLCheck

Especifica que un cliente no debe comprobar la lista de revocación de certificados (CRL) cuando se comunica a través de HTTPS con un certificado PKI. Cuando no se especifica este parámetro, el cliente comprueba la CRL antes de establecer una conexión HTTPS. Para obtener más información sobre la comprobación de CRL de cliente, vea [Planear la revocación de certificados PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Ejemplo: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

Este parámetro especifica un archivo de texto que enumera las propiedades de la instalación de cliente.

- Si CCMSetup se ejecuta como un servicio, coloque este archivo en la carpeta del sistema CCMSetup: `%Windir%\Ccmsetup`.

- Si especifica el parámetro [ **/noservice**](#noservice), coloque este archivo en la misma carpeta que CCMSetup.exe.

Ejemplo: `CCMSetup.exe /config:"configuration file name.txt"`

Para proporcionar el formato de archivo correcto, use el archivo **mobileclienttemplate.tcf** de la carpeta `\bin\<platform>` en el directorio de instalación de Configuration Manager del servidor de sitio. Este archivo tiene comentarios sobre las secciones y cómo se usan. Especifique las propiedades de la instalación del cliente en la sección `[Client Install]`, después del texto siguiente: `Install=INSTALL=ALL`.

Ejemplo de entrada de la sección `[Client Install]`: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`.  

### <a name="skipprereq"></a>/skipprereq

Este parámetro especifica que CCMSetup.exe no instala el requisito previo especificado. Puede especificar más de un valor. Use el carácter de punto y coma (`;`) para separar cada valor.

Ejemplos:

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

Para obtener más información sobre los requisitos previos de cliente, vea [Requisitos previos de cliente de Windows](prerequisites-for-deploying-clients-to-windows-computers.md).

### <a name="forceinstall"></a>/forceinstall

Especifica que CCMSetup.exe desinstala los clientes existentes e instala un cliente nuevo.  

### <a name="excludefeatures"></a>/ExcludeFeatures

Este parámetro especifica que CCMSetup.exe no instala la característica especificada.

Ejemplo: `CCMSetup.exe /ExcludeFeatures:ClientUI` no instala el Centro de software en el cliente.  

> [!NOTE]  
> `ClientUI` es el único valor compatible con el parámetro **/ExcludeFeatures**.

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> Códigos de retorno de CCMSetup.exe

El comando CCMSetup.exe proporciona los siguientes códigos de retorno. Para solucionar problemas, revise el archivo `%WinDir%\ccmsetup\ccmsetup.log` en el cliente para determinar el contexto y los detalles adicionales sobre los códigos de retorno.

|Código de retorno|Significado|  
|-----------|-------|  
|0|Correcto|  
|6|Error|  
|7|Es necesario reiniciar|  
|8|El programa de instalación se está ejecutando|  
|9|Error de evaluación de requisitos previos|  
|10|Error de validación de hash del manifiesto de la instalación|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a> Propiedades de Ccmsetup.msi

Las siguientes propiedades pueden modificar el comportamiento de la instalación de ccmsetup.msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

Use esta propiedad de ccmsetup.*msi* para pasar más parámetros y propiedades de la línea de comandos a ccmsetup.*exe*. Incluye otros parámetros y propiedades entre comillas (`"`). Use esta propiedad cuando arranque el cliente de Configuration Manager con el [método de instalación de MDM de Intune](plan/client-installation-methods.md#microsoft-intune-mdm-installation).

Ejemplo: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune limita la línea de comandos a 1024 caracteres.

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a> Propiedades de Client.msi

Las siguientes propiedades pueden modificar el comportamiento de la instalación de client.msi, instalado por ccmsetup.exe. Si usa el [método de instalación de inserción de cliente](plan/client-installation-methods.md#client-push-installation), especifique estas propiedades en la pestaña **Cliente** de **Propiedades de instalación de inserción de cliente** en la consola de Configuration Manager.

### <a name="aadclientappid"></a>AADCLIENTAPPID

Especifica el identificador de aplicación cliente de Azure Active Directory (Azure AD). La aplicación cliente se crea o importa al [configurar servicios de Azure](../../servers/deploy/configure/azure-services-wizard.md) para la administración en la nube. Un administrador de Azure puede obtener el valor de esta propiedad desde Azure Portal. Para obtener más información, vea [Obtención del id. y la clave de autenticación de la aplicación](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). Para la propiedad **AADCLIENTAPPID**, este identificador de aplicación es para el tipo de aplicación **Native**.

Ejemplo: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Especifica el identificador de aplicación de servidor de Azure AD. La aplicación de servidor se crea o importa al [configurar servicios de Azure](../../servers/deploy/configure/azure-services-wizard.md) para la administración en la nube. Al crear la aplicación de servidor, en la ventana Crear aplicación de servidor, esta propiedad es el **URI de id. de aplicación**.

Un administrador de Azure puede obtener el valor de esta propiedad desde Azure Portal. En **Azure Active Directory**, busque la aplicación de servidor en **Registros de aplicaciones**. Busque el tipo de aplicación **Aplicación web o API**. Abra la aplicación, seleccione **Configuración** y, después, elija **Propiedades**. Use el valor del **URI de id. de aplicación** para esta propiedad de instalación de cliente **AADRESOURCEURI**.

Ejemplo: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

Especifica el identificador de inquilino de Azure AD. Configuration Manager vincula a este inquilino al [configurar servicios de Azure](../../servers/deploy/configure/azure-services-wizard.md) para la administración en la nube. Para obtener el valor de esta propiedad, siga los pasos siguientes:

- En un dispositivo Windows 10 unido al mismo inquilino de Azure AD, abra un símbolo del sistema.
- Ejecute el comando siguiente: `dsregcmd.exe /status`.
- En la sección Estado del dispositivo, busque el valor **TenantId**. Por ejemplo, `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`.

  > [!Note]
  > Un administrador de Azure también puede obtener este valor en Azure Portal. Para obtener más información, vea [Obtención del identificador de inquilino](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).

Ejemplo: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Especifica la concesión del acceso de una o más cuentas o grupos de usuarios de Windows a directivas y configuraciones de cliente. Esta propiedad es útil si no tiene credenciales administrativas locales en el equipo cliente. Especifique una lista de cuentas separadas por punto y coma (`;`).

Ejemplo: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Si es necesario, permita que el equipo se reinicie automáticamente después de la instalación del cliente.

> [!IMPORTANT]  
> Cuando se usa esta propiedad, el equipo se reinicia sin previo aviso. Este comportamiento se produce incluso si un usuario ha iniciado sesión en Windows.

Ejemplo: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

Para especificar que el cliente siempre está basado en Internet y nunca se conecta a la intranet, establezca el valor de esta propiedad en `1`. El tipo de conexión del cliente muestra **Siempre Internet**.  

Use esta propiedad con [**CCMHOSTNAME**](#ccmhostname) para especificar el FQDN del punto de administración basado en Internet. Úselo también con el parámetro de CCMSetup [ **/UsePKICert**](#usepkicert) y con el código de sitio ([**SMSSITECODE**](#smssitecode)).

Para obtener más información sobre la administración de clientes basada en Internet, vea [Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).

Ejemplo: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

Use esta propiedad para especificar la lista de emisores de certificados. Esta lista incluye información de certificado sobre las entidades de certificación raíz de confianza en las que confía el sitio de Configuration Manager.  

Este valor es una coincidencia de mayúsculas y minúsculas de los atributos del firmante que se encuentran en el certificado de entidad de certificación raíz. Separe los atributos mediante una coma (`,`) o un punto y coma (`;`). Para especificar más de un certificado de entidad de certificación raíz, use una barra de separación (`|`).

Ejemplo: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> Use el valor del atributo **CertificateIssuers** en el archivo **mobileclient.tcf** para el sitio. Este archivo se encuentra en la subcarpeta `\bin\<platform>` del directorio de instalación de Configuration Manager, en el servidor del sitio.

Para obtener más información sobre la lista de emisores de certificados y cómo los clientes la usan durante el proceso de selección de certificados, vea [Planear la selección de certificados de cliente PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).

### <a name="ccmcertsel"></a>CCMCERTSEL

Si el cliente tiene más de un certificado para la comunicación HTTPS, esta propiedad especifica los criterios para que seleccione un certificado de autenticación de cliente válido.

Use las siguientes palabras clave para buscar el nombre del firmante o el nombre alternativo del firmante del certificado:

- **Asunto**: busca una coincidencia exacta.
- **SubjectStr**: busca una coincidencia parcial.

Ejemplos:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: busca un certificado con una coincidencia exacta con el nombre de equipo `computer1.contoso.com` en el nombre del firmante o en el nombre alternativo del firmante.

- `CCMCERTSEL="SubjectStr:contoso.com"`: busca un certificado que contenga `contoso.com` en el nombre del firmante o en el nombre alternativo del firmante.

Use la palabra clave **SubjectAttr** para buscar los atributos de nombre distintivo (DN) o de identificador de objeto (OID) en el nombre del firmante o el nombre alternativo del firmante.

Ejemplos:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: busca el atributo de unidad organizativa expresado como un identificador de objeto y con el nombre `Computers`.

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: busca el atributo de unidad organizativa expresado como un nombre distintivo (DN) y con el nombre `Computers`.

> [!IMPORTANT]
> Si usa el nombre del firmante, la palabra clave **Subject** distingue mayúsculas de minúsculas y la palabra clave **SubjectStr** no distingue mayúsculas de minúsculas.
>
> Si usa el nombre alternativo del firmante, las palabras clave **Subject** y **SubjectStr** no distinguen mayúsculas de minúsculas.

Para obtener la lista completa de atributos que puede usar para la selección de certificados, consulte [Valores de atributos admitidos para los criterios de selección de certificado PKI](#BKMK_attributevalues).

Si más de un certificado coincide con la búsqueda y establece la propiedad [**CCMFIRSTCERT**](#ccmfirstcert) en `1`, el instalador del cliente selecciona el certificado con el período de validez más largo.

### <a name="ccmcertstore"></a>CCMCERTSTORE

Si el instalador del cliente no encuentra un certificado válido en el almacén de certificados **Personal** predeterminado para el equipo, use esta propiedad para especificar un nombre de almacén de certificados alternativo.

Ejemplo: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

Esta propiedad habilita el registro de depuración cuando se instala el cliente. Esta propiedad hace que el cliente registre información de bajo nivel para la solución de problemas. Evite usar esta propiedad en sitios de producción. Puede producirse un registro excesivo, lo que podría hacer que resultase difícil encontrar información relevante en los archivos de registro. Habilite también [**CCMENABLELOGGING**](#ccmenablelogging).

Valores admitidos:

- `0`: desactiva el registro de depuración (valor predeterminado).
- `1`: activa el registro de depuración.

Ejemplo: `CCMSetup.exe CCMDEBUGLOGGING=1`  

Para obtener más información, consulte [Acerca de los archivos de registro](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Configuration Manager habilita el registro de forma predeterminada.

Valores admitidos:

- `TRUE`: activa el registro (valor predeterminado).
- `FALSE`: desactiva el registro.

Ejemplo: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

Para obtener más información, consulte [Acerca de los archivos de registro](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

Indica la frecuencia en minutos a la que se ejecuta la herramienta de evaluación de mantenimiento del cliente (ccmeval.exe). Especifique un valor entero comprendido entre `1` y `1440`. De forma predeterminada, ccmeval se ejecuta una vez al día (1440 minutos).

Ejemplo: `CCMSetup.exe CCMEVALINTERVAL=1440`

Para obtener más información sobre la evaluación de mantenimiento del cliente, consulte [Supervisión de clientes](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmevalhour"></a>CCMEVALHOUR

Indica la hora del día a la que se ejecuta la herramienta de evaluación de mantenimiento del cliente (ccmeval.exe). Especifique un valor entero comprendido entre `0` (medianoche) y `23` (23:00). De forma predeterminada, ccmeval se ejecuta a la medianoche.

Para obtener más información sobre la evaluación de mantenimiento del cliente, consulte [Supervisión de clientes](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

Si establece esta propiedad en `1`, el cliente seleccionará el certificado PKI con el período de validez más largo.

Ejemplo: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

Si el cliente se administra a través de Internet, esta propiedad especifica el FQDN del punto de administración basado en Internet.  

No especifique esta opción con la propiedad de instalación **SMSSITECODE=AUTO**. Asigne directamente los clientes basados en Internet a un sitio basado en Internet.

Ejemplo: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Esta propiedad puede especificar la dirección de una instancia de Cloud Management Gateway (CMG). Para obtener el valor de esta propiedad, siga los pasos siguientes:

- Cree una instancia de CMG. Para más información, vea [Configurar una instancia de CMG](../manage/cmg/setup-cloud-management-gateway.md).
- En un cliente activo, abra un símbolo del sistema de Windows PowerShell como administrador.
- Ejecute el comando siguiente:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Use el valor devuelto tal cual con la propiedad **CCMHOSTNAME**.

Por ejemplo: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Cuando especifique la dirección de una instancia de CMG para la propiedad **CCMHOSTNAME**, no anexe un prefijo como `https://`. Use este prefijo solo con la dirección URL **/mp** de una instancia de CMG.

### <a name="ccmhttpport"></a>CCMHTTPPORT

Especifica el puerto que el cliente usará al comunicarse a través de HTTP con los servidores de sistema de sitio. De forma predeterminada, este valor es `80`.

Ejemplo: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Especifica el puerto que el cliente usará al comunicarse a través de HTTPS con los servidores de sistema de sitio. De forma predeterminada, este valor es `443`.

Ejemplo: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

Use esta propiedad para establecer la carpeta para instalar los archivos de cliente de Configuration Manager. De forma predeterminada, usa `%WinDir%\CCM`.

> [!TIP]
> Independientemente de la ubicación en la que instale los archivos de cliente, siempre instalará el archivo **ccmcore.dll** en la carpeta `%WinDir%\System32`. En un sistema operativo de 64 bits, instala una copia de ccmcore.dll en la carpeta `%WinDir%\SysWOW64`. Este archivo es compatible con aplicaciones de 32 bits que usan la versión de 32 bits de las API de cliente del SDK de Configuration Manager.

Ejemplo: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Use esta propiedad para especificar el nivel de detalle con el que se va a escribir en los archivos de registro de Configuration Manager.

Valores admitidos:

- `0`: Detallado
- `1`: Predeterminado
- `2`: Advertencias y errores
- `3`: Solo errores

Ejemplo: `CCMSetup.exe CCMLOGLEVEL=0`

Para obtener más información, consulte [Acerca de los archivos de registro](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Cuando un archivo de registro de Configuration Manager alcanza el tamaño máximo, el cliente le cambia el nombre como si fuera una copia de seguridad y crea un archivo de registro. Esta propiedad especifica el número de versiones anteriores del archivo de registro que se van a conservar. El valor predeterminado es `1`. Si establece el valor en `0`, el cliente no conserva ningún historial de archivos de registro.

Ejemplo: `CCMSetup.exe CCMLOGMAXHISTORY=5`

Para obtener más información, consulte [Acerca de los archivos de registro](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Esta propiedad especifica el tamaño máximo del archivo de registro en bytes. Cuando un registro crece hasta el tamaño especificado, el cliente le cambia el nombre como si fuera un archivo de historial y crea uno nuevo. El tamaño predeterminado es de 250 000 bytes y el tamaño mínimo es de 10 000 bytes.

Ejemplo: `CCMSetup.exe CCMLOGMAXSIZE=300000` 300 000 bytes

### <a name="disablesiteopt"></a>DISABLESITEOPT

Establezca esta propiedad en `TRUE` para impedir que los administradores cambien el sitio asignado en el panel de control de Configuration Manager.

Ejemplo: **CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Si se establece en TRUE, esta propiedad deshabilita la posibilidad de que los usuarios administrativos cambien la configuración de la carpeta de caché de cliente en el panel de control de **Configuration Manager**.  

Ejemplo: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

Especifique un dominio DNS para que los clientes localicen los puntos de administración que publique en DNS. Cuando el cliente encuentre un punto de administración, le informará sobre otros puntos de administración en la jerarquía. Este comportamiento implica que el punto de administración que el cliente encuentre en DNS podrá ser cualquiera de la jerarquía.

> [!NOTE]
> No es necesario especificar esta propiedad si el cliente está en el mismo dominio que un punto de administración publicado. En este caso, el dominio del cliente se usa automáticamente para buscar los puntos de administración en DNS.

Para obtener más información sobre la publicación de DNS como método de ubicación del servicio para clientes de Configuration Manager, vea [Ubicación del servicio y cómo los clientes averiguan su punto de administración asignado](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).

> [!NOTE]  
> De forma predeterminada, Configuration Manager no habilita la publicación de DNS.

Ejemplo: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Especifique el punto de estado de reserva que recibe y procesa los mensajes de estado que envían los clientes de Configuration Manager.

Para obtener más información, determine si necesita un [punto de estado de reserva](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).

Ejemplo: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

Si establece esta propiedad en `TRUE`, el instalador del cliente no comprueba la presencia de la versión mínima necesaria de Microsoft Application Virtualization (App-V).

> [!IMPORTANT]  
> Si se instala el cliente de Configuration Manager sin instalar App-V, no se pueden [implementar aplicaciones virtuales](../../../apps/get-started/deploying-app-v-virtual-applications.md).

Ejemplo: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

Cuando se habilita esta propiedad, el cliente informa del estado, pero no soluciona los problemas que encuentre.

Ejemplo: `CCMSetup.exe NOTIFYONLY=TRUE`

Para obtener más información, vea [Cómo configurar el estado de cliente](configure-client-status.md).

### <a name="provisionts"></a>PROVISIONTS

<!--5526972-->

A partir de la versión 2002, use esta propiedad para iniciar una secuencia de tareas en un cliente después de que se registre correctamente en el sitio.

Por ejemplo, puede aprovisionar un nuevo dispositivo Windows 10 con Windows Autopilot, inscribirlo de forma automática en Microsoft Intune y, después, instalar el cliente de Configuration Manager para la administración conjunta. Si especifica esta nueva opción, el cliente recién aprovisionado ejecutará una secuencia de tareas. Este proceso ofrece flexibilidad adicional para instalar aplicaciones y actualizaciones de software, o bien para configurar opciones.

Use el procedimiento siguiente:

1. [Cree una secuencia de tareas de implementación que no sea de sistema operativo](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md) para instalar aplicaciones o actualizaciones de software, así como para configurar opciones.

1. [Implemente esta secuencia de tareas](../../../osd/deploy-use/deploy-a-task-sequence.md) en la nueva recopilación integrada **Todos los dispositivos de aprovisionamiento**. Anote el identificador de la implementación de la secuencia de tareas, por ejemplo, `PRI20001`.

1. [Instale el cliente de Configuration Manager](deploy-clients-to-windows-computers.md#BKMK_Manual) en un dispositivo e incluya la propiedad `PROVISIONTS=PRI20001`. Establezca el valor de esta propiedad como el identificador de la implementación de la secuencia de tareas.

    - Si va a instalar el cliente desde Intune durante la inscripción de administración conjunta, vea [Preparación de dispositivos basados en Internet para la administración conjunta](../../../comanage/how-to-prepare-Win10.md).

      > [!NOTE]
      > Este método puede tener requisitos previos adicionales. Por ejemplo, la inscripción del sitio en Azure Active Directory o la creación de una instancia de Cloud Management Gateway habilitada para el contenido.

Una vez que el cliente se instala y se registra correctamente en el sitio, inicia la secuencia de tareas a la que se hace referencia. Si se produce un error en el registro del cliente, la secuencia de tareas no se iniciará.

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

Si un cliente tiene la clave raíz confiable de Configuration Manager errónea, no puede contactar con un punto de administración confiable para recibir la nueva clave raíz confiable. Use esta propiedad para quitar la antigua clave raíz confiable. Esta situación se puede producir cuando se mueve un cliente de una jerarquía de sitio a otra. Esta propiedad se aplica a los clientes que utilizan la comunicación de cliente HTTP y HTTPS. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Ejemplo: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Habilita la reasignación de sitio automática para las actualizaciones de cliente cuando se usa con [SMSSITECODE=AUTO](#smssitecode).

Ejemplo: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Especifica la ubicación de la carpeta de caché de cliente en el equipo cliente. De forma predeterminada, la ubicación de la caché es `%WinDir%\ccmcache`.

Ejemplo: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Use esta propiedad con la propiedad [**SMSCACHEFLAGS**](#smscacheflags) para controlar la ubicación de la carpeta de caché de cliente. Por ejemplo, para instalar la carpeta de caché de cliente en la unidad de disco de cliente más grande disponible: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`.

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Use esta propiedad para especificar otros detalles de la instalación de la carpeta de caché de cliente. Puede usar las propiedades **SMSCACHEFLAGS** individualmente o en combinación, separadas por punto y coma (`;`).

Si no incluye esta propiedad:

- El cliente instala la carpeta de caché según la propiedad [**SMSCACHEDIR**](#smscachedir).
- La carpeta no se comprime.
- El cliente usa la propiedad [**SMSCACHESIZE**](#smscachesize) como límite de tamaño en MB de la memoria caché.

Cuando se actualiza un cliente existente, el instalador del cliente omite esta propiedad.

#### <a name="values-for-the-smscacheflags-property"></a>Valores de la propiedad SMSCACHEFLAGS

- **PERCENTDISKSPACE**: especifique el tamaño de la caché como un porcentaje del espacio *total* en disco. Si especifica esta propiedad, establezca también [**SMSCACHESIZE**](#smscachesize) en un valor de porcentaje.

- **PERCENTFREEDISKSPACE**: especifique el tamaño de la caché como un porcentaje del espacio *libre* en disco. Si especifica esta propiedad, establezca también [**SMSCACHESIZE**](#smscachesize) en un valor de porcentaje. Por ejemplo, el disco tiene 10 MB libres y usted especifica `SMSCACHESIZE=50`. El instalador del cliente establece el tamaño de la caché en 5 MB. No puede usar esta propiedad con la propiedad **PERCENTDISKSPACE**.

- **MAXDRIVE**: Instale la memoria caché en el disco disponible más grande. Si especifica una ruta de acceso con la propiedad [**SMSCACHEDIR**](#smscachedir), el instalador del cliente omite este valor.

- **MAXDRIVESPACE**: instale la memoria caché en la unidad de disco con más espacio libre. Si especifica una ruta de acceso con la propiedad [**SMSCACHEDIR**](#smscachedir), el instalador del cliente omite este valor.

- **NTFSONLY**: instale la memoria caché únicamente en una unidad de disco con formato NTFS. Si especifica una ruta de acceso con la propiedad [**SMSCACHEDIR**](#smscachedir), el instalador del cliente omite este valor.

- **COMPRESS**: almacene la memoria caché en un formato comprimido.

- **FAILIFNOSPACE**: si no hay espacio suficiente para instalar la memoria caché, quite el cliente de Configuration Manager.

Ejemplo: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Hay opciones de cliente disponibles para especificar el tamaño de la carpeta de caché del cliente. La adición de dichas opciones reemplaza efectivamente el uso de SMSCACHESIZE como propiedad de client.msi para especificar el tamaño de la caché del cliente. Para más información, consulte la [configuración del cliente del tamaño de la caché](about-client-settings.md#client-cache-settings).  

Cuando se actualiza un cliente existente, el instalador del cliente omite esta configuración. El cliente también omite el tamaño de la caché cuando descarga actualizaciones de software.

Ejemplo: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> Si vuelve a instalar un cliente, no puede usar **SMSCACHESIZE** o **SMSCACHEFLAGS** para establecer el tamaño de caché en un valor inferior al anterior. El tamaño anterior es el valor mínimo.

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Use esta propiedad para especificar la ubicación y el orden en que el instalador del cliente comprueba si hay valores de configuración. Es una cadena de uno o más caracteres, cada uno de los cuales define un origen de configuración específico:

- `R`: comprueba los valores de configuración en el Registro.

  Para obtener más información, vea [Aprovisionamiento de propiedades de instalación de cliente](deploy-clients-to-windows-computers.md#BKMK_Provision).

- `P`: comprueba los valores de configuración de las propiedades de instalación proporcionados desde la línea de comandos.

- `M`: comprueba la configuración existente al actualizar un cliente anterior.

- `U`: actualiza el cliente instalado a una versión más reciente y usa el código de sitio asignado.

De forma predeterminada, el instalador del cliente usa `PU`. Primero comprueba las propiedades de instalación (`P`) y, luego, la configuración existente (`U`).  

Ejemplo: `CCMSetup.exe SMSCONFIGSOURCE=RP`

<!--
### SMSDIRECTORYLOOKUP

Specifies whether the client can use Windows Internet Name Service (WINS) to find a management point that accepts HTTP connections. Clients use this method when they can't find a management point in Active Directory Domain Services or in DNS.  

 This property doesn't affect whether the client uses WINS for name resolution.  

 You can configure two different modes for this property:  

-   NOWINS: This value is the most secure setting for this property and prevents clients from finding a management point in WINS. When you use this setting, clients must have an alternative method to locate a management point on the intranet, such as Active Directory Domain Services or by using DNS publishing.  

-   WINSSECURE (default): In this mode, a client that uses HTTP communication can use WINS to find a management point. However, the client must have a copy of the trusted root key before it can successfully connect to the management point. For more information, see [Planning for the trusted root key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

Example: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  
-->

### <a name="smsmp"></a>SMSMP

Especifica un punto de administración inicial para que lo use el cliente de Configuration Manager.  

> [!IMPORTANT]  
> Si el punto de administración solo acepta conexiones de cliente a través de HTTPS, anteponga `https://` al nombre del punto de administración.

Ejemplos:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

Si el cliente no puede obtener de Active Directory Domain Services la clave raíz confiable de Configuration Manager, use esta propiedad para especificar la clave. Esta propiedad se aplica a los clientes que usan la comunicación HTTP y HTTPS. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Ejemplo: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> Obtenga el valor de la clave raíz confiable del sitio desde el archivo mobileclient.tcf en el servidor de sitio. Para obtener más información, consulte [Aprovisionamiento previo de un cliente con la clave raíz confiable mediante un archivo](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file).

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

Use esta propiedad para volver a instalar la clave raíz confiable de Configuration Manager. Especifica el nombre y la ruta de acceso completa en un archivo que contiene la clave raíz confiable. Esta propiedad se aplica a los clientes que utilizan la comunicación de cliente HTTP y HTTPS. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Ejemplo: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

Especifica la ruta de acceso completa y el nombre del certificado autofirmado exportado en el servidor de sitio. El servidor de sitio almacena este certificado en el almacén de certificados de **SMS**. Tiene el nombre de firmante **Servidor de sitio** y el nombre descriptivo **Certificado de firma de servidor de sitio**.

Ejemplo: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

Esta propiedad especifica un sitio de Configuration Manager al que se asigna el cliente. Este valor puede ser un código de sitio de tres caracteres o la palabra `AUTO`. Si se especifica `AUTO`, o si no se especifica esta propiedad, el cliente intenta determinar su asignación de sitio desde Active Directory Domain Services o desde un punto de administración especificado. Para habilitar `AUTO` para las actualizaciones de cliente, establezca también [SITEREASSIGN=TRUE](#sitereassign).

> [!NOTE]  
> Si además especifica un punto de administración basado en Internet con la propiedad [**CCMHOSTNAME**](#ccmhostname), no use `AUTO` con **SMSSITECODE**. Asigne directamente el cliente a su sitio mediante el código de sitio.

Ejemplo: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> Valores de atributo para los criterios de selección de certificados

Configuration Manager admite los siguientes valores de atributos para los criterios de selección de certificado PKI:

|Atributo OID|Atributo de nombre distintivo|Definición de atributo|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|Componente de dominio|  
|1.2.840.113549.1.9.1|E o E-mail|Dirección de correo electrónico|  
|2.5.4.3|CN|Nombre común|  
|2.5.4.4|SN|Nombre de sujeto|  
|2.5.4.5|SERIALNUMBER|Número de serie|  
|2.5.4.6|C|Código de país|  
|2.5.4.7|L|Localidad|  
|2.5.4.8|S o ST|Nombre de estado o provincia|  
|2.5.4.9|STREET|Dirección|  
|2.5.4.10|O|Nombre de la organización|  
|2.5.4.11|OU|Unidad organizativa|  
|2.5.4.12|T o Title|Título|  
|2.5.4.42|G o GN o GivenName|Nombre dado|  
|2.5.4.43|I o Initials|Iniciales|  
|2.5.29.17|(ningún valor)|Nombre alternativo del sujeto|  
