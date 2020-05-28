---
title: Herramienta Descargador del programa de instalación
titleSuffix: Configuration Manager
description: Use la herramienta independiente para descargar las versiones actuales de los principales archivos de instalación para el programa de instalación.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428830"
---
# <a name="setup-downloader-for-configuration-manager"></a>Descargador del programa de instalación de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de ejecutar el programa de instalación de Configuration Manager para instalar o actualizar un sitio, puede usar la herramienta independiente Descargador del programa de instalación para descargar los archivos de instalación actualizados. Ejecute la herramienta desde la versión de Configuration Manager que quiere instalar. Use archivos de instalación actualizados para asegurarse de que la instalación del sitio usa las versiones actuales de los principales archivos de instalación.

Cuando se usa el descargador del programa de instalación, se especifica una carpeta para que contenga los archivos. La cuenta que use para ejecutar la herramienta debe tener permisos de **Control total** de la carpeta de descarga. Al ejecutar el programa de instalación para instalar o actualizar un sitio, puede especificar esta copia local de los archivos descargados anteriormente. Este comportamiento evita que el programa de instalación tenga que conectarse a Microsoft cuando se inicia la instalación o la actualización del sitio. Puede usar la misma copia local de los archivos de instalación para otras instalaciones o actualizaciones del sitio de la misma versión.

La herramienta Descargador del programa de instalación descarga los siguientes tipos de archivos:

- Archivos redistribuibles como requisitos previos
- Paquetes de idioma
- Las últimas actualizaciones del producto para el programa de instalación

Tiene dos opciones para ejecutar el descargador del programa de instalación:

- Ejecutar la aplicación con la interfaz de usuario.
- Ejecutar la aplicación en un símbolo del sistema para tener opciones adicionales de la línea de comandos

Si la organización restringe la comunicación de red con Internet mediante un dispositivo proxy o firewall, tiene que permitir que la herramienta acceda a puntos de conexión de Internet. El dispositivo en el que se ejecutará la herramienta requiere acceso a Internet, al igual que el punto de conexión del servicio. Para más información, consulte los [requisitos de acceso a Internet](../../../plan-design/network/internet-endpoints.md#bkmk_scp).<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> Ejecutar el descargador del programa de instalación con la interfaz de usuario

1. En un equipo que tenga acceso a Internet, busque los medios de instalación de la versión de Configuration Manager que quiere instalar.

1. En la subcarpeta **SMSSETUP\BIN\X64**, ejecute **Setupdl.exe**.

1. Especifique la ruta de acceso de la carpeta en la que se almacenan los archivos de instalación actualizados y después seleccione **Descargar**. El descargador del programa de instalación comprueba los archivos que se encuentran en la carpeta de descarga. Solo descarga los archivos que faltan o que son más recientes que los archivos existentes. Crea subcarpetas para los idiomas descargados y otros componentes necesarios.

1. Para revisar los resultados de la descarga, vea **C:\ConfigMgrSetup.log**.

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> Ejecutar el descargador del programa de instalación desde el símbolo del sistema

1. Abra un símbolo del sistema y cambie el directorio para los medios de instalación de la versión de Configuration Manager que quiere instalar.

1. Cambie el directorio a la subcarpeta **SMSSETUP\BIN\X64** y ejecute **Setupdl.exe** con las opciones necesarias.

1. Para revisar los resultados de la descarga, vea **C:\ConfigMgrSetup.log**.

### <a name="command-line-options"></a>Opciones de línea de comandos

Puede usar las siguientes opciones de línea de comandos con **Setupdl.exe**:

- **/VERIFY**: para comprobar los archivos en la carpeta de descarga, que incluyen los archivos de idioma. Para ver la lista de archivos obsoletos, revise **C:\ConfigMgrSetup.log**. Cuando se usa esta opción, no descarga ningún archivo.

- **/VERIFYLANG**: para comprobar solo los archivos de idioma en la carpeta de descarga. Para ver la lista de archivos de idioma obsoletos, revise **C:\ConfigMgrSetup.log**.

- **/LANG**: para descargar solo los archivos de idioma en la carpeta de descarga.

- **/NOUI**: Inicie el descargador del programa de instalación sin la interfaz de usuario. Cuando se usa esta opción, se requiere la **ruta de acceso de descarga**.

- **Ruta de acceso de descarga**: para iniciar automáticamente el proceso de comprobación o descarga, especifique la ruta de acceso a la carpeta de descarga. Cuando use la opción **/NOUI**, se requiere la ruta de acceso de descarga. Si no especifica una ruta de acceso de descarga, el descargador del programa de instalación le pedirá que especifique la ruta de acceso. Si la carpeta no existe, el descargador del programa de instalación la crea.

### <a name="example-commands"></a>Comandos de ejemplo

#### <a name="example-1"></a>Ejemplo 1

El descargador del programa de instalación comprueba los archivos de la carpeta de descarga especificada.

`setupdl.exe C:\Download`

#### <a name="example-2"></a>Ejemplo 2

El descargador del programa de instalación solo comprueba los archivos de la carpeta de descarga especificada.

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>Ejemplo 3

El descargador del programa de instalación comprueba los archivos de la carpeta de descarga especificada. La herramienta no muestra ninguna interfaz de usuario.

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>Ejemplo 4

El descargador del programa de instalación comprueba los archivos de idioma de la carpeta de descarga especificada y luego descarga solo los archivos de idioma.

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> Copiar a otro equipo los archivos del descargador del programa de instalación

1. En el Explorador de Windows, vaya a una de las siguientes ubicaciones:

    - **&lt;Medios de instalación de Configuration Manager>\SMSSETUP\BIN\X64**

    - **&lt;Ruta de instalación de Configuration Manager>\BIN\X64**

1. Copie los archivos siguientes en la misma carpeta de destino del otro equipo:

    - **setupdl.exe**

    - **.\\&lt;idioma>\\setupdlres.dll**

        > [!NOTE]
        > Este archivo se encuentra en la subcarpeta del idioma de instalación. Por ejemplo, el idioma inglés se encuentra en la subcarpeta `00000409`.

    Las carpetas de destino del dispositivo deben ser similares al ejemplo siguientes:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Ejecute el descargador del programa de instalación desde el equipo de destino. Use la [interfaz de usuario](#bkmk_ui) o el [símbolo del sistema](#bkmk_cmd).
