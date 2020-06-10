---
title: Notificaciones de reinicio del dispositivo
titleSuffix: Configuration Manager
description: Comportamiento de las notificaciones de reinicio para diversas opciones de configuración de cliente en Configuration Manager.
ms.date: 06/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b326c4dd8112a72555239f2c3eda078ebf47bf82
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347226"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Notificaciones de reinicio del dispositivo en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las notificaciones que recibe un usuario para un reinicio del dispositivo pendiente pueden variar en función de la [configuración de cliente de reinicio de equipo](#client-settings) y de la versión de Configuration Manager que se use. Este artículo lo ayuda a configurar la experiencia del usuario para las notificaciones de reinicio de dispositivo pendiente.

## <a name="deployment-types-for-restart-notifications"></a>Tipos de implementación para las notificaciones de reinicio

La [configuración de cliente de reinicio de equipo](#client-settings) cambia la experiencia de usuario en todas las implementaciones necesarias que requieren un reinicio de los siguientes tipos:

- [Aplicación](../../../apps/deploy-use/deploy-applications.md)
- [Secuencia de tareas](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Actualización de software](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Tipos de notificación de reinicio

Cuando un dispositivo requiere un reinicio, el cliente muestra al usuario final una notificación del próximo reinicio. Hay cuatro notificaciones generales que pueden recibir los usuarios.

### <a name="toast-notification"></a>Notificación del sistema

Una notificación del sistema de Windows informa al usuario de que el dispositivo se debe reiniciar. La información de la notificación del sistema puede ser diferente dependiendo de la versión de Configuration Manager que ejecute. Este tipo de notificación es nativo del sistema operativo Windows. Con este tipo de notificación también puede ver software de terceros.

![Notificación del sistema de reinicio pendiente](media/3555947-restart-toast.png)

### <a name="software-center-notification-with-snooze"></a>Notificación del Centro de software con opción de posponer

El Centro de software muestra una notificación con una opción de posponer y el tiempo restante antes de forzar el reinicio de los dispositivos. El mensaje puede ser diferente dependiendo de su versión de Configuration Manager.

![Notificación del Centro de software de reinicio pendiente con el botón Posponer](media/3976435-snooze-restart-countdown.png)

### <a name="software-center-final-countdown-notification"></a>Notificación de cuenta regresiva final del Centro de software

El Centro de software muestra esta notificación de cuenta regresiva final que el usuario no puede cerrar ni posponer.

![Notificación de cuenta regresiva final del Centro de software](media/3976435-final-restart-countdown.png)

A partir de la versión 1906, el usuario no verá una barra de progreso en la notificación de reinicio hasta que el reinicio pendiente sea anterior a 24 horas.

### <a name="software-center-notification-before-deadline"></a>Notificación del Centro de software antes de la fecha límite

Si el usuario instala de forma proactiva software necesario antes de la fecha límite y tiene que reiniciarse, verá otra notificación. La siguiente notificación se recibe si la configuración de la experiencia del usuario permite las notificaciones y no se usan notificaciones del sistema para la implementación. Para obtener más información sobre esta configuración, consulte [Configuración de la **experiencia del usuario** de implementación](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) y [Notificaciones de usuario para implementaciones obligatorias](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Notificación de software instalado de forma proactiva](media/3976435-proactive-user-restart-notification.png)

#### <a name="available-apps"></a>Aplicaciones disponibles

Si no usa notificaciones del sistema, el cuadro de diálogo de software marcado como **Disponible** será similar al del software instalado de forma proactiva. En el caso del software **Disponible**, la notificación no tiene una fecha límite para el reinicio y el usuario puede elegir su propio intervalo de repetición. Para obtener más información, consulte [Configuración de aprobación](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

![El software marcado como "Disponible" no tiene una fecha límite para el reinicio en la notificación.](media/3555947-deployment-marked-available-restart.png)

## <a name="client-settings"></a>Configuración de cliente

Para controlar los comportamientos de reinicio del cliente, establezca la configuración siguiente de cliente de dispositivo en el grupo **Reinicio de equipo**. Para obtener más información, vea [Cómo configurar el cliente](configure-client-settings.md).

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Especificar el tiempo después de la fecha límite antes de reiniciarse un dispositivo (minutos)

Esta configuración debe tener menos duración que la ventana de mantenimiento más corta que se aplique en el equipo. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../manage/collections/use-maintenance-windows.md).

El valor predeterminado es 90 minutos. A partir de la versión 1906, el valor máximo aumentó de 1440 minutos (24 horas) a 20 160 minutos (dos semanas).

> [!NOTE]
> Esta configuración se denominaba **Mostrar una notificación temporal al usuario que indique el intervalo antes de que el usuario se desconecte o el equipo se inicie (minutos)** .

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>Especificar el tiempo durante el que se le presenta a un usuario una notificación de cuenta atrás final antes de reiniciarse un dispositivo (minutos)

Esta configuración debe tener menos duración que la ventana de mantenimiento más corta que se aplique en el equipo. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../manage/collections/use-maintenance-windows.md).

El valor predeterminado es 15 minutos.

> [!NOTE]
> Esta configuración se denominaba **Mostrar un cuadro de diálogo que el usuario no pueda cerrar, que muestre el intervalo de recuento antes de que el usuario se desconecte o el equipo se reinicie (minutos)** .

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Especificar la frecuencia de las notificaciones de recordatorio presentadas al usuario, después de la fecha límite, antes de reiniciar un dispositivo (minutos)
<!--3976435-->
_A partir de la versión 1906_

Este valor de duración de frecuencia debe ser menor que el valor de **Especificar el tiempo después de la fecha límite antes de reiniciarse un dispositivo (minutos)** menos el valor de **Especificar el tiempo durante el que se le presenta a un usuario una notificación de cuenta atrás final antes de reiniciarse un dispositivo (minutos)** . De lo contrario, las notificaciones de recordatorio no funcionarán.

El valor predeterminado es 240 minutos.

> [!NOTE]
> Esta configuración tenía el título **Especificar la duración de repetición para las notificaciones de cuenta regresiva de reinicio de equipo (minutos)** .

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de diálogo en lugar de una notificación del sistema
<!--3555947-->
A partir de la versión 1902, al configurar este valor en **Sí**, la experiencia del usuario pasa a ser más intrusiva. Esta configuración se aplica a todas las implementaciones de aplicaciones, secuencias de tareas y actualizaciones de software. Para más información, consulte [Planeamiento del centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> En Configuration Manager 1902, en determinadas circunstancias, el cuadro de diálogo no reemplazará las notificaciones del sistema. Para resolver este problema, instale el [paquete acumulativo de actualizaciones para Configuration Manager versión 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>Notificaciones de reinicio del dispositivo (versión 1906)
<!--3976435-->
Algunos clientes prefieren notificaciones de reinicio frecuentes y permiten que los usuarios tengan un plazo de tiempo breve para posponer. Otros permiten que los usuarios pospongan un reinicio durante períodos de tiempo más largos y notificar con poca frecuencia a los usuarios respecto del reinicio pendiente. A partir de la versión 1906 de Configuration Manager, se proporciona a un administrador control adicional sobre el tiempo y la frecuencia de las notificaciones de reinicio.

### <a name="install-required-software-at-or-after-the-deadline"></a>Instalación del software necesario en la fecha límite o después

Al instalarse el software necesario en la fecha límite o después, sus usuarios verán notificaciones en función de la configuración de cliente que haya seleccionado.

Si la opción **Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de diálogo en lugar de una notificación del sistema** se establece en:

- **No**: Windows muestra las notificaciones del sistema hasta que la implementación alcanza la notificación de cuenta regresiva final.

- **Sí**: El Centro de software muestra una notificación:

  - Si el reinicio supera las 24 horas, muestra un tiempo de reinicio estimado. La hora de esta notificación se basa en la opción: **Especificar el tiempo después de la fecha límite antes de reiniciarse un dispositivo (minutos)** .

    ![El tiempo de reinicio supera las 24 horas](media/3976435-notification-greater-than-24-hours.png)

  - Si el reinicio dura menos de 24 horas, muestra una barra de progreso. La hora de esta notificación se basa en la opción: **Especificar el tiempo después de la fecha límite antes de reiniciarse un dispositivo (minutos)** .

    ![El tiempo de reinicio no llega a las 24 horas](media/3976435-notification-less-than-24-hours.png)

Si el usuario selecciona **Posponer**, se muestra otra notificación temporal una vez transcurrido el período de aplazamiento. Este comportamiento presupone que todavía no llega a la cuenta regresiva final. La hora de la siguiente notificación se basa en la opción: **Especificar la frecuencia de las notificaciones de recordatorio presentadas al usuario, después de la fecha límite, antes de reiniciar un dispositivo (minutos)** . Si el usuario selecciona **Posponer** y el intervalo de aplazamiento es una hora, el Centro de software notifica al usuario nuevamente en 60 minutos. Este comportamiento presupone que todavía no llega a la cuenta regresiva final.

Cuando llega a la cuenta regresiva final, el Centro de software muestra al usuario una notificación que no puede cerrar. La barra de progreso está de color rojo y el usuario no puede darle a **Posponer**.

![Notificación de cuenta regresiva final del Centro de software en la versión 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="proactively-install-required-software-before-the-deadline"></a>Instalación proactiva del software necesario antes de la fecha límite

Si el usuario instala de forma proactiva el software necesario que debe reiniciarse antes de la fecha límite, verá otra notificación. Para obtener más información sobre esta configuración, consulte [Configuración de la **experiencia del usuario** de implementación](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) y [Notificaciones de usuario para implementaciones obligatorias](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

La siguiente notificación se recibe si la configuración de la experiencia del usuario permite las notificaciones y no se usan notificaciones del sistema para la implementación:

![Notificación de software instalado de forma proactiva](media/3976435-proactive-user-restart-notification.png)

Una vez que la implementación llega a la fecha límite, el Centro de software sigue el comportamiento para la [instalación del software necesario en la fecha límite o después](#install-required-software-at-or-after-the-deadline).

## <a name="example-configurations"></a>Configuraciones de ejemplo

En los ejemplos siguientes se describe cómo configurar las opciones de cliente para lograr comportamientos específicos.

### <a name="reminders-are-off"></a>Los recordatorios están desactivados

| Setting | Valor |
|---------|---------|
|Especificar el tiempo después de la fecha límite antes de reiniciarse un dispositivo (minutos)|180|
|Especificar el tiempo durante el que se le presenta a un usuario una notificación de cuenta atrás final antes de reiniciarse un dispositivo (minutos)|60|
|Especificar la frecuencia de las notificaciones de recordatorio presentadas al usuario, después de la fecha límite, antes de reiniciar un dispositivo (minutos)|240|
|Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de diálogo en lugar de una notificación del sistema|No|

El dispositivo se reiniciará tres horas (**180** minutos) después de la fecha límite de la implementación. Una hora (**60** minutos) antes de que se reinicie, el usuario ve una cuenta regresiva que no se puede cerrar ni posponer. La primera notificación de recordatorio está establecida para iniciarse cuatro horas (**240** minutos) después de la fecha límite, que es después del reinicio. Por lo tanto, el usuario no ve ningún recordatorio.

### <a name="low-reminder-frequency"></a>Frecuencia baja de los recordatorios

| Setting | Valor |
|---------|---------|
|Especificar el tiempo después de la fecha límite antes de reiniciarse un dispositivo (minutos)|7200|
|Especificar el tiempo durante el que se le presenta a un usuario una notificación de cuenta atrás final antes de reiniciarse un dispositivo (minutos)|120|
|Especificar la frecuencia de las notificaciones de recordatorio presentadas al usuario, después de la fecha límite, antes de reiniciar un dispositivo (minutos)|900|
|Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de diálogo en lugar de una notificación del sistema|Sí|

El dispositivo se reiniciará cinco días (**7200** minutos) después de la fecha límite de la implementación. Dos horas (**120** minutos) antes de que se reinicie, el usuario ve una cuenta regresiva que no se puede cerrar ni posponer. Esta configuración permite 118 horas para mostrar recordatorios (`(7200 - 120) / 60`). 15 horas (**900** minutos) después de la fecha límite, el Centro de software muestra el primer recordatorio. Muestra un máximo de seis recordatorios adicionales cada 15 horas (**900 minutos**). El usuario ve el recordatorio como una ventana en la pantalla, en lugar de una notificación que desaparece en unos segundos.

### <a name="high-reminder-frequency"></a>Frecuencia alta de los recordatorios

| Setting | Valor |
|---------|---------|
|Especificar el tiempo después de la fecha límite antes de reiniciarse un dispositivo (minutos)|2880|
|Especificar el tiempo durante el que se le presenta a un usuario una notificación de cuenta atrás final antes de reiniciarse un dispositivo (minutos)|60|
|Especificar la frecuencia de las notificaciones de recordatorio presentadas al usuario, después de la fecha límite, antes de reiniciar un dispositivo (minutos)|30|
|Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de diálogo en lugar de una notificación del sistema|Sí|

El dispositivo se reiniciará dos días (**2880** minutos) después de la fecha límite de la implementación. Una hora (**60** minutos) antes de que se reinicie, el usuario ve una cuenta regresiva que no se puede cerrar ni posponer. Esta configuración permite 47 horas para mostrar recordatorios (`(2880 - 60) / 60`). **30** minutos después de la fecha límite, el Centro de software muestra el primer recordatorio. Muestra un máximo de 92 recordatorios adicionales cada **30 minutos**. El usuario ve el recordatorio como una ventana en la pantalla, en lugar de una notificación que desaparece en unos segundos.

## <a name="device-restart-notifications-version-1902"></a>Notificaciones de reinicio del dispositivo (versión 1902)

<!--3555947-->
A veces los usuarios no ven la notificación del sistema de Windows sobre un reinicio o una implementación necesaria. Entonces no ven la experiencia de posponer el recordatorio. Este comportamiento puede conducir a una mala experiencia de usuario cuando el cliente llega a una fecha límite.

A partir de la versión 1902, cuando se requieren cambios de software o es necesario reiniciar las implementaciones, tiene la opción de usar una ventana de diálogo más intrusiva.

En el grupo [Reinicio de equipo](#client-settings) de la configuración de cliente, habilite la siguiente opción: **Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de diálogo en lugar de una notificación del sistema**.  

Cuando se realiza esta configuración del cliente, cambia la experiencia de usuario en todas las implementaciones necesarias que requieren un reinicio a partir de las notificaciones del sistema:

![Notificación del sistema de reinicio necesario](media/3555947-restart-toast-initial.png)  

En la ventana de diálogo del Centro de software más intrusiva:

![Ventana de diálogo con el reinicio del equipo](media/3976435-proactive-user-restart-notification.png)

Si el usuario no reinició su dispositivo tras la instalación, recibirá una notificación como recordatorio. Este recordatorio temporal se mostrará al usuario en función de la configuración de cliente: **Mostrar una notificación temporal al usuario que indique el intervalo antes de que el usuario se desconecte o el equipo se inicie (minutos)** . Esta configuración es el tiempo general del que dispone el usuario para reiniciar la máquina antes de que se fuerce un reinicio.

- Notificación temporal al usar notificaciones del sistema:

  ![Notificación del sistema de reinicio pendiente](media/3555947-restart-toast.png)

- Notificación temporal al usar la ventana de diálogo del Centro de software, no notificación del sistema:

  ![Notificación del Centro de software de reinicio pendiente con el botón Posponer](media/3555947-1902-hide-notification.png)

Si el usuario no lleva a cabo el reinicio tras la notificación temporal, recibirá la notificación de cuenta regresiva final que no puede cerrar. La hora a la que aparece la notificación final se basa en la configuración de cliente: **Mostrar un cuadro de diálogo que el usuario no pueda cerrar, que muestre el intervalo de recuento antes de que el usuario se desconecte o el equipo se reinicie (minutos)** . Por ejemplo, si el valor es 60, se mostrará al usuario la notificación final una hora antes de forzarse un reinicio:

![Notificación de cuenta regresiva final del Centro de software](media/3555947-1902-final-countdown.png)

Las opciones siguientes deben tener menos duración que la [ventana de mantenimiento](../manage/collections/use-maintenance-windows.md) más corta que se aplique en el equipo:

- **Mostrar una notificación temporal al usuario que indique el intervalo antes de que el usuario se desconecte o el equipo se inicie (minutos)**
- **Mostrar un cuadro de diálogo que el usuario no pueda cerrar, que muestre el intervalo de recuento antes de que el usuario se desconecte o el equipo se reinicie (minutos)**

> [!IMPORTANT]
> En Configuration Manager 1902, en determinadas circunstancias, el cuadro de diálogo no reemplazará las notificaciones del sistema. Para resolver este problema, instale el [paquete acumulativo de actualizaciones para Configuration Manager versión 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="log-files"></a>Archivos de registro

Para solucionar problemas con los reinicios de dispositivo, use los archivos **RebootCoordinator.log** y **SCNotify.log** en el cliente. Según el tipo de implementación específico, es posible que también tenga que usar [archivos de registro](../../plan-design/hierarchy/log-files.md) de cliente adicionales.

## <a name="next-steps"></a>Pasos siguientes

- [Cómo establecer la configuración del cliente](configure-client-settings.md)
- [Configuración de la **experiencia del usuario** de implementación de aplicación](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [Notificaciones de usuario para implementaciones de aplicaciones obligatorias](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
