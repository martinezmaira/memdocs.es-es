---
title: Cómo analizar y convertir paquetes
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo analizar y convertir paquetes con el Administrador de conversión de paquetes en Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f72e7330909bc5653e69790e38ae043e539cc239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689043"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Cómo analizar y convertir paquetes con el Administrador de conversión de paquetes

*Se aplica a: Configuration Manager (rama actual)*

<!--1357861-->

Para poder convertir un paquete, primero analícelo. Según los resultados del análisis, puede efectuar una de las siguientes tareas:

- **Convertir** el paquete a una aplicación. En la lista **Paquete** de la consola, el estado de disponibilidad es **Automático**.  

- **Corregir y convertir** el paquete, adjuntar colecciones y crear condiciones globales. En la lista **Paquete** de la consola, el estado de disponibilidad es **Automático**.  

- **Corregir y convertir** el paquete. En la lista **Paquete** de la consola, el estado de disponibilidad es **Manual**.  

- Dejar el paquete sin convertir. En la lista **Paquete** de la consola, el estado de disponibilidad es **No disponible**.  



## <a name="how-to-analyze-packages"></a><a name="bkmk_analyze"></a> Cómo analizar los paquetes

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**.  

2. Seleccione el paquete que desea convertir. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Conversión de paquetes**, seleccione **Analizar paquete**. El Administrador de conversión de paquetes analiza el paquete.  

3. Para ver el estado de preparación del paquete, agregue la columna **Preparación** a la lista de paquetes. El estado de preparación del paquete determina la acción siguiente:  

    - **Automático**: [procedimiento para convertir los paquetes](#bkmk_convert)  

        Para adjunta también colecciones y crear condiciones globales con un estado de preparación **Automático**, vea [Cómo corregir y convertir paquetes](#bkmk_fix).  

    - **Manual**: [procedimiento para corregir y convertir los paquetes](#bkmk_fix)

    - **No aplicable**: a este paquete le falta contenido necesario o un programa. Agregue cualquier contenido o los programas que faltan y vuelva a intentar el análisis. O bien déjelo en un estado sin convertir y siga implementándolo como paquete.  

    - **Desconocido**: primero ejecute la tarea de **análisis** o espere al siguiente análisis programado. Si el estado no cambia, vea [Solución de problemas del Administrador de conversión de paquetes](troubleshoot-pcm.md).<!-- SCCMDocs#2044 -->

## <a name="how-to-convert-packages"></a><a name="bkmk_convert"></a> Cómo convertir los paquetes

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**.  

2. Seleccione el paquete que desea convertir con un estado de preparación **Automático**. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Conversión de paquetes**, seleccione **Convertir paquete**. Se abre el asistente para convertir paquetes en aplicaciones.  

3. En el asistente para convertir paquetes en aplicaciones, revise la lista de paquetes seleccionados. Quite todos los paquetes que no desea convertir y luego seleccione **Aceptar**. El Administrador de conversión de paquetes convierte el paquete. En la ventana Conversión completada se muestra el estado de conversión de las nuevas aplicaciones.  

    > [!Note]  
    > Al convertir un paquete, el sitio registra la fecha y hora de la conversión como la hora UTC.  

4. Siga las instrucciones de la ventana. Seleccione **Ver aplicaciones** o **Cerrar**.  



## <a name="how-to-fix-and-convert-packages"></a><a name="bkmk_fix"></a> Cómo corregir y convertir los paquetes

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**.  

2. Seleccione un paquete con un estado de preparación **Manual** o **Automático**. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Conversión de paquetes**, seleccione **Corregir y convertir**.  

3. En el Asistente para la conversión de paquetes, revise la información de la página **Selección de paquetes**, teniendo en cuenta los **elementos de corrección**. A continuación, seleccione **Siguiente**.  

4. En la página **Revisión de dependencias**, revise si el paquete depende de otros paquetes indicados y luego seleccione **Siguiente**.  

    > [!Note]  
    > Si no ha convertido ninguno de los paquetes dependientes indicados, primero conviértalos. A continuación, reinicie el proceso de conversión de paquetes.  
    >  
    > Si no se requiere ninguna dependencia, elimínela o ignórela y continúe con el proceso de conversión.  

5. En la página **Tipo de implementación**, revise los tipos de implementación de la nueva aplicación. Cambie sus propiedades o elimine los tipos de implementación.  

6. Si cualquiera de los nuevos tipos de implementación no tiene un método de detección asociado, en la columna **Método de detección** aparece un icono de advertencia. Complete las siguientes acciones:  

    1. Seleccione **Editar método de detección**.  

    2. Seleccione **Agregar**.  

    3. En el cuadro Regla de detección, especifique un **tipo de configuración**.  

    4. Para el tipo de configuración especificado, escriba la información adicional necesaria para la regla de detección.  

    5. Seleccione **Aceptar**. Si es necesario, repita este proceso para agregar varios métodos de detección a cada tipo de implementación.  

    6. Seleccione **Aceptar**. Verifique si en la columna **Método de detección** aparece un icono para confirmar un método de detección correctamente especificado.  

7. Seleccione **Siguiente**.  

8. En la página **Selección de requisitos**, revise los tipos de implementación de la nueva aplicación. Seleccione un tipo de implementación y revise los requisitos para dicho tipo de implementación.  

    > [!Note]  
    > El asistente solo muestra los requisitos que el Administrador de conversión de paquetes convierte. No convierte todas las consultas WQL de las colecciones de dispositivos en requisitos.  

9. Agregue los requisitos para un tipo de implementación seleccionado, si es necesario.  

10. Seleccione **Siguiente**.  

11. Complete el asistente para crear la aplicación.  

    > [!Note]  
    > Al convertir un paquete, el sitio registra la fecha y hora de la conversión como la hora UTC.  



## <a name="monitor"></a><a name="bkmk_monitor"></a> Supervisar

Vaya al área de trabajo **Supervisión** de la consola de Configuration Manager y seleccione **Estado de conversión del paquete**. En este panel se muestra el análisis general y el estado de conversión de los paquetes del sitio. Los datos de análisis se resumen automáticamente mediante una nueva tarea en segundo plano.

> [!Tip]  
> El Administrador de conversión de paquetes integrado con Configuration Manager no requiere que se programe el análisis de paquetes. Esta acción la controla la tarea de resumen integrada.

![Captura de pantalla del panel de ejemplo de Estado de conversión de paquetes](media/1357861-pcm-dashboard.png)
