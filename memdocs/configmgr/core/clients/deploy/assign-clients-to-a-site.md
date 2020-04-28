---
title: Asignación de clientes a un sitio
titleSuffix: Configuration Manager
description: Asigne clientes a un sitio en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2270435ac13585cb0b7d3271f1faa02cc728d3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075751"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Cómo asignar clientes a un sitio en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de instalar un cliente de Configuration Manager, este debe unirse a un sitio primario de Configuration Manager para poder administrarlo. El sitio al que se une un cliente se denomina su *sitio asignado*. Los clientes no se pueden asignar a un sitio de administración central o a un sitio secundario.  

El proceso de asignación tiene lugar una vez que el cliente está instalado correctamente y permite determinar qué sitio administra el equipo cliente. Puede asignar directamente el cliente a un sitio o puede usar la asignación de sitio automática, que consiste en que el cliente busca automáticamente un sitio adecuado en función de su ubicación de red actual o un sitio de reserva configurado para la jerarquía.

Cuando instala el cliente de dispositivo móvil durante la inscripción de Configuration Manager, el dispositivo siempre se asigna automáticamente a un sitio. Cuando instala el cliente en un equipo, puede decidir si quiere asignar o no el cliente a un sitio. Sin embargo, si el cliente está instalado pero no asignado, el cliente no se administra hasta que se realiza correctamente la asignación de sitio.  
 

> [!NOTE]  
>  Asigne siempre clientes a sitios que ejecutan la misma versión de Configuration Manager. Evite asignar un cliente de Configuration Manager de una versión más reciente a un sitio de una versión anterior.   Si es necesario, actualice el sitio primario a la misma versión de Configuration Manager que está usando para los clientes.  

Una vez que el cliente se asigna a un sitio, permanece asignado a ese sitio aunque cambie su dirección IP y se desplace a otro sitio. Solo un administrador puede asignar manualmente el cliente a otro sitio o quitar la asignación del cliente.  

> [!WARNING]  
>  Se presenta una excepción a la asignación permanente de un cliente a un sitio si se asigna el cliente de un dispositivo de Windows Embedded cuando están habilitados los filtros de escritura. Si en primer lugar no se deshabilitan los filtros de escritura antes de asignar el cliente, el estado de asignación de sitio del cliente vuelve a su estado original con el siguiente reinicio del dispositivo.  
>   
>  Por ejemplo, si el cliente está configurado para la asignación de sitio automática, se reasignará durante el inicio y podría ser asignado a un sitio diferente. Si el cliente no está configurado para la asignación de sitio automática sino que requiere la asignación de sitio manual, se debe reasignar manualmente después del inicio para poder administrarlo de nuevo mediante Configuration Manager.  
>   
>  Para evitar este comportamiento, deshabilite los filtros de escritura antes de asignar el cliente de los dispositivos incrustados, y, a continuación, habilite los filtros de escritura después de comprobar que la asignación de sitio se realizó correctamente.  

Si se produce un error en la asignación del cliente, el software cliente permanece instalado, pero no se administrará. Se considera que un cliente no está administrado cuando está instalado pero no está asignado a un sitio, o está asignado a un sitio pero no se puede comunicar con un punto de administración.  

##  <a name="using-manual-site-assignment-for-computers"></a>Uso de la asignación de sitio manual para los equipos  
 Puede asignar manualmente los equipos cliente a un sitio mediante los dos métodos siguientes:  

-   Utilice una propiedad de instalación de cliente que especifique el código de sitio.  

-   En el panel de control, en **Configuration Manager**, especifique el código del sitio.  

> [!NOTE]  
>  Si asigna manualmente un equipo cliente a un código de sitio de Configuration Manager que no existe, se produce un error en la asignación de sitio.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a> Uso de la asignación de sitio automática para los equipos  
 La asignación de sitio automática puede tener lugar durante la implementación del cliente, o cuando se hace clic en **Buscar sitio** en la pestaña **Avanzadas** de **Propiedades de Configuration Manager** en el panel de control. El cliente de Configuration Manager compara su propia ubicación de red con los límites configurados en la jerarquía de Configuration Manager. Cuando la ubicación de red del cliente está dentro de un grupo de límites habilitado para la asignación de sitio, o la jerarquía está configurada para un sitio de reserva, el cliente se asigna automáticamente a ese sitio sin tener que especificar un código de sitio.  

 Puede configurar los límites mediante una o varias de las opciones siguientes:  

