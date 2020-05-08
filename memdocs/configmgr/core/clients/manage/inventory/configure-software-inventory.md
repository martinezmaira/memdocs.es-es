---
title: Configuración del inventario de software
titleSuffix: Configuration Manager
description: Configure el inventario de software y excluya carpetas del inventario de software en Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f6fcf4736c30d8743d0d26b52aac60ef12b5c9cd
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906311"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>Cómo configurar el inventario de software en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este procedimiento configura las opciones de cliente predeterminadas para el inventario de software y se aplica a todos los equipos de la jerarquía. Si solo quiere aplicar esta configuración a algunos clientes, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación. Para obtener más información sobre cómo crear configuraciones de dispositivo personalizadas, vea [Cómo establecer la configuración de cliente](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Cómo configurar el inventario de software  

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** **Configuración de cliente predeterminada**.  

2. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

3. En el cuadro de diálogo **Configuración predeterminada**, elija **Inventario de software**.  

4. En la lista **Configuración de dispositivo** , configure los valores siguientes:  

   -   **Habilitar inventario de software en clientes**: en la lista desplegable, seleccione **Verdadero**.  

   -   **Programar inventario de software y recopilación de archivos**: configura el intervalo en el que los clientes recopilan archivos e inventario de software.   

5. Configure las opciones de cliente que necesite. En la sección [Inventario de software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) del artículo [Acerca de la configuración de cliente](../../../../core/clients/deploy/about-client-settings.md) se incluye una lista de la configuración de cliente.  

   Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Cómo administrar clientes](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   El código de error 80041006 en inventoryprovider.log significa que el proveedor de WMI no tiene memoria suficiente. Es decir, se ha alcanzado el límite de cuota de memoria para un proveedor y el proveedor de inventario no puede continuar.
   > En este caso, el agente de inventario crea un informe con 0 entradas, por lo que no se informa de ningún elemento de inventario. <br/>
   > Una posible solución para este error sería reducir el ámbito de la recopilación de inventario de software. En los casos en los que el error se produce después de limitar el ámbito de inventario, aumentar la propiedad [MemoryPerHost](https://techcommunity.microsoft.com/t5/ask-the-performance-team/memory-and-handle-quotas-in-the-wmi-provider-service/ba-p/373319) definida en la clase [_ProviderHostQuotaConfiguration](https://docs.microsoft.com/windows/win32/wmisdk/--providerhostquotaconfiguration) puede proporcionar una solución.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Cómo excluir carpetas del inventario de software  

1.  Con Notepad.exe, cree un archivo vacío llamado **Skpswi.dat**.  

2.  Haga clic con el botón derecho en el archivo **Skpswi.dat** y después haga clic en **Propiedades**. En las propiedades de archivo del archivo Skpswi.dat, seleccione el atributo **Oculto** .  

3.  Coloque el archivo **Skpswi.dat** en la raíz de cada estructura de carpeta o unidad de disco duro de cliente que quiera excluir del inventario de software.  

> [!NOTE]  
>  El inventario de software no inventariará la unidad de cliente de nuevo a menos que este archivo se elimine de la unidad del equipo cliente.
