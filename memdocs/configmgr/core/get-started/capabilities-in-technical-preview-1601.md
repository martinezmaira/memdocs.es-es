---
title: Funcionalidades de Technical Preview 1601
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1601.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: be1401f28ccbd15de2561a19169ed67a81a91550
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526039"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Funciones de Technical Preview 1601 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1601 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager.      Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.  

 **Problemas conocidos de esta Technical Preview:**  

-   : al administrar **Opciones de actualización de cliente** para promover un cliente de preproducción a producción, el texto de la casilla muestra una versión de cliente de cero (0) en lugar del número de compilación real del cliente. La versión de cliente de preproducción correcta se muestra en el área por encima de esta opción y corresponde a la versión de cliente que se promueve a producción cuando se selecciona esta opción.  

-   Al actualizar a Technical Preview 1601 y elegir la opción de probar el cliente de Configuration Manager en una colección de preproducción, el paquete de cliente de la colección no se actualizará. Este problema solo se produce en Technical Preview 1601.  

     Para solucionar estos problemas, realice alguna de las siguientes acciones:  

    -   Ejecute el siguiente script de SQL en la base de datos del sitio primario:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Agregue un nuevo rol de sistema de sitio de punto de distribución al sitio de laboratorio. El nuevo punto de distribución actualizará la colección de preproducción con el nuevo paquete de cliente.  

**Estas son las nuevas características que puede probar con esta versión.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a> Mejoras en la integración con Microsoft Intune  
En la versión Technical Preview 1601, hemos agregado compatibilidad con las siguientes características:  

### <a name="improvements-to-conditional-access"></a>Mejoras de acceso condicional  

