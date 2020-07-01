---
title: Ready for Windows
titleSuffix: Configuration Manager
description: Acerca de la retirada del sitio web Ready for Windows
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 18e703691696a2cfc02a5b9715fb6062360229e2
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353469"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Preguntas frecuentes sobre la retirada de Ready for modern desktop

<!-- placeholder -->

## <a name="ready-for-windows-adoption-status"></a>Estado de adopción de Ready for Windows

El estado de adopción se basa en la información de los dispositivos comerciales que comparten datos con Microsoft. El estado se integra con las instrucciones de soporte técnico de los proveedores de software.

Análisis de escritorio proporciona el estado de adopción para cada versión de un recurso que se encuentra en dispositivos comerciales. Este estado no incluye datos de los dispositivos de consumidor ni de aquellos que no comparten datos. El estado puede no ser representativo de la tasa de adopción en todos los dispositivos Windows 10.

Las categorías posibles son:

- **Adopción alta**: al menos 100 000 dispositivos comerciales de Windows 10 tienen instalada esta aplicación.

- **Adoptada**: al menos 10 000 dispositivos comerciales de Windows 10 tienen instalada esta aplicación.

- **Datos insuficientes**: son muy pocos los dispositivos comerciales de Windows 10 que están compartiendo información de esta aplicación como para que Microsoft clasifique su adopción.

- **Ponerse en contacto con el desarrollador**: puede que haya problemas de compatibilidad con esta versión de la aplicación. Microsoft recomienda ponerse en contacto con el proveedor de software para obtener más información.

- **Desconocido**: no hay información disponible para esta versión de esta aplicación. Puede que haya información disponible para otras versiones de la aplicación.

## <a name="general"></a>General

### <a name="what-happened-to-the-ready-for-windows-website"></a>¿Qué ha ocurrido con el sitio web Ready for Windows?

Muchos clientes tienen dificultades para estar siempre actualizados con Windows 10 y Office 365 ProPlus. La principal dificultad es la prueba de aplicaciones, puesto que este proceso suele ser manual. Para los administradores de TI y los propietarios de aplicaciones, se tarda mucho tiempo en analizar continuamente las aplicaciones existentes y luego corregir los problemas que surjan.

En el directorio *Ready for modern desktop* se enumeraban las soluciones de software admitidas y en uso en dispositivos comerciales que ejecutaban Windows 10 y Office 365 ProPlus. El directorio ayuda a los administradores de TI que están pensado en implementar las versiones más recientes de Windows 10 y Office 365.

