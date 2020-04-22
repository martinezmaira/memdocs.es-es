---
title: Crear medios de secuencia de tareas
titleSuffix: Configuration Manager
description: Cree medios de secuencia de tareas para implementar un sistema operativo en un equipo de destino en su entorno de Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690603"
---
# <a name="create-task-sequence-media"></a>Crear medios de secuencia de tareas

*Se aplica a: Configuration Manager (rama actual)*

Puede usar medios para capturar una imagen del sistema operativo de un equipo de referencia o para implementar un sistema operativo en un equipo de destino en su entorno de Configuration Manager. La creación de medios puede realizarse en un CD, un DVD o una unidad flash USB.  

Los medios se usan mayoritariamente para implementar sistemas operativos en equipos de destino que no tienen una conexión de red o que tienen una conexión de bajo ancho de banda en el sitio de Configuration Manager. Sin embargo, también se pueden usar medios para iniciar una implementación del sistema operativo fuera de un sistema operativo Windows existente. Este método es útil cuando aún no hay un sistema operativo, el sistema operativo no funciona o quiere volver a particionar el disco duro.  

Los medios de implementación incluyen medios de arranque, medios independientes y medios preconfigurados. El contenido de los medios varía según el tipo de medio que se utilice. Por ejemplo, los medios independientes contienen la secuencia de tareas que implementa el sistema operativo. Otros tipos de medios recuperan secuencias de tareas del punto de administración.  

> [!IMPORTANT]  
> Para crear medios de secuencia de tareas, debe ser administrador en el equipo donde se ejecuta la consola de Configuration Manager. Si no es administrador, se le pedirán las credenciales de administrador al iniciar el Asistente para crear medio de secuencia de tareas.  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a> Medios de captura

Los medios de captura le permiten capturar una imagen del sistema operativo de un equipo de referencia. Los medios de captura contienen la imagen de arranque que inicia el equipo de referencia y la secuencia de tareas que captura la imagen del sistema operativo.

Para más información sobre cómo crear medios de captura, consulte [Crear medios de captura](create-capture-media.md).  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a> Medio de arranque

Los medios de arranque contienen los siguientes componentes:

- La imagen de arranque
- [Comandos de preinicio](../understand/prestart-commands-for-task-sequence-media.md) opcionales y sus archivos necesarios
- Binarios de Configuration Manager

Cuando se inicia el equipo de destino, se conecta a la red y se recupera la secuencia de tareas, la imagen del sistema operativo y cualquier otro tipo de contenido necesario de la red. Dado que la secuencia de tareas no está en el medio, puede cambiar la secuencia de tareas o el contenido sin tener que volver a crear el medio.  

> [!IMPORTANT]  
> Los paquetes en el medio de arranque no están cifrados. Adopte las medidas de seguridad adecuadas, como agregar una contraseña a los medios, para asegurarse de que el contenido del paquete está protegido contra usuarios no autorizados.  

Para más información sobre cómo crear un medio de arranque, consulte [Crear medios de arranque](create-bootable-media.md).  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a> Medios preconfigurado

Los medios preconfigurados le permiten aplicar medios de arranque y una imagen del sistema operativo a un disco duro antes del proceso de aprovisionamiento. Los medios preconfigurados son un archivo de imagen de Windows (WIM). Se pueden instalar en un equipo sin sistema operativo por el fabricante o en su centro de almacenamiento provisional que no está conectado al entorno de producción de Configuration Manager.  

Los medios preconfigurados contienen la imagen de arranque que se usa para iniciar el equipo de destino y la imagen del sistema operativo que se aplica al equipo de destino. También puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiere incluir como parte de los medios preconfigurados. La secuencia de tareas que implementa el sistema operativo no se incluye en los medios. Al implementar una secuencia de tareas que usa medios preconfigurados, el cliente comprueba primero que el contenido de la caché de secuencia de tareas local sea válido. Si el contenido no se encuentra o se ha revisado, el cliente lo descarga desde un punto de distribución o un homólogo.  

Los medios preconfigurados se aplican a la unidad de disco duro de un nuevo equipo antes de enviar el equipo al usuario final. Cuando el equipo se inicia por primera vez después de haber aplicado los medios preconfigurados, el equipo se inicia en Windows PE. Se conecta a un punto de administración para encontrar la secuencia de tareas que completa el proceso de implementación del sistema operativo.  

> [!IMPORTANT]  
> Los paquetes en el medio preconfigurado no están cifrados. Adopte las medidas de seguridad adecuadas, como agregar una contraseña a los medios, para asegurarse de que el contenido del paquete está protegido contra usuarios no autorizados.  

Para más información sobre cómo crear medios preconfigurados, consulte [Crear medios preconfigurados](create-prestaged-media.md).  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a> Medios independientes

Los medios independientes contienen todo lo necesario para implementar el sistema operativo. Este contenido incluye la secuencia de tareas y demás elementos necesarios. Dado que todo lo necesario para implementar el sistema operativo se almacena en el medio independiente, el espacio en disco necesario en él es mayor que para otros tipos de medios.  

Para obtener información sobre cómo crear medios independientes, consulte [Crear medios independientes](create-stand-alone-media.md).  


## <a name="considerations-when-using-https"></a>Consideraciones al usar HTTPS

Cuando configure sus puntos de administración y puntos de distribución para usar HTTPS, cree medios de arranque y medios preconfigurados en un sitio primario, y no en el sitio de administración central. Además, tenga en cuenta el siguiente aspecto como ayuda para determinar si se configura el medio como dinámico o basado en el sitio:  

- Para configurar el medio como dinámico, todos los sitios primarios deben tener la entidad de certificación (CA) raíz del sitio desde el que se creó el medio. Puede importar la entidad de certificación raíz en todos los sitios primarios en la jerarquía.  

- Si los sitios primarios de su jerarquía de Configuration Manager usan otras entidades de certificación raíz, debe usar medios basados en sitio en cada sitio.  
