---
title: Implementar clientes en Windows
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar el cliente de Configuration Manager en equipos Windows.
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07c5488b0ea28f37f7f8a07b532c67fb64aad810
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694013"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Cómo implementar clientes en equipos Windows con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo proporciona información sobre cómo implementar el cliente de Configuration Manager en equipos Windows. Para más información sobre el planeamiento y la preparación de la implementación de cliente, consulte los artículos siguientes:

- [Métodos de instalación de cliente](plan/client-installation-methods.md)  
- [Requisitos previos para la implementación de clientes en equipos Windows](prerequisites-for-deploying-clients-to-windows-computers.md)
- [Seguridad y privacidad para los clientes de Configuration Manager](plan/security-and-privacy-for-clients.md)  
- [Procedimientos recomendados para la implementación de clientes](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a> Instalación de inserción de cliente

Hay tres maneras principales de utilizar la inserción de cliente:  

- Cuando configura la instalación de inserción de cliente para un sitio, la instalación del cliente se ejecuta automáticamente en los equipos que detecta el sitio. Este método se limita a los límites configurados del sitio cuando estos se configuran como un grupo de límites.  

- Inicie una instalación de inserción de cliente mediante la ejecución del Asistente para instalación de inserción de cliente para una recopilación o recurso específico dentro de una recopilación.  

- Use el Asistente para instalación de inserción de cliente para instalar el cliente de Configuration Manager, que puede usar para [consultar](../../servers/manage/introduction-to-queries.md) el resultado. La instalación se realizará correctamente solo si uno de los elementos devueltos por la consulta es el atributo **ResourceID** de la clase **Recurso del sistema**.

Si el servidor de sitio no se puede poner en contacto con el equipo cliente ni iniciar el proceso de instalación, reintenta automáticamente la instalación cada hora. El servidor continúa intentándolo hasta un máximo de siete días.  

Para realizar el seguimiento del proceso de instalación de cliente, instale un punto de estado de reserva antes de instalar los clientes. Cuando instala un punto de estado de reserva, se asigna automáticamente a los clientes cuando se instalan por el método de instalación de inserción de cliente. Para realizar el seguimiento del progreso de la instalación de cliente, vea los informes de implementación y asignación de cliente.

Los archivos de registro de cliente proporcionan información más detallada sobre la solución de problemas. Los archivos de registro no requieren un punto de estado de reserva. Por ejemplo, el archivo CCM.log en el servidor de sitio registra todos los problemas que se producen cuando el servidor de sitio se conecta al equipo. El archivo CCMSetup.log en el cliente registra el proceso de instalación.  

> [!IMPORTANT]  
> La inserción del cliente se realizará correctamente solo si se cumplen todos los requisitos previos. Para obtener más información, vea [Dependencias de los métodos de instalación](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies).

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurar el sitio para que use automáticamente la inserción de cliente para los equipos detectados

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Seleccione el sitio para el que va a configurar la instalación de inserción de cliente automática en todo el sitio.  

3. En la pestaña **Inicio** de la cinta, en el grupo **Configuración**, seleccione **Configuración de instalación de cliente** y, luego, **Instalación de inserción de cliente**.  

4. En la pestaña **General** de la ventana Propiedades de instalación de inserción de cliente, seleccione **Habilitar instalación de inserción de cliente automática en todo el sitio**.

5. A partir de la versión 1806, cuando actualice el sitio, se habilita una comprobación de Kerberos de la inserción de clientes. La opción **Permitir retroceso de conexión a NTLM** está habilitada de forma predeterminada, lo cual es coherente con el comportamiento anterior. Si el sitio no puede autenticar al cliente mediante Kerberos, vuelve a intentar la conexión mediante NTLM. La configuración recomendada para mejorar la seguridad consiste en deshabilitar esta configuración, lo que requiere Kerberos sin la reserva de NTLM.<!--1358204-->  

    > [!NOTE]  
    > Cuando se usa la inserción de cliente para instalar el cliente de Configuration Manager, el servidor de sitio crea una conexión remota al cliente. A partir de la versión 1806, el sitio puede requerir la autenticación mutua de Kerberos al no permitir el retroceso a NTLM antes de establecer la conexión. Esta mejora ayuda a proteger la comunicación entre el servidor y el cliente.  
    >
    > En función de las directivas de seguridad, puede que el entorno ya prefiera o requiera Kerberos en lugar de la autenticación NTLM anterior. Para más información sobre las consideraciones de seguridad de estos protocolos de autenticación, lea sobre la [configuración de la directiva de seguridad de Windows para restringir NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    >
    > Para usar esta característica, los clientes deben estar en un bosque de Active Directory de confianza. Kerberos en Windows se basa en Active Directory para la autenticación mutua.  

6. Seleccione los tipos de sistema en los que Configuration Manager debe insertar el software cliente. Seleccione si quiere instalar el cliente en controladores de dominio.  

7. En la pestaña **Cuentas**, especifique una o varias cuentas de Configuration Manager para conectarse al equipo de destino. Seleccione el icono **Crear**, escriba los valores de **Nombre de usuario** y **Contraseña** (inferior a 38 caracteres), confirme la contraseña y, después, seleccione **Aceptar**. Especifique al menos una cuenta de instalación de inserción de cliente. Esta cuenta debe tener derechos de administrador local en el equipo de destino para instalar el cliente. Si no especifica al menos una cuenta de instalación de inserción de cliente, Configuration Manager intenta usar la cuenta de equipo de sistema de sitio. Se produce un error en la inserción de cliente entre dominios cuando se usa la cuenta de equipo de sistema de sitio.  

    > [!NOTE]  
    > Para usar la inserción de cliente desde un sitio secundario, especifique la cuenta en el sitio secundario que inicia la inserción de cliente.  
    >
    > Para obtener más información sobre la cuenta de instalación de inserción de cliente, vea el procedimiento siguiente, [Usar el Asistente para instalación de inserción de cliente](#use-the-client-push-installation-wizard).  

8. Especifique las propiedades de instalación necesarias en la pestaña **Propiedades de instalación**.

    Si ha extendido el esquema de Active Directory a Configuration Manager, el sitio publica las [propiedades de instalación de cliente](about-client-installation-properties.md) especificadas en Active Directory Domain Services. Cuando se ejecuta CCMSetup sin propiedades de instalación, lee estas propiedades de Active Directory.  

    > [!NOTE]  
    > Si se habilita la instalación de inserción de cliente en un sitio secundario, establezca la propiedad **SMSSITECODE** en el código de sitio de Configuration Manager de su sitio primario principal. Si ha extendido el esquema de Active Directory a Configuration Manager para que busque automáticamente la asignación de sitio correcta, establezca esta propiedad en **AUTO**.

### <a name="use-the-client-push-installation-wizard"></a>Usar el Asistente para instalación de inserción de cliente

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Seleccione el sitio para el que va a configurar la instalación de inserción de cliente automática en todo el sitio.  

3. En la pestaña **Inicio** de la cinta, en el grupo **Configuración**, seleccione **Configuración de instalación de cliente** y, luego, **Instalación de inserción de cliente**.  

4. Especifique las propiedades de instalación necesarias en la pestaña **Propiedades de instalación**.  

    Si ha extendido el esquema de Active Directory a Configuration Manager, el sitio publica las [propiedades de instalación de cliente](about-client-installation-properties.md) especificadas en Active Directory Domain Services. Cuando se ejecuta CCMSetup sin propiedades de instalación, lee estas propiedades de Active Directory.

5. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**.  

6. En el nodo **Dispositivos**, seleccione uno o varios equipos. O seleccione una colección de equipos en el nodo **Colecciones de dispositivos**.  

7. En la pestaña **Inicio** de la cinta, elija una de las opciones siguientes:  

    - Para insertar el cliente en uno o más dispositivos, en el grupo **Dispositivo**, elija **Instalar cliente**.  

    - Para insertar el cliente en una colección de dispositivos, en el grupo **Colección**, elija **Instalar cliente**.  

8. En la página **Antes de comenzar** del Asistente para instalación del cliente de Configuration Manager, revise la información y después seleccione **Siguiente**.  

9. Seleccione las opciones adecuadas en la página **Opciones de instalación**.  

10. Revise la configuración de instalación y después cierre el asistente.  

> [!NOTE]  
> Use este asistente para instalar clientes incluso si el sitio no está configurado para la inserción de clientes.  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> Instalación basada en actualización de software  

La instalación de clientes basada en actualizaciones de software publica el cliente en un punto de actualización de software como una actualización de software. Use este método para una actualización o instalación por primera vez.  

Si el cliente de Configuration Manager está instalado en un equipo, este recibe la directiva de cliente desde el sitio. Esta directiva incluye el nombre del servidor de punto de actualización de software y el puerto desde el que se van a obtener las actualizaciones de software.

> [!IMPORTANT]  
> Para la instalación basada en actualizaciones de software, use el mismo servidor de Windows Server Update Services (WSUS) para la instalación de cliente y actualizaciones de software. Este servidor debe ser el punto de actualización de software activo de un sitio primario. Para obtener más información, consulte [Install a software update point](../../../sum/get-started/install-a-software-update-point.md) (Instalar un punto de actualización de software).

Si el cliente de Configuration Manager no está instalado en un equipo, configure y asigne un objeto de directiva de grupo. Esta directiva de grupo especifica el nombre del servidor del punto de actualización de software.  

No se pueden agregar propiedades de línea de comandos a una instalación de cliente basada en actualizaciones de software. Si se extendió el esquema de Active Directory a Configuration Manager, durante la instalación del cliente se consultan automáticamente las propiedades de instalación en Active Directory Domain Services.  

Si no se extendió el esquema de Active Directory, use la directiva de grupo para aprovisionar la configuración de instalación del cliente. Esta configuración se aplica automáticamente a cualquier instalación de cliente basada en actualizaciones de software. Para obtener más información, vea la sección en [Cómo aprovisionar propiedades de instalación de cliente](#BKMK_Provision) y el artículo sobre [Cómo asignar clientes a un sitio](assign-clients-to-a-site.md).  

Use los procedimientos siguientes para configurar equipos sin un cliente de Configuration Manager para usar el punto de actualización de software. También hay un procedimiento para publicar el software cliente en el punto de actualización de software.  

> [!TIP]  
> Si los equipos se encuentran en un estado de reinicio pendiente tras una instalación de software previa, una instalación de cliente basada en actualizaciones de software podría provocar que el equipo se reinicie.  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Configuración de un objeto de directiva de grupo para especificar el punto de actualización de software  

1. Use la **Consola de administración de directivas de grupo** para abrir un objeto de directiva de grupo nuevo o existente.  

2. Expanda **Configuración del equipo**, **Plantillas administrativas** y **Componentes de Windows** y después seleccione **Windows Update**.  

3. Abra las propiedades de la opción **Especificar la ubicación del servicio Windows Update en la intranet** y, después, seleccione **Habilitado**.  

4. **Establecer el servicio de actualización de la intranet para detectar actualizaciones**: especifique el nombre y el puerto del servidor de punto de actualización de software.  

    - Si ha configurado el sistema de sitio de Configuration Manager para usar un nombre de dominio completo (FQDN), use ese formato.  

    - Si el sistema de sitio de Configuration Manager no está configurado para usar un FQDN, use un formato de nombre corto.

    > [!TIP]  
    > Para determinar el número de puerto, vea [Configuración del puerto de WSUS](../../../sum/plan-design/plan-for-software-updates.md).

    Ejemplo con el formato FQDN: `http://server1.contoso.com:8530`  

5. **Establecer el servidor de estadísticas de la intranet**: esta configuración normalmente se realiza con el mismo nombre de servidor.

6. Asigne el objeto de directiva de grupo a los equipos en los que se va a instalar el cliente y recibir actualizaciones de software.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publicar el cliente de Configuration Manager en el punto de actualización de software  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Seleccione el sitio para el que va a configurar la instalación de cliente basada en actualizaciones de software.  

3. En la pestaña **Inicio** de la cinta, en el grupo **Configuración**, seleccione **Configuración de instalación de cliente** y, luego, **Instalación de cliente basada en actualizaciones de software**.  

4. Seleccione **Habilitar instalación de cliente basada en actualizaciones de software**.  

5. Si la versión del cliente es más reciente que la versión en el punto de actualización de software, se abre el cuadro de diálogo **Se detectó una versión más reciente del paquete de cliente**. Seleccione **Sí** para publicar la versión más reciente.  

    > [!NOTE]  
    > Si aún no ha publicado el software cliente en el punto de actualización de software, este cuadro de diálogo está en blanco.

La actualización de software para el cliente de Configuration Manager no se actualiza automáticamente cuando hay una versión nueva. Cuando se actualiza el sitio, repita este procedimiento para actualizar el cliente.  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a> Instalación de la directiva de grupo

Use la directiva de grupo de Active Directory Domain Services para publicar o asignar el cliente de Configuration Manager. El cliente se instala cuando se inicia el equipo. Cuando se usa la directiva de grupo, el cliente aparece en **Agregar o quitar programas** en el Panel de control. El usuario puede instalarlo desde ahí.  

Use el paquete CCMSetup.msi de Windows Installer con instalaciones basadas en directiva de grupo. Este archivo se encuentra en la carpeta `<ConfigMgr installation directory>\bin\i386` del servidor de sitio. No se pueden agregar propiedades a este archivo para modificar el comportamiento de instalación.  

> [!IMPORTANT]  
> Es necesario tener permisos de administrador para acceder a los archivos de instalación del cliente.  

- Si ha extendido el esquema de Active Directory a Configuration Manager y ha seleccionado el dominio en la pestaña **Publicación** del cuadro de diálogo **Propiedades del sitio**, los equipos cliente buscan automáticamente las propiedades de instalación en Active Directory Domain Services. Para obtener más información, vea [Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md).  

- Si no ha extendido el esquema de Active Directory, consulte la sección sobre [cómo aprovisionar propiedades de instalación de cliente](#BKMK_Provision) para información sobre el almacenamiento de propiedades de instalación en el Registro de Windows de los equipos. El cliente usa estas propiedades de instalación cuando instala.  

Para más información, consulte [Cómo utilizar directiva de grupo para instalar software de forma remota](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a> Instalación manual

Instale manualmente el software cliente en los equipos mediante CCMSetup.exe. Puede encontrar este programa y sus archivos auxiliares en la carpeta Cliente de la carpeta de instalación de Configuration Manager en el servidor de sitio. El sitio comparte esta carpeta en la red como:  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>` es el nombre del servidor de sitio principal. `<site code>` es el código de sitio principal al que se asigna el cliente. Para ejecutar CCMSetup.exe desde la línea de comandos en el cliente, conéctese a esta ubicación de red y luego ejecute el comando.  

> [!IMPORTANT]  
> Es necesario tener permisos de administrador para acceder a los archivos de instalación del cliente.  

CCMSetup.exe copia todos los requisitos previos necesarios en el equipo cliente y llama al paquete de Windows Installer (Client.msi) para instalar el cliente. No se puede ejecutar Client.msi directamente.  

Para modificar el comportamiento de la instalación del cliente especifique las propiedades de línea de comandos para CCMSetup.exe y Client.msi. Asegúrese de especificar los parámetros CCMSetup que comienzan por `/` antes de especificar las propiedades de Client.msi. Por ejemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

En este ejemplo, el cliente se instala con las siguientes opciones:  

|Opción|Descripción|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Este parámetro CCMSetup especifica el punto de administración SMSMP01 para descargar los archivos de instalación de cliente necesarios.|  
|`/logon`|Este parámetro de CCMSetup especifica que la instalación se debe detener si se encuentra un cliente de Configuration Manager en el equipo.|  
|`SMSSITECODE=AUTO`|Esta propiedad Client.msi especifica que el cliente intenta localizar el código de sitio de Configuration Manager que va a usar, por ejemplo, mediante Active Directory Domain Services.|  
|`FSP=SMSFP01`|Esta propiedad de Client.msi especifica que el punto de estado de reserva denominado SMSFP01 se usa para recibir mensajes de estado enviados desde el equipo cliente.|  

Para obtener más información, vea [Acerca de los parámetros y propiedades de instalación de cliente](about-client-installation-properties.md).  

> [!TIP]  
> Para conocer el procedimiento de instalación del cliente de Configuration Manager en un dispositivo Windows 10 moderno mediante identidades de Azure Active Directory (Azure AD), consulte [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](deploy-clients-cmg-azure.md). Ese procedimiento es para los clientes de una intranet o de Internet.  

### <a name="manual-installation-examples"></a>Ejemplos de instalación manual

Estos ejemplos son para los clientes unidos a Active Directory en la intranet. Usan los valores siguientes:  

- **MPSERVER**: servidor que hospeda el punto de administración
- **FSPSERVER**: servidor que hospeda el punto de estado de reserva  
- **ABC**: código de sitio  
- **contoso.com**: nombre de dominio  

Supongamos que ha configurado todos los servidores del sistema de sitio con un FQDN de intranet y que ha publicado la información del sitio en Active Directory.  

Comience con los pasos siguientes en el equipo cliente:  

1. Inicie sesión como administrador local.  
2. Asigne la unidad Z a `\\MPSERVER\SMS_ABC\Client`.  
3. Cambie el símbolo del sistema a la unidad Z.  

Después, ejecute uno de los siguientes comandos:  

#### <a name="manual-example-1"></a>Ejemplo manual 1  

`CCMSetup.exe`  

Este comando instala el cliente sin propiedades ni parámetros adicionales. El cliente se configura automáticamente con las propiedades de instalación de cliente publicadas en Active Directory Domain Services, incluida la siguiente configuración:  

- Código de sitio: este valor requiere que la ubicación de red del cliente se incluya en un grupo de límites configurado para la asignación de cliente.  
- Punto de administración
- Punto de estado de reserva
- Comunicación solo mediante HTTPS  

Para obtener más información, vea [Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md).  

#### <a name="manual-example-2"></a>Ejemplo de manual 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Este comando reemplaza la configuración automática que proporciona Active Directory Domain Services. No requiere que la ubicación de red del cliente esté incluida en un grupo de límites configurado para la asignación de cliente. En su lugar, la instalación especifica los valores siguientes:

- Código de sitio
- Punto de administración de intranet
- Punto de administración basado en Internet
- Punto de estado de reserva que acepta conexiones desde Internet
- Use un certificado de infraestructura de clave pública (PKI) (si está disponible) que tenga el período de validez más largo.

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a> Instalación de script de inicio de sesión

Configuration Manager admite el uso de scripts de inicio de sesión para instalar el software cliente de Configuration Manager. Use el archivo de programa CCMSetup.exe en un script de inicio de sesión para desencadenar la instalación del cliente.  

La instalación del script de inicio de sesión utiliza los mismos métodos que la instalación manual del cliente. Especifique el parámetro `/logon` de instalación para CCMSsetup.exe. Si ya existe una versión del cliente en el equipo, este parámetro evita que el cliente se instale. Este comportamiento impide que se vuelva a instalar el cliente cada vez que se ejecute el script de inicio de sesión.  

Si no especifica ningún origen de instalación mediante el parámetro `/Source` ni ningún punto de administración del que obtener la instalación mediante el parámetro `/MP`, CCMSetup.exe busca en Active Directory Domain Services el punto de administración. Este comportamiento solo se produce si ha extendido el esquema de Configuration Manager a Active Directory Domain Services y ha publicado el sitio ahí. Como alternativa, el cliente puede utilizar DNS o WINS para localizar un punto de administración.  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a> Instalación de paquete y programa

Use Configuration Manager para crear e implementar un paquete y un programa que actualice el software cliente para dispositivos seleccionados. Configuration Manager suministra un archivo de definición del paquete que rellena las propiedades del paquete con los valores que se suelen usar. Puede personalizar el comportamiento de la instalación del cliente mediante la especificación de propiedades y parámetros de línea de comandos adicionales.  

> [!NOTE]  
> No puede actualizar clientes de Configuration Manager 2007 con este método. En su lugar, utilice la actualización de cliente automática, que automáticamente crea e implementa un paquete que contiene la versión más reciente del cliente. Para obtener más información, vea [Actualizar clientes](../manage/upgrade/upgrade-clients.md).  
>
> Para obtener más información sobre cómo migrar desde versiones anteriores del cliente de Configuration Manager, vea [Planear una estrategia de migración de clientes](../../migration/planning-a-client-migration-strategy.md).  

### <a name="create-a-package-and-program-for-the-client-software"></a>Crear un paquete y un programa para el software cliente  

Use el procedimiento siguiente para crear un paquete y un programa de Configuration Manager que pueda implementar en equipos cliente de Configuration Manager para actualizar el software cliente.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**.  

2. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear paquete a partir de definición**.  

3. En la página **Definición de paquete** del asistente, seleccione **Microsoft** en la lista desplegable **Editor** y seleccione **Actualización de cliente de Configuration Manager** en la lista **Definición de paquete**.  

4. En la página **Archivos de origen**, seleccione **Obtener siempre los archivos de la carpeta de origen**.  

5. En la página **Carpeta de origen**, seleccione **Ruta de red (nombre UNC)** . Después, escriba la ruta de acceso de red del servidor y el recurso compartido que contiene los archivos de instalación del cliente.  

    > [!NOTE]  
    > El equipo en el que se ejecute la implementación de Configuration Manager debe tener acceso a la carpeta de red especificada. De lo contrario, se produce un error en la instalación del cliente.  

    Para cambiar alguna de las propiedades de instalación de cliente, modifique la línea de comandos de CCMSetup.exe en la pestaña **General** del cuadro de diálogo del programa **Propiedades de actualización silenciosa de agente de Configuration Manager**. Las propiedades de instalación predeterminada son `/noservice SMSSITECODE=AUTO`.  

6. Distribuya el paquete a todos los puntos de distribución en los que desea hospedar el paquete de actualización de cliente. Después implemente el paquete en las colecciones de dispositivos que contengan los clientes que quiere actualizar.  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a> Dispositivos Windows administrados por MDM con Intune

Implemente el cliente de Configuration Manager en dispositivos inscritos con Microsoft Intune.

Este procedimiento es para un cliente tradicional que está conectado a una intranet. Usa métodos de autenticación de cliente tradicionales. Para asegurarse de que el dispositivo permanece en un estado administrado después de instalar el cliente, el dispositivo debe encontrarse en la intranet y dentro de los límites del sitio de Configuration Manager.  

Para conocer el procedimiento de instalación del cliente de Configuration Manager en un dispositivo Windows 10 moderno mediante identidades de Azure AD, consulte [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](deploy-clients-cmg-azure.md).

Después de instalar el cliente de Configuration Manager, no se anula la inscripción de los dispositivos en Intune. Pueden usar el cliente de Configuration Manager y la inscripción de MDM al mismo tiempo. Para obtener más información, vea [Información general sobre la administración conjunta](../../../comanage/overview.md).  

> [!Note]
> Puede usar otros métodos de instalación de cliente para instalar el cliente de Configuration Manager en un dispositivo administrado por Intune. Por ejemplo, si un dispositivo administrado por Intune está en la intranet y está unido al dominio Active Directory, puede usar la directiva de grupo para instalar el cliente de Configuration Manager.<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>Instalación del cliente de Configuration Manager mediante Intune

1. En Intune, [agregue una aplicación de línea de negocio de Windows](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows) que contenga el archivo de instalación del cliente de Configuration Manager **CCMSetup.msi**. Puede encontrar este archivo en la carpeta `\bin\i386` en el directorio de instalación de Configuration Manager del servidor del sitio.  

2. En el editor de software de Intune, escribe los parámetros de línea de comandos. Por ejemplo, use este comando con un cliente tradicional en una intranet:  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > Para ver un ejemplo de comando para usar con un cliente de Windows 10 moderno mediante la autenticación de Azure AD, consulte [Preparación de dispositivos basados en Internet para la administración conjunta](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).  

3. [Asigne la aplicación](https://docs.microsoft.com/mem/intune/apps/apps-deploy) a un grupo de equipos Windows inscritos.  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a> Instalación de la imagen de sistema operativo

Preinstale el cliente de Configuration Manager en un equipo de referencia que use para crear una imagen de SO.

> [!IMPORTANT]  
> Al usar la secuencia de tareas de Configuration Manager para implementar una imagen del SO, el paso [Preparar el cliente de Configuration Manager](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture) quita completamente el cliente de Configuration Manager.  

### <a name="prepare-the-client-computer-for-imaging"></a>Preparar el equipo cliente para la creación de imágenes  

1. Instale manualmente el software de cliente de Configuration Manager en el equipo de referencia. Para obtener más información, vea [How to install Configuration Manager Clients Manually (Instalación manual de clientes de Configuration Manager)](#BKMK_Manual).  

    > [!IMPORTANT]  
    > No especifique un código de sitio de Configuration Manager para el cliente en las propiedades de línea de comandos de CCMSetup.exe.  

2. En un símbolo del sistema, escriba `net stop ccmexec` para detener el servicio Host de agente de SMS (Ccmexec.exe) en el equipo de referencia.  

3. Elimine el archivo SMSCFG.INI de la carpeta Windows del equipo de referencia.  

4. Quite todos los certificados almacenados en el almacén del equipo local en el equipo de referencia. Por ejemplo, si usa certificados PKI, antes de crear la imagen del equipo, quite los certificados del almacén **Personal** para **Equipo** y **Usuario**.  

5. Si los clientes están instalados en una jerarquía de Configuration Manager diferente a la del equipo de referencia, quite la clave raíz confiable del equipo de referencia.  

    > [!NOTE]  
    > Si los clientes no pueden consultar los Active Directory Domain Services para localizar un punto de administración, utilizan la clave raíz de confianza para determinar los puntos de administración de confianza. Si implementa todos los clientes con imágenes en la misma jerarquía que el equipo maestro, deje la clave raíz confiable.
    >
    > Si implementa los clientes en jerarquías distintas, quite la clave raíz confiable. Aprovisione también estos clientes con la nueva clave raíz confiable. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

6. Utilice software de creación de imágenes para capturar una imagen del equipo de referencia.  

7. Implemente la imagen en los equipos de destino.  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Equipos de grupo de trabajo

Configuration Manager admite la instalación de cliente para equipos del grupo de trabajo. Instale el cliente en los equipos del grupo de trabajo mediante el método especificado en [Instalación manual de clientes de Configuration Manager](#BKMK_Manual).  

### <a name="prerequisites"></a>Requisitos previos  

- Instalar manualmente el cliente en cada equipo del grupo de trabajo. Durante la instalación, el usuario interactivo debe tener derechos de administrador local.  

- Para acceder a los recursos del dominio del servidor de sitio de Configuration Manager, configure una cuenta de acceso de red para el sitio. Especifique esta cuenta en el componente de sitio de distribución de software. Para obtener más información, vea [Componentes de sitio](../../servers/deploy/configure/site-components.md).  

### <a name="limitations"></a>Limitaciones  

- Los clientes del grupo de trabajo no pueden encontrar puntos de administración de Active Directory Domain Services. En su lugar, usan DNS, WINS u otro punto de administración.  

- No se admite la itinerancia global. Los clientes del grupo de trabajo no pueden consultar Active Directory Domain Services para obtener información del sitio.  

- Los métodos de detección de Active Directory no pueden detectar equipos en los grupos de trabajo.  

- No se puede implementar software para usuarios de equipos del grupo de trabajo.  

- No se puede utilizar el método de instalación de inserción de cliente para instalar el cliente en equipos del grupo de trabajo.  

- Los clientes del grupo de trabajo no pueden usar Kerberos para la autenticación, por lo que podrían necesitar aprobación manual.  

- No puede configurar un cliente de grupo de trabajo como punto de distribución. Configuration Manager requiere que los equipos de punto de distribución pertenezcan a un dominio.  

### <a name="install-the-client-on-workgroup-computers"></a>Instalar el cliente en equipos del grupo de trabajo  

Compruebe los requisitos previos y, después, siga las instrucciones de la sección sobre [cómo instalar clientes de Configuration Manager manualmente](#BKMK_Manual).  

#### <a name="workgroup-example-1"></a>Ejemplo de grupo de trabajo 1

Este ejemplo realiza las siguientes acciones:

- Instala el cliente para la administración de cliente de intranet
- Especifica el código de sitio
- Especifica el sufijo DNS para localizar un punto de administración  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>Ejemplo de grupo de trabajo 2

En este ejemplo se requiere que el cliente se encuentre en una ubicación de red configurada en un grupo de límites. Si no se cumple este requisito, no funcionará la asignación automática del sitio. El comando incluye un punto de estado de reserva en el servidor FSPSERVER. Esta propiedad ayuda a realizar el seguimiento de la implementación del cliente y a identificar cualquier problema de comunicación del cliente.

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> Administración de cliente basada en Internet  

> [!NOTE]  
> Esta sección no se aplica a los clientes que usan una instancia de [Cloud Management Gateway](../manage/cmg/plan-cloud-management-gateway.md). Para instalar clientes basados en Internet mediante una instancia de Cloud Management Gateway, consulte [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](deploy-clients-cmg-azure.md).  

Si el sitio de Configuration Manager admite la [administración de clientes basada en Internet](../manage/plan-internet-based-client-management.md) para clientes que a veces se encuentran en la intranet y a veces en Internet, dispone de dos opciones para instalar clientes en la intranet:  

- Puede incluir la propiedad Client.msi de `CCMHOSTNAME=<internet FQDN of the internet-based management point>` cuando instale el cliente, por ejemplo, mediante la instalación manual o la inserción del cliente. Cuando use este método, asigne directamente el cliente al sitio. Puede usar una asignación automática de sitio. Vea la sección [Cómo instalar clientes de Configuration Manager manualmente](#BKMK_Manual), que proporciona un ejemplo de este método de configuración.  

- Instale el cliente para la administración de cliente de intranet y después asignar un punto de administración de cliente basado en Internet al cliente. Cambie el punto de administración mediante las propiedades de cliente de la página de **Configuration Manager** en el Panel de control o bien mediante un script. Cuando utilice este método, puede utilizar la asignación automática de cliente. Para obtener más información, vea la sección [Cómo configurar clientes para la administración de cliente basada en Internet después de la instalación de cliente](#BKMK_ConfigureIBCM_MP).  

Para instalar clientes que están en Internet, elija uno de los siguientes métodos admitidos:  

- Proporcione un mecanismo para que estos clientes se conecten temporalmente a la intranet con una VPN. Después, instale el cliente mediante cualquier método de instalación de cliente adecuado.  

- Use un método de instalación independiente de Configuration Manager. Por ejemplo, empaquete los archivos de origen de instalación del cliente en medios extraíbles y envíelos a los usuarios. Los archivos de origen de instalación están ubicados en la carpeta `<installation path>\Client` en el servidor de sitio de Configuration Manager. Incluya un script en los medios para copiarlo manualmente en la carpeta de cliente. Desde esta carpeta, instale el cliente mediante CCMSetup.exe y todas las propiedades de línea de comandos apropiadas de CCMSetup.  

> [!NOTE]  
> Configuration Manager no admite la instalación de un cliente directamente desde el punto de administración basado en Internet ni desde el punto de actualización de software basado en Internet.

Los clientes que se administran a través de Internet se deben comunicar con sistemas de sitio basados en Internet. Asegúrese de que estos clientes también disponen de certificados de infraestructura de clave pública (PKI) antes de instalar al cliente. Instale estos certificados con independencia de Configuration Manager. Para obtener más información, vea [Requisitos de certificados PKI](../../plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Instalar clientes en Internet mediante la especificación de propiedades de línea de comandos de CCMSetup  

1. Siga las instrucciones de la sección [Instalación manual de clientes de Configuration Manager](#BKMK_Manual). Incluya siempre las siguientes opciones:  

    - Parámetro de la línea de comandos de CCMSetup `/source:<local path of the copied Client folder>`  

    - Parámetro de la línea de comandos de CCMSetup `/UsePKICert`  

    - Propiedad Client.msi `CCMHOSTNAME=<FQDN of internet-based management point>`  

    - Propiedad Client.msi `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - Propiedad Client.msi `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > Si el sitio tiene más de un punto de administración basado en Internet, no importa cuál especifique para la propiedad `CCMHOSTNAME`. Cuando un cliente de Configuration Manager se conecta al punto de administración basado en Internet especificado, envía al cliente una lista de los puntos de administración basados en Internet disponibles en el sitio. El cliente selecciona uno de la lista de manera aleatoria.

2. Si no quiere que el cliente compruebe la lista de revocación de certificados (CRL), especifique el parámetro de línea de comandos de CCMSetup `/NoCRLCheck`.  

3. Si usa un punto de estado de reserva basado en Internet, especifique la propiedad Client.msi `FSP=<internet FQDN of the internet-based fallback status point>`.  

4. Si va a instalar el cliente para la administración de cliente solo de Internet, especifique la propiedad Client.msi `CCMALWAYSINF=1`.  

5. Determine si tiene que especificar parámetros de línea de comandos de CCMSetup adicionales. Por ejemplo, si el cliente tiene más de un certificado válido de PKI es posible que tenga que especificar un criterio de selección de certificado. Para obtener una lista de las propiedades disponibles, vea [Acerca de los parámetros y propiedades de instalación de cliente](about-client-installation-properties.md).  

#### <a name="internet-based-example"></a>Ejemplo basado en Internet

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

En este ejemplo se instala el cliente con los comportamientos siguientes:

- Usar archivos de origen de una carpeta en la unidad D
- Usar un certificado PKI de cliente
- Seleccionar el certificado con el período de validez más largo
- Administración de clientes solo de Internet
- Asignar el cliente para usar el punto de administración basado en Internet denominado SERVER1
- Asignar el punto de estado de reserva basado en Internet en el dominio contoso.com
- Asignar el cliente al sitio ABC  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> Para configurar clientes para la administración de cliente basada en Internet después de la instalación de cliente  

Para asignar el punto de administración basado en Internet después de instalar el cliente, use uno de estos procedimientos. El primero necesita una configuración manual y es apropiado para pocos clientes. El segundo es más apropiado para configurar muchos clientes.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Configure clientes para administración de cliente basada en Internet después de la instalación de cliente desde el panel de control de Configuration Manager  

1. Abra el panel de control **Configuration Manager** en el cliente.  

2. En la pestaña **Internet**, escriba el nombre de dominio completo (FQDN) del punto de administración basado en Internet en el cuadro de texto **FQDN de Internet**.  

    > [!NOTE]  
    > La pestaña **Internet** solo está disponible si el cliente tiene un certificado PKI de cliente.  

3. Si el cliente va a tener acceso a Internet mediante un servidor proxy, escriba la configuración del servidor proxy.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurar clientes para la administración de cliente basada en Internet después de la instalación de cliente mediante un script  

##### <a name="powershell"></a>PowerShell

1. Abra un editor en línea de PowerShell, como PowerShell ISE o Visual Studio Code. También puede usar un editor de texto, como el Bloc de notas.

2. Copie e inserte las líneas de código siguiente en el editor. Reemplace `'mp.contoso.com'` por el FQDN de Internet de su punto de administración basado en Internet.

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > La última línea existe solo para comprobar el nuevo valor del punto de administración de Internet.
    >
    > Para eliminar un punto de administración basado en Internet, quite el valor FQDN entre las comillas de servidor. Esta línea se convierte en `$newInternetBasedManagementPointFQDN = ''`.

3. Guarde el archivo con una extensión .ps1.  

4. Ejecute el script con derechos elevados en los equipos cliente. Use uno de estos métodos:  

    - Implemente el archivo en clientes de Configuration Manager existentes mediante un paquete y un programa.  

    - Ejecute el archivo localmente en los clientes existentes de Configuration Manager; para ello, haga doble clic en el archivo de script en el Explorador de Windows.  

Tendrá que reiniciar el cliente para que los cambios surtan efecto.  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a> Aprovisionamiento de propiedades de instalación de cliente

Aprovisione las propiedades de instalación del cliente para la instalación de cliente con directivas de grupo y basada en actualizaciones de software. Use la directiva de grupo de Windows para aprovisionar los equipos con las propiedades de instalación del cliente de Configuration Manager. Estas propiedades se almacenan en el registro del equipo. El cliente los lee cuando lo instala. Normalmente, este procedimiento no es necesario, pero es posible que se necesite en algunos escenarios de instalación de cliente, como:  

- Se está usando la configuración de directiva de grupo o métodos de instalación de cliente basados en actualizaciones de software. No se ha ampliado el esquema de Active Directory para Configuration Manager.  

- Desea reemplazar las propiedades de instalación de cliente en equipos específicos.  

> [!NOTE]  
> Si se proporcionan propiedades de instalación en la línea de comandos de CCMSetup.exe, no se usan las propiedades de instalación aprovisionadas en los equipos.

En el medio de instalación de Configuration Manager se proporciona una plantilla administrativa de directiva de grupo denominada `ConfigMgrInstallation.adm`. Use esta plantilla para aprovisionar equipos cliente con propiedades de instalación.

> [!TIP]
> De forma predeterminada, `ConfigMgrInstallation.adm` no admite cadenas de más de 255 caracteres. Esta configuración puede afectar a la adición de varios parámetros o a parámetros con valores largos, como CCMCERTISSUERS.<!-- SCCMDocs#1648 -->
>
> Para solucionar este problema:
>
> 1. Edite `ConfigMgrInstallation.adm` en el Bloc de notas.
> 2. Para la propiedad `VALUENAME SetupParameters`, cambie el valor `MAXLEN` a un entero más grande. Por ejemplo, `MAXLEN 511`.

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurar y asignar propiedades de instalación de cliente mediante un objeto de directiva de grupo  

1. Importe la plantilla administrativa ConfigMgrInstallation.adm en un objeto de directiva de grupo nuevo o existente, mediante un editor como el Editor de objetos de directiva de grupo de Windows. Puede encontrar este archivo en la carpeta `TOOLS\ConfigMgrADMTemplates` en los medios de instalación de Configuration Manager.  

2. Abra las propiedades de la configuración importada **Configurar opciones de implementación de cliente**.  

3. Seleccione **Habilitado**.  

4. En el cuadro **CCMSetup** , escriba las propiedades de línea de comandos de CCMSetup necesarias. Para obtener una lista de las propiedades de la línea de comandos de CCMSetup y ejemplos de su uso, vea [Acerca de los parámetros y propiedades de instalación de clientes](about-client-installation-properties.md).  

5. Asigne el objeto de directiva de grupo a los equipos que quiera aprovisionar con las propiedades de instalación de cliente de Configuration Manager.  
