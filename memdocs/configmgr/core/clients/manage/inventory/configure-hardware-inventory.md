---
title: Configuración del inventario de hardware
titleSuffix: Configuration Manager
description: Configure el inventario de hardware de todos los clientes o de una recopilación en Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695453"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>Cómo configurar el inventario de hardware en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este procedimiento configura las opciones de cliente predeterminadas del inventario de hardware y se aplicará a todos los clientes de la jerarquía. Si quiere que esta configuración solo se aplique a algunos clientes, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los dispositivos que quiera usar para el inventario de hardware. Vea [Cómo establecer la configuración del cliente](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Si un dispositivo cliente recibe la configuración de inventario de hardware de varios conjuntos de configuraciones de cliente, las clases de inventario de hardware de cada conjunto de configuraciones se combinarán cuando el cliente informe del inventario de hardware. Además, no activar una clase en una configuración de cliente personalizada con una prioridad más alta no deshabilita al cliente para realizar el inventario de esa clase. 

Para deshabilitar una clase de inventario de hardware específica en la mayoría de los sistemas excepto en algunos, es necesario desactivar la clase en la configuración predeterminada del cliente. Después, se crea una configuración de cliente personalizada para habilitar la clase y se implementa en los sistemas de destino.


### <a name="to-configure-hardware-inventory"></a>Cómo configurar el inventario de hardware  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  En el cuadro de diálogo **Configuración predeterminada**, pulse **Inventario de hardware**.  

6.  En la lista **Configuración de dispositivo** , configure lo siguiente:  

    -   **Habilitar inventario de hardware en clientes**; seleccione **Sí**.  

    -   **Programación de inventario de hardware**; haga clic en **Programar** para especificar el intervalo en el que los clientes recopilan el inventario de hardware.  

7.  Configure otras opciones de [configuración del cliente de inventario de hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) que necesite.  

Los dispositivos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Cómo administrar clientes](../../../../core/clients/manage/manage-clients.md).  
