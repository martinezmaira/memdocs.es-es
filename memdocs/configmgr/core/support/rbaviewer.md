---
title: Herramienta de administración basada en roles
titleSuffix: Configuration Manager
description: Use Role-based Administration and Auditing Tool para modelar y auditar ámbitos y roles de seguridad en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff940db21711aabb5d57a45b05d90d04415639bb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707563"
---
# <a name="role-based-administration-and-auditing-tool"></a>Role-based Administration and Auditing Tool

*Se aplica a: Configuration Manager (rama actual)*

Role-based Administration and Auditing Tool es una de las [herramientas de Configuration Manager](tools.md). Utilice esta herramienta para las siguientes tareas:

- Modelar roles de seguridad con permisos específicos  

- Auditar los ámbitos y roles de seguridad que tienen otros usuarios



## <a name="requirements"></a>Requisitos

- Ejecutarla en el mismo equipo que la consola de Configuration Manager  

- Tener el rol **Administrador total**, **Analista de solo lectura** o **Administrador de seguridad**  

- Asignar la cuenta al ámbito de seguridad **Todos** y todas las recopilaciones  

- (*Opcional*) Para analizar la seguridad de la carpeta de informes, debe tener acceso a SQL  

- (*Opcional*) Para analizar el informe detallado, ejecute esta herramienta en el servidor de sistema de sitio con el rol de punto de notificación



## <a name="procedures"></a>Procedimientos


### <a name="model-permissions-for-a-new-role"></a>Modelar permisos para un nuevo rol

Use el procedimiento siguiente para modelar permisos para un nuevo rol que quiere crear: 

1. Ejecute **RBAViewer.exe**.  

2. Seleccione los roles de seguridad base que quiere agregar o comience con un conjunto de permisos vacío. Seleccione los permisos necesarios.  

3. Haga clic en **Analizar** para ver la interfaz de usuario que verá este rol personalizado.  

    > [!Note]  
    > Para ver si existe un rol de seguridad que cumpla sus requisitos, cambie a la pestaña **Similitud**.  

4. Haga clic en **Exportar** para guardar el rol como archivo XML. Luego impórtelo a la consola de Configuration Manager. Para obtener más información, vea [Crear roles de seguridad personalizados](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Auditar ámbitos de seguridad existentes

Utilice el procedimiento siguiente para auditar todos los usuarios administrativos, las recopilaciones y los ámbitos de seguridad existentes en Configuration Manager:

1. Ejecute **RBAViewer.exe**.  

2. Seleccione el botón **Audit RBA** (Auditar RBA) en la barra de herramientas.  

    1. Para ver las relaciones limitadas a la recopilación en una vista de árbol, cambie a la pestaña **Collection Summary** (Resumen de la recopilación).  

    2. Para ver los objetos asignados a un rol de seguridad, cambie a la pestaña **Resumen del ámbito**.  


### <a name="audit-a-specific-user"></a>Auditar un usuario específico

Use el procedimiento siguiente para auditar la configuración de administración basada en roles de un usuario específico:

1. Ejecute **RBAViewer.exe**.  

2. Seleccione el botón **Ejecutar como** en la barra de herramientas.  

3. Escriba el nombre de usuario específico para comprobar los permisos de esa cuenta.  

4. La herramienta muestra los roles de seguridad asignados al usuario o al grupo de seguridad al que el usuario pertenece. También muestra los objetos que puede ver el usuario y las acciones que puede realizar en la consola.  



## <a name="see-also"></a>Vea también

- [Aspectos básicos de la administración basada en roles](../understand/fundamentals-of-role-based-administration.md)
- [Configurar la administración basada en roles](../servers/deploy/configure/configure-role-based-administration.md)
