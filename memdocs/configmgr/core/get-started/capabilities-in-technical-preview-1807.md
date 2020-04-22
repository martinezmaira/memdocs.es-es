---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: Obtenga información sobre las nuevas características disponibles en la versión de rama Technical Preview 1807 de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 398f16b8f75d894030d76406807f74bdaa4be9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695953"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Funcionalidades de la versión 1807 Technical Preview de Configuration Manager 

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1807 Technical Preview de Configuration Manager. Instale esta versión para actualizar y agregar características nuevas a su sitio de Technical Preview. 

Revise el artículo [Technical Preview para System Center Configuration Manager](technical-preview.md) antes de instalar esta actualización. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Problemas conocidos 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a> Problemas con las actualizaciones de software de Office 365
<!--521365-->
Si administra las actualizaciones de Office 365 mediante las versiones de rama 1806 y 1806.2 Technical Preview, es posible que no se instalen en los clientes. 

#### <a name="workaround"></a>Solución alternativa
- Elimine los paquete de implementación y los grupos de actualizaciones de software existentes para Office 365.  

- A partir del 31 de julio de 2018, sincronice las actualizaciones de software de Office 365 e implemente solo las actualizaciones más recientes.  



</br>

**En las secciones siguientes se describen las características nuevas para probar de esta versión:**  


## <a name="community-hub"></a><a name="bkmk_hub"></a> Central de la comunidad
<!--1357766-->

La Central de la comunidad es una ubicación centralizada para compartir objetos útiles de Configuration Manager con otros usuarios. Consulte la nueva área de trabajo **Comunidad** en la consola de Configuration Manager y seleccione el nodo **Central**. Use la Central de la comunidad para descargar los tipos de objetos de Configuration Manager siguientes: 
- Scripts
- Elementos de configuración

![Consola de Configuration Manager, área de trabajo Comunidad, nodo Central](media/1357766-hub.png)

Para más información sobre un elemento disponible, haga clic en la central. En la página de detalles, haga clic en **Descargar** para adquirir el elemento. Al descargar un elemento desde la central, se agrega automáticamente al sitio. 

![Consola de Configuration Manager, área de trabajo Comunidad, nodo Central, página de detalles](media/1357766-hub-details.png)

El área de trabajo **Comunidad** también incluye estos nodos:

