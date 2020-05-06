---
title: Referencia técnica de instalación de aplicaciones
titleSuffix: Configuration Manager
description: Referencia técnica para la solución de problemas de instalaciones de aplicaciones para Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688823"
---
# <a name="application-installation"></a>Instalación de la aplicación

*Se aplica a: Configuration Manager (rama actual)*

Antes de continuar, revise [Componentes de cliente de implementación de aplicaciones](client-components-technical-reference.md) para comprender el procesamiento de trabajos de agente de CI y DCM.

La instalación de la aplicación la realizan los componentes Agente de DCM y Agente de CI cuando se aplica la implementación. El tiempo de aplicación es distinto para las implementaciones disponibles y requeridas. Para saber cuándo se aplica la asignación, vea los artículos [Implementación de aplicaciones en colecciones de dispositivos](device-deployment-technical-reference.md) o [Implementación de aplicaciones en colecciones de usuarios](user-deployment-technical-reference.md).

## <a name="enforcement-initiation"></a>Inicio del cumplimiento

La instalación de la aplicación se inicia mediante el componente Agente de CI en el cliente durante la fase **StateEnforcingCIs**. Este proceso es el mismo, con independencia de que la aplicación se implemente en una colección de dispositivos o de usuarios.

- En el caso de las implementaciones **disponibles**, la aplicación se instala cuando el usuario inicia su instalación desde el Centro de software.
- En el caso de las implementaciones **requeridas**, la aplicación se instala en la fecha límite de la implementación. Pero el usuario puede iniciar la instalación desde el Centro de software antes de la fecha límite.

Cuando el agente de CI inicia la instalación de la aplicación, crea una tarea que controla el componente Administrador de tareas de CI. Después, el Administrador de tareas de CI inicia la instalación. Se puede realizar el seguimiento de esta actividad en **CITaskMgr.log** mediante el identificador único del tipo de implementación.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Cumplimiento de aplicaciones

Una vez que se ha iniciado la aplicación, el cliente vuelve a realizar la detección para asegurarse de que la aplicación no está ya instalada. Una vez que se determina que la aplicación no está instalada, se inicia su instalación. Se puede realizar el seguimiento de esta actividad en **AppEnforce.log** en el cliente mediante el identificador único del tipo de implementación.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Comprobación de la instalación

Una vez que se ha instalado la aplicación, se vuelve a usar el método de detección de aplicaciones para asegurarse de que la aplicación se haya detectado como instalada.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Por último, una vez completada la aplicación, el agente de CI recibe la notificación de tarea completada y el trabajo del agente de CI pasa a la fase siguiente.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Pasos siguientes

[Solución de problemas de implementación de aplicaciones](../deploy-use/troubleshoot-application-deployment.md)
