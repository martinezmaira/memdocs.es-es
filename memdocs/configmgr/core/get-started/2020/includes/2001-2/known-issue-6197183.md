---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703007"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> No se pueden crear o editar algunas colecciones

<!--6197183-->
En esta versión de la rama Technical Preview no se pueden crear colecciones. Además, tampoco se pueden editar las propiedades de una colección de usuario.

Para buscar una solución alternativa a este problema, use los cmdlets de PowerShell de Configuration Manager para crear colecciones y editar las colecciones de usuario existentes. Algunos de los cmdlets disponibles para administrar colecciones son los siguientes:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)