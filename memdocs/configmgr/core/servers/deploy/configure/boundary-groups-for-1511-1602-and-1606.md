---
title: Grupos de límites para 1511, 1602 y 1606
titleSuffix: Configuration Manager
description: Use grupos de límites con las versiones 1511, 1602 y 1606 de Configuration Manager.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09c1b0613d36cd135ff3ac71ac7ec8472ad1e8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704843"
---
# <a name="boundary-groups-for-configuration-manager-version-1511-1602-and-1606"></a>Grupos de límites para las versiones 1511, 1602 y 1606 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*
<!-- This topic drops from TOC with the release of version 1706 -->

La información de este tema es específica para el uso de grupos de límites con las versiones 1511, 1602 y 1606 de Configuration Manager.
Si utiliza la versión 1610 o posterior, vea [Configure boundary groups](boundary-groups.md) (Configuración de grupos de límites) para obtener información sobre cómo usar los grupos de límites rediseñados.  


##  <a name="boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 Cree grupos de límites para agrupar de forma lógica las ubicaciones de red (límites) de manera que su infraestructura de red resulte más fácil de administrar. Debe asignar límites a grupos de límites para poder utilizar el grupo de límites. Los clientes usan la configuración de grupos de límites para lo siguiente:  

-   Asignación automática de sitio  

-   Ubicación del contenido  

-   Puntos de administración preferidos

    Si va a usar puntos de administración preferidos, debe habilitar esta opción para la jerarquía y no desde la configuración del grupo de límites. Consulte el procedimiento *Para habilitar el uso de puntos de administración preferidos* que aparece más adelante en este tema.  

Al configurar grupos de límites, se agregan uno o varios límites al grupo de límites. Luego, es necesario configurar valores adicionales para que los clientes ubicados en esos límites los usen.  

#### <a name="to-create-a-boundary-group"></a>Para crear un grupo de límites  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

2.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear grupo de límites**.  

3.  En el cuadro de diálogo **Crear grupo de límites**, elija la pestaña **General** y especifique un **Nombre** para este grupo de límites.  

4.  Elija **Aceptar** para guardar el nuevo grupo de límites.  

#### <a name="to-set-up-a-boundary-group"></a>Para configurar un grupo de límites  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

2.  Elija el grupo de límites que quiera cambiar.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** del grupo de límites, elija la pestaña **General** para cambiar los límites que pertenecen a este grupo de límites:  

    -   Para agregar límites, elija **Agregar**, active la casilla de uno o varios límites y, luego, elija **Aceptar**.  

    -   Para quitar límites, seleccione uno y elija **Quitar**.  

5.  Elija la pestaña **Referencias** para cambiar la configuración de la asignación de sitio y del servidor del sistema de sitios asociado:  

    -   Para habilitar este grupo de límites a fin de que lo usen los clientes para la asignación de sitio, active la casilla correspondiente a **Usar este grupo de límites para la asignación de sitio** y, luego, elija un sitio en la lista desplegable **Sitio asignado**.  

    -   Para configurar los servidores de sistema de sitio disponibles asociados a este grupo de límites:  

    1.  Elija **Agregar** y, después, active la casilla de uno o varios servidores. Los servidores se agregan como servidores del sistema de sitio asociados para este grupo de límites. Solo están disponibles los servidores que admitieron el rol de sistema de sitio que se instaló en ellos.  

        > [!NOTE]  
        >  Puede seleccionar cualquier combinación de sistemas de sitio disponibles en cualquier sitio de la jerarquía. Los sistemas de sitio seleccionados se muestran en la pestaña **Sistemas de sitio** en las propiedades de cada límite miembro de este grupo de límites.  

    2.  Para quitar un servidor de este grupo de límites, elija el servidor y, luego, elija **Quitar**.  

        > [!NOTE]  
        >  Para que este grupo de límites deje de usarse para asociar sistemas de sitio, debe quitar todos los servidores que se enumeran como servidores de sistema de sitio asociados.  

    3.  Para cambiar la velocidad de conexión de la red correspondiente a un servidor de sistema de sitio de este grupo de límites, elija el servidor y, luego, **Cambiar conexión**.  

         De forma predeterminada, la velocidad de conexión de cada sistema de sitio es **Rápida**, pero puede cambiarla a **Lenta**. La velocidad de conexión de red y la configuración de una implementación determinan si un cliente puede descargar contenido desde el servidor.  

6.  Elija **Aceptar** para cerrar las propiedades del grupo de límites y guardar la configuración.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Para asociar un servidor de implementación de contenido o un grupo de administración a un grupo de límites  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** >  **Grupos de límites**.  

2.  Elija el grupo de límites que quiera cambiar.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** correspondiente al grupo de límites, elija la pestaña **Referencias**.  

5.  En **Seleccionar servidores de sistema de sitio**, elija **Agregar**, active la casilla correspondiente a los servidores de sistema de sitio que quiera asociar a este grupo de límites y, después, elija **Aceptar**.  

6.  Elija **Aceptar** para cerrar el cuadro de diálogo y guardar la configuración del grupo de límites.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Para habilitar el uso de puntos de administración preferidos  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración del sitio** > **Sitios** y, después, en la pestaña **Inicio**, elija **Configuración de jerarquía**.  

2.  En la pestaña **General** de **Configuración de jerarquía**, elija **Los clientes prefieren usar puntos de administración especificados en grupos de límites**.  

3.  Elija **Aceptar** para cerrar el cuadro de diálogo y guardar la configuración.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Para configurar un sitio de reserva para la asignación de sitios automática  

1. En la consola de Configuration Manager, pulse **Administración** > **Configuración del sitio** >  **Sitios**.  

