---
title: Content Library Explorer
titleSuffix: Configuration Manager
description: Utilice el Explorador de la biblioteca de contenido para ver y solucionar problemas de la biblioteca de contenido en un punto de distribución de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92aa778dded970800a65cab9074a547e870bf88e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707863"
---
# <a name="content-library-explorer"></a>Content Library Explorer

*Se aplica a: Configuration Manager (rama actual)*

Content Library Explorer es una de las [herramientas de Configuration Manager](tools.md). Use esta herramienta para las siguientes actividades:  

- Explorar la biblioteca de contenido en un punto de distribución específico  

- Solucionar problemas relacionados con la biblioteca de contenido  

- Copiar paquetes, contenido, carpetas y archivos de la biblioteca de contenido  

- Redistribuir los paquetes al punto de distribución  

- Validar los paquetes en los puntos de distribución remotos  



## <a name="requirements"></a>Requisitos

- Ejecute la herramienta con una cuenta a la que tenga acceso administrativo:  

    - El punto de distribución de destino  

    - El proveedor WMI en el servidor de sitio  

    - El proveedor de Configuration Manager  

- Solo los roles **Administrador total** y **analista de solo lectura** tienen derechos suficientes para ver toda la información de esta herramienta.  

    - Otros roles, como **Administrador de la aplicación** pueden ver información parcial. Para obtener más información, consulte [Disabled packages](#bkmk_disabled-packages).  

    - El **Analista de solo lectura** no puede redistribuir los paquetes desde esta herramienta.  

- Ejecute la herramienta desde cualquier equipo, siempre que se pueda conectar a:  

    - El punto de distribución de destino  

    - El servidor de sitio primario  

    - El proveedor de Configuration Manager  

- Aunque el punto de distribución esté en el servidor de sitio, aún es necesario tener acceso administrativo al servidor de sitio.  



## <a name="usage"></a>Uso 

Al iniciar **ContentLibraryExplorer.exe**, escriba el nombre de dominio completo (FQDN) del punto de distribución de destino. Después se conecta al punto de distribución. Si el punto de distribución forma parte de un sitio secundario, le pide el FQDN del servidor del sitio primario y el código de sitio primario.

En el panel izquierdo, vea los paquetes que se distribuyen a este punto de distribución. Expanda los paquetes y explore su estructura de carpetas. Esta estructura coincide con la estructura de carpetas desde la que creó el paquete.

Cuando selecciona una carpeta, muestra en el panel derecho los archivos dentro de la carpeta. Esta vista incluye la siguiente información: 
- Nombre de archivo
- Tamaño de archivo
- En qué unidad está
- Otros paquetes que usan el mismo archivo en la unidad
- Cuándo el archivo se cambió por última vez en el punto de distribución

La herramienta también se conecta al proveedor de Configuration Manager. Esta conexión consiste en determinar qué paquetes se distribuyen al punto de distribución y si están realmente en la biblioteca de contenido del punto de distribución. Por ejemplo, es posible que un paquete que está pendiente de distribución no exista aún en la biblioteca de contenido. Este tipo de paquete aparecería como "PENDIENTE" en la herramienta, y ninguna de las acciones están habilitadas para este paquete.


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a> Paquetes deshabilitados

Algunos paquetes están presentes en el punto de distribución pero no están visibles en la consola de Configuration Manager. Estos paquetes se marcan con un asterisco (\*). En estos paquetes no se puede realizar ninguna acción. También es posible que otros paquetes se deban marcar con un asterisco y se deban deshabilitar sus acciones. 

Existen tres razones principales por las que se deshabilitan paquetes:  

- El paquete es la actualización de cliente de Configuration Manager. Este paquete incluye "ccmsetup.exe".  

- Su cuenta de usuario no puede acceder al paquete, probablemente debido a la administración basada en roles. Por ejemplo, el rol **Autor de la aplicación** no puede ver los paquetes de controladores en la consola, por lo que los paquetes de controladores en el punto de distribución se marcan como deshabilitados.  

- El paquete está huérfano en el punto de distribución.  


### <a name="validate-packages"></a>Validar paquetes

Valide paquetes usando **Paquete** > **Validar** en la barra de herramientas. Seleccione primero un nodo de paquete en el panel izquierdo, no seleccione un contenido o una carpeta. La herramienta se conecta al proveedor WMI del punto de distribución para esta acción. Cuando se inicia la herramienta, los paquetes a los que les falta contenido se marcan como no válidos. Validar el paquete muestra el contenido que falta. Si todo el contenido está presente, pero los datos están dañados, la validación detecta los daños.


### <a name="redistribute-packages"></a>Redistribuir los paquetes

Redistribuya paquetes mediante **Paquete** > **Redistribuir** en la barra de herramientas. En primer lugar, seleccione un nodo de paquete en el panel izquierdo. Esta acción requiere permisos para redistribuir los paquetes.


### <a name="other-actions"></a>Otras acciones

Use **Editar** > **Copiar** para copiar los paquetes, el contenido, las carpetas y los archivos de la biblioteca de contenido en una carpeta especificada. No puede copiar la propia biblioteca de contenido. Seleccione más de un archivo, pero no puede seleccionar varias carpetas.

Busque paquetes usando **Editar** > **Buscar paquete**. Esta acción busca la consulta en el nombre del paquete y el identificador del paquete.



## <a name="limitations"></a>Limitaciones

- La herramienta no puede manipular la biblioteca de contenido directamente de ningún modo. Los cambios realizados en la biblioteca de contenido pueden producir errores de funcionamiento.  

- La herramienta puede redistribuir los paquetes, pero solo para el punto de distribución de destino.  

- Al colocar el punto de distribución con el servidor de sitio, no puede validar los datos del paquete. Usar la consola de Configuration Manager en su lugar. La herramienta todavía inspecciona el paquete para asegurarse de que todo el contenido está presente, aunque no necesariamente intacto.  

- No se puede eliminar el contenido con esta herramienta.



## <a name="see-also"></a>Vea también

- [Conceptos básicos de la administración de contenido](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [La biblioteca de contenido](../plan-design/hierarchy/the-content-library.md)
