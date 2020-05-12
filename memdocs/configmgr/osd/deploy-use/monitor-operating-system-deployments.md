---
title: Supervisar implementaciones del sistema operativo
titleSuffix: Configuration Manager
description: Para ayudarle a supervisar los objetos de implementación de sistema operativo, la consola de Configuration Manager proporciona varios indicadores de estado, informes y alertas.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7afab9fbbb443b2f9fb4af15a3805c0b7df7a014
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802173"
---
# <a name="monitor-operating-system-deployments-in-configuration-manager"></a>Supervisión de implementaciones de sistemas operativos en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para ayudarle a supervisar los objetos de implementación de sistema operativo, la consola de Configuration Manager proporciona lo siguiente.  


##  <a name="alerts-for-operating-system-deployments"></a><a name="BKMK_OSDAlerts"></a> Alertas para implementaciones de sistemas operativos  
 Puede configurar una alerta en la configuración de implementación de secuencia de tareas para notificar a los usuarios administrativos cuando los niveles de cumplimiento de la implementación están por debajo del porcentaje configurado.  

 Después de configurar las opciones de alertas, si se producen las condiciones especificadas, Configuration Manager genera una alerta. Puede revisar alertas de implementación de secuencia de tareas en las siguientes ubicaciones:  

1.  Revise las alertas recientes en el nodo **Sistemas operativos** del área de trabajo **Biblioteca de software** .  

2.  Administre las alertas configuradas en el nodo **Alertas** en el área de trabajo **Supervisión** .  

##  <a name="task-sequence-deployment-status"></a><a name="BKMK_TSDeployStatus"></a> Estado de implementación de la secuencia de tareas  
 Después de implementar una secuencia de tareas, puede supervisar el estado de implementación. Use el siguiente procedimiento para supervisar el estado de implementación de una secuencia de tareas.  

#### <a name="to-monitor-deployment-status"></a>Para supervisar el estado de implementación  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo Supervisión, haga clic en **Implementaciones**.  

3.  Haga clic en la secuencia de tareas cuyo estado de implementación quiere supervisar.  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Ver estado**.  

> [!NOTE]  
> Cuando se inicia una actualización, se genera el mensaje de estado 52200. Contiene el usuario que ha realizado la actualización.  

##  <a name="operating-system-deployment-reports"></a><a name="BKMK_TSReports"></a> Informes de implementación de sistema operativo  
 Hay muchos informes de implementación de sistema operativo predefinidos disponibles. Se organizan en diferentes categorías y se pueden usar para proporcionar información específica sobre migración de estado e implementaciones de secuencias de tareas. Además de utilizar los informes preconfigurados, también puede crear informes de actualizaciones de software personalizados según las necesidades de la empresa. Para obtener más información, vea [Operaciones y mantenimiento de informes](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a> Supervisar contenido  
 Puede supervisar el contenido en la consola de Configuration Manager para consultar el estado de todos los tipos de paquetes en relación con los puntos de distribución asociados. Esto puede incluir el estado de validación del contenido del paquete, el estado del contenido asignado a un grupo de puntos de distribución específico, el estado del contenido asignado a un punto de distribución y el estado de las características opcionales de cada punto de distribución (validación de contenido, PXE y multidifusión).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Supervisión del estado del contenido  
 El nodo **Estado de contenido** en el área de trabajo **Supervisión** proporciona información acerca de los paquetes de contenido. Puede consultar información general acerca del paquete, el estado de distribución del paquete e información de estado detallada acerca del paquete. Utilice el procedimiento siguiente para ver el estado del contenido.  

#### <a name="to-monitor-content-status"></a>Para supervisar el estado del contenido  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo Supervisión, expanda **Estado de distribución**y, a continuación, haga clic en **Estado de contenido**. Se mostrarán los paquetes.  

3.  Seleccione el paquete del que desea ver información de estado detallada.  

4.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del paquete.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Estado del grupo de puntos de distribución  
 El nodo **Estado de grupo de puntos de distribución** en el área de trabajo **Supervisión** proporciona información acerca de los grupos de puntos de distribución. Puede consultar información general acerca del grupo de puntos de distribución, como el estado y la tasa de compatibilidad del grupo de puntos de distribución, así como información de estado detallada acerca del grupo de puntos de distribución. Utilice el procedimiento siguiente para ver el estado del grupo de puntos de distribución.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para supervisar el estado del grupo de puntos de distribución  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo Supervisión, expanda **Estado de distribución**y, a continuación, haga clic en **Estado de grupo de puntos de distribución**. Se mostrarán los grupos de puntos de distribución.  

3.  Seleccione el grupo de puntos de distribución del que desea ver información de estado detallada.  

4.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del grupo de puntos de distribución.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> Estado de configuración de los puntos de distribución  
 El nodo **Estado de configuración de punto de distribución** en el área de trabajo **Supervisión** proporciona información acerca del punto de distribución. Puede revisar los atributos que están habilitados para el punto de distribución, como PXE, multidifusión y validación de contenido. También puede ver información detallada del estado del punto de distribución. Utilice el procedimiento siguiente para ver el estado de configuración del punto de distribución.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para supervisar el estado de configuración de punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo Supervisión, expanda **Estado de distribución**y, a continuación, haga clic en **Estado de configuración de punto de distribución**. Se mostrarán los puntos de distribución.  

3.  Seleccione el punto de distribución del que desea ver información de estado de punto de distribución.  

4.  En el panel de resultados, haga clic en la pestaña **Detalles** . Se mostrará información de estado del punto de distribución.  
