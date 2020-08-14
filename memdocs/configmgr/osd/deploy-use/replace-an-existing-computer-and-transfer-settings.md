---
title: Reemplazar un equipo existente y transferir la configuración
titleSuffix: Configuration Manager
description: En Configuration Manager puede reemplazar un equipo existente por uno nuevo mediante varios métodos de implementación, como medios de arranque, la multidifusión o el Centro de software.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 860ee3aeb255921ccd8bf3b1695a9647b514752f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124875"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Reemplazo de un equipo existente y transferencia de la configuración con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este tema se indican los pasos generales en Configuration Manager para reemplazar un equipo existente por uno nuevo. Para este escenario, puede elegir entre muchos métodos de implementación diferentes, como el medio de arranque, la multidifusión o el Centro de software. También puede optar por instalar un punto de migración de estado para almacenar la configuración y, después, restaurarla en el nuevo sistema operativo después de instalarlo. Si no está seguro de si se trata del escenario de implementación de sistema operativo adecuado para usted, consulte [Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md).  

 Use las secciones siguientes para actualizar un equipo existente con una nueva versión de Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a> Plan  

-   **Planear e implementar los requisitos de infraestructura**  

     Hay varios requisitos de infraestructura que deben cumplirse antes de implementar sistemas operativos, como Windows ADK, la Herramienta de migración de estado de usuario (USMT), los Servicios de implementación de Windows (WDS), las configuraciones compatibles de disco duro, etc. Para obtener más información, consulte [Infrastructure requirements for operating system deployment](../plan-design/infrastructure-requirements-for-operating-system-deployment.md) (Requisitos de infraestructura para la implementación de sistema operativo).  

-   **Instalar un punto de migración de estado (solo es necesario si se transfiere la configuración)**  

     Si se dispone a capturar la configuración del equipo existente para restaurarla posteriormente en el nuevo sistema operativo, debe instalar un punto de migración de estado. Para obtener más información, consulte [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints) (Punto de migración de estado).  

##  <a name="configure"></a><a name="BKMK_Configure"></a> Configurar  

1.  **Preparar una imagen de arranque**  

     Las imágenes de arranque inician un equipo en un entorno de Windows PE (un sistema operativo mínimo con componentes y servicios limitados) que puede instalar un sistema operativo completo de Windows en el equipo. Al implementar sistemas operativos, debe seleccionar una imagen de arranque para el uso y la distribución de la imagen en un punto de distribución. Para preparar la imagen de arranque, use lo siguiente:  

    -   Para obtener más información sobre las imágenes de arranque, consulte [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

    -   Para obtener más información sobre la personalización de una imagen de arranque, consulte [Customize boot images (Personalizar imágenes de arranque)](../get-started/customize-boot-images.md).  

    -   Distribuya la imagen de arranque a puntos de distribución. Para obtener más información, vea [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparar una imagen de sistema operativo**  

     La imagen del sistema operativo contiene los archivos necesarios para instalar el sistema operativo en el equipo de destino. Use lo siguiente para preparar la imagen del sistema operativo:  

    -   Para obtener más información sobre cómo crear una imagen de sistema operativo, consulte [Manage operating system images (Administrar imágenes de sistema operativo)](../get-started/manage-operating-system-images.md).  

    -   Distribuya la imagen del sistema operativo a los puntos de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Crear una secuencia de tareas para implementar sistemas operativos a través de la red**  

     Use una secuencia de tareas para automatizar la instalación del sistema operativo a través de la red. Siga los pasos de [Crear una secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md). Según el método de implementación que elija, puede haber consideraciones adicionales para la secuencia de tareas.  

    > [!NOTE]  
    >  En este escenario, si captura y restaura los archivos y la configuración de usuario, puede optar por usar un punto de migración de estado o guardar los archivos localmente. Para obtener más información, consulte [Manage user state](../get-started/manage-user-state.md) (Administrar el estado de usuario).  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> Implementar  

-   Use uno de los siguientes métodos de implementación para implementar el sistema operativo:  

    -   [Usar el Centro de software para implementar Windows a través de la red](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Usar medios de arranque para implementar Windows a través de la red](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Usar multidifusión para implementar Windows a través de la red](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Crear una imagen para un OEM en fábrica o en un almacén local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Supervisión  

-   **Supervisar la implementación de la secuencia de tareas**  

     Para supervisar la implementación de la secuencia de tareas con la que se instala el sistema operativo, consulte [Monitor operating system deployments](monitor-operating-system-deployments.md) (Supervisar implementaciones del sistema operativo).  
