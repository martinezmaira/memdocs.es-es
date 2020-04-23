---
title: Centro de soporte técnico OneTrace (versión preliminar)
titleSuffix: Configuration Manager
description: OneTrace es un nuevo visor de registros del Centro de soporte técnico que tiene mejoras relativas a CMTrace.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707453"
---
# <a name="support-center-onetrace-preview"></a>Centro de soporte técnico OneTrace (versión preliminar)

<!--3555962-->

A partir de la versión 1906, OneTrace es un nuevo visor de registros del Centro de soporte técnico. Funciona de forma similar a CMTrace, con las mejoras siguientes:

- Una vista con pestañas.
- Ventanas acoplables.
- Funciones de búsqueda mejoradas.
- Capacidad de habilitar filtros sin salir de la vista del registro.
- Sugerencias de la barra de desplazamiento para identificar rápidamente clústeres de errores.
- Apertura de registro rápida para archivos de gran tamaño

[![Captura de pantalla del visor de registros OneTrace](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace funciona con muchos tipos de archivos de registro, como los siguientes:

- Registros de cliente de Configuration Manager.
- Registros de servidor de Configuration Manager.
- Mensajes de estado
- Archivo de registro ETW de Windows Update en Windows 10.
- Archivo de registro de Windows Update en Windows 7 y Windows 8.1.

## <a name="prerequisites"></a>Requisitos previos

- .NET Framework, versión 4.6 o posteriores

## <a name="install"></a>Instalar

OneTrace se instala con el Centro de soporte técnico. Busque el instalador del Centro de soporte técnico en la siguiente ruta de acceso del servidor de sitio: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

De forma predeterminada, la aplicación OneTrace se instala en `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`.

> [!Note]  
> El Centro de soporte técnico y OneTrace usan Windows Presentation Foundation (WPF). Este componente no está disponible en Windows PE. Siga usando CMTrace en las imágenes de arranque con implementaciones de secuencia de tareas.  

## <a name="log-groups"></a>Grupos de registros

<!--5559993-->

A partir de la versión 2002, OneTrace admite grupos de registros personalizables, similar a la característica del centro de soporte técnico. Los grupos de registros permiten abrir todos los archivos de registro de un único escenario. Actualmente, OneTrace incluye grupos para los siguientes escenarios:

- Administración de aplicaciones
- Configuración de cumplimiento (también llamada Administración de configuración deseada)
- Actualizaciones de software

Para mostrar los grupos de registros, vaya al menú **Ver** y seleccione **Grupos de registros**.

![Captura de pantalla del grupo de registros OneTrace para la administración de aplicaciones](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Personalización de los grupos de registros

Para personalizar estos grupos, modifique el XML de configuración, que de forma predeterminada se encuentra en la siguiente ruta: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`.

El ejemplo siguiente es una parte del archivo de configuración predeterminado:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

La propiedad `GroupType` acepta los valores siguientes:

- `0`: desconocido u otro
- `1`: Registros de cliente de Configuration Manager.
- `2`: Registros de servidor de Configuration Manager.

La propiedad `GroupFilePath` puede incluir una ruta explícita para los archivos de registro. Si está en blanco, OneTrace se basa en la configuración del registro del tipo de grupo. Por ejemplo, si establece `GroupType=1`, OneTrace buscará automáticamente en `C:\Windows\CCM\Logs` los registros del grupo. En este ejemplo, no es necesario especificar `GroupFilePath`.

## <a name="see-also"></a>Vea también

- [Visor de registros del Centro de soporte técnico](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
