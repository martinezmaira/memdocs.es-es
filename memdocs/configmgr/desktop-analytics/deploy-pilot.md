---
title: Implementación en un grupo piloto
titleSuffix: Configuration Manager
description: Guía de procedimientos para la implementación en un grupo piloto de Análisis de escritorio.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 3aa722415248ad9275c6ad065f0120bfe78d3ce4
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311227"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Implementación en un grupo piloto con Análisis de escritorio

Una de las ventajas de Análisis de escritorio es que ayuda a identificar el conjunto más pequeño de dispositivos que proporcionan la mayor cobertura de factores. Se centra en los factores que son más importantes para una prueba piloto de las actualizaciones de Windows. Al tener la seguridad de que el piloto es más satisfactorio, puede seguir ampliando con rapidez y confianza las implementaciones en producción.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>Identificación de dispositivos

El primer paso es identificar los dispositivos que se van a incluir en el piloto. Análisis de escritorio recomienda dispositivos basados en los datos de los informes, y se pueden incluir o reemplazar dispositivos de esta lista.

1. Vaya al [portal de Análisis de escritorio](https://aka.ms/desktopanalytics) y, en el grupo Administrar, seleccione **Planes de implementación**.

1. Seleccione un plan de implementación.

1. En el grupo Preparar del menú Plan de implementación, seleccione **Identificar piloto**.

Verá que los datos de Análisis de escritorio muestran el número de dispositivos que se recomienda incluir para una mejor cobertura. Este algoritmo se basa principalmente en el uso de aplicaciones importantes y críticas, y en el abanico de configuraciones de hardware.

Realice las siguientes acciones para ver la lista de dispositivos recomendados adicionales:

- **Agregar todo a piloto**: agrega todos los dispositivos recomendados al grupo piloto.
- **Agregar a piloto**: agrega solo dispositivos individuales.
- **Reemplazar**: para reemplaza cualquier dispositivo específico del piloto.

A medida que se agregan dispositivos de la lista piloto de **recomendados** a la de **incluidos**, la cobertura y la redundancia de los activos críticos e importantes en el piloto aumenta. Una mayor redundancia significa que los recursos cubiertos tienen un número estadísticamente significativo de dispositivos incluidos en el programa piloto.

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>Piloto global

También puede tomar decisiones a nivel global del sistema sobre qué recopilaciones de Configuration Manager incluir o excluir de los pilotos. En el menú principal de Análisis de escritorio, en el grupo Configuración global, seleccione **Piloto global**.

Si conecta varias jerarquías de Configuration Manager a la misma instancia de Análisis de escritorio, un nombre para mostrar de la jerarquía prefijará el nombre de la colección en la configuración piloto global. Este nombre es la propiedad **nombre para mostrar** de la conexión de Análisis de escritorio en la consola de Configuration Manager.<!-- 4814075 -->

> [!NOTE]
> La compatibilidad con varias jerarquías requiere la versión 1910 o posterior de Configuration Manager.

- No incluya colecciones que contengan más del 20 % del total de dispositivos inscritos a Análisis de escritorio. Si incluye una colección grande, el portal muestra una advertencia. Puede incluir varias colecciones pequeñas sin advertencia, pero tenga cuidado con el número de dispositivos de la prueba piloto. <!-- 6079184 -->

- Para obtener recomendaciones piloto precisas para los planes de implementación en una jerarquía de Configuration Manager específica, incluya solo las recopilaciones de esa jerarquía.

### <a name="example"></a>Ejemplo

- La conexión de Análisis de escritorio se configura en Configuration Manager para tener como destino la recopilación **Todos los sistemas**. Esta acción inscribe todos los clientes en el servicio.

- También se configuran colecciones adicionales para sincronizar con Análisis de escritorio:

  - Todos los clientes de Windows 10 (3000 dispositivos)

  - Todos los dispositivos de TI (200 dispositivos en total, 150 de los cuales ejecutan Windows 10)

  - Oficina del director general (20 dispositivos)

- En la configuración del **Piloto global**, incluirá las recopilaciones **Todos los clientes de Windows 10**. Excluya la colección **Oficina del director general**.

- Cree un plan de implementación y seleccione la recopilación **Todos los dispositivos de TI** como **Grupo de destino**. Este plan de implementación solo está pensado para dispositivos del departamento de TI.

- La lista **Dispositivos piloto incluidos** contiene el subconjunto de dispositivos que se encuentra en ambos **grupos de destino**: **Todos los dispositivos de TI** y la lista de *inclusión* del piloto global: **Todos los clientes de Windows 10** En la lista están 150 dispositivos, ya que solo los 150 dispositivos de la recopilación **Todos los dispositivos de IT** ejecutan Windows 10.

- La lista **Dispositivos adicionales recomendados** contiene un conjunto de dispositivos del **grupo de destino** que proporcionan cobertura y redundancia máximas de los recursos importantes. Análisis de escritorio excluye de esta lista todos los dispositivos de la lista de *exclusión* del piloto global: **Oficina del director general**

## <a name="address-issues"></a>Solución de problemas

Use el portal de Análisis de escritorio para revisar los problemas notificados con recursos que podrían bloquear la implementación. A continuación, apruebe, rechace o modifique la corrección sugerida. Todos los elementos deben estar marcados como **Listo** o **Listo con corrección** antes de que se inicie la implementación piloto.

1. Vaya al [portal de Análisis de escritorio](https://aka.ms/desktopanalytics) y, en el grupo Administrar, seleccione **Planes de implementación**.  

2. Seleccione un plan de implementación.  

3. En el grupo Preparar del menú Plan de implementación, seleccione **Preparar piloto**.  

4. En la pestaña **Aplicaciones**, revise las aplicaciones que necesitan que aporte información.  

5. Para cada aplicación, seleccione su nombre. En el panel de información, revise la recomendación y seleccione la decisión de actualización. Si elige **Sin revisar** o **No se puede**, Análisis de escritorio no incluye los dispositivos con esta aplicación en la implementación piloto. Si elige **Listo con corrección**, use las **notas de corrección** para capturar las acciones que se realizarán para resolver un problema, por ejemplo, *reinstalar* o *encontrar la versión recomendada del fabricante*.

6. Repita esta revisión con otros recursos.  

Para más información para ayudar con este proceso de revisión, consulte [Evaluación de compatibilidad en Análisis de escritorio](compat-assessment.md).

## <a name="create-software"></a>Creación de software

Antes de implementar Windows, cree primero los objetos de software en Configuration Manager. Para más información, consulte [Secuencia de tareas de actualización en contexto de Windows 10](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

## <a name="deploy-to-pilot-devices"></a>Implementación en dispositivos piloto

Configuration Manager usa los datos de Análisis de escritorio para crear recopilaciones para las implementaciones piloto y de producción. Estas recopilaciones se encuentran en área de trabajo **Activos y compatibilidad** del nodo **Recopilaciones de dispositivos** de la carpeta **Planes de implementación**.

> [!IMPORTANT]
> Configuration Manager administra estas recopilaciones para los planes de implementación de Análisis de escritorio. No se admiten cambios manuales. Si elimina una de estas colecciones, el Análisis de escritorio no funcionará y tendrá que [conectarse con Configuration Manager](connect-configmgr.md) de nuevo.<!--7208090-->

Para asegurarse de que los dispositivos están en buen estado después de cada fase de implementación, use el procedimiento siguiente para crear una implementación por fases integrada en Análisis de escritorio:

1. En la consola de Configuration Manager, vaya a **Biblioteca de software**, expanda **Servicio Análisis de escritorio** y seleccione el nodo **Planes de implementación**.  

2. Seleccione el plan de implementación y, luego, seleccione **Detalles del plan de implementación** en la cinta de opciones.  

3. Seleccione **Crear una implementación por fases** en la cinta de opciones. Esta acción inicia el Asistente para crear una implementación por fases.

    > [!Tip]  
    > Si quiere crear una implementación de secuencia de tareas clásica solo para la recopilación piloto, seleccione **Implementar** en el icono **Estado piloto**. Esta acción inicia el Asistente para implementar software. Para obtener más información, vea [Deploy a task sequence](../osd/deploy-use/deploy-a-task-sequence.md).  

4. Escriba un nombre para la implementación y seleccione la secuencia de tareas que se va a usar. Use la opción **Crear automáticamente una implementación predeterminada de dos fases** y, luego, configure las recopilaciones siguientes:  

    - **Primera recopilación**: busque y seleccione la recopilación **Piloto** de este plan de implementación. La convención de nomenclatura estándar de esta recopilación es `<deployment plan name> (Pilot)`.

    - **Segunda recopilación**: busque y seleccione la recopilación **Producción** de este plan de implementación. La convención de nomenclatura estándar de esta recopilación es `<deployment plan name> (Production)`.

    > [!Note]  
    > Con la integración de Análisis de escritorio, Configuration Manager crea automáticamente recopilaciones piloto y de producción para el plan de implementación. Antes de poder usarlas, puede que estas recopilaciones tarden en sincronizarse. Para más información, consulte [Solución de problemas: latencia de datos](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Estas recopilaciones están reservadas para los dispositivos del plan de implementación de Análisis de escritorio. No se admiten cambios manuales en estas recopilaciones.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Realice el asistente para configurar la implementación por fases. Para más información, vea [Crear implementaciones por fases](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

    > [!Note]  
    > Use la configuración predeterminada para **Iniciar automáticamente esta fase después de un período de aplazamiento (en días)** . Para que se inicie la segunda fase se deben satisfacer los siguientes criterios:
    >
    > 1. La primera fase alcanza el criterio de **porcentaje de éxito de la implementación**. Esta opción se configura en la implementación por fases.
    > 1. Debe revisar y tomar decisiones de actualización en Análisis de escritorio para marcar los recursos importantes y críticos como *listos*. Para más información, consulte [Revisar los recursos que necesitan una decisión de actualización](deploy-prod.md#bkmk_review).
    > 1. Análisis de escritorio se sincroniza con las recopilaciones de Configuration Manager de todos los dispositivos de producción que cumplen los criterios de *listo*.

> [!Important]  
> Estas recopilaciones se siguen sincronizando a medida que cambia su pertenencia. Por ejemplo, si identifica un problema con un recurso y lo marca como **No se puede**, los dispositivos con ese recurso ya no cumplen los criterios de *listo*. Estos dispositivos se quitan de la colección de implementación de producción.

## <a name="monitor"></a>Supervisión

### <a name="configuration-manager-console"></a>Consola de Configuration Manager

Abra el plan de implementación. En el icono **Preparando decisiones de actualización: estado general** se proporciona un resumen del estado del plan de implementación. Este estado es para las recopilaciones piloto y de producción. Los dispositivos pueden estar en una de las siguientes categorías:

- **Actualizado**: los dispositivos se han actualizado a la versión de Windows de destino en este plan de implementación.

- **Decisión de actualización completada**: uno de los siguientes estados:

  - Dispositivos con recursos destacados con el estado **Listo** o **Listo con corrección**.

  - El estado del dispositivo es **Bloqueado**, [**Reemplazar dispositivo**](about-deployment-plans.md#plan-assets) o **Reinstalar dispositivo**.

- **Sin revisar**: dispositivos con recursos destacados **Sin revisar** o **Revisión en curso**.

las actualizaciones de estado del dispositivo de los iconos **Estado piloto** y **Estado de producción** con las siguientes acciones:

- Se realizan cambios en la evaluación de compatibilidad.
- Los dispositivos se actualizan a la versión de destino de Windows.
- La implementación progresa.

También, puede usar la supervisión de implementación de Configuration Manager igual que cualquier otra implementación de secuencia de tareas. Para más información, vea [Supervisar las implementaciones de sistema operativo en System Center Configuration Manager](../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="desktop-analytics-portal"></a>Portal de Análisis de escritorio

Use el [portal de Análisis de escritorio](https://aka.ms/desktopanalytics) para ver el estado de cualquier plan de implementación. Seleccione el plan de implementación y, luego, **Información general del plan**.

![Captura de pantalla de información general del plan de implementación en Análisis de escritorio](media/deployment-plan-overview.png)

Seleccione el icono **Piloto**. Este icono resume el estado actual de la implementación piloto. También muestra los datos del número de dispositivos no iniciados, en curso, completados o que devuelven problemas.

Los dispositivos que notifican errores u otros problemas también se enumeran en el área de detalles del piloto, a la derecha. Para obtener detalles del problema detectado, seleccione **Revisar**. Esta acción cambia la vista a la página **Estado de implementación**.

La página **Estado de implementación** muestra los dispositivos de las siguientes categorías:

- No iniciado
- En curso
- Completed
- Precisa atención: dispositivos
- Precisa atención: problemas

Las categorías **Precisa atención** muestran la misma información, pero ordenada de manera diferente.

Seleccione una lista concreta de cualquiera de las vistas para obtener más detalles sobre el problema detectado.

A medida que se solucionan estos problemas de implementación, el panel continúa mostrando el progreso de los dispositivos. Se actualiza cuando los dispositivos pasan de **Precisa atención** a **Completado**.

## <a name="next-steps"></a>Pasos siguientes

Permita que el piloto se ejecute durante un rato para recopilar datos operativos. Anime a los usuarios de los dispositivos piloto a que prueben las aplicaciones.

Cuando la implementación piloto cumpla los criterios de éxito, vaya al siguiente artículo para realizar la implementación en producción.
> [!div class="nextstepaction"]  
> [Implementación en producción](deploy-prod.md)  
