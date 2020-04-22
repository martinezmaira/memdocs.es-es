---
title: Supervisión y planeamiento de la administración de energía
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo supervisar y planear la administración de energía en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a4e5ee9c35dd96f79ea1a88ab09200d4386a7535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696563"
---
# <a name="how-to-monitor-and-plan-for-power-management-in-configuration-manager"></a>Cómo supervisar y planear la administración de energía en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La siguiente información puede ayudarle a supervisar y planear la administración de energía en Configuration Manager.  

##  <a name="how-to-use-reports-for-power-management"></a><a name="BKMK_How_to_use_reports"></a> Cómo usar informes de administración de energía  
 La administración de energía en Configuration Manager incluye varios informes que le ayudarán a analizar la configuración de energía del equipo y el consumo de energía en su organización. Los informes también pueden usarse como ayuda para solucionar problemas.  

 Para poder usar los informes de administración de energía, debe configurar los informes para la jerarquía. Para obtener más información sobre los informes en Configuration Manager, consulte [Introducción a los informes](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  La información de administración de energía usada en los informes diarios se conserva en la base de datos de sitio de Configuration Manager durante 31 días.  
>           La información de administración de energía usada en los informes mensuales se conserva en la base de datos de sitio de Configuration Manager durante 13 meses.  
>   
>  Cuando ejecute informes durante las fases de supervisión, planeamiento y cumplimiento de la administración de energía, guarde o exporte los resultados de aquellos cuyos datos quiera conservar para una comparación posterior por si Configuration Manager los elimina más adelante.  

## <a name="list-of-power-management-reports"></a>Lista de informes de administración de energía  
 Las listas siguientes detallan los informes de administración de energía que están disponibles en Configuration Manager.  

> [!NOTE]  
>  Informes de administración de energía muestran el número de equipos físicos y el número de equipos virtuales en una recopilación seleccionada. Sin embargo, en los informes de administración de energía únicamente se muestra la información de administración de energía de los equipos físicos.  

###  <a name="computer-activity-report"></a><a name="BKMK_Activity"></a> Informe actividad del equipo  
 El informe **Actividad de equipo** muestra un gráfico con la siguiente actividad para una recopilación especificada durante un período determinado:  

- **Computer On** : el equipo se ha activado.  

- **Monitor On** : el monitor se ha activado.  

- **User Active** : se ha detectado actividad del mouse del equipo, el teclado del equipo o de una conexión de Escritorio remoto con el equipo.  

  Este informe se usa durante las fases de supervisión, planeamiento y aplicación para ayudarle a entender la alineación entre la actividad del equipo, la actividad del monitor y la actividad del usuario durante un período de 24 horas. Si ejecuta el informe durante varios días, los datos se agregan durante ese período. Este informe puede ayudarle a determinar las horas habituales laborables (punta) y no laborales (fuera de horas punta) para una recopilación seleccionada para ayudarle a decidir cuándo debe aplicar los planes de administración de energía configurado.  

  El gráfico muestra los períodos de tiempo en que un equipo puede estar encendido, pero no hay ninguna actividad de usuario. Considere la posibilidad de aplicar una configuración de energía más restrictiva en esos momentos para ahorrar en los costos de energía de los equipos que están activados, pero no se usan. Un equipo se cuenta como activo si ha habido actividad de equipo, de usuario o de monitor durante un minuto o más en la hora mostrada en el gráfico. Si un equipo no notifica datos de administración de energía, no se incluirá en el informe **Actividad de equipo** .  

  Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Fecha de inicio**|En la lista desplegable, seleccione la fecha de inicio para este informe.|  
|**Fecha de finalización (opcional)**|En la lista desplegable, seleccione la fecha de finalización opcional para este informe.|  
|**Nombre de recopilación**|En la lista desplegable, seleccione la recopilación que quiere usar para este informe.|  
|**Tipo de dispositivo**|En la lista desplegable, seleccione el tipo de equipo que se desea un informe. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles).|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Si no se especifica un valor para **Fecha de finalización (opcional)** , este informe contiene un vínculo para el siguiente informe que proporciona más información.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles de la actividad del equipo**|Haga clic en el vínculo **Haga clic para obtener información detallada** para ver una lista de equipos activos, inactivos y sin informes para la fecha especificada.<br /><br /> Para obtener más información, consulte [Computer Activity Details Report](#BKMK_Activity_Details) en este tema.|  

###  <a name="computer-activity-by-computer-report"></a><a name="BKMK_Comp_Activity_by_computer"></a> Informe Actividad de equipo por equipo  
 El informe **Actividad de equipo por equipo** muestra un gráfico con la siguiente actividad para un equipo especificado durante una fecha determinada:  

- **Computer On** : el equipo se ha activado.  

- **Monitor On** : el monitor se ha activado.  

- **User Active** : se ha detectado actividad del mouse del equipo, el teclado del equipo o de una conexión de Escritorio remoto con el equipo.  

  Este informe puede ejecutarse de forma independiente o puede llamarlo el informe **Detalles de actividad de equipo** .  

> [!NOTE]  
>  Se recopila información sobre la actividad de equipo de los equipos cliente durante el inventario de hardware. Según la hora en que se ejecuta el inventario de hardware, se puede recopilar la actividad durante un plan de energía aplicado para horas punta o para horas no punta.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Fecha de informe**|En la lista desplegable, seleccione una fecha para este informe.|  
|**Nombre del equipo**|Escriba un nombre de equipo para el que quiere un informe.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles del equipo**|Haga clic en el vínculo **Haga clic para obtener información detallada** para ver las capacidades de energía, la configuración de energía y los planes de energía aplicados para el equipo seleccionado.|  

###  <a name="computer-activity-details-report"></a><a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 El informe **Detalles de actividad de equipo** muestra una lista de los equipos activos o inactivos con sus capacidades de suspensión y activación. Este informe se denomina la [Computer Activity Report](#BKMK_Activity) y no está diseñado para ser ejecutadas directamente por el administrador del sitio.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre de recopilación**|En la lista desplegable, seleccione la recopilación que quiere usar para este informe.|  
|**Fecha de informe**|En la lista desplegable, seleccione una fecha para usarla en este informe.|  
|**Hora de informe**|En la lista desplegable, seleccione una hora de la fecha especificada para la que quiere ejecutar este informe. Los valores válidos están comprendidos entre **12 a.m.** y **11 p.m**.|  
|**Estado del equipo**|En la lista desplegable, seleccione el estado del equipo para el que se va a ejecutar este informe. Los valores válidos son **Todos** (los equipos que se han activado o desactivado), **Activado** (los equipos que se han activado) y **Desactivado** (los equipos que se han desactivado o que están en modo de suspensión o hibernación). Estos valores se devuelven solo para el período de informe seleccionado.|  
|**Tipo de dispositivo**|En la lista desplegable, seleccione el tipo de equipo que se desea un informe. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles). Estos valores se devuelven solo para el período de informe seleccionado.|  
|**Con capacidad de suspensión**|En la lista desplegable, seleccione si desea mostrar los equipos capaces de suspensión en el informe. Los valores válidos son **Todos** (equipos con y sin capacidad de suspensión), **No** (equipos sin capacidad de suspensión) y **Sí** (equipos con capacidad de suspensión).|  
|**Con capacidad de activación desde suspensión**|En la lista desplegable, seleccione si desea mostrar los equipos capaces de reactivación de una suspensión en el informe. Los valores válidos son **Todos** (equipos con y sin capacidad de reactivación tras suspensión), **No** (equipos sin capacidad de reactivación tras suspensión) y **Sí** (equipos con capacidad de reactivación tras suspensión).|  
|**Plan de energía**|En la lista desplegable, seleccione los tipos de plan de energía que desea mostrar en el informe. Los valores válidos son **Todos** (equipos que no tienen ningún plan de administración de energía aplicado; equipos que tienen un plan de administración de energía aplicado; equipos excluidos de la administración de energía), **Sin especificar** (equipos que no tienen un plan de administración de energía aplicado) **Definido** (equipos que tienen un plan de administración de energía aplicado) y **Excluido** (equipos que se han excluido de la administración de energía).|  
|**Sistema operativo**|En la lista desplegable, seleccione los sistemas operativos que quiere mostrar en el informe o seleccione **Todos** para mostrar todos los sistemas operativos.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Actividad de equipo por equipo**|Haga clic en un nombre de equipo para ver la actividad específica para ese equipo a lo largo de un período de elaboración de informes seleccionado. Estas actividades incluyen **Equipo encendido** (¿el equipo se ha activado), **Monitor encendido** (¿el monitor se ha activado?) y **Usuario activo** (se ha detectado actividad de teclado o mouse del equipo o una conexión a escritorio remoto).<br /><br /> Para obtener más información, consulte [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) en este tema.|  

###  <a name="computer-details-report"></a><a name="BKMK_Computer_Details"></a> Informe Detalles de equipo  
 El informe **Detalles de equipo** muestra información detallada sobre las capacidades de energía, las configuraciones de energía y los planes de energía aplicados a un equipo especificado. Los informes **Actividad de equipo por equipo** , **Equipos con varios planes de energía** , **Capacidades de energía** y **Detalles de configuración de energía** llaman a este informe. No está diseñado para que el administrador del sitio lo ejecute directamente.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre del equipo**|Escriba un nombre de equipo para el que quiere un informe.|  
|**Modo de energía**|En la lista desplegable, seleccione el tipo de configuración de energía que quiere mostrar en los resultados del informe. Seleccione **Con corriente alterna** para ver la configuración de energía para cuando el equipo está conectado y **Con batería** para ver la configuración de energía para cuando el equipo funciona con batería.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe no se vincula a otros informes de administración de energía.  

###  <a name="computer-not-reporting-details-report"></a><a name="BKMK_Not_Reporting"></a> Informe El equipo no proporciona detalles  
 El informe **El equipo no proporciona detalles** muestra una lista de equipos de una recopilación especificada que no han notificado ninguna actividad de energía en una fecha y hora especificadas. El **Computer Activity Report** llama a este informe y no está diseñado para que el administrador del sitio lo ejecute directamente.  

