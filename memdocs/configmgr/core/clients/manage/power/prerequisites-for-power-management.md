---
title: Requisitos previos de la administración de energía
titleSuffix: Configuration Manager
description: Consulte los requisitos previos de administración de energía en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696523"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Requisitos previos para la administración de energía en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La administración de energía en Configuration Manager tiene dependencias externas y dependencias dentro del producto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  
 En la tabla siguiente se enumeran las dependencias externas a Configuration Manager para usar la administración de energía.  

|Dependencia|Más información|  
|----------------|----------------------|  
|Los equipos cliente deben ser capaces de admitir los estados de energía necesarios|Para usar todas las características de administración de energía, los equipos cliente deben ser capaces de admitir las acciones de suspensión, hibernación, reactivación de una suspensión y reactivación de una hibernación. Puede usar el informe **Capacidades de energía** para determinar si los equipos pueden admitir estas acciones. Para más información, vea [Informe de las capacidades de energía](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) en el tema [Cómo supervisar y planear la administración de energía](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  
 En la tabla siguiente se enumeran las dependencias dentro de Configuration Manager para usar la administración de energía.  

|Dependencia|Más información|  
|----------------|----------------------|  
|La administración de energía debe estar habilitada para poder crear y supervisar planes de energía.|Para más información sobre cómo habilitar y configurar la administración de energía, vea [Configuración de la administración de energía](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Punto de servicios de informes|Debe configurar un punto de servicios de informes antes de poder ver los informes de administración de energía. Para obtener más información, vea [Introducción a los informes](../../../servers/manage/introduction-to-reporting.md).|  
