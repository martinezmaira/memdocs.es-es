---
title: Herramienta de limpieza de la biblioteca de contenido
titleSuffix: Configuration Manager
description: Use la herramienta de limpieza de la biblioteca de contenido para quitar contenido huérfano que ya no esté asociado con una implementación de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703633"
---
# <a name="content-library-cleanup-tool"></a>Herramienta de limpieza de la biblioteca de contenido

*Se aplica a: Configuration Manager (rama actual)*

Use la herramienta de línea de comandos de limpieza de la biblioteca de contenido para quitar contenido que ya no esté asociado con ningún paquete o aplicación en un punto de distribución. Este tipo de contenido se denomina *contenido huérfano*. Esta herramienta sustituye a las versiones anteriores de herramientas similares publicadas para productos anteriores de Configuration Manager.  

La herramienta solo afecta al contenido del punto de distribución que especifique al ejecutar la herramienta. La herramienta no puede quitar el contenido de la biblioteca de contenido en el servidor de sitio.

Busque **ContentLibraryCleanup.exe** en `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` en el servidor de sitio.



## <a name="requirements"></a>Requisitos  

- La herramienta solo se puede ejecutar en un único punto de distribución a la vez.  

- Ejecútela directamente en el equipo que hospeda el punto de distribución que se va a limpiar, o bien de manera remota desde otro equipo.  

- La cuenta de usuario que ejecuta la herramienta debe tener los mismos permisos que el rol de seguridad **Administrador total** en Configuration Manager.  



## <a name="modes-of-operation"></a>Modos de operación

Ejecute la herramienta en los dos modos siguientes: [Hipótesis](#what-if-mode) y [Eliminación](#delete-mode).

> [!Tip]  
> Comience con el modo *Hipótesis*. Cuando esté satisfecho con los resultados, ejecute la herramienta en modo *Eliminación*.  


### <a name="what-if-mode"></a>Modo Hipótesis   

Si no se especifica el parámetro `/delete`, la herramienta se ejecuta en modo de hipótesis. Este modo identifica el contenido que se podría eliminar del punto de distribución.

- Cuando se ejecuta en este modo, la herramienta no elimina ningún dato.  

- La herramienta escribe en el archivo de registro información sobre el contenido que podría eliminar. No se le solicita que confirme cada eliminación potencial.  


### <a name="delete-mode"></a>Modo de eliminación   

Cuando la herramienta se ejecuta con el parámetro `/delete`, se ejecuta en el modo de eliminación.

- Cuando se ejecuta en este modo, el contenido huérfano que detecta en el punto de distribución especificado se puede eliminar de la biblioteca de contenido del punto de distribución.  

- Antes de eliminar cada archivo, confirme que la herramienta debe eliminarlo. Haga clic en **S** para sí, **N** para no o **Sí a todo** para omitir mensajes adicionales y eliminar todo el contenido huérfano.  


### <a name="log-file"></a>Archivo de registro

Al ejecutar la herramienta en cualquiera de los modos, crea un registro de forma automática. Asigna un nombre al archivo de registro con la información siguiente: 
- El modo en que se ejecuta la herramienta  
- El nombre del punto de distribución  
- La fecha y hora de la operación  

Cuando la herramienta termina, abre automáticamente el archivo de registro en Windows. 

De forma predeterminada, la herramienta escribe el archivo de registro en la carpeta temporal de la cuenta de usuario que ejecuta la herramienta. Esta ubicación se encuentra en el equipo donde se ejecuta la herramienta, que no siempre es el destino de la herramienta. Use el parámetro `/log` para redirigir el archivo de registro a otra ubicación, incluido un recurso compartido de red.



## <a name="run-the-tool"></a>Ejecutar la herramienta

Para ejecutar la herramienta: 

1. Abra un símbolo del sistema como administrador. Cambie el directorio a la carpeta que contiene **ContentLibraryCleanup.exe**.  

2. Escriba una línea de comandos que incluya los [parámetros de línea de comandos necesarios](#bkmk_params) y cualquier parámetro opcional que quiera usar.



## <a name="command-line-parameters"></a><a name="bkmk_params"></a> Parámetros de línea de comandos  

Use estos parámetros de línea de comandos en cualquier orden.   

### <a name="required-parameters"></a>Parámetros requeridos

|Parámetro|Detalles|
|---------|-------|
| `/dp <distribution point FQDN>`  | Especifique el nombre de dominio completo (FQDN) del punto de distribución que se va a limpiar. |
| `/ps <primary site FQDN>` | Solo es *requerido* al limpiar contenido de un punto de distribución en un sitio secundario. La herramienta se conecta al sitio primario principal para ejecutar consultas en el proveedor de SMS. Estas consultas permiten que la herramienta determine qué contenido debe estar en el punto de distribución. Después puede identificar el contenido huérfano que se va a quitar. Esta conexión con el sitio primario principal se debe realizar para los puntos de distribución de un sitio secundario, ya que los detalles necesarios no están disponibles directamente en el sitio secundario.|
| `/sc <primary site code>`  | Solo es *requerido* al limpiar contenido de un punto de distribución en un sitio secundario. Especifique el código de sitio del sitio primario principal. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Ejemplo: Análisis y registro del contenido que se podría eliminar (hipótesis)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Ejemplo: Análisis y registro del contenido de un punto de distribución en un sitio secundario
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Parámetros opcionales

|Parámetro|Detalles|
|---------|-------|
|`/delete`| Use este parámetro cuando esté listo para eliminar contenido del punto de distribución. Antes de eliminar el contenido le pedirá que lo confirme. </br></br> Si no se usa este parámetro, la herramienta registra los resultados sobre el contenido que podría eliminar. Sin este parámetro, en realidad no elimina ningún contenido del punto de distribución. |
| `/q` | Este parámetro ejecuta la herramienta en un modo silencioso que suprime todos los mensajes. Estos mensajes incluyen cuándo elimina el contenido. Tampoco abre el archivo de registro de forma automática. |
| `/ps <primary site FQDN>` | Opcional solo al limpiar contenido de un punto de distribución en un sitio primario. Especifique el FQDN del sitio primario al que pertenece el punto de distribución. |
| `/sc <primary site code>` | Opcional solo al limpiar contenido de un punto de distribución en un sitio primario. Especifique el código de sitio del sitio primario al que pertenece el punto de distribución. |
| `/log <log file directory>` | Especifique la ubicación donde la herramienta escribe el archivo de registro. Esta ubicación puede ser una unidad local o un recurso compartido de red.</br></br> Si no se usa este parámetro, la herramienta coloca el archivo de registro en el directorio temporal del usuario en el equipo donde se ejecuta la herramienta.|

#### <a name="example-delete-content"></a>Ejemplo: Eliminar contenido 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Ejemplo: Eliminar contenido sin pedir confirmación
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Ejemplo: Registro en la unidad local
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Ejemplo: Registro en un recurso compartido de red
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Problema conocido

Cuando se produce un error en un paquete o una implementación, o bien está en curso, es posible que la herramienta devuelva el error siguiente: `System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

No hay ninguna solución para este problema. La herramienta no puede identificar de manera confiable archivos huérfanos cuando el contenido está en curso o si se ha producido un error en la implementación. La herramienta no permitirá que el contenido se limpie hasta que este problema se resuelva.
