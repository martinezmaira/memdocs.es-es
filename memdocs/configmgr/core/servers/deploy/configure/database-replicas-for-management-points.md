---
title: Réplicas de bases de datos de punto de administración
titleSuffix: Configuration Manager
description: Use una réplica de base de datos para reducir la carga de CPU que los puntos de administración colocan en el servidor de base de datos del sitio.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db1e0d78263d264c66eed7258db800397baad735
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607588"
---
# <a name="database-replicas-for-management-points-for-configuration-manager"></a>Réplicas de bases de datos para puntos de administración de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los sitios primarios de Configuration Manager pueden usar una réplica de base de datos para reducir la carga de CPU que los puntos de administración colocan en el servidor de base de datos del sitio mientras atienden las solicitudes de servicio de los clientes.  

-   Cuando un punto de administración usa una réplica de base de datos, dicho punto de administración solicita datos desde el equipo de SQL Server que hospeda la réplica de base de datos, en lugar de desde el servidor de base de datos del sitio.  

-   Esto puede ayudar a reducir los requisitos de procesamiento de CPU en el servidor de base de datos del sitio mediante la descarga de tareas de procesamiento frecuentes relacionadas con los clientes.  Un ejemplo de tareas de procesamiento frecuentes para clientes son los sitios en los que hay un gran número de clientes que realizan solicitudes frecuentes para la directiva de cliente  


##  <a name="prepare-to-use-database-replicas"></a><a name="bkmk_Prepare"></a> Prepararse para el uso de réplicas de base de datos  
**Información sobre las réplicas de bases de datos para puntos de administración:**  

-   Las réplicas son una copia parcial de la base de datos que se replica en una instancia independiente de SQL Server:  

    -   Los sitios primarios admiten una réplica de base de datos dedicada para cada punto de administración en el sitio (los sitios secundarios no admiten réplicas de bases de datos)  

    -   Una sola réplica de base de datos se puede usar en más de un punto de administración desde el mismo sitio  

    -   Un servidor SQL Server puede hospedar varias réplicas de bases de datos que podrán usar distintos puntos de administración, siempre y cuando cada uno de ellos se ejecute en una instancia independiente de SQL Server  

-   Las réplicas sincronizan una copia de la base de datos según una programación fija de los datos publicados por el servidor de bases de datos de los sitios para este propósito.  

-   Los puntos de administración pueden configurarse para que usen una réplica al instalar el punto de administración, o más tarde al volver a configurar el punto de administración previamente instalado para usar la réplica de base de datos  

-   Supervise regularmente el servidor de base de datos del sitio, así como cada servidor de réplica de la base de datos para garantizar que la replicación tiene lugar entre ellos y que el rendimiento del servidor de réplica de base de datos es suficiente para el sitio y para el rendimiento de cliente requerido.  

**Requisitos previos para las réplicas de bases de datos:**  

