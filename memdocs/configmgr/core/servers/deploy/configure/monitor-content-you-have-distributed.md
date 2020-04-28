---
title: Supervisar contenido
titleSuffix: Configuration Manager
description: Aprenda a supervisar contenido distribuido mediante la consola de Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fafcbffe3231af78ae3a079061accc9f112a181c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110022"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Supervisión del contenido distribuido con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Utilice la consola de Configuration Manager para supervisar el contenido distribuido, incluido lo siguiente:  

- Estado de todos los tipos de paquetes para los puntos de distribución asociados  
- Estado de validación del contenido de un paquete  
- Estado del contenido asignado a un grupo específico de puntos de distribución  
- Estado del contenido asignado a un punto de distribución  
- Estado de las características opcionales de cada punto de distribución (validación de contenido, PXE y multidifusión)  

> [!NOTE]  
> Configuration Manager solo supervisa el contenido de un punto de distribución que se encuentre en la biblioteca de contenido. No se supervisa el contenido almacenado en el punto de distribución de recursos compartidos personalizados o de paquete.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Supervisión del estado del contenido

El nodo **Estado de contenido** en el área de trabajo **Supervisión** proporciona información acerca de los paquetes de contenido. En la consola de Configuration Manager, revise la información como la siguiente:  

- Nombre, tipo e identificador del paquete
- El número de puntos de distribución a los que se envió un paquete
- La tasa de compatibilidad
- Cuándo se creó el paquete
- La versión de origen

También puede encontrar información detallada del estado de cualquier paquete, como:  

- El estado de distribución
- El número de errores
- Distribuciones pendientes  
- El número de instalaciones

También puede administrar las distribuciones que siguen en curso en un punto de distribución o que no pudieron distribuir correctamente el contenido en un punto de distribución:  

- La opción para cancelar o redistribuir contenido está disponible cuando ve el mensaje de estado de implementación de un trabajo de distribución en un punto de distribución en el panel **Detalles del activo**. Este panel se encuentra en la pestaña **En curso**, o bien en la pestaña **Error** del nodo **Estado de contenido**.  
- Además, en los detalles del trabajo se muestra el porcentaje del trabajo que se ha completado al consultarlo en la pestaña **En curso**. Los detalles del trabajo también muestran el número de reintentos que quedan para un trabajo. Al ver los detalles de un trabajo en la pestaña **Error**, se muestra el tiempo que debe transcurrir antes de que se produzca el siguiente reintento.  

Al cancelar una implementación que no está completa, se detiene el trabajo de distribución para transferir ese contenido:  

- Luego, el estado de la implementación se actualiza para indicar que se produjo un error en la distribución y que esta se canceló por medio de una acción del usuario.  
- Este nuevo estado aparece en la ficha **Error** .  

> [!NOTE]  
> Cuando una implementación está a punto de terminar, es posible que la acción para cancelar esa distribución no se procese antes de que se complete la distribución al punto de distribución. Cuando esto ocurre, se omite la acción para cancelar la implementación, y el estado de la implementación se muestra como correcto.  
>
> Aunque puede seleccionar la opción de cancelar una distribución a un punto de distribución que se encuentra en un servidor del sitio, no tiene efecto. Este comportamiento se debe a que el servidor del sitio y el punto de distribución de un servidor del sitio comparten el mismo almacén de contenido de instancia único. No hay ningún trabajo de distribución real que cancelar.  

Cuando se redistribuye contenido que previamente no se pudo transferir a un punto de distribución, Configuration Manager comienza inmediatamente a volver a implementar ese contenido en el punto de distribución. Configuration Manager actualiza el estado de la implementación para reflejar el estado en curso de esa reimplementación.  

### <a name="tasks-to-monitor-content"></a>Tareas para supervisar el contenido

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado de distribución** y, después, haga clic en el nodo **Estado del contenido**. Este nodo muestra los paquetes.  

2. Seleccione el paquete que desea administrar.  

3. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Contenido** y seleccione **Ver estado**. En la consola se muestra información detallada del estado del paquete.

Continúe en una de las siguientes secciones para realizar otras acciones:

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Cancelación de una distribución que sigue en curso  

1. Vaya a la pestaña **En curso**.

2. En el panel **Detalles del activo**, haga clic con el botón derecho en la entrada de la distribución que quiera cancelar y seleccione **Cancelar**.  

3. Seleccione **Sí** para confirmar la acción y cancelar el proceso de distribución a ese punto de distribución.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Redistribución del contenido que no se ha podido distribuir  

1. Cambie a la pestaña **Error**.

2. En el panel **Detalles del activo**, haga clic con el botón derecho en la entrada de la distribución que quiera redistribuir y seleccione **Redistribuir**.  

3. Seleccione **Sí** para confirmar la acción e iniciar el proceso de redistribución a ese punto de distribución.  


## <a name="distribution-point-group-status"></a>Estado del grupo de puntos de distribución

El nodo **Estado de grupo de puntos de distribución** en el área de trabajo **Supervisión** proporciona información acerca de los grupos de puntos de distribución. Puede revisar información como la siguiente:  