-   **Compatibilidad de acceso condicional para equipos administrados por Configuration Manager**  

     Ahora puede establecer directivas de acceso condicional para equipos administrados por Configuration Manager, lo que requiere que los equipos sean conformes a la directiva de cumplimiento con el fin de obtener acceso a los servicios Exchange Online y SharePoint Online.  Con esta nueva característica, también puede registrar equipos en Azure AD a través de la directiva de cumplimiento, así como supervisar y notificar sobre el registro en Azure AD.  

    > [!NOTE]  
    >  Windows 10 aún no admite el acceso condicional.  

    A continuación se detallan los requisitos previos para usar esta característica:  

    -   Suscripción a Azure Active Directory Premium ADFS y sincronización con ADFS.  

    -   Suscripción a Microsoft Intune. La suscripción a Microsoft Intune debe configurarse en la consola de Configuration Manager.  

    -   [Requisitos previos para el registro automático en Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Para usar esta opción, debe crear una directiva de cumplimiento en Configuration Manager con las reglas específicas que se describen a continuación y establecer una directiva de acceso condicional en la consola de Intune.  Además, para asegurarse de que se permita el acceso únicamente a los equipos compatibles, debe establecer el requisito de equipo Windows en la opción **Los dispositivos deben ser compatibles**. Aquí se detallan las reglas de directiva de cumplimiento que se aplican a los equipos administrados por Configuration Manager.  

    -   **Requiere registro en Azure Active Directory:** esta regla comprueba si el dispositivo del usuario está unido al área de trabajo en Azure AD y, si no, se registra automáticamente en Azure AD. El registro automático solo se admite en Windows 8.1. Para equipos con Windows 7, implemente un archivo MSI para realizar el registro automático. Para más información, vea [aquí](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Todas las actualizaciones necesarias que se instalan con una fecha límite anterior a un número determinado de días:** esta regla comprueba si el dispositivo del usuario tiene todas las actualizaciones necesarias (especificadas en la regla **Actualizaciones automáticas requeridas**) dentro de la fecha límite y el período de gracia que usted especifique, e instala automáticamente cualquier actualización necesaria pendiente.  

    -   **Requerir cifrado de unidad BitLocker:** se trata de una comprobación para ver si la unidad principal (por ejemplo, C:\\) del dispositivo está cifrada con BitLocker. Si el cifrado BitLocker no está habilitado en el dispositivo primario, se bloquea el acceso a los servicios de correo electrónico y SharePoint.  

    -   **Requerir antimalware:** se trata de una comprobación para ver si el software antimalware (System Center Endpoint Protection o Windows Defender solamente) está habilitado y en ejecución.  
         Si no está habilitado, se bloquea el acceso a los servicios de correo electrónico y SharePoint.  

    Los usuarios finales que están bloqueados debido a la falta de cumplimiento verán información de cumplimiento en el Centro de software e iniciarán una nueva evaluación de directivas cuando se corrijan los problemas de cumplimiento.  

-   **Acceso condicional con servicio de atestación de estado** Ahora puede restringir el acceso a los servicios de correo electrónico y 0365 según el estado de los dispositivos notificado por el servicio de atestación de estado.  Además, los dispositivos administrados por Intune se incluyen en los informes de estado de dispositivos.  

    Se ha agregado una nueva regla de cumplimiento a la consola de Configuration Manager que permite especificar si debe permitir o bloquear el acceso de los dispositivos en función de su estado.  Para crear esta regla, abra el **Asistente para crear directivas de cumplimiento** y agregue una nueva regla.  Seleccione **Notificado como estado correcto por el servicio de atestación de estado** para la condición y establezca el valor en **True**.  Esto garantiza que solo los dispositivos que se notifican con un estado correcto tienen acceso a los recursos de la compañía. Para obtener detalles sobre el servicio de atestación de estado y cómo se notifica el estado de los dispositivos en Intune, vea [Device Health Attestation (Atestación de estado de un dispositivo)](capabilities-in-technical-preview-1512.md#bkmk_devicehealth).  

-   **Nuevas opciones de directiva de cumplimiento:** las nuevas opciones de directiva de cumplimiento ayudan a mejorar la seguridad y la protección en los dispositivos que se usan para obtener acceso a los servicios de correo electrónico y SharePoint de la empresa:  

    -   **Requerir actualizaciones automáticas:** puede exigir que los dispositivos con Windows 8.1 o posterior permitan la instalación automática de actualizaciones y, además, puede especificar la clase de actualizaciones que se instalan.  Puede elegir entre instalar solo las actualizaciones marcadas como importantes o instalar todas las actualizaciones recomendadas.  

         Para crear una regla de actualizaciones automáticas, abra el **Asistente para crear directivas de cumplimiento** y agregue una nueva regla.  Seleccione **Clasificación mínima de actualizaciones necesarias** como condición y establezca el valor en uno de los valores disponibles: **Ninguno**, **Recomendado** e **Importante**.  

        -   **Ninguno:** las actualizaciones no se instalan automáticamente.  

        -   **Recomendado:** se instalan todas las actualizaciones recomendadas.  

        -   **Importante:** solo se instalan las actualizaciones clasificadas como importantes.  

    -   **Requerir una contraseña para desbloquear dispositivos móviles:** cuando esta opción está establecida en **Sí**, los usuarios finales deben escribir una contraseña para poder tener acceso a su dispositivo.  

         Para crear una regla para exigir una contraseña a fin de desbloquear los dispositivos móviles, abra el **Asistente para crear directivas de cumplimiento** y agregue una nueva regla. Seleccione **Requerir contraseña para desbloquear un dispositivo inactivo** como condición y establezca el valor en **True**.  

    -   **Minutos de inactividad antes de que se requiera la contraseña:**  Especifica el tiempo de inactividad antes de que el usuario deba volver a escribir la contraseña.  

         Para crear esta regla, abra el **Asistente para crear directivas de cumplimiento** y agregue una nueva regla. Seleccione **Minutos de inactividad antes de solicitar la contraseña** como condición y establezca el valor en una de las opciones disponibles: 1 minuto, 5 minutos, 15 minutos, 30 minutos o 1 hora.  

-   **Invalidación de la regla predeterminada: permitir siempre que los dispositivos compatibles e inscritos en Intune accedan a Exchange:**  

     Si se selecciona esta opción, los dispositivos inscritos en Intune y que cumplen con las directivas establecidas pueden tener acceso a Exchange local. Esta regla invalida la Regla predeterminada, lo que significa que aunque configure dicha regla y la establezca en Cuarentena o Bloquear el acceso, aquellos dispositivos inscritos y que cumplen con las directivas seguirán teniendo acceso a Exchange local.  
     Use esta opción cuando quiera que los dispositivos inscritos y conformes a las directivas siempre tengan acceso a correo electrónico a través de Exchange local.  

     Esto es compatible en las siguientes plataformas:  Dispositivos con Windows Phone 8 y versiones posteriores, e iOS 6 y versiones posteriores Android 4.0 y versiones posteriores, Samsung KNOX Standard 4.0 y versiones posteriores.  

     Para usar esta opción, vaya a la página **General** del **Asistente de configuración de directivas de acceso condicional** de Exchange local.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a> Estado de conexión de clientes  
A partir de Technical Preview 1601, se puede identificar de un vistazo si un cliente está o no conectado en la consola de Configuration Manager. Con iconos y columnas actualizados en las listas de dispositivos de la consola, puede evaluar el estado de los clientes en el entorno para identificar las áreas problemáticas y otros inconvenientes que podrían requerir su atención.  

Un cliente está en línea si en ese momento está conectado a un rol de sistema de sitio del punto de administración de Configuration Manager. Siempre que el punto de administración reciba mensajes de tipo ping provenientes del cliente, su estado será en línea. Si la administración no recibe un mensaje durante un período de cinco minutos, el estado del cliente cambia a sin conexión.  

### <a name="icons-for-client-status"></a>Iconos de estado de cliente  

| Icono | Descripción |
| ---- | ----------- |
|![icono de estado conectado para los clientes](media/online-status-icon.png)|El cliente está en línea.|  
|![icono de estado desconectado para los clientes](media/offline-status-icon.png)|El cliente está sin conexión.|  
|![icono de estado desconocido para los clientes](media/unknown-status-icon.png)|Se desconoce el estado de cliente.|  

### <a name="prerequisites"></a>Requisitos previos  
 El estado de conexión de cliente no tiene requisitos previos. Puede empezar a usarlo una vez instalado Configuration Manager Technical Preview 1601.  

### <a name="limitations"></a>Limitaciones  
 El estado de conexión de cliente solo está disponible en los equipos Windows que tienen instalado el cliente de Configuration Manager. El estado de conexión de cliente no es compatible con los equipos Mac, Linux o UNIX ni con los dispositivos administrados con la administración local de dispositivos móviles.  

### <a name="to-view-client-online-status"></a>Para ver el estado de conexión de cliente  

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad > Información general > Dispositivos**.  

2. Haga clic con el botón derecho en el encabezado de columna y luego haga clic en uno de los campos de estado de conexión de cliente para agregarlo a la vista del dispositivo. Los campos son los siguientes:  

   -   **Estado de conexión del dispositivo** indica si el cliente está actualmente conectado o no.  

   -   **Hora de la última conexión** indica cuándo cambió el estado de conexión del cliente de sin conexión a en línea.  

   -   **Hora de la última desconexión** indica cuándo cambió el estado de en línea a sin conexión.  

   Para mostrar los cambios recientes del estado de cliente, actualice la consola.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a> Mejoras en la administración de aplicaciones  
 En la versión Technical Preview 1601, hemos agregado compatibilidad con las siguientes características:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Administrar aplicaciones compradas por volumen para dispositivos iOS  
 Algunas tiendas de aplicaciones permiten comprar varias licencias de una aplicación que se quiere ejecutar en la compañía. Esto ayuda a reducir la carga administrativa relacionada con el seguimiento de varias copias compradas de las aplicaciones.  

 Configuration Manager ahora ayuda a administrar las aplicaciones adquiridas a través de este tipo de programa al importar la información de licencia desde la tienda de aplicaciones y realizar el seguimiento de la cantidad de licencias que se han usado.  


### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS: configuración de aplicaciones para aplicaciones<br />Híbrida  
 Algunas aplicaciones de iOS admiten la configuración previa de, por ejemplo, un servidor o una base de datos a los que debe conectarse la aplicación. Configuration Manager ahora admite la implementación de directivas de configuración de aplicación en el dispositivo, lo que permite que el usuario use la aplicación de inmediato sin necesidad de conocer esta información. Los desarrolladores deben habilitar esta característica en sus aplicaciones.  

 Un número limitado de aplicaciones publicadas admite actualmente la configuración previa de valores. Es probable que también tenga aplicaciones de línea de negocio desarrolladas internamente que admitan esto.  

#### <a name="prerequisites-for-this-scenario"></a>Requisitos previos para este escenario  

-   Debe haber agregado una suscripción de Microsoft Intune a Configuration Manager.  

-   Debe haber agregado un certificado válido de APN de Apple para la suscripción de Intune.  

-   Debe haber implementado una aplicación iOS que admite la configuración de la aplicación.  

#### <a name="try-it-out"></a>Haga la prueba  
 Una vez que se cumplen los requisitos previos antes mencionados, debe crear una aplicación de Configuration Manager que use un tipo de implementación de iOS. La aplicación que use debe admitir la configuración de la aplicación. Consulte la documentación del proveedor de la aplicación para conocer qué elementos específicos (pares nombre-valor) puede configurar.  

 A continuación, asocie la directiva de configuración de aplicación al tipo de implementación de iOS durante la implementación de la aplicación. También puede implementar la directiva desde el nodo **Directivas de configuración de aplicaciones**, destinada a una aplicación y una colección existentes.  

 Intente realizar las siguientes tareas y después use la información de comentarios que se encuentra al principio de este tema para hacernos saber cómo han funcionado:  

-   Si tiene una aplicación iOS que admite la configuración de la aplicación, consulte la documentación del proveedor de la aplicación para conocer los pares nombre-valor que debe especificar al configurar la aplicación.  

-   Inicie el asistente **Crear directiva de configuración de aplicaciones**. En la página **Directiva de iOS** del asistente, intente agregar los pares nombre-valor que encontró en la documentación del proveedor de la aplicación, o bien puede importar un archivo XML que contenga los valores necesarios.  

-   En el asistente **Implementar software**, en la página **Directiva de configuración de la aplicación**, asocie la directiva de configuración de aplicación que ha creado a un tipo de implementación compatible desde la aplicación.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a> Mejoras en la configuración de cumplimiento  
 En la versión Technical Preview 1601, hemos agregado compatibilidad con las siguientes características:  

### <a name="microsoft-edge-browser-settings"></a>Configuración del explorador Microsoft Edge  
 Se han agregado nuevas opciones para el explorador Microsoft Edge al elemento de configuración de **Windows 8.1 y Windows 10** (se aplican a dispositivos de Windows 10 únicamente).  

 Para ver las nuevas opciones, elija **Microsoft Edge** en la página **Configuración del dispositivo** del elemento de configuración en el asistente **Crear elemento de configuración**.  

 Para más información, vea [Cómo crear elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Configuración de cumplimiento para dispositivos Windows 10 Team  
 Use la nueva configuración de cumplimiento para configurar dispositivos que ejecutan Windows 10 Team, como los dispositivos Surface Hub.  

 Para ver las nuevas opciones, elija **Windows 10 Team** en la página **Configuración del dispositivo** del elemento de configuración en el asistente **Crear elemento de configuración**.  

 Para más información, vea [Cómo crear elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android: pantalla completa para Samsung KNOX Standard<br />Híbrida  
 La pantalla completa le permite bloquear un dispositivo para permitir que solo funcionen determinadas características. Por ejemplo, puede permitir que un dispositivo ejecute solo una aplicación administrada que especifique, o puede deshabilitar los botones de volumen de un dispositivo. Esta configuración podría utilizarse para un modelo de demostración de un dispositivo o para un dispositivo que está dedicado a realizar solo una función, como un dispositivo de punto de venta. Estas opciones no están disponibles para dispositivos Samsung KNOX Standard en el elemento de configuración **Windows 8.1 y Windows 10** (se aplican a dispositivos Windows 10 únicamente).  

 Para ver las nuevas opciones, elija **Pantalla completa: Samsung KNOX** en la página **Configuración del dispositivo** del elemento de configuración del asistente **Crear elemento de configuración**.  

 Para más información, vea [Cómo crear elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
