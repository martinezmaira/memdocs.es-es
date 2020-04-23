---
title: Versión preliminar técnica 1803
titleSuffix: Configuration Manager
description: Obtenga información sobre las características disponibles en la versión preliminar técnica 1803 de Configuration Manager.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701953"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Funciones de Technical Preview 1803 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión preliminar técnica de Configuration Manager, versión 1803. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de versión preliminar técnica. 

Revise el artículo [Technical Preview para System Center Configuration Manager](technical-preview.md) antes de instalar esta actualización. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Estas son las nuevas características que puede probar con esta versión.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Compatibilidad de puntos de distribución de extracción con puntos de distribución de nube como orígenes  
<!--1321554-->
Muchos clientes usan [puntos de distribución de extracción](../plan-design/hierarchy/use-a-pull-distribution-point.md) en sucursales u oficinas remotas, que descargan contenido desde un punto de distribución de origen en la WAN. Si sus oficinas remotas tienen una mejor conexión a Internet o si quiere reducir la carga en los vínculos a WAN, ahora puede usar como origen un [punto de distribución de nube](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) en Microsoft Azure. Cuando se agrega un origen en la pestaña **Punto de distribución de extracción** de las propiedades del punto de distribución, cualquier punto de distribución de nube en el sitio aparece como un punto de distribución disponible. El comportamiento de ambos roles de sistema de sitio sigue siendo el mismo en cualquier caso. 

### <a name="prerequisites"></a>Requisitos previos
- El punto de distribución de extracción necesita acceso a Internet para comunicarse con Microsoft Azure.
- El contenido debe distribuirse al punto de distribución de nube de origen.

