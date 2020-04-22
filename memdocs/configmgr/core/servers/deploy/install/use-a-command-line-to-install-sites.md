---
title: Instalación de línea de comandos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo ejecutar el programa de instalación de Configuration Manager en un símbolo del sistema para diversas instalaciones de sitio.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700403"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>Usar una línea de comandos para instalar sitios de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

 Puede ejecutar el programa de instalación de Configuration Manager en un símbolo del sistema para instalar diversos tipos de sitio.

## <a name="supported-tasks-for-command-line-installations"></a>Tareas admitidas para las instalaciones de línea de comandos
 Este método para ejecutar el programa de instalación es compatible con las siguientes tareas de instalación y de mantenimiento del sitio:

- **Instalar un sitio de administración central o sitio primario desde un símbolo del sistema**  
  Consulte [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md) (Opciones de línea de comandos para el programa de instalación).

- **Modificar los idiomas que se pueden usar en un sitio de administración central o sitio primario**  
   Para modificar los idiomas que están instalados en un sitio desde un símbolo del sistema (incluidos los idiomas para dispositivos móviles), debe hacer lo siguiente:  

  - Ejecute el programa de instalación desde **&lt;ConfigMgrInstallationPath\>\Bin\X64** en el servidor de sitio.
  - Use la opción de la línea de comandos **/MANAGELANGS**.
  - Especifique un archivo de script de idioma que especifique los idiomas que quiere agregar o quitar.  

    Por ejemplo, use la siguiente sintaxis de comando: **setupwpf.exe /MANAGELANGS &lt;archivo de script de idioma\>** .  

    Para crear el archivo de script de idioma, use la información de [Command line options to manage languages](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang) (Opciones de línea de comandos para administrar idiomas).  

- **Usar un archivo de script de instalación para realizar instalaciones desatendidas de sitios o para recuperar sitios**  
   Puede ejecutar el programa de instalación desde un símbolo del sistema mediante un script de instalación y ejecutar una instalación desatendida del sitio. También puede usar esta opción para recuperar un sitio.    

   Para usar un script con el programa de instalación, haga lo siguiente:  

  - Ejecute el programa de instalación con la opción de la línea de comandos **/SCRIPT** y especifique un archivo de script.  

  - El archivo de script debe estar configurado con las claves y los valores necesarios.  

    Para llevar a cabo una instalación desatendida de un sitio de administración central o un sitio primario, el archivo de script debe tener las secciones siguientes:  

  - Identificación    
  - Options    
  - SQLConfigOptions    
    -   HierarchyOptions    
  - CloudConnectorOptions   

    Para recuperar un sitio, debe incluir también las siguientes secciones del archivo de script:  

  - Identificación  
  - Recuperación

Para obtener más información, consulte [Recuperación de sitio desatendida de Configuration Manager](../../manage/unattended-recovery.md).  

Para obtener una lista de claves y valores que se pueden usar en un archivo de script de instalación desatendida, vea [Claves de archivo de script de instalación desatendida](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Acerca del archivo de script de línea de comandos  
 Para llevar a cabo instalaciones desatendidas de Configuration Manager, puede ejecutar el programa de instalación con la opción de línea de comandos **/SCRIPT** y especificar un archivo de script que contenga opciones de instalación. Este método admite las siguientes tareas:  

-   Instalar un sitio de administración central  
-   Instalar un sitio primario  
-   Instalar una consola de Configuration Manager  
-   Recuperar un sitio  

> [!NOTE]  
>  No puede usar el archivo de script de instalación desatendida para actualizar un sitio de evaluación a una instalación con licencia de Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>El nombre de clave CDLatest
Si usa medios de la carpeta CD.Latest para ejecutar una instalación por script de las cuatro opciones de instalación siguientes, el script debe incluir la clave **CDLatest** con un valor de **1**:
- Instalar un sitio de administración central nuevo
- Instalar un sitio primario nuevo
- Recuperar un sitio de administración central
- Recuperar un sitio primario

El uso de este valor no se admite con los medios de instalación obtenidos del sitio de licencia por volumen de Microsoft.
Vea las [opciones de línea de comandos](command-line-options-for-setup.md) para obtener información sobre cómo utilizar este nombre de clave en el archivo de script.



### <a name="create-the-script"></a>Crear el script
El script de instalación se crea automáticamente al [ejecutar el programa de instalación para instalar un sitio mediante la interfaz de usuario](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Cuando se confirma la configuración en la página **Resumen** del asistente, sucede lo siguiente:  

-   El programa de instalación crea el script **%TEMP%\ConfigMgrAutoSave.ini**.  Puede cambiar el nombre de este archivo antes de usarlo, pero este debe conservar la extensión de archivo .ini.  
-   El script de instalación desatendida contiene la configuración seleccionada en el asistente.  
-   Después de crear el script, puede modificarlo para instalar otros sitios en la jerarquía.  
-   Luego puede usar este script para realizar una instalación desatendida de Configuration Manager.  

El archivo de script proporciona el mismo tipo de información que solicita el Asistente para instalación, excepto por el hecho de que no existe una configuración predeterminada.   
Debe especificar todos los valores de las claves de configuración que se aplican al tipo de instalación que esté usando.   

Cuando el programa de instalación crea el script de instalación desatendida, se rellena con el valor de clave de producto que especifique durante la instalación. Este puede ser una clave de producto válida, o bien **EVAL** si instala una versión de evaluación de Configuration Manager. El valor de la clave de producto en el script se rellena para que la comprobación de requisitos previos pueda finalizar.   

Cuando el programa de instalación inicia la instalación real de un sitio, el script creado automáticamente se escribe otra vez para borrar el valor de la clave de producto en el script que crea. Antes de usar el script para la instalación desatendida de un nuevo sitio, puede editarlo para proporcionar una clave de producto válida o especificar una instalación de evaluación de Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Nombres de sección, nombres de clave y valores
El script contiene valores, nombres de clave y nombres de sección. Tenga en cuenta la información siguiente:
-   Los nombres de clave de sección requeridos varían según el tipo de instalación para el que crea el script.
-   No hay un orden determinado para las secciones ni para las claves de las secciones.     
-   Las claves no distinguen mayúsculas de minúsculas.  
-   Cuando proporcione valores para las claves, el nombre de la clave debe ir seguido por un signo igual (=) y el valor de la clave.    

> [!TIP]  
>  Para ver el conjunto completo de opciones, consulte [Command-line options for Setup and scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md) (Opciones de línea de comandos para el programa de instalación y los scripts).  

## <a name="use-the-script-setup-command-line-option"></a>Usar la opción de la línea de comandos de instalación /SCRIPT

-   Debe usar un archivo de script de instalación y especificar el nombre de archivo después de la opción de línea de comandos del programa de instalación **/SCRIPT**. Tenga en cuenta la información siguiente:   
    -   El nombre del archivo debe tener la extensión de nombre de archivo **.ini**.  
    -   Cuando hace referencia al archivo de script del programa de instalación en el símbolo del sistema, debe proporcionar la ruta de acceso completa al archivo. Por ejemplo, si su archivo de inicialización de instalación se denomina Setup.ini y se almacena en la carpeta C:\Setup, en el símbolo del sistema, escriba: **setup /script c:\setup\setup.ini**.  

-   La cuenta que ejecuta el programa de instalación debe tener derechos de **administrador** en el equipo. Al ejecutar el programa de instalación con el script de instalación desatendida, abra la ventana del símbolo del sistema mediante la opción **Ejecutar como administrador**.   
