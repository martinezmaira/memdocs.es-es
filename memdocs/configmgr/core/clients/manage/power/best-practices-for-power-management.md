---
title: Recomendaciones para la administración de energía
titleSuffix: Configuration Manager
description: Obtenga información sobre las recomendaciones de Microsoft para la administración de energía en Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696633"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Recomendaciones para la administración de energía en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use las recomendaciones siguientes para la administración de energía en Configuration Manager.  

## <a name="monitor-at-a-representative-time"></a>Supervisión en una hora representativa

La fase de supervisión de la administración de energía proporciona la información siguiente de los equipos de la organización:

- Consumo de energía
- Actividad
- Funciones de administración de energía
- Impacto medioambiental

Elija una hora representativa para supervisar los dispositivos. Por ejemplo, la supervisión en un día festivo no proporciona un informe realista sobre el uso de energía del equipo.

## <a name="create-a-control-collection"></a>Creación de una recopilación de control

Cree dos recopilaciones de equipos para ayudarle a supervisar los efectos de la aplicación de los planes de energía en equipos. La primera recopilación debe contener la mayoría de los equipos a los que quiera aplicar la configuración de energía. La *recopilación de control* debe contener los equipos restantes. Aplique el plan de administración de energía necesario a la primera recopilación. Después, ejecute informes para comparar el impacto entre las dos recopilaciones.  

## <a name="run-reports-before-you-apply-a-plan"></a>Ejecución de informes antes de aplicar un plan

Antes de aplicar un plan de administración de energía a una recopilación de equipos, ejecute el informe de **configuración de energía**. Use este informe para ayudarle a comprender la configuración de administración de energía que ya está configurada en los equipos de la recopilación. Si aplica una configuración de administración de energía nueva a los equipos sin examinar primero la configuración existente, es posible que aumente su consumo de energía.  

## <a name="exclude-servers"></a>Exclusión de servidores

No se admite la administración de energía para los equipos que ejecutan Windows Server. Agregue los servidores a una recopilación y exclúyala de la administración de energía.  

> [!NOTE]
> Aunque Configuration Manager no admite la administración de energía de Windows Server, sí que recopila datos de uso de energía para el análisis y los informes.

## <a name="exclude-other-computers"></a>Exclusión de otros equipos

Si tiene equipos que no quiere administrar con la administración de energía, agréguelos a una colección de exclusión.  

Es posible que quiera excluir de la administración de energía los tipos de equipo siguientes:

- Los equipos que deban permanecer encendidos.  

- Los equipos a los que los usuarios necesitan conectarse de forma remota.  

- Los equipos que no puedan usar la administración de energía.  

- Los equipos que tengan el rol de sistema de sitio de punto de distribución.  

- Los equipos públicos como los quioscos multimedia, las pantallas de información o las consolas de supervisión, donde el equipo y el monitor siempre deben estar encendidos.  

Para más información, vea [Configuración de administración de energía](configuring-power-management.md).  

## <a name="apply-power-plans-to-a-test-collection"></a>Aplicación de planes de energía a una recopilación de prueba

Pruebe siempre el efecto de aplicar un plan de administración de energía en un conjunto de equipos de prueba antes de aplicar el plan de energía a un gran conjunto de equipos.  

Cuando se excluye un equipo de la administración de energía, toda la configuración de energía vuelve a sus valores originales. No puede revertir una configuración de energía individual a sus valores originales.  

## <a name="apply-power-plan-settings-individually"></a>Aplicar la configuración de plan de energía individualmente

Supervise el efecto de aplicar cada configuración de energía antes de aplicar la siguiente. Este proceso garantiza que cada valor tenga el efecto necesario. Para más información sobre las configuraciones de plan de administración, vea [Configuración de Plan de administración de energía disponibles](create-and-apply-power-plans.md#BKMK_Plans).  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>Supervisión periódica de los equipos para varios planes de energía

La administración de energía incluye un informe en el que se muestran los equipos que tengan varios planes de energía aplicados: **Equipos con varios planes de energía**.

Si un equipo es miembro de varias recopilaciones, y en cada una se aplican distintos planes de energía, se aplican los comportamientos siguientes:  

- **Plan de energía**: si se aplican varios valores para la configuración de energía a un equipo, se usa el valor menos restrictivo.  

- **Hora de reactivación**: si se aplican varias horas de activación a un equipo de escritorio, se usa la hora más cercana a la medianoche.  

Para más información, vea [Equipos con varios planes de energía](monitor-and-plan-for-power-management.md#BKMK_Multiple).  

## <a name="save-or-export-power-management-information"></a>Guardado o exportación de información de administración de energía

Cuando ejecute informes durante las fases de supervisión y cumplimiento, guarde o exporte los resultados. Conserve los datos para una comparación posterior en caso de que Configuration Manager quite los datos después.  

Configuration Manager mantiene la siguiente información de administración de energía en la base de datos del sitio:

- Información de administración de energía usada por los informes diarios: 31 días

- Información de administración de energía usada por los informes mensuales: 13 meses
