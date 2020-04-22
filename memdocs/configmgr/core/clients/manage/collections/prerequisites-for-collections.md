---
title: Requisitos previos de las recopilaciones
titleSuffix: Configuration Manager
description: Consulte los requisitos previos para usar recopilaciones en Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695543"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Requisitos previos de las recopilaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las recopilaciones de Configuration Manager solo contienen dependencias dentro del producto.  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Punto de servicios de informes|El rol de sistema de sitio de punto de servicios de informes debe instalarse antes de poder ejecutar informes para las recopilaciones. Para obtener más información, vea [Introducción a los informes](../../../servers/manage/introduction-to-reporting.md).|  
|Para administrar recopilaciones, se deben tener permisos de seguridad específicos.|Debe tener los siguientes permisos de seguridad para administrar la configuración de cumplimiento:<br /><br /> - Para crear y administrar recopilaciones: permisos **Crear**, **Eliminar**, **Modificar**, **Modificar carpeta**, **Mover objeto**, **Leer** y **Leer recurso** en el objeto **Collection**.<br /><br /> - Para administrar la configuración de la recopilación: permiso **Modificar configuración de recopilación** en el objeto **Collection**.<br /><br /> El permiso **Modificar carpeta** es necesario para todas las carpetas de la recopilación, incluida la carpeta raíz.|  
