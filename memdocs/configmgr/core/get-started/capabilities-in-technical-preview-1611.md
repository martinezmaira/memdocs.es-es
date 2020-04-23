---
title: Funcionalidades de Technical Preview 1611
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1611.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e1348e9d230a5525a91e7e7dceea4da6d1311b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705473"
---
# <a name="capabilities-in-technical-preview-1611-for-configuration-manager"></a>Funciones de Technical Preview 1611 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*



En este artículo se presentan las características disponibles en la versión 1611 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    

**Problemas conocidos de esta Technical Preview:**   
- ***Estado de los requisitos previos***: cuando instala la versión 1611, el estado general de los requisitos previos puede aparecer como superado con advertencias, pero no aparecen qué requisitos previos han provocado las advertencias. Esto puede deberse a los dos siguientes requisitos previos:
  - Opciones Memoria para creación de índices de SQL
  - Comprobaciones de la versión de SQL Server admitida  

  Como estas son solo advertencias, pueden omitirse.

- ***PowerShell***: cuando se conecta a Windows PowerShell desde la consola de Configuration Manager, puede recibir el siguiente error: **Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml no está firmado digitalmente**.  

   Puede resolver este problema reemplazando determinados archivos por las versiones firmadas de la versión 1610. Copie todos los archivos con las siguientes extensiones de la carpeta **&lt;directorio de instalación>\AdminConsole\bin\\** de la instalación de la versión 1610: **.psd1**, **.ps1xml** y **.psm1**. Pegue estos archivos en la carpeta **&lt;directorio de instalación>\AdminConsole\bin\\** de la instalación de la versión 1611 de Technical Preview, sobrescribiendo la versión 1611 de los archivos.


**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Almacenar en la caché previa contenido para las implementaciones y las secuencias de tareas disponibles
En esta Technical Preview, para las secuencias de tareas e implementaciones disponibles, puede decidir usar la característica de caché previa para que los clientes solo descarguen el contenido relevante antes de que un usuario instale el contenido.

Por ejemplo, supongamos que quiere implementar una secuencia de tareas de actualización de Windows 10, solo quiere una única secuencia de tareas para todos los usuarios y tiene varias arquitecturas o idiomas. En la rama actual, si crea una implementación disponible y, después, el usuario hace clic en **Instalar** en el Centro de software, el contenido se descarga en ese momento. Esto agrega tiempo adicional antes de que la instalación esté lista para iniciarse. De manera alternativa, en la rama actual, si crea una implementación de secuencia de tareas disponible, todo el contenido al que se hace referencia en la secuencia de tareas se descarga. Esto incluye el paquete de actualizaciones del sistema operativo para todos los idiomas y arquitecturas. Si cada uno es aproximadamente de 3 GB de tamaño, el paquete de descarga puede ser bastante grande.

La característica de contenido de caché previa le proporciona la opción de que el cliente solo descargue el contenido aplicable tan pronto como reciba la implementación. Por lo tanto, cuando el usuario hace clic en **Instalar** en el Centro de software, el contenido está listo y la instalación se inicia rápidamente porque el contenido se encuentra en la unidad de disco duro local.

### <a name="to-configure-the-pre-cache-feature"></a>Para configurar la característica de caché previa

1. Cree paquetes de actualización de sistema operativo para los idiomas y las arquitecturas específicas. Especifique la arquitectura y el idioma en la pestaña **Origen de datos** del paquete. Para el idioma, use la conversión decimal (por ejemplo, 1033 es el decimal de inglés y 0x0409 es el hexadecimal equivalente). Para obtener más información, vea [Cree una secuencia de tareas para actualizar un sistema operativo en System Center Configuration Manager](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

    Los valores de idioma y arquitectura se usan para que coincidan con las condiciones de paso de secuencia de tareas que creará en el siguiente paso para determinar si el paquete de actualización de sistema operativo debe estar previamente en la caché.
2. Cree una secuencia de tareas con pasos condicionales para los diferentes idiomas y arquitecturas. Por ejemplo, para la versión en inglés puede crear un paso como el siguiente:

    ![propiedades de la caché previa](media/precacheproperties2.png)

    ![opciones de la caché previa](media/precacheoptions2.png)  

3. Implemente la secuencia de tareas. Para la característica de caché previa, configure lo siguiente:
    - En la pestaña **General**, seleccione **Descargar contenido previamente para esta secuencia de tareas**.
    - En la pestaña **Configuración de implementación**, configure la secuencia de tareas con la opción **Disponible** para **Propósito**. Si crea una implementación **Requerida**, la característica de caché previa no funcionará.
    - En la pestaña **Programación**, para la opción **Programar cuándo estará disponible esta implementación**, elija una hora futura que proporcione a los clientes tiempo suficiente para almacenar en caché previamente el contenido antes de que la implementación esté disponible para los usuarios. Por ejemplo, puede establecer que el tiempo disponible sea de 3 horas para permitir suficiente tiempo al contenido para que se almacene previamente en la caché.  
    - En la pestaña **Puntos de distribución**, configure los valores **Opciones de implementación**. Si el contenido no se ha almacenado previamente en la caché de un cliente antes de que un usuario inicie la instalación, se usa está configuración.


### <a name="user-experience"></a>Experiencia del usuario
- Cuando el cliente reciba la directiva de implementación, comenzará a almacenar previamente en caché el contenido. Esto incluye todo el contenido al que se hace referencia (cualquier otro tipo de paquete) y solo el paquete de actualizaciones del sistema operativo que coincide con el cliente en función de las condiciones que establezca en la secuencia de tareas.
- Cuando la implementación está disponible para los usuarios (configuración de la pestaña **Programación** de la implementación), se muestra una notificación para informar a los usuarios sobre la nueva implementación y esta se muestra en el Centro de software. El usuario puede ir al Centro de software y hacer clic en **Instalar** para iniciar la instalación.
- Si el contenido no se ha almacenado en la caché completamente, usará la configuración especificada en la pestaña **Opción de implementación** de la implementación. Recomendamos que haya suficiente tiempo entre el momento en que se crea la implementación y el momento en que la implementación está disponible para los usuarios, para permitir que los clientes tengan el tiempo suficiente para almacenar el contenido previamente en la caché.


## <a name="see-also"></a>Consulte también
[Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md)
