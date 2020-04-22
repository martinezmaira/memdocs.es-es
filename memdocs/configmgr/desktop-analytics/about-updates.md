---
title: Actualizaciones de Análisis de escritorio
titleSuffix: Configuration Manager
description: Aprenda sobre las actualizaciones de características y seguridad de Análisis de escritorio.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec510414f11aa312e6c1a7d1d5bfa8126f473fe3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706583"
---
# <a name="updates-in-desktop-analytics"></a>Actualizaciones de Análisis de escritorio

En el portal de Análisis de escritorio, vea el estado de las actualizaciones de características y seguridad. Seleccione estos nodos del grupo de supervisión del menú principal de Análisis de escritorio. Estos nodos proporcionan información detallada sobre el estado de estas actualizaciones en el entorno.


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

Si un dispositivo Windows 10 *no está autenticado* con un cuenta Microsoft, Windows no informa de estos datos. Esta autenticación se realiza normalmente como parte de la configuración rápida de Windows (OOBE).<!-- 5148153 -->


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

Si un dispositivo Windows 10 *no está autenticado* con un cuenta Microsoft, Windows no informa de estos datos. Esta autenticación se realiza normalmente como parte de la configuración rápida de Windows (OOBE).<!-- 5148153 -->


## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre los recursos de Análisis de escritorio](about-assets.md): dispositivos, controladores y aplicaciones  

- [Más información sobre los planes de desarollo](about-deployment-plans.md)  
