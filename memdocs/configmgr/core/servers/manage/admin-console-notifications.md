---
title: Notificaciones de la consola de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre las notificaciones de la consola de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129610"
---
# <a name="configuration-manager-console-notifications"></a>Notificaciones de la consola de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--3556016, fka 1318035-->
A partir de la versión 1902 de Configuration Manager, la consola de Configuration Manager notifica los eventos específicos que ocurren. Puede configurar algunas de las notificaciones de eventos para los sitios de Configuration Manager.

- Notificaciones de eventos no configurables:
   - Cuando hay una actualización disponible para el propio Configuration Manager
   - Cuando se producen eventos de ciclo de vida y mantenimiento en el entorno
- Notificaciones de eventos configurables:
   - [Cambios de estado de sitio no críticos](#bkmk_noncrit)
   - [Mensajes de Microsoft](#bkmk_msft) (a partir de la versión 2006)

Esta notificación es una barra en la parte superior de la ventana de la consola, debajo de la cinta. Reemplaza a la experiencia anterior cuando había disponibles actualizaciones de Configuration Manager. Estas notificaciones en consola aún muestran información crítica, pero no interfieren con el trabajo en la consola. No se pueden descartar las notificaciones críticas. La consola muestra todas las notificaciones en una nueva área de notificación de la barra de título.

![Barra de notificación y marca en consola](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a> Configuración de un sitio para que muestre notificaciones no críticas

Puede configurar cada sitio para que muestre las notificaciones no críticas en las propiedades del sitio.

1. En el área de trabajo **Administración**, expanda **Configuración del sitio** y, a continuación, seleccione el nodo **Sitios**.
1. Seleccione el sitio que quiere configurar para las notificaciones no críticas.
1. En la cinta, seleccione **Propiedades**.
1. En la pestaña **Alertas**, seleccione la opción de **habilitar las notificaciones de la consola para cambios de estado de sitio no críticos**.
   - Si habilita esta opción, todos los usuarios de la consola ven notificaciones críticas, de advertencia e informativas. Esta opción está habilitada de forma predeterminada.  
   - Si deshabilita esta opción, los usuarios de la consola solo ven las notificaciones críticas.  

La mayoría de las notificaciones de consola son por sesión. La consola evalúa las consultas cuando un usuario la inicia. Para ver los cambios en las notificaciones, reinicie la consola. Si un usuario descarta una notificación no crítica, vuelve a notificar cuando se reinicia la consola, si sigue siendo aplicable.

Las siguientes notificaciones se vuelven a evaluar cada cinco minutos:

- El sitio está en modo de mantenimiento  
- El sitio está en modo de recuperación  
- El sitio está en modo de actualización  

Las notificaciones siguen los permisos de la administración basada en roles. Por ejemplo, si un usuario no tiene permisos para ver las actualizaciones de Configuration Manager, no ve esas notificaciones.

Algunas notificaciones tienen una acción relacionada. Por ejemplo, si la versión de la consola no coincide con la versión del sitio, seleccione **Instalar la nueva versión de la consola**. Esta acción inicia el instalador de la consola.

A partir de la versión 2006, si configura los servicios de Azure para asociar su sitio en la nube, verá notificaciones con una acción para [renovar la clave secreta](../deploy/configure/azure-services-wizard.md#bkmk_renew).<!--6386392--> El sitio evalúa el estado de las siguientes alertas una vez por hora:

- Una o más claves secretas de la aplicación de Azure AD expirarán pronto.
- Una o más claves secretas de la aplicación de Azure AD han expirado.

Las siguientes notificaciones son más aplicables a la rama de Technical Preview:  

- La versión de evaluación expira en 30 días (advertencia): faltan 30 días desde la fecha actual para la fecha de expiración de la versión de evaluación  
- La versión de evaluación ha expirado (crítico): la fecha actual es posterior a la fecha de expiración de la versión de evaluación  
- Discrepancia de versiones de consola (crítico): la versión de la consola no coincide con la versión del sitio  
- Actualización de sitio disponible (advertencia): hay un nuevo paquete de actualización disponible  

Para obtener más información y ayuda para la solución de problemas, vea el archivo **SmsAdminUI.log** en el equipo de la consola. De forma predeterminada, este archivo de registro está en la ruta de acceso siguiente: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a> Configuración de un sitio para recibir mensajes desde Microsoft
 <!--3953121-->

A partir de la versión 2006, puede optar por recibir notificaciones de Microsoft en la consola de Configuration Manager. Estas notificaciones le ayudan a mantenerse informado acerca de los cambios o las actualizaciones de características, los cambios en Configuration Manager y los servicios asociados y los problemas que requieren una acción para solucionarse.

### <a name="configure-notification-settings-for-microsoft-messages"></a>Configuración de las opciones de notificación para mensajes de Microsoft

1. Vaya a **Administración** > **Configuración de sitio** > **Sitios**.
1. Haga clic con el botón derecho en un sitio y seleccione **Propiedades**.
1. En la pestaña **Alertas**, habilite las notificaciones; para ello, seleccione **Receive messages from Microsoft** (Recibir mensajes de Microsoft). Puede anular la selección de cualquiera de las siguientes notificaciones si prefiere no recibirlas:  
   - **Prevent/fix** (Evitar/corregir): problemas conocidos que afectan a su organización y que pueden requerir que realice una acción.
   - **Plan de cambio**: cambios en Configuration Manager que pueden requerir que realice una acción.
   - **Manténgase informado**: le informa de las características nuevas o actualizadas que están disponibles.

     [ ![Notificación de las opciones de Microsoft en las propiedades del sitio](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>Pasos siguientes

- [Uso del a consola](admin-console.md)
- [Sugerencias de la consola](admin-console-tips.md)
- [Características de accesibilidad](../../understand/accessibility-features.md)
