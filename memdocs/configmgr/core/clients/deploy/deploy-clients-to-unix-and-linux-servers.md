---
title: Implementación de clientes UNIX o Linux
titleSuffix: Configuration Manager
description: Aprenda a implementar un cliente en un servidor UNIX o Linux en Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9e8e40a6bdfa129a03e6042985e4956ffb21b5c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906316"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Implementación de clientes en servidores UNIX y Linux en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> A partir de la versión 1902, Configuration Manager no admite clientes Linux o UNIX. 
> 
> Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.


Para poder administrar un servidor Linux o UNIX con Configuration Manager, debe instalar el cliente de Configuration Manager para Linux y UNIX en cada servidor Linux o UNIX. Puede realizar la instalación del cliente manualmente en cada equipo o usar un script de shell que instale el cliente de forma remota. Configuration Manager no admite el uso de la instalación de inserción de cliente en servidores Linux o UNIX. Opcionalmente puede configurar un Runbook de System Center Orchestrator para automatizar la instalación del cliente en el servidor Linux o UNIX.  

 Independientemente del método de instalación que use, el proceso de instalación requiere el uso de un script denominado **install** para administrar el proceso de instalación. Esta secuencia de comandos se incluye al descargar el cliente para Linux y UNIX.  

 El script de instalación del cliente de Configuration Manager para Linux y UNIX admite propiedades de línea de comandos. Algunas propiedades de línea de comandos son necesarias, mientras que otras son opcionales. Por ejemplo, cuando se instala el cliente, debe especificar un punto de administración del sitio que usa el servidor Linux o UNIX para su contacto inicial con el sitio. Para obtener una lista completa de propiedades de línea de comandos, consulte [Propiedades de línea de comandos para la instalación del cliente en servidores Linux y UNIX](#BKMK_CmdLineInstallLnUClient).  

 Después de instalar el cliente, se especifican las opciones de cliente en la consola de Configuration Manager para configurar el agente cliente de la misma manera que lo haría con clientes basados en Windows. Para obtener más información, consulte [Client settings for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU) (Configuración de cliente para servidores Linux y UNIX).  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a> Acerca de los paquetes de instalación de cliente y el agente universal  
 Para instalar el cliente para Linux y UNIX en una plataforma concreta, debe usar el paquete de instalación de cliente aplicable para el equipo donde se instala el cliente. Los paquetes de instalación de cliente aplicables se incluyen como parte de la descarga de cada cliente desde el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). Además de los paquetes de instalación de cliente, la descarga de cliente incluye el script de **install** que administra la instalación del cliente en cada equipo.  

 Cuando instala un cliente, puede utilizar las mismas propiedades de proceso y línea de comandos sin importar el paquete de instalación de cliente que utilice.  

 Para obtener información sobre los sistemas operativos, las plataformas y los paquetes de instalación de cliente que son compatibles con cada versión del cliente de Configuration Manager para Linux y UNIX, consulte [Linux and UNIX servers](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers) (Servidores Linux y UNIX).  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a> Instalación del cliente en servidores Linux y UNIX  
 Para instalar al cliente para Linux y UNIX, ejecutar un script en cada equipo Linux o UNIX. El script se llama **install** y admite propiedades de línea de comandos que modifican el comportamiento de instalación y hacen referencia al paquete de instalación de cliente. El paquete de instalación de cliente y la secuencia de comandos de instalación debe encontrarse en el cliente. El paquete de instalación de cliente contiene los archivos de cliente de Configuration Manager para una plataforma y sistema operativo Linux o UNIX específicos.
