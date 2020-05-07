---
title: Definiciones de malware de Endpoint Protection
titleSuffix: Configuration Manager
description: Aprenda a configurar las actualizaciones de software en Configuration Manager para entregar las actualizaciones de definiciones a los equipos cliente.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126079"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>Uso de Configuration Manager para entregar actualizaciones de definiciones

*Se aplica a: Configuration Manager (rama actual)*

Puede configurar las actualizaciones de software en Configuration Manager para entregar de forma automática actualizaciones de definiciones a los equipos cliente. Antes de empezar a crear reglas de implementación automática, asegúrese de que configura las actualizaciones de software de Configuration Manager. Para obtener más información, vea [Introducción a las actualizaciones de software](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
> Este procedimiento es específico de Endpoint Protection. Para obtener información más general sobre las reglas de implementación automática, vea [Implementación automática de actualizaciones de software](../../sum/deploy-use/automatically-deploy-software-updates.md).

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Actualizaciones de software** y, después, seleccione **Reglas de implementación automática**.

1. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear regla de implementación automática**.

1. En la página **General** del **Asistente para crear regla de implementación automática**, especifique la información siguiente:

    - **Nombre**: escriba un nombre único para la regla de implementación automática.

    - **Colección**: seleccione la colección de dispositivos en la que quiera implementar las actualizaciones de definiciones.

        > [!NOTE]
        > Las actualizaciones de definiciones no se pueden implementar en una colección de usuarios.

1. Seleccione **Agregar a un grupo de actualizaciones de software existente**.

1. Seleccione **Habilitar la implementación después de ejecutar la regla**.

1. En la página **Configuración de implementación** del asistente, en **Nivel de detalle**, seleccione **Solo mensajes de error**.

    > [!NOTE]
    > Al seleccionar **Solo mensajes de error**, se reduce el número de mensajes de estado que envía la implementación de la definición. Esta configuración ayuda a reducir el procesamiento de la CPU en los servidores de Configuration Manager.

1. En la página **Actualizaciones de software**:

    1. Seleccione el filtro de propiedades **Clasificación de actualizaciones**. En la lista **Criterios de búsqueda**, seleccione **<elementos que buscar\>** .

        En la ventana **Criterios de búsqueda**, seleccione **Actualizaciones de definiciones** y después **Aceptar**.

    1. Seleccione el filtro de propiedades **Producto**. En la lista **Criterios de búsqueda**, seleccione **<elementos que buscar\>** .

        En la ventana **Criterios de búsqueda**, seleccione **System Center Endpoint Protection** para Windows 8.1 y versiones anteriores, o bien **Windows Defender** para Windows 10 y versiones posteriores, y seleccione **Aceptar**.

    > [!NOTE]
    > Si quiere, puede filtrar las actualizaciones reemplazadas. Seleccione el filtro de propiedades **Reemplazado**. En la lista **Criterios de búsqueda**, seleccione **<elementos que buscar\>** . En la ventana **Criterios de búsqueda**, seleccione **No** y después **Aceptar**.

1. En la página **Programación de evaluación** del asistente, seleccione **Ejecutar la regla después de cualquier sincronización de punto de actualización de software**.

1. En la página **Programación de implementación** , configure las siguientes opciones:

    - **Hora basada en:** si quiere que todos los clientes instalen las definiciones más recientes a la misma hora, seleccione **UTC**. La hora real de la instalación tendrá una variación de dos horas.

    - **Horas de disponibilidad del software**: especifique las horas disponibles para la implementación que crea esta regla. La hora especificada debe ser al menos una hora después de que se ejecute la regla de implementación automática. Esta configuración se asegura de que el contenido tiene tiempo suficiente para replicarse en los puntos de distribución. Es probable que algunas actualizaciones de definición también incluyan actualizaciones del motor de antimalware, que podrían tardar más tiempo en llegar a los puntos de distribución.

    - **Fecha límite de instalación**: Seleccione **Lo antes posible**.

        > [!NOTE]
        > Las fechas límite de actualización de software varían durante un período de dos horas. Este comportamiento impide que todos los clientes soliciten una actualización al mismo tiempo.

1. En la página **Experiencia del usuario** del asistente, en **Notificaciones de usuario**, seleccione **Ocultar en el Centro de software y ocultar todas las notificaciones**. Con esta configuración, las actualizaciones de definiciones se instalan de forma silenciosa.

1. En la página **Paquete de implementación** del asistente, seleccione un paquete de implementación existente o cree uno.

    > [!NOTE]
    > Considere la posibilidad de colocar las actualizaciones de definiciones en un paquete que no contenga otras actualizaciones de software. Con esta estrategia se mantiene un tamaño más pequeño de paquete de actualización de definiciones, lo que permite que se replique en los puntos de distribución más rápidamente.

1. Si crea un paquete de implementación, seleccione uno o varios puntos de distribución en la página **Puntos de distribución** del asistente. El sitio copia el contenido de este paquete en estos puntos de distribución.

1. En la página **Ubicación de descarga**, seleccione **Descargar actualizaciones de software de Internet**.

1. En la página **Selección del idioma**, seleccione cada versión de idioma de las actualizaciones que se van a descargar.

1. En la página **Configuración de descarga**, seleccione el comportamiento de descarga de las actualizaciones de software necesario.

1. Complete el asistente.

Compruebe que en el nodo **Reglas de implementación automática** de la consola de Configuration Manager se muestra la nueva regla.

> [!div class="nextstepaction"]
> [Creación e implementación de directivas antimalware](endpoint-antimalware-policies.md)
