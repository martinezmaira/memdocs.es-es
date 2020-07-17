---
title: Supervisión de la configuración de cumplimiento
titleSuffix: Configuration Manager
description: Siga uno o varios de los procedimientos de este tema para mostrar el estado de cumplimiento de la línea base de configuración.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: e2a378c1f54eb9bccbcc21f50419176bd39cb3ac
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240055"
---
# <a name="monitor-compliance-settings-in-configuration-manager"></a>Supervisión de la configuración de cumplimiento en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de haber implementado líneas base de configuración de Configuration Manager en los dispositivos de la jerarquía, puede usar uno o varios de los procedimientos de este tema para mostrar el estado de cumplimiento de la línea base de configuración:

> [!NOTE]  
>  Los campos de criterios de validación en los informes de configuración de cumplimiento (el equivalente en el informe del cliente es **Restricciones**) muestran el SML (Service Modeling Language) subyacente. Esto puede hacer que sea difícil para los administradores que han creado el elemento de configuración en la consola de Configuration Manager comprender cuáles son los criterios de validación si no tienen conocimiento de SML. En este caso, use el área de trabajo **Supervisión** en la consola de Configuration Manager para ver las propiedades del elemento de configuración y sus criterios de validación.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver los resultados de cumplimiento en la consola de Configuration Manager  
 Use este procedimiento para ver los detalles sobre el cumplimiento de líneas base de configuración implementadas en la consola de Configuration Manager.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver los resultados de cumplimiento en la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Supervisión** > **Implementaciones**.  

3.  En la lista **Implementaciones** , seleccione la implementación de línea base de configuración para la que quiere revisar la información de cumplimiento.  

4.  Puede revisar la información de resumen sobre el cumplimiento de la implementación de la línea base de configuración en la página principal. Para ver información más detallada, seleccione la implementación de la línea base de configuración y, a continuación, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Ver estado** para abrir la página **Estado de implementación** .  

     La página **Estado de implementación** contiene las siguientes pestañas:  

    -   **Conforme**: muestra el cumplimiento de la línea de base de configuración según el número de activos afectados. Puede hacer clic en una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos** en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios o dispositivos compatibles con esta regla. El panel **Detalles del activo** muestra los usuarios o dispositivos que son conformes a la línea base de configuración. Haga doble clic en un usuario o dispositivo de la lista para mostrar información adicional.  

        > [!IMPORTANT]  
        >  Una regla de elemento de configuración no se evalúa si no se detecta o no es aplicable en un dispositivo cliente; sin embargo, la regla se devuelve como conforme.  

    -   **Error**: muestra una lista de todos los errores de la implementación de línea de base de configuración seleccionada, según el número de activos afectados. Puede hacer clic en una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos** , en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios o dispositivos que generaron errores con esta regla. Cuando se selecciona un usuario o dispositivo, el panel **Detalles del activo** muestra los usuarios o dispositivos afectados por el problema seleccionado. Haga doble clic en un dispositivo o usuario de la lista para mostrar información adicional sobre el problema.  

    -   **No conforme**: muestra una lista de todas las reglas no conformes en la línea base de configuración según el número de activos afectados. Puede hacer clic en una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos** en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios o dispositivos no compatibles con esta regla. Cuando se selecciona un usuario o dispositivo, el panel **Detalles del activo** muestra los usuarios o dispositivos afectados por el problema seleccionado. Haga doble clic en un usuario o dispositivo de la lista para mostrar información adicional sobre el problema.  

    -   **Desconocido**: muestra una lista de todos los usuarios y dispositivos que no han notificado del incumplimiento de la implementación de línea de base de configuración seleccionada y el estado de cliente actual de los dispositivos.  

5.  En la página **Estado de implementación** , puede revisar la información detallada sobre el cumplimiento de la línea base de configuración implementada. Se crea un nodo temporal en el nodo **Implementaciones** que le permite encontrar esta información rápidamente.  

