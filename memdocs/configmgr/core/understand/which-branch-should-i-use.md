---
title: La rama que se debería usar
titleSuffix: Configuration Manager
description: Obtenga información sobre las diferencias entre las ramas disponibles de Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c54648f1f98ad5fef8efd16d2abe53f204a38f5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700674"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>¿Qué rama de Configuration Manager debo utilizar?

*Se aplica a: Configuration Manager (rama actual y rama de Technical Preview) y System Center Configuration Manager (rama de mantenimiento a largo plazo)*

Hay tres ramas de Configuration Manager disponibles:

- Rama actual
- Rama de mantenimiento a largo plazo
- Rama de Technical Preview

Use este artículo para seleccionar la que más le convenga.

> [!TIP]  
> Todos los sitios de la jerarquía deben ejecutar la misma rama. No se admite una jerarquía con distintas ramas en diferentes sitios.

## <a name="current-branch"></a>Rama actual

Esta rama tiene licencia para uso en un entorno de producción. Use esta rama para obtener las últimas características y funcionalidades. Si tiene una de las siguientes licencias, puede usar esta rama:  

- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- Derechos de suscripción equivalentes  

Para más información sobre Software Assurance y las opciones de licencia, vea [Licencias y ramas de Configuration Manager](learn-more-editions.md) y [Preguntas más frecuentes sobre las licencias y ramas de Configuration Manager](product-and-licensing-faq.md).

Microsoft tiene previsto publicar actualizaciones de la rama actual de Configuration Manager varias veces al año. Cada versión de actualización seguirá siendo compatible durante 18 meses a partir de la fecha de lanzamiento de disponibilidad general (GA). Durante todo el período, ofrecemos soporte técnico. Pero nuestra estructura de soporte técnico es dinámica, es decir, ha evolucionado a dos fases distintas de servicio que dependen de la disponibilidad de la última versión de la rama actual. Para más información, vea [Compatibilidad con versiones de la rama actual de System Center Configuration Manager](../servers/manage/current-branch-versions-supported.md). Las actualizaciones a las versiones más recientes están disponibles como las actualizaciones en la consola.

