---
title: Creación de elementos de configuración secundarios
titleSuffix: Configuration Manager
description: Cree elementos de configuración secundarios en Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 319f673200244d4451b957dcb778ce378f9569fa
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240327"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Cómo crear elementos de configuración secundarios en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los elementos de configuración secundarios de Configuration Manager son copias de los elementos de configuración que mantienen una relación con el elemento de configuración original; por tanto, heredan la configuración original del elemento de configuración primario.  

Al ver las propiedades de un elemento de configuración secundario en la consola de Configuration Manager, no puede editar la configuración y los objetos heredados con sus criterios de validación. No obstante, puede agregar y después editar los criterios de validación adicionales para el elemento de configuración secundario, y también puede agregar nuevos objetos y configuraciones en el elemento de configuración secundario.
Un ejemplo para crear y editar un elemento de configuración secundario es ajustar el elemento de configuración original para adaptarse a sus requisitos empresariales.  

> [!NOTE]  
>  Solo puede crear elementos de configuración secundarios a partir de elementos de configuración del tipo **Servidores y equipos de escritorio de Windows (personalizados)** .  

## <a name="to-create-a-child-configuration-item"></a>Cómo crear elementos de configuración secundarios  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

3.  En la lista **Elementos de configuración** , seleccione el elemento de configuración para el que quiere crear un elemento de configuración secundario y después, en la pestaña **Inicio** , en el grupo **Elemento de configuración** , haga clic en **Crear elemento de configuración secundario**.  

4.  En la página **General** del **Asistente para crear elemento de configuración secundario**, puede elegir una revisión concreta del elemento de configuración primario que se usará para crear el elemento secundario. El resto de pasos de este asistente son idénticos a los que seguiría para crear un elemento de configuración estándar. Para obtener más información, consulte [How to create custom configuration items for Windows desktop and server computers](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md) (Cómo crear elementos de configuración personalizados para equipos de escritorio y servidores).  

5.  Complete el asistente. El nuevo elemento de configuración secundario se muestra en la lista **Elementos de configuración** .  