-   **Requisitos de SQL Server:**  

    -   El servidor SQL Server que hospeda la réplica de base de datos debe cumplir los mismos requisitos que el servidor de base de datos del sitio. Sin embargo, el servidor de réplica no tiene por qué ejecutar la misma versión o edición de SQL Server que el servidor de base de datos del sitio, siempre y cuando ejecute una versión y edición compatibles de SQL Server. Para más información, vea [Versiones de SQL Server compatibles con Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

    -   El servicio SQL Server en el equipo que hospeda la base de datos de réplica debe ejecutarse como la cuenta del **sistema** .  

    -   Tanto el servidor SQL Server que hospeda la base de datos del sitio como el que hospeda la réplica de base de datos deben tener la **Replicación de SQL Server** instalada.  

    -   La base de datos del sitio debe **publicar** la réplica de base de datos y cada uno de los servidores remotos de réplica de la base de datos deben **suscribirse** a los datos publicados.  

    -   Tanto el servidor de SQL Server que hospeda la base de datos del sitio como el que hospeda una réplica de la base de datos deben configurarse para admitir un **Tamaño de replicación de texto máximo** de 2 GB. Para obtener un ejemplo acerca de cómo configurarlo para SQL Server 2012, consulte [Establecer la opción de configuración del servidor Tamaño de replicación de texto máximo](/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option).  

-   **Certificado autofirmado**: para configurar una réplica de base de datos, debe crear un certificado autofirmado en el servidor de réplica de base de datos y hacer que este certificado esté disponible para todos los puntos de administración que van a usar ese servidor de réplica de base de datos.  

    -   El certificado está automáticamente disponible para un punto de administración que está instalado en el servidor de réplica de base de datos.  

    -   Para que este certificado esté disponible para los puntos de administración remotos, debe exportar el certificado y agregarlo al almacén de certificados de **Personas de confianza** en el punto de administración remoto.  

-   **Notificación de cliente:** para admitir la notificación de cliente con una réplica de base de datos para un punto de administración, debe configurar la comunicación entre el servidor de base de datos del sitio y el servidor de réplica de base de datos para **SQL Server Service Broker**. Para ello, deberá hacer lo siguiente:  

    -   Configurar cada base de datos con información sobre la otra base de datos  

    -   Intercambiar los certificados entre las dos bases de datos para una comunicación segura  

**Limitaciones al usar réplicas de bases de datos:**  

-   Cuando se configura el sitio para publicar las réplicas de bases de datos, deben seguirse estos procedimientos en lugar de la orientación habitual:  

    -   [Desinstalar un servidor de sitio que publica una réplica de base de datos](#BKMK_DBReplicaOps_Uninstall)  

    -   [Mover una base de datos de servidor de sitio que publica una réplica de base de datos](#BKMK_DBReplicaOps_Move)  

-   **Actualización a la rama actual de Configuration Manager**: antes de actualizar un sitio de System Center 2012 Configuration Manager a la rama actual de Configuration Manager o de actualizar la rama actual de Configuration Manager a la última versión, debe deshabilitar las réplicas de bases de datos para los puntos de administración.  Después de actualizar los sitios, puede volver a configurar las réplicas de bases de datos de los puntos de administración.  

-   **Varias réplicas en un único servidor de SQL Server:**  si configura un servidor de réplica de bases de datos para hospedar varias réplicas de bases de datos para puntos de administración (cada réplica debe estar en una instancia independiente), debe usar un script de configuración modificado (del paso 4 de la sección siguiente) para impedir que se sobrescriba el certificado autofirmado que usaban las réplicas de bases de datos previamente configuradas en ese servidor.  

- Las implementaciones de usuario en el Centro de software no funcionarán en un punto de administración con una réplica de SQL. <!--sccmdocs-1011-->

##  <a name="configure-database-replicas"></a><a name="BKMK_DBReplica_Config"></a> Configurar réplicas de bases de datos  
Para configurar una réplica de base de datos, debe seguir los siguientes pasos:  

-   [Paso 1: configurar el servidor de base de datos del sitio para publicar la réplica de base de datos](#BKMK_DBReplica_ConfigSiteDB)  

-   [Paso 2: configurar el servidor de réplica de bases de datos](#BKMK_DBReplica_ConfigSrv)  

-   [Paso 3: configurar los puntos de administración para usar la réplica de base de datos](#BKMK_DBReplica_ConfigMP)  

-   [Paso 4: configurar un certificado autofirmado para el servidor de réplica de base de datos](#BKMK_DBReplica_Cert)  

-   [Paso 5: configurar SQL Server Service Broker para el servidor de réplica de base de datos](#BKMK_DBreplica_SSB)  

###  <a name="step-1---configure-the-site-database-server-to-publish-the-database-replica"></a><a name="BKMK_DBReplica_ConfigSiteDB"></a> Paso 1: configurar el servidor de base de datos del sitio para publicar la réplica de base de datos  
 Utilice el procedimiento siguiente como ejemplo de cómo configurar el servidor de base de datos del sitio en un equipo Windows Server 2008 R2 para publicar la réplica de base de datos. Si tiene otra versión de sistema operativo, consulte la documentación del sistema operativo correspondiente y adapte los pasos de este procedimiento, si fuera necesario.  

##### <a name="to-configure-the-site-database-server"></a>Para configurar el servidor de base de datos del sitio  

1.  En el servidor de base de datos del sitio, establezca el Agente SQL Server para que se inicie automáticamente.  

2.  En el servidor de base de datos del sitio, cree un grupo de usuarios local con el nombre **ConfigMgr_MPReplicaAccess**. Debe agregar la cuenta de equipo a cada servidor de réplica de base de datos que utilice en este sitio a este grupo para que dichos servidores se sincronicen con la réplica de base de datos publicada.  

3.  En el servidor de base de datos del sitio, configure un recurso compartido de archivos con el nombre **ConfigMgr_MPReplica**.  

4.  Agregue los siguientes permisos al recurso compartido **ConfigMgr_MPReplica** :  

    > [!NOTE]  
    >  Si el Agente SQL Server utiliza una cuenta distinta de la cuenta sistema local, reemplace SYSTEM con ese nombre de cuenta en la lista siguiente.  

    -   **Permisos de recurso compartido**:  

        -   SISTEMA: **Escritura**  

        -   ConfigMgr_MPReplicaAccess: **Lectura**  

    -   **Permisos NTFS**:  

        -   SISTEMA: **Control total**  

        -   ConfigMgr_MPReplicaAccess: **Lectura**, **Lectura y ejecución**, **Mostrar el contenido de la carpeta**  

5.  Use **SQL Server Management Studio** para conectarse a la base de datos del sitio y ejecute el siguiente procedimiento almacenado como una consulta: **spCreateMPReplicaPublication**  

Cuando se completa el procedimiento almacenado, el servidor de base de datos del sitio está configurado para publicar la réplica de base de datos.  

###  <a name="step-2---configuring-the-database-replica-server"></a><a name="BKMK_DBReplica_ConfigSrv"></a> Paso 2: configurar el servidor de réplica de bases de datos  
El servidor de réplica de base de datos es un equipo que ejecuta SQL Server y que hospeda una réplica de la base de datos del sitio para que la utilicen los puntos de administración. En una programación fija, el servidor de réplica de base de datos sincroniza su copia de la base de datos con la réplica de base de datos que publica el servidor de base de datos del sitio.  

El servidor de réplica de base de datos debe cumplir los mismos requisitos que el servidor de base de datos del sitio. Sin embargo, el servidor de réplica de base de datos puede ejecutar una edición o versión diferente de SQL Server que la que utiliza el servidor de base de datos del sitio. Para más información sobre las versiones compatibles de SQL Server, vea el tema [Compatibilidad con versiones de SQL Server de Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!IMPORTANT]  
>  El servicio SQL Server en el equipo que hospeda la base de datos de réplica debe ejecutarse como la cuenta del sistema.  

Utilice el procedimiento siguiente como ejemplo de cómo configurar un servidor de réplica de base de datos en un equipo Windows Server 2008 R2. Si tiene otra versión de sistema operativo, consulte la documentación del sistema operativo correspondiente y adapte los pasos de este procedimiento, si fuera necesario.  

##### <a name="to-configure-the-database-replica-server"></a>Para configurar el servidor de réplica de base de datos  

1. En el servidor de réplica de base de datos, establezca el Agente SQL Server para que se inicie automáticamente.  

2. En el servidor de réplica de base de datos, utilice **SQL Server Management Studio** para conectarse al explorador local, vaya a la carpeta **Replicación** , haga clic en Suscripciones locales y seleccione **Nuevas suscripciones** para iniciar el **Asistente para nuevas suscripciones**:  

   1. En la página **Publicación** , en el cuadro de lista **Publicador** , seleccione **Buscar publicador de SQL Server**, escriba el nombre del servidor de base de datos del sitio y haga clic en **Conectar**.  

   2. Seleccione **ConfigMgr_MPReplica**y, a continuación, haga clic en **Siguiente**.  

   3. En la página **Ubicación del Agente de distribución** , seleccione **Ejecutar cada agente en su suscriptor (suscripciones de extracción)** y haga clic en **Siguiente**.  

   4. En la página **Suscriptores** realice una de las acciones siguientes:  

      -   Seleccione una base de datos existente desde el servidor de réplica de base de datos que se va a utilizar para la réplica de base de datos y, a continuación, haga clic en **Aceptar**.  

      -   Seleccione **Nueva base de datos** para crear una nueva base de datos para la réplica de base de datos. En la página **Nueva base de datos** , especifique un nombre de base de datos y, a continuación, haga clic en **Aceptar**.  

   5. Haga clic en **Siguiente** para continuar.  

   6. En la página **Seguridad del Agente de distribución**, haga clic en el botón de propiedades **(....)** en la fila Conexión de suscriptor del cuadro de diálogo y, después, configure las opciones de seguridad para la conexión.  

      > [!TIP]  
      >  El botón de propiedades **(....)** se encuentra en la cuarta columna del cuadro de visualización.  

      **Configuración de seguridad:**  

      - Configure la cuenta que se ejecuta el proceso del Agente de distribución (la cuenta de proceso):  

        -   Si el Agente SQL Server se ejecuta como sistema local, seleccione **Ejecutar en la cuenta de servicio del Agente SQL Server (no es un método de seguridad recomendado).**  

        -   Si el Agente SQL Server se ejecuta mediante una cuenta diferente, seleccione **Ejecutar en la siguiente cuenta de Windows**y después configure dicha cuenta. Puede especificar una cuenta de Windows o una cuenta de SQL Server.  

        > [!IMPORTANT]  
        >  Debe conceder permiso a la cuenta que ejecuta el Agente de distribución en el publicador como suscripción de extracción. Para obtener información acerca de la configuración de estos permisos, consulte [Seguridad del Agente de distribución](/sql/relational-databases/replication/distribution-agent-security).  

      - Para **Conectarse al distribuidor**, seleccione **Mediante la suplantación de la cuenta de proceso**.  

      - Para **Conectarse al suscriptor**, seleccione **Mediante la suplantación de la cuenta de proceso**.  

        Después de configurar las opciones de seguridad de conexión, haga clic en **Aceptar** para guardarlas y, a continuación, haga clic en **Siguiente**.  

   7. En la página **Programación de sincronización** , en el cuadro de lista **Programación del agente** , seleccione **Definir programación**y después configure la **Nueva programación de trabajo**. Establezca la frecuencia para que tenga lugar **Diariamente**, se repita cada **5 minuto(s)** y que la duración tenga el valor **Sin fecha de finalización**. Haga clic en **Siguiente** para guardar la programación y, a continuación, vuelva a hacer clic en **Siguiente** .  

   8. En la página **Acciones del asistente** , active la casilla para **crear las suscripciones**y haga clic en **Siguiente**.  

   9. En la página **Complete el asistente** , haga clic en **Finalizar**y, a continuación, haga clic en **Cerrar** para completar el asistente.  

3. Inmediatamente después de completar el Asistente para nueva suscripción, utilice **SQL Server Management Studio** para conectarse a la base de datos del servidor de réplica de bases de datos y ejecute la consulta siguiente para habilitar la propiedad de base de datos TRUSTWORTHY:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. Revise el estado de sincronización para validar que la suscripción es correcta:  

   -   En el equipo del suscriptor:  

       -   En **SQL Server Management Studio**, conéctese al servidor de réplica de base de datos y expanda **Replicación**.  

       -   Expanda **Suscripciones locales**, haga clic con el botón secundario en la suscripción a la publicación de la base de datos del sitio y, a continuación, seleccione **Ver estado de sincronización**.  

   -   En el equipo del publicador:  

       -   En **SQL Server Management Studio**, conéctese al equipo de base de datos del sitio, pulse con el botón secundario en la carpeta **Replicación** y seleccione **Iniciar Monitor de réplica**.  

5. Para habilitar la integración con Common Language Runtime (CLR) para la réplica de base de datos, use **SQL Server Management Studio** para conectarse a la réplica de base de datos en el servidor de réplica de base de datos y ejecute el siguiente procedimiento almacenado como una consulta: **exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE**  

6. Para cada punto de administración que utilice un servidor de réplica de base de datos, agregue la cuenta de equipo de puntos de administración al grupo de **administradores** locales en ese servidor de réplica de base de datos.  

   > [!TIP]  
   >  Este paso no es necesario para un punto de administración que se ejecuta en el servidor de réplica de base de datos.  

   La réplica de base de datos ya está preparada para que la utilice el punto de administración.  

###  <a name="step-3---configure-management-points-to-use-the-database-replica"></a><a name="BKMK_DBReplica_ConfigMP"></a> Paso 3: configurar los puntos de administración para usar la réplica de base de datos  
 Puede configurar un punto de administración en un sitio primario para que utilice una réplica de base de datos cuando instale el rol de punto de administración, o bien puede volver a configurar un punto de administración existente para que utilice una réplica de base de datos.  

 Utilice la siguiente información para configurar un punto de administración para que utilice una réplica de base de datos:  

-   **Para configurar un nuevo punto de administración:** en la página **Base de datos de punto de administración** del asistente que usa para instalar el punto de administración, seleccione **Use a database replica** (Usar una réplica de base de datos) y especifique el FQDN del equipo que hospeda la réplica de base de datos. A continuación, en **Nombre de base de datos de sitio de ConfigMgr**, especifique el nombre de base de datos de la réplica de base de datos en ese equipo.  

-   **Para configurar un punto de administración instalado anteriormente**: abra la página de propiedades del punto de administración, seleccione la pestaña **Base de datos de punto de administración**, seleccione **Use a database replica** (Usar una réplica de base de datos) y, después, especifique el FQDN del equipo que hospeda la réplica de base de datos. A continuación, en **Nombre de base de datos de sitio de ConfigMgr**, especifique el nombre de base de datos de la réplica de base de datos en ese equipo.  

-   **Para cada punto de administración que usa una réplica de base de datos**, debe agregar manualmente la cuenta de equipo del servidor de punto de administración al rol **db_datareader** de la réplica de base de datos.  

Además de configurar el punto de administración para que utilice el servidor de réplica de base de datos, debe habilitar **Autenticación de Windows** en **IIS** en el punto de administración:  

1.  Abra el **Administrador de Internet Information Services (IIS)** .  

2.  Seleccione el sitio web utilizado por el punto de administración y abra **Autenticación**.  

3.  Establezca **Autenticación de Windows** en **Habilitado**y, a continuación, cierre **Administración de Internet Information Services (IIS)** .  

###  <a name="step-4--configure-a-self-signed-certificate-for-the-database-replica-server"></a><a name="BKMK_DBReplica_Cert"></a> Paso 4: configurar un certificado autofirmado para el servidor de réplica de base de datos  
 Debe crear un certificado autofirmado en el servidor de réplica de base de datos y hacer que este certificado esté disponible para todos los puntos de administración que van a utilizar ese servidor de réplica de base de datos.  

 El certificado está automáticamente disponible para un punto de administración que está instalado en el servidor de réplica de base de datos. Sin embargo, para que este certificado esté disponible para los puntos de administración remotos, debe exportar el certificado y agregarlo al almacén de certificados Personas de confianza en el punto de administración remoto.  

 Utilice los procedimientos siguientes como ejemplo cómo configurar el certificado autofirmado en el servidor de réplica de base de datos para un equipo de Windows Server 2008 R2. Si tiene otra versión de sistema operativo, consulte la documentación del sistema operativo correspondiente y adapte los pasos de estos procedimientos, si fuera necesario.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>Para configurar un certificado autofirmado para el servidor de réplica de base de datos  

1.  En el servidor de réplica de base de datos, abra un símbolo del sistema de PowerShell con privilegios administrativos y, a continuación, ejecute el comando siguiente: **set-executionpolicy UnRestricted**  

2.  Copie el siguiente script de PowerShell y guárdelo como un archivo con el nombre **CreateMPReplicaCert.ps1**. Coloque una copia de este archivo en la carpeta raíz de la partición del sistema del servidor de réplica de base de datos.  

    > [!IMPORTANT]  
    >  Si va a configurar más de una réplica de base de datos en un único servidor SQL Server, para cada réplica posterior que configure, deberá usar una versión modificada de este script para realizar este procedimiento. Vea  [Script adicional para las réplicas de bases de datos adicionales en un único servidor de SQL](#bkmk_supscript).  

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  En el servidor de réplica de base de datos, ejecute el comando siguiente que se aplica a la configuración del SQL Server:  

    -   Para una instancia predeterminada de SQL Server: haga clic con el botón derecho en el archivo **CreateMPReplicaCert.ps1** y seleccione **Ejecutar con PowerShell**. Cuando se ejecuta el script, crea el certificado autofirmado y configura SQL Server para que utilice el certificado.  

    -   Para una instancia con nombre de SQL Server: Use PowerShell para ejecutar el comando **%path%\CreateMPReplicaCert.ps1 xxxxxx**, donde **xxxxxx** es el nombre de la instancia de SQL Server.  

    -   Tras completarse el script, compruebe que se está ejecutando el Agente SQL Server. Si no es así, reinicie el Agente SQL Server.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>Para configurar puntos de administración remotos a fin de utilizar el certificado autofirmado del servidor de réplica de base de datos  

1.  Siga los pasos descritos más adelante en el servidor de réplica de base de datos para exportar el certificado autofirmado del servidor:  

    1.  Haga clic en **Inicio**y en **Ejecutar**, y escriba **mmc.exe**. En la consola vacía, haga clic en **Archivo**y, a continuación, haga clic en **Agregar o quitar complemento**.  

    2.  En el cuadro de diálogo **Agregar o quitar complementos** , seleccione **Certificados** en la lista de **Complementos disponibles**y, a continuación, haga clic en **Agregar**.  

    3.  En el cuadro de diálogo **Complemento Certificado** , seleccione **Cuenta de equipo**y, a continuación, haga clic en **Siguiente**.  

    4.  En el cuadro de diálogo **Seleccionar equipo** , asegúrese de que está seleccionado **Equipo local: (el equipo en el que se está ejecutando esta consola)** y, a continuación, haga clic en **Finalizar**.  

    5.  En el cuadro de diálogo **Agregar o quitar complementos** , haga clic en **Aceptar**.  

    6.  En la consola, expanda **Certificados (equipo local)** , expanda **Personal**y, a continuación, seleccione **Certificados**.  

    7.  Haga clic con el botón secundario en el certificado con el nombre descriptivo **ConfigMgr SQL Server Identification Certificate**, haga clic en **Todas las tareas**y, a continuación, seleccione **Exportar**.  

    8.  Complete el **Asistente para exportación de certificados** con las opciones predeterminadas y guarde el certificado con la extensión de nombre de archivo **.cer** .  

2.  Realice los pasos siguientes en el equipo de punto de administración para agregar el certificado autofirmado para el servidor de réplica de base de datos al almacén de certificados de Personas de confianza en el punto de administración:  

    1.  Repita que los pasos anteriores del 1.a al 1.e para configurar el MMC del complemento **Certificado** en el equipo de punto de administración.  

    2.  En la consola, expanda **Certificados (equipo local)** , expanda **Personas de confianza**, haga clic con el botón secundario en **Certificados**, seleccione **Todas las tareas**y, a continuación, seleccione **Importar** para iniciar el **Asistente para importación de certificados**.  

    3.  En la página **Archivo para importar** , seleccione el certificado que guardó en el paso 1.h y, a continuación, haga clic en **Siguiente**.  

    4.  En la página **Almacén de certificados** , seleccione **Colocar todos los certificados en el siguiente almacén**, con el **Almacén de certificados** establecido en **Personas de confianza**y, a continuación, haga clic en **Siguiente**.  

    5.  Haga clic en **Finalizar** para cerrar el asistente y completar la configuración de certificado en el punto de administración.  

###  <a name="step-5---configure-the-sql-server-service-broker-for-the-database-replica-server"></a><a name="BKMK_DBreplica_SSB"></a> Paso 5: configurar SQL Server Service Broker para el servidor de réplica de base de datos  
Para admitir la notificación de cliente con una réplica de base de datos para un punto de administración, debe configurar la comunicación entre el servidor de base de datos de sitio y el servidor de réplica de base de datos para SQL Server Service Broker. Esto requiere configurar cada base de datos con información acerca de la otra base de datos, así como intercambiar certificados entre las dos bases de datos para una comunicación segura.  

> [!NOTE]  
>  Para poder utilizar el procedimiento siguiente, el servidor de réplica de base de datos debe completar correctamente la sincronización inicial con el servidor de base de datos de sitio.  

 El siguiente procedimiento no modifica el puerto de Service Broker configurado en SQL Server para el servidor de base de datos de sitio o el servidor de réplica de base de datos. En su lugar, con este procedimiento se configura cada base de datos para comunicarse con la otra base de datos a través del puerto correcto de Service Broker.  

 Utilice el siguiente procedimiento para configurar Service Broker para el servidor de base de datos de sitio y el servidor de réplica de base de datos.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>Para configurar Service Broker para una réplica de base de datos  

1. Use **SQL Server Management Studio** para conectarse con la base de datos del servidor de réplica de base de datos y, después, ejecute la siguiente consulta para habilitar Service Broker en el servidor de réplica de base de datos: **ALTER DATABASE &lt;nombre de base de datos de réplica\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2. A continuación, en el servidor de réplica de base de datos, configure Service Broker para la notificación de cliente y exporte el certificado de Service Broker. Para ello, ejecute un procedimiento almacenado de SQL Server con el que se configure Service Broker y con el que también se exporte el certificado como una única acción. Al ejecutar el procedimiento almacenado, debe especificar el FQDN del servidor de réplica de base de datos, el nombre de la base de datos de réplicas de base de datos y, a continuación, especifique una ubicación para exportar el archivo de certificado.  

    Ejecute la consulta siguiente para configurar los detalles necesarios en el servidor de réplica de base de datos y para exportar el certificado para el servidor de réplica de base de datos: **EXEC sp_BgbConfigSSBForReplicaDB '&lt;FQDN de SQL Server de réplica\>', '&lt;nombre de base de datos de réplica\>', '&lt;ruta de archivo de copia de seguridad de certificado\>'**  

   > [!NOTE]  
   >  Cuando el servidor de réplica de base de datos no está en la instancia predeterminada de SQL Server, en este paso debe especificar el nombre de instancia junto con el nombre de la base de datos de réplica. Para ello, reemplace **&lt;nombre de base de datos de réplica\>** por **&lt;nombre de instancia\\nombre de base de datos de réplica\>** .  

    Después de exportar el certificado del servidor de réplica de base de datos, coloque una copia del certificado en el servidor de base de datos de sitios primarios.  

3. Utilice **SQL Server Management Studio** para conectarse a la base de datos de sitio primario. Después de conectarse a la base de datos de sitios primarios, ejecute una consulta para importar el certificado y especifique el puerto de Service Broker que se utiliza en el servidor de réplica de base de datos, el FQDN del servidor de réplica de base de datos y el nombre de la base de datos de réplicas de base de datos. De esta forma, se configura la base de datos de sitios primarios a fin de utilizar Service Broker para comunicarse con la base de datos del servidor de réplica de base de datos.  

    Ejecute la siguiente consulta para importar el certificado del servidor de réplica de base de datos y especifique los detalles necesarios: **EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '&lt;puerto de SQL Service Broker\>', '&lt;ruta de archivos de certificado\>', '&lt;FQDN de SQL Server de réplica\>', '&lt;nombre de base de datos de réplica\>'**  

   > [!NOTE]  
   >  Cuando el servidor de réplica de base de datos no está en la instancia predeterminada de SQL Server, en este paso debe especificar el nombre de instancia junto con el nombre de la base de datos de réplica. Para ello, reemplace **&lt;nombre de base de datos de réplica\>** por **\nombre de instancia\\nombre de base de datos de réplica\>** .  

4. A continuación, en el servidor de base de datos de sitio, ejecute el comando siguiente para exportar el certificado para el servidor de base de datos del sitio: **EXEC sp_BgbCreateAndBackupSQLCert '&lt;ruta de archivo de copia de seguridad de certificado\>'**  

    Después de exportar el certificado del servidor de base de datos de sitio, coloque una copia del certificado en el servidor de réplica de base de datos.  

5. Utilice **SQL Server Management Studio** para conectarse a la base de datos del servidor de réplica de base de datos. Después de conectarse a la base de datos del servidor de réplica de base de datos, ejecute una consulta para importar el certificado y especifique el código de sitio del sitio primario y el puerto de Service Broker que se utiliza en el servidor de base de datos de sitio. De esta forma, se configura el servidor de réplica de base de datos a fin de utilizar Service Broker para comunicarse con la base de datos del sitio primario.  

    Ejecute la siguiente consulta para importar el certificado del servidor de base de datos del sitio: **EXEC sp_BgbConfigSSBForRemoteService '&lt;código de sitio\>', '&lt;puerto de SQL Service Broker\>', '&lt;ruta de archivo de certificado\>'**  

   Unos minutos después de completar la configuración de la base de datos de sitio y de la base de datos de réplica de base de datos, el administrador de notificaciones del sitio primario configura la conversación de Service Broker para la notificación de cliente desde la base de datos de sitio primario a la réplica de base de datos.  

###  <a name="supplemental-script-for-additional-database-replicas-on-a-single-sql-server"></a><a name="bkmk_supscript"></a> Script adicional para las réplicas de bases de datos adicionales en un único servidor de SQL  
 Si usa el script del paso 4 para configurar un certificado autofirmado para el servidor de réplica de base de datos en un servidor SQL Server que ya tiene una réplica de base de datos que va a continuar usando, debe usar una versión modificada del script original. Las siguientes modificaciones evitan que el script elimine un certificado existente en el servidor y crean posteriores certificados con nombres descriptivos únicos.  Edite el script original como sigue:  

-   Convierta en comentario (evitar que se ejecute) cada línea entre las entradas del script **# Eliminar certificado existente si existe uno** y **# Crear el nuevo certificado**. Para ello, agregue un  **#**  como primer carácter de cada línea aplicable.  

-   En cada réplica de base de datos posterior, use este script para configurar y actualizar el nombre descriptivo del certificado.  Para ello, modifique la línea **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** y sustituya **ConfigMgr SQL Server Identification Certificate** por un nuevo nombre, como por ejemplo,  **ConfigMgr SQL Server Identification Certificate1**.  

##  <a name="manage-database-replica-configurations"></a><a name="BKMK_DBReplicaOps"></a> Administrar configuraciones de réplica de base de datos  
 Al utilizar una réplica de base de datos en un sitio, use la información de las siguientes secciones para complementar el proceso para desinstalar una réplica de base de datos, desinstalar un sitio que utiliza una réplica de base de datos o mover la base de datos de sitio a una instalación nueva de SQL Server. Si utiliza la información de las siguientes secciones para eliminar publicaciones, utilice la guía para eliminar la replicación transaccional de la versión SQL Server utilizada para la réplica de base de datos. Para obtener más información, vea [Eliminar una publicación](/sql/relational-databases/replication/publish/delete-a-publication).  

> [!NOTE]  
>  Después de restaurar una base de datos de sitio configurada para réplicas de base de datos, para poder utilizar las réplicas de base de datos debe volver a configurar cada réplica de base de datos y volver a crear tanto las publicaciones como las suscripciones.  

###  <a name="uninstall-a-database-replica"></a><a name="BKMK_UninstallDbReplica"></a> Desinstalación de una réplica de base de datos  
 Al utilizar una réplica de base de datos para un punto de administración, debe desinstalar la réplica de base de datos durante un período de tiempo y, a continuación, volver a configurarla para utilizarla. Por ejemplo, debe quitar las réplicas de base de datos antes de actualizar un sitio de Configuration Manager a un nuevo Service Pack. Una vez completada la actualización del sitio, puede restaurar la réplica de base de datos para poder utilizarla.  

 Utilice los pasos siguientes para desinstalar una réplica de base de datos.  

1.  En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Configuración del sitio**, seleccione **Servidores y roles del sistema de sitios** y, después, en el panel de detalles, seleccione el servidor de sistema de sitio que hospeda el punto de administración que usa la réplica de base de datos que va a desinstalar.  

2.  En el panel **Roles del sistema de sitio** , haga clic con el botón secundario en **Punto de administración** y seleccione **Propiedades**.  

3.  En la pestaña **Base de datos de punto de administración** , seleccione **Usar la base de datos de sitio** para configurar el punto de administración a fin de utilizar la base de datos de sitio en lugar de la réplica de base de datos. A continuación, haga clic en **Aceptar** para guardar la configuración.  

4.  Utilice **SQL Server Management Studio** para realizar las siguientes tareas:  

    -   Eliminar la publicación para la réplica de base de datos de la base de datos del servidor de sitio.  

    -   Eliminar la subscripción para la réplica de base de datos del servidor de réplica de base de datos.  

    -   Eliminar la base de datos de réplica del servidor de réplica de base de datos.  

    -   Deshabilitar la publicación y distribución en el servidor de base de datos de sitio. Para deshabilitar la publicación y distribución, haga clic con el botón secundario en la carpeta de replicación y, a continuación, haga clic en **Deshabilitar la publicación y distribución**.  

5.  Después de eliminar la publicación, la suscripción, la base de datos de réplica, y tras deshabilitar la publicación en el servidor de base de datos de sitio, se desinstala la réplica de base de datos.  

###  <a name="uninstall-a-site-server-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Uninstall"></a> Desinstalar un servidor de sitio que publica una réplica de base de datos  
 Antes de desinstalar un sitio que publica una réplica de base de datos, siga estos pasos para limpiar la publicación y las suscripciones.  

1.  Utilice **SQL Server Management Studio** para eliminar la publicación de réplica de base de datos de la base de datos del servidor de sitio.  

2.  Utilice **SQL Server Management Studio** para eliminar la suscripción de réplica de base de datos de cada SQL Server remoto que hospeda una réplica de base de datos para este sitio.  

3.  Desinstale el sitio.  

###  <a name="move-a-site-server-database-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Move"></a> Mover una base de datos de servidor de sitio que publica una réplica de base de datos  
 Cuando se mueve la base de datos de sitio a un nuevo equipo, siga estos pasos:  

1.  Utilice **SQL Server Management Studio** para eliminar la publicación de réplica de base de datos de la base de datos del servidor de sitio.  

2.  Utilice **SQL Server Management Studio** para eliminar la suscripción para la réplica de base de datos de cada servidor de réplica de base de datos e este sitio.  

3.  Mueva la base de datos al nuevo equipo de SQL Server. Para más información, vea la sección [Modificar la configuración de la base de datos del sitio](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) del tema [Modificar la infraestructura de Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

4.  Vuelva a crear la publicación para la réplica de base de datos en el servidor de base de datos de sitio. Para obtener más información, consulte [Paso 1: configurar el servidor de base de datos del sitio para publicar la réplica de base de datos](#BKMK_DBReplica_ConfigSiteDB) en este tema.  

5.  Vuelva a crear las suscripciones para la réplica de base de datos en cada servidor de réplica de base de datos. Para obtener más información, consulte [Paso 2: configurar el servidor de réplica de bases de datos](#BKMK_DBReplica_ConfigSrv) en este tema.