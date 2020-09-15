---
title: Configurar la administración basada en roles
titleSuffix: Configuration Manager
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
description: Combinación de roles de seguridad, ámbitos de seguridad y recopilaciones asignadas para definir el ámbito administrativo de cada usuario administrativo
ms.openlocfilehash: a475660d2a171829e1592c1c411a3251e74eb79f
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607612"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Configuración de la administración basada en roles para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En Configuration Manager, la administración basada en roles combina roles de seguridad, ámbitos de seguridad y recopilaciones asignadas para definir el ámbito administrativo de cada usuario administrativo. Un ámbito administrativo incluye los objetos que puede ver un usuario administrativo en la consola de Configuration Manager y las tareas relacionadas con esos objetos que el usuario administrativo tiene permiso para realizar. Las configuraciones de la administración basada en roles se aplican en cada sitio en una jerarquía.  

 Si todavía no está familiarizado con los conceptos relacionados con la administración basada en roles, vea [Conceptos básicos de la administración basada en roles](../../../understand/fundamentals-of-role-based-administration.md).  

 La información de los procedimientos siguientes puede ayudarle a crear y configurar la administración basada en roles y la configuración de seguridad relacionada:  

- [Crear roles de seguridad personalizados](#BKMK_CreateSecRole)  
- [Configurar roles de seguridad](#BKMK_ConfigSecRole)  
- [Configurar ámbitos de seguridad para un objeto](#BKMK_ConfigSecScope)  
- [Configurar recopilaciones para administrar la seguridad](#BKMK_ConfigColl)  
- [Crear un nuevo usuario administrativo](#BKMK_Create_AdminUser)  
- [Modify the administrative scope of an administrative user (Modificar el ámbito administrativo de un usuario administrativo)](#BKMK_ModAdminUser)  

## <a name="create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Crear roles de seguridad personalizados

 Configuration Manager proporciona varios roles de seguridad integrados. Si necesita más roles de seguridad, puede crear un rol de seguridad personalizado si crea una copia de un rol de seguridad existente y, a continuación, modifica la copia. Puede crear un rol de seguridad personalizado para conceder a los usuarios administrativos permisos de seguridad adicionales necesarios que no estén incluidos en un rol de seguridad asignado actualmente. Mediante el uso de un rol de seguridad personalizado, puede concederles solamente los permisos que requieran y evitar así la asignación de un rol de seguridad que conceda más permisos de los necesarios.  

 Utilice el procedimiento siguiente para crear un nuevo rol de seguridad mediante el uso de un rol de seguridad existente como plantilla.  

### <a name="to-create-custom-security-roles"></a>Para crear roles de seguridad personalizados

1. En la consola de Configuration Manager, vaya a **Administración**.  

2. En el área de trabajo **Administración**, expanda **Seguridad** y elija **Roles de seguridad**.  

   Utilice uno de los siguientes procesos para crear el nuevo rol de seguridad:  

    - Para crear un nuevo rol de seguridad personalizado, realice las siguientes acciones:  

      1. Seleccione un rol de seguridad existente para usarlo como el origen del nuevo rol de seguridad.
      2. En el grupo **Rol de seguridad** de la pestaña **Inicio**, elija **Copiar**. Esta acción crea una copia del rol de seguridad de origen.  
      3. En el asistente Copiar rol de seguridad, especifique un **Nombre** para el nuevo rol de seguridad personalizado.  
      4. En **Asignaciones de operación de seguridad**, expanda todos los nodos de **Operaciones de seguridad** para mostrar las acciones disponibles.  
      5. Para cambiar el valor de una operación de seguridad, elija la flecha abajo en la columna **Valor** y seleccione **Sí** o **No**.

            > [!CAUTION]  
            > Cuando configure un rol de seguridad personalizado, asegúrese de no conceder permisos que no sean necesarios para los usuarios administrativos asociados al nuevo rol de seguridad. Por ejemplo, el valor **Modificar** para la operación de seguridad **Roles de seguridad** concede a los usuarios administrativos permiso para editar cualquier rol de seguridad accesible, aunque no estén asociados a ese rol de seguridad.  

      6. Después de configurar los permisos, elija **Aceptar** para guardar el nuevo rol de seguridad.  

    - Para importar un rol de seguridad que se haya exportado desde otra jerarquía de Configuration Manager, realice las acciones siguientes:  

        1. En el grupo **Crear** de la pestaña **Inicio**, elija **Importar rol de seguridad**.  
        2. Especifique el archivo .xml que contiene la configuración de rol de seguridad que quiere importar. Elija **Abrir** para completar el procedimiento y guardar el rol de seguridad.  

            > [!NOTE]  
            > Después de importar un rol de seguridad, puede editar las propiedades del rol de seguridad para cambiar los permisos de objeto asociados al rol de seguridad.  

## <a name="configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Configurar roles de seguridad

 Los grupos de permisos de seguridad que se definen para un rol de seguridad se denominan asignaciones de operación de seguridad. Las asignaciones de operación de seguridad representan una combinación de tipos de objetos y acciones que están disponibles para cada tipo de objeto. Puede modificar las operaciones de seguridad que están disponibles para cada rol de seguridad personalizado, pero no puede modificar los roles de seguridad integrados que ofrece Configuration Manager.  

 Utilice el siguiente procedimiento para modificar las operaciones de seguridad para un rol de seguridad.  

### <a name="to-modify-security-roles"></a>Para modificar roles de seguridad

1. En la consola de Configuration Manager, seleccione **Administración**.  
2. En el área de trabajo **Administración**, expanda **Seguridad** y elija **Roles de seguridad**.  
3. Seleccione el rol de seguridad personalizado que desee modificar.  
4. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  
5. Elija la pestaña **Permisos**.  
6. En **Asignaciones de operación de seguridad**, expanda todos los nodos de **Operaciones de seguridad** para mostrar las acciones disponibles.  
7. Para cambiar el valor de una operación de seguridad, elija la flecha abajo en la columna **Valor** y elija **Sí** o **No**.  

    > [!CAUTION]  
    > Cuando configure un rol de seguridad personalizado, asegúrese de no conceder permisos que no sean necesarios para los usuarios administrativos asociados al nuevo rol de seguridad. Por ejemplo, el valor **Modificar** para la operación de seguridad **Roles de seguridad** concede a los usuarios administrativos permiso para editar cualquier rol de seguridad accesible, aunque no estén asociados a ese rol de seguridad.  

8. Cuando haya terminado de configurar las asignaciones de operación de seguridad, elija **Aceptar** para guardar el nuevo rol de seguridad.  

##  <a name="configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Configurar ámbitos de seguridad para un objeto
 La asociación de un ámbito de seguridad a un objeto se administra desde el objeto, no desde el ámbito de seguridad. Las únicas configuraciones directas que admiten los ámbitos de seguridad son los cambios en su nombre y descripción. Para cambiar el nombre y la descripción de un ámbito de seguridad cuando ve las propiedades del ámbito de seguridad, debe tener el permiso **Modificar** en el objeto protegible **Ámbitos de seguridad** .  

 Cuando crea un nuevo objeto en Configuration Manager, se asocia con cada ámbito de seguridad que está asociado con los roles de seguridad de la cuenta utilizada para crear el objeto. Este comportamiento se produce cuando esos roles de seguridad proporcionan el permiso **Crear** o **Establecer ámbito de seguridad**. Puede cambiar los ámbitos de seguridad para el objeto después de crearlo.  

 Por ejemplo, tiene asignado un rol de seguridad que le concede permiso para crear un grupo de límites. Cuando cree un nuevo grupo de límites, no tendrá ninguna opción a la que pueda asignar ámbitos de seguridad específicos. En su lugar, los ámbitos de seguridad disponibles en los roles de seguridad a los que está asociado se asignan automáticamente al nuevo grupo de límites. Después de guardar el nuevo grupo de límites, puede editar los ámbitos de seguridad asociados al nuevo grupo de límites.  

 Utilice el siguiente procedimiento para configurar los ámbitos de seguridad asignados a un objeto.  

### <a name="to-configure-security-scopes-for-an-object"></a><a name="bkmk_config-sec-scope"></a> Para configurar ámbitos de seguridad para un objeto  

1. En la consola de Configuration Manager, seleccione un objeto que admita la asignación a un ámbito de seguridad.  
2. En el grupo **Clasificar** de la pestaña **Inicio**, elija **Establecer ámbitos de seguridad**.
3. En el cuadro de diálogo **Establecer ámbitos de seguridad** , seleccione o quite los ámbitos de seguridad a los que esté asociado este objeto. Cada objeto que admita ámbitos de seguridad debe asignarse a un ámbito de seguridad como mínimo.  
4. Elija **Aceptar** para guardar los ámbitos de seguridad asignados.  

    > [!NOTE]  
    > Cuando cree un nuevo objeto, puede asignar el objeto a varios ámbitos de seguridad. Para modificar el número de ámbitos de seguridad asociados al objeto, debe cambiar esta asignación una vez creado el objeto.

### <a name="to-configure-security-scopes-for-a-folder-starting-in-version-1906"></a><a name="bkmk_config-folder"></a> Para configurar ámbitos de seguridad para una carpeta (a partir de la versión 1906)
<!--3600867-->

1. En la consola de Configuration Manager, seleccione una carpeta.  
1. En la pestaña **Carpeta** de la cinta de opciones, seleccione **Establecer ámbitos de seguridad**.
   - También puede hacer clic con el botón derecho en la carpeta y seleccionar **Carpeta** > **Establecer ámbitos de seguridad**.
1. En el cuadro de diálogo **Establecer ámbitos de seguridad**, seleccione o quite los ámbitos de seguridad de la carpeta. Cada carpeta debe asignarse al menos a un ámbito de seguridad. A todas las carpetas se les asigna el ámbito de seguridad **Predeterminado** hasta que se cambia.
1. Elija **Aceptar** para guardar los ámbitos de seguridad asignados.  

    > [!IMPORTANT]  
    > - Los roles de seguridad existente obtendrán automáticamente los permisos **Clase de carpeta** agregados al instalar la versión 1906 de Configuration Manager. Deberá agregar los permisos **Clase de carpeta** para todos los nuevos roles de seguridad y verificar que los roles existentes tienen los permisos adecuados para el entorno.
    > 
    > - Un elemento se puede buscar en una carpeta fuera del ámbito de seguridad de un usuario si ese usuario comparte un ámbito de seguridad con la persona que creó el objeto. <!--5602690-->

## <a name="configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Configurar recopilaciones para administrar la seguridad

 No hay ningún procedimiento para configurar recopilaciones para la administración basada en roles. Las colecciones no tienen una configuración de administración basada en roles. En su lugar, se asignan colecciones a un usuario administrativo cuando este se configura. Las operaciones de seguridad de colección que se habiliten en los roles de seguridad asignados a los usuarios determinan los permisos que tiene un usuario administrativo en las colecciones y los recursos de colección (miembros de la colección).  

 Cuando un usuario administrativo tiene permisos en una recopilación, también tiene permisos en las recopilaciones limitadas a esa recopilación. Por ejemplo, su organización usa una recopilación denominada Todos los equipos de escritorio. También hay una recopilación denominada Todos los equipos de escritorio de Norteamérica que se limita a la recopilación Todos los equipos de escritorio. Si un usuario administrativo tiene permisos para Todos los equipos de escritorio, también tienen los mismos permisos en la recopilación Todos los equipos de escritorio de Estados Unidos.

 Además, un usuario administrativo no puede usar el permiso **Eliminar** o **Modificar** en una recopilación que se le haya asignado directamente. Pero puede usar estos permisos en las colecciones que están limitadas a esa colección. En el ejemplo anterior, el usuario administrativo puede eliminar o modificar la colección Todos los equipos de escritorio de Estados Unidos, pero no puede eliminar o modificar la colección Todos los equipos de escritorio.  

## <a name="create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Crear un nuevo usuario administrativo

 Para conceder a usuarios individuales o a miembros de un grupo de seguridad acceso para administrar Configuration Manager, cree un usuario administrativo en Configuration Manager y especifique la cuenta de Windows del usuario o grupo de usuarios. Cada usuario administrativo de Configuration Manager debe tener asignado al menos un rol de seguridad y un ámbito de seguridad. También puede asignar recopilaciones para limitar el ámbito administrativo del usuario administrativo.  

 Utilice los procedimientos siguientes para crear nuevos usuarios administrativos.  

### <a name="to-create-a-new-administrative-user"></a>Para crear un nuevo usuario administrativo  

1. En la consola de Configuration Manager, seleccione **Administración**.  
2. En el área de trabajo **Administración**, expanda **Seguridad**y, a continuación, elija **Usuarios administrativos**.  
3. En el grupo **Crear** de la pestaña **Inicio**, elija **Agregar usuario o grupo**.  
4. Elija **Examinar** y luego seleccione la cuenta de usuario o grupo que se utilizará para este nuevo usuario administrativo.  

    > [!NOTE]  
    > Para la administración basada en consola, únicamente los usuarios de dominio o grupos de seguridad pueden especificarse como usuarios administrativos.

5. En **Roles de seguridad asociados**, elija **Agregar** para abrir una lista de roles de seguridad disponibles, active la casilla de uno o varios roles de seguridad y elija **Aceptar**.  

6. Seleccione una de las dos opciones siguientes para definir el comportamiento del objeto protegible para el nuevo usuario:  

    - **Todas las instancias de los objetos que están relacionados con los roles de seguridad asignados**: de forma predeterminada, esta opción asocia el usuario administrativo al ámbito de seguridad **Todo** y a las recopilaciones **Todos los sistemas** y **Todos los usuarios y grupos de usuarios**. Los roles de seguridad que están asignados al usuario definen el acceso a los objetos. Los nuevos objetos que cree este usuario administrativo se asignan al ámbito de seguridad **Predeterminado** .  

    - **Solo las instancias de objetos asignados a los ámbitos y recopilaciones de seguridad especificados**: de forma predeterminada, esta opción asocia el usuario administrativo al ámbito de seguridad **Predeterminado** y a las recopilaciones **Todos los sistemas** y **Todos los usuarios y grupos de usuarios**. Sin embargo, las recopilaciones y los ámbitos de seguridad reales están limitados a aquellos que están asociados a la cuenta que utilizó para crear el nuevo usuario administrativo. Esta opción es compatible con la adición o eliminación de ámbitos de seguridad y recopilaciones para personalizar el ámbito administrativo del usuario administrativo.  

    > [!IMPORTANT]  
    > Las opciones anteriores asocian cada ámbito de seguridad y colección asignado a cada rol de seguridad que se asigne al usuario administrativo. Puede utilizar una tercera opción, **Asociar roles de seguridad asignados con ámbitos y recopilaciones de seguridad específicos**, para asociar roles de seguridad individuales a recopilaciones y ámbitos de seguridad específicos. Esta tercera opción está disponible después de crear el nuevo usuario administrativo, cuando lo modifica.  

7. Según su selección en el paso 6, lleve a cabo la acción siguiente:  

    - Si seleccionó **Todas las instancias de los objetos que están relacionados con los roles de seguridad asignados**, elija **Aceptar** para completar este procedimiento.  

    - Si seleccionó **Solo las instancias de objetos asignados a los ámbitos de seguridad o recopilaciones especificados**, puede elegir **Agregar** para seleccionar más recopilaciones y ámbitos de seguridad. También puede seleccionar uno o más objetos de la lista y luego elegir **Quitar** para quitarlos. Elija **Aceptar** para completar el procedimiento.  

## <a name="modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Modificar el ámbito administrativo de un usuario administrativo

 Para modificar el ámbito administrativo de un usuario administrativo, agregue o quite roles de seguridad, ámbitos de seguridad y recopilaciones que estén asociados al usuario. Cada usuario administrativo debe estar asociado al menos a un rol de seguridad y a un ámbito de seguridad. Es posible que tenga que asignar una o más recopilaciones al ámbito administrativo del usuario. La mayoría de los roles de seguridad interactúan con colecciones y no funcionan correctamente sin una colección asignada.  

 Cuando se modifica un usuario administrativo, puede cambiar el comportamiento en cuanto a cómo se asocian los objetos protegibles a los roles de seguridad asignados. Los tres comportamientos que se pueden seleccionar son los siguientes:  

- **Todas las instancias de los objetos que están relacionados con los roles de seguridad asignados**: de forma predeterminada, esta opción asocia el usuario administrativo al ámbito **Todo** y a las recopilaciones **Todos los sistemas** y **Todos los usuarios y grupos de usuarios**. Los roles de seguridad que están asignados al usuario definen el acceso a los objetos.  

- **Solo las instancias de objetos asignados a los ámbitos y recopilaciones de seguridad especificados**: esta opción asocia el usuario administrativo a los mismos ámbitos de seguridad y recopilaciones que están asociados a la cuenta utilizada para configurar el usuario administrativo. Esta opción es compatible con la adición o eliminación de roles de seguridad y recopilaciones para personalizar el ámbito administrativo del usuario administrativo.  

- **Asociar roles de seguridad asignados con ámbitos y recopilaciones de seguridad específicos**: esta opción le permite crear asociaciones específicas entre roles de seguridad individuales y ámbitos de seguridad y recopilaciones específicos para el usuario.  

    > [!NOTE]  
    > Esta opción está disponible solamente cuando modifica las propiedades de un usuario administrativo.  

La configuración actual del comportamiento del objeto protegible cambia el proceso que se utiliza para asignar roles de seguridad adicionales. Utilice los procedimientos siguientes basados en las distintas opciones de objetos protegibles para administrar un usuario administrativo.  

Use el procedimiento siguiente para ver y administrar la configuración de los objetos protegibles para un usuario administrativo.  

### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Para ver y administrar el comportamiento de los objetos protegibles para un usuario administrativo  

1. En la consola de Configuration Manager, seleccione **Administración**.  
2. En el área de trabajo **Administración**, expanda **Seguridad**y, a continuación, elija **Usuarios administrativos**.  
3. Seleccione el usuario administrativo que desee modificar.  
4. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  
5. Elija la pestaña **Ámbitos de seguridad** para ver la configuración actual de los objetos protegibles para este usuario administrativo.  
6. Para modificar el comportamiento de los objetos protegibles, seleccione una opción nueva para el comportamiento de los objetos protegibles. Después de cambiar esta configuración, vea el correspondiente procedimiento para obtener más información para configurar colecciones y ámbitos de seguridad y roles de seguridad para este usuario administrativo.  
7. Haga clic en **Aceptar** para completar el procedimiento.  

Use el siguiente procedimiento para modificar un usuario administrativo que tenga el comportamiento de objetos protegibles establecido en **Todas las instancias de los objetos que están relacionados con los roles de seguridad asignados**.  

### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Para la opción: Todas las instancias de los objetos que están relacionados con los roles de seguridad asignados  

1. En la consola de Configuration Manager, seleccione **Administración**.  
2. En el área de trabajo **Administración**, expanda **Seguridad**y, a continuación, elija **Usuarios administrativos**.  
3. Seleccione el usuario administrativo que desee modificar.  
4. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  
5. Elija la pestaña **Ámbitos de seguridad** para confirmar que el usuario administrativo esté configurado con **Todas las instancias de los objetos que están relacionados con los roles de seguridad asignados**.  
6. Para modificar los roles de seguridad asignados, elija la pestaña **Roles de seguridad**.  

    - Para asignar roles de seguridad adicionales a este usuario administrativo, elija **Agregar**, active la casilla de cada rol de seguridad adicional que desee asignar y elija **Aceptar**.  
    - Para quitar roles de seguridad, seleccione uno o varios roles de seguridad de la lista y luego elija **Quitar**.

7. Para modificar el comportamiento de los objetos protegibles, elija la pestaña **Ámbitos de seguridad** y seleccione otra opción para el comportamiento de los objetos protegibles. Después de cambiar esta configuración, vea el correspondiente procedimiento para obtener más información para configurar colecciones y ámbitos de seguridad y roles de seguridad para este usuario administrativo.  

    > [!NOTE]  
    > Cuando el comportamiento de objetos protegibles se establece en **Todas las instancias de los objetos que están relacionados con los roles de seguridad asignados**, no puede agregar ni quitar recopilaciones ni ámbitos de seguridad específicos.  

8. Elija **Aceptar** para completar el procedimiento.  

Use el siguiente procedimiento para modificar un usuario administrativo que tenga el comportamiento de objetos protegibles establecido en **Solo las instancias de objetos asignados a los ámbitos de seguridad o recopilaciones especificados**.  

### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Para la opción: Solo las instancias de objetos asignados a los ámbitos y recopilaciones de seguridad especificados  

1. En la consola de Configuration Manager, seleccione **Administración**.  
2. En el área de trabajo **Administración**, expanda **Seguridad**y, a continuación, elija **Usuarios administrativos**.  
3. Seleccione el usuario administrativo que desee modificar.  
4. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  
5. Elija la pestaña **Ámbitos de seguridad** para confirmar que el usuario esté configurado con **Solo las instancias de objetos asignados a los ámbitos de seguridad o recopilaciones especificados**.  
6. Para modificar los roles de seguridad asignados, elija la pestaña **Roles de seguridad**.  

    - Para asignar roles de seguridad adicionales a este usuario, elija **Agregar**, active la casilla de cada rol de seguridad adicional que desee asignar y elija **Aceptar**.  
    - Para quitar roles de seguridad, seleccione uno o varios roles de seguridad de la lista y luego elija **Quitar**.  
7. Para modificar las colecciones y los ámbitos de seguridad asociados a roles de seguridad, elija la pestaña **Ámbitos de seguridad**.  

    - Para asociar nuevos ámbitos de seguridad o colecciones a todos los roles de seguridad que estén asignados a este usuario administrativo, elija **Agregar** y seleccione una de las cuatro opciones. Si seleccionó **Ámbito de seguridad** o **Colección**, active la casilla de uno o más objetos para completar esa selección y luego elija **Aceptar**.  
    - Para quitar un ámbito de seguridad o colección, elija el objeto y luego, **Quitar**.

8. Elija **Aceptar** para completar el procedimiento.  

Use el siguiente procedimiento para modificar un usuario administrativo que tenga el comportamiento de objetos protegibles establecido en **Asociar roles de seguridad asignados con ámbitos y recopilaciones de seguridad específicos**.  

### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Para la opción: Asociar roles de seguridad asignados con ámbitos y recopilaciones de seguridad específicos  

1. En la consola de Configuration Manager, seleccione **Administración**.  
2. En el área de trabajo **Administración**, expanda **Seguridad**y, a continuación, elija **Usuarios administrativos**.  
3. Seleccione el usuario administrativo que desee modificar.  
4. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  
5. Elija la pestaña **Ámbitos de seguridad** para confirmar que el usuario administrativo esté configurado con **Asociar roles de seguridad asignados con ámbitos y recopilaciones de seguridad específicos**.  
6. Para modificar los roles de seguridad asignados, elija la pestaña **Roles de seguridad**.  

    - Para asignar roles de seguridad adicionales a este usuario administrativo, elija **Agregar**. En el cuadro de diálogo **Agregar rol de seguridad**, seleccione uno o varios roles de seguridad disponibles, elija **Agregar** y seleccione el tipo de objeto que desea asociar a los roles de seguridad seleccionados. Si seleccionó **Ámbito de seguridad** o **Colección**, active la casilla de uno o más objetos para completar esa selección y luego elija **Aceptar**.  

        > [!NOTE]  
        > Debe configurar al menos un ámbito de seguridad para que se puedan asignar los roles de seguridad seleccionados al usuario administrativo. Al seleccionar varios roles de seguridad, cada ámbito de seguridad y recopilación que se configure está asociado a cada uno de los roles de seguridad seleccionados.  

    - Para quitar roles de seguridad, seleccione uno o varios roles de seguridad de la lista y luego elija **Quitar**.  

7. Para modificar las colecciones y los ámbitos de seguridad asociados a un rol de seguridad específico, elija la pestaña **Ámbitos de seguridad**, seleccione el rol de seguridad y elija **Editar**.  

    - Para asociar nuevos objetos a este rol de seguridad, elija **Agregar** y seleccione un tipo de objeto para asociarlo a los roles de seguridad seleccionados. Si seleccionó **Ámbito de seguridad** o **Colección**, active la casilla de uno o más objetos para completar esa selección y luego elija **Aceptar**.  

        > [!NOTE]  
        > Debe configurar al menos un ámbito de seguridad.  

    - Para quitar una colección o un ámbito de seguridad que esté asociado a este rol de seguridad, seleccione el objeto y elija **Quitar**.  

    - Cuando haya terminado de modificar los objetos asociados, elija **Aceptar**.  

8. Elija **Aceptar** para completar el procedimiento.  

    > [!CAUTION]  
    > Cuando un rol de seguridad concede a usuarios administrativos el permiso de implementación de recopilaciones, dichos usuarios administrativos pueden distribuir objetos de cualquier ámbito de seguridad para el que tengan permisos de **lectura** de objetos, incluso si ese ámbito de seguridad está asociado a un rol de seguridad diferente.  

## <a name="next-steps"></a>Pasos siguientes

[Cuentas que se usan en Configuration Manager](../../../plan-design/hierarchy/accounts.md)