> [!NOTE]  
>  Los equipos notifican la información de administración de energía como parte de la programación de inventario de hardware. Antes de considerar que un equipo no informa, asegúrese de que ha notificado el inventario de hardware.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre de recopilación**|En la lista desplegable, seleccione la recopilación que quiere usar para este informe.|  
|**Fecha de informe**|En la lista desplegable, seleccione una fecha para este informe.|  
|**Hora de informe**|En la lista desplegable, seleccione una hora de la fecha especificada para la que quiere ejecutar este informe. Los valores válidos están comprendidos entre **12 a.m.** y **11 p.m**.|  
|**Tipo de dispositivo**|En la lista desplegable, seleccione el tipo de equipo que se desea un informe. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles). Estos valores se devuelven solo para el período de informe seleccionado.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe no se vincula a otros informes de administración de energía.  

###  <a name="computers-excluded"></a><a name="BKMK_Excluded"></a> Equipos excluidos  
 El informe **Equipos excluidos** muestra una lista de equipos de una recopilación especificada que se han excluido de la administración de energía de Configuration Manager.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Colección**|En la lista desplegable, seleccione una colección para este informe.|  
|**Motivo**|En la lista desplegable, seleccione el motivo por el que los equipos se excluyeron de la administración de energía. Puede mostrar  **Todos** (todos los equipos excluidos), **Excluido por el administrador** (solo equipos que se han excluido por un usuario administrativo) y **Excluido por el usuario** (solo los equipos que se han excluido por un usuario del Centro de software).|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles del equipo de energía**|Haga clic en el nombre de un equipo para ver las capacidades de energía, la configuración de energía y los planes de energía aplicados para el equipo seleccionado.<br /><br /> Para obtener más información, consulte [Computer Details Report](#BKMK_Computer_Details) en este tema.|  

###  <a name="computers-with-multiple-power-plans"></a><a name="BKMK_Multiple"></a> Equipos con varios planes de energía  
 El informe **Equipos con varios planes de energía** muestra una lista de equipos que son miembros de varias recopilaciones y cada una de las cuales aplica un plan de energía diferente. Para cada equipo con una configuración de energía potencialmente conflictiva, el informe muestra el nombre del equipo y los planes de energía que se aplican para cada recopilación de la que el equipo es miembro.  

> [!IMPORTANT]  
>  Si un equipo es miembro de varias recopilaciones, donde cada recopilación tiene planes de energía diferentes, se aplicará el plan de energía menos restrictivo.  
>   
>  Si un equipo es miembro de varias recopilaciones, donde cada recopilación tiene tiempos de activación diferentes, se usará la hora más cercana a la medianoche.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre de recopilación**|En la lista desplegable, seleccione una colección para este informe.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles del equipo de energía**|Haga clic en el nombre de un equipo para ver las capacidades de energía, la configuración de energía y los planes de energía aplicados para el equipo seleccionado.<br /><br /> Para obtener más información, consulte [Computer Details Report](#BKMK_Computer_Details) en este tema.|  

###  <a name="energy-consumption-report"></a><a name="BKMK_Consumption"></a> Informe Consumo de energía  
 El informe **Consumo de energía** muestra la siguiente información:  

- Un gráfico que muestra el consumo de energía mensual total de los equipos en kilovatios por hora (kWh) de la recopilación especificada durante el período de tiempo especificado.  

- Un gráfico que muestra el consumo de energía promedio en kilovatios por hora (kWh) de cada equipo de la recopilación especificada durante el período de tiempo especificado.  

- Una tabla que muestra el consumo de energía mensual total en kilovatios por hora (kWh) y el consumo de energía promedio de los equipos de la recopilación especificada durante el período de tiempo especificado.  

  Esta información puede usarse como ayuda para entender las tendencias de consumo de energía en el entorno. Después de aplicar un plan de energía en los equipos de la recopilación seleccionada, el consumo de energía de los equipos debe disminuir.  

> [!NOTE]  
>  Si agrega miembros a la recopilación, o los quita de ella, después de haber aplicado un plan de energía, afectará a los resultados mostrados por el informe **Consumo de energía** y podría dificultar la comparación de los resultados de la fase de supervisión y planeamiento y la fase de aplicación.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Fecha de inicio**|En la lista desplegable, seleccione una fecha de inicio para este informe.|  
|**Fecha de finalización**|En la lista desplegable, seleccione una fecha de finalización para este informe.|  
|**Nombre de recopilación**|En la lista desplegable, seleccione una colección para este informe.|  
|**Tipo de dispositivo**|En la lista desplegable, seleccione el tipo de equipo que se desea un informe. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles). Estos valores se devuelven solo para el período de informe seleccionado.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Pueden especificarse de manera opcional los siguientes parámetros ocultos para cambiar el comportamiento de este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Equipo de escritorio encendido**|Especifique el consumo de energía de un equipo de escritorio cuando está encendido. El valor predeterminado es **0,07** kW por hora.|  
|**Equipo portátil encendido**|Especifique el consumo de energía de un equipo portátil cuando está encendido. El valor predeterminado es **0,02** kW por hora.|  
|**Equipo de escritorio suspendido**|Especifique el consumo de energía de un equipo de escritorio cuando ha entrado en suspensión. El valor predeterminado es **0,003** kW por hora.|  
|**Equipo portátil suspendido**|Especifique el consumo de energía de un equipo portátil cuando ha entrado en suspensión. El valor predeterminado es **0,001** kW por hora.|  
|**Equipo de escritorio apagado**|Especifique el consumo de energía de un equipo de escritorio cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Equipo portátil apagado**|Especifique el consumo de energía de un equipo portátil cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Monitor de escritorio encendido**|Especifique el consumo de energía de un monitor de equipo de escritorio cuando está encendido. El valor predeterminado es **0,028** kW por hora.|  
|**Monitor de portátil encendido**|Especifique el consumo de energía de un monitor de equipo portátil cuando está encendido. El valor predeterminado es **0** kW por hora.|  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe no se vincula a otros informes de administración de energía.  

###  <a name="energy-consumption-by-day-report"></a><a name="BKMK_Consumption_by_Day"></a> Informe Consumo de energía por día  
 El informe **Consumo de energía por día** muestra la siguiente información:  

- Un gráfico que muestra el consumo de energía diario total de los equipos en kilovatios por hora (kWh) de la recopilación especificada durante el período de tiempo especificado.  

- Un gráfico que muestra el consumo de energía diario promedio en kilovatios por hora (kWh) de cada equipo de la recopilación especificada durante los últimos 31 días.  

- Una tabla que muestra el consumo de energía diario total en kilovatios por hora (kWh) y el consumo de energía promedio de los equipos de la recopilación especificada durante los últimos 31 días.  

  Esta información puede usarse como ayuda para entender las tendencias de consumo de energía en el entorno. Después de aplicar un plan de energía en los equipos de la recopilación seleccionada, el consumo de energía de los equipos debe disminuir.  

> [!NOTE]  
>  Si agrega miembros a la recopilación, o los quita de ella, después de haber aplicado un plan de energía, afectará a los resultados mostrados por el informe **Consumo de energía** y podría dificultar la comparación de los resultados de la fase de supervisión y planeamiento y la fase de aplicación.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Colección**|En la lista desplegable, seleccione una colección para este informe.|  
|**Device Type**|En la lista desplegable, seleccione el tipo de equipo del que quiere informar. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles). Estos valores se devuelven solo para el período de informe seleccionado.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Pueden especificarse de manera opcional los siguientes parámetros ocultos para cambiar el comportamiento de este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Equipo de escritorio encendido**|Especifique el consumo de energía de un equipo de escritorio cuando está encendido. El valor predeterminado es **0,07** kW por hora.|  
|**Equipo portátil encendido**|Especifique el consumo de energía de un equipo portátil cuando está encendido. El valor predeterminado es **0,02** kW por hora.|  
|**Equipo de escritorio suspendido**|Especifique el consumo de energía de un equipo de escritorio cuando ha entrado en suspensión. El valor predeterminado es **0,003** kW por hora.|  
|**Equipo portátil suspendido**|Especifique el consumo de energía de un equipo portátil cuando ha entrado en suspensión. El valor predeterminado es **0,001** kW por hora.|  
|**Equipo de escritorio apagado**|Especifique el consumo de energía de un equipo de escritorio cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Equipo portátil apagado**|Especifique el consumo de energía de un equipo portátil cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Monitor de escritorio encendido**|Especifique el consumo de energía de un monitor de equipo de escritorio cuando está encendido. El valor predeterminado es **0,028** kW por hora.|  
|**Monitor de portátil encendido**|Especifique el consumo de energía de un monitor de equipo portátil cuando está encendido. El valor predeterminado es **0** kW por hora.|  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe no se vincula a otros informes de administración de energía.  

