---
title: Solucionar problemas de acción de dispositivo
titleSuffix: Configuration Manager
description: Solución de problemas de acciones de dispositivo referencia técnica para Configuration Manager
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "82140280"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Solución de problemas de acciones de dispositivo para dispositivos Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

A partir de Configuration Manager 2002, Configuration Manager clientes se pueden sincronizar con el centro de administración de Microsoft Endpoint Manager. Algunas acciones de cliente se pueden ejecutar desde el centro de administración de Microsoft Endpoint Manager en los clientes sincronizados.

Las acciones disponibles son las siguientes:
- Sincronizar Directiva de equipo
- Sincronizar Directiva de usuario
- Ciclo de evaluación de la aplicación


[![Información general del dispositivo en el centro de administración de Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
Cuando un administrador ejecuta una acción desde el centro de administración de Microsoft Endpoint Manager, la solicitud de notificación se reenvía a Configuration Manager sitio y desde el sitio al cliente.

## <a name="configuration-manager-components"></a>Componentes de Configuration Manager

- **SMS_SERVICE_CONNECTOR**: usa el trabajador de notificación de puerta de enlace para procesar la notificación desde el centro de administración de Microsoft Endpoint Manager.
- **SMS_NOTIFICATION_SERVER**: obtiene la notificación y crea una notificación de cliente.
- **BgbAgent**: el cliente obtiene la tarea y ejecuta la acción solicitada.

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Cuando se inicia una acción desde el centro de administración de Endpoint Manager de Microsoft, **CMGatewayNotificationWorker. log** procesa la solicitud.  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Se recibe una notificación del centro de administración de Microsoft Endpoint Manager.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. Se validan las acciones de usuario y de dispositivo.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. La tarea remota se reenvía al SMS_NOTIFICATION_SERVER.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

Una vez que el mensaje se envía al SMS_NOTIFICATION_SERVER, se envía una tarea desde el punto de administración al cliente correspondiente. Verá lo siguiente en **BgbServer. log**, que se encuentra en el punto de administración:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

El último paso se produce en el cliente y puede verse en **CcmNotificationAgent. log**. Una vez recibida la tarea, solicitará al programador que realice la acción. Cuando se realice la acción, verá un mensaje de confirmación:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Problemas comunes

Si el administrador no tiene los permisos necesarios en Configuration Manager, verá una `Unauthorized` respuesta en **CMGatewayNotificationWorker. log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Asegúrese de que el usuario que ejecuta la acción desde el centro de administración de Microsoft Endpoint Manager tiene los permisos necesarios en Configuration Manager sitio. Para obtener más información, consulte [requisitos previos de Asociación de inquilinos del administrador de puntos](device-sync-actions.md#prerequisites)de conexión de Microsoft.

## <a name="next-steps"></a>Pasos siguientes

[Habilitar la administración conjunta](../comanage/overview.md) para obtener funcionalidades adicionales con tecnología de la nube, como el acceso condicional.
