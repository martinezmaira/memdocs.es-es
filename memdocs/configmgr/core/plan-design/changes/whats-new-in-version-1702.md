---
title: Nueva versión 1702
titleSuffix: Configuration Manager
description: Conozca en detalle los cambios y las nuevas funciones introducidas en la versión 1702 de Configuration Manager.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 5c125bc92c8949384486c7efc03cea122258092e
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993512"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>Novedades de la versión 1702 de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 1702 de la rama actual de Configuration Manager está disponible como actualización en consola en los sitios instalados previamente que ejecutan las versiones 1602, 1606 o 1610. También está disponible como una versión de línea de base que puede utilizar al instalar una nueva implementación.

> [!TIP]  
> Para instalar un sitio nuevo, debe usar una versión de línea base de Configuration Manager.  
>
> Más información acerca de:    
> - [Instalación de nuevos sitios](../../servers/deploy/install/installing-sites.md)  
> - [Instalación de actualizaciones en los sitios](../../servers/manage/updates.md)  
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)

En las secciones siguientes se proporcionan detalles sobre los cambios y las nuevas funciones introducidas en la versión 1702 de Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Características y sistemas operativos en desuso
Obtenga información sobre los cambios de compatibilidad antes de implementarlos en [Elementos eliminados y en desuso](deprecated/removed-and-deprecated.md).

