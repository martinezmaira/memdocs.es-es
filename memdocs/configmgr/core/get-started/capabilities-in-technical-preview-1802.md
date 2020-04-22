---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1802.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 50e05d07ec3e2612c170157c45f5e64abe3766de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701333"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Funciones de Technical Preview 1802 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1802 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. 

Repase [Technical Preview de Configuration Manager](technical-preview.md) antes de instalar esta versión de Technical Preview. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conocidos de esta Technical Preview
- **La actualización a una nueva versión preliminar no se puede realizar cuando hay un servidor de sitio en modo pasivo**. Si tiene un [servidor de sitio primario en modo pasivo](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), debe desinstalarlo antes de actualizar a esta nueva versión preliminar. Puede volver a instalar el servidor de sitio en modo pasivo después de que el sitio finalice la actualización.

  Para desinstalar el servidor de sitio en modo pasivo:
  1. En la consola de Configuration Manager vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles del sistema de sitios** y seleccione el servidor de sitio en modo pasivo.
  2. En el panel **Roles del sistema de sitio**, haga clic con el botón derecho en el rol **Servidor de sitio** y después elija **Quitar rol**.
  3. Haga clic con el botón derecho en el servidor de sitio en modo pasivo y después elija **Eliminar**.
  4. Después de que el servidor de sitio se desinstala, en el servidor de sitio principal activo, reinicie el servicio **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


</br>

**Estas son las nuevas características que puede probar con esta versión.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Transición de la carga de trabajo de Endpoint Protection a Intune mediante la administración conjunta    
<!-- 1357365 -->
En esta versión, ahora puede pasar la carga de trabajo de Endpoint Protection de Configuration Manager a Intune después de habilitar la administración conjunta. Para realizar la transición de la carga de trabajo de Endpoint Protection, vaya a la página de propiedades de la administración conjunta y mueva la barra deslizante de Configuration Manager a **Piloto** o **Todos**. Para más información, consulte [Administración conjunta para dispositivos de Windows 10](../../comanage/overview.md).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configuración de la optimización de distribución de Windows para usar grupos de límites de Configuration Manager
<!-- 1324696 -->
Los grupos de límites de Configuration Manager se usan para definir y regular la distribución de contenido a través de la red corporativa y en las oficinas remotas. La [optimización de distribución de Windows](/windows/deployment/update/waas-delivery-optimization) es una tecnología entre iguales basada en la nube para compartir contenido entre los dispositivos de Windows 10. A partir de esta versión, configure la optimización de distribución para usar los grupos de límites al compartir contenido entre iguales. Una nueva configuración de cliente aplica el identificador del grupo de límites como el identificador del grupo de optimización de distribución en el cliente. Cuando el cliente se comunica con el servicio en la nube de optimización de distribución, utiliza este identificador para buscar elementos del mismo nivel con el contenido deseado. 

### <a name="prerequisites"></a>Requisitos previos
- La optimización de distribución solo está disponible en clientes de Windows 10

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

1. En la consola de Configuration Manager, área de trabajo **Administración**, nodo **Configuración de cliente**, cree una directiva de configuración de dispositivos cliente personalizada.
2. Seleccione el nuevo grupo **Optimización de distribución**.
3. Habilite el parámetro **Use Configuration Manager Boundary Groups for Delivery Optimization Group ID** (Uso de grupos de límites de Configuration Manager para id. del grupo de optimización de distribución).

Para obtener más información, consulte la opción de modo de distribución **Grupo** en [Delivery Optimization options](/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization) (Opciones de optimización de distribución).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Secuencia de tareas de actualización en contexto de Windows 10 a través de Cloud Management Gateway
<!-- 1357149 -->

La [secuencia de tareas de actualización en contexto](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) de Windows 10 ahora admite la implementación en los clientes basados en Internet que se administran a través de [Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md). Esta función permite a los usuarios remotos actualizar con mayor facilidad a Windows 10 sin necesidad de conectarse a la red corporativa. 

Asegúrese de que todo el contenido al que hace referencia la secuencia de tareas de actualización en contexto se distribuye a un [punto de distribución de nube](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). En caso contrario, los dispositivos no podrán ejecutar la secuencia de tareas.