Para instalar la rama actual como un nuevo sitio, use [medios de línea base](../servers/manage/updates.md#bkmk_Baselines). Además use medios de línea base para actualizar desde System Center 2012 Configuration Manager con Service Pack 2 o System Center 2012 R2 Configuration Manager con Service Pack 1. El acceso a este medio depende del tipo de licencia que tenga la organización para Configuration Manager.

También se pueden usar los medios de línea base para instalar un nuevo sitio que sea una edición de evaluación de la rama actual. La edición de evaluación no requiere una licencia. Puede usar la edición de evaluación de 180 días. Admite la actualización a una edición con licencia de la rama actual. Para instalar únicamente una versión de evaluación, obténgala desde el [Centro de evaluación](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> Use los medios de línea base para instalar sitios para una nueva jerarquía de Configuration Manager. Si ha instalado previamente una versión de línea base, use las actualizaciones en consola para actualizar los sitios a una nueva versión.  
>
> Los sitios que se actualizan mediante las actualizaciones en la consola dan lugar a sitios que son iguales que el nuevo sitio instalado mediante los medios de linea base.
>
> Para obtener más información, vea [Actualizaciones para Configuration Manager](../servers/manage/updates.md).  

### <a name="features-of-the-current-branch"></a>Características de la rama actual

- Recibe [actualizaciones en la consola](../servers/manage/install-in-console-updates.md) que ponen las características nuevas a disposición de los usuarios.
- Recibe actualizaciones en la consola que ofrecen seguridad y revisiones de calidad para las características existentes.
- Admite actualizaciones de fuera de banda cuando sea necesario. Para obtener más información, vea [Uso de la herramienta de registro de actualizaciones](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) o [Uso del instalador de revisiones](../servers/manage/use-the-hotfix-installer-to-install-updates.md).
- Se integra con servicios basados en la nube.
- Admite la [migración de datos](../migration/migrate-data-between-hierarchies.md) desde y hacia otras instalaciones de Configuration Manager.
- Admite la actualización desde versiones anteriores de Configuration Manager.
- Admite la instalación como versión de evaluación, desde la que más adelante puede actualizar a una instalación con licencia completa.

Microsoft recomienda actualizar a la versión más reciente poco después de su lanzamiento. Puede esperar hasta 18 meses antes de actualizar a una versión más reciente. También puede omitir una actualización para instalar la versión más reciente disponible. Dado que cada versión es acumulativa, si omite una actualización e instala la versión más reciente, seguirá teniendo acceso a todas las características y mejoras de las versiones anteriores.

Para obtener más información, vea [Compatibilidad con versiones de la rama actual](../servers/manage/current-branch-versions-supported.md).

### <a name="current-branch-update-options"></a>Opciones de actualización de la rama actual

- Con Software Assurance activo, puede instalar actualizaciones en la consola para las versiones de la rama actual.  
- No hay ninguna opción para convertir la rama actual en una rama de Technical Preview. Las ramas de Technical Preview son instalaciones independientes que no requieren una licencia.
- No existe ninguna opción para convertir la rama actual en una rama de mantenimiento a largo plazo (LSTB). Debe desinstalar la rama actual y luego instalar la LTSB como una nueva instalación.

## <a name="long-term-servicing-branch"></a>Rama de mantenimiento a largo plazo

Se trata de una rama con licencia para uso en producción para los clientes de Configuration Manager que usan la rama actual y que han permitido que su versión de Software Assurance (SA) de Configuration Manager o derechos de suscripción equivalentes expiren después del 1 de octubre de 2016. Para más información sobre Software Assurance y las opciones de licencia, vea [Licencias y ramas de Configuration Manager](learn-more-editions.md) y [Preguntas más frecuentes sobre las licencias y ramas de Configuration Manager](product-and-licensing-faq.md).

LTSB se basa en la versión 1606. Esta rama no recibe las actualizaciones en la consola que ofrecen nuevas características o actualizan las funciones existentes. Sin embargo, se proporcionan las revisiones de seguridad importantes. Para instalar LTSB, debe usar la versión 1606 de [medios de línea base](../servers/manage/updates.md#bkmk_Baselines), que se obtiene con System Center 2016. Las versiones de línea base posteriores no admiten la instalación de LTSB.

Para instalar LTSB como un sitio nuevo o una actualización de un sitio compatible de System Center 2012 Configuration Manager, use la versión 1606 del [medio de línea base](../servers/manage/updates.md#bkmk_Baselines) que se obtiene con System Center 2016. Puede usar los medios de línea base para instalar un nuevo sitio que ejecuta la versión 1606 de la rama actual o un nuevo sitio que ejecuta la rama de mantenimiento a largo plazo.

> [!TIP]  
> Para obtener información sobre System Center 2016, consulte la [documentación de System Center 2016](/system-center/index). Esta documentación también especifica el proceso de obtención de System Center 2016, que requiere un contrato de licencia de Microsoft o derechos similares.  
>  
> Para encontrar la versión 1606 de Configuration Manager en el Centro de servicios de licencias por volumen (VLSC), vaya a la pestaña **Downloads and Keys** (Descargas y claves) de [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), busque `System Center 2016` y luego seleccione **System Center 2016 Datacenter** o **System Center 2016 Standard**.  
>  
> También puede obtener una versión de evaluación de System Center 2016 en el [Centro de evaluación](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  

### <a name="features-of-the-ltsb"></a>Características de la LTSB

- Recibe actualizaciones en la consola que ofrecen las revisiones de seguridad importantes.
- Proporciona una opción de instalación cuando expira el contrato de SA o los derechos equivalentes para Configuration Manager.
- Admite la actualización (conversión) a la rama actual cuando tenga un contrato de SA o derechos equivalentes en vigor para Configuration Manager.

### <a name="ltsb-limitations"></a>Limitaciones de LTSB

La LTSB se basa en la versión 1606 de la rama actual y tiene las siguientes limitaciones:

- La LTSB tiene soporte técnico durante 10 años con actualizaciones de seguridad críticas después de su disponibilidad general (octubre de 2016). Una vez transcurrido este período, el soporte para esta rama expira. Para obtener más información acerca del ciclo de vida de soporte técnico, consulte [Directiva de ciclos de vida de Microsoft](https://support.microsoft.com/lifecycle).
- Admite una lista limitada de conjuntos de sistemas operativos de servidor y cliente, y tecnologías relacionadas, como versiones de SQL Server. Para más información, vea [Configuraciones admitidas para la rama de mantenimiento a largo plazo](supported-configurations-for-ltsb.md).
- No recibe actualizaciones de nuevas características
- No admite las siguientes funciones:
  - Características conectadas a la nube, como la administración conjunta o Análisis de escritorio
  - MDM local
  - El panel de mantenimiento de Windows 10, los planes de mantenimiento o el canal semianual de Windows 10
  - Versiones futuras de la LTSB de Windows 10 y Windows Server
  - Asset Intelligence
  - Ninguna característica de versión preliminar

### <a name="ltsb-update-options"></a>Opciones de actualización de LTSB

- Puede convertir la instalación de LTSB en una instalación de rama actual. Se admite la conversión a la Rama actual antes o después de que caduque la LSTB.

  Para convertir, debe tener un contrato de Software Assurance activo con Microsoft. Vea los siguientes artículos para más información:

  - [Actualizar la rama de mantenimiento a largo plazo a la rama actual](convert-to-current-branch.md)
  - [Licencias y ramas para Configuration Manager](learn-more-editions.md)
  - [Versiones de línea de base y versiones de actualización](../servers/manage/updates.md#bkmk_Baselines)

- No hay ninguna opción para convertir la LTSB en una rama de Technical Preview. Las ramas de Technical Preview son instalaciones independientes que no requieren una licencia.

- No se puede actualizar una edición de evaluación de la rama actual a una instalación de LTSB.

## <a name="technical-preview-branch"></a>Rama de Technical Preview

La rama de Technical Preview está pensada para uso en un entorno de laboratorio. Conozca y pruebe las características más recientes que se están desarrollando para Configuration Manager. No se admite en un entorno de producción y no requiere un contrato de licencia de Software Assurance.

Para instalar un sitio nuevo que ejecute la rama de Technical Preview, use el [medio de línea base para la rama de Technical Preview](../get-started/technical-preview.md#bkmk_install) más reciente. Después de instalar la rama de Technical Preview, las nuevas versiones están disponibles como actualizaciones en la consola cada mes.

### <a name="features-of-the-technical-preview-branch"></a>Características de la rama de Technical Preview

- Se basa en versiones de línea base recientes de la rama actual
- Recibe actualizaciones en la consola que actualizan la instalación a la versión más reciente de la rama de Technical Preview
- Incluye nuevas características que se están desarrollando y sobre las que Microsoft querría recibir comentarios
- Recibe actualizaciones que se aplican solo a la rama de Technical Preview

### <a name="technical-preview-limitations"></a>Limitaciones de Technical Preview

- [El soporte es limitado](../get-started/technical-preview.md#bkmk_reqs), por ejemplo un único sitio primario y hasta 10 clientes.  
- No se puede actualizar o migrar a una rama actual o a una instalación de LTSB.
- No admite los siguientes comportamientos:
  - Uso de la migración para importar o exportar datos a otra instalación de Configuration Manager
  - Actualización desde una versión anterior de Configuration Manager
  - Instalación como una edición de evaluación

Las características que se presentan por primera vez en una rama de Technical Preview a menudo se agregan a la rama actual en una actualización posterior. Cada nueva versión de rama de Technical Preview incluye las características de ramas de Technical Preview anteriores, incluso una vez que esas características se han agregado a la rama actual.

Para más información, vea [Technical Preview para Configuration Manager](../get-started/technical-preview.md).

### <a name="technical-preview-update-options"></a>Opciones de actualización de Technical Preview

- Puede instalar cualquier actualización en la consola para una nueva versión de rama de Technical Preview.

- No hay ninguna opción para convertir una rama de Technical Preview a la rama actual o LTSB.

## <a name="identify-your-version-and-branch"></a>Identificar la versión y la rama

### <a name="version"></a>Version

Para comprobar la versión del sitio, en la esquina superior izquierda de la consola, vaya a **Acerca de Configuration Manager**. Este cuadro de diálogo muestra la **Versión del sitio**. Para obtener una lista de versiones de sitios, vea [Versiones de línea base y versiones de actualización](../servers/manage/updates.md#bkmk_Baselines).

### <a name="branch"></a>Rama

Para confirmar la rama del sitio, en la consola, vaya a **Administración** > **Configuración de sitio** > **Sitios** y abra **Configuración de jerarquía**. Si existe una opción activa de conversión a la rama actual, el sitio ejecuta la versión de LTSB. Cuando el sitio ejecuta la rama actual, la consola deshabilita esta opción.

Para obtener más información sobre las diferentes versiones de Configuration Manager, vea [Versiones de línea base y versiones de actualización](../servers/manage/updates.md#bkmk_Baselines).