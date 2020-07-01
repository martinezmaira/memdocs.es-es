---
title: Configurar los servicios de Azure
titleSuffix: Configuration Manager
description: Conecte el entorno de Configuration Manager con los servicios de Azure para la administración en la nube, Microsoft Store para Empresas y Log Analytics.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6ca5307de5c7df54c3cf7924bc91b0175b1bfa39
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715329"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configuración de servicios de Azure para utilizarlos con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use el **Asistente para servicios de Azure** para simplificar el proceso de configuración de Azure Cloud Services que se usan con Configuration Manager. Este asistente proporciona una experiencia de configuración común mediante registros de aplicación web de Azure Active Directory (Azure AD). Estas aplicaciones proporcionan detalles de suscripción y configuración, y autentican la comunicación con Azure AD. La aplicación evita tener que escribir esta misma información cada vez que se configura un servicio o componente nuevo de Configuration Manager con Azure.

## <a name="available-services"></a>Servicios disponibles

Configure los servicios de Azure siguientes mediante este asistente:  

- **Administración en la nube**: este servicio permite al sitio y a los clientes autenticarse mediante Azure AD. Esta autenticación habilita otros escenarios, como:  

  - [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](../../../clients/deploy/deploy-clients-cmg-azure.md).  

  - [Configuración de la detección de usuarios de Azure AD](configure-discovery-methods.md#azureaadisc).  

  - [Configuración de la detección de grupos de usuarios de Azure AD](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - Admitir algunos [escenarios de Cloud Management Gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios).  

  - [Notificaciones por correo electrónico de aprobación de aplicaciones](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Conector de Log Analytics**: [conéctese a Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm). Sincronice los datos de la recopilación con Log Analytics.  

    > [!Note]  
    > Este artículo se refiere al *conector de Log Analytics*, que anteriormente se denominaba *conector de OMS*. No hay ninguna diferencia funcional. Para obtener más información, vea [Administración de Azure: supervisión](https://docs.microsoft.com/azure/azure-monitor/terminology#log-analytics).  

- **Microsoft Store para Empresas**: conéctese a [Microsoft Store para Empresas](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md). Obtenga aplicaciones de la tienda para la organización que se puedan implementar con Configuration Manager.  

### <a name="service-details"></a>Detalles del servicio

En la tabla siguiente se muestran detalles sobre cada uno de los servicios.  

- **Inquilinos**: el número de instancias de servicio que se puede configurar. Cada instancia debe ser un inquilino de Azure AD distinto.  

- **Nubes**: todos los servicios admiten la nube de Azure global, pero no todos son compatibles con las nubes privadas, como la nube Azure Gobierno de EE. UU.  

- **Aplicación web**: si el servicio usa una aplicación de Azure AD de tipo *Aplicación web o API*, también denominada "aplicación de servidor" en Configuration Manager.  

- **Aplicación nativa**: si el servicio usa una aplicación de Azure AD de tipo *Nativa*, también denominada "aplicación cliente" en Configuration Manager.  

- **Acciones**: si estas aplicaciones se pueden importar o crear en el Asistente para servicios de Azure de Configuration Manager.  

|Servicio  |Inquilinos  |Nubes  |Aplicación web  |Aplicación nativa  |Acciones  |
|---------|---------|---------|---------|---------|---------|
|Administración en la nube con<br>Detección de Azure AD | Varios | Pública, Privada | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | Importar, Crear |
|Conector de Log Analytics | Uno | Pública, Privada | ![Compatible.](media/green_check.png) | ![No compatible](media/Red_X.png) | Importar |
|Microsoft Store para<br>Business | Uno | Público | ![Compatible.](media/green_check.png) | ![No compatible](media/Red_X.png) | Importar, Crear |

### <a name="about-azure-ad-apps"></a>Acerca de las aplicaciones de Azure AD

Cada servicio de Azure requiere configuraciones distintas, que se establecen en Azure Portal. Además, las aplicaciones para cada servicio pueden requerir permisos distintos a los recursos de Azure.  

Puede usar una única aplicación para más de un servicio. Solo hay un objeto para administrar en Configuration Manager y Azure AD. Cuando caduca la clave de seguridad en la aplicación, basta con actualizar una clave.

Al crear servicios adicionales de Azure en el asistente, Configuration Manager está diseñado para reutilizar la información que es común entre los servicios. Este comportamiento evita la necesidad de especificar varias veces la misma información.

Para obtener más información sobre los permisos de aplicación necesarios y las configuraciones para cada servicio, vea el artículo correspondiente de Configuration Manager en [Servicios disponibles](#available-services).

Para obtener más información sobre las aplicaciones de Azure, empiece con los artículos siguientes:

- [Autenticación y autorización en Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)
- [Introducción a Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)
- [Conceptos básicos sobre el registro de una aplicación en Azure AD](/azure/active-directory/develop/authentication-scenarios)  
- [Integración de aplicaciones con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>Antes de comenzar

Una vez decidido el servicio al que quiere conectarse, consulte la tabla de la sección [Detalles del servicio](#service-details). En esta tabla se proporciona la información necesaria para completar el Asistente para servicios de Azure. Primero, consúltelo con el administrador de Azure AD. Decida cuál de las siguientes acciones quiere emprender:

- Cree las aplicaciones manualmente y de antemano en Azure Portal. Después, importe los detalles de la aplicación en Configuration Manager.  

- Use Configuration Manager para crear las aplicaciones directamente en Azure AD. Para recopilar los datos necesarios de Azure AD, revise la información de las demás secciones de este artículo.  

Algunos servicios requieren que las aplicaciones de Azure AD tengan permisos específicos. Revise la información de cada servicio para determinar los permisos necesarios. Por ejemplo, para poder importar una aplicación web, un administrador de Azure debe crearla primero en [Azure Portal](https://portal.azure.com).

Al configurar el conector de Log Analytics, conceda permisos de *colaborador* a la aplicación web recién registrada en el grupo de recursos que contiene el área de trabajo pertinente. Este permiso permite que Configuration Manager tenga acceso a esa área de trabajo. Al asignar el permiso, busque el nombre del registro de aplicación en el área **Agregar usuarios** de Azure Portal. Este proceso es el mismo que la [concesión de permisos a Configuration Manager para acceder a Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Un administrador de Azure debe asignar estos permisos antes de importar la aplicación en Configuration Manager.

## <a name="start-the-azure-services-wizard"></a>Inicio del Asistente para servicios de Azure

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**.  

2. En la pestaña **Inicio** de la cinta, en el grupo **Servicios de Azure**, haga clic en **Configurar servicios de Azure**.  

3. En la página **Servicios de Azure** del Asistente para servicios de Azure:  

    1. Especifique un **Nombre** para el objeto en Configuration Manager.  

    2. Especifique una **Descripción** opcional para ayudar a identificar el servicio.  

    3. Seleccione el servicio de Azure al que se quiere conectar con Configuration Manager.  

4. Haga clic en **Siguiente** para continuar a la página [Propiedades de la aplicación de Azure](#azure-app-properties) del Asistente para servicios de Azure.  

## <a name="azure-app-properties"></a>Propiedades de la aplicación de Azure

En la página **Aplicación** del Asistente para servicios de Azure, primero seleccione el **Entorno de Azure** en la lista. Consulte la tabla de la sección [Detalles del servicio](#service-details) para saber qué entorno está actualmente disponible para el servicio.

El resto de la página Aplicación varía en función del servicio específico. Consulte la tabla de la sección [Detalles del servicio](#service-details) para saber qué tipo de aplicación usa el servicio y qué acción se puede realizar.

- Si la aplicación es compatible con las acciones de importación y creación, haga clic en **Examinar**. Esta acción abre el [cuadro de diálogo Aplicación de servidor](#server-app-dialog) o el [cuadro de diálogo Aplicación cliente](#client-app-dialog).  

- Si la aplicación solo admite la acción de importación, seleccione **Importar**. Esta acción abre el [cuadro de diálogo Importar aplicaciones (servidor)](#import-apps-dialog-server) o el [cuadro de diálogo Importar aplicaciones (cliente)](#import-apps-dialog-client).

Después de especificar las aplicaciones en esta página, haga clic en **Siguiente** para continuar a la página [Configuración o detección](#configuration-or-discovery) del Asistente para servicios de Azure.

### <a name="web-app"></a>Aplicación web

Esta aplicación es el tipo *Aplicación web o API* de Azure AD, también denominada aplicación de servidor en Configuration Manager.

#### <a name="server-app-dialog"></a>Cuadro de diálogo Aplicación de servidor

Al hacer clic en **Examinar** para la **Aplicación web** en la página Aplicación del Asistente para servicios de Azure, se abre el cuadro de diálogo Aplicación de servidor. Muestra una lista en la que se muestran las propiedades siguientes de las aplicaciones web existentes:

- Nombre descriptivo del inquilino
- Nombre descriptivo de la aplicación
- Tipo de servicio

Hay tres acciones que se pueden realizar desde el cuadro de diálogo Aplicación de servidor:

- Para volver a usar una aplicación web existente, selecciónela en la lista.
- Haga clic en **Importar** para abrir el [cuadro de diálogo Importar aplicaciones](#import-apps-dialog-server).
- Haga clic en **Crear** para abrir el [cuadro de diálogo Crear aplicación de servidor](#create-server-application-dialog).

Después de seleccionar, importar o crear una aplicación web, haga clic en **Aceptar** para cerrar el cuadro de diálogo Aplicación de servidor. Esta acción devuelve a la [página Aplicación](#azure-app-properties) del Asistente para servicios de Azure.

#### <a name="import-apps-dialog-server"></a>Cuadro de diálogo Importar aplicaciones (servidor)

Al seleccionar **Importar** desde el cuadro de diálogo Aplicación de servidor o la página Aplicación del Asistente para servicios de Azure, se abre el cuadro de diálogo Importar aplicaciones. Esta página permite especificar información sobre una aplicación web de Azure AD que ya se ha creado en Azure Portal. Importa metadatos sobre esa aplicación web en Configuration Manager. Especifique la información siguiente:

- **Nombre de inquilino de Azure AD**: el nombre del inquilino de Azure AD.
- **Id. de inquilino de Azure AD**: el GUID del inquilino de Azure AD.
- **Nombre de aplicación**: un nombre descriptivo para la aplicación, el nombre para mostrar en el registro de la aplicación.
- **Id. de cliente**: el valor **Id. de aplicación (cliente)** del registro de la aplicación. El formato es un GUID estándar.
- **Clave secreta**: debe copiar la clave secreta al registrar la aplicación en Azure AD.
- **Expiración de la clave secreta**: seleccione una fecha futura en el calendario.
- **URI de id. de aplicación**: este valor debe ser único en el inquilino de Azure AD. Se encuentra en el token de acceso que usa el cliente de Configuration Manager para solicitar acceso al servicio. El valor es el **URI del identificador de la aplicación** de la entrada del registro de la aplicación en el portal de Azure AD. El formato es similar a `https://ConfigMgrService`.

Después de escribir la información, haga clic en **Comprobar**. Luego, haga clic en **Aceptar** para cerrar el cuadro de diálogo Importar aplicaciones. Esta acción devuelve a la [página Aplicación](#azure-app-properties) del Asistente para servicios de Azure o al [cuadro de diálogo Aplicación de servidor](#server-app-dialog).

> [!TIP]
> Al registrar la aplicación en Azure AD, es posible que tenga que especificar manualmente el **URI de redireccionamiento** siguiente: `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>`. Especifique el GUID del id. de cliente de la aplicación, por ejemplo: `ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49`.<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>Cuadro de diálogo Crear aplicación de servidor

Al hacer clic en **Crear** desde el cuadro de diálogo Aplicación de servidor, se abre el cuadro de diálogo Crear aplicación de servidor. Esta página automatiza la creación de una aplicación web en Azure AD. Especifique la información siguiente:

- **Nombre de aplicación**: nombre descriptivo de la aplicación.
- **Dirección URL de la página principal**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrService`.  
- **URI de id. de aplicación**: este valor debe ser único en el inquilino de Azure AD. Se encuentra en el token de acceso que usa el cliente de Configuration Manager para solicitar acceso al servicio. De forma predeterminada, este valor es `https://ConfigMgrService`.  
- **Período de validez de clave secreta**: elija **1 año** o **2 años** en la lista desplegable. El valor predeterminado es un año.

Haga clic en **Iniciar sesión** para autenticarse en Azure como un usuario administrativo. Configuration Manager no guarda estas credenciales. Este rol no requiere permisos de Configuration Manager y no tiene que ser la misma cuenta que ejecuta al Asistente para servicios de Azure. Después de autenticarse correctamente en Azure, en la página se muestra el **Nombre de inquilino de Azure AD** como referencia.

Haga clic en **Aceptar** para crear la aplicación web en Azure AD y cerrar el cuadro de diálogo Crear aplicación de servidor. Esta acción devuelve al [cuadro de diálogo Aplicación de servidor](#server-app-dialog).

> [!NOTE]
> Si tiene una directiva de acceso condicional de Azure AD definida y se aplica a **todas las aplicaciones en la nube**, debe excluir la aplicación de servidor creada de esta directiva. Para obtener más información sobre cómo excluir aplicaciones específicas, vea [ Documentación de acceso condicional de Azure AD](https://docs.microsoft.com/azure/active-directory/conditional-access/).

### <a name="native-client-app"></a>Aplicación cliente nativa

Esta aplicación es el tipo *Nativa* de Azure AD, también denominada aplicación cliente en Configuration Manager.

#### <a name="client-app-dialog"></a>Cuadro de diálogo Aplicación cliente

Al hacer clic en **Examinar** para la **Aplicación cliente nativa** en la página Aplicación del Asistente para servicios de Azure, se abre el cuadro de diálogo Aplicación cliente. Muestra una lista en la que se muestran las propiedades siguientes de las aplicaciones nativas existentes:

- Nombre descriptivo del inquilino
- Nombre descriptivo de la aplicación
- Tipo de servicio

Hay tres acciones que se pueden realizar desde el cuadro de diálogo Aplicación cliente:

- Para volver a usar una aplicación nativa existente, selecciónela en la lista. 
- Haga clic en **Importar** para abrir el [cuadro de diálogo Importar aplicaciones](#import-apps-dialog-client).
- Haga clic en **Crear** para abrir el [cuadro de diálogo Crear aplicación cliente](#create-client-application-dialog).

Después de seleccionar, importar o crear una aplicación nativa, haga clic en **Aceptar** para cerrar el cuadro de diálogo Aplicación cliente. Esta acción devuelve a la [página Aplicación](#azure-app-properties) del Asistente para servicios de Azure.

#### <a name="import-apps-dialog-client"></a>Cuadro de diálogo Importar aplicaciones (cliente)

Al hacer clic en **Importar** desde el cuadro de diálogo Aplicación cliente, se abre el cuadro de diálogo Importar aplicaciones. Esta página permite especificar información sobre una aplicación nativa de Azure AD que ya se ha creado en Azure Portal. Importa metadatos sobre esa aplicación nativa en Configuration Manager. Especifique la información siguiente:

- **Nombre de aplicación**: nombre descriptivo de la aplicación.
- **Id. de cliente**: el valor **Id. de aplicación (cliente)** del registro de la aplicación. El formato es un GUID estándar.

Después de escribir la información, haga clic en **Comprobar**. Luego, haga clic en **Aceptar** para cerrar el cuadro de diálogo Importar aplicaciones. Esta acción devuelve al [cuadro de diálogo Aplicación cliente](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Cuadro de diálogo Crear aplicación cliente

Al hacer clic en **Crear** desde el cuadro de diálogo Aplicación cliente se abre el cuadro de diálogo Crear aplicación cliente. Esta página automatiza la creación de una aplicación nativa en Azure AD. Especifique la información siguiente:

- **Nombre de aplicación**: nombre descriptivo de la aplicación.
- **Dirección URL de respuesta**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrService`.

Haga clic en **Iniciar sesión** para autenticarse en Azure como un usuario administrativo. Configuration Manager no guarda estas credenciales. Este rol no requiere permisos de Configuration Manager y no tiene que ser la misma cuenta que ejecuta al Asistente para servicios de Azure. Después de autenticarse correctamente en Azure, en la página se muestra el **Nombre de inquilino de Azure AD** como referencia.

Haga clic en **Aceptar** para crear la aplicación nativa en Azure AD y cerrar el cuadro de diálogo Crear aplicación cliente. Esta acción devuelve al [cuadro de diálogo Aplicación cliente](#client-app-dialog).

## <a name="configuration-or-discovery"></a>Configuración o detección

Después de especificar las aplicaciones web y nativas en la página Aplicaciones, el Asistente para servicios de Azure continúa a una página **Configuración** o **Detección**, en función del servicio al que se esté conectando. Los detalles de esta página varían para cada servicio. Para obtener más información, vea uno de los artículos siguientes:  

- Servicio **Administración en la nube**, página **Detección**: [Configuración de la detección de usuarios de Azure AD](configure-discovery-methods.md#azureaadisc).  

- Servicio **Conector de Log Analytics**, página **Configuración**: [Configuración de la conexión a Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- Servicio **Microsoft Store para Empresas**, página **Configuraciones**: [Configuración de la sincronización de Microsoft Store para Empresas](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

Por último, complete al Asistente para servicios de Azure a través de las páginas Resumen, Progreso y Finalización. Ha completado la configuración de un servicio de Azure en Configuration Manager. Repita este proceso para configurar otros servicios de Azure.

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a> Renovar clave secreta

### <a name="renew-key-for-created-app"></a>Renovación de la clave de la aplicación creada

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Inquilinos de Azure Active Directory**.

1. En el panel de detalles, seleccione el inquilino de Azure AD para la aplicación.

1. En la cinta de opciones, seleccione **Renovar clave secreta**. Escriba las credenciales del propietario de la aplicación o de un administrador de Azure AD.

### <a name="renew-key-for-imported-app"></a>Renovación de la clave de la aplicación importada

Si importó la aplicación de Azure en Configuration Manager, use Azure Portal para realizar la renovación. Anote la nueva clave secreta y la fecha de expiración. Agregue esta información en el asistente **Renovar clave secreta**.  

> [!NOTE]
> Guarde la clave secreta antes de cerrar la página **Clave** de las propiedades de aplicación de Azure. Esta información se quita al cerrar la página.

## <a name="view-the-configuration-of-an-azure-service"></a>Visualización de la configuración de un servicio de Azure

Vea las propiedades de un servicio de Azure que haya configurado para usarse. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en **Servicios de Azure**. Seleccione el servicio que quiere ver o modificar y, luego, haga clic en **Propiedades**.

Si selecciona un servicio y después hace clic en **Eliminar** en la cinta, esta acción elimina la conexión en Configuration Manager. No quita la aplicación de Azure AD. Pida al administrador de Azure que elimine la aplicación cuando ya no la necesite. O bien, ejecute el Asistente para servicios de Azure para importar la aplicación.<!--483440-->

## <a name="cloud-management-data-flow"></a>Flujo de datos de administración en la nube

El diagrama siguiente es un flujo de datos conceptual para la interacción entre Configuration Manager, Azure AD y los servicios en la nube conectados. En este ejemplo concreto se usa el servicio **Cloud Management**, que incluye un cliente de Windows 10 y aplicaciones de servidor y cliente. Los flujos para otros servicios son similares.

![Diagrama de flujo de datos de Configuration Manager con Azure AD y Cloud Management](media/aad-auth.png)

1. El administrador de Configuration Manager importa o crea las aplicaciones cliente y de servidor en Azure AD.  

2. Configuration Manager ejecuta el método de detección de usuarios de Azure AD. El sitio usa el token de aplicación de servidor de Azure AD para realizar consultas de objetos de usuario en Microsoft Graph.  

3. El sitio almacena datos sobre los objetos de usuario. Para obtener más información, vea [Detección de usuarios de Azure AD](about-discovery-methods.md#azureaddisc).  

4. El cliente de Configuration Manager solicita el token de usuario de Azure AD. El cliente realiza la notificación con el id. de aplicación de la aplicación cliente de Azure AD y la aplicación de servidor como público. Para obtener más información, vea [Notificaciones de tokens de seguridad de Azure AD](/azure/active-directory/develop/authentication-scenarios#security-tokens).  

5. El cliente se autentica con el sitio presentando el token de Azure AD a la instancia de Cloud Management Gateway y al punto de administración local habilitado para HTTPS.  

Para obtener información más detallada, vea [Flujo de trabajo de autenticación de Azure AD](../../../clients/manage/azure-ccmsetup.md).
