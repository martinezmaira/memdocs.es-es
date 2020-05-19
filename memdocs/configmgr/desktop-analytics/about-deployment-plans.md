---
title: Planes de implementación en Análisis de escritorio
titleSuffix: Configuration Manager
description: Aprenda sobre los planes de implementación de Análisis de escritorio.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ccc325ac4b8e02142a1442862ad661a77b0561f2
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268494"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Acerca de los planes de implementación en Análisis de escritorio

Análisis de escritorio recopila y analiza los datos de dispositivos, aplicaciones y controladores de la organización. En función de este análisis y de la información que usted especifique, puede usar el servicio para crear planes de implementación para Windows 10. Los planes de implementación tienen las siguientes características:  

- Recomendar automáticamente los dispositivos que se van a incluir en los pilotos  

- Identificar problemas de compatibilidad y sugerir mitigaciones  

- Evaluar el estado de la implementación antes, durante y después de las actualizaciones  

- Realizar el seguimiento del progreso de la implementación.  

Como parte del plan de implementación, realizará las siguientes acciones:  

- Definir qué versiones de Windows 10 quiere implementar  

- Elegir los grupos de dispositivos destino de la implementación  

- Crear reglas de preparación para la implementación  

- Definir la importancia de las aplicaciones  

- Elegir dispositivos piloto según recomendaciones automáticas  

- Decidir cómo corregir problemas con las aplicaciones según las recomendaciones de Análisis de escritorio  

