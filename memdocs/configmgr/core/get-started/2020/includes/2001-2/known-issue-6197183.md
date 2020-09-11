---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: c7fce3664d23d6402d28b053129fb2b15b540a87
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644412"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> No se pueden crear o editar algunas colecciones

<!--6197183-->
En esta versión de la rama Technical Preview no se pueden crear colecciones. Además, tampoco se pueden editar las propiedades de una colección de usuario.

Para buscar una solución alternativa a este problema, use los cmdlets de PowerShell de Configuration Manager para crear colecciones y editar las colecciones de usuario existentes. Algunos de los cmdlets disponibles para administrar colecciones son los siguientes:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)