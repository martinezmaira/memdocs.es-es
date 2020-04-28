---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: Conozca las nuevas características disponibles en la versión Technical Preview 1806 de Configuration Manager.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 647eba601cbfa5304bf02f8bcf059fe6e851cbf0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074068"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Funciones de Technical Preview 1806 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en Technical Preview 1806 de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de versión preliminar técnica. 

Revise el artículo [Technical Preview para System Center Configuration Manager](technical-preview.md) antes de instalar esta actualización. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conocidos de esta Technical Preview

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a> El sitio no puede actualizarse con la biblioteca de contenido remota
<!--514642-->
El sitio no se puede actualizar y muestra los siguientes errores en **cmupdate.log**:  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

El problema se produce en esta versión cuando la biblioteca de contenido está en una ubicación remota.

#### <a name="workaround"></a>Solución alternativa
Transfiera la biblioteca de contenido a una unidad local del servidor de sitio. Para obtener más información, consulte [Configuración de una biblioteca de contenido remoto para el servidor de sitio](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server). 



</br>

**Estas son las nuevas características que puede probar con esta versión.**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a> Actualizaciones de software de terceros
<!--1352101-->
En esta versión se amplía la compatibilidad con las actualizaciones de software de terceros como resultado de los [comentarios de UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co) de los clientes. Ya no es necesario utilizar System Center Updates Publisher (SCUP) en algunos escenarios comunes. El nuevo nodo **Catálogos de actualizaciones de software de terceros** de la consola de Configuration Manager permite suscribirse a catálogos de terceros, publicar sus actualizaciones en el punto de actualización de software e implementarlas posteriormente en los clientes. 

En esta versión están disponibles los siguientes catálogos de actualizaciones de software de terceros:

 | Publicador | Nombre del catálogo |
 |--------|---------------------|
 | HP | HP Client Updates Catalog |

SCUP continúa siendo compatible con otros catálogos y escenarios. La lista de catálogos del nodo Catálogos de actualizaciones de software de terceros de la consola de Configuration Manager es dinámico y se actualizará a medida que aparezcan y se acepten nuevos catálogos.


