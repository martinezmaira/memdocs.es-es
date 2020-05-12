---
title: Funcionalidades de Technical Preview 1605
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1605.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: d52725e0127f7129a3962cd3ef178d2540bb785a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905749"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Funciones de Technical Preview 1605 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1605 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager.      Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.  

 **Problemas conocidos de esta Technical Preview:**  

- Con Technical Preview 1605, si actualiza las propiedades de un punto de administración después de que esté instalado, puede ver un error de la consola que obliga a cerrarla.  Si ocurre esto, puede desinstalar el punto de administración y luego volver a instalarlo con la configuración deseada. También puede modificar el punto de administración antes de instalar Technical Preview 1605.  

- Si usa la característica Tienda Windows para empresas con Technical Preview 1604 y luego actualiza a Technical Preview 1605, ya no podrá ver los datos de incorporación. Las demás características siguen funcionando. Si se incorporó con Technical Preview 1604, seguirá incorporado después de instalar Technical Preview 1605 sin necesidad de hacer nada más.  

  **Estas son las nuevas características que puede probar con esta versión.**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a> VPN por aplicación para dispositivos Windows 10  
 En los dispositivos Windows 10 administrados con Configuration Manager con Intune, puede agregar una lista de aplicaciones que abran automáticamente una conexión VPN que haya configurado mediante la consola de administración de Configuration Manager. Tiene la opción de restringir el tráfico VPN a esas aplicaciones o puede seguir permitiendo todo el tráfico a través de la conexión VPN.  

 **Requisitos**:  

-   Configuration Manager con Intune  

-   Un perfil de VPN de Windows 10 que se haya implementado en al menos un dispositivo  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a> Mejoras en la secuencia de tareas Instalar actualizaciones de software  
 Se han realizado las siguientes mejoras en la secuencia de tareas Instalar actualizaciones de software:  

-   Hay disponible una nueva variable de secuencia de tareas, SMSTSSoftwareUpdateScanTimeout, para ofrecerle la posibilidad de controlar el tiempo de espera en la detección de actualizaciones de software durante el paso de la secuencia de tareas Instalar actualizaciones de software. El valor predeterminado es 30 minutos.  

-   Ha habido mejoras en el registro. El archivo de registro smsts.log contendrá nuevas entradas de registro que hagan referencia a otros archivos de registro que le ayuden a solucionar problemas durante el proceso de instalación de actualizaciones de software.  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a> Mejoras en el paso Preparar cliente de Configuration Manager para la captura de la secuencia de tareas  
 El paso Preparar el cliente de Configuration Manager quitará por completo el cliente de Configuration Manager en lugar de quitar solo la información de clave. Cuando la secuencia de tareas implementa la imagen capturada del sistema operativo, se instala un nuevo cliente de Configuration Manager cada vez.  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a> Período de gracia para las implementaciones de aplicaciones necesarias  
 En algunos casos, es posible que quiera dar más tiempo a los usuarios para instalar las implementaciones de aplicaciones necesarias más allá de los plazos que estableció. Por ejemplo, si un usuario final acaba de volver de vacaciones, es posible que tenga que esperar bastante mientras se instalan las implementaciones de aplicaciones vencidas. No obstante, aún puede instalar la aplicación de inmediato en cualquier momento que quiera.  

 Para solucionar este problema, puede definir un **período de gracia** mediante la implementación de la configuración de cliente de Configuration Manager en una colección.  

 Para configurar el período de gracia, haga lo siguiente:  

1. En la página **Agente de equipo** de la configuración de cliente, configure la nueva propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** con un valor entre **1** y **120** horas.  