Cuando se implementa una secuencia de tareas de actualización, utilice la siguiente configuración:
- **Permitir que la secuencia de tareas se ejecute para el cliente en Internet**, en la pestaña Experiencia del usuario de la implementación.
- **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas** en la página Puntos de distribución de la implementación. Otras opciones como **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas** no funcionan en este escenario. El motor de la secuencia de tareas no puede obtener contenido actualmente desde un punto de distribución de nube. El cliente de Configuration Manager debe descargar el contenido desde el punto de distribución de nube antes de iniciar la secuencia de tareas.
- (*Opcional*) **Descargar contenido previamente para esta secuencia de tareas** en la pestaña General de la implementación. Para obtener más información, vea [Configuración del contenido de la caché previa](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Mejoras en la secuencia de tareas de actualización en contexto de Windows 10
<!-- 1357425 -->
La plantilla de secuencia de tareas predeterminada para la actualización en contexto de Windows 10 ahora incluye grupos adicionales con las acciones recomendadas que se agregarán antes y después del proceso de actualización. Estas acciones son comunes entre muchos clientes que están actualizando correctamente los dispositivos a Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Nuevos grupos en **Preparar para actualización**
- **Comprobaciones de la batería**: agregue pasos a este grupo para comprobar si el equipo usa la batería o una conexión por cable. Esta acción requiere un script o utilidad personalizado a fin de realizar la comprobación.
- **Comprobaciones de conexión por cable o red**: agregue pasos a este grupo para comprobar si el equipo está conectado a una red y no está usando una conexión inalámbrica. Esta acción requiere un script o utilidad personalizado a fin de realizar la comprobación.
- **Quitar aplicaciones no compatibles**: agregue pasos a este grupo para quitar las aplicaciones no compatibles con esta versión de Windows 10. El método para desinstalar una aplicación es diferente en cada situación. Si la aplicación usa Windows Installer, copie la línea de comandos de **Desinstalar programa** desde la pestaña **Programas** en las propiedades del tipo de implementación de Windows Installer de la aplicación. Luego, agregue un paso para **Ejecutar línea de comandos** a este grupo con la línea de comandos de desinstalar programa. Por ejemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Quitar controladores no compatibles**: agregue pasos a este grupo para quitar los controladores no compatibles con esta versión de Windows 10.
- **Quitar o suspender seguridad de terceros**: agregue pasos a este grupo para quitar o suspender programas de seguridad de terceros, como antivirus.
   - Si usa un programa de cifrado de disco de otro fabricante, indique su controlador de cifrado en el programa de instalación de Windows con la [opción de línea de comandos](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers**. Agregue un paso para [establecer la variable de secuencia de tareas](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) a la secuencia de tareas en este grupo. Establezca la variable de secuencia de tareas en **OSDSetupAdditionalUpgradeOptions**. Establezca el valor en **/ReflectDriver** con la ruta de acceso al controlador. Esta [variable de acción de secuencia de tareas](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) anexa la línea de comandos del programa de instalación de Windows utilizada por la secuencia de tareas. Para obtener las instrucciones adicionales sobre este proceso, póngase en contacto con su proveedor de software.

### <a name="new-groups-under-post-processing"></a>Nuevos grupos en **Posprocesamiento**
- **Aplicar controladores basados en la instalación**: agregue pasos a este grupo para instalar controladores de instalación (.exe) a partir de paquetes.
- **Instalar/Habilitar seguridad de terceros**: agregue pasos a este grupo para instalar o habilitar programas de seguridad de terceros, como antivirus. 
- **Establecer aplicaciones predeterminadas de Windows y asociaciones**: agregue pasos a este grupo para establecer las aplicaciones predeterminadas de Windows y las asociaciones de archivos. En primer lugar, prepare un equipo de referencia con las asociaciones de aplicaciones deseadas. A continuación, ejecute la siguiente línea de comandos para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Agregue el archivo XML a un paquete. Luego, ejecute el paso [Ejecutar línea de comandos](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) en este grupo. Especifique el paquete que contiene el archivo XML y, a continuación, especifique la siguiente línea de comandos: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para obtener más información, consulte [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations) (Exportación o importación de asociaciones de aplicaciones predeterminadas).
- **Aplicar personalizaciones**: agregue pasos a este grupo para aplicar personalizaciones al menú Inicio, como la organización de los grupos de programas. Para obtener más información, consulte [Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen) (Personalización de la pantalla Inicio).

### <a name="additional-recommendations"></a>Otras recomendaciones
- Consulte la documentación de Windows para [solucionar los errores de actualización de Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). En este artículo también se incluye información detallada sobre el proceso de actualización.
- En el paso predeterminado **Comprobar preparación**, habilite **Garantizar espacio libre mínimo en disco (MB)** . Establezca el valor en al menos **16384** (16 GB) para un paquete de actualización de sistema operativo de 32 bits, o **20480** (20 GB) para 64 bits. 
- Use la [variable de secuencia de tareas integradas](../../osd/understand/task-sequence-variables.md) **SMSTSDownloadRetryCount** para intentar descargar de nuevo la directiva. En este momento, el cliente lo reintenta de manera predeterminada dos veces; esta variable está configurada en dos (2). Si los clientes no utilizan una conexión de red corporativa por cable, una mayor cantidad de reintentos ayudará al cliente a obtener la directiva. El uso de esta variable no tiene ningún efecto secundario, además del retraso que implica la imposibilidad de descargar la directiva.<!-- 501016 --> Aumente también la variable **SMSTSDownloadRetryDelay** desde el valor predeterminado de 15 segundos.
- Realice una evaluación de compatibilidad en línea. 
   - Agregue un segundo paso para **actualizar el sistema operativo** al principio del grupo **Preparar para la actualización**. Póngale el nombre *Evaluación de actualización*. Especifique el mismo paquete de actualización y, a continuación, habilite la opción **Realizar examen de compatibilidad del programa de instalación de Windows sin iniciar la actualización**. Habilite **Continuar después de un error** en la pestaña Opciones. 
   - Inmediatamente después de este paso de *Evaluación de actualización*, agregue otro paso **Ejecutar línea de comandos**. Especifique la siguiente línea de comandos:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>En la pestaña **Opciones** , agregue la siguiente condición: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno es el equivalente decimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que es un examen de compatibilidad en el que no se detecta ningún problema. Si el paso *Evaluación de actualización* se realiza correctamente y devuelve este código, este paso se omitirá. En caso contrario, si el paso de la evaluación devuelve cualquier otro código de retorno, este paso produce un error en la secuencia de tareas con el código de retorno del examen de compatibilidad del programa de instalación de Windows.
   - Para obtener más información, consulte [Actualizar el sistema operativo](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).
- Si desea cambiar el dispositivo de BIOS a UEFI durante esta secuencia de tareas, consulte [Conversión de BIOS a UEFI durante una actualización local](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Envíe **comentarios** desde la pestaña **Inicio** de la cinta si tiene más recomendaciones o sugerencias.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Mejoras en los puntos de distribución habilitados con PXE
<!-- 1357580 -->
Para aclarar el comportamiento de la [nueva funcionalidad de PXE](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6) presentada por primera vez en la versión 1706 de Technical Preview, hemos cambiado el nombre de la opción **Admitir IPv6**. En la pestaña **PXE** de las propiedades del punto de distribución, active **Enable a PXE responder without Windows Deployment Service** (Habilitar un respondedor PXE sin Servicios de implementación de Windows). 

Esta opción habilita un respondedor PXE en el punto de distribución que no requiere servicios de implementación de Windows. Si habilita esta nueva opción en un punto de distribución que ya está habilitado para PXE, Configuration Manager suspenderá los servicios de implementación de Windows. Si deshabilita esta nueva opción, pero mantiene **Habilitar compatibilidad de PXE para clientes**, el punto de distribución habilitará los servicios de implementación de Windows de nuevo.

Dado que los servicios de implementación de Windows no son necesarios, el punto de distribución habilitado para ellos puede ser un sistema operativo cliente o servidor, como Windows Server Core. Este nuevo servicio de respondedor PXE sigue siendo compatible con IPv6, y también mejora la flexibilidad de los puntos de distribución habilitados para PXE en oficinas remotas.

> [!NOTE]
> Este servicio utiliza la misma tecnología fundamental que el [servicio de respondedor PXE basado en cliente](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) de la versión 1712 de Technical Preview. Esta característica no requiere la sobrecarga del rol del punto de distribución.

### <a name="multicast"></a>Multidifusión
Para habilitar y configurar la multidifusión en la pestaña **Multidifusión** de las propiedades del punto de distribución, el punto de distribución debe usar servicios de implementación de Windows. 
- Si activa **Habilitar compatibilidad de PXE para clientes** y **Habilitar multidifusión para enviar datos simultáneamente a varios clientes**, no podrá **habilitar un respondedor PXE sin el servicio de implementación de Windows**.
- Si activa **Habilitar compatibilidad de PXE para clientes** y **Enable a PXE responder without Windows Deployment Service** (Habilitar un respondedor PXE sin el servicio de implementación de Windows), no podrá activar **Habilitar multidifusión para enviar datos simultáneamente a varios clientes**.



## <a name="deployment-templates-for-task-sequences"></a>Plantillas de implementación para secuencias de tareas
<!-- 1357391 -->
El asistente para la implementación de secuencias de tareas ahora puede crear una plantilla de implementación. La plantilla de implementación puede guardarse y aplicarse a una secuencia de tareas nueva o existente para crear una implementación. 

### <a name="try-it-out"></a>Haga la prueba  
Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado. 

 **Creación de una plantilla de implementación para la implementación de una nueva secuencia de tareas** <br/> 
1. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.
2. Haga clic con el botón derecho en una secuencia de tareas y seleccione **Implementar**. 
3. En la pestaña **General**, observe que ahora existe la opción **Seleccionar plantilla de implementación**. 
4. Continúe con el **Asistente para implementar software** seleccionando los parámetros de implementación para la secuencia de tareas. 
5. Cuando llegue a la pestaña **Resumen** del **Asistente para implementar software**, haga clic en **Guardar como plantilla**.
6. Asigne un nombre a la plantilla y seleccione la configuración que desea guardar en la plantilla. 
7. Haga clic en **Guardar**. La plantilla ahora está disponible para su uso desde la opción **Seleccionar plantilla de implementación**.



## <a name="product-lifecycle-dashboard"></a>Panel de ciclo de vida del producto
<!--1319632-->
El nuevo [Panel de ciclo de vida del producto](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md) muestra el estado de la directiva de ciclo de vida para productos de Microsoft instalados en los dispositivos administrados con Configuration Manager. El panel proporciona información acerca de los productos de Microsoft de su entorno, el estado de compatibilidad y la fechas de finalización del soporte técnico. Puede utilizar el panel para tener constancia de la disponibilidad del soporte técnico para cada producto. 

Para tener acceso al panel de ciclo de vida, en la consola de Configuration Manager, vaya a **Activos y compatibilidad** >**Asset Intelligence** >**Ciclo de vida del producto**



## <a name="improvements-to-reporting"></a>Mejoras en la creación de informes
<!--1357653-->
Como resultado de [los comentarios](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and)recibidos, hemos agregado un nuevo informe sobre los **detalles de mantenimiento de Windows 10 para una recopilación específica**. En este informe aparecen el identificador de recurso, el nombre de NetBIOS, el nombre del sistema operativo, la compilación, la rama de sistema operativo y el estado del servicio para dispositivos Windows 10. Para obtener acceso al informe, vaya a **Supervisión** >**Generación de informes** >**Informes** >**Sistemas operativos** >**Windows 10 Servicing details for a specific collection** (Detalles de mantenimiento de Windows 10 para una colección específica).



## <a name="improvements-to-software-center"></a>Mejoras en el Centro de software
<!--1357592-->
Como resultado de [los comentarios](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) recibidos, hemos agregado la posibilidad de ocultar las aplicaciones instaladas en el Centro de Software. Las aplicaciones que estén instaladas ya no aparecerán en la pestaña Aplicaciones cuando se habilite esta opción. 

### <a name="try-it-out"></a>Haga la prueba
Habilite el parámetro **Hide Installed Applications in Software Center** (Ocultar aplicaciones instaladas en el Centro de software) en la configuración de cliente del Centro de software. Observe el comportamiento del Centro de Software cuando el usuario final instala una aplicación.



## <a name="improvements-to-run-scripts"></a>Mejoras para ejecutar scripts
<!--1236459-->
La característica [Ejecutar scripts](../../apps/deploy-use/create-deploy-scripts.md) ahora devuelve la salida del script en formato JSON. Este formato devuelve de manera uniforme una salida de script legible. Es posible que los scripts que no puedan ejecutarse no obtengan una salida. 



## <a name="boundary-group-fallback-for-management-points"></a>Reserva de grupo de límites para puntos de administración
<!-- 1324594 -->
A partir de esta versión, puede configurar las relaciones de reserva para los puntos de administración entre [grupos de límites](../servers/deploy/configure/boundary-groups.md). Este comportamiento proporciona mayor control para los puntos de administración que utilizan los clientes. En la pestaña **Relaciones** de las propiedades del grupo de límites, hay una nueva columna para el punto de administración. Cuando se agrega un nuevo grupo de límites de reserva, el tiempo de reserva para el punto de administración actualmente siempre es cero (0). Este comportamiento es el mismo para el **comportamiento predeterminado** en el grupo de límites predeterminado del sitio.

Anteriormente se producía un problema con frecuencia cuando tenía un punto de administración protegido en una red segura. Los clientes de la red corporativa principal reciben una directiva que incluye este punto de administración protegido, incluso aunque no se puedan comunicar con él a través de un firewall. Para solucionar este problema, utilice la opción **No usar reserva nunca** para asegurarse de que los clientes solo reservan para los puntos de administración con los que pueden comunicarse.

Al actualizar el sitio a esta versión, Configuration Manager agrega todos los puntos de administración que no son accesibles desde Internet al grupo de límites predeterminado del sitio. Con este comportamiento de actualización se garantiza que las versiones de cliente anteriores seguirán comunicándose con puntos de administración. Para aprovechar plenamente esta característica, mueva los puntos de administración a los grupos de límites deseados.

La reserva del grupo de límites de un punto de administración no cambia el comportamiento durante la instalación de cliente (ccmsetup). Si la línea de comandos no especifica el punto de administración inicial mediante el parámetro/MP, el cliente nuevo recibe la lista completa de puntos de administración disponibles. Para su proceso de arranque inicial, el cliente utiliza el primer punto de administración al que pueda tener acceso. Una vez que el cliente se registre en el sitio, recibirá la lista de puntos de administración ordenada correctamente de acuerdo con este nuevo comportamiento. 

### <a name="prerequisites"></a>Requisitos previos
- Habilite los [puntos de administración preferidos](../servers/deploy/configure/boundary-groups.md#bkmk_preferred). En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione **Sitios**. Haga clic en **Configuración de jerarquía** en la cinta de opciones. En la pestaña **General**, elija **Los clientes prefieren usar puntos de administración especificados en grupos de límites**. 

### <a name="known-issues"></a>Problemas conocidos
- Los procesos de implementación de sistema operativo no operan de acuerdo con los grupos de límites.

### <a name="troubleshooting"></a>Solución de problemas
Las nuevas entradas aparecen en **LocationServices.log**. El atributo **Localidad** identifica uno de los siguientes estados:
- 0: Unknown
- 1: el punto de administración especificado solo está en el grupo de límites predeterminado del sitio para la reserva.
- 2: el punto de administración especificado está en un grupo de límites remoto o vecino. Cuando el punto de administración está simultáneamente en un grupo vecino y en un grupo de límites predeterminado del sitio, la localidad es 2.
- 3: el punto de administración especificado está en el grupo de límites local o actual. Cuando el punto de administración está en el grupo de límites actual, así como en un grupo vecino o de límites predeterminado del sitio, la localidad es 3. Si no habilita la configuración de los puntos de administración preferidos en la configuración de jerarquía, la localidad siempre es 3, con independencia de en qué grupo de límites se encuentre el punto de administración.

Los clientes utilizan puntos de administración locales primero (localidad 3), luego remotos (localidad 2) y por último reserva (localidad 1). 

Cuando un cliente recibe cinco errores en diez minutos y no puede comunicarse con un punto de administración de su grupo de límites actual, trata de contactar con un punto de administración en un grupo vecino o el grupo de límites predeterminado del sitio. Si el punto de administración del grupo de límites actual más adelante vuelve a estar conectado, el cliente volverá al punto de administración local en el siguiente ciclo de actualización. El ciclo de actualización es de 24 horas, o cuando se reinicia el servicio del agente de Configuration Manager.



## <a name="improved-support-for-cng-certificates"></a>Mejora de la compatibilidad con certificados CNG
<!-- 1357314 -->
La versión 1710 de Configuration Manager (rama actual) admite [certificados Cryptography: Next Generation (CNG)](../plan-design/network/cng-certificates-overview.md). En la versión 1710 se limita la compatibilidad a certificados cliente en determinados escenarios. 

A partir de esta versión de Technical Preview, use certificados CNG para los siguientes roles de servidor habilitados para HTTPS:
- Punto de administración
- Punto de distribución
- Punto de actualización de software

La lista de [escenarios no admitidos](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios) sigue siendo la misma.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Compatibilidad con Cloud Management Gateway para Azure Resource Manager
<!-- 1324735 -->
Al crear una instancia de [Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG), el asistente proporciona ahora la opción de crear una **implementación de Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) es una moderna plataforma para administrar todos los recursos de la solución como una única entidad, denominada [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Al implementar CMG con Azure Resource Manager, el sitio usa Azure Active Directory (Azure AD) para autenticar y crear los recursos necesarios en la nube. Esta implementación modernizada no requiere el certificado de administración de Azure clásico.  

El asistente de CMG sigue ofreciendo la opción de una **implementación del servicio clásico** mediante un certificado de administración de Azure. Para simplificar la implementación y administración de recursos, se recomienda utilizar el modelo de implementación de Azure Resource Manager para todas las instancias nuevas de CMG. Si es posible, vuelva a implementar las instancias existentes de CMG a través de Resource Manager.

Configuration Manager no migra las instancias existentes de CMG clásicas al modelo de implementación de Azure Resource Manager. Cree nuevas instancias de CMG mediante implementaciones de Azure Resource Manager y, a continuación, quite instancias de CMG clásicas. 

> [!IMPORTANT]
> Esta función no habilita la compatibilidad de los proveedores de servicios en la nube de Azure. La implementación de CMG con Azure Resource Manager continúa usando el servicio en la nube clásico, que no es compatible con los proveedores de servicios en la nube. Para obtener más información, consulte [Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services) (Servicios de Azure disponibles en los proveedores de servicios en la nube de Azure).  

### <a name="prerequisites"></a>Requisitos previos
- Integración con [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). No se necesita la detección de usuario de Azure AD.
- Los mismos [requisitos que para Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements), excepto el certificado de administración de Azure.

### <a name="try-it-out"></a>Haga la prueba  
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

1. En la consola de Configuration Manager, área de trabajo **Administración**, expanda **Servicios de nube** y seleccione **Cloud Management Gateway**. Haga clic en **Crear instancia de Cloud Management Gateway** en la cinta de opciones. 
2. En la página **General**, seleccione **Implementación de Azure Resource Manager**. Haga clic en **Iniciar sesión** para autenticarse con una cuenta de administrador de suscripción de Azure. El asistente rellena automáticamente los campos restantes con la información de suscripción de Azure AD almacenada durante el requisito previo de integración. Si tiene varias suscripciones, seleccione la suscripción deseada. Haga clic en **Siguiente**.  
3. En la página **Configuración**, proporcione el archivo de certificado de PKI del servidor del modo habitual. Este certificado define el nombre del servicio de CMG en Azure. Seleccione la **Región** y, a continuación, seleccione la opción de grupo de recursos **Crear nuevo** o **Utilizar existente**. Escriba el nombre del nuevo grupo de recursos, o seleccione un grupo de recursos existente en la lista desplegable. 
4. Complete el asistente.

> [!NOTE] 
> Para la aplicación de servidor de Azure AD, Azure asigna el permiso de **colaborador** de la suscripción. 

Supervise el progreso de la implementación del servicio con el punto de conexión de servicio **cloudmgr.log**.



## <a name="approve-application-requests-for-users-per-device"></a>Aprobación de solicitudes de aplicación para los usuarios por dispositivo
<!-- 1357015 -->
A partir de esta versión, cuando un usuario solicita una aplicación que requiere aprobación, el nombre de dispositivo específico ahora forma parte de la solicitud. Si el administrador aprueba la solicitud, el usuario solo tiene la posibilidad de instalar la aplicación en ese dispositivo. El usuario debe enviar otra solicitud para instalar la aplicación en otro dispositivo. 

> [!NOTE]
> Esta característica es opcional. Al actualizar a esta versión, habilite esta característica en el asistente para la actualización. También tiene la posibilidad de habilitar la característica en la consola más adelante. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../servers/manage/install-in-console-updates.md#bkmk_options).

### <a name="prerequisites"></a>Requisitos previos
- Actualizar el cliente de Configuration Manager a la versión más reciente
- Habilitar la configuración de cliente **Usar nuevo Centro de software** en el grupo [Agente de equipo](../clients/deploy/about-client-settings.md#computer-agent)

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

1. Implemente una aplicación como disponible para una colección de usuarios.
2. En la página **Configuración de implementación**, habilite la opción: **Un administrador debe aprobar una solicitud para esta aplicación en el dispositivo**.
3. Como usuario afectado, use el Centro de software para enviar una solicitud para la aplicación. 
4. Vea **Solicitudes de aprobación** en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** de la consola de Configuration Manager. Ahora hay una columna **Dispositivo** en la lista para cada solicitud. Al realizar acciones en la solicitud, el cuadro de diálogo Solicitud de aplicación también incluye el nombre del dispositivo desde el que el usuario envió la solicitud.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Uso del Centro de software para buscar e instalar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD
<!-- 1322613 -->
Si implementa aplicaciones como disponibles para los usuarios, ahora puede examinarlas e instalarlas a través del Centro de software en dispositivos de Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Requisitos previos
- Habilitar el HTTPS en el punto de administración
- Integrar el sitio con [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md)
- Implementar una aplicación como disponible para una colección de usuarios
- Distribuir el contenido de la aplicación a un [punto de distribución en la nube](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- Habilitar la configuración de cliente **Usar nuevo Centro de software** en el grupo [Agente de equipo](../clients/deploy/about-client-settings.md#computer-agent)
- El cliente debe: 
   - Windows 10
   - estar unido a Azure AD, lo que se conoce también como unido a dominio en la nube
- Para admitir clientes basados en Internet:
    - [Puerta de enlace de administración en la nube](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - Habilite la configuración de cliente: **Habilitar solicitudes de directiva de usuario de clientes de Internet** en el grupo [Directiva de cliente](../clients/deploy/about-client-settings.md#client-policy).
- Para admitir clientes en la red corporativa:
    - Agregar el punto de distribución en la nube a un grupo de límites utilizado por los clientes
    - Los clientes deben poder resolver el nombre de dominio completo (FQDN) del punto de administración habilitado para HTTPS



## <a name="report-on-windows-autopilot-device-information"></a>Información de dispositivo Windows AutoPilot
<!-- 1351442 -->
Windows AutoPilot es una solución para la incorporación y configuración de nuevos dispositivos de Windows 10 de forma moderna. Para obtener más información, vea [información general sobre Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Un método para registrar dispositivos existentes con Windows AutoPilot es cargar la información de dispositivo a Microsoft Store para Empresas y Educación. Esta información incluye el número de serie del dispositivo, el identificador de producto de Windows y un identificador de hardware. Use Configuration Manager para recopilar y notificar esta información del dispositivo. 

### <a name="prerequisites"></a>Requisitos previos
- Esta información del dispositivo solo se aplica a los clientes de Windows 10, versión 1703 y posteriores.

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

1. En la consola de Configuration Manager, área de trabajo **Supervisión**, expanda el nodo **Generación de informes**, expanda **Informes** y seleccione el nodo **Hardware - General**.
2. Ejecute el nuevo informe con **información de dispositivo Windows AutoPilot** y observe los resultados. 
3. En el visor de informes, haga clic en el icono **Exportar** y seleccione la opción **CSV (delimitado por comas)** .
4. Después de guardar el archivo, cargue los datos en Microsoft Store para Empresas y Educación. Para obtener más información, consulte [Add devices in Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile) (Agregar dispositivos en Microsoft Store para Empresas y Educación). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Mejoras en las directivas de Configuration Manager para Protección contra vulnerabilidades de seguridad de Windows Defender
<!-- 1356220 -->
Se han agregado nuevos parámetros de directivas para el acceso a las carpetas Reducción de la superficie expuesta a ataques y Controlado para [Protección contra vulnerabilidades de seguridad de Windows Defender](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) en Configuration Manager.

**Nueva configuración para el acceso a la carpeta Controlado**<br/>
Hay dos opciones adicionales al configurar el acceso controlado a carpetas: **Bloquear solo sectores del disco** y **Auditar solo sectores del disco**. Estos dos parámetros permiten que el acceso a la carpeta Controlado se habilite solo para sectores de arranque, y no habilita la protección de carpetas específicas o las carpetas protegidas de manera predeterminada. 

**Nueva configuración para la reducción de la superficie expuesta a ataques**
- Use la protección avanzada frente a ransomware.
- Bloquee el robo de credenciales desde el subsistema de autoridad de seguridad local de Windows. 
- Bloquee la ejecución de archivos ejecutables a menos que cumplan una¡os criterios de prevalencia, antigüedad o lista de confianza. 
- Bloquee la ejecución desde USB de procesos que no sean de confianza y estén sin firmar.



## <a name="microsoft-edge-browser-policies"></a>Directivas del explorador Microsoft Edge
<!-- 1357310 -->
Para los clientes que usan el explorador web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) en los clientes de Windows 10, ahora puede crear una directiva de configuración de cumplimiento de Configuration Manager para configurar varias opciones de Microsoft Edge. Actualmente, esta directiva incluye las siguientes opciones:
- **Set Microsoft Edge browser as default** (Establecer el explorador Microsoft Edge como predeterminado): configura los parámetros de la aplicación predeterminada de Windows 10 en cuanto a explorador web para que sea Microsoft Edge.
- **Permitir funcionalidad desplegable de la barra de direcciones**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [AllowAddressBarDropdown browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown) (Directiva de explorador AllowAddressBarDropdown).
- **Permitir sincronizar favoritos entre exploradores de Microsoft**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [SyncFavoritesBetweenIEAndMicrosoftEdge browser policy](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge) (Directiva de explorador SyncFavoritesBetweenIEAndMicrosoftEdge).
- **Permitir borrar datos de exploración al salir**: requiere Windows 10, versión 1703 o posteriores. Para obtener más información, consulte [ClearBrowsingDataOnExit browser policy](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit) (Directiva de explorador ClearBrowsingDataOnExit).
- **Permitir encabezados Do Not Track**: para obtener más información, vea [AllowDoNotTrack browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack) (Directiva de explorador AllowDoNotTrack).
- **Permitir autorrelleno**: para obtener más información, vea [AllowAutofill browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill) (Directiva de explorador AllowAutofill).
- **Permitir cookies**: para obtener más información, vea [AllowCookies browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies). (Directiva de explorador AllowCookies).
- **Permitir bloqueador de elementos emergentes**: para obtener más información, vea [AllowPopups browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups). (Directiva de explorador AllowPopups).
- **Permitir sugerencias de búsqueda en la barra de direcciones**: para obtener más información, vea [AllowSearchSuggestionsinAddressBar browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar) (Directiva de explorador AllowSearchSuggestionsinAddressBar).
- **Permitir el envío de tráfico de la intranet a Internet Explorer**: para obtener más información, vea [SendIntranetTraffictoInternetExplorer browser policy](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer) (Directiva de explorador SendIntranetTraffictoInternetExplorer).
- **Permitir administrador de contraseñas**: para obtener más información, vea [AllowPasswordManager browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager) (Directiva de explorador AllowPasswordManager).
- **Permitir Herramientas de desarrollo**: para obtener más información, vea [AllowDeveloperTools browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools) (Directiva de explorador AllowDeveloperTools).
- **Permitir extensiones**: para obtener más información, vea [AllowExtensions browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions) (Directiva de explorador AllowExtensions).

### <a name="prerequisites"></a>Requisitos previos
- Cliente de Windows 10 unido a Azure Active Directory. 

### <a name="known-issues"></a>Problemas conocidos
- Los dispositivos unidos a un dominio local no pueden aplicar esta directiva en esta versión. Este problema también afecta a los dispositivos unidos a un dominio híbrido.

### <a name="try-it-out"></a>Haga la prueba  
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.

**Creación de la directiva**
1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**. Expanda **Configuración de cumplimiento** y seleccione el nuevo nodo **Microsoft Edge Browser Profiles** (Perfiles de explorador de Microsoft Edge). Haga clic en la opción de cinta de opciones **Create Microsoft Edge Browser Policy** (Crear directiva de explorador de Microsoft Edge).
2. Especifique un **nombre** para la directiva, opcionalmente, escriba una **descripción** y haga clic en **Siguiente**.
3. En la página **configuración**, cambie el valor a **Configurado** para incluir en esta directiva y haga clic en **Siguiente**.
4. En la página **Plataformas admitidas**, seleccione las versiones y las arquitecturas de sistema operativo a las que se aplica esta directiva y haga clic en **Siguiente**. 
5. Complete el asistente.

**Implementación de la directiva**
1. Seleccione la directiva y haga clic en la opción de cinta de opciones **Implementar**.
2. Haga clic en **Examinar** para seleccionar la recopilación de usuarios o dispositivos en la que desea implementar la directiva. 
3. Seleccione opciones adicionales según sea necesario. Genere alertas cuando la directiva no sea compatible. Establezca la programación según la cual el cliente evalúa el cumplimiento del dispositivo con esta directiva.
4. Haga clic en **Aceptar** para crear la implementación.

Como ocurre con cualquier directiva de configuración de cumplimiento, el cliente corrige la configuración según la programación que especifique. [Supervise el cumplimiento del dispositivo y genere informes al respecto](../../compliance/deploy-use/monitor-compliance-settings.md) en la consola de Configuration Manager.



## <a name="report-for-default-browser-counts"></a>Informe sobre la cantidad de exploradores predeterminados
<!-- 1357830 -->
Ahora hay un nuevo informe para mostrar la cantidad de clientes con un explorador web específico como valor predeterminado de Windows. 

### <a name="known-issues"></a>Problemas conocidos
- Cuando abra el informe por primera vez, solo aparece el número y no el valor BrowserProgID. Para solucionar este problema, modifique la consulta para el informe a la siguiente sintaxis:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Haga la prueba  
 Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.
1. En la consola de **Configuration Manager**, área de trabajo **Supervisión**, expanda **Generación de informes**, **Informes** y seleccione **Software - Compañías y productos**.
2. Ejecute el informe **Default Browser counts** (Cantidad de exploradores predeterminados).

Utilice la siguiente referencia para los valores BrowserProgID más habituales:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE.HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Opera Software
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Compatibilidad con dispositivos Windows 10 ARM64
<!-- 1353704 -->
A partir de esta versión, el cliente de Configuration Manager se admite en dispositivos Windows 10 ARM64. Las características de administración de cliente existentes deben funcionar con estos nuevos dispositivos. Por ejemplo, el inventario de hardware y software, las actualizaciones de software y la administración de aplicaciones. La implementación de sistema operativo no se admite actualmente. 

## <a name="changes-to-phased-deployments"></a>Cambios en las implementaciones por fases
<!-- 1357405 -->
Las implementaciones por fases automatizan una implementación coordinada y secuencial de software en varias implementaciones. En esta versión Technical Preview, se puede completar el Asistente para la implementación por fases para secuencias de tareas en la consola de administración y para las implementaciones que se creen. Sin embargo, la segunda fase no se inicia automáticamente después de cumplir los criterios de la primera fase. La segunda fase se puede iniciar manualmente con una instrucción SQL.   

### <a name="try-it-out"></a>Haga la prueba  
  Intente completar las tareas. Después, envíe **Comentarios** desde la pestaña **Inicio** de la cinta de opciones para hacernos saber cómo ha funcionado.
 
**Creación de una implementación por fases para una secuencia de tareas** </br>
1. En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en **Secuencias de tareas**.
2. Haga clic con el botón derecho en una secuencia de tareas existente y seleccione **Create Phased Deployment** (Crear implementación por fases). 
3. En la pestaña **General** asigne un nombre y una descripción (opcional) a la implementación por fases y seleccione **Automatically create a default two phase deployment** (Crear automáticamente una implementación de dos fases predeterminada). 
4. Rellene los campos **First Collection** (Primera recopilación) y **Second Collection** (Segunda recopilación). Seleccione **Siguiente**.
5. En la pestaña **Configuración**, elija una opción para cada una de las opciones de programación y haga clic en **Siguiente** cuando haya terminado. 
6. En la pestaña **Fases**, modifique cualquiera de las fases si es necesario y después haga clic en **Siguiente**.
7. Confirme las selecciones en la pestaña **Resumen** y después haga clic en **Siguiente** para continuar.
8. Cuando se cumplan los criterios para la primera fase, siga las instrucciones para iniciar la segunda fase con una instrucción SQL.
 
**Inicio de la segunda fase con una instrucción SQL**
1. Identifiquer el valor de PhasedDeploymentID para la implementación que ha creado con la siguiente consulta SQL:<br/> `Select * from PhasedDeployment`
2. Ejecute la instrucción siguiente para iniciar la fase de producción:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
