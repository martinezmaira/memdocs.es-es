---
title: Reactivación de clientes
titleSuffix: Configuration Manager
description: Planee la reactivación de clientes en Configuration Manager mediante Wake On LAN (WOL).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feea1cdea52b76b900497e84eea210444535fcd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693773"
---
# <a name="plan-how-to-wake-up-clients-in-configuration-manager"></a>Planeación de la reactivación de clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

 Configuration Manager admite paquetes de reactivación tradicionales para reactivar equipos en modo de suspensión si desea instalar software requerido, como actualizaciones de software y aplicaciones.

> [!NOTE]
> En este artículo se describe cómo funciona una versión anterior de Wake on LAN. Esta funcionalidad sigue existiendo en la versión 1810 de Configuration Manager, que también incluye una versión más reciente de Wake on LAN. Ambas versiones de Wake on LAN se pueden habilitar de manera simultánea y en muchos casos será así. Para más información sobre cómo funciona la versión nueva de Wake on LAN a partir de la versión 1810 y cómo permitir ambas de las versiones o alguna de ellas, consulte [Configurar Wake on LAN](../configure-wake-on-lan.md).  

## <a name="how-to-wake-up-clients-in-configuration-manager"></a>Cómo reactivar clientes en Configuration Manager

 Configuration Manager admite paquetes de reactivación tradicionales para reactivar equipos en modo de suspensión si desea instalar software requerido, como actualizaciones de software y aplicaciones.  

Puede complementar el método de los paquetes de reactivación tradicionales mediante la configuración del cliente proxy de reactivación. El proxy de reactivación usa un protocolo punto a punto y equipos elegidos para comprobar si otros equipos de la subred están activados y, si no es así, reactivarlos en caso necesario. Si el sitio está configurado para Wake On LAN y los clientes están configurados para el proxy de reactivación, el proceso funciona del siguiente modo:  

1. Los equipos que tengan instalado el cliente de Configuration Manager que no estén inactivos en la subred comprueban si los demás equipos de la subred están activos. Realizan esta comprobación enviando entre sí un comando ping de TCP/IP cada cinco segundos.  

2. Si no hay respuesta desde los demás equipos, se asume que están en modo de suspensión. Los equipos que están activos se convierten en el *equipo administrador* de la subred.  

    Dado que es posible que un equipo no responda por un motivo distinto a estar inactivo (por ejemplo, si está apagado o fuera de la red o si ya no se aplica la configuración del cliente proxy de activación), se enviará a los equipos un paquete de reactivación cada día a las 2:00 p.m. (hora local). Dejará de suponerse que los equipos que no responden están inactivos, y no se reactivarán mediante el proxy de reactivación.  

    Para admitir el proxy de reactivación, es necesario que al menos tres equipos estén activos para cada subred. Para conseguir este requisito, se eligen tres equipos de manera no determinista para que sean los *equipos guardianes* para la subred. Este estado significa que permanecerán activos, independientemente de la directiva de energía que tengan configurada para que entren en modo de suspensión o hibernación después de un determinado período de inactividad. Los equipos guardianes obedecen los comandos de apagado o reinicio, por ejemplo, resultantes de las tareas de mantenimiento. Si esta acción ocurre, los demás equipos guardianes activan a otros equipos de la subred para que esta siga teniendo tres equipos guardianes.  

