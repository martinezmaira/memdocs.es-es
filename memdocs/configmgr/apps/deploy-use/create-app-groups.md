---
title: Crear grupos de aplicaciones
titleSuffix: Configuration Manager
description: Cree un grupo de aplicaciones que puede enviar a una colección de usuarios o dispositivos como una sola implementación en Configuration Manager.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643125"
---
# <a name="create-application-groups"></a>Crear grupos de aplicaciones

*Se aplica a: Configuration Manager (rama actual)*

<!--3555907-->

A partir de la versión 1906, cree un grupo de aplicaciones que puede enviar a una colección de usuarios o dispositivos como una sola implementación. Los metadatos que especifique sobre el grupo de aplicaciones se ven en el Centro de software como una sola entidad. Puede ordenar las aplicaciones en el grupo para que el cliente las instale en un orden específico.

> [!Note]  
> En esta versión de Configuration Manager, los grupos de aplicaciones son una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](../../core/servers/manage/pre-release-features.md).  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Administración de aplicaciones** y seleccione el nodo **Grupo de aplicaciones**.  

1. En el grupo Crear de la cinta de opciones, seleccione **Crear grupo de aplicaciones**.

1. En la página **Información general**, especifique información sobre el grupo de aplicaciones.  

1. En la página **Centro de software**, incluya la información que se muestra en el Centro de software.  

1. En la página **Grupo de aplicaciones**, seleccione **Agregar**. Seleccione una o más aplicaciones para este grupo. Puede cambiarlas de orden con las acciones **Subir** y **Bajar**.  

1. Complete el asistente.  

Implemente el grupo de aplicaciones con el mismo proceso que para una aplicación. Para obtener más información, consulte [Deploy applications](deploy-applications.md) (Implementar aplicaciones). A partir de la versión 1910, puede implementar un grupo de aplicaciones en recopilaciones de dispositivos o usuarios.

Después de implementar el grupo:

- Si agrega una nueva aplicación al grupo, debe distribuir por separado el nuevo contenido de la aplicación en los puntos de distribución.

- Si modifica una aplicación en el grupo de aplicaciones, redistribuya el contenido.

Para solucionar problemas con la implementación de un grupo de aplicaciones, use los siguientes archivos de registro en el cliente:

- **AppGroupHandler.log**
- **AppEnforce.log**
- **SettingsAgent.log**

> [!Important]  
> No cree ni implemente un grupo de aplicaciones hasta que actualice la jerarquía completa y los clientes de destino a la versión 1906 como mínimo.

### <a name="known-issues"></a>Problemas conocidos

- *Versión 1906*: las aplicaciones del grupo solo pueden contener tipos de implementación de **Windows Installer** o de **script**.
  - *Versión 1906*: establezca el comportamiento de la instalación del tipo de implementación en **Instalar para el sistema**.
- Es posible que las siguientes opciones de implementación no funcionen: alertas, aprobación, implementación por fases, reparación.
- No se pueden exportar ni importar grupos de aplicaciones.
- No incluya en el grupo aplicaciones que exijan un reinicio, de lo contrario, puede producirse un error en la implementación del grupo.
- *Versión 1906*: no se puede implementar un grupo de aplicaciones en una recopilación de usuarios.
- *Versión 1906*: los usuarios no pueden **desinstalar** el grupo de aplicaciones en el Centro de software.
- Si elimina una aplicación que forma parte de un grupo de aplicaciones, verá la siguiente advertencia la próxima vez que vea las propiedades del grupo de aplicaciones: "No se puede cargar la información de todas las aplicaciones del grupo". Realice un pequeño cambio en el grupo de aplicaciones y guárdelo. Por ejemplo, agregue un espacio a los **comentarios del administrador**. Al guardar el cambio, se quita la aplicación eliminada del grupo.<!-- 7099542 -->