> [!Note]  
> Esta característica no genera gastos por almacenamiento de datos y salida de red en la suscripción de Azure. Para más información, vea [Costo de la utilización de la distribución basada en la nube](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Compatibilidad de descarga parcial en la memoria caché del mismo nivel de cliente para reducir la utilización de la WAN
<!--1357346-->
Los orígenes de la caché del mismo nivel de cliente ahora pueden dividir el contenido en partes. Estas partes reducen al mínimo la transferencia de red para usar menos WAN. El punto de administración proporciona un seguimiento más detallado de las partes de contenido e intenta eliminar más de una descarga del mismo contenido por grupo de límites. 

### <a name="example-scenario"></a>Escenario de ejemplo
Contoso tiene un único sitio primario con dos grupos de límites: oficina central y sucursal. Hay una relación de reserva de 30 minutos entre los dos grupos de límites. El punto de administración y el punto de distribución del sitio solo están en el límite de oficina central. La ubicación de la sucursal no tiene ningún punto de distribución local. Dos de los cuatro clientes de la sucursal están configurados como orígenes de caché del mismo nivel. 

![Diagrama de configuración de red descrita para el escenario de ejemplo](media/1357346-peer-cache-source-parts.png)

1. Su destino es una implementación con contenido para los cuatro clientes de la sucursal. Solo ha distribuido el contenido en el punto de distribución.
2. El cliente 3 y el cliente 4 no tienen un origen local para la implementación. El punto de administración indica a los clientes que esperen 30 minutos antes de recurrir al grupo de límites remoto.
3. El cliente 1 (PCS1) es el primer origen de caché del mismo nivel que actualiza la directiva con el punto de administración. Dado que este cliente está habilitado como un origen de caché del mismo nivel, el punto de administración le indica que inicie inmediatamente la descarga de la parte A desde el punto de distribución.  
4. Cuando el cliente 2 (PCS2) se pone en contacto con el punto de administración, como la parte A ya está en curso pero aún no se ha completado, el punto de administración indica que se inicie inmediatamente la descarga de la parte B desde el punto de distribución.
5. PCS1 termina la descarga de la parte A y notifica inmediatamente al punto de administración. Como la parte B ya está en curso pero aún no se ha completado, el punto de administración le indica que empiece la descarga de la parte C desde el punto de distribución.
6. PCS2 termina la descarga de la parte B y notifica inmediatamente al punto de administración. El punto de administración le indica que empiece a descargar la parte D desde el punto de distribución. 
7. PCS1 termina la descarga de la parte C y notifica inmediatamente al punto de administración. El punto de administración le informa de que ya no hay más partes disponibles en el punto de distribución remoto. El punto de administración le indica que descargue la parte B desde su elemento del mismo nivel local, PCS2.
8. Este proceso continúa hasta que ambos orígenes de la memoria caché del mismo nivel de cliente obtienen todos los elementos el uno del otro. El punto de administración da prioridad a las partes procedentes del punto de distribución remoto antes de indicar a los orígenes de la memoria caché del mismo nivel que descarguen partes del elemento del mismo nivel local. 
9. El cliente 3 es el primero que actualiza la directiva después de expirar el período de reserva de 30 minutos. Ahora vuelve a comprobar con el punto de administración, que informa al cliente de que hay nuevos orígenes locales. En lugar de descargar el contenido por completo desde el punto de distribución a través de la WAN, descarga el contenido en su totalidad desde uno de los orígenes de caché del mismo nivel de cliente. Los clientes dan prioridad a los orígenes del mismo nivel local. 

> [!Note]  
> Si el número de orígenes de caché del mismo nivel de cliente es mayor que el número de partes de contenido, el punto de administración indica a los orígenes de caché del mismo nivel adicionales que esperen el tiempo de reserva, como un cliente normal. 


### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

1. Configure los [grupos de límites](../servers/deploy/configure/boundary-groups.md) y los [orígenes de caché del mismo nivel](../plan-design/hierarchy/client-peer-cache.md) siguiendo el procedimiento normal.
2. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda el nodo **Configuración del sitio** y haga clic en **Sitios**. Haga clic en **Configuración de jerarquía** en la cinta de opciones. 
3. En la pestaña **General**, habilite la opción **Configure client peer cache sources to divide content into parts** (Configurar orígenes de caché del mismo nivel de cliente para que dividan el contenido en partes). 
4. Cree una implementación requerida con contenido.  

   > [!Note]  
   > Esta característica solo funciona cuando el cliente descarga el contenido en segundo plano, como con una implementación requerida. Las descargas a petición, como cuando el usuario instala una implementación disponible en el Centro de software, se comportan como de costumbre.  

1. Para ver cómo controlan la descarga de contenido en partes, vea el **ContentTransferManager.log** en el origen de caché del mismo nivel de cliente y el **MP_Location.log** en el punto de administración.  
 



## <a name="maintenance-windows-in-software-center"></a>Ventanas de mantenimiento en el Centro de software
<!--1358131-->
El Centro de software ahora muestra la siguiente ventana de mantenimiento programado. En la pestaña Estado de la instalación, cambie la vista de Todas a Próximas. Muestra el intervalo de tiempo y la lista de implementaciones que están programadas. La lista está vacía si no hay ninguna ventana de mantenimiento futuro. 

![El Centro de software mostrando la lista de las próximas implementaciones en la pestaña Estado de la instalación](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Pestaña personalizada de la página web en el Centro de software
<!--1358132-->
Ahora puede crear una pestaña personalizada para abrir una página web en el Centro de software. Esta característica permite mostrar contenido a los usuarios finales de una manera coherente y confiable. En esta lista se incluyen algunos ejemplos:
- Contactar con TI: información sobre cómo ponerse en contacto con el departamento de TI de la organización
- Centro de soporte técnico: acciones de autoservicio de TI, como buscar una base de conocimientos o abrir una incidencia de soporte técnico.
- Documentación de usuario final: artículos para los usuarios de la organización sobre diversos temas de TI como, por ejemplo, el uso de aplicaciones o la actualización a Windows 10.


### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

1. En la consola de Configuration Manager, en el área de trabajo **Administración**, en el nodo **Configuración de cliente**, abra la directiva **Configuración de cliente predeterminada**.
2. Seleccione el grupo **Centro de software**.
3. Para **Configuración del Centro de software**, haga clic en **Personalizar**.
4. Cambie a la pestaña **Pestañas**.
5. Habilite la opción **Specify a custom tab for Software Center** (Especificar una pestaña personalizada para el Centro de Software).
    1. Escriba un nombre en el campo de texto **Nombre de pestaña**. Este nombre es lo que se muestra al usuario en el Centro de software.
    2. Escriba una URL válida en el campo de texto **Dirección URL de contenido**. Esta dirección URL es el contenido que muestra el Centro de software cuando los usuarios hacen clic en esta pestaña.

> [!Tip]  
> El Centro de software usa componentes de Internet Explorer para representar la página web.

## <a name="enable-third-party-software-update-support-on-clients"></a>Habilitar compatibilidad con la actualización de software de terceros en clientes

Ahora puede habilitar la configuración de clientes de Configuration Manager para actualizaciones de software de terceros. Cuando usa la opción **Habilitar actualizaciones de software de terceros** para las propiedades de componente de SUP, este descargará el certificado de firma usado por WSUS para las actualizaciones de terceros. <!--1357605-->

Al seleccionar **Habilitar actualizaciones de software de terceros** en la configuración de cliente, se produce lo siguiente: 
- En el cliente, se establece la directiva "Permitir actualizaciones firmadas procedentes de una ubicación del servicio Microsoft Update en la intranet". 
- Se instala el certificado de firma en el almacén de editores de confianza en el cliente. 

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

1. En el sitio de nivel superior de la jerarquía de Configuration Manager, vaya al nodo **Administración**, expanda **Configuración del sitio** y, después, **Sitios**.
2. Haga clic con el botón derecho en el servidor de sitio de nivel superior, seleccione **Configurar componentes de sitio** y, después, elija **Punto de actualización de software**.
3. Haga clic en la pestaña **Actualizaciones de terceros** y marque **Habilitar actualizaciones de software de terceros**.
4. Abra **Configuración de cliente** y vaya a la configuración de **Actualizaciones de software**.
5. Asegúrese de que **Habilitar actualizaciones de software de terceros** está establecido en **Sí**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Habilitar la copia y el pegado de detalles de activos desde vistas de supervisión
En respuesta a los [comentarios de los usuarios](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det), hemos habilitado la característica de copiar y pegar en el panel de detalles de activos en las vistas de supervisión de estado de implementación y distribución.  <!--1357552-->

## <a name="scap-extensions"></a>Extensiones SCAP
La versión preliminar de las extensiones SCAP está disponible en la carpeta Cd.latest en SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Esta versión preliminar de las extensiones SCAP puede instalarse en cualquier versión admitida de Rama actual de Configuration Manager y LTSB 1606.



## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
