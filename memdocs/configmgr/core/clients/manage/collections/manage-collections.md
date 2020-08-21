---
title: Administración de recopilaciones
titleSuffix: Configuration Manager
description: Realice tareas de administración de recopilaciones comunes en Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 063ce963e805651ffd795e830d2b21dfed6fc043
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693138"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Administración de recopilaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Utilice la información de introducción de este artículo como ayuda para realizar tareas de administración para las recopilaciones en Configuration Manager.  

> [!NOTE]  
>  Para obtener información sobre cómo crear recopilaciones de Configuration Manager, vea [How to create collections](create-collections.md) (Creación de recopilaciones).



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a> Administración de recopilaciones de dispositivos  

En el área de trabajo **Activos y compatibilidad** , seleccione **Recopilaciones de dispositivos**, seleccione la recopilación que se debe administrar y luego seleccione una tarea de administración.  


#### <a name="show-members"></a>Mostrar miembros
Muestra todos los recursos que sean miembros de la recopilación seleccionada en un nodo temporal en el nodo **Dispositivos** .


#### <a name="add-selected-items"></a>Agregar los elementos seleccionados
Se muestran las opciones siguientes: 

- **Agregar elementos seleccionados a la recopilación de dispositivos existente**: Abre el cuadro de diálogo **Seleccionar recopilación** . Seleccione la recopilación a la que desea agregar los miembros de la recopilación seleccionada. La recopilación seleccionada se incluye en esta recopilación mediante una regla de pertenencia **Incluir recopilaciones** .  

- **Agregar elementos seleccionados a la nueva recopilación de dispositivos**: abre el **Asistente para crear recopilación de dispositivos**, donde puede crear una recopilación. La recopilación seleccionada se incluye en esta recopilación mediante una regla de pertenencia **Incluir recopilaciones** .  


Para obtener más información, vea [Creación de recopilaciones](create-collections.md).


