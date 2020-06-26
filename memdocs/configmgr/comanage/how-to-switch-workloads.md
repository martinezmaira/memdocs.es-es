---
title: Cambio de las cargas de trabajo de administración conjunta
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo cambiar las cargas de trabajo que administra actualmente Configuration Manager a Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: how-to
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 88c8b34437ba52e700ef97885aafed40734a0f32
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776963"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Cambio de las cargas de trabajo de Configuration Manager a Intune

Una de las ventajas de la administración conjunta es cambiar las cargas de trabajo de Configuration Manager a Microsoft Intune. Cuando un dispositivo Windows 10 tiene el cliente de Configuration Manager y está inscrito en Intune, el usuario recibe las ventajas de ambos servicios. El usuario controla para qué cargas de trabajo, si corresponde, cambia la entidad desde Configuration Manager a Intune. Configuration Manager sigue administrando todas las demás cargas de trabajo, incluidas las que no cambia a Intune, y todas las demás características de Configuration Manager que no admite la administración conjunta.

Si cambia una carga de trabajo a Intune, pero después cambia de opinión, puede volver a cambiarla a Configuration Manager.

Para más información sobre las cargas de trabajo admitidas, consulte [Cargas de trabajo](workloads.md).

## <a name="switch-workloads-starting-in-version-1906"></a>Modificación de las cargas de trabajo a partir de la versión 1906
<!--3555750 FKA 1357954 -->
A partir de la versión 1906, puede configurar distintas colecciones piloto para cada una de las cargas de trabajo de administración conjunta. La posibilidad de usar diferentes colecciones piloto permite adoptar un enfoque más específico al cambiar las cargas de trabajo. Puede cambiar las cargas de trabajo cuando habilita la administración conjunta o puede hacerlo posteriormente cuando esté preparado. Si todavía no habilita la administración conjunta, primero debe hacer eso. Para más información, consulte [cómo habilitar la administración conjunta](how-to-enable.md). Después de habilitar la administración conjunta, modifique la configuración en las propiedades de administración conjunta.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**.  
2. Seleccione el objeto de administración conjunta y, después, elija **Propiedades** en la cinta.  
3. Cambie a la pestaña **Cargas de trabajo**. De manera predeterminada, todas las cargas de trabajo se establecen en la configuración **Configuration Manager**. Para cambiar una carga de trabajo, mueva el control deslizante de esa carga de trabajo a la configuración deseada.  

    ![Captura de pantalla de la pestaña Cargas de trabajo en la página de propiedades de administración conjunta](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**: Configuration Manager sigue administrando esta carga de trabajo.  

    - **Intune piloto**: cambie esta carga de trabajo solo en los dispositivos de la recopilación piloto. Puede cambiar las **recopilaciones piloto** en la pestaña **Almacenamiento provisional** de la página de propiedades de administración conjunta.  

    - **Intune**: cambie esta carga de trabajo para todos los dispositivos de Windows 10 inscritos en la administración conjunta.  

4. Vaya a la pestaña **Almacenamiento provisional** y cambie la **recopilación piloto** de todas las cargas que sea necesario.
  
   ![Captura de pantalla de la pestaña Cargas de trabajo en la página de propiedades de administración conjunta](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Antes de cambiar las cargas de trabajo, asegúrese de que la carga de trabajo correspondiente en Intune se configuró e implementó correctamente. Asegúrese de que las cargas de trabajo siempre se administren mediante una de las herramientas de administración para los dispositivos.
> - A partir de la versión 1806 de Configuration Manager, cuando se cambia una carga de trabajo de administración compartida, los dispositivos administrados conjuntamente sincronizan automáticamente la directiva MDM de Microsoft Intune. Esta sincronización también se produce al iniciar la acción **Descargar directiva de equipo** desde Notificaciones de cliente en la consola de Configuration Manager. Para obtener más información, vea [Iniciar la recuperación de directivas de cliente mediante la notificación de cliente](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Modificación de las cargas de trabajo en la versión 1902 y versiones anteriores

Puede cambiar las cargas de trabajo cuando habilita la administración conjunta o puede hacerlo posteriormente cuando esté preparado. Si todavía no habilita la administración conjunta, primero debe hacer eso. Para más información, consulte [cómo habilitar la administración conjunta](how-to-enable.md). Después de habilitar la administración conjunta, modifique la configuración en las propiedades de administración conjunta.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**.  

2. Seleccione el objeto de administración conjunta y, después, elija **Propiedades** en la cinta.
   - Se le pedirá que inicie sesión en Azure AD. El aviso no le impide actualizar la incorporación. Sin embargo, se le pedirá cada vez que abra la página **Propiedades** hasta que inicie sesión.

3. Cambie a la pestaña **Cargas de trabajo**. De manera predeterminada, todas las cargas de trabajo se establecen en la configuración **Configuration Manager**. Para cambiar una carga de trabajo, mueva el control deslizante de esa carga de trabajo a la configuración deseada.  

    ![Captura de pantalla de la pestaña Cargas de trabajo en la página de propiedades de administración conjunta](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager sigue administrando esta carga de trabajo.  

    - **Intune piloto**: cambie esta carga de trabajo solo en los dispositivos de la recopilación piloto. Puede cambiar la **recopilación piloto** en la pestaña **Almacenamiento provisional** de la página de propiedades de administración conjunta.  

    - **Intune**: cambie esta carga de trabajo para todos los dispositivos de Windows 10 inscritos en la administración conjunta.  

4. En la pestaña **Almacenamiento provisional** de la página de propiedades de la administración conjunta, cambie la **recopilación piloto** de las cargas de trabajo en caso de ser necesario.

5. Haga clic en **Aceptar** para guardar los cambios y salir de las propiedades de administración conjunta.

> [!Important]  
> - Antes de cambiar las cargas de trabajo, asegúrese de que la carga de trabajo correspondiente en Intune se configuró e implementó correctamente. Asegúrese de que las cargas de trabajo siempre se administren mediante una de las herramientas de administración para los dispositivos. 
> - A partir de la versión 1806 de Configuration Manager, cuando se cambia una carga de trabajo de administración compartida, los dispositivos administrados conjuntamente sincronizan automáticamente la directiva MDM de Microsoft Intune. Esta sincronización también se produce al iniciar la acción **Descargar directiva de equipo** desde Notificaciones de cliente en la consola de Configuration Manager. Para obtener más información, vea [Iniciar la recuperación de directivas de cliente mediante la notificación de cliente](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="next-steps"></a>Pasos siguientes

[Supervisión de la administración conjunta](how-to-monitor.md)
