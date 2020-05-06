---
title: Archivos de definición del paquete
titleSuffix: Configuration Manager
description: Obtenga información sobre el uso de archivos de definición del paquete para crear paquetes y programas en Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689333"
---
# <a name="package-definition-files"></a>Archivos de definición del paquete

*Se aplica a: Configuration Manager (rama actual)*

Los archivos de definición del paquete son scripts que facilitan automatizar la creación de [paquetes y programas](packages-and-programs.md) en Configuration Manager. Proporcionan toda la información que Configuration Manager necesita para crear un paquete y un programa, excepto la ubicación de los archivos de origen del paquete.

## <a name="about-the-package-definition-file-format"></a>Sobre el formato de archivo de definición de paquete

Cada archivo de definición del paquete es un archivo de texto ASCII o UTF-8 que usa el formato de archivo .ini. Contiene las secciones siguientes:  

### <a name="pdf"></a>[PDF]

Esta sección identifica el archivo como un archivo de definición de paquete. Contiene la siguiente información:  

- **Versión**: especifique la versión del formato del archivo de definición del paquete que usa el archivo. Esta versión se corresponde a la de Configuration Manager para la que se ha escrito. Esta entrada es necesaria.  

### <a name="package-definition"></a>[Definición del paquete]

Especifique las propiedades del paquete y del programa. Proporciona la siguiente información:  

- **Nombre**: el nombre del paquete, de hasta 50 caracteres.  

- **Versión** (opcional): la versión del paquete, de hasta 32 caracteres.  

- **Icono** (opcional): archivo que contiene el icono que se va a usar para este paquete. Si se especifica, este icono reemplaza al icono de paquete predeterminado en la consola de Configuration Manager.

- **Publicador**: el publicador del paquete, de hasta 32 caracteres.

- **Idiomas**: la versión de idioma del paquete, de hasta 32 caracteres.

- **Comentario** (opcional): comentario sobre el paquete, de hasta 127 caracteres.

- **ContainsNoFiles**: esta entrada indica si el paquete tiene archivos de código fuente.  

- **Programas**: los programas que se definen para este paquete. Cada nombre de programa se corresponde con un **[programa]** sección en este archivo de definición de paquete.  

    Ejemplo:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: el nombre del archivo de formato de información de administración (MIF) que contiene el estado del paquete, hasta 50 caracteres.  

- **MIFName**: el nombre del paquete para la coincidencia de MIF, hasta 50 caracteres.  

- **MIFVersion**: el número de versión del paquete para la coincidencia de MIF, hasta 32 caracteres.  

- **MIFPublisher**: el editor de software del paquete para la coincidencia de MIF, hasta 32 caracteres.  

### <a name="program"></a>[programa]

Incluya una sección [Programa] para cada programa que especifique en la entrada **Programas** de la sección **[Definición de paquete]** . En esta sección se define cada programa. Cada sección de programa proporciona la siguiente información:  

- **Nombre**: el nombre del programa, hasta 50 caracteres. Esta entrada debe ser única dentro de un paquete.  

- **Icono** (opcional): especifique el archivo que contiene el icono que se va a usar para este programa. Este icono reemplaza el icono de programa predeterminado en la consola de Configuration Manager. El cliente también muestra este icono al implementar el programa en una colección.

- **Comentario** (opcional): comentario sobre el programa, de hasta 127 caracteres.

- **CommandLine**: especifique la línea de comandos del programa, de hasta 127 caracteres. El comando es relativa a la carpeta de origen del paquete.

- **StartIn**: especifique la carpeta de trabajo del programa, de hasta 127 caracteres. Esta entrada puede ser una ruta de acceso absoluta en el equipo cliente o una ruta de acceso relativa a la carpeta de origen del paquete.

- **Ejecutar**: especifique el modo de programa en el que se ejecuta el programa. Puede especificar **minimizada**, **maximizado**, o **Hidden**. Si no se incluye esta entrada, el programa se ejecuta en modo normal.  

- **AfterRunning**: especifique alguna acción especial que se produzca cuando el programa se complete correctamente. Las opciones disponibles son **SMSRestart**, **ProgramRestart**, o **SMSLogoff**. Si no se incluye esta entrada, el programa no ejecuta una acción especial.  

