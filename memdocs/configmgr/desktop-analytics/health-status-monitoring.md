---
title: Supervisión del estado de mantenimiento
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo funciona la supervisión del estado de mantenimiento en Análisis de escritorio.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 359fdec13ee6bfd43e66d4bf9cec70c5a3188a32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693053"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Supervisión del estado de mantenimiento en Análisis de escritorio

A medida que [implementa una actualización en producción](deploy-prod.md), use Análisis de escritorio para supervisar el estado de mantenimiento de los dispositivos. En este artículo se explica con detalle cómo funciona la supervisión de estado.

Para obtener más información sobre el empleo de esta característica, consulte [Supervisión de estado de mantenimiento](deploy-prod.md#bkmk_monitor).

![Captura de pantalla de la página Supervisar el estado de Análisis de escritorio](media/monitor-health.png)

> [!NOTE]  
> Análisis de escritorio solo recopila datos de estado de los dispositivos que proporcionan datos de uso que puede usar como denominador. Esto significa que no se incluyen los dispositivos que ejecutan Windows 7 y Windows 10 que no están establecidos para compartir datos de diagnóstico en el nivel mejorado (limitado). Si más del 10 % de los dispositivos que ejecutan Windows 10 están configurados para compartir datos de diagnóstico en niveles distintos de mejorado (limitado), la página **Supervisión de estado** muestra una advertencia en el área del banner.  

Para ver más información sobre una aplicación específica, selecciónela en la lista.

## <a name="apps"></a>Aplicaciones

### <a name="health-status-factors"></a>Factores del estado de mantenimiento

![Factores de estado de mantenimiento de una aplicación en Análisis de escritorio](media/monitor-health-status-factors.png)

Análisis de escritorio supervisa los siguientes factores de estado de mantenimiento de las aplicaciones:

- **% de dispositivos con bloqueos**: en las últimas dos semanas, el número de dispositivos en los que se ha bloqueado esta aplicación en particular dividido por el número de dispositivos en los que se ha usado la aplicación. Esta vista le permite ver si la estabilidad de la aplicación ha aumentado o ha disminuido en la nueva versión del sistema operativo. Análisis de escritorio calcula este porcentaje para los siguientes conjuntos:  

  - **Después de actualizar**: dispositivos que se han actualizado a la versión de sistema operativo de destino especificada en el plan de implementación. Para reducir el número de recursos con datos insuficientes, Análisis de escritorio recopila estos datos para todos los dispositivos actualizados. Este conjunto incluye los dispositivos que no están en el plan de implementación.  

  - **Antes de actualizar**: dispositivos que se encuentran en una versión de SO anterior a lo que se especifica en el plan de implementación. Esta lista no incluye los dispositivos que ejecutan Windows 7.  

  - **Promedio comercial**: la tasa media (promedio) de bloqueos en todos los dispositivos comerciales. Este promedio se calcula en *todas* las versiones de la aplicación. Si la versión muestra una tasa de bloqueo por encima del promedio comercial, puede haber disponible una versión más estable.  

- **% de sesiones con bloqueos**: similar al anterior, pero cuenta el porcentaje de sesiones con bloqueos en las últimas dos semanas.  

Para determinar el estado de mantenimiento de una aplicación, Análisis de escritorio requiere datos de al menos 20 dispositivos. En caso contrario, notifica **datos insuficientes** para la aplicación. El servicio calcula el estado de mantenimiento en función de la *tasa de bloqueo de sesiones* desde estos dispositivos. La tasa de bloqueo de dispositivos solo se proporciona para fines informativos. No se usa en el cálculo del estado de mantenimiento.

### <a name="usage"></a>Uso

<!-- 5533890 -->

- **Dispositivos activos**: este valor indica el número de dispositivos en los que un usuario ha iniciado la aplicación seleccionada en las últimas dos semanas. Se basa en los dispositivos del plan de implementación seleccionado que ejecutan la versión de destino de Windows 10.

- **Sesiones**: este valor indica el número total de veces que un usuario ha iniciado la aplicación seleccionada en la versión de destino de Windows.

### <a name="additional-tabs"></a>Otras pestañas

En la parte inferior de la página de detalles de la aplicación, las tres pestañas siguientes pueden ayudarle a solucionar problemas:

- **Otras versiones**: una lista de versiones alternativas de esta aplicación. En cada versión, se muestran los cambios relativos en las tasas de bloqueo dentro de la organización y el promedio comercial. Si encuentra una versión posterior de la aplicación con una tasa de bloqueo inferior, puede que la actualización de la aplicación le ayude.  

    También muestra si la versión tiene información avanzada. Para más información, consulte [Evaluación de compatibilidad](compat-assessment.md).  

- **Problemas principales**: una lista de los identificadores de error más frecuentes por recuento de instancias. Un identificador de error identifica el seguimiento de la pila asociado al bloqueo. Puede usar este identificador al llamar al proveedor de la aplicación para obtener soporte técnico.  

- **Bloqueos recientes**:  una lista de dispositivos en los que la aplicación se ha bloqueado recientemente. Puede filtrar por identificador de error y otros criterios. Use esta información para solucionar el problema mediante la recopilación de registros o la prueba de correcciones en dispositivos específicos antes de intentar una implementación más amplia.  

Si encuentra una regresión de estado grave que no puede corregir, cambie la **Decisión sobre la actualización** a **Unable** (No se puede). Esta acción evita la futura implementación de la actualización en los dispositivos con este recurso.

## <a name="see-also"></a>Vea también

- [Evaluación de compatibilidad en Análisis de escritorio](compat-assessment.md)  

- [Implementación en producción con Análisis de escritorio](deploy-prod.md)  
