---
title: Instalación de Windows en un nuevo equipo
titleSuffix: Configuration Manager
description: Use Configuration Manager para instalar un sistema operativo en un equipo nuevo (sin sistema operativo) mediante el entorno PXE, OEM o medios independientes.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a70269839b4a550fbef4dc5cab1b7ff3d426d87
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690673"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Instalación de una nueva versión de Windows en un equipo nuevo (sin sistema operativo) con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este tema se indican los pasos generales de Configuration Manager para instalar un sistema operativo en un equipo nuevo. Para este escenario, puede elegir entre muchos métodos de implementación diferentes, como PXE, OEM o medios independientes. Si no está seguro de si se trata del escenario de implementación de sistema operativo adecuado para usted, consulte [Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md).  

Use las secciones siguientes para actualizar un equipo existente con una nueva versión de Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a> Plan  

-   **Planear e implementar los requisitos de infraestructura**  

     Hay varios requisitos de infraestructura que deben cumplirse antes de implementar sistemas operativos, como Windows ADK, los Servicios de implementación de Windows (WDS), las configuraciones compatibles de disco duro, etc. Para obtener más información, consulte [Infrastructure requirements for operating system deployment](../plan-design/infrastructure-requirements-for-operating-system-deployment.md) (Requisitos de infraestructura para la implementación de sistema operativo).

##  <a name="configure"></a><a name="BKMK_Configure"></a> Configurar  

1.  **Preparar una imagen de arranque**  

     Las imágenes de arranque inician un equipo en un entorno de Windows PE (un sistema operativo mínimo con componentes y servicios limitados) que puede instalar un sistema operativo completo de Windows en el equipo.   Al implementar sistemas operativos, debe seleccionar una imagen de arranque para el uso y la distribución de la imagen en un punto de distribución. Para preparar la imagen de arranque, use lo siguiente:  

    -   Para obtener más información sobre las imágenes de arranque, consulte [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

    -   Para obtener más información sobre la personalización de una imagen de arranque, consulte [Customize boot images (Personalizar imágenes de arranque)](../get-started/customize-boot-images.md).  

    -   Distribuya la imagen de arranque a puntos de distribución. Para obtener más información, vea [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparar una imagen de sistema operativo**  

     La imagen del sistema operativo contiene los archivos necesarios para instalar el sistema operativo en el equipo de destino. Use lo siguiente para preparar la imagen del sistema operativo:  

    -   Para obtener más información sobre cómo crear una imagen de sistema operativo, consulte [Manage operating system images (Administrar imágenes de sistema operativo)](../get-started/manage-operating-system-images.md).

    -   Distribuya la imagen del sistema operativo a los puntos de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > Las nuevas instalaciones de Windows también se pueden realizar desde archivos de origen de instalación a través de los paquetes de actualización del sistema operativo, pero, en su lugar, use imágenes del sistema operativo, como **install.wim**.
    >
    > La implementación de nuevas instalaciones de Windows a través de paquetes de actualización del sistema operativo sigue siendo compatible, pero depende de que los controladores admitan este método. Cuando se instala Windows desde un paquete de actualización del sistema operativo, los controladores se instalan en Windows PE en lugar de simplemente inyectarse en Windows PE. Algunos controladores no son compatibles con la instalación en Windows PE. Si los controladores no son compatibles con la instalación en Windows PE, en su lugar, use una imagen del sistema operativo.  

3.  **Crear una secuencia de tareas para implementar sistemas operativos a través de la red**  

     Use una secuencia de tareas para automatizar la instalación del sistema operativo a través de la red. Siga los pasos de [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md). Según el método de implementación que elija, puede haber consideraciones adicionales para la secuencia de tareas.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> Implementar  

-   Use uno de los siguientes métodos de implementación para implementar el sistema operativo:  

    -   [Usar PXE para implementar Windows a través de la red](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Usar multidifusión para implementar Windows a través de la red](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Crear una imagen para un OEM en fábrica o en un almacén local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md) (Uso de medios independientes para implementar Windows sin usar la red)  

    -   [Usar medios de arranque para implementar Windows a través de la red](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Supervisión  

-   **Supervisar la implementación de la secuencia de tareas**  

     Para supervisar la implementación de la secuencia de tareas para instalar el sistema operativo, consulte [Monitor operating system deployments (Supervisar implementaciones del sistema operativo)](monitor-operating-system-deployments.md).  
