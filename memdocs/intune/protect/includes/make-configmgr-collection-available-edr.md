---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823527"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Desde una consola de Configuration Manager conectada al sitio de nivel superior, haga clic con el botón derecho en una colección de dispositivos que sincronice con el centro de administración de Microsoft Endpoint Manager y seleccione **Propiedades**.

2. En la pestaña **Cloud Sync** (Sincronización en la nube), habilite la opción **Make this collection available to assign Endpoint security policies from Microsoft Endpoint Manager admin center** (Permitir que esta colección esté disponible para asignar directivas de seguridad de punto de conexión desde el centro de administración de Microsoft Endpoint Manager).

   - No se puede seleccionar esta opción si la jerarquía de Configuration Manager no está asociada al inquilino.
   - Las colecciones disponibles para esta opción están limitadas por el [ámbito de la colección seleccionado para la carga de asociación de inquilinos](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit). <!--CM7423168-->
  
   ![Configuración de la sincronización en la nube](../media/tenant-attach-intune/cloud-sync.png)

3. Seleccione **Aceptar** para guardar la configuración.

   Los dispositivos de esta colección pueden incorporar ahora ATP de Microsoft Defender y admiten el uso de directivas de seguridad de punto de conexión de Intune.