3. Los equipos administradores piden al conmutador de la red que redirija el tráfico de red para los equipos inactivos a ellos mismos.  

    La redirección se consigue mediante la difusión por parte del equipo administrador de una trama Ethernet que utiliza la dirección MAC del equipo inactivo como dirección de origen. Este comportamiento hace que el conmutador de red se comporte como si el equipo inactivo se hubiera movido al mismo puerto en el que se encuentra el equipo administrador. El equipo administrador también envía paquetes ARP para que los equipos inactivos conserven la capacidad de admitir entradas en la memoria caché de ARP. El equipo administrador también responde a las solicitudes ARP en nombre del equipo inactivo y responde con la dirección MAC del equipo inactivo.  

   > [!WARNING]  
   >  Durante este proceso, la asignación de IP a MAC del equipo inactivo seguirá siendo la misma. El proxy de reactivación funciona informando al conmutador de red de que un adaptador de red diferente utiliza el puerto que fue registrado por otro adaptador de red. Sin embargo, este comportamiento (conocido como solapa de MAC) es poco común para el funcionamiento de redes estándar. Algunas herramientas de supervisión de red buscan este comportamiento y pueden dar por hecho que algo no funciona correctamente. Por lo tanto, estas herramientas de supervisión pueden generar alertas o cerrar puertos cuando se utiliza el proxy de reactivación.  
   >   
   >  No utilice el proxy de reactivación si las herramientas y servicios de supervisión de su red no permiten solapas de MAC.  

4. Cuando un equipo administrador ve una solicitud de conexión de TCP nueva para un equipo inactivo y la solicitud es a un puerto al que estaba escuchando el equipo inactivo antes de quedar inactivo, el equipo administrador enviará un paquete de reactivación al equipo inactivo, y dejará de redirigir tráfico a dicho equipo.  

5. El equipo inactivo recibirá el paquete de reactivación y se reactivará. El equipo remitente reintentará automáticamente la conexión y, esta vez, el equipo estará activo y podrá responder.  

   El proxy de reactivación tiene los siguientes requisitos previos y limitaciones:  

> [!IMPORTANT]  
>  Si dispone de un equipo independiente que se encargue de la infraestructura de red y de los servicios de red, notifique a este equipo e inclúyalo durante su período de evaluación y pruebas. Por ejemplo, en una red que utilice el control de acceso de red 802.1X, el proxy de reactivación no funcionará y podrá interrumpir el servicio de red. Además, el proxy de reactivación podría provocar que algunas herramientas de supervisión de red generen alertas cuando las herramientas detecten el tráfico para reactivar otros equipos.  

-   Todos los sistemas operativos de Windows enumerados como clientes compatibles en [Sistemas operativos compatibles con clientes y dispositivos](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) se admiten en Wake on LAN.  

-   No se admiten sistemas operativos invitados que se ejecuten en una máquina virtual.  

-   Los clientes deberán estar habilitados para el proxy de reactivación mediante la configuración de cliente. Aunque el funcionamiento del proxy de reactivación no depende del inventario de hardware, los clientes no notifican la instalación del servicio proxy de reactivación a menos que estén habilitados para el inventario de hardware y hayan enviado al menos un inventario de hardware.  

-   Es necesario que los adaptadores de red (y posiblemente el BIOS) estén habilitados y configurados para los paquetes de reactivación. Si el adaptador de red no está configurado para los paquetes de reactivación, o si esta configuración está deshabilitada, Configuration Manager lo configurará automáticamente y lo habilitará para un equipo si recibe la configuración cliente para habilitar el proxy de reactivación.  

-   Si un equipo tiene más de un adaptador de red, no podrá configurar qué adaptador se debe usar para el proxy de activación; la opción es no determinista. Pero el adaptador seleccionado se registra en el archivo SleepAgent_<DOMINIO\>@SYSTEM_0.log.  

-   La red deberá permitir solicitudes de eco ICMP (al menos dentro de la subred). No se puede configurar el intervalo de cinco segundos que se utiliza para enviar los comandos ping de ICMP.  

-   La comunicación está sin encriptar y sin autenticar y no se admite IPsec.  

-   No se admiten las siguientes configuraciones de red:  

    -   802.1X con autenticación de puertos  

    -   Redes inalámbricas  

    -   Conmutadores de red que enlacen direcciones MAC con puertos específicos  

    -   Redes exclusivamente IPv6  

    -   Duración de las concesiones DHCP de menos de 24 horas  

