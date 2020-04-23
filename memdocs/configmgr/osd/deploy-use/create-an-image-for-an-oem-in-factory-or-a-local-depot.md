---
title: Creación de una imagen para un OEM en fábrica o en un almacén local
titleSuffix: Configuration Manager
description: Use implementaciones de medios preconfigurados para reducir el tráfico de red mientras implementa un sistema operativo en un equipo que no esté aprovisionado por completo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c4d445d18b9e239ace673199f6a7d0f26d10a42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707293"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Crear una imagen para un OEM en fábrica o en un almacén local con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las implementaciones de medios preconfigurados de Configuration Manager permiten implementar un sistema operativo en un equipo que no esté aprovisionado por completo. Los medios preconfigurados son un archivo Windows Imaging Format (WIM) que puede ser instalado en un equipo sin sistema operativo por el fabricante (OEM) o en un centro de configuración empresarial no relacionado con el entorno de Configuration Manager. Más adelante, en el entorno de Configuration Manager, el equipo se iniciará mediante la imagen de arranque proporcionada por los medios, se ejecutará una comprobación del algoritmo hash en los medios preconfigurados para garantizar su validez y, después, el equipo se conectará al punto de administración del sitio en busca de secuencias de tareas disponibles que completen el proceso de descarga.


Este método de implementación puede reducir el tráfico de red porque la imagen de arranque y la imagen de sistema operativo ya están en el equipo de destino. Puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiera incluir en los medios preconfigurados. Después de instalar el sistema operativo en el equipo, primero se buscan en la memoria caché de la secuencia de tareas aplicaciones, paquetes o paquetes de controladores y, si el contenido no se encuentra o se ha revisado, el contenido se descarga desde un punto de distribución configurado en los medios preconfigurados y se instala.  

 Puede usar los medios preconfigurados en los siguientes escenarios de implementación de sistema operativo:  

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

- [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md)  

  Complete las etapas de uno de los escenarios de implementación de sistema operativo y luego use las secciones siguientes para preparar y crear los medios preconfigurados.  

## <a name="configure-deployment-settings"></a>Configurar la implementación  
 Cuando use un medio preconfigurado para iniciar el proceso de implementación del sistema operativo, debe configurar la implementación para que el sistema operativo esté disponible para los medios. Puede configurar esto en la página **Configuración de implementación** del Asistente para implementar Software o en la pestaña **Configuración de implementación** en las propiedades de la implementación.  Para la opción de configuración **Estar disponible para** , configure uno de los siguientes:  

-   **Clientes de Configuration Manager, medios y PXE**  

-   **Solo medios y PXE**  

-   **Sólo medios y PXE (ocultos)**  

## <a name="create-the-prestaged-media"></a>Crear los medios preconfigurados  
 Cree el archivo de medios preconfigurados para enviar al OEM o al almacén local. Para más información, consulte [Crear medios preconfigurados con Configuration Manager](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Enviar el archivo de medios preconfigurados al OEM o al almacén local  
 Envíe los medios al OEM o al almacén local para preconfigurar los equipos. El archivo de medios preconfigurados se aplica a un disco duro formateado en el equipo.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Iniciar el equipo para instalar el sistema operativo  
 El archivo de medios preconfigurados se aplica a los equipos. Cuando el equipo se inicia por primera vez, se inicia el proceso de instalación del sistema operativo.  