###  <a name="energy-cost-report"></a><a name="BKMK_Cost"></a> Informe Coste de energía  
 El informe **Coste de energía** muestra la siguiente información:  

- Un gráfico que muestra el coste de energía mensual total de los equipos de la recopilación especificada durante el período de tiempo especificado.  

- Un gráfico que muestra el coste de energía mensual promedio de cada equipo de la recopilación especificada durante el período de tiempo especificado.  

- Una tabla que muestra el coste de energía mensual total y el coste de energía mensual promedio de los equipos de la colección especificada durante los últimos 31 días.  

  Esta información puede usarse como ayuda para entender las tendencias de coste de energía en el entorno. Después de aplicar un plan de energía en los equipos de la recopilación seleccionada, el coste de energía de los equipos debe disminuir.  

  Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Fecha de inicio**|En la lista desplegable, seleccione una fecha de inicio para este informe.|  
|**Fecha de finalización**|En la lista desplegable, seleccione una fecha de finalización para este informe.|  
|**Coste de kWh**|Especifique el coste por kWh de electricidad. El valor predeterminado es **0,09**.<br /><br /> Puede modificar la unidad de moneda que se usa en este informe en la sección de parámetros ocultos.|  
|**Nombre de recopilación**|En la lista desplegable, seleccione la recopilación que quiere usar para este informe.|  
|**Tipo de dispositivo**|En la lista desplegable, seleccione el tipo de equipo del que quiere informar. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles). Estos valores se devuelven solo para el período de informe seleccionado.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Pueden especificarse de manera opcional los siguientes parámetros ocultos para cambiar el comportamiento de este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Equipo de escritorio encendido**|Especifique el consumo de energía de un equipo de escritorio cuando está encendido. El valor predeterminado es **0,07** kW por hora.|  
|**Equipo portátil encendido**|Especifique el consumo de energía de un equipo portátil cuando está encendido. El valor predeterminado es **0,02** kW por hora.|  
|**Equipo de escritorio suspendido**|Especifique el consumo de energía de un equipo de escritorio cuando ha entrado en suspensión. El valor predeterminado es **0,003** kW por hora.|  
|**Equipo portátil suspendido**|Especifique el consumo de energía de un equipo portátil cuando ha entrado en suspensión. El valor predeterminado es **0,001** kW por hora.|  
|**Equipo de escritorio apagado**|Especifique el consumo de energía de un equipo de escritorio cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Equipo portátil apagado**|Especifique el consumo de energía de un equipo portátil cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Monitor de escritorio encendido**|Especifique el consumo de energía de un monitor de equipo de escritorio cuando está encendido. El valor predeterminado es **0,028** kW por hora.|  
|**Monitor de portátil encendido**|Especifique el consumo de energía de un monitor de equipo portátil cuando está encendido. El valor predeterminado es **0** kW por hora.|  
|**Moneda**|Especifique la etiqueta de moneda que se debe usar para este informe. El valor predeterminado es **USD ($)** .|  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe no se vincula a otros informes de administración de energía.  

