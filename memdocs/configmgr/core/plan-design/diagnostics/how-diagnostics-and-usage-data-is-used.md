---
title: Uso de datos de diagnóstico
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Microsoft usa los datos de uso y diagnóstico que Configuration Manager recopila.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697133"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Empleo de los datos de diagnóstico y uso de Configuration Manager por parte de Microsoft

*Se aplica a: Configuration Manager (rama actual)*

Los datos de uso y diagnóstico recopilados por Configuration Manager proporcionan información casi inmediata a Microsoft sobre cómo funciona y se usa el producto para ajustar futuras actualizaciones. Microsoft también puede ver datos de configuración que le permite diseñar y probar las configuraciones que se usan en producción. Por ejemplo:

- Versiones de servidor de Windows que se usan en los servidores de sitio

- Paquetes de idioma instalados

- Las diferencias entre el esquema SQL y el valor predeterminado del producto

Estos datos ayudan al equipo de ingeniería a planear futuras pruebas para garantizar la mejor experiencia con las configuraciones más comunes. Estos datos son imprescindibles para ajustarse y adaptarse con un ciclo de versiones frecuente.

Reviste la misma importancia la forma en que no se usan los datos de diagnóstico y uso. Microsoft no utiliza estos datos para:

- Auditorías de licencias, como comparar el uso del cliente con respecto a los contratos de licencia

- Auditoría de los productos que están fuera del soporte técnico

- Publicidad basada en los datos disponibles, como el uso de características o la ubicación geográfica (zona horaria)

Microsoft utiliza los datos disponibles para mejorar el producto. Por ejemplo:

- La compatibilidad inicial que ofrecía la rama actual de Configuration Manager limitaba la escala de tiempo del soporte técnico para Windows Server 2008 R2. Microsoft examinó los datos de uso de los clientes que habían hecho la actualización a la rama actual de Configuration Manager. Después, detectó la necesidad de revisar y ampliar esta escala de tiempo para ofrecer soporte técnico a los clientes que siguen usando este sistema operativo.

- Microsoft mejoró las comprobaciones de requisitos previos para instalar una actualización. Se han quitado las reglas obsoletas, se han incluido casos adicionales y se han solucionado automáticamente algunos problemas.  

> [!div class="nextstepaction"]
> [Recopilación de los datos por parte Configuration Manager](how-diagnostics-and-usage-data-is-collected.md)
