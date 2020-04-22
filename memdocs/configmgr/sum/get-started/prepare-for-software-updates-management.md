---
title: Preparar la administración de actualizaciones de software
titleSuffix: Configuration Manager
description: Para preparar la administración de actualizaciones, lleve a cabo estas tareas para mostrar los datos de la evaluación de compatibilidad en la consola de Configuration Manager.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ab22fdcacf7574884f7cfd21859cb4b1aeb8e23f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699503"
---
# <a name="prepare-for-software-updates-management"></a>Preparar la administración de actualizaciones de software

*Se aplica a: Configuration Manager (rama actual)*

Antes de que se muestren los datos de evaluación de compatibilidad de la actualización de software en la consola de Configuration Manager, y antes de poder implementar actualizaciones de software en los equipos cliente, debe llevar a cabo los pasos descritos en las siguientes secciones.

## <a name="step-1-install-a-software-update-point"></a>Paso 1: Instalar un punto de actualización de software  
El punto de actualización de software es necesario en el sitio de administración central (o sitio principal independiente) y en los sitios principales para habilitar la evaluación del compatibilidad de las actualizaciones de software e implementar las actualizaciones de software en los clientes. El punto de actualización de software es opcional en los sitios secundarios. Para obtener información detallada, consulte [Install a software update point](install-a-software-update-point.md) (Instalar un punto de actualización de software).  

## <a name="step-2-synchronize-software-updates"></a>Paso 2: Sincronizar actualizaciones de software
La sincronización de las actualizaciones de software es el proceso de recuperación de los metadatos de actualización de software que cumplen los criterios configurados. Las actualizaciones de software no se muestran en la consola de Configuration Manager hasta que se sincronizan. Para obtener detalles, vea [Synchronize software updates (Sincronizar actualizaciones de software)](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Paso 3: Configurar las clasificaciones y los productos que va a sincronizar
Realice esta configuración en el sitio de administración central o el sitio primario independiente. Después de sincronizar las actualizaciones de software por primera vez, Configuration Manager recupera una lista actualizada de productos y clasificaciones. Ahora puede seleccionar entre las opciones nuevas de las propiedades del componente de punto de actualización de software. Después de configurar las clasificaciones y productos nuevos, repita el paso 2 para iniciar la sincronización de actualizaciones de software para recuperar los metadatos de las actualizaciones de software para los criterios nuevos. Para obtener información detallada, consulte [Configurar las clasificaciones y los productos que va a sincronizar](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Paso 4: Administración de la configuración de actualizaciones de software
Después de sincronizar las actualizaciones de software, compruebe la configuración del cliente de Configuration Manager, la configuración de las directivas de grupo y la configuración de las actualizaciones de software antes de implementarlas. Para obtener información detallada, consulte [Manage settings for software updates](manage-settings-for-software-updates.md) (Administrar la configuración de las actualizaciones de software).
