---
title: Configuración de puertos de comunicación de cliente
titleSuffix: Configuration Manager
description: Configure puertos de comunicación de cliente en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30b553bbe2a68ec97e4d5200644a88d09ee5967d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693563"
---
# <a name="how-to-configure-client-communication-ports-in-configuration-manager"></a>Cómo configurar puertos de comunicación de cliente en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede cambiar los números de puerto de solicitud que usan los clientes de Configuration Manager para comunicarse con los sistemas de sitio que usan HTTP y HTTPS para la comunicación. Si bien es probable que HTTP o HTTPS estén ya configurados para los firewalls, la notificación de cliente que utiliza HTTP o HTTPS requiere más uso de CPU y memoria en el equipo de punto de administración que si se usa un número de puerto personalizado. También se puede especificar el número de puerto de sitio que se va a usar para activar clientes mediante los paquetes de reactivación tradicionales.  

 Al especificar puertos de solicitud HTTP y HTTPS, puede especificar un número de puerto predeterminado y un número de puerto alternativo. Los clientes procederán automáticamente con el puerto alternativo si no se logra la comunicación con el puerto predeterminado. Puede especificar la configuración para la comunicación de datos HTTP y HTTPS.  

 Los valores predeterminados para los puertos de solicitud de cliente son **80** para el tráfico HTTP y **443** para el tráfico HTTPS. Cámbielos sólo si no desea utilizar estos valores predeterminados. Un escenario típico de uso de puertos personalizados es en el que se utiliza un sitio web personalizado en IIS en lugar del sitio web predeterminado. Si cambia los números de puerto predeterminados para el sitio web predeterminado en IIS y otras aplicaciones también utilizan el sitio web predeterminado, es muy posible que estas generen errores.  

> [!IMPORTANT]
>  No cambie los números de puerto en Configuration Manager sin conocer bien las consecuencias de ello. Ejemplos:  
> 
> - Si cambia los números de puerto para los servicios de solicitud de cliente como una configuración de sitio, y no se actualiza la configuración de los clientes existentes para que utilicen los números de puerto nuevos, estos clientes llegarán a tener un estado no administrado.  
>   -   Antes de configurar un número de puerto no predeterminado, asegúrese de que los firewalls y dispositivos de red implicados pueden admitir esta configuración para, si es necesario, realizar los ajustes necesarios. Si va a administrar los clientes en Internet y cambia el número de puerto HTTPS 443 predeterminado, los enrutadores y firewalls de Internet podrían bloquear esta comunicación.  

 Para asegurarse de mantener los clientes en estado de administrado una vez cambiados los números de puerto de solicitud, configure los clientes para que utilicen los números de puerto de solicitud nuevos. Al cambiar los puertos de solicitud de un sitio primario, los sitios secundarios asociados heredan automáticamente la misma configuración de puerto. Utilice el procedimiento en este tema para configurar los puertos de solicitud en el sitio primario.  

> [!NOTE]  
>  Para más información sobre cómo configurar los puertos de solicitud de clientes en equipos que ejecutan Linux y UNIX, vea [Configure Request Ports for the Client for Linux and UNIX (Configurar puertos de solicitud del cliente para UNIX y Linux)](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Si el sitio de Configuration Manager se publica en Active Directory Domain Services, tanto los clientes nuevos como los existentes que tienen acceso a esta información adquirirán automáticamente la configuración del puerto de sitio, por lo que no se necesitará acción alguna al respecto. Los clientes que no tienen acceso a esta información publicada en Active Directory Domain Services son los clientes de grupo de trabajo, clientes de otro bosque de Active Directory, clientes configurados solo para Internet y aquellos clientes que están actualmente en Internet. Si cambia los números de puerto predeterminados una vez instalados estos clientes, vuelva a instalarlos e instale los clientes nuevos mediante uno de los métodos siguientes:  

- Reinstalar los clientes mediante el Asistente para la instalación de inserción de cliente. La instalación de inserción de cliente establece automáticamente en los clientes la configuración de puerto del sitio actual. Para más información sobre cómo usar el Asistente para instalación de inserción de cliente, vea [How to Install Configuration Manager Clients by Using Client Push (Instalación de clientes de Configuration Manager mediante la inserción de cliente)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

- Volver a instalar los clientes mediante CCMSetup.exe y las propiedades de instalación de client.msi de CCMHTTPPORT y CCMHTTPSPORT. Para más información sobre estas propiedades, vea [Acerca de las propiedades de instalación de clientes](../../../core/clients/deploy/about-client-installation-properties.md).  

- Volver a instalar los clientes con un método que busque las propiedades de instalación del cliente de Configuration Manager en Active Directory Domain Services. Para obtener más información, vea [Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

  Para reconfigurar los números de puerto para los clientes existentes, también puede utilizar el script PORTSWITCH.VBS que incluye los medios de instalación en la carpeta SMSSETUP\Tools\PortConfiguration.  

> [!IMPORTANT]  
>  Para los clientes existentes y los nuevos que están actualmente en Internet, debe configurar los números de puerto no predeterminados mediante las propiedades de client.msi de CCMSetup.exe de CCMHTTPPORT y CCMHTTPSPORT.  

 Una vez cambiados los puertos de solicitud en el sitio, los clientes nuevos que se instalan con el método de instalación de inserción de cliente de todo el sitio se configurarán automáticamente con los números de puerto actuales para el sitio.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Para configurar los números de puerto de comunicación de cliente para un sitio  

1. En la consola de Configuration Manager, haga clic en **Administración**.  

2. En el área de trabajo **Administración** , expanda **Configuración del sitio**, haga clic en **Sitios**y seleccione el sitio primario que se va a configurar.  

3. En la pestaña **Inicio** , haga clic en **Propiedades**y, a continuación, haga clic en la pestaña **Puertos** .  

4. Seleccione uno de los elementos y haga clic en el icono Propiedades para mostrar el cuadro de diálogo **Detalles del puerto** .  

5. En el cuadro de diálogo **Detalles del puerto** , especifique el número de puerto y la descripción para el elemento y, a continuación, haga clic en **Aceptar**.  

6. Seleccione **Usar sitio web personalizado** si va a utilizar el nombre de sitio web personalizado **SMSWeb** para los sistemas del sitio que ejecutan IIS.  

7. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de propiedades del sitio.  

   Repita este procedimiento para todos los sitios primarios de la jerarquía.