###  <a name="energy-cost-by-day-report"></a><a name="BKMK_Cost_by_Day"></a> Informe Coste de energía por día  
 El informe **Coste de energía por día** muestra la siguiente información:  

- Un gráfico que muestra el coste de energía diario total de los equipos de la recopilación especificada durante los últimos 31 días.  

- Un gráfico que muestra el coste de energía diario promedio de cada equipo de la recopilación especificada durante los últimos 31 días.  

- Una tabla que muestra el coste de energía diario total y el coste de energía diario promedio de los equipos de la colección especificada durante los últimos 31 días.  

  Esta información puede usarse como ayuda para entender las tendencias de coste de energía en el entorno. Después de aplicar un plan de energía en los equipos de la recopilación seleccionada, el coste de energía de los equipos debe disminuir.  

  Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre de recopilación**|En la lista desplegable, seleccione la recopilación que quiere usar para este informe.|  
|**Tipo de dispositivo**|En la lista desplegable, seleccione el tipo de equipo sobre el que quiere informar. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles). Estos valores se devuelven solo para el período de informe seleccionado.|  
|**Coste de kWh**|Especifique el coste por kWh de electricidad. El valor predeterminado es **0,09**.<br /><br /> Puede modificar la unidad de moneda que se usa en este informe en la sección de parámetros ocultos.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Pueden especificarse de manera opcional los siguientes parámetros ocultos para cambiar el comportamiento de este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Equipo de escritorio encendido**|Especifique el consumo de energía de un equipo de escritorio cuando está encendido. El valor predeterminado es **0,07** kW por hora.|  
|**Equipo portátil encendido**|Especifique el consumo de energía de un equipo portátil cuando está encendido. El valor predeterminado es **0,02** kW por hora.|  
|**Equipo de escritorio suspendido**|Especifique el consumo de energía de un equipo de escritorio cuando ha entrado en suspensión. El valor predeterminado es **0,003** kW por hora.|  
|**Equipo portátil suspendido**|Especifique el consumo de energía de un equipo portátil cuando ha entrado en suspensión. El valor predeterminado es **0,001** kW por hora.|  
|**Equipo de escritorio apagado**|Especifique el consumo de energía de un equipo de escritorio cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Equipo portátil apagado**|Especifique el consumo de energía de un equipo portátil cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Monitor de escritorio encendido**|Especifique el consumo de energía de un monitor de equipo de escritorio cuando está encendido. El valor predeterminado es **0,028** kW por hora.|  
|**Monitor de portátil encendido**|Especifique el consumo de energía de un monitor de equipo portátil cuando está encendido. El valor predeterminado es **0** kW por hora.|  
|**Moneda**|Especifique la etiqueta de moneda que se debe usar para este informe. El valor predeterminado es **USD ($)** .|  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe no se vincula a otros informes de administración de energía.  

###  <a name="environmental-impact-report"></a><a name="BKMK_Environmental_Impact"></a> Informe Impacto medioambiental  
 El informe **Impacto medioambiental** muestra la siguiente información:  

- Un gráfico que muestra el CO2 mensual total generado (en toneladas) por los equipos de la recopilación especificada durante el período de tiempo especificado.  

- Un gráfico que muestra el CO2 mensual promedio generado (en toneladas) por los equipos de la recopilación especificada durante el período de tiempo especificado.  

- Una tabla que muestra el CO2 mensual total generado (en toneladas) y el CO2 mensual promedio generado por los equipos de la recopilación especificada durante el período de tiempo especificado.  

  El informe **Impacto medioambiental** calcula la cantidad de CO2 generado (en toneladas) usando el tiempo que un equipo o monitor ha estado encendido durante un período de 24 horas.  

  Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Fecha de inicio de informe**|En la lista desplegable, seleccione una fecha de inicio para este informe.|  
|**Fecha de finalización de informe**|En la lista desplegable, seleccione una fecha de finalización para este informe.|  
|**Nombre de recopilación**|En la lista desplegable, seleccione una colección para este informe.|  
|**Tipo de dispositivo**|En la lista desplegable, seleccione el tipo de equipo que se desea un informe. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles). Estos valores se devuelven solo para el período de informe seleccionado.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Pueden especificarse de manera opcional los siguientes parámetros ocultos para cambiar el comportamiento de este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Equipo de escritorio encendido**|Especifique el consumo de energía de un equipo de escritorio cuando está encendido. El valor predeterminado es **0,07** kW por hora.|  
|**Equipo portátil encendido**|Especifique el consumo de energía de un equipo portátil cuando está encendido. El valor predeterminado es **0,02** kW por hora.|  
|**Equipo de escritorio suspendido**|Especifique el consumo de energía de un equipo de escritorio cuando ha entrado en suspensión. El valor predeterminado es **0,003** kW por hora.|  
|**Equipo portátil suspendido**|Especifique el consumo de energía de un equipo portátil cuando ha entrado en suspensión. El valor predeterminado es **0,001** kW por hora.|  
|**Equipo de escritorio apagado**|Especifique el consumo de energía de un equipo de escritorio cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Equipo portátil apagado**|Especifique el consumo de energía de un equipo portátil cuando está apagado. El valor predeterminado es **0** kW por hora.|  
|**Monitor de escritorio encendido**|Especifique el consumo de energía de un monitor de equipo de escritorio cuando está encendido. El valor predeterminado es **0,028** kW por hora.|  
|**Monitor de portátil encendido**|Especifique el consumo de energía de un monitor de equipo portátil cuando está encendido. El valor predeterminado es **0** kW por hora.|  
|**Factor de carbono (toneladas/kWh)** (combinación de CO2)|Especifique el valor del factor de carbono (en toneladas/kWh) que normalmente puede obtener de su compañía eléctrica. El valor predeterminado es **0,0015** toneladas por kWh.|  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe no se vincula a otros informes de administración de energía.  

###  <a name="environmental-impact-by-day-report"></a><a name="BKMK_Environmental_Impact_by_Day"></a> Informe Impacto medioambiental por día  
 El informe **Impacto medioambiental por día** muestra la siguiente información:  

- Un gráfico que muestra el CO2 diario total generado (en toneladas) por los equipos de la recopilación especificada durante los últimos 31 días.  

- Un gráfico que muestra el CO2 diario promedio generado (en toneladas) por cada equipo de la recopilación especificada durante los últimos 31 días.  

- Una tabla que muestra el CO2 diario total generado y el CO2 diario promedio generado por los equipos de la recopilación especificada durante los últimos 31 días.  

  El informe **Impacto medioambiental por día** calcula la cantidad de CO2 generado (en toneladas) usando el tiempo que un equipo o monitor ha estado encendido durante un período de 24 horas.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre de recopilación**|En la lista desplegable, seleccione una colección para este informe.|  
|**Tipo de dispositivo**|En la lista desplegable, seleccione el tipo de equipo sobre el que quiere informar. Los valores válidos son **Todos** (equipos de escritorio y portátiles), **Escritorio** (solo equipos de escritorio) y **Portátil** (solo equipos portátiles). Estos valores se devuelven solo para el período de informe seleccionado.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Pueden especificarse de manera opcional los siguientes parámetros ocultos para cambiar el comportamiento de este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Equipo de escritorio encendido**|Especifique el consumo de energía de un equipo de escritorio cuando está encendido. El valor predeterminado es **0,07** kWh.|  
|**Equipo portátil encendido**|Especifique el consumo de energía de un equipo portátil cuando está encendido. El valor predeterminado es **0,02** kWh.|  
|**Equipo de escritorio apagado**|Especifique el consumo de energía de un equipo de escritorio cuando está apagado. El valor predeterminado es **0** kWh.|  
|**Equipo portátil apagado**|Especifique el consumo de energía de un equipo portátil cuando está apagado. El valor predeterminado es **0** kWh.|  
|**Equipo de escritorio suspendido**|Especifique el consumo de energía de un equipo de escritorio cuando ha entrado en suspensión. El valor predeterminado es **0,003** kWh.|  
|**Equipo portátil suspendido**|Especifique el consumo de energía de un equipo portátil que ha entrado en suspensión. El valor predeterminado es **0,001** kWh.|  
|**Monitor de escritorio encendido**|Especifique el consumo de energía de un monitor de equipo de escritorio cuando está encendido. El valor predeterminado es **0,028** kWh.|  
|**Monitor de portátil encendido**|Especifique el consumo de energía de un monitor de equipo portátil cuando está encendido. El valor predeterminado es **0** kWh.|  
|**Factor de carbono (toneladas/kWh)** (combinación de CO2)|Especifique un valor para el factor de carbono (en toneladas/kWh) que normalmente puede obtener de su compañía eléctrica. El valor predeterminado es **0,0015** toneladas por kWh.|  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe no se vincula a otros informes de administración de energía.  

