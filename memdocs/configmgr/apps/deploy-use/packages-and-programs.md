---
title: Paquetes y programas
titleSuffix: Configuration Manager
description: Admita implementaciones que usan paquetes y programas heredados con Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2c125212a13790e196d001f53411633d1e42d4f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689293"
---
# <a name="packages-and-programs-in-configuration-manager"></a>Paquetes y programas en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager sigue siendo compatible con los paquetes y programas usados en Configuration Manager 2007. Una implementación que utilice paquetes y programas podría ser más adecuada que una aplicación cuando se implementa cualquiera de las siguientes herramientas o scripts:  

- Herramientas administrativas que no instalan una aplicación en un equipo.
- Los scripts "únicos" que no es necesario supervisar continuamente.  
- Scripts que se ejecutan según una programación periódica y no pueden usar evaluación global.

> [!TIP]  
> Considere el uso de la característica [Scripts](create-deploy-scripts.md) en la consola de Configuration Manager. Los scripts pueden ser una mejor solución para algunos de los escenarios anteriores, en lugar de paquetes y programas.

Al migrar paquetes desde una versión anterior de Configuration Manager puede implementarlos en su jerarquía de Configuration Manager. Cuando la migración se haya completado, los paquetes aparecerán en el nodo **Paquetes** del área de trabajo **Biblioteca de software**.

Puede modificar e implementar estos paquetes de la misma manera que mediante la distribución de software. El **Asistente para importar paquetes desde una definición** permanece en Configuration Manager para importar paquetes heredados. Los anuncios se convierten en implementaciones cuando migra desde Configuration Manager 2007 a una jerarquía de Configuration Manager.  

> [!NOTE]  
> Use el Administrador de conversión de paquetes para convertir paquetes y programas en aplicaciones de Configuration Manager.  
>
> A partir de la versión 1806, el administrador de conversión de paquetes está integrado con Configuration Manager. Para más información, vea [Administrador de conversión de paquetes](../pcm/package-conversion-manager.md).  

Los paquetes pueden usar algunas características nuevas de Configuration Manager, incluidos los grupos de puntos de distribución y la supervisión. No se pueden implementar aplicaciones de Microsoft Application Virtualization (App-V) con paquetes y programas en Configuration Manager. Para distribuir aplicaciones virtuales, créelas como aplicaciones de Configuration Manager. Para obtener más información, consulte [Implementación de aplicaciones virtuales de App-V](../get-started/deploying-app-v-virtual-applications.md).  


## <a name="create-a-package-and-program"></a>Crear un paquete y programa

### <a name="use-the-create-package-and-program-wizard"></a>Use el asistente para crear paquetes y programas

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Crear paquete**.  

3. En el **paquete** página de la **crear un paquete y programa asistente**, especifique la siguiente información:  

    - **Nombre**: especifique un nombre para el paquete con un máximo de 50 caracteres.  

    - **Descripción**: especifique una descripción para este paquete con un máximo de 128 caracteres.  

    - **Fabricante** (opcional): especifique un nombre de fabricante para ayudarle a identificar el paquete en la consola de Configuration Manager. Este nombre puede ser un máximo de 32 caracteres.

    - **Idioma** (opcional): especifique la versión de idioma del paquete con un máximo de 32 caracteres.  

    - **Versión** (opcional): especifique un número de versión del paquete con un máximo de 32 caracteres.

    - **Este paquete contiene archivos de origen**: este valor indica si el paquete requiere que los archivos de origen estén presentes en los dispositivos cliente. De forma predeterminada, el asistente no habilita esta opción y Configuration Manager no usa puntos de distribución para el paquete. Al seleccionar esta opción, especifique el contenido del paquete que se distribuirá a los puntos de distribución.  

    - **Carpeta de origen**: si el paquete contiene archivos de origen, haga clic en **Examinar** para abrir el cuadro de diálogo **Establecer carpeta de origen** y, después, especifique la ubicación de los archivos de origen del paquete.  

        > [!NOTE]  
        > La cuenta de equipo del servidor de sitio debe tener permisos de acceso de lectura a la carpeta de origen que especifique.  

    - A partir de la versión 1906, si quiere almacenar previamente en caché contenido en un cliente, especifique la **Arquitectura** y el **Lenguaje** de la imagen. Para obtener más información, vea [Configuración del contenido de la caché previa](../../osd/deploy-use/configure-precache-content.md).<!--4224642-->  

