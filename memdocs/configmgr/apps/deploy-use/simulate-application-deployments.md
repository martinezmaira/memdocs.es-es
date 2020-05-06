---
title: Simulación de implementaciones de aplicaciones
titleSuffix: Configuration Manager
description: Evalúe el método de detección, los requisitos y las dependencias de un tipo de implementación sin instalar la aplicación.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689983"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Simulación de implementaciones de aplicaciones con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede usar las implementaciones simuladas para probar la implementación de una aplicación sin necesidad de instalar o desinstalar la aplicación. Una implementación simulada evalúa el método de detección, los requisitos y las dependencias de un tipo de implementación. Informa sobre los resultados en el nodo **Implementaciones** del área de trabajo **Supervisión**. Use el procedimiento de este tema para simular una implementación de aplicación en Configuration Manager.  

> [!NOTE]  
> No puede usar implementaciones simuladas para recopilaciones de dispositivos móviles.  
>   
> No puede implementar una aplicación con un propósito de implementación **Desinstalar** si se activó una implementación simulada de la misma aplicación.  

## <a name="configure-a-simulated-application-deployment"></a>Configurar una implementación de aplicación simulada

1.  En la consola de Configuration Manager, seleccione uno de los siguientes:  
    -   Una recopilación de usuarios.  
    -   Una recopilación de dispositivos.  
    -   Una aplicación de Configuration Manager.  

2.  En la pestaña **Inicio**, en el grupo **Implementación**, seleccione **Simular implementación**.  

3.  En el Asistente para simular implementación de aplicación, establezca las siguientes opciones de la implementación simulada:  

    -   **Aplicación**. Seleccione **Examinar** y, después, la aplicación para la que quiere crear una implementación simulada.  

    -   **Recopilación**. Seleccione **Examinar** y, después, la recopilación que quiere usar para la implementación simulada.  

    -   **Acción**. En la lista desplegable, seleccione si quiere simular la instalación o la desinstalación de la aplicación seleccionada.  

    -   **Implementar automáticamente con o sin inicio de sesión del usuario**. Si se activa esta opción, los clientes evalúan la implementación simulada independientemente de si los clientes han iniciado sesión.  

4.  Haga clic en **Siguiente**, revise la información en la página **Resumen** y, después, finalice el asistente para crear la implementación simulada.  

5.  Las aplicaciones simuladas aparecen en el nodo **Implementaciones** del área de trabajo **Supervisión** con el propósito **Simular**. Para más información sobre cómo supervisar implementaciones de aplicaciones, consulte [Supervisar aplicaciones desde la consola de System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  
