---
title: Funcionalidades de Technical Preview 1701
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1701.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 7b2afaf1090b1e7c9c53d403f70c17d3e171cdbf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705343"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Funciones de Technical Preview 1701 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*



En este artículo se presentan las características disponibles en la versión 1701 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    


**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Mejoras de los grupos de límites para puntos de actualización de software
A partir de esta vista previa, se usan grupos de límites para asociar los clientes con los puntos de actualización de software. Esto forma parte de un trabajo continuo para expandir los cambios en los grupos de límites para administrar roles adicionales de sistema de sitio.  Se introdujeron cambios en los grupos de límites por primera vez en Technical Preview 1609 y en la Rama actual en la versión 1610.  

Con esta vista previa, se puede usar el nuevo comportamiento del grupo de límites para administrar los puntos de actualización de software que puede usar un cliente, de forma parecida a la manera de administrar el punto de distribución que puede usar un cliente:  

- Los grupos de límites se configuran de modo que se asocien a uno o más servidores que hospedan un punto de actualización de software.
- Los clientes que buscan un nuevo punto de actualización de software intentarán usar uno que esté asociado a su grupo de límites actual.
- Cuando el cliente no puede ponerse en contacto con su punto de actualización de software actual y no encuentra uno en su grupo de límites actual, usa el comportamiento de reserva para expandir el conjunto de puntos de actualización de software disponibles que puede usar.    

Para más información sobre los grupos de límites, vea [Grupos de límites](../servers/deploy/configure/boundary-groups.md) en el contenido de la Rama actual.

Pero con esta vista previa, los grupos de límites para los puntos de actualización de software solo se implementan parcialmente. Puede agregar puntos de actualización de software y configurar grupos de límites vecinos que contengan puntos de actualización de software, pero todavía no se admite el tiempo de reserva para los puntos de actualización de software, por lo que los clientes tendrán que esperar dos horas hasta que se inicie la reserva.

A continuación se describe el comportamiento de los puntos de actualización de software con esta Technical Preview:  

- **Los clientes nuevos usan grupos de límites para seleccionar los puntos de actualización de software.** Los clientes que se instalan después de instalar la versión 1701 seleccionan un punto de actualización de software de entre los que estén asociados al grupo de límites del cliente.

  Esto sustituye el comportamiento anterior, según el cual los clientes seleccionan un punto de actualización de software aleatoriamente de una lista de puntos que comparten el bosque del cliente.   

- **Los clientes instalados previamente siguen usando su punto de actualización de software actual hasta que recurren a la reserva para buscar uno nuevo.**
  Los clientes que ya estaban instalados y que tienen un punto de actualización de software seguirán usándolo hasta que recurran a la reserva. Esto incluye los puntos de actualización de software que no están asociados al grupo de límites actual del cliente. No intentarán encontrar y usar inmediatamente un punto de actualización de software de su grupo de límites actual.

  Los clientes que ya tengan un punto de actualización de software empezarán a usar el comportamiento de este nuevo grupo de límites únicamente cuando el cliente no logre llegar a su punto de actualización de software actual e inicie la reserva.
  Este retraso al cambiar al nuevo comportamiento es deliberado. Se debe a que un cambio en el punto de actualización de software puede producir un gran uso del ancho de banda de red cuando el cliente sincroniza los datos con el nuevo punto de actualización de software. El retraso en la transición puede ayudar a evitar que se sature la red en caso de que todos los clientes cambien a puntos de actualización de software nuevos al mismo tiempo.

- **Opciones de configuración del tiempo de reserva.** En esta Technical Preview no se admiten opciones de configuración para cuando los clientes inician la reserva para buscar un nuevo punto de actualización de software. Esto incluye las opciones de configuración **Fallback times (in minutes)** (Tiempos de reserva (en minutos)) y **Never fallback** (Nunca reserva), que se pueden configurar para las relaciones de diversos grupos de límites.

  En su lugar, los clientes conservan su comportamiento actual, según el cual el cliente intenta conectarse a su punto de actualización de software actual durante dos horas antes de que inicie la reserva para buscar un nuevo punto de actualización de software que pueda usar.

  Cuando un cliente use la reserva, usará las opciones de configuración del grupo de límites para la reserva a fin de crear un grupo de puntos de actualización de software disponibles. Este grupo contiene todos los puntos de actualización de software del *grupo de límites actual* del cliente, los *grupos de límites vecinos* y el *grupo de límites predeterminado del sitio* del cliente.

- **Configuración del grupo de límites de sitio predeterminado.**  
  Considere la posibilidad de agregar un punto de actualización de software a la *Default-Site-Boundary-Group&lt;CódigoDeSitio >* . Esto garantiza que los clientes que no sean miembros de otro grupo de límites puedan recurrir a la reserva para buscar un punto de actualización de software.


Para administrar los puntos de actualización de software de grupos de límites, use los [procedimientos de la documentación de la Rama actual](../servers/deploy/configure/boundary-group-procedures.md), pero recuerde que los tiempos de reserva que puede configurar aún no se usan para los puntos de actualización de software.


## <a name="hardware-inventory-collects-uefi-information"></a>El inventario de hardware recopila información de UEFI
Para ayudarle a determinar si un equipo se inicia en modo UEFI están disponibles una nueva clase de inventario de hardware (**SMS_Firmware**) y la propiedad (**UEFI**). Cuando un equipo se inicia en modo UEFI, la propiedad **UEFI** está establecida en **TRUE**. Esto está habilitado en el inventario de hardware de forma predeterminada. Para más información sobre el inventario de hardware, vea [Cómo configurar el inventario de hardware](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="improvements-to-operating-system-deployment"></a>Mejoras en la implementación de sistema operativo
Hemos realizado las siguientes mejoras en la implementación del sistema operativo, muchas de las cuales son el resultado de los comentarios de User Voice.
- [**Compatibilidad de más aplicaciones con el paso de secuencia de tareas Instalar aplicaciones**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): hemos aumentado el número máximo de aplicaciones que se pueden instalar a 99 en el paso de secuencia de tareas **Instalar aplicaciones**. Antes, el número máximo era de 9 aplicaciones.
- [**Selección de varias aplicaciones en el paso de secuencia de tareas Instalar aplicación**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): ahora, al agregar aplicaciones en el paso de secuencia de tareas Instalar aplicación en el editor de secuencia de tareas, puede seleccionar varias aplicaciones en el panel **Select the application to install** (Seleccione la aplicación que quiere instalar).
- [**Expiración de los medios independientes**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): Al crear medios independientes, hay nuevas opciones para establecer en los medios fechas opcionales de inicio y expiración. Estas opciones están deshabilitadas de forma predeterminada. Las fechas se comparan con la hora del sistema del equipo antes de que se ejecuten los medios independientes. Cuando la hora del sistema es anterior a la hora de inicio o posterior a la hora de expiración, los medios independientes no se inician. Estas opciones también están disponibles mediante el cmdlet de PowerShell New-CMStandaloneMedia.
- [**Compatibilidad con contenido adicional en medios independientes**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): Ahora se admite contenido adicional en medios independientes. Puede seleccionar paquetes adicionales, paquetes de controladores y aplicaciones para que se realice una copia intermedia en los medios junto con el resto del contenido al que se hace referencia en la secuencia de tareas. Antes, solo se realizaba una copia intermedia en los medios independientes del contenido al que se hace referencia en la secuencia de tareas.
- [**Tiempo de espera configurable para el paso de secuencia de tareas de aplicación automática de controladores**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): Ahora hay disponibles nuevas variables de secuencia de tareas para configurar el valor del tiempo de espera en el paso de secuencia de tareas de aplicación automática de controladores cuando se realizan solicitudes del catálogo HTTP. Están disponibles las siguientes variables y valores predeterminados (en segundos):
   - Valor predeterminado de SMSTSDriverRequestResolveTimeOut: 60
   - Valor predeterminado de SMSTSDriverRequestConnectTimeOut: 60
   - Valor predeterminado de SMSTSDriverRequestSendTimeOut: 60
   - Valor predeterminado de SMSTSDriverRequestReceiveTimeOut: 480
- [**El identificador de paquete ahora se muestra en los pasos de secuencia de tareas**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): Todos los pasos de secuencia de tareas que hagan referencia a un paquete, un paquete de controladores, una imagen de sistema operativo, una imagen de arranque o un paquete de actualización del sistema operativo mostrarán el identificador de paquete del objeto al que se hace referencia. Cuando un paso de secuencia de tareas haga referencia a una aplicación, mostrará el identificador de objeto.
- **Seguimiento de Windows 10 ADK según la versión de compilación**: Ahora, la versión de compilación realiza un seguimiento de Windows 10 ADK para garantizar una experiencia más compatible al personalizar las imágenes de arranque de Windows 10. Por ejemplo, si el sitio usa Windows ADK para Windows 10, versión 1607, solo se pueden personalizar en la consola las imágenes de arranque con la versión 10.0.14393. Para más información sobre cómo personalizar las versiones de WinPE, vea [Personalizar imágenes de arranque](../../osd/get-started/customize-boot-images.md).
- **Ya no se puede cambiar la ruta de acceso al origen de la imagen de arranque predeterminada**: Configuration Manager administra las imágenes de arranque predeterminadas, y la ruta de acceso de origen de la imagen de arranque predeterminada ya no se puede cambiar en la consola de Configuration Manager o mediante el SDK de Configuration Manager. Puede seguir configurando una ruta de acceso de origen personalizada para las imágenes de arranque personalizadas.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Hospedar actualizaciones de software en puntos de distribución basados en la nube
A partir de esta versión de vista previa, puede usar un punto de distribución basado en la nube para hospedar un paquete de actualización de software. Pero, dado que puede configurar los clientes para que descarguen las actualizaciones de software directamente desde Microsoft Update, debe tener en cuenta los costes adicionales que puede suponer la implementación de un paquete de actualización de software en un punto de distribución basado en la nube.

Para información sobre el uso de puntos de distribución basados en la nube, vea [Usar un punto de distribución basado en la nube](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) en el contenido de la Rama actual de Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Validar datos de atestación de estado de dispositivo mediante puntos de administración

A partir de esta versión de vista previa, puede configurar los puntos de administración para que validen los datos de informes de atestación de estado para el servicio de atestación de estado local o en la nube. Una nueva pestaña **Opciones avanzadas** en el cuadro de diálogo **Propiedades de componente de punto de administración** permite **Agregar**, **Editar** o **Quitar** la **dirección URL del servicio de atestación de estado del dispositivo local**. También puede especificar una **Configuración de dispositivo personalizada** para que el agente cliente **use el servicio de atestación de estado local**.  Si establece esta opción en **Sí**, se habilitarán los informes al punto de administración local en lugar del servicio basado en la nube.

### <a name="try-it-out"></a>Haga la prueba

- **Habilitar la atestación de estado de dispositivo local en un punto de administración**<br>  En la consola de Configuration Manager, vaya al punto de administración y abra **Propiedades de componente de punto de administración**. Después, haga clic en la pestaña **Opciones avanzadas**. Haga clic en **Agregar** y especifique la dirección URL local (por ejemplo, https://10.10.10.10) para **On-premises device health attestation service URLs** (Direcciones URL del servicio de atestación de estado de dispositivo local)).
- **Habilitar los informes de atestación de estado del punto de administración local para el agente cliente**<br>En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** y haga doble clic o cree una **Configuración de dispositivo personalizada**. Seleccione **Agente de equipo** y establezca **Use on-premises Health Attestation Service** (Usar el servicio de atestación de estado local) en **Sí**. Si **Enable communication with Device Health Attestation Service** (Habilitar la comunicación con el servicio de atestación de estado de dispositivo) está establecido en **Sí** y **Use on-premises Health Attestation** (Usar la atestación de estado local) está establecido en **No**, el punto de administración usará el servicio de atestación de estado de dispositivo basado en la nube.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Usar el conector de OMS para la nube de Microsoft Azure Government
Con esta Technical Preview, ahora puede usar el conector de Microsoft Operations Management Suite (OMS) para conectarse a un área de trabajo de OMS que se encuentre en la nube de Microsoft Azure Government.  

Para ello, modifique un archivo de configuración de modo que apunte a la nube de Government y, después, instale el conector de OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Configurar un conector de OMS para la nube de Microsoft Azure Government
1. En un equipo que tenga instalada la consola de Configuration Manager, edite el archivo de configuración siguiente de modo que apunte a la nube de Government:  ***&lt;ruta de acceso de instalación de CM>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

   **Ediciones:**

   Cambie el valor del nombre de la configuración *FairFaxArmResourceID* de modo que sea igual a "<https://management.usgovcloudapi.net/”>

   - **Original:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
     &lt;value>&lt;/value>   
     &lt;/setting>

   - **Editado:**      
     &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value><https://management.usgovcloudapi.net/&lt;/value>>  
     &lt;/setting>

   Cambie el valor del nombre de la configuración *FairFaxAuthorityResource* para que sea igual a "<https://login.microsoftonline.com/>".

   - **Original:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value>&lt;/value>

   - **Editado:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value><https://login.microsoftonline.com/&lt;/value>>

2. Después de guardar el archivo con los dos cambios, reinicie la consola de Configuration Manager en el mismo equipo y úsela para instalar el conector de OMS. Para instalar el conector, use la información incluida en [Sincronizar datos de Configuration Manager con Microsoft Operations Management Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)y seleccione el **Área de trabajo de Operations Management Suite** que se encuentra en la nube de Microsoft Azure Government.

3. Cuando se haya instalado el conector de OMS, la conexión a la nube de Government estará disponible al usar cualquier consola que se conecte al sitio.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>En los asistentes para creación de MDM híbrida ya no se pueden seleccionar como destino las versiones de iOS y Android.

A partir de esta Technical Preview para la administración de dispositivos móviles (MDM) híbrida, ya no necesita especificar versiones concretas de iOS y Android al crear nuevas directivas y perfiles para dispositivos administrados por Intune. En su lugar, elija uno de los siguientes tipos de dispositivo:

- Android
- Samsung KNOX Standard 4.0 y superior
- iPhone
- iPad

Este cambio afecta a los asistentes para crear los siguientes elementos:

- Elementos de configuración
- Directivas de cumplimiento
- Perfiles de certificado
- Perfiles de correo electrónico
- Perfiles de VPN
- Perfiles de Wi-Fi

Con este cambio, las implementaciones híbridas pueden ofrecer compatibilidad con mayor rapidez para nuevas versiones de iOS y Android sin necesidad de una nueva versión o extensión de Configuration Manager. Una vez que una nueva versión es compatible con Intune independiente, los usuarios podrán actualizar sus dispositivos móviles a dicha versión.

Para evitar problemas al actualizar desde versiones anteriores de Configuration Manager, las versiones de sistema operativo móvil siguen estando disponibles en las páginas de propiedades de estos elementos. Si aún necesita establecer como destino una versión concreta, puede crear el nuevo elemento y, después, especificar la versión de destino en la página de propiedades del elemento recién creado.