2. En una nueva implementación de aplicación o en las propiedades de una implementación existente, en la página **Programación**, active la casilla de verificación **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario** hasta el período de gracia definido en la configuración del cliente.  

    Todas las implementaciones que tienen activada esta casilla y que están destinadas a dispositivos en los que también se ha implementado la configuración de cliente usarán el período de gracia.  

   En esta versión, los dispositivos cliente no usan el período de gracia que configure. Si configura un período de gracia y activa la casilla, la aplicación se instalará en la primera ventana que no sea de empresa que configure el usuario después de la fecha límite.  

   Se han agregado opciones similares al asistente para la implementación de actualizaciones de software, al asistente para reglas de implementación automática y a las páginas de propiedades, pero de momento no están implementadas en esta Technical Preview.  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a> Nueva experiencia para acciones del dispositivo remoto  
 Se ha mejorado la experiencia para realizar acciones de dispositivo remoto desde la consola de Configuration Manager.  
Acciones comunes como **Retirar/borrar**, **Restablecer contraseña**, **Bloqueo remoto** y **Omitir bloqueo de activación** ahora se encuentran en el menú **Acciones de dispositivo remoto**, al que se accede desde el área de trabajo **Activos y compatibilidad**.  

 ![Captura de pantalla de las nuevas acciones de dispositivo remoto](media/New-Remote-Device-Actions.png)  

 Encontrará el estado de cada una de estas operaciones en las ubicaciones siguientes:  

- En el panel de detalles al seleccionar un dispositivo desde el nodo **Dispositivos**.  

- En la página **Propiedades** de un dispositivo.  

- En la página principal del nodo **Dispositivos** (no todas las columnas podrían estar visibles de forma predeterminada).  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a> Tienda Windows para aplicaciones empresariales  
 La [Tienda Windows para empresas](https://www.microsoft.com/business-store) es el lugar donde puede buscar y adquirir aplicaciones para su organización, individualmente o por volumen. Al conectar la tienda a Configuration Manager, puede administrar aplicaciones adquiridas por volumen desde la consola de Configuration Manager, por ejemplo:  

- Puede sincronizar la lista de aplicaciones adquiridas con Configuration Manager.  

- Las aplicaciones que se sincronizan aparecen en la consola de Configuration Manager y se pueden implementar igual que cualquier otra aplicación.  

- Cada 24 horas, Configuration Manager descarga información de licencia de las aplicaciones de la tienda que se puede revisar en la consola de Configuration Manager.  

  En la versión 1604 de Technical Preview, puede sincronizar y ver las aplicaciones de la Tienda Windows para empresas en la consola de Configuration Manager. En esta versión, se ha agregado la posibilidad de crear e implementar aplicaciones de Configuration Manager a partir de aplicaciones sincronizadas de la tienda.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Configurar la sincronización de la Tienda Windows para empresas  

1.  En Azure Active Directory, registre Configuration Manager como una herramienta de administración "Aplicación web o API web". De este modo, obtendrá un identificador de cliente que necesitará más adelante.  

    1.  En el nodo de Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), seleccione Azure Active Directory y, luego, haga clic en **Aplicaciones** > **Agregar**.  

    2.  Haga clic en **Agregar una aplicación que mi organización está desarrollando**.  

    3.  Escriba un nombre para la aplicación, seleccione **Aplicación web** y/o **API web** y haga clic en la flecha **Siguiente**.  

    4.  Escriba la misma dirección URL para **URL de inicio de sesión** y **URI de id. de aplicación**. La dirección URL puede ser cualquiera (no es necesario que se resuelva en una dirección real). Por ejemplo, puede escribir **https://&lt;suDominio>/sccm**.  

    5.  Complete el asistente.  

2.  En Azure Active Directory, cree una clave de cliente para la herramienta de administración registrada.  

    1.  Resalte la aplicación que acaba de crear y haga clic en **Configurar**.  

    2.  En **Claves**, seleccione una duración de la lista y haga clic en **Guardar**. De este modo, se creará una nueva clave de cliente. No salga de esta página hasta que haya incorporado correctamente la Tienda Windows para empresas a Configuration Manager.  