-   Subred IP  

-   Sitio de Active Directory  

-   Prefijo IPv6  

-   Intervalo de direcciones IP  

> [!NOTE]  
>  Si un cliente de Configuration Manager tiene varios adaptadores de red y, por tanto, tiene varias direcciones IP, la dirección IP usada para evaluar la asignación de sitio del cliente se asigna de manera aleatoria.  

 Para más información sobre cómo configurar grupos de límites para la asignación de sitio y cómo configurar un sitio de reserva para la asignación de sitio automática, vea [Definir límites de sitio y grupos de límites para Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Los clientes de Configuration Manager que usan la asignación de sitio automática intentan encontrar grupos de límites de sitio que están publicados en Active Directory Domain Services. Si esto produce un error (por ejemplo, el esquema de Active Directory no se extiende para Configuration Manager o los clientes son equipos de grupo de trabajo), los clientes pueden obtener la información de grupos de límites desde un punto de administración.  

 Se puede especificar un punto de administración para que lo utilicen los equipos cliente cuando están instalados, o los clientes pueden buscar un punto de administración mediante el uso de la publicación en DNS o WINS.  

 Si el cliente no encuentra un sitio asociado a un grupo de límites que contenga su ubicación de red y la jerarquía no tiene un sitio de reserva, el cliente lo vuelve a intentar cada 10 minutos hasta que puede asignarse a un sitio.  

 Los equipos cliente de Configuration Manager no se pueden asignar automáticamente a un sitio si se aplica cualquiera de las siguientes condiciones, y deberán por tanto asignarse manualmente:  

-   Ya están asignados a un sitio.  

-   Están en Internet o están configurados como clientes solo de Internet.  

-   Su ubicación de red no está dentro de uno de los grupos de límites configurados en la jerarquía de Configuration Manager y no hay ningún sitio de reserva para la jerarquía.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Finalización de la asignación de sitio mediante la comprobación de compatibilidad de sitio  
 Una vez que un cliente encuentra su sitio asignado, se comprueban la versión y el sistema operativo del cliente para garantizar que pueda administrarlo un sitio de Configuration Manager. Por ejemplo, Configuration Manager no puede administrar clientes de Configuration Manager 2007, de System Center 2012 Configuration Manager ni clientes con Windows 2000.  

 La asignación de sitio produce un error si asigna un cliente que ejecuta Windows 2000 a un sitio de Configuration Manager. Cuando asigna un cliente de Configuration Manager 2007 o de System Center 2012 Configuration Manager a un sitio de Configuration Manager (rama actual), la asignación de sitio se realiza correctamente para admitir la actualización de cliente automática. Pero hasta que se actualizan los clientes de la generación anterior a un cliente de Configuration Manager (rama actual), este no puede administrar este cliente mediante la configuración de cliente, las aplicaciones o las actualizaciones de software.  

> [!NOTE]  
>  Para admitir la asignación de sitio de un cliente de Configuration Manager 2007 o System Center 2012 Configuration Manager a un sitio de Configuration Manager (rama actual), debe configurar la actualización automática de cliente para la jerarquía. Para más información, vea [Cómo actualizar clientes para equipos Windows](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Configuration Manager también comprueba que se ha asignado el cliente de Configuration Manager (rama actual) a un sitio compatible. Los escenarios siguientes podrían tener lugar durante la migración desde versiones anteriores de Configuration Manager.  

- Escenario: ha usado la asignación de sitio automática y los límites se superponen con los límites definidos en una versión anterior de Configuration Manager.  

   En este caso, el cliente intenta buscar automáticamente un sitio de Configuration Manager (rama actual).  

   El cliente comprueba en primer lugar Active Directory Domain Services y si encuentra un sitio de Configuration Manager (rama actual) publicado, la asignación de sitio se realiza correctamente. Si esto produce un error (por ejemplo, el sitio de Configuration Manager no está publicado o el equipo es un cliente de grupo de trabajo), el cliente comprobará la información de sitio desde su punto de administración asignado.  

  > [!NOTE]  
  >  Puede asignar un punto de administración al cliente durante la instalación del cliente mediante la propiedad de Client.msi **SMSMP=&lt;nombre_servidor>** .  

   Si no se puede utilizar ninguno de los dos métodos, no se puede llevar a cabo la asignación de sitio y se debe asignar manualmente el cliente.  

- Escenario: se ha asignado el cliente de Configuration Manager (rama actual) mediante el uso de un código de sitio específico en lugar de la asignación de sitio automática, y se ha especificado erróneamente un código de sitio para una versión de Configuration Manager anterior a System Center 2012 R2 Configuration Manager.  

   En este caso, no se puede llevar a cabo la asignación de sitio y se debe reasignar manualmente el cliente a un sitio de Configuration Manager (rama actual).  

  La comprobación de compatibilidad de sitio requiere el cumplimiento de una de las siguientes condiciones:  

- El cliente puede acceder a la información de sitio publicada en Servicios de dominio de Active Directory.  

- El cliente se puede comunicar con un punto de administración del sitio.  

  Si la comprobación de compatibilidad de sitio no finaliza correctamente, no se puede realizar la asignación de sitio y el cliente permanece sin administrar hasta que la comprobación de compatibilidad de sitio finalice correctamente cuando se vuelva a ejecutar.  

  Como excepción, la comprobación de compatibilidad de sitio no se lleva a cabo cuando un cliente está configurado para un punto de administración basado en Internet. En este caso, no se realiza ninguna comprobación de compatibilidad de sitio. Si va a asignar clientes a un sitio que contiene sistemas de sitio basados en Internet y especifica un punto de administración basado en Internet, asegúrese de que asigna el cliente al sitio correcto. Si asigna erróneamente el cliente a un sitio de Configuration Manager 2007, System Center 2012 Configuration Manager o a un sitio de Configuration Manager sin roles de sistema de sitio basados en Internet, el cliente no se administrará.  

##  <a name="locating-management-points"></a>Búsqueda de puntos de administración  
 Un cliente, una vez asignado correctamente a un sitio, busca un punto de administración en el sitio.  

 Los equipos cliente descargan una lista de puntos de administración a los que se pueden conectar en el sitio. Esto sucede siempre que se reinicia el cliente, o cada 25 horas o si el cliente detecta un cambio de red, como por ejemplo si el equipo se desconecta y se vuelve a conectar en la red o si recibe una nueva dirección IP. La lista incluye los puntos de administración de la intranet y si aceptan o no las conexiones de cliente a través de HTTP o HTTPS. Cuando el equipo cliente está en Internet y el cliente no tiene todavía una lista de puntos de administración, se conecta al punto de administración basado en Internet especificado para obtener una lista de puntos de administración. Cuando el cliente tiene una lista de puntos de administración para su sitio asignado, selecciona uno al que conectarse:  

-   Cuando el cliente está en la intranet y tiene un certificado PKI válido que puede utilizar, el cliente elige los puntos de administración de HTTPS antes que los puntos de administración de HTTP. A continuación, busca el punto de administración más cercano en función de su pertenencia al bosque.  

-   Cuando el cliente está en Internet, elige de manera aleatoria uno de los puntos de administración basados en Internet.  

Los clientes de dispositivos móviles inscritos por Configuration Manager solo se conectan a un punto de administración de su sitio asignado y nunca a los puntos de administración de los sitios secundarios. Estos clientes siempre se conectan a través de HTTPS y el punto de administración debe estar configurado para aceptar conexiones de cliente a través de Internet. Cuando hay más de un punto de administración para los clientes de dispositivos móviles en el sitio primario, Configuration Manager elige de manera aleatoria uno de estos puntos de administración durante la asignación y el cliente de dispositivo móvil sigue usando el mismo punto de administración.  

Si el cliente descargó la directiva de cliente desde un punto de administración del sitio, el cliente será un cliente administrado.  

##  <a name="downloading-site-settings"></a>Descarga de la configuración de sitio  
 Una vez realizada correctamente la asignación de sitio, y si el cliente encontró un punto de administración, un equipo cliente que utiliza Servicios de dominio de Active Directory para la comprobación de compatibilidad de sitio descarga la configuración de sitio relacionada con el cliente para su sitio asignado. Esta configuración incluye los criterios de selección de certificados de cliente, si se debe utilizar o no una lista de revocación de certificados y los números de puerto de solicitud de cliente. El cliente seguirá comprobando la configuración de forma periódica.  

 Cuando los equipos cliente no pueden obtener la configuración de sitio en Servicios de dominio de Active Directory, la descargan desde su punto de administración. Los equipos cliente también pueden obtener la configuración de sitio cuando se instalan mediante la inserción de cliente, o puede especificarlos manualmente mediante las propiedades de instalación de cliente y CCMSetup.exe. Para más información sobre las propiedades de instalación de clientes, vea [Acerca de las propiedades de instalación de clientes](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>Descarga de la configuración de cliente  
 Todos los clientes descargan la directiva de configuración de cliente predeterminada y cualquier directiva de configuración de cliente personalizada que corresponda. El Centro de software se basa en estas directivas de configuración de cliente para equipos Windows y notificará a los usuarios que el Centro de Software no se puede ejecutar correctamente hasta que se descarga esta información de configuración. En función de la configuración de cliente que se configure, la descarga inicial de la configuración de cliente podría llevar algún tiempo, y es posible que algunas tareas de administración de cliente no se ejecuten mientras no se complete el proceso.  

##  <a name="verifying-site-assignment"></a>Comprobación de asignación de sitio  
 Puede comprobar si la asignación de sitio se ha realizado correctamente mediante uno de los siguientes métodos:  

-   En los clientes de equipos Windows, use Configuration Manager en el Panel de control para comprobar que el código de sitio se muestra correctamente en la pestaña **Sitio**.  

-   En equipos cliente, en el área de trabajo **Activos y compatibilidad** > nodo **Dispositivos**, compruebe que el equipo muestra **Sí** en la columna **Cliente** y el código de sitio primario correcto en la columna **Código de sitio**.  

-   En clientes de dispositivo móvil, en el área de trabajo **Activos y compatibilidad** , use la recopilación **Todos los dispositivos móviles** para comprobar que el dispositivo móvil muestra **Sí** en la columna **Cliente** y el código de sitio primario correcto en la columna **Código de sitio** .  

-   Use los informes para la asignación de clientes y la inscripción de dispositivos móviles.  

-   Para equipos cliente, use el archivo LocationServices.log en el cliente.  

##  <a name="roaming-to-other-sites"></a>Desplazamiento a otros sitios  
 Cuando los equipos cliente en la intranet se asignan a un sitio primario pero su ubicación de red cambia y pasa a figurar en un grupo de límites configurado para otro sitio, se han movido a otro sitio. Si este sitio es un sitio secundario de su sitio asignado, los clientes pueden usar un punto de administración en el sitio secundario para descargar directivas de cliente y cargar datos de cliente para evitar el envío de datos a través de una red potencialmente lenta. Sin embargo, si los clientes se mueven hasta los límites de otro sitio primario o de un secundario que no es un sitio secundario de su sitio asignado, estos clientes siempre usan un punto de administración en su sitio asignado para descargar directivas de cliente y cargar datos en su sitio.  

 Estos equipos cliente que se desplazan a otros sitios (todos los sitios primarios y secundarios) siempre pueden usar puntos de administración en otros sitios para solicitudes de ubicación de contenido. Los puntos de administración en el sitio actual pueden dar a los clientes una lista de puntos de distribución que tienen el contenido que los clientes solicitan.  

 En los equipos cliente configurados para la administración de cliente solo a través de Internet y en los equipos y dispositivos móviles Mac inscritos mediante Configuration Manager, estos clientes solo se comunican con puntos de administración de su sitio asignado. Estos clientes nunca se comunican con puntos de administración en sitios secundarios o con puntos de administración en otros sitios primarios.  
