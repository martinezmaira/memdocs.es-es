---
title: Ubicaciones de archivo de base de datos personalizadas
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo especificar ubicaciones personalizadas para archivos de base de datos de SQL Server.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc7eb1a8ba721545bdee50d45887ab9d3aa8e952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704703"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Ubicaciones personalizadas para archivos de base de datos del sitio de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

 Configuration Manager es compatible con las ubicaciones personalizadas de los archivos de base de datos de SQL Server.  

> [!NOTE]  
>  La opción de especificar ubicaciones de archivos no predeterminadas no está disponible cuando se usa un clúster de SQL Server.  

 **Durante la configuración** de un nuevo sitio principal o un sitio de administración central, puede hacer lo siguiente:  

-   **Especificar ubicaciones de archivo no predeterminadas para la base de datos del sitio**: después, el programa de instalación de Configuration Manager crea la base de datos del sitio mediante estas ubicaciones.  

-   **Especificar el uso de una base de datos de SQL Server existente que use ubicaciones de archivo personalizadas**:  después, el programa de instalación de Configuration Manager usa esa base de datos existente y las ubicaciones de archivo preconfiguradas.  

**Después de la configuración**, puede cambiar la ubicación de los archivos de la base de datos del sitio. Para ello, es necesario detener el sitio y editar la ubicación de los archivos en SQL Server:  

-   En el servidor de sitio de Configuration Manager, detenga el servicio **SMS_Executive**.  

-   Use la documentación de su versión de SQL Server para obtener información sobre cómo mover una base de datos de usuario. Por ejemplo, si usa SQL Server 2014, vea [Mover bases de datos de usuario](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) en TechNet.  

-   Después de completar el movimiento de archivos de la base de datos, reinicie el servicio **SMS_Executive** en el servidor de sitio de Configuration Manager.  
