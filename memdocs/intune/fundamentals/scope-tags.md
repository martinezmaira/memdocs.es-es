---
title: Uso del control de acceso basado en rol (RBAC) y etiquetas de ámbito para TI distribuida en Intune | Microsoft Docs
description: Use las etiquetas de ámbito para filtrar los perfiles de configuración por roles específicos.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: a21d3039-f2ed-4f43-b6fa-d00c071edbc4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a229b9159c4c3613edc2d718db1fd0931f94cf9f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240751"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito para TI distribuida

Puede usar control de acceso basado en rol y etiquetas de ámbito para asegurarse de que los administradores adecuados tengan el acceso y la visibilidad correctos para los objetos de Intune apropiados. Los roles determinan qué acceso tienen los administradores a qué objetos. Las etiquetas de ámbito determinan qué objetos pueden ver los administradores.

Por ejemplo, imagine que un administrador de la sucursal regional de Seattle tiene el rol Administrador de perfiles y directivas. Quiere que este administrador solo vea y administre los perfiles y las directivas que se aplican exclusivamente a los dispositivos de Seattle. Para configurar este acceso, debería hacer lo siguiente:

1. Crear una etiqueta de ámbito denominada Seattle.
2. Crear una asignación de roles para el rol Administrador de perfiles y directivas con: 
    - Miembros (grupos) = un grupo de seguridad denominado Administradores de TI de Seattle. Todos los administradores de este grupo tienen permiso para administrar las directivas y los perfiles de los usuarios o los dispositivos de Ámbito (grupos).
    - Ámbito (grupos) = un grupo de seguridad denominado Usuarios de Seattle. Todos los usuarios o dispositivos de este grupo pueden tener sus perfiles y directivas administrados por los administradores de Miembros (grupos). 
    - Ámbito (etiquetas) = Seattle. Los administradores de Miembros (grupos) pueden ver los objetos de Intune que tienen también la etiqueta de ámbito Seattle.
3. Agregue la etiqueta de ámbito Seattle a las directivas y los perfiles a los que quiera que puedan tener acceso los administradores de Miembros (grupos).
4. Agregar la etiqueta de ámbito Seattle a los dispositivos que quiere que sean visibles para los administradores de Miembros (grupos). 

## <a name="default-scope-tag"></a>Etiquetas de ámbito predeterminadas
La etiqueta de ámbito predeterminada se agrega de forma automática a todos los objetos sin etiqueta que admiten etiquetas de ámbito.

Esta característica es similar a la característica de ámbitos de seguridad de Microsoft Endpoint Configuration Manager. 

## <a name="to-create-a-scope-tag"></a>Para crear una etiqueta de ámbito

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Administración de inquilinos** > **Roles** > **Ámbito (etiquetas)**  > **Crear**.
2. En la página **Datos básicos**, proporcione un **Nombre** y una **Descripción** opcional. Elija **Siguiente**.
3. En la página **Asignaciones**, elija los grupos que contengan los dispositivos que quiera asignar a esta etiqueta de ámbito. Elija **Siguiente**.
4. En la página **Revisar y crear**, elija **Crear**.

## <a name="to-assign-a-scope-tag-to-a-role"></a>Para asignar una etiqueta de ámbito a un rol

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Administración de inquilinos** > **Roles** > **Todos los roles** > seleccione un rol > **Asignaciones** > **Asignar**.
2. En la página **Datos básicos**, proporcione un **Nombre de asignación** y una **Descripción**. Elija **Siguiente**.
3. En la página **Grupos de administración**, elija **Seleccionar grupos para incluir** y seleccione los grupos que quiere que formen parte de esta asignación. Los usuarios de este grupo tendrán permisos para administrar los usuarios o dispositivos de Ámbito (grupos). Elija **Siguiente**.

    ![Captura de pantalla de la selección de grupos de miembros.](./media/scope-tags/select-member-groups.png)

