---
title: Asociación de inquilinos del administrador de puntos de conexión de Microsoft
titleSuffix: Configuration Manager
description: Cargue los dispositivos de Configuration Manager en el servicio en la nube y tome medidas del centro de administración.
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: e2b8c07a64265d33ade0b1c2c08c2d9c4096b741
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693462"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Asociación de inquilinos de Microsoft Endpoint Manager: sincronización de dispositivos y acciones de dispositivo
<!--3555758 live 3/4/2020-->
*Se aplica a: Configuration Manager (rama actual)*

Microsoft Endpoint Manager es una solución integrada para administrar todos los dispositivos. Microsoft reúne Configuration Manager e Intune en una única consola denominada **centro de administración de Microsoft Endpoint Manager**.

A partir de Configuration Manager versión 2002, puede cargar los dispositivos Configuration Manager en el servicio en la nube y tomar medidas en la hoja **dispositivos** del centro de administración.

## <a name="prerequisites"></a>Requisitos previos

- Una cuenta que sea un *administrador global* para iniciar sesión cuando aplique este cambio. Para obtener más información, consulte [roles de administrador de Azure Active Directory (Azure ad)](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - La incorporación crea una aplicación de terceros y una entidad de servicio de primera entidad en el inquilino de Azure AD.
- Un entorno de nube pública de Azure.
- Las cuentas de usuario que desencadenan acciones de dispositivo tienen los siguientes requisitos previos:
   - Se ha descubierto con la [detección de usuarios de Azure Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) y la [detección de Active Directory usuario](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
      - Esto significa que la cuenta de usuario debe ser un objeto de usuario sincronizado en Azure AD.
   - El permiso **iniciar Configuration Manager acción** en **tareas remotas** en el centro de administración de Microsoft Endpoint Manager.


## <a name="internet-endpoints"></a>Puntos de conexión de Internet

- `https://aka.ms/configmgrgateway`
- `https://gateway.configmgr.manage.microsoft.com`
- `https://us.gateway.configmgr.manage.microsoft.com`
- `https://eu.gateway.configmgr.manage.microsoft.com`


## <a name="enable-device-upload"></a>Habilitar carga de dispositivo

- Si tiene la administración conjunta habilitada actualmente, [edite las propiedades de administración conjunta](#bkmk_edit) para habilitar la carga del dispositivo.
- Si no tiene la administración conjunta habilitada, [use el Asistente para **configurar la administración conjunta** ](#bkmk_config) para habilitar la carga del dispositivo.
   - Puede cargar los dispositivos sin habilitar la inscripción automática de cargas de trabajo de administración conjunta o cambio en Intune.
- Se cargarán todos los dispositivos administrados por Configuration Manager que tengan el **valor sí** en la columna **cliente** . Si es necesario, puede limitar la carga a una sola recopilación de dispositivos.

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>Editar propiedades de administración conjunta para habilitar la carga de dispositivos

Si tiene la administración conjunta habilitada actualmente, edite las propiedades de administración conjunta para habilitar la carga de dispositivos con las instrucciones siguientes:

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **información general** > **Cloud Services** > **administración conjunta**.
1. Haga clic con el botón derecho en la configuración de administración conjunta y seleccione **propiedades**.
1. En la pestaña **configurar carga** , seleccione **cargar al centro de administración de Microsoft Endpoint Manager**. Haga clic en **Aplicar**.
   - La configuración predeterminada para la carga de dispositivos es **todos mis dispositivos administrados por el punto de conexión de Microsoft Configuration Manager**. Si es necesario, puede limitar la carga a una sola recopilación de dispositivos.

   [![Asistente para configuración de administración conjunta](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. Inicie sesión con su cuenta de *administrador global* cuando se le solicite.
1. Haga clic en **sí** para aceptar la notificación de creación de la **aplicación de AAD** . Esta acción aprovisiona una entidad de servicio y crea un registro de aplicación Azure AD para facilitar la sincronización.
1. Haga clic en **Aceptar** para salir de las propiedades de administración conjunta una vez que haya terminado de realizar los cambios.


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>Usar el Asistente para configurar la administración conjunta para habilitar la carga de dispositivos
Si no tiene la administración conjunta habilitada, use el Asistente para **configurar la administración conjunta** para habilitar la carga del dispositivo. Puede cargar los dispositivos sin habilitar la inscripción automática de cargas de trabajo de administración conjunta o cambio en Intune. Habilite la carga de dispositivos con las instrucciones siguientes:

1. En la consola de administración de Configuration Manager, vaya a **Administración** > **información general** > **Cloud Services** > **administración conjunta**.
1. En la cinta de opciones, haga clic en **configurar la administración conjunta** para abrir el asistente.
1. En la página **incorporación de inquilinos** , seleccione **AzurePublicCloud** para su entorno. Azure Government nube no es compatible.
1. Haga clic en **Iniciar sesión**. Use la cuenta de *administrador global* para iniciar sesión.
1. Asegúrese de que la opción **cargar en el centro de administración de Microsoft Endpoint Manager** está seleccionada en la página **incorporación de inquilinos** .
   - Asegúrese de que la opción **Habilitar la inscripción automática de clientes para la administración conjunta** no está activada si no desea habilitar la administración conjunta ahora. Si desea habilitar la administración conjunta, seleccione la opción.
   - Si habilita la administración conjunta junto con la carga del dispositivo, se le proporcionarán páginas adicionales en el Asistente para completar el asistente. Para más información, consulte [Habilitación de la administración conjunta](../comanage/how-to-enable.md).

   [![Asistente para configuración de administración conjunta](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Haga clic en **siguiente** y luego en **sí** para aceptar la notificación de creación de la **aplicación de AAD** . Esta acción aprovisiona una entidad de servicio y crea un registro de aplicación Azure AD para facilitar la sincronización.
1. En la página **configurar carga** , seleccione la configuración de carga de dispositivo recomendada para **todos mis dispositivos administrados por el punto de conexión de Microsoft Configuration Manager**. Si es necesario, puede limitar la carga a una sola recopilación de dispositivos.
1. Haga clic en **Resumen** para revisar la selección y, a continuación, haga clic en **siguiente**.
1. Una vez completado el asistente, haga clic en **cerrar**.  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>Revisión de la carga

1. Abra **CMGatewaySyncUploadWorker. log** desde &lt;el directorio de instalación de Configuration Manager> \logs.
1. La siguiente hora de sincronización se indica mediante entradas de registro `Next run time will be at approximately: 02/28/2020 16:35:31`similares a.
1. En el caso de las cargas de dispositivo, busque entradas de `Batching N records`registro similares a. **N** es el número de dispositivos que se cargan en la nube. 
1. La carga se produce cada 15 minutos para los cambios. Una vez que se cargan los cambios, los cambios del cliente pueden tardar entre 5 y 10 minutos en aparecer en el **centro de administración de Microsoft Endpoint Manager**.

## <a name="perform-device-actions"></a>Realizar acciones de dispositivo

1. En un explorador, vaya a`endpoint.microsoft.com`
1. Seleccione **dispositivos** y, a continuación, **todos los dispositivos** para ver los dispositivos cargados. Verá **ConfigMgr** en la columna **administrado por** para los dispositivos cargados.
   [![Todos los dispositivos del centro de administración de Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Haga clic en un dispositivo para cargar su página de **información general** .
1. Haga clic en cualquiera de las siguientes acciones:
   - **Sincronizar Directiva de equipo**
   - **Sincronizar Directiva de usuario**
   - **Ciclo de evaluación de la aplicación**

   [![Información general del dispositivo en el centro de administración de Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>Problemas conocidos

### <a name="specific-devices-dont-synchronize"></a>Los dispositivos específicos no se sincronizan

<!--7099564-->
Es posible que determinados dispositivos, que son Configuration Manager clientes, no se carguen en el servicio.

**Dispositivos afectados:** Si un dispositivo es un punto de distribución que usa el mismo certificado PKI para la funcionalidad de punto de distribución y su agente de cliente, el dispositivo no se incluirá en la sincronización de dispositivos de Asociación de inquilinos.

**Comportamiento:** Al realizar la Asociación de inquilinos durante la fase de incorporación, se realiza una sincronización completa la primera vez. Los ciclos de sincronización posteriores son sincronizaciones diferenciales. Cualquier actualización de los dispositivos afectados hará que el dispositivo se quite de la sincronización.

## <a name="log-files"></a>Archivos de registro
Use los registros siguientes ubicados en el punto de conexión de servicio:

- **CMGatewaySyncUploadWorker. log**
- **CMGatewayNotificationWorker. log**

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los archivos de registro de datos adjuntos de inquilinos, consulte [solucionar problemas de Asociación de inquilino](technical-reference.md).