4. En la página **Tipo de programa** del **Asistente para crear paquetes y programas**, seleccione el tipo de programa que quiere crear y, luego, seleccione **Siguiente**. Puede crear un programa para un [equipo](#create-a-standard-program) o [dispositivo](#create-a-device-program), o puede omitir este paso y crear un programa más tarde.  

    > [!TIP]  
    > Para crear un programa para un paquete existente, seleccione primero el paquete. Después, en la pestaña **Inicio**, en el grupo **Paquete**, seleccione **Crear programa** para abrir el **Asistente para crear programas**.  

#### <a name="create-a-standard-program"></a>Crear un programa estándar

1. En la página **Tipo de programa** del **Asistente para crear paquetes y programas**, seleccione **Programa estándar** y, luego, **Siguiente**.  

2. En la página **Programa estándar** , especifique la siguiente información:  

    - **Nombre:** especifique un nombre para el programa con un máximo de 50 caracteres.  

        > [!NOTE]  
        > El nombre del programa debe ser único dentro de un paquete. Después de crear un programa, no puede modificar su nombre.  

    - **Línea de comandos**: escriba la línea de comandos que se va a usar para iniciar este programa, o bien haga clic en **Examinar** para ir a la ubicación del archivo.  

        Si no especifica una extensión para un nombre de archivo, Configuration Manager intentará usar .com, .exe y .bat como posibles extensiones.  

        Cuando el cliente ejecuta el programa, Configuration Manager busca el archivo en las siguientes ubicaciones:

        - Dentro del paquete
        - En la carpeta local de Windows
        - En el valor *%path%* local

        Si no encuentra el archivo, se produce un error en el programa.  

    - **Carpeta de inicio** (opcional): especifique la carpeta desde la que se ejecuta el programa, con un máximo de 127 caracteres. Esta carpeta puede ser una ruta de acceso absoluta en el cliente. También puede ser una ruta de acceso relacionada con la carpeta del punto de distribución que contiene el paquete.

    - **Ejecutar**: especifique el modo en el que se ejecuta el programa en los equipos cliente. Seleccione una de las siguientes opciones:  

        - **Normal**: el programa se ejecuta en el modo normal según los valores predeterminados del programa y del sistema. Este es el modo predeterminado.  

        - **Minimizado**: el programa se ejecuta minimizado en los dispositivos cliente. Los usuarios pueden ver la actividad de instalación en el área de notificación o la barra de tareas.  

        - **Maximizado**: el programa se ejecuta maximizado en los dispositivos cliente. Los usuarios ven toda la actividad de instalación.  

        - **Oculto**: el programa se ejecuta de forma oculta en los dispositivos cliente. Los usuarios no ven ninguna actividad de instalación.  

    - **El programa se puede ejecutar**: especifique si el programa se ejecuta solo cuando un usuario ha iniciado sesión, solo cuando ningún usuario ha iniciado sesión o sin importar si un usuario ha iniciado sesión en el equipo cliente.  

    - **Modo de ejecución**: especifique si el programa se ejecuta con permisos administrativos o con los permisos del usuario que tenga la sesión actualmente iniciada.  

    - **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**: use esta opción, si está disponible, para especificar si quiere permitir a los usuarios interactuar con el programa de instalación. Esta opción solo está disponible si se cumplen las condiciones siguientes:

        - La opción **El programa se puede ejecutar** está establecida en **Solo cuando ningún usuario haya iniciado sesión** o **Tanto si un usuario ha iniciado sesión como si no**.
        - La opción **Modo de ejecución** está establecida en **Ejecutar con derechos administrativos**.  

    - **Modo de unidad**: especifique información sobre cómo se ejecuta este programa en la red. Elija una de las siguientes opciones:  

        - **Se ejecuta con nombre UNC**: especifique que el programa se ejecuta con un nombre de convención de nomenclatura universal (UNC). Esta configuración es la predeterminada.  

        - **Requiere letra de unidad**: indica que el programa requiere una letra de unidad para que su ubicación esté completa. Para esta configuración, Configuration Manager puede usar cualquier letra de unidad disponible en el cliente.  

        - **Requiere una letra de unidad específica**: especifique que el programa requiere una letra de unidad concreta que establezca para que su ubicación esté completa. Por ejemplo, **Z:** . Si el cliente ya usa la letra de unidad especificada, el programa no se ejecuta.  

    - **Reconectarse al punto de distribución al iniciar sesión**: especifique si el cliente se vuelve a conectar al punto de distribución cuando el usuario inicia sesión. De forma predeterminada, el asistente no habilita esta opción.

3. En la página **Requisitos** del **Asistente para crear paquetes y programas**, especifique la información siguiente:  

    - **Ejecutar otro programa primero**: identifica un paquete y programa que se ejecutan antes de este paquete y programa.  

    - **Requisitos de la plataforma**: Seleccione **Este programa puede ejecutarse en cualquier plataforma** o **Este programa solo puede ejecutarse en las plataformas especificadas**. Después, elija las versiones de sistema operativo que los clientes deben tener para instalar este paquete y programa.  

    - **Espacio en disco estimado**: especifique la cantidad de espacio en disco que necesita el programa para ejecutarse en el equipo. El valor predeterminado es **Desconocido**. Si es necesario, especifique un número entero mayor o igual que cero. Si establece un valor, seleccione también unidades para el valor.  

    - **Duración máxima permitida de la ejecución (minutos)** : especifica el tiempo máximo que espera el programa para ejecutarse en el equipo cliente. El valor predeterminado es **120** minutos. Use solo números enteros mayores que cero.  

        > [!IMPORTANT]  
        > Si usa ventanas de mantenimiento en la misma recopilación en la que se ejecuta este programa, puede producirse un conflicto si el **Tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programada. Si el tiempo de ejecución máximo se establece en **Desconocido**, el programa empieza a ejecutarse durante la ventana de mantenimiento. Después, sigue ejecutándose cuando sea necesario una vez que se ha cerrado la ventana de mantenimiento. Si establece el tiempo de ejecución máximo en un periodo concreto que sea superior a la duración de alguna ventana de mantenimiento disponible, el cliente no ejecutará el programa.  

        Si establece este valor en **Desconocido**, Configuration Manager establece el tiempo máximo de ejecución permitido en 12 horas (720 minutos).  

        > [!NOTE]  
        > Si el programa supera el tiempo de ejecución máximo, Configuration Manager lo detendrá en caso de que se cumplan las condiciones siguientes:
        >
        > - Ha habilitado la opción **Ejecutar con derechos administrativos**.
        > - No ha habilitado la opción para **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**.  

#### <a name="create-a-device-program"></a>Crear un programa de dispositivo  

1. En la página **Tipo de programa** del **Asistente para crear paquetes y programas**, seleccione **Programa para dispositivo** y, luego, **Siguiente**.  

2. En la página **Programa para dispositivo**, especifique la siguiente configuración:  

    - **Nombre**: especifique un nombre para el programa con un máximo de 50 caracteres.  

        > [!NOTE]  
        > El nombre del programa debe ser único dentro de un paquete. Después de crear un programa, no puede modificar su nombre.  

    - **Comentario** (opcional): especifique un comentario para este programa de dispositivo con un máximo de 127 caracteres.  

    - **Carpeta de descarga**: especifique el nombre de la carpeta del dispositivo en la que se almacenarán los archivos de origen del paquete. El valor predeterminado es `\Temp\`.  

    - **Línea de comandos**: escriba la línea de comandos que se usará para iniciar este programa. Para ir a la ubicación del archivo, seleccione **Examinar**.  

    - **Ejecutar línea de comandos en carpeta de descarga**: seleccione esta opción para ejecutar el programa desde la carpeta de descarga.  

    - **Ejecutar línea de comandos desde esta carpeta**: seleccione esta opción para especificar otra carpeta desde la que se va a ejecutar el programa.  

3. En la página **Requisitos**, especifique la siguiente configuración:  

    - **Espacio en disco estimado**: especifique la cantidad de espacio en disco necesario para el software. El cliente muestra este valor a los usuarios de dispositivos móviles antes de que instalen el programa.  

    - **Descargar programa**: especifique información sobre cuándo puede el dispositivo móvil descargar este programa. Puede especificar **tan pronto como sea posible**, **sólo a través de una red rápida**, o **sólo cuando el dispositivo está acoplado**.  

    - **Requisitos adicionales**: especifique los requisitos adicionales para este programa. Los usuarios verán estos requisitos antes de instalar el software. Por ejemplo, podría notificar a los usuarios que necesitan para cerrar todas las demás aplicaciones antes de ejecutar el programa.  

## <a name="deploy-packages-and-programs"></a>Implementar paquetes y programas  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**.  

2. Seleccione el paquete que desea implementar. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y elija **Implementar**.  

3. En la página **General** del **Asistente para implementar software**, especifique el nombre del paquete y el programa que quiere implementar. Seleccione la recopilación en la que quiere implementar el paquete y el programa, así como cualquier comentario opcional.  

    Para almacenar el contenido del paquete en el grupo de puntos de distribución predeterminado de la recopilación, seleccione la opción **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación**. Si no asoció esta recopilación con un grupo de puntos de distribución, esta opción no estará disponible.  

4. En la página **Contenido**, elija **Agregar**. Seleccione los puntos de distribución o los grupos de puntos de distribución en los que quiera distribuir el contenido para este paquete y programa.  

5. En la página **Configuración de implementación**, configure las siguientes opciones:  

    - **Finalidad**: Elija una de las siguientes opciones:

        - **Disponible**: El usuario verá el paquete y el programa publicados en el Centro de software y los podrá instalar a petición.  

        - **Requerido**: el paquete y el programa se implementan de forma automática según la programación configurada. En el Centro de software, puede realizar un seguimiento de su estado de implementación e instalarlos antes de la fecha límite.  

        > [!NOTE]
        > Si varios usuarios inician sesión en el dispositivo, es posible que las implementaciones de paquete y secuencia de tareas no aparezcan en el centro de Software.

    - **Enviar paquetes de reactivación**: Si establece el propósito de implementación en **Requerido** y selecciona esta opción, el sitio envía primero un paquete de reactivación a los equipos a la hora límite de instalación. Para poder usar esta opción, configure los equipos para Wake On LAN. Para obtener más información, vea [Cómo configurar Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    - **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costos adicionales**  

    > [!NOTE]  
    > Al implementar un paquete y un programa, la opción **Implementar previamente el software en el dispositivo primario del usuario** no está disponible.  

6. En la página **Programación**, configure cuándo se implementarán este paquete y programa en los dispositivos cliente.  

    Las opciones de esta página variarán en función de si estableció la acción de implementación en **Disponible** o **Requerido**.  

    En el caso de las implementaciones **requeridas**, configure el comportamiento de volver a ejecutar el programa en el menú desplegable **comportamiento de volver a ejecutar** . Elija entre las siguientes opciones:  

    | comportamiento de reejecución | Descripción |
    |----------------|-------------|
    | **No volver a ejecutar nunca el programa implementado** | El cliente no volverá a ejecutar el programa. Este comportamiento sucederá incluso aunque se haya producido originalmente un error en el programa o se hayan cambiado los archivos de programa. |
    | **Volver a ejecutar siempre el programa** | el cliente siempre vuelve a ejecutar el programa cuando se programa la implementación. Este comportamiento se produce incluso si el programa ya se ha ejecutado correctamente. Resulta útil dadas las implementaciones periódicas al actualizar el programa. |
    | **Volver a ejecutar en caso de error del intento anterior** | El cliente vuelve a ejecutar el programa cuando se programa la implementación solo si se produjo un error en el intento de ejecución anterior. |
    | **Volver a ejecutar si el intento anterior se realizó correctamente** | El cliente vuelve a ejecutar el programa solo si previamente se ejecutó correctamente en el cliente. Este comportamiento es útil con las implementaciones periódicas cuando el programa se actualiza de forma regular y cada actualización requiere que la actualización anterior esté correctamente instalada. |

7. En la página **Experiencia del usuario** , especifique la siguiente información:  

    - **Permitir que los usuarios ejecuten el programa independientemente de las asignaciones**: los usuarios pueden instalar este software desde el Centro de software independientemente de la hora de instalación programada.  

    - **Instalación de software**: permite que el software se instale fuera de las ventanas de mantenimiento configuradas.  

    - **Reinicio del sistema (si es necesario para completar la instalación)** : si la instalación de software requiere un reinicio del dispositivo para completarse, permita que esta acción se produzca fuera de las ventanas de mantenimiento configuradas.  

    - **Dispositivos de Embedded**: cuando implemente paquetes y programas en dispositivos de Windows Embedded habilitados con filtro de escritura, puede especificar que instalen los paquetes y programas en la superposición temporal y confirmar los cambios más tarde. También puede confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar y los cambios se conservan en el dispositivo.  

        > [!NOTE]  
        > Al implementar un paquete o programa a un dispositivo de Windows Embedded, asegúrese de que el dispositivo es un miembro de una colección que tiene una ventana de mantenimiento configurada. Para obtener más información sobre cómo se usan las ventanas de mantenimiento al implementar paquetes y programas en dispositivos de Windows Embedded, vea [Creación de aplicaciones de Windows Embedded](../get-started/creating-windows-embedded-applications.md).  

8. En la página **Puntos de distribución** , especifique la siguiente información:  

    - **Opciones de implementación**: Especifique la acción que realiza un cliente cuando usa un punto de distribución en su grupo de límites actual. Seleccione también la acción para el cliente cuando use un punto de distribución de un grupo de límites vecino o el grupo de límites de sitio predeterminado.

        > [!IMPORTANT]  
        > Si establece la opción de implementación en **Ejecutar programa desde el punto de distribución**, asegúrese de habilitar la opción **Copiar el contenido de este paquete en un recurso compartido de paquete en los puntos de distribución** en la pestaña **Acceso a datos** de las propiedades del paquete. De lo contrario, el paquete no estará disponible para ejecutarse desde puntos de distribución.  

    - **Permitir que los clientes usen puntos de distribución del grupo de límite del sitio predeterminado**: cuando este contenido no esté disponible desde ningún punto de distribución de los grupos de límites actuales o vecinos, habilite esta opción para permitirles probar puntos de distribución en el grupo de límites predeterminado del sitio.

9. Complete el asistente.  

Vea la implementación en el nodo **Implementaciones** del área de trabajo **Supervisión** y en el panel de detalles de la pestaña de la implementación de paquetes cuando se selecciona la implementación. Para más información, vea [Supervisar paquetes y programas](#monitor-packages-and-programs).  


## <a name="monitor-packages-and-programs"></a>Supervisar paquetes y programas

Para supervisar las implementaciones de paquetes y programas, use los mismos procedimientos que usa para supervisar aplicaciones, tal y como se detalla en [Supervisar aplicaciones](monitor-applications-from-the-console.md).  

Los paquetes y programas también incluyen varios informes integrados, lo que permite supervisar la información sobre el estado de implementación de los paquetes y programas. Estos informes tienen la categoría de informe de **la distribución de Software, paquetes y programas** y **distribución de Software-paquete y el estado de implementación de programa**.  

Para obtener más información sobre cómo configurar informes en Configuration Manager, vea [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).  


## <a name="manage-packages-and-programs"></a>Administrar paquetes y programas

En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**. Seleccione el paquete que quiere administrar y elija una tarea de administración.  

### <a name="create-prestage-content-file"></a>Crear archivo de contenido preconfigurado

Abre el **Asistente para crear archivos de contenido preconfigurados** para crear un archivo que contenga el contenido del paquete. Use este archivo para importar manualmente el paquete en un punto de distribución remoto. Esta acción es útil cuando tiene poco ancho de banda entre el servidor de sitio y el punto de distribución.

### <a name="create-program"></a>Crear el programa

Abre el **Asistente para crear programas**  para crear un nuevo programa para este paquete.

### <a name="export"></a>Exportar

Abre el **Asistente para exportar paquete** para exportar el paquete seleccionado y su contenido en un archivo. Use este archivo para importar el archivo en otra jerarquía.

Para información sobre cómo importar paquetes y programas, consulte [Crear un paquete y programa](#create-a-package-and-program).

### <a name="deploy"></a>Implementar

Abre el **Asistente para implementar software** para implementar el paquete y el programa seleccionados en una recopilación. Para más información, vea [Implementar paquetes y programas](#deploy-packages-and-programs).

### <a name="distribute-content"></a>Distribución de contenido

Abre el **Asistente para distribuir contenido**, que envía el contenido para el paquete y el programa a puntos de distribución o grupos de puntos de distribución seleccionados.

### <a name="update-distribution-points"></a>Actualizar puntos de distribución

Actualiza los puntos de distribución con el contenido más reciente para el programa y el paquete seleccionados.


## <a name="see-also"></a>Vea también

- [Scripts](create-deploy-scripts.md)

- [Administrador de conversión de paquetes](../pcm/package-conversion-manager.md)

- [Archivos de definición del paquete](package-definition-files.md)
