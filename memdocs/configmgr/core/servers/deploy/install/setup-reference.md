---
title: Referencia de instalación
titleSuffix: Configuration Manager
description: Consulte esta referencia para prepararse para instalar un sitio o jerarquía de Configuration Manager.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d948452da54a41e35095b01cb0e942e02a7a597f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700563"
---
# <a name="reference-for-configuration-manager-setup"></a>Referencia de la instalación de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

El programa de instalación de Configuration Manager ofrece vínculos a varios temas que se indican en las secciones siguientes. La información que encontrará aquí puede ayudarle a preparar la instalación de un sitio o jerarquía de Configuration Manager, así como ayudarle a preparar algunas de las decisiones que necesita tomar durante la instalación.  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a> Antes de comenzar  
Antes de instalar nuevos sitios de Configuration Manager, asegúrese de revisar la información siguiente, que puede resultarle útil para preparar correctamente un diseño de implementación:  

-   [Aspectos básicos de Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planear la infraestructura de Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Preparar la instalación de sitios de Configuration Manager](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a> Evaluar la preparación del servidor  
Antes de empezar la instalación de un nuevo sitio, asegúrese de que el servidor de sitio y los servidores del sistema de sitio remoto que quiera usar para el sitio (por ejemplo, el servidor que hospeda la base de datos del sitio) cumplan todos los requisitos previos de configuración. Estos temas de la biblioteca de documentación pueden resultarle útiles:  

-   [Configuraciones admitidas para Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Comprobador de requisitos previos](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Clientes para sistemas operativos adicionales  
Puede descargar el software cliente de Configuration Manager desde el Centro de descarga de Microsoft para los siguientes sistemas operativos:  

- macOS (Apple)
- UNIX
- Linux

Use los vínculos siguientes para descargar los clientes de la versión de Configuration Manager que use:  

- [Microsoft Endpoint Configuration Manager: cliente macOS (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Clientes de Microsoft Configuration Manager para sistemas operativos adicionales](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Configuración y niveles de datos de uso  
Al instalar el primer sitio de Configuration Manager, Configuration Manager instala y configura automáticamente un nuevo rol de sistema de sitio (el **punto de conexión de servicio**) en el servidor de sitio. El punto de conexión de servicio tiene esta configuración predeterminada:  

-   Modo **con conexión** (también hay disponible un modo sin conexión)  
-   Nivel **mejorado** de recopilación de datos (también hay disponibles otros dos niveles de recopilación de datos, básico y completo)  

Cuando el rol de sistema de sitio del punto de conexión de servicio está con conexión, Microsoft puede recopilar automáticamente información de uso y diagnósticos por Internet. La información recopilada nos ayuda a realizar las siguientes tareas:  

-   Identificar y solucionar problemas  
-   Mejorar nuestros productos y servicios  
-   Identificar las actualizaciones de Configuration Manager que se aplican a la versión de Configuration Manager actualmente en uso  

### <a name="levels-of-data-collection"></a>Niveles de recopilación de datos  
En la recopilación de datos se incluyen estos tres niveles:

-   En el nivel **básico** se incluyen datos sobre la instalación y la actualización, como el número de sitios y las características de Configuration Manager que están habilitadas. No se transmite información de identificación personal.  

-   En el nivel **mejorado** se incluyen los datos de la configuración del nivel básico y, además, se transmiten datos sobre la jerarquía, el uso de cada característica (en frecuencia y duración) e información de diagnóstico mejorada, como el estado de memoria del servidor si se produce un bloqueo del sistema o de una aplicación. No se transmite información de identificación personal.  

-   En el nivel **completo** se incluyen los datos de la configuración de los niveles básico y mejorado y, además, se envía información de diagnóstico avanzada, como archivos del sistema e instantáneas de memoria. Con esta opción podría incluirse información de identificación personal, pero no usaremos esa información para identificarle o ponernos en contacto con usted, ni para enviarle publicidad.  

Para más información, incluida la divulgación de los detalles recopilados por cada nivel, vea [Diagnósticos y datos de uso para Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Para ver la declaración de privacidad en línea de Configuration Manager, vaya a [https://go.microsoft.com/fwlink/?LinkID=626527](https://go.microsoft.com/fwlink/?LinkID=626527).
