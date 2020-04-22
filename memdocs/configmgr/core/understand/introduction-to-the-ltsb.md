---
title: Introducción a LTSB
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de mantenimiento a largo plazo de Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eda58982094860ccf075bcd2d1d8ed9e3d3bb2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706923"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Obtenga información sobre la rama de mantenimiento a largo plazo de Configuration Manager.

*Se aplica a: System Center Configuration Manager (rama de mantenimiento a largo plazo)*

La rama de mantenimiento a largo plazo (LTSB) de System Center Configuration Manager es un canal distinto de Configuration Manager que se ha diseñado como opción de instalación disponible para todos los clientes. Sin embargo, se trata de la única opción para los clientes que dejen caducar sus derechos de suscripción de Software Assurance (SA) o equivalente para Configuration Manager.

Basada en la versión 1606 de Configuration Manager, la LTSB tiene menor funcionalidad cuando se compara con la rama actual de Configuration Manager.

> [!TIP]   
> La LTSB de Configuration Manager no está relacionado con el canal de mantenimiento a largo plazo (LTSC) del conjunto de System Center. Para obtener más información, vea [Información general de las opciones de publicación de System Center](https://docs.microsoft.com/system-center/ltsc-and-sac-overview).

## <a name="features-that-arent-available"></a>Características que no están disponibles

La rama actual de Configuration Manager admite la funcionalidad siguiente que no está disponible cuando se usa la LTSB:

- Actualizaciones en consola que agregan nueva funcionalidad y mejoras.
- Compatibilidad con sistemas operativos recién publicados que se usen como clientes y servidores de sitio.
- MDM local
- Los planes y el panel de mantenimiento de Windows 10, incluida la compatibilidad con las versiones recientes de Windows 10.  
- Compatibilidad con versiones futuras de Windows 10 LTSB y Windows Server
- Asset Intelligence
- Puntos de distribución basados en la nube
- Exchange Online como Exchange Connector    

Aunque la compatibilidad con estas características no está disponible en la LTSB, algunas características permanecen visibles en la consola de Configuration Manager, pero no se pueden seleccionar ni usar.

Las integraciones en la nube, así como las características incluidas con la versión de la rama actual 1610 o posterior de Configuration Manager, no están disponibles para la LTSB. Entre estas características se incluyen las siguientes:<!--SCCMDocs#1823-->

- Administración conjunta
- Análisis de escritorio
- Puerta de enlace de administración en la nube
- Integración de Azure Active Directory
- Aplicaciones de Microsoft Store para Empresas

## <a name="find-ltsb-documentation"></a>Búsqueda de documentación de LTSB

La LTSB se basa en la versión 1606 de la rama actual. Use la [documentación de la rama actual](https://docs.microsoft.com/sccm/), con advertencias y limitaciones que son específicas de la LTSB. Estas advertencias y limitaciones se identifican en los artículos siguientes:

- [Instalar la rama de mantenimiento a largo plazo](install-the-ltsb.md)
- [Actualizar la rama de mantenimiento a largo plazo a la rama actual](convert-to-current-branch.md)
- [Configuraciones admitidas de la rama de mantenimiento a largo plazo](supported-configurations-for-ltsb.md)
- [Administrar la rama de mantenimiento a largo plazo de Configuration Manager](manage-the-ltsb.md)

Cuando se hace referencia a la documentación de la rama actual sobre la rama de mantenimiento a largo plazo, los detalles que se aplican a la versión 1606 también se aplican dicha rama de mantenimiento. Las características o los detalles que se presentan con la versión 1610 o versiones posteriores no se admiten en la rama de mantenimiento a largo plazo.

## <a name="licensing-overview-for-the-ltsb"></a>Introducción a las licencias para la LTSB   

Los clientes con Software Assurance (SA) activo en licencias de Configuration Manager o con derechos de suscripción equivalentes el 1 de octubre de 2016, tienen derecho a usar la versión 1606 de octubre de 2016 de Configuration Manager. Los clientes con derechos para Configuration Manager el 1 de octubre de 2016 o después de esta fecha encontrarán dos opciones de licencia tras la instalación: la rama actual y la rama de mantenimiento a largo plazo (LTSB).

Los clientes que tengan derechos perpetuos en System Center Configuration Manager, o que admitan que SA o la suscripción expiren después del 1 de octubre, pueden instalar la versión de LTSB de System Center Configuration Manager actual en el momento de caducidad.

Para obtener más información sobre estas licencias, vea los [términos y condiciones completos de los productos que compra mediante los programas de licencias por volumen de Microsoft](https://go.microsoft.com/fwlink/?LinkId=800052).

Para obtener más información sobre licencias para ramas de Configuration Manager, vea [Licencias y ramas para Configuration Manager](learn-more-editions.md).

## <a name="next-steps"></a>Pasos siguientes

Si decide que la LTSB de Configuration Manager es la rama adecuada para su entorno, [instale un nuevo sitio de LTSB](install-the-ltsb.md#install-a-new-site) como parte de una nueva jerarquía o [actualice un sitio de System Center 2012 Configuration Manager](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager) y la jerarquía.
