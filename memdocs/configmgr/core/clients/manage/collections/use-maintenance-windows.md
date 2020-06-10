---
title: Uso de ventanas de mantenimiento
titleSuffix: Configuration Manager
description: Use recopilaciones y ventanas de mantenimiento para administrar eficazmente los clientes en Configuration Manager.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b81599c6c5e4dda418b69c6e3c6d3b8cd144253
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428550"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Cómo usar las ventanas de mantenimiento en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use ventanas de mantenimiento para definir cuándo Configuration Manager puede ejecutar tareas que afectan en los dispositivos. Las ventanas de mantenimiento ayudan a garantizar que los cambios en la configuración de cliente se produzcan en momentos que no afecten a la productividad. Con el Centro de software, los usuarios pueden ver la próxima ventana de mantenimiento del dispositivo en la pestaña **Estado de la instalación**. <!--1358131-->

Las tareas siguientes admiten ventanas de mantenimiento:

- Implementaciones de aplicaciones y paquetes

- Implementaciones de actualización de software

- Implementación y evaluación de la configuración de cumplimiento

- Implementaciones de secuencias de tareas personalizadas y de sistema operativo

Configure ventanas de mantenimiento con una fecha de vigencia, una hora de inicio y de finalización y un patrón de periodicidad. La duración máxima de una ventana tiene que ser inferior a 24 horas. La consola no permite una ventana de mantenimiento única durante más de 24 horas. Por ejemplo, si quiere permitir el mantenimiento todos los días sábado y domingo, cree dos ventanas de mantenimiento de 24 horas para cada día.<!-- MEMDocs#310 -->

De manera predeterminada, los reinicios de equipo ocasionados por una implementación no se permiten fuera de una ventana de mantenimiento, pero se puede invalidar el valor predeterminado. Las ventanas de mantenimiento solo afectan la hora a la que se ejecuta la implementación. Las implementaciones que están configuradas para descargarse y ejecutarse localmente pueden descargar contenido fuera de la ventana.

Si un cliente es miembro de una colección de dispositivos que tiene una ventana de mantenimiento, una implementación solo se ejecuta si el tiempo de ejecución máximo permitido no supera la duración de la ventana. Si la implementación no se puede ejecutar, el cliente genera una alerta. Luego vuelve a ejecutar la implementación durante la ventana de mantenimiento programada siguiente que tenga tiempo disponible.

## <a name="multiple-maintenance-windows"></a>Varias ventanas de mantenimiento

Si un equipo cliente forma parte de varias recopilaciones de dispositivos que tienen ventanas de mantenimiento, se aplican estas reglas:  

- Si las ventanas de mantenimiento no se superponen, el cliente las trata como dos ventanas de mantenimiento independientes.

- Si las ventanas de mantenimiento se superponen, el cliente las trata como una sola ventana para todo el tiempo de ambas ventanas. Por ejemplo, se crean dos ventanas de mantenimiento en una colección. La primera es efectiva entre 6:00 y 7:00 y la segunda, de 6:30 a 7:30. Dado que se superponen en 30 minutos, la duración efectiva de la ventana de mantenimiento combinada es de 90 minutos, de 6:00 a 7:30.

Cuando un usuario instala una aplicación desde el Centro de software, el cliente la inicia de inmediato. Da prioridad a la intención del usuario por sobre la del administrador.

Si la implementación de una aplicación con un propósito de **Requerido** alcanza su fecha límite de instalación fuera del horario laboral que un usuario configura en el Centro de software, el cliente instala la aplicación. Da prioridad a la intención del administrador por sobre la del usuario.

De manera predeterminada, con varias ventanas de mantenimiento, el cliente solo instala actualizaciones de software durante las ventanas de tipo **Actualización de software**. Omite cualquier ventana de mantenimiento de tipo **Todas las implementaciones**, a menos que sean el único tipo. Puede configurar este comportamiento con la configuración de cliente siguiente en el grupo **Actualizaciones de software**: **Habilitar la instalación de actualizaciones de software en la ventana de mantenimiento "Todas las implementaciones" cuando esté disponible la ventana de mantenimiento "Actualización de software"** . Para más información, vea [Acerca de la configuración de cliente](../../deploy/about-client-settings.md#bkmk_SUMMaint).<!-- SCCMDocs#1317 -->

> [!NOTE]
> Esta opción también es válida en las ventanas de mantenimiento que se configuren para aplicarse a **secuencias de tareas**.<!-- SCCMDocs-pr #4596 -->
>
> Si el cliente solo tiene una ventana **Todas las implementaciones** disponible, sigue instalando las actualizaciones de software o las secuencias de tareas en esa ventana.

## <a name="configure-maintenance-windows"></a>Configuración de ventanas de mantenimiento

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**.

1. Seleccione el nodo **Colecciones de dispositivos** y luego seleccione una colección.

    > [!NOTE]
    > No se pueden crear ventanas de mantenimiento para la colección **Todos los sistemas**.

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.

1. Cambie a la pestaña **Ventana de mantenimiento** y seleccione el icono **Nuevo**.

    1. Especifique un **Nombre** para identificar de manera única esta ventana de mantenimiento para la colección.

    1. Configure los valores de **Tiempo**:

        - **Fecha de vigencia**: fecha en la que se inicia la ventana de mantenimiento. La fecha predeterminada es la actual.

        - **Inicio** y **Finalización**: horas de inicio y finalización de la ventana de mantenimiento. Calcula la **Duración** de la ventana. La duración mínima es de cinco minutos y la máximo es de 24 horas. La duración predeterminada es de tres horas, de 01:00 a 04:00.

        - **Hora universal coordinada (UTC)** : habilite esta opción para que el cliente interprete las horas de inicio y finalización en la zona horaria UTC. En el caso de los dispositivos distribuidos de forma regional o global en la misma colección, esta opción establece la ventana de mantenimiento para que se produzca simultáneamente en todos los dispositivos de la colección. Deshabilite esta opción para que el cliente use la zona horaria local del dispositivo. Esta opción está deshabilitada de forma predeterminada.

    1. Configure la programación de periodicidad. El valor predeterminado es una vez por semana en el día actual de la semana.

    1. **Aplicar esta programación a**: de manera predeterminada, la ventana se aplica a **Todas las implementaciones**. Puede seleccionar **Actualizaciones de software** o **Secuencias de tareas** para controlar mejor qué implementaciones se ejecutan durante esta ventana.

        > [!TIP]
        > Si configura varias ventanas de mantenimiento de distintos tipos en la misma colección, asegúrese de entender los comportamientos del cliente. Para más información, consulte [Varias ventanas de mantenimiento](#multiple-maintenance-windows).

1. Seleccione **Aceptar** para guardar y cerrar la ventana.

En la pestaña **Ventanas de mantenimiento** de las propiedades de la colección se muestran todas las ventanas configuradas.

## <a name="use-powershell"></a><a name="bkmk_powershell"></a> Uso de PowerShell

PowerShell puede usarse para configurar ventanas de mantenimiento. Vea los siguientes artículos para más información:

- [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow?view=sccm-ps)
- [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow?view=sccm-ps)
- [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow?view=sccm-ps)
- [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow?view=sccm-ps)
