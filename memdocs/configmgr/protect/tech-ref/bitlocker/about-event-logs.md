---
title: Registros de eventos de BitLocker
titleSuffix: Configuration Manager
description: Aprenda a trabajar con la información de BitLocker en el registro de eventos de Windows para solucionar problemas.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4875e7875321294d815bfcd8a25a805d3e085aab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706033"
---
# <a name="bitlocker-event-logs"></a>Registros de eventos de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

El agente de administración y los servicios web de BitLocker usan registros de eventos de Windows para registrar los mensajes. En el Visor de eventos, vaya a **Registros de aplicaciones y servicios**, **Microsoft**, **Windows**. El canal de registro (nodo) varía en función del equipo y del componente:

- **MBAM**: agente de administración de BitLocker en un equipo cliente
- **MBAM-Web**:
  - Servicio de recuperación en el punto de administración
  - Portal de autoservicio
  - Sitio web de administración y supervisión

Para obtener más información sobre mensajes específicos de estos registros, vea los artículos siguientes:

- [Registros de eventos de cliente](client-event-logs.md)
- [Registros de eventos de servidor](server-event-logs.md)

De forma predeterminada, en cada nodo verá dos canales de registro: **Administración** y **Operativo**. Para obtener información más detallada sobre la solución de problemas, también puede mostrar los [registros analíticos y de depuración](#bkmk_debug).

## <a name="log-properties"></a>Propiedades del registro

En Visor de eventos de Windows, seleccione un registro específico. Por ejemplo, **Administración**. Vaya al menú **Acción** y seleccione **Propiedades**. Configure las siguientes opciones:

- **Tamaño máximo de registro (KB)** : de forma predeterminada, este valor es `1028` (1 MB) para todos los registros.
- **Cuando alcance el tamaño máx. del reg. de eventos**: de forma predeterminada, los registros de tipo **Administración** y **Operativo** están establecidos en **Sobrescribir eventos si es necesario (los anteriores primero)** .

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a> Registros analíticos y de depuración

Puede habilitar registros más detallados para la solución de problemas. En el Visor de eventos, vaya al menú **Vista** y seleccione **Mostrar registros analíticos y de depuración**. Ahora, cuando vaya al canal de registro, verá otros dos registros: **analíticos** y **de depuración**.

> [!TIP]
> De forma predeterminada, estos registros tienen las propiedades siguientes:
>
> - **Tamaño máximo de registro (KB)** : `1028` (1 MB)
> - **No sobrescribir eventos (borrado manual del registro)**

## <a name="export-logs-to-text"></a>Exportación de los registros a texto

Especialmente en el caso de los [registros analíticos y de depuración](#bkmk_debug), puede que le resulte más fácil revisar las entradas de los registros en un solo archivo de texto. Use los siguientes comandos de PowerShell para exportar las entradas del registro de eventos a archivos de texto:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
