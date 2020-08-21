---
title: Herramientas de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre las herramientas que ayudan a administrar la infraestructura de Configuration Manager y a solucionar problemas de ella.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cb2529dbbe923a5035f0b7586dab696cd6fc917e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699422"
---
# <a name="configuration-manager-tools"></a>Herramientas de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las herramientas de Configuration Manager incluyen [herramientas basadas en cliente](#client-tools) y [basadas en servidor](#server-tools). Use estas herramientas para prestar soporte y solucionar problemas en la infraestructura de Configuration Manager.

A partir de Configuration Manager versión 1806, estas herramientas están incluidas en la carpeta `CD.Latest\SMSSETUP\Tools` del servidor de sitio. No se necesita ninguna otra instalación.<!--1357145--> Use estas versiones de las herramientas con Configuration Manager versión 1806 y versiones posteriores.

Todos los sistemas operativos Windows que se indican como clientes compatibles en [Sistemas operativos compatibles con clientes y dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) se pueden usar con estas herramientas.

> [!Note]  
> El [kit de herramientas de System Center 2012 R2 Configuration Manager](https://www.microsoft.com/download/details.aspx?id=50012) sigue estando disponible en el Centro de descarga de Microsoft. En Configuration Manager versión 1806 y versiones posteriores, use las versiones de las herramientas de la carpeta CD.Latest del servidor de sitio. Antes, algunas herramientas se encontraban en el kit de herramientas, pero no se incluían en la versión 1806. Estas herramientas heredadas ya no se admiten.


## <a name="client-tools"></a>Herramientas de cliente

Estas herramientas están en la subcarpeta `ClientTools`:

- [CMTrace](cmtrace.md): sirve para ver, supervisar y analizar archivos de registro de Configuration Manager  

- [Cliente Spy](clispy.md): soluciona problemas relacionados con la distribución de software, el inventario y la medición

- [Deployment Monitoring Tool](deployment-monitoring-tool.md): permite solucionar los problemas de aplicaciones, actualizaciones e implementaciones de línea de base  

- [Policy Spy](policy-spy.md): vea asignaciones de directiva  

- [Power Viewer Tool](power-viewer-tool.md): permite ver el estado de la característica de administración de energía  

- [Send Schedule Tool](send-schedule-tool.md): desencadena programaciones y evaluaciones de líneas de base de configuración  

> [!Note]  
> La carpeta `ClientTools` también incluye el archivo Microsoft.Diagnostics.Tracing.EventSource.dll. Varias herramientas de cliente necesitan esta biblioteca. No se puede usar directamente.  


## <a name="server-tools"></a>Herramientas de servidor

Estas herramientas están en la subcarpeta `ServerTools`:

- [DP Job Queue Manager](dp-job-manager.md): soluciona los problemas de los trabajos de distribución de contenido a los puntos de distribución  

- [Collection Evaluation Viewer](ceviewer.md): vea detalles de la evaluación de colecciones  

- [Content Library Explorer](content-library-explorer.md): permite ver el contenido del almacén de instancia única de la biblioteca de contenido  

- [Content Library Transfer](content-library-transfer.md): transfiere la biblioteca de contenido entre unidades  

- [Content Ownership Tool](content-ownership-tool.md): cambia la propiedad de los paquetes huérfanos. Estos paquetes existen en el sitio sin un servidor de sitio propietario.

- [Role-based Administration and Auditing Tool](rbaviewer.md): ayuda a los administradores a auditar la configuración de roles  

- [Run Meter Summarization Tool](run-meter-summ.md): Ejecuta la tarea de resumen de medición y analiza los datos de medición

> [!Note]  
> La carpeta ServerTools también incluye los siguientes archivos:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Varias herramientas de servidor necesitan estas bibliotecas. No se pueden usar directamente.  

## <a name="other-tools-and-toolkits"></a>Otras herramientas y kits de herramientas

- [Centro de soporte técnico](support-center.md): Recopile información de los clientes para facilitar el análisis para solucionar el problema.

    A partir de la versión 1906, **OneTrace** es un nuevo visor de registros del Centro de soporte técnico. Funciona de manera similar a CMTrace, pero con mejoras. Para obtener más información, consulte [Centro de soporte técnico OneTrace](support-center-onetrace.md).

- [Extensión y migración de un sitio local a Microsoft Azure](azure-migration-tool.md): sirve para crear máquinas virtuales (VM) de Azure para Configuration Manager mediante programación. <!--3556022--> 

- [Content library cleanup tool](../plan-design/hierarchy/content-library-cleanup-tool.md): use **ContentLibraryCleanup.exe** en `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para quitar contenido huérfano de un punto de distribución.  

- [Hierarchy Maintenance Tool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): use **Preinst.exe** en la carpeta compartida `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` del servidor de sitio para pasar comandos al componente Administrador de jerarquía.  

- [Update reset tool](../servers/manage/update-reset-tool.md): use **CMUpdateReset.exe** en `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` para solucionar los problemas de descarga o replicación de las actualizaciones en la consola.  

- [Service Connection Tool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): use **ServiceConnectionTool.exe** en `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` para mantener actualizado el sitio cuando el punto de conexión de servicio está sin conexión.   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): Una colección de herramientas, procesos y guías para automatizar las implementaciones de SO de escritorio y servidor.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): Una herramienta independiente para administrar e importar las actualizaciones de software personalizadas.

- [Administrador de conversión de paquetes](../../apps/pcm/package-conversion-manager.md): Convierta paquetes heredados en aplicaciones.