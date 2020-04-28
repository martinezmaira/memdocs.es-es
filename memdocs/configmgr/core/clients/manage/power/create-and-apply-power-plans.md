---
title: Creación y aplicación de planes de energía
titleSuffix: Configuration Manager
description: Cree y aplique planes de energía en Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ba5479a4c75d3ab8f91a8439a6799589b93972d0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076703"
---
# <a name="how-to-create-and-apply-power-plans-in-configuration-manager"></a>Cómo crear y aplicar planes de energía en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La administración de energía de Configuration Manager permite poner en marcha los planes de energía provistos por Configuration Manager en recopilaciones de equipos de la jerarquía, o bien crear sus propios planes de energía personalizados. Use el procedimiento de este tema para aplicar un plan de energía integrado o personalizado a los equipos.  

> [!IMPORTANT]  
>  Solo se pueden aplicar planes de energía de Configuration Manager a colecciones de dispositivos.  

 Si un equipo es miembro de varias recopilaciones y cada una de ellas aplica planes de energía diferentes, se realizará las siguientes acciones:  

- Plan de energía: si se aplican varios valores para la configuración de energía de un equipo, se usa el valor menos restrictivo.  

- Hora de reactivación: si se aplican varias horas de activación a un equipo de escritorio, se usa la hora más cercana a medianoche.  

  Use el informe **Equipos con varios planes de energía** para mostrar todos los equipos a los que se aplican varios planes de energía. Esto puede ayudarle a detectar los equipos que tienen conflictos de energía. Para más información sobre los informes de administración de energía, vea [Cómo supervisar y planear la administración de energía en Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Al configurar la energía con la directiva de grupo de Windows se invalidará la configuración establecida por la administración de energía de Configuration Manager.  

 Use el procedimiento siguiente para crear y aplicar un plan de energía de Configuration Manager.  

### <a name="to-create-and-apply-a-power-plan"></a>Para crear y aplicar un plan de energía  

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.  

3. En la lista **Recopilaciones de dispositivos** , haga clic en la recopilación a la que quiere aplicar la configuración de administración de energía y, a continuación, en la pestaña **Inicio** en el grupo **Propiedades** , haga clic en **Propiedades**.  

4. En la pestaña **Administración de energía** del cuadro de diálogo <em><Nombre de la colección>\></em>**Propiedades**, seleccione **Especificar la configuración de administración de energía para esta recopilación**.  

   > [!NOTE]  
   >  También puede hacer clic en **Examinar** y, a continuación, copiar la configuración de administración de energía de una recopilación seleccionada en la recopilación seleccionada.  

5. En los campos **Inicio** y **Fin** , especifique las horas de inicio y fin para las horas punta (o laborables).  

6. Habilite **Hora de activación (equipos de escritorio)** para especificar una hora en la que un equipo de escritorio se activará desde suspensión o hibernación para instalar actualizaciones o instalaciones de software programadas.  

   > [!IMPORTANT]  
   >  La administración de energía usa la característica interna de hora de activación de Windows para activar los equipos en suspensión o hibernación. La configuración de la hora de activación no se aplica a los equipos portátiles para evitar escenarios en los que se activaran cuando no estuvieran enchufados. La hora de activación es aleatoria y los equipos se activarán durante un período de una hora desde la hora de activación especificada.  

7. Si quiere configurar un plan de energía personalizado para las horas punta (o laborables), seleccione **Máximo personalizado (ConfigMgr)** en la lista desplegable **Plan para horas punta** y, a continuación, haga clic en **Editar**. Si quiere configurar un plan de energía para fuera de horas punta (o no laborables), seleccione **Fuera de horas punta personalizado (ConfigMgr)** en la lista desplegable **Plan fuera de horas punta** y, a continuación, haga clic en **Editar**.  

   > [!NOTE]  
   >  Puede usar el informe **Actividad de equipo** que le ayudará a decidir las programaciones que debe usar para las horas punta y fuera de horas punta al aplicar planes de energía a recopilaciones de equipos. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

    También puede seleccionar los planes de energía integrados, **Equilibrado (ConfigMgr)** , **Alto rendimiento (ConfigMgr)** y **Ahorro de energía (ConfigMgr)** y, a continuación, hacer clic en **Ver** para mostrar las propiedades de cada plan de energía.  

   > [!NOTE]  
   >  No se pueden modificar los planes de energía integrados.  

8. En el cuadro de diálogo <em><nombre de plan de energía\></em>**Propiedades**, configure las opciones siguientes:  

   -   **Nombre:** especifique un nombre para este plan de energía o use el nombre predeterminado proporcionado.  

   -   **Descripción:**  especifique una descripción para este plan de energía o use la descripción predeterminada proporcionada.  

   -   **Especificar las propiedades de este plan de energía:** configure las propiedades del plan de energía. Para deshabilitar una propiedad, desactive su casilla. Para obtener más información sobre las opciones disponibles, vea [Available power management plan settings](#BKMK_Plans) en este tema.  

       > [!IMPORTANT]  
       >  La configuración habilitada se aplica a los equipos cuando se aplica el plan de energía. Si desactiva una casilla de configuración de energía, no se cambia el valor en el equipo cliente cuando se aplica el plan de energía. Al desactivar una casilla no se restaura la configuración de energía a su valor anterior antes de haber aplicado un plan de energía.  

9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo <em><nombre de plan de energía\></em>**Propiedades**.  

10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo <em><Nombre de la colección>\></em>**Configuración** y aplicar el plan de energía.  

##  <a name="available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Available power management plan settings  
 En la tabla siguiente se muestran las opciones de administración de energía disponibles en Configuration Manager. Puede definir configuraciones diferentes para cuando el equipo está conectado o funciona con batería. Según la versión de Windows que use, puede que algunas opciones no sean configurables.  

> [!NOTE]  
>  Las opciones de energía que no configure conservarán su valor actual en los equipos cliente.  

|Nombre|Descripción|  
|----------|-----------------|  
|**Apagar pantalla tras (minutos)**|Especifica el período de tiempo, en minutos, que el equipo debe estar inactivo antes de que la pantalla se apague. Especifique un valor de **0** si no quiere que la administración de energía apague la pantalla.|  
|**Suspender tras (minutos)**|Especifica el período de tiempo, en minutos, que el equipo debe estar inactivo antes de que entre en suspensión. Especifique un valor de **0** si no quiere que la administración de energía coloque el equipo en suspensión.|  
|**Requerir contraseña al reactivarse**|Un valor **Sí** o **No** especifica si una contraseña es necesaria para desbloquear el equipo cuando entra en activación de la suspensión.|  
|**Acción del botón de encendido**|Especifica la acción que se realiza cuando se presiona el botón de encendido del equipo. Los valores posibles son **No hacer nada**, **Suspender**, **Hibernar** y **Apagar**.|  
|**Botón de encendido del menú Inicio**|Especifica la acción que se produce cuando se presiona el botón de encendido del menú **Inicio** del equipo. Los valores posibles son **Suspender**, **Hibernar** y **Apagar**.|  
|**Acción del botón de suspensión**|Especifica la acción que se produce cuando se presiona el botón **Suspender** del equipo. Los valores posibles son **No hacer nada**, **Suspender**, **Hibernar** y **Apagar**.|  
|**Acción al cerrar la tapa**|Especifica la acción que se produce cuando el usuario cierra la tapa de un equipo portátil. Los valores posibles son **No hacer nada**, **Suspender**, **Hibernar** y **Apagar**.|  
|**Apagar disco duro tras (minutos)**|Especifica el período de tiempo, en minutos, que el disco duro del equipo debe estar inactivo antes de que se apague. Especifique un valor de **0** si no quiere que la administración de energía apague el disco duro del equipo.|  
|**Hibernar tras (minutos)**|Especifica el período de tiempo, en minutos, que el equipo debe estar inactivo antes de que entre en hibernación. Especifique un valor de **0** si no quiere que la administración de energía coloque el equipo en hibernación.|  
|**Acción de batería baja**|Especifica la acción que se produce cuando la batería del equipo alcanza el nivel de notificación de batería baja especificado. Los valores posibles son **No hacer nada**, **Suspender**, **Hibernar** y **Apagar**.|  
|**Acción de nivel crítico de batería**|Especifica la acción que se realiza cuando la batería del equipo alcanza el nivel de notificación de batería crítica especificado. Con la opción **Con batería**, los valores posibles son **Suspender**, **Hibernar** y **Apagar**. Con la opción **Con corriente alterna**, los valores posibles son **No hacer nada**, **Suspender**, **Hibernar** y **Apagar**.|  
|**Permitir suspensión híbrida**|La selección del valor **Activado** o **Desactivado** especifica si Windows guarda un archivo de hibernación al entrar en suspensión, que puede usarse para restaurar el estado del equipo en caso de pérdida de energía mientras ha entrado en modo de suspensión.<br /><br /> La suspensión híbrida está diseñada para equipos de escritorio y, de forma predeterminada, no está habilitada en equipos portátiles. En equipos que ejecutan Windows 7, la habilitación de la suspensión híbrida deshabilita la función de hibernación.|  
|**Permitir el estado de suspensión durante la acción de reposo**|La selección del valor **Activado** o **Desactivado** permite que el equipo esté en modo de espera, que todavía consume algo de energía, pero permite que el equipo se reactive con mayor rapidez. Si esta opción se establece en **Desactivar**, el equipo solo puede hibernar o apagarse.|  
|**Inactividad requerida para entrar en suspensión (%)**|Especifica el porcentaje de tiempo de inactividad en el tiempo de procesador del equipo necesario para que el equipo entre en suspensión. En equipos que ejecutan Windows 7, este valor siempre se establece en **0**.|  
|**Habilitar temporizador de activación de Windows para equipos de escritorio**|La selección del valor **Habilitar** o **Deshabilitar** puede habilitar el temporizador de Windows integrado para que la administración de energía lo use para reactivar un equipo de escritorio. Cuando se reactiva un equipo de escritorio utilizando el temporizador de activación Windows, permanecerá activo durante 10 minutos para que tenga tiempo para el equipo para instalar las actualizaciones o para recibir la directiva de forma predeterminada.<br /><br /> Los temporizadores de activación no se admiten en equipos portátiles para evitar escenarios en los que se activen sin estar enchufados.|  
