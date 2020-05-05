---
title: Administración de dispositivos con Exchange
titleSuffix: Configuration Manager
description: Administrar dispositivos móviles con el conector de Exchange Server en Configuration Manager.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724809"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Administración de dispositivos con Exchange y Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Si tiene dispositivos móviles que se conectan a Exchange Server mediante el protocolo ActiveSync, puede usar el conector de Exchange Server en Configuration Manager para administrar estos dispositivos. El conector funciona con Exchange Server local o Exchange Online. Use la consola de Configuration Manager para configurar las características de administración de dispositivos móviles de Exchange. Por ejemplo, el borrado remoto del dispositivo y el control de configuración para varios servidores de Exchange.

![Diagrama lógico del conector de Exchange Server con Configuration Manager](media/configmgr-with-exchange.png)  

Cuando se administran dispositivos móviles con este conector, no se instala el cliente de Configuration Manager ni se inscriben los dispositivos a través de MDM. Las funciones de administración de Exchange Server están limitadas en comparación con estas otras opciones. Por ejemplo, no puede instalar software ni utilizar elementos de configuración para configurar estos dispositivos. Para obtener más información, vea [elegir una solución de administración de dispositivos para Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

## <a name="policies"></a>Directivas

Cuando se usa el conector, Configuration Manager configura los valores en los dispositivos móviles. Los dispositivos no usan las directivas de buzón predeterminadas de Exchange ActiveSync. Defina la configuración que desea usar en los siguientes grupos:

- **General**
- **Contraseña**
- **Administración de correo electrónico**
- **Seguridad**
- **Aplicación**

Por ejemplo, en el grupo **contraseña** , puede configurar las siguientes opciones:

- Si los dispositivos móviles requieren una contraseña
- La longitud mínima de la contraseña
- Complejidad de la contraseña
- Si se permite la recuperación de contraseñas

Cuando se configura al menos una opción en el grupo, Configuration Manager administra toda la configuración del grupo para dispositivos móviles. Si no configura ninguna opción en un grupo, Exchange sigue administrando esa configuración para los dispositivos móviles. Todavía se aplican las directivas de buzón de Exchange ActiveSync que se configuran en el servidor de Exchange y se asignan a los usuarios.

## <a name="access-rules-and-remote-actions"></a>Reglas de acceso y acciones remotas

También puede configurar el conector de Exchange Server para administrar las reglas de acceso de Exchange. Estas reglas de acceso incluyen permitir, bloquear o poner en cuarentena dispositivos móviles. Puede borrar de forma remota dispositivos móviles mediante la consola de Configuration Manager y los usuarios pueden borrar sus dispositivos móviles de forma remota mediante el catálogo de aplicaciones.

El dispositivo móvil de un usuario aparece automáticamente en el catálogo de aplicaciones cuando lo administra y el servidor de Exchange es local. Para que el dispositivo móvil aparezca en el catálogo de aplicaciones cuando se usa Exchange Online, configure manualmente la afinidad de dispositivo de usuario. Para obtener más información, consulte [vincular usuarios y dispositivos con afinidad entre usuario y dispositivo](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

> [!TIP]  
> Cuando un dispositivo móvil se transfiere a otro usuario, antes de que el nuevo propietario configure su cuenta de Exchange en el dispositivo, elimine el dispositivo móvil de la consola de Configuration Manager.

## <a name="prerequisites"></a>Prerrequisitos

> [!IMPORTANT]  
> Antes de instalar este conector, confirme que Configuration Manager sea compatible con su versión de Exchange. Para obtener más información, consulte [configuraciones admitidas: conector de Exchange Server](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS).  

### <a name="permissions-to-configure-the-connector"></a>Permisos para configurar el conector

Necesita los siguientes permisos de seguridad para configurar el conector de Exchange Server en Configuration Manager:

- Para agregar, modificar y eliminar el conector de Exchange Server: permiso **Modificar** para el objeto **Sitio** .  

- Para establecer la configuración del dispositivo móvil: permiso **ModifyConnectorPolicy** para el objeto **Sitio** .  

Por ejemplo, el rol integrado **Administrador total** incluye estos permisos necesarios.  

### <a name="permissions-to-manage-mobile-devices"></a>Permisos para administrar dispositivos móviles

Necesita los siguientes permisos de seguridad para administrar dispositivos móviles:  

- Para borrar un dispositivo móvil: **Eliminar recurso** para el objeto **Recopilación** .  

- Para cancelar un comando de borrado: **Modificar recurso** para el objeto **Recopilación** .  

- Para permitir y bloquear dispositivos móviles: **Modificar recurso** para el objeto **Colección** .  

Por ejemplo, el rol integrado **Administrador de operaciones** incluye estos permisos necesarios.

Para obtener más información, consulte [configurar la administración basada en roles](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Instalación y configuración de Exchange Connector](install-configure-exchange-connector.md)
