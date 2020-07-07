---
title: Actualizaciones de Análisis de escritorio
titleSuffix: Configuration Manager
description: Aprenda sobre las actualizaciones de características y seguridad de Análisis de escritorio.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 96a014f4919480854b57bae82e982ce783f5f59b
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590973"
---
# <a name="updates-in-desktop-analytics"></a>Actualizaciones de Análisis de escritorio

En el portal de Análisis de escritorio, vea el estado de las actualizaciones de características y seguridad. Seleccione estos nodos del grupo de supervisión del menú principal de Análisis de escritorio. Estos nodos proporcionan información detallada sobre el estado de estas actualizaciones en el entorno.

<!--7362999-->

> [!IMPORTANT]
> Análisis de escritorio muestra el estado de actualización de la seguridad y las características de los dispositivos con el id. comercial asociado al área de trabajo de Análisis de escritorio. Este comportamiento se produce con independencia de que haya inscrito o no los dispositivos con Configuration Manager. El número total de dispositivos en estos iconos puede no coincidir con el número de dispositivos inscritos en [**Servicios conectados**](monitor-connection-health.md#commercial-id-configuration).

## <a name="security-updates"></a>Actualizaciones de seguridad

Para revisar el estado actual de las actualizaciones de seguridad, seleccione **Actualizaciones de seguridad** en la sección **Supervisión** de Análisis de escritorio:

![Nodo de actualizaciones de seguridad de Análisis de escritorio](media/security-updates.png)

En esta vista se resumen las actualizaciones de *seguridad* de los dispositivos que ejecutan Windows 10. Los dispositivos del gráfico de barras se clasifican por las siguientes etiquetas:

#### <a name="latest"></a>Más reciente

Los dispositivos ejecutan la actualización de seguridad más reciente de esa versión y canal.

#### <a name="latest-1"></a>Más reciente 1

Los dispositivos ejecutan una actualización de seguridad de una versión anterior a la última disponible en dicho canal.

#### <a name="older"></a>Antigua

Los dispositivos ejecutan una actualización de seguridad anterior a Más reciente-1.

#### <a name="not-measured"></a>No medido

Análisis de escritorio no ha evaluado el dispositivo. Este estado incluye los dispositivos que ejecutan Windows 7 y Windows 8.1 o los dispositivos Windows 10 registrados para el programa Windows Insider.  

Para ver las tendencias de adopción de las actualizaciones de seguridad, seleccione **Ver más** para una versión específica de Windows. El gráfico de áreas apiladas clasifica los dispositivos por la actualización de seguridad que han instalado en el tiempo.

Para revisar el estado de implementación de las actualizaciones de seguridad, seleccione **Ver todas**. En esta vista se enumeran los dispositivos de las categorías siguientes:

- No iniciado
- En curso
- Completed
- Necesita atención: dispositivos (ordenados por nombre de dispositivo)
- Necesita atención: problemas (ordenados por tipo de problema)

Para mostrar los dispositivos con información nueva que el servicio sigue procesando, seleccione **Ver datos recientes**. Análisis de escritorio mostrará esta información después de la siguiente actualización de datos completa.

  > [!IMPORTANT]
  > La opción de Análisis de escritorio para **Ver datos recientes** está en desuso. Esta acción se quitará en una versión futura del servicio de Análisis de escritorio. Para más información, vea [Deprecated Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md) (Características en desuso).<!--7080949-->  

## <a name="feature-updates"></a>Actualizaciones de características

Para revisar el estado actual de las actualizaciones de características, seleccione **Actualizaciones de características** en la sección **Supervisión** de Análisis de escritorio:

![Nodo de actualizaciones de características de Análisis de escritorio](media/feature-updates.png)

En esta vista se resumen las actualizaciones de *características* de los dispositivos que ejecutan Windows 10.

Para más información sobre los períodos de servicio, consulte [Hoja de datos del ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Los dispositivos del gráfico de barras se clasifican por las siguientes etiquetas:

#### <a name="in-service"></a>En servicio

Los dispositivos ejecutan la actualización de características más reciente de esa versión y canal.  

#### <a name="near-end-of-service"></a>Próximo fin de servicio

Los dispositivos ejecutan una actualización de características que se encuentra a 90 días de llegar a final del servicio.

#### <a name="end-of-service"></a>Fin de servicio

Los dispositivos ejecutan una actualización de características que ha pasado la fecha de fin de servicio. Estas fechas son específicas de las ediciones Empresa y Educación de Windows. No se aplican a las ediciones Hogar, Pro, Pro Education o Pro for Workstations. Para más información, consulte [Hoja de datos del ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>No medido

Análisis de escritorio no ha evaluado el dispositivo. Este estado incluye los dispositivos que ejecutan Windows 7 y Windows 8.1 o los dispositivos Windows 10 registrados para el programa Windows Insider.

Seleccione el icono para ver las tendencias de adopción de las actualizaciones de características. El gráfico de áreas apiladas clasifica los dispositivos por la actualización de características que han instalado en el tiempo.

## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre los recursos de Análisis de escritorio](about-assets.md): dispositivos, controladores y aplicaciones  

- [Más información sobre los planes de desarollo](about-deployment-plans.md)  
