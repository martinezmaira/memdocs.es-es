---
title: Referencia técnica de evaluación de aplicaciones
titleSuffix: Configuration Manager
description: Referencia técnica para la solución de problemas de evaluación de aplicaciones para Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688843"
---
# <a name="application-deployment-evaluation"></a>Evaluación de implementación de aplicaciones

*Se aplica a: Configuration Manager (rama actual)*

Antes de continuar, revise [Componentes de cliente de implementación de aplicaciones](client-components-technical-reference.md) para comprender el procesamiento de trabajos de agente de CI y DCM.

La evaluación de la aplicación la realizan los componentes Agente de DCM y Agente de CI cuando se ha activado la implementación. Para saber cuándo se activa la asignación, vea los artículos [Implementación de aplicaciones en colecciones de dispositivos](device-deployment-technical-reference.md) o [Implementación de aplicaciones en colecciones de usuarios](user-deployment-technical-reference.md).

## <a name="application-detection-and-evaluation"></a>Detección y evaluación de aplicaciones

La evaluación de la aplicación se realiza durante la fase **InvokingSdmMethod** de un trabajo del agente de CI. En esta fase, el cliente evalúa el método de detección definido para la aplicación a fin de determinar si está instalada en el dispositivo. Se puede realizar el seguimiento de esta actividad en **AppDiscovery.log** mediante el identificador único del tipo de implementación o el nombre del tipo de implementación.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> En el ejemplo anterior se muestra la detección de una aplicación MSI en la que, para realizar la detección, se comprueba si el código de producto MSI está instalado en el dispositivo. En el caso de las aplicaciones que usan métodos de detección alternativos, se usa el adecuado para comprobar si la aplicación está instalada.

Después, el cliente evalúa el estado deseado de la aplicación según el propósito de implementación. Este paso también implica detectar si la aplicación tiene dependencias o reglas de sustitución que se deban respetar. Se puede realizar el seguimiento de esta actividad en **AppIntentEval.log** mediante el identificador único de la aplicación y el tipo de implementación.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

En la entrada de registro anterior, **Estado actual** indica si la aplicación está instalada actualmente en el dispositivo. **Aplicabilidad** indica si la aplicación es aplicable en función de las reglas de requisitos definidas. **ResolvedState** indica el estado deseado de la aplicación según el propósito de implementación.

> [!TIP]
> Use [Deployment Monitoring Tool](../../core/support/deployment-monitoring-tool.md) para ver el estado de la aplicación, el estado de aplicabilidad y las infracciones de los requisitos.

## <a name="next-steps"></a>Pasos siguientes

- [Descarga de la aplicación](deployment-download-technical-reference.md)
