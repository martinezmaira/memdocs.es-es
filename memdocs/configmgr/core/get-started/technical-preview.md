---
title: Versiones de Technical Preview
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de Technical Preview para probar nuevas funcionalidades y funcionalidades de Configuration Manager.
ms.date: 03/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec49f9931240e17218c125f1fa514088c83c55fd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701843"
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

- Solo es compatible con las versiones siguientes de **SQL Server**:

  - SQL Server 2017 (con la actualización acumulativa 2 o posterior)
  - SQL Server 2016 (sin ningún Service Pack)
  - SQL Server 2014 (con Service Pack 1, o versiones posteriores)
  - SQL Server 2012 (con Service Pack 3, o versiones posteriores)

- El sitio admite hasta 10 clientes que pueden ejecutar cualquier [versión de SO de cliente compatible](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- SCCMDocs#1656 -->

> [!Note]
> La inclusión de estos productos en este contenido no implica una extensión de la compatibilidad con una versión que están fuera de su ciclo de vida de soporte. Configuration Manager no es compatible con los productos que están fuera de su ciclo de vida de soporte. Para más información, consulte [Directiva de ciclo de vida de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).

## <a name="install-and-update"></a><a name="bkmk_install"></a> Instalación y actualización

La rama de Technical Preview de Configuration Manager para su uso en laboratorio es distinta de la rama actual de Configuration Manager para su uso en producción.

En primer lugar, instale una versión de base de referencia de la rama de Technical Preview. Después de instalar una versión de referencia, use las actualizaciones en consola para que la instalación se actualice a la versión preliminar más reciente. Normalmente, las nuevas versiones de Technical Preview están disponibles cada mes.

Microsoft admite cada versión de Technical Preview hasta que hay disponibles tres versiones sucesivas. Por ejemplo, cuando se publica la versión 1908, se deja de admitir la versión 1904. Las versiones 1905, 1906 y 1907 siguen siendo compatibles. Cuando una base de referencia deja de ser compatible, todavía se admite para instalar un nuevo sitio de Technical Preview, suponiendo que se actualiza inmediatamente a una versión compatible. La base de referencia anterior se admite hasta que haya disponible una versión de base de referencia nueva. Actualice a la versión disponible más reciente desde la base de referencia y repita el proceso de actualización hasta instalar la versión de Technical Preview más reciente.

> [!TIP]
> Cuando se instala una actualización de versión preliminar técnica, la instalación de versión preliminar se actualiza a la nueva versión preliminar técnica. Una instalación de Technical Preview nunca tiene la opción de actualizar a una instalación de rama actual. Tampoco recibe nunca actualizaciones desde la versión de rama actual.
>
> Varias veces a lo largo del año, hay versiones de rama de Technical Preview y versiones de rama actuales con el mismo número de versión. Por ejemplo, hay una versión 1910 de Technical Preview y una versión 1910 de rama actual.

### <a name="active-baseline-versions"></a>Versiones de base de referencia activas

Instale una versión de base de referencia hasta un año después de su lanzamiento. Al instalar un nuevo sitio de Technical Preview, use la versión de línea de base más reciente.

- **Versión 2002 de Technical Preview**: la versión 2002 de la rama Technical Preview de Configuration Manager está disponible como actualización en la consola y como nueva versión de línea de base.

Descargue las versiones de línea de base del [Centro de evaluación de TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

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
<!-- - [title](2020/technical-preview-2003.md#bkmk_anchor) <!--ID-->

Las características siguientes están disponibles con la versión de Technical Preview de Configuration Manager más reciente:

### <a name="technical-preview-version-2003"></a>Versión 2003 de Technical Preview

- [Incorporación de clientes de Configuration Manager a ATP de Microsoft Defender a través de la consola de Microsoft Endpoint Manager](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [Seguimiento de las correcciones de elementos de configuración](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [Visualización de los grupos de límites de los dispositivos](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [Nuevo asistente para comentarios](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Mejoras en el panel Administración de Microsoft Edge](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [Mejoras en CMPivot](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [Consulta de comentarios enviados a Microsoft](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [Nuevo método de SDK para el progreso de la secuencia de tareas](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [Mejoras de la implementación del sistema operativo](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

> [!NOTE]
> Las características que estaban disponibles en una versión anterior de Technical Preview siguen estando disponibles en versiones posteriores. Del mismo modo, las características que se agregan a la rama actual de Configuration Manager siguen estando disponibles en la rama de Technical Preview.

<!-- temp remove for 2002 CB ## Features in recent technical previews -->

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

<!--temp remove for 2002 CB  The following features were released with previous versions of the Configuration Manager technical preview branch since current branch version 1910: -->

> [!TIP]
> Cuando esté disponible una nueva versión de la rama actual, se mostrarán las características que disponibles en esa versión en el último artículo sobre las *novedades*. Para obtener más información, vea [Novedades en las versiones incrementales](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

<!-- ### Technical preview version 2003 -->

## <a name="features-in-previous-technical-previews"></a>Características de las versiones de Technical Preview anteriores

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Las características siguientes se lanzaron con versiones anteriores de la rama de Technical Preview de Configuration Manager. Estas características siguen estando disponibles en versiones posteriores, pero todavía no están disponibles en la rama actual.

| Característica        | Versión de Technical Preview |
|----------------|---------------------------|
| Anexo de archivos a los comentarios <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Mejoras en los puntos de distribución habilitados para multidifusión <!--3785535--> | [Tech Preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Plantillas de implementación por fases <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Control remoto en cualquier lugar mediante Cloud Management Gateway <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Mejoras en el Centro de comunidad <!--3555935--> | [Tech Preview 1906](2019/technical-preview-1906.md#bkmk_hub) |
| Mejoras en el Centro de comunidad <!--4224401--> | [Tech Preview 1905](2019/technical-preview-1905.md#bkmk_hub) |
| GitHub y Centro de comunidad <!--3555935--> | [Tech Preview 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| Programa de estimación de costes de servicios en la nube <!--3555774--> | [Versión preliminar técnica 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Descarga de informes desde el Centro de comunidad <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Centro de comunidad <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
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
