---
title: Uso de medios independientes para implementar Windows
titleSuffix: Configuration Manager
description: Use medios independientes de Configuration Manager para implementar Windows en aquellos casos en los que el ancho de banda sea limitado o como una opción para actualizar o instalar equipos.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124659"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>Uso de medios independientes para implementar Windows sin usar la red

*Se aplica a: Configuration Manager (rama actual)*

Los medios independientes de Configuration Manager contienen todo lo necesario para implementar un sistema operativo en un equipo. Los medios incluyen la imagen de arranque, la imagen del sistema operativo, la directiva de secuencia de tareas, las aplicaciones, los controladores, etc. Las implementaciones de medios independientes le permiten implementar sistemas operativos en las condiciones siguientes:

- En entornos donde no resulta práctico copiar una imagen del sistema operativo u otros paquetes grandes a través de la red.

- En entornos sin conectividad de red o conectividad de red de bajo ancho de banda.

Use medios independientes en los siguientes escenarios de implementación del sistema operativo:

- [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)

- [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)

Realice los pasos de uno de estos escenarios de implementación del sistema operativo. A continuación, use las secciones siguientes para preparar y crear los medios independientes.

## <a name="unsupported-task-sequence-actions"></a>Acciones de secuencia de tareas no admitidas

Cuando se usan medios independientes, Configuration Manager no admite las siguientes acciones en la secuencia de tareas:

- El paso [Aplicar controladores automáticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers). No se admite la aplicación automática de controladores de dispositivos del catálogo de controladores. Para que un determinado conjunto de controladores esté disponible para la instalación de Windows, use el paso [Apply Driver Package](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) (Aplicar paquete de controladores).

- Instalación de actualizaciones de software.

- Instalación de software antes de implementar el sistema operativo.

- Asociación de usuarios con el equipo de destino para permitir la afinidad entre usuario y dispositivo.

- El paquete dinámico se instala con el paso [Instalar paquete](../understand/task-sequence-steps.md#BKMK_InstallPackage).

- La aplicación dinámica se instala con el paso [Instalar aplicación](../understand/task-sequence-steps.md#BKMK_InstallApplication).

> [!NOTE]
> Si la secuencia de tareas para implementar un sistema operativo incluye el paso **Instalar paquete** y crea los medios independientes en un sitio de administración central (CAS), podría producirse un error. Los CAS no tienen las directivas de configuración de cliente necesarias para habilitar el agente de distribución de software cuando se ejecuta la secuencia de tareas. Es probable que aparezca el siguiente error en el archivo **CreateTsMedia.log**:
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> En el caso de medios independientes que incluyan un paso **Instalar paquete**, debe crearlos en un sitio primario que tenga habilitado el agente de distribución de software.
>
> Como alternativa, edite la secuencia de tareas para agregar un paso [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) (Ejecutar línea de comandos) después del paso [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) (Instalar Windows y Configuration Manager). El paso **Run Command Line** (Ejecutar línea de comandos) ejecuta el siguiente comando de WMI para habilitar el agente de distribución de software antes de que se ejecute el primer paso **Instalar paquete**:
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>Configurar la implementación

Cuando use medios independientes para iniciar el proceso de implementación del sistema operativo, configure la implementación para que el sistema operativo esté disponible para los medios. En la página **Deployment Settings** (Configuración de implementación) de la implementación, en la opción **Make available to the following** (Estar disponible para), seleccione una de las siguientes opciones:

- Clientes de Configuration Manager, medios y PXE

- Solo medios y PXE

- Sólo medios y PXE (ocultos)

## <a name="create-the-standalone-media"></a>Creación de medios independientes

Puede especificar si el medio independiente es una unidad flash USB o un conjunto de CD o DVD. El equipo que iniciará el medio debe admitir la opción que elija como unidad de arranque. Para más información, consulte [Crear medios independientes](create-stand-alone-media.md).

## <a name="install-the-os-from-standalone-media"></a>Instalación del sistema operativo desde un medio independiente

Para instalar el sistema operativo, inserte el medio independiente en el equipo y, luego, encienda este.

## <a name="next-steps"></a>Pasos siguientes

[Experiencias de usuario para la implementación de sistemas operativos](../understand/user-experience.md#task-sequence-wizard)
