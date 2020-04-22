---
title: Supervisión del estado de implementación de cliente
titleSuffix: Configuration Manager
description: Supervise el estado de implementación de clientes en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80cfa1576ae2cc4505147aee07a247e035b07ada
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693853"
---
# <a name="how-to-monitor-client-deployment-status-in-configuration-manager"></a>Supervisión del estado de implementación de clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La implementación de clientes en el sitio lleva tiempo y algunas instalaciones no se realizan correctamente la primera vez. La consola de Configuration Manager ofrece una manera de vigilar las implementaciones de clientes en una recopilación mediante la notificación de su estado en tiempo real.  

> [!NOTE]  
>  La manera mejor y más confiable de supervisar la implementación del cliente es con la consola de Configuration Manager (como se describe en este artículo). La sección **Estado de cliente** del área de trabajo **Supervisión** de la consola proporciona información precisa y en tiempo real sobre el estado de la implementación. Las implementaciones de cliente se pueden supervisar con otras herramientas, como el Administrador de servidores de Windows Server o System Center Operations Manager, pero puede recibir alarmas aunque la actividad de la instalación de cliente sea normal. Como el programa de instalación de cliente (CCMSetup.exe) se ejecuta en varios entornos, estas otras herramientas pueden generar falsas alarmas y advertencias que no reflejan con precisión el estado de las implementaciones de cliente.  

 En el área de trabajo **Supervisión** de la consola, puede supervisar los siguientes estados para las implementaciones de cliente que tienen lugar dentro de una recopilación especificada:  

- conforme  

- En curso  

- No conforme  

- Failed  

- Unknown  

  Informes de Configuration Manager en implementaciones de clientes de producción o clientes de preproducción. La consola de Configuration Manager también proporciona un gráfico de implementaciones de cliente erróneas durante un período de tiempo especificado para ayudarle a determinar si las acciones que realiza para solucionar los problemas con las implementaciones mejoran su índice de éxito con el tiempo.  

## <a name="to-monitor-client-deployments"></a>Para supervisar las implementaciones de cliente  

- En la consola de Configuration Manager, haga clic en **Supervisión** > **Estado de cliente**.  

- Haga clic en **Implementación del cliente de producción** o **Implementación del cliente de preproducción**, según la versión de cliente que quiera supervisar.  

- Revise los gráficos de estado de implementación de cliente y error de implementación de cliente.  

- Si quiere cambiar el ámbito del informe, haga clic en **Examinar...** y elija otra recopilación.  

  Para más información sobre las implementaciones de clientes de preproducción, vea [Cómo probar las actualizaciones de cliente en una recopilación de preproducción](../../../core/clients/manage/upgrade/test-client-upgrades.md).

  > [!NOTE]
  > El estado de implementación en equipos que hospedan los roles de sistema de sitio en una recopilación de preproducción puede aparecer registrado como **No compatible** incluso cuando el cliente se ha implementado correctamente. Cuando se promueve el cliente a la producción, el estado de implementación se registrará correctamente.   

  Para supervisar el estado de los clientes implementados, vea [Supervisión de clientes](../../../core/clients/manage/monitor-clients.md).  

  Puede usar informes de Configuration Manager para tener más información sobre el estado de los clientes en el sitio. Para obtener más información sobre cómo ejecutar informes, vea [Introducción a los informes](../../servers/manage/introduction-to-reporting.md).  
