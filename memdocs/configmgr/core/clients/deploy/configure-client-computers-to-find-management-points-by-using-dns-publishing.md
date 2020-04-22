---
title: Configurar los clientes para que usen la publicación en DNS
titleSuffix: Configuration Manager
description: Configure los equipos cliente de Configuration Manager para buscar puntos de administración mediante la publicación en DNS.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d28a8a35f711dcef7e3f9adb6dccbabc4082ab28
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693543"
---
# <a name="configure-client-computers-to-find-management-points-by-using-dns-publishing"></a>Configuración de equipos cliente para buscar puntos de administración mediante la publicación en DNS

*Se aplica a: Configuration Manager (rama actual)*

Los clientes de Configuration Manager deben encontrar un punto de administración para completar la asignación de sitios y como proceso continuo para seguir siendo administrados. Los Servicios de dominio de Active Directory proporcionan el método más seguro para que los clientes en la intranet encuentren puntos de administración. Sin embargo, si los clientes no pueden usar este método de ubicación de servicio (por ejemplo, no han extendido el esquema de Active Directory o son parte de un grupo de trabajo) use la publicación en DNS con método de ubicación de servicio alternativo.  

> [!NOTE]  
>  Al instalar el cliente para Linux y UNIX, debe especificar un punto de administración como punto inicial de contacto. Para más información sobre cómo instalar el cliente para Linux y UNIX, vea [Cómo implementar clientes en servidores UNIX y Linux en Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Antes de utilizar la publicación en DNS para puntos de administración, asegúrese de que los servidores DNS en la intranet tienen registros de recurso de ubicación de servicio (SRV RR) y los correspondientes registros de recurso de host (A o AAA) para los puntos de administración del sitio. Los registros de recurso de ubicación de servicio pueden ser creados automáticamente por Configuration Manager o, de manera manual, por el administrador de DNS que crea los registros en DNS.  

 Para más información sobre la publicación en DNS como método de ubicación de servicio para clientes de Configuration Manager, vea [Comprender cómo los clientes buscan servicios y recursos de sitio para Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 De forma predeterminada, los clientes buscan DNS para puntos de administración en su dominio DNS. Pero si no se publican puntos de administración en el dominio de los clientes, debe configurar manualmente los clientes con un sufijo DNS del punto de administración. Puede configurar este sufijo DNS en clientes durante o después de la instalación del cliente:  

-   Para configurar clientes para un sufijo de punto de administración durante la instalación del cliente, configure las propiedades de Client.msi de CCMSetup.  

-   Para configurar clientes para un sufijo de punto de administración tras la instalación del cliente, en el Panel de control, configure las **Propiedades de Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Para configurar clientes para un sufijo de punto de administración durante la instalación del cliente  

- Instale el cliente con la siguiente propiedad de Client.msi de CCMSetup:  

  - **DNSSUFFIX=** *&lt;dominio del punto de administración\>*  

     Si el sitio tiene varios puntos de administración en más de un dominio, especifique un solo dominio. Cuando los clientes se conectan a un punto de administración en este dominio, descargarán una lista de puntos de administración disponibles que incluirá los puntos de administración de los otros dominios.  

    Para más información sobre las propiedades de la línea de comandos de CCMSetup, vea [Acerca de las propiedades de instalación de clientes](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Para configurar clientes para un sufijo de punto de administración después de la instalación del cliente  

1.  En el Panel de Control del equipo cliente, vaya a **Configuration Manager**y, a continuación, haga doble clic en **Propiedades**.  

2.  En la pestaña **Sitio** , especifique el sufijo DNS de un punto de administración y, a continuación, haga clic en **Aceptar**.  

     Si el sitio tiene varios puntos de administración en más de un dominio, especifique un solo dominio. Cuando los clientes se conectan a un punto de administración en este dominio, descargarán una lista de puntos de administración disponibles que incluirá los puntos de administración de los otros dominios.