3.  En la Tienda Windows para empresas, configure Configuration Manager como la herramienta de administración de la tienda.  

    1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) e inicie sesión si se le solicita.  

    2.  Si es necesario, acepte los términos de uso.  

    3.  En **Herramientas de administración**, haga clic en **Agregar una herramienta de administración**.  

    4.  En **Buscar la herramienta por nombre**, escriba el nombre de la aplicación que creó anteriormente en AAD y luego haga clic en **Agregar**.  

    5.  Haga clic en **Activar** junto a la aplicación que acaba de importar.  

    6.  En el asistente **Mostrar aplicaciones con licencia sin conexión**, haga clic en **Sí** si quiere permitir la adquisición de aplicaciones con licencia sin conexión.  

4.  Adquiera al menos una aplicación de la Tienda Windows para empresas.  

5.  En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Servicios de nube** y luego haga clic en **Tienda Windows para empresas**.  

6.  En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Agregar cuenta de la Tienda Windows para empresas**.  

7.  Agregue el identificador de inquilino, el identificador de cliente y la clave de cliente de Azure Active Directory y finalice el asistente.  

8.  Una vez que haya terminado, verá la cuenta configurada en la lista **Cuentas de la Tienda Windows para empresas** en la consola de Configuration Manager.  

### <a name="try-it-out"></a>Haga la prueba  
 Intente realizar la siguiente tarea y háganos saber cómo le ha ido mediante el formulario de comentarios de la página [Programa de comentarios de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) del sitio de Microsoft Connect:  

 Cree e implemente una aplicación de Configuration Manager a partir de una aplicación con licencia sin conexión de la Tienda Windows para empresas.  

1. En el área de trabajo **Biblioteca de software** de la consola de Configuration Manager, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.  

2. Elija la aplicación que quiere implementar y, luego, en la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear aplicación**.  

   Se crea una aplicación de Configuration Manager que contiene la aplicación de la Tienda Windows para empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.  

> [!IMPORTANT]  
>  Cuando se crea una aplicación de Configuration Manager con un solo tipo de implementación a partir de una aplicación con licencia sin conexión, se puede implementar en dispositivos administrados mediante MDM y también administrados con el cliente de Configuration Manager. Si intenta implementar una aplicación con varios tipos de implementación, se producirá un error en la instalación.  
>   
>  De momento no se pueden implementar aplicaciones con licencia en línea con Configuration Manager.  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a> Mejoras generales para aplicaciones adquiridas por volumen  

-   En esta versión, las aplicaciones adquiridas por volumen en la Tienda Windows para empresas e iOS App Store se han consolidado en la misma vista, **Información de licencia para las aplicaciones de la Tienda**.  

-   En el caso de las aplicaciones iOS adquiridas por volumen, se ha quitado la pestaña del Programa de Compras por Volumen de Apple del cuadro de diálogo **Paquete de aplicación para explorador iOS** del Asistente para crear aplicaciones. Para crear una aplicación adquirida por volumen para iOS, siga estos pasos:  

    1.  1.  En el área de trabajo **Biblioteca de software** de la consola de Configuration Manager, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.  

    2.  2.  Elija la aplicación que quiere implementar y, luego, en la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear aplicación**.  

-   Ha cambiado la ubicación que se usa para obtener y cargar un token de PCV de Apple para aplicaciones adquiridas por volumen en la consola de Configuration Manager. Ahora puede hacerlo en el área de trabajo **Administración**, en el nodo **Servicios de nube** > **Tokens del Programa de Compras por Volumen de Apple**.  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a> Protección de datos empresariales (EDP)  
 Puede crear elementos de configuración que le permitan implementar las directivas de protección de datos empresariales (EDP), incluso que le permitan elegir las aplicaciones protegidas, el nivel de protección EDP y cómo buscar datos empresariales en la red. Para más información sobre EDP, vea los temas siguientes:  

