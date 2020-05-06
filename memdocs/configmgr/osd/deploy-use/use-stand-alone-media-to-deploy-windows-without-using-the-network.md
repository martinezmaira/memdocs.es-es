---
title: Uso de medios independientes para implementar Windows
titleSuffix: Configuration Manager
description: Use medios independientes en Configuration Manager para implementar Windows en aquellos casos en los que el ancho de banda sea limitado o como una opción para actualizar o instalar equipos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709043"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>Usar medios independientes para implementar Windows sin usar la red

*Se aplica a: Configuration Manager (rama actual)*

Los medios independientes de Configuration Manager contienen todo lo necesario para implementar un sistema operativo en un equipo. Esto incluye la imagen de arranque, la imagen de sistema operativo y la secuencia de tareas para instalar el sistema operativo, incluidas las aplicaciones, los controladores, etcétera. las implementaciones de medios independientes le permiten implementar sistemas operativos en las condiciones siguientes:  

-   En entornos donde no resulta práctico copiar una imagen de sistema operativo u otros paquetes grandes a través de la red.  

-   En entornos sin conectividad de red o conectividad de red de bajo ancho de banda.  

Puede usar medios independientes en los siguientes escenarios de implementación de sistema operativo:  

- [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

- [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md)  

  Complete los pasos de uno de los escenarios de implementación de sistema operativo y luego use las secciones siguientes para prepararse y crear los medios independientes.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Acciones de la secuencia de tareas no admitidas si se usan medios independientes  
 Si completó los pasos de uno de los escenarios admitidos de implementación de sistema operativo, la secuencia de tareas para implementar (o actualizar) el sistema operativo se ha creado y todo el contenido asociado se ha distribuido a un punto de distribución. Cuando se usan medios independientes, no se admiten las siguientes acciones en la secuencia de tareas:  

-   El paso Aplicar controladores automáticamente en la secuencia de tareas. No se admite la aplicación automática de controladores de dispositivos desde el catálogo de controladores, pero puede elegir el paso Aplicar paquete de controladores para que haya un conjunto especificado de controladores disponible para el Programa de instalación de Windows.  

-   Instalación de actualizaciones de software.  

-   Instalación de software antes de implementar un sistema operativo.  

-   Asociación de usuarios con el equipo de destino para admitir la afinidad de dispositivo de usuario.  

-   El paquete dinámico se instala a través de la tarea Instalar paquete.  

-   La aplicación dinámica se instala a través de la tarea Instalar aplicación.  

> [!NOTE]  
>  Si la secuencia de tareas para implementar un sistema operativo incluye el paso [Instalar paquete](../understand/task-sequence-steps.md#BKMK_InstallPackage) y usted crea los medios independientes en un sitio de administración central, podría producirse un error. El sitio de administración central no tiene las directivas de configuración de cliente necesarias para habilitar el agente de distribución de software durante la ejecución de la secuencia de tareas. Es probable que aparezca el siguiente error en el archivo CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  En medios independientes que incluyen un paso **Instalar paquete**, debe crear los medios independientes en un sitio primario que tenga el agente de distribución de software habilitado o agregar un paso [Ejecutar línea de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) después del paso [Instalar Windows y Configuration Manager](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) y antes del primer paso **Instalar paquete** de la secuencia de tareas. El paso **Ejecutar línea de comandos** ejecuta un comando de WMIC para habilitar el agente de distribución de software antes de que se ejecuta el primer paso Instalar paquete. Puede utilizar lo siguiente en su paso de secuencia de tareas **Ejecutar línea de comandos** :  
>   
>  **Línea de comandos**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Configurar la implementación  
 Cuando use medios independientes para iniciar el proceso de implementación del sistema operativo, debe configurar la implementación para que el sistema operativo esté disponible para los medios. Puede configurar esto en la página **Configuración de implementación** del Asistente para implementar Software o en la pestaña **Configuración de implementación** en las propiedades de la implementación.  Para la opción de configuración **Estar disponible para** , configure uno de los siguientes:  

-   **Clientes de Configuration Manager, medios y PXE**  

-   **Solo medios y PXE**  

-   **Sólo medios y PXE (ocultos)**  

## <a name="create-the-stand-alone-media"></a>Crear medios independientes  
 Puede especificar si el medio independiente es una unidad flash USB o un conjunto de CD o DVD. El equipo que iniciará el medio debe admitir la opción que elija como unidad de arranque. Para obtener más información, consulte [Create stand-alone media](create-stand-alone-media.md) (Crear medios independientes).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Instalar el sistema operativo desde medios independientes  
 Inserte el medio independiente en una unidad de arranque del equipo y luego vuelva a encenderlo para instalar el sistema operativo.  
