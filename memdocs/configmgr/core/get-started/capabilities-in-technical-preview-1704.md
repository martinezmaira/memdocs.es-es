---
title: Funcionalidades de Technical Preview 1704
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1704.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705273"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Funciones de Technical Preview 1704 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1704 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    


**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Configuración de aplicaciones de Android con directivas de configuración de aplicaciones
Puede usar directivas de configuración de aplicaciones en Configuration Manager para distribuir valores de configuración que podrían ser necesarios cuando un usuario ejecuta una aplicación en dispositivos de Android for Work. Las directivas de configuración de aplicaciones Android solo están disponibles en los dispositivos que ejecutan Android for Work y se aplican a las aplicaciones aprobadas en la tienda Play for Work.

### <a name="try-it-out"></a>Haga la prueba                 

En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Administración de aplicaciones** > **Directivas de configuración de aplicaciones** y elija **Crear directiva de configuración de aplicaciones**. En la página **General** del asistente, ahora puede **seleccionar un tipo de directiva de configuración**. Especifique la plataforma de destino de la directiva de configuración de aplicación: **Directiva de configuración para aplicaciones de Android for Work**. A continuación, puede **especificar pares de nombre y valor** o **buscar un archivo JSON de la lista de propiedades**. La nueva directiva de configuración de aplicaciones se muestra en el área de trabajo **Biblioteca de software**, en el nodo **Directivas de configuración de aplicaciones**. Para asociar una directiva de configuración de aplicaciones a la implementación de una aplicación de Android for Work, implemente la aplicación del modo habitual con el procedimiento indicado en el tema [Implementar aplicaciones](../../apps/deploy-use/deploy-applications.md).

## <a name="hardware-inventory-collects-secure-boot-information"></a>El inventario de hardware recopila información de arranque seguro
Ahora, el inventario de hardware recopila información sobre si el arranque seguro está habilitado en los clientes. Esta información se almacena en la clase **SMS_Firmware** (introducida en la versión 1702) y se habilita en el inventario de hardware de forma predeterminada. Para obtener más información sobre el inventario de hardware, vea [Cómo configurar el inventario de hardware](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adición de secuencias de tareas secundarias a una secuencia de tareas
En esta versión, puede agregar un nuevo paso de secuencia de tareas que ejecuta otra secuencia de tareas, y que crea una relación de elemento primario/secundario entre las secuencias de tareas. De este modo, puede crear más secuencias de tareas modulares que puede volver a utilizar.  

Tenga en cuenta lo siguiente al agregar una secuencia de tareas secundaria a una secuencia de tareas:

- Las secuencias de tareas primaria y secundaria se combinan eficazmente en una única directiva que ejecuta el cliente.
- No es posible agregar una secuencia de tareas secundaria que sea un elemento primario de otra secuencia de tareas.
- El entorno es global. Por ejemplo, si una variable se establece por la secuencia de tareas primaria y, a continuación, se cambia por la secuencia de tareas secundaria, la variable permanece cambiada en adelante. De forma similar, si la secuencia de tareas secundaria crea una nueva variable, la variable está disponible para los pasos restantes de la secuencia de tareas primaria.
- Los mensajes de estado se envían de manera normal para una operación de secuencia de tareas única.
- Las secuencias de tareas escriben entradas en el archivo smsts.log, con nuevas entradas de registro que dejan claro cuando se inicia una secuencia de tareas secundaria.
- En Technical Preview para Configuration Manager, versión 1704, si las secuencias de tareas secundarias hacen referencia a cualquier paquete y ejecuta la secuencia de tareas primaria desde el Centro de software, el cliente no encontrará el contenido del paquete cuando se ejecuta la secuencia de tareas secundaria. En este escenario, debe ejecutar la secuencia de tareas desde los medios (medio de arranque, PXE, etc.).  

    Si la secuencia de tareas secundaria usa pasos como **Ejecutar línea de comandos** (sin ninguna referencia de paquete), **Formato**, **BitLocker**, entre otros, la secuencia de tareas se ejecutará correctamente desde el Centro de software.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Para agregar una secuencia de tareas secundaria a una secuencia de tareas
1. En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y haga clic en **Ejecutar secuencia de tareas**.
2. Haga clic en **Examinar** para seleccionar la secuencia de tareas secundaria.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Nueva carga de imágenes de arranque con la versión actual de Windows PE
Al ejecutar **Actualizar puntos de distribución** en una imagen de arranque seleccionada, ahora puede volver a cargar la versión más reciente de Windows PE (desde el directorio de instalación de Windows ADK) en la imagen de arranque. La página **General** del asistente proporciona información acerca de la versión de Windows ADK instalada en el servidor de sitio, la versión de Windows ADK desde la que se usó Windows PE en la imagen de arranque y la versión de cliente de Configuration Manager. Puede utilizar esta información para ayudarle a decidir si desea volver a cargar la imagen de arranque. Además, se ha agregado una nueva columna (**Versión del cliente**) al visualizar imágenes de arranque en el nodo **Imágenes de arranque** para que pueda conocer la versión del cliente de Configuration Manager que utiliza cada imagen de arranque.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Para volver a cargar una imagen de arranque con la versión actual de Windows PE

1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Sistemas operativos** > **Imágenes de arranque**.
2. Seleccione una imagen de arranque y haga clic en **Actualizar puntos de distribución**.
3. En la página **General** del asistente, seleccione **Reload boot image using the current version of Windows PE from the installed Windows ADK** (Volver a cargar la imagen de arranque con la versión actual de Windows PE desde el Windows ADK instalado).

## <a name="improvements-to-operating-system-deployment"></a>Mejoras en la implementación de sistema operativo
Hemos realizado las siguientes mejoras en la implementación del sistema operativo, muchas de las cuales son el resultado de los comentarios de los usuarios.

- [Nueva columna **Versión de SO** para las imágenes de sistema operativo](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): hemos agregado una nueva columna denominada **Versión de SO** para mostrar la versión del sistema operativo de la imagen al ver la información en los nodos **Imágenes de sistema operativo** y **Paquetes de actualización del sistema operativo**. Solo se muestra la versión del primer índice en el .WIM. Vaya a la pestaña **Detalles** de la imagen para revisar las versiones de sistema operativo para otros índices.

- [Registro más eficaz en Smsts.log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): a partir de esta versión, se dejan de escribir entradas en el archivo smsts.log para obtener información de CCM_CIVersionInfo.PolicyID. Antes de esta versión, podría haber muchas entradas con esta información, lo que dificultaba la búsqueda de la información más pertinente en el archivo de registro.
