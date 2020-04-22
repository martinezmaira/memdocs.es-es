---
title: Actualización de las instalaciones de evaluación
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo actualizar una instalación de evaluación a una instalación completa de Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8a42b2538ff1baaceb6895d371081ac2a444c5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700463"
---
# <a name="upgrade-an-evaluation-installation-of-configuration-manager-to-a-full-installation"></a>Actualización de una instalación de evaluación de Configuration Manager a una instalación completa

*Se aplica a: Configuration Manager (rama actual)*

Si ha instalado Configuration Manager como versión de evaluación, transcurridos 180 días la consola de Configuration Manager pasará a ser de solo lectura hasta que active el producto en la página **Mantenimiento del sitio** del programa de instalación. Puede actualizar una instalación de evaluación a una instalación completa en cualquier momento (antes o después del período de 180 días).  

> [!NOTE]  
>  Al conectar una consola de Configuration Manager a una instalación de evaluación de Configuration Manager, en la barra de título de la consola se mostrará el número de días que quedan hasta que expire la instalación de evaluación. El número de días no se actualiza automáticamente (solo se actualiza cuando se realiza una nueva conexión a un sitio).  

 Puede actualizar los siguientes sitios que ejecutan una instalación de evaluación:  

-   Sitio de administración central  
-   Sitio primario  

Ya que los sitios secundarios no se tratan como instalaciones de evaluación, no es necesario modificar un sitio secundario si su sitio primario principal se actualiza a una instalación completa.  

Requisitos previos para actualizar una versión de evaluación a una versión con licencia:  

-   Necesita usar un producto válido durante la actualización.  
-   La cuenta necesita tener permisos de **administrador** en el equipo donde se instalará el sitio.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Para actualizar de una versión de evaluación de Configuration Manager a una versión con licencia  

1.  En el servidor de sitio, busque y ejecute **Setup.exe** (programa de instalación de Configuration Manager) en la carpeta de instalación de Configuration Manager ( **%path%\BIN\X64**). Debe ejecutar la copia del programa de instalación que se encuentra en el servidor de sitio, en la carpeta de Configuration Manager, porque las opciones de mantenimiento del sitio no están disponibles si ejecuta el programa de instalación desde medios de instalación.  
2.  En la página **Antes de empezar**, seleccione **Siguiente**.  
3.  En la página **Introducción**, seleccione **Realizar mantenimiento de sitio o restablecer este sitio** y, después, haga clic en **Siguiente**.  
4.  En la página **Mantenimiento del sitio**, seleccione **Actualizar la edición de evaluación a una edición con licencia**, escriba una clave del producto válida y, después, haga clic en **Siguiente**.  
5.  En la página **Términos de licencia del software de Microsoft**, lea y acepte los términos de licencia y, después, seleccione **Siguiente**.  
6.  En la página **Configuración**, seleccione **Cerrar** para completar el asistente.  

    > [!NOTE]  
    >  Es posible que en la barra de título de una consola de Configuration Manager que siga conectada al sitio actualizado se indique que el sitio aún es de una versión de evaluación, pero cambiará cuando vuelva a conectar la consola al sitio.  