De forma predeterminada, Análisis de escritorio actualiza los datos del plan de implementación diariamente. Los cambios que realice en un plan de implementación, como asignar importancia a una aplicación o elegir un dispositivo para incluirlo en un piloto, tardan hasta 24 horas en procesarse. Para acelerar este proceso, solicite una actualización de datos a petición. Para más información, consulte [Preguntas frecuentes sobre Análisis de escritorio](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Después de conectar Análisis de escritorio a Configuration Manager, seleccione sus recopilaciones en los planes de implementación. Esta integración le permite implementar Windows en una recopilación basada en los datos de Análisis de escritorio.

## <a name="readiness-rules"></a>Reglas de preparación

Las siguientes reglas de preparación están disponibles en los planes de implementación:

- Si los dispositivos reciben controladores automáticamente de Windows Update. Si los dispositivos reciben las actualizaciones del controlador de Windows Update, los problemas de controladores identificados como parte de la evaluación de la preparación se marcan automáticamente como **Listo**.  

- Umbral de recuento de instalaciones bajo para las aplicaciones de Windows. Si una aplicación se instala en un porcentaje superior de equipos que este umbral, el plan de implementación marca la aplicación como **Destacada**. Esta etiqueta significa que puede decidir lo importante que es probar la aplicación durante la fase piloto.  

## <a name="plan-assets"></a>Planeamiento de recursos

<!-- 4670224 -->

Aunque el área [Recursos](about-assets.md) también muestra dispositivos y aplicaciones, el área **Plan assets** (Planear recursos) en un plan de implementación específico incluye información adicional.

### <a name="devices"></a>Dispositivos

Consulte la **decisión de actualización de Windows** de cada dispositivo del plan de implementación.

La decisión de actualización de Windows a **Reemplazar dispositivo** puede deberse a uno de los siguientes motivos:

- No se pudo realizar una comprobación del procesador necesaria para Windows 10. Para más información, consulte [Requisitos mínimos de hardware](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Hay un bloqueo del BIOS.
- No hay suficiente memoria.
- Un componente crítico para el arranque en el sistema tiene un controlador bloqueado.
- La marca y el modelo específicos no pueden actualizarse.
- Hay un componente de clase de pantalla con un bloqueo del controlador que tiene todos los atributos siguientes:
  - No se reemplaza.
  - No hay ningún controlador en la nueva versión del sistema operativo.
  - Todavía no está en Windows Update.
- Hay otro componente plug-and-play en el sistema que bloquea la actualización.
- Hay un componente inalámbrico que usa un controlador emulado por XP.
- Un componente de red con una conexión activa perderá su controlador. En otras palabras, después de la actualización, podría perder la conectividad de red.

La decisión de actualización de Windows de **reinstalar** indica que la actualización requerirá una reinstalación en lugar de una actualización local.

Una decisión de actualización de Windows **bloqueada** puede deberse a los siguientes motivos:

- La decisión de actualización de uno o más activos está establecida en **No se puede**.

- Los datos de inventario de ese dispositivo están incompletos y Análisis de escritorio no puede realizar una evaluación de compatibilidad completa.

### <a name="apps"></a>Aplicaciones

Establezca la **decisión de actualización** y la **importancia** de esta aplicación en este plan de implementación. Para más información, consulte [Creación de planes de implementación](create-deployment-plans.md).

En los detalles de la aplicación, también puede ver la siguiente información: recomendaciones, factores de riesgo de compatibilidad y problemas conocidos de Microsoft. Úsela para establecer la **decisión de actualización**. Para más información, consulte [Evaluación de compatibilidad](compat-assessment.md).

Las aplicaciones que Análisis de escritorio que se muestran como *destacadas* se basan en el umbral de recuento de instalaciones bajo de las reglas de preparación del plan de implementación. Para más información, consulte [Reglas de preparación](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > Para más información sobre la categoría de aplicación "No importante", consulte [Decisión de actualización automática de las aplicaciones del sistema y de la tienda](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->

La opción **App Versions Details** (Detalles de versiones de la aplicación) está desactivada de forma predeterminada, por lo que en esta pestaña se combinan todas las versiones de las aplicaciones con el mismo nombre y el mismo editor.<!-- 5542186 --> El comportamiento predeterminado ayuda a reducir el número total de aplicaciones que se ven, lo que contribuye a reducir la labor de anotar las aplicaciones. El recuento de aplicaciones en el icono **Aplicaciones de interés** también refleja este valor. Por ejemplo, en lugar de mostrar cientos de instancias de Microsoft Edge, hay una sola instancia para todas las versiones. Puede tomar decisiones una vez para todas las versiones. Si tiene que tomar decisiones sobre versiones específicas de una aplicación, active esta opción. También puede configurar esta opción al trabajar en el nivel global de recursos. Para más información, vea [Acerca de los recursos: aplicaciones](about-assets.md#apps).

Cuando la opción **App Versions Details** (Detalles de versiones de la aplicación) está desactivada, el panel Detalles de la aplicación muestra el número de versiones de la aplicación y los idiomas que combina. Los cambios en los detalles de la aplicación que se guarden, se aplican a todas las versiones. Por ejemplo, establezca la **decisión de actualización** o la **importancia**. Algunos valores mostrarán "varios", lo que significa que no hay un valor coherente en todas las versiones. El servicio sigue realizando evaluaciones de riesgos de compatibilidad para cada versión. Active **App Versions Details** (Detalles de versiones de la aplicación) para ver la evaluación de riesgos de compatibilidad para una versión específica de la aplicación.

### <a name="drivers"></a>Controladores

Consulte la lista de controladores que se incluyen en este plan de implementación. Establezca la **decisión de actualización**, revise la recomendación de Microsoft y vea los factores de riesgo de compatibilidad.

## <a name="importance"></a>Importancia

Como parte del plan de implementación, establezca la *importancia* de las aplicaciones. Análisis de escritorio detecta estas aplicaciones como instaladas en los dispositivos de destino. Esta configuración ayuda a Análisis de escritorio a determinar qué dispositivos se incluyen en la fase piloto de la implementación.

Si una aplicación está instalada en menos del 2 % de los dispositivos de destino, se marcará como **Recuento de instalaciones bajo**. 2 % es el valor predeterminado. Puede ajustar el umbral en la configuración de preparación de 0 % a 10 %. Análisis de escritorio marca automáticamente estas aplicaciones como **Preparado para la actualización**.  

Para las aplicaciones, elija una importancia de **Crítica**, **Importante** o **No importante**. Si marca una como crítica o importante, Análisis de escritorio incluye en la implementación piloto algunos dispositivos con esa aplicación. El servicio incluye en el piloto más instancias de una aplicación crítica. Si marca una aplicación como no importante, Análisis de escritorio la establece automáticamente en **Preparado para actualizar**.

## <a name="pilot-devices"></a>Dispositivos piloto

Análisis de escritorio combina su información de importancia con la configuración del piloto global. Luego, crea una recomendación sobre qué dispositivos deben formar parte de la implementación piloto. La implementación piloto recomendada incluye dispositivos con diferentes configuraciones de hardware y una o más instancias de todas las aplicaciones críticas e importantes. Si una aplicación está marcada como crítica, el servicio recomienda más dispositivos con esa aplicación en el piloto.

## <a name="deployment-plans-in-configuration-manager"></a>Planes de implementación en Configuration Manager

Después de crear un plan de implementación, use Configuration Manager para implementar los productos. Una vez que se inicia la implementación, Análisis de escritorio la supervisa según los valores de configuración del plan.

## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre los recursos de Análisis de escritorio](about-assets.md): dispositivos, controladores y aplicaciones  

- [Más información sobre la actualizaciones de características y seguridad](about-updates.md)  

- [Creación de un plan de implementación](create-deployment-plans.md)  