Si quiere reactivar equipos para la instalación programada de software, deberá configurar cada sitio primario para usar paquetes de reactivación.  

 Para usar el proxy de reactivación, deberá implementar la configuración del cliente proxy de reactivación de Administración de energía además de configurar el sitio principal.  

Decida si quiere usar paquetes de difusiones dirigidas a subred o paquetes de unidifusión y qué número de puerto UDP usar. De forma predeterminada, los paquetes de reactivación tradicionales se transmiten mediante el puerto 9 de UDP, pero, para aumentar la seguridad, puede seleccionar un puerto alternativo para el sitio si lo admiten los enrutadores y firewalls intervinientes.  

## <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>elija entre Unidifusión y Difusión dirigida a subred para Wake-on-LAN  
 Si decide reactivar equipos mediante el envío de paquetes de reactivación tradicionales, deberá decidir si desea transmitir paquetes de unidifusión o paquetes de difusión dirigida a subred. Si usa el proxy de reactivación, deberá usar paquetes de unidifusión. De lo contrario, utilice la siguiente tabla como ayuda para determinar qué método de transmisión desea elegir.  

|Método de transmisión|Ventaja|Desventaja|  
|-------------------------|---------------|------------------|  
|Unidifusión|Solución más segura que las difusiones dirigidas a subred, porque el paquete se envía directamente a un equipo en lugar de hacerlo a todos los equipos de una subred.<br /><br /> Podría no requerir la reconfiguración de los enrutadores (puede que tenga que configurar la memoria caché de ARP).<br /><br /> Consume menos ancho de banda de red que las transmisiones de difusión dirigida a subred.<br /><br /> Compatible con IPv4 e IPv6.|Los paquetes de reactivación no encuentran los equipos de destino que cambiaron su dirección de subred después de la última programación de inventario de hardware.<br /><br /> Es posible que haya que configurar los conmutadores para reenviar paquetes UDP.<br /><br /> Algunos adaptadores de red podrían no responder a los paquetes de reactivación en todos los estados de suspensión si usan la unidifusión como método de transmisión.|  
|Difusión dirigida a subred|Mayor proporción de éxito que la unidifusión si tiene equipos que cambian frecuentemente su dirección IP en la misma subred.<br /><br /> No se requiere la reconfiguración de conmutadores.<br /><br /> Elevada tasa de compatibilidad con los adaptadores de equipos para todos los estados de suspensión, pues las transmisiones dirigidas a subred eran el método de transmisión original para el envío de paquetes de reactivación.|Solución menos segura que el uso de unidifusión, ya que un atacante podría enviar secuencias continuas de solicitudes de eco ICMP desde una dirección de origen falsificada a la dirección de difusión dirigida. Esto haría que todos los hosts respondieran a esa dirección de origen. Si los enrutadores están configurados para permitir las difusiones dirigidas a subred, se recomienda una configuración adicional por razones de seguridad:<br /><br /> - Configure los enrutadores para permitir solo difusiones dirigidas de IP desde el servidor de sitio de Configuration Manager mediante el uso de un número de puerto UDP especificado.<br />- Configure Configuration Manager para usar el número de puerto no predeterminado que se ha especificado.<br /><br /> Es posible que sea necesario volver a configurar todos los enrutadores que intervienen para habilitar las difusiones dirigidas de subred.<br /><br /> Consume más ancho de banda de red que las transmisiones de difusión.<br /><br /> Compatible sólo con IPv4; no se admite IPv6.|  

> [!WARNING]  
>  Existen riesgos de seguridad asociados con las difusiones dirigidas de subred: Un atacante podría enviar un flujo continuo de solicitudes de eco del Protocolo de mensajes de control de Internet (ICMP) a la dirección de difusión dirigida desde una dirección de origen falsificada, lo que provocaría que todos los hosts respondieran a esa dirección de origen. Este tipo de ataque de denegación de servicio se suele denominar ataque smurf y normalmente se mitiga no habilitando las difusiones dirigidas de subred.
