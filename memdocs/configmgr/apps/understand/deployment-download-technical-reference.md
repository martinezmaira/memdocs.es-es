---
title: Referencia técnica de descarga de aplicaciones
titleSuffix: Configuration Manager
description: Referencia técnica para la solución de problemas de descarga de aplicaciones para Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688863"
---
# <a name="application-download-in-configuration-manager"></a>Descarga de aplicaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de continuar, revise [Componentes cliente de implementación de aplicaciones](client-components-technical-reference.md) para comprender el procesamiento de trabajos de agente de CI y DCM.

## <a name="download-initiation"></a>Inicio de la descarga

La descarga del contenido de la aplicación se inicia mediante el componente del agente de CI en el cliente durante la fase **StateDownloadingContents**. Este proceso es el mismo, con independencia de que la aplicación se implemente en una colección de dispositivos o de usuarios.

- En el caso de las implementaciones **disponibles**, el contenido de la aplicación se descarga cuando el usuario inicia la instalación de la aplicación desde el Centro de software.
- En el caso de las implementaciones **requeridas**, el contenido de la aplicación se descarga cuando se activa la asignación y la evaluación encuentra que la aplicación es aplicable. Para saber cuándo se activa la asignación, vea los artículos [Implementación de aplicaciones en colecciones de dispositivos](device-deployment-technical-reference.md) o [Implementación de aplicaciones en colecciones de usuarios](user-deployment-technical-reference.md).

Cuando el agente de CI inicia la descarga del contenido, crea una tarea que controla el componente del administrador de tareas de CI. Después, el administrador de tareas de CI inicia la descarga del contenido. Se puede realizar el seguimiento de esta actividad en el registro **CITaskMgr.log** mediante el identificador único del tipo de implementación.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Ubicación del punto de distribución

Todas las tareas de descarga se controlan mediante el componente de acceso al contenido, que es responsable de administrar la caché del cliente. Después de crear la tarea de descarga, el componente de acceso al contenido comprueba si el contenido ya está disponible en la caché del cliente. Si el contenido no está disponible, crea una solicitud de ubicación para obtener una lista de puntos de distribución desde los que se puede obtener el contenido. Se puede realizar un seguimiento de esta actividad en los registros **CAS.log** y **LocationServices.log** en el cliente con el identificador único de contenido.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Aunque el componente de servicios de ubicación controla las solicitudes de ubicación, no solicita directamente ubicaciones al punto de administración. Todas las solicitudes al punto de administración suelen pasar por el componente de mensajería de CCM, que registra la información en el archivo **CcmMessaging.log**.

El archivo XML de respuesta de ubicación contiene la lista de puntos de distribución en función del grupo de límites del cliente. Esta lista se analiza y se almacena en WMI en el cliente según la [prioridad de origen de contenido](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority). Esta actividad se puede ver en el registro **ContentTransferManager.log** si se usa el identificador único de contenido y se busca `Persisted location`. 

Si el archivo XML de respuesta de ubicación no contiene ningún punto de distribución, **ContentTransferManager.log** muestra el mensaje `Received empty location update` y el cliente puede quedarse atascado en 0 % mientras se descarga la aplicación. Normalmente, esta respuesta puede producirse debido a problemas de configuración de los grupos de límites. Para obtener más información, vea [Errores de descarga](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## <a name="content-download"></a>Descarga de contenido

Una vez obtenidas las ubicaciones de los puntos de distribución, el componente de acceso al contenido crea un trabajo de transferencia de contenido. Se puede realizar un seguimiento de esta actividad en el registro **CAS.log** mediante el uso del identificador único de contenido.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

A continuación, el administrador de transferencia de contenido crea un trabajo de servicio de transferencia de datos para realizar la descarga del contenido. Se puede realizar el seguimiento de esta actividad en **ContentTransferManager.log** en el cliente mediante el identificador único de contenido.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Esta entrada de registro se puede usar para identificar los identificadores de trabajo de CTM y DTS, los cuales se pueden usar para realizar un seguimiento del progreso de la transferencia de contenido en los registros **ContentTransferManager.log** y **DataTransferService.log**, respectivamente.

El servicio de transferencia de datos lleva a cabo la descarga del contenido de la aplicación mediante la creación de un trabajo de Servicio de transferencia inteligente en segundo plano (BITS), y espera a que termine la descarga. Se puede realizar un seguimiento de esta actividad en **DataTransferService.log** en el cliente con el identificador de trabajo de DTS obtenido del registro **ContentTransferService.log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

Una vez completada la descarga, se notifica al componente de acceso al contenido. A continuación, el componente de acceso al contenido comprueba el contenido descargado para asegurarse de que no se ha modificado durante la descarga. Se puede realizar un seguimiento de esta actividad en el registro **CAS.log** mediante el uso del identificador único de contenido.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Por último, una vez comprobado el contenido, el agente de CI recibe la notificación de tarea completada y el trabajo del agente de CI pasa a la siguiente fase.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Pasos siguientes

- [Instalación de la aplicación](deployment-install-technical-reference.md)