- [Protege los datos de tu empresa con Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Creación e implementación de una directiva de Windows Information Protection (WIP) con Configuration Manager](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a> Los usuarios finales pueden instalar aplicaciones desde el Portal de empresa  
 MDM local se presentó en la versión 1511 de Configuration Manager. En versiones anteriores, se podían implementar aplicaciones en dispositivos de Windows 10 administrados por MDM con un propósito de implementación de instalación **Obligatoria** para dispositivos administrados por MDM locales.  

 En esta versión se pueden implementar aplicaciones con un propósito de implementación de **Disponible** para los usuarios de equipos de Windows 10 administrados por MDM locales y los usuarios pueden instalar estas aplicaciones ellos mismos desde el Portal de empresa.
En esta Technical Preview, si el Portal de empresa está abierto durante más de 15 minutos, el usuario final verá un mensaje de error. Para solucionar el problema, reinicie el Portal de empresa.  

### <a name="before-you-start"></a>Antes de empezar  

#### <a name="server-prerequisites"></a>Requisitos previos del servidor  

-   .NET 4.5 o superior (exige reiniciar)  

-   PowerShell 3.0 para el script de configuración (exige reiniciar)  

#### <a name="client-prerequisites"></a>Requisitos previos del cliente  

-   Windows 10 Escritorio 1511 (compilación del SO 10586.218) o posterior  

#### <a name="general-prerequisites"></a>Requisitos previos generales  

-   Asegúrese de haber finalizado los [pasos de preparación para la administración local de dispositivos móviles](../../mdm/plan-design/plan-on-premises-mdm.md) y de haber [inscrito los dispositivos](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md).  

-   Para la mejor experiencia de instalación de la aplicación al usar el Portal de empresa, asegúrese de que Configuration Manager tenga una conexión activa a Microsoft Intune.  

-   Si elige la opción de inscripción masiva, configure la afinidad entre usuario y dispositivo para el dispositivo inscrito antes de probar este escenario.  

### <a name="configuration-steps"></a>Pasos de configuración  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Instalar los roles del catálogo de aplicaciones y habilitar la compatibilidad con la administración de dispositivos móviles  

1.  Agregar los roles Servicio web del catálogo de aplicaciones y Sitios web  

    1.  Seleccione **Modo HTTPS** y la opción **Permitir que los dispositivos móviles usen este punto de servicio web del catálogo de aplicaciones**.  

    2.  Limitaciones de esta Technical Preview:  

        -   Debe desinstalar cualquier rol existente del catálogo de aplicaciones antes de seleccionar la opción que permite conectar dispositivos móviles.  

        -   Asegúrese de que haya un solo conjunto de roles del catálogo de aplicaciones y de que los roles se encuentren en el mismo sistema de sitio que los roles Punto de inscripción y Punto de proxy de inscripción.  

2.  Compruebe que los siguientes componentes están operativos desde el nodo Estado del componente de la consola de Configuration Manager:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Configurar límites  
 Configure los límites necesarios para los puntos de distribución solo de intranet.  

> [!NOTE]  
>  De momento solo se admiten límites de intervalo de IPv4 para la administración de dispositivos móviles.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Implementar la aplicación Portal de empresa y la configuración  

1. Use el script de configuración incluido en la Technical Preview para preparar la implementación y la configuración del Portal de empresa:  

   1. Abra una ventana de comandos de PowerShell con privilegios elevados.  

   2. Ejecute **set-executionPolicy RemoteSigned**  

   3. Desde la carpeta **&lt;directorio de instalación SCCM\>\cd.latest\SMSSETUP\TOOLS\MDM**, ejecute **.\ConfigurationScript.ps1**  

      El script de configuración hace lo siguiente:  

   4. Crea una aplicación de Configuration Manager con un tipo de implementación de paquete de aplicaciones de Windows mediante **CompanyPortalOnPremisesMDM.appx** en la misma carpeta.  

   5. Crea un elemento de configuración y una línea base de configuración que configura el Portal de empresa.  

   6. Implementa la línea base de configuración y la aplicación y agrega la aplicación a todos los puntos de distribución.  

   > [!NOTE]
   >  Si los roles del catálogo de aplicaciones no se encuentran en el sitio primario, haga lo siguiente:  
   > 
   > - En el área de trabajo **Activos y compatibilidad**, busque el elemento de configuración **OnPremMDM Portal Configuration CI - server urls**.  
   >   -   Cambie el valor **Reglas de compatibilidad** al nombre de dominio completo del sistema de sitio donde se encuentran los roles del catálogo de aplicaciones.  

2. Una vez implementadas la aplicación Portal de empresa y su configuración, compruebe que la aplicación y la línea base de configuración son compatibles con el dispositivo en cuestión mediante la sección **Implementaciones** de la consola de Configuration Manager. El Portal de empresa aparecerá como **Portal de empresa (Technical Preview)** en el menú de inicio del dispositivo.  

### <a name="try-it-out"></a>Haga la prueba  
 Intente realizar las siguientes tareas y háganos saber cómo le ha ido mediante el formulario de comentarios de la página [Programa de comentarios de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) del sitio de Microsoft Connect:  

1.  Implemente varias aplicaciones con tipos de implementación compatibles para una colección de usuarios con un propósito de implementación de **Disponible**. En esta Technical Preview, las aplicaciones que exigen aprobación del administrador no se admiten y no aparecerán en el Portal de empresa.  

2.  Los usuarios pueden buscar e instalar aplicaciones desde el Portal de empresa.  

     Después de abrir el Portal de empresa, verá un cuadro de diálogo de autenticación denominado **Configuration Manager**. Especifique las credenciales de Active Directory del usuario (ya sea con el formato user@domain o con dominio\usuario) para iniciar sesión.  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a> Nuevas pestañas para actualizaciones y sistemas operativos en el Centro de software  
 En esta versión, se han realizado los siguientes cambios para mejorar el diseño de la aplicación Centro de Software:  

-   La pestaña **Aplicaciones** se ha dividido en tres pestañas independientes para **Actualizaciones**, **Sistemas operativos** (que antes se encontraban en la lista **Filtros**) y **Aplicaciones**.  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a> Dar servicio a un grupo de servidores  
 La Technical Preview de Configuration Manager, versión 1511, incluía la capacidad de crear una recopilación en la que todos los dispositivos formaban un grupo de servidores. Después se podían configurar las opciones del grupo de servidores para usarlas al implementar actualizaciones de software para el grupo de servidores, controlar el porcentaje de equipos que se actualizaba en un momento dado y configurar scripts de PowerShell anteriores y posteriores a la implementación para ejecutar acciones personalizadas.  

 La Technical Preview de Configuration Manager, versión 1605, incluye la capacidad de actualizar los equipos del grupo de servidores en un orden especificado por el usuario, incorpora supervisión mejorada para ver el estado de los equipos del grupo de servidores y proporciona la capacidad de borrar los bloqueos de implementación, lo cual resulta útil cuando los clientes no han podido instalar las actualizaciones de software y evitan que otros clientes instalen las suyas.  

### <a name="try-it-out"></a>Haga la prueba  
 Intente realizar las siguientes tareas y háganos saber cómo le ha ido mediante el formulario de comentarios de la página [Programa de comentarios de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) del sitio de Microsoft Connect:  

-   Puedo crear una colección que representa a un grupo de servidores. Para esta prueba puede configurar las reglas de pertenencia de la recopilación para tener 2 máquinas en esta recopilación.   

-   Puedo especificar que los equipos del grupo de servidores instalen actualizaciones de software en un orden concreto basado en la configuración del grupo de servidores de la colección. Use los scripts de ejemplo del procedimiento para especificar los scripts anteriores y posteriores a la implementación.  

-   Puedo implementar una actualización de software para esta colección. Revise los archivos start.txt y end.txt (creados a partir de los scripts de ejemplo) en C:\temp y compruebe las horas de inicio y finalización de la implementación en los equipos del grupo de servidores. Revise el archivo UpdatesDeployment.log para obtener más información.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Para crear una colección para un grupo de servidores  

1.  [Cree una colección de dispositivos](../clients/manage/collections/create-collections.md) que contenga los equipos del grupo de servidores.  

2.  En el área de trabajo **Activos y compatibilidad**, haga clic en **Recopilaciones de dispositivos**, haga clic con el botón derecho en la recopilación que contiene los equipos del grupo de servidores y luego haga clic en **Propiedades**.  

3.  En la pestaña **General**, seleccione **Todos los dispositivos forman parte del mismo grupo de servidores** y luego haga clic en **Configuración**.  

4.  En la página **Configuración de grupo de servidores**, especifique una de las opciones siguientes:  

    -   **Permitir que un porcentaje de máquinas se actualice a la vez**: especifica que solo un determinado porcentaje de clientes se actualiza en un momento dado. Si, por ejemplo, la recopilación tiene 10 clientes y se configura para actualizar el 30 % de los clientes a la vez, solo 3 clientes instalarán las actualizaciones de software en un momento dado.  

    -   **Permitir que varias máquinas se actualicen a la vez**: especifica que solo un determinado número de clientes se actualiza en un momento dado.  

    -   **Indique la secuencia de mantenimiento**: especifica que los clientes de la recopilación se actualizarán de uno en uno en la secuencia que configure. Un cliente solo instalará las actualizaciones de software después de que el cliente que va por delante de él en la lista haya terminado de instalar sus actualizaciones de software.  

5.  Especifique si quiere usar un script anterior a la implementación (purga de nodo) o posterior a la implementación (reanudación de nodo).  

    > [!TIP]  
    >  Los siguientes son ejemplos que puede usar en las pruebas para los scripts anteriores a la implementación y posteriores a la implementación que escriben la hora actual en un archivo de texto:  
    >   
    >  **Anterior a la implementación**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Posterior a la implementación**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Para implementar actualizaciones de software en el grupo de servidores y supervisar el estado  

1.  [Implemente las actualizaciones de software](../../sum/deploy-use/deploy-software-updates.md) en la colección del grupo de servidores.  

2.  [Supervise la implementación de las actualizaciones de software](../../sum/deploy-use/monitor-software-updates.md). Además de las vistas de supervisión estándar para la implementación de actualizaciones de software, se muestra una nueva descripción de estado cuando un cliente está esperando su turno para instalar las actualizaciones de software. Aparece **En espera de bloqueo** para este nuevo estado.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Para borrar los bloqueos de implementación de los equipos de un grupo de servidores  

1.  En el área de trabajo **Activos y compatibilidad**, haga clic en **Colecciones de dispositivos** y luego haga clic en la colección para borrar los bloqueos de implementación.  

2.  En la pestaña **Inicio**, en el grupo **Implementación**, haga clic en **Borrar los bloqueos de implementación del grupo de servidores**. Si los clientes no han podido instalar las actualizaciones de software e impiden que otros clientes instalen las suyas, los bloqueos de implementación se pueden borrar de forma manual.  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a> Compatibilidad con el servicio Protección contra amenazas avanzada de Microsoft Defender  
 Protección contra amenazas avanzada (ATP) de Microsoft Defender es un servicio que ayuda a las empresas a detectar ataques avanzados en sus redes, a investigarlos y a responder a ellos. ATP de Microsoft Defender se conocía anteriormente como ATP de Windows Defender. Más información sobre [ATP de Microsoft Defender](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Configuration Manager puede ayudarle a incorporar y supervisar dispositivos cliente administrados de Windows 10 Anniversary Edition.  

### <a name="try-it-now"></a>Haga la prueba  
 Intente realizar las siguientes tareas y háganos saber cómo le ha ido mediante el formulario de comentarios de la página [Programa de comentarios de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) del sitio de Microsoft Connect:  

- Incorporación de dispositivos al servicio en línea Protección contra amenazas avanzada (ATP) de Microsoft Defender  

- Supervisión de la implementación de ATP de Microsoft Defender en dispositivos administrados  

  **Requisitos previos**  

- Suscripción al servicio en línea Protección contra amenazas avanzada de Microsoft Defender  

- Clientes con Windows 10, Anniversary Edition (compilación 14328 y superiores)  

- Crear un archivo de configuración de incorporación de cliente  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Cómo crear un archivo de configuración de incorporación de cliente  

  1.  Inicie sesión en el servicio en línea ATP de Microsoft Defender.  

  2.  Haga clic en el elemento de menú **Incorporación de cliente**.  

  3.  Seleccione **Configuration Manager** y haga clic en **Descargar paquete**.  

  4.  Descargue el archivo comprimido (.zip) y extraiga el contenido.  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Incorporación de dispositivos para ATP de Microsoft Defender  

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Endpoint Protection** > **Directivas de Windows Defender ATP** y haga clic en **Crear directiva de Windows Defender ATP**. Se abre el Asistente para crear directiva de ATP de Microsoft Defender.  

2. Escriba el **nombre** y la **descripción** de la directiva de ATP de Microsoft Defender y seleccione **Incorporación**. Haga clic en Siguiente.  

3. **Vaya** al archivo de configuración proporcionado por el espacio empresarial del servicio ATP de Microsoft Defender en la nube de la organización. Haga clic en **Siguiente**.  

4. Especifique los ejemplos de archivos de dispositivos administrados que se recopilan y se comparten para su análisis.  

   - **Ninguno**: ningún archivo de ejemplo se recopila para su análisis.  

   - **Archivos portables ejecutables**: se recopilan para su análisis archivos como archivos de programa (.exe), archivos de vínculo de biblioteca dinámica (.dll), archivos de fuentes y similares que pueden aprovecharse en ciberataques.  

     Haga clic en **Siguiente**.  

5. Revise el resumen y finalice el asistente.  

6. Ahora puede hacer clic en **Implementar** para implementar la directiva de ATP de Microsoft Defender en equipos cliente administrados.  

##### <a name="monitor-microsoft-defender-atp"></a>Supervisión de ATP de Microsoft Defender  

1.  En la consola de Configuration Manager, vaya a **Supervisión** > **Información general** > **Seguridad** y luego haga clic en **Protección contra amenazas avanzada de Windows Defender**.  

2.  Revise el panel de Protección contra amenazas avanzada de Microsoft Defender.  

    -   **Estado de implementación del agente de Windows Defender**: el número y el porcentaje de equipos cliente administrados aptos con directiva de ATP de Microsoft Defender activa incorporados.  

    -   **Agent Health de ATP de Windows Defender**: porcentaje de equipos cliente que envían informes de estado de su agente de ATP de Microsoft Defender.  

        -   **Correcto**: funciona correctamente.  

        -   **Inactivo**: no se ha enviado ningún dato al servicio durante el período.  

        -   **Estado del agente**: el servicio del sistema del agente en Windows no se está ejecutando.  

        -   **No incorporado**: se aplicó la directiva, pero el agente no ha notificado la incorporación de la directiva.  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a> Atestación de estado del dispositivo local  
 Ahora es posible configurar la atestación de estado para dispositivos con Windows 10 a fin de establecer comunicación mediante la infraestructura local. Los administradores pueden especificar si la notificación se realiza a través de la nube o de recursos locales. Si se selecciona local para la notificación de atestación de estado, se puede especificar una dirección URL para el servicio. Esto permite a los equipos cliente sin acceso a Internet habilitar y administrar dispositivos con la atestación de estado.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Habilitación de la atestación de estado para dispositivos locales  
 En 1605, se han corregido algunos errores detectados en 1604 Technical Preview.  Para probarlo, configure el servicio de atestación de estado local mediante la configuración del agente de cliente.  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración de cliente** y, después, establezca **Usar el servicio de atestación de estado local** en **Sí**.  

2.  Especifique el valor de **URL del servicio de atestación de estado local**y, después, haga clic en **Aceptar**.  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Nuevas opciones de reinicio para los clientes de Windows 10 después de la instalación de la actualización del software  
 Cuando se implementa y se instala en un equipo una actualización de software que requiere un reinicio con Configuration Manager, se programa un reinicio pendiente y se muestra un cuadro de diálogo de reinicio. Ahora, en Windows 8 y posterior, si apaga o reinicia el equipo con las opciones de energía de Windows (en lugar de hacerlo desde el cuadro de diálogo de reinicio), este cuadro de diálogo sigue apareciendo después de reiniciar el equipo, que tendrá que reiniciarse en la fecha límite configurada. En esta Technical Preview, la opción para **Actualizar y reiniciar** y **Actualizar y apagar** está disponible en los equipos de Windows 10 en las opciones de energía de Windows siempre que haya un reinicio pendiente para una actualización de software de Configuration Manager. Después de utilizar una de estas opciones, tras reiniciar el equipo, no se mostrará el cuadro de diálogo de reinicio.  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a> Declarar previamente dispositivos corporativos con número de serie IMEI o iOS  
 Ahora puede identificar los dispositivos corporativos si importa sus números de identidad internacional de equipo móvil (IMEI). Puede cargar un archivo de valores separados por comas (.csv) que incluya los números IMEI de los dispositivos o escribir la información de los dispositivos de forma manual.  También puede importar los números de serie de los dispositivos iOS.  La información importada establecerá la propiedad de los dispositivos que se inscriban como "Corporativo".  Se sigue necesitando una licencia de Intune para cada usuario que acceda al servicio.  

### <a name="try-it-out"></a>Haga la prueba  
 Intente realizar las siguientes tareas y háganos saber cómo le ha ido mediante el formulario de comentarios de la página [Programa de comentarios de Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) del sitio de Microsoft Connect:  

-   Importar un conjunto de números IMEI en un archivo .csv. Cada fila puede contener el número IMEI seguido por un campo de detalles.  

-   Importar manualmente números IMEI desde la consola de Configuration Manager.  

-   Importar un conjunto de números de serie iOS en un archivo .csv. De nuevo, cada fila contiene un número seguido de los detalles del dispositivo.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Declarar previamente dispositivos corporativos con número de serie IMEI o iOS  

1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Todos los dispositivos corporativos** > **Dispositivos declarados previamente** y, luego, haga clic en **Crear dispositivos declarados previamente**. Se abre el asistente para dispositivos declarados previamente.  

2. Especifique cómo quiere agregar la información del dispositivo:  

   -   **Cargar un archivo .csv que contiene los números IMEI y los detalles**: para cargar una lista de números, vea el paso 3.  

   -   **Agregar manualmente los números IMEI y los detalles**: para especificar manualmente la información, escriba el número IMEI o el número de serie iOS y los detalles de los dispositivos y luego vaya al paso 4.  

3. En el caso de los archivos cargados, busque el archivo .csv que contiene información para declarar previamente dispositivos corporativos. El archivo debe tener el siguiente formato, excepto la fila superior (proporcionada únicamente como guía):  

   |**N.º IMEI**|**Serie iOS**|**SO**|**Detalles**|
   |---|---|---|---|
   |123456789012345||WINDOWS|Dispositivo Windows propiedad de la empresa|
   |123456789012|A0BCD0EFGH0J|IOS|Dispositivos iOS propiedad de la empresa|
   |123456789012346||ANDROID|Dispositivo Android propiedad de la empresa|

    **Columnas:**  

   - Columna 1: número IMEI (se necesita un número IMEI o un número de serie iOS para cada fila).  

   - Columna 2: número de serie iOS – solo se pueden declarar previamente los números de serie iOS. Usar número IMEI para otras plataformas de dispositivo  

   - Columna 3: sistema operativo del dispositivo (mayúsculas y minúsculas necesarias):  

     -   iOS – todos los dispositivos iOS.  

     -   WINDOWS – incluye Windows Phone, Windows 10 Mobile y equipos de Windows.  

     -   ANDROID – todos los dispositivos Android.  

   - Columna 4: detalles (información adicional del dispositivo que aparece en la consola de Configuration Manager).  

     Haga clic en **Siguiente**.  

4. Revise los resultados de la importación del archivo. Los números IMEI o de serie previamente importados verán actualizados sus detalles con detalles nuevos.  Haga clic en **Siguiente** para continuar o en **Atrás** para conservar la información actualizada; luego, finalice el asistente.  
