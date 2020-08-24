---
title: Creación de una imagen para un OEM en fábrica o en un almacén local
titleSuffix: Configuration Manager
description: Use implementaciones de medios preconfigurados para reducir el tráfico de red mientras implementa un sistema operativo en un equipo que no esté aprovisionado por completo.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125447"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Crear una imagen para un OEM en fábrica o en un almacén local con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las implementaciones de medios preconfigurados de Configuration Manager permiten implementar un sistema operativo en un equipo que no esté aprovisionado por completo. Los medios preconfigurados son archivos de imagen de Windows (WIM). El fabricante (OEM) puede instalarlo en un equipo sin sistema operativo, o puede usarlo en un centro de ensayo independiente del entorno de producción.

Este método de implementación puede reducir el tráfico de red porque la imagen de arranque y la imagen del sistema operativo ya están en el equipo de destino. Puede especificar las aplicaciones, los paquetes y los paquetes de controladores que quiera incluir en los medios preconfigurados. Después de instalar el sistema operativo en el equipo, la secuencia de tareas comprueba primero las aplicaciones, los paquetes o los paquetes de controladores en la caché preconfigurada. Si no se encuentra el contenido necesario o hay disponible una revisión más reciente en línea, la secuencia de tareas descarga el contenido desde un punto de distribución.

Use los medios preconfigurados en los siguientes escenarios de implementación del sistema operativo:

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)

- [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md)

Realice los pasos de uno de estos escenarios de implementación del sistema operativo. A continuación, use las siguientes secciones para preparar y crear los medios preconfigurados.

## <a name="configure-deployment-settings"></a>Configurar la implementación

En la página **Deployment Settings** (Configuración de implementación) de la implementación, en la opción **Make available to the following** (Estar disponible para), seleccione una de las siguientes opciones:

- Clientes de Configuration Manager, medios y PXE

- Solo medios y PXE

- Sólo medios y PXE (ocultos)

## <a name="create-the-prestaged-media"></a>Crear los medios preconfigurados

Cree el archivo de medios preconfigurados para enviar al OEM o al almacén local. Para más información, consulte [Crear medios preconfigurados con Configuration Manager](create-prestaged-media.md).

## <a name="send-the-prestaged-media-file"></a>Envío del archivo del medio preconfigurado

Envíe el medio al OEM o al almacén local para preconfigurar los equipos. Ellos aplicarán el archivo de imagen a un disco duro formateado del equipo.

## <a name="deliver-the-computer"></a>Entrega del equipo

Cuando se entrega el equipo a un usuario y se activa por primera vez:

1. El equipo se inicia con la imagen de arranque preconfigurada.

1. Se comprueba un valor hash en el medio preconfigurado para asegurarse de que es válido.

1. El equipo se conecta al punto de administración para que las secuencias de tareas estén disponibles para completar el proceso.

## <a name="next-steps"></a>Pasos siguientes

[Experiencias de usuario para la implementación de sistemas operativos](../understand/user-experience.md)
