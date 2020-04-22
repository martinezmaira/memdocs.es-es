---
title: Clasificar automáticamente dispositivos en recopilaciones
titleSuffix: Configuration Manager
description: Clasifique dispositivos en recopilaciones de forma automática.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695273"
---
# <a name="automatically-categorize-devices-into-collections"></a>Clasificar automáticamente dispositivos en recopilaciones

*Se aplica a: Configuration Manager (rama actual)*

Puede crear categorías de dispositivos, que se pueden usar para colocar automáticamente los dispositivos en colecciones de dispositivos cuando se usa Configuration Manager con Microsoft Intune. Después, los usuarios tienen que elegir una categoría de dispositivos cuando inscriben un dispositivo en Intune. Puede cambiar una categoría de dispositivo desde la consola de Configuration Manager.

> [!IMPORTANT]
>  Esta capacidad funciona con la versión de **junio de 2016** de Microsoft Intune y versiones posteriores. Asegúrese de haber actualizado a esta versión antes de probar estos procedimientos.

## <a name="create-device-categories"></a>Crear categorías de dispositivos

1.  Vaya a **Activos y compatibilidad** > **Información general** > **Recopilaciones de dispositivos**.
2.  En el grupo **Recopilaciones de dispositivos** de la pestaña **Inicio**, haga clic en **Administrar categorías de dispositivos**.
3.  Crear, editar o quitar categorías

## <a name="associate-a-collection-with-a-device-category"></a>Asociar una colección a una categoría de dispositivos

Cuando asocia una recopilación a una categoría de dispositivos, todos los dispositivos de esa categoría se agregan a la recopilación. No se puede agregar una regla de categoría de dispositivos a una colección integrada como **Todos los sistemas**.

1.  En la pestaña **Reglas de pertenencia** del cuadro de diálogo **Propiedades** de una recopilación de dispositivos, seleccione **Agregar regla** > **Regla de categoría de dispositivos**.
2.  En el cuadro de diálogo **Seleccionar categorías de dispositivos**, seleccione una o más categorías de dispositivos que se vayan a aplicar a todos los dispositivos de la colección.

## <a name="change-the-category-of-a-device"></a>Cambiar la categoría de un dispositivo

1.  En **Activos y compatibilidad** > **Información general** > **Dispositivos**, seleccione un dispositivo de la lista **Dispositivos**.
2.  En la pestaña **Inicio**, en el grupo **Dispositivo**, seleccione **Cambiar categoría**.
3.  Elija una categoría y después haga clic en **Aceptar**.

## <a name="view-which-category-a-device-belongs-to"></a>Ver a qué categoría pertenece un dispositivo

En **Activos y compatibilidad** > **Información general** > **Dispositivos**, en la lista **Dispositivos**, la categoría se muestra en la columna **Categoría de dispositivos**.

Si la columna **Categoría de dispositivos** no aparece, haga clic con el botón derecho en el encabezado de una de las columnas de la lista **Dispositivos** (como **Nombre**) y seleccione **Categoría de dispositivos**.

Si asigna un dispositivo a una categoría y posteriormente elimina la categoría, el informe **Lista de dispositivos inscritos en Microsoft Intune por usuario** mostrará un GUID en la columna **Categoría de dispositivos** en lugar de un nombre de categoría.