#### <a name="install-client"></a>Instalar el cliente
Se abre el **Asistente para la instalación de cliente**. Este asistente utiliza la instalación de inserción de cliente para instalar un cliente de Configuration Manager en todos los equipos de la recopilación seleccionada. Para obtener más información, vea [Instalación de inserción de cliente](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


#### <a name="run-script"></a>Ejecutar script
Se abre el Asistente para **ejecutar script** para ejecutar un script de PowerShell en todos los clientes de la recopilación. Para obtener más información, consulte [Creación y ejecución de scripts de PowerShell](../../../../apps/deploy-use/create-deploy-scripts.md).


#### <a name="manage-affinity-requests"></a>Administrar solicitudes de afinidad
Se abre el cuadro de diálogo **Administrar solicitudes de afinidad de dispositivo de usuario**. Apruebe o rechace solicitudes pendientes para establecer afinidades de dispositivos de usuario de dispositivos de la recopilación seleccionada. Para obtener más información, vea [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).


#### <a name="clear-required-pxe-deployments"></a>Desactive las implementaciones de PXE necesaria
Borra las implementaciones de arranque PXE necesarias de todos los miembros de la recopilación seleccionada. Para más información, vea [Use PXE to deploy Windows over the network](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Uso de PXE para implementar Windows a través de la red).


#### <a name="update-membership"></a>Actualizar pertenencia
Evalúa la pertenencia a la colección seleccionada. En las recopilaciones con muchos miembros, esta actualización puede tardar algo de tiempo en finalizar. Utilice la acción **Actualizar** para actualizar la pantalla con los nuevos miembros de las recopilaciones después de que se complete la actualización.


#### <a name="add-resources"></a>Agregar recursos
Se abre el cuadro de diálogo **Agregar recursos a la recopilación**. Busque nuevos recursos para agregarlos a la recopilación seleccionada. El icono de la recopilación seleccionada muestra un símbolo de reloj de arena mientras la actualización está en curso.


#### <a name="client-notification"></a>Notificación de cliente
Para obtener más información, vea [Notificación de cliente](../client-notification.md).


#### <a name="endpoint-protection"></a>Endpoint Protection
Para obtener más información, vea [Notificación de cliente](../client-notification.md).


#### <a name="export"></a>Exportar
Abre el **Asistente para exportación de recopilación** que le ayuda a exportar esta recopilación a un archivo de formato de objetos administrados (MOF). Este archivo puede archivarse o importarse luego en otro sitio de Configuration Manager. Al exportar una recopilación, no se exportan las recopilaciones a las que se hace referencia. Este tipo de recopilaciones son aquellas a las que se hace referencia por parte de la recopilación seleccionada mediante una regla de **inclusión** o **exclusión**.


#### <a name="copy"></a>Copiar
Crea una copia de la colección seleccionada. La nueva recopilación utiliza la recopilación seleccionada como una recopilación de restricción.


#### <a name="refresh"></a>Actualizar
Actualiza la vista.


#### <a name="delete"></a>Eliminar
Elimina la colección seleccionada. También puede eliminar todos los recursos de la recopilación de la base de datos del sitio. 

No puede eliminar las recopilaciones integradas en Configuration Manager. Para obtener una lista de las recopilaciones integradas, consulte [Introduction to collections](introduction-to-collections.md#built-in-collections) (Introducción a las recopilaciones).


#### <a name="simulate-deployment"></a>Simular implementación
Se abre el **Asistente para simular implementación de aplicación**. Este asistente le permite probar los resultados de una implementación de aplicación en equipos sin instalar ni desinstalar la aplicación. Para obtener más información, consulte [Cómo simular implementaciones de aplicaciones](../../../../apps/deploy-use/simulate-application-deployments.md).


#### <a name="deploy"></a>Implementar
Se muestran las opciones siguientes:  

- **Aplicación**: abre el **Asistente para implementar software**. Seleccione y configure una implementación de aplicación en la recopilación seleccionada. Para obtener más información, consulte [Cómo implementar aplicaciones](../../../../apps/deploy-use/deploy-applications.md).  

- **Programa**: abre el **Asistente para implementar software**. Seleccione y configure una implementación de paquete y programa en la recopilación seleccionada. Para obtener más información, consulte [Paquetes y programas](../../../../apps/deploy-use/packages-and-programs.md).  

- **Línea de base de configuración**: abre el cuadro de diálogo **Implementar líneas de base de configuración**. Configure la implementación de una o varias líneas base de configuración en la recopilación seleccionada. Para más información, vea [Cómo implementar líneas base de configuración](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  

- **Secuencia de tareas**: abre el **Asistente para implementar software**. Seleccione y configure una implementación de secuencia de tareas en la recopilación seleccionada. Para obtener más información, vea [Manage task sequences to automate tasks](../../../../osd/deploy-use/deploy-a-task-sequence.md) (Administración de secuencias de tareas para automatizar tareas).  

- **Actualizaciones de software**: se abre el **Asistente para implementar actualizaciones de software**. Configure la implementación de actualizaciones de software en los recursos de la recopilación seleccionada. Para obtener más información, vea [Administrar actualizaciones de software](../../../../sum/understand/software-updates-introduction.md).  


#### <a name="clear-server-group-deployment-locks"></a>Borrar los bloqueos de implementación del grupo de servidores
Libere de forma manual todos los bloqueos de implementación del grupo de servidores de la recopilación. Para obtener más información, consulte [Dar servicio a un grupo de servidores](../../../../sum/deploy-use/service-a-server-group.md).


#### <a name="move"></a>Mover
Mueva la recopilación seleccionada a otra carpeta en el nodo **Recopilaciones de dispositivos**. 


#### <a name="properties"></a>Propiedades
Para obtener más información, consulte [Propiedades de recopilación](#BKMK_CollProp).  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a> Administración de recopilaciones de usuarios  

En el área de trabajo **Activos y compatibilidad** , seleccione **Recopilaciones de usuarios**, seleccione la recopilación que se debe administrar y luego seleccione una tarea de administración.  

> [!Note]  
> Las siguientes acciones están disponibles en las recopilaciones de usuarios, pero los comportamientos son los mismos que en las recopilaciones de dispositivos. La diferencia es que se aplican a las recopilaciones de usuarios y los usuarios contenidos en estas. Para obtener más información, vea la acción correspondiente en [Cómo administrar recopilaciones de dispositivos](#bkmk_device).  

- **Mostrar miembros**  
- **Agregar elementos seleccionados**  
    - **Agregar elementos seleccionados a la recopilación de usuario existente**  
    - **Agregar elementos seleccionados a la nueva recopilación de usuario**  
- **Administrar solicitudes de afinidad**  
- **Actualizar pertenencia**  
- **Agregar recursos**  
- **Exportarar**  
- **Copiar**  
- **Actualizar**  
- **Eliminar**  
- **Simular implementación**  
- **Implementar**  
    - **Aplicación**  
    - **Programa**  
    - **Línea de base de configuración**
- **Moverr**  
- **Propiedades**


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> Propiedades de recopilación  

Al abrir el cuadro de diálogo **Propiedades** de una recopilación, vea y configure las opciones siguientes:  

#### <a name="general"></a>General
Vea y configure información general sobre la recopilación seleccionada, incluidos el nombre de la recopilación y la recopilación de restricción.

#### <a name="membership-rules"></a>Reglas de asociación
Configure las reglas de pertenencia que definen la pertenencia de esta recopilación. Para obtener más información, vea [Creación de recopilaciones](create-collections.md).  

#### <a name="power-management"></a>Administración de energía
Configure los planes de administración de energía que se asignan a los equipos de la recopilación seleccionada. Para obtener más información, consulte [Introduction to power management](../power/introduction-to-power-management.md) (Introducción a la administración de energía).  

#### <a name="deployments"></a>Implementaciones
Muestra cualquier software que haya implementado en los miembros de la recopilación seleccionada.  

#### <a name="maintenance-windows"></a>Ventanas de mantenimiento
Vea y configure ventanas de mantenimiento que se aplican a los miembros de la recopilación seleccionada. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](use-maintenance-windows.md) (Uso de ventanas de mantenimiento en Configuration Manager).

#### <a name="collection-variables"></a>Colección de Variables
Configure variables que se aplican a esta recopilación y se pueden utilizar por las secuencias de tareas. Para obtener más información, consulte [How to set task sequence variables](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set) (Establecimiento de las variables de secuencia de tareas).  

#### <a name="distribution-point-groups"></a>Grupos de puntos de distribución
Asocie uno o varios grupos de puntos de distribución a los miembros de la recopilación seleccionada. Para obtener más información, consulte [Manage content and content infrastructure](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración del contenido y de la infraestructura de contenido).

#### <a name="aad-group-sync"></a>Sincronización de grupos de AAD
Sincronice los resultados de la pertenencia a recopilaciones con grupos de Azure Active Directory. Esta sincronización es una [característica de versión preliminar](../../../servers/manage/pre-release-features.md) a partir de la versión 1906. Para más información, vea [Create collections](create-collections.md#bkmk_aadcollsync) (Crear recopilaciones).

#### <a name="security"></a>Seguridad
Muestra los usuarios administrativos que tienen permisos para la recopilación seleccionada de ámbitos de seguridad y roles asociados. Para obtener más información, vea [Aspectos básicos de la administración basada en roles](../../../understand/fundamentals-of-role-based-administration.md).  

#### <a name="alerts"></a>Alertas 
Configure cuándo se generan alertas del estado de los clientes y Endpoint Protection. Para obtener más información, vea [Cómo configurar el estado de cliente](../../deploy/configure-client-status.md) y [Cómo supervisar Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md).  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Con PowerShell

PowerShell puede usarse para administrar las recopilaciones.  Para obtener más información, vea:

* [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)
* [Copy-CMCollection](/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](/powershell/module/configurationmanager/import-cmcollection)
* [Export-CMCollection](/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)