---
title: Configuración del firewall y el puerto para clientes de Windows
titleSuffix: Configuration Manager
description: Seleccione la configuración de puertos y Firewall de Windows en clientes de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2290899c0159221c5f45ce6c34332b766984e4c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694783"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-configuration-manager"></a>Configuración de puertos y Firewall de Windows en clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los equipos cliente en Configuration Manager que ejecutan Firewall de Windows a menudo requieren que se configuren excepciones para permitir la comunicación con su sitio. Las excepciones que debe configurar dependen de las características de administración que se usen con el cliente de Configuration Manager.  

 Use las secciones siguientes para identificar estas características de administración y para obtener más información acerca de cómo configurar Firewall de Windows para estas excepciones.  

##  <a name="modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> Modificación de los puertos y los programas permitidos por Firewall de Windows  
 Utilice el siguiente procedimiento para modificar los puertos y los programas en Firewall de Windows para el cliente de Configuration Manager.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Para modificar los puertos y los programas permitidos por Firewall de Windows  

1.  En el equipo que ejecuta Firewall de Windows, abra el Panel de Control.  

2.  Haga clic con el botón secundario en **Firewall de Windows**y, a continuación, haga clic en **Abrir**.  

3.  Configure las excepciones necesarias y los puertos y programas personalizados que necesite.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Programas y puertos que necesita Configuration Manager  
 Las siguientes características de Configuration Manager requieren excepciones del Firewall de Windows:  

### <a name="queries"></a>Consultas  
 Si ejecuta la consola de Configuration Manager en un equipo que ejecuta Firewall de Windows, las consultas producirán un error la primera vez que las ejecute y el sistema operativo mostrará un cuadro de diálogo preguntando si desea desbloquear statview.exe. Si desbloquea statview.exe, las consultas futuras se ejecutarán sin errores. También puede agregar manualmente Statview.exe a la lista de programas y servicios en la pestaña **Excepciones** de Firewall de Windows antes de ejecutar una consulta.  

### <a name="client-push-installation"></a>Instalación de inserción de cliente  
 Para usar la inserción de cliente para instalar el cliente de Configuration Manager, agregue las excepciones siguientes al Firewall de Windows:  

-   Entrante y saliente: **Uso compartido de archivos e impresoras**  