La versión 1702 anula la compatibilidad de los siguientes productos:
- **SQL Server 2008 R2**, para los servidores de base de datos del sitio. La interrupción de la compatibilidad se [anunció por primera vez](deprecated/removed-and-deprecated-server.md#sql-server) el 10 de julio de 2015. Esta versión de SQL Server sigue siendo compatible cuando se utiliza una versión de Configuration Manager anterior a la versión 1702.
- **Windows Server 2008 R2**, para servidores del sistema de sitios y la mayoría de roles de sistema de sitio. La interrupción de la compatibilidad se [anunció por primera vez](deprecated/removed-and-deprecated-server.md#server-os) el 10 de julio de 2015. Esta versión de Windows sigue siendo compatible cuando se utiliza una versión de Configuration Manager anterior a la versión 1702.  
- **Windows Server 2008**, para servidores del sistema de sitios y la mayoría de roles de sistema de sitio. La interrupción de la compatibilidad se [anunció por primera vez](deprecated/removed-and-deprecated-server.md#server-os) el 10 de julio de 2015.
- **Windows XP Embedded**, como un sistema operativo cliente. La interrupción de la compatibilidad se [anunció por primera vez](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems) el 10 de julio de 2015. Esta versión de Windows sigue siendo compatible cuando se utiliza una versión de Configuration Manager anterior a la versión 1702.




## <a name="site-infrastructure"></a>Infraestructura del sitio

### <a name="improvements-for-in-console-search"></a>Mejoras de búsqueda en consola
A continuación se presentan mejoras en el uso de la búsqueda en la consola de Configuration Manager:
- **Ruta del objeto:**  
  Ahora muchos objetos admiten una columna denominada **Ruta del objeto**.  Cuando busca e incluye esta columna en los resultados mostrados, puede ver la ruta de cada objeto. Por ejemplo, si ejecuta una búsqueda de aplicaciones en el nodo Aplicaciones y también está buscando subnodos, la columna *Ruta del objeto* del panel de resultados le mostrará la ruta de acceso a cada objeto devuelto.   

- **Conservación del texto de búsqueda:**  
  Ahora, cuando escribe texto en el cuadro de texto de búsqueda y luego cambia entre buscar en un subnodo y el nodo actual, el texto que escribió se conserva y permanece disponible para una nueva búsqueda sin tener que volver a escribirlo.

- **Conservación de su decisión para buscar subnodos:**  
  La opción que elija para buscar el *nodo actual* o *todos los subnodos* ahora se mantiene cuando cambia el nodo en el que está trabajando. Este nuevo comportamiento significa que no necesita restablecer constantemente la decisión al desplazarse por la consola. De manera predeterminada, cuando abre la consola, la opción es la de buscar solo en el nodo actual.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentarios desde la consola de Configuration Manager

Puede utilizar las opciones de comentario en consola para enviar comentarios directamente al equipo de desarrollo.

Puede encontrar la opción **Comentarios**:
- En la cinta de opciones, en el extremo izquierdo de la pestaña Inicio de cada nodo.  
  ![Cinta de opciones](./media/feedback-home.png)

- Al hacer clic con el botón derecho en cualquier objeto de la consola.   
   ![Opción de hacer clic con el botón derecho](./media/feedback-option.png)   

  Al hacer clic en **Comentarios** se abre el explorador en el [sitio web de comentarios de UserVoice de Configuration Manager](https://configurationmanager.uservoice.com/forums/300492-ideas).


###  <a name="changes-for-updates-and-servicing"></a>Cambios para actualizaciones y mantenimiento
A continuación se indican los cambios en Actualizaciones y mantenimiento:

- **Ubicación del nodo**   
  Después de instalar la versión 1702, el nodo **Actualizaciones y mantenimiento** aparece como un nodo de nivel superior en **Administración**. Ya no aparece como un nodo secundario en **Cloud Services**.

- **Nuevos estados de las actualizaciones**  
  Cuando aparecen las actualizaciones disponibles en la consola, hay dos nuevos estados:  
  - **Disponible para instalar**: se trata de una actualización que ha descargado y está disponible para instalarla.
  - **Listo para descargar**: esta actualización está disponible, pero no se ha descargado. Puede descargar esta actualización, pero se ha sustituido por una más reciente.


- **Opciones de actualización más sencillas**  
  La próxima vez que la infraestructura sea apta para dos o más actualizaciones, se descargará únicamente la actualización más reciente. Por ejemplo, si la versión actual del sitio es dos o más versiones más antigua que la versión más reciente disponible, solo se descarga automáticamente la versión más reciente de la actualización.  

  Puede optar por descargar e instalar las demás actualizaciones disponibles, incluso cuando no sean la versión más reciente. Si descarga una actualización anterior, recibirá una advertencia de que la actualización se ha reemplazado por una más reciente. Para descargar una actualización que esté *Disponible para descarga*, seleccione la actualización en la consola y después haga clic en **Descargar**.

- **Limpieza mejorada de las actualizaciones más antiguas**   
  Se ha agregado una función de limpieza automática que elimina las descargas innecesarias de la carpeta "EasySetupPayload" en el servidor de sitio. Como esta función se presenta con la versión 1702, la limpieza comienza a funcionar después de instalar una actualización subsiguiente como un paquete acumulativo de actualizaciones o una versión futura de actualización.  


### <a name="data-warehouse-service-point"></a>Punto de servicio de almacenamiento de datos
Use el punto de servicio de almacenamiento de datos para almacenar y generar informes de datos históricos a largo plazo para su implementación de Configuration Manager.

El almacenamiento de datos admite hasta 2 TB de datos, con marcas de tiempo para el seguimiento de cambios. El almacenamiento de datos se consigue mediante sincronizaciones automatizadas desde la base de datos del sitio de Configuration Manager a la base de datos de almacenamiento de datos. Puede acceder a esta información desde su punto de Reporting Services.

Para más información, consulte [Punto de servicio del almacenamiento de datos](../../servers/manage/data-warehouse.md).


### <a name="peer-cache-improvements"></a>Mejoras de almacenamiento en caché del mismo nivel
A partir de la versión 1702, un equipo de origen de almacenamiento en caché del mismo nivel rechazará una solicitud de contenido cuando el equipo de origen de almacenamiento en caché del mismo nivel cumpla alguna de las condiciones siguientes:  
-  Está en modo de batería baja.
-  La carga de CPU supera el 80 % en el momento en que se solicita el contenido.
-  E/S de disco tiene un valor *AvgDiskQueueLength* superior a 10.
-  No hay más conexiones disponibles para el equipo.   
Para más información, vea **Acceso limitado al origen de almacenamiento en caché del mismo nivel** en [Caché del mismo nivel para clientes de Configuration Manager](../hierarchy/client-peer-cache.md).   

Además, se han agregado tres nuevos informes al punto de notificación. Puede utilizar estos informes para conocer más detalles sobre las solicitudes rechazadas de contenido, incluidos qué grupo de límites, equipos y contenidos están afectados. Vea [Supervisión](../hierarchy/client-peer-cache.md#monitoring) en el tema del almacenamiento en caché del mismo nivel.

### <a name="content-library-cleanup-tool"></a>Herramienta de limpieza de la biblioteca de contenido
Utilice la herramienta [Content Library Cleanup Tool](../hierarchy/content-library-cleanup-tool.md) para quitar contenido de puntos de distribución cuando el contenido deja de estar asociado con una aplicación.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Uso del conector de OMS con la nube de Azure Government
Puede usar el conector de OMS para conectarse a Log Analytics de OMS en la nube de Microsoft Azure Government. Para ello, debe modificar un archivo de configuración antes de instalar el conector de OMS para que el conector pueda trabajar con la nube de Government. Para más información, vea [Uso del conector de OMS con la nube de Azure Government](/azure/azure-monitor/platform/collect-sccm).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Los puntos de actualización de software se agregan a grupos de límites
A partir de la versión 1702, los clientes utilizan grupos de límites para encontrar un nuevo punto de actualización de software, además de para reservar y buscar un nuevo punto de actualización de software si ya no pueden acceder al actual. Puede agregar puntos de actualización de software individuales a grupos de límites diferentes para controlar qué servidores puede encontrar un cliente. Para más información, vea [puntos de actualización de software](../../servers/deploy/configure/boundary-groups.md#bkmk_sup) en el tema de [configuración de grupos de límites](../../servers/deploy/configure/boundary-groups.md).


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Configuración de cumplimiento

### <a name="new-compliance-settings-for-ios"></a>Nueva configuración de cumplimiento para iOS

Hemos agregado muchas configuraciones nuevas para dispositivos iOS, a fin de que coincidan con los disponibles en Microsoft Intune.


## <a name="application-management"></a>Administración de aplicaciones

### <a name="improved-support-for-windows-store-for-business-apps"></a>Compatibilidad mejorada para aplicaciones de la Tienda Windows para empresas

Ahora puede implementar aplicaciones con licencia en línea desde la Tienda Windows para empresas en equipos con Windows 10 que administra con el cliente de Configuration Manager.
Para más información, vea [Administración de aplicaciones adquiridas en la Tienda Windows para empresas](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Comprobar los archivos ejecutables en ejecución antes de instalar una aplicación

En el cuadro de diálogo **Propiedades** de un tipo de implementación, en la pestaña **Comportamiento de instalación**, ahora se puede especificar uno de varios archivos ejecutables que, si se está ejecutando, bloqueará la instalación del tipo de implementación. El usuario debe cerrar el archivo ejecutable en ejecución (o se puede cerrar automáticamente para las implementaciones con un propósito de requerido) antes de poder instalar el tipo de implementación.

Si la aplicación se ha implementado como **Disponible** y un usuario final intenta instalar una aplicación, se le pedirá que cierre los ejecutables en ejecución especificados antes de poder continuar con la instalación.

Si la aplicación se ha implementado como **Requerido** y la opción **Cerrar automáticamente los ejecutables en ejecución especificados en la pestaña Comportamiento de instalación del cuadro de diálogo de propiedades del tipo de implementación** está seleccionada, verán un cuadro de diálogo que les informa de que los archivos ejecutables especificados se cerrarán automáticamente cuando se alcance la fecha límite de instalación de la aplicación.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Mejoras de administración de aplicaciones para MDM híbrida

- [Implementación de aplicaciones iOS adquiridas por volumen en colecciones de dispositivos](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Compatibilidad con el Programa de compras por volumen de iOS para educación](#support-for-ios-volume-purchase-program-for-education)
- [Compatibilidad con varios token del Programa de compras por volumen](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Implementación de sistema operativo

### <a name="expire-stand-alone-media"></a>Expiración de los medios independiente
Al crear medios independientes, hay nuevas opciones para establecer en los medios fechas opcionales de inicio y expiración. Estas opciones están deshabilitadas de forma predeterminada. Las fechas se comparan con la hora del sistema del equipo antes de que se ejecuten los medios independientes. Cuando la hora del sistema es anterior a la hora de inicio o posterior a la hora de expiración, los medios independientes no se inician. Estas opciones también están disponibles mediante el cmdlet de PowerShell New-CMStandaloneMedia. Para obtener información detallada, vea [Crear medios independientes](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="package-id-displayed-in-task-sequence-steps"></a>El identificador de paquete se muestra en los pasos de secuencia de tareas
Todos los pasos de secuencia de tareas que hagan referencia a un paquete, un paquete de controladores, una imagen de sistema operativo, una imagen de arranque o un paquete de actualización del sistema operativo mostrarán el identificador de paquete del objeto al que se hace referencia. Cuando un paso de secuencia de tareas haga referencia a una aplicación, mostrará el identificador de objeto.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Compatibilidad con contenido adicional en medios independientes
Ahora se admite contenido adicional en medios independientes. Puede seleccionar paquetes adicionales, paquetes de controladores y aplicaciones para que se realice una copia intermedia en los medios junto con el resto del contenido al que se hace referencia en la secuencia de tareas. Antes, solo se realizaba una copia intermedia en los medios independientes del contenido al que se hace referencia en la secuencia de tareas. Para obtener información detallada, vea [Crear medios independientes](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="hardware-inventory-collects-uefi-information"></a>El inventario de hardware recopila información de UEFI
Para ayudarle a determinar si un equipo se inicia en modo UEFI están disponibles una nueva clase de inventario de hardware (**SMS_Firmware**) y la propiedad (**UEFI**). Cuando un equipo se inicia en modo UEFI, la propiedad **UEFI** está establecida en **TRUE**. Esto está habilitado en el inventario de hardware de forma predeterminada. Para más información sobre el inventario de hardware, vea [Cómo configurar el inventario de hardware](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Mejoras en los mensajes de advertencia del Centro de software para las secuencias de tareas de alto impacto
Esta versión incluye las siguientes mejoras en los mensajes de advertencia del Centro de software para las secuencias de tareas de implementación de alto impacto:

- En las propiedades de la secuencia de tareas, ahora se puede configurar cualquier secuencia de tareas, incluidas las que no son del sistema operativo, como una implementación de alto riesgo. Cualquier secuencia de tareas que cumpla determinadas condiciones se define automáticamente como de alto impacto. Para obtener información detallada, vea [Administrar implementaciones de alto riesgo](../../servers/manage/settings-to-manage-high-risk-deployments.md).
- En las propiedades de la secuencia de tareas, puede elegir usar el mensaje de notificación predeterminado o crear su propio mensaje de notificación personalizado para las implementaciones de alto impacto.
- En las propiedades de la secuencia de tareas, puede configurar las propiedades del Centro de software, que incluyen realizar un reinicio obligatorio, el tamaño de descarga de la secuencia de tareas y el tiempo de ejecución estimado.
- El mensaje de la implementación de alto impacto predeterminado para actualizaciones en contexto indica ahora que las aplicaciones, los datos y la configuración se migran automáticamente. Anteriormente, el mensaje predeterminado para cualquier instalación de sistema operativo indicaba que todas las aplicaciones, datos y configuraciones se perderían, lo que no era cierto para una actualización en contexto.

Para obtener información detallada, vea [Configuración de los ajustes de la secuencia de tareas de gran impacto](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence).

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Volver a la página anterior cuando se produce un error en una secuencia de tareas
Ahora puede volver a la página anterior cuando ejecuta una secuencia de tareas y se produce un error. Antes de esta versión, tenía que reiniciar la secuencia de tareas si se producía un error. Por ejemplo, puede usar el botón **Anterior** en los siguientes escenarios:

- Cuando un equipo se inicia en Windows PE, el cuadro de diálogo de arranque de la secuencia de tareas puede mostrarse antes de que la secuencia de tareas esté disponible. Cuando hace clic en Siguiente en este escenario, la página final de la secuencia de tareas se muestra con un mensaje de que no existe ninguna secuencia de tareas disponible. Ahora, puede hacer clic en **Anterior** para buscar de nuevo secuencias de tareas disponibles. Puede repetir este proceso hasta que la secuencia de tareas esté disponible.
- Cuando ejecuta una secuencia de tareas, pero los paquetes de contenido dependientes todavía no están disponibles en los puntos de distribución, se produce un error en la secuencia de tareas. Ahora puede distribuir el contenido que falta (si no se ha distribuido todavía) o esperar a que el contenido esté disponible en los puntos de distribución y, después, hacer clic en **Anterior** para reanudar la búsqueda de la secuencia de tareas para el contenido.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Almacenar en la caché previa contenido para las implementaciones y las secuencias de tareas disponibles
A partir de la versión 1702, para las implementaciones disponibles de secuencias de tareas, puede usar el contenido de la caché previa. El contenido de caché previa le proporciona la opción de que el cliente solo descargue el contenido aplicable tan pronto como reciba la implementación. Por lo tanto, cuando el usuario hace clic en **Instalar** en el Centro de software, el contenido está listo y la instalación se inicia rápidamente porque el contenido se encuentra en la unidad de disco duro local. Para obtener información detallada, vea [Configuración del contenido de la caché previa](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversión de BIOS a UEFI durante una actualización local
Windows 10 Creators Update presenta una herramienta de conversión sencilla que automatiza el proceso para volver a particionar el disco duro de hardware compatible con UEFI e integra la herramienta de conversión en el proceso de actualización local de Windows 7 a Windows 10. Cuando esta herramienta se combina con la secuencia de tareas de actualización del sistema operativo y la herramienta de OEM que convierte el firmware de BIOS a UEFI, puede convertir los equipos de BIOS a UEFI durante una actualización local a Windows 10 Creators Update. Para obtener más información, consulte [Task sequence steps to manage BIOS to UEFI conversion (Pasos de la secuencia de tareas para administrar la conversión de BIOS a UEFI)](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Mejoras en el paso de secuencia de tareas para instalar aplicaciones
Esta versión presenta las siguientes mejoras:
- Aumenta el número máximo de aplicaciones que se pueden instalar a 99 en el paso de la secuencia de tareas **Instalar aplicaciones**. Antes, el número máximo era de 9 aplicaciones.
- Al agregar aplicaciones en el paso de secuencia de tareas **Instalar aplicaciones** en el editor de secuencia de tareas, puede seleccionar varias aplicaciones en el panel **Seleccione la aplicación que desea instalar**.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Mejoras en la secuencia de tareas Aplicar controladores automáticamente
Ahora hay disponibles nuevas variables de secuencia de tareas para configurar el valor del tiempo de espera en el paso de secuencia de tareas de aplicación automática de controladores cuando se realizan solicitudes del catálogo HTTP. Están disponibles las siguientes variables y valores predeterminados (en segundos):
- Valor predeterminado de SMSTSDriverRequestResolveTimeOut:  
  Valor predeterminado: 60
- Valor predeterminado de SMSTSDriverRequestConnectTimeOut:  
  Valor predeterminado: 60
- Valor predeterminado de SMSTSDriverRequestSendTimeOut:  
  Valor predeterminado: 60
- Valor predeterminado de SMSTSDriverRequestReceiveTimeOut:  
  Valor predeterminado: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Seguimiento de Windows 10 ADK según la versión de compilación
Ahora, la versión de compilación realiza un seguimiento de Windows 10 ADK para garantizar una experiencia más compatible al personalizar las imágenes de arranque de Windows 10. Por ejemplo, si el sitio usa Windows ADK para Windows 10, versión 1607, solo se pueden personalizar en la consola las imágenes de arranque con la versión 10.0.14393. Para más información sobre cómo personalizar las versiones de WinPE, vea [Personalizar imágenes de arranque](../../../osd/get-started/customize-boot-images.md).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Ya no se puede cambiar la ruta de acceso al origen de la imagen de arranque predeterminada
Configuration Manager administra las imágenes de arranque predeterminadas, y la ruta de acceso de origen de la imagen de arranque predeterminada ya no se puede cambiar en la consola de Configuration Manager o mediante el SDK de Configuration Manager. Puede seguir configurando una ruta de acceso de origen personalizada para las imágenes de arranque personalizadas.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Imágenes de arranque predeterminadas regeneradas tras actualizar Configuration Manager a una versión nueva
A partir de esta versión, al actualizar la versión de Windows ADK y usar las actualizaciones para instalar la última versión de Configuration Manager, este regenerará las imágenes de arranque predeterminadas. Esto incluye la nueva versión de Windows PE a partir del Windows ADK actualizado y la nueva versión del cliente de Configuration Manager, así como los controladores, las personalizaciones, etc. Las imágenes de arranque personalizadas no se verán modificadas. Para obtener más información, consulte [Administrar imágenes de arranque](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault).

## <a name="software-updates"></a>Actualizaciones de software

### <a name="deploy-microsoft-365-apps-to-clients"></a>Implementación de Aplicaciones de Microsoft 365 en clientes
A partir de la versión 1702, desde el panel Administración de clientes de Office 365, puede iniciar el Instalador de Office 365, que le permite configurar las opciones de instalación, descargar archivos desde redes de entrega de contenido (CDN) de Office e implementar los archivos como una aplicación en Configuration Manager. Para obtener más información, consulte [Administrar actualizaciones de Aplicaciones de Microsoft 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_deploy).

> [!IMPORTANT]
> Configuration Manager no administra automáticamente la aplicación de Microsoft 365 creada e implementada con el Asistente para aplicaciones de Office 365 en Configuration Manager hasta que habilite de nuevo la configuración **Habilitar administración del Agente cliente de Office 365** del agente cliente de actualizaciones de software. Para obtener información detallada, vea [Acerca de la configuración de cliente](../../clients/deploy/about-client-settings.md).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Administración de archivos de instalación rápida para actualizaciones de Windows 10
A partir de la versión 1702, Configuration Manager admite archivos de instalación rápida para las actualizaciones de Windows 10. Cuando use una versión compatible con Windows 10, puede usar la configuración de Configuration Manager para descargar solo los cambios entre la actualización acumulativa de Windows 10 del mes actual y la actualización del mes anterior. Sin los archivos de instalación rápida, Configuration Manager descarga cada mes la actualización acumulativa completa de Windows 10 (incluidas todas las actualizaciones de los meses anteriores). Usar los archivos de instalación rápida proporciona descargas más pequeñas y tiempos de instalación más rápidos en los clientes. Para obtener información detallada, vea [Administración de archivos de instalación rápida para actualizaciones de Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Administración de dispositivos móviles

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>En los asistentes para creación de MDM híbrida ya no se pueden seleccionar como destino las versiones de iOS y Android.

A partir de la versión 1702 para la administración de dispositivos móviles (MDM) híbrida, ya no necesita especificar versiones concretas de iOS y Android al crear nuevas directivas y perfiles para dispositivos administrados por Intune. En su lugar, elija uno de los siguientes tipos de dispositivo:

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

> [!NOTE]
> La última versión del sistema operativo móvil disponible en las páginas de propiedades se aplica a esa versión y a todas las versiones subsiguientes. Las páginas de propiedades ofrecen las siguientes opciones para tener como destino sistemas operativos posteriores a Android 7 y iOS 10: 
> - **Android 7 y versiones posteriores**
> - **Todos los dispositivos táctiles iPhone o iPod con iOS 10 y versiones posteriores**
> - **Todos los dispositivos iPad con iOS 10 y versiones posteriores**

### <a name="android-for-work-support"></a>Compatibilidad de Android for Work
A partir de la versión 1702, la administración de dispositivos móviles híbrida con Microsoft Intune ahora admite la inscripción y administración de dispositivos Android for Work.

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementación de aplicaciones iOS adquiridas por volumen en colecciones de dispositivos

Ahora puede implementar aplicaciones con licencia para dispositivos y usuarios. Dependiendo de la capacidad de las aplicaciones para admitir licencias de dispositivo, se solicitará una licencia adecuada al realizar la implementación, como sigue:

| Versión de Configuration Manager | ¿La aplicación admite licencias de dispositivo? | Tipo de colección de implementación | Licencia exigida |
| ----------------------------- | ------------------------------ | -------------------------- | --------------- |
|Anterior a 1702|Sí|Usuario|Licencia de usuario|
|Anterior a 1702|No|Usuario|Licencia de usuario|
|Anterior a 1702|Sí|Dispositivo|Licencia de usuario|
|Anterior a 1702|No|Dispositivo|Licencia de usuario|
|1702 y versiones posteriores|Sí|Usuario|Licencia de usuario|
|1702 y versiones posteriores|No|Usuario|Licencia de usuario|
|1702 y versiones posteriores|Sí|Dispositivo|Licencia de dispositivo|
|1702 y versiones posteriores|No|Dispositivo|Licencia de usuario|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Compatibilidad con el Programa de compras por volumen de iOS para educación

Ahora también puede implementar las aplicaciones adquiridas en el Programa de compra por volumen de iOS para educación y realizar un seguimiento de ellas.

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Compatibilidad con varios token del Programa de compras por volumen

Ahora puede asociar varios tokens del Programa de compras por volumen de Apple con Configuration Manager.

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Compatibilidad con la línea de aplicaciones empresariales de la Tienda Windows para empresas

Ahora puede sincronizar la línea personalizada de aplicaciones empresariales en la Tienda Windows para empresas.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Mejoras de la directiva de cumplimiento de dispositivos de acceso condicional

Una nueva regla de directiva de cumplimiento de dispositivos está disponible para ayudar a bloquear el acceso a los recursos corporativos que admiten el acceso condicional, cuando los usuarios usan aplicaciones que forman parte de una lista de aplicaciones no compatibles. El administrador puede definir la lista de aplicaciones no compatibles cuando se agrega la nueva regla conforme **Aplicaciones que no se pueden instalar**. Esta regla requiere que el administrador escriba el **Nombre de la aplicación**, el **Id. de la aplicación** y el **Publicador de la aplicación** (opcional) al agregar una aplicación a la lista de aplicaciones no compatibles. Esta configuración solo se aplica a dispositivos iOS y Android.

Además, esto ayuda a las organizaciones a mitigar la pérdida de datos a través de aplicaciones no seguras y evitar el consumo excesivo de datos a través de determinadas aplicaciones.


### <a name="new-mobile-threat-defense-monitoring-tools"></a>Nuevas herramientas de supervisión de Mobile Threat Defense

A partir de la versión 1702, tiene a su disposición nuevas formas de supervisar el estado de cumplimiento con el proveedor de servicios Mobile Threat Defense.


## <a name="protect-devices"></a>Proteger los dispositivos

### <a name="detect-outdated-antimalware-client-versions"></a>Detección de versiones del cliente antimalware obsoletas
A partir de la versión 1702, puede configurar una alerta para asegurarse de que los clientes de Endpoint Protection no están obsoletos. Para más información, vea [Alerta para clientes de malware obsoletos](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client).

### <a name="device-health-attestation-updates"></a>Actualizaciones de Atestación de estado de dispositivo
El servicio Atestación de estado de dispositivo para clientes locales ahora puede configurarse y administrarse desde el punto de administración. Para más información, vea [Atestación de estado](../../servers/manage/health-attestation.md).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Perfiles de certificado de Windows Hello para empresas

Si pretende almacenar perfiles de certificado en el contenedor de claves de Windows Hello para empresas, y el perfil de certificado usa el EKU Inicio de sesión de tarjeta inteligente, debe configurar permisos para el registro de clave, a fin de asegurarse de que el certificado se valida correctamente.
Para más información, vea [Configuración de Windows Hello para empresas](../../../protect/deploy-use/windows-hello-for-business-settings.md).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nueva notificación de Windows Hello para empresas para los usuarios finales
Una nueva notificación de Windows 10 informa a los usuarios finales de que deben realizar acciones adicionales para completar la configuración de Windows Hello para empresas (por ejemplo, configurar un PIN).