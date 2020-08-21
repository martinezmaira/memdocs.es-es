---
title: Creación de recopilaciones
titleSuffix: Configuration Manager
description: Cree recopilaciones en Configuration Manager para facilitar la administración de grupos de usuarios y dispositivos.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5606d7bb5656fe4616ba416836dab2c04c490cfa
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693308"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Creación de recopilaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las recopilaciones son grupos de usuarios o dispositivos. Use recopilaciones para tareas como administrar aplicaciones, implementar la configuración de cumplimiento o instalar actualizaciones de software. También puede utilizar las recopilaciones para administrar grupos de configuraciones de cliente o usarlas con administración basada en roles para especificar recursos a los que puede un usuario administrativo puede acceder. Configuration Manager contiene varias recopilaciones integradas. Para obtener más información, consulte [Introduction to collections](introduction-to-collections.md) (Introducción a las recopilaciones).  

> [!NOTE]  
> Una recopilación puede contener usuarios o dispositivos, pero no ambos.  


La información de este artículo puede ayudarlo a crear recopilaciones en Configuration Manager. También puede importar recopilaciones creadas en este u otro sitio de Configuration Manager. Para obtener información acerca de cómo exportar las recopilaciones, vea [Administración de recopilaciones en Configuration Manager](manage-collections.md).  


## <a name="collection-rules"></a>Reglas de recopilación

Hay diferentes tipos de reglas que puede usar para configurar los miembros de una recopilación en Configuration Manager.  


### <a name="direct-rule"></a>Regla directa

Use reglas directas para elegir los usuarios o equipos que quiera agregar a una recopilación. La pertenencia no cambia a menos que quite un recurso de Configuration Manager. Configuration Manager debe haber detectado los recursos o se deben haber importado antes de poderlos agregar a una recopilación de regla directa. Las recopilaciones de reglas directas tienen una mayor carga administrativa que las recopilaciones de reglas de consulta porque requieren cambios manuales.


### <a name="query-rule"></a>Regla de consulta

Actualice de forma dinámica la pertenencia de una recopilación basándose en una consulta que Configuration Manager ejecuta según una programación. Por ejemplo, puede crear una recopilación de usuarios que sean miembros de la unidad organizativa Recursos humanos de los Servicios de dominio de Active Directory. Esta recopilación se actualiza automáticamente cuando se agregan usuarios nuevos o se quitan usuarios de la unidad organizativa Recursos humanos.

Para ver ejemplos de consultas que puede usar para crear recopilaciones, consulte [Cómo crear consultas](../../../servers/manage/create-queries.md).


### <a name="device-category-rule"></a>Regla de categoría de dispositivos

Puede facilitar la administración de los dispositivos mediante la asociación de las categorías de dispositivos con las recopilaciones de dispositivos. 

Para más información, vea [Cómo clasificar automáticamente dispositivos en recopilaciones](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regla de inclusión de recopilación

Incluya los miembros de otra recopilación en una recopilación de Configuration Manager. Configuration Manager actualiza la pertenencia de la recopilación actual según una programación si cambia la recopilación incluida.

Puede agregar varias reglas de inclusión de recopilación a una recopilación.


### <a name="exclude-collection-rule"></a>Regla de exclusión de recopilación

Las reglas de exclusión de recopilación le permiten excluir a los miembros de una recopilación de otra recopilación de Configuration Manager. Configuration Manager actualiza la pertenencia de la recopilación actual según una programación si cambia la recopilación excluida.

Puede agregar varias reglas de exclusión de recopilación a una recopilación. Si una recopilación incluye tanto reglas de inclusión de recopilación como reglas de exclusión de recopilación y se produce un conflicto, la regla de exclusión tiene prioridad.

#### <a name="example"></a>Ejemplo
se crea una recopilación que tiene una regla de inclusión de recopilación y una regla de exclusión de recopilación. La regla de inclusión de recopilación es para una recopilación de equipos de escritorio de Dell. La de exclusión de recopilación es una recopilación de equipos que tienen menos de 4 GB de RAM. La nueva recopilación contiene los equipos de escritorio Dell que tengan al menos 4 GB de RAM.



## <a name="create-a-collection"></a><a name="bkmk_create"></a> Creación de una recopilación  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**.  

    - Para crear una *recopilación de dispositivos*, seleccione el nodo **Recopilaciones de dispositivos**. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear recopilación de dispositivos**.  

    - Para crear una *recopilación de usuarios*, seleccione el nodo **Recopilaciones de usuarios**. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, haga clic en **Crear recopilación de usuarios**.  

2. En la página **General** del asistente, proporcione un **Nombre** y un **Comentario**. En la sección **Recopilación de restricción**, elija **Examinar** y seleccione una recopilación de restricción. La recopilación que está creando solo contendrá miembros de la recopilación de restricción.  

4. En la página **Reglas de pertenencia**, en la lista **Agregar regla**, seleccione el tipo de regla de pertenencia que quiere usar para esta recopilación. Puede configurar varias reglas para cada recopilación. La configuración para cada regla varía. Para más información sobre cómo configurar cada regla, consulte las secciones siguientes de este artículo:  
    - [Regla directa](#bkmk-direct)
    - [Regla de consulta](#bkmk-query)
    - [Regla de categoría de dispositivos](#bkmk-category)
    - [Regla de inclusión de recopilación](#bkmk-include)
    - [Regla de exclusión de recopilación](#bkmk-exclude)

5. También en la página **Reglas de pertenencia**, revise la configuración siguiente:

    - **Usar actualizaciones incrementales para esta recopilación**: Seleccione esta opción para buscar y actualizar periódicamente solo recursos nuevos o modificados desde la evaluación de recopilación anterior. Este proceso es independiente de una evaluación de recopilación completa. Las actualizaciones incrementales se producen en intervalos de 5 minutos de manera predeterminada.  

        > [!IMPORTANT]  
        >  Las recopilaciones con reglas de consulta que usan las clases siguientes no admiten las actualizaciones incrementales:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (solo para las recopilaciones de usuarios)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (solo para las recopilaciones de usuarios)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Programar una actualización completa en esta recopilación**: programe una evaluación completa regular de la pertenencia a la recopilación.  

        A partir de la versión 1810, los siguientes cambios en el comportamiento de evaluación de las recopilaciones pueden mejorar el rendimiento del sitio:<!--3607726-->  

        - Anteriormente, cuando se configuraba una programación de una recopilación basada en consultas, el sitio continuaba con la evaluación de la consulta aunque habilitara o no la configuración de la recopilación como **Programar una actualización completa en esta recopilación**. Para deshabilitar completamente la programación, tenía que cambiar la programación a **Ninguna**.

            Ahora el sitio elimina la programación cuando se deshabilita esta configuración. Para especificar una programación de evaluación de recopilación, habilite la opción para **Programar una actualización completa en esta recopilación**.  

            Al actualizar el sitio, en cualquier recopilación existente en la que se especifica una programación, el sitio habilita la opción para **Programar una actualización completa en esta recopilación**. Aunque puede que su intención no sea esta configuración, era el comportamiento real de la programación antes de actualizar el sitio. Para que el sitio deje de evaluar una recopilación según una programación, deshabilite esta opción.  

        - No puede deshabilitar la evaluación de las recopilaciones integradas como **Todos los sistemas**, pero ahora puede configurar la programación. Este comportamiento permite personalizar esta acción en el momento en que se cumplen sus requisitos. 

            > [!TIP]  
            > En las recopilaciones integradas, cambie solo la **hora** de la programación personalizada. No cambie el **Patrón de periodicidad**. Las iteraciones futuras pueden exigir un patrón de periodicidad específico.  

6. Complete el asistente para crear la nueva recopilación. La nueva recopilación se muestra en el nodo **Recopilaciones de dispositivos** del área de trabajo **Activos y compatibilidad** .  

> [!NOTE]  
> Debe actualizar o volver a cargar la consola de Configuration Manager para ver los miembros de la recopilación. No aparecen en la recopilación hasta después de la primera actualización programada. Puede seleccionar también manualmente **Actualizar pertenencia** para la recopilación. La actualización de la recopilación puede tardar unos minutos en completarse.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a> Configuración de una regla directa  

1. En la página **Buscar recursos** del **Asistente para crear reglas de pertenencia directa**, especifique la información siguiente:  

    - **Clase de recurso:** seleccione el tipo de recurso que quiera buscar y agregar a la recopilación. Por ejemplo:
        - **Recurso del sistema**: busque datos de inventario devueltos de los equipos cliente.
        - **Equipo desconocido**: seleccione entre los valores devueltos por equipos desconocidos.
        - **Recurso de usuario**: busque información de usuario recopilada por Configuration Manager.
        - **Recurso de grupo de usuarios**: busque información de grupo de usuarios recopilada por Configuration Manager.

    - **Nombre de atributo**: seleccione el atributo asociado a la clase de recurso seleccionado que quiera buscar. Por ejemplo:  

        - Si quiere seleccionar equipos por su nombre NETBIOS, seleccione **Recurso del sistema** en la lista **Clase de recurso** y **Nombre NETBIOS** en la lista **Nombre de atributo**.  

        - Si quiere seleccionar usuarios por su nombre de unidad organizativa (UO), seleccione **Recurso de usuario** en la lista **Clase de recurso** y **Nombre de OU de usuario** en la lista **Nombre de atributo**.  

    - **Excluir recursos marcados como obsoletos**: si un equipo cliente está marcado como obsoleto, no incluya este valor en los resultados de la búsqueda.  

    - **Excluir recursos que no tengan instalado el cliente de Configuration Manager**: estos recursos no se mostrarán en los resultados de búsqueda.  

    - **Valor**: escriba un valor para buscar el nombre del atributo seleccionado. Use el carácter de porcentaje (%) como carácter comodín. Por ejemplo:  
        - Para buscar equipos que tengan un nombre NETBIOS que comience por "M", escriba **M%** en este campo.  
        - Para buscar usuarios en la UO de Contoso, escriba **Contoso** en este campo.

2. En la página **Seleccionar recursos**, seleccione los recursos que quiere agregar a la recopilación en la lista **Recursos** y luego elija **Siguiente**.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a> Configuración de una regla de consulta  

En el cuadro de diálogo **Propiedades de regla de consulta**, especifique la siguiente información:  

- **Nombre**: especifique un nombre único para la consulta.  

- **Importar instrucción de consulta**: abre el cuadro de diálogo **Examinar consulta**. Seleccione una [consulta de Configuration Manager](../../../servers/manage/create-queries.md) para usarla como la regla de consulta de la colección.   

- **Clase de recurso:** seleccione el tipo de recurso que quiera buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso del sistema** para buscar datos de inventario devueltos por los equipos cliente, o **Equipo desconocido** para seleccionar entre los valores devueltos por equipos desconocidos.  

- **Editar instrucción de consulta**: abre el cuadro de diálogo **Propiedades de instrucción de consulta**, donde puede crear una consulta para usarla como regla para la recopilación. Para más información sobre las consultas, vea [Introducción a las consultas](../../../servers/manage/introduction-to-queries.md).  

    > [!TIP]  
    > En la pestaña General, al activar la casilla **Omitir filas duplicadas (seleccionar distinto)** , pueden devolverse menos filas y los resultados se pueden obtener más rápido.

### <a name="device-category-rule"></a><a name="bkmk-category"></a> Regla de categoría de dispositivos

Las siguientes acciones están disponibles en la ventana **Seleccionar categorías de dispositivos**:

- **Crear**: especifique un nombre para crear una categoría.
- **Cambiar nombre**: cambie el nombre de la categoría seleccionada.
- **Eliminar**: seleccione una o varias categorías y use esta acción para quitarlas de la lista.

Para más información, vea [Cómo clasificar automáticamente dispositivos en recopilaciones](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a> Configuración de una regla de inclusión de recopilación  

En el cuadro de diálogo **Seleccionar recopilaciones**, seleccione las recopilaciones que quiere incluir en la nueva recopilación y después elija **Aceptar**.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a> Configuración de una regla de exclusión de recopilación  

En el cuadro de diálogo **Seleccionar recopilaciones**, seleccione las recopilaciones que quiere excluir de la nueva recopilación y después elija **Aceptar**.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a> Importación de una recopilación  

Cuando se exporta una recopilación de un sitio, Configuration Manager la guarda como un archivo Managed Object Format (MOF). Utilice este procedimiento para importar ese archivo en la base de datos del sitio. Para completar este procedimiento, debe **crear** permisos en la clase de recopilaciones.

> [!IMPORTANT]  
> - Asegúrese de que el archivo solo contenga datos de la recopilación, proceda de un origen de confianza y no se haya manipulado.  
> 
> - Asegúrese de que el archivo se exportó desde un sitio que ejecuta la misma versión de Configuration Manager que usa.  

Para obtener más información acerca de cómo exportar las colecciones, vea [Administración de recopilaciones en Configuration Manager](manage-collections.md).


1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Seleccione el nodo **Recopilaciones de usuarios** o **Recopilaciones de dispositivos**.  

2. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Importar recopilaciones**.  

3. En la página **General** del **Asistente para importar recopilaciones**, haga clic en **Siguiente**.  

4. En la página **Nombre de archivo MOF**, seleccione **Examinar**. Busque el archivo MOF que contenga la información de la recopilación que quiera importar.  

5. Complete el asistente para importar la recopilación. La nueva recopilación se muestra en el nodo **Recopilaciones de usuarios** o **Recopilaciones de dispositivos** del área de trabajo **Activos y compatibilidad** . Actualice o vuelva a cargar la consola de Configuration Manager para ver los miembros de la recopilación recién importada.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a> Sincronización de los resultados de pertenencia a recopilaciones con grupos de Azure Active Directory

<!--3607475-->
> [!Tip]  
> Esta característica se introdujo por primera vez en la versión 1906 como una [característica de versión preliminar](../../../servers/manage/pre-release-features.md). A partir de la versión 2002, ya no es de versión preliminar.  

Puede habilitar la sincronización de las pertenencias a recopilaciones con un grupo de Azure Active Directory (Azure AD). Esta sincronización permite usar las reglas de agrupación locales existentes en la nube mediante la creación de pertenencias a grupos de Azure AD en función de los resultados de la pertenencia a recopilaciones. Puede sincronizar recopilaciones de dispositivos. Solo los dispositivos con un registro de Azure Active Directory se reflejan en el grupo de Azure AD. Se admiten tanto los dispositivos unidos a Azure Active Directory como los unidos a Azure HD híbrido.

La sincronización con Azure AD se realiza cada cinco minutos. Es un proceso unidireccional, desde Configuration Manager a Azure AD. Los cambios realizados en Azure AD no se reflejan en las recopilaciones de Configuration Manager, pero Configuration Manager no las sobrescribe. Por ejemplo, si la recopilación de Configuration Manager tiene dos dispositivos y el grupo de Azure AD tiene tres dispositivos diferentes, después de la sincronización el grupo de Azure AD tendrá cinco dispositivos.

### <a name="prerequisites"></a>Requisitos previos

- Integración con Azure AD para [Administración en la nube](../../../servers/deploy/configure/azure-services-wizard.md)
- [Detección de usuarios de Azure Active Directory](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- Punto de administración habilitado para HTTPS o [HTTP mejorado](../../../plan-design/hierarchy/enhanced-http.md)
- Acceso a la recopilación **Todos los sistemas**

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Creación de un grupo y establecimiento del propietario en Azure AD

1. Vaya a [https://portal.azure.com](https://portal.azure.com).
1. Vaya a **Azure Active Directory** > **Grupos** > **Todos los grupos**.
1. Haga clic en **Nuevo grupo** y especifique los valores de **Nombre del grupo** y, opcionalmente, **Descripción del grupo**.
1. Asegúrese de que **Tipo de pertenencia** es **Asignado**.
1. Seleccione **Propietarios** y, luego, agregue la identidad que creará la relación de sincronización en Configuration Manager.
1. Haga clic en **Crear** para completar la creación del grupo de Azure AD.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Habilitación de la sincronización de recopilaciones para el servicio de Azure

1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios en la nube** > **Servicios de Azure**.
1. Haga clic con el botón derecho en el inquilino de Azure AD donde creó el grupo y seleccione **Propiedades**.
1. En la pestaña **Sincronización de recopilaciones**, active la casilla de la opción **Enable Azure Directory Group Sync** (Habilitar la sincronización de grupos de Azure Directory).
1. Haga clic en **Aceptar** para guardar la configuración.

### <a name="enable-the-collection-to-synchronize"></a>Habilitación de la recopilación para sincronizar

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Recopilaciones de dispositivos**.
1. Haga clic en la recopilación que se va a sincronizar y, luego, haga clic en **Propiedades**. 
1. En la pestaña **Sincronización en la nube**, haga clic en **Agregar**.
1. En el menú desplegable, seleccione el **inquilino** donde creó el grupo de Azure AD.
1. Escriba los criterios de búsqueda en el campo **El nombre empieza por** y, luego, haga clic en **Buscar**.
  - Si se le pide iniciar sesión, use la identidad que especificó como el propietario del grupo de Azure AD.
1. Seleccione el grupo de destino, haga clic en **Aceptar** para agregar el grupo y nuevamente en **Aceptar** para salir de las propiedades de la recopilación.
1. Tendrá que esperar unos 5 o 7 minutos antes de poder comprobar las pertenencias a un grupo en Azure Portal.
   - Para iniciar una sincronización completa, haga clic con el botón derecho en la recopilación y, luego, seleccione **Synchronize Membership** (Sincronizar pertenencia).


### <a name="verify-the-azure-ad-group-membership"></a>Compruebe la pertenencia a un grupo de Azure AD

1. Vaya a [https://portal.azure.com](https://portal.azure.com).
1. Vaya a **Azure Active Directory** > **Grupos** > **Todos los grupos**.
1. Busque el grupo que creó y seleccione **Miembros**. 
1. Confirme que los miembros reflejan los de la recopilación de Configuration Manager.
   - E el grupo solo se mostrarán los dispositivos con identidad de Azure AD.


![Sincronización de recopilaciones con Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Con PowerShell

Puede usar PowerShell para crear e importar las recopilaciones. Para obtener más información, vea:

* [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Pasos siguientes

[Administración de recopilaciones](manage-collections.md)