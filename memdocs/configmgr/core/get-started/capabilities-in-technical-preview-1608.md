---
title: Funcionalidades de Technical Preview 1608
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1608.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074187"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Funciones de Technical Preview 1608 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1608 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager.      Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    


**Estas son las nuevas características que puede probar con esta versión.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Mejoras en el paso Preparar cliente de Configuration Manager para la captura de la secuencia de tareas  
El paso Preparar el cliente de Configuration Manager quitará por completo el cliente de Configuration Manager en lugar de quitar solo la información de clave. Cuando la secuencia de tareas implementa la imagen capturada del sistema operativo, se instala un nuevo cliente de Configuration Manager cada vez.  


## <a name="improvements-to-software-center"></a>Mejoras en el Centro de software
* Las pestañas **Aplicaciones**, **Actualizaciones** y **Sistemas operativos** del Centro de software ahora muestran el software agregado recientemente. Los números del panel de navegación muestran cuántos elementos nuevos de software hay en cada pestaña.
* Los usuarios ahora pueden solicitar aprobación para aplicaciones y luego ver el historial de solicitudes en la vista **Detalles de la aplicación** del Centro de Software. El botón **Solicitar** de **Detalles de la aplicación** ya no redirige al catálogo de aplicaciones basado en web.

## <a name="improvements-to-asset-intelligence"></a>Mejoras en Asset Intelligence
Se ha agregado un campo a las propiedades del software inventariado que permite establecer una relación de elementos primarios y secundarios con otro software. Así, en la lista Software inventariado, puede ver el elemento primario de cualquier software y también ocultar todo el software secundario.

### <a name="configure-a-parent-to-child-relationship"></a>Configurar una relación de elementos primarios y secundarios
  1. Para establecer el software primario, en el nodo Software inventariado, haga clic con el botón derecho en un elemento de software de la lista **Software inventariado** y elija **Propiedades**.
  2. En el cuadro de diálogo que se abre, seleccione el software que quiere establecer como software primario para la selección inicial.

### <a name="filter-the-software-display"></a>Filtrar la visualización de software
Después de haber definido las relaciones de elementos primarios y secundarios, puede filtrar la vista para mostrar solo el software primario o que no tiene ninguna relación definida. Con esto se oculta todo el software establecido como secundario de otro software inventariado. Para ello:
   1. En la barra de búsqueda, elija **Agregar criterios**
   2. Seleccione **Software primario** y luego cambie el valor del criterio a **está vacío**; después, haga clic en **Buscar**.

Ahora la vista solo muestra los elementos de software primarios o el software que no tiene ninguna relación definida. No se muestra el software que es solo un secundario de otro título.

## <a name="remote-control-keyboard-translation"></a>Traducción de teclado de control remoto
Anteriormente, Configuration Manager transmitía la posición de la tecla desde la ubicación del lector a la del colaborador. Esto era problemático para las configuraciones de teclado que diferían entre lector y colaborador. Por ejemplo, un lector con un teclado inglés escribiría una "A", pero el teclado francés del colaborador proporcionaría una "Q". Se está modificando el comportamiento predeterminado para que sea el propio carácter el que se transmita desde el teclado del lector al del colaborador y para que sea lo que el lector intenta escribir lo que llegue al colaborador.

El lector puede desactivar este comportamiento si prefiere escribir conforme a la disposición de teclado del colaborador. Para cambiar el comportamiento, en **Control remoto de Configuration Manager**, elija **Acción** y luego **Habilitar traducción del teclado** para transmitir la posición de las teclas.

> [!NOTE]
>
> Las teclas especiales, como ~!#@$%, no se traducirán correctamente.
