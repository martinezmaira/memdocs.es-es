---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Conozca las nuevas características disponibles en la versión Technical Preview 1805 de Configuration Manager.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 88234bb3117850bc3280242671ae459308a5262e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696033"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Funciones de Technical Preview 1805 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión Technical Preview 1805 de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de versión preliminar técnica. 

Revise el artículo [Technical Preview para System Center Configuration Manager](technical-preview.md) antes de instalar esta actualización. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Estas son las nuevas características que puede probar con esta versión.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Creación de una implementación por fases con fases configuradas manualmente para una secuencia de tareas
<!--1358148-->
Ahora puede [crear una implementación por fases](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) con fases configuradas manualmente para una secuencia de tareas. Puede agregar hasta 10 fases adicionales desde la pestaña **Fases** del asistente Crear una implementación por fases. 


### <a name="try-it-out"></a>Haga la prueba
Siga las instrucciones para crear una implementación por fases donde puede configurar manualmente todas las fases. Envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido. 

1. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.  

2. Haga clic con el botón derecho en una secuencia de tareas existente y seleccione **Create Phased Deployment** (Crear implementación por fases).  

3. En la pestaña **General** asigne un nombre y una descripción (opcional) a la implementación por fases y seleccione **Configurar manualmente todas las fases**.  

4. En la pestaña **Fases**, haga clic en **Agregar**.  

5. En **Nombre**, especifique un nombre para la fase y luego busque el destino **Recopilación de fase**.  

6. En la pestaña **Configuración de fase**, elija una opción para cada una de las opciones de programación y haga clic en **Siguiente** cuando haya terminado.  

    - Criterios de éxito de la fase anterior (esta opción está deshabilitada en la primera fase).
        - **Porcentaje de éxito de la implementación**: especifique el porcentaje de dispositivos que completan correctamente la implementación para los criterios de éxito de la fase anterior.  

    - Condiciones para comenzar esta fase de implementación una vez que la anterior se complete correctamente  
        - **Iniciar automáticamente esta fase después de un período de aplazamiento (en días)** : elija el número de días que se esperará antes de comenzar la siguiente fase después del éxito de la anterior. 
        - **Empezar esta fase de la implementación manualmente**: no inicie esta fase automáticamente después de completar correctamente la primera.  

    - Una vez que un dispositivo se establece como destino, instalar el software
        - **Lo antes posible**: establece la fecha límite para la instalación en el dispositivo en cuanto el dispositivo se selecciona.
        - **Hora límite (relativa a la hora a la que se destina el dispositivo)** : establece la fecha límite para la instalación en un número determinado de días después de que se seleccione el dispositivo.  
     
7. Complete el asistente Configuración de fase.

8. En la pestaña **Fases** del asistente Crear una implementación por fases, ahora puede agregar, quitar, reordenar o editar las fases para esta implementación.  

