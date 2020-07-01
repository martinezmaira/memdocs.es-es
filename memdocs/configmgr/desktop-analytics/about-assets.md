---
title: Recursos de Análisis de escritorio
titleSuffix: Configuration Manager
description: Aprenda sobre los dispositivos, los controladores y las aplicaciones de Análisis de escritorio.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: f87c4cc1bcbe8039acb5876dc8e26ac597f12e59
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107301"
---
# <a name="assets-in-desktop-analytics"></a>Recursos de Análisis de escritorio

Después de que los dispositivos comunican datos a Análisis de escritorio, se proporciona un inventario de los siguientes recursos:

- Dispositivos
- Aplicaciones instaladas  

En el portal de servicios, seleccione **Recursos** en el menú de Análisis de escritorio.

## <a name="devices"></a>Dispositivos

En la pestaña **Dispositivos** se muestra información clave sobre todos los dispositivos de la organización que se inscriben en Análisis de escritorio. Puede ordenar valores concretos por columna o filtro.

> [!NOTE]  
> Si el panel no informa del número de dispositivos que espera ver para su entorno, consulte [Solución de problemas de Análisis de escritorio](troubleshooting.md).  

En un plan de implementación, hay más detalles sobre los dispositivos. Para más información, consulte [Planeamiento de recursos](about-deployment-plans.md#plan-assets).

## <a name="apps"></a>Aplicaciones

En la pestaña **Aplicaciones** se muestran todas las aplicaciones instaladas que el servicio detecta en los dispositivos Windows.

Las aplicaciones **destacadas** se instalan en más del 2 % de los dispositivos inscritos.

La opción **App Versions Details** (Detalles de versiones de la aplicación) está desactivada de forma predeterminada, por lo que en esta pestaña se combinan todas las versiones de las aplicaciones con el mismo nombre y el mismo editor.<!-- 5542186 --> El comportamiento predeterminado ayuda a reducir el número total de aplicaciones que se ven, lo que contribuye a reducir la labor de anotar las aplicaciones. El recuento de aplicaciones en el icono **Aplicaciones de interés** también refleja este valor. Por ejemplo, en lugar de mostrar cientos de instancias de Microsoft Edge, hay una sola instancia para todas las versiones. Puede tomar decisiones una vez para todas las versiones. Si tiene que tomar decisiones sobre versiones específicas de una aplicación, active esta opción. También puede establecer esta opción al trabajar con un plan de implementación. Para más información, consulte [Planeamiento de recursos](about-deployment-plans.md#plan-assets).

Seleccione la aplicación en la lista y elija **Editar**. Esta acción muestra los detalles de la aplicación. Seleccione el menú desplegable **Importancia** y establezca un valor. También puede asignar un **propietario**. Si realiza algún cambio, seleccione **Guardar**.

Configure la **importancia** de las aplicaciones mediante una de las siguientes categorías:

- Crítica
- Importante
- Ignorar
- Sin revisar
- No importante<!-- 3587232 -->

Cuando la opción **App Versions Details** (Detalles de versiones de la aplicación) está desactivada, el panel Detalles de la aplicación muestra el número de versiones de la aplicación y los idiomas que combina. Los cambios en los detalles de la aplicación que se guarden, se aplican a todas las versiones. Por ejemplo, establezca la **importancia** o el **propietario**. Algunos valores mostrarán "varios", lo que significa que no hay un valor coherente en todas las versiones.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp"> </a> Decisión de actualización automática de las aplicaciones del sistema y de la tienda

<!-- 3587232 -->
La identificación de **Importancia** y **Decisión de actualización** es fundamental para todas las aplicaciones destacadas del flujo de trabajo de Análisis de escritorio. Para ayudar a reducir el trabajo de anotar estas aplicaciones, determinados tipos de aplicaciones se marcan automáticamente como *No importante*. La decisión de actualizar el plan de implementación de estas aplicaciones también se marca como *Preparado*. Las siguientes aplicaciones son compatibles y deben seguir funcionando después de actualizar Windows:

- Aplicaciones del sistema y componentes publicados por Microsoft

- Aplicaciones administradas y actualizadas desde Microsoft Store

> [!TIP]
> Administre las entradas de cualquier aplicación en un nivel global o por plan de implementación.
>
> 1. En el portal de Análisis de escritorio, en el menú **Administrar**, seleccione **Recursos**. Luego, seleccione **Aplicaciones**.
>
> 2. Use las columnas **Tipo** y **Categoría** para administrar estas categorías de aplicaciones:
>
>    - En el caso de las aplicaciones de la tienda, filtre **Tipo** por **Moderno**
>    - En el caso de las aplicaciones del sistema, filtre **Categoría** por **Proceso en segundo plano** o **Componente de Windows**.

En un plan de implementación, también puede establecer la **decisión de actualización**. Para más información, consulte [Planeamiento de recursos](about-deployment-plans.md#plan-assets).

### <a name="usage"></a>Uso

<!-- 5533890 -->

- **Instalaciones totales**: este valor indica el número de instalaciones de la aplicación seleccionada en todos los dispositivos inscritos en Análisis de escritorio.

- **Porcentaje de instalación**: este valor indica el porcentaje de instalación de la aplicación seleccionada en relación con el número total de dispositivos inscritos en Análisis de escritorio.

- **Dispositivos que han iniciado esta aplicación durante los últimos 30 días**: este valor indica el número de dispositivos en los que un usuario ha iniciado la aplicación seleccionada. Solo incluye los dispositivos que han registrado un uso en los últimos 30 días. Este número engloba todos los dispositivos inscritos con Análisis de escritorio que ejecutan cualquier versión de Windows 10. Es posible que el número varíe según el plan de implementación.

## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre los planes de implementación de Análisis de escritorio](about-deployment-plans.md)  

- [Más información sobre la actualizaciones de características y seguridad](about-updates.md)  

- [Evaluación de compatibilidad en Análisis de escritorio](compat-assessment.md)  