4. En la página **Grupos de ámbito**, seleccione una de las opciones siguientes para **Asignar a**
    - **Grupos seleccionados**: seleccione los grupos que contienen los usuarios o dispositivos que quiere administrar. Todos los usuarios o dispositivos de los grupos seleccionados serán administrados por los usuarios de los grupos de administración.
    - **Todos los usuarios**: todos los usuarios pueden ser administrados por los usuarios de los grupos de administración.
    - **Todos los dispositivos**: todos los dispositivos pueden ser administrados por los usuarios de los grupos de administración.
    - **Todos los usuarios y dispositivos**: todos los usuarios y todos los dispositivos pueden ser administrados por los usuarios de los grupos de administración.

5. Elija **Siguiente**.
6. En la página **Ámbito (etiquetas)** , seleccione las etiquetas que quiera agregar a este rol. Los usuarios de los grupos de administración tendrán acceso a los objetos de Intune que también tengan la misma etiqueta de ámbito. Puede asignar un máximo de 100 etiquetas de ámbito a un rol.
7. Elija **Siguiente** para ir a la página **Revisar y crear** y, después, seleccione **Crear**.

## <a name="assign-scope-tags-to-other-objects"></a>Asignación de etiquetas de ámbito a otros objetos

En el caso de los objetos que admiten etiquetas de ámbito, estas suelen aparecer en **Propiedades**. Por ejemplo, para asignar una etiqueta de ámbito a un perfil de configuración, siga estos pasos:

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione **Dispositivos** > **Perfiles de configuración** > elija un perfil.

2. Seleccione **Propiedades** > **Ámbito (etiquetas)**  > **Editar** > **Seleccionar etiquetas de ámbito** > elija las etiquetas que quiera agregar al perfil. Puede asignar un máximo de 100 etiquetas de ámbito a un objeto.
4. Elija **Seleccionar** > **Revisar + guardar**.

## <a name="scope-tag-details"></a>Detalles de las etiquetas de ámbito
Al trabajar con etiquetas de ámbito, recuerde estos detalles: 

- Puede asignar etiquetas de ámbito a un tipo de objeto de Intune si el inquilino puede tener varias versiones de ese objeto (como asignaciones de roles o aplicaciones).
  Los objetos de Intune siguientes son excepciones a esta regla y actualmente no admiten etiquetas de ámbito:
    - Perfiles ESP de Windows
    - Identificadores de dispositivos corporativos
    - Dispositivos Autopilot
    - Ubicaciones de cumplimiento de dispositivos
    - Dispositivos Jamf
- Las aplicaciones de VPP y los libros electrónicos asociados al token de VPP heredan las etiquetas de ámbito asignadas al token de VPP asociado.
- Cuando un administrador crea un objeto en Intune, todas las etiquetas de ámbito asignadas a ese administrador se asignan automáticamente al nuevo objeto.
- El RBAC de Intune no se aplica a los roles de Azure Active Directory. Por lo tanto, los roles Administradores de servicios de Intune y Administradores globales tienen acceso de administrador completo a Intune independientemente de las etiquetas de ámbito que tengan.
- Si una asignación de roles no tiene etiqueta de ámbito, el administrador de TI puede ver todos los objetos en función de los permisos de los administradores de TI. Los administradores que no tienen etiquetas de ámbito esencialmente tienen todas las etiquetas de ámbito.
- Solo puede asignar una etiqueta de ámbito que tenga en las asignaciones de roles.
- Solo puede dirigirse a grupos que aparezcan en el Ámbito (grupos) de la asignación de roles.
- Si tiene una etiqueta de ámbito asignada a su rol, no puede eliminar todas las etiquetas de ámbito en un objeto de Intune. Se necesita al menos una etiqueta de ámbito.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo se comportan las etiquetas de ámbito cuando hay [varias asignaciones de roles](role-based-access-control.md#multiple-role-assignments).
Administre sus [roles](role-based-access-control.md) y [perfiles](../configuration/device-profile-assign.md).


