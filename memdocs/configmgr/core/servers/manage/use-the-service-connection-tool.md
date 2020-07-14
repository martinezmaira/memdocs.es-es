---
title: Herramienta de conexión de servicio
titleSuffix: Configuration Manager
description: Obtenga información sobre esta herramienta que le permite conectarse al servicio en la nube de Configuration Manager para cargar manualmente la información de uso.
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 48aa08f3318aaa4629691bfb30b60580cd3e25f0
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946851"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Uso de la herramienta de conexión de servicio para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la **herramienta de conexión de servicio** cuando el punto de conexión de servicio esté en modo sin conexión. También la puede usar cuando los servidores de sistema del sitio de Configuration Manager no estén conectados a Internet. La herramienta puede ayudarlo a mantener actualizado el sitio con las actualizaciones más recientes de Configuration Manager.

Al ejecutar la herramienta, se conecta al servicio en la nube de Configuration Manager, carga información de uso de la jerarquía y descarga actualizaciones. La carga de los datos de uso es necesaria para habilitar el servicio en la nube para proporcionar las actualizaciones correctas para el entorno.

## <a name="prerequisites"></a>Requisitos previos

- El sitio tiene un punto de conexión de servicio y se configura en **Sin conexión, conexión a petición**.

- Ejecute la herramienta desde un símbolo del sistema como administrador. No hay interfaz de usuario.

- Puede ejecutar la herramienta desde el punto de conexión de servicio y un equipo que se pueda conectar a Internet. Cada uno de estos equipos debe tener un sistema operativo de 64 bits y los componentes siguientes:

  - Los archivos de x86 y x64 de **Visual C++ Redistributable** . De forma predeterminada, Configuration Manager instala la versión x64 en el equipo que hospeda el punto de conexión de servicio. Para descargar este componente, consulte [Paquetes redistribuibles de Visual C++ para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784).

  - **.NET Framework 4.5.2** o versiones posteriores

- La cuenta que utilice para ejecutar la herramienta necesita los permisos siguientes:

  - **Administrador local** en el equipo que hospeda el punto de conexión de servicio

  - Permisos de **lectura** para la base de datos del sitio

- Necesita un método para transferir los archivos entre el equipo con acceso a Internet y el punto de conexión de servicio. Por ejemplo, una unidad USB con espacio libre suficiente para almacenar los archivos y las actualizaciones.

## <a name="overview"></a>Introducción

1. **Preparar:** ejecute la herramienta en el punto de conexión de servicio. Coloca los datos de uso en un archivo. cab en la ubicación que especifique. Copie el archivo de datos en el equipo con conexión a Internet.

2. **Conectar**: ejecute la herramienta en el equipo con una conexión a Internet. Carga los datos de uso y, luego, descarga las actualizaciones de Configuration Manager. Copie las actualizaciones descargadas en el punto de conexión de servicio.

    Puede cargar varios archivos de datos al mismo tiempo, cada uno de una jerarquía distinta. También puede especificar un servidor proxy y un usuario para el servidor proxy.

3. **Importar**: ejecute la herramienta en el punto de conexión de servicio. Importa las actualizaciones y las agrega al sitio. Después, puede ver e [instalar esas actualizaciones](install-in-console-updates.md) en la consola de Configuration Manager.

### <a name="upload-multiple-data-files"></a>Carga de varios archivos de datos

- Coloque todos los archivos de datos exportados de jerarquías independientes en la misma carpeta. Asigne un nombre único a cada archivo. Si es necesario, puede cambiar el nombre de manera manual.

- Cuando ejecute la herramienta para cargar datos a Microsoft, puede especificar la carpeta que contiene los archivos de datos.

- Cuando ejecuta la herramienta para importar los datos, la herramienta solo importa los datos para esa jerarquía.

### <a name="specify-a-proxy-server"></a>Especificación de un servidor proxy