9. Complete el asistente Crear una implementación por fases.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Compatibilidad con puntos de distribución de nube para Azure Resource Manager
<!--1322209-->
Al crear una instancia del [punto de distribución de nube](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md), el asistente ahora proporciona la opción de crear una **implementación de Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) es una moderna plataforma para administrar todos los recursos de la solución como una única entidad, denominada [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Al implementar un punto de distribución de nube con Azure Resource Manager, el sitio usa Azure Active Directory (Azure AD) para autenticar y crear los recursos necesarios en la nube. Esta implementación modernizada no requiere el certificado de administración de Azure clásico.  

El asistente para punto de distribución de nube sigue ofreciendo la opción de una **implementación del servicio clásico** mediante un certificado de administración de Azure. Para simplificar la implementación y administración de recursos, se recomienda utilizar el modelo de implementación de Azure Resource Manager para todos los puntos de distribución de nube nuevos. Si es posible, vuelva a implementar los puntos de distribución de nube a través de Resource Manager.

Configuration Manager no migra los puntos de distribución de nube clásicos existentes al modelo de implementación de Azure Resource Manager. Cree nuevos puntos de distribución de nube con las implementaciones de Azure Resource Manager y luego quite los puntos de distribución de nube clásicos. 

> [!IMPORTANT]  
> Esta función no habilita la compatibilidad de los proveedores de servicios en la nube de Azure. La implementación de puntos de distribución de nube con Azure Resource Manager continúa usando el servicio en la nube clásico, que no es compatible con los proveedores de servicios en la nube. Para obtener más información, consulte [Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services) (Servicios de Azure disponibles en los proveedores de servicios en la nube de Azure).  


### <a name="prerequisites"></a>Requisitos previos  
- Integración con [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). No se necesita la detección de usuario de Azure AD.  

- Los mismos [requisitos que para un punto de distribución de nube](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements), excepto el certificado de administración de Azure.  


### <a name="try-it-out"></a>Haga la prueba  
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, área de trabajo **Administración**, expanda **Cloud Services** y seleccione **Puntos de distribución de nube**. Haga clic en **Crear punto de distribución de nube** en la cinta.   

2. En la página **General**, seleccione **Implementación de Azure Resource Manager**. Haga clic en **Iniciar sesión** para autenticarse con una cuenta de administrador de suscripción de Azure. El asistente rellena automáticamente los campos restantes con la información de suscripción de Azure AD almacenada durante el requisito previo de integración. Si tiene varias suscripciones, seleccione la suscripción deseada. Haga clic en **Siguiente**.  

3. En la página **Configuración**, proporcione el **archivo de certificado** de PKI del servidor del modo habitual. Este certificado define el punto de distribución de nube **FQDN de servicio** que Azure usa. Seleccione la **Región** y, a continuación, seleccione la opción de grupo de recursos **Crear nuevo** o **Utilizar existente**. Escriba el nombre del nuevo grupo de recursos, o seleccione un grupo de recursos existente en la lista desplegable.  

4. Complete el asistente.  

> [!NOTE]  
> Para la aplicación de servidor de Azure AD, Azure asigna el permiso de **colaborador** de la suscripción.  

Supervise el progreso de la implementación del servicio con el punto de conexión de servicio **cloudmgr.log**.



## <a name="take-actions-based-on-management-insights"></a>Realización de acciones basadas en la información de administración
<!--1357930-->
Alguna [información de administración](../servers/manage/management-insights.md) ahora tiene la opción de realizar una acción. Dependiendo de la regla, esta acción muestra uno de los siguientes comportamientos:  

- Navegar automáticamente por la consola hasta el nodo donde se puede realizar una acción. Por ejemplo, si la información de administración recomienda cambiar una configuración de cliente, al llevar a cabo la acción navegará hasta el nodo Configuración de cliente. Puede realizar otra acción modificando los valores predeterminados o un objeto de configuración de cliente personalizado.  

- Navegar a una vista filtrada basándose en una consulta. Por ejemplo, al actuar en la regla de recopilaciones vacías se muestran solo estas recopilaciones en la lista de recopilaciones. Aquí se puede realizar otra acción, como eliminar una recopilación o modificar sus reglas de pertenencia.  

Las siguientes reglas de información de administración tienen acciones en esta versión:
- Seguridad
    - Versiones del cliente antimalware no admitidas
- Centro de software
    - Usar la nueva versión del Centro de software
- Aplicaciones
    - Aplicaciones sin implementaciones
- Administración simplificada
    - Versiones de cliente diferentes de CB
- Recopilaciones
    - Recopilaciones vacías 
- Cloud Services
    - Actualización de clientes a la versión más reciente de Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Transición de la carga de trabajo de la configuración del dispositivo a Intune mediante la administración conjunta
<!--1357903-->

Ahora puede pasar la carga de trabajo de la configuración del dispositivo de Configuration Manager a Intune después de habilitar la administración conjunta. La transición de esta carga de trabajo le permite usar Intune para implementar directivas de MDM y seguir utilizando Configuration Manager para la implementación de aplicaciones. 

Para realizar la transición de esta carga de trabajo, vaya a la página de propiedades de administración conjunta y mueva la barra deslizante de Configuration Manager a **Piloto** o a **Todo**. Para más información, vea [Administración conjunta para dispositivos de Windows 10](../../comanage/overview.md).

> [!Note]  
> Al mover esta carga de trabajo también se mueven las cargas de trabajo **Acceso a los recursos** y **Endpoint Protection**, que son un subconjunto de la carga de trabajo de configuración del dispositivo.

Cuando realiza la transición de esta carga de trabajo, todavía puede implementar la configuración de Configuration Manager en dispositivos conjuntamente administrados, aunque Intune sea la autoridad de configuración de dispositivos. Esta excepción podría utilizarse para definir la configuración que necesita su organización, pero aún no está disponible en Intune. Especifique esta excepción en una línea de base de configuración de Configuration Manager. Habilite la opción **Always apply this baseline even for co-managed clients** (Aplicar siempre esta línea de base incluso para los clientes conjuntamente administrados) al crear la línea de base, o en la pestaña **General** de las propiedades de una línea de base existente. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Habilitación de los puntos de distribución para usar el control de congestión de red
<!--1358112-->

Windows Low Extra Delay Background Transport (LEDBAT) es una característica de Windows Server que ayuda a administrar transferencias de red en segundo plano. Para puntos de distribución que se ejecutan en versiones compatibles de Windows Server, puede habilitar una opción para ayudar a ajustar el tráfico de red. Los clientes solo usan el ancho de banda de red cuando está disponible. 

Para más información sobre Windows LEDBAT, consulte la entrada de blog [New transport advancements](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) (Nuevas ventajas de transporte).


### <a name="prerequisites"></a>Requisitos previos
- Un punto de distribución en Windows Server, versión 1709.  

- No existen requisitos previos de cliente.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Seleccione el nodo **Puntos de distribución**. Seleccione el punto de distribución de destino y haga clic en **Propiedades** en la cinta.  

2. En la pestaña **General**, habilite la opción **Adjust the download speed to use the unused network bandwidth (Windows LEDBAT)** (Ajustar la velocidad de descarga para usar el ancho de banda de red no utilizado [Windows LEDBAT]).  



## <a name="cloud-management-dashboard"></a>Panel de administración en la nube
<!--1358461-->
El nuevo **panel de administración en la nube** proporciona una vista centralizada para el uso de Cloud Management Gateway (CMG). Cuando el sitio está incorporado con Azure AD, también muestra los datos sobre los usuarios en la nube y los dispositivos.  

La captura de pantalla siguiente es una parte del panel de administración en la nube que muestra dos de los iconos disponibles:  
![Iconos del panel de administración: Tráfico de CMG y Clientes en línea actuales](media/1358461-cmg-dashboard.png)

Esta característica también incluye el **analizador de conexión de CMG** para la comprobación en tiempo real que ayuda a solucionar problemas. La utilidad en la consola comprueba el estado actual del servicio y el canal de comunicación a través del punto de conexión de CMG a todos los puntos de administración que permiten el tráfico CMG.


### <a name="prerequisites"></a>Requisitos previos
- Una instancia de [Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md) activa usada por clientes basados en Internet.  

- El sitio incorporado a los [servicios de Azure](../servers/deploy/configure/azure-services-wizard.md) para la administración en la nube.  


### <a name="try-it-out"></a>Haga la prueba
Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

#### <a name="cloud-management-dashboard"></a>Panel de administración en la nube

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Seleccione el nodo **Administración en la nube** y vea los iconos del panel.  

#### <a name="cmg-connection-analyzer"></a>Analizador de conexión de CMG

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Cloud Services** y seleccione **Cloud Management Gateway**.  

2. Seleccione la instancia de CMG de destino y luego seleccione **Analizador de conexión** en la cinta.  

3. En la ventana del analizador de conexión de CMG, seleccione una de las siguientes opciones para autenticarse con el servicio:  

     1. **Usuario de Azure AD**: utilice esta opción para simular la comunicación de la misma manera que una identidad de usuario basado en la nube que ha iniciado sesión en un dispositivo con Windows 10 unido a Azure AD. Haga clic en **Iniciar sesión** para escribir las credenciales de forma segura para esta cuenta de usuario de Azure AD.  

     2. **Certificado de cliente**: utilice esta opción para simular la comunicación de la misma manera que un cliente de Configuration Manager con un [certificado de autenticación del cliente](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Haga clic en **Iniciar** para iniciar el análisis. Los resultados se muestran en la ventana del analizador. Seleccione una entrada para ver más detalles en el campo Descripción.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager siempre ha proporcionado un gran almacén centralizado de datos de dispositivo, que los clientes utilizan para informes. Sin embargo, esos datos son solo tan buenos como la última vez que se recopilaron de los clientes. 

CMPivot es una nueva utilidad en la consola que proporciona acceso al estado en tiempo real de los dispositivos de su entorno. Esta utilidad ejecuta una consulta inmediatamente en todos los dispositivos conectados actualmente en la colección de destino y devuelve los resultados. A continuación, puede filtrar y agrupar estos datos en la herramienta. Mediante el suministro de datos en tiempo real de los clientes en línea, puede contestar preguntas empresariales, solucionar problemas y responder a incidentes de seguridad más rápidamente.

Por ejemplo, en la [mitigación de vulnerabilidades de canal lateral de ejecución especulativa](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), uno de los requisitos consiste en actualizar el BIOS del sistema. Puede usar CMPivot para realizar consultas rápidamente sobre la información del BIOS del sistema y buscar clientes que no cumplen los requisitos. 

En esta captura de pantalla, CMPivot muestra dos versiones independientes del BIOS con un recuento de dispositivos de cada una de ellas. Puede usar esta consulta de ejemplo cuando pruebe CMPivot:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![Ventana de CMPivot con la consulta de ejemplo para BIOSVersion](media/1358456-cmpivot-biosversion.png)

Puede hacer clic en el recuento de dispositivos para explorar en profundidad y ver los dispositivos específicos. Al mostrar dispositivos en CMPivot, puede hacer clic con el botón derecho en un dispositivo y seleccionar las siguientes [acciones de notificación de cliente](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode):
- Ejecutar script
- Control remoto
- Explorador de recursos

Al hacer clic con el botón derecho en un dispositivo específico, también puede dinamizar la vista de dicho dispositivo a uno de los siguientes atributos:
- Comandos de inicio automático
- Productos instalados
- Procesos
- Servicios
- Usuarios
- Conexiones activas
- Actualizaciones que faltan

### <a name="prerequisites"></a>Requisitos previos
- Los clientes de destino deben actualizarse a la versión más reciente.  

- El administrador de Configuration Manager necesita permisos para ejecutar scripts. Para más información, consulte [Crear roles de seguridad para scripts](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Haga la prueba
Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione **Recopilaciones de dispositivos**. Seleccione una recopilación de destino y haga clic en **Iniciar CMPivot** en la cinta para iniciar la herramienta.  

2. La interfaz proporciona más información sobre el uso de la herramienta. 
     - Puede especificar cadenas de consulta manualmente en la parte superior, o hacer clic en los vínculos en la documentación en línea.
     - Haga clic en una de las opciones de **Entidades** para agregarla a la cadena de consulta. 
     - Los vínculos de **Table Operators** (Operadores de tabla), **Aggregation Functions** (Funciones de agregación) y **Funciones escalares** abren la documentación de referencia del lenguaje en el explorador web. CMPivot utiliza el mismo lenguaje de consulta que [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).



## <a name="improved-secure-client-communications"></a>Comunicaciones de cliente seguras mejoradas
<!--1356889,1358228,1358460-->
Es recomendable utilizar la comunicación HTTPS para todas las vías de comunicación de Configuration Manager, pero puede ser un reto para algunos clientes debido a la sobrecarga de administración de certificados PKI. La introducción de la integración de Azure Active Directory (Azure AD) reduce algunos requisitos de certificado, pero no todos. 

Esta versión incluye mejoras en la forma en que los clientes se comunican con los sistemas de sitio. Hay dos objetivos principales para estas mejoras:  

- Puede proteger la comunicación de cliente sin necesidad de certificados de autenticación de servidor PKI.  

- Los clientes pueden acceder de forma segura a contenido desde puntos de distribución sin necesidad de una cuenta de acceso de red.  

> [!Note]  
> Los certificados PKI siguen siendo una opción válida para los clientes que desean usarlos.  


### <a name="scenarios"></a><a name="bkmk_token"></a>Escenarios
Los siguientes escenarios aprovechan estas mejoras:  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a> Escenario 1: Cliente a punto de administración
<!--1356889-->
Los [dispositivos unidos a Azure AD](/azure/active-directory/devices/concept-azure-ad-join) pueden comunicarse a través de una instancia de Cloud Management Gateway (CMG) con un punto de administración configurado para HTTP. El servidor de sitio genera un certificado para el punto de administración para que pueda comunicarse a través de un canal seguro.   

> [!Note]  
> Este comportamiento se cambia desde la versión de rama actual 1802 de Configuration Manager, lo que requiere un punto de administración habilitado para HTTPS para este escenario. Para obtener más información, vea [Enable management point for HTTPS](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps) (Habilitar el punto de administración para HTTPS).  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a> Escenario 2: Cliente a punto de distribución
<!--1358228-->
Un grupo de trabajo o un cliente unido a Azure AD puede descargar contenido a través de un canal seguro desde un punto de distribución configurado para HTTP.   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a> Escenario 3: Identidad de dispositivo de Azure AD 
<!--1358460-->
Un [dispositivo de Azure AD híbrido](/azure/active-directory/devices/concept-azure-ad-join-hybrid) o unido a Azure AD sin un usuario de Azure AD con sesión iniciada puede comunicarse de forma segura con su sitio asignado. La identidad del dispositivo basado en la nube ahora es suficiente para autenticarse con el punto de administración y CMG.  


### <a name="prerequisites"></a>Requisitos previos  

- Un punto de administración configurado para conexiones de cliente HTTP. Establezca esta opción en la pestaña **General** de las propiedades del rol de sistema de sitio.  

- Un punto de distribución configurado para conexiones de cliente HTTP. Establezca esta opción en la pestaña **General** de las propiedades del rol de sistema de sitio. No habilite la opción **Permitir a los clientes conectarse de forma anónima**.  

- Una instancia de Cloud Management Gateway.  

- Incorpore el sitio a Azure AD para administración en la nube.  

    - Si ya se ha cumplido este requisito previo para el sitio, debe actualizar la aplicación de Azure AD. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione **Inquilinos de Azure Active Directory**. Seleccione el inquilino de Azure AD, seleccione la aplicación web en el panel **Aplicaciones** y luego haga clic en **Actualizar configuración de la aplicación** en la cinta.  

- Un cliente con Windows 10 versión 1803 y unido a Azure AD. (Este requisito es técnicamente solo para el [escenario 3](#bkmk_token3)). 


### <a name="try-it-out"></a>Haga la prueba
Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda el nodo **Configuración del sitio** y haga clic en **Sitios**. Seleccione el sitio y haga clic en **Propiedades** en la cinta.  

2. Cambie a la pestaña **Comunicación de equipo cliente**. Seleccione la opción **HTTPS o HTTP** y habilite la nueva opción **Use Configuration Manager-generated certificates for HTTP site systems** (Usar certificados generados por Configuration Manager para sistemas de sitio HTTP).  

Consulte la [lista de escenarios](#bkmk_token) anterior para realizar la validación.

> [!Tip]
> En esta versión, espere hasta 30 minutos para que el punto de administración reciba y configure el nuevo certificado desde el sitio.

Puede ver estos certificados en la consola de Configuration Manager. Vaya al área de trabajo **Administración**, expanda **Seguridad** y seleccione el nodo **Certificados**. Busque el certificado raíz **SMS Issuing** (Emisión de SMS), así como los certificados de rol del servidor de sitio emitidos por la raíz SMS Issuing (Emisión de SMS).


### <a name="known-issues"></a>Problemas conocidos
- El usuario no puede ver en el centro de software ninguna aplicación dirigida a él como disponible.  

- Los escenarios de implementación de sistema operativo aún requieren la cuenta de acceso de red.  

- La habilitación y deshabilitación rápidas y repetidas de la opción **Use Configuration Manager-generated certificates for HTTP site systems** (Usar certificados generados por Configuration Manager para sistemas de sitio HTTP) pueden hacer que el certificado no se enlace correctamente a los roles de sistema de sitio. Ningún certificado emitido por el certificado "SMS Issuing" (Emisión de SMS) está enlazado a un sitio web en Windows Server Internet Information Services (IIS). Para solucionar este problema temporalmente, elimine todos los certificados emitidos por "SMS Issuing" (Emisión de SMS) desde el almacén de certificados **SMS** en Windows y luego reinicie el servicio smsexec.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Mejoras para habilitar la compatibilidad de actualización de software de terceros
<!--1357605-->
Como resultado de los comentarios de UserVoice sobre la [compatibilidad de actualización de software de terceros](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), esta versión itera en la integración con System Center Updates Publisher (SCUP). La [versión 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) de la versión preliminar técnica de Configuration Manager agregó la capacidad de leer el certificado de WSUS para actualizaciones de terceros y, luego, implementar ese certificado en los clientes. Pero todavía había que usar la herramienta SCUP para crear y administrar el certificado para firmar las actualizaciones de software de terceros.

En esta versión, puede permitir que el sitio de Configuration Manager configure automáticamente el certificado. El sitio se comunica con WSUS para generar un certificado para esta finalidad. Después, Configuration Manager continúa con la implementación de ese certificado a los clientes. Esta iteración elimina la necesidad de usar la herramienta SCUP para crear y administrar el certificado. 

Para más información sobre el uso general de la herramienta SCUP, consulte [System Center Updates Publisher](../../sum/tools/updates-publisher.md).

### <a name="prerequisites"></a>Requisitos previos
- Habilite e implemente la configuración de cliente **Habilitar actualizaciones de software de terceros** en el grupo **Actualizaciones de software**.
- Si WSUS se encuentra en un servidor independiente del punto de actualización de software, debe realizar una de las siguientes opciones en el servidor WSUS remoto:
    - Habilitar el servicio Registro remoto en Windows  
    o bien
    - En la clave del registro `HKLM\Software\Microsoft\Update Services\Server\Setup`, cree un nuevo DWORD denominado **EnableSelfSignedCertificates** con un valor de `1`. 

### <a name="try-it-out"></a>Haga la prueba
Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione **Sitios**. Seleccione el sitio de nivel superior, haga clic en **Configurar componentes de sitio** en la cinta y seleccione **Punto de actualización de software**.  

2. Cambie a la pestaña **Actualizaciones de terceros**. Seleccione las opciones **Habilitar actualizaciones de software de terceros** y **Configuration Manager automatically manages the certificate** (Configuration Manager administra automáticamente el certificado).

3. Continúe con el resto del flujo de trabajo típico de SCUP para la importación de un catálogo de actualizaciones de software de terceros y luego implemente las actualizaciones en los clientes.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Mejoras en la secuencia de tareas de actualización en contexto de Windows 10
<!--1358500-->

La plantilla de secuencia de tareas predeterminada para la actualización local de Windows 10 ahora incluye otro grupo adicional con las acciones recomendadas que se deben agregar en caso de error del proceso de actualización. Estas acciones facilitan la solución de problemas.

### <a name="new-groups-under-run-actions-on-failure"></a>Nuevos grupos en **Run actions on failure** (Ejecutar acciones en caso de error)
- **Recopilar registros**: para recopilar registros del cliente, agregue pasos en este grupo. 
    - Una práctica común consiste en copiar los archivos de registro en un recurso compartido de red. Para establecer esta conexión, use el paso [Conectar a carpeta de red](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder). 
    - Para llevar a cabo la operación de copia, utilice una utilidad o script personalizado con el paso [Ejecutar línea de comandos](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) o [Ejecutar script de PowerShell Script](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).
    - Los archivos para recopilar podrían incluir los siguientes registros:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Para más información sobre setupact.log y otros registros de instalación de Windows, vea [Windows Setup Log files](/windows/deployment/upgrade/log-files) (Archivos de registro de instalación de Windows).
    - Para más información sobre registros de cliente de Configuration Manager, consulte [Registros de cliente de Configuration Manager](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
    - Para más información sobre _SMSTSLogPath y otras variables útiles, consulte [Variables integradas de secuencias de tareas en System Center Configuration Manager](../../osd/understand/task-sequence-variables.md).

- **Ejecutar herramientas de diagnóstico**: para ejecutar herramientas de diagnóstico adicionales, agregue pasos en este grupo. Estas herramientas se deberían automatizar para recopilar información adicional del sistema tan pronto como fuera posible después del error.
    - Una de estas herramientas es Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). Es una herramienta de diagnóstico independiente que puede usar para obtener detalles sobre por qué una actualización de Windows 10 se realizó incorrectamente.
         - En Configuration Manager, [cree un paquete](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) para la herramienta.
         - Agregue un paso [Ejecutar línea de comandos](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) a este grupo de la secuencia de tareas. Use la opción **Paquete** para hacer referencia a la herramienta. La siguiente cadena es una **línea de comandos** de ejemplo:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>Herramienta CMTrace instalada con el cliente
<!--1357971-->

La herramienta de visualización de registro de CMTrace ahora se instala automáticamente junto con el cliente de Configuration Manager. Se agrega al directorio de instalación del cliente, que de forma predeterminada es `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> CMTrace *no* se registra automáticamente con Windows para abrir la extensión de archivo. log.



## <a name="improvement-to-the-configuration-manager-console"></a>Mejora en la consola de Configuration Manager
<!--1358202-->
Hemos realizado la siguiente mejora en la consola de Configuration Manager:

- En las listas de dispositivos bajo Activos y compatibilidad, Dispositivos, ahora, de forma predeterminada, se muestra el usuario que ha iniciado sesión. Este valor es tan actual como el [estado de cliente](../clients/manage/monitor-clients.md#bkmk_indStatus). El valor se borra cuando el usuario cierra la sesión. Si ningún usuario ha iniciado sesión, el valor está en blanco. 

### <a name="known-issues"></a>Problemas conocidos
El valor del usuario que tiene iniciada sesión actualmente están en blanco en el nodo Dispositivos o al ver una lista de dispositivos en el nodo Recopilaciones de dispositivos. Para solucionar este problema temporalmente, descargue este [script de SQL](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Ejecute sp_BgbUpdateLiveData.sql en el servidor de base de datos del sitio y luego reinicie los servicios smsexec y sms_notification_server en el punto de administración.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Mejoras en los comentarios de la consola
<!--1357542-->
Esta versión incluye las siguientes mejoras en el nuevo mecanismo [Comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) en la consola de Configuration Manager:  

- El cuadro de diálogo de comentarios ahora recuerda la configuración anterior, como las opciones seleccionadas y su dirección de correo electrónico.  

- Ahora es compatible con comentarios sin conexión. Guarde sus comentarios de la consola y luego cárguelos en Microsoft desde un sistema conectado a Internet. Use la nueva herramienta de cargador de comentarios sin conexión que se encuentra en `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`. Para ver las opciones de línea de comandos disponibles y requeridas, ejecute la herramienta con la opción `--help`. El sistema conectado necesita acceder a **petrol.office.microsoft.com**.

### <a name="known-issues"></a>Problemas conocidos
Cuando se usa **Enviar una sonrisa** o **Enviar un ceño fruncido** desde la consola de un equipo con conectividad a Internet, pueden devolver el siguiente mensaje: "Error al enviar comentarios." Si hace clic en **Más detalles**, se mostrará el siguiente texto: `{"Message":""}`. Este error es debido a un problema conocido con la respuesta del sistema de comentarios de back-end. Puede pasar por alto el error. Microsoft seguirá recibiendo sus comentarios. (Si los detalles muestran un mensaje diferente, utilice la opción de comentarios sin conexión para volver a intentar enviar los comentarios en otro momento).



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Mejoras en los puntos de distribución habilitados con PXE
<!--1357580-->

Esta versión incluye las siguientes mejoras adicionales cuando se usa la opción [**Habilitar un respondedor PXE sin Servicios de implementación de Windows**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) en un punto de distribución:  

- Se crean las reglas de Firewall de Windows automáticamente en el punto de distribución cuando se habilita esta opción  
- Mejoras en el registro de componentes



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Mejora en el inventario de hardware para los valores enteros grandes
<!--1357880-->
El inventario de hardware actualmente tiene un límite para los enteros mayores que 4 294 967 296 (2^32). Este límite puede alcanzarse en atributos como tamaños de unidades de disco duro en bytes. El punto de administración no procesa los valores de enteros por encima de este límite, por lo que no se almacena ningún valor en la base de datos. Ahora, en esta versión, se ha aumentado el límite hasta 18 446 744 073 709 551 616 (2^64). 

Para una propiedad con un valor que no cambia, como el tamaño total del disco, no puede ver inmediatamente el valor después de actualizar el sitio. La mayoría del inventario de hardware es un informe diferencial. El cliente envía solamente los valores que cambian. Para solucionar este comportamiento temporalmente, agregue otra propiedad a la misma clase. Esta acción hace que el cliente actualice todas las propiedades de la clase que ha cambiado. 



## <a name="improvement-to-wsus-maintenance"></a>Mejora en el mantenimiento de WSUS
<!--1357898-->

Ahora, el asistente para limpieza de WSUS rechaza las actualizaciones que han expirado o se han sustituido según las reglas de sustitución. Estas reglas se definen en las propiedades de componentes del punto de actualización de software.

### <a name="try-it-out"></a>Haga la prueba
Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione **Sitios**. Seleccione el sitio de nivel superior, haga clic en **Configurar componentes de sitio** en la cinta y seleccione **Punto de actualización de software**.  

2. Cambie a la pestaña **Reglas de sustitución**. Habilite la opción **Ejecutar el asistente de limpieza WSUS**. Especifique el comportamiento de sustitución que desee.  

3. Revise el archivo WSyncMgr.log.



## <a name="improvement-to-support-for-cng-certificates"></a>Mejora en la compatibilidad con certificados CNG
<!--1357314-->
En esta versión, use [certificados CNG](../plan-design/network/cng-certificates-overview.md) para los siguientes roles de servidor adicionales habilitados para HTTPS:  
- Punto de registro de certificados, incluido el servidor NDES con el módulo de directivas de Configuration Manager



## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
