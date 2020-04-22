---
title: Comandos de preinicio para medios de secuencia de tareas
titleSuffix: Configuration Manager
description: Cree un script para usarlo con el comando de preinicio, distribuya el contenido asociado al comando de preinicio y configure el comando de preinicio en los medios.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9dd921d58e6ef777017af3e2eb24dbf4bd611fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699773"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>Comandos de preinicio para medios de secuencia de tareas en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede crear un comando de preinicio en Configuration Manager para usarlo con medios de arranque, medios independientes o medios preconfigurados. El comando de preinicio es un script o un archivo ejecutable que se ejecuta antes de que se seleccione la secuencia de tareas, y que puede interactuar con el usuario en Windows PE. El comando de preinicio puede solicitar información al usuario, y guardarla en el entorno de la secuencia de tareas, o consultar una variable de la secuencia de tareas para obtener información. Cuando se arranca el equipo de destino, se ejecuta la línea de comandos antes de que se descargue la directiva desde el punto de administración. Utilice los siguientes procedimientos para crear un script para utilizarlo con el comando de preinicio, distribuir el contenido asociado con el comando de preinicio, y configurar el comando de preinicio en el medio.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Crear un archivo de script para utilizarlo para el comando de preinicio  
 Las variables de la secuencia de tareas se pueden leer y escribir mediante el objeto COM de Microsoft.SMS.TSEnvironment mientras la secuencia de tareas está en ejecución. En el ejemplo siguiente, un archivo de script de Visual Basic consulta la variable de secuencia de tareas _SMSTSLogPath para obtener la ubicación del registro actual. El script también establece una variable personalizada.  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Crear un paquete para el archivo de script y distribuir el contenido  
 Tras crear el script o el archivo ejecutable para el comando de preinicio, debe crear un origen del paquete para hospedarlos, crear un paquete para los archivos (no se requiere ningún programa), y, a continuación, distribuir el contenido a un punto de distribución.  

 Para obtener más información sobre cómo crear un paquete, consulte [Paquetes y programas](../../apps/deploy-use/packages-and-programs.md).  

 Para obtener más información sobre la distribución de contenido, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute) (Distribución del contenido).  

## <a name="configure-the-prestart-command-in-media"></a>Configurar el comando de preinicio en medios  
 Se puede configurar un comando de preinicio en el Asistente para crear medio de secuencia de tareas para medios independientes, medios de arranque y medios preconfigurados. Para obtener más información sobre los tipos de medios, consulte [Crear medios de secuencia de tareas](../deploy-use/create-task-sequence-media.md). Utilice el siguiente procedimiento para crear un comando de preinicio en medios.  

#### <a name="to-create-a-prestart-command-in-media"></a>Para crear un comando de preinicio en medios  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear medio de secuencia de tareas** para iniciar el Asistente para crear medio de secuencia de tareas.  

4.  En la página **Seleccionar tipo de medio** , seleccione **Medio independiente**, **Medio de arranque**o **Medio preconfigurado**y, a continuación, haga clic en **Siguiente**.  

5.  Desplácese a la página **Personalización** del asistente. Para obtener más información sobre la configuración del resto de las páginas del asistente, consulte [Crear medios de secuencia de tareas](../deploy-use/create-task-sequence-media.md).  

6.  En la página **Personalización** , especifique la siguiente información y, a continuación, haga clic en **Siguiente**.  

    -   Seleccione **Habilitar comando de preinicio**.  

    -   En el cuadro de texto **Línea de comandos** , introduzca el script o el archivo ejecutable que creó para el comando de preinicio.  

        > [!IMPORTANT]  
        >  Use **cmd /C <comando de preinicio\>** para especificar el comando de preinicio. Por ejemplo, si utilizó TSScript.vbs como nombre del script del comando de preinicio, debería escribir **cmd /C TSScript.vbs** como la línea de comandos. Donde **cmd /C** abre una ventana de intérprete de comandos de Windows, y utiliza la variable de entorno Path para localizar el archivo ejecutable o el script del comando de preinicio. También puede especificar la ruta de acceso completa al comando de preinicio, aunque la letra de unidad puede variar en función de las configuraciones de unidad de los equipos.  

    -   Seleccione **Incluir archivos para el comando de preinicio**.  

    -   Haga clic en **Establecer** para seleccionar el paquete que se va a asociar con los archivos del comando de preinicio.  

    -   Haga clic en **Examinar** para seleccionar el punto de distribución que hospeda el contenido para el comando de preinicio.  

7.  Complete el asistente.  