-   Entrante: **Instrumental de administración de Windows (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>Instalación del cliente mediante el uso de la directiva de grupo  
 Para usar la directiva de grupo para instalar el cliente de Configuration Manager, agregue **Compartir archivos e impresoras** como excepción al Firewall de Windows.  

### <a name="client-requests"></a>Solicitudes de cliente  
 Para que los equipos cliente se comuniquen con los sistemas de sitio de Configuration Manager, agregue las siguientes excepciones al Firewall de Windows:  

 Saliente: puerto TCP **80** (para comunicación HTTP)  

 Saliente: puerto TCP **443** (para comunicación HTTP)  

> [!IMPORTANT]  
>  Estos son los números de puerto predeterminados que se pueden cambiar en Configuration Manager. Para más información, vea [Configuración de puertos de comunicación de cliente](../../../core/clients/deploy/configure-client-communication-ports.md). Si se han cambiado los valores predeterminados de estos puertos, también debe configurar las excepciones correspondientes en el Firewall de Windows.  

### <a name="client-notification"></a>Notificación de cliente  
 Para que el punto de administración notifique a los equipos cliente sobre una acción que deben efectuar cuando un usuario administrativo selecciona una acción de cliente en la consola de Configuration Manager, como descargar la directiva de equipo o iniciar un examen antimalware, agregue la siguiente excepción al Firewall de Windows:  

 Saliente: puerto TCP **10123**  

 Si esta comunicación no se realiza correctamente, Configuration Manager revierte automáticamente al uso del puerto de comunicación de HTTP o HTTPS entre el cliente y el punto de administración existente:  

 Saliente: puerto TCP **80** (para comunicación HTTP)  

 Saliente: puerto TCP **443** (para comunicación HTTP)  

> [!IMPORTANT]  
>  Estos son los números de puerto predeterminados que se pueden cambiar en Configuration Manager. Para más información, vea [Configuración de puertos de comunicación de cliente](../../../core/clients/deploy/configure-client-communication-ports.md). Si se han cambiado los valores predeterminados de estos puertos, también debe configurar las excepciones correspondientes en el Firewall de Windows.  

### <a name="remote-control"></a>Control remoto  
 Para usar el control remoto de Configuration Manager, permita el puerto siguiente:  

-   Entrante: puerto TCP **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Asistencia remota y Escritorio remoto  
 Para iniciar Asistencia remota desde la consola de Configuration Manager, agregue el programa personalizado **Helpsvc.exe** y el puerto personalizado de entrada TCP **135** a la lista de programas y servicios permitidos en Firewall de Windows en el equipo cliente. También debe permitir **Asistencia remota** y **Escritorio remoto**. Si inicia Asistencia remota desde el equipo cliente, Firewall de Windows configura y permite de forma automática **Asistencia remota** y **Escritorio remoto**.  

### <a name="wake-up-proxy"></a>Proxy de reactivación  
 Si habilita la configuración de cliente proxy de reactivación, un nuevo servicio llamado Proxy de reactivación de Configuration Manager usa un protocolo punto a punto para comprobar si hay otros equipos activados en la subred y los reactiva en caso necesario. Esta comunicación utiliza los siguientes puertos:  

 Saliente: puerto UDP **25536**  

 Saliente: Puerto UDP **9**  

 Estos son los números de puerto predeterminado que se pueden cambiar en Configuration Manager mediante el uso de configuraciones de clientes de **Administración de energía** de **Número de puerto de proxy de reactivación (UDP)** y **Número de puerto de Wake On LAN (UDP)** . Si especifica la opción de cliente **Administración de energía**: **Excepción del Firewall de Windows para proxy de reactivación**, estos puertos se configuran automáticamente en el Firewall de Windows para los clientes. Sin embargo, si los clientes ejecutan otro firewall, debe configurar manualmente las excepciones para estos números de puerto.  

 Además de estos puertos, el proxy de reactivación también utiliza los mensajes de solicitud de eco del Protocolo de mensajes de control de Internet (ICMP) desde un equipo cliente a otro equipo cliente. Esta comunicación se utiliza para confirmar si el otro equipo cliente está activo en la red. ICMP se conoce a veces como comandos ping de TCP/IP.  

 Para obtener más información sobre el proxy de reactivación, vea [Planear la reactivación de clientes](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Visor de eventos de Windows, Monitor de rendimiento de Windows y Diagnósticos de Windows  
 Para acceder al Visor de eventos de Windows, al Monitor de rendimiento de Windows y a Diagnósticos de Windows desde la consola de Configuration Manager, habilite **Compartir archivos e impresoras** como una excepción en Firewall de Windows.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Puertos utilizados durante la implementación de cliente de Configuration Manager  
 Las tablas siguientes enumeran los puertos que se utilizan durante el proceso de instalación del cliente.  

> [!IMPORTANT]  
>  Si existe un firewall entre los servidores de sistema de sitio y el equipo cliente, confirme si el firewall permite el tráfico en los puertos necesarios para el método de instalación de cliente que elija. Por ejemplo, los firewall suelen impedir que se produzca la instalación de inserción de cliente correctamente porque bloquean el Bloque de mensajes del servidor (SMB) y las llamadas a procedimiento remoto (RPC). En este escenario, utilice un método de instalación de cliente diferente, como la instalación manual (ejecutando CCMSetup.exe) o la instalación de cliente basada en directiva de grupo. Estos métodos de instalación de cliente alternativos no requieren SMB o RPC.  

 Para obtener información acerca de cómo configurar Firewall de Windows en el equipo cliente, consulte [Modificación de los puertos y los programas permitidos por Firewall de Windows](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Puertos que se usan para todos los métodos de instalación  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP) desde el equipo cliente a un punto de estado de reserva, cuando se asigna un punto de estado de reserva al cliente.|--|80 (Véase la nota 1, **Puerto alternativo disponible**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Puertos que se utilizan con la instalación de inserción de cliente  
 Además de los puertos enumerados en la tabla siguiente, la instalación de inserción de cliente también usa mensajes de solicitud de eco del Protocolo de mensajes de control de Internet (ICMP) desde el servidor de sitio al equipo cliente para confirmar si el equipo cliente está disponible en la red. ICMP se conoce a veces como comandos ping de TCP/IP. ICMP no tiene un número de protocolo UDP o TCP y, por lo tanto, no aparece en la tabla siguiente. Sin embargo, los dispositivos de red que intervienen, tales como firewalls, deben permitir el tráfico ICMP para que la instalación de inserción de cliente se produzca correctamente.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB) entre el equipo cliente y el servidor de sitio.|--|445|  
|Asignador de extremos de RPC entre el servidor de sitio y el equipo cliente.|135|135|  
|Puertos dinámicos de RPC entre el servidor de sitio y el equipo cliente.|--|DINÁMICO|  
|Protocolo de transferencia de hipertexto (HTTP) desde el equipo cliente a un punto de administración cuando la conexión es a través de HTTP.|--|80 (Véase la nota 1, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS) desde el equipo cliente a un punto de administración cuando la conexión es a través de HTTPS.|--|443 (véase la nota 1, **Puerto alternativo disponible**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Puertos que se utilizan con la instalación basada en el punto de actualización de software  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP) desde el equipo cliente al punto de actualización de software.|--|80 o 8530 (Véase la nota 2, **Windows Server Update Services**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS) desde el equipo cliente al punto de actualización de software.|--|443 o 8531 (véase la nota 2, **Windows Server Update Services**)|  
|Bloque de mensajes del servidor (SMB) entre el servidor de origen y el equipo cliente cuando especifica la propiedad de la línea de comandos CCMSetup **/source:&lt;Ruta\>** .|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Puertos que se utilizan con la instalación basada en directiva de grupo  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo de transferencia de hipertexto (HTTP) desde el equipo cliente a un punto de administración cuando la conexión es a través de HTTP.|--|80 (Véase la nota 1, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS) desde el equipo cliente a un punto de administración cuando la conexión es a través de HTTPS.|--|443 (véase la nota 1, **Puerto alternativo disponible**)|  
|Bloque de mensajes del servidor (SMB) entre el servidor de origen y el equipo cliente cuando especifica la propiedad de la línea de comandos CCMSetup **/source:&lt;Ruta\>** .|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Puertos que se utilizan con la instalación manual y la instalación basada en script de inicio de sesión  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB) entre el equipo cliente y un recurso compartido de red desde el que se ejecuta CCMSetup.exe.<br /><br /> Cuando instala Configuration Manager, los archivos de origen de la instalación del cliente se copian y se comparten de forma automática desde la carpeta *&lt;RutaDeInstalación\>* \Client en los puntos de administración. Sin embargo, puede copiar estos archivos y crear un nuevo recurso compartido en cualquier equipo de la red. Como alternativa, puede eliminar este tráfico de red ejecutando CCMSetup.exe localmente, por ejemplo, mediante el uso de medios extraíbles.|--|445|  
|Protocolo de transferencia de hipertexto (HTTP) desde el equipo cliente a un punto de administración cuando la conexión es a través de HTTP y no se especifica la propiedad de la línea de comandos CCMSetup **/source:&lt;Ruta\>** .|--|80 (Véase la nota 1, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS) desde el equipo cliente a un punto de administración cuando la conexión es a través de HTTPS y no se especifica la propiedad de la línea de comandos CCMSetup **/source:&lt;Ruta\>** .|--|443 (véase la nota 1, **Puerto alternativo disponible**)|  
|Bloque de mensajes del servidor (SMB) entre el servidor de origen y el equipo cliente cuando especifica la propiedad de la línea de comandos CCMSetup **/source:&lt;Ruta\>** .|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Puertos que se utilizan con la instalación basada la distribución de software  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB) entre el punto de distribución y el equipo cliente.|--|445|  
|Protocolo de transferencia de hipertexto (HTTP) desde el cliente a un punto de distribución cuando la conexión es a través de HTTP.|--|80 (Véase la nota 1, **Puerto alternativo disponible**)|  
|Protocolo seguro de transferencia de hipertexto (HTTPS) desde el cliente a un punto de distribución cuando la conexión es a través de HTTPS.|--|443 (véase la nota 1, **Puerto alternativo disponible**)|  

## <a name="notes"></a>Notas  
 **1 Puerto alternativo disponible** En Configuration Manager, puede definir un puerto alternativo para este valor. Si se definió un puerto personalizado, sustituya ese puerto personalizado cuando defina la información del filtro IP para las directivas IPsec o para configurar firewalls.  

 **2 Windows Server Update Services** Puede instalar Windows Server Update Service (WSUS) tanto en el sitio web predeterminado (puerto 80) como en un sitio web personalizado (puerto 8530).  

 Después de la instalación, puede cambiar el puerto. No es necesario utilizar el mismo número de puerto en toda la jerarquía del sitio.  

 Si el puerto HTTP es 80, el puerto HTTPS debe ser 443.  

 Si el puerto HTTP es cualquier otro, el puerto HTTPS debe ser 1 valor mayor. Por ejemplo, 8530 y 8531.