Cada paquete de instalación de cliente contiene todos los archivos necesarios para completar la instalación del cliente y, a diferencia de los equipos basados en Windows, descarga los archivos adicionales desde un punto de administración u otra ubicación de origen.  

 Después de instalar el cliente de Configuration Manager para Linux y UNIX, no es necesario reiniciar el equipo. Tan pronto como se complete la instalación del software, el cliente está operativo. Si reinicia el equipo, el cliente de Configuration Manager se reinicia automáticamente.  

 El cliente instalado se ejecuta con credenciales raíz. Las credenciales raíz son necesarias para recopilar el inventario de hardware y realizar las implementaciones de software.  

 Use el formato de comando siguiente:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install` es el nombre del archivo de script que instala el cliente para Linux y UNIX. Este archivo se proporciona con el software cliente.  

-   `-mp <computer>` especifica el punto de administración inicial que usa el cliente. Ejemplo: `smsmp.contoso.com`  

-   `-sitecode <site code>` especifica el código de sitio al que se asigna el cliente. Ejemplo: `S01`  

-   `<property #1> <property #2>` especifica las propiedades de línea de comandos que se deben usar con el script de instalación.  

    > [!NOTE]  
    >  Para más información, consulte [Propiedades de línea de comandos para la instalación del cliente en servidores Linux y UNIX](#BKMK_CmdLineInstallLnUClient).  

-   **paquete de instalación de cliente** es el nombre del paquete .tar de instalación de cliente para este sistema operativo, versión y arquitectura de CPU del equipo. El archivo .tar de instalación de cliente debe especificarse en último lugar. Ejemplo: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a> Instalación del cliente de Configuration Manager en servidores Linux y UNIX  

1.  En un equipo Windows, [descargue el archivo de cliente apropiado para el servidor Linux o UNIX](https://www.microsoft.com/download/details.aspx?id=47719) que quiere administrar.  

2.  Ejecute el archivo autoextraíble .exe en el equipo Windows para extraer el script de instalación y el archivo .tar de instalación de cliente.  

3.  Copie el script **install** y el archivo .tar a una carpeta en el servidor que quiere administrar.  

4.  En el servidor UNIX o Linux, ejecute el siguiente comando para permitir que el script se ejecute como un programa: `chmod +x install`  

    > [!IMPORTANT]  
    >  Debe utilizar credenciales raíz para instalar al cliente.  

5.  A continuación, ejecute el siguiente comando para instalar el cliente de Configuration Manager: `./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Cuando escriba este comando, utilice las propiedades de línea de comandos adicionales que necesite. Para obtener la lista de propiedades de línea de comandos, consulte [Propiedades de línea de comandos para la instalación del cliente en servidores Linux y UNIX](#BKMK_CmdLineInstallLnUClient).  

6.  Después de ejecutar el script, valide la instalación revisando el archivo **/var/opt/microsoft/scxcm.log** . Además, puede confirmar que el cliente está instalado y se comunica con el sitio. Para ello, consulte los detalles del cliente en el nodo **Dispositivos** del área de trabajo **Activos y compatibilidad** en la consola de Configuration Manager.  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a> Propiedades de línea de comandos para la instalación del cliente en servidores Linux y UNIX  
 Las propiedades siguientes están disponibles para modificar el comportamiento del script de instalación:  

> [!NOTE]  
>  Utilice la propiedad `-h` para mostrar la lista de propiedades admitidas.  

-   `-mp <server FQDN>`  

     Necesario. Especifica mediante el FQDN el servidor de punto de administración que utilizará el cliente como punto inicial de contacto.  

    > [!IMPORTANT]  
    >  Esta propiedad no especifica el punto de administración al que se asignará el cliente después de la instalación.  

    > [!NOTE]  
    >  Cuando usa la propiedad `-mp` para especificar un punto de administración que está configurado para aceptar solo conexiones de cliente HTTPS, también debe usar la propiedad `-UsePKICert`.  

-   `-sitecode <sitecode>`  

     Necesario. Especifica el sitio primario de Configuration Manager al que se va a asignar el cliente de Configuration Manager. Ejemplo: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Opcional. Especifica el FQDN, el servidor de punto de estado de reserva que utiliza el cliente para enviar mensajes de estado. Para más información, consulte [Determinar si necesita un punto de estado de reserva](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

-   `-dir <directory>`  

     Opcional. Especifica una ubicación alternativa para instalar los archivos de cliente de Configuration Manager. De forma predeterminada, el cliente se instala en la siguiente ubicación: `/opt/microsoft`.  

-   `-nostart`  

     Opcional. Impide el inicio automático del servicio de cliente de Configuration Manager, **ccmexec.bin**, una vez completada la instalación del cliente.  

     Cuando haya instalado el cliente, debe iniciar manualmente el servicio del cliente.  

     De forma predeterminada, el servicio de cliente se inicia después de completarse la instalación del cliente y cada vez que se reinicia el equipo.  

-   `-clean`  

     Opcional. Especifica la eliminación de todos los archivos de cliente y los datos de un cliente instalado previamente para Linux y UNIX, antes de empezar la instalación nueva. Esta acción quita la base de datos y el almacén de certificados del cliente.  

-   `-keepdb`  

     Opcional. Especifica que la base de datos de cliente local se conserva y se vuelve a usar cuando se vuelve a instalar un cliente. De forma predeterminada, cuando vuelve a instalar un cliente se elimina esta base de datos.  

-   `-UsePKICert <parameter>`  

     Opcional. Especifica el nombre completo de ruta de acceso y a un certificado de PKI X.509 en el formato Public Key Certificate Standard (PKCS #12). Este certificado se utiliza para la autenticación de cliente. Si no se especifica un certificado durante la instalación y necesita agregar o cambiar un certificado, use la utilidad **certutil** . Para más información, consulte [Cómo administrar clientes de Linux y UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Cuando use `-UsePKICert`, también debe proporcionar la contraseña asociada con el archivo PKCS #12 mediante el uso del parámetro de línea de comandos `-certpw`.  

     Si no usa esta propiedad para especificar un certificado PKI, el cliente utiliza un certificado autofirmado y todas las comunicaciones con los sistemas del sitio se realizan a través de HTTP.  

     Si especifica un certificado no válido en el cliente instale la línea de comandos, no se devuelven errores. La validación de certificados se produce después de instalar el cliente. Cuando se inicia el cliente, los certificados se validan con el punto de administración. Si un certificado no pasa la validación, aparece el siguiente mensaje en **scxcm.log**: **No se puede validar el certificado de punto de administración**. La ubicación del archivo de registro predeterminado es:  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > Debe especificar esta propiedad cuando instale un cliente y usar la propiedad `-mp` para especificar un punto de administración que está configurado para aceptar únicamente conexiones de cliente HTTPS.  

     Ejemplo: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Opcional. Especifica la contraseña asociada con el archivo PKCS #12 que especificó mediante el uso de la propiedad `-UsePKICert`.  

     Ejemplo: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Opcional. Especifica que un cliente no debe comprobar la lista de revocación de certificados (CRL) cuando se comunica a través de HTTPS mediante el uso de un certificado PKI. Cuando no se especifica esta opción, el cliente comprueba la CRL antes de establecer una conexión HTTPS mediante el uso de certificados PKI. Para obtener más información acerca de la comprobación de CRL de cliente, consulte Diseño de revocación de certificados PKI.  

     Ejemplo: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Opcional. Especifica el nombre de archivo y la ruta de acceso completa de la clave raíz confiable de Configuration Manager. La clave raíz confiable de Configuration Manager proporciona un mecanismo que los clientes Linux y UNIX usan para comprobar que están conectados a un sistema de sitio que pertenece a la jerarquía correcta.  

     Si no especifica la clave raíz confiable en la línea de comandos, el cliente confiará en el primer punto de administración con el que se comunique y recuperará automáticamente la clave raíz confiable del punto de administración.  

     Para obtener más información, consulte [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) (Planeación de la clave raíz confiable).  

     Ejemplo: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Opcional. Especifica el puerto que está configurado en los puntos de administración que utiliza el cliente cuando se comunican a puntos de administración a través de HTTP. Si el puerto no se especifica, se utiliza el valor predeterminado de 80.  

     Ejemplo: `-httpport 80`  

-   `-httpsport <port>`  

     Opcional. Especifica el puerto que está configurado en los puntos de administración que utiliza el cliente al comunicarse con los puntos de administración a través de HTTPS. Si el puerto no se especifica, se utiliza el valor predeterminado de 443.  

     Ejemplo: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Opcional. Especifica que la instalación de cliente omite la validación de SHA-256. Use esta opción al instalar el cliente en sistemas operativos que no se publicaron con una versión de OpenSSL que admite SHA-256. Para más información, consulte [acerca de los sistemas operativos Linux y UNIX que no admiten SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Opcional. Especifica la ruta de acceso completa y **.cer** nombre de archivo del certificado autofirmado exportado en el servidor de sitio. Si no hay certificados PKI disponibles, el servidor de sitio de Configuration Manager genera automáticamente los certificados autofirmados.  

     Estos certificados se utilizan para validar que las directivas de cliente descargadas desde el punto de administración se enviaron desde el sitio deseado. Si no se especifica un certificado autofirmado durante la instalación o necesita cambiar el certificado, use la utilidad **certutil** . Para más información, consulte [Cómo administrar clientes de Linux y UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Este certificado se puede recuperar a través del almacén de certificados **SMS** ; el nombre del firmante es **Servidor de sitio** y su nombre descriptivo es **Certificado de firma de servidor de sitio**.  

     Si no se especifica esta opción durante la instalación, los clientes Linux y UNIX confían en el primer punto de administración con el que se comunican. Estos clientes recuperan automáticamente el certificado de firma de ese punto de administración.  

     Ejemplo: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Opcional. Especifica otros certificados PKI para importar que no forman parte de una jerarquía de entidad emisora (CA) de certificados de puntos de administración. Si especifica varios certificados en la línea de comandos, deben ser delimitada por comas.  

     Utilice esta opción si utiliza certificados de cliente PKI que no están vinculados a un certificado de CA raíz que sea de confianza para los puntos de administración de sitios. Los puntos de administración rechazarán el cliente si el certificado de cliente no está vinculado a un certificado raíz confiable en la lista de emisores de certificados del sitio.  

     Si no usa esta opción, el cliente Linux y UNIX comprobará la jerarquía de confianza usando solo el certificado de la opción `-UsePKICert`.  

     Ejemplo: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a> Desinstalación del cliente de servidores Linux y Unix  
 Para desinstalar el cliente de Configuration Manager para Linux y UNIX, use la utilidad de desinstalación **uninstall**. De forma predeterminada, este archivo se encuentra en la **/opt/microsoft, Configuration Manager/bin/** carpeta en el equipo cliente. Este comando de desinstalación no admite los parámetros de línea de comandos y se quitarán del servidor todos los archivos relacionados con el software de cliente.  

 Para desinstalar el cliente, utilice la siguiente línea de comandos: **/opt/microsoft/configmgr/bin/uninstall**  

 No es necesario reiniciar el equipo después de desinstalar el cliente de Configuration Manager para Linux y UNIX.  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a> Configurar puertos de solicitud para el cliente para Linux y UNIX  
 De forma similar a los clientes basados en Windows, el cliente de Configuration Manager para Linux y UNIX usa HTTP y HTTPS para comunicarse con sistemas de sitio de Configuration Manager. Los puertos que el cliente de Configuration Manager usa para comunicarse se conocen como puertos de solicitud.  

 Al instalar el cliente de Configuration Manager para Linux y UNIX, puede cambiar los puertos de solicitud de clientes predeterminados. Para ello, especifique las propiedades de instalación **-httpport** y **-httpsport**. Cuando no se especifica la propiedad de instalación y un valor personalizado, el cliente utiliza los valores predeterminados. Los valores predeterminados son **80** para el tráfico HTTP y **443** para el tráfico HTTPS.  

 Después de instalar al cliente, no se puede cambiar su configuración de puerto de la solicitud. En su lugar, para cambiar la configuración del puerto debe volver a instalar al cliente y especificar la configuración del puerto nuevo. Cuando reinstale el cliente para cambiar los números de puerto de solicitud, ejecute el comando **install** similar a la nueva instalación de cliente, pero utilice la propiedad de línea de comandos adicional de **- keepdb**. Este modificador indica a la instalación que conserve la base de datos y los archivos de cliente, lo que incluye el GUID y el almacén de certificados de los clientes.  

 Para más información sobre los números de puerto de comunicación de cliente, vea [Configurar puertos de comunicación de cliente en Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a> Configurar al cliente para Linux y UNIX buscar puntos de administración  
 Al instalar el cliente de Configuration Manager para Linux y UNIX, debe especificar un punto de administración para usarlo como punto de contacto inicial.  

 El cliente de Configuration Manager para Linux y UNIX se pone en contacto con este punto de administración en el momento de la instalación del cliente. Si el cliente no puede ponerse en contacto con el punto de administración, el software cliente continúa intentándolo hasta que lo logra.  

 Para obtener más información sobre cómo los clientes buscan puntos de administración, consulte [Búsqueda de puntos de administración](assign-clients-to-a-site.md#locating-management-points) (Búsqueda de puntos de administración).
