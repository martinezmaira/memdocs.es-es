---
title: Supervisar actualizaciones de software
titleSuffix: Configuration Manager
description: La consola de Configuration Manager proporciona alertas y estados para supervisar la compatibilidad y las actualizaciones.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110379"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>Supervisar actualizaciones de software en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager ofrece muchas maneras de ayudarle a supervisar los objetos, procesos e información de compatibilidad de las actualizaciones de software. Use las secciones siguientes para supervisar las actualizaciones de software.

## <a name="software-updates-dashboard"></a>Panel de actualizaciones de software

*(Se introdujo en la versión 1610)*

A partir de Configuration Manager versión 1610, puede usar el panel de actualizaciones de software para ver el estado de cumplimiento actual de los dispositivos de la organización y analizar rápidamente los datos para ver los dispositivos que están en riesgo. Para ver el panel, vaya a **Supervisión** > **Introducción** > **Seguridad** > **Software Updates Dashboard** (Panel de actualizaciones de software).

## <a name="drill-through-required-updates"></a>Obtención de detalles de actualizaciones necesarias
<!--4224414-->
*(Se introdujo en la versión 1906)*

Se pueden obtener detalles de las estadísticas de compatibilidad para ver qué dispositivos requieren una actualización de software de Aplicaciones de Microsoft 365 específica. Para ver la lista de dispositivos, necesita permiso para ver las actualizaciones y las colecciones a las que pertenecen los dispositivos. Para explorar en profundidad la lista de dispositivos:

1. Vaya a **Biblioteca de software** > **Actualizaciones de software** > **Todas las actualizaciones de software**.
1. Seleccione las actualizaciones que requiera al menos un dispositivo.
1. En la pestaña **Resumen** encontrará un gráfico circular bajo **Estadísticas**.
1. Seleccione el hipervínculo **Vista necesaria** situado junto al gráfico circular para obtener los detalles de la lista de dispositivos.
1. Esta acción le llevará a un nodo temporal en **Dispositivos** donde podrá ver los dispositivos que requieren la actualización. También puede realizar acciones para el nodo, como crear una colección a partir de la lista.


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> Alertas de actualizaciones de software  
 Puede configurar alertas de actualizaciones de software a fin de notificar a los usuarios administrativos cuándo los niveles de compatibilidad de las implementaciones de actualizaciones de software están por debajo del porcentaje configurado. Puede configurar alertas para las implementaciones de actualizaciones de software en las siguientes ubicaciones:  

-   Configuración de ADR: puede configurar las opciones de alertas en el Asistente para crear regla de implementación automática y en las propiedades de la regla de implementación automática.  

-   Configuración de implementación: puede configurar las opciones de alertas en el Asistente para implementar actualizaciones de software y en las propiedades de la implementación.  

Después de configurar las opciones de alertas, si se producen las condiciones especificadas, Configuration Manager genera una alerta. Puede revisar las alertas de actualizaciones de software en las siguientes ubicaciones:  

1.  Revise las alertas recientes en el nodo **Actualizaciones de software** en el área de trabajo **Biblioteca de software** .  

2.  Administre las alertas configuradas en el nodo **Alertas** en el área de trabajo **Supervisión** .  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a> Estado de sincronización de las actualizaciones de software  
 Después de iniciar el proceso de sincronización, puede usar la consola de Configuration Manager para supervisar el proceso de sincronización de todos los puntos de actualización de software de la jerarquía. Utilice el siguiente procedimiento para supervisar el proceso de sincronización de la actualización de software.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para supervisar el proceso de sincronización de las actualizaciones de software  

- En la consola de Configuration Manager, navegue hasta **Supervisión** > **Introducción** > **Estado de sincronización de punto de actualización de software**.  

    Los puntos de la actualización de software en su jerarquía de Configuration Manager se muestran en el panel de resultados. Desde esta vista, puede supervisar el estado de la sincronización de todos los puntos de actualización de software. Para consultar más información detallada sobre el proceso de sincronización, puede revisar el archivo wsyncmgr.log, que se encuentra en <*Ruta de instalación de Configuration Manager*>\Logs en cada servidor de sitio.  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> Estado de implementación de actualizaciones de software  
 Después de implementar las actualizaciones de software en un grupo de actualizaciones de software, o después de implementar una actualización de software individual, puede supervisar el estado de implementación. Utilice el siguiente procedimiento para supervisar el estado de implementación de un grupo de actualizaciones de software o de una actualización de software.  

#### <a name="to-monitor-deployment-status"></a>Para supervisar el estado de implementación  

1.  En la consola de Configuration Manager, navegue hasta **Supervisión** > **Información general** > **Implementaciones**.  

2.  Haga clic en el grupo de actualizaciones de software o en una actualización de software cuyo estado de implementación desea supervisar.  

