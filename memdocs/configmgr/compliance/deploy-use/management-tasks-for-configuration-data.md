---
title: Administrar datos de configuración
titleSuffix: Configuration Manager
description: Después de crear los elementos de configuración y las líneas base en Configuration Manager, puede utilizar otros comandos para realizar diversas acciones.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: c375b5d773775e1be89f1e9dda38ee04e7f9f63f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240259"
---
# <a name="manage-configuration-data-in-configuration-manager"></a>Administración de datos de configuración en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Una vez creados los elementos de configuración y las líneas base de configuración en Configuration Manager, puede hacer uso de los diferentes comandos a su disposición para ejecutar diferentes acciones.  

## <a name="manage-configuration-items"></a>Administración de elementos de configuración  

-   En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** > **Elementos de configuración**, seleccione el elemento de configuración que quiere administrar y después seleccione una tarea de administración.  

|Tarea de administración|Detalles|  
|---------------------|-------------|  
|**Crear elemento de configuración secundario**|Abre el **Asistente para crear elemento de configuración secundario** , donde puede crear un elemento de configuración secundario a partir del elemento de configuración seleccionado.<br /><br /> No se puede crear un elemento de configuración secundario a partir de un elemento de configuración de dispositivo móvil.<br /><br /> Para obtener más información, consulte [Create child configuration items](../../compliance/deploy-use/create-child-configuration-items.md) (Creación de elementos de configuración secundarios).|  
|**Historial de revisiones**|Abre el cuadro de diálogo **Historial de revisión del elemento de configuración** , donde puede ver y administrar las revisiones anteriores del elemento de configuración seleccionado.|  
|**Ver definición de XML**|Muestra el archivo de definición XML del elemento de configuración seleccionado en una nueva ventana. Esta información puede ser útil cuando desee crear manualmente datos de configuración.|  
|**Exportarar**|Exporta un elemento de configuración en un formato de archivo .cab, si se creó en ese sitio. Después, puede importarlo en el mismo sitio de Configuration Manager o en otro. Los datos de configuración se convierten en el resumen de DCM.|  
|**Copiar**|Crea una copia del elemento de configuración seleccionado con un nombre que especifique. El nuevo elemento de configuración no conserva ninguna relación con el elemento de configuración original. Esto significa que el elemento de configuración duplicada no continúa heredar información de configuración del elemento de configuración original.|  
|**Eliminar**|Abre el cuadro de diálogo **Eliminar elemento de configuración** , donde puede revisar las referencias a este elemento de configuración.<br /><br /> Debe quitar todas las referencias a un elemento de configuración antes de poder eliminar el elemento de configuración.|  

## <a name="manage-configuration-baselines"></a>Administración de líneas base de configuración  

-   En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** > **Líneas base de configuración**, seleccione la línea base de configuración que quiere administrar y después seleccione una tarea de administración.  


|Tarea de administración|Detalles|  
|---------------------|-------------|  
|**Mostrar miembros**|Muestra todos los elementos de configuración a los que la línea base hace referencia.|  
|**Programar resumen**|Configura la programación que determina la actualización de los datos que se muestran en el nodo **Líneas base de configuración** en la consola de Configuration Manager con la información más reciente de la base de datos del sitio.|  
|**Ejecutar resumen**|El resumen hace que los datos del nodo **Líneas base de configuración** se actualicen con los datos más recientes de la base de datos del sitio. Esta acción puede tardar varios minutos en completarse. Es posible que tenga que hacer clic en **Actualizar** para poder ver los datos más recientes en la consola.|  
|**Ver definición de XML**|Muestra el archivo de definición XML de la línea base de configuración seleccionada en una nueva ventana. Esta información puede ser útil cuando desee crear manualmente datos de configuración.|  
|**Habilitar**|Permite una referencia de configuración para la supervisión del cumplimiento de normas.|  
|**Deshabilitar**|Deshabilita una línea base de configuración para que ya no se evalúe su cumplimiento en los equipos cliente. Líneas base de configuración que hacen referencia a esta línea de base de configuración también se deshabilitará.|  
|**Exportarar**|Exporta una línea base de configuración en un formato de archivo .cab, si se creó en ese sitio. Después, puede importarlo en el mismo sitio de Configuration Manager o en otro. Los datos de configuración se convierten en el resumen de DCM.<br /><br /> Para obtener información sobre cómo importar datos de configuración, consulte [Importe datos de configuración](../../compliance/deploy-use/import-configuration-data.md).|  
|**Copiar**|Crea una copia de la línea base de configuración seleccionada con un nombre que especifique. La nueva instantánea de configuración no conserva ninguna relación con la línea de base original.|  
|**Eliminar**|Abre el cuadro de diálogo **Eliminar línea base de configuración** , donde puede revisar las referencias a esta línea base de configuración.<br /><br /> Debe quitar todas las referencias a una línea base de configuración antes de poder eliminar la línea base de configuración.|  
|**Implementar**|Abre el cuadro de diálogo **Implementar línea de base de configuración** , en el que puede implementar una o varias líneas base de configuración en dispositivos de la jerarquía.<br /><br /> Para obtener más información, consulte [Deploy configuration baselines](../../compliance/deploy-use/deploy-configuration-baselines.md) (Implementación de líneas base de configuración).|  
