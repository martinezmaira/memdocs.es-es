---
title: Acerca de la instalación y la actualización
titleSuffix: Configuration Manager
description: Obtenga información acerca de la diferencia entre las condiciones de instalación, actualización al administrar la infraestructura de Configuration Manager.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706723"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Acerca de la actualización e instalación para sitios y jerarquía de infraestructura

*Se aplica a: Configuration Manager (rama actual)*

Al administrar sitios de Configuration Manager y la infraestructura de la jerarquía, los términos *mejorar*, *actualizar* e *instalar* se emplean para describir tres conceptos diferentes.

## <a name="upgrade"></a>Mejorar

La *actualización* o *actualización in situ* se usan al convertir la jerarquía o el sitio de Configuration Manager 2012 en una jerarquía o un sitio que ejecuta la rama actual de Configuration Manager.

Cuando actualice de System Center 2012 Configuration Manager a la rama actual de Configuration Manager, seguirá usando los mismos servidores para hospedar los sitios y servidores de sitios y para conservar los datos y configuraciones existentes de Configuration Manager.  Esto difiere de la [migración](../migration/migrate-data-between-hierarchies.md), que es una manera de conservar las configuraciones y datos relativos a los dispositivos administrados mientras se usan los nuevos sitios de la rama actual de Configuration Manager instalados en el nuevo hardware.

Para más información, vea [Actualizar a Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).



## <a name="update"></a>Actualizar
La *actualización* se usa para instalar actualizaciones en la consola de Configuration Manager y para actualizaciones fuera de banda, que son actualizaciones que no se pueden enviar desde la consola de Configuration Manager. Las actualizaciones en la consola pueden modificar la versión del sitio de la rama actual (o sitio de vista previa técnica), por lo ejecuta una versión superior. Por ejemplo, si el sitio ejecuta la versión 1806, puede instalar una actualización para la versión 1810. Las actualizaciones también pueden instalar revisiones para un problema conocido sin modificar la versión del sitio.      

Normalmente, las actualizaciones agregan revisiones de seguridad, mejoras de calidad y nuevas características a la implementación existente. Si usa la rama de versión preliminar técnica, una actualización puede instalar una versión más reciente de la versión preliminar técnica.
- Elija cuándo instalar la actualización en la consola, comenzando por el sitio del nivel superior de la jerarquía.
- Puede instalar cualquier actualización disponible desde dentro de la consola. Por ejemplo, si su sitio ejecuta la versión 1802 y se ofrecen 1806 y 1810, considere instalar la versión 1810 porque cada versión incluye las características que estaban disponibles primero en las versiones publicadas anteriormente.
- Después de que se complete una nueva actualización en el sitio de nivel superior, los sitios primarios principales inician automáticamente el proceso de actualización. Sin embargo, puede establecer [Ventanas de servicio](../servers/manage/service-windows.md) para controlar la temporización de las actualizaciones.
- Los sitios secundarios no instalan automáticamente las actualizaciones. En su lugar, inicie manualmente la actualización desde dentro de la consola de Configuration Manager.

Para más información, vea [Actualizaciones de Configuration Manager](../servers/manage/updates.md) y [Technical Preview de Configuration Manager](../get-started/technical-preview.md).



## <a name="install"></a>Instalar
La *instalación* se utiliza cuando crea una nueva jerarquía de Configuration Manager desde el principio o cuando agrega sitios adicionales a una jerarquía existente.  

Cuando se instala un nuevo sitio primario o un sitio de administración central, la ubicación de setup.exe y los archivos de origen relacionados que utiliza dependen de su escenario de instalación.

Para obtener más información, consulte [Preparar la instalación de sitios](../servers/deploy/install/prepare-to-install-sites.md).
