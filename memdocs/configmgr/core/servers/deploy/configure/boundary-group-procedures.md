---
title: Procedimientos de los grupos de límites
titleSuffix: Configuration Manager
description: Configure grupos de límites para organizar de manera lógica las ubicaciones de red relacionadas denominadas límites.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697393"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Cómo configurar grupos de límites para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se incluyen procedimientos sobre cómo configurar grupos de límites. Antes de empezar, asegúrese de que comprende los conceptos de grupo de límites. Para obtener más información, consulte [Boundary groups (Grupos de límites)](boundary-groups.md).



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a> Creación de un grupo de límites  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Grupos de límites**.  

2.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear grupo de límites**.  

3.  En el cuadro de diálogo **Crear grupo de límites**, en la pestaña **General**, especifique un **Nombre** para este grupo de límites. De forma opcional, incluya una **Descripción**.  

4.  Seleccione **Aceptar** para guardar el nuevo grupo de límites o continuar con la siguiente sección para configurarlo.  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a> Configuración de un grupo de límites  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración de jerarquía** y seleccione el nodo **Grupos de límites**.  

2.  Seleccione el grupo de límites que desea modificar y haga clic en **Propiedades** en la cinta de opciones. Esta acción abre la ventana Propiedades del grupo de límites.  

Configure las siguientes opciones:  
- [Adición o eliminación de límites](#bkmk_add)  
- [Configuración de la asignación de sitio y selección de los servidores de sistema de sitio](#bkmk_references)  
- [Configuración del comportamiento de reserva](#bkmk_bg-fallback)  
- [Configuración de opciones del grupo de límites](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a> Adición o eliminación de límites

En la ventana Propiedades del grupo de límites, use la pestaña **General** para modificar los límites que son miembros de este grupo de límites:  

- Para agregar límites, seleccione **Agregar**. En la ventana Agregar límites, seleccione la casilla de uno o varios límites y luego haga clic en **Aceptar**.  

- Para quitar límites, seleccione el límite en la lista y haga clic en **Quitar**.  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a> Configuración de la asignación de sitio y selección de los servidores de sistema de sitio

Para modificar la asignación de sitio y la configuración del servidor del sistema de sitio asociado, cambie a la pestaña **Referencias** de la ventana Propiedades del grupo de límites.  

- Para habilitar este grupo de límites para que los clientes lo usen para la asignación de sitio, seleccione **Usar este grupo de límites para la asignación de sitio**. Después, seleccione un sitio en la lista desplegable **Sitio asignado**. Para más información, vea [Asignación de sitio](boundary-groups.md#site-assignment).  

- Para asociar los servidores del sistema de sitio disponibles con este grupo de límites, seleccione **Agregar**. En la ventana Agregar sistemas de sitio solo se enumeran los servidores que tienen roles de sistema de sitio compatibles. Seleccione la casilla de uno o varios servidores y luego haga clic en **Aceptar**. Se agregan como servidores de sistema de sitio asociados para este grupo de límites.  

    > [!NOTE]  
    >  Puede seleccionar cualquier combinación de sistemas de sitio disponibles en cualquier sitio de la jerarquía. Los sistemas de sitio seleccionados se muestran en la pestaña **Sistemas de sitio** en las propiedades de cada límite miembro de este grupo de límites.  

- Para quitar un servidor de este grupo de límites, seleccione el servidor y luego haga clic en **Quitar**.  

    > [!NOTE]  
    >  Para que este grupo de límites deje de usarse para asociar sistemas de sitio, quite todos los servidores que se enumeran como servidores de sistema de sitio asociados.  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a> Configuración del comportamiento de reserva

Para configurar el comportamiento de reserva, cambie a la pestaña **Relaciones** de la ventana Propiedades del grupo de límites.  

- Para crear una relación con otro grupo de límites:  

  - Seleccione **Agregar**. En la ventana Grupos de límites de reserva, seleccione el grupo de límites que desea configurar.  

  - Defina un tiempo de reserva para los siguientes roles de sistema de sitio:  
    - Punto de distribución  
    - Punto de actualización de software  
    - Punto de administración  

      > [!Note]  
      > Por ejemplo, abra la ventana Propiedades del grupo de límites de la sucursal. En la ventana Grupos de límites de reserva, seleccione el grupo de límites de la sede principal. Defina el tiempo de reserva del punto de distribución en `20`. Al guardar esta configuración, los clientes del grupo de límites de la sucursal empezarán a buscar contenido de los puntos de distribución del grupo de límites de la sede principal después de 20 minutos.  

  - Para impedir la reserva de un grupo de límites específico, seleccione el grupo de límites y luego haga clic en **No usar reserva nunca** para este tipo de rol de sistema de sitio. Esta acción puede incluir el *grupo de límites de sitio predeterminado*.  

- Para modificar la configuración de una relación existente, seleccione el grupo de límites en la lista y haga clic en **Cambiar**. Esta acción abre la ventana Grupos de límites de reserva solo para este grupo de límites.  
 
- Para quitar una relación, seleccione el grupo de límites en la lista y luego haga clic en **Quitar**.  

Para más información, vea [Reserva](boundary-groups.md#fallback). 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a> Configuración de opciones del grupo de límites
<!--1356193-->
A partir de la versión 1806, para configurar opciones adicionales para los clientes de este grupo de límites, cambie a la pestaña **Opciones**. Para más información, vea [Opciones de grupo de límites para descargas del mismo nivel](boundary-groups.md#bkmk_bgoptions).

- **Permitir descargas del mismo nivel en este grupo de límites**: Esta opción está habilitada de forma predeterminada. El punto de administración proporciona a los clientes una lista de ubicaciones de contenido que incluye orígenes del mismo nivel.  

    - **Durante las descargas del mismo nivel, use solo elementos del mismo nivel dentro de la misma subred**: Esta configuración depende de la anterior. Si habilita esta opción, el punto de administración solo se incluye en los orígenes del mismo nivel de la lista de ubicaciones de contenido que se encuentran en la misma subred que el cliente.  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a> Configurar un sitio de reserva para la asignación de sitios automática  

Si los clientes no están en un grupo de límites con un sitio asignado, puede asignarlos a este sitio cuando se instalan.

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2.  En la pestaña **Inicio** de la cinta de opciones, en el grupo **Sitios**, seleccione **Configuración de jerarquía**.  

3.  En la pestaña **General**, seleccione la casilla para **Usar un sitio de reserva**. Después, seleccione un sitio en la lista desplegable **Sitio de reserva**.  

4.  Seleccione **Aceptar** para guardar la configuración.  

Para más información, vea [Asignación de sitio](boundary-groups.md#site-assignment).


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a> Habilitar el uso de puntos de administración preferidos  

Para más información, vea [Puntos de administración preferidos](boundary-groups.md#bkmk_preferred).

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Sitios**, seleccione **Configuración de jerarquía**.  

3. En la pestaña **General**, seleccione **Los clientes prefieren usar puntos de administración especificados en grupos de límites**.  

4. Seleccione **Aceptar** para guardar la configuración.  

