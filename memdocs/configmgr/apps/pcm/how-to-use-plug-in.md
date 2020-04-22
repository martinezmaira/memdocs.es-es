---
title: Uso del complemento de conversión
titleSuffix: Configuration Manager
description: Use el complemento del Administrador de conversión de paquetes para personalizar los procesos de análisis y conversión.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688963"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Cómo usar el complemento del Administrador de conversión de paquetes

*Se aplica a: Configuration Manager (rama actual)*

<!--1357861-->

El complemento del Administrador de conversión de paquetes le ayuda a personalizar los procesos de análisis y conversión. Para usar el complemento del Administrador de conversión de paquetes, escriba un archivo ejecutable o un archivo de script que realice operaciones personalizadas. A continuación, edite el archivo de configuración, Microsoft.ConfigurationManagement.exe.config, para llamar al ejecutable o script. Los lenguajes más comunes que se usan para escribir el script son VBScript o PowerShell.

El complemento del Administrador de conversión de paquetes se ejecuta una vez para cada paquete. Si analiza o convierte varios paquetes al mismo tiempo, el complemento del Administrador de conversión de paquetes se ejecuta cada vez.

> [!NOTE]  
> Para más información sobre los elementos del Administrador de conversión de paquetes en el archivo de configuración de Configuration Manager, vea [Referencia técnica del XML de configuración del complemento del Administrador de conversión de paquetes](plugin-config-xml.md).



## <a name="default-process"></a>Proceso predeterminado

De forma predeterminada, el Administrador de conversión de paquetes realiza las siguientes acciones:

1.  Lee un paquete de Configuration Manager.  

2.  Crea una aplicación a partir del paquete y agrega atributos predeterminados.  

3.  Analiza la aplicación y determina el estado de la preparación del paquete.  

4.  Realiza una de las acciones siguientes, según la operación del Administrador de conversión de paquetes:  

    - **Analizar**: mostrar el estado de preparación del paquete en la consola de Configuration Manager.  

    - **Convertir**: escribir la aplicación en la base de datos de Configuration Manager.  


## <a name="plug-in-based-process"></a>Proceso basado en el complemento 

Al usar el complemento, el Administrador de conversión de paquetes realiza las siguientes acciones:

1.  Lee un paquete de Configuration Manager.  

2.  Crea una aplicación a partir del paquete y agrega atributos predeterminados.  

3.  Convierte la aplicación a XML. Luego guarda el archivo en el disco.  

4.  Ejecuta el script del complemento para modificar el XML de la aplicación. Para más información, vea [Referencia técnica del XML de configuración del complemento del Administrador de conversión de paquetes](plugin-config-xml.md).  

5.  Convierte el XML de la aplicación en una aplicación de Configuration Manager.  

6.  Analiza la aplicación y determina el estado de la preparación del paquete.  

7.  Realiza una de las acciones siguientes, según la operación del Administrador de conversión de paquetes:  

    - **Analizar**: mostrar el estado de preparación del paquete en la consola de Configuration Manager.  

    - **Convertir**: escribir la aplicación en la base de datos de Configuration Manager.  



## <a name="see-also"></a>Vea también

[Referencia técnica del XML de configuración del complemento del Administrador de conversión de paquetes](plugin-config-xml.md)
