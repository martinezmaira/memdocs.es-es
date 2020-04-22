---
title: Administración de consultas
titleSuffix: Configuration Manager
description: Aprenda a administrar sus consultas. Incluye una tabla de referencia detallada.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694473"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Cómo administrar las consultas en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo puede servir de ayuda para administrar consultas en Configuration Manager.  

 Para más información sobre cómo crear consultas, vea [Creación de consultas](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Administración de consultas
 En el área de trabajo **Supervisión** , seleccione **Consultas**, seleccione la consulta que se debe administrar y luego seleccione una tarea de administración.  

 En la tabla siguiente se incluye información sobre las tareas de administración.  

|Tarea de administración|Detalles| 
|---------------------|-------------|
|**Ejecutar**|Ejecuta la consulta seleccionada y muestra los resultados en la consola de Configuration Manager.|
|**Instalar cliente**|Abre el **Asistente para instalación de cliente** que le permite instalar el cliente de Configuration Manager en los equipos devueltos por la consulta seleccionada.<br /><br /> Esta opción no está disponible para consultas que devuelven dispositivos móviles, usuarios o grupos de usuarios. <br /><br /> Para obtener más información sobre cómo instalar clientes de Configuration Manager mediante la inserción de cliente, consulte [Implementar clientes en equipos Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Exportarar**|Abre el **Asistente para exportar objetos**. Este asistente le permite exportar la consulta a un archivo Managed Object Format (MOF) que luego puede importar en otro sitio.
|**Moverr**|Abre el cuadro de diálogo **Mover elementos seleccionados**. Este cuadro de diálogo le permite mover la consulta seleccionada a una carpeta que haya creado anteriormente en el nodo **Consultas**.|

## <a name="next-steps"></a>Pasos siguientes 
 [Crear consultas](../../../core/servers/manage/create-queries.md)