###  <a name="insomnia-computer-details-report"></a><a name="BKMK_Insomnia_Computer_Details"></a> Informe Detalles de insomnio de equipo  
 El informe **Detalles de insomnio de equipo** muestra una lista de equipos que no entraron suspensión o hibernación por un motivo concreto dentro de un período de tiempo especificado. El **Informe de insomnio** llama a este informe y no está diseñado para que el administrador del sitio lo ejecute directamente.  

 El **Informe de insomnio** muestra los equipos como **Sin capacidad de suspensión** cuando no tienen la capacidad de suspensión y han estado encendidos durante todo el intervalo de informe especificado. El informe muestra los equipos como **Sin capacidad de hibernación** cuando no tienen la capacidad de hibernación y han estado encendidos durante todo el intervalo de informe especificado.  

> [!NOTE]  
>  La administración de energía solo puede recopilar las causas que impidieron que los equipos entraran en suspensión o hibernación de equipos que ejecutan Windows 7 o Windows Server 2008 R2.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre de recopilación**|En la lista desplegable, seleccione la recopilación que quiere usar para este informe.|  
|**Intervalo de informe (días)**|Especifique el número de días de los que quiere el informe. El valor predeterminado es **7** días.|  
|**Causa del insomnio**|En la lista desplegable, seleccione una de las causas que pueden impedir que los equipos entren en suspensión o hibernación.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles del equipo**|Haga clic en el vínculo **Haga clic para obtener información detallada** para ver las capacidades de energía, la configuración de energía y los planes de energía aplicados para el equipo seleccionado.<br /><br /> Para obtener más información, consulte [Computer Details Report](#BKMK_Computer_Details) en este tema.|  

###  <a name="insomnia-report"></a><a name="BKMK_Insomnia"></a> Insomnia report  
 El **Informe de insomnio** muestra una lista de las causas comunes que impidieron que los equipos entraran en modo de suspensión o hibernación y el número de equipos afectados por cada causa durante un período de tiempo especificado. Hay varias causas que pueden impedir que un equipo entre en suspensión o hibernación, como un proceso que se ejecuta en el equipo, una sesión abierta de Escritorio remoto o que el equipo no tenga la capacidad de suspensión o hibernación. En este informe, puede abrir el informe **Detalles de insomnio de equipo** que muestra una lista de los equipos que no están en modo de suspensión o hibernación afectados por cada causa.  

 El informe de insomnio de energía muestra los equipos como **Sin capacidad de suspensión** cuando no tienen la capacidad de suspensión y han estado encendidos durante todo el intervalo de informe especificado. El informe muestra los equipos como **Sin capacidad de hibernación** cuando no tienen la capacidad de hibernación y han estado encendidos durante todo el intervalo de informe especificado.  

> [!NOTE]  
>  La administración de energía solo puede recopilar las causas que impidieron que los equipos entraran en suspensión o hibernación de equipos que ejecutan Windows 7 o Windows Server 2008 R2.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre de recopilación**|En la lista desplegable, seleccione la recopilación que quiere usar para este informe.|  
|**Intervalo de informe (días)**|Especifique el número de días de los que quiere el informe. El valor predeterminado es **7** días. El valor máximo es de **365** días. Especifique **0** para ejecutar el informe de hoy.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles de insomnio de equipo**|Haga clic en un número en la columna **Equipos afectados** para ver una lista de equipos que no pudieron entran en suspensión o hibernación debido a la causa seleccionada.<br /><br /> Para obtener más información, consulte [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) en este tema.|  

###  <a name="power-capabilities-report"></a><a name="BKMK_Capabilites"></a> Informe Capacidades de energía  
 El informe **Capacidades de energía** muestra las capacidades de hardware para la administración de energía de los equipos de la recopilación especificada. Este informe se usa normalmente en la fase de supervisión de la administración de energía para determinar las capacidades de administración de energía de los equipos de su organización. La información mostrada en el informe puede usarse para crear recopilaciones de equipos a las que se vayan a aplicar los planes de energía o que se vayan a excluir de la administración de energía. Las capacidades de administración de energía que muestra este informe son:  

- **Con capacidad de suspensión** : indica si el equipo tiene la capacidad de entrar en suspensión si se configura para ello.  

- **Con capacidad de hibernación** : indica si el equipo puede entrar en hibernación si se configura para ello.  

- **Activación desde suspensión** : indica si el equipo puede activarse desde la suspensión si se configura para ello.  

- **Activación desde hibernación** : indica si el equipo puede activarse desde la hibernación si se configura para ello.  

  Los valores notificados por el informe **Capacidades de energía** indican las capacidades de suspensión e hibernación de los equipos tal como las notifica Windows. Sin embargo, los valores notificados no reflejan los casos en que la configuración de Windows o del BIOS impide el funcionamiento de estas funciones.  

  Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Colección**|En la lista desplegable, seleccione una colección para este informe.|  
|**Mostrar filtro**|En la lista desplegable, seleccione **No se admite** para mostrar solo los equipos de la recopilación especificada que no tienen la capacidad de suspensión, hibernación, reactivación de una suspensión o reactivación de hibernación. Seleccione **Mostrar todo** para mostrar todos los equipos de la recopilación especificada.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Este informe no tiene parámetros ocultos que se puedan establecer.  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles del equipo**|Haga clic en el nombre de un equipo para ver las capacidades de energía, la configuración de energía y los planes de energía aplicados para el equipo seleccionado.<br /><br /> Para obtener más información, consulte [Computer Details Report](#BKMK_Computer_Details) en este tema.|  

###  <a name="power-settings-report"></a><a name="BKMK_Settings"></a> Informe Configuración de energía  
 El informe **Configuración de energía** muestra una lista agregada de configuraciones de energía usadas por los equipos de la recopilación especificada. Para cada configuración de energía, se muestran los modos, los valores y las unidades de energía posibles, junto con un recuento del número de equipos que usan esos valores. Este informe puede usarse durante la fase de supervisión de la administración de energía para ayudar al administrador a comprender la configuración de energía existente que los equipos usan en el sitio y para ayudar a planificar la configuración de energía óptima que se debe aplicar mediante un plan de administración de energía. El informe también es útil al solucionar problemas para validar que la configuración de energía se aplicó correctamente.  

> [!NOTE]  
>  La configuración mostrada se recopila de los equipos cliente durante el inventario de hardware. Según la hora en que se ejecuta el inventario de hardware, se puede recopilar la configuración de planes de energía aplicados para horas punta o para horas no punta.  

 Use los parámetros siguientes para configurar este informe.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Nombre de recopilación**|En la lista desplegable, seleccione una colección para este informe.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Pueden especificarse de manera opcional los siguientes parámetros ocultos para cambiar el comportamiento de este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Especifique el número de idiomas en el que quiere ver los nombres de configuración de energía notificados por los equipos cliente. Si solo quiere verlos en el lenguaje más popular, deje esta configuración en el valor predeterminado de **1**. Para ver todos los idiomas, establezca este valor en **0**.|  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles de configuración de energía**|Haga clic en el número de equipos en la columna **Equipos** para ver una lista de todos los equipos que usan la configuración de energía de esa fila.<br /><br /> Para obtener más información, consulte [Power Settings Details Report](#BKMK_Settings_Details) en este tema.|  

###  <a name="power-settings-details-report"></a><a name="BKMK_Settings_Details"></a> Power Settings Details report  
 El informe **Detalles de configuración de energía** muestra información adicional sobre los equipos seleccionados en el informe **Configuración de energía** . El informe **Configuración de energía** llama a este informe y no está diseñado para que el administrador del sitio lo ejecute directamente.  

#### <a name="required-report-parameters"></a>Parámetros de informe necesarios  
 Deben especificarse los siguientes parámetros para ejecutar este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**Colección**|En la lista desplegable, seleccione la recopilación que quiere usar para este informe.|  
|**GUID de configuración de energía**|En la lista desplegable, seleccione el GUID de configuración de energía en el que desee notificar. Para obtener una lista de todas las configuraciones de energía y sus usos, vea [Configuración de los planes de administración de energía disponibles](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) en el tema [Creación y aplicación de planes de energía](../../../../core/clients/manage/power/create-and-apply-power-plans.md).|  
|**Power Mode**|En la lista desplegable, seleccione el tipo de configuración de energía que quiere mostrar en los resultados del informe. Seleccione **Con corriente alterna** para ver la configuración de energía para cuando el equipo está conectado y **Con batería** para ver la configuración de energía para cuando el equipo funciona con batería.|  
|**Índice de configuración**|En la lista desplegable, seleccione el valor para el nombre de la configuración de energía seleccionada sobre el que quiere informar. Por ejemplo, si quiere mostrar todos los equipos con la opción **Apagar disco duro tras** definida en **10** minutos, seleccione **Apagar disco duro tras** para **Nombre de configuración de energía** y **10** para **Índice de configuración**.|  

#### <a name="hidden-report-parameters"></a>Parámetros de informe ocultos  
 Pueden especificarse de manera opcional los siguientes parámetros ocultos para cambiar el comportamiento de este informe.  

|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Especifique el número de idiomas en el que quiere ver los nombres de configuración de energía notificados por los equipos cliente. Si solo quiere verlos en el lenguaje más popular, deje esta configuración en el valor predeterminado de **1**. Para ver todos los idiomas, establezca este valor en **0**.|  

#### <a name="report-links"></a>Vínculos de informes  
 Este informe contiene vínculos al siguiente informe que proporciona más información sobre el elemento seleccionado.  

|Nombre del informe|Detalles|  
|-----------------|-------------|  
|**Detalles del equipo**|Haga clic en el nombre de un equipo para ver las capacidades de energía, la configuración de energía y los planes de energía aplicados para el equipo seleccionado.<br /><br /> Para obtener más información, consulte [Computer Details Report](#BKMK_Computer_Details) en este tema.|  
