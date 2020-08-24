---
title: Crear medios de secuencia de tareas
titleSuffix: Configuration Manager
description: Cree medios de secuencia de tareas para implementar un sistema operativo en un equipo de destino en su entorno de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf7ce32ed9e126b5526c68b7da03cf44d9b5062d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125175"
---
# <a name="create-task-sequence-media"></a>Crear medios de secuencia de tareas

*Se aplica a: Configuration Manager (rama actual)*

Puede usar medios para capturar una imagen del sistema operativo de un equipo de referencia o para implementar un sistema operativo en un equipo de destino en su entorno de Configuration Manager. La creación de medios puede realizarse en un CD, un DVD o una unidad flash USB.

Los medios se usan principalmente para implementar un sistema operativo en equipos que no tienen una conexión de red o que tienen una conexión de ancho de banda bajo al sitio. Sin embargo, también se pueden usar medios para iniciar una implementación del sistema operativo fuera de un sistema operativo Windows existente. Este método es útil cuando aún no hay un sistema operativo, el sistema operativo no funciona o quiere volver a particionar el disco.

Los medios de implementación incluyen medios de arranque, medios independientes y medios preconfigurados. El contenido de los medios varía según el tipo de medio que se utilice. Por ejemplo, los medios independientes contienen la secuencia de tareas que implementa el sistema operativo. Otros tipos de medios recuperan secuencias de tareas del punto de administración.

> [!IMPORTANT]
> Para crear medios de secuencia de tareas, debe ser administrador en el equipo donde se ejecuta la consola de Configuration Manager. Si no es administrador, se le pedirán las credenciales de administrador al iniciar el Asistente para crear medio de secuencia de tareas.

## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a> Medios de captura

Los medios de captura le permiten capturar una imagen del sistema operativo de un equipo de referencia. Los medios de captura contienen la imagen de arranque que inicia el equipo de referencia y la secuencia de tareas que captura la imagen del sistema operativo.

## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a> Medio de arranque

Los medios de arranque contienen los siguientes componentes:

- La imagen de arranque
- [Comandos de preinicio](../understand/prestart-commands-for-task-sequence-media.md) opcionales y sus archivos necesarios
- Binarios de Configuration Manager

Cuando se inicia el equipo de destino, se conecta a la red y se recupera la secuencia de tareas, la imagen del sistema operativo y cualquier otro tipo de contenido necesario de la red. Dado que la secuencia de tareas no está en el medio, puede cambiar la secuencia de tareas o el contenido sin tener que volver a crear el medio.  

> [!IMPORTANT]  
> Los paquetes en el medio de arranque no están cifrados. Adopte las medidas de seguridad adecuadas, como agregar una contraseña a los medios, para asegurarse de que el contenido del paquete está protegido contra usuarios no autorizados.  

A partir de la versión 2006, el medio de arranque puede descargar contenido de la nube. El dispositivo sigue necesitando una conexión de intranet al punto de administración. El contenido se puede obtener de un punto de distribución de nube o de una instancia de Cloud Management Gateway (CMG) habilitados para contenido.<!--6209223--> Para más información, consulte [Compatibilidad con el contenido basado en la nube](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a> Medios preconfigurado

Los medios preconfigurados le permiten aplicar medios de arranque y una imagen del sistema operativo a un disco duro antes del proceso de aprovisionamiento. Los medios preconfigurados son un archivo de imagen de Windows (WIM). El fabricante puede instalarlo en el equipo sin sistema operativo durante su proceso de compilación. También, puede utilizarlo en un centro de ensayo que no está conectado al entorno de Configuration Manager de producción.

Los medios preconfigurados contienen la imagen de arranque que se usa para iniciar el equipo de destino y la imagen del sistema operativo que se aplica al equipo de destino. También puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiere incluir como parte de los medios preconfigurados. La secuencia de tareas que implementa el sistema operativo no se incluye en los medios. Al implementar una secuencia de tareas que usa medios preconfigurados, el cliente comprueba primero que el contenido de la caché de secuencia de tareas local sea válido. Si el contenido no se encuentra o se ha revisado, el cliente lo descarga desde un punto de distribución o un homólogo.  

Los medios preconfigurados se aplican a la unidad de disco duro de un nuevo equipo antes de enviar el equipo al usuario. Cuando el equipo se inicia por primera vez después de haber aplicado los medios preconfigurados, el equipo se inicia en Windows PE. Se conecta a un punto de administración para encontrar la secuencia de tareas que completa el proceso de implementación del sistema operativo.  

> [!IMPORTANT]
> Los paquetes en el medio preconfigurado no están cifrados. Adopte las medidas de seguridad adecuadas, como agregar una contraseña a los medios, para asegurarse de que el contenido del paquete está protegido contra usuarios no autorizados.

## <a name="standalone-media"></a><a name="BKMK_PlanStandaloneMedia"></a> Medios independientes

Los medios independientes contienen todo lo necesario para implementar el sistema operativo. Este contenido incluye la secuencia de tareas y demás elementos necesarios. Dado que todo está en el medio, el espacio en disco necesario es mayor que para otros tipos de medios.

## <a name="considerations-when-using-https"></a>Consideraciones al usar HTTPS

Cuando configure sus puntos de administración y puntos de distribución para usar HTTPS, cree medios de arranque y medios preconfigurados en un sitio primario, y no en el sitio de administración central. Además, tenga en cuenta el siguiente aspecto como ayuda para determinar si se configura el medio como dinámico o basado en el sitio:  

- Para configurar el medio como dinámico, todos los sitios primarios deben tener la entidad de certificación (CA) raíz del sitio desde el que se creó el medio. Puede importar la entidad de certificación raíz en todos los sitios primarios en la jerarquía.  

- Si los sitios primarios de su jerarquía de Configuration Manager usan otras entidades de certificación raíz, debe usar medios basados en sitio en cada sitio.  

## <a name="next-steps"></a>Pasos siguientes

- [Crear medios de captura](create-capture-media.md)

- [Crear medios de arranque](create-bootable-media.md)

- [Crear medios preconfigurados](create-prestaged-media.md)

- [Creación de medios independientes](create-stand-alone-media.md)
