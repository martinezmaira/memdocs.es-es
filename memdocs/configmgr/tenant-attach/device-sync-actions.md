---
title: Asociación de inquilinos de Microsoft Endpoint Manager
titleSuffix: Configuration Manager
description: Cargue los dispositivos de Configuration Manager en el servicio en la nube y tome medidas del centro de administración.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: bac86ca5a74d35b64e211936806ef1735f4e0eea
ms.sourcegitcommit: 231e2c3913a1d585310dfab7ffcd5c78c6bc5703
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88970471"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo
<!--3555758 live 3/4/2020-->
*Se aplica a: Configuration Manager (rama actual)*

Microsoft Endpoint Manager es una solución integrada para administrar todos los dispositivos. Microsoft reúne Configuration Manager e Intune en una única consola denominada **centro de administración de Microsoft Endpoint Manager**.

A partir de Configuration Manager versión 2002, puede cargar los dispositivos Configuration Manager en el servicio en la nube y tomar medidas en la hoja **dispositivos** del centro de administración.

## <a name="prerequisites"></a>Requisitos previos

- Una cuenta que sea un *administrador global* para iniciar sesión cuando aplique este cambio. Para obtener más información, consulte [roles de administrador de Azure Active Directory (Azure ad)](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - La incorporación crea una aplicación de terceros y una entidad de servicio de primera entidad en el inquilino de Azure AD.
- Un entorno de nube pública de Azure.
- Las cuentas de usuario que desencadenan acciones de dispositivo tienen los siguientes requisitos previos:
   - Se ha descubierto con la [detección de usuarios de Azure Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) y la [detección de Active Directory usuario](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
      - Esto significa que la cuenta de usuario debe ser un objeto de usuario sincronizado en Azure AD.
   - El permiso **iniciar Configuration Manager acción** en **tareas remotas** en el centro de administración de Microsoft Endpoint Manager.
- Si el sitio de administración central tiene un [proveedor remoto](../core/plan-design/hierarchy/plan-for-the-sms-provider.md), siga las instrucciones para el escenario de [CAS tiene un proveedor remoto](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) en el artículo de CMPivot. <!--7796824-->

## <a name="internet-endpoints"></a>Puntos de conexión de Internet

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

El punto de conexión de servicio realiza una conexión saliente de larga duración con estos extremos. Compruebe que el proxy usado para el punto de conexión de servicio no agota el tiempo de espera de las conexiones salientes demasiado rápido. Se recomiendan 3 minutos para las conexiones salientes a estos puntos de conexión de Internet. <!--7820969-->

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a> Habilitar la carga de dispositivos cuando la administración conjunta ya está habilitada

Si tiene la administración conjunta habilitada actualmente, usará las propiedades de administración conjunta para habilitar la carga del dispositivo. Si la administración conjunta todavía no está habilitada, [use el Asistente para **configurar la administración conjunta** ](#bkmk_config) para habilitar la carga del dispositivo en su lugar.

Cuando la administración conjunta ya esté habilitada, edite las propiedades de administración conjunta para habilitar la carga de dispositivos con las instrucciones siguientes:

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).
1. En la cinta de opciones, seleccione **las propiedades** de la Directiva de producción de administración conjunta.
1. En la pestaña **Configure upload** (Configurar carga), seleccione **Upload to Microsoft Endpoint Manager admin center** (Cargar en el centro de administración de Microsoft Endpoint Manager). Seleccione **Aplicar**.
   - El valor predeterminado para la carga de dispositivos es **All my devices managed by Microsoft Endpoint Configuration Manager** (Todos los dispositivos administrados por Microsoft Endpoint Configuration Manager). Si es necesario, puede limitar la carga a una sola recopilación de dispositivos.
1. Active la opción **Habilitar el análisis de puntos de conexión para dispositivos cargados en el administrador de puntos de conexión de Microsoft** si también quiere obtener información para optimizar la experiencia del usuario final en el análisis de puntos de [conexión](../../analytics/overview.md).

   [![Carga de dispositivos en el centro de administración de Microsoft Endpoint Manager](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. Inicie sesión con la cuenta de *administrador global* cuando se le pida.
1. Seleccione **sí** para aceptar la notificación de creación de la **aplicación de AAD** . Esta acción aprovisiona una entidad de servicio y crea un registro de aplicación de Azure AD para facilitar la sincronización.
1. Elija **Aceptar** para salir de las propiedades de administración conjunta una vez que haya terminado de realizar los cambios.


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a> Habilitar la carga de dispositivos cuando la administración conjunta no está habilitada

Si no tiene la administración conjunta habilitada, use el Asistente para **configurar la administración conjunta** para habilitar la carga del dispositivo. Puede cargar los dispositivos sin habilitar la inscripción automática de cargas de trabajo de administración conjunta o cambio en Intune. Se cargarán todos los dispositivos administrados por Configuration Manager que tengan el **valor sí** en la columna **cliente** . Si es necesario, puede limitar la carga a una sola recopilación de dispositivos. Si la administración conjunta ya está habilitada en su entorno, [edite las propiedades de administración conjunta](#bkmk_edit) para habilitar la carga del dispositivo en su lugar.

Si la administración conjunta no está habilitada, siga estas instrucciones para habilitar la carga de dispositivos:

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).
1. En la cinta de opciones, seleccione **configurar la administración conjunta** para abrir el asistente.
1. En la página **Tenant onboarding** (Incorporación de inquilinos), seleccione **AzurePublicCloud** para el entorno. No se admiten Azure Government Cloud y Azure China 21Vianet.
1. Seleccione **Iniciar sesión**. Use la cuenta de *administrador global* para iniciar sesión.
1. Asegúrese de que la opción **cargar en el centro de administración de Microsoft Endpoint Manager** está seleccionada en la página **incorporación de inquilinos** .
   - Asegúrese de que la opción **Habilitar la inscripción automática de clientes para la administración conjunta** no está activada si no desea habilitar la administración conjunta ahora. Si desea habilitar la administración conjunta, seleccione la opción.
   - Si habilita la administración conjunta junto con la carga del dispositivo, se le proporcionarán páginas adicionales en el Asistente para completar el asistente. Para más información, consulte [Habilitación de la administración conjunta](../comanage/how-to-enable.md).

   [![Asistente para configuración de administración conjunta](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Elija **siguiente** y luego **sí** para aceptar la notificación de creación de la **aplicación de AAD** . Esta acción aprovisiona una entidad de servicio y crea un registro de aplicación de Azure AD para facilitar la sincronización.
     - Opcionalmente, puede importar una aplicación Azure AD creada anteriormente durante la incorporación de la Asociación de inquilinos (a partir de la versión 2006). Para obtener más información, consulte la sección [importar una aplicación Azure ad creada anteriormente](#bkmk_aad_app) .
1. En la página **configurar carga** , seleccione la configuración de carga de dispositivo recomendada para **todos mis dispositivos administrados por el punto de conexión de Microsoft Configuration Manager**. Si es necesario, puede limitar la carga a una sola recopilación de dispositivos.
1. Active la opción **Habilitar el análisis de puntos de conexión para dispositivos cargados en el administrador de puntos de conexión de Microsoft** si también quiere obtener información para optimizar la experiencia del usuario final en el análisis de puntos de [conexión](../../analytics/overview.md) .
1. Seleccione **Resumen** para revisar la selección y, a continuación, elija **siguiente**.
1. Cuando el asistente se haya completado, seleccione **cerrar**.  

## <a name="perform-device-actions"></a>Realizar acciones de dispositivo

1. En un explorador, vaya a `endpoint.microsoft.com`
1. Seleccione **dispositivos** y, a continuación, **todos los dispositivos** para ver los dispositivos cargados. Verá **ConfigMgr** en la columna **administrado por** para los dispositivos cargados.
   [![Todos los dispositivos del centro de administración de Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Seleccione un dispositivo para cargar su página de **información general** .
1. Elija cualquiera de las siguientes acciones:
   - **Sincronizar directiva de máquina**
   - **Sincronizar directiva de usuario**
   - **Ciclo de evaluación de aplicaciones**

   [![Información general del dispositivo en el centro de administración de Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a> Importar una aplicación Azure AD creada anteriormente (opcional)
<!--6479246-->
*(Introducido en la versión 2006)*

Durante una [nueva incorporación](#bkmk_config), un administrador puede especificar una aplicación creada anteriormente durante la incorporación a la Asociación de inquilinos. No comparta ni reutilice Azure AD aplicaciones en varias jerarquías. Si tiene varias jerarquías, cree aplicaciones de Azure AD independientes para cada una.

En la página **Incorporación de inquilinos** del **Asistente para la configuración de la administración conjunta**, seleccione **Opcionalmente, importar una aplicación web independiente para sincronizar los datos del cliente de Configuration Manager con el Centro de administración de Microsoft Endpoint Manager**. Esta opción le pedirá que especifique la información siguiente para la aplicación de Azure AD:

- Nombre de inquilino de Azure AD
- Id. de inquilino de Azure AD
- Nombre de la aplicación
- Identificador de cliente
- Clave secreta
- Expiración de la clave secreta
- URI de id. de aplicación

### <a name="azure-ad-application-permissions-and-configuration"></a>Azure AD los permisos y la configuración de la aplicación

El uso de una aplicación creada anteriormente durante la incorporación a la Asociación de inquilinos requiere los siguientes permisos:

- Configuration Manager permisos de microservicio:
   - CmCollectionData. Read
   - CmCollectionData. Write

- Microsoft Graph permisos:
   - Permiso Directory. Read. All [Applications](/graph/permissions-reference#application-permissions)
   - Directory. Read. todos los [permisos de directorio delegado](/graph/permissions-reference#directory-permissions)

- Asegúrese de que **conceder el consentimiento de administrador para el inquilino** está seleccionado para la aplicación Azure ad. Para obtener más información, consulte [conceder consentimiento de administrador en registros de aplicaciones](/azure/active-directory/manage-apps/grant-admin-consent).

- La aplicación importada debe configurarse de la siguiente manera:
   - **Solo se registra para las cuentas de este directorio de la organización**. Para obtener más información, vea [cambiar quién puede tener acceso a la aplicación](/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application).
   -  Tiene un URI de ID. de aplicación y un secreto válidos



## <a name="next-steps"></a>Pasos siguientes

- [Inscripción de dispositivos Configuration Manager en el análisis de puntos de conexión](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- Para obtener información sobre los archivos de registro de datos adjuntos de inquilino, consulte [solucionar problemas de Asociación de inquilinos](troubleshoot.md).