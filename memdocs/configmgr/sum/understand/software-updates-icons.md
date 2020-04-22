---
title: Iconos que se usan para las actualizaciones de software
titleSuffix: Configuration Manager
description: La consola de Configuration Manager contiene iconos que indican un estado del grupo de actualizaciones de software o actualización sincronizada.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3843dd4ab4fe5a9aecaae8e6f207c3d037fc1950
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700053"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>Iconos usados para las actualizaciones de software en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las actualizaciones de software sincronizadas se muestran en la consola de Configuration Manager y la primera columna de cada actualización de software contiene un icono que indica un estado específico. Los grupos de actualizaciones de software también se representan con un icono que proporciona información sobre el estado de las actualizaciones de software que contiene el grupo. Esta sección proporciona información acerca de los iconos de actualización de software y de lo que representa cada icono.  

## <a name="icons-for-software-updates"></a>Iconos de las actualizaciones de software  
 Las actualizaciones de software sincronizadas se representan mediante uno de los siguientes iconos.  

### <a name="normal-icon"></a>Icono de normal  
 ![icono](../media/Normal.jpg "Icono de normal") El icono con la flecha verde representa una actualización de software normal.  

 **Descripción:**  

 Las actualizaciones de software normales están sincronizadas y disponibles para la implementación de software.  

 **Preocupaciones operativas:**  

 No existe ninguna preocupación operativa.  

### <a name="expired-icon"></a>Icono de expirado  
 ![icono](../media/Expired.jpg "Icono de expirado") El icono con la X de color negro representa una actualización de software expirada. Para identificar actualizaciones de software expiradas, también puede consultar la columna **Expirado** de la actualización de software cuando se muestre en la consola de Configuration Manager.  

 **Descripción:**  

 Las actualizaciones de software expiradas se podían implementar anteriormente en los equipos cliente, pero cuando una actualización de software expira, ya no se pueden crear nuevas implementaciones para las actualizaciones de software. Las actualizaciones de software expiradas se quitan de las implementaciones activas y ya no estarán disponibles para los clientes.  

 **Preocupaciones operativas:**  

 No existe ninguna preocupación operativa.

### <a name="superseded-icon"></a>Icono de sustituido  
 ![icono](../media/Superseded.jpg "Icono de reemplazado") El icono con una estrella amarilla representa una actualización de software sustituida. Para identificar actualizaciones de software sustituidas, también puede consultar la columna **Se sustituyó** de la actualización de software cuando se muestre en la consola de Configuration Manager.  

 **Descripción:**  

 Las actualizaciones de software sustituidas se reemplazaron por versiones más recientes de la actualización de software. Por lo general, una actualización de software que sustituye a otra actualización de software realiza una o varias de las siguientes acciones:  

- Mejora o agrega la revisión proporcionada por una o varias de las actualizaciones publicadas anteriormente.  

- Mejora la eficacia del paquete de archivos de actualización de software, que los clientes instalan si la actualización de software se aprueba para la instalación. Por ejemplo, la actualización de software sustituida podría contener archivos que ya no son relevantes para la revisión o para los sistemas operativos que se admiten en la nueva actualización de software; por tanto, esos archivos ya no se incluyen en el paquete de archivos de sustitución de la actualización de software.  

