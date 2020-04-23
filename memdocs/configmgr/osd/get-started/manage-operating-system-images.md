---
title: Administrar imágenes del sistema operativo
titleSuffix: Configuration Manager
description: Obtenga información sobre los métodos para administrar imágenes de sistema operativo almacenadas en archivos de imagen (WIM) de Windows.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 190a203494cecfd28c198197f3a582adff745265
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708893"
---
# <a name="manage-os-images-with-configuration-manager"></a>Administración de imágenes del sistema operativo con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las imágenes de sistema operativo en Configuration Manager se almacenan en el formato de archivo de la imagen de Windows (WIM). Estas imágenes son una recopilación comprimida de archivos y carpetas de referencia utilizados para instalar y configurar un nuevo sistema operativo en un equipo. Una imagen de sistema operativo puede ser necesaria en muchos escenarios de implementación de sistemas operativos.


## <a name="os-image-types"></a>Tipos de imagen de sistema operativo

Puede usar la [imagen de sistema operativo predeterminada](#default-image) o crearla desde un [equipo de referencia](#bkmk_capture) que configure. Al compilar el equipo de referencia, se agregan archivos del sistema operativo, controladores, archivos de soporte técnico, actualizaciones de software, herramientas y aplicaciones en el sistema operativo. Después, se captura para crear el archivo de imagen.

### <a name="default-image"></a>Imagen predeterminada

Los archivos de instalación de Windows incluyen la imagen de sistema operativo de forma predeterminada. Se trata de una imagen de sistema operativo básica que contiene un conjunto estándar de controladores. Para usar la imagen de sistema operativo predeterminada, deberá seguir los pasos de secuencia de tareas para instalar aplicaciones y realizar otras configuraciones después de que el sistema operativo se instale en un dispositivo. Busque la imagen de sistema operativo predeterminada en los archivos de origen de Windows: `\Sources\install.wim`.  

#### <a name="default-image-advantages"></a>Ventajas de la imagen predeterminada

- El tamaño de la imagen es menor que una imagen capturada.  

- La instalación de aplicaciones y configuraciones con pasos de secuencia de tareas es más dinámica. Por ejemplo, permite cambiar las configuraciones y aplicaciones que se instalan en la secuencia de tareas sin tener que restablecer la imagen inicial del dispositivo.  

#### <a name="default-image-disadvantages"></a>Desventajas de la imagen predeterminada

- La instalación del sistema operativo puede tardar más tiempo. La instalación de la aplicación y otras configuraciones se producen una vez finalizada la instalación del sistema operativo.  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a> Imagen capturada desde un equipo de referencia

Para crear una imagen de SO personalizada, cree un equipo de referencia con el sistema operativo deseado. Después, instale las aplicaciones y configure las opciones. Capture la imagen del sistema operativo desde el equipo de referencia para crear el archivo WIM. Compile el equipo de referencia de forma manual o use una secuencia de tareas para automatizar algunos o todos los pasos de generación. Para obtener más información, vea [Personalizar imágenes de sistema operativo](customize-operating-system-images.md).  

#### <a name="captured-image-advantages"></a>Ventajas de capturar una imagen

- La instalación puede resultar más rápida que el uso de la imagen predeterminada. Por ejemplo, la captura de la imagen del sistema operativo permite que las aplicaciones estén preinstaladas. Después no tendrá que instalar esas mismas aplicaciones siguiendo los pasos de la secuencia de tareas.  

#### <a name="captured-image-disadvantages"></a>Desventajas de capturar una imagen

- El tamaño de la imagen es potencialmente mayor que la imagen predeterminada.  

- Debe crear una imagen cuando se deban efectuar actualizaciones de aplicaciones y herramientas.  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a> Agregar una imagen de sistema operativo  

Para poder usar una imagen de sistema operativo, primero debe agregarla a su sitio de Configuration Manager.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Imágenes de sistema operativo**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Agregar imagen de sistema operativo**. Esta acción inicia el asistente para agregar una imagen de sistema operativo.  

3. En la página **Origen de datos**, especifique la información siguiente:

    - **Ruta de acceso** de red al archivo de imagen de sistema operativo. Por ejemplo, `\\server\share\path\image.wim`.

    - Seleccione la opción **Extraer un índice de imágenes específico del archivo WIM especificado** y, después, elija un índice de imagen de la lista.<!--3719699--> A partir de la versión 1902, esta opción importa automáticamente un solo índice, en lugar de todos los índices de imágenes del archivo. Con esta opción se garantiza un archivo de imagen más pequeño y un mantenimiento sin conexión más rápido. Además, permite que el proceso [optimice el mantenimiento de las imágenes](#bkmk_resetbase), lo que tiene como resultado un archivo de imagen más pequeño después de aplicar las actualizaciones de software.  

        > [!Note]  
        > Configuration Manager no modifica el archivo de imagen de origen. Crea un nuevo archivo de imagen en el mismo directorio de origen.
        >
        > Puede producirse un error en este proceso de extracción en el caso de los archivos de imagen muy grandes, por ejemplo, de más de 60 GB. El error de DISM es `Not enough storage is available to process this command.` La línea de comandos que usa Configuration Manager está en smsprov.log y dism.log. Ejecute manualmente el mismo comando y, luego, importe la imagen.<!-- SCCMDocs-pr issue 3502 -->  

    - A partir de la versión 1906, si quiere almacenar previamente en caché contenido en un cliente, especifique la **Arquitectura** y el **Lenguaje** de la imagen. Para obtener más información, vea [Configuración del contenido de la caché previa](../deploy-use/configure-precache-content.md).<!--4224642-->  

4. En la página **General**, especifique la siguiente información. Esta información es útil para identificar la imagen de sistema operativo cuando se tiene más de una.  

    - **Nombre**: nombre único de la imagen. De forma predeterminada, el nombre se toma del nombre del archivo WIM.  

    - **Versión**: identificador de versión opcional. Esta propiedad no tiene que ser la versión del sistema operativo de la imagen. A menudo es la versión de la organización para el paquete.  

    - **Comentario**: breve descripción opcional.  

5. Complete el asistente.  

Para conocer el cmdlet de PowerShell equivalente de este asistente para la consola, vea [New-CMOperatingSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps).

Después, distribuya la imagen de sistema operativo por los puntos de distribución.  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a> Distribución de contenido por puntos de distribución  

Distribuya las imágenes de sistema operativo por puntos de distribución del mismo modo que otro tipo de contenido. Antes de implementar la secuencia de tareas, distribuya la imagen de sistema operativo al menos a un punto de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a> Preparación de la imagen de sistema operativo para implementaciones de multidifusión  

Use las implementaciones de multidifusión para permitir que más de un equipo descargue una imagen de sistema operativo simultáneamente. El punto de distribución envía la imagen mediante multidifusión a los clientes en vez de que cada cliente tenga que descargar una copia de la imagen desde el punto de distribución a través de una conexión independiente. Si elige el método de implementación de sistema operativo para [usar multidifusión para implementar Windows a través de la red](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), configure la imagen de sistema operativo para que admita la multidifusión. Después distribuya la imagen a un punto de distribución habilitado para multidifusión.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Imágenes de sistema operativo**.  

2. Seleccione la imagen de sistema operativo que se va a distribuir en un punto de distribución habilitado para multidifusión.  

3. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.  

4. Cambie a la pestaña **Configuración de distribución** y configure las siguientes opciones:  

    - **Permitir que este paquete se transfiera mediante multidifusión (solo WinPE)** : seleccione esta opción para que Configuration Manager implemente de forma simultánea imágenes de SO mediante multidifusión.  

    - **Cifrar paquetes de multidifusión**: especifique si el sitio cifra la imagen antes de enviarse al punto de distribución. Use esta opción si la imagen contiene información confidencial. Si la imagen no está cifrada, su contenido está visible en texto no cifrado en la red. En este caso, un usuario no autorizado podría interceptar y ver el contenido de la imagen.  

    - **Transferir este paquete solo mediante multidifusión**: especifique si desea que el punto de distribución implemente la imagen solamente durante una sesión de multidifusión.  

         Si selecciona **Transferir este paquete solo mediante multidifusión**, también deberá especificar la opción de implementación de la secuencia de tareas para **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas**. Para obtener más información, vea [Deploy a task sequence](../deploy-use/deploy-a-task-sequence.md).  

5. Haga clic en **Aceptar** para guardar la configuración y cierre las propiedades de la imagen.  
