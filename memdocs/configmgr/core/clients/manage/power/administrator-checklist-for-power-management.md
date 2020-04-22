---
title: Lista de comprobación del administrador de energía
titleSuffix: Configuration Manager
description: Use la lista de comprobación del administrador como ayuda para planear e implementar la administración de energía en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 039ebf73fba9850b8479bfabab6ab928b7d6f2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696663"
---
# <a name="administrator-checklist-for-power-management-in-configuration-manager"></a>Lista de comprobación del administrador para la administración de energía en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Esta lista de comprobación del administrador proporciona los pasos recomendados para usar la administración de energía de Configuration Manager en la organización.  

## <a name="configuring-power-management"></a>Configuración de la administración de energía  
 Siga estos pasos para configurar la jerarquía a fin de recopilar información de la administración de energía de los equipos cliente.  

> [!IMPORTANT]  
>  No aplique planes de energía a los equipos de la jerarquía hasta que recopile y analice los datos de energía de los equipos cliente. Si aplica la nueva configuración de administración de energía en equipos sin examinar primero la configuración existente, puede provocar un aumento del consumo de energía.  

|Tarea|Detalles|  
|----------|-------------|  
|Revise los conceptos de administración de energía en la biblioteca de documentación de Configuration Manager.|Vea [Introduction to power management (Introducción a la administración de energía)](introduction-to-power-management.md).|  
|Revise los requisitos previos de administración de energía en la biblioteca de documentación de Configuration Manager.|Vea [Requisitos previos para la administración de energía ](prerequisites-for-power-management.md).|  
|Revise la información sobre los procedimientos recomendados para la administración de energía.|Vea [Prácticas recomendadas para la administración de energía](best-practices-for-power-management.md).|  
|Configure las colecciones para administrar el consumo de energía de los equipos del entorno.|Use la **Colección para la generación de informes de datos de línea de base**, **Colección para la generación de informes de datos de línea de base**, la **Colección de equipos que no pueden administrar la energía**, las **Colecciones de equipos a los que se aplicarán planes de energía**, las **Colecciones de equipos a los que se aplicarán planes de energía** y las **Colecciones de equipos que ejecutan Windows Server** como ayuda para administrar la configuración de energía de los equipos de la jerarquía. Puede crear varias colecciones y aplicar diferentes planes de energía a cada recopilación.|  
|Habilite la administración de energía.|Antes de comenzar a usar la administración de energía, debe habilitarla y configurar las opciones de cliente necesarias. Para más información, vea [Configuración de administración de energía](configuring-power-management.md).|  
|Recopile información de administración de energía de los equipos cliente.|Los clientes notifican los datos de administración de energía a través del inventario de hardware de Configuration Manager. Según la programación de inventario de hardware que haya configurado, puede tardar algún tiempo en recuperar el inventario de todos los equipos cliente.|  

## <a name="monitoring-and-planning-phase"></a>Supervisión y fase de planeamiento  

|Tarea|Detalles|  
|----------|-------------|  
|Ejecute el informe **Actividad de equipo**.|El informe **Actividad de equipo** muestra un gráfico con la actividad del monitor, el equipo y el usuario de una recopilación especificada durante un período de tiempo especificado. Este informe está vinculado al informe **Detalles de actividad de equipo** que muestra las capacidades de suspensión y activación de los equipos de la recopilación especificada. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Ejecute el informe **Consumo de energía** o **Consumo de energía por día**.|Los informes **Consumo de energía** y **Consumo de energía por día** muestran el consumo total de energía mensual en kilovatios por hora (kWh) para una recopilación especificada durante un período de tiempo determinado. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Ejecute el informe **Impacto medioambiental** o  **Impacto medioambiental por día**.|Los informes **Impacto medioambiental** e **Impacto medioambiental por día** muestran un gráfico con las emisiones de dióxido de carbono (CO2) guardadas por una recopilación especificada de equipos para un período de tiempo determinado. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Ejecute el informe **Coste de energía** o **Coste de energía por día**.|Los informes **Coste de energía** y **Coste de energía por día** muestran el coste del consumo total de energía para un período de tiempo especificado. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Ejecute el informe **Capacidades de energía**.|El informe **Capacidades de energía** muestra las capacidades de administración de energía de los equipos de la recopilación especificada. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Ejecute el informe **Configuración de energía**.|El informe **Configuración de energía** muestra una lista agregada de las configuraciones de energía actuales usadas por los equipos de la recopilación especificada. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Excluya las recopilaciones de equipos necesarias de la administración de energía|Vea [Configuración de administración de energía](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Asegúrese de guardar la información de los informes de administración de energía generada durante la fase de supervisión y planeamiento. Puede comparar estos datos con la información de administración de energía generada durante las fases de la aplicación y cumplimiento que le ayudará a evaluar el uso de energía, los costes de energía y el ahorro del impacto medioambiental de aplicar un plan de energía en los equipos de la jerarquía.  

## <a name="enforcement-phase"></a>Fase de aplicación  

|Tarea|Detalles|  
|----------|-------------|  
|Seleccione planes de energía existentes o cree nuevos planes de energía para las recopilaciones de equipos de la organización.|Vea [Cómo crear y aplicar energía planes](create-and-apply-power-plans.md).|  
|Aplique estos planes de energía a equipos.|Vea [Cómo crear y aplicar energía planes](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Datos de cumplimiento  

|Tarea|Detalles|  
|----------|-------------|  
|Ejecute el informe **Actividad de equipo**.|El informe **Actividad de equipo** muestra un gráfico con la actividad del monitor, el equipo y el usuario de una recopilación especificada durante un período de tiempo especificado. Este informe está vinculado al informe **Detalles de actividad de equipo de energía** que muestra las capacidades de suspensión y activación de los equipos de la recopilación especificada. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Ejecute el informe **Consumo de energía** o **Consumo de energía por día**.|Los informes **Consumo de energía** y **Consumo de energía por día** muestran el consumo total de energía mensual en kilovatios por hora (kWh) para una recopilación especificada durante un período de tiempo determinado. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Ejecute el informe **Impacto medioambiental** o **Impacto medioambiental por día**.|Los informes **Impacto medioambiental** e **Impacto medioambiental por día** muestran un gráfico con las emisiones de dióxido de carbono (CO2) guardadas por una recopilación especificada de equipos para un período de tiempo determinado. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Ejecute el informe **Coste de energía** o **Coste de energía por día**.|Los informes **Coste de energía** y **Coste de energía por día** muestran el coste del consumo total de energía para un período de tiempo especificado. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Solución de problemas  

|Tarea|Detalles|  
|----------|-------------|  
|Si los equipos de la jerarquía no han entrado en el modo de suspensión o hibernación, ejecute el informe **Informe de insomnio** para mostrar las causas posibles.|El **Informe de insomnio** muestra una lista de las causas comunes que impidieron que los equipos entraran en modo de suspensión o hibernación y el número de equipos afectados por cada causa durante un período de tiempo especificado. Para más información, vea [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
|Si se aplican varios planes de energía a un equipo, se aplica el plan de energía menos restrictivo. Ejecute el informe **Equipos con varios planes de energía** para ver los equipos con varios planes de energía aplicados.|Vea **Equipos con varios planes de energía** en [Cómo supervisar y planear la administración en el Administrador de configuración de energía](monitor-and-plan-for-power-management.md).|  
