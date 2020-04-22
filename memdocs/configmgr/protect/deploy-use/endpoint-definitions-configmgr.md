---
title: Definiciones de malware de Endpoint Protection
titleSuffix: Configuration Manager
description: Aprenda a configurar las actualizaciones de software en Configuration Manager para entregar las actualizaciones de definiciones a los equipos cliente.
ms.date: 10/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 16dce8e11edbe41dda3dcbf0fd503374ce05bf83
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697263"
---
#  <a name="using-configuration-manager-software-updates-to-deliver-definition-updates"></a>El uso de las actualizaciones de Software de Configuration Manager para entregar actualizaciones de definiciones

*Se aplica a: Configuration Manager (rama actual)*


 Puede configurar las actualizaciones de software en Configuration Manager para entregar las actualizaciones de definiciones a los equipos cliente. Esto se hace mediante la configuración de reglas de implementación automática. Antes de empezar a crear reglas de implementación automática, asegúrese de que ha configurado las actualizaciones de software de Configuration Manager. Para obtener más información, vea [Introducción a las actualizaciones de software](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
>  Este procedimiento solo es válido para los elementos que deben configurarse específicamente para Endpoint Protection. Para obtener más información sobre el Asistente para crear regla de implementación automática, consulte [Automatically deploy software updates](../../sum/deploy-use/automatically-deploy-software-updates.md) (Implementar actualizaciones de software automáticamente).

## <a name="to-configure-an-automatic-deployment-rule-to-deliver-definition-updates"></a>Para configurar una regla de implementación automática destinada a entregar actualizaciones de definiciones

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.

2. En el área de trabajo **Biblioteca de software** , expanda **Actualizaciones de software**y haga clic en **Reglas de implementación automática**.

3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear regla de implementación automática**.

4. En la página **General** del **Asistente para crear regla de implementación automática**, especifique la información siguiente:

   -   **Nombre**: escriba un nombre único para la regla de implementación automática.

   -   **Colección**: seleccione la recopilación de equipos cliente en la que va a implementar las actualizaciones de definiciones.

       > [!NOTE]
       >  No se pueden implementar actualizaciones de definiciones en una recopilación de usuarios.

5. Haga clic en **Agregar a un grupo de actualizaciones de software existente**.

6. Asegúrese de que está activada la casilla  **Habilitar la implementación después de ejecutar la regla** y luego haga clic en **Siguiente**.

7. En la página **Configuración de implementación** del asistente, en la lista **Nivel de detalle**, seleccione **Solo mensajes de error** y haga clic en **Siguiente**.

   > [!NOTE]
   >  Al seleccionar **Solo mensajes de error** se reducirá el número de mensajes de estado que se devuelven en la implementación de definición. Esta configuración ayuda a reducir el uso del procesamiento de la CPU en los servidores de Configuration Manager.

8. En la lista **Filtros de propiedad** , seleccione la casilla **Actualizar clasificación** .

9. En la lista **Criterios de búsqueda**, haga clic en **<elementos que buscar\>** . A continuación, en el cuadro de diálogo **Criterios de búsqueda** , en la lista **Especifique el valor que se va a buscar** , seleccione **Actualizaciones de definiciones**.

10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Criterios de búsqueda** .

11. En la lista **Filtros de propiedad** , active la casilla **Producto** .

12. En la lista **Criterios de búsqueda**, haga clic en **<elementos que buscar\>** . A continuación, en el cuadro de diálogo **Criterios de búsqueda** , en la lista **Especifique el valor que se va a buscar** , seleccione **Forefront Endpoint Protection 2010** para Windows 8.1 y versiones anteriores o **Windows Defender** para Windows 10 y versiones posteriores.

13. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Criterios de búsqueda** y haga clic en **Siguiente**.

14. Si quiere, puede filtrar las actualizaciones reemplazadas.   Para ello:
    1.  En la lista **Filtros de propiedad** , active la casilla **Se reemplazó** .
    2.  En la lista **Criterios de búsqueda**, haga clic en **<elementos que buscar\>** . A continuación, en el cuadro de diálogo **Criterios de búsqueda** , en la lista **Especifique el valor que se va a buscar** , seleccione **No**.  <br><br>

15. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Criterios de búsqueda** y haga clic en **Siguiente**.

16. En la página **Programación de evaluación** del asistente, seleccione **Habilitar regla para que se ejecute según una programación**y después configure la programación que se va a usar para descargar actualizaciones de definiciones. Como mínimo, establezca la regla para que se ejecute dos horas después de cada sincronización de punto de actualización de software. Haga clic en **Siguiente**.

17. En la página **Programación de implementación** , configure las siguientes opciones:

    -   **Hora basada en:** seleccione **UTC** si quiere que todos los clientes de la jerarquía instalen las definiciones más recientes a la misma hora. La hora real de la instalación variará dentro de una ventana de dos horas. Esta opción es un procedimiento recomendado.

    -   **Horas de disponibilidad del software**: especifique las horas disponibles para la implementación que se crea mediante esta regla. La hora especificada debe ser al menos una hora después de que se ejecute la regla de implementación automática. Esto ayuda a garantizar que el contenido tiene suficiente tiempo para replicarse en los puntos de distribución de la jerarquía. Es probable que algunas actualizaciones de definición también incluyan actualizaciones del motor de antimalware, que podrían tardar más tiempo en llegar a los puntos de distribución.

    -   **Fecha límite de instalación**: Seleccione **Lo antes posible**.

        > [!NOTE]
        >  Las fechas límite de actualización de software varían durante un período de dos horas para impedir que todos los clientes soliciten una actualización al mismo tiempo.

18. Haga clic en **Siguiente**.

19. En la página **Experiencia del usuario** del asistente, en la lista **Notificaciones de usuario** , seleccione **Ocultar en el Centro de software y ocultar todas las notificaciones**.   Esto garantiza que las actualizaciones de definiciones se instalen de forma silenciosa. Haga clic en **Siguiente**.

20. En la página **Alertas** del asistente, no es necesario configurar alertas. Endpoint Protection en Configuration Manager genera las alertas que sean necesarias. Haga clic en **Siguiente**.

21. En la página **Paquete de implementación** del asistente, seleccione un paquete de implementación existente o cree uno nuevo que contenga los archivos de actualización de software asociados a la regla.

    > [!NOTE]
    >  Considere la posibilidad de colocar las actualizaciones de definición en un paquete que no contenga otras actualizaciones de software. Con esta estrategia se mantiene un tamaño más pequeño de paquete de actualización de definiciones, lo que permite que se replique en los puntos de distribución más rápidamente.

22. Si crea un nuevo paquete, en la página **Puntos de distribución** del asistente, seleccione uno o varios puntos de distribución a los que se va a copiar el contenido de este paquete y luego haga clic en **Siguiente**.

23. En la página **Ubicación de descarga** del asistente, seleccione **Descargar actualizaciones de software de Internet**y haga clic en **Siguiente**.

24. En la página **Selección del idioma** del asistente, seleccione cada versión de idioma de las actualizaciones que se van a descargar y luego haga clic en **Siguiente**.

25. En la página **Configuración de descarga** del asistente, seleccione el comportamiento de descarga de actualizaciones de software necesario y luego haga clic en **Siguiente**.

26. En la página **Resumen** del asistente, revise la configuración y después haga clic en **Siguiente**.

26. Complete el Asistente para crear regla de implementación automática.

27. Compruebe que la nueva regla se muestra en el nodo **Reglas de implementación automática** de la consola de Configuration Manager.


> [!div class="button"]
> [Paso siguiente >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Atrás >](endpoint-configure-alerts.md)
