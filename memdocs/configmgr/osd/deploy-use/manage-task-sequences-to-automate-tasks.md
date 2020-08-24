---
title: Administrar secuencias de tareas
titleSuffix: Configuration Manager
description: Cree, edite, implemente, importe y exporte secuencias de tareas para administrarlas y automatizar las tareas en su entorno.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 609f5d010018fa23dd4a533b2f1079f07d8c2283
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125072"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Administrar secuencias de tareas para automatizar tareas

*Se aplica a: Configuration Manager (rama actual)*

Use secuencias de tareas para automatizar los pasos en su entorno de Configuration Manager. Estos pasos pueden implementar una imagen de sistema operativo en un equipo de destino, compilar y capturar una imagen de sistema operativo a partir de un conjunto de archivos de instalación de sistema operativo, y capturar y restaurar la información de estado de usuario. Las secuencias de tareas se encuentran en la consola de Configuration Manager. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**. El nodo **Secuencia de tareas**, incluidas todas las subcarpetas creadas, se replica en toda la jerarquía de Configuration Manager. Para obtener información, consulte [Planning considerations for automating tasks](../plan-design/planning-considerations-for-automating-tasks.md) (Consideraciones de planeación para la automatización de tareas).  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a> Creación

Cree secuencias de tareas con el Asistente para crear secuencia de tareas. Este asistente puede crear los siguientes tipos de secuencias de tareas:  

- [Secuencia de tareas para instalar un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md): cree los pasos para instalar un sistema operativo. También incluye opciones para migrar datos de usuario, incluir actualizaciones de software e instalar aplicaciones.

- [Secuencia de tareas para actualizar un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md): cree los pasos para actualizar un sistema operativo. También incluye opciones para incluir actualizaciones de software e instalar aplicaciones.

- [Secuencia de tareas para capturar un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md) Cree los pasos para compilar y capturar un sistema operativo desde un equipo de referencia. Puede incluir actualizaciones de software e instalar aplicaciones en el equipo de referencia antes de capturar la imagen.

- [Secuencia de tareas para capturar y restaurar un estado de usuario](create-a-task-sequence-to-capture-and-restore-user-state.md): agregue pasos a una secuencia de tareas existente para capturar y restaurar los datos de estado de usuario.

- [Secuencia de tareas personalizada](create-a-custom-task-sequence.md) Este tipo no agrega ningún paso a la secuencia de tareas. Después de crear esta secuencia de tareas, modifíquela y agregue pasos.

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a> Editar  

Modifique una secuencia de tareas, agregue o quite pasos, agregue o quite grupos, o cambie el orden de los pasos. Para más información, vea [Uso del editor de secuencias de tareas](../understand/task-sequence-editor.md).

## <a name="reduce-the-size-of-task-sequence-policy"></a><a name="bkmk_policysize"></a> Reducción del tamaño de la directiva de secuencia de tareas

<!--6982275-->
Cuando el tamaño de la directiva de secuencia de tareas supera los 32 MB, el cliente no puede procesar la directiva de gran tamaño. En consecuencia, el cliente no puede ejecutar la implementación de la secuencia de tareas.

El tamaño de la secuencia de tareas almacenada en la base de datos del sitio es menor, pero puede producir problemas si es demasiado grande. Cuando el cliente procesa toda la directiva de secuencia de tareas, el tamaño expandido puede ocasionar problemas si supera 32 MB.