##  <a name="view-compliance-results-by-using-reports"></a>Visualización de los resultados de compatibilidad mediante informes  
 La configuración de cumplimiento de Configuration Manager incluye una serie de informes integrados que permiten supervisar la información sobre los elementos de configuración, las líneas base de configuración y las implementaciones. Estos informes tienen la categoría de informe de **Administración de compatibilidad y configuración**.  

> [!IMPORTANT]  
>  Debe usar un carácter comodín ( **%** ) para usar los parámetros **Filtro del dispositivo** y Filtro de usuarios en los informes de configuración de cumplimiento.  

 Para obtener más información sobre cómo configurar informes en Configuration Manager, vea [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Visualización de los resultados de cumplimiento en un equipo cliente Windows de Configuration Manager

> [!NOTE]  
>  No se puede ver información sobre el cliente Windows de Configuration Manager si se ha iniciado sesión con una cuenta de invitado del dominio.    

1.  Navegue hasta **Configuration Manager** en el Panel de Control del equipo cliente y haga doble clic para abrir sus propiedades.  

2.  Haga clic en la pestaña **Configuraciones** y vea la lista de líneas base de configuración implementadas.  

3.  Vea el **Estado de compatibilidad** para cada línea base de configuración:  

    > [!IMPORTANT]  
    >  Los resultados de la evaluación se almacenan en caché en el cliente durante 15 minutos. Si inicia una nueva evaluación dentro del período de 15 minutos, se devuelven los resultados de cumplimiento de esta memoria caché en lugar de una nueva evaluación. Por lo tanto, si realiza un cambio en el cliente que podría afectar a los resultados de la evaluación de cumplimiento, espere hasta que hayan transcurrido los 15 minutos antes de iniciar una nueva evaluación.  

    -   **Conforme**: el equipo cliente cumple con la línea de base de configuración evaluada.  

    -   **No conforme**: el equipo cliente no cumple con la línea de base de configuración evaluada.  

    -   **Desconocido**: el equipo cliente todavía no ha evaluado la línea de base de configuración. Si quiere iniciar una evaluación fuera de la programación de evaluación de cumplimiento, seleccione las líneas base de configuración para evaluar y, a continuación, haga clic en **Evaluar**.  

        > [!NOTE]  
        >  Si tiene credenciales de administrador local en el equipo cliente, puede ver detalles de cada línea base de configuración evaluada para determinar qué elemento de configuración está informando de un estado no conforme. Para ello, seleccione la línea base de configuración y, a continuación, haga clic en **Ver informe**.  

4.  Haga clic en **Aceptar**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Creación de recopilaciones basadas en el cumplimiento de línea base de configuración  
 Use el procedimiento siguiente para crear una recopilación de Configuration Manager basada en dispositivos con un cumplimiento especificado. Puede crear recopilaciones basadas en los siguientes estados de cumplimiento:  

-   **Compatible**  

-   **Error**  

-   **Non-compliant**  

-   **Desconocida**  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Líneas base de configuración**.  

3.  En la lista **Líneas de base de configuración** , seleccione la línea base de configuración a partir de la que quiere crear una recopilación.  

4.  En la pestaña **Implementación** , en el grupo **Grupo de implementación**, haga clic en **Crear nueva recopilación** y, a continuación, en la lista desplegable, seleccione el nivel de cumplimiento que quiere para crear una recopilación.  

5.  Se abre el **Asistente para crear recopilación de usuario** o el **Asistente para crear recopilación de dispositivos** , en función de si el elemento de configuración se implementa en usuarios o dispositivos. El asistente se rellena automáticamente con los valores correctos para crear la recopilación; sin embargo, puede editar estos valores.  

6.  Después de completar el asistente, la recopilación se muestra en el nodo **Recopilaciones de usuarios** o **Recopilaciones de dispositivos** en el área de trabajo **Activos y compatibilidad** .  
