---
title: Niveles de datos de uso y diagnóstico
titleSuffix: Configuration Manager
description: Obtenga información sobre los niveles de datos de diagnóstico y uso que se recopilan en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9de63280786d620229c7d408f09ef2fe583e231d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703803"
---
# <a name="levels-of-diagnostic-usage-data"></a>Niveles de datos de uso y diagnóstico

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager recopila tres niveles de datos de diagnóstico y de uso: **Básico**, **Mejorado** y **Completo**. De forma predeterminada, esta característica se establece en el nivel Mejorado.

> [!IMPORTANT]
> Configuration Manager no recopila códigos de sitio, nombres de sitios, direcciones IP, nombres de usuario o equipo, direcciones físicas o direcciones de correo electrónico en los niveles Básico o Mejorado. Cualquier recopilación de esta información en el nivel Completo no tiene ninguna finalidad. Se incluye potencialmente en la información de diagnóstico avanzada como archivos de registro o instantáneas de memoria. Microsoft no usa esta información para identificarle, para ponerse en contacto con usted ni para el desarrollo de publicidad.

## <a name="levels"></a>Niveles

### <a name="basic"></a>Básico

El nivel Básico incluye datos sobre la jerarquía. Es necesario para ayudar a mejorar la experiencia de instalación o actualización. Estos datos también ayudan a determinar las actualizaciones de Configuration Manager que se aplican a la jerarquía.

### <a name="enhanced"></a>Mejorado

El nivel Mejorado es el valor predeterminado después de que finalice la instalación. Este nivel incluye datos que se recopilan en el nivel Básico y datos específicos de características. Muestra la frecuencia y duración de uso de diferentes características. También incluye datos de configuración del cliente de Configuration Manager: nombre de componente, estado y determinadas opciones como intervalos de sondeo. La información sobre actualizaciones de software contiene información básica sobre como usar las características y no incluye datos sobre el cumplimiento de las actualizaciones en este nivel.

Microsoft recomienda este nivel porque proporciona los datos mínimos necesarios para realizar mejoras de productos y servicios.

Ejemplos de datos que este nivel no incluye:

- Nombres de sitios, usuarios, equipos u otros objetos

- Detalles de objetos relacionados con la seguridad

- Vulnerabilidades, como recuentos de sistemas, que requieren actualizaciones de software

### <a name="full"></a>Full

El nivel Completo incluye todos los datos de los niveles Básico y Mejorado. También incluye información adicional sobre Endpoint Protection, porcentajes de cumplimiento de actualización e información de actualización de software. Este nivel también puede incluir información de diagnóstico avanzada, como archivos del sistema e instantáneas de memoria. Estos datos avanzados pueden incluir información personal existente en la memoria o los archivos de registro en el momento de captura.

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Cómo cambiar el nivel

Para cambiar el nivel de recopilación de datos, necesita permisos **Modificar** en la clase de objeto **Sitio**.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.
1. Haga clic en **Configuración de jerarquía** en la cinta de opciones.
1. Vaya a la pestaña **Datos de diagnóstico y uso** y elija el nivel de datos.

## <a name="version-specific-details"></a><a name="bkmk_versions"></a> Detalles específicos de la versión

En los artículos que hay a continuación se incluyen los datos específicos que Configuration Manager recopila en cada nivel con cada versión admitida:

- [Datos de diagnóstico y uso en la versión 2002](levels-of-diagnostic-usage-data-collection-2002.md)
- [Datos de diagnóstico y uso en la versión 1910](levels-of-diagnostic-usage-data-collection-1910.md)
- [Datos de diagnóstico y uso en la versión 1906](levels-of-diagnostic-usage-data-collection-1906.md)
- [Datos de diagnóstico y uso en la versión 1902](levels-of-diagnostic-usage-data-collection-1902.md)
- [Datos de diagnóstico y uso en la versión 1810](levels-of-diagnostic-usage-data-collection-1810.md)

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Preguntas más frecuentes](frequently-asked-questions.md)
