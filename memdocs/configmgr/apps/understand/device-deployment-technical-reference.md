---
title: Referencia técnica de implementación de aplicaciones en colecciones de dispositivos
titleSuffix: Configuration Manager
description: Referencia técnica para la solución de problemas de implementaciones de aplicaciones en colecciones de dispositivos para Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688793"
---
# <a name="application-deployment-for-device-collections"></a>Implementación de aplicaciones en colecciones de dispositivos

*Se aplica a: Configuration Manager (rama actual)*

Cuando una aplicación se implementa en una colección de dispositivos, la directiva se destina a todos los dispositivos de la colección, con independencia del propósito de implementación. En este artículo se explica la descarga de directivas y el procesamiento de la implementación en el cliente.

> [!TIP]
> Toda la información necesaria para revisar los registros de cliente se puede obtener mediante la ejecución de la consulta SQL a la que se hace referencia en la sección [Antes de empezar](app-deployment-technical-reference.md#before-you-begin).

## <a name="policy-download"></a>Descarga de la directiva

Después de que la directiva para la implementación de la aplicación se destine al cliente, este la descargará en el siguiente ciclo de sondeo de directivas. Cuando el cliente descarga la directiva, descarga las directivas relacionadas además de la de implementación. Estas directivas relacionadas incluyen la directiva de la aplicación, el tipo de implementación, las condiciones globales, etc. Se puede realizar el seguimiento de la actividad de descarga de directivas en **PolicyAgent.log** en el cliente, mediante el identificador único de la aplicación o de la asignación.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

Una vez descargadas las directivas en el cliente, el componente Scheduler crea programaciones para la activación y el cumplimiento de la implementación.

## <a name="deployment-activation"></a>Activación de la implementación

La evaluación de la aplicación se inicia al activar la implementación. El componente Scheduler crea una programación para activar la asignación en el tiempo disponible configurado en la implementación. Se puede realizar el seguimiento de esta actividad en **scheduler.log** desde el cliente mediante el id. único de asignación de la aplicación.

- En el caso de las implementaciones **requeridas**, se crea la programación de activación, pero tiene un retraso de hasta dos horas para evitar la contención de recursos en los servidores de sitio y los puntos de distribución. El retraso ayuda a evitar la contención, ya que el contenido de la aplicación puede descargarse durante la evaluación si la aplicación es aplicable en función de las reglas de requisitos definidas.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- En el caso de las implementaciones **disponibles**, la programación de activación se crea para que se desencadene en el tiempo disponible configurado en la implementación.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Cuando llega la hora programada, el componente Scheduler envía el mensaje de activación al agente de DCM para realizar la evaluación de la aplicación.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

El agente de DCM recibe el mensaje de activación y crea un trabajo para evaluar la aplicación.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Cumplimiento de la implementación

La instalación de la aplicación se inicia cuando se aplica la implementación.

- En el caso de las implementaciones **requeridas**, Scheduler crea una programación de fecha límite después de descargar la directiva para aplicar la aplicación en la fecha límite de implementación. De forma predeterminada, la programación de fecha límite no es aleatoria. El comportamiento de la selección aleatoria se puede controlar mediante la configuración de cliente [Deshabilitar selección aleatoria de fecha límite](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization).

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    En la fecha límite, el componente Scheduler envía el mensaje de fecha límite al agente de DCM. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    El agente de DCM recibe el mensaje de fecha límite y crea un trabajo para aplicar la aplicación.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > En el caso de las implementaciones con fecha límite en el pasado, la aplicación se activa y se aplica de forma inmediata mediante el mismo trabajo del agente de DCM que realiza las acciones de evaluación, descarga e instalación.

- En el caso de las implementaciones **disponibles**, no hay ninguna programación de fecha límite, ya que el cumplimiento se produce cuando el usuario inicia la instalación de la aplicación desde el Centro de software. Cuando el usuario inicia una instalación, se crea un trabajo del agente de DCM para realizar la evaluación, descarga e instalación de la aplicación. Se puede realizar el seguimiento de esta actividad en **DCMAgent.log** desde el cliente.

## <a name="next-steps"></a>Pasos siguientes

- [Descripción de los componentes de cliente de implementación de aplicaciones](client-components-technical-reference.md)
