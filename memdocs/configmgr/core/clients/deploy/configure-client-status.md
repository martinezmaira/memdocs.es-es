---
title: Configuración del estado de cliente
titleSuffix: Configuration Manager
description: Seleccione la configuración del estado de cliente en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bb77e1e9f55919a03368d549946ee4dd1cda58a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694223"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Cómo configurar el estado de cliente en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para poder supervisar el estado de cliente de Configuration Manager y solucionar los problemas detectados, debe configurar el sitio para especificar los parámetros que se usan para marcar los clientes como inactivos y configurar las opciones para alertarle si la actividad de cliente cae por debajo de un umbral determinado. También puede deshabilitar en los equipos la corrección automática de problemas detectados por el estado de cliente.  

##  <a name="to-configure-client-status"></a><a name="BKMK_1"></a> Para configurar el estado de cliente  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Estado de cliente**. En la pestaña **Inicio** , en el grupo **Estado de cliente** haga clic en **Configuración de estado de cliente**.  

3.  En el cuadro de diálogo **Propiedades de configuración de estado de cliente** , especifique los valores siguientes para determinar la actividad del cliente:  

    > [!NOTE]  
    >  Si no se cumple ninguna de las opciones, el cliente se marcará como inactivo.  

    -   **Solicitudes de directiva de cliente durante los días siguientes:** especifique el número de días transcurridos desde que un cliente solicitó una directiva. El valor predeterminado es **7** días.  

    -   **Detección de latidos durante los días siguientes:** especifique el número de días transcurridos desde que el equipo cliente envió un registro de detección de latido a la base de datos del sitio. El valor predeterminado es **7** días.  

    -   **Inventario de hardware durante los días siguientes:** especifique el número de días transcurridos desde que el equipo cliente envió un registro de inventario de hardware a la base de datos del sitio. El valor predeterminado es **7** días.  

    -   **Inventario de software durante los días siguientes:** especifique el número de días transcurridos desde que el equipo cliente envió un registro de inventario de software a la base de datos del sitio. El valor predeterminado es **7** días.  

    -   **Mensajes de estado durante los días siguientes:** especifique el número de días transcurridos desde que el equipo cliente envió mensajes de estado a la base de datos del sitio. El valor predeterminado es **7** días.  

4.  En el cuadro de diálogo **Propiedades de configuración de estado de cliente** , especifique el valor siguiente para determinar el periodo de conservación de los datos del historial de estado de cliente:  

    -   **Retener el historial de estado de cliente durante el siguiente número de días:** especifique cuánto tiempo quiere que el historial de estado de cliente permanezca en la base de datos del sitio. El valor predeterminado es **31** días.  

5.  Haga clic en **Aceptar** para guardar las propiedades y cerrar el cuadro de diálogo **Propiedades de configuración de estado de cliente** .  

##  <a name="to-configure-the-schedule-for-client-status"></a><a name="BKMK_Schedule"></a> Para configurar la programación del estado de cliente  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Estado de cliente**. En la pestaña **Inicio** , en el grupo **Estado de cliente** haga clic en **Programar actualización de estado de cliente**.  

3.  En el cuadro de diálogo **Programar actualización de estado de cliente** , configure el intervalo en el que desea que el estado de cliente se actualice y, a continuación, haga clic en Aceptar.  

    > [!NOTE]  
    >  Cuando se cambia la programación de actualizaciones de estado de cliente, la actualización no tendrá efecto hasta la siguiente actualización de estado de cliente programada (según la programación configurada previamente).  

##  <a name="to-configure-alerts-for-client-status"></a><a name="BKMK_2"></a> Para configurar las alertas del estado de cliente  

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.  

3. En la lista **Recopilaciones de dispositivos** , seleccione la recopilación para la que desea configurar las alertas y, a continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

   > [!NOTE]  
   >  No puede configurar alertas para recopilaciones de usuario.  

4. En la pestaña **Alertas** del cuadro de diálogo <em>&lt;Nombre de la colección\></em>**Propiedades**, haga clic en **Agregar**.  

   > [!NOTE]  
   >  La pestaña **Alertas** solo es visible si el rol de seguridad con el que está asociado tiene permisos para alertas.  

5. En el cuadro de diálogo **Agregar nuevas alertas de recopilación** , seleccione las alertas que desea que se generen cuando el umbral de estado de cliente cae por debajo de un determinado valor y, a continuación, haga clic en **Aceptar**.  

6. En la lista **Condiciones** de la pestaña **Alertas** , seleccione cada alerta de estado de cliente y, a continuación, especifique la información siguiente.  

   -   **Nombre de alerta**: acepte el nombre predeterminado o escriba un nombre nuevo para la alerta.  

   -   **Gravedad de alerta**: seleccione el nivel de la alerta de la lista desplegable que se mostrará en la consola de Configuration Manager.  

   -   **Generar alerta**: especifique el porcentaje de umbral para la alerta.  

7. Haga clic en **Aceptar** para cerrar el cuadro de diálogo <em>&lt;Nombre de la colección\></em>**Propiedades**.  

##  <a name="to-exclude-computers-from-automatic-remediation"></a><a name="BKMK_3"></a> Para excluir la corrección automática de equipos  

1. Abra el Editor del Registro en el equipo cliente en el que desea deshabilitar la corrección automática.  

   > [!WARNING]  
   >  Si utiliza incorrectamente el Editor del Registro, puede ocasionar problemas que podrían requerir la reinstalación del sistema operativo. Microsoft no puede garantizar que seas capaz de resolver problemas ocasionados por el uso inapropiado del Editor del Registro. Usa el Editor del Registro bajo tu propia responsabilidad.  

2. Vaya a **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3. Escriba uno de los siguientes valores para esta clave del Registro:  

   -   **True**: el equipo cliente no corregirá automáticamente los problemas que se detecten. Sin embargo, recibirá una alerta en el área de trabajo **Supervisión** acerca de cualquier problema con este cliente.  

   -   **False**: el equipo cliente corregirá automáticamente los problemas al detectarlos. Se notificará en el área de trabajo **Supervisión**. Esta es la configuración predeterminada.  

4. Cierre el Editor del Registro.  

   También puede instalar clientes mediante la propiedad de instalación CCMSetup **NotifyOnly** para excluirlos de la corrección automática. Para más información sobre esta propiedad de instalación de clientes, vea [Acerca de las propiedades de instalación de clientes](../../../core/clients/deploy/about-client-installation-properties.md).  
