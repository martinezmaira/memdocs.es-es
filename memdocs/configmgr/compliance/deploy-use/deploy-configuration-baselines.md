---
title: Implementación de líneas base de configuración
titleSuffix: Configuration Manager
description: Implemente líneas base de configuración para definir implementaciones de línea base de configuración y agregar o quitar líneas base de configuración de las implementaciones.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 55b559f9b16eabfe2c2096497e6f63816b400803
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692453"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Implementación de líneas base de configuración en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las líneas base de configuración de Configuration Manager deben implementarse en una o varias recopilaciones de usuarios o dispositivos antes de que los dispositivos cliente de esas recopilaciones puedan evaluar su compatibilidad con la línea base de configuración.  

Utilice el cuadro de diálogo **Implementar líneas base de configuración** para definir implementaciones de línea de base de configuración, lo que incluye agregar o quitar líneas base de configuración de las implementaciones, además de especificar la programación de la evaluación.  

## <a name="deploy-a-configuration-baseline"></a>Implementar una línea de base de configuración  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Líneas base de configuración**.  

3.  En la lista **Líneas base de configuración** , seleccione la línea base de configuración que quiere implementar y después en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

4.  En el cuadro de diálogo **Implementar líneas de base de configuración** , seleccione las líneas base de configuración que quiera implementar en la lista **Líneas de base de configuración disponibles** . Haga clic en **Agregar** para agregarlas a la lista **Líneas de base de configuración seleccionadas** .  

    > [!IMPORTANT]  
    >  Si cambia un elemento de configuración que se haya agregado a una línea base de configuración implementada, no se evalúa la compatibilidad del elemento de configuración revisado hasta la hora de su próxima evaluación programada.  

5.  Especifique la siguiente información adicional:  

    -   **Corregir las reglas no compatibles cuando se admita**: corrige automáticamente las reglas que no sean compatibles con Instrumental de administración de Windows (WMI), el Registro, los scripts y toda la configuración de los dispositivos móviles que Configuration Manager haya inscrito.  

    -   **Permitir la corrección fuera de la ventana de mantenimiento** : si se ha configurado una ventana de mantenimiento para la recopilación en la que se va a implementar la línea base de configuración, habilite esta opción para permitir que la configuración de cumplimiento corrija el valor fuera de la ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  

6.  **Generar una alerta**: configura una alerta que se genera si la compatibilidad de la línea base de configuración es inferior a un determinado porcentaje en una hora y fecha especificadas. También puede especificar si desea que se envíe una alerta a System Center Operations Manager.  

7.  **Recopilación** : haga clic en **Examinar** para seleccionar la recopilación en la que quiere implementar la línea base de configuración.  

8.  **Especifique la programación de evaluación de compatibilidad para esta línea de base de configuración:** especifica la programación por la que se evalúa la línea base de configuración implementada en los equipos cliente. Puede ser una programación simple o personalizada.  

    > [!NOTE]  
    >  Si la línea base de configuración se implementa en un equipo, su compatibilidad se evalúa en las dos horas siguientes a la hora de inicio que programe. Si se implementa para un usuario, la compatibilidad se evalúa cuando el usuario inicia sesión.  

9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Implementar líneas de base de configuración** y crear la implementación. Para obtener más información sobre cómo supervisar la implementación, consulte [Monitor compliance settings](monitor-compliance-settings.md) (Supervisar la configuración de cumplimiento).  