2. En la pestaña **Inicio**, en el grupo **Sitios**, pulse **Configuración de jerarquía**.  

3. En la pestaña **General**, active la casilla de **Usar un sitio de reserva** y, luego, elija un sitio en la lista desplegable **Sitio de reserva**.  

4. Elija **Aceptar** para guardar la configuración.  

   Las secciones siguientes proporcionan detalles adicionales sobre las configuraciones de grupos de límites.  

###  <a name="about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Información sobre la asignación de sitio  
 Puede configurar cada grupo de límites con un sitio asignado para los clientes.  

-   Un cliente recién instalado que use la asignación de sitios automática se unirá al sitio asignado de un grupo de límites que tenga la ubicación de red actual del cliente.  

-   Un cliente asignado a un sitio no cambia su asignación de sitio aunque cambie su ubicación de red. Por ejemplo, si el cliente se mueve a una nueva ubicación de red representada por un límite en un grupo de límites que tiene una asignación de sitio diferente, el sitio asignado del cliente no se modificará.  

-   Cuando la detección de sistemas de Active Directory detecta un nuevo recurso, la información de red para el recurso detectado se evalúa en relación con los límites en los grupos de límites. Este proceso asocia el nuevo recurso con un sitio asignado para que use el método de instalación de inserción de cliente.  

-   Cuando un límite es miembro de varios grupos de límites que tienen diferentes sitios asignados, los clientes seleccionan uno de los sitios de forma aleatoria.  

-   Los cambios que se realicen en el sitio asignado de un grupo de límites solo se aplicarán a las nuevas acciones de asignación de sitio. Los clientes previamente asignados a un sitio no vuelven a evaluar su asignación de sitio según los cambios en la configuración de un grupo de límites (o en su propia ubicación de red).  

Para más información sobre la asignación de sitio de los clientes, vea [Uso de la asignación de sitio automática para los equipos](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) en [Cómo asignar clientes a un sitio](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Información sobre la ubicación del contenido  
 Puede configurar cada uno de los grupos de límites con uno o varios puntos de distribución y puntos de migración de estado, y puede asociar los mismos puntos de distribución y puntos de migración de estado a varios grupos de límites.  

-   **Durante la distribución de software**, los clientes solicitan una ubicación para el contenido de la implementación. Configuration Manager envía al cliente una lista de puntos de distribución asociados a cada grupo de límites que incluye la ubicación de red actual del cliente.  

-   **Durante la implementación de sistema operativo**, los clientes solicitan una ubicación para enviar o recibir su información de estado de la migración. Configuration Manager envía al cliente una lista de puntos de migración de estado asociados a cada grupo de límites que incluye la ubicación de red actual del cliente.  

Este comportamiento permite al cliente seleccionar el servidor más cercano desde el que transferir el contenido o la información de migración de estado.  

###  <a name="about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Información sobre los puntos de administración preferidos  
 Los puntos de administración preferidos permiten que un cliente identifique un punto de administración asociado a su ubicación de red (límite) actual.  

-   Un cliente intenta usar un punto de administración preferido de su sitio asignado antes de usar un punto de administración de su sitio asignado que no está configurado como preferido.  

-   Para usar esta opción, debe habilitarla para la jerarquía y configurar grupos de límites en los sitios principales individuales para que incluyan los puntos de administración que se deben asociar a esos límites asociados del grupo de límites.  

-   Cuando se configuran los puntos de administración preferidos y un cliente organiza su lista de puntos de administración, el cliente coloca los puntos de administración preferidos en la parte superior de su lista de puntos de administración asignados, que incluye todos los puntos de administración del sitio asignado del cliente.  

> [!NOTE]  
>  Cuando un cliente se mueve, por ejemplo, cuando se desplaza con un equipo portátil a una ubicación de oficina remota y cambia su ubicación de red, podría usar un punto de administración (o punto de administración proxy) desde el sitio local de su nueva ubicación, antes de intentar usar un punto de administración desde su sitio asignado (que incluye los puntos de administración preferidos).  Vea [Comprender cómo los clientes buscan servicios y recursos de sitio para Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para más información.  

###  <a name="about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Información sobre la superposición de límites  
 Configuration Manager admite configuraciones de límites que se superponen para la ubicación del contenido:  

-   **Cuando un cliente solicita contenido** y la ubicación de red del cliente pertenece a varios grupos de límites, Configuration Manager envía al cliente una lista de todos los puntos de distribución que tienen el contenido.  

-   **Cuando un cliente solicita a un servidor que envíe o reciba información de su migración de estado** y la ubicación de red del cliente pertenece a varios grupos de límites, Configuration Manager envía al cliente una lista de todos los puntos de migración de estado asociados a un grupo de límites que incluye la ubicación de red actual del cliente.  

Este comportamiento permite al cliente seleccionar el servidor más cercano desde el que transferir el contenido o la información de migración de estado.  

###  <a name="about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Información sobre la velocidad de conexión de red  
 Puede establecer la velocidad de conexión de la red para cada servidor de sistema de sitio de un grupo de límites. Esta configuración se aplica a los clientes que se conectan a un sistema de sitio basado en la configuración de este grupo de límites. El mismo servidor de sistema de sitio puede tener diferentes velocidades de conexión establecidas para distintos grupos de límites.  

 De forma predeterminada, la velocidad de conexión de la red se establece en **Rápida**, pero puede cambiarla a **Lenta**. La velocidad de conexión de la red y la configuración de implementación permiten comprobar si un cliente puede descargar contenido desde un punto de distribución cuando este se encuentra en un grupo de límites asociado.  

 Para obtener más información sobre cómo afecta la configuración de la velocidad de conexión de la red a la forma en que los clientes obtienen el contenido, consulte [Escenarios de ubicación de orígenes de contenido](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