- **EstimatedDiskSpace**: especifique la cantidad de espacio en disco que requiere el programa de software para poder ejecutarse en el equipo. El valor predeterminado es **Desconocido**. Puede establecer el valor como un número entero mayor o igual que cero. Si especifica un valor, incluya también las unidades de este.  

    Ejemplo:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**: especifique la duración estimada en minutos que espera que el programa se ejecute en el equipo cliente. El valor predeterminado es **120**. Puede establecer el valor como un número entero mayor que cero, o bien como **Desconocido**.  

    Ejemplo:  

    `EstimatedRunTime=25`  

- **SupportedClients**: especifique los procesadores y sistemas operativos en los que se ejecuta este programa. Separe las plataformas mediante comas. Si no incluye esta entrada, el cliente no comprueba las plataformas admitidas para este programa.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: especifique el intervalo de inicio a fin de los números de versión de los sistemas operativos especificados en la entrada **SupportedClients**.  

    Ejemplo:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (opcional): proporcione otra información o requisitos de los equipos cliente, hasta 127 caracteres.

- **CanRunWhen**: especifique el estado de usuario que el programa requiere para ejecutarse en el equipo cliente. Los valores disponibles son **UserLoggedOn**, **NoUserLoggedOn**, o **AnyUserStatus**. El valor predeterminado es **UserLoggedOn**.  

- **UserInputRequired**: especifique si el programa requiere interacción con el usuario. Los valores disponibles son **True** o **False**. El valor predeterminado es **True**. Esta entrada se establece en **False** si **CanRunWhen** no está establecido en **UserLoggedOn**.  

- **AdminRightsRequired**: especifique si el programa requiere credenciales administrativas en el equipo para ejecutarse. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**. Esta entrada se establece en **True** si **CanRunWhen** no está establecido en **UserLoggedOn**.  

- **UseInstallAccount**: especifique si el programa usa la cuenta de instalación del software cliente cuando se ejecuta en equipos cliente. De forma predeterminada, este valor es **False**. Este valor también es **False** si **CanRunWhen** está establecido en **UserLoggedOn**.  

- **DriveLetterConnection**: especifique si el programa requiere la conexión de una letra de unidad a los archivos del paquete en el punto de distribución. Puede especificar **True** o **False**. El valor predeterminado es **False**, lo que permite al programa usar una conexión de convención de nomenclatura universal (UNC). Cuando este valor se establece en **True**, el cliente usa la siguiente letra de unidad disponible, comenzando por Z: y continuando hacia atrás.  

- **SpecifyDrive** (opcional): especifique una letra de unidad que el programa necesita para conectarse a los archivos del paquete en el punto de distribución. Este valor fuerza el uso de la letra de unidad especificada para las conexiones de cliente a los puntos de distribución.

- **ReconnectDriveAtLogon**: especifique si el equipo se vuelve a conectar al punto de distribución cuando el usuario inicia sesión. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**.  

- **DependentProgram**: especifique un programa de este paquete que se tenga que ejecutar antes del programa actual. Esta entrada usa el formato `DependentProgram=<ProgramName>`, donde `<ProgramName>` es la entrada **Name** de ese programa en el archivo de definición del paquete. Si no hay ningún programa dependiente, deje en blanco esta entrada.  

    Ejemplos:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Asignación**: especifique cómo se asigna el programa a los usuarios. Este valor puede ser:

    - **FirstUser**: solo el primer usuario que inicia sesión en el cliente ejecuta el programa.
    - **EveryUser**: todos los usuarios que inician sesión ejecutan el programa.

    Cuando **CanRunWhen** no está establecido en **UserLoggedOn**, esta entrada se establece en **FirstUser**.  

- **Disabled**: especifique si se puede implementar este programa en los clientes. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**.  


## <a name="use-a-package-definition-file"></a>Use un archivo de definición de paquete  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**.  

2. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear paquete a partir de definición**.  

3. En la página **Definición de paquete** del **Asistente para crear paquete a partir de definición**, elija un archivo de definición del paquete existente. Para abrir un archivo de definición del paquete nuevo, elija **Examinar**. Después de especificar un archivo de definición del paquete nuevo, selecciónelo en la lista **Definición del paquete**.

4. En la página **Archivos de origen**, especifique la información sobre los archivos de origen necesarios para el paquete y el programa.  

5. Si el paquete requiere archivos de origen, en la página **Carpeta de origen**, especifique la ubicación desde la que el sitio puede obtenerlos.  

6. Complete el asistente.  


## <a name="see-also"></a>Vea también

[Paquetes y programas](packages-and-programs.md)
