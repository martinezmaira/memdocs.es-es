---
title: Experiencias de usuario para la implementación de sistemas operativos
titleSuffix: Configuration Manager
description: Obtenga información sobre experiencias de usuario, como el progreso de las secuencias de tareas y el asistente para medios, para la implementación de sistemas operativos en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f92e76047a70f6d86406b1a364603163d902e62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703223"
---
# <a name="user-experiences-for-os-deployment"></a>Experiencias de usuario para la implementación de sistemas operativos

*Se aplica a: Configuration Manager (rama actual)*

Después de [implementar una secuencia de tareas](../deploy-use/deploy-a-task-sequence.md), los usuarios pueden interactuar de diferentes maneras con la implementación en función del escenario. En este artículo se muestran las experiencias de usuario principales con las implementaciones de sistemas operativos y también cómo se pueden configurar:

- Notificación de usuario del Centro de software para una implementación de alto impacto
- Una experiencia de arranque PXE de ejemplo
- Asistente para secuencia de tareas desde medios
- Ventana de progreso cuando se ejecuta la secuencia de tareas
- Ventana de error cuando se produce un error en la secuencia de tareas

## <a name="software-center"></a>Centro de software

En el caso de una implementación de alto impacto, puede personalizar el mensaje que muestra el Centro de software. Cuando el usuario abra la implementación del sistema operativo en el Centro de software, verá un mensaje similar al de la siguiente ventana:

![Notificación de la secuencia de tareas personalizada que se muestra al usuario final desde el Centro de software](../media/user-notification-enduser.png)

Para obtener más información sobre cómo personalizar el mensaje de esta ventana, consulte la sección [Crear una notificación personalizada para implementaciones de alto riesgo](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments).

También puede personalizar el nombre de la organización en la parte superior de la ventana. (En el ejemplo anterior se muestra el valor predeterminado, `IT Organization`). Cambie la configuración de cliente del **Nombre de la organización** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md#computer-agent).

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

Para obtener más información, vea cómo [usar el Centro de software para implementar Windows a través de la red](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md).

## <a name="pxe"></a>PXE

Los diferentes modelos de hardware tienen distintas experiencias para PXE. Para arrancarlos en la red, los dispositivos basados en UEFI suelen usar la tecla `Enter`, y los dispositivos basados en BIOS usan la tecla `F12`.

En el ejemplo siguiente se muestra la experiencia de PXE de Hyper-V Gen1 (BIOS):

![Pantalla de ejemplo de PXE de BIOS desde una máquina virtual de Hyper-V](media/hyperv-pxe.png)

