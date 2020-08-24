---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de Technical Preview para probar nuevas funcionalidades y funcionalidades de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76d1edf8598e1abd71b6fd1db7faffa1750110d4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129127"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview para Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

Este artículo proporciona detalles sobre de la rama de Technical Preview mensual de Configuration Manager. Technical Preview presenta una funcionalidad nueva en que está trabajando Microsoft. Presenta características nuevas que no están todavía incluida en la rama actual de Configuration Manager. Estas características podrían incluirse finalmente en una actualización de la rama actual. Antes de finalizar la las características, queremos que las pruebe y nos comparta sus comentarios.

Como esta es una versión preliminar técnica, los detalles y las funcionalidades están sujetos a cambios.

Esta información se aplica a todas las versiones de la rama de Technical Preview de Configuration Manager. En este artículo se enumera cada una de las características nuevas junto con la versión de Technical Preview en las que aparece por primera vez. Por ejemplo, la versión **2001** de enero (`01`) de 2020 (`20`). Los artículos independientes dedicados a cada versión preliminar detallan las características individuales.

Para más información sobre las novedades de la *rama actual* de Configuration Manager, consulte [Novedades de las versiones incrementales de Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a> Limitaciones y requisitos

> [!IMPORTANT]
> La versión preliminar técnica solo tiene licencia para su uso en un entorno de laboratorio. Es posible que Microsoft no proporcione servicios de soporte técnico y que algunas características no estén disponibles en las versiones preliminares técnicas. Además, es posible que el software de versión preliminar técnica tenga estándares de seguridad, privacidad, accesibilidad, disponibilidad y confiabilidad reducidos o diferentes a los del software proporcionado comercialmente.

Para la mayoría de requisitos previos de producto, use la información que se encuentra en las [configuraciones admitidas](../plan-design/configs/supported-configurations.md). Las excepciones siguientes se aplican a la rama de Technical Preview:

- Cada instalación permanece activa durante 90 días y luego cambia a inactiva.

- El único idioma admitido es el inglés.

- Solo admite los parámetros de línea de comandos de configuración siguientes:

  - `/silent`
  - `/testdbupgrade`

- El punto de conexión del servicio se instala en el modo en línea. No admite el modo sin conexión.

- En los artículos independientes de cada versión específica de Technical Preview se incluyen limitaciones o requisitos adicionales, según corresponda.

- Las características siguientes no son compatibles con la rama de Technical Preview:

  - [Migración](../migration/migrate-data-between-hierarchies.md) desde o hasta esta rama de versión preliminar.

  - [Actualización](../servers/deploy/install/upgrade-to-configuration-manager.md) a esta rama de versión preliminar.

  - [Recuperación del sitio](../servers/manage/recover-sites.md) desde la carpeta cd.latest.<!--507106-->

- No se admite la actualización de esta rama de versión preliminar a la rama actual.

    > [!Note]
    > Cuando haya actualizaciones disponibles para una versión preliminar, seguirá siendo posible buscarlas e instalarlas desde el nodo **Actualizaciones y mantenimiento** de la consola de Configuration Manager. Para ver un vídeo del proceso de actualización en la consola, vea [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Instalación de las actualizaciones de Configuration Manager) en youtube.com.

- Solo admite un sitio primario independiente. No se admiten sitios de administración central, varios sitios primarios ni sitios secundarios.

La rama de Technical Preview de Configuration Manager admite los productos y las tecnologías siguientes:

- A menos que se indique lo contrario, la rama de Technical Preview admite las mismas versiones de SQL Server que la rama actual. Para obtener más información, vea [Versiones de SQL Server compatibles](../plan-design/configs/support-for-sql-server-versions.md).

- El sitio admite hasta 10 clientes que pueden ejecutar cualquier [versión de SO de cliente compatible](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- SCCMDocs#1656 -->

> [!Note]
> La inclusión de estos productos en este contenido no implica una extensión de la compatibilidad con una versión que están fuera de su ciclo de vida de soporte. Configuration Manager no es compatible con los productos que están fuera de su ciclo de vida de soporte. Para más información, consulte [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle).

## <a name="install-and-update"></a><a name="bkmk_install"></a> Instalación y actualización

La rama de Technical Preview de Configuration Manager para su uso en laboratorio es distinta de la rama actual de Configuration Manager para su uso en producción.

En primer lugar, instale una versión de base de referencia de la rama de Technical Preview. Después de instalar una versión de referencia, use las actualizaciones en consola para que la instalación se actualice a la versión preliminar más reciente. Normalmente, las nuevas versiones de Technical Preview están disponibles cada mes.

Microsoft admite cada versión de Technical Preview hasta que hay disponibles tres versiones sucesivas. Por ejemplo, cuando se publica la versión 1908, se deja de admitir la versión 1904. Las versiones 1905, 1906 y 1907 siguen siendo compatibles. Cuando una base de referencia deja de ser compatible, todavía se admite para instalar un nuevo sitio de Technical Preview, suponiendo que se actualiza inmediatamente a una versión compatible. La base de referencia anterior se admite hasta que haya disponible una versión de base de referencia nueva. Actualice a la versión disponible más reciente desde la base de referencia y repita el proceso de actualización hasta instalar la versión de Technical Preview más reciente.

> [!TIP]
> Cuando se instala una actualización de versión preliminar técnica, la instalación de versión preliminar se actualiza a la nueva versión preliminar técnica. Una instalación de Technical Preview nunca tiene la opción de actualizar a una instalación de rama actual. Tampoco recibe nunca actualizaciones desde la versión de rama actual.
>
> Varias veces a lo largo del año, hay versiones de rama de Technical Preview y versiones de rama actuales con el mismo número de versión. Por ejemplo, hay una versión 1910 de Technical Preview y una versión 1910 de rama actual.

### <a name="active-baseline-versions"></a>Versiones de base de referencia activas

Instale una versión de base de referencia hasta un año después de su lanzamiento. Al instalar un nuevo sitio de Technical Preview, use la versión de línea de base más reciente. Las siguientes versiones de la rama Technical Preview de Configuration Manager están disponibles como actualizaciones en la consola y como nuevas versiones de línea base:

- **Versión 2007, Technical Preview**

Descargue las versiones de línea de base del [Centro de evaluación](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> Proporcionar comentarios

Nos encanta recibir sus comentarios sobre las características nuevas en Technical Preview. Para obtener más información, vea [Comentarios sobre el producto](../understand/find-help.md#product-feedback).

Si tiene ideas sobre algunas características nuevas que le gustaría ver, no dude en decírnoslo. Envíe sus nuevas ideas y vote las ideas de otras personas: [UserVoice de Configuration Manager](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> Características de la versión más reciente

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2007.md) <!--ID-->

Las características siguientes están disponibles con la versión de Technical Preview de Configuration Manager más reciente:

### <a name="technical-preview-version-2008"></a>Versión preliminar técnica 2008

- [Versión preliminar de consultas de la recopilación](2020/technical-preview-2008.md#collection-query-preview) <!--7380401-->
- [Análisis de errores de SetupDiag en actualizaciones de características](2020/technical-preview-2008.md#bkmk_setupdiag) <!--4385028-->
- [Supervisión del estado del escenario](2020/technical-preview-2008.md#bkmk_health) <!--7699463-->
- [Vista de evaluación de la recopilación](2020/technical-preview-2008.md#bkmk_colleval) <!--6251274-->
- [Consulta del tamaño de la secuencia de tareas en la consola](2020/technical-preview-2008.md#bkmk_tssize) <!--7645732-->
- [Tarea para eliminar archivos de diagnóstico recopilados antiguos](2020/technical-preview-2008.md#bkmk_logs) <!--6503308-->
- [Importación de objetos en la carpeta actual](2020/technical-preview-2008.md#bkmk_folder) <!--6601203-->

> [!NOTE]
> Las características que estaban disponibles en una versión anterior de Technical Preview siguen estando disponibles en versiones posteriores. Del mismo modo, las características que se agregan a la rama actual de Configuration Manager siguen estando disponibles en la rama de Technical Preview.

## <a name="features-in-recent-technical-previews"></a>Características en versiones recientes de Technical Preview

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Las características siguientes se publicaron con versiones anteriores de la rama de la versión preliminar técnica de Configuration Manager desde la versión 2006 de la rama actual:

> [!TIP]
> Cuando esté disponible una nueva versión de la rama actual, se mostrarán las características que disponibles en esa versión en el último artículo sobre las *novedades*. Para obtener más información, vea [Novedades en las versiones incrementales](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### <a name="technical-preview-version-2007"></a>Versión 2007, Technical Preview

- [Asociación de inquilinos: Vista del inventario de hardware en el Centro de administración de Microsoft Endpoint Manager](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [Mejoras en el panel de orígenes de datos de cliente](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [Fuente con ancho fijo que se usa ahora en algunas áreas de la consola](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [Administración del tamaño de la directiva de secuencia de tareas](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [Mejoras en la escala de tiempo del dispositivo en el centro de administración](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

## <a name="features-in-previous-technical-previews"></a>Características de las versiones de Technical Preview anteriores

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Las características siguientes se lanzaron con versiones anteriores de la rama de Technical Preview de Configuration Manager. Estas características siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en la rama actual.

| Característica        | Versión de Technical Preview |
|----------------|---------------------------|
| Uso de la aplicación Portal de empresa en dispositivos administrados conjuntamente <!--3601237--> | [Versión preliminar técnica 2006](2020/technical-preview-2006.md#bkmk_portal) |
| Mejoras en las aplicaciones disponibles a través de CMG <!--7033501--> | [Versión preliminar técnica 2006](2020/technical-preview-2006.md#bkmk_availapp) |
| Asociación de inquilinos: Mejoras en las acciones de Configuration Manager del centro de administración de Microsoft Endpoint Manager <!--7518897--> | [Versión preliminar técnica 2006](2020/technical-preview-2006.md#bkmk_apps) |
| Asociación de inquilinos: escala de tiempo del dispositivo en el centro de administración <!--7141381--> | [Versión preliminar técnica 2005](2020/technical-preview-2005.md#bkmk_timeline) |
| Asociación de inquilinos: instalación de una aplicación desde el centro de administración <!--6024389--> | [Versión preliminar técnica 2005](2020/technical-preview-2005.md#bkmk_apps) |
| Asociación de inquilinos: CMPivot desde el centro de administración <!--6024392--> | [Versión preliminar técnica 2005](2020/technical-preview-2005.md#bkmk_cmpivot) |
| Asociación de inquilinos: ejecución de scripts desde el centro de administración <!--6234688--> | [Versión preliminar técnica 2005](2020/technical-preview-2005.md#bkmk_scripts) |
| Mejoras en los cmdlets de Cloud Management Gateway <!--6978300--> | [Versión preliminar técnica 2005](2020/technical-preview-2005.md#bkmk_pwshcmg) |
| Notificación de errores de instalación y actualización a Microsoft <!--5622909--> | [Versión preliminar técnica 2005](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) |
| Mejoras en la herramienta de limpieza de la biblioteca de contenido <!--6887878--> | [Versión preliminar técnica 2005](2020/technical-preview-2005.md#bkmk_content) |
| Copia de datos de detección desde la consola <!--6890051--> | [Versión preliminar técnica 2004](2020/technical-preview-2004.md#bkmk_copydisco) |
| Compatibilidad con PowerShell, versión 7 <!--6023299--> | [Versión preliminar técnica 2004](2020/technical-preview-2004.md#bkmk_pwsh7) |
| Nuevo asistente para comentarios <!--3180826--> | [Versión preliminar técnica 2003](2020/technical-preview-2003.md#bkmk_feedback) |
| Consulta de comentarios enviados a Microsoft <!--6488450--> | [Versión preliminar técnica 2003](2020/technical-preview-2003.md#bkmk_smile) |
| Anexo de archivos a los comentarios <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Mejoras en los puntos de distribución habilitados para multidifusión <!--3785535--> | [Tech Preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Plantillas de implementación por fases <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Control remoto en cualquier lugar mediante Cloud Management Gateway <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Programa de estimación de costes de servicios en la nube <!--3555774--> | [Versión preliminar técnica 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Servicio del respondedor PXE basado en cliente <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Compatibilidad con el arranque de red de PXE para IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Uso de Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Mejoras en Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Vea también

Vea los siguientes artículos para más información:

- [Evaluar Configuration Manager en un laboratorio](evaluate-with-lab-environment.md)
- [Novedades de las versiones incrementales de Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)
- [Introducción a Configuration Manager](../understand/introduction.md)

> [!Tip]
> Para más información sobre las características de la rama actual que requieren consentimiento, consulte las [características de versión preliminar](../servers/manage/pre-release-features.md).
>
> Para más información sobre las características de la rama actual que se deben habilitar primero, consulte [Habilitar características opcionales de las actualizaciones](../servers/manage/install-in-console-updates.md#bkmk_options).
