---
title: Supervisión del estado de Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga información acerca de cómo supervisar Endpoint Protection en la jerarquía de Configuration Manager.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 18bbbfc6486a1e5a784603e6725629d966f6c11a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706283"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Cómo supervisar el estado de Endpoint Protection

*Se aplica a: Configuration Manager (rama actual)*

Puede supervisar Endpoint Protection en la jerarquía de Microsoft Configuration Manager por medio del nodo **Estado de Endpoint Protection** en **Seguridad** del área de trabajo **Supervisión**, del nodo **Endpoint Protection** del área de trabajo **Activos y compatibilidad** y del uso de informes.  

##  <a name="how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a> Supervisión de Endpoint Protection mediante el nodo de estado de Endpoint Protection  

1. En la consola de Configuration Manager, haga clic en **Supervisión**.  

2. En el área de trabajo **Supervisión**, expanda **Seguridad** y, luego, haga clic en **Estado de Endpoint Protection**.  

3. En el **colección** seleccione la colección para la que desea ver información de estado.  

   > [!IMPORTANT]
   >  Las colecciones están disponibles para la selección en los casos siguientes:  
   > 
   > - Si selecciona la opción **Ver esta recopilación en el panel de Endpoint Protection** en la pestaña **Alerta**s del cuadro de diálogo <em><nombre de recopilación\></em>**Propiedades**.  
   >   -   Al implementar una directiva antimalware de Endpoint Protection en la recopilación.  
   >   -   Al habilitar e implementar la configuración de cliente de Endpoint Protection en la recopilación.  

4. Revise la información que se muestra en el **estado de seguridad** y **estado operativo** secciones. Puede hacer clic en cualquier vínculo de estado para crear una recopilación temporal en el **dispositivos** nodo en el **activos y compatibilidad** área de trabajo. La colección temporal contiene los equipos con el estado seleccionado.  

   > [!IMPORTANT]  
   >  La información que se muestra en el nodo **Estado de Endpoint Protection** se basa en los últimos datos que se resumen a partir de la base de datos de Configuration Manager y puede no estar actualizada. Si desea recuperar los datos más recientes, en la pestaña **Inicio** , haga clic en **Ejecutar resumen**, o haga clic en **Programar resumen** para ajustar el intervalo del resumen.  

##  <a name="how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a> Supervisión de Endpoint Protection en el área de trabajo Activos y compatibilidad  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el **activos y compatibilidad** área de trabajo, realice una de las siguientes acciones:  

    -   Haga clic en **dispositivos**. En el **dispositivos** lista, seleccione un equipo y, a continuación, haga clic en el **Detalles de Malware** ficha.  

    -   Haga clic en **recopilaciones de dispositivos**. En la lista **Recopilaciones de dispositivos** , seleccione la recopilación que contiene el equipo que desea supervisar y, en la pestaña **Inicio** , en el grupo **Recopilación** , haga clic en **Mostrar miembros**.  

3.  En la lista *<nombre de recopilación\>* , seleccione un equipo y luego haga clic en la pestaña **Detalles de malware**.  

##  <a name="how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a> Supervisión de Endpoint Protection mediante informes  
 Utilice los siguientes informes para ayudarle a ver la información sobre Endpoint Protection en su jerarquía. También puede usar estos informes para ayudar a solucionar posibles problemas de Endpoint Protection. Para obtener más información sobre cómo configurar informes en Configuration Manager, consulte [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md) y [Archivos de registro](../../core/plan-design/hierarchy/log-files.md). Los informes de Endpoint Protection están en la carpeta de Endpoint Protection.  

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|**Informe de actividad de antimalware**|Muestra una visión general de la actividad de antimalware para una colección especificada.|  
|**Equipos infectados**|Muestra una lista de equipos en los que se detecta una amenaza especificada.|  
|**Usuarios principales de amenazas**|Muestra una lista de usuarios con el mayor número de amenazas detectadas.|  
|**Lista de amenazas de usuario**|Muestra una lista de amenazas que se han encontrado para una cuenta de usuario especificada.|  

## <a name="malware-alert-levels"></a>Niveles de alerta de malware  
 Use la siguiente tabla para identificar los diferentes niveles de alerta de Endpoint Protection que podrían mostrarse en los informes o en la consola de Configuration Manager.  

|Nivel de alerta|Descripción|  
|-----------------|-----------------|  
|**Error**|Endpoint Protection no pudo corregir el malware. Compruebe los registros para obtener información detallada del error.<br /><br /> **Nota:** Para obtener una lista de los archivos de registro de Configuration Manager y Endpoint Protection, consulte la sección "Endpoint Protection" del tema [Archivos de registro](../../core/plan-design/hierarchy/log-files.md).|  
|**Quitado**|Endpoint Protection quitó correctamente el malware.|  
|**En cuarentena**|Endpoint Protection trasladó el malware a una ubicación segura y evitó su ejecución hasta que lo quite o permita que se ejecute.|  
|**Limpio**|Se ha limpiado el malware del archivo infectado.|  
|**Permitido**|Un usuario administrativo seleccionado para permitir que el software que contiene el ejecución de malware.|  
|**Ninguna acción**|Endpoint Protection no realizó ninguna acción en el malware. Esto puede ocurrir si el equipo se reinicia después de que se ha detectado malware y ya no se detecta software malintencionado; Por ejemplo, si una red asignada en la unidad se detecta software malintencionado no vuelva a conectarse cuando se reinicia el equipo.|  
|**Bloqueado**|Endpoint Protection bloqueó la ejecución del malware. Esto puede ocurrir si se encuentra un proceso en el equipo para que contenga código malintencionado.|
