---
title: Tareas de administración de aplicaciones
titleSuffix: Configuration Manager
description: Administre tipos de implementación y aplicaciones de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0896204fa994643064676b55b20d63d349c4098b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689303"
---
# <a name="management-tasks-for-configuration-manager-applications"></a>Tareas de administración de aplicaciones de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la información de este artículo como ayuda para administrar las aplicaciones y los tipos de implementación de Configuration Manager.  

Para obtener más información sobre la creación de aplicaciones y los tipos de implementación, consulte [Create applications](../../apps/deploy-use/create-applications.md) (Creación de aplicaciones).  

> [!IMPORTANT]  
>  En función del tipo de aplicación o implementación, algunas de las opciones de administración no están disponibles.  

##  <a name="manage-applications"></a>Administración de aplicaciones  
 En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** > **Aplicaciones**, seleccione la aplicación que quiere administrar y, después, seleccione una tarea de administración.  

|Tarea|Detalles|  
|----------|-------------|  
|**Administrar cuentas de acceso**|Se abre el cuadro de diálogo **Administrar cuentas de acceso** , en el que podrá especificar el nivel de acceso que se permite para el contenido asociado a la aplicación seleccionada.|  
|**Crear archivo de contenido preconfigurado**|Se abre el **Asistente para crear archivos de contenido preconfigurados** que le ayuda a administrar la distribución de contenido en puntos de distribución remotos. Cuando la programación y la limitación no proporcionan una solución válida para el punto de distribución remoto, puede preconfigurar el contenido en el punto de distribución<br /><br /> Consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración de contenido e infraestructura de contenido).|  
|**Historial de revisiones**|Abre el cuadro de diálogo **Historial de revisiones de la aplicación** que le permite visualizar las propiedades de las revisiones que se han realizado en esta aplicación, eliminar revisiones antiguas y restaurar versiones antiguas de esta aplicación.<br /><br /> Consulte [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md) (Revisión y sustitución de aplicaciones).|  
|**Crear tipo de implementación**|Abre el **Asistente para crear tipos de implementación** que le permite agregar un nuevo tipo de implementación a la aplicación seleccionada.<br /><br /> Consulte [Create applications](../../apps/deploy-use/create-applications.md) (Creación de aplicaciones).|  
|**Actualizar estadísticas**|Actualiza la información que se muestra en el nodo **Implementaciones** del área de trabajo **Supervisión** sobre las implementaciones de esta aplicación.<br /><br /> Consulte [Supervisar aplicaciones desde la consola de System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Restablecer**|Restablece una aplicación retirada anteriormente mediante la tarea de administración **Retirar**.|  
|**Retirar**|Cuando retira una aplicación, dejará de estar disponible para la implementación. En cambio, la aplicación y sus implementaciones no se eliminan. No se quitarán las copias existentes de la aplicación que se instalaron en equipos cliente. Todos los cambios hechos en la aplicación se eliminarán de Configuration Manager transcurridos 60 días. Pero, las copias instaladas de la aplicación no se eliminan.<br /><br /> Para eliminar una aplicación primero debe retirarla, eliminar todas las implementaciones, quitar las referencias de otras implementaciones a la aplicación y, después, eliminar todas sus revisiones.<br /><br /> See [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md) (Revisión y sustitución de aplicaciones).|  
|**Exportarar**|Abre el **Asistente para exportar aplicaciones** que le permite exportar las aplicaciones seleccionadas en un archivo .zip que puede archivar o instalar en otro sitio. Si decide exportar el contenido de una aplicación, se creará una carpeta con el contenido.<br /><br /> También puede exportar las dependencias de aplicación, las relaciones de sustitución y las condiciones, y el contenido de la aplicación y de sus dependencias.<br /><br /> El cmdlet de Windows PowerShell, **Export-CMApplication**, realiza la misma función. Para obtener más información, consulte [Export-CMApplication](https://go.microsoft.com/fwlink/p/?LinkID=258880) en la documentación de referencia del cmdlet de Microsoft System Center 2012 Configuration Manager SP1.|  
|**Eliminar**|Elimina la aplicación seleccionada.<br /><br /> No se puede eliminar una aplicación si otras aplicaciones dependen de la misma, si tiene una implementación activa o si tiene secuencias de tareas dependientes.|  
|**Simular implementación**|Abre el **Asistente para simular implementación de aplicación** , en el que puede probar el resultado de una implementación de aplicación en equipos sin instalar o desinstalar la aplicación.<br /><br /> Consulte [Simulate application deployments](../../apps/deploy-use/simulate-application-deployments.md) (Simulación de implementaciones de aplicaciones).|  
|**Implementar**|Abre el **Asistente para implementar software** , en el que puede implementar la aplicación seleccionada en recopilaciones de equipos en su jerarquía.<br /><br /> Consulte [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implementación de aplicaciones).|  
|**Distribuir contenido**|Abre el **Asistente para distribuir contenido** , en el que puede copiar el contenido de la aplicación seleccionada en puntos de distribución en la jerarquía.<br /><br /> Consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración de contenido e infraestructura de contenido).|  
|**Ver relaciones**|Muestra un diagrama gráfico de las relaciones de las aplicaciones seleccionadas con otras aplicaciones. Elija una de las siguientes opciones:<br><br><ul><li>**Dependencia**: muestra las aplicaciones que dependen de la aplicación seleccionada y las aplicaciones de las que la aplicación seleccionada depende.</li><li>**Sustitución**: muestra las aplicaciones que la aplicación seleccionada sustituye y las aplicaciones por las que se sustituye la aplicación seleccionada.</li><li>**Condiciones globales**: muestra las condiciones globales a las que esta aplicación hace referencia.</li></ol><br /> Consulte [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md) (Revisión y sustitución de aplicaciones) y [Cómo crear condiciones globales](../../apps/deploy-use/create-global-conditions.md).|  
|**Copiar aplicaciones**|Copie (o duplique) aplicaciones de Configuration Manager para crear una nueva. Esta acción es útil para probar algo o cuando es necesario crear una aplicación similar. El sitio crea una aplicación con **-copy** anexado al nombre. Aunque el sitio copia la mayoría de los metadatos para la nueva aplicación, no copia ninguna implementación.|

##  <a name="manage-deployment-types"></a>Administración de tipos de implementaciones  
 En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones**, pulse **Aplicaciones** y, después, elija la aplicación que tenga el tipo de implementación que quiere administrar. En el panel de detalles, pulse la pestaña **Tipos de implementación**, elija el tipo de implementación que quiere administrar y, después, elija una tarea de administración.  

|Tarea|Detalles|  
|----------|-------------|  
|**Aumentar prioridad**|Aumenta la prioridad del tipo de implementación seleccionado. Los tipos de implementación se evalúan en orden. Cuando un tipo de implementación cumple los requisitos especificados se ejecutará y no se evaluarán otros tipos de implementación de la lista de prioridad.|  
|**Reducir prioridad**|Reduce la prioridad del tipo de implementación seleccionado.|  
|**Eliminar**|Elimina el tipo de implementación seleccionado.<br><br>No se puede eliminar un tipo de implementación si un tipo de implementación en otra aplicación hace referencia al mismo.<br>Para eliminar un tipo de implementación, primero debe quitar todas las dependencias al tipo de implementación que se incluyen en otros tipos de implementación.<br>Además, también debe quitar las revisiones anteriores de todas las aplicaciones que tienen un tipo de implementación que hace referencia al tipo de implementación que quiere eliminar.|  
|**Actualizar contenido**|Actualiza el contenido del tipo de implementación seleccionado.<br /><br /> Al iniciar el asistente para un tipo de implementación que tiene una aplicación virtual, se inicia el **Asistente para actualizar contenido**. Este asistente le permite modificar las opciones de publicación y las reglas de requisitos para la aplicación virtual seleccionada. Para obtener más información, consulte [Create applications](../../apps/deploy-use/create-applications.md) (Creación de aplicaciones).<br /><br /> Al actualizar el contenido de un tipo de implementación, se crea una nueva revisión de la aplicación. Esto puede provocar que los dispositivos cliente se actualicen con la nueva aplicación.|  
