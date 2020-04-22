---
title: Uso del editor de secuencias de tareas
titleSuffix: Configuration Manager
description: Procedimiento para usar el editor de secuencias de tareas en la consola de Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047ae9e276ac94b633d1dc30814ed641cd34d03
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691153"
---
# <a name="use-the-task-sequence-editor"></a>Uso del editor de secuencias de tareas

*Se aplica a: Configuration Manager (rama actual)*

Edite secuencias de tareas en la consola de Configuration Manager con el **editor de secuencias de tareas**. Use el editor para:  

- Abrir una vista de solo lectura de la secuencia de tareas

- Agregar o quitar pasos de la secuencia de tareas  

- Cambiar el orden de los pasos de la secuencia de tareas  

- Agregar o quitar grupos de pasos  

- Copiar y pegar pasos entre secuencias de tareas

- Establecer opciones de pasos, por ejemplo, si la secuencia de tareas continúa cuando se produce un error  

- Agregar condiciones a los pasos y grupos de una secuencia de tareas  

- Copiar y pegar condiciones entre pasos de una secuencia de tareas

- Realizar búsquedas en la secuencia de tareas para localizar pasos rápidamente

Para poder editar una secuencia de tareas, primero debe crearla. Para obtener más información, consulte [Administrar y crear secuencias de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md).

## <a name="about-the-task-sequence-editor"></a>Acerca del editor de secuencias de tareas

El editor de secuencias de tareas incluye los siguientes componentes:

![Captura de pantalla anotada de la ventana del editor de secuencias de tareas de ejemplo](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. Nombre de la secuencia de tareas.
2. de búsqueda. Para obtener más información, vea [Búsqueda](#bkmk_search).
3. **Propiedades** del grupo o paso seleccionado en la secuencia.

    Para obtener más información sobre las propiedades y las opciones de un paso específico, consulte [Acerca de los pasos de la secuencia de tareas](task-sequence-steps.md).

4. **Opciones** del grupo o paso seleccionado en la secuencia.

    Para obtener más información sobre las opciones generales de todos los pasos, o sobre opciones de un paso específico, consulte [Acerca de los pasos de la secuencia de tareas](task-sequence-steps.md).

    Para obtener más información sobre cómo configurar las condiciones, consulte [Condiciones](#bkmk_conditions).

5. **Agregar** un grupo o pasos.
6. **Quitar** un grupo o pasos.
7. Contraer o expandir todos los grupos.
8. Mover la posición de un grupo o un paso en la secuencia (subir o bajar).
9. La secuencia de tareas:
    - Ver el orden de los pasos y grupos.
    - Expandir o contraer un grupo.
    - Al deshabilitar un paso o grupo en sus **opciones**, se atenúa en la secuencia.
    - El icono de un paso cambia a un error rojo si hay algún problema con el paso. Por ejemplo, falta un valor obligatorio.
10. **Aceptar**: Guardar y cerrar
11. **Cancelar**: Cerrar sin guardar los cambios
12. **Aplicar**: Guardar los cambios y mantenerlo abierto.

Puede cambiar el tamaño del editor de secuencias de tareas con los controles estándar de Windows. Para cambiar el ancho de los dos paneles principales, use el mouse para seleccionar la barra entre las propiedades de la secuencia de tareas y del paso y, a continuación, arrástrela hacia la izquierda o hacia la derecha.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a> Visualización de una secuencia de tareas

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la lista **Secuencia de tareas**, seleccione la secuencia de tareas que quiere ver.  

3. En la pestaña **Inicio** de la cinta, en el grupo **Secuencia de tareas**, seleccione **Ver**.

    > [!TIP]
    > Esta acción es la predeterminada. Si hace doble clic en una secuencia de tareas, **verá** la secuencia de tareas.

Esta acción abre el editor de secuencias de tareas en modo de solo lectura. En este modo se pueden realizar estas acciones:

- Ver todos los grupos, pasos, propiedades y opciones
- Expandir y contraer grupos
- Buscar la secuencia de tareas
- Cambiar el tamaño de la ventana del editor

En este modo de solo lectura no puede hacer cambios, ni copiar un paso o condición. Esta acción tampoco bloquea la secuencia de tareas para su edición. Para obtener más información sobre estos bloqueos, consulte [Reclamación de bloqueo para editar secuencias de tareas](#bkmk_sedo).

Para hacer cambios en una secuencia de tareas, cierre el editor de secuencias de tareas que ha abierto en modo de solo lectura. Luego [edite](#bkmk_edit) la secuencia de tareas.

> [!NOTE]  
> Cuando vea o edite una secuencia de tareas creada mediante el Asistente para crear secuencia de tareas, el nombre del paso puede ser la acción o el tipo del paso. Por ejemplo, puede ver un paso con el nombre "Disco de partición 0", que es la acción de un paso de tipo [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk). Todos los pasos de la secuencia de tareas se documentan por su *tipo*, no necesariamente por el nombre del paso que se muestra en el editor.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> Editar una secuencia de tareas

Use el procedimiento siguiente para modificar una secuencia de tareas existente:  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee editar.  

3. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Secuencia de tareas** y seleccione **Editar**. Luego, realice cualquiera de las siguientes acciones:  

    - **Agregar un paso**: Seleccione **Agregar**, una categoría y, a continuación, el paso que quiera agregar. Por ejemplo, para agregar el paso [Ejecutar línea de comandos](task-sequence-steps.md#BKMK_RunCommandLine): seleccione **Agregar**, elija la categoría **General** y luego seleccione **Ejecutar línea de comandos**. Esta acción agrega el paso después del paso seleccionado actualmente.

    - **Agregar un grupo**: Seleccione **Agregar** y, a continuación, **Nuevo grupo**. Después de agregar un grupo, agregue pasos a este.  

    - **Cambiar el orden**: Seleccione el paso o grupo que quiera reordenar. A continuación, use los iconos **Subir** o **Bajar**. Solo puede mover un paso o un grupo cada vez. Estas acciones también están disponibles al hacer clic con el botón derecho en un grupo o paso.

        Puede cortar, copiar y pegar un grupo o paso. Haga clic con el botón derecho en el elemento y seleccione la acción. También puede usar métodos abreviados de teclado estándar para cada acción:

        - Cortar: **CTRL** + **X**
        - Copiar: **CTRL** + **C**
        - Pegar: **CTRL** + **V**

    - **Quitar un paso o un grupo**: seleccione el paso o el grupo y elija **Quitar**.  

4. Seleccione **Aceptar** para guardar los cambios y cerrar la ventana. Seleccione **Cancelar** para descartar los cambios y cerrar la ventana. Seleccione **Aplicar** para guardar los cambios y mantener abierto el editor de secuencias de tareas.  

Para obtener una lista de las etapas de secuencia de tareas disponibles, consulte [Pasos de la secuencia de tareas](task-sequence-steps.md).  

> [!IMPORTANT]  
> Si la secuencia de tareas tiene referencias sin asociar a un objeto como resultado de la edición, el editor requiere que corrija la referencia para cerrarse. Las posibles acciones incluyen:  
>
> - Corregir la referencia
> - Eliminar el objeto sin referencia de la secuencia de tareas  
> - Deshabilitar temporalmente el paso de la secuencia de tareas con errores hasta que se corrija o se quite la referencia errónea  

Puede abrir a la vez más de una instancia del editor de secuencias de tareas. Este comportamiento le permite comparar varias secuencias de tareas, o copiar y pegar pasos entre ellas. Puede **editar** una secuencia de tareas y **ver** otra, pero no puede llevar a cabo ambas acciones en la misma secuencia de tareas.

## <a name="conditions"></a><a name="bkmk_conditions"></a> Condiciones

Use condiciones para controlar el comportamiento de la secuencia de tareas. Agregue condiciones a un solo paso o a un grupo de pasos. La secuencia de tareas evalúa las condiciones antes de ejecutar el paso en el dispositivo. Solo ejecuta el paso si las condiciones se evalúan como "true". Si una condición se evalúa como "false", la secuencia de tareas omitirá el grupo o paso.

Use la pestaña **Opciones** para administrar las condiciones:

![Administración de las condiciones en la pestaña Opciones del editor de secuencias de tareas](media/4621098-copy-paste-ts-condition.png)

Están disponibles los siguientes tipos de condiciones:

- **Instrucción If**: Use una instrucción *If* para agrupar condiciones. Puede evaluar **todas las condiciones**, **cualquier condición**o **ninguna**.

- **Variable de secuencia de tareas**. Evalúe el valor actual de cualquier [variable de secuencia de tareas](task-sequence-variables.md) integrada, de acción, personalizada o de solo lectura en el entorno de la secuencia de tareas. Para obtener más información, consulte [Condiciones de paso](using-task-sequence-variables.md#bkmk_access-condition).

    > [!NOTE]
    > Puede usar una variable de matriz en esta condición, pero deberá especificar el miembro específico de la matriz. Por ejemplo, `OSDAdapter0EnableDHCP` especifica si el *primer* adaptador de red habilita DHCP. Para obtener más información, vea [Variables de matriz](using-task-sequence-variables.md#bkmk_array).

- **Versión del SO**: Evalúe la versión del sistema operativo del dispositivo en el que se ejecuta la secuencia de tareas. Esta lista muestra las versiones de sistema operativo generales que se usan en Configuration Manager. Para evaluar una versión más detallada del sistema operativo, como una versión específica de Windows 10, use la condición **Consultar WMI**.

- **Idioma del sistema operativo**: Evalúe el idioma del sistema operativo del dispositivo en el que se ejecuta la secuencia de tareas. Esta lista incluye los 257 idiomas que Windows admite.

- **Propiedades del archivo**: Evalúe la versión o marca de tiempo de cualquier archivo del dispositivo donde se ejecuta la secuencia de tareas.

- **Propiedades de carpeta**: Evalúe la marca de tiempo de cualquier carpeta del dispositivo donde se ejecuta la secuencia de tareas.

- **Configuración del Registro**: Evalúe cualquier valor de una clave del Registro del dispositivo en el que se ejecuta la secuencia de tareas.

- **Consultar WMI**: Especifique el espacio de nombres y la consulta que se van a evaluar en el dispositivo donde se ejecuta la secuencia de tareas.

- **Software instalado**: Especifique un archivo de Windows Installer para cargar la información del producto que debe coincidir en el dispositivo donde se ejecuta la secuencia de tareas. Puede buscar coincidencias con un producto específico o con cualquier versión del producto.

### <a name="cmdlets-for-conditions"></a>Cmdlets para condiciones

Administre las condiciones con los siguientes cmdlets de PowerShell:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-CMTSStepConditionIfStatement](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>Copiado y pegado de condiciones

<!-- 4621098 -->

Para reutilizar las condiciones de un paso a otro, a partir de la versión 1910 ahora puede copiar y pegar condiciones en el editor de secuencias de tareas. Seleccione una condición para cortarla o copiarla. Si la selección tiene elementos secundarios, se copia todo el bloque. Si hay una condición en el Portapapeles, puede pegarla con las opciones siguientes:

- Pegar antes
- Pegar después
- Pegar en (solo se aplica a condiciones anidadas)

Use los métodos abreviados de teclado estándar para copiar (**CTRL** + **C**) y cortar (**CTRL** + **X**). El método abreviado de teclado estándar **CTRL** + **V** lleva a cabo la acción de **Pegar después**.

También hay opciones nuevas para subir o bajar las condiciones en la lista.

> [!Note]  
> Puede copiar y pegar condiciones entre los pasos de una secuencia de tareas. Esta acción no se admite entre distintas secuencias de tareas.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a> Reclamación de bloqueo para editar

<!--3699337-->
Si la consola de Configuration Manager deja de responder, podría quedarse bloqueado y no poder realizar más cambios hasta que expire el bloqueo al cabo de 30 minutos. Este bloqueo forma parte del sistema SEDO (edición serializada de objetos distribuidos) de Configuration Manager. Para obtener más información, vea [Configuration Manager SEDO](../../develop/core/understand/sedo.md) (SEDO de Configuration Manager).

A partir de la versión 1906 puede borrar el bloqueo en una secuencia de tareas. Esta acción solo se aplica a la cuenta de usuario que tiene el bloqueo, en el mismo dispositivo desde el que el sitio concedió el bloqueo. Cuando intente obtener acceso a una secuencia de tareas bloqueada, ahora podrá **descartar los cambios** y seguir editando el objeto. Estos cambios se perderían de todos modos al expirar el bloqueo.

> [!TIP]
> A partir de la versión 1910, se puede borrar el bloqueo de cualquier objeto de la consola de Configuration Manager. Para obtener más información, vea [Uso de la consola de Configuration Manager](../../core/servers/manage/admin-console.md#bkmk_sedo).<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a> Buscar

<!-- 4621085 -->

Si tiene una secuencia de tareas de gran tamaño con muchos pasos y grupos, encontrar pasos específicos puede ser difícil. A partir de la versión 1910, ahora puede buscar en el editor de secuencias de tareas. Esta acción le permite localizar más rápidamente los pasos en una secuencia de tareas.

![Búsqueda en el editor de secuencias de tareas](media/4621085-task-sequence-search.png)

Escriba un término de búsqueda para comenzar. Puede limitar la búsqueda con los siguientes tipos:

- Nombre del paso
- Descripción del paso
- Tipo de paso
- Nombre del grupo
- Descripción del grupo
- Nombre de la variable
- Condiciones
- Otro tipo de contenido, como las cadenas de tipo de valores de variables o líneas de comandos

Habilita todos los ámbitos de forma predeterminada.

También puede filtrar en todos los pasos con los siguientes atributos:

- Continuar después de un error
- Tiene al menos una condición

No habilita ninguno de los filtros de forma predeterminada.

Al realizar una búsqueda, la ventana del editor resaltará en amarillo los pasos que coincidan con los criterios de búsqueda.

Acceda rápidamente a estos campos de búsqueda y navegue por los resultados de búsqueda con los siguientes métodos abreviados de teclado:

- **Control** + **F**: escriba una cadena de búsqueda.
- **Control** + **O**: seleccione las opciones de búsqueda para definir el ámbito de los resultados.
- **F3** o **ENTRAR**: avance por los resultados.
- **Mayús** + **F3**: vuelva atrás en los resultados.

## <a name="see-also"></a>Vea también

- [Administración y creación de secuencias de tareas](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [Acerca de los pasos de la secuencia de tareas](task-sequence-steps.md)

- [Uso de variables de secuencias de tareas](using-task-sequence-variables.md)

- [Uso de la consola de Configuration Manager](../../core/servers/manage/admin-console.md)
