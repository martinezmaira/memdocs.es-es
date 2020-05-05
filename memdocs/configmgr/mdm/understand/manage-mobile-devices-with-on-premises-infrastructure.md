---
title: MDM local
titleSuffix: Configuration Manager
description: Más información acerca de la administración local de dispositivos móviles (MDM) en Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724679"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager la administración de dispositivos móviles (MDM) local es una solución de administración de dispositivos que se basa en las capacidades integradas de administración de Windows. Esta característica se basa en el estándar de administración de dispositivos (DM) Open Mobile Alliance (OMA). Usa la infraestructura de Configuration Manager de su organización para administrar y mantener los dispositivos. Su organización requiere Microsoft Intune licencias para usar esta característica, pero no requiere ninguna conexión a la nube. Configuration Manager almacena todos los datos acerca de los dispositivos en la base de datos del sitio local.

La MDM local difiere de Microsoft Intune, que también se basa en las funcionalidades integradas de OMA DM. Todas las funciones de administración de Intune se entregan a través de Cloud Services. La MDM local también difiere de la solución de administración basada en cliente que tradicionalmente ofrece Configuration Manager. Se basa en una infraestructura similar, pero no usa software cliente instalado de forma independiente en los dispositivos que administra.  

## <a name="comparison"></a>De comparación

En las siguientes secciones se enumeran las ventajas y desventajas de la MDM local en comparación con la administración basada en cliente tradicional:  

### <a name="advantages"></a>Ventajas

- **Infraestructura simplificada**: se necesitan menos roles de sistema de sitio.

- **Fácil de mantener**: dado que la funcionalidad de administración está integrada en el sistema operativo del dispositivo, no se necesitan nuevas versiones del cliente Configuration Manager cuando se introducen nuevas características de administración en el sitio.

- **Local**:-todos los datos y la administración se conservan de forma local.

### <a name="disadvantages"></a>Inconvenientes

**Menos funcionalidad de administración de cliente**: no hay orquestación, medición de software, integración de terceros, secuenciación de tareas ni soporte técnico del centro de software.

- **Compatibilidad con dispositivos limitados**: MDM local no admite tantas versiones del sistema operativo como el cliente Configuration Manager. Para más información, consulte [Versiones de sistemas operativos compatibles para clientes y dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="next-step"></a>Paso siguiente

Obtenga información sobre lo que debe tener en cuenta al configurar la infraestructura de Configuration Manager y planear la inscripción de dispositivos en MDM local.

> [!div class="nextstepaction"]
> [Planear la MDM local](../plan-design/plan-on-premises-mdm.md)  
