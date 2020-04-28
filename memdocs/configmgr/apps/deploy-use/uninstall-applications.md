---
title: Desinstalar aplicaciones
titleSuffix: Configuration Manager
description: Desinstalación de una aplicación mediante Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d9b5152c094ecc1470f748c57f2831cfdd66474
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075853"
---
# <a name="uninstall-applications-with-configuration-manager"></a>Desinstalación de aplicaciones con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


Realice las acciones siguientes para desinstalar una aplicación que haya implementado.

-   Especifique la línea de comandos para desinstalar el contenido del tipo de implementación en la página **Contenido** del Asistente para crear tipos de implementación.  

-   Implemente la aplicación mediante la acción de implementación **Desinstalar**.  

> [!IMPORTANT]  
> Algunos tipos de aplicaciones no admiten la desinstalación.  

 En esta lista se proporciona más información sobre cómo funciona la desinstalación de la aplicación:  

-   Cuando se desinstala una aplicación de Configuration Manager, las aplicaciones dependientes no se desinstalan de forma automática.  

-   Si implementa una aplicación que usa la acción **Desinstalar** en un usuario y la aplicación se ha instalado para todos los usuarios del equipo, es posible que se produzca un error en la desinstalación si la cuenta de usuario no tiene permisos para desinstalar la aplicación.  

-   Si quita un usuario o un dispositivo de una recopilación que tiene implementada una aplicación, la aplicación no se quitará automáticamente del dispositivo.  

-   Una implementación con el propósito de implementación **Desinstalar** no comprueba las reglas de requisitos. Si la aplicación está instalada en el equipo donde se ejecuta la implementación, se desinstalará.  

> [!IMPORTANT]  
> Para implementar la aplicación con la acción Desinstalar, primero debe eliminar cualquier implementación existente de la aplicación, las implementaciones simuladas o las implementaciones de secuencia de tareas que incluyan esta aplicación. 

 Para obtener más información sobre cómo crear un tipo de implementación, consulte [Crear aplicaciones](../../apps/deploy-use/create-applications.md).  

 Para obtener más información sobre cómo implementar una aplicación, consulte [Implementar aplicaciones](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Desinstalar una aplicación  

1.  Configure el tipo de implementación de la aplicación con la línea de comandos de desinstalación mediante alguno de los métodos siguientes:  

    -   En la página **General** del Asistente para crear implementación, seleccione **Identificar automáticamente la información sobre este tipo de implementación a partir de los archivos de instalación**. Si la información está disponible en los archivos de instalación, la línea de comandos de desinstalación se agrega automáticamente a las propiedades del tipo de implementación.  

    -   En la página **Contenido** del Asistente para crear tipos de implementación, en el campo **Programa de desinstalación**, especifique la línea de comandos para desinstalar la aplicación.  

        > [!NOTE]  
        >  La página **Contenido** se muestra solo si selecciona la opción **Especificar manualmente la información del tipo de implementación** en la página **General** del Asistente para crear tipos de implementación.  

    -   En la pestaña **Programas** del cuadro de diálogo **<*Propiedades de <nombre de tipo de implementación*>** , especifique la línea de comandos para desinstalar la aplicación en el campo **Programa de desinstalación**.  

2.  Implemente la aplicación y seleccione la acción de implementación **Desinstalar** en la página **Configuración de implementación** del Asistente para implementar software.  

    > [!NOTE]  
    >  Al seleccionar la acción de implementación **Desinstalar**, el propósito de la implementación se configura automáticamente como **Requerido**.  
