---
title: Recopilador de registros
titleSuffix: Configuration Manager
description: Uso de la herramienta de recopilación de registros para la solución de problemas de Análisis de escritorio
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8782913e40bffdcbe5a151fac8821f05b7e7fece
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268579"
---
# <a name="desktop-analytics-log-collector"></a>Recopilador de registros de Análisis de escritorio

A partir de la versión 1906 de Configuration Manager, use la herramienta **DesktopAnalyticsLogsCollector.ps1** del directorio de instalación de Configuration Manager para solucionar problemas de inscripción de dispositivos de Análisis de escritorio. Ejecuta algunos pasos básicos para solucionar problemas y recopila los registros pertinentes en un solo directorio de trabajo. Puede compartir este contenido con el servicio de soporte técnico de Microsoft.


## <a name="prerequisites"></a>Requisitos previos

- Un cliente de Análisis de escritorio con Windows 10, Windows 8.1 o Windows 7 con Service Pack 1

- Ejecute el script en el dispositivo como usuario administrativo y seleccione **Ejecutar como administrador**.

    > [!Tip]
    > Puede usar la característica **Scripts** de Configuration Manager con esta herramienta. Para más información, consulte [Ejemplo 5: Implementación de un script mediante **Scripts**](#bkmk_ex5) de Configuration Manager.

- En Windows 7 con Service Pack 1, la versión 4.0 o posterior de PowerShell.
    - La [versión 4.6 o posterior de .NET Framework](https://dotnet.microsoft.com/download/dotnet-framework).

    - Windows Management Framework [versión 4.0](https://support.microsoft.com/help/2819745) (aka.ms/wmf4download) o [versión 5.1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.ms/wmf5download)

## <a name="usage"></a>Uso

Obtención del script del contenido de instalación de Configuration Manager: `SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parámetros

### `-LogPath`

Especifica una ruta de acceso local o UNC para colocar el registro y otros archivos de salida.

**Valores**:

- ruta de acceso local (longitud máxima = 130), por ejemplo: `c:\myfolder`

- Ruta de acceso UNC (longitud máxima = 130), por ejemplo: `\\myserver\myfolder`

**Tipo**: String

**Posición**: 1

**Valor predeterminado**: `$Env:SystemDrive\M365AnalyticsLogs` (Cuando este parámetro es NULL, está vacío o es un espacio en blanco, el script crea la carpeta M365AnalyticsLogs en la unidad del sistema).

### `-LogMode`

Especifica el nivel de detalle de los registros.

**Valores**:

- `0`: los mensajes de script solo se registran en la ventana de comandos de PowerShell.

- `1`: los mensajes de script de registran en el archivo de registro de la carpeta de salida y en la ventana de comandos de PowerShell.

- `2`: los mensajes de script solo se registran en el archivo de registro de la carpeta de salida.

**Tipo**: Int16

**Posición**: 2

**Valor predeterminado**: `1` (los mensajes de script se registran en el archivo de registro y en la ventana de comandos de PowerShell).

### `-CollectNetTrace`

Especifica si el script recopila el seguimiento de red.

**Valores**:

- `0`: no se habilita el seguimiento de red.

- `1` (cualquier valor entero distinto de cero): se habilita el seguimiento de red y se recopilan los resultados.

**Tipo**: Int16

**Posición**: 3

**Valor predeterminado**: `0` (no se habilita el seguimiento de red).

### `-CollectUTCTrace`

Especifica si el script recopila el seguimiento de la hora UTC de Windows y ejecuta el diagnóstico de conectividad.

**Valores**:

- `0`: no se habilita el seguimiento UTC ni se ejecuta el diagnóstico de conectividad.

- `1` (cualquier valor entero distinto de cero): se habilita el seguimiento UTC, se ejecuta el diagnóstico de conectividad y se recopilan los resultados.

**Tipo**: Int16

**Posición**: 4

**Valor predeterminado**: `0` (no se habilita el seguimiento de UTC ni se ejecuta el diagnóstico de conectividad).


## <a name="output"></a>Salida

El script crea una *carpeta de trabajo* en la ruta de acceso especificada. Por ejemplo, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Coloca todos los archivos de salida en esta carpeta de trabajo.

Si permite que el script escriba en un *archivo de registro*, se genera uno en la carpeta de trabajo. Por ejemplo, **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss.txt**.

El script también genera otros *archivos de diagnóstico* en la carpeta de trabajo. Por ejemplo:

- `installedKBs.txt`: una lista de las actualizaciones de Windows instaladas en el dispositivo.
- `appcompat`: datos de compatibilidad de las aplicaciones.
- `Reg*.txt`: una serie de archivos con datos exportados del Registro de Windows.


## <a name="examples"></a>Ejemplos

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a> Ejemplo 1: Ejecución de un script a través de la ventana de comandos de PowerShell con valores predeterminados

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a> Ejemplo 2: Ejecución de un script a través de la ventana de comandos de PowerShell con parámetros especificados

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a> Ejemplo 3: Ejecución de un script a través de la ventana de comandos de PowerShell con parámetros especificados en posición

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a> Ejemplo 4: Ejecución de un script a través de la ventana de comandos de PowerShell con parámetros especificados y mensajes detallados

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a> Ejemplo 5: Implementación de un script a través de **Scripts** de Configuration Manager

Para obtener más información, consulte [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](../apps/deploy-use/create-deploy-scripts.md).

DesktopAnalyticsLogsCollector.ps1 está firmado digitalmente por Microsoft. Puede que tenga que agregar su certificado de firma de código de Microsoft como un editor de confianza en el dispositivo de destino.

1. Abra las propiedades del script en el Explorador de Windows. Cambie a la pestaña **Firmas digitales** y seleccione **Detalles**.

2. En la pestaña **General**, seleccione **Ver certificado**.

    > [!Note]
    > Para distribuir el certificado a través de otros mecanismos, primero expórtelo a un archivo. Vaya a la pestaña **Detalles** y seleccione **Copiar a archivo**.

3. Seleccione **Instalar certificado**. Importe el certificado y colóquelo en el almacén **Editores de confianza**.


## <a name="see-also"></a>Vea también

- [Solución de problemas de Análisis de escritorio](troubleshooting.md)

- [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](../apps/deploy-use/create-deploy-scripts.md)