- El nombre, la descripción y el estado del grupo de puntos de distribución
- El número de puntos de distribución que pertenecen al grupo de puntos de distribución
- El número de paquetes que se asignaron al grupo
- La tasa de compatibilidad

También puede ver la siguiente información detallada del estado:  

- Errores del grupo de puntos de distribución  
- El número de distribuciones que están en curso
- El número de distribuciones que son correctas  

### <a name="monitor-distribution-point-group-status"></a>Supervisión del estado del grupo de puntos de distribución  

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado de distribución** y, después, haga clic en el nodo **Estado de grupo de puntos de distribución**. Se muestran los grupos de puntos de distribución.  

2. Seleccione el grupo de puntos de distribución para el que quiera obtener información detallada de su estado.  

3. En la pestaña **Inicio** de la cinta de opciones, seleccione **Ver estado**. Se muestra información detallada del estado del grupo de puntos de distribución.  


## <a name="distribution-point-configuration-status"></a>Estado de configuración de los puntos de distribución

El nodo **Estado de configuración de punto de distribución** en el área de trabajo **Supervisión** proporciona información acerca del punto de distribución. Puede revisar los atributos que están habilitados para el punto de distribución, como el entorno PXE, la multidifusión y la validación del contenido. Revise también el estado de distribución del punto de distribución.

> [!WARNING]  
> El estado de la configuración del punto de distribución se refiere a las últimas 24 horas. Si el punto de distribución tiene un error y se recupera, el estado del error podría mostrarse hasta 24 horas después de que se recupere el punto de distribución.  

### <a name="monitor-distribution-point-configuration-status"></a>Supervisión del estado de configuración del punto de distribución  

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado de distribución** y, después, haga clic en el nodo **Estado de configuración de punto de distribución**.  

2. Seleccione un punto de distribución.  

3. En el panel de resultados, cambie a la pestaña **Detalles**. Se muestra información del estado del punto de distribución.  


## <a name="client-data-sources-dashboard"></a>Panel de orígenes de datos de cliente

Use el panel **Orígenes de datos de cliente** para entender mejor desde dónde los clientes obtienen el contenido de su entorno. El panel empieza a mostrar los datos después de que los clientes descarguen contenido y notifiquen esa información al sitio. Este proceso puede tardar hasta 24 horas.

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Debe habilitar la característica **Caché del mismo nivel de cliente** antes de usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../manage/install-in-console-updates.md#bkmk_options).  

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado de distribución** y, después, haga clic en el nodo **Orígenes de datos de cliente**. Seleccione un período de tiempo para aplicarlo al panel. Después, seleccione el grupo de límites del que desea ver información. Puede mantener el puntero sobre los iconos para ver más detalles sobre los distintos orígenes de contenido o directiva.

Use también el informe **Orígenes de datos de cliente - Resumen** para ver un resumen de los orígenes de datos de cliente de cada grupo de límites.

### <a name="dashboard-tiles"></a>Mosaicos del panel

En el panel se incluyen los iconos siguientes:  

#### <a name="client-content-sources"></a>Orígenes de contenido de cliente

Se muestra el origen desde el que obtienen contenido los clientes:

- Punto de distribución
- [Punto de distribución de nube](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Almacenamiento en caché del mismo nivel](../../../plan-design/hierarchy/client-peer-cache.md)
- [Optimización de distribución](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (a partir de la versión 1906)<sup>[Nota 1](#bkmk_note1)</sup>
- Microsoft Update: Los dispositivos informan a este origen cuando el cliente de Configuration Manager descarga actualizaciones de software de los servicios en la nube de Microsoft. Estos servicios incluyen Microsoft Update y Aplicaciones de Microsoft 365 para empresas.

![Icono Orígenes de contenido de cliente en el panel](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> A partir de la versión 1906,<!--3555759-->para incluir la optimización de distribución en este panel, realice las acciones siguientes:
>
> - Configure la opción de cliente **Enable installation of Express Updates on clients** (Habilitar la instalación de actualizaciones rápidas en clientes) en el grupo Actualizaciones de software.
>
> - Implementación de actualizaciones rápidas de Windows 10
>
> Para obtener más información, consulte [Administración de archivos de instalación rápida para actualizaciones de Windows 10](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Puntos de distribución

Se muestra el número de puntos de distribución que forman parte del grupo de límites seleccionado.

#### <a name="clients-that-used-a-distribution-point"></a>Clientes que utilizan un punto de distribución

Del número de clientes que están en el grupo de límites seleccionado, este icono muestra cuántos han usado un punto de distribución para obtener el contenido.

#### <a name="peer-cache-sources"></a>Orígenes de almacenamiento en caché del mismo nivel

Para el grupo de límites seleccionado, este icono muestra cuántos orígenes de caché del mismo nivel han informado del historial de descargas.

#### <a name="clients-that-used-a-peer"></a>Clientes que usan un elemento del mismo nivel

Del número de clientes que están en el grupo de límites seleccionado, este icono muestra cuántos han usado un origen de caché del mismo nivel para obtener el contenido.

#### <a name="top-distributed-content"></a>Contenido distribuido superior

Los paquetes más distribuidos por tipo de origen
