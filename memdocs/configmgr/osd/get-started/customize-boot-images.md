---
title: 'Personalizar imágenes de arranque '
titleSuffix: Configuration Manager
description: Conozca diversas maneras de usar Configuration Manager o la herramienta de línea de comandos de Administración y mantenimiento de imágenes de implementación (DISM) para personalizar una imagen de arranque.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc679ec7e73e9d43902ad70e09fb2a01c95eed65
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906877"
---
# <a name="customize-boot-images-with-configuration-manager"></a>Personalización de imágenes de arranque con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Cada versión de Configuration Manager admite una determinada versión de Windows Assessment and Deployment Kit (Windows ADK). Puede mantener o personalizar imágenes de arranque desde la consola de Configuration Manager si se basan en una versión de Windows PE de la versión admitida de Windows ADK. Puede personalizar otras imágenes de arranque mediante otros métodos como, por ejemplo, a través de la herramienta de línea de comandos DISM (Administración y mantenimiento de imágenes de implementación) que forma parte de AIK de Windows y Windows ADK.  

 En la tabla siguiente se proporciona la versión admitida de Windows ADK, la versión de Windows PE en la que se basa la imagen de arranque y que se puede personalizar mediante la consola de Configuration Manager, y las versiones de Windows PE en las que se basa la imagen de arranque, que se pueden personalizar mediante DISM y, después, agregar la imagen a Configuration Manager.  

- **Versión de Windows ADK**  

   Windows ADK para Windows 10  

- **Versiones de Windows PE para imágenes de arranque personalizables desde la consola de Configuration Manager**  

   Windows PE 10  

- **Versiones admitidas de Windows PE para imágenes de arranque que no se pueden personalizar desde la consola de Configuration Manager**  

   Windows PE 3.1<sup>1</sup> y Windows PE 5  

   <sup>1</sup> Solo se puede agregar una imagen de arranque a Configuration Manager si se basa en Windows PE 3.1. Instale el complemento de AIK de Windows para Windows 7 SP1 a fin de actualizar AIK de Windows para Windows 7 (basado en Windows PE 3) con el complemento de AIK de Windows para Windows 7 SP1 (basado en Windows PE 3.1). Puede descargar el complemento de AIK de Windows para Windows 7 SP1 en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

   Por ejemplo, si tiene Configuration Manager, puede personalizar imágenes de arranque desde Windows ADK para Windows 10 (basado en Windows PE 10) mediante la consola de Configuration Manager. Sin embargo, aunque se admiten imágenes de arranque basadas en Windows PE 5, debe personalizarlas desde otro equipo y usar la versión de DISM instalada con Windows ADK para Windows 8. Después, puede agregar la imagen de arranque a la consola de Configuration Manager.  

  En los procedimientos de este tema se muestra cómo agregar los componentes adicionales requeridos por Configuration Manager a la imagen de arranque mediante los paquetes de Windows PE siguientes:  

- **WinPE-WMI**: agrega compatibilidad con Instrumental de administración de Windows (WMI).  

- **WinPE-Scripting**: agrega compatibilidad con Windows Script Host (WSH).  

- **WinPE-WDS-Tools**: instala las herramientas de Servicios de implementación de Windows.  

  Hay otros paquetes de Windows PE que puede agregar. Para obtener más información sobre los componentes opcionales que puede agregar a la imagen de arranque, consulte [WinPE: agregar paquetes (referencia de los componentes opcionales)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

> [!NOTE]
>Al arrancar en WinPE desde una imagen de arranque personalizada que incluye herramientas que se han agregado, puede abrir un símbolo del sistema desde WinPE y escribir el nombre de archivo de la herramienta para ejecutarla. La ubicación de estas herramientas se agrega automáticamente a la variable de ruta de acceso. Solo se puede agregar el símbolo del sistema si está seleccionada la opción **Habilitar compatibilidad de comando (solo prueba)** en la pestaña **Personalización** de las propiedades de la imagen de arranque.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Personalizar una imagen de arranque que usa Windows PE 5  
 Para personalizar una imagen de arranque que usa Windows PE 5, debe instalar Windows ADK y usar la herramienta de línea de comandos DISM para montar la imagen de arranque, agregar componentes y controladores opcionales y confirmar los cambios en la imagen de arranque. Utilice el procedimiento siguiente para personalizar la imagen de arranque.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Para personalizar una imagen de arranque que usa Windows PE 5  

1. Instale Windows ADK en un equipo que no tenga ninguna otra versión de AIK de Windows o Windows ADK, y que no tenga instalado ningún componente de Configuration Manager.  

2. Descargue Windows ADK para Windows 8.1 del [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=39982).  

3. Copie la imagen de arranque (wimpe.wim) de la carpeta de instalación de Windows ADK (por ejemplo, <*ruta de instalación*>\Windows Kits\\<*versión*>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<*x86 o amd64*>\\<*configuración regional*>) a una carpeta de destino en el equipo en el que se personalizará la imagen de arranque. En este procedimiento se utiliza C:\WinPEWAIK como nombre de carpeta de destino.  

4. Use DISM para montar la imagen de arranque en una carpeta local de Windows PE. Por ejemplo, escriba la siguiente línea de comandos:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    En la que C:\WinPEWAIK es la carpeta que contiene la imagen de arranque y C:\WinPEMount es la carpeta montada.  

   > [!NOTE]
   >  Para obtener más información, consulte la referencia de [DISM (administración y mantenimiento de imágenes de implementación)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

5. Después de montar la imagen de arranque, use DISM para agregar componentes opcionales a la imagen de arranque. En Windows PE 5, los componentes opcionales de 64 bits se encuentran en <*ruta de instalación*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs.  

   > [!NOTE]
   >  En este procedimiento se utiliza la siguiente ubicación para los componentes opcionales: C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs. La ruta de acceso que se utiliza puede variar según las opciones de instalación y la versión que elija para Windows ADK.  

    Escriba lo siguiente para instalar los componentes opcionales:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<configuración regional\>* **\WinPE-SecureStartup_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<configuración regional\>* **\WinPE-WMI_** *<configuración regional\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<configuración regional\>* **\WinPE-Scripting** *<configuración regional\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<configuración regional\>* **\WinPE-WDS-Tools_** *<configuración regional\>* **.cab"**  

    Donde C:\WinPEMount es la carpeta montada y locale es la configuración regional para los componentes. Por ejemplo, para la configuración regional **en-us** , escriba:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

   > [!TIP]
   >  Para obtener más información sobre los componentes opcionales que puede agregar a la imagen de arranque, consulte el tema [Referencia de los componentes opcionales de Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

6. Use DISM para agregar controladores a la imagen de arranque cuando sea necesario. Escriba lo siguiente para agregar controladores a la imagen de arranque:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *ruta de acceso al archivo .inf del controlador* **>**  

    Donde C:\WinPEMount es la carpeta montada.  

7. Escriba lo siguiente para desmontar el archivo de imagen de arranque y confirmar los cambios.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Donde C:\WinPEMount es la carpeta montada.  

8. Agregue la imagen de arranque actualizada a Configuration Manager para que se pueda usar en las secuencias de tareas. Utilice los pasos siguientes para importar la imagen de arranque actualizada:  

   1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

   2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

   3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Agregar imagen de arranque** para iniciar el Asistente para agregar imagen de archivo.  

   4. En la página **Origen de datos** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**:  

      - En el cuadro **Ruta de acceso** , especifique la ruta de acceso del archivo actualizado de imagen de arranque. La ruta de acceso especificada debe ser una ruta de acceso de red válida con el formato UNC. Por ejemplo: **\\\\<** <em>nombreDeServidor</em> **>\\<** <em>recurso compartido de WinPEWAIK</em> **>\winpe.wim**.  

      - Seleccione la imagen de arranque de la lista desplegable **Imagen de arranque** . Si el archivo WIM contiene varias imágenes de arranque, se mostrará cada imagen.  

   5. En la página **General** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

      -   En el cuadro **Nombre** , especifique un nombre único para la imagen de arranque.  

      -   En el cuadro **Versión** , especifique un número de versión para la imagen de arranque.  

      -   En el cuadro **Comentario** , especifique una descripción breve sobre cómo se utiliza la imagen de arranque.  

   6. Complete el asistente.  

9. Puede habilitar un shell de comandos en la imagen de arranque para depurar y solucionar problemas de Windows PE. Utilice los pasos siguientes para habilitar el shell de comandos.  

   1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

   2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

   3. Busque la nueva imagen de arranque en la lista y el identificador de paquete de la imagen. Puede encontrar el identificador de paquete en la columna **Id. de imagen** de la imagen de arranque.  

   4. En un símbolo del sistema, escriba **wbemtest** para abrir la Herramienta de comprobación del instrumental de administración de Windows.  

   5. Escriba **\\\\<** <em>Equipo del proveedor de SMS</em> **>\root\sms\site_<** <em>código de sitio</em> **>** en **Espacio de nombres** y, después, haga clic en **Conectar**.  

   6. Haga clic en **Abrir instancia**, escriba **sms_bootimagepackage.packageID="<idDePaquete\>"** y haga clic en **Aceptar**. Como IDdepaquete, escriba el valor que se identificó en el paso 3.  

   7. Haga clic en **Actualizar objeto**y, a continuación, haga clic en **EnableLabShell** en el panel **Propiedades** .  

   8. Haga clic en **Modificar propiedad**, cambie el valor a **TRUE**y haga clic en **Guardar propiedad**.  

   9. Haga clic en **Guardar objeto**y, tras ello, salga de la Herramienta de comprobación del instrumental de administración de Windows.  

10. Debe distribuir la imagen de arranque en puntos de distribución, grupos de puntos de distribución o recopilaciones asociadas con grupos de puntos de distribución para poder usar la imagen de arranque en una secuencia de tareas. Utilice los pasos siguientes para distribuir la imagen de arranque.  

    1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

    2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

    3.  Haga clic en la imagen de arranque que se identificó en el paso 3.  

    4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Actualizar puntos de distribución**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Personalizar una imagen de arranque que usa Windows PE 3.1  
 Para personalizar una imagen de arranque que usa WinPE 3.1, debe instalar AIK de Windows, instalar el complemento de AIK de Windows para Windows 7 SP1 y usar la herramienta de línea de comandos DISM para montar la imagen de arranque, agregar componentes y controladores opcionales y confirmar los cambios en la imagen de arranque. Utilice el procedimiento siguiente para personalizar la imagen de arranque.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Para personalizar una imagen de arranque que usa Windows PE 3.1  

1. Instale AIK de Windows en un equipo que no tenga ninguna otra versión de AIK de Windows o Windows ADK, y que no tenga instalado ningún componente de Configuration Manager. Descargue AIK de Windows del [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=5753).  

2. Instale el complemento de AIK de Windows para Windows 7 con SP1 en el equipo en el paso 1. Descargue el complemento de AIK de Windows para Windows 7 SP1 en el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

3. Copie la imagen de arranque (wimpe.wim) de la carpeta de instalación de AIK de Windows (por ejemplo, <*rutaDeInstalación*>\Windows AIK\Tools\PETools\amd64\\) en una carpeta del equipo en el que desea personalizar la imagen de arranque. En este procedimiento se utiliza C:\WinPEWAIK como nombre de carpeta.  

4. Use DISM para montar la imagen de arranque en una carpeta local de Windows PE. Por ejemplo, escriba la siguiente línea de comandos:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    En la que C:\WinPEWAIK es la carpeta que contiene la imagen de arranque y C:\WinPEMount es la carpeta montada.  

   > [!NOTE]
   > Para obtener más información, consulte la referencia de [DISM (administración y mantenimiento de imágenes de implementación)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

5. Después de montar la imagen de arranque, use DISM para agregar componentes opcionales a la imagen de arranque. En Windows PE 3.1, por ejemplo, los componentes opcionales se encuentran en <*rutaDeInstalación*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\.  

   > [!NOTE]
   >  En este procedimiento se utiliza la siguiente ubicación para los componentes opcionales: C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs. La ruta de acceso que se utiliza puede variar según las opciones de instalación y la versión que elija para AIK de Windows.  

    Escriba lo siguiente para instalar los componentes opcionales:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<configuración regional\>* **\winpe-wmi_** *<configuración regional\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<configuración regional\>* **\winpe-scripting_** *<configuración regional\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<configuración regional\>* **\winpe-wds-tools_** *<configuración regional\>* **.cab"**  

    Donde C:\WinPEMount es la carpeta montada y locale es la configuración regional para los componentes. Por ejemplo, para la configuración regional **en-us** , escriba:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Archivos de programa\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

   > [!TIP]
   >  Para más información sobre los diferentes paquetes que puede agregar a la imagen de arranque, consulte el tema [Agregar un paquete a una imagen de Windows PE](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd799312(v=ws.10)).

6. Use DISM para agregar controladores a la imagen de arranque cuando sea necesario. Escriba lo siguiente para agregar controladores a la imagen de arranque:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *ruta de acceso al archivo .inf del controlador* **>**  

    Donde C:\WinPEMount es la carpeta montada.  

7. Escriba lo siguiente para desmontar el archivo de imagen de arranque y confirmar los cambios.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Donde C:\WinPEMount es la carpeta montada.  

8. Agregue la imagen de arranque actualizada a Configuration Manager para que se pueda usar en las secuencias de tareas. Utilice los pasos siguientes para importar la imagen de arranque actualizada:  

   1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

   2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

   3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Agregar imagen de arranque** para iniciar el Asistente para agregar imagen de archivo.  

   4. En la página **Origen de datos** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**:  

      - En el cuadro **Ruta de acceso** , especifique la ruta de acceso del archivo actualizado de imagen de arranque. La ruta de acceso especificada debe ser una ruta de acceso de red válida con el formato UNC. Por ejemplo: **\\\\<** <em>nombreDeServidor</em> **>\\<** <em>recurso compartido de WinPEWAIK</em> **>\winpe.wim**.  

      - Seleccione la imagen de arranque de la lista desplegable **Imagen de arranque** . Si el archivo WIM contiene varias imágenes de arranque, se mostrará cada imagen.  

   5. En la página **General** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

      -   En el cuadro **Nombre** , especifique un nombre único para la imagen de arranque.  

      -   En el cuadro **Versión** , especifique un número de versión para la imagen de arranque.  

      -   En el cuadro **Comentario** , especifique una descripción breve sobre cómo se utiliza la imagen de arranque.  

   6. Complete el asistente.  

9. Puede habilitar un shell de comandos en la imagen de arranque para depurar y solucionar problemas de Windows PE. Utilice los pasos siguientes para habilitar el shell de comandos.  

   1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

   2. En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

   3. Busque la nueva imagen de arranque en la lista y el identificador de paquete de la imagen. Puede encontrar el identificador de paquete en la columna **Id. de imagen** de la imagen de arranque.  

   4. En un símbolo del sistema, escriba **wbemtest** para abrir la Herramienta de comprobación del instrumental de administración de Windows.  

   5. Escriba **\\\\<** <em>Equipo del proveedor de SMS</em> **>\root\sms\site_<** <em>código de sitio</em> **>** en **Espacio de nombres** y, después, haga clic en **Conectar**.  

   6. Haga clic en **Abrir instancia**, escriba **sms_bootimagepackage.packageID="<idDePaquete\>"** y haga clic en **Aceptar**. Como IDdepaquete, escriba el valor que se identificó en el paso 3.  

   7. Haga clic en **Actualizar objeto**y, a continuación, haga clic en **EnableLabShell** en el panel **Propiedades** .  

   8. Haga clic en **Modificar propiedad**, cambie el valor a **TRUE**y haga clic en **Guardar propiedad**.  

   9. Haga clic en **Guardar objeto**y, tras ello, salga de la Herramienta de comprobación del instrumental de administración de Windows.  

10. Debe distribuir la imagen de arranque en puntos de distribución, grupos de puntos de distribución o recopilaciones asociadas con grupos de puntos de distribución para poder usar la imagen de arranque en una secuencia de tareas. Utilice los pasos siguientes para distribuir la imagen de arranque.  

    1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

    2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de arranque**.  

    3.  Haga clic en la imagen de arranque que se identificó en el paso 3.  

    4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Actualizar puntos de distribución**.  
