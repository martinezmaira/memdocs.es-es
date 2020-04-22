---
title: Notificaciones de reinicio del dispositivo
titleSuffix: Configuration Manager
description: Comportamiento de las notificaciones de reinicio para diversas opciones de configuración de cliente en Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693963"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Notificaciones de reinicio del dispositivo en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las notificaciones que recibe un usuario para un reinicio del dispositivo pendiente pueden variar en función de la [configuración de cliente de reinicio de equipo](about-client-settings.md#computer-restart) y de la versión de Configuration Manager usada. Este artículo ayuda a los administradores a determinar cuál es la experiencia de usuario en las notificaciones de reinicio del dispositivo pendientes.

>[!NOTE]
> - Se centra en la configuración de cliente encontrada en las versiones 1902 y 1906 de Configuration Manager.


## <a name="deployment-types-for-restart-notifications"></a>Tipos de implementación para las notificaciones de reinicio

La [configuración de cliente de reinicio de equipo](about-client-settings.md#computer-restart) cambia la experiencia de usuario en todas las implementaciones necesarias que requieren un reinicio de los siguientes tipos:

- [Aplicación](../../../apps/deploy-use/deploy-applications.md)
- [Secuencia de tareas](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Actualización de software](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Tipos de notificación de reinicio

Cuando es necesario un reinicio, el usuario final recibe una notificación del próximo reinicio. Hay cuatro notificaciones generales que pueden recibir los usuarios:

**Notificación del sistema** que le informa de que es necesario un reinicio. La información de la notificación del sistema puede ser diferente dependiendo de la versión de Configuration Manager que ejecute. Este tipo de notificación es nativa del SO Windows y es posible que también vea software de terceros mediante este tipo de notificación.

![Notificación del sistema de reinicio pendiente](media/3555947-restart-toast.png)

Notificación del Centro de software con la opción Posponer, que muestra el tiempo restante antes de que se fuerce un reinicio. El mensaje puede ser diferente dependiendo de su versión de Configuration Manager.

![Notificación del Centro de software de reinicio pendiente con el botón Posponer](media/3976435-snooze-restart-countdown.png)

Notificación de cuenta regresiva final del Centro de software que el usuario no puede cerrar. El botón Posponer está atenuado.

![Notificación de cuenta regresiva final del Centro de software](media/3976435-final-restart-countdown.png)

Si el usuario instala de forma proactiva software necesario que debe reiniciarse antes de que llegue la fecha límite, verá otra notificación. La siguiente notificación se recibe si la configuración de la experiencia del usuario permite las notificaciones y no se usan notificaciones del sistema para la implementación. Para obtener más información sobre esta configuración, consulte [Configuración de la **experiencia del usuario** de implementación](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) y [Notificaciones de usuario para implementaciones obligatorias](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Notificación de software instalado de forma proactiva](media/3976435-proactive-user-restart-notification.png)

- Si no usa notificaciones del sistema, el cuadro de diálogo de software marcado como **Disponible** será similar al del software instalado de forma proactiva.

  - En el caso del software **Disponible**, la notificación no tiene una fecha límite para el reinicio y el usuario puede elegir su propio intervalo de repetición. Para obtener más información, consulte [Configuración de aprobación](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

    ![El software marcado como "Disponible" no tiene una fecha límite para el reinicio en la notificación.](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>Notificaciones de reinicio del dispositivo en la versión 1902

<!--3555947-->
A veces los usuarios no ven la notificación del sistema de Windows sobre un reinicio o una implementación necesaria. Entonces no ven la experiencia de posponer el recordatorio. Este comportamiento puede conducir a una mala experiencia de usuario cuando el cliente llega a una fecha límite.

A partir de la versión 1902, cuando se requieren cambios de software o es necesario reiniciar las implementaciones, tiene la opción de usar una ventana de diálogo más intrusiva.

En el grupo [Reinicio de equipo](about-client-settings.md#computer-restart) de la configuración de cliente, habilite la siguiente opción: **Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de diálogo en lugar de una notificación del sistema**.  

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

## <a name="device-restart-notifications-starting-in-version-1906"></a>Notificaciones de reinicio del dispositivo a partir de la versión 1906
<!--3976435-->
Algunos administradores prefieren notificaciones de reinicio frecuentes y un período de tiempo breve que permitan a los reinicios posponerse. Otros administradores permiten a los usuarios posponer un reinicio durante períodos de tiempo más largos y desean que se notifique a estos el reinicio pendiente con poca frecuencia. La versión 1906 de Configuration Manager proporciona a un administrador control adicional sobre el tiempo y la frecuencia de las notificaciones de reinicio. Los siguientes elementos se incorporaron en 1906 para proporcionar un mayor control al administrador:

- **Especificar la duración de repetición para las notificaciones de cuenta regresiva de reinicio de equipo (minutos)** se agregó a la [configuración de cliente de reinicio de equipo](about-client-settings.md#computer-restart).
- El valor máximo de **Mostrar una notificación temporal al usuario que indique el intervalo antes de que el usuario se desconecte o el equipo se inicie (minutos)** ha aumentado de 1440 minutos (24 horas) a 20160 minutos (2 semanas).
- El usuario no verá una barra de progreso en la notificación de reinicio hasta que el reinicio pendiente sea anterior a 24 horas.

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>Notificaciones al instalarse el software necesario en la fecha límite o después

Al instalarse el software necesario en la fecha límite o después, sus usuarios verán notificaciones en función de la configuración de cliente que haya seleccionado.

Si la opción **Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de diálogo en lugar de una notificación del sistema** se establece en:

- **No**: las notificaciones del sistema se usan hasta alcanzarse la notificación de cuenta regresiva final.
- **Sí**: se ve una notificación del Centro de software.
  - Si el reinicio supera las 24 horas, se verá un tiempo de reinicio estimado. La hora de esta notificación se basa en la opción: **Mostrar una notificación temporal al usuario que indique el intervalo antes de que el usuario se desconecte o el equipo se inicie (minutos)** .

     ![El tiempo de reinicio supera las 24 horas](media/3976435-notification-greater-than-24-hours.png)

  - Si el reinicio dura menos de 24 horas, se verá una barra de progreso. La hora de esta notificación se basa en la opción: **Mostrar una notificación temporal al usuario que indique el intervalo antes de que el usuario se desconecte o el equipo se inicie (minutos)**

     ![El tiempo de reinicio no llega a las 24 horas](media/3976435-notification-less-than-24-hours.png)

Si el usuario selecciona el botón **Posponer**, se recibirá otra notificación temporal una vez transcurrido el período de repetición, suponiendo que aún no haya alcanzado la cuenta regresiva final. La hora de la siguiente notificación se basa en la opción: **Especificar la duración de repetición para las notificaciones de cuenta regresiva de reinicio de equipo (horas)** . Si el usuario selecciona **Posponer** y su intervalo de repetición es de una hora, volverá a notificarse al usuario en 60 minutos, suponiendo que aún no haya alcanzado la cuenta regresiva final.

Al alcanzarse la cuenta regresiva final, el usuario recibe una notificación que no puede cerrar. La barra de progreso está de color rojo y el usuario no puede darle a **Posponer**.

![Notificación de cuenta regresiva final del Centro de software en la versión 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>El usuario lleva a cabo la instalación de forma proactiva antes de la fecha límite

Si el usuario instala de forma proactiva software necesario que debe reiniciarse antes de que llegue la fecha límite, verá otra notificación. Para obtener más información sobre esta configuración, consulte [Configuración de la **experiencia del usuario** de implementación](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) y [Notificaciones de usuario para implementaciones obligatorias](../../../apps/deploy-use/deploy-applications.md#bkmk_notify). 

La siguiente notificación se recibe si la configuración de la experiencia del usuario permite las notificaciones y no se usan notificaciones del sistema para la implementación:

![Notificación de software instalado de forma proactiva](media/3976435-proactive-user-restart-notification.png)

Una vez que se alcance la fecha límite para el software, se seguirá el comportamiento [Notificaciones al instalarse el software necesario en la fecha límite o después](#notifications-when-required-software-is-installed-at-or-after-the-deadline).

## <a name="log-files"></a>Archivos de registro

Use **RebootCoordinator.log** y **SCNotify.log** para solucionar problemas relativos al reinicio de dispositivos. Es posible que también tenga que usar [archivos de registro](../../plan-design/hierarchy/log-files.md) de cliente en función del tipo de implementación usada.

## <a name="next-steps"></a>Pasos siguientes

- [Introducción a la administración de aplicaciones](../../../apps/understand/introduction-to-application-management.md)
- [Introduction to operating system deployment](../../../osd/understand/introduction-to-operating-system-deployment.md) (Introducción a la implementación de sistema operativo)
- [Introducción a la administración de actualizaciones de software](../../../sum/understand/software-updates-introduction.md)