A partir de la versión 2006, para comprobar el tamaño de la directiva de secuencia de tareas de 32 MB en los clientes, use la [Información de administración](../../core/servers/manage/management-insights.md#operating-system-deployment).

Para ayudar a reducir el tamaño general de la directiva de una implementación de secuencia de tareas, haga lo siguiente:

- Separe los segmentos funcionales en secuencias de tareas secundarias y use el paso [Ejecutar secuencia de tareas](../understand/task-sequence-steps.md#child-task-sequence). Cada secuencia de tareas tiene un límite de 32 MB independiente en el tamaño de la directiva.

    > [!NOTE]
    > La reducción del número total de pasos y grupos de una secuencia de tareas tiene una repercusión mínima en el tamaño de la directiva. Cada paso suele ser un par de KB en la directiva. El traslado de grupos de pasos a una secuencia de tareas secundaria afecta en mayor medida.

- Reduzca el número de actualizaciones de software de las implementaciones a la misma colección que la secuencia de tareas.

- En lugar de escribir un script en el paso [Ejecutar script de PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript), haga referencia a él a través de un paquete.

- Hay un límite de 8 KB en el tamaño del entorno de la secuencia de tareas cuando se ejecuta. Revise el uso de variables personalizadas de las secuencias de tareas, que también pueden contribuir al tamaño de la directiva.

- Como último recurso, divida una secuencia de tareas dinámica y compleja en secuencias de tareas independientes con implementaciones distintas en colecciones diferentes.

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a> Propiedades del Centro de software

Siga este procedimiento para configurar los detalles de la secuencia de tareas que aparece en el Centro de software. Estos detalles son meramente informativos.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y seleccione **Propiedades**.  

3. En la pestaña **General**, está disponible la siguiente configuración para el Centro de software:  

    - **Es necesario reiniciar**: permite al usuario saber si es necesario reiniciar durante la instalación.  

    - **Tamaño de la descarga (MB)** : especifica cuántos megabytes se muestran en el Centro de software para la secuencia de tareas.  

    - **Tiempo de ejecución estimado (minutos)** : especifica el tiempo de ejecución estimado en minutos que se muestra en el Centro de software para la secuencia de tareas.  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a> Configuración avanzada

Use el procedimiento siguiente para configurar el comportamiento de la secuencia de tareas en el cliente de Configuration Manager.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y seleccione **Propiedades**.  

3. En la pestaña **Avanzadas** están disponibles las opciones siguientes:  

    - **Ejecutar otro programa primero**: seleccione esta opción para ejecutar un programa en otro paquete antes de ejecutar la secuencia de tareas. De forma predeterminada, esta casilla de verificación está desactivada. No es necesario implementar por separado el programa especificado para que se ejecute primero.  

        > [!IMPORTANT]
        > Esta configuración solo se aplica a las secuencias de tareas que se ejecutan en el sistema operativo completo. Si inicia la secuencia de tareas mediante PXE o medios de arranque, Configuration Manager ignora este ajuste.  

        - **Paquete**: busque el paquete que contiene el programa que se va a ejecutar antes de esta secuencia de tareas.  

        - **Programa**: seleccione el programa que se va a ejecutar antes de esta secuencia de tareas.  

        > [!NOTE]  
        > Si el programa seleccionado no se ejecuta en un cliente, la secuencia de tareas tampoco se ejecuta. Si el programa seleccionado se ejecuta correctamente, no se ejecutará de nuevo, incluso aunque la secuencia de tareas se vuelva a ejecutar en el mismo cliente.  

    - **Suprimir notificaciones de secuencia de tareas**: seleccione esta opción para ocultar la notificación del sistema **Hay nuevo software disponible**. En el área de notificaciones se seguirá mostrando el icono **Nuevo software** del Centro de software. Esta opción está deshabilitada de forma predeterminada.  

    - **Deshabilitar esta secuencia de tareas en los equipos en los que se implementó**: si selecciona esta opción, Configuration Manager deshabilita temporalmente todas las implementaciones que contienen esta secuencia de tareas. También quita la secuencia de tareas de la lista de implementaciones disponibles para su ejecución. La secuencia de tareas no se ejecuta hasta que la habilite. Esta opción está deshabilitada de forma predeterminada.  

    - **Tiempo de ejecución máximo permitido**: especifica el tiempo máximo (en minutos) previsto para la ejecución de la secuencia de tareas en el equipo de destino. Use un número entero igual o mayor que cero. De forma predeterminada, este valor es de 120 minutos.  

        > [!IMPORTANT]  
        > Si está usando ventanas de mantenimiento para la recopilación en las que implementa esta secuencia de tareas, puede producirse un conflicto si el **Tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programada. Si el tiempo de ejecución máximo se establece en **0**, la secuencia de tareas se inicia durante la ventana de mantenimiento. Sigue ejecutándose hasta que se complete o se produzca un error después de cerrar la ventana de mantenimiento. Como resultado, las secuencias de tareas con un tiempo de ejecución máximo establecido en **0** podrían ejecutarse después del final de sus ventanas de mantenimiento. Si establece el tiempo de ejecución máximo en un periodo específico (diferente de 0) que supera la duración de cualquiera de las ventanas de mantenimiento disponibles, la secuencia de tareas no se ejecutará. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md) (Uso de ventanas de mantenimiento en Configuration Manager).  

        Si el valor se establece en **0**, Configuration Manager evalúa el tiempo de ejecución máximo permitido en **12** horas (720 minutos) para el progreso de la supervisión. Aun así, la secuencia de tareas se iniciará siempre y cuando la duración de la cuenta atrás no supere el valor de la ventana de mantenimiento.  

        > [!NOTE]
        > Cuando alcanza el tiempo de ejecución máximo, si no permite que los usuarios interactúen con una implementación requerida, Configuration Manager detiene la secuencia de tareas. Si no se detiene la secuencia de tareas, Configuration Manager detiene la supervisión de la secuencia de tareas una vez que se alcanza el tiempo de ejecución máximo permitido.

    - **Usar una imagen de arranque**: use la imagen de arranque seleccionada cuando se ejecuta la secuencia de tareas. Seleccione **Examinar** para seleccionar otra imagen de arranque. Desactive esta opción para deshabilitar el uso de la imagen de arranque seleccionada cuando se ejecuta la secuencia de tareas.  

    - **This task sequence can run on any platform** (Esta secuencia de tareas puede ejecutarse en cualquier plataforma): si selecciona esta opción, Configuration Manager no comprueba el tipo de plataforma del equipo de destino cuando se implementa la secuencia de tareas. Esta opción está seleccionada de forma predeterminada.  

    - **This task sequence can only run on the specified client platforms** (Esta secuencia de tareas solo puede ejecutarse en las plataformas cliente especificadas): Esta opción especifica los procesadores, las versiones de sistema operativo y los Service Pack en los que se puede ejecutar esta secuencia de tareas. Cuando seleccione esta opción, seleccione al menos una plataforma de la lista. De forma predeterminada, no hay ninguna plataforma seleccionada. Configuration Manager usa esta información cuando se evalúa qué equipos de destino de una recopilación reciben la secuencia de tareas implementada.  

        > [!NOTE]  
        > Cuando se ejecuta una secuencia de tareas desde PXE o medios de arranque, Configuration Manager ignora esta opción. La secuencia de tareas se ejecuta como si estuviera seleccionada la opción **Este programa puede ejecutarse en cualquier plataforma**.  

## <a name="high-impact-settings"></a>Configuración de alto impacto

Configure una secuencia de tareas como de gran impacto y personalice los mensajes que reciben los usuarios cuando ejecutan la secuencia de tareas.

> [!WARNING]
> Si usa implementaciones de PXE y configura el hardware del dispositivo con el adaptador de red como primer dispositivo de arranque, estos dispositivos pueden iniciar automáticamente una secuencia de tareas de implementación de sistema operativo sin interacción del usuario. La verificación de la implementación no administra esta configuración. Aunque esta configuración puede simplificar el proceso y reducir la interacción del usuario, coloca al dispositivo ante un riesgo mayor de restablecimiento de imagen inicial accidental.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Establecer una secuencia de tareas como una secuencia de tareas de alto impacto

Siga este procedimiento para establecer una secuencia de tareas como de alto impacto.

> [!NOTE]  
> Cualquier secuencia de tareas que cumpla determinadas condiciones se define automáticamente como de alto impacto. Para obtener más información, vea [Configuración para administrar implementaciones de alto riesgo](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y seleccione **Propiedades**.  

3. En la pestaña **Notificación de usuario**, seleccione **Es una secuencia de tareas de alto impacto**.  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Crear una notificación personalizada para implementaciones de alto riesgo

Utilice el procedimiento siguiente para crear una notificación personalizada para las implementaciones de gran impacto.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Seleccione la secuencia de tareas que se va editar y seleccione **Propiedades**.  

3. En la pestaña **Notificación de usuario**, seleccione **Usar texto personalizado**.  

    > [!NOTE]
    > Solo puede establecer el texto de la notificación del usuario cuando seleccione la opción **Es una secuencia de tareas de alto impacto**.  

4. Configure las siguientes opciones:  

    > [!Note]  
    > Cada cuadro de texto tiene un límite máximo de 255 caracteres.  

    - **Texto del título de la notificación de usuario**: especifica el texto de color azul que aparece en la notificación de usuario del Centro de software. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Confirm you want to upgrade the operating system on this computer" (Confirme que quiere actualizar el sistema operativo en este equipo).  

    - **Texto del mensaje de notificación de usuario**: hay tres cuadros de texto que proporcionan el cuerpo de la notificación personalizada. Todos los cuadros de texto requieren que agregue texto.  

        - Cuadro de texto 1: especifica el cuerpo principal del texto, que normalmente contiene instrucciones para el usuario. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Upgrading the operating system takes time and your computer might restart several times" (La actualización del sistema operativo lleva un tiempo y es posible que el equipo se reinicie varias veces).  

        - Cuadro de texto 2: especifica el texto en negrita debajo del cuerpo de texto principal. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "This in-place upgrade installs the new operating system and automatically migrates your apps, data, and settings" (Esta actualización en contexto instala el nuevo sistema operativo y migra automáticamente sus aplicaciones, datos y configuración).  

        - Cuadro de texto 3: especifica la última línea de texto debajo del texto en negrita. Por ejemplo, en la notificación de usuario predeterminada, esta sección contiene: "Click Install to begin" (Haga clic en Instalar para comenzar). De lo contrario, haga clic en Cancelar".  

#### <a name="example"></a>Ejemplo

Supongamos que configura la siguiente notificación personalizada en las propiedades.

![Pestaña de notificación de usuario personalizada de las propiedades de la secuencia de tareas](../media/user-notification.png)

Se mostrará el siguiente mensaje de notificación cuando el usuario final abra la instalación desde el Centro de software.

![Notificación de la secuencia de tareas personalizada que se muestra al usuario final desde el Centro de software](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a>Mejoras en el rendimiento para los planes de energía

<!--3555926-->

A partir de la versión 1910, ahora puede ejecutar una secuencia de tareas con el plan de energía de alto rendimiento. Esta opción mejora la velocidad total de la secuencia de tareas. Configura Windows para usar el plan de energía de alto rendimiento integrado, que brinda el máximo rendimiento con el consiguiente aumento del consumo de energía. Esta opción está activada de forma predeterminada para las nuevas secuencias de tareas.

Cuando se inicia la secuencia de tareas, en la mayoría de los escenarios registra el plan de energía actualmente habilitado. A continuación, cambia el plan de energía activo al plan de **alto rendimiento** predeterminado de Windows. Si la secuencia de tareas reinicia el equipo, repite este proceso. Al final de la secuencia de tareas, restablece el plan de energía en el valor almacenado. Esta funcionalidad sirve tanto en Windows como en Windows PE, pero no tiene impacto en las máquinas virtuales.

- Si la secuencia de tareas se inicia en Windows PE, esta no registra el plan de energía habilitado actualmente para su reutilización posterior.

- Una secuencia de tareas de implementación de SO que restablece la imagen inicial del equipo (instalación desde cero) no conserva la configuración del plan de energía del SO anterior. Al final de la secuencia de tareas, restaura el plan de energía predeterminado **Equilibrado**.

> [!Important]
> Para aprovechar esta nueva característica de Configuration Manager, después de actualizar el sitio, actualice los clientes a la versión más reciente. Actualice también las imágenes de arranque para incluir los componentes cliente más recientes. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Sistemas operativos** y seleccione el nodo **Secuencias de tareas**.

1. Cree una secuencia de tareas o elija una existente y, luego, seleccione **Propiedades**.

1. Cambie a la pestaña **Rendimiento**.

1. Habilite la opción para **ejecutar como plan de energía de alto rendimiento**.

> [!Warning]
> Tenga cuidado con esta configuración en hardware de rendimiento bajo. Ejecutar operaciones intensas del sistema durante un período de tiempo prolongado puede sobrecargar hardware lentos. Consulte al fabricante de hardware para obtener guías específicas.

### <a name="known-issue"></a>Problema conocido

<!-- 5554928 -->

Normalmente, al cambiar la configuración en las propiedades de la secuencia de tareas, se actualizan todas las implementaciones existentes. Al cambiar esta configuración de rendimiento en las propiedades de la secuencia de tareas, las implementaciones existentes de la secuencia de tareas no se ven afectadas. Para habilitar o deshabilitar esta configuración para alto rendimiento, cree una implementación de la secuencia de tareas.
<!-- MEMDocs#437, SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a> Distribución del contenido al que se hace referencia  

Antes de que los clientes ejecuten una secuencia de tareas que haga referencia a contenido, distribuya dicho contenido a los puntos de distribución. En cualquier momento, puede seleccionar la secuencia de tareas y distribuir su contenido para crear una nueva lista de paquetes de referencia para su distribución. Si realiza cambios en la secuencia de tareas con contenido actualizado, redistribuya el contenido antes de que esté disponible para los clientes. Utilice el siguiente procedimiento para distribuir el contenido al que hace referencia una secuencia de tareas.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Proceso para distribuir el contenido al que se hace referencia a los puntos de distribución  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee distribuir.  

3. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y seleccione **Distribuir contenido**. Esta acción inicia al Asistente para distribuir contenido.  

4. En la página **General** , compruebe que esté seleccionada la secuencia de tareas correcta para la distribución.  

5. En la página **Contenido**, compruebe el contenido que se va a distribuir, como la imagen de arranque a la que hace referencia la secuencia de tareas.  

6. En la página **Destino del contenido**, especifique las recopilaciones, el punto de distribución o el grupo de puntos de distribución donde quiera distribuir el contenido de la secuencia de tareas.  

    > [!IMPORTANT]  
    > Si la secuencia de tareas seleccionada hace referencia a contenido que ya se distribuyó a un punto de distribución específico, el asistente no muestra ese punto de distribución.  

7. Complete el asistente.  

También puede preconfigurar el contenido al que se hace referencia en la secuencia de tareas. Configuration Manager crea un archivo de contenido preconfigurado comprimido que contiene los archivos, las dependencias asociadas y los metadatos asociados del contenido que se selecciona. A continuación puede importar manualmente el contenido en un servidor de sitio, un sitio secundario o un punto de distribución. Para más información sobre cómo preconfigurar archivos de contenido, consulte [Preconfigurar el contenido](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a> Implementar  

Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a> Exportación e importación  

Exporte e importe secuencias de tareas con o sin sus objetos relacionados. Este contenido al que se hace referencia incluye los siguientes objetos:  

- Imágenes de SO  
- Imágenes de arranque  
- Paquetes como el cliente de instalación del cliente  
- Paquetes de controladores  
- Aplicaciones con dependencias  

Considere los puntos siguientes al exportar e importar secuencias de tareas:  

- Configuration Manager no exporta contraseñas en la secuencia de tareas. Si exporta e importa una secuencia de tareas que contiene contraseñas, edite la secuencia de tareas importada para especificar las contraseñas de nuevo. Revise los siguientes pasos que pueden incluir una contraseña:  

  - [Unirse a dominio o grupo de trabajo](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [Conectar a carpeta de red](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- Cuando exporta una secuencia de tareas con el paso **Establecer variables dinámicas**, Configuration Manager no exporta ningún valor para las variables que configure con la opción **Valor secreto**. Vuelva a escribir los valores de estas variables después de importar la secuencia de tareas.  

- Si tiene varios sitios primarios, importe las secuencias de tareas en el sitio de administración central.  

### <a name="process-to-export-task-sequences"></a>Proceso para exportar secuencias de tareas  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que va a exportar. Si selecciona más de una secuencia de tareas, se almacenan en un archivo de exportación.  

3. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Secuencia de tareas** y seleccione **Exportar**. Esta acción inicia al Asistente para exportar secuencia de tareas.  

4. En la página **General** , especifique la siguiente configuración:  

    - **Archivo**: especifique la ubicación y el nombre del archivo de exportación. Si escribe el nombre de archivo directamente, asegúrese de incluir la extensión .zip. Si examina el archivo de exportación, el asistente agrega automáticamente esta extensión de nombre de archivo.  

    - Si no desea exportar las dependencias de secuencia de tareas, desactive la opción de **Exportar todas las dependencias de secuencia de tareas**. De forma predeterminada, el asistente explora todos los objetivos relacionados y los exporta con la secuencia de tareas. Estas dependencias incluyen secuencias de tareas para las aplicaciones.  

    - Si no desea copiar el contenido del origen de paquete en la ubicación de exportación, desactive la opción de **Exportar todo el contenido de las secuencias de tareas y las dependencias seleccionadas**. Si activa esta opción, el Asistente para importar secuencia de tareas utiliza la ruta de acceso de importación como la nueva ubicación del origen de paquete.  

    - **Comentarios del administrador**: agregue una descripción de las secuencias de tareas que se van a exportar.  

5. Complete el asistente.  

El asistente crea los siguientes archivos de salida:  

- Si no se exporta contenido: un archivo .zip.  

- Si se exporta contenido: un archivo .zip y una carpeta *export*_files, donde *export* es el nombre del archivo .zip que contiene el contenido exportado.  

Si incluye contenido cuando exporta una secuencia de tareas, asegúrese de que copia el archivo .zip y la carpeta *export*_files; de lo contrario, la importación no se completará correctamente.  

### <a name="process-to-import-task-sequences"></a>Proceso para importar secuencias de tareas  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Crear** y seleccione **Importar secuencia de tareas**. Esta acción inicia al Asistente para importar secuencia de tareas.  

3. En la página **General** de la cinta de opciones, especifique el archivo .zip exportado.  

4. En la página **Contenido del archivo** , seleccione la acción que requiere para cada objeto que importa. En esta página se muestran todos los objetos que Configuration Manager ha encontrado para importar.  

    - Si es la primera vez que se importó el objeto, seleccione **Crear nuevo**.  

    - Si no es la primera vez que se importa, seleccione una de las siguientes acciones:  

        - **Omitir duplicado** (predeterminado): esta acción no importa el objeto. En su lugar, el asistente vincula el objeto existente con la secuencia de tareas.  

        - **Sobrescribir**: esta acción sobrescribe el objeto existente con el objeto importado. Para aplicaciones, puede agregar una revisión para actualizar la aplicación existente o crear una aplicación nueva.  

5. Complete el asistente.  

Después de importar la secuencia de tareas, edítela para especificar las contraseñas que se encontraban en la secuencia de tareas original. Por motivos de seguridad, no se exportan las contraseñas.  

## <a name="return-to-previous-page-on-failure"></a>Volver a la página anterior en caso de error

Al ejecutar una secuencia de tareas y se produce un error, puede volver a la página anterior del Asistente para secuencia de tareas. En versiones anteriores de Configuration Manager, tenía que reiniciar la secuencia de tareas si se producía un error. Use el botón **Anterior** en los siguientes escenarios:

- Cuando un equipo se inicia en Windows PE, el cuadro de diálogo de arranque de la secuencia de tareas puede mostrarse antes de que la secuencia de tareas esté disponible. Cuando hace clic en Siguiente en este escenario, la página final de la secuencia de tareas se muestra con un mensaje de que no existe ninguna secuencia de tareas disponible. Ahora, puede seleccionar **Anterior** para buscar de nuevo secuencias de tareas disponibles. Puede repetir este proceso hasta que la secuencia de tareas esté disponible.  

- Cuando ejecuta una secuencia de tareas, pero los paquetes de contenido dependientes todavía no están disponibles en los puntos de distribución, se produce un error en la secuencia de tareas. Si aún no se ha distribuido el contenido que falta, distribúyalo ahora. También puede esperar a que el contenido esté disponible en los puntos de distribución. Después, seleccione **Anterior** para que la secuencia de tareas busque de nuevo el contenido.

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a> Variables de recopilación y dispositivo

Puede definir variables de secuencia de tareas personalizadas para equipos y recopilaciones. Las variables que se definen para un determinado equipo se conocen como variables de secuencia de tareas por equipo. Las variables definidas para una determinada recopilación se conocen como variables de secuencia de tareas por recopilación. Para obtener más información, vea [Variables de recopilación y dispositivo](../understand/using-task-sequence-variables.md#bkmk_set-coll-var).

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a> Acciones adicionales  

Puede administrar secuencias de tareas con acciones adicionales cuando se selecciona la secuencia de tareas.  

### <a name="edit"></a>Editar

Para más información, vea [Uso del editor de secuencias de tareas](../understand/task-sequence-editor.md#bkmk_edit).

### <a name="enable"></a>Habilitar

Habilita la secuencia de tareas para que los clientes la puedan ejecutar. No es necesario volver a implementar una secuencia de tareas después de habilitarla.  

### <a name="disable"></a>Deshabilitar

Deshabilita la secuencia de tareas para que no pueda ejecutarse en equipos. Puede implementar una secuencia de tareas deshabilitada, pero los equipos no la ejecutarán hasta que la habilite.  

### <a name="export"></a>Exportar

Para más información, consulte [Exportar e importar secuencias de tareas](#BKMK_ExportImport).

### <a name="copy"></a>Copiar

Realiza una copia de la secuencia de tareas seleccionada. Esta acción es útil para crear una secuencia de tareas basada en una secuencia de tareas existente.

Al realizar una copia de una secuencia de tareas en una carpeta, la copia se muestra en la carpeta hasta que actualice el nodo de secuencia de tareas. Después de la actualización, la copia aparece en la carpeta raíz.  

### <a name="refresh"></a>Actualizar

Actualiza los detalles de la secuencia de tareas seleccionada.

### <a name="delete"></a>Eliminar

Elimina la secuencia de tareas seleccionada.

### <a name="create-phased-deployment"></a>Crear una implementación por fases

Para más información, vea [Crear implementaciones por fases](create-phased-deployment-for-task-sequence.md).

### <a name="deploy"></a>Implementar

Para obtener más información, vea [Deploy a task sequence](deploy-a-task-sequence.md).

### <a name="distribute-content"></a>Distribuir contenido

Inicia el Asistente para distribuir contenido para enviar el contenido al que se hace referencia a los puntos de distribución.

### <a name="create-prestaged-content-file"></a>Crear archivo de contenido preconfigurado

Inicia el Asistente para crear archivos de contenido preconfigurados para preconfigurar el contenido de la secuencia de tareas. Para obtener información sobre cómo crear un archivo de contenido preconfigurado, consulte [Preconfigurar el contenido](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).

### <a name="move"></a>Mover

Mueve la secuencia de tareas a otra carpeta en el nodo **Secuencias de tareas**.

### <a name="set-security-scopes"></a>Establecer ámbitos de seguridad

Seleccione los ámbitos de seguridad para la secuencia de tareas seleccionada. Para obtener más información, consulte [Ámbitos de seguridad](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

### <a name="properties"></a>Propiedades

Para obtener más información, consulte [Configurar propiedades del Centro de software](#bkmk_prop-general) y [Configuración de los ajustes de la secuencia de tareas avanzada](#bkmk_prop-advanced).

### <a name="view"></a>Ver

<!--3633146-->
A partir de la versión 1902, la acción **Ver** de las secuencias de tareas es la predeterminada. Esta acción le permite ver los pasos de la secuencia de tareas sin bloquearla para su edición. Para más información, vea [Uso del editor de secuencias de tareas](../understand/task-sequence-editor.md#bkmk_view).

## <a name="see-also"></a>Vea también

- [Escenarios para implementar sistemas operativos de empresa](scenarios-to-deploy-enterprise-operating-systems.md)

- [Uso del editor de secuencias de tareas](../understand/task-sequence-editor.md)

- [Implementación de una secuencia de tareas](deploy-a-task-sequence.md)

- [Pasos de la secuencia de tareas](../understand/task-sequence-steps.md)

- [Variables de recopilación y dispositivo](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [Crear implementaciones por fases](create-phased-deployment-for-task-sequence.md)
