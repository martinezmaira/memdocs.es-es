---
title: Manual del usuario del Centro de software
titleSuffix: Configuration Manager
description: Obtenga información sobre las características y funcionalidad del Centro de software
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715557"
---
# <a name="software-center-user-guide"></a>Manual del usuario del Centro de software

*Se aplica a: Configuration Manager (rama actual)*

El administrador de TI de la organización usa el Centro de software para instalar aplicaciones, actualizaciones de software y actualizar Windows. En este manual del usuario se explica la funcionalidad del Centro de software para los usuarios del equipo.

El Centro de software se instala automáticamente en los dispositivos Windows que administra la organización de TI. Para comenzar, consulte [Cómo abrir el Centro de software](#bkmk_open).

Notas generales sobre la funcionalidad del Centro de software:

- En este artículo se describen las características más recientes del Centro de software. Si en la organización se usa una versión más antigua, pero que todavía se admite, del Centro de software, no estarán disponibles todas las características. Para obtener más información, póngase en contacto con el administrador de TI.

- El administrador de TI puede deshabilitar algunos aspectos del Centro de software. Su experiencia concreta puede variar.

- Si varios usuarios usan un dispositivo al mismo tiempo, el usuario con el identificador de sesión más bajo será el único que vea todas las implementaciones disponibles en el Centro de software. Por ejemplo, varios usuarios en un entorno de escritorio remoto. Es posible que los usuarios con identificadores de sesión más altos no vean algunas de las implementaciones del Centro de software. Por ejemplo, los usuarios con identificadores de sesión más altos podrían ver las aplicaciones implementadas, pero no los paquetes o secuencias de tareas implementados. Mientras tanto, el usuario con el identificador de sesión más bajo verá todas las aplicaciones, paquetes y secuencias de tareas implementados. La pestaña **Usuarios** del Administrador de tareas de Windows muestra todos los usuarios y sus identificadores de sesión.

- El administrador de TI puede cambiar el color del Centro de software y agregar el logotipo de la organización.

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a> Cómo abrir el Centro de software

El Centro de software se instala automáticamente en los dispositivos Windows que administra la organización de TI. El método más sencillo de iniciar el Centro de software en un equipo Windows 10 consiste en presionar **Inicio** y escribir `Software Center`. Posiblemente no tenga que escribir la cadena completa para que Windows encuentre la mejor coincidencia.

:::image type="content" source="media/start-menu-software-center.png" alt-text="Mejor coincidencia del Centro de software en el menú Inicio":::

Para ir al menú Inicio, busque en el grupo **Microsoft Endpoint Manager** el icono **Centro de software**.

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Iconos del menú Inicio de Microsoft Endpoint Manager":::

> [!NOTE]
> La ruta de acceso del menú Inicio anterior es para las versiones de noviembre 2019 (versión 1910) o posterior. En versiones anteriores, el nombre de la carpeta es **Microsoft System Center**.

Si no encuentra el Centro de software en el menú Inicio, póngase en contacto con el administrador de TI.

## <a name="applications"></a>Aplicaciones

:::image type="content" source="media/software-center-apps.png" alt-text="Pestaña Aplicaciones del Centro de software" lightbox="media/software-center-apps.png":::

Seleccione la pestaña **Aplicaciones** (1) para buscar e instalar las aplicaciones que el administrador de TI implementa para usted o para este equipo.

- **Todas** (2): muestra todas las aplicaciones que se pueden instalar.

- **Requeridas** (3): el administrador de TI aplica estas aplicaciones. Si desinstala una de estas aplicaciones, el Centro de software vuelve a instalarla.

- **Filtros** (4): el administrador de TI puede crear categorías de aplicaciones. Si está disponible, seleccione la lista desplegable para filtrar la vista solamente a las aplicaciones de una categoría específica. Haga clic en **Todas** para mostrar todas las aplicaciones.

- **Ordenar por** (5): permite reorganizar la lista de aplicaciones. De forma predeterminada esta lista se ordena por **Más recientes**. Las aplicaciones disponibles recientemente se muestran con un título **Nueva** que es visible durante siete días.

- **Buscar** (6): ¿todavía no encuentra lo que busca? Escriba palabras clave en el cuadro Buscar para encontrarlo.

- Switch the view (Cambiar la vista) (7): seleccione los iconos para cambiar entre vista de lista y vista de mosaico. De forma predeterminada la lista de aplicaciones se muestra como mosaicos gráficos.

|Icono|Ver|Descripción|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|**Modo de selección múltiple**|Instale más de una aplicación a la vez. Para más información, consulte [Instalar varias aplicaciones](#install-multiple-applications).|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|**Vista de lista**|en esta vista, se muestra el icono de la aplicación, el nombre, el editor, la versión y el estado.|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|**Vista de mosaico**|el administrador de TI puede personalizar los iconos. Debajo de cada icono se muestra el nombre de la aplicación, el editor y la versión.|

### <a name="install-an-application"></a>Instalación de una aplicación

Seleccione una aplicación de la lista para ver más información sobre ella. Seleccione **Instalar** para instalarla. Si ya hay instalada una aplicación, puede que tenga la opción **Desinstalar**.

Es posible que algunas aplicaciones necesiten aprobación antes de instalarlas.

- Al intentar instalarla, puede escribir un comentario y, luego, hacer clic en **Solicitar** para solicitar la aplicación.

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="Solicitud de instalación de la aplicación del Centro de software para aprobación":::

- El Centro de software muestra el historial de solicitudes, y puede cancelar la solicitud.

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="Instalación de la aplicación del Centro de software solicitada":::

- Cuando un administrador aprueba la solicitud, puede instalar la aplicación. Si espera, el Centro de software instala automáticamente la aplicación durante el horario no comercial.

  :::image type="content" source="media/software-center-app-approved.png" alt-text="Instalación aprobada de la aplicación del Centro de software":::

### <a name="install-multiple-applications"></a>Instalar varias aplicaciones

<!-- 1357126 -->
Instale más de una aplicación a la vez en lugar de esperar a que finalice una antes de iniciar la siguiente. Las aplicaciones seleccionadas deben calificarse:

- La aplicación es visible para usted.
- La aplicación todavía no se descargado o instalado.
- El administrador de TI no requiere la aprobación para instalar la aplicación.

Para instalar más de una aplicación a la vez:

1. Seleccione el icono de selección múltiple en la esquina superior derecha: :::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::.

2. Seleccione dos o más aplicaciones para instalar. Active la casilla situada a la izquierda de cada aplicación de la lista.

3. Elija el botón **Instalar seleccionadas** para comenzar.

Las aplicaciones se instalan como de costumbre, pero ahora de forma sucesiva.

### <a name="share-an-application"></a>Compartir aplicaciones

Para compartir un vínculo a una aplicación específica, después de seleccionar la aplicación, elija el icono **Compartir** en la esquina superior derecha: :::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="Compartir una aplicación desde el Centro de software":::

**Copie** la cadena y péguela en otra parte, como un mensaje de correo electrónico. Por ejemplo, `softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a`. Cualquier otro usuario de la organización con el Centro de software puede usar el vínculo para abrir la misma aplicación.

## <a name="updates"></a>Actualizaciones

:::image type="content" source="media/software-center-updates.png" alt-text="Pestaña Actualizaciones del Centro de software" lightbox="media/software-center-updates.png":::

Seleccione la pestaña **Actualizaciones** (1) para ver e instalar las actualizaciones de software que el administrador de TI implementa en este equipo.  

- **Todas** (2): muestra todas las actualizaciones que se pueden instalar.

- **Requeridas** (3): el administrador de TI aplica estas actualizaciones.

- **Ordenar por** (4): permite reorganizar la lista de actualizaciones. De forma predeterminada, esta lista se ordena por **Nombre de aplicación: A a Z**.

- **Buscar** (5): ¿todavía no encuentra lo que busca? Escriba palabras clave en el cuadro Buscar para encontrarlo.

Para instalar actualizaciones, seleccione **Instalar todas** (6).

Para instalar solo actualizaciones específicas, seleccione el icono para entrar en el modo de selección múltiple (7): :::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
Active las actualizaciones que se van a instalar y, después, seleccione **Instalar seleccionadas**.

## <a name="operating-systems"></a>Sistemas operativos

:::image type="content" source="media/software-center-os.png" alt-text="Pestaña Sistemas operativos del Centro de software" lightbox="media/software-center-os.png":::

Seleccione la pestaña **Sistemas operativos** (1) para ver e instalar las versiones de Windows que el administrador de TI implementa en este equipo.  

- **Todas** (2): muestra todas las versiones de Windows que se pueden instalar.

- **Requeridas** (3): el administrador de TI aplica estas actualizaciones.

- **Ordenar por** (4): permite reorganizar la lista de actualizaciones. De forma predeterminada, esta lista se ordena por **Nombre de aplicación: A a Z**.

- **Buscar** (5): ¿todavía no encuentra lo que busca? Escriba palabras clave en el cuadro Buscar para encontrarlo.

## <a name="installation-status"></a>Estado de la instalación

Seleccione la pestaña **Estado de instalación** para ver el estado de las aplicaciones. Puede ver los estados siguientes:

- **Instalado**: el Centro de software ya ha instalado esta aplicación en este equipo.

- **Descargando**: el Centro de software está descargando el software para instalarlo en este equipo.

- **Error**: el Centro de software no pudo instalar el software.

- **Programado para instalar después de**: muestra la fecha y hora de la siguiente ventana de mantenimiento del dispositivo para instalar software que se publicará próximamente. El administrador de TI define las ventanas de mantenimiento.<!--1358131-->

  - Se puede ver el estado en las pestañas **Todo** y **Próximas**.

  - Puede instalar antes de la hora de la ventana de mantenimiento seleccionando el botón **Instalar ahora**.

## <a name="device-compliance"></a>Cumplimiento de dispositivos

Seleccione la pestaña **Cumplimiento de dispositivo** para ver el estado de cumplimiento de este equipo.

Seleccione **Comprobar cumplimiento** para evaluar la configuración del dispositivo con las directivas de seguridad definidas por el administrador de TI.

## <a name="options"></a>Options

Seleccione la pestaña **Opciones** para ver opciones adicionales para este equipo.

### <a name="work-information"></a>Información del trabajo

Indique el horario en el que suele trabajar. Es posible que el administrador de TI programe las instalaciones de software fuera de su horario laboral. Permita al menos cuatro horas al día para las tareas de mantenimiento del sistema. El administrador de TI puede seguir instalando aplicaciones críticas y actualizaciones de software durante el horario laboral.

- Seleccione la primera y la última hora a las que se usa este equipo. De forma predeterminada, estos valores son de las **5:00 a. m.** a las **10:00 p. m.**

- Seleccione los días de la semana que usará normalmente este equipo. De forma predeterminada, el Centro de software solo selecciona los días laborables.

Especifique si usa este equipo periódicamente para realizar su trabajo. El administrador podría instalar aplicaciones de manera automática o hacer que otras aplicaciones estén disponibles para los equipos principales.<!--3485366--> Seleccione **Normalmente uso este equipo para realizar mi trabajo** si el equipo que usa es un equipo principal.

### <a name="power-management"></a>Administración de energía

El administrador de TI puede establecer directivas de administración de energía. Estas directivas ayudan a la organización a ahorrar electricidad cuando este equipo no está en uso.

Para que este equipo esté exento de estas directivas, seleccione **Do not apply power settings from my IT department to this computer** (No aplicar la configuración de energía del departamento de TI en este equipo). De forma predeterminada, esta opción está deshabilitada, y el equipo aplica la configuración de energía.

### <a name="computer-maintenance"></a>Mantenimiento del equipo

Especifique el modo en que el Centro de software aplica los cambios al software antes de la fecha límite.

- **Instalar o desinstalar automáticamente el software necesario y reiniciar el equipo solo fuera del horario de atención especificado**: Esta configuración está deshabilitada de manera predeterminada.

- **Suspender las actividades del Centro de software si el equipo está en modo Presentación**: Esta opción está habilitada de forma predeterminada.

Cuando lo indique el administrador de TI, seleccione **Sync Policy** (Directiva de sincronización). Este equipo comprueba cualquier novedad con los servidores, como aplicaciones, actualizaciones de software o sistemas operativos.

### <a name="remote-control"></a>Control remoto

Especifique la configuración de acceso remoto y de control remoto del equipo.

**Use remote access settings from your IT department** (Usar la configuración de acceso remoto del departamento de TI): de forma predeterminada, el departamento de TI define la configuración para ayudarlo de forma remota. Los demás valores de esta sección muestran el estado de la configuración que define el departamento de TI. Para cambiar la configuración, primero deshabilite esta opción.

- **Nivel de acceso remoto permitido**
  - **Do not allow remote access** (No permitir el acceso remoto): los administradores de TI no pueden acceder de forma remota a este equipo para ayudarlo.
  - **View only** (Solo vista): un administrador de TI solo puede ver la pantalla de forma remota.
  - **Completa**: un administrador de TI puede controlar este equipo de forma remota. Esta configuración es la opción predeterminada.

- **Permitir que los administradores controlen este equipo de forma remota cuando no estoy**. De forma predeterminada, esta opción es **Sí**.

- **Cuando un administrador intenta controlar de forma remota este equipo**
  - **Pedir permiso cada vez**: Esta configuración es la opción predeterminada.
  - **No pedir permiso**

- **Mostrar lo siguiente durante el control remoto**: estas notificaciones visuales están habilitadas de forma predeterminada para indicar que un administrador tiene acceso remoto al dispositivo.
  - **Icono de estado en el área de notificación**
  - **Barra de conexión de sesión en el escritorio**

- **Reproducir sonido**: esta notificación audible le permite saber que un administrador tiene acceso remoto al dispositivo.
  - **Cuando la sesión comienza y termina**: esta configuración es la opción predeterminada.
  - **Varias veces durante la sesión**
  - **Nunca**

## <a name="custom-tabs"></a>Pestañas personalizadas

El administrador de TI puede quitar las pestañas predeterminadas o agregar pestañas adicionales al Centro de software. El administrador asigna un nombre a las pestañas personalizadas, que abren un sitio web que este especifica. Por ejemplo, podría tener una pestaña llamada "Departamento de soporte técnico" que abra el sitio web del departamento de soporte técnico de la organización. <!--1358132-->

## <a name="more-information-for-it-administrators"></a>Más información para los administradores de TI

Puede encontrar más información destinada a los administradores de TI sobre cómo planear y configurar el Centro de software en los siguientes artículos:

- [Planeamiento del centro de software](../../apps/plan-design/plan-for-software-center.md)
- [Configuración de cliente del Centro de software](../clients/deploy/about-client-settings.md#software-center)
- [Notificaciones de reinicio del dispositivo](../clients/deploy/device-restart-notifications.md)
- [Introducción al control remoto](../clients/manage/remote-control/introduction-to-remote-control.md)