Los administradores de TI expresan en sus comentarios que quieren que esta información se integre con las herramientas que ya usan para crear sus planes de implementación. Use [Análisis de escritorio](https://aka.ms/dadocs) y las [características de preparación para Office 365 ProPlus](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) de Configuration Manager para planear y administrar los proyectos de actualización de Windows 10 y Office 365 ProPlus. 

> [!Note]
> A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Es posible que siga viendo referencias al nombre anterior en la consola de Configuration Manager y la documentación complementaria mientras se está actualizando la consola.

### <a name="what-is-desktop-analytics"></a>¿Qué es Análisis de escritorio?

[Análisis de escritorio](https://aka.ms/dadocs) es un servicio basado en la nube que se integra con Configuration Manager. Este servicio proporciona información detallada e inteligente para que pueda tomar decisiones más fundamentadas sobre la preparación de actualizaciones de sus punto de conexión de Windows. Combina los datos específicos de la organización con información agregada de los millones de dispositivos Windows conectados a los servicios en la nube de Microsoft.

-    Obtenga una visión completa de los puntos de conexión, las aplicaciones y los controladores en proceso de administración en su organización.

-    Evalúe la compatibilidad de aplicaciones y controladores con las actualizaciones de características de Windows más recientes. Reciba recomendaciones para la mitigación de problemas conocidos, así como información avanzada de las aplicaciones de línea de negocio.

-    Use la inteligencia artificial (IA) de la nube de Microsoft para optimizar el conjunto de dispositivos piloto que representan adecuadamente el entorno global.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>¿Por qué debo usar Análisis de escritorio en mis planes de implementación de Windows?

Análisis de escritorio ofrece las siguientes ventajas:

-    **Inventario de hardware y software**: inventario de factores clave, como aplicaciones y versiones de Windows.

-    **Identificación de piloto**: identificación del conjunto más pequeño de dispositivos que proporcionan la más amplia cobertura de factores. Se centra en los factores que son más importantes para una prueba piloto de actualizaciones de Windows. Al tener la seguridad de que el piloto es más satisfactorio, puede seguir ampliando con rapidez y confianza las implementaciones en producción.

-    **Identificación de problemas**: con los datos de mercado agregados en combinación con los datos de su entorno, el servicio predice posibles problemas para estar siempre actualizado con Windows. Luego, sugiere posibles mitigaciones.

-    **Integración de Configuration Manager**: habilita para la nube la infraestructura local existente. Use estos datos y análisis para implementar y administrar Windows en sus dispositivos.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>¿Qué significa el estado *Ready for Windows* en Análisis de escritorio?

El **estado de adopción** se basa en la información de los dispositivos comerciales que comparten datos con Microsoft. El estado se integra con las instrucciones de soporte técnico de los proveedores de software.

Análisis de escritorio proporciona el estado de adopción para cada versión de un recurso que se encuentra en dispositivos comerciales. Este estado no incluye datos de los dispositivos de consumidor ni de aquellos que no comparten datos. El estado puede no ser representativo de la tasa de adopción en todos los dispositivos Windows 10.

Para más información, consulte [Evaluación de compatibilidad](compat-assessment.md).

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>¿Qué recursos obtiene el estado *Ready for Windows* en Análisis de escritorio? 

Los recursos tienen el estado *Ready for Windows* en Análisis de escritorio en los siguientes casos:

-    El proveedor de software los declara compatibles con la solución.
-    Los clientes los han implementado en un número significativo de dispositivos Windows 10 comerciales que comparten información con Microsoft.
-    El recurso es pertinente para los usuarios comerciales.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>¿Qué información adicional obtengo en Análisis de escritorio?

Análisis de escritorio proporciona un inventario de los [dispositivos y sus aplicaciones instaladas](about-assets.md), así como [información avanzada](compat-assessment.md#advanced-insights) de las aplicaciones de línea de negocio. 

## <a name="software-providers"></a>Proveedores de software

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>¿Todavía puedo mostrar mi solución de software en Análisis de escritorio?

Publique una declaración de compatibilidad de que el producto funciona con Windows 10 de 32 o 64 bits o con Office 365 ProPlus. Para exhibir sus soluciones en Análisis de escritorio, hable con su contacto de Microsoft.

### <a name="how-can-listing-my-solutions-benefit-me"></a>¿Cómo me beneficia la presentación de mis soluciones?

Miles de administradores de TI administran millones de dispositivos con Configuration Manager y Análisis de escritorio. Usan estas herramientas para planear y actualizar con confianza sus organizaciones a la versión más reciente de Windows 10 y Office 365 ProPlus. También las usan para tomar decisiones de compra de soluciones de software.

Microsoft integra declaraciones de compatibilidad de proveedores de software con la información de adopción que reciben de los dispositivos comerciales. Organizaciones de todo el mundo usan estos datos en las herramientas de preparación para Análisis de escritorio y Office. 

Si las declaraciones de compatibilidad no están asociadas correctamente a los recursos, hable con su contacto de Microsoft.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>¿Puedo ver métricas de rendimiento detalladas sobre mis recursos?

Evalúe el rendimiento de las soluciones con informes de estado y métricas a través del centro para desarrolladores: 

- [Tienda Windows](https://docs.microsoft.com/windows/uwp/publish/health-report)
- [Escritorio](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
- [Complementos de Office](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>¿Cómo puedo desarrollar recursos compatibles para Windows 10 y Office 365 ProPlus?

Asegúrese de que las aplicaciones de escritorio sean compatibles con Windows 10 ahora y en el futuro. Para más información, consulte [Compatibilidad de aplicaciones para desarrolladores](https://developer.microsoft.com/windows/desktop/app-compatibility).

Si desarrolla soluciones para Office 365 ProPlus, consulte [Procedimientos de desarrollo recomendados para complementos COM, VSTO y VBA en Office](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).
