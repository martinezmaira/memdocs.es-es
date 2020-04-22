---
title: Consideraciones especiales sobre la migración
titleSuffix: Microsoft Intune
description: En este artículo se proporcionan aspectos especiales sobre la migración que deben considerarse antes de iniciar una campaña de migración a Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f29d2894-e98b-4f2c-b444-a8ccc1b7efdd
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a954732b2df5824d7116dc10e035b10290c0290
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "79358330"
---
# <a name="special-migration-considerations"></a>Consideraciones especiales sobre la migración

Hay consideraciones especiales sobre la migración que se pueden aplicar en función del entorno del proveedor de MDM existente.

## <a name="wipe-for-apples-device-enrollment-program-dep"></a>Borrado para el Programa de inscripción de dispositivos (DEP) de Apple

El Programa de inscripción de dispositivos (DEP) de Apple establece configuraciones de dispositivo que el usuario final no puede quitar. Para conservar las características de administración avanzada del DEP, el dispositivo se debe devolver al estado original (nuevo) mediante un borrado para inscribirlo en Intune.

Para seguir usando DEP a fin de administrar los dispositivos en Intune, [configure la inscripción de dispositivos iOS/iPadOS con el Programa de inscripción de dispositivos](../enrollment/device-enrollment-program-enroll-ios.md).

## <a name="next-steps"></a>Pasos siguientes

[Fase 2: Campaña de migración](migration-guide-campaign.md)
