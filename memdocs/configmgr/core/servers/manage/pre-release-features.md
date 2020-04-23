---
title: Características de la versión preliminar
titleSuffix: Configuration Manager
description: Las características de versión preliminar son las que se encuentran en la rama actual para realizar las primeras pruebas en un entorno de producción.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703543"
---
# <a name="pre-release-features-in-configuration-manager"></a>Características de versión preliminar en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las características de versión preliminar son las que se encuentran en la rama actual para realizar las primeras pruebas en un entorno de producción. Estas características son totalmente compatibles, pero siguen en fase de desarrollo activo. Es posible que reciban cambios hasta que se saquen de la categoría de versión preliminar.

## <a name="give-consent"></a>Dar el consentimiento  

Antes de usar las características de versión preliminar, dé su consentimiento para usarlas. Dar el consentimiento es una acción que se realiza una sola vez por jerarquía y no se puede deshacer. Mientras no dé su consentimiento, no podrá habilitar las características de versión preliminar nuevas incluidas con las actualizaciones. Después de activar una característica de versión preliminar, no se puede desactivar.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Haga clic en **Configuración de jerarquía** en la cinta de opciones.  

3. En la pestaña **General** de las Propiedades de configuración de la jerarquía, habilite la opción **Consentimiento para usar características de versión preliminar**. Haga clic en **Aceptar**.  

## <a name="enable-pre-release-features"></a>Habilitar características de la versión preliminar

Cuando se instala una actualización que incluye características de versión preliminar, esas características son visibles en el Asistente de actualizaciones y mantenimiento con las características convencionales incluidas en la actualización.

### <a name="if-you-have-given-consent"></a>Si ha dado su consentimiento

En el Asistente de actualizaciones y mantenimiento, habilite las características de versión preliminar. Seleccione las características de versión preliminar como haría con cualquier otra característica.

Opcionalmente, espere a habilitar las características de versión preliminar más tarde desde el nodo **Características** de **Actualizaciones y mantenimiento** en el área de trabajo **Administración**. Seleccione una característica y, después, haga clic en **Activar** en la cinta. Hasta que dé su consentimiento, esta opción no está disponible para su uso.

### <a name="if-you-havent-given-consent"></a>Si no ha dado su consentimiento

En el Asistente de actualizaciones y mantenimiento, las características de versión preliminar están visibles pero no se pueden habilitar. Después de instalar la actualización, estas características son visibles en el nodo **Características**. Pero no las puede habilitar hasta que no dé su consentimiento.

> [!IMPORTANT]  
> En una jerarquía multisitio solo se pueden habilitar características opcionales o de versión preliminar desde el sitio de administración central. Con este comportamiento se procura que no haya ningún conflicto en la jerarquía. <!--507197-->  
>
> Si ha dado su consentimiento en un sitio primario independiente y, después, expande la jerarquía mediante la instalación de un sitio de administración central nuevo, deberá volver a dar su consentimiento en el sitio de administración central.  

Al habilitar una característica de versión preliminar, el Administrador de jerarquía de Configuration Manager (HMAN) debe procesar el cambio antes de que dicha característica esté disponible. El procesamiento del cambio suele ser inmediato. Según el ciclo de procesamiento de HMAN, puede tardar hasta 30 minutos en completarse. Una vez procesado el cambio, reinicie la consola antes de usar la característica.

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a> Lista de características de la versión preliminar

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Característica          | Agregado como versión preliminar | Agregado como característica completa |
|------------------|----------------------|-------------------------|
| [Grupos de orquestaciones](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | Versión 2002 | ![Todavía no](media/red_x.png) |
| [Tipo de implementación de la secuencia de tareas](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | Versión 2002 | ![Todavía no](media/red_x.png) |
| [Quitar el sitio de administración central](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | Versión 2002 | ![Todavía no](media/red_x.png) |
| [Depurador de secuencia de tareas](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Versión 1906 | ![Todavía no](media/red_x.png) |
| [Grupos de aplicaciones](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Versión 1906 | ![Todavía no](media/red_x.png) |
| [Detección de grupos de usuarios de Azure Active Directory](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Versión 1906 | Versión 2002 |
| [Sincronización de los resultados de pertenencia a recopilaciones con Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Versión 1906| Versión 2002 |
| [CMPivot independiente](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | Versión 1906 | Versión 2002 |
| [Servicio de administración Proveedor de SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | Versión 1810 | Versión 1906 |
| [Sistema de sitio HTTP mejorado](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | Versión 1806 | Versión 1810 |
| [Aplicaciones cliente para dispositivos administrados conjuntamente](../../../comanage/workloads.md#client-apps) <br/> (antes denominadas *aplicaciones móviles para dispositivos administrados conjuntamente*) <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Versión 1806 | Versión 2002 |
| [Administrador de conversión de paquetes](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | Versión 1806 | Versión 1810 |
| [Implementaciones por fases](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | Versión 1802 | Versión 1806 |
| [Administración del control de aplicaciones de Windows Defender](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | Versión 1702 | Versión 1906 |
| [Mantenimiento de una recopilación compatible con clústeres (grupos de servidores)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Versión 1602 | ![Todavía no](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> Para más información sobre las características de versión preliminar que se deben habilitar primero, vea [Habilitar características opcionales de las actualizaciones](install-in-console-updates.md#bkmk_options).  
>
> Para más información sobre las características que solo están disponibles en la rama de Technical Preview, vea [Technical Preview](../../get-started/technical-preview.md).  
