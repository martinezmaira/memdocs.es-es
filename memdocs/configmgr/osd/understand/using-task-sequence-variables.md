---
title: Uso de variables en una secuencia de tareas
titleSuffix: Configuration Manager
description: Obtenga información sobre el uso de variables en una secuencia de tareas de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7013ae10de753cbcb664771bd30dc51b259aa390
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697558"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Uso de variables en una secuencia de tareas en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

 El motor de secuencia de tareas en la característica de implementación de sistema operativo de Configuration Manager usa muchas variables para controlar sus comportamientos. Use estas variables para:

- Establecer las condiciones en los pasos  
- Cambiar los comportamientos de determinados pasos  
- Usar en scripts para acciones más complejas  

Para consultar una referencia de todas las variables de secuencia de tareas disponibles, conste [Variables de secuencia de tareas](task-sequence-variables.md).

## <a name="types-of-variables"></a><a name="bkmk_types"></a> Tipos de variables

Hay varios tipos de variables:  

- [Integrada](#bkmk_built-in)  
- [Acción](#bkmk_action)  
- [Personalizado](#bkmk_custom)  
- [Solo lectura](#bkmk_read-only)  
- [Matriz](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a> Variables integradas

Las variables integradas proporcionan información sobre el entorno donde se ejecuta la secuencia de tareas. Sus valores están disponibles a lo largo de toda la secuencia de tareas. Por lo general, el motor de secuencia de tareas inicializa las variables integradas antes de ejecutar los pasos.

Por ejemplo, `_SMSTSLogPath` es una variable de entorno que especifica la ruta de acceso en la que los componentes de Configuration Manager escriben archivos de registro. Cualquier paso de secuencia de tareas puede tener acceso a esta variable de entorno.

La secuencia de tareas evalúa algunas de las variables antes de cada paso. Por ejemplo, `_SMSTSCurrentActionName` muestra el nombre del paso actual.

### <a name="action-variables"></a><a name="bkmk_action"></a> Variables de acción

Las variables de acción de secuencia de tareas especifican los valores de configuración que utiliza un único paso de una secuencia de tareas. De forma predeterminada, el paso inicializa su configuración antes de ejecutarse. Esta configuración solo está disponible mientras se está ejecutando el paso asociado de la secuencia de tareas. La secuencia de tareas agrega el valor de la variable de acción al entorno antes de ejecutar el paso. Luego, quita el valor del entorno después de que se ejecuta el paso.

Por ejemplo, agrega el paso **Ejecutar línea de comandos** a una secuencia de tareas. Este paso incluye un propiedad **Iniciar en**. La secuencia de tareas almacena un valor predeterminado para esta propiedad como variable `WorkingDirectory`. La secuencia de tareas inicializa este valor antes de ejecutar el paso **Ejecutar línea de comandos**. Mientras se ejecuta este paso, acceda al valor de propiedad **Iniciar en** desde el valor `WorkingDirectory`. Una vez completado el paso, la secuencia de tareas quita el valor de la variable `WorkingDirectory` del entorno. Si la secuencia de tareas incluye otro paso **Ejecutar línea de comandos**, inicializa una nueva variable `WorkingDirectory`. En ese momento, la secuencia de tareas establece la variable como el valor inicial para el paso actual. Para obtener más información, consulte [WorkingDirectory](task-sequence-variables.md#WorkingDirectory).  

El valor *predeterminado* de una variable de acción está presente cuando se ejecuta el paso. Si establece un *nuevo* valor, estará disponible para varios pasos de la secuencia de tareas. Si reemplaza un valor predeterminado, el nuevo valor permanece en el entorno. Este nuevo valor reemplaza al valor predeterminado para otros pasos en la secuencia de tareas. Por ejemplo, agregue un paso **Configurar variable de secuencia de tareas** como primer paso de la secuencia de tareas. En este paso se establece la variable de `WorkingDirectory` en `C:\`. Cualquier paso de **Ejecutar línea de comandos** de la secuencia de tareas usa el nuevo valor de directorio inicial.  

Algunos pasos de secuencia de tareas marcan determinadas variables de acción como *salida*. Las pasos que tienen lugar posteriormente en la secuencia de tareas leen estas variables de salida.

> [!Note]  
> No todos los pasos de secuencia de tareas tienen variables de acción. Por ejemplo, aunque hay variables asociadas a la acción **Habilitar BitLocker**, no hay ninguna variable asociada a la acción **Deshabilitar BitLocker**.  

### <a name="custom-variables"></a><a name="bkmk_custom"></a> Variables personalizadas

Estas variables son aquellas que Configuration Manager no crea. Inicialice sus propias variables para usarlas como condiciones, en líneas de comandos o en scripts.

Cuando especifique un nombre para una nueva variable de secuencia de tareas, siga estas instrucciones:  

- El nombre de la variable de secuencia de tareas puede incluir letras, números, el carácter de subrayado (`_`) y un guión (`-`).  

- El nombre de la variable de secuencia de tareas tiene una longitud mínima de 1 carácter y una longitud máxima de 256 caracteres.  

- Las variables definidas por el usuario deben comenzar con una letra (`A-Z` o `a-z`).  

- Los nombres de las variables definidas por el usuario no pueden comenzar con el carácter de subrayado. Únicamente las variables de secuencia de tareas de solo lectura van precedidas por el carácter de subrayado.  

- Los nombres de variables de secuencia de tareas no distinguen mayúsculas de minúsculas. Por ejemplo, `OSDVAR` y `osdvar` son la misma variable de secuencia de tareas.  

- Los nombres de variables de secuencia de tareas no pueden comenzar ni terminar con un espacio. Tampoco pueden contener espacios incrustados. La secuencia de tareas ignora los espacios que quedan al principio o al final de un nombre de variable.  

No hay ningún límite establecido respecto al número de variables de secuencias de tareas que puede crear. Sin embargo, el número de variables está limitado por el tamaño del entorno de secuencia de tareas. El límite de tamaño total para el entorno de secuencia de tareas es de 8 KB. Para más información, consulte [Reducción del tamaño de la directiva de secuencia de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize).

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a> Variables de solo lectura

No se puede cambiar el valor de algunas variables, que son de solo lectura. Normalmente, el nombre comienza con un carácter de subrayado (`_`). La secuencia de tareas las usa para sus operaciones. Las variables de solo lectura están visibles en el entorno de secuencia de tareas.

Estas variables son útiles en los scripts o líneas de comandos. Por ejemplo, la ejecución de una línea de comandos y la canalización de la salida a un archivo de registro de `_SMSTSLogPath` con los demás archivos de registro.

> [!NOTE]  
> Los pasos de secuencia de tareas pueden leer las variables de secuencia de tareas de solo lectura en una secuencia de tareas, pero no pueden configurarse. Por ejemplo, utilice una variable de solo lectura como parte de la línea de comandos para un paso **Ejecutar línea de comandos**. No puede establecer una variable de solo lectura mediante el paso **Configurar variable de secuencia de tareas**.  

### <a name="array-variables"></a><a name="bkmk_array"></a> Variables de matriz

La secuencia de tareas almacena algunas de las variables como una matriz. Cada uno de los elementos de la matriz representa la configuración de un único objeto. Use estas variables cuando un dispositivo tenga más de un objeto que configurar. Los siguientes pasos de secuencia de tareas utilizan variables de matriz:

- [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a> Configuración de las variables

En el caso de las variables personalizadas o las variables que no son de solo lectura, existen varios métodos para inicializar y establecer el valor de la variable:  

- Paso [Configurar variable de secuencia de tareas](#bkmk_set-ts-step)
- Paso [Establecer variables dinámicas](#bkmk_set-dyn-step)
- Paso [Ejecutar script de PowerShell](#bkmk_run-ps)
- [Variables de recopilación y dispositivo](#bkmk_set-coll-var)  
- [Objeto COM TSEnvironment](#bkmk_set-com)  
- [Comando de preinicio](#bkmk_set-prestart)  
- [Asistente para secuencia de tareas](#bkmk_set-tswiz)
- [Asistente para crear medio de secuencia de tareas](#bkmk_set-media)  

Elimine una variable del entorno con alguno de los métodos que sirven para crear una variable. Para eliminar una variable, establezca el valor de la variable en una cadena vacía.  

Puede combinar métodos para establecer una variable de secuencia de tareas en valores diferentes para la misma secuencia. Por ejemplo, establezca los valores predeterminados mediante el editor de secuencia de tareas y, a continuación, establezca valores personalizados mediante un script.

Si establece la misma variable por medio de distintos métodos, el motor de secuencia de tareas utiliza el siguiente orden:  

1. Primero se evalúan las variables de la recopilación.  

2. Las variables específicas de dispositivo invalidan la misma variable establecida en una recopilación.  

3. Las variables establecidas por cualquier método durante la secuencia de tareas tienen prioridad sobre las variables de la recopilación o el dispositivo.  

### <a name="general-limitations-for-task-sequence-variable-values"></a>Limitaciones generales para los valores de las variables de secuencia de tareas

- Los valores de las variables de secuencia de tareas no pueden superar los 4000 caracteres.  

- No se puede cambiar una variable de secuencia de tareas de solo lectura. Las variables de solo lectura tienen nombres que empiezan por un carácter de subrayado (`_`).  

- Los valores de variables de secuencias de tareas pueden distinguir entre mayúsculas y minúsculas dependiendo del uso del valor. En la mayoría de los casos, los valores de variables de secuencias de tareas no distinguen entre mayúsculas y minúsculas. Una variable que incluye una contraseña distingue mayúsculas de minúsculas.  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a> Establecer variable de secuencia de tareas

Utilice este paso en la secuencia de tareas para establecer una única variable en un solo valor.

Para más información, vea [Configurar variable de secuencia de tareas](task-sequence-steps.md#BKMK_SetTaskSequenceVariable).

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a> Establecer variables dinámicas

Utilice este paso en la secuencia de tareas para establecer una o varias variables de secuencia de tareas. Defina reglas en este paso para determinar las variables y los valores que se usarán.

Para obtener más información, consulte [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a> Ejecutar script de PowerShell

<!-- 6315548 -->

Use este paso en la secuencia de tareas para usar un script de PowerShell para establecer una variable de secuencia de tareas.

Puede especificar un nombre de script de un paquete o escribir directamente un script de PowerShell en el paso. A continuación, use la propiedad del paso para la **salida a la variable de secuencia de tareas** a fin de guardar la salida del script en una variable de secuencia de tareas personalizada.

Para más información sobre este paso, vea [Ejecutar script de PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).

> [!NOTE]
> También puede usar un script de PowerShell para establecer una o varias variables con el objeto **TSEnvironment**. Para obtener más información, consulte [How to use variables in a running task sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) (Uso de variables en una secuencia de tareas en ejecución) en el SDK de Configuration Manager.

#### <a name="example-scenario-with-run-powershell-script-step"></a>Escenario de ejemplo con el paso Ejecutar script de PowerShell

Su entorno tiene usuarios en varios países o regiones, por lo que desea consultar el idioma del sistema operativo para establecerlo como una condición en varios pasos de **Aplicar sistema operativo** específicos del idioma.

1. Agregue una instancia de **Ejecutar script de PowerShell** a la secuencia de tareas antes de que se apliquen los pasos de **Aplicar sistema operativo**.

1. Use la opción **Especificar un script de PowerShell** para especificar el comando siguiente:

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    Para obtener más información sobre el cmdlet, vea [Get-Culture](/powershell/module/microsoft.powershell.utility/get-culture). Para obtener más información sobre los nombres de dos letras de los idiomas de ISO, consulte la [lista de códigos ISO 639-1](https://wikipedia.org/wiki/List_of_ISO_639-1_codes).

1. Para la opción de la **salida a la variable de secuencia de tareas**, especifique `CurrentOSLanguage`.

    ![Captura de pantalla del paso Ejecutar script de PowerShell](media/run-powershell-script-example-language.png)

1. En el paso **Aplicar sistema operativo** para la imagen del idioma inglés, cree la siguiente condición: `Task Sequence Variable CurrentOSLanguage equals "en"`

    ![Captura de pantalla de la condición de ejemplo en el paso Aplicar sistema operativo](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > Para obtener más información sobre cómo crear una condición en un paso, vea [Acceso a las variables - Condición de paso](#bkmk_access-condition).

1. Guarde e implemente la secuencia de tareas.

Cuando se ejecuta el paso **Ejecutar script de PowerShell** en un dispositivo con la versión en inglés de Windows, el comando devuelve el valor `en`. A continuación, guarda ese valor en la variable personalizada. Cuando se ejecuta el paso **Aplicar sistema operativo** para la imagen del idioma inglés en el mismo dispositivo, la condición se evalúa como verdadera. Si tiene varias instancias del paso **Aplicar sistema operativo** para distintos idiomas, la secuencia de tareas ejecuta dinámicamente el paso que coincide con el idioma del sistema operativo.

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a> Variables de recopilación y dispositivo

Puede definir variables de secuencia de tareas personalizadas para dispositivos y recopilaciones. Las variables que se definen para un determinado dispositivo se conocen como variables de secuencia de tareas por dispositivo. Las variables definidas para una determinada recopilación se conocen como variables de secuencia de tareas por recopilación. Si hay un conflicto, las variables por dispositivo tienen prioridad sobre las variables por recopilación. Este comportamiento significa que las variables de secuencia de tareas asignadas a un determinado dispositivo tienen automáticamente más prioridad que las asignadas a la recopilación que contiene el dispositivo.  

Por ejemplo, el dispositivo XYZ es miembro de la recopilación ABC. Asigna MiVariable a la recopilación ABC con un valor de 1. También asigna MiVariable al dispositivo XYZ con un valor de 2. La variable que se asigna a XYZ tiene mayor prioridad que la variable que se asigna a la recopilación ABC. Cuando se ejecuta una secuencia de tareas con esta variable en XYZ, MiVariable tiene un valor de 2.

Puede ocultar las variables por dispositivo y por recopilación para que no sean visibles en la consola de Configuration Manager. Cuando se usa la opción **No mostrar este valor en la consola de Configuration Manager**, el valor de la variable no se muestra en la consola. El archivo de registro de la secuencia de tareas (**smsts.log**) o el depurador de secuencias de tareas no mostrarán el valor de la variable. Aun así, la secuencia de tareas puede seguir usando la variable cuando se ejecute. Si ya no desea que estas variables estén ocultas, elimínelas en primer lugar. A continuación, vuelva a definir las variables sin seleccionar la opción para ocultarlas.  

> [!WARNING]  
> Si incluye variables en el paso **Run Command Line** (Ejecutar línea de comandos), el archivo de registro de la secuencia de tareas muestra la línea de comandos completa, incluidos los valores de las variables. Para evitar que datos posiblemente confidenciales aparezcan en el archivo de registro, establezca la variable de secuencia de tareas **OSDDoNotLogCommand** en `TRUE`.

Puede administrar las variables por dispositivo en un sitio primario o en un sitio de administración central. Configuration Manager no admite más de 1000 variables asignadas en un dispositivo.  

> [!IMPORTANT]  
> Cuando se usan variables por recopilación para secuencias de tareas, tenga en cuenta los comportamientos siguientes:  
>
> - Los cambios en las recopilaciones siempre se replican por toda la jerarquía. Los cambios que realice en las variables de la recopilación se aplicarán no solo a los miembros del sitio actual, sino a todos los miembros de la recopilación en la jerarquía.  
>  
> - Cuando se elimina una recopilación también se eliminan las variables de secuencia de tareas que configuró para la recopilación.  

#### <a name="create-task-sequence-variables-for-a-device"></a>Creación de variables de secuencia de tareas para un *dispositivo*

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y haga clic en el nodo **Dispositivos**.  

2. Seleccione el dispositivo de destino y elija **Propiedades**.  

3. En el cuadro de diálogo **Propiedades**, cambie a la pestaña **Variables**.  

4. Para cada variable que quiera crear, seleccione el icono **Nuevo**. Especifique el **Nombre** y el **Valor** de la variable de la secuencia de tareas. Active la opción **No mostrar este valor en la consola de Configuration Manager** si desea ocultar la variable para que no esté visible en la consola de Configuration Manager.  

5. Después de agregar todas las variables a las propiedades del dispositivo, seleccione **Aceptar**.  

#### <a name="create-task-sequence-variables-for-a-collection"></a>Creación de variables de secuencia de tareas para una *recopilación*

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Recopilaciones de dispositivos**. Seleccione la recopilación de destino y elija **Propiedades**.  

2. En el cuadro de diálogo **Propiedades**, cambie a la pestaña **Variables de la recopilación**.  

3. Para cada variable que quiera crear, seleccione el icono **Nuevo**. Especifique el **Nombre** y el **Valor** de la variable de la secuencia de tareas. Active la opción **No mostrar este valor en la consola de Configuration Manager** si desea ocultar la variable para que no esté visible en la consola de Configuration Manager.  

4. Si lo desea, especifique la prioridad de Configuration Manager que desea utilizar cuando se evalúen las variables de la secuencia de tareas.  

5. Después de agregar todas las variables a las propiedades de la recopilación, seleccione **Aceptar**.  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a> Objeto COM TSEnvironment

Para trabajar con variables de un script, use el objeto **TSEnvironment**.

Para obtener más información, consulte [How to use variables in a running task sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) (Uso de variables en una secuencia de tareas en ejecución) en el SDK de Configuration Manager.

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a> Comando de preinicio

El comando de preinicio es un script o un archivo ejecutable que se ejecuta en Windows PE antes de que el usuario seleccione la secuencia de tareas. El comando de preinicio puede consultar una variable o pedir información al usuario y, luego, guardarla en el entorno. Use el objeto COM [TSEnvironment](#bkmk_set-com) para leer y escribir variables desde el comando de preinicio.

Para obtener más información, consulte [Prestart commands for task sequence media](prestart-commands-for-task-sequence-media.md) (Comandos de preinicio para medios de secuencia de tareas).

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a> Asistente para secuencia de tareas

A partir de la versión 1906, después de seleccionar una secuencia de tareas en la ventana del Asistente para secuencia de tareas, la página para editar las variables de secuencia de tareas incluye un botón **Editar**. Puede usar métodos abreviados de teclado accesibles para editar las variables. Este cambio ayuda en casos en los que no hay un mouse disponible.<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a> Asistente para crear medio de secuencia de tareas

Especifique las variables de secuencias de tareas que se ejecutan desde un medio. Cuando se utiliza un medio para implementar el sistema operativo, se agregan las variables de secuencia de tareas y se especifican sus valores al crear el medio. Las variables y sus valores se almacenan en el medio.  

> [!NOTE]  
> Las secuencias de tareas se almacenan en medios independientes. Sin embargo, todos los demás tipos de medios, como los medios preconfigurados, recuperan la secuencia de tareas desde un punto de administración.  

Al ejecutar una secuencia de tareas desde un medio, puede agregar una variable a la página **Personalización** del asistente.

Use las variables de los medios en lugar de las variables por recopilación o por equipo. Si se está ejecutando la secuencia de tareas desde un medio, las variables por equipo y por recopilación no se aplican y no se utilizan.  

> [!TIP]  
> La secuencia de tareas escribe el identificador de paquete y la línea de comandos de preinicio en el archivo **CreateTSMedia.log** en el equipo que ejecuta la consola de Configuration Manager. Este archivo de registro incluye el valor de las variables de secuencia de tareas. Revise este archivo de registro para comprobar el valor de las variables de secuencia de tareas.  

Para obtener más información, consulte [Crear medios de secuencia de tareas ](../deploy-use/create-task-sequence-media.md).

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a> Acceso a variables

Después de especificar la variable y su valor mediante uno de los métodos indicados en la sección anterior, utilícela en sus secuencias de tareas. Por ejemplo, acceda a los valores predeterminados para las variables de secuencia de tareas integradas o condicione un paso al valor de una variable.  

Use los siguientes métodos para tener acceso a los valores de las variables en el entorno de la secuencia de tareas:

- [Usar en un paso](#bkmk_access-step)  
- [Condición de paso](#bkmk_access-condition)  
- [Script personalizado](#bkmk_access-script)  
- [Archivo de respuesta de configuración de Windows](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a> Usar en un paso

Especifique un valor de variable para un ajuste de un paso de secuencia de tareas. En el editor de secuencia de tareas, modifique el paso y especifique el nombre de variable como el valor del campo. Rodee el nombre de la variable de signos de porcentaje (`%`).

Por ejemplo, utilice el nombre de la variable como parte del campo **Línea de comandos** del paso **Ejecutar línea de comandos**. La siguiente línea de comandos escribe el nombre del equipo en un archivo de texto.

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a> Condición de paso

Use variables de secuencia de tareas integradas o personalizadas como parte de una condición en un paso o grupo. La secuencia de tareas evalúa el valor de la variable antes de ejecutar el paso o grupo.

Para agregar una condición que evalúa un valor de variable, haga lo siguiente:  

1. En el editor de secuencia de tareas, seleccione el paso o grupo al que desea agregar la condición.  

2. Cambie a la pestaña **Opciones** para el paso o grupo. Haga clic en **Agregar condición** y seleccione **Variable de secuencia de tareas**.  

3. En el cuadro de diálogo **Variable de secuencia de tareas**, especifique la siguiente configuración:  

    - **Variable**: nombre de la variable. Por ejemplo, `_SMSTSInWinPE`.  

    - **Condición**: condición para evaluar el valor variable. Por ejemplo, **igual a**.  

    - **Valor**: valor de la variable que se va a comprobar. Por ejemplo, `false`.  

Los tres ejemplos anteriores conforman en conjunto una condición para comprobar si la secuencia de tareas se está ejecutando desde una imagen de arranque de Windows PE:

> **Variable de secuencia de tareas** `_SMSTSInWinPE equals "false"`

Consulte esta condición en el grupo **Capturar archivos y configuraciones** de la plantilla de secuencia de tareas predeterminada para instalar una imagen de sistema operativo existente.

Para obtener más información sobre las condiciones, consulte [Editor de secuencias de tareas: condiciones](task-sequence-editor.md#bkmk_conditions).

### <a name="custom-script"></a><a name="bkmk_access-script"></a> Script personalizado

Lea y escriba variables mediante el objeto COM de **Microsoft.SMS.TSEnvironment** mientras la secuencia de tareas está en ejecución.

El ejemplo siguiente de Windows PowerShell consulta la variable **_SMSTSLogPath** para obtener la ubicación del registro actual. El script también establece una variable personalizada.

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a> Archivo de respuesta de configuración de Windows

El archivo de respuesta de configuración de Windows que suministre puede tener insertadas variables de secuencia de tareas. Utilice el formulario `%varname%`, donde *varname* es el nombre de la variable. El paso **Instalar Windows y Configuration Manager** sustituye la cadena del nombre de la variable por el valor real de la variable. Estas variables de secuencia de tareas insertadas no se pueden usar en campos solo numéricos de un archivo de respuesta unattend.xml.

Para obtener más información, consulte [Instalar Windows y Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).

## <a name="see-also"></a>Vea también

- [Pasos de la secuencia de tareas](task-sequence-steps.md)

- [Variables de secuencias de tareas](task-sequence-variables.md)

- [Planificación de consideraciones para la automatización de tareas](../plan-design/planning-considerations-for-automating-tasks.md)

- [Editor de secuencias de tareas](task-sequence-editor.md)