---
title: Dar servicio a un grupo de servidores
titleSuffix: Configuration Manager
description: La consola de Configuration Manager proporciona alertas y estados para supervisar la compatibilidad y las actualizaciones.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: 7d6d8bef145e14547e5e6a726a93cb9470b94afd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709193"
---
# <a name="service-a-server-group"></a>Dar servicio a un grupo de servidores

*Se aplica a: Configuration Manager (rama actual)*

>[!IMPORTANT]
> - A partir de la versión 2002 de Configuration Manager, los grupos de servidores se han reemplazado por grupos de orquestaciones. Para obtener más información, consulte [Grupos de orquestaciones](orchestration-groups.md).
> - Las características de versión preliminar son características que se encuentran en la Rama actual para realizar las primeras pruebas en un entorno de producción. Estas características son totalmente compatibles pero aún se encuentran en proceso de desarrollo y podrían recibir cambios hasta que se saquen de la categoría de versión preliminar. Debe activar esta función para que esté disponible. Para más información, consulte [Use pre-release features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Uso de características de la versión preliminar a partir de las actualizaciones).

A partir de Configuration Manager versión 1606, puede configurar los grupos de servidores de una recopilación para definir la cantidad, el porcentaje o el orden en que instalarán las actualizaciones de software los equipos de la recopilación. También puede configurar scripts de PowerShell anteriores y posteriores a la implementación para ejecutar acciones personalizadas.

Al implementar actualizaciones de software en una recopilación que tiene configurado el grupo de servidores, Configuration Manager determina cuántos equipos de la recopilación pueden instalar las actualizaciones de software en un momento dado y proporciona el mismo número de bloqueos de implementación. Solo los equipos que obtengan un bloqueo de implementación iniciarán la instalación de la actualización de software. Cuando está disponible un bloqueo de implementación, un equipo obtiene el bloqueo de implementación, instala las actualizaciones de software y después libera el bloqueo de implementación cuando la instalación de actualizaciones de software se completa correctamente. Después, el bloqueo de implementación está disponible para otros equipos. Si un equipo no puede liberar un bloqueo de implementación, puede liberar de forma manual todos los bloqueos de implementación del grupo de servidores de la recopilación.

>[!IMPORTANT]
>Todos los equipos de la recopilación deben asignarse al mismo sitio.

#### <a name="to-create-a-collection-for-a-server-group"></a>Para crear una recopilación para un grupo de servidores  
El grupo de servidores se configura en las propiedades de una recopilación de dispositivos. Para atender a un grupo de servidores, todos los miembros de la recopilación deben asignarse al mismo sitio. Use los pasos siguientes para crear una recopilación y configurar el grupo de servidores:
1.  [Cree una recopilación de dispositivos](../../core/clients/manage/collections/create-collections.md) que contenga los equipos del grupo de servidores.  

2.  En el área de trabajo **Activos y compatibilidad**, haga clic en **Recopilaciones de dispositivos**, haga clic con el botón derecho en la recopilación que contiene los equipos del grupo de servidores y luego haga clic en **Propiedades**.  

3.  En la pestaña **General**, seleccione **Todos los dispositivos forman parte del mismo grupo de servidores** y luego haga clic en **Configuración**.  

4.  En la página **Configuración de grupo de servidores**, especifique una de las opciones siguientes:  

    -   **Permitir que un porcentaje de máquinas se actualice a la vez**: especifica que solo un determinado porcentaje de clientes se actualiza en un momento dado. Si, por ejemplo, la recopilación tiene 10 clientes y se configura para actualizar el 30 % de los clientes a la vez, solo 3 clientes instalarán las actualizaciones de software en un momento dado.  

    -   **Permitir que varias máquinas se actualicen a la vez**: especifica que solo un determinado número de clientes se actualiza en un momento dado.  

    -   **Indique la secuencia de mantenimiento**: especifica que los clientes de la recopilación se actualizarán de uno en uno en la secuencia que configure. Un cliente solo instalará las actualizaciones de software después de que el cliente que va por delante de él en la lista haya terminado de instalar sus actualizaciones de software.  

5.  Especifique si quiere usar un script anterior a la implementación (purga de nodo) o posterior a la implementación (reanudación de nodo).  

    > [!WARNING]
    > Los scripts personalizados no están firmados por Microsoft. Es su responsabilidad para mantener la integridad de estos scripts.

    > [!TIP]  
    > Los siguientes son ejemplos que puede usar en las pruebas para los scripts anteriores a la implementación y posteriores a la implementación que escriben la hora actual en un archivo de texto:  
    >   
    >  **Anterior a la implementación**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Posterior a la implementación**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Implementar actualizaciones de software en el grupo de servidores y supervisar el estado  
Para implementar actualizaciones de software en la recopilación del grupo de servidores, siga el proceso de implementación típico. Después de implementar las actualizaciones de software, puede supervisar la implementación de actualizaciones de software en la consola de Configuration Manager.
1.  [Implemente las actualizaciones de software](manually-deploy-software-updates.md) en la recopilación del grupo de servidores.   

2.  [Supervise la implementación de las actualizaciones de software](monitor-software-updates.md). Además de las vistas de supervisión estándar para la implementación de actualizaciones de software, se muestra el estado **En espera de bloqueo** cuando un cliente está esperando su turno para instalar las actualizaciones de software. Puede revisar el archivo UpdatesDeployment.log para obtener más información.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Borrar los bloqueos de implementación de los equipos de un grupo de servidores  
Si un equipo no puede liberar un bloqueo de implementación, puede liberar de forma manual todos los bloqueos de implementación del grupo de servidores de la recopilación. Borre bloqueos solo cuando se bloquee una implementación al actualizar equipos en la recopilación y haya equipos que aún no sean compatibles.  
1.  En el área de trabajo **Activos y compatibilidad**, haga clic en **Recopilaciones de dispositivos** y luego haga clic en la recopilación para borrar los bloqueos de implementación.  

2.  En la pestaña **Inicio**, en el grupo **Implementación**, haga clic en **Borrar los bloqueos de implementación del grupo de servidores**. Si los clientes no han podido instalar las actualizaciones de software e impiden que otros clientes instalen las suyas, los bloqueos de implementación se pueden borrar de forma manual.  
