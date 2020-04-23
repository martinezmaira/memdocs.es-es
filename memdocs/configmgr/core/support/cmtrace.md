---
title: CMTrace
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar la herramienta CMTrace para ver los archivos de registro de Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707903"
---
# <a name="cmtrace"></a>CMTrace

*Se aplica a: Configuration Manager (rama actual)*

CMTrace es una de las [herramientas de Configuration Manager](tools.md). Permite ver y supervisar los archivos de registro, incluidos los siguientes tipos:  

- Archivos de registro en formato de Configuration Manager o de Administrador de componentes cliente (CCM)  

- Archivos de texto Unicode o ASCII sin formato, como los registros de Windows Installer  

La herramienta ayuda a analizar los archivos de registro mediante el resaltado, el filtrado y la búsqueda de errores.

A partir de la versión 1806, la herramienta de visualización de registros CMTrace se instala automáticamente con el cliente de Configuration Manager. Se agrega al directorio de instalación del cliente, que de forma predeterminada es `%WinDir%\CCM\CMTrace.exe`.<!--1357971-->

> [!Note]  
> CMTrace no se registra automáticamente con Windows para abrir la extensión de archivo. log. Para más información, vea [Asociaciones de archivo](#file-associations).  

A partir de la versión 1906, **OneTrace** es un nuevo visor de registros del Centro de soporte técnico. Funciona de manera similar a CMTrace, pero con mejoras. Para obtener más información, consulte [Centro de soporte técnico OneTrace](support-center-onetrace.md).

## <a name="usage"></a>Uso

Ejecute **CMTrace.exe**. La primera vez que ejecute la herramienta, verá una solicitud de asociación de archivos. Para más información, vea [Asociaciones de archivo](#file-associations).

La mayoría de las acciones de CMTrace se realizan desde los siguientes menús:

- [File](#file-menu)
- [Herramientas](#tools-menu)

### <a name="file-menu"></a>Menú Archivo

Las acciones siguientes están disponibles en el menú **Archivo**:  

- [Abrir](#open)
- [Open on Server](#open-on-server) (Abrir en el servidor)
- [Imprimir](#print)
- [Preferencias](#preferences)

El menú Archivo también muestra los ocho archivos más recientes. Para reabrir rápidamente uno de estos registros, selecciónelo en el menú Archivo.

#### <a name="open"></a>Abrir

Muestra el cuadro de diálogo Abrir para buscar un archivo de registro.

Filtre la vista por archivos de los siguientes tipos:

- Archivos de registro (\*.log)  
- Archivos de registro antiguos (\*.lo_)
- Todos los archivos (\*.\*)

Las dos opciones siguientes no están seleccionadas de forma predeterminada:  

- **Omitir líneas existentes**: cuando se selecciona, CMTrace omite el contenido existente del archivo de registro seleccionado y solo muestra las nuevas líneas cuando se agregan. Utilice esta opción solo para supervisar nuevas acciones cuando ya no necesite el historial completo del archivo de registro.  

- **Combinar archivos seleccionados**: si habilita esta opción y selecciona más de un archivo de registro, CMTrace combina los registros seleccionados en la vista. Los muestra como si fuesen un solo archivo de registro. El registro combinado actualiza lo mismo y admite el resto de características de CMTrace como si fuera un solo archivo de registro.  

#### <a name="open-on-server"></a>Open on Server (Abrir en el servidor)

Vaya a la carpeta de registros de Configuration Manager en un equipo de sistema de sitio con el cuadro de diálogo Examinar estándar. También puede buscar un equipo remoto en la red.

Al seleccionar un equipo remoto para examinarlo, CMTrace busca el recurso compartido de Configuration Manager. Si no encuentra un recurso compartido con archivos de registro de Configuration Manager, muestra un mensaje de error.  

Para conectarse directamente a un equipo conocido sin navegar, use la acción [Abrir](#open). Luego escriba un nombre de servidor y compártalo con el formato UNC.

#### <a name="print"></a>Imprimir

Muestra el cuadro de diálogo Imprimir de Windows estándar. Con esta acción se envía el archivo de registro actual a una impresora. Da formato a la salida según la configuración de la pestaña de impresión de las preferencias de CMTrace.

#### <a name="preferences"></a>Preferencias

Configure las opciones de CMTrace. Están disponibles las siguientes opciones:  

- Pestaña**General**  

    - **Intervalo de actualización**: controla la frecuencia con la que CMTrace comprueba si hay cambios en los archivos de registro y carga nuevas líneas. De forma predeterminada, este valor es de 500 milisegundos.  

    - **Resaltar**: establece el color que CMTrace usa para resaltar las líneas del registro que seleccione. De forma predeterminada, este color es amarillo básico (rojo: 255, verde: 255, azul: 0).  

    - **Columnas:** configura las columnas que están visibles en la vista del registro y el orden en que aparecen. De forma predeterminada, muestra Texto del registro, Componente, Fecha y hora y Subproceso.  

- Pestaña **Impresión**  

    - **Columnas:** configure las columnas que se usan al imprimir archivos de registro y el orden en que aparecen. De forma predeterminada, imprime las mismas columnas que muestra.  

    - **Orientación**: establece la orientación de impresión predeterminado al imprimir archivos de registro. Reemplace esta configuración en el cuadro de diálogo Imprimir. De forma predeterminada, utiliza orientación Vertical.  

- Pestaña **Avanzadas**  

    - **Intervalo de actualización**: obliga a CMTrace a actualizar la vista del registro en un intervalo especificado al cargar un gran número de líneas. De forma predeterminada, esta opción está deshabilitada con un valor de cero.  

        > [!Note]  
        > En general, no modifique el **intervalo de actualización**. Eso puede aumentar considerablemente la cantidad de tiempo necesario para abrir archivos de registro grandes.

### <a name="tools-menu"></a>Menú Herramientas

Las acciones siguientes están disponibles en el menú **Herramientas**:

- [Buscar](#find)
- [Buscar siguiente](#find-next)
- [Copiar al Portapapeles](#copy-to-clipboard)
- [Resaltar](#highlight)
- [Filtro](#filter)
- [Búsqueda de errores](#error-lookup)
- [Pausar](#pause)
- [Mostrar u ocultar detalles](#showhide-details)
- [Show/Hide Info Pane](#showhide-info-pane) (Mostrar u ocultar panel de información)

#### <a name="find"></a>Buscar

Busque una cadena de texto especificado en el archivo de registro abierto.  

#### <a name="find-next"></a>Buscar siguiente

Busca la siguiente cadena coincidente con la especificada anteriormente en el cuadro de diálogo Buscar.  

#### <a name="copy-to-clipboard"></a>Copiar al Portapapeles

Copia las líneas seleccionadas como texto sin formato en el Portapapeles de Windows. Si se examinan archivos de registro de CCM y Configuration Manager, copia las columnas en el mismo orden en que aparecen en la vista. Separa cada columna con un carácter de tabulación. Utilice esta acción cuando copie registros en los mensajes de correo electrónico o en otros documentos.  

#### <a name="highlight"></a>Resaltar

Escriba una cadena que CMTrace use para buscar el texto de cada entrada del registro. Luego se resalta cualquier texto del registro que coincida con la cadena especificada.  

- El resaltado utiliza el color que se especifique en Preferencias.  

- Para desactivar el resaltado, borre la cadena de este campo.  

- Si escribe un número decimal o hexadecimal, CMTrace intenta hacer coincidir el valor con la columna Subproceso. Utilice este comportamiento para resaltar el procesamiento de un único subproceso, sin filtrar otros subprocesos que puedan interactuar con él.  

- Para comparar cadenas por mayúsculas y minúsculas, habilite la opción **Distinguir mayúsculas de minúsculas**.  

#### <a name="filter"></a>Filtro

Muestra u oculta las líneas de registro según los criterios especificados. Aplique filtros a cualquiera de las cuatro columnas independientemente de si están visibles. Estas opciones se aplican a cada archivo de registro abierto.

Ejemplos:
<!--SCCMDocs issue #603-->

- Filtro **smsts.log** en texto de entrada que contenga "la acción" o "el grupo".
- Filtro **InventoryAgent.log** cuando el texto de entrada contiene "destino".

#### <a name="error-lookup"></a>Búsqueda de errores

Escriba o pegue un código de error en formato decimal o hexadecimal para mostrar una descripción. Entre los posibles orígenes de errores, se incluyen los siguientes: Windows, WMI o WinHTTP.

#### <a name="pause"></a>Pausar

Suspenda o reinicie la supervisión del registro. Los siguientes casos de uso son algunos de los posibles motivos para usar esta acción:  

- Cuando CMTrace muestra información del archivo de registro demasiado rápido  

- Cuando pausa la supervisión del registro, la información que CMTrace muestra no se pierde si el archivo actual pasa a un nuevo registro  

- Cuando quiere que CMTrace deje de mostrar nuevos datos mientras se examina el archivo de registro  

#### <a name="showhide-details"></a>Mostrar u ocultar detalles

Muestra u oculta todas las columnas aparte de la de texto del registro. También expande la columna de texto del registro hasta el ancho de la ventana. Use esta acción cuando visualice los registros en un equipo con una resolución de pantalla baja. Se muestra mayor parte del texto de registro.  

> [!Note]  
> Cuando se visualizan archivos de texto sin formato, CMTrace oculta automáticamente los detalles porque siempre están vacíos.  

#### <a name="showhide-info-pane"></a>Show/Hide Info Pane (Mostrar u ocultar panel de información)

Muestra u oculta el panel de información. Use esta acción cuando visualice los registros en un equipo con una resolución de pantalla baja. Se muestran más detalles del registro.  


## <a name="log-pane"></a>Panel de registro

El panel de registro se encuentra en la parte superior de la ventana CMTrace. Muestra líneas de los archivos de registro.

Cuando se selecciona una línea, se resalta temporalmente con la combinación de colores de selección de Windows.

Las líneas resaltadas coinciden con los criterios definidos con la opción **Resaltar** del menú **Herramientas**. El resaltado utiliza el color que se especifique en **Preferencias**.

CMTrace utiliza texto de color amarillo sobre un fondo rojo para mostrar las líneas con errores. En los registros con formato de CCM, las entradas del registro tienen un valor de tipo explícito que indica la entrada como un error. Para otros formatos de registro, CMTrace realiza una búsqueda que no distingue mayúsculas de minúsculas de cualquier cadena de texto que coincida con "error" en cada entrada.

Muestra las líneas con advertencias con un fondo amarillo. En los registros con formato de CCM, las entradas del registro tienen un valor de tipo explícito que indica la entrada como una advertencia. Para otros formatos de registro, CMTrace realiza una búsqueda que no distingue mayúsculas de minúsculas de cualquier cadena de texto que coincida con "warn" en cada entrada.


## <a name="info-pane"></a>Panel de información

El panel de información se encuentra en la parte inferior de la ventana CMTrace. Contiene las características siguientes:

- Detalles sobre la entrada del registro seleccionada actualmente  

- Un cuadro de texto que muestra el texto del registro  

- Muestra los retornos de carro para que el texto con formato sea más fácil de leer  

- Las entradas largas que no son totalmente visibles en el panel de registro resultan más fáciles de leer  

Muestre u oculte el panel de información con la opción **Show/Hide Info Pane** (Mostrar u ocultar panel de información) del menú **Herramientas**. Si el panel de información ocupa más de la mitad de la ventana de registro, CMTrace lo oculta automáticamente.

### <a name="progress-bar"></a>Barra de progreso

Al abrir un archivo de registro por primera vez, CMTrace reemplaza el panel de información por una barra de progreso. El progreso indica cuánto contenido del archivo existente está cargado. Cuando el progreso llega al 100 %, CMTrace quita la barra de progreso y la reemplaza por el panel de información. Al cargar archivos grandes, este comportamiento le indica cuánto tiempo puede tardar la carga.

### <a name="status-bar"></a>Barra de estado

En el caso de los archivos de registro con formato de Configuration Manager y de CCM, la barra de estado muestra el tiempo transcurrido para las entradas del registro seleccionadas. Si se selecciona una sola entrada, la herramienta muestra el tiempo desde la primera entrada del registro hasta la entrada seleccionada. Si se seleccionan varias entradas, calcula el tiempo desde la primera entrada seleccionada hasta la última entrada seleccionada. CMTrace da formato a esta información de la manera siguiente:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Integración de Windows Shell

CMTrace admite [asociaciones de archivo](#file-associations) y [arrastrar y colocar](#drag-and-drop).

### <a name="file-associations"></a>Asociaciones de archivo

CMTrace puede asociarse a extensiones de nombre de archivo .log y .lo_. Cuando el programa se inicia, comprueba el registro para determinar si ya está asociado a estas extensiones de nombre de archivo. Si CMTrace no está ya asociado ninguna extensión de nombre de archivo, se le pedirá que asocie las extensiones de nombre de archivo a CMTrace. Si selecciona **No volver a preguntar**, CMTrace omitirá esta comprobación cada vez que se ejecute en este equipo.

### <a name="drag-and-drop"></a>Arrastrar y colocar

CMTrace admite funcionalidad básica de arrastrar y colocar. Arrastre un archivo de registro desde el Explorador de Windows a CMTrace para abrirlo.


## <a name="other-tips"></a>Otras sugerencias

### <a name="last-directory-registry-key"></a>Clave del registro de Last Directory

<!--511280-->
De forma predeterminada, CMTrace guarda la última ubicación del registro que se ha abierto. Este comportamiento es útil en el servidor de sitio porque el valor predeterminado es siempre la ruta de acceso de los registros.

La primera vez que se inicie en un cliente, el valor predeterminado es el directorio de trabajo actual. Esta ubicación puede ser la ruta de acceso donde guardó CMTrace o una ruta de acceso como `%userprofile%\Desktop`.

El valor **Last Directory** de la clave del registro `HKEY_CURRENT_USER\Software\Microsoft\Trace32` controla esta ubicación predeterminada. Si establece este valor en `%windir%\CCM\Logs` en los clientes, CMTrace abrirá los archivos en la ubicación de registro del cliente la primera vez que lo ejecute.


## <a name="see-also"></a>Vea también

- [Archivos de registro](../plan-design/hierarchy/log-files.md)

- [Visor de archivos de registro del Centro de soporte técnico](support-center.md#support-center-log-file-viewer)

- [Centro de soporte técnico OneTrace](support-center-onetrace.md)
