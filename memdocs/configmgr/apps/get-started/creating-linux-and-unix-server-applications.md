---
title: Creación de aplicaciones de servidor Linux y Unix
titleSuffix: Configuration Manager
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos Linux y UNIX.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3f5d0cfb930e6d1b8cf4cd6dfb0eabfa38ddab16
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075802"
---
# <a name="create-linux-and-unix-server-applications-with-configuration-manager"></a>Creación de aplicaciones de servidor Linux y UNIX con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> A partir de la versión 1902, Configuration Manager no admite clientes Linux o UNIX. 
> 
> Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

Tenga en cuenta lo siguiente cuando cree e implemente aplicaciones para equipos que ejecutan Linux y UNIX.  

## <a name="general-considerations"></a>Consideraciones generales  
 El cliente de Configuration Manager para Linux y UNIX admite **implementaciones de software que usan paquetes y programas**. No se puede implementar aplicaciones de Configuration Manager en equipos que ejecutan Linux y UNIX.  

 Las funcionalidades de implementación de software de UNIX y Linux incluyen:  

-   Instalación del software para servidores de Linux y UNIX, incluidas las siguientes funcionalidades:  

    -   Nueva implementación de software  

    -   Actualizaciones de software para los programas ya existentes en un equipo  

    -   Revisiones del sistema operativo  

-   Comandos nativos de Linux y UNIX y scripts que se encuentran en servidores Linux y UNIX  

-   Implementaciones que están limitadas a los sistemas operativos que especifica cuando selecciona la opción de programa **Solo en plataformas cliente especificadas**

-   Ventanas de mantenimiento para controlar el momento en que se instala el software

-   Mensajes de estado de implementación para supervisar las implementaciones  

-   La opción de que el cliente limite el uso de la red al descargar el software desde un punto de distribución  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Diferencias entre la implementación en equipos de Linux y UNIX y la implementación en dispositivos de Windows
Las principales diferencias entre implementar paquetes y programas en equipos Linux y UNIX e implementar paquetes y programas en dispositivos Windows son las siguientes:  

