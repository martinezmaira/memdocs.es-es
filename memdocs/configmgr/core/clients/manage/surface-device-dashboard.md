---
title: Panel de dispositivos Surface
titleSuffix: Configuration Manager
description: Revise la información sobre los dispositivos Surface mediante el panel.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 08baf595199bdda121f897d507de97cb7e93e620
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696353"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Panel de dispositivos Surface en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

A partir de la versión 1802, en el panel de dispositivos Surface se proporciona información sobre los dispositivos Surface que se encuentran en el entorno de un solo vistazo. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Abrir el panel de dispositivos Surface

Para abrir el panel de dispositivos Surface, siga estos pasos: 

1. Abra la consola de Configuration Manager. 
2. Haga clic en el nodo **Supervisión**. 
3. Para cargar el panel, haga clic en **Dispositivos Surface**.

**Panel de dispositivos Surface**
![Surface device dashboard](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Revisión de la información en el panel de dispositivos Surface

En el panel de dispositivos Surface se muestran tres gráficos para el entorno. 

- **Percent of Surface devices** (Porcentaje de dispositivos Surface): proporciona el porcentaje de los dispositivos Surface en todo el entorno.

    ![Gráfico Porcentaje de dispositivos Surface](media/Percent-Surface-Devices.PNG)
- **Modelos de Surface**: muestra el número de dispositivos por modelo de Surface. 
  - Al mantener el puntero sobre una sección del gráfico se proporciona el porcentaje de los dispositivos Surface en el modelo seleccionado. 

       ![Gráfico Modelos de Surface](media/Surface-Models-Hover.PNG)
  - Al hacer clic en una sección del gráfico se tiene acceso a una lista de dispositivos para el modelo. 
      ![Lista de dispositivos del modelo de Surface](media/Surface-Model-Device-List.PNG)

- **Cinco versiones principales de firmware**: muestra un gráfico con los cinco modelos de firmware principales en el entorno. 
  - Al mantener el puntero sobre una sección del gráfico se proporciona el porcentaje de los dispositivos Surface en la versión de firmware seleccionada. A partir de la versión 1806 de Configuration Manager, al hacer clic en una sección del gráfico muestra una lista de los dispositivos correspondientes. <!--1358654-->
     ![Lista de dispositivos del modelo de Surface](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Más información

Para obtener más información sobre los dispositivos Surface, vea:
- El sitio web de [Surface]( https://go.microsoft.com/fwlink/?linkid=861998).

Para más información sobre cómo implementar actualizaciones de firmware de Surface en Configuration Manager, vea:
- [Cómo administrar actualizaciones de controladores de Surface en Configuration Manager]( https://support.microsoft.com/help/4098906).




