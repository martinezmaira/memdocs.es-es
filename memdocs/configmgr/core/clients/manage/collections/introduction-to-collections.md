---
title: Introducción a las colecciones
titleSuffix: Configuration Manager
description: Obtenga una introducción para usar las recopilaciones en Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e43f5a36f2a1bf44959b9645c2fb48a22cc71f1
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126780"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Introducción a las recopilaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las recopilaciones le ayudan a organizar los recursos en unidades administrables. Puede crear colecciones para satisfacer las necesidades de administración del cliente y para realizar operaciones en varios recursos a la vez. 

La mayoría de las tareas de administración se basan en el uso de una o más recopilaciones o requieren el uso de una o más de ellas. Aunque puede utilizar la recopilación integrada de Todos los sistemas, utilizarla para tareas de administración no es una práctica recomendada. Cree recopilaciones personalizadas para identificar más específicamente los dispositivos o usuarios para una tarea.  

 Las recopilaciones integradas y personalizadas aparecen en los nodos **Recopilaciones de usuarios** y **Recopilaciones de dispositivos** en el área de trabajo **Activos y compatibilidad** en la consola de Configuration Manager.  

 Las recopilaciones que ha visto recientemente aparecen en el nodo **Usuarios** y en el nodo **Dispositivos** en el área de trabajo **Activos y compatibilidad**.  

Estos son algunos ejemplos de uso de la colección:  

|Operación|Ejemplo|  
|---------|-------|  
|Agrupación de recursos|Puede crear recopilaciones que agrupen recursos según la jerarquía de la organización.<br /><br /> Por ejemplo, podría crear una recopilación de todos los equipos que se encuentran en la unidad organizativa (UO) de Active Directory "oficina central de Londres". Para más información sobre cómo crear este tipo de recopilación, vea [Cómo crear recopilaciones](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Después, podría usar esta recopilación para realizar operaciones como la configuración de Endpoint Protection, configurar opciones de administración de energía de dispositivos o instalar el cliente de Configuration Manager.|  
|Implementación de aplicaciones|Puede crear una colección de todos los equipos que no tienen instalado Aplicaciones de Microsoft Office 365 y, luego, implementarlo en todos los equipos de esa colección.<br /><br /> También puede utilizar los requisitos de la aplicación para realizar esta tarea. Para más información, vea [Cómo crear aplicaciones con Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Administración de la configuración de clientes](../../../../core/clients/deploy/about-client-settings.md)|Aunque la configuración predeterminada del cliente de Configuration Manager se aplica a todos los dispositivos y todos los usuarios, puede crear una configuraciones personalizadas de cliente que se apliquen a una recopilación de dispositivos o una recopilación de usuarios.<br /><br /> Por ejemplo, si desea que el control remoto esté disponible en la mayoría de los dispositivos, defina la configuración predeterminada del cliente para permitir el control remoto y, a continuación, defina los parámetros personalizados del cliente que no permiten el control remoto y realice la implementación en la colección de clientes excepcionales. |  
|[Administración de energía](../power/introduction-to-power-management.md)|Puede establecer la configuración de alimentación específica por colección.|  
|[Administración basada en roles](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Use las colecciones para controlar qué grupos de usuarios tienen acceso a distintas funcionalidades en la consola de Configuration Manager.|  
|[Ventanas de mantenimiento](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Las ventanas de mantenimiento le permiten definir un periodo durante el cual es posible llevar a cabo varias operaciones de Configuration Manager en miembros de una colección de dispositivos. |  


## <a name="collection-types-in-configuration-manager"></a>Tipos de recopilación en Configuration Manager  
 Configuration Manager tiene colecciones integradas para operaciones comunes. Además, también puede crear colecciones personalizadas.   

### <a name="built-in-collections"></a>Recopilaciones integradas  
 De manera predeterminada, Configuration Manager incluye las siguientes recopilaciones, que no pueden modificarse.  

|**Nombre de recopilación**|Descripción|  
|-------------------------|-----------------|  
|**Todos los grupos de usuarios**|Contiene los grupos de usuarios que se detectan mediante la detección de grupos de seguridad de Active Directory.|  
|**Todos los usuarios**|Contiene los usuarios que se detectan mediante la detección de usuarios de Active Directory.|  
|**Todos los usuarios y grupos de usuarios**|Contiene las recopilaciones Todos los usuarios y Todos los grupos de usuarios. Esta recopilación contiene el ámbito más amplio de recursos de usuarios y grupos de usuarios.|  
|**Todos los clientes de escritorio y servidor**|Contiene los dispositivos de servidor y de escritorio que tienen instalado el cliente de Configuration Manager. La pertenencia se mantiene mediante la detección de latidos.|  
|**Todos los dispositivos móviles**|Contiene los dispositivos móviles administrados por Configuration Manager. La pertenencia está restringida a aquellos dispositivos móviles que se asignan correctamente a un sitio o los detecta el conector de Exchange Server.|  
|**Todos los sistemas**|Contiene las colecciones Todos los clientes de escritorio y servidor, Todos los dispositivos móviles, Todos los equipos desconocidos y todos los dispositivos móviles inscritos por Microsoft Intune. Esta colección contiene el ámbito más grande de recursos de dispositivos.|  
|**Todos los equipos desconocidos**|Contiene registros de equipos genéricos para varias plataformas de equipos. Puede utilizar esta recopilación para implementar un sistema operativo mediante una secuencia de tareas y el arranque PXE, medios de arranque o medios preconfigurados.|  

### <a name="custom-collections"></a>Recopilaciones personalizadas  
 Cuando se crea una recopilación personalizada en Configuration Manager, la pertenencia de dicha recopilación viene determinada por una o varias reglas de recopilación, como se describe en [Cómo crear recopilaciones](../../../../core/clients/manage/collections/create-collections.md). 