Si el equipo con conexión a Internet requiere un servidor proxy, la herramienta admite una configuración de proxy básica. Use los parámetros opcionales **-proxyserveruri** y **-proxyusername**. Para más información, consulte [Parámetros de línea de comandos](#bkmk_cmd).

### <a name="specify-the-type-of-updates-to-download"></a>Especificar el tipo de actualizaciones que quiere descargar

La herramienta admite opciones para controlar los archivos que se descargan. De forma predeterminada, la herramienta descarga únicamente la última actualización disponible que sea válida para la versión de su sitio. No descarga revisiones.

Para modificar este comportamiento, use uno de los parámetros siguientes para cambiar los archivos que descargará:

- **-downloadall**: descargue todas las actualizaciones, incluidas las actualizaciones y revisiones, independientemente de la versión del sitio.
- **-downloadhotfix**: descargue todas las revisiones, independientemente de la versión del sitio.
- **-downloadsiteversion**: descarga actualizaciones y revisiones con una versión posterior a la versión del sitio.

    > [!IMPORTANT]
    > Debido a un problema conocido en la versión 2002 de Configuration Manager, el comportamiento predeterminado no funciona según lo previsto. Use el parámetro **-downloadsiteversion** para descargar las actualizaciones necesarias para la versión 2002.<!-- 7594517 -->

Para más información, consulte [Parámetros de línea de comandos](#bkmk_cmd).

> [!TIP]
> La herramienta determina la versión del sitio a partir del archivo de datos. Para comprobar la versión, busque el archivo de texto con nombre de la versión del sitio en el archivo .cab.

## <a name="use-the-tool"></a>Uso de la herramienta  

La herramienta de conexión de servicio está en los soportes de instalación de Configuration Manager en la ruta de acceso siguiente: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe`. Use siempre la herramienta de conexión de servicio que coincida con la versión de Configuration Manager que use. Todos estos archivos deben estar en la misma carpeta para que funcione la herramienta de conexión de servicio.

Copie la carpeta **ServiceConnectionTool** con todo el contenido en el equipo con conexión a Internet.

En este procedimiento, los ejemplos de línea de comandos usan los nombres de archivo y ubicaciones de carpetas siguientes. No es necesario que use estos nombres de archivo y rutas de acceso. Puede usar alternativas que coincidan con el entorno y sus preferencias.

- La ruta de acceso a los archivos de origen del soporte de instalación de Configuration Manager en el punto de conexión de servicio: `C:\Source`

- La ruta de acceso a una unidad USB donde se almacenan los datos que se van a transferir entre equipos: `D:\USB\`

- El nombre del archivo de datos que se exporta del sitio: `UsageData.cab`

- El nombre de la carpeta vacía donde la herramienta almacena las actualizaciones descargadas para Configuration Manager: `UpdatePacks`

### <a name="prepare"></a>Preparación

1. En el equipo que hospeda el punto de conexión de servicio, abra un símbolo del sistema como administrador y cambie el directorio a la ubicación de la herramienta. Por ejemplo:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Ejecute el comando siguiente para preparar el archivo de datos:

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > Si va a cargar archivos de datos de más de una jerarquía al mismo tiempo, asigne un nombre único a cada archivo de datos. Si es necesario, puede cambiar el nombre de los archivos más adelante.

    Los datos del archivo se basan en el nivel de diagnósticos y datos de uso que configura para el sitio. Para más información, consulte [Información general sobre los diagnósticos y datos de uso](../../plan-design/diagnostics/diagnostics-and-usage-data.md). Puede usar la herramienta para exportar los datos a un archivo .csv para ver el contenido. Para más información, consulte [-export](#-export).

1. Una vez que la herramienta termine de exportar los datos de uso, copie el archivo de datos en un equipo con acceso a Internet.

### <a name="connect"></a>Conectar

1. En el equipo con acceso a Internet, abra un símbolo del sistema como administrador y cambie el directorio a la ubicación de la herramienta. Esta ubicación es una copia de toda la carpeta **ServiceConnectionTool**. Por ejemplo:

    `cd D:\USB\ServiceConnectionTool\`

1. Ejecute el comando siguiente para cargar el archivo de datos y descargar las actualizaciones de Configuration Manager:

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    Para más ejemplos, consulte [Parámetros de línea de comandos](#bkmk_cmd).

    > [!NOTE]  
    > Cuando ejecute esta línea de comandos, es posible que vea el error siguiente:
    >
    > **Excepción no controlada: System.UnauthorizedAccessException: El acceso a la ruta de acceso "C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql" se denegó.**
    >
    > Puede omitir este error de forma segura. Cierre la ventana de error para continuar.

1. Una vez que la herramienta termine de descargar las actualizaciones, cópielos en el punto de conexión de servicio.

### <a name="import"></a>Importar

1. En el equipo que hospeda el punto de conexión de servicio, abra un símbolo del sistema como administrador y cambie el directorio a la ubicación de la herramienta. Por ejemplo:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Ejecute el comando siguiente para importar las actualizaciones:

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. Una vez finalizada la importación, cierre el símbolo del sistema. Solo importa las actualizaciones para la jerarquía aplicable.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**. Ahora se pueden instalar las actualizaciones importadas. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](install-in-console-updates.md).

## <a name="log-files"></a>Archivos de registro

- **ServiceConnectionTool.log**: cada vez que se ejecuta la herramienta de conexión de servicio, se escribe en este archivo de registro. La ruta de acceso del archivo de registro siempre es la misma ubicación que la herramienta. Este archivo de registro proporciona detalles sencillos sobre el uso de la herramienta en función de los parámetros que se usan. Cada vez que se ejecuta la herramienta, esta reemplaza cualquier archivo de registro existente.

- **ConfigMgrSetup.log**: durante la fase de [Conexión](#connect), la herramienta escribe en este archivo de registro en la raíz de la unidad del sistema. Este archivo de registro proporciona información más detallada. Por ejemplo, los archivos que descarga la herramienta y si las comprobaciones del hash se realizan correctamente.

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a> Parámetros de línea de comandos

En esta sección se enumeran en orden alfabético todos los parámetros disponibles para la herramienta de conexión de servicio.

### <a name="-connect"></a>-connect

Úselo durante la fase de [Conexión](#connect) en el equipo con acceso a Internet. Se conecta al servicio en la nube de Configuration Manager para cargar el archivo de datos y descarga actualizaciones.

Requiere estos parámetros:

- **-usagedatasrc**: la ubicación del archivo de datos que se va a cargar.
- **-updatepackdest**: una ruta de acceso para las actualizaciones descargadas.

También puede usar estos parámetros opcionales:

- **-proxyserveruri**: el FQDN del servidor proxy.
- **-proxyusername**: nombre de usuario para el servidor proxy.
- **-downloadall**: descargue todo, incluidas las actualizaciones y revisiones, independientemente de la versión del sitio.
- **-downloadhotfix**: descargue todas las revisiones, independientemente de la versión del sitio.
- **-downloadsiteversion**: descarga actualizaciones y revisiones con una versión posterior a la versión del sitio.

#### <a name="example-of-connect-without-a-proxy-server"></a>Ejemplo de conexión sin un servidor proxy

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>Ejemplo de conexión con un servidor proxy

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>Ejemplo de conexión para descargar solo las actualizaciones aplicables a la versión del sitio

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-dest

Un parámetro requerido con el parámetro **-export** para especificar la ruta de acceso y el nombre de archivo del archivo .csv que se va a exportar. Para más información, consulte [-export](#-export).

### <a name="-downloadall"></a>-downloadall

Un parámetro opcional con el parámetro **-connect** para descargarlo todo, incluidas actualizaciones y revisiones, independientemente de la versión del sitio. Para más información, consulte [-connect](#connect).

### <a name="-downloadhotfix"></a>-downloadhotfix

Un parámetro opcional con el parámetro **-connect** para descargar solo todas las revisiones, independientemente de la versión del sitio. Para más información, consulte [-connect](#-connect).

### <a name="-downloadsiteversion"></a>-downloadsiteversion

Un parámetro opcional con el parámetro **-connect** para descargar solo las actualizaciones y revisiones con una versión posterior a la versión del sitio. Para más información, consulte [-connect](#-connect).

### <a name="-export"></a>-export

Úselo durante la fase de [Preparación](#prepare) para exportar los datos de uso a un archivo .csv. Ejecútelo como administrador en el punto de conexión de servicio. Esta acción permite revisar el contenido de los datos de uso antes de cargarlos en Microsoft. Requiere el parámetro **-dest** para especificar la ubicación del archivo .csv.

#### <a name="example-of-export"></a>Ejemplo de exportación

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>-import

Úselo durante la fase de [Importación](#import) del punto de conexión de servicio para importar las actualizaciones al sitio. Requiere el parámetro **-updatepacksrc** para especificar la ubicación de las actualizaciones descargadas.

#### <a name="example-of-import"></a>Ejemplo de importación

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>-prepare

Úselo durante la fase de [Preparación](#prepare) en el punto de conexión de servicio para exportar los datos de uso del sitio. Requiere el parámetro **-usagedatadest** para especificar la ubicación del archivo de datos exportado.

#### <a name="example-of-prepare"></a>Ejemplo de preparación

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>-proxyserveruri

Un parámetro opcional con el parámetro **-connect** para especificar el FQDN del servidor proxy. Para más información, consulte [-connect](#-connect).

### <a name="-proxyusername"></a>-proxyusername

Un parámetro opcional con el parámetro **-connect** para especificar el nombre de usuario que se va a autenticar con el servidor proxy. Para más información, consulte [-connect](#-connect).

### <a name="-updatepackdest"></a>-updatepackdest

Un parámetro requerido con el parámetro **-connect** para especificar una ruta de acceso para las actualizaciones descargadas. Para más información, consulte [-connect](#-connect).

### <a name="-updatepacksrc"></a>-updatepacksrc

Un parámetro requerido con el parámetro **-import** para especificar una ruta de acceso de las actualizaciones descargadas. Para más información, consulte [-import](#-import).

### <a name="-usagedatadest"></a>-usagedatadest

Un parámetro requerido con el parámetro **-prepare** para especificar una ruta de acceso y un nombre de archivo del archivo de datos exportado. Para más información, consulte [-prepare](#-prepare).

## <a name="next-steps"></a>Pasos siguientes

[Instalación de actualizaciones en la consola](install-in-console-updates.md)

[Visualización de datos de diagnóstico y uso](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
