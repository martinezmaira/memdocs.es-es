---
title: Referencia técnica de los componentes cliente de implementación de aplicaciones
titleSuffix: Configuration Manager
description: Componentes cliente usados para la solución de problemas de implementación de aplicaciones en Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688853"
---
# <a name="understanding-application-deployment-client-components"></a>Descripción de los componentes cliente de implementación de aplicaciones

*Se aplica a: Configuration Manager (rama actual)*

Las operaciones de evaluación y cumplimiento de la implementación de aplicaciones se controlan mediante los componentes del agente de DCM y del agente de CI en el cliente. En este artículo se explica cómo funciona un trabajo típico del agente de DCM y del agente de CI.

## <a name="dcm-agent"></a>Agente de DCM

El agente de DCM es el componente cliente de nivel superior responsable de la evaluación de los elementos de configuración, lo que incluye las aplicaciones. Cuando se activa o se aplica una implementación, se crea un trabajo del agente de DCM que lee la directiva de asignación y determina las acciones que se deben realizar. Se puede hacer un seguimiento de esta actividad en el registro **DCMAgent.log** en el cliente mediante el identificador del trabajo del agente de DCM, el cual puede localizar si busca el identificador único de la aplicación.

### <a name="device-deployments"></a>Implementaciones de dispositivos

- En el caso de las implementaciones **requeridas**, DCMAgent.log muestra las acciones aplicables. Estas acciones pueden variar en función de si ya ha pasado la fecha límite de la implementación.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- En el caso de las implementaciones **disponibles**, DCMAgent.log muestra que la implementación no es obligatoria (`is not mandatory`). Para estas implementaciones, se lleva a cabo la evaluación de la aplicación, pero el cumplimiento se omite a menos que el usuario haya iniciado la instalación.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Implementaciones de usuarios

- En el caso de las implementaciones **requeridas**, DCMAgent.log muestra las acciones aplicables. Estas acciones pueden variar en función de si ya ha pasado la fecha límite de la implementación.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- En el caso de las implementaciones **disponibles**, se crean trabajos del agente de DCM para su evaluación y cumplimiento cuando el usuario inicia la instalación de la aplicación.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>Agente de CI

El agente de CI es el componente cliente responsable de la evaluación y la corrección de los elementos de configuración. El agente de DCM lee la directiva de asignación y crea un trabajo para que el componente del agente de CI realice las acciones solicitadas. **DCMAgent.log** registra el identificador del trabajo del agente de CI, el cual resulta útil para realizar el seguimiento de la actividad del agente de CI en el registro **CIAgent.log** en el cliente.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Un trabajo de agente de CI típico pasa por varias fases, que se pueden identificar si se filtra el registro **CIAgent.log** por el id. del trabajo del agente de CI y, a continuación, se busca `TransitionState`. Algunas de las fases clave de un trabajo del agente de CI para la implementación de aplicaciones son:

- **DownloadingCIs**
  - Durante esta fase, se descargan los metadatos de la aplicación necesarios para evaluar la aplicación. Los metadatos incluyen el método de detección, las reglas de requisitos, las condiciones globales, etc. Se puede realizar un seguimiento de esta actividad en los registros **CIDownloader.log** y **DataTransferService.log**. En el caso de las implementaciones **disponibles**, este proceso se produce durante la primera evaluación de la aplicación. Sin embargo, en el caso de las implementaciones **requeridas**, este proceso se produce inmediatamente después de descargar la directiva.

- **InvokingSdmMethod**
  - Durante esta fase, se usa el método de detección de aplicaciones para comprobar que la aplicación está instalada y se determina el estado deseado. Se puede realizar un seguimiento de esta actividad en **AppDiscovery.log** y **AppIntentEval.log**. Para obtener más información acerca de esta fase, vea el artículo sobre la [evaluación de aplicaciones](deployment-evaluation-technical-reference.md).

- **StateDownloadingContents**
  - Durante esta fase, se descarga el contenido de la aplicación si es necesario. Se puede realizar un seguimiento de esta actividad en los registros **CAS.log**, **ContentTransferManager.log**, **LocationServices.log** y **DataTransferService.log**. Para obtener más información acerca de esta fase, consulte el artículo sobre la [descarga de aplicaciones](deployment-download-technical-reference.md).

- **StateEnforcingCIs**
  - Durante esta fase, se inicia la instalación de la aplicación. Se puede realizar el seguimiento de esta actividad en **AppEnforce.log**. Para obtener más información acerca de esta fase, vea el artículo [Instalación de aplicaciones](deployment-install-technical-reference.md).

- **StateEnforcementReporting**
  - Durante esta fase, se registra el estado de instalación de la aplicación para la informar al punto de administración. Se puede realizar el seguimiento de esta actividad en **StateMessage.log**.

Aunque el trabajo del agente de CI pasa por todas las fases, puede omitir una fase si no es necesaria. Por ejemplo, en el caso de las implementaciones **disponibles**, las fases StateDownloadingContents y StateEnforcingCIs se omiten hasta que el usuario intenta instalar la aplicación desde el Centro de software. Sin embargo, en el caso de las implementaciones **requeridas**, la fase StateDownloadingContents descarga el contenido de la aplicación (si es necesario) cuando se activa la asignación, pero la fase StateEnforcingCIs se omite si la fecha límite es futura. Este comportamiento se puede observar en el registro CIAgent.log si filtra por el identificador del trabajo del agente de CI y busca `Skipping policy`.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Pasos siguientes

- [Evaluación de la aplicación](deployment-evaluation-technical-reference.md)
- [Descarga de la aplicación](deployment-download-technical-reference.md)
- [Instalación de la aplicación](deployment-install-technical-reference.md)