- **Documentación**: muestra la [biblioteca de documentación](https://docs.microsoft.com/sccm/) de Configuration Manager  

- **Comentarios**: muestra el [sitio de UserVoice](https://configurationmanager.uservoice.com/) de Configuration Manager  


### <a name="prerequisites"></a>Requisitos previos

- Use la consola de Configuration Manager en un SO cliente.  

    - Si bien no se recomienda, también existe esta opción: en un SO servidor, deshabilite [Internet Explorer: configuración de seguridad mejorada](https://go.microsoft.com/fwlink/?LinkId=253461).  

- El equipo con la consola requiere acceso a internet y la conectividad a los sitios siguientes:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Problema conocido

La contribución de elementos a la central actualmente no está disponible en esta versión. 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a> Especificación de la unidad para la instalación sin conexión de imágenes de SO  
<!--1358924-->

En función de sus [comentarios sobre UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive), ahora se puede especificar la unidad que Configuration Manager usa durante la instalación sin conexión de imágenes de SO. Este proceso puede consumir una gran cantidad de espacio en disco con los archivos temporales, por lo que esta opción le ofrece flexibilidad para seleccionar la unidad que se va a usar. 


### <a name="try-it-out"></a>Haga la prueba

Intente completar las tareas. Luego envíe [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) con sus opiniones sobre la característica.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. En la cinta, haga clic en **Configurar componentes de sitio** y seleccione **Punto de actualización de software**.  

2. Cambie a la pestaña **Instalación sin conexión** y especifique la opción para **Una unidad local que se usará en la instalación de imágenes sin conexión**.  

De manera predeterminada, esta configuración es **Automática**. Con este valor, Configuration Manager selecciona la unidad donde está instalado. 

Durante la instalación sin conexión, Configuration Manager almacena los archivos temporales en la carpeta, `<drive>:\ConfigMgr_OfflineImageServicing`. También monta las imágenes del SO en esta carpeta. 

Revise el archivo de registro **OfflineServicingMgr.log**. 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a> Actividad de sincronización de dispositivos administrados conjuntamente desde Intune
<!--1358565-->

Muestre en la consola de Configuration Manager si un dispositivo administrado conjuntamente está activo con Microsoft Intune. Este estado se basa en los datos del [Almacenamiento de datos de Intune](https://docs.microsoft.com/intune/reports-nav-create-intune-reports). El panel **Estado de cliente** de la consola de Configuration Manager muestra **Clientes inactivos que usan Intune**. Esta categoría nueva es para los dispositivos administrados conjuntamente que están inactivos con Configuration Manager, pero que se sincronizaron con el servicio de Intune durante la última semana.


### <a name="try-it-out"></a>Haga la prueba

Intente completar las tareas. Luego envíe [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) con sus opiniones sobre la característica.

Si ya configuró el sitio para la administración conjunta: 

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**. Haga clic en **Propiedades** de la cinta.  

2. Cambie a la pestaña **Informes**. Haga clic en **Iniciar sesión** y autentíquese. Luego haga clic en **Actualizar** para habilitar los permisos de lectura para el Almacenamiento de datos de Intune.  

3. Después de que el sitio se sincronice con Intune, vaya al área de trabajo **Supervisión** y seleccione nodo **Estado de cliente**. En la sección **Estado general de cliente**, consulte la fila para **IClientes inactivos que usan Intune**.  

Para más información sobre cómo habilitar la administración conjunta, consulte [Administración conjunta para dispositivos de Windows 10](../../comanage/overview.md).



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a> Reparación de aplicaciones
<!--1357866-->

En función de sus [comentarios de UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application), ahora se puede especificar una línea de comandos de reparación para tipos de implementación de Windows Installer y de instalador de scripts. 


### <a name="try-it-out"></a>Haga la prueba

Intente completar las tareas. Luego envíe [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) con sus opiniones sobre la característica.

1. En la consola de Configuration Manager, abra las propiedades de un tipo de implementación de Windows Installer o de instalador de scripts.  

2. Cambie a la pestaña **Programas**. Especifique el comando **Repair program** (Reparar programa).  

3. Implemente la aplicación. En la pestaña **Configuración de implementación**, habilite la opción para **Allow end users to attempt to repair this application** (Permitir que los usuarios finales intenten reparar esta aplicación).  


### <a name="known-issue"></a>Problema conocido

El botón nuevo del Centro de software para que los usuarios puedan **reparar** la aplicación no es visible en esta versión.  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a> Aprobación de solicitudes de aplicación por correo electrónico
<!--1321550-->

Configure notificaciones por correo electrónico para las solicitudes de aprobación de aplicaciones. Recibirá un correo electrónico cuando un usuario solicite una aplicación. Haga clic en los vínculos que aparecen en el correo electrónico para aprobar o denegar la solicitud, sin requerir la consola de Configuration Manager.


### <a name="prerequisites"></a>Requisitos previos

#### <a name="to-send-email-notifications"></a>Para enviar notificaciones por correo electrónico
- Habilite la [característica opcional](../servers/manage/install-in-console-updates.md#bkmk_options) **Aprobación de solicitudes de aplicación para los usuarios por dispositivo**.  

- Configure la [notificación por correo electrónico para las alertas](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>Para aprobar o denegar solicitudes de correo electrónico
Si no configura estos requisitos previos, el sitio envía una notificación por correo electrónico de solicitudes de la aplicación sin vínculos para aprobar ni denegar la solicitud.  

- En las propiedades del sitio, active la opción **Habilitar el punto de conexión REST para todos los roles de proveedor de este sitio y permitir el tráfico de puerta de enlace de Configuration Manager en la nube**. Para más información, consulte [Acceso a datos del punto de conexión de OData](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access).  

    - Reinicie el servicio SMS_EXEC después de habilitar el punto de conexión REST.

- [Puerta de enlace de administración en la nube](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- Incorpore el sitio a los [servicios de Azure](../servers/deploy/configure/azure-services-wizard.md) para la **administración en la nube**.  

    - Habilite [Detección de usuarios de Azure AD](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc).  

    - Configure manualmente los valores siguientes para esta aplicación nativa en Azure AD:  

        - **URI de redireccionamiento**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`. Use el nombre de dominio completo (FQDN) del servicio de Cloud Management Gateway (CMG), como GraniteFalls.Contoso.com.   

        - **Manifiesto**: establezca **oauth2AllowImplicitFlow** en true: `"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Haga la prueba

Intente completar las tareas. Luego envíe [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) con sus opiniones sobre la característica.

1. En la consola de Configuration Manager, implemente una aplicación como disponible para una recopilación de usuarios. En la página **Configuración de implementación**, habilítela para su aprobación. Luego escriba una dirección de correo electrónico *única* para recibir una notificación.  

     > [!Note]  
     > Cualquier persona de su organización de Azure AD que reciba el correo electrónico puede aprobar la solicitud. No reenvíe el correo electrónico a otros usuarios a menos que quiera que ellos lleven a cabo alguna acción.  

2. Como usuario, solicite la aplicación en Centro de software.  

3. Recibirá una notificación por correo electrónico similar al ejemplo siguiente:  

![Notificación por correo electrónico de ejemplo para la aprobación de aplicación](media/1321550-email.png)

> [!Note]  
> El vínculo para aprobar o denegar es para un solo uso. Por ejemplo, digamos que configura un alias de grupo para recibir notificaciones. Meg aprueba la solicitud. Y ahora, Bruce no puede denegarla.  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a> Mejora en la salida del script
<!--1236459-->

Ahora puede ver una salida de script detallada sin formato o con formato JSON estructurado. Este formato permite leer y analizar la salida de manera más sencilla. Si el script devuelve texto válido con formato JSON, podrá ver la salida detallada como **salida JSON** o **salida sin formato**. En caso contrario, la única opción es **Salida de script**. 

#### <a name="example-script-output-is-valid-json"></a>Ejemplo: la salida de script es un archivo JSON válido
Comando: `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Ejemplo: la salida de script no es un archivo JSON válido
Comando: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Haga la prueba

Intente completar las tareas. Luego envíe [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) con sus opiniones sobre la característica.

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Recopilaciones de dispositivos**. Haga clic con el botón derecho en una recopilación y seleccione **Ejecutar script**. Para más información sobre cómo crear y ejecutar scripts, consulte [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md).  

2. Ejecute un script en la recopilación de destino.  

3. En la página **Supervisión del estado del script** del Asistente para la ejecución de scripts, seleccione la pestaña **Resumen** en la parte inferior. Cambie las dos listas desplegables que se encuentran en la parte superior a **Salida de script** y **Tabla de datos**. Luego, haga doble clic en la fila de resultados para abrir el cuadro de diálogo **Salida detallada**.  

4. En la página **Supervisión del estado del script** del Asistente para la ejecución de scripts, seleccione la pestaña **Detalles de ejecución** en la parte inferior. Haga doble clic en la fila de resultados para abrir el cuadro de diálogo Salida detallada correspondiente a ese dispositivo.  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a> Mejora de las actualizaciones de software de terceros
<!--1358714-->

Ahora puede modificar las propiedades de los catálogos personalizados.

Para más información, consulte [Soporte técnico de actualizaciones de software de terceros para catálogos personalizados](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate).



## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo instalar o actualizar la rama Technical Preview, consulte [Technical Preview](technical-preview.md).    

Para más información sobre las distintas ramas de Configuration Manager, consulte [¿Qué rama de Configuration Manager debo utilizar?](../understand/which-branch-should-i-use.md)
