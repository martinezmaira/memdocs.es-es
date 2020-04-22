---
title: Descargador del programa de instalación
titleSuffix: Configuration Manager
description: Lea sobre esta aplicación independiente diseñada para asegurar que la instalación del sitio usa las versiones actuales de los archivos de instalación principales.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700573"
---
# <a name="setup-downloader-for-configuration-manager"></a>Descargador del programa de instalación de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de ejecutar el programa de instalación para instalar o actualizar un sitio de Configuration Manager, puede usar la aplicación independiente del descargador del programa de instalación de la versión de Configuration Manager que quiera instalar para descargar los archivos actualizados del programa de instalación.  

Si usa los archivos actualizados del programa de instalación, la instalación del sitio usará las versiones actuales de los archivos de instalación principales. En resumen:   
-   Al usar el descargador del programa de instalación para descargar los archivos antes de iniciar la instalación, especifique la carpeta que contendrá los archivos.  
-   La cuenta que use para ejecutar el descargador del programa de instalación debe tener permisos de **Control total** de la carpeta de descarga.  
-   Al ejecutar el programa de instalación para instalar o actualizar un sitio, puede dirigirlo para que use esta copia local de los archivos descargados anteriormente. Esto evita que el programa de instalación tenga que conectarse a Microsoft cuando se inicia la instalación o la actualización del sitio.  
-   Puede usar la misma copia local de los archivos de instalación para instalaciones o actualizaciones posteriores del sitio.  

El descargador del programa de instalación descarga los siguientes tipos de archivos:  
-   Archivos redistribuibles como requisitos previos  
-   Paquetes de idioma  
-   Las últimas actualizaciones del producto para el programa de instalación  

Tiene dos opciones para ejecutar el descargador del programa de instalación:
- Ejecutar la aplicación con la interfaz de usuario.
- Para las opciones de línea de comandos, ejecutar la aplicación en un símbolo del sistema.


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> Ejecutar el descargador del programa de instalación con la interfaz de usuario  

1.  En un equipo que tiene acceso a Internet, abra el Explorador de Windows y vaya a **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  Haga doble clic en **Setupdl.exe** para abrir el descargador del programa de instalación.   

3. Especifique la ruta de acceso de la carpeta en la que se hospedarán los archivos de instalación actualizados y después haga clic en **Descargar**. El descargador del programa de instalación comprueba los archivos que se encuentran en la carpeta de descarga. Solo descarga los archivos que faltan o que son más recientes que los archivos existentes. El descargador del programa de instalación crea subcarpetas para los idiomas descargados y otras subcarpetas necesarias.  

4.  Para revisar los resultados de la descarga, abra el archivo **ConfigMgrSetup.log** en el directorio raíz de la unidad C.  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> Ejecutar el descargador del programa de instalación desde el símbolo del sistema  

1.  En una ventana del símbolo del sistema, vaya a **&lt;*medio de instalación de Configuration Manager*\>\SMSSETUP\BIN\X64**.   

2.  Ejecute **Setupdl.exe** para abrir el descargador del programa de instalación.

    Puede usar las siguientes opciones de línea de comandos con **Setupdl.exe**:   

    -   **/VERIFY**: utilice esta opción para comprobar los archivos en la carpeta de descarga, que incluyen los archivos de idioma. Consulte el archivo ConfigMgrSetup.log en el directorio raíz de la unidad C para obtener una lista de archivos que no están actualizados. No se descarga ningún archivo al utilizar esta opción.  

    -   **/VERIFYLANG**: utilice esta opción para comprobar los archivos de idioma en la carpeta de descarga. Consulte el archivo ConfigMgrSetup.log en el directorio raíz de la unidad C para obtener una lista de archivos de idioma que no están actualizados.

    -   **/LANG**: utilice esta opción para descargar solo los archivos de idioma en la carpeta de descarga.  

    -   **/NOUI**: utilice esta opción para iniciar el descargador del programa de instalación sin mostrar la interfaz de usuario. Al usar esta opción, debe especificar la **ruta de acceso de la descarga** como parte del comando en el símbolo del sistema.  

    -   **&lt;DownloadPath\>** : puede especificar la ruta de acceso a la carpeta de descarga para iniciar automáticamente el proceso de comprobación o descarga. Debe especificar la ruta de acceso de descarga al usar la opción **/NOUI**. Si no se especifica ninguna ruta de acceso de descarga, debe especificarla cuando se abra el descargador del programa de instalación. El descargador del programa de instalación crea la carpeta en caso de que no exista.  

    Comandos de ejemplo:

    -   **setupdl &lt;DownloadPath\>**  

        -   El descargador del programa de instalación se inicia, comprueba los archivos de la carpeta de descarga especificada y luego descarga solo los archivos que faltan o que tienen versiones más recientes que los archivos existentes.     

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   El descargador del programa de instalación se inicia y comprueba los archivos de la carpeta de descarga especificada.  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   El descargador del programa de instalación se inicia, comprueba los archivos de la carpeta de descarga especificada y luego descarga solo los archivos que faltan o que son más recientes que los archivos existentes.  

    -   **setupdl /LANG  &lt;DownloadPath\>**  

        -   El descargador del programa de instalación se inicia, comprueba los archivos de idioma de la carpeta de descarga especificada y luego descarga solo los archivos que faltan o que son más recientes que los archivos existentes.  

    -   **setupdl /VERIFY**  

        -   El descargador del programa de instalación se inicia y, a continuación, debe especificar la ruta a la carpeta de descarga. Después de hacer clic en **Comprobar**, el descargador del programa de instalación comprueba los archivos en la carpeta de descarga.  

3.  Para revisar los resultados de la descarga, abra el archivo **ConfigMgrSetup.log** en el directorio raíz de la unidad C.

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> Copiar a otro equipo los archivos del descargador del programa de instalación

1. En el Explorador de Windows, vaya a una de las siguientes ubicaciones:

    - **&lt;Medios de instalación de Configuration Manager>\SMSSETUP\BIN\X64**
    - **&lt;Ruta de instalación de Configuration Manager>\BIN\X64**
    
1. Copie los archivos siguientes en la misma carpeta de destino del otro equipo:
    
    - **setupdl.exe**
    - **.\\&lt;idioma>\\setupdlres.dll**
      - Este archivo se encuentra en la subcarpeta del idioma de instalación. Por ejemplo, el idioma inglés se encuentra en la subcarpeta `00000409`.

    Por ejemplo, estas serían las carpetas de destino de su dispositivo:
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. Inicie el descargador del programa de instalación desde el equipo mediante la [interfaz de usuario](#bkmk_ui) o el [símbolo del sistema](#bkmk_cmd) tal como se describe en las secciones de más arriba.
