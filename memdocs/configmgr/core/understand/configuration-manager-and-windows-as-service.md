---
title: Configuration Manager y Windows como servicio
titleSuffix: Configuration Manager
description: Obtenga información básica sobre cómo adoptar la rama actual de Configuration Manager para admitir Windows como servicio.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701253"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager y Windows como servicio

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager proporciona un amplio control sobre las actualizaciones de características en Windows 10. Para adoptar totalmente Windows como modelo de servicio, también debe adoptar el modelo de rama actual de Configuration Manager. Para mantenerse al día con Windows 10 y obtener la mejor experiencia posible, es necesario hacerlo también con Configuration Manager. Las nuevas versiones de Configuration Manager son necesarias para aprovechar al máximo las nuevas y emocionantes características empresariales para Windows 10. Este artículo está diseñado para ser la página de destino de los artículos clave necesarios para adoptar la rama actual de Configuration Manager. La rama actual de Configuration Manager permite iniciar el camino hacia Windows como servicio.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Artículos clave sobre la adopción de la rama actual de Configuration Manager

| Artículo        | Descripción          | 
| ------------- |-------------|
|[Overview of Configuration Manager current branch](../plan-design/changes/whats-new-incremental-versions.md) (Introducción a la rama actual de Configuration Manager)|Se proporciona un breve resumen de los puntos clave para el nuevo modelo de servicio para Configuration Manager (rama actual)|
|[Ciclo de vida de soporte técnico](../servers/manage/current-branch-versions-supported.md)|Se explica el nuevo modelo de soporte técnico y servicios.|
|[Elementos eliminados y en desuso](../plan-design/changes/deprecated/removed-and-deprecated.md)|Se proporcionan notificaciones anticipadas sobre los cambios futuros que es posible que afecten al uso de Configuration Manager.|
|[Updates to Configuration Manager current branch](../servers/manage/updates.md) (Actualizaciones de la rama actual de Configuration Manager)|Se explica el sencillo método en consola para aplicar actualizaciones de características a Configuration Manager.|
|[Obtención de actualizaciones disponibles](../servers/manage/install-in-console-updates.md#get-available-updates)|Se explican los dos modos disponibles para obtener las nuevas actualizaciones de características de Configuration Manager.|
|[Lista de comprobación de actualización](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Se proporcionan listas de comprobación de actualización específicas de la versión, si procede.| 
|[Instalación de nuevas actualizaciones de características de Configuration Manager](../servers/manage/install-in-console-updates.md#bkmk_install)|Se explican los pasos de instalación para actualizaciones de características.|
|[Compatibilidad con Windows 10](../plan-design/configs/support-for-windows-10.md)|Se proporciona una matriz de compatibilidad para versiones de Windows 10 (y ADK).|
|[Technical Preview para Configuration Manager](../get-started/technical-preview.md)|Se proporciona información sobre el programa de Technical Preview de Configuration Manager.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Artículos clave sobre la adopción de Windows como servicio

| Artículo        | Descripción          |
| ------------- |-------------|
|[Administración de Windows como servicio](../../osd/deploy-use/manage-windows-as-a-service.md)|Se explica cómo usar los planes de mantenimiento para implementar actualizaciones de características de Windows 10.|
|[Upgrade Windows 10 via task sequence](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) (Actualizar Windows 10 mediante la secuencia de tareas)|Detalles de la creación de una secuencia de tareas para actualizar Windows 10 con recomendaciones adicionales.|
|[Implementaciones por fases](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|Las implementaciones por fases automatizan una implementación coordinada y secuencial de una secuencia de tareas en varias recopilaciones.|  
|[Optimizar la distribución de actualizaciones de Windows 10](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Use Configuration Manager para administrar el contenido de actualización para estar al día con Windows 10.|
|[Uso de Análisis de escritorio](../../desktop-analytics/overview.md)|Análisis de escritorio permite evaluar y analizar si los dispositivos del entorno están preparados para la actualización a Windows 10.|
|[Integración de Windows Update para empresas (opcional)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Se explica cómo definir e implementar directivas de Windows Update para empresas (WUfB) mediante Configuration Manager.|
|[Uso de la administración conjunta con Microsoft Intune y Windows Update para empresas (opcional)](../../comanage/overview.md)|Se proporciona información general sobre la administración conjunta|


## <a name="related-articles"></a>Artículos relacionados

- [Actualización en contexto a la rama actual de Configuration Manager desde System Center 2012 Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Planeación de la migración a la rama actual de Configuration Manager](../migration/planning-for-migration.md)
