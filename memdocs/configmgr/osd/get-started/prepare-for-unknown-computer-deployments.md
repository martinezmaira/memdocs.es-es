---
title: Preparación para implementaciones en equipos desconocidos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar sistemas operativos en equipos que no están administrados por Configuration Manager en el entorno de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708823"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Preparar implementaciones en equipos desconocidos en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Emplee la información de este tema para implementar sistemas operativos en equipos desconocidos del entorno de Configuration Manager. Un equipo desconocido es un equipo no administrado por Configuration Manager. Esto significa que no hay ningún registro de estos equipos en la base de datos de Configuration Manager. Los equipos desconocidos incluyen los siguientes:  

- Un equipo que no tiene instalado el cliente de Configuration Manager  

- Un equipo que no se importa en Configuration Manager  

- Un equipo que no ha detectado Configuration Manager  

  Puede implementar sistemas operativos en equipos desconocidos con los siguientes métodos de implementación:  

- [Usar PXE para implementar Windows a través de la red](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Usar medios de arranque para implementar un sistema operativo](../deploy-use/create-bootable-media.md)  

- [Usar medios preconfigurados para implementar un sistema operativo](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Flujo de trabajo de implementación en un equipo desconocido  
 Este es el flujo de trabajo básico para implementar un sistema operativo en un equipo desconocido:  

-   Seleccione un objeto de equipo desconocido para usar en la implementación. Puede implementar el sistema operativo en uno de los objetos de equipo desconocido de la recopilación **Todos los equipos desconocidos** , o puede agregar los objetos de la recopilación **Todos los equipos desconocidos** a otra recopilación. Configuration Manager proporciona dos objetos de equipo desconocido en la recopilación **Todos los equipos desconocidos**. Un objeto es para equipos x86 y el otro objeto es para equipos x64.  

    > [!NOTE]  
    >  El objeto **x86 - Equipo desconocido** es para equipos que solo son compatibles con x86. El objeto **x64 - Equipo desconocido** es para equipos que son compatibles con x86 y x64. En otras palabras, estos objetos describen la arquitectura del equipo de destino. No describen el sistema operativo que quiere implementar en el equipo de destino.  

-   Configure un punto de distribución habilitado con PXE o cree medios para admitir implementaciones en equipos desconocidos.  

-   Implemente la secuencia de tareas para instalar el sistema operativo.  

## <a name="unknown-computer-installation-process"></a>Proceso de instalación de equipo desconocido  
 Cuando un equipo se inicia por primera vez desde PXE o desde medios, Configuration Manager comprueba si existe un registro de ese equipo en la base de datos de Configuration Manager. Si existe, Configuration Manager comprueba si hay alguna secuencia de tareas implementada en el registro. Si no existe ningún registro, Configuration Manager comprueba si hay alguna secuencia de tareas implementada en un objeto de equipo desconocido. En ambos casos, Configuration Manager lleva a cabo una de las acciones siguientes:  

- Si hay una secuencia de tareas disponible, Configuration Manager solicita al usuario que ejecute la secuencia de tareas.  

- Si hay una secuencia de tareas requerida, Configuration Manager ejecuta la secuencia de tareas automáticamente.  

- Si no hay una secuencia de tareas implementada para el registro, Configuration Manager genera un error para indicar que no hay ninguna secuencia de tareas implementada para el equipo de destino.  

  Además, cuando se inicia un equipo desconocido, Configuration Manager lo reconoce como un equipo no aprovisionado en lugar de hacerlo como un equipo desconocido. Esto significa que el equipo ahora puede recibir las secuencias de tareas que se implementaron en el objeto de equipo desconocido. A continuación, la secuencia de tareas implementada instala una imagen de sistema operativo que debe incluir el cliente de Configuration Manager.  

  Después de que se instala el cliente de Configuration Manager, se crea un registro para el equipo y el equipo pasa a figurar en la recopilación de Configuration Manager correspondiente. Si un equipo no logra instalar la imagen de sistema operativo o el cliente de Configuration Manager, se crea un registro "Desconocido" para el equipo y el equipo se muestra en la recopilación **Todos los sistemas**.  

> [!NOTE]  
>  Durante la instalación de la imagen de sistema operativo, la secuencia de tareas puede recuperar variables de recopilación pero no variables de equipo de este equipo.  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> Habilitación de la compatibilidad con equipos desconocidos  
 Use la información siguiente para habilitar la compatibilidad con equipos desconocidos al implementar un sistema operativo mediante PXE, medios de arranque y medios preconfigurados.  

-   **PXE**  

     Active la casilla **Habilitar la compatibilidad con equipos desconocidos** en la pestaña **PXE** para un punto de distribución habilitado para PXE. Para obtener más información, consulte [Configuración de puntos de distribución para aceptar solicitudes PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Medio de arranque**  

     Seleccione la casilla **Habilitar compatibilidad con equipos desconocidos** en la página **Seguridad** del Asistente para crear medio de secuencia de tareas. Para más información, consulte [Configuración de puntos de distribución para aceptar solicitudes PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) y [Usar PXE para implementar Windows a través de la red con Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Medio preconfigurado**  

     Seleccione la casilla **Habilitar compatibilidad con equipos desconocidos** en la página **Seguridad** del Asistente para crear medio de secuencia de tareas. Para más información, consulte [Crear medios preconfigurados con Configuration Manager](../deploy-use/create-prestaged-media.md).  