### <a name="prerequisites"></a>Requisitos previos
- Configure la administración de actualizaciones de software, con un punto de actualización de software habilitado para HTTPS. Para obtener más información, consulte [Prepare for software updates management](../../sum/get-started/prepare-for-software-updates-management.md) (Preparación para la administración de actualizaciones de software).  
  - El punto de actualización de software debe encontrarse en el servidor de sitio para esta característica en esta versión. <!--515810--> 

    > [!Tip]  
    > El punto de actualización de software requiere HTTPS porque es un requisito para las API de WSUS que se usan para administrar certificados de firma. No es necesario que los clientes también estén habilitados para HTTPS. Para obtener más información sobre cómo habilitar HTTPS en WSUS, vea los artículos siguientes para obtener ayuda:  
    > - [Secure WSUS with the Secure Sockets Layer Protocol](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) (Protección de WSUS con el protocolo Capa de sockets seguros) 
    > - [Entrada del blog de soporte técnico de WSUS](https://blogs.technet.microsoft.com/sus/2011/05/09/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names/)

- Espacio en disco suficiente en el punto de actualización de software (la carpeta WSUSContent) para almacenar el contenido binario de origen de las actualizaciones de software de terceros. La cantidad de almacenamiento necesaria varía según el proveedor, los tipos de actualizaciones y las actualizaciones específicas que se publican para la implementación. Si necesita mover la carpeta WSUSContent a otra unidad con más espacio disponible, consulte el artículo del blog del equipo de soporte técnico de WSUS sobre [cómo cambiar la ubicación donde WSUS almacena las actualizaciones localmente](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/).  

- Habilite e implemente la configuración de cliente [Habilitar actualizaciones de software de terceros](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) en el grupo **Actualizaciones de software**.  

- El servidor de sitio requiere conexión a Internet para acceder a download.microsoft.com a través del puerto HTTPS 443. El servicio de sincronización de actualizaciones de software de terceros se ejecuta actualmente en el servidor de sitio. Este servicio actualiza la lista de catálogos disponibles de otros fabricantes, los descarga cuando se suscribe y descarga las actualizaciones en el momento en que se publican. Si es necesario, configure el proxy de internet en la pestaña **Proxy** de las propiedades del rol de sistema de sitio del equipo del servidor de sitio.  


### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fase 1: Habilitar y configurar la característica
Realice los pasos siguientes *una vez por cada jerarquía* para habilitar y configurar la característica:  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Seleccione el sitio de nivel superior en la jerarquía. En la cinta, haga clic en **Configurar componentes de sitio** y seleccione **Punto de actualización de software**.  

3. Cambie a la pestaña **Actualizaciones de terceros**. Seleccione la opción **Habilitar actualizaciones de software de terceros**. Para obtener más información acerca de las opciones de certificado, consulte [Mejoras para habilitar la compatibilidad de actualización de software de terceros](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Si utiliza la opción predeterminada de Configuration Manager para administrar este certificado, se crea un nuevo certificado de tipo **Firma de WSUS de terceros** en el nodo **Certificados**, en la sección **Seguridad** del área de trabajo de **Administración**.  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fase 2: Suscribirse a un catálogo de terceros y sincronizar las actualizaciones
Realice los pasos siguientes para *cada catálogo de aplicaciones de terceros* al que quiera suscribirse:  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Actualizaciones de software** y seleccione el nodo **Catálogos de actualizaciones de software de terceros**.  

2. Seleccione el catálogo al que quiera suscribirse y haga clic en **Suscribirse al catálogo** en la cinta de opciones.   

3. Revise y apruebe el certificado de catálogo.  

   > [!Note]  
   > Cuando se suscribe a un catálogo de actualizaciones de software de terceros, el certificado que revisa y aprueba en el asistente se agrega al sitio. Este certificado es de tipo **Catálogo de actualizaciones de software de terceros**. Se puede administrar desde el nodo **Certificados** de la sección **Seguridad** en el área de trabajo de **Administración**.  

4. Complete el asistente.  

   > [!Tip]  
   > Después de la suscripción inicial, el catálogo debería de empezar a descargarse de inmediato. En adelante, el catálogo se sincronizará cada 24 horas en esta versión. Si no quiere esperar a que el catálogo se descargue automáticamente, haga clic en **Sincronizar ahora** en la cinta de opciones.  
   > 
   > Después de descargar el catálogo, los metadatos del producto deben sincronizarse con el punto de actualización de software. Para obtener más información sobre este proceso, así como para iniciarlo manualmente, consulte [Sincronizar actualizaciones de software](../../sum/get-started/synchronize-software-updates.md). En este momento, puede ver las actualizaciones de terceros en el nodo **Todas las actualizaciones**. 

5. A continuación, configure el punto de actualización de software **Productos** para aplicarlo al catálogo de aplicaciones de terceros al que se ha suscrito. Para más información, vea [Configurar las clasificaciones y los productos que va a sincronizar](../../sum/get-started/configure-classifications-and-products.md). Cuando cambien los criterios del producto, será necesario sincronizar de nuevo las actualizaciones de software.

Para poder ver los resultados del cumplimiento de los clientes, estos deben primero examinar y evaluar las actualizaciones. Para desencadenar manualmente este ciclo desde el panel de control de Configuration Manager en un cliente mediante, ejecute la acción **Ciclo de detecciones de actualizaciones de software**. Para obtener más información sobre el proceso, consulte la [introducción a las actualizaciones de Software](../../sum/understand/software-updates-introduction.md).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Fase 3: Implementar las actualizaciones de software de terceros
Realice los pasos siguientes con *las actualizaciones de software de terceros* que quiera implementar en los clientes:  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Actualizaciones de software** y seleccione el nodo **Todas las actualizaciones de software**.  

   > [!Tip]  
   > Haga clic en **Agregar criterios** para filtrar la lista de actualizaciones. Por ejemplo, para ver todas las actualizaciones de Adobe, agregue **Proveedor** para **Adobe Systems, Inc.**  

2. Seleccione las actualizaciones requeridas por los clientes. Haga clic en **Publicar el contenido de la actualización de software de terceros** y revise el progreso en SMS_ISVUPDATES_SYNCAGENT.log. Esta acción descarga los archivos binarios de actualización del proveedor y los almacena en la carpeta WSUSContent que está ubicada en el punto de actualización de software. También modifica el estado de la actualización, que pasa de contener solo metadatos, a incluir contenido y poder implementarse.  

   > [!Note]  
   > Al publicar contenido de la actualización de software de terceros, los certificados usados para firmar el contenido se agregan al sitio. Estos certificados son de tipo **Contenido de actualizaciones de software de terceros**. Se pueden administrar desde el nodo **Certificados** de la sección **Seguridad** en el área de trabajo de **Administración**.  

3. Implemente las actualizaciones utilizando para ello el proceso de administración de actualizaciones de software existente. Para obtener más información, consulte [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) (Implementación de actualizaciones de software). En la página **Ubicaciones de descarga** del Asistente para implementar actualizaciones de software, seleccione la opción predeterminada para **Descargar actualizaciones de software de Internet**. En este escenario, el contenido ya está publicado en el punto de actualización de software, que se utiliza para descargar el contenido del paquete de implementación.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Supervisión del progreso de las actualizaciones de software de terceros
La sincronización de actualizaciones de software de terceros se controla mediante el componente SMS_ISVUPDATES_SYNCAGENT en el servidor de sitio. Puede ver los mensajes de estado de este componente, o ver un estado más detallado en SMS_ISVUPDATES_SYNCAGENT.log. Este registro se encuentra en el servidor de sitio, dentro de la subcarpeta **Registros** del directorio de instalación del sitio. De forma predeterminada, esta ruta de acceso es `C:\Program Files\Microsoft Configuration Manager\Logs`. Para obtener más información sobre la supervisión del proceso general de administración de actualizaciones de software, vea [Supervisar las actualizaciones de software](../../sum/deploy-use/monitor-software-updates.md).


### <a name="known-issues"></a>Problemas conocidos
- El servicio de sincronización de actualizaciones de software de terceros no admite que el punto de actualización de software esté configurado para usar una **cuenta de conexión del servidor de WSUS**. Si esta cuenta está configurada en la pestaña **Configuración de cuenta y proxy** de la página Propiedades del punto de actualización de software, verá el siguiente error en SMS_ISVUPDATES_SYNCAGENT.log:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Para más información sobre esta cuenta, consulte [Cuenta de conexión de punto de actualización de software](../plan-design/hierarchy/accounts.md#software-update-point-connection-account).<!--515492-->  

- No combine otras herramientas como SCUP con esta nueva característica integrada de actualización de software de terceros. El servicio de sincronización de actualización de software de terceros no puede publicar contenido en las actualizaciones de solo metadatos que otra aplicación, herramienta o script —como SCUP— haya agregado a WSUS. La acción **Publicar el contenido de la actualización de software de terceros** genera un error en estas actualizaciones. Si necesita implementar actualizaciones de terceros aún no admitidas por esta característica, use en su totalidad el proceso existente para implementar esas actualizaciones.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurar SmartScreen de Windows Defender para Microsoft Edge
<!--1353701-->
Esta versión agrega tres configuraciones de [SmartScreen de Windows Defender](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) a la [directiva de configuración de cumplimiento del explorador Microsoft Edge](../../compliance/deploy-use/browser-profiles.md). La directiva ahora incluye los siguientes valores adicionales en la página **Configuración de SmartScreen**:
- **Permitir SmartScreen**: especifica si se permite SmartScreen de Windows Defender. Para obtener más información, consulte la [directiva de explorador AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Los usuarios pueden invalidar los avisos de SmartScreen para los sitios**: especifica si los usuarios pueden invalidar las advertencias del filtro SmartScreen de Windows Defender sobre sitios web potencialmente malintencionados. Para obtener más información, consulte la [directiva de explorador PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Los usuarios pueden invalidar los avisos de SmartScreen para los archivos**: especifica si los usuarios pueden invalidar las advertencias del filtro SmartScreen de Windows Defender sobre la descarga de archivos no comprobados. Para obtener más información, consulte la [directiva de explorador PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Sincronizar directiva MDM desde Microsoft Intune para un dispositivo administrado conjuntamente
<!--1357377-->
A partir de esta versión, cuando se [cambia una carga de trabajo de administración compartida](../../comanage/how-to-switch-workloads.md), los dispositivos administrados conjuntamente sincronizan automáticamente la directiva MDM de Microsoft Intune. Esta sincronización también se produce al iniciar la acción **Descargar directiva de equipo** desde Notificaciones de cliente en la consola de Configuration Manager. Para obtener más información, vea [Iniciar la recuperación de directivas de cliente mediante la notificación de cliente](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Transición de la carga de trabajo de Office 365 a Intune mediante la administración conjunta
<!--1357841-->
Ahora puede pasar la carga de trabajo de Office 365 de Configuration Manager a Microsoft Intune después de habilitar la administración conjunta. Para realizar la transición de esta carga de trabajo, vaya a la página de propiedades de administración conjunta y mueva la barra deslizante de Configuration Manager a Piloto o a Todo. Para más información, vea [Administración conjunta para dispositivos de Windows 10](../../comanage/overview.md).

También hay una nueva condición global, **Are Office 365 applications managed by Intune on the device** (¿Las aplicaciones de Office 365 están administradas por Intune en este dispositivo?). Esta condición se agrega de forma predeterminada como requisito a las nuevas aplicaciones de Office 365. Cuando se hace la transición de esta carga de trabajo, los clientes administrados conjuntamente no cumplen el requisito en la aplicación. Por lo tanto, no instale Office 365 implementado a través de Configuration Manager.

### <a name="known-issue"></a>Problema conocido
- Esta transición de carga de trabajo actualmente solo se aplica a las implementaciones de Office 365. Configuration Manager continúa administrando las actualizaciones de Office 365.<!--510876--> Para obtener más información y una posible solución alternativa, consulte las notas de la versión 1802 de Configuration Manager [No se aplica la configuración cliente de cambios de Office 365](../servers/deploy/install/release-notes.md).



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager es ahora una herramienta integrada que permite convertir paquetes de Configuration Manager 2007 heredados en aplicaciones de la rama actual Configuration Manager. Luego, pueden usarse las características de aplicaciones como dependencias, reglas de requisitos y afinidad entre usuario y dispositivo.

> [!Tip]  
> En [TechNet](https://technet.microsoft.com/library/hh531519.aspx) puede encontrar documentación heredada sobre la funcionalidad existente en Package Conversion Manager. Hay información importante en proceso para migrar a la biblioteca de docs.microsoft.com.

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

> [!Important]  
> Si tiene instalada una versión anterior de Package Conversion Manager, desinstálela antes de actualizar el sitio. La nueva versión integrada no requiere la instalación, pero puede entrar en conflicto con las versiones existentes.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Administración de aplicaciones** y seleccione **Paquetes**.  
2. Seleccione un paquete. Las tres opciones siguientes están disponibles en el grupo **Package Conversion** (Conversión de paquetes) de la cinta de opciones:  
     - **Analyze Package** (Analizar paquete): el proceso de conversión se inicia con el análisis del paquete.
     - **Convert Package** (Convertir paquete): con esta acción, algunos paquetes se pueden convertir fácilmente en aplicaciones.
     - **Fix and Convert** (Corregir y convertir): algunos paquetes requieren que se corrijan los problemas antes de su conversión en aplicaciones.  

   Para obtener más información sobre estas acciones, consulte [Cómo analizar y convertir paquetes](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29).  

3. Vaya al área de trabajo **Monitoring** (Supervisión) y seleccione **Package Conversion Status** (Estado de conversión de paquete). Este nuevo panel muestra el análisis general y el estado de conversión de los paquetes del sitio. Los datos de análisis se resumen automáticamente mediante una nueva tarea en segundo plano.  

   > [!Tip]  
   > Package Conversion Manager no requiere que se programe el análisis de paquetes. Esta acción está ahora controlada por la tarea integrada de resumen.  

![Captura de pantalla del panel de estado de conversión de paquetes](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Implementar actualizaciones de software sin contenido
<!--1357933-->
Ahora puede implementar las actualizaciones de software en los dispositivos sin antes descargar y distribuir el contenido de la actualización de software a los puntos de distribución. Esta característica es útil cuando se trabaja con contenido de actualización extremadamente grande, o cuando se quiere que los clientes obtengan siempre el contenido desde el servicio de nube de Microsoft Update. En este escenario, los clientes también pueden descargar el contenido desde los equipos del mismo nivel que ya tienen el contenido necesario. El cliente de Configuration Manager sigue administrando la descarga del contenido, por lo que puede usar la característica de caché del mismo nivel de Configuration Manager u otras tecnologías como, por ejemplo, Optimización de distribución. Esta característica es compatible con cualquier tipo de actualización admitida por la administración de actualizaciones de software de Configuration Manager, incluidas las actualizaciones de Windows y Office. 

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. Inicie una implementación de actualizaciones de software del modo habitual. Para obtener más información, consulte [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) (Implementación de actualizaciones de software).
2. En el Asistente para implementar actualizaciones de software, en la página **Paquete de implementación**, seleccione la opción nueva para **No deployment package** (Ningún paquete de implementación).

### <a name="known-issues"></a>Problemas conocidos
- El icono de una actualización que se implementan con esta configuración muestra incorrectamente una X roja como si la actualización no fuese válida. Para obtener más información, consulte [Iconos que se usan para las actualizaciones de software](../../sum/understand/software-updates-icons.md). <!--515556-->  
- Esta configuración solo se integra con el Asistente para implementar actualizaciones de software. Actualmente no está disponible con reglas de implementación automática. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integración de la Herramienta de personalización de Office en el instalador de Office 365
<!--1358149-->
La Herramienta de personalización de Office está ahora integrada con el programa de instalación de Office 365 en la consola de Configuration Manager. Al crear una implementación de Office 365, ahora puede configurar de manera dinámica la configuración más reciente de la manejabilidad de Office. La Herramienta de personalización de Office se actualiza al mismo tiempo que la versión de las nuevas compilaciones de Office 365. Esto permite sacar partido de nuevos valores de manejabilidad en Office 365 en cuanto están disponibles. 

### <a name="prerequisites"></a>Requisitos previos
- El equipo que ejecuta la consola de Configuration Manager necesita acceso a Internet a través del puerto HTTPS 443. El Asistente para instalación de cliente de Office 365 usa una API de explorador web estándar de Windows para abrir https://config.office.com. Si se utiliza un proxy de Internet, el usuario debe poder tener acceso a esta dirección URL.

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software** y seleccione el nodo **Administración de clientes de Office 365**.
2. En el panel, haga clic en el mosaico del **Instalador de Office 365** para iniciar el Asistente para instalación de cliente de Office 365. Para obtener más información, consulte [Implementación de aplicaciones de Office 365](../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).
3. En la página **Office Setting** (Configuración de Office), haga clic en **Go To Office Web Page** (Ir a la página web de Office). Utilice la Herramienta de personalización de Office online para especificar la configuración de esta implementación. 
4. Cuando haya finalizado, haga clic en **Enviar** en la esquina superior derecha. Finalice el Asistente para la instalación de cliente de Office 365.



## <a name="improvements-to-cloud-management-gateway"></a>Mejoras en Cloud Management Gateway
Esta versión incluye las mejoras siguientes en Cloud Management Gateway (CMG):

### <a name="simplified-client-bootstrap-command-line"></a>Línea de comandos de arranque de cliente simplificada
<!--1358215-->
Al instalar el cliente de Configuration Manager en Internet a través de una CMG, ahora son necesarias menos propiedades de línea de comandos. Para obtener más información sobre un ejemplo de este escenario, vea el [Línea de comandos para instalar el cliente de Configuration Manager](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) cuando se prepare para la administración conjunta. 

Las siguientes propiedades de línea de comandos son necesarias en todos los escenarios:
- CCMHOSTNAME  
- SMSSITECODE  

Las propiedades siguientes son necesarias al usar Azure AD para la autenticación de cliente en lugar de certificados de autenticación de cliente basada en PKI:
- AADCLIENTAPPID  
- AADRESOURCEURI  

La siguiente propiedad es obligatoria si el cliente volverá a la intranet:
- SMSMP  

En el ejemplo siguiente se incluyen todas las propiedades anteriores:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obtener más información, vea [Acerca de las propiedades de instalación de clientes](../clients/deploy/about-client-installation-properties.md).

### <a name="download-content-from-a-cmg"></a>Descargar contenido desde un CMG
<!--1358651-->
Anteriormente, era necesario implementar un punto de distribución de nube y CMG como funciones independientes. Ahora, en esta versión, una CMG también puede servir contenido a los clientes. Esta funcionalidad reduce los certificados necesarios y el costo de máquinas virtuales de Azure. Para activar esta característica, habilite la nueva opción **Allow CMG to function as a cloud distribution point and serve content from Azure storage** (Permitir que CMG funcione como un punto de distribución de nube y servir el contenido desde el almacenamiento de Azure) en la pestaña **Settings** (Configuración) de las propiedades de CMG. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>El certificado raíz de confianza no es necesario con Azure AD
<!--503899-->
Para crear una CMG ya no es necesario proporcionar un [certificado raíz de confianza](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) en la página de configuración. Este certificado no es necesario cuando se usa Azure Active Directory (Azure AD) para la autenticación de cliente, pero solía ser necesario en el asistente.

> [!Important]  
> Si usa certificados de autenticación de cliente PKI, entonces todavía debe agregar un certificado raíz de confianza a la CMG.



## <a name="improvements-to-secure-client-communications"></a>Mejoras en las comunicaciones de cliente seguras
<!--1358278,1358279-->
Esta versión insiste en la [mejora de las comunicaciones de cliente seguras](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) al eliminar las dependencias adicionales en la cuenta de acceso de red. Cuando se habilita en el sitio nuevo la opción **Use Configuration Manager-generated certificates for HTTP site systems** (Usar certificados generados por Configuration Manager para sistemas de sitios HTTP), los escenarios siguientes no requieren una cuenta de acceso de red al descargar contenido desde un punto de distribución:  

- Secuencias de tareas que se ejecutan desde un entorno PXE o medios de arranque
- Secuencias de tareas que se ejecutan desde el Centro de software  

Estas secuencias de tareas pueden ser para la implementación del sistema operativo o ser personalizadas. También se admite para los equipos del grupo de trabajo.



## <a name="software-center-infrastructure-improvements"></a>Mejoras de la infraestructura del Centro de software
<!--1358309-->
Los roles del catálogo de aplicaciones ya no son necesarios para mostrar las aplicaciones disponibles para el usuario en el Centro de software. Este cambio ayuda a reducir la infraestructura de servidor necesaria para entregar las aplicaciones a los usuarios. El Centro de software se basa ahora en el punto de administración para obtener esta información, lo que facilita el escalado de los entornos de mayor tamaño al asignarlos a [grupos de límites](../servers/deploy/configure/boundary-groups.md#management-points).

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. Quite todos los roles de catálogo de aplicaciones del sitio. Entre estos roles están el punto de servicio web del catálogo de aplicaciones y el punto de sitio web del catálogo de aplicaciones.
2. Implemente una aplicación como disponible para una colección de usuarios.
3. Use el Centro de software como un usuario de destino para buscar, solicitar e instalar la aplicación.

### <a name="known-issue"></a>Problema conocido
- Si usa un cliente unido a Azure Active Directory con esta característica, no configure el sitio para usar certificados generados por Configuration Manager para sistemas de sitios HTTP (**Use Configuration Manager-generated certificates for HTTP site systems**). Actualmente está en conflicto con esta característica.<!--515846--> Para obtener más información sobre esta configuración, consulte [Comunicaciones de cliente seguras mejoradas](capabilities-in-technical-preview-1805.md#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Aprovisionar los paquetes de aplicación de Windows para todos los usuarios en un dispositivo
<!--1358310-->
Ahora puede aprovisionar una aplicación con un paquete de aplicación de Windows para todos los usuarios en el dispositivo. Un ejemplo común de este escenario es el aprovisionamiento de una aplicación de Microsoft Store para Empresas y Educación, como Minecraft: Education Edition, en todos los dispositivos que usan los alumnos de una escuela. Anteriormente, Configuration Manager solo admitía la instalación de estas aplicaciones por usuario. Tras iniciar sesión en un dispositivo nuevo, un estudiante tendría que esperar para obtener acceso a una aplicación. Ahora, al aprovisionarse la aplicación en el dispositivo para todos los usuarios, estos pueden empezar a trabajar más rápidamente.

> [!Important]  
> Tenga cuidado con la instalación, el aprovisionamiento y la actualización de versiones diferentes del mismo paquete de aplicación de Windows en un dispositivo, ya que puede producir resultados inesperados. Este comportamiento puede producirse si se usa Configuration Manager para aprovisionar la aplicación y, después, se permite a los usuarios actualizar la aplicación desde Microsoft Store. Para obtener más información, consulte las instrucciones del paso siguiente si [administra aplicaciones de Microsoft Store para Empresas](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Al aprovisionar una aplicación con licencia sin conexión, Configuration Manager no permite que Windows la actualice automáticamente desde Microsoft Store.  

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. Cree una aplicación nueva. Esta aplicación debe provenir de un paquete de aplicación de Windows —o ser una aplicación con licencia sin conexión— que se haya sincronizado desde Microsoft Store para empresas y educación.  

2. En la página **Información general** del asistente para crear aplicaciones, habilite la opción para **Provision this application for all users on the device** (Aprovisionar esta aplicación para todos los usuarios en el dispositivo).  

   > [!Tip]  
   > Si va a modificar una aplicación existente, esta opción está en la pestaña de **Experiencia del usuario** de las propiedades de la aplicación.  

3. Implemente la aplicación en una colección de dispositivos.  

4. Inicie sesión en un dispositivo de destino con distintas cuentas de usuario e inicie la aplicación.  

> [!Note]  
> Si necesita desinstalar una aplicación aprovisionada de dispositivos en los que los usuarios ya han iniciado sesión, deberá crear dos implementaciones de desinstalación. Dirija la primera instalación de desinstalación a una colección de dispositivos que contenga los dispositivos. Dirija la segunda implementación de desinstalación a una colección que contenga los usuarios que ya han iniciado sesión en los dispositivos que incluyan la aplicación aprovisionada. Cuando se desinstala una aplicación aprovisionada de un dispositivo, Windows no desinstala actualmente la aplicación para los usuarios. 



## <a name="improvements-to-the-surface-dashboard"></a>Mejoras en el panel de Surface
<!--1358654-->
Esta versión incluye las siguientes mejoras en el [panel de Surface](../clients/manage/surface-device-dashboard.md):
- Ahora, en el panel de Surface se muestra una lista de los dispositivos correspondientes al seleccionar las secciones de un gráfico.
   - Al hacer clic en el mosaico **Porcentaje de dispositivos Surface**, se abre una lista de dispositivos de Surface.
   - Al hacer clic en una barra del mosaico **Cinco versiones principales de firmware**, se abre una lista de los dispositivos de Surface que cuentan con esa versión concreta de firmware.
- Al visualizar estas listas de dispositivos en el panel de Surface, se puede hacer clic con el botón derecho en un dispositivo para llevar a cabo a acciones comunes.



## <a name="hardware-inventory-default-unit-revision"></a>Revisión de unidad predeterminada de inventario de hardware
<!--514442-->
En [Configuration Manager versión 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure), la unidad predeterminada de las vistas de informes se cambió de megabytes (MB) a gigabytes (GB). Debido a las [mejoras en el inventario de hardware para los valores enteros grandes](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values), y en base a los comentarios de los clientes, esta unidad predeterminada vuelve a ser MB.



## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
