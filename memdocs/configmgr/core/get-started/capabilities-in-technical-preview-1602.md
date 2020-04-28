---
title: Funcionalidades de Technical Preview 1602
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1602.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 64d01598f3d5feb162898761645ac84b1c73b175
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074476"
---
# <a name="capabilities-in-technical-preview-1602-for-configuration-manager"></a>Funciones de Technical Preview 1602 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1602 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.  

 Estas son las nuevas características que puede probar con esta versión.  

##  <a name="improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a> Mejoras en la administración de dispositivos móviles  

### <a name="ios-activation-lock"></a>Bloqueo de activación de iOS  
 Configuration Manager puede ayudarle a administrar el bloqueo de activación de iOS, una característica de la aplicación Buscar mi iPhone disponible en iOS 7.1 y en dispositivos más modernos. El bloqueo de activación se habilita automáticamente cuando se usa la aplicación Buscar mi iPhone en un dispositivo. Tras su activación, se debe escribir el identificador y la contraseña de Apple del usuario para poder:  

- Desactivar Buscar mi iPhone  

- Borrar el dispositivo  

- Reactivar el dispositivo  

  Configuration Manager puede solicitar el estado de bloqueo de activación de los dispositivos supervisados y no supervisados que ejecutan iOS 7.1 y versiones posteriores. Para los dispositivos supervisados, Intune puede recuperar el código de bypass del bloqueo de activación y emitirlo directamente al dispositivo.  

##  <a name="improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a> Mejoras en el Centro de software en la versión 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Actualizar la directiva de usuario y máquina desde el Centro de software  
 Se ha agregado una nueva opción, **Directiva de sincronización**, a la página **Opciones** > **Mantenimiento del equipo** del Centro de software que hace que el equipo actualice su directiva de usuario y máquina de Configuration Manager.  

##  <a name="improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a> Mejoras en mantenimiento de Windows 10  
 En la versión Technical Preview 1602 se agregaron las siguientes mejoras al mantenimiento de Windows 10:  

-   Nuevas opciones de filtro para los planes de mantenimiento.  Ahora puede filtrar por **Idioma**, **Necesario** y **Título**. Solo se agregarán a la implementación asociada las actualizaciones que cumplan con los criterios especificados.  

-   Cuando se selecciona la clasificación **Actualizaciones** para la sincronización de las actualizaciones de software, se muestra un cuadro de diálogo de advertencia para informarle de que la [revisión 3095113](https://support.microsoft.com/kb/3095113) de WSUS es necesaria para sincronizar correctamente las actualizaciones de software y para que el mantenimiento de Windows 10 se realice correctamente.  Desde el cuadro de diálogo, puede ir al artículo de knowledge base de la revisión.  

-   Ahora las actualizaciones de Windows 10 disponibles solo se muestran en el nodo **Mantenimiento de Windows 10** \ **Todas las actualizaciones de Windows 10** de la consola de Configuration Manager. Estas actualizaciones ya no se mostrarán en el nodo **Actualizaciones de software** \ **Todas las actualizaciones de software**.  

-   Se mostrará a los usuarios finales que inicien un paquete de actualización de Windows 10 un cuadro de diálogo para notificarles que van a actualizar su sistema operativo.  
