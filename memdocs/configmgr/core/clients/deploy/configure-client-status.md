---
title: Configuración del estado de cliente
titleSuffix: Configuration Manager
description: Seleccione la configuración del estado de cliente en Configuration Manager.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a352e53a672f7fb47416214884fe7adf0fb829cc
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384917"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Cómo configurar el estado de cliente en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para poder supervisar clientes de Configuration Manager y corregir problemas, configure las opciones de estado de cliente del sitio. Esta configuración especifica los parámetros que usa el sitio para marcar los clientes como inactivos. Configure también opciones que le alerten si la actividad de los clientes cae por debajo de un umbral especificado.

## <a name="configure-client-status"></a>Configuración del estado de cliente

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del cliente**. En la pestaña **Inicio** de la cinta, en el grupo **Estado de cliente**, seleccione **Configuración de estado de cliente**.

1. Configure las siguientes opciones:

    > [!NOTE]
    > Si un cliente no cumple ninguno de los valores, el sitio lo marcará como inactivo.

    - **Solicitudes de directiva de cliente durante los días siguientes:** especifique el número de días desde que el cliente solicitó una directiva del sitio. El valor predeterminado es de `7` días.

      Compare este valor con el de la opción **Intervalo de sondeo de directiva de cliente** del grupo **Directiva de cliente** de la configuración de cliente. El valor predeterminado es de 60 minutos. En otras palabras, un cliente debe sondear el sitio con respecto a la directiva cada hora. Si no solicita una directiva después de una semana, el sitio lo marcará como inactivo.

    - **Detección de latidos durante los días siguientes:** especifique el número de días desde que el cliente envió un registro de detección de latido al sitio. El valor predeterminado es de `7` días.

      Compare este valor con el de la programación del [Método de detección de latidos](../../servers/deploy/configure/about-discovery-methods.md). De forma predeterminada, el sitio ejecuta la detección de latidos una vez a la semana.

    - **Inventario de hardware durante los días siguientes:** especifique el número de días desde que el cliente envió un registro de inventario de hardware al sitio. El valor predeterminado es de `7` días.

      Compare este valor con el de **Programación de inventario de hardware** del grupo **Inventario de hardware** de la configuración de cliente. El valor predeterminado es de siete días.

    - **Inventario de software durante los días siguientes:** especifique el número de días desde que el cliente envió un registro de inventario de software al sitio. El valor predeterminado es de `7` días.

      Compare este valor con el de la opción **Programar inventario de software y recopilación de archivos** del grupo **Inventario de software** de la configuración de cliente. El valor predeterminado es de siete días.

    - **Mensajes de estado durante los días siguientes:** especifique el número de días desde que el cliente envió mensajes de estado al sitio. El valor predeterminado es de `7` días. El cliente puede enviar mensajes de estado para diferentes tipos de actividades, como la ejecución de una secuencia de tareas. El sitio elimina los mensajes de estado antiguos como parte de la tarea de mantenimiento **Eliminar mensajes de estado antiguos**.

1. Especifique el valor siguiente para determinar durante cuánto tiempo el sitio mantiene los datos del historial de estado de cliente:

    - **Retener el historial de estado de cliente durante el siguiente número de días:** de forma predeterminada, el sitio mantiene la información de estado de cliente durante `31` días. Esta opción no afecta al comportamiento del cliente ni del sitio. Es similar a una tarea de mantenimiento del historial de estado de cliente.

## <a name="configure-the-schedule"></a>Configuración de la programación

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del cliente**. En la pestaña **Inicio** de la cinta, en el grupo **Estado de cliente**, seleccione **Programar actualización de estado de cliente**.

1. Configure el intervalo en el que quiere que se actualice el estado de cliente.

    > [!NOTE]
    > Al cambiar la programación de las actualizaciones de estado de cliente, dicho cambio no se aplicará hasta la siguiente actualización de estado de cliente programada en la programación anterior.

## <a name="configure-alerts"></a>Configuración de alertas

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Recopilaciones de dispositivos**.

1. Seleccione la recopilación para la que quiera configurar las alertas. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.

    > [!NOTE]
    > no puede configurar alertas para recopilaciones de usuario.

1. Cambie a la pestaña **Alertas** y seleccione **Agregar**.

   > [!TIP]
   > Solo puede ver la pestaña **Alertas** si el rol de seguridad tiene permisos para las alertas.

    Elija las alertas que quiere que el sitio genere para los umbrales de estado de cliente y seleccione **Aceptar**.

1. En la lista **Condiciones** de la pestaña **Alertas**, seleccione cada alerta de estado de cliente y, luego, especifique la información siguiente:

    - **Nombre de alerta**: acepte el nombre predeterminado de la alerta o escriba otro.

    - **Gravedad de alerta**: elija el nivel de alerta que se muestra en la consola de Configuration Manager.

    - **Generar alerta**: especifique el porcentaje de umbral para la alerta.

## <a name="automatic-remediation-exclusion"></a>Exclusión de corrección automática

1. En el equipo cliente en el que quiera deshabilitar la corrección automática, abra el Editor del Registro.

    > [!WARNING]
    > Si utiliza el Editor del Registro incorrectamente, puede causar problemas graves que quizás requieran reinstalar Windows. Microsoft no puede garantizar que pueda resolver problemas ocasionados por un uso incorrecto del Editor del Registro. Úselo bajo su responsabilidad.

1. Desplácese hasta la clave del Registro **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval**.

1. Cambie el valor de la entrada **NotifyOnly**:

    - `TRUE`: el cliente no corregirá automáticamente los problemas que encuentre. El sitio continuará notificando cualquier problema con este cliente en el área de trabajo **Supervisión**.

    - `FALSE`: Esta configuración es la predeterminada. El cliente corrige automáticamente los problemas cuando los encuentra, y el sitio se lo notifica en el área de trabajo **Supervisión**.

Al instalar clientes, puede excluirlos de la corrección automática mediante la propiedad de instalación **NotifyOnly**. Para obtener más información, vea [Información sobre las propiedades de instalación de clientes](about-client-installation-properties.md).

## <a name="next-steps"></a>Pasos siguientes

[Supervisión de clientes](../manage/monitor-clients.md)