3.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Ver estado**.  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> Informes de actualizaciones de software  
 Los mensajes de estado para las actualizaciones de software proporcionan información acerca de la compatibilidad de las actualizaciones de software y el estado de la evaluación y aplicación de las implementaciones de actualizaciones de software. Puede ejecutar informes de actualizaciones de software para mostrar los mensajes de estado. Se encuentran disponibles más de 30 informes predefinidos de actualizaciones de software. Se organizan en diferentes categorías y se pueden utilizar para proporcionar información específica acerca de las implementaciones y actualizaciones de software. Además de utilizar los informes preconfigurados, también puede crear informes de actualizaciones de software personalizados según las necesidades de la empresa. Para obtener más información, vea [Operaciones y mantenimiento de informes](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Informes de actualizaciones de software recomendados
Los siguientes son algunos de los informes que son útiles para identificar posibles problemas: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Cumplimiento 9 - Mantenimiento general y cumplimiento (a partir de la versión 1806)
El informe incluye las siguientes partes:

- **Clientes correctos frente a clientes totales**: en este gráfico de barras se comparan los clientes "correctos" que se han comunicado con el sitio en el período de tiempo especificado frente al número total de clientes de la colección especificada.
- **Información general de cumplimiento**: en este gráfico circular se muestra el estado de cumplimiento general de un grupo de actualizaciones de software específico de clientes activos de la colección especificada.
- **Cinco principales actualizaciones no conformes por identificador de artículo**: en este gráfico de barras se muestran las cinco principales actualizaciones de software del grupo especificado no conformes de los clientes activos de la colección especificada.
- En la parte inferior del informe se muestra una tabla con detalles adicionales, en la que se enumeran las actualizaciones de software del grupo especificado.

#### <a name="management-2---updates-required-but-not-deployed"></a>Administración 2 - Actualizaciones necesarias pero no implementadas

Este informe muestra las actualizaciones de software específicas del proveedor en una clasificación de actualizaciones específica que se detectaron como requeridas en los clientes pero que no se implementaron en una colección especificada. 

#### <a name="troubleshooting-2---deployment-errors"></a>Solución de problemas 2 - Errores de implementación

Este informe devuelve los errores de implementación del sitio y un recuento de equipos en los que se produce cada error. 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a> Supervisar contenido  
 Puede supervisar el contenido en la consola de Configuration Manager para consultar el estado de todos los tipos de paquetes en relación con los puntos de distribución asociados. Esto puede incluir el estado de validación del contenido del paquete, el estado del contenido asignado a un grupo de puntos de distribución específico, el estado del contenido asignado a un punto de distribución y el estado de las características opcionales de cada punto de distribución (validación de contenido, PXE y multidifusión).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Supervisión del estado del contenido  
 El nodo **Estado de contenido** en el área de trabajo **Supervisión** proporciona información acerca de los paquetes de contenido. Puede consultar información general acerca del paquete, el estado de distribución del paquete e información de estado detallada acerca del paquete. Utilice el procedimiento siguiente para ver el estado del contenido.  

#### <a name="to-monitor-content-status"></a>Para supervisar el estado del contenido  

1.  En la consola de Configuration Manager, navegue hasta **Supervisión** > **Información general** > **Estado de distribución** > **Estado del contenido**. Se mostrarán los paquetes.  

2.  Seleccione el paquete del que desea ver información de estado detallada.  

3.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del paquete.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Estado del grupo de puntos de distribución  
 El nodo **Estado de grupo de puntos de distribución** en el área de trabajo **Supervisión** proporciona información acerca de los grupos de puntos de distribución. Puede consultar información general acerca del grupo de puntos de distribución, como el estado y la tasa de compatibilidad del grupo de puntos de distribución, así como información de estado detallada acerca del grupo de puntos de distribución. Utilice el procedimiento siguiente para ver el estado del grupo de puntos de distribución.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para supervisar el estado del grupo de puntos de distribución  

1.  En la consola de Configuration Manager, navegue hasta **Supervisión** > **Información general** > **Estado de distribución** > **Estado del grupo de puntos de distribución**. Se mostrarán los grupos de puntos de distribución.  

2.  Seleccione el grupo de puntos de distribución del que desea ver información de estado detallada.  

3.  En la pestaña **Inicio** , haga clic en **Ver estado**. Se mostrará información detallada del estado del grupo de puntos de distribución.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> Estado de configuración de los puntos de distribución  
 El nodo **Estado de configuración de punto de distribución** en el área de trabajo **Supervisión** proporciona información acerca del punto de distribución. Puede revisar los atributos que están habilitados para el punto de distribución, como PXE, multidifusión y validación de contenido. También puede ver información detallada del estado del punto de distribución. Utilice el procedimiento siguiente para ver el estado de configuración del punto de distribución.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para supervisar el estado de configuración de punto de distribución  

1.  En la consola de Configuration Manager, navegue hasta **Supervisión** > **Información general** > **Estado de distribución** > **Estado de configuración de punto de distribución**. Se mostrarán los puntos de distribución.  

2.  Seleccione el punto de distribución del que desea ver información de estado de punto de distribución.  

3.  En el panel de resultados, haga clic en la pestaña **Detalles** . Se mostrará información de estado del punto de distribución.  

## <a name="next-steps"></a>Pasos siguientes

- [Archivos de registro de las actualizaciones de software](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Notas del producto de administración de actualizaciones de software](https://www.microsoft.com/download/confirmation.aspx?id=44578)
