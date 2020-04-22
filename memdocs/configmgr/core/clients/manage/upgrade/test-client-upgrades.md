---
title: Prueba de las actualizaciones de cliente en una recopilación de preproducción
titleSuffix: Configuration Manager
description: Pruebe las actualizaciones de cliente en una recopilación de preproducción en Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3098356eb96609867c0cc16b70d7b141e2a91c26
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696843"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-configuration-manager"></a>Cómo probar las actualizaciones de cliente en una recopilación de preproducción en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede probar una nueva versión de cliente de Configuration Manager en una recopilación de preproducción antes de actualizar el resto del sitio con ella.  Al hacerlo, solo se actualizan los dispositivos que forman parte de la recopilación de prueba. Una vez que haya tenido la oportunidad de probar el cliente, puede promover el cliente, lo que hace que la nueva versión del software cliente esté disponible para el resto del sitio.

> [!NOTE]
> Para promover un cliente de prueba a producción, debe iniciar sesión como un usuario con el rol de seguridad de **Administrador total** y un ámbito de seguridad de **Todo**. Para obtener más información, vea [Aspectos básicos de la administración basada en roles](../../../understand/fundamentals-of-role-based-administration.md). También debe iniciar sesión en un servidor conectado al sitio de administración central o en un sitio primario independiente de nivel superior.

 Hay tres pasos básicos para probar los clientes en preproducción.  

1.  Configurar las actualizaciones automáticas de cliente para que usen una recopilación de preproducción.  

2.  Instalar una actualización de Configuration Manager que incluye una nueva versión del cliente.  

3.  Promover el nuevo cliente a producción.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Para configurar las actualizaciones automáticas de cliente para que usen una recopilación de preproducción  
> [!IMPORTANT]
> La implementación de clientes de preproducción no se admite en equipos del grupo de trabajo. no pueden usar la autenticación requerida para que el punto de distribución obtenga acceso al paquete de cliente de preproducción.  Reciben el cliente más reciente cuando se promueve a cliente de producción.

1. [Configure una recopilación](../collections/create-collections.md) que contenga los equipos en los que quiere implementar el cliente de preproducción.   

2. En la consola de Configuration Manager, abra **Administración** > **Configuración del sitio** > **Sitios** y elija **Configuración de jerarquía**.  

    En la pestaña **Actualización de cliente** de las **Propiedades de configuración de la jerarquía**:  

   -   Seleccione **Actualizar todos los clientes de la colección de preproducción automáticamente mediante el cliente de preproducción**.  

   -   Escriba el nombre de una colección para usarla como colección de preproducción.  

![Probar actualizaciones de cliente](media/test-client-upgrades.png)

>[!NOTE]
>Para cambiar esta configuración, la cuenta debe ser miembro del rol de seguridad **Administrador total** y el ámbito de seguridad **Todo**.


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Para instalar una actualización de Configuration Manager que incluye una nueva versión del cliente  

1.  En la consola de Configuration Manager, abra **Administración** > **Actualizaciones y mantenimiento**, seleccione una actualización **Disponible** y después elija **Instalar el paquete de actualización**. (Antes de la versión 1702, la opción Actualizaciones y mantenimiento se encontraba en **Administración** > **Cloud Services**).

     Para más información sobre cómo instalar actualizaciones, vea [Actualizaciones de Configuration Manager](../../../../core/servers/manage/updates.md).  

2.  Durante la instalación de la actualización, en la página **Opciones de cliente** del asistente, seleccione **Probar en la colección de preproducción**.  

3.  Complete el resto del asistente e instale el paquete de actualización.  

     Una vez que se complete el Asistente, los clientes de la recopilación de preproducción empezarán a implementar el cliente actualizado. Puede supervisar la implementación de clientes actualizados yendo a **Supervisión** > **Estado de cliente** > **Implementación de cliente de preproducción**. Para más información, vea [Supervisar el estado de implementación de cliente](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > El estado de implementación en equipos que hospedan los roles de sistema de sitio en una recopilación de preproducción puede aparecer registrado como **No compatible** incluso cuando el cliente se ha implementado correctamente. Cuando se promueve el cliente a la producción, el estado de implementación se registrará correctamente.

##  <a name="to-promote-the-new-client-to-production"></a>Para promover el nuevo cliente a producción  

1.  En la consola de Configuration Manager, abra **Administración** > **Actualizaciones y mantenimiento** y elija **Promover el cliente de preproducción**. (Antes de la versión 1702, la opción Actualizaciones y mantenimiento se encontraba en **Administración** > **Cloud Services**).

    > [!TIP]
    > El botón **Promover el cliente de preproducción** también está disponible cuando se están supervisando las implementaciones de cliente en la consola en **Supervisión** > **Estado de cliente** > **Implementación del cliente de preproducción**.

2.  Revise las versiones de cliente de preproducción y de producción, asegúrese de que está especificada la recopilación de preproducción correcta y, luego, haga clic en **Promover** y en **Sí**.  

3.  Después de cerrar el cuadro de diálogo, la versión del cliente actualizado reemplazará a la versión del cliente que se usa en la jerarquía. A continuación, puede actualizar los clientes de todo el sitio. Para más información, vea [Cómo actualizar clientes para equipos Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

>[!NOTE]
>Para habilitar el cliente de preproducción o promover un cliente de preproducción a un cliente de producción, su cuenta debe ser miembro del rol de seguridad que tiene permisos **Leer** y **Modificar** para el objeto **Paquetes de actualización**.
>Las actualizaciones de cliente cumplen las ventanas de mantenimiento de Configuration Manager que ha configurado.