|Configuración|Detalles|  
|-------------------|-------------|  
|Utilice solo configuraciones diseñadas específicamente para equipos y no las diseñadas para usuarios.|El cliente de Configuration Manager para Linux y UNIX no es compatible con configuraciones diseñadas para usuarios.|  
|Configure los programas para descargar el software desde el punto de distribución y ejecutar los programas desde la caché del cliente local.|El cliente de Configuration Manager para Linux y UNIX no es compatible con software que se ejecute desde el punto de distribución. En cambio, la configuración debe especificar que el software se descargue en el cliente y, a continuación, se instale.<br /><br /> De forma predeterminada, después de que el cliente para Linux y UNIX instala el software, el software se elimina de la caché del cliente. No obstante, los paquetes cuya configuración indica **Conservar contenido en la memoria caché del cliente** no se eliminan del cliente y permanecen en su caché después de la instalación del software.<br /><br /> El cliente para Linux y UNIX no es compatible con configuraciones para la caché del cliente y el tamaño máximo de la memoria caché del cliente está limitada solo por el espacio libre en disco que tenga el equipo cliente.|  
|Configurar la cuenta de acceso de red para acceso al punto de distribución|Los equipos Linux y UNIX están diseñados para ser equipos de grupo de trabajo. Para tener acceso a los paquetes del punto de distribución en el dominio del servidor de sitio de Configuration Manager, debe configurar la cuenta de acceso de red para el sitio. Debe especificar esta cuenta como una propiedad de componente de distribución de software y debe configurar la cuenta antes de implementar software.<br /><br /> Puede configurar varias cuentas de acceso de red en cada sitio. El cliente para Linux y UNIX puede utilizar cada una de las cuentas que se configuran como una cuenta de acceso de red.<br /><br /> Para más información, consulte [Componentes de sitio para Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 Puede implementar paquetes y programas en recopilaciones que contienen solo clientes Linux o UNIX, o puede implementarlos en recopilaciones que contienen una mezcla de tipos de clientes, tales como la **Recopilación de todos los sistemas**. Sin embargo, los clientes que no sean Linux o UNIX no instalarán el software o notificarán un error.  

 Cuando el cliente de Configuration Manager para Linux y UNIX recibe y ejecuta una implementación, genera mensajes de estado. Puede ver estos mensajes de estado en la consola de Configuration Manager o mediante informes que permitan supervisar el estado de implementación.  

 Para obtener información sobre cómo usar paquetes y programas, consulte [Packages and programs](../../apps/deploy-use/packages-and-programs.md) (Paquetes y programas).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Configurar paquetes, programas e implementaciones para servidores Linux y UNIX  
 Puede crear e implementar paquetes y programas mediante las opciones que están disponibles de manera predeterminada en la consola de Configuration Manager. El cliente no requiere ninguna configuración única.  

 Utilice la información que se brinda en las secciones siguientes para configurar los paquetes y programas, así como las implementaciones.  

### <a name="packages-and-programs"></a>Paquetes y programas  
 Para crear un paquete y un programa para un servidor Linux o UNIX, use el **Asistente para crear paquetes y programas** de la consola de Configuration Manager. El cliente para Linux y UNIX es compatible con la mayoría de las configuraciones de paquete y programa. Sin embargo, hay varias opciones de configuración que no se admiten. Al crear o configurar un paquete y un programa, tenga en cuenta los siguientes puntos:  

-   Incluya los tipos de archivo que son compatibles con los equipos de destino.  

-   Defina las líneas de comandos que son adecuadas para utilizar en el equipo de destino.  

-   Tenga en cuenta que no se admiten las configuraciones que interactúan con los usuarios.  

La tabla siguiente enumera las propiedades de los paquetes y programas que no son compatibles:  

|Propiedad de paquete y programa|Comportamiento|Más información|  
|----------------------------------|--------------|----------------------|  
|Configuración de recurso compartido de paquete:<br /><br /> - Todas las opciones|Se genera un error y se produce un error en la instalación de software|El cliente no admite esta configuración. En cambio, el cliente debe descargar el software mediante HTTP o HTTPS y, a continuación, ejecutar la línea de comandos desde su caché local.|  
|Configuración de la actualización de paquete:<br /><br /> - Desconectar usuarios de los puntos de distribución|Se omite la configuración|El cliente no admite esta configuración.|  
|Configuración de implementación de sistema operativo:<br /><br /> - Todas las opciones|Se omite la configuración|El cliente no admite esta configuración.|  
|Generación de informes:<br /><br /> - Usar las propiedades del paquete para la coincidencia de MIF de estado<br /><br /> - Usar estos campos para la coincidencia de MIF de estado|Se omite la configuración|El cliente no admite el uso de archivos MIF de estado.|  
|**Ejecutar**:<br /><br /> - Todas las opciones|Se omite la configuración|El cliente siempre ejecuta los paquetes sin la interfaz de usuario.<br /><br /> El cliente omite todas las opciones de configuración relacionadas con la ejecución.|  
|Tras ejecutar:<br /><br />Configuration Manager reinicia el equipo<br /><br /> - El programa controla el reinicio<br /><br /> - Configuration Manager cierra la sesión del usuario|Se genera un error y se produce un error en la instalación de software|No se admiten las opciones de configuración específicas del usuario ni las relacionadas con el reinicio del sistema.<br /><br /> Cuando se está usando cualquier opción de configuración diferente de **Ninguna acción requerida** , el cliente genera un error y continúa con la instalación de software sin realizar ninguna acción.|  
|El programa se puede ejecutar:<br /><br /> - Solo cuando un usuario haya iniciado sesión|Se genera un error y se produce un error en la instalación de software|No se admiten las opciones de configuración específicas del usuario.<br /><br /> Cuando se configura esta opción, el cliente genera un error y se produce un error de la instalación de software.<br /><br /> Se omiten otras opciones y se continúa la instalación de software.|  
|Modo de ejecución:<br /><br /> - Ejecutar con derechos de usuario|Se omite la configuración|No se admiten las opciones de configuración específicas del usuario.<br /><br /> Sin embargo, el cliente admite la configuración que especifica la ejecución con derechos administrativos.<br /><br /> Cuando se especifica **Ejecutar con derechos administrativos**, el cliente de Configuration Manager emplea sus credenciales raíz.<br /><br /> Esta configuración no genera un error ni una entrada de registro. En cambio, la instalación de software produce un error cuando el cliente genera un error para la configuración de requisitos previos para **El programa se puede ejecutar** = **Solo cuando un usuario haya iniciado sesión**.|  
|Permitir a los usuarios ver la instalación del programa e interactuar con la misma|Se omite la configuración|No se admiten las opciones de configuración específicas del usuario.<br /><br /> Se omite esta configuración y se continúa la instalación de software.|  
|Modo de unidad:<br /><br /> - Todas las opciones|Se omite la configuración|Esta configuración no se admite porque el contenido siempre se descarga al cliente y se ejecuta de forma local.|  
|Ejecutar otro programa primero|Se genera un error y se produce un error en la instalación de software|No se admite la instalación de programa recurrente.<br /><br /> Cuando un programa está configurado para ejecutar otro programa en primer lugar, se produce un error en la instalación de software, y no se inicia la instalación del otro programa.|  
|Cuando este programa se asigne a un equipo:<br /><br /> - Ejecutar una vez para cada usuario que inicie sesión|Se omite la configuración|No se admiten las opciones de configuración específicas del usuario.<br /><br /> Sin embargo, el cliente es compatible con la configuración que especifica la ejecución una vez para el equipo.<br /><br /> Esta configuración no genera un error ni una entrada de registro porque ya se crearon un error y una entrada de registro para la configuración de requisitos previos relacionados con **El programa se puede ejecutar** = **Solo cuando un usuario haya iniciado sesión**.|  
|Suprimir notificaciones de programa|Se omite la configuración|El cliente no implementa una interfaz de usuario.<br /><br /> Cuando se selecciona esta configuración, se omite y continúa la instalación de software.|  
|Deshabilitar este programa en equipos en los que esté implementado|Se omite la configuración|Esta configuración no se admite y no afecta a la instalación de software.|  
|Permitir que este programa se instale desde la secuencia de tareas de instalación de paquete sin implementarse||El cliente no admite secuencias de tareas.<br /><br /> Esta configuración no se admite y no afecta a la instalación de software.|  
|Windows Installer:<br /><br /> - Todas las opciones|Se omite la configuración|El cliente no admite opciones de configuración ni archivos de Windows Installer.|  
|Modo de mantenimiento de Operations Manager:<br /><br /> - Todas las opciones|Se omite la configuración|El cliente no admite esta configuración.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Implementar software en un servidor de Linux o UNIX
 Para implementar software en un servidor Linux o UNIX mediante un paquete y un programa, puede usar el **Asistente para implementar software** de la consola de Configuration Manager. El cliente admite la mayoría de las opciones de configuración de implementación para Linux y UNIX. Sin embargo, hay varias opciones de configuración que no se admiten. Al implementar software, considere los puntos siguientes:  

- Aprovisione el paquete en, al menos, un punto de distribución que esté asociado a un grupo de límites configurado para la ubicación de contenido.  

- El cliente para Linux y UNIX que recibe esta implementación debe poder acceder a este punto de distribución desde su ubicación de red.  

- El cliente para Linux y UNIX descarga el paquete desde el punto de distribución y ejecuta el programa en el equipo local.  

- El cliente para Linux y UNIX no puede descargar paquetes desde carpetas compartidas. Descarga paquetes desde puntos de distribución con IIS habilitado que admiten HTTP o HTTPS.  

  En la tabla siguiente se enumeran las propiedades de las implementaciones que no son compatibles:  

|Propiedad de la implementación|Comportamiento|Más información|  
|-------------------------|--------------|----------------------|  
|Configuración de implementación – propósito:<br /><br /> - Disponible<br /><br /> - Requerido|Se omite la configuración|No se admiten las opciones de configuración específicas del usuario.<br /><br /> No obstante, el cliente admite la opción de configuración **Requerido**, la cual hace cumplir la hora de instalación programada, pero no admite la instalación manual antes de esa hora programada.|  
|Enviar paquetes de reactivación|Se omite la configuración|El cliente no admite esta configuración.|  
|Programación de asignación:<br /><br /> - iniciar sesión<br /><br /> - cerrar sesión|Se genera un error y se produce un error en la instalación de software|No se admiten las opciones de configuración específicas del usuario.<br /><br /> Sin embargo, el cliente admite la configuración **Lo antes posible**.|  
|Configuración de notificaciones:<br /><br /> - Permitir que los usuarios ejecuten el programa independientemente de las asignaciones|Se omite la configuración|El cliente no implementa una interfaz de usuario.|  
|Cuando se alcance la hora de asignación programada, permitir que se realicen las siguientes actividades fuera de la ventana de mantenimiento:<br /><br /> - Reinicio del sistema (si es necesario para completar la instalación)|Se genera un error|El cliente no admite el reinicio del sistema.|  
|Opción de implementación para redes (LAN) rápidas:<br /><br /> - Ejecutar programa desde el punto de distribución|Se genera un error y se produce un error en la instalación de software|El cliente no puede ejecutar el software desde el punto de distribución y, en cambio, debe descargar el programa para que pueda ejecutarse.|  
|Opción de implementación para un límite de red lenta o no fiable, o una ubicación de origen de reserva para contenido:<br /><br /> - Permitir a los clientes compartir el contenido con otros clientes en la misma subred|Se omite la configuración|El cliente no admite compartir contenido dentro del mismo nivel.|  

 Para más información sobre la ubicación de contenido, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Para obtener más información sobre cómo crear una implementación, consulte [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implementar aplicaciones).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a>Administrar el ancho de banda de red para las descargas de software de puntos de distribución  
 El cliente de Linux y UNIX admite controles de ancho de banda de red cuando descarga software de un punto de distribución.  

 El cliente usa la configuración de Servicio de transferencia inteligente en segundo plano (Background Intelligent Transfer, BITS) que se establece como configuración del cliente en Configuration Manager, pero no implementa BITS. En su lugar, para limitar el uso de ancho de banda de red, el cliente controla el tamaño del fragmento de la solicitud HTTP y el retraso entre fragmentos para descargar el software.  

 Para configurar un cliente para que use controles de ancho de banda de red, puede establecer la configuración del cliente para **Transferencia inteligente en segundo plano** y después aplicar la configuración al equipo cliente. Para utilizar controles de ancho de banda, el cliente debe recibir la configuración del cliente para **Transferencia inteligente en segundo plano** con la siguiente configuración establecida en **Sí**:  

- **Limitar el ancho de banda de red máximo para transferencias BITS en segundo plano**  

  El cliente admite las siguientes configuraciones para la transferencia inteligente en segundo plano:  

  -   **Hora de inicio de período de limitación**  

  -   **Hora de finalización del período de limitación**  

  -   **Velocidad de transferencia máxima durante el período de limitación (Kbps)**  

  -   **Velocidad de transferencia máxima fuera del período de limitación (Kbps)**  

No se admite la siguiente configuración de transferencia inteligente en segundo plano y el cliente la omite para Linux y UNIX:  

- **Permitir descargas de BITS fuera del período de limitación**  

  Si se interrumpe la descarga del software al cliente desde un punto de distribución, el cliente para Linux y UNIX no reanuda la descarga. En su lugar, reinicia la descarga de todos el paquete de software.  

##  <a name="configure-operations-for-software-deployments"></a>Configurar operaciones para las implementaciones de software  
 De manera similar al cliente de Windows, el cliente de Configuration Manager para Linux y UNIX detecta las implementaciones de nuevo software al sondear y comprobar si hay nuevas directivas. La frecuencia con que el cliente comprueba si hay nuevas directivas depende de la configuración del cliente. Puede configurar ventanas de mantenimiento para controlar el momento en que se producen las implementaciones de software.  

 Puede configurar las implementaciones de software para servidores Linux y UNIX mediante el uso de propiedades de paquete, propiedades de programa y propiedades de implementación.  

 Cuando el cliente recibe la directiva para una implementación, envía un mensaje de estado. También envía mensajes de estado cuando se inicia la instalación de software y cuando la instalación finaliza, o se produce un error.  

 Los programas para implementaciones de software se ejecutan con las mismas credenciales raíz con que se ejecuta el cliente de Configuration Manager para Linux y UNIX. Se utiliza el código de salida del comando de programa para determinar si la operación se realizó correctamente o no. Un código de salida igual a 0 (cero) significa que el proceso se realizó correctamente. Además, se copian **stdout** (secuencia de salida estándar) y **stderr** (secuencia de error estándar) al archivo de registro cuando el nivel de registro se establece en INFO o TRACE.  

> [!TIP]  
>  Si el software que desea implementar está ubicado en un recurso compartido de Network File System (NFS) al que el servidor Linux o UNIX tiene acceso, no necesita usar un punto de distribución para descargar el paquete. En cambio, cuando cree el paquete, no active la casilla **Este paquete contiene archivos de origen**. Luego, cuando configure el programa, especifique la línea de comandos adecuada para tener acceso directo al paquete en el punto de montaje NFS.  
