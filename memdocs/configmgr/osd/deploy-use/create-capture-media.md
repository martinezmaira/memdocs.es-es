---
title: Crear medios de captura
titleSuffix: Configuration Manager
description: Use medios de captura en Configuration Manager para capturar una imagen del sistema operativo de un equipo de referencia.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f8f8d6512e0ddd9881005c5916eeb804aac59e2d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698017"
---
# <a name="create-capture-media"></a>Crear medios de captura

*Se aplica a: Configuration Manager (rama actual)*

Los medios de captura de Configuration Manager permiten capturar una imagen del sistema operativo de un equipo de referencia. Los medios de captura contienen la imagen de arranque que inicia el equipo de referencia y la secuencia de tareas que captura la imagen del sistema operativo. Use medios de captura en el escenario para [crear una secuencia de tareas para capturar un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md).  


## <a name="prerequisites"></a>Requisitos previos

Antes de crear medios de captura con el Asistente para crear medio de secuencia de tareas, asegúrese de que se cumplen las condiciones siguientes:

### <a name="boot-image"></a>Imagen de arranque

Tenga en cuenta los siguientes puntos sobre la imagen de arranque que usará en la secuencia de tareas para implementar el sistema operativo:

- La arquitectura de la imagen de arranque debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.
- Asegúrese de que la imagen de arranque contenga los controladores de almacenamiento y red necesarios para aprovisionar el equipo de destino.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo el contenido asociado con la secuencia de tareas

Distribuya todo el contenido requerido por la secuencia de tareas a un punto de distribución como mínimo. Este contenido incluye la imagen de arranque, la imagen de sistema operativo y otros archivos asociados. El asistente recopila el contenido del punto de distribución al crear los medios de captura.

Su cuenta de usuario necesita al menos acceso de **Lectura** a la biblioteca de contenido en ese punto de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar la unidad USB extraíble

Si usa una unidad USB extraíble, conéctela al equipo donde se ejecuta el Asistente para crear medio de secuencia de tareas. Windows debe identificar la unidad USB como un dispositivo extraíble. El asistente escribe directamente en la unidad extraíble cuando crea los medios.

### <a name="create-an-output-folder"></a>Crear una carpeta de salida

Antes de ejecutar el Asistente para crear medio de secuencia de tareas para crear medios para un conjunto de CD o DVD, cree una carpeta para los archivos de salida que se crean. Los medios que se crean para un conjunto de CD o DVD se escriben como un archivo .ISO directamente en la carpeta.


## <a name="process"></a>Proceso

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione el nodo **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Crear medio de secuencia de tareas**. Esta acción inicia el Asistente para crear medio de secuencia de tareas.  

3. En la página **Seleccionar tipo de medio**, seleccione **Medio de captura**.  

4. En la página **Tipo de medios**, especifique si el medio es una **unidad USB extraíble** o un **conjunto de CD/DVD**. Luego, configure las siguientes opciones:  

    > [!IMPORTANT]  
    > Los medios usan un sistema de archivos FAT32. No puede crear medios en una unidad USB cuyo contenido incluya un archivo de más de 4 GB de tamaño.  

    - Si selecciona **Unidad USB extraíble**, especifique dónde quiere almacenar el contenido.  

        - **Formatear la unidad USB extraíble (FAT32) y hacerla de arranque** : de forma predeterminada, permita que Configuration Manager prepare la unidad USB. Muchos de los nuevos dispositivos UEFI requieren una partición FAT32 de arranque. Sin embargo, este formato también limita el tamaño de los archivos y la capacidad total de la unidad. Si ya ha formateado y configurado la unidad extraíble, deshabilite esta opción.

    - Si selecciona **Conjunto de CD/DVD**, especifique la capacidad del medio (**Tamaño de medio**) y el nombre y la ruta de acceso del archivo de salida (**Archivo multimedia**). El asistente escribe los archivos de salida en esta ubicación. Por ejemplo: `\\servername\folder\outputfile.iso`  

        Si la capacidad del medio es demasiado pequeña para almacenar todo el contenido, crea varios archivos. A continuación, deberá almacenar el contenido en varios CD o DVD. Si se requieren varios archivos multimedia, Configuration Manager agrega un número de secuencia al nombre de cada archivo de salida que crea.  

        > [!IMPORTANT]  
        > Si selecciona una imagen .iso existente, el Asistente para crear medio de secuencia de tareas elimina la imagen de la unidad o el recurso compartido cuando pasa a la siguiente página del asistente. Se elimina la imagen existente incluso si, a continuación, se cancela al asistente.  

    - **Carpeta de almacenamiento provisional**:<!--1359388-->: el proceso de creación de medios puede requerir una gran cantidad de espacio en disco temporal. De forma predeterminada, esta ubicación es similar a la siguiente ruta de acceso: `%UserProfile%\AppData\Local\Temp`. A partir de la versión 1902, para ofrecer mayor flexibilidad con respecto al almacenamiento de estos archivos temporales, cambie este valor a otra unidad y ruta de acceso.  

    - **Etiqueta de medio**:<!--1359388-->: a partir de la versión 1902, agregue una etiqueta al medio de secuencia de tareas. Esta etiqueta ayuda a identificar mejor el medio después de crearlo. El valor predeterminado es `Configuration Manager`. Este campo de texto aparece en las siguientes ubicaciones:  

        - Si monta un archivo ISO, Windows muestra esta etiqueta como el nombre de la unidad montada  

        - Si aplica formato a una unidad USB, usa los primeros 11 caracteres de la etiqueta como nombre  

        - Configuration Manager escribe un archivo de texto denominado `MediaLabel.txt` en la raíz del medio. De forma predeterminada, el archivo incluye una sola línea de texto: `label=Configuration Manager`. Si personaliza la etiqueta del medio, esta línea usa la etiqueta personalizada en lugar del valor predeterminado.  

    - **Incluir archivo autorun.inf en el medio**:<!-- 4090666 -->: a partir de la versión 1906, Configuration Manager no agrega un archivo autorun.inf de forma predeterminada. Normalmente, los productos antimalware bloquean este archivo. Para obtener más información sobre la característica de ejecución automática de Windows, vea [Creating an AutoRun-enabled CD-ROM Application](/windows/desktop/shell/autoplay) (Creación de una aplicación de CD-ROM con ejecución automática habilitada). Si todavía lo necesita en su escenario, seleccione esta opción para incluir el archivo.  

5. En la página **Imagen de arranque**, especifique las opciones siguientes:  

    > [!IMPORTANT]  
    > La arquitectura de la imagen de arranque que se distribuye debe ser adecuada para la arquitectura del equipo de destino. Por ejemplo, un equipo de destino x64 puede arrancar y ejecutar una imagen de arranque x86 o x64. Sin embargo, un equipo de destino x86 solo puede arrancar y ejecutar una imagen de arranque x86.  

    - **Imagen de arranque**: seleccione la imagen de arranque para iniciar el equipo de destino.  

    - **Punto de distribución**: seleccione el punto de distribución que tiene la imagen de arranque. El asistente recupera la imagen de arranque desde el punto de distribución y la escribe en el medio.  

        > [!NOTE]  
        > Su cuenta de usuario necesita al menos permisos de **Lectura** para la biblioteca de contenido en el punto de distribución.  

6. Complete el asistente.  


## <a name="next-steps"></a>Pasos siguientes

[Creación de una secuencia de tareas para capturar un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)