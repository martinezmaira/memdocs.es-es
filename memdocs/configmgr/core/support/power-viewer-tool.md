---
title: Power Viewer Tool
titleSuffix: Configuration Manager
description: Use Power Viewer Tool para ver el estado de la característica de administración de energía en un cliente de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707573"
---
# <a name="power-viewer-tool"></a>Power Viewer Tool

*Se aplica a: Configuration Manager (rama actual)*

Power Viewer Tool es una de las [herramientas de Configuration Manager](tools.md). Úsela para ver el estado de la característica de administración de energía en un cliente de Configuration Manager.

Ejecute **PowerVwr.exe** como administrador. Cuando la herramienta se inicia, muestra las capacidades de energía y la configuración de energía del equipo local en la pestaña **Configuración de energía**. 

Para ver los datos de administración de energía de un equipo remoto:  

1. Vaya al menú **Archivo** y haga clic en **Conectar**. 

2. Escriba el nombre del **equipo** y un **nombre de usuario** y **contraseña**, si es necesario. 

Hay tres pestañas en Power Viewer:  

- **Configuración de energía**: vea las funciones de energía y la configuración de energía del equipo de destino.  

- **Actividad diaria**: vea los gráficos de la actividad diaria del cliente, que incluyen la siguiente información:  

    - **Equipo activado**: el estado de energía del equipo en un día. En el modo de suspensión se considera que el equipo está desactivado.  

    - **Supervisión activada**: estado activado o desactivado de la supervisión en un día.  

    - **Usuario activo**: información de la actividad de usuario en un día.  

- **Eventos de energía**: permite visualizar todos los eventos de energía diarios. El cliente resume estos eventos a las 12:00. Este resumen genera datos para el diagrama de actividad diaria.  
