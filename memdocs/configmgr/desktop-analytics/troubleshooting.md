---
title: Solución de problemas de Análisis de escritorio
titleSuffix: Configuration Manager
description: Detalles técnicos para ayudarle a solucionar problemas con Análisis de escritorio.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: cfd329b7edb695c1e7316323555bfc18a2fd479e
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428572"
---
# <a name="troubleshoot-desktop-analytics"></a>Solución de problemas de Análisis de escritorio

Use los detalles de este artículo para ayudar a solucionar problemas con el Análisis de escritorio integrado con Configuration Manager.

## <a name="confirm-prerequisites"></a>Confirmación de los requisitos previos

Muchos problemas comunes se deben a que faltan requisitos previos. Primero confirme los siguientes parámetros:

- [Requisitos previos](overview.md#prerequisites)  

- [Actualizaciones de los componentes de Windows](enroll-devices.md#update-devices)  

- [Habilitación del uso compartido de datos](enable-data-sharing.md), que trata los temas siguientes:  

  - Puntos de conexión de Internet a los que los clientes deben conectarse  

  - Autenticación del servidor proxy  

  - Niveles de datos de diagnóstico  

## <a name="monitor-connection-health"></a>Supervisión del estado de conexión

Use el panel **Estado de conexión** de Configuration Manager para profundizar en las categorías por estado de dispositivo. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda el nodo **Servicio de Análisis de escritorio** y seleccione el panel **Mantenimiento de la conexión**.  

Para más información, consulte [Supervisión del estado de conexión](monitor-connection-health.md).

> [!NOTE]
> La conexión de Configuration Manager con Análisis de escritorio se basa en el punto de conexión de servicio. Cualquier cambio que se realice en este rol de sistema de sitio pueden afectar a la sincronización con el servicio en la nube. Para obtener más información, consulte [About the service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move) (Sobre el punto de conexión del servicio).

A partir de la versión 2002, si el sitio de Configuration Manager no se puede conectar a los puntos de conexión necesarios para un servicio en la nube, genera un mensaje de estado crítico con el identificador 11488. Si no se puede conectar al servicio, el estado del componente SMS_SERVICE_CONNECTOR cambia a crítico. Consulte el estado detallado en el nodo [Estado del componente](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) de la consola de Configuration Manager.<!-- 5566763 -->

## <a name="log-files"></a>Archivos de registro

Para más información, consulte [Archivos de registro para Análisis de escritorio](../core/plan-design/hierarchy/log-files.md#desktop-analytics).

A partir de la versión 1906 de Configuration Manager, use la herramienta **DesktopAnalyticsLogsCollector.ps1** del directorio de instalación de Configuration Manager para solucionar problemas de Análisis de escritorio. Ejecuta algunos pasos básicos para solucionar problemas y recopila los registros pertinentes en un solo directorio de trabajo. Para más información, consulte [Recopilador de registros](log-collector.md).

### <a name="enable-verbose-logging"></a>Habilitar el registro detallado

1. En el punto de conexión de servicio, vaya a la siguiente clave del Registro: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Establezca el valor de **LoggingLevel** en `0`.  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a> Aplicaciones de Azure AD

Análisis de escritorio agrega las siguientes aplicaciones a su instancia de Azure AD:

- **Configuration Manager Microservice**: conecta Configuration Manager con Análisis de escritorio. Esta aplicación no tiene ningún requisito de acceso.  

- **MALogAnalyticsReader**: Supervisa el área de trabajo de Log Analytics de Azure para asegurarse de que la instantánea diaria se haya copiado correctamente. Para obtener más información, consulte [Rol de aplicación MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

- **Análisis de escritorio**: Permite que Configuration Manager recupere la información sobre el plan de implementación y el estado de preparación de los dispositivos de Análisis de escritorio.

Si tiene que aprovisionar estas aplicaciones después de completar la instalación, vaya al panel de **Servicios conectados**. Seleccione **Configurar el acceso de los usuarios y las aplicaciones** y aprovisione las aplicaciones.  

- **Aplicación de Azure AD para Configuration Manager**. Si necesita aprovisionar o solucionar problemas de conexión después de completar la instalación, consulte [Creación e importación de una aplicación para Configuration Manager](#create-and-import-app-for-configuration-manager). Esta aplicación requiere los permisos **Write CM Collection Data** (Escribir datos de recopilación de CM) y **Read CM Collection Data** (Leer datos de colección de CM) en la API **Configuration Manager Service**.  

### <a name="create-and-import-app-for-configuration-manager"></a>Creación e importación de una aplicación para Configuration Manager

Si no puede crear la aplicación de Azure AD para Configuration Manager desde el Asistente para configurar servicios de Azure, o si desea volver a usar una aplicación existente, debe crearla e importarla manualmente. Después de completar el proceso de [incorporación inicial](set-up.md#initial-onboarding) en el portal de Análisis de escritorio, siga estos pasos:

#### <a name="create-app-in-azure-ad"></a>Creación de una aplicación en Azure AD

1. Abra [Azure Portal](https://portal.azure.com) como usuario con permisos de *administrador global*, vaya a **Azure Active Directory** y seleccione **Registros de aplicaciones**. A continuación, seleccione **Nuevo registro**.  

2. En el panel **Crear**, establezca la siguiente configuración:  

    - **Nombre**: un nombre único que identifica la aplicación, por ejemplo: `Desktop-Analytics-Connection`  

    - **Tipos de cuenta admitidos**: **Solo las cuentas de este directorio organizativo (Contoso)**

    - **URI de redirección (opcional)** : **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Seleccione **Registrar**.  

3. Seleccione la aplicación y anote el **Id. de aplicación (cliente)** y el **Id. de directorio (inquilino)** . Los valores son los GUID que se usan para configurar la conexión de Configuration Manager.  

4. En **Administrar**, seleccione **Certificados y secretos**. Seleccione **Nuevo secreto de cliente**. Escriba una **descripción**, especifique una duración de expiración y seleccione **Agregar**. Copie el **valor** de la clave, que se usa para configurar la conexión de Configuration Manager.

    > [!Important]  
    > Esta es la única oportunidad para copiar el valor de clave. Si no lo copia ahora, debe crear otra clave.  
    >
    > Guarde el valor de la clave en una ubicación segura.  

5. En el menú **Administrar**, seleccione **Permisos de API**.  

    1. En el panel **Permisos de API**, seleccione **Agregar un permiso**.  

    2. En el panel **Solicitud de permisos de API**, cambie a **API usadas en mi organización**.  

    3. Busque y seleccione la API **Configuration Manager Microservice**.  

    4. Seleccione el grupo **Permisos de la aplicación**. Expanda **CmCollectionData** y seleccione los dos permisos siguientes: **Write CM Collection Data** (Escribir datos de recopilación de CM) y **Read CM Collection Data** (Leer datos de colección de CM).  

    5. Seleccione **Agregar permisos**.  

6. En el panel **Permisos de API**, seleccione **Conceder consentimiento de administrador...** Seleccione **Sí**.  

#### <a name="import-app-in-configuration-manager"></a>Importación de aplicaciones en Configuration Manager

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **Configurar servicios de Azure** en la cinta de opciones.  

2. En la página **Servicios de Azure** del Asistente para servicios de Azure, configure las siguientes opciones:  

    - Especifique un **Nombre** para el objeto en Configuration Manager.  

    - Especifique una **Descripción** opcional para ayudar a identificar el servicio.  

    - Seleccione **Análisis de escritorio** en la lista de servicios disponibles.  
  
   Seleccione **Siguiente**.  

3. En la página **Aplicación**, seleccione el **entorno de Azure** adecuado. Luego, seleccione **Importar** para la aplicación web. Configure las opciones siguientes en la ventana **Importar aplicaciones**:  

    - **Nombre de inquilino de Azure AD**: el nombre que recibe en Configuration Manager  

    - **Id. de inquilino de Azure AD**: el **Id. de directorio** copiado de Azure AD.  

    - **Id. de cliente**: el **Id. de aplicación** copiado de la aplicación Azure AD.  

    - **Clave secreta**: el **valor** de la clave copiado de la aplicación Azure AD.  

    - **Expiración de la clave secreta**: la misma fecha de expiración de la clave.  

    - **URI de id. de aplicación**: Esta configuración debe rellenarse automáticamente con el siguiente valor: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Seleccione **Comprobar** y luego **Aceptar** para cerrar el cuadro de diálogo Importar aplicaciones. Seleccione **Siguiente** en la página Aplicación del Asistente para servicios de Azure.  

Para continuar con el resto del asistente en la página **Datos de diagnóstico**, consulte [Conexión al servicio](connect-configmgr.md#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Solución de problemas de la aplicación en Configuration Manager

Si tiene problemas para crear o importar la aplicación, compruebe en primer lugar **SMSAdminUI. log** para ver el error específico. Luego, compruebe las configuraciones siguientes:

- Ha inscrito correctamente el inquilino en el servicio de Análisis de escritorio. Para más información, consulte [Configuración de Análisis de escritorio](set-up.md).

- Se puede tener acceso a todos los puntos de conexión necesarios. Para más información, consulte [Puntos de conexión](enable-data-sharing.md#endpoints).

- Asegúrese de que el usuario que inicia sesión tenga los permisos correctos. Para obtener más información, consulte [Requisitos previos](overview.md#prerequisites).

- Asegúrese de que el usuario puede iniciar sesión en Azure en general. Esta acción determina si hay algún problema de autenticación general en Azure AD.

- Compruebe los mensajes de estado para el componente **SMS_SERVICE_CONNECTOR** con respecto al *trabajo de Análisis de escritorio*.

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a> Rol de aplicación de MALogAnalyticsReader

Al configurar Análisis de escritorio, da su consentimiento en nombre de su organización. Este consentimiento es para asignar a la aplicación MALogAnalyticsReader el rol de lector Log Analytics para el área de trabajo. Análisis de escritorio requiere este rol de aplicación.

Si hay un problema con este proceso durante la instalación, utilice el siguiente proceso para agregar manualmente este permiso:

1. Vaya a [Azure Portal](https://portal.azure.com) y seleccione **Todos los recursos**. Seleccione el área de trabajo de tipo **Log Analytics**.  

2. En el menú del área de trabajo, seleccione **Control de acceso (IAM)** y, luego, seleccione **Agregar**.  

3. En el panel **Agregar permiso**, establezca la siguiente configuración:  

    - **Rol**: **lector**  

    - **Asignar acceso a**: **usuario, grupo o aplicación de Azure AD**  

    - **Seleccionar**: **MALogAnalyticsReader**  

4. Seleccione **Guardar**.

El portal muestra una notificación de que agregó la asignación de roles.

## <a name="data-latency"></a>Latencia de datos

<!-- 3846531 -->
La primera vez que configura Análisis de escritorio, inscribe clientes nuevos o configura nuevos planes de implementación, puede que los informes de Configuration Manager y el portal de Análisis de escritorio no muestren los datos completos de inmediato. Pueden transcurrir 2-3 días para que se produzcan los siguientes pasos:

- Los dispositivos activos envían datos de diagnóstico al servicio Análisis de escritorio.
- El servicio de archivos procesa los datos.
- El servicio se sincroniza con el sitio de Configuration Manager.

Al sincronizar las recopilaciones de dispositivos de la jerarquía de Configuration Manager con Análisis de escritorio, las colecciones pueden tardar hasta una hora en aparecer en el portal de Análisis de escritorio. Del mismo modo, cuando se crea un plan de implementación en Análisis de escritorio, las nuevas colecciones asociadas al plan de implementación pueden tardar hasta una hora en aparecer en la jerarquía de Configuration Manager. Los sitios primarios crean las recopilaciones y el sitio de administración central se sincroniza con Análisis de escritorio. Configuration Manager pueden tardar hasta 24 horas en evaluar y actualizar la pertenencia a la recopilación. Para acelerar este proceso, actualice manualmente la pertenencia a la colección.<!-- 4984639 -->

> [!Note]
> Para que las actualizaciones de recopilación manuales reflejen los cambios, el componente SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker primero debe sincronizarse. Este proceso puede tardar hasta una hora en ejecutarse. Para obtener más información, vea el registro **M365ADeploymentPlanWorker.log**.

Hay dos tipos de datos en el portal de Análisis de escritorio: **datos de administrador** y **datos de diagnóstico**.

- Los **datos de administrador** hacen referencia a los cambios que realiza en la configuración del área de trabajo. Por ejemplo, cuando se cambia la **decisión de actualización** o la **importancia** de un recurso, se están cambiando los datos del administrador. Estos cambios suelen tener un efecto compuesto, ya que pueden modificar el estado de disponibilidad de un dispositivo con el recurso en cuestión instalado.

- Los **datos de diagnóstico** hacen referencia a los metadatos del sistema cargados desde dispositivos cliente a Microsoft. Estos datos alimentan a Análisis de escritorio. Incluye atributos como el inventario de dispositivos y el estado de actualización de características y seguridad.

De forma predeterminada, todos los datos del portal de Análisis de escritorio se actualizan de forma automática diariamente. Esta actualización incluye los cambios en los datos de diagnóstico y los cambios que realice en la configuración (datos de administrador). Debe estar visible en el portal de Análisis de escritorio a las 08:00 A.M. UTC cada día.

Al realizar cambios en los datos de administrador, puede desencadenar una actualización a petición de los datos del administrador en el área de trabajo. En cualquier página del portal de Análisis de escritorio, abra el control flotante de la divisa de datos:

![Captura de pantalla del control flotante de divisa de datos en el portal Análisis de escritorio](media/data-currency-flyout.png)

A continuación, seleccione **Aplicar cambios**:

![Captura de pantalla del control flotante de divisa de datos en el portal Análisis de escritorio](media/data-currency-flyout-expand.png)

Este proceso suele tardar entre 15 y 60 minutos. El tiempo depende del tamaño del área de trabajo y del ámbito de los cambios que necesitan procesamiento. Cuando solicita una actualización de datos a petición, no se producen cambios en los datos de diagnóstico.  Para más información, consulte [Preguntas frecuentes sobre Análisis de escritorio](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Si no ve los cambios actualizados dentro de los intervalos de tiempo indicados anteriormente, espere a que transcurran otras 24 horas para la siguiente actualización diaria. Si ve retrasos más largos, consulte el panel de estado del servicio. Si el servicio informa de un estado correcto, póngase en contacto con el soporte técnico de Microsoft.<!-- 3896921 -->

> [!IMPORTANT]
> La opción de Análisis de escritorio para **Ver datos recientes** está en desuso. Esta acción se quitará en una versión futura del servicio de Análisis de escritorio. Para más información, vea [Deprecated Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md) (Características en desuso).<!--7080949-->  
