---
title: Send Schedule Tool
titleSuffix: Configuration Manager
description: Utilice Send Schedule Tool para activar una programación en un cliente de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707473"
---
# <a name="send-schedule-tool"></a>Send Schedule Tool

*Se aplica a: Configuration Manager (rama actual)*

Send Schedule Tool es una de las [herramientas de Configuration Manager](tools.md). Úsela para activar una programación en un cliente o desencadenar la evaluación de una línea de base de configuración especificada. Funciona con el equipo local o estableciendo un cliente remoto como destino.  

Por ejemplo, use la herramienta para desencadenar una evaluación de cumplimiento o de programación de inventario. Si un número de clientes de Configuration Manager no ha informado recientemente de su estado de inventario o de cumplimiento, ejecute la herramienta para iniciar la programación necesaria en cada cliente.



## <a name="usage"></a>Uso

Ejecute **SendSchedule.exe** como administrador. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Cuando desencadene un mensaje (GUID), vea **SMSClientMethodProvider.log**. Para obtener más información sobre los GUID de mensajes disponibles, vea [Message IDs](#bkmk_sendschedule-guids).

Cuando desencadene la evaluación de una línea de base de configuración (DCM UID), vea **DCMAgent.log**.



## <a name="command-line-options"></a>Opciones de línea de comandos


### <a name="option-l"></a>Opción: `/L` 
Lista de todos los GUID de mensaje o UID de DCM disponibles para el envío. Muestre el nombre descriptivo de los mensajes en la tabla de datos para cada uno de ellos. Si falta el nombre del equipo, use el equipo local. Si especifica un mensaje sin un nombre de equipo, se envía a la máquina local. 



## <a name="examples"></a>Ejemplos

#### <a name="list-the-available-messages-on-the-local-machine"></a>Lista de los mensajes disponibles en el equipo local 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Lista de los mensajes disponibles en el cliente MyPC: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Desencadenar el inventario de hardware en el equipo local
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Desencadene inventario de hardware en MyPC: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Desencadene la evaluación de una línea de base de configuración específica en MyPC: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a> Identificadores de mensaje

|Message ID  |Nombre para mostrar  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Inventario de hardware|
|{00000000-0000-0000-0000-000000000002}|Inventario de software|
|{00000000-0000-0000-0000-000000000003}|Inventario de detección|
|{00000000-0000-0000-0000-000000000010}|Colección de archivos|
|{00000000-0000-0000-0000-000000000011}|Colección de IDMIF|
|{00000000-0000-0000-0000-000000000021}|Asignaciones de máquinas de solicitud|
|{00000000-0000-0000-0000-000000000022}|Evaluar las directivas de equipo|
|{00000000-0000-0000-0000-000000000023}|Actualizar la tarea de módulo de administración predeterminada|
|{00000000-0000-0000-0000-000000000024}|Tarea de ubicaciones de actualización de servicio de ubicación (LS)|
|{00000000-0000-0000-0000-000000000025}|Tarea de actualización de tiempo de espera de LS|
|{00000000-0000-0000-0000-000000000026}|Asignación de solicitud de directiva del agente (Usuario)|
|{00000000-0000-0000-0000-000000000027}|Asignación de evaluación de directiva del agente (Usuario)|
|{00000000-0000-0000-0000-000000000031}|Informes de uso de generación de disponibilidad de software|
|{00000000-0000-0000-0000-000000000032}|Mensaje de actualización de origen|
|{00000000-0000-0000-0000-000000000037}|Borrar la memoria caché de configuración de proxy|
|{00000000-0000-0000-0000-000000000040}|Agente de limpieza de directiva de máquina|
|{00000000-0000-0000-0000-000000000041}|Agente de limpieza de directiva de usuario|
|{00000000-0000-0000-0000-000000000042}|Asignación / Directiva de máquina de validación de agente de directiva|
|{00000000-0000-0000-0000-000000000043}|Asignación / Directiva de usuario de validación de agente de directiva|
|{00000000-0000-0000-0000-000000000051}|Reintentar/Actualizar los certificados en AD o en MP|
|{00000000-0000-0000-0000-000000000061}|Notificación de estado de DP del mismo nivel|
|{00000000-0000-0000-0000-000000000062}|Programación de comprobación de paquete pendiente de DP del mismo nivel|
|{00000000-0000-0000-0000-000000000063}|Programación de instalación de actualizaciones de SUM|
|{00000000-0000-0000-0000-000000000101}|Ciclo de recopilación de inventario de hardware|
|{00000000-0000-0000-0000-000000000102}|Ciclo de recopilación de inventario de software|
|{00000000-0000-0000-0000-000000000103}|Ciclo de recopilación de datos de detección|
|{00000000-0000-0000-0000-000000000104}|Ciclo de recopilación de archivos|
|{00000000-0000-0000-0000-000000000105}|Ciclo de recopilación de IDMIF|
|{00000000-0000-0000-0000-000000000106}|Ciclo de informes de uso de disponibilidad de software|
|{00000000-0000-0000-0000-000000000107}|Ciclo de actualización de la lista de origen de Windows Installer|
|{00000000-0000-0000-0000-000000000108}|Ciclo de evaluación de asignaciones de actualizaciones de software de acción de directiva de actualizaciones de software|
|{00000000-0000-0000-0000-000000000109}|Tarea de mantenimiento del punto de distribución de rama de directiva de mantenimiento PDP|
|{00000000-0000-0000-0000-000000000110}|Directiva DCM|
|{00000000-0000-0000-0000-000000000111}|Enviar mensajes de estado no enviados|
|{00000000-0000-0000-0000-000000000112}|Limpieza de caché de directiva de estado del sistema|
|{00000000-0000-0000-0000-000000000113}|Actualizar la directiva de origen|
|{00000000-0000-0000-0000-000000000114}|Actualizar la directiva de almacenamiento|
|{00000000-0000-0000-0000-000000000115}|Punto alto de envío masivo de directiva de sistema de estado|
|{00000000-0000-0000-0000-000000000116}|Punto bajo de envío masivo de directiva de sistema de estado|
|{00000000-0000-0000-0000-000000000121}|Acción de directiva del administrador de aplicación|
|{00000000-0000-0000-0000-000000000122}|Acción de directiva del usuario de administrador de aplicación|
|{00000000-0000-0000-0000-000000000123}|Acción de evaluación global del administrador de aplicación|
|{00000000-0000-0000-0000-000000000131}|Generador de resumen de inicio de Power Management|
|{00000000-0000-0000-0000-000000000221}|Volver a evaluar implementación de extremo|
|{00000000-0000-0000-0000-000000000222}|Volver a evaluar directiva de AM de extremo|
|{00000000-0000-0000-0000-000000000223}|Detección de eventos externos|



