---
title: Administración de implementaciones de alto riesgo
titleSuffix: Configuration Manager
description: Configure las opciones del sitio de verificación de la implementación en Configuration Manager para advertir a los administradores en caso de que creen una implementación de alto riesgo.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703303"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Configuración para administrar implementaciones de alto riesgo en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Con Configuration Manager, se pueden configurar las opciones del sitio de *verificación de la implementación*. Estos parámetros advierten a los administradores en caso de que creen una implementación de secuencia de tareas de alto riesgo. Se consideran implementaciones de alto riesgo las siguientes:  

- Una implementación que se instala automáticamente  

- Una implementación que tiene el potencial de provocar resultados no deseados  

Por ejemplo, una secuencia de tareas con el propósito **Requerido** que implementa un sistema operativo se considera de alto riesgo.  

> [!WARNING]
> Si usa implementaciones de entorno PXE y configura el hardware del dispositivo con el adaptador de red como primer dispositivo de arranque, estos dispositivos pueden iniciar automáticamente una secuencia de tareas de implementación de sistema operativo sin interacción del usuario. La verificación de la implementación no administra esta configuración. Aunque esta configuración puede simplificar el proceso y reducir la interacción del usuario, coloca al dispositivo ante un riesgo mayor de restablecimiento de imagen inicial accidental.

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a> Configuración de verificación de la implementación

Para reducir el riesgo de una implementación de alto riesgo no deseada, puede configurar límites de tamaño en estas opciones de comprobación de la implementación:  

- **Límites de tamaño de la colección**: al crear una implementación, oculte las colecciones con más clientes que el límite.  

  - **Tamaño predeterminado**: al crear una implementación, esta opción oculta de forma predeterminada las colecciones con más clientes que este límite. Puede ver igualmente estas recopilaciones al crear la implementación, pero están ocultas de manera predeterminada. El valor predeterminado es **100**. Para omitir esta opción, escriba un valor de **0**.  

  - **Tamaño máximo**: al crear una implementación, esta opción siempre oculta las colecciones con más clientes que este límite. El valor predeterminado es **0**, que omite esta opción. El valor del **Tamaño máximo** debe ser mayor que el valor del **Tamaño predeterminado** .  

    Por ejemplo, establezca el **Tamaño predeterminado** en 100 y el **Tamaño máximo** en 1000. Al crear una implementación de alto riesgo, en la ventana **Seleccionar recopilación** solo se muestran las recopilaciones con menos de 100 clientes. Si desactiva la opción **Hide collections with a member count greater than the site's minimum size configuration** (Ocultar recopilaciones con un número de miembros superior a la configuración de tamaño mínimo del sitio), en la ventana se muestran las recopilaciones con menos de 1000 clientes.  

- **Colecciones con servidores del sistema de sitio:** : cuando la colección de destino contiene un equipo con un rol de sistema de sitio, bloquee las implementaciones o solicite una comprobación antes de crear la implementación. Cuando se bloquee una implementación, seleccione otra recopilación que cumpla los criterios de verificación de la implementación para seguir creando la implementación.  

> [!NOTE]
> Las implementaciones de alto riesgo siempre se limitan a las recopilaciones personalizadas, las recopilaciones que cree y la recopilación integrada **Equipos desconocidos** . Si crea una implementación de alto riesgo, no podrá seleccionar una recopilación integrada como **Todos los sistemas**.  

## <a name="configure-deployment-verification"></a>Configuración de verificación de la implementación

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio**; seleccione **Sitios** y luego el sitio primario que quiera configurar.

2. En la cinta de opciones, seleccione **Propiedades** y luego cambie a la pestaña **Verificación de la implementación**.

3. Configure las [opciones](#bkmk_settings) que quiere usar y seleccione **Aceptar** para guardar la configuración y cerrar las propiedades.

## <a name="next-steps"></a>Pasos siguientes

[Administrar secuencias de tareas: Configuración de alto impacto](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[Configurar sitios y jerarquías](../deploy/configure/configure-sites-and-hierarchies.md)
