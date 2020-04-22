---
title: Visualización del inventario de software con el Explorador de recursos
titleSuffix: Configuration Manager
description: Use el Explorador de recursos para ver el inventario de software en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690073"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Cómo usar el Explorador de recursos para ver el inventario de software en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use el Explorador de recursos en Configuration Manager para ver información sobre el inventario de software recopilado de los equipos de la jerarquía.  

> [!NOTE]  
>  El Explorador de recursos no mostrará ningún dato de inventario hasta que se haya ejecutado un ciclo de inventario de software en el cliente.  

 El Explorador de recursos proporciona la siguiente información de inventario de software:  

-   **Software**:  

    -   **Archivos recopilados**: archivos que se han recopilado durante el inventario de software.  

    -   **Detalles de archivo**: archivos incluidos en el inventario durante el inventario de software que no están asociados a un fabricante o producto específico.  

    -   **Última exploración de software**: fecha y hora del último inventario de software y recopilación de archivos para el equipo cliente.  

    -   **Detalles del producto**: productos de software que se han inventariado en el inventario de software, agrupados por fabricante.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para ejecutar el Explorador de recursos desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, pulse **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad**, pulse **Dispositivos** o abra cualquier recopilación que muestre dispositivos.  

3.  Seleccione el equipo que contiene el inventario que quiere ver y, después, en la pestaña **Inicio** > grupo **Dispositivos**, pulse **Iniciar** > **Explorador de recursos**.

4.  Puede hacer clic con el botón derecho en cualquier elemento del panel derecho de la ventana Explorador de recursos y pulsar **Propiedades** para ver la información de inventario recopilada en un formato más legible.  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> Ver y administrar los archivos de diagnóstico recopilados

A partir de Configuration Manager versión 2002, use el Explorador de recursos para ver y administrar los archivos que se recopilan cuando se utiliza la notificación de cliente para [recopilar registros de cliente](../client-notification.md#client-diagnostics). 

1. Desde el nodo **Dispositivos**, haga clic con el botón derecho en el dispositivo cuyos registros quiera consultar.
1. Seleccione **Inicio** y, después, **Explorador de recursos**.
1. Desde **Explorador de recursos**, haga clic en **Archivos de diagnóstico**.
1. En la lista **Archivos de diagnóstico**, puede ver la fecha de la recopilación de los archivos. El formato de nombre de los registros de cliente es `Support_<guid>.zip`.
1. Haga clic con el botón derecho en el archivo ZIP y seleccione una de las opciones siguientes:
    - **Abrir el Centro de soporte técnico**: inicia el [Centro de soporte técnico](../../../support/support-center.md).
    - **Copiar**: copia la información de fila del Explorador de recursos.
    - **Ver archivo**: abre la carpeta donde se encuentra el archivo ZIP con el Explorador de archivos.
    - **Guardar**: abre un cuadro de diálogo Guardar archivo para el archivo seleccionado.
    - **Exportar**: guarda las columnas del Explorador de recursos que se muestran en **Archivos de diagnóstico**.
    - **Actualizar**: actualiza la lista de archivos.
    - **Propiedades**: devuelve las propiedades del archivo seleccionado. 

[![Revisar y guardar registros de cliente desde el Explorador de recursos](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>Pasos siguientes

[Use el Centro de soporte técnico](../../../support/support-center.md) para ver los archivos de diagnóstico recopilados.