- Actualiza las versiones más recientes de un producto o, en otras palabras, ya no se aplica a las versiones o configuraciones más antiguas de un producto. Las actualizaciones de software también pueden sustituir a otras actualizaciones de software si se realizaron modificaciones para ampliar la compatibilidad de idioma. Por ejemplo, una revisión posterior de la actualización de un producto para Microsoft Office puede quitar la compatibilidad para un sistema operativo más antiguo, pero podría agregar compatibilidad adicional para nuevos idiomas en la versión de actualización de software inicial.  

  En la ficha Reglas de sustitución en las propiedades de componente de punto de actualización de software, puede especificar cómo administrar las actualizaciones de software sustituidas. Para obtener más información, consulte [Reglas de sustitución](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Preocupaciones operativas:**  

  Cuando sea posible, implemente la actualización de software de sustitución en los equipos cliente en lugar de la actualización de software sustituida. Puede mostrar una lista de las actualizaciones de software que sustituyen a la actualización de software en la ficha **Información de sustitución** de las propiedades de actualización de software.  

### <a name="invalid-icon"></a>Icono de no válido  
 ![icono](../media/Invalid.jpg "Icono de no válido") El icono con la X roja representa una actualización de software no válida.  

 **Descripción:**  

 Las actualizaciones de software no válidas se encuentran en una implementación activa, pero por alguna razón no está disponible el contenido (archivos de actualización de software). Los siguientes son escenarios en que puede producirse este estado:  

- Implementa correctamente la actualización de software, pero el archivo de actualización de software se quita del paquete de implementación y ya no está disponible.  

- Crea una implementación de actualizaciones de software en un sitio y el objeto de implementación se replica correctamente en un sitio secundario, pero el paquete de implementación no se replica correctamente en el sitio secundario.  

  **Preocupaciones operativas:**  

  Si falta el contenido de una actualización de software, los clientes no pueden instalar la actualización de software hasta que el contenido esté disponible en un punto de distribución. Puede redistribuir el contenido a los puntos de distribución mediante la acción **Redistribuir** . Si falta el contenido de una actualización de software en una implementación creada en un sitio primario, la actualización de software se debe replicar o redistribuir al sitio secundario. Para obtener más información sobre la redistribución de contenido, consulte [Administrar el contenido distribuido](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Icono de solo metadatos
 ![icono](../media/MetadataOnly.png "Icono de solo metadatos") El icono con la flecha azul representa una actualización de software de solo metadatos.

 **Descripción:**  

 Las actualizaciones de software de solo metadatos están disponibles en la consola de Configuration Manager para los informes. No se pueden implementar ni descargar actualizaciones de software de solo metadatos porque un archivo de actualización de software no está asociado con los metadatos de las actualizaciones de software.  

 **Preocupaciones operativas:**  

 Las actualizaciones de software de solo metadatos están disponibles para la elaboración de informes y no están pensadas para la implementación de actualizaciones de software.  

## <a name="icons-for-software-update-groups"></a>Iconos de grupos de actualizaciones de software  
 Los grupos de actualizaciones de software se representan mediante uno de los siguientes iconos.  

### <a name="normal-icon"></a>Icono de normal  
 ![icono](../media/Normal.jpg "Icono de normal") El icono con la flecha verde representa un grupo de actualizaciones de software que contiene solo actualizaciones de software normales.  

 **Preocupaciones operativas:**  

 No existe ninguna preocupación operativa.  

### <a name="expired-icon"></a>Icono de expirado  
 ![icono](../media/Expired.jpg "Icono de expirado") El icono con la X negra representa un grupo de actualizaciones de software que contiene una o varias actualizaciones de software expiradas.  

 **Preocupaciones operativas:**  

 Quite o reemplace las actualizaciones de software expiradas del grupo de actualizaciones de software cuando sea posible.  

### <a name="superseded-icon"></a>Icono de sustituido  
 ![icono](../media/Superseded.jpg "Icono de reemplazado") El icono con la estrella amarilla representa un grupo de actualizaciones de software que contiene una o varias actualizaciones de software reemplazadas.  

 **Preocupaciones operativas:**  

 Reemplace la actualización de software sustituida en el grupo de actualizaciones de software por la actualización de software de sustitución cuando sea posible.  

### <a name="invalid-icon"></a>Icono de no válido  
 ![icono](../media/Invalid.jpg "Icono de no válido") El icono con la X roja representa un grupo de actualizaciones de software que contiene una o varias actualizaciones de software no válidas.  

 **Preocupaciones operativas:**  

 Si falta el contenido de una actualización de software, los clientes no pueden instalar la actualización de software hasta que el contenido esté disponible en un punto de distribución. Puede redistribuir el contenido a los puntos de distribución mediante la acción **Redistribuir** . Si falta el contenido de una actualización de software en una implementación creada en un sitio primario, la actualización de software se debe replicar o redistribuir al sitio secundario. Para obtener más información sobre la redistribución de contenido, consulte [Administrar el contenido distribuido](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  


## <a name="next-steps"></a>Pasos siguientes 

[Planear las actualizaciones de software](../plan-design/plan-for-software-updates.md)