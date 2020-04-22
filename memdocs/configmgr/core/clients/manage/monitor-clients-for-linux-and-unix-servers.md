---
title: Supervisión de clientes UNIX/Linux
titleSuffix: Configuration Manager
description: Supervise clientes en servidores Linux y UNIX en Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696773"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Supervisión de clientes para servidores Linux y UNIX en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> A partir de la versión 1902, Configuration Manager no admite clientes Linux o UNIX. 
> 
> Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

La información de los servidores Linux y UNIX se puede ver en la consola de Configuration Manager mediante los mismos métodos que se usan para ver la información de clientes basados en Windows.  

 La información que se puede ver incluye lo siguiente:  

- Detalles de estado de los clientes, en los paneles de la consola de Configuration Manager  

- Detalles sobre los clientes en los informes predeterminados de Configuration Manager  

- Detalles de inventario en el Explorador de recursos  

  En las siguientes secciones se describe cómo obtener estos detalles del Explorador de recursos y de los informes.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> Usar el Explorador de recursos para ver el inventario de servidores Linux y UNIX  

 Una vez que un cliente de Configuration Manager envía el inventario de hardware al sitio de Configuration Manager, se puede usar el Explorador de recursos para ver esta información. El cliente de Configuration Manager para Linux y UNIX no agrega nuevas clases ni vistas de inventario al Explorador de recursos. Los datos del inventario de Linux y UNIX se asigna a las clases WMI existentes. Con el Explorador de recursos, es posible ver los detalles de inventario de los servidores Linux y UNIX en la clasificación basada en Windows.  

 Por ejemplo, puede recopilar la lista de todos los programas instalados de forma nativa que se encuentran en los servidores Linux y UNIX. Los ejemplos de programas instalados de forma nativa incluyen **.rpms** en Linux o **.pkgs** en Solaris. Después de que un cliente Linux o UNIX envía el inventario, se puede ver la lista de todos los programas de Linux o UNIX instalados de forma nativa mediante el Explorador de recursos en la consola de Configuration Manager.  

 Para más información sobre cómo usar el Explorador de recursos, vea [Cómo utilizar el Explorador de recursos para ver el inventario de hardware](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Usar informes para ver la información de servidores Linux y UNIX  
 Los informes de Configuration Manager incluyen información de servidores de Linux y UNIX, así como información de equipos basados en Windows. No se necesitan configuraciones adicionales para integrar los datos de Linux y UNIX en los informes.  

 Por ejemplo, si ejecuta el informe denominado Recuento de versiones de sistema operativo, se muestra la lista de los distintos sistemas operativos y el número de clientes que ejecutan cada sistema operativo. El informe se basa en la información de inventario de hardware enviada por los diferentes clientes de Configuration Manager que se ejecutan en los distintos sistemas operativos.  

 También se pueden crear informes personalizados específicos para datos de servidores Linux y UNIX. La propiedad **Título** de la clase de inventario de hardware **Sistema operativo** es un atributo útil que puede usarse para identificar sistemas operativos específicos en la consulta del informe.  

 Para obtener información sobre los informes en Configuration Manager, vea [Introducción a los informes](../../servers/manage/introduction-to-reporting.md).  