Una vez que el dispositivo arranca correctamente a través de PXE, se comporta de forma similar a los medios de arranque. Para obtener más información, consulte la sección siguiente sobre el [Asistente para secuencia de tareas](#task-sequence-wizard).

Para más información, vea [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).

> [!WARNING]
> Si usa implementaciones de entorno PXE y configura el hardware del dispositivo con el adaptador de red como primer dispositivo de arranque, estos dispositivos pueden iniciar automáticamente una secuencia de tareas de implementación de sistema operativo sin interacción del usuario. La verificación de la implementación no administra esta configuración. Aunque esta configuración puede simplificar el proceso y reducir la interacción del usuario, coloca al dispositivo ante un riesgo mayor de restablecimiento de imagen inicial accidental.

## <a name="task-sequence-wizard"></a>Asistente para secuencia de tareas

Cuando usa [medios de secuencia de tareas](../deploy-use/create-task-sequence-media.md), se ejecuta el asistente para secuencia de tareas para ayudarle en el proceso.

### <a name="welcome-to-the-task-sequence-wizard"></a>Asistente para secuencia de tareas

![Captura de pantalla de la página principal del Asistente para secuencia de tareas](media/welcome-task-sequence-wizard.png)

- Si protege el medio con contraseña, el usuario tiene que escribir la contraseña en esta página de bienvenida.

- Seleccione **Configurar opciones de red** para especificar una dirección IP estática u otra configuración de red personalizada. De lo contrario, el dispositivo usa DHCP de forma predeterminada.

- Si la red requiere un proxy, seleccione **Configurar parámetros proxy**.

### <a name="select-a-task-sequence-to-run"></a>Selección de la secuencia de tareas que se va a ejecutar

Si implementa más de una secuencia de tareas en el dispositivo, verá esta página para seleccionar una. Asegúrese de usar un nombre y una descripción para la secuencia de tareas que los usuarios puedan entender.

![Captura de pantalla de la página de selección de una secuencia de tareas en el Asistente para secuencia de tareas](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>Edición de variables de secuencias de tareas

Si alguna de las variables de la secuencia de tareas tiene valores vacíos, el asistente muestra una página para editar los valores de las variables.

![Captura de pantalla de la página de edición de las variables de la secuencia de tareas en el Asistente para secuencia de tareas](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>Comandos de preinicio

Puede personalizar las imágenes de arranque o los medios de secuencia de tareas para que ejecuten un comando de preinicio. Un comando de preinicio se ejecuta antes de que se inicie la secuencia de tareas. Las siguientes acciones son algunas de las más comunes:

- Solicitar al usuario valores dinámicos, como el nombre del equipo.
- Especificar la configuración de la red.
- Establecer la afinidad entre usuario y dispositivo.

El comando de preinicio es una línea de comandos que se especifica mediante un script o un programa. La experiencia del usuario es única en función de ese script o programa.

Vea los siguientes artículos para más información:

- [Comandos de preinicio para medios de secuencia de tareas](prestart-commands-for-task-sequence-media.md)
- [Administrar imágenes de arranque](../get-started/manage-boot-images.md#customization)
- [Medios de secuencia de tareas](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>Progreso de la secuencia de tareas

Cuando se ejecuta la secuencia de tareas, se muestra la ventana **Progreso de la instalación**:

![Ejemplo de la ventana de progreso de la secuencia de tareas](media/task-sequence-progress.png)

- Esta ventana está siempre visible; puede moverla, pero no puede cerrarla ni minimizarla.

- Puede personalizar el nombre de la organización en la parte superior de la ventana. (En el ejemplo anterior se muestra el valor predeterminado, `IT Organization`). Cambie la configuración de cliente del **Nombre de la organización** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md#computer-agent).

    > [!TIP]
    > La secuencia de tareas almacena este valor en la variable de solo lectura [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName).

- Puede personalizar el subtítulo. (En el ejemplo anterior se muestra el valor predeterminado, `Running: <task sequence name>`). En las propiedades de la secuencia de tareas, seleccione la opción **Usar texto personalizado** para el texto de notificación del progreso. Puede usar un máximo de 255 caracteres.

- **Acción en ejecución**: la primera línea muestra el nombre del paso actual de la secuencia de tareas. En la barra de progreso inferior se muestra el total completado de la secuencia de tareas.

- La segunda línea solo se muestra para algunos pasos que proporcionan un progreso más detallado.

- Use la variable de secuencia de tareas [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) para controlar cuándo se debe mostrar el progreso de la secuencia de tareas.

    Para deshabilitar completamente la ventana de progreso, desactive la opción **Mostrar progreso de la secuencia de tareas** en la página **Experiencia del usuario** de la implementación de la secuencia de tareas.

A partir de la versión 2002, la ventana de progreso de la secuencia de tareas incluye las mejoras siguientes:<!--5932692-->

- Muestra el número de paso actual, el número total de pasos y el porcentaje completado.

- Se ha aumentado el ancho de la ventana para proporcionar más espacio de modo que se vea mejor el nombre de la organización en una sola línea.

![Ejemplo de la ventana de progreso de una secuencia de tareas](media/2356386-task-sequence-progress.png)

De forma predeterminada, en la ventana de progreso de las secuencias de tareas se utiliza el texto existente. Si no aplica ningún cambio, seguirá funcionando como en la versión 1910 y en las anteriores. Para mostrar la nueva información de progreso, especifique la variable de secuencia de tareas [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel).

El recuento y el porcentaje completado están pensados únicamente para fines orientativos. Estos valores se basan en el número total de pasos de la secuencia de tareas. En el caso de secuencias de tareas más complejas con pasos que se ejecutan de forma condicional en una lógica de secuencia de tareas, el progreso puede no ser lineal.

El número total de pasos no incluye los siguientes elementos en la secuencia de tareas:

- Grupos. Este elemento es un contenedor para otros pasos, no un propio paso.

- Instancias del paso **Ejecutar secuencia de tareas**. Este paso es un contenedor para otros pasos.

- Pasos que se deshabilitan explícitamente. Un paso deshabilitado no se ejecuta durante la secuencia de tareas.

    > [!NOTE]
    > Los pasos habilitados en un grupo deshabilitado todavía se incluyen en el recuento total.

## <a name="task-sequence-error"></a>Error de secuencia de tareas

Si se produce un error en la secuencia de tareas, se muestra la ventana **Error de secuencia de tareas**.

![Ejemplo de la ventana Error de secuencia de tareas](media/task-sequence-error.png)

- La información del encabezado se personaliza igual que en la ventana de progreso de la secuencia de tareas.

- Muestra el nombre de la secuencia de tareas, un código de error y un mensaje general para los usuarios. Por ejemplo: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- La ventana se cierra automáticamente después de un tiempo de espera. De forma predeterminada, el tiempo de espera es de 15 minutos. Puede personalizar este valor con la variable de secuencia de tareas [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout).
