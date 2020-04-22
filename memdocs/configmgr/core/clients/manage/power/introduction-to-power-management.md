---
title: Introducción a la administración de energía
titleSuffix: Configuration Manager
description: Obtenga una introducción a la administración de energía en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 400fe3113207217504317eeb8ef8bbce4ab6a298
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696573"
---
# <a name="introduction-to-power-management-in-configuration-manager"></a>Introducción a la administración de energía en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La administración de energía de Configuration Manager gestiona la necesidad que tienen muchas organizaciones de supervisar y reducir el consumo de energía de sus equipos. La característica saca partido de las características de administración de energía integradas en Windows para aplicar la configuración pertinente y coherente a los equipos de la organización. Puede aplicar diferentes configuraciones de energía a los equipos durante y fuera del horario laboral. Por ejemplo, puede aplicar un plan de energía más restrictivo a los equipos fuera del horario laboral. En los casos en los que los equipos siempre deban permanecer encendidos, puede impedir la aplicación de la configuración de administración de energía.  

 La administración de energía en Configuration Manager incluye varios informes que le ayudarán a analizar la configuración de energía del equipo y el consumo de energía en su organización. También puede usar los informes para ayudarle a solucionar problemas relacionados con la administración de energía.  

 Para obtener un flujo de trabajo detallado sobre cómo configurar y usar la administración de energía, vea [Lista de comprobación del administrador para la administración de energía](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  La administración de energía de Configuration Manager no se admite en máquinas virtuales. No se pueden aplicar planes de energía a máquinas virtuales, ni se puede informar de datos de energía desde ellas.  

## <a name="the-power-management-workflow"></a>Flujo de trabajo de administración de energía  
 Use las siguientes tres fases para planear e implementar la administración de energía en Configuration Manager.  

### <a name="monitoring-and-planning-phase"></a>Supervisión y fase de planeamiento  
 La administración de energía usa el inventario de hardware de Configuration Manager para recopilar datos sobre el uso del equipo y la configuración de energía para los equipos del sitio. Hay una serie de informes que puede usar para analizar estos datos y determinar la configuración de administración de energía óptima para equipos. Por ejemplo, durante la fase de supervisión y planeamiento del flujo de trabajo de administración de energía, puede crear recopilaciones basadas en los datos que se incluyen en el informe **Capacidades de energía** y usar estos datos para identificar los equipos que no tienen la capacidad de administración de energía. A continuación, puede excluir esos equipos de la administración de energía.  

> [!IMPORTANT]  
>  No aplique planes de energía a los equipos de su sitio hasta que recopile y analice los datos de energía de los equipos cliente. Si aplica la nueva configuración de administración de energía en equipos sin examinar primero la configuración existente, es posible que experimente un aumento en el consumo de energía.  

### <a name="enforcement-phase"></a>Fase de aplicación  
 La administración de energía permite crear planes de energía que puede aplicar a recopilaciones de equipos de su sitio. Estos planes de energía configuran la administración de energía de Windows en equipos. Puede usar los planes de energía que se incluyen con Configuration Manager, o puede configurar sus propios planes de energía personalizados. Puede usar los datos de energía que se recopilan durante la fase de supervisión y planeamiento como línea base para ayudarle a evaluar el ahorro de energía después de aplicar un plan de energía en equipos. Para más información, vea [Lista de comprobación del administrador para la administración de energía](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Datos de cumplimiento  
 En la fase de cumplimiento, puede ejecutar informes que le ayudarán a evaluar el uso de energía y el ahorro de coste de energía en su organización. También puede ejecutar informes que describen las mejoras en la cantidad de CO2 generado por los equipos. También están disponibles informes que ayudan a validar que la configuración de energía que se ha aplicado correctamente en los equipos y que ayudan a solucionar problemas relacionados con la característica de administración de energía.  
