---
title: Configuración de alertas de Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga más información sobre cómo configurar alertas de Endpoint Protection en Configuration Manager.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 55877923ae2e9a7aa47b3ebe774f7dc0e4ea21a4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697343"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configurar alertas de Endpoint Protection en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

 Puede configurar alertas de Endpoint Protection en Microsoft Configuration Manager para enviar notificaciones a los usuarios administrativos cuando se producen eventos específicos, como una infección de malware en su jerarquía. Las notificaciones se muestran en el panel de Endpoint Protection en la consola de Configuration Manager, en el nodo **Alertas** del área de trabajo **Supervisión**. También se pueden enviar por correo electrónico a los usuarios especificados.

 Use los siguientes pasos y procedimientos adicionales de este tema para configurar las alertas de Endpoint Protection en Configuration Manager.

> [!IMPORTANT]
>  Debe tener el permiso **Aplicar seguridad** para que las recopilaciones configuren las alertas de Endpoint Protection.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Pasos para configurar alertas de Endpoint Protection en Configuration Manager

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.

3.  En la lista **Recopilaciones de dispositivos** , seleccione la recopilación para la que quiere configurar las alertas y luego, en la pestaña **Inicio** del grupo **Propiedades** , haga clic en **Propiedades**.

    > [!NOTE]
    >  No puede configurar alertas para recopilaciones de usuario.

4.  En la pestaña **Alertas** del cuadro de diálogo _<Nombre de recopilación\>_ **Propiedades**, seleccione **Ver esta recopilación en el panel de Endpoint Protection** si quiere ver los detalles de las operaciones de antimalware realizadas para esta recopilación en el área de trabajo **Supervisión** de la consola de Configuration Manager.

    > [!NOTE]
    >  Esta opción no está disponible para la recopilación **Todos los sistemas** .

5.  En la pestaña **Alertas** del cuadro de diálogo _<Nombre de recopilación\>_ **Propiedades**, haga clic en **Agregar**.

6.  En el cuadro de diálogo **Agregar nuevas alertas de recopilación**, en la sección **Generate an alert when these conditions apply** (Generar una alerta si se cumplen estas condiciones), seleccione las alertas que quiere que Configuration Manager genere cuando se produzcan los eventos de Endpoint Protection especificados y después haga clic en **Aceptar**.

7.  En la lista **Condiciones** de la pestaña **Alertas**, seleccione cada alerta de Endpoint Protection y luego especifique la información siguiente:

    -   **Nombre de alerta**: acepte el nombre predeterminado o escriba un nombre nuevo para la alerta.

    -   **Gravedad de alerta**: en la lista, seleccione el nivel de alerta que se va a mostrar en la consola de Configuration Manager.

8.  En función de la alerta que seleccione, especifique la siguiente información adicional:

    -   **Detección de malware**: esta alerta se genera si se detecta malware en cualquier equipo de la recopilación que se supervisa. **Umbral de detección de malware**: especifica los niveles de detección de malware en los que se genera esta alerta.

        -   **Alta: todas las detecciones**: la alerta se genera cuando se detecta cualquier malware en uno o varios equipos de la recopilación especificada, independientemente de la acción que lleva a cabo el cliente de Endpoint Protection.

        -   **Media: detectada, pendiente de acción**: la alerta se genera cuando se detecta malware en uno o varios equipos de la recopilación especificada y es necesario quitarlo manualmente.

        -   **Baja: detectada, todavía activa**: la alerta se genera cuando se detecta malware en uno o varios equipos de la recopilación especificada y aún está activo.

    -   **Ataque de malware**: esta alerta se genera si se detecta el malware especificado en un porcentaje específico de equipos de la recopilación que se supervisa.

        -   **Porcentaje de equipos con malware detectado**: la alerta se genera cuando el porcentaje de equipos con malware detectado en la recopilación supera el porcentaje que indique. Especifique un porcentaje entre **1** y **99**.

            > [!NOTE]
            >  El valor de porcentaje se basa en el número de equipos de la recopilación, pero excluye los equipos que no tienen instalado un cliente de Configuration Manager. Incluye equipos que aún no tienen instalado el cliente de Endpoint Protection.

    -   **Detección reiterada de malware**: esta alerta se genera si se detecta malware específico más veces que las especificadas durante un determinado número de horas en los equipos de la recopilación que se supervisa. Especifique la siguiente información para configurar la alerta:

        -   **Número de veces que se ha detectado malware** : la alerta se genera cuando se detecta el mismo malware en los equipos de la recopilación más veces que las establecidas. Especifique un número entre **2** y **32**.

        -   **Intervalo de detección (horas):** indique el intervalo de detección (en horas) en que se debe producir el número de detecciones de malware. Especifique un número entre **1** y **168**.

    -   **Detección de varios programas de malware**: esta alerta se genera si se detectan más tipos de malware que el número de tipos especificado durante un determinado número de horas en los equipos de la recopilación que se supervisa. Especifique la siguiente información para configurar la alerta:

        -   **Número de tipos de malware detectados:** la alerta se genera cuando el número establecido de tipos de software malintencionado se detecta en los equipos de la recopilación. Especifique un número entre **2** y **32**.

        -   **Intervalo de detección (horas):** indique el intervalo de detección (en horas) en que se debe producir el número de detecciones de malware. Especifique un número entre **1** y **168**.

9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo _<Nombre de la recopilación\>_ **Propiedades**.  

## <a name="alert-for-outdated-malware-client"></a>Alerta para clientes de malware obsoletos

A partir de la versión 1702 de Configuration Manager, puede configurar una alerta para asegurarse de que los clientes de Endpoint Protection no están obsoletos. Desde cualquier colección de dispositivos, ya puede agregar columnas a la lista para estos atributos: **Versión del cliente antimalware** y **Estado de la implementación de Endpoint Protection**. Por ejemplo, en la consola vaya a **Activos y compatibilidad** > **Información general** > **Recopilaciones de dispositivos** > **Todos los clientes de escritorio y servidor**. Haga clic con el botón derecho en el encabezado de columna y seleccione esas columnas para agregarlas. Para comprobar una alerta, vea **Alertas** en el área de trabajo **Supervisión**. Si más de un 20 % de los clientes administrados ejecutan una versión expirada del software antimalware, la versión de cliente de antimalware está obsoleta y se muestra la alerta. Esta alerta no aparece en la pestaña **Supervisión** > **Información general**. Para actualizar los clientes antimalware expirados, habilite las actualizaciones de software para los clientes antimalware.

Para configurar el porcentaje en el que se genera la alerta, expanda **Supervisión** > **Alertas** > **Todas las alertas**, haga doble clic en **Clientes antimalware obsoletos** y modifique la opción **Generar alerta si el porcentaje de clientes administrados con una versión obsoleta del cliente antimalware es más de**.

> [!div class="button"]
> [Paso siguiente >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [Atrás >](endpoint-protection-site-role.md)
