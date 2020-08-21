---
title: Requisitos previos de los informes
titleSuffix: Configuration Manager
description: Analice varias dependencias que afectan al uso de los informes en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b082ae578052a92c0afacd3d1f62fdb2e21bd6d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699541"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Requisitos previos de informes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La generación de informes en Configuration Manager tiene las dependencias siguientes:

- SQL Server Reporting Services
- Punto de servicios de informes
- Power BI Report Server (opcional, a partir de la versión 2002)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Para poder usar los informes en Configuration Manager, instale y configure SQL Server Reporting Services.

Para obtener más información sobre la planeación e implementación de Reporting Services, vea [Instalar SQL Server Reporting Services](/sql/reporting-services/install-windows/install-reporting-services).

Instale la base de datos de Reporting Services en la instancia predeterminada o en una instancia con nombre de una instalación de SQL Server de 64 bits. Coloque la instancia de SQL Server con el servidor de sistema de sitio, o configúrela en un equipo remoto.

Configuration Manager admite las mismas versiones de SQL Server para la generación de informes que para la base de datos de sitio. Para obtener más información, vea [Versiones de SQL Server compatibles](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Punto de servicios de informes

Para poder usar los informes en Configuration Manager, configure el rol de sistema de sitio del punto de servicios de informes.

Para obtener más información, consulte [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint) (Requisitos previos de sitio y sistema de sitio).

## <a name="power-bi-report-server"></a>Power BI Report Server

A partir de la versión 2002, puede integrar informes con Power BI Report Server. Para obtener más información, incluidos los requisitos previos, vea [integrar con Power BI Report Server](powerbi-report-server.md).

## <a name="next-steps"></a>Pasos siguientes

[Configuración de informes](configuring-reporting.md)