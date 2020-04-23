---
title: Administrar paquetes de actualización del sistema operativo
titleSuffix: Configuration Manager
description: Aprenda a administrar paquetes de actualización del sistema operativo en Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc50fc60601b63bca7b4a4b01ba3fb4a39fd8b91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708873"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Administrar paquetes de actualización del sistema operativo con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Un paquete de actualización del sistema operativo en Configuration Manager contiene los archivos de origen de instalación de Windows necesarios para actualizar un sistema operativo existente en un equipo. En este artículo se describe cómo agregar, distribuir y reparar un paquete de actualización de sistema operativo.

> [!NOTE]
> Los paquetes de actualización del sistema operativo también pueden utilizarse para las nuevas instalaciones de Windows. Sin embargo, dependen de que los controladores sean compatibles con este método. Al realizar nuevas instalaciones de Windows desde un paquete de actualización del sistema operativo, los controladores se instalan en Windows PE en lugar de simplemente inyectarse en Windows PE. Algunos controladores no son compatibles con la instalación en Windows PE. Si los controladores no son compatibles con la instalación en Windows PE, en su lugar, use una [imagen del sistema operativo](manage-operating-system-images.md), como **install.wim**.

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a> Agregar un paquete de actualización del sistema operativo  

Para poder usar un paquete de actualización del sistema operativo, primero debe agregarlo a su sitio de Configuration Manager.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Paquetes de actualización del sistema operativo**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Agregar paquete de actualización de sistema operativo**. Esta acción inicia el asistente para agregar una actualización del sistema operativo.  

3. En la página **Origen de datos**, especifique la siguiente configuración:

    - La **Ruta** de red a la instalación de los archivos de origen del paquete de actualización del sistema operativo. Por ejemplo, `\\server\share\path`.  

        > [!NOTE]  
        >  Los archivos de origen de instalación contienen setup.exe y otros archivos y carpetas para instalar el sistema operativo.  

        > [!IMPORTANT]  
        >  Limite el acceso a los archivos de origen de instalación para evitar la manipulación no deseada.  

    - **Extraiga un índice de imágenes específico del archivo install.wim del paquete de actualización seleccionado** y, a continuación, seleccione un índice de imágenes en la lista.<!--4931110--> A partir de la versión 1910, esta opción importa automáticamente un solo índice, en lugar de todos los índices de imágenes del archivo. Con esta opción se garantiza un archivo de imagen más pequeño y un mantenimiento sin conexión más rápido. Además, permite que el proceso [optimice el mantenimiento de las imágenes](#bkmk_resetbase), lo que tiene como resultado un archivo de imagen más pequeño después de aplicar las actualizaciones de software.  

        > [!IMPORTANT]  
        > Configuration Manager sobrescribe el archivo install.wim existente en el paquete de actualización del sistema operativo. Extrae el índice de imágenes a una ubicación temporal y, luego, lo mueve al directorio de origen original. Antes de importar un paquete de actualización de SO y habilitar esta opción, asegúrese de crear una copia de seguridad de los archivos de origen originales.

    - Si quiere almacenar previamente en caché contenido en un cliente, especifique la **Arquitectura** y el **Lenguaje** de la imagen. Para obtener más información, vea [Configuración del contenido de la caché previa](../deploy-use/configure-precache-content.md).  

4. En la página **General**, especifique la siguiente información. Esta información es útil para identificar el paquete de actualización del sistema operativo cuando se tiene más de uno.  

    - **Nombre**: nombre único del paquete de actualización del sistema operativo.  

    - **Versión**: identificador de versión opcional. Esta propiedad no tiene que ser la versión del sistema operativo del paquete de actualización. A menudo es la versión de la organización para el paquete.  

    - **Comentario**: breve descripción opcional.  

5. Complete el asistente.  

A continuación, distribuya el paquete de actualización del sistema operativo a puntos de distribución.  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a> Distribución de contenido a un punto de distribución  

Distribuya los paquetes de actualización del sistema operativo a puntos de distribución del mismo modo que otro tipo de contenido. Antes de implementar la secuencia de tareas, distribuya el paquete de actualización del sistema operativo al menos a un punto de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>Pasos siguientes

[Creación de una secuencia de tareas para actualizar un sistema operativo](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
