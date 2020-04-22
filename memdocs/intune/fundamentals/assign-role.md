---
title: Asignación de un rol a un usuario de Intune
description: Obtenga información sobre cómo asignar un rol integrado o personalizado a un usuario de Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: a679df157a2623012d19fab2370792cac73f6f2b
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "80326814"
---
# <a name="assign-a-role-to-an-intune-user"></a>Asignación de un rol a un usuario de Intune

Puede asignar un rol [integrado](role-based-access-control.md#built-in-roles) o [personalizado](create-custom-role.md) a un usuario de Intune.

Para crear, editar o asignar roles, la cuenta debe tener uno de los siguientes permisos en Azure AD:
- **Administrador global**
- **Administrador del servicio de Intune**

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Administración de inquilinos** > **Roles** > **Todos los roles**.

2. En la hoja **Roles de Intune: Todos los roles**, elija el rol integrado que quiera asignar > **Asignaciones** > **Asignar**.

5. En la página **Datos básicos**, escriba un **Nombre de asignación** y una **Descripción de la asignación** opcional y, luego, elija **Siguiente**.

6. En la página **Grupos de administradores**, seleccione el grupo que contenga el usuario al que quiera conceder los permisos. Elija **Siguiente**.

7. En la página **Ámbito (grupos)** , elija un grupo que contenga los usuarios o dispositivos que el miembro anterior tendrá permiso para administrar. Seleccione **Siguiente**.

8. En la página **Ámbito (etiquetas)** , elija las etiquetas donde se aplicará esta asignación de roles. Seleccione **Siguiente**.

9. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**. La nueva asignación se muestra en la lista de asignaciones.

## <a name="next-steps"></a>Pasos siguientes
- [Más información sobre el control de acceso basado en rol en Intune](role-based-access-control.md)
- [Creación de un rol personalizado](create-custom-role.md)


