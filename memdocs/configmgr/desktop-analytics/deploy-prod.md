---
title: Implementación en producción
titleSuffix: Configuration Manager
description: Guía de procedimientos para la implementación en un grupo de producción de Análisis de escritorio.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0a7ffe8eea1048e696ce7dd254d58364226efc58
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268798"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Implementación en producción con Análisis de escritorio

Una vez que haya [implementado en el piloto](deploy-pilot.md) y haya revisado el estado de los recursos, está listo para actualizar el resto del entorno de producción.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

La implementación de actualizaciones en dispositivos de producción consta principalmente de tres partes:

1. [Revisar los recursos que necesitan una decisión de actualización](#bkmk_review): para que los dispositivos estén listos para la implementación de producción, sus recursos deben tener su decisión de actualización establecida en **Listo** o **Ready, remediations required** (Listo, correcciones necesarias).  

2. [Implementar en dispositivos que están listos](#bkmk_deploy): use Configuration Manager para actualizar los dispositivos que están listos. Análisis de escritorio proporciona la lista de dispositivos listos para la implementación de producción e informes para supervisar que la implementación se produce correctamente.  

3. [Supervisar el estado de los dispositivos actualizados](#bkmk_monitor): a medida que progresa la implementación de actualizaciones, supervise el estado de los recursos importantes. Si necesita atención, solucione los problemas y corríjalos. Si decide que los problemas no se pueden corregir, detenga la implementación en los dispositivos afectados estableciendo su decisión de actualización en **Unable** (No se puede).  

> [!NOTE]  
> Cuando esté seguro de que la implementación piloto se ha realizado correctamente, inicie la implementación de producción en cualquier momento. No es necesario que todos los dispositivos piloto alcancen primero el estado de completado.  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a> Revisar los recursos que necesitan una decisión de actualización

Análisis de escritorio le guía por el proceso de revisión de los recursos para la implementación de producción. En Azure Portal, vaya a **Planes de implementación**, seleccione un plan de implementación y, a continuación, seleccione **Preparar producción** en el menú de la izquierda.

![Captura de pantalla de la vista Preparar producción en Análisis de escritorio](media/prepare-production.png)

Revise el estado de las aplicaciones. Utilice esa información para establecer la decisión de actualización de cada uno de esos recursos.

Use cada una de las pestañas para revisar el estado de las aplicaciones. En cada vista con pestañas, puede filtrar los resultados para mostrar los dispositivos que están en seguimiento para la actualización, dispositivos que requieren su atención, dispositivos con resultados mixtos y dispositivos en un estado indeterminado.

Seleccione **Cumpliendo con los objetivos** para filtrar la vista a los recursos que probablemente estén listos para la implementación de producción en función de los criterios siguientes:

- Riesgo: evaluación previa a la actualización de los riesgos conocidos para actualizar los dispositivos que tienen este recurso instalado  

- Estado de mantenimiento: evaluación posterior a la actualización de dispositivos en otras implementaciones y posibles problemas experimentados después de instalar la actualización. Para obtener más información sobre el estado, consulte [Supervisar el estado de los dispositivos actualizados](#bkmk_monitor).  

Para aprobar un recurso para su actualización, seleccione el nombre en la lista y, a continuación, seleccione una de las siguientes opciones en la lista **Decisión sobre la actualización**:

- Revisión en curso
- Listo
- Listo (con corrección)
- No se puede
- Sin revisar

Para establecer este valor para varias aplicaciones a la vez, use la primera columna para **seleccionar este elemento** y, a continuación, elija **Establecer la decisión sobre la actualización**.

![Opción de establecer la decisión sobre la actualización en varias aplicaciones](media/prep-prod-set-upgrade-decision.png)

Seleccione **No hay datos** para ver los recursos que no se pudieron clasificar. Normalmente, estos recursos son recursos que no tienen suficiente cobertura para que Análisis de escritorio realice un análisis del riesgo o el estado de mantenimiento. Para mejorar la cobertura, agregue dispositivos adicionales con estos recursos al piloto o pida a los usuarios piloto que prueben estos recursos.

También podría haber activos en el estado **Se requiere atención** o **Mixed results** (Resultados mixtos). Estos recursos pueden requerir una revisión adicional antes de tomar una decisión de actualización para ellos.

Revise todas las aplicaciones. Una vez que un dispositivo determinado tenga una decisión de actualización positiva para todos los recursos, su estado cambia para indicar que está listo para producción. Para ver el recuento actual en la página principal del plan de implementación, seleccione el tercer paso de implementación, **Implementar**.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a> Implementar en dispositivos que están listos

Configuration Manager usa los datos de Análisis de escritorio para crear una recopilación para la implementación de producción. No implemente la secuencia de tareas mediante una implementación tradicional. Use el procedimiento siguiente para crear una implementación integrada de Análisis de escritorio:

Si siguió el proceso recomendado para [implementar en los dispositivos piloto](deploy-pilot.md#deploy-to-pilot-devices), la implementación por fases de Configuration Manager está lista. A medida que se marcan los recursos como *listos*, Análisis de escritorio sincroniza automáticamente esos dispositivos con Configuration Manager. Después, estos dispositivos se agregan a la recopilación de producción. Cuando la implementación por fases avanza a la segunda fase, estos dispositivos de producción reciben la implementación de la actualización.

Si ha configurado la implementación por fases para **iniciar manualmente la segunda fase de implementación**, deberá pasarla manualmente a la siguiente fase. Para obtener más información, vea [Administración y supervisión de implementaciones por fases](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move).

Si ha creado una implementación única integrada en Análisis de escritorio en la recopilación piloto, deberá repetir ese proceso para implementar en la recopilación de producción.


### <a name="address-deployment-alerts"></a>Solución de alertas de implementación

Al igual que con la implementación piloto, Análisis de escritorio le informa de los problemas que requieren su atención durante la implementación de producción. En Análisis de escritorio, vaya al plan de implementación y seleccione **Estado de implementación** en el menú de la izquierda. La vista de estado de implementación muestra los dispositivos de las siguientes categorías:  

- No iniciado
- En curso
- Completed
- Necesita atención: dispositivos (ordenados por nombre de dispositivo)
- Necesita atención: problemas (ordenados por tipo de problema)

![Captura de pantalla del estado de implementación de producción de Análisis de escritorio](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a> Supervisar el estado de los dispositivos actualizados

La página **Preparar producción** se centra en ayudarle a tomar decisiones de actualización para sus recursos. De forma predeterminada, la página muestra solo los recursos que aún no están en el estado **Listo**. La página **Monitorear el estado** muestra los problemas de estado en cualquier recurso destacado, incluso en los activos marcados como **Listo**. Si detecta problemas, puede solucionarlo o bien cambiar la decisión de actualización a **Unable** (No se puede). Al cambiar la decisión de actualización, esta acción evita actualizaciones futuras en los dispositivos con ese recurso.

Filtre esta página por recursos con los siguientes estados de mantenimiento:

| Filtro del estado de mantenimiento | Descripción |
|----------------------|-------------|
| **Se requiere atención** | (Filtro predeterminado) Análisis de escritorio detecta una regresión estadísticamente significativa en alguna métrica de estado de ese recurso.
| **Cumpliendo objetivos** | Análisis de escritorio no detecta ninguna regresión en el comportamiento. |
| **Datos insuficientes** | Análisis del escritorio no tiene suficientes datos sobre este recurso para hacer recomendaciones. |
| **No hay datos** | No hay datos de uso disponibles aún para este recurso. |

Para mostrar una vista sin filtrar de todos los recursos, seleccione el filtro actual. Esta acción quita ese filtro.

> [!NOTE]  
> Para reducir el número de recursos con datos insuficientes, Análisis de escritorio supervisa los recursos de todos los dispositivos que se han actualizado a la versión de Windows de destino especificada en el plan de implementación. Entre estos dispositivos están los que no están incluidos en el plan de implementación específico.  

El criterio de ordenación predeterminado es el número de dispositivos que han tenido un incidente con ese recurso en particular, por lo que puede ver rápidamente cuáles están causando la mayoría de los problemas. Por ejemplo, al ver **Aplicaciones**, se ordena por **Devices with app crashes last two weeks** (Dispositivos con bloqueos de la aplicación en las dos últimas semanas).

Si desea ver el estado de todos los recursos, incluso los recursos con datos insuficientes para que Análisis de escritorio realice inferencias estadísticas, use el proceso siguiente:

1. Seleccione la lista desplegable de la columna **Devices with incidents in last two weeks** (Dispositivos con incidentes en las últimas dos semanas). Agregue un filtro solo a los recursos que han tenido incidentes en algún número mínimo de dispositivos para que resulte interesante. Por ejemplo, mostrar elementos con un valor **mayor que** 100.  

2. Seleccione la lista desplegable de la columna **% Devices with incidents in the last two weeks** (% de dispositivos con incidentes en las dos últimas semanas) y seleccione un orden **descendente**.  

    La vista resultante muestra los recursos con la mayor tasa de incidentes con un número mínimo de incidentes.  

3. Seleccione un recurso para obtener más detalles o cambiar su decisión de actualización.  

Para obtener más información, consulte [Supervisión del estado de mantenimiento](health-status-monitoring.md).
