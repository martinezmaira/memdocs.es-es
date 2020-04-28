---
title: Funcionalidades de Technical Preview 1604
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1604.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1785880af8c7d0d106abfe3eea8ecd390f6ce6b1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074459"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Funciones de Technical Preview 1604 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1604 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager.      Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.  

 Estas son las nuevas características que puede probar con esta versión.  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a> Administración de aplicaciones adquiridas por volumen de la Tienda Windows para empresas  
 La [Tienda Windows para empresas](https://www.microsoft.com/business-store) es el lugar donde puede buscar y adquirir aplicaciones para su organización, individualmente o por volumen. Al conectar la tienda a Configuration Manager, puede administrar aplicaciones adquiridas por volumen desde la consola de Configuration Manager, por ejemplo:  

-   Puede sincronizar la lista de aplicaciones adquiridas con Configuration Manager.  

-   Las aplicaciones que se sincronizan aparecen en la consola de Configuration Manager y se pueden implementar igual que cualquier otra aplicación.  

-   Puede controlar cuántas licencias hay disponibles y cuántas se están usando en la consola de Configuration Manager  

### <a name="try-it-out"></a>Haga la prueba  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Escenario 1: Configurar la sincronización de la Tienda Windows para empresas  

1.  En Azure Active Directory, registre Configuration Manager como una herramienta de administración "Aplicación web o API web". De este modo, obtendrá un identificador de cliente que necesitará más adelante.  

    1.  En el nodo **Active Directory** de [https://manage.windowsazure.com](https://manage.windowsazure.com), seleccione Azure Active Directory y luego haga clic en **Aplicaciones** > **Agregar**.  

    2.  Haga clic en **Agregar una aplicación que mi organización está desarrollando**.  

    3.  Escriba un nombre para la aplicación, seleccione **Aplicación web y/o** **API web** y haga clic en la flecha Siguiente.  

    4.  Escriba la misma dirección URL para **URL de inicio de sesión** y **URI de id. de aplicación**.  La dirección URL puede ser cualquiera (no es necesario que se resuelva en una dirección real). Por ejemplo, puede escribir **https://&lt;suDominio\>/sccm**.  

    5.  Complete el asistente.  

2.  En Azure Active Directory, cree una clave de cliente para la herramienta de administración registrada.  

    1.  Resalte la aplicación que acaba de crear y haga clic en **Configurar**.  

    2.  En **Claves**, seleccione una duración de la lista y haga clic en **Guardar**.  De este modo, se creará una nueva clave de cliente.  No salga de esta página hasta que haya incorporado correctamente la Tienda Windows para empresas a Configuration Manager.  

3.  En la Tienda Windows para empresas, configure Configuration Manager como la herramienta de administración de la tienda.  

    1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e inicie sesión si se le solicita.  

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

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Escenario 2: Crear e implementar una aplicación de Configuration Manager a partir de una aplicación con licencia sin conexión de la Tienda Windows para empresas  

1.  En el área de trabajo **Biblioteca de software** de la consola de Configuration Manager, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.  

2.  La lista **Aplicaciones adquiridas de la Tienda Windows para empresas** muestra un listado de las aplicaciones que se han sincronizado desde la tienda. Elija la aplicación que quiere implementar y, luego, en la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear aplicación**.  

3.  Se crea una aplicación de Configuration Manager que contiene la aplicación de la Tienda Windows para empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a> Mejoras en la administración de Microsoft Passport for Work  
 Ahora puede implementar directivas de Passport for Work para dispositivos de Windows 10 unidos a dominio administrados por el cliente de Configuration Manager.  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a> Opción de cambio a un nuevo punto de actualización de software para clientes  
 En 1604 Technical Preview, puede habilitar la opción de cambiar a un nuevo punto de actualización de software para clientes de Configuration Manager cuando hay problemas con el punto de actualización de software activo. Para esta opción, debe tener varios puntos de actualización de software disponibles en un sitio primario. Esta opción se habilita en una colección de dispositivos y, una vez habilitada, los clientes de la colección buscan otro punto de actualización de software en el siguiente examen cuando el cliente no se puede conectar correctamente al punto de actualización de software activo. En función de las opciones de configuración de WSUS (clasificaciones de actualizaciones, productos, etc.), el cambio a un nuevo punto de actualización de software generará tráfico de red adicional. Por lo tanto, solo se debe utilizar esta opción cuando sea necesario.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para habilitar la opción de cambiar los puntos de actualización de software  

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad > Información general > Recopilaciones de dispositivos**.  

2.  En la pestaña **Inicio** del grupo **Recopilación** , haga clic en **Notificación de cliente**y luego en **Cambiar al siguiente punto de actualización de software**.  

> [!NOTE]  
>  Esta opción solo está disponible en los sitios que tienen varios puntos de actualización de software.  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a> Configuración de cliente para administrar la Configuración de caché de cliente y la Caché del mismo nivel de clientes  
 La versión 1604 de Technical Preview introduce dos nuevas opciones de configuración para el cliente del dispositivo que repercuten en el uso de la caché del cliente. Las dos se pueden utilizar individualmente, pero se configuran en la misma hoja de propiedades de la configuración del cliente y se combinan para ayudarle a administrar la implementación de contenido para clientes en ubicaciones remotas.  

-   La primera es la **caché del mismo nivel de cliente**, una solución integrada de Configuration Manager para que los clientes compartan contenido con otros clientes directamente desde su caché local. Para que los clientes de la Caché del mismo nivel compartan contenido, estos deben pertenecer al mismo grupo de límites. La caché del mismo nivel no reemplaza el uso de otras soluciones como BranchCache, sino que funciona en paralelo para ofrecerle más opciones que amplíen las tradicionales soluciones de implementación de contenido (como los puntos de distribución).  

     Después de implementar la configuración de cliente que habilita la caché del mismo nivel en una colección, los miembros de esa colección pueden actuar como origen de contenido del mismo nivel para otros clientes de su grupo de límites.  El cliente que actúa como origen de contenido del mismo nivel enviará una lista de contenido disponible que ha almacenado en caché a su punto de administración. Después, cuando el siguiente cliente de ese grupo de límites solicita ese contenido, se ofrece el origen de caché del mismo nivel como posible origen de contenido junto con todos los puntos de distribución configurados para ser rápidos. El cliente selecciona un origen de contenido aleatorio de este grupo combinado de orígenes de contenido. Los clientes solo buscarán contenido de un punto de distribución configurado para ser lento cuando no haya puntos de distribución rápidos ni orígenes de caché del mismo nivel en el grupo de límites.  

-   La segunda opción nueva permite **administrar el tamaño de la memoria caché** en los clientes. Puede establecer que la memoria caché tenga un tamaño máximo en megabytes y como porcentaje del espacio en la unidad del cliente.  El cliente aplica el valor que se alcance primero.  

Para ayudarle a entender el uso de la caché del mismo nivel, puede ver el panel **Orígenes de datos de cliente**. En la consola, vaya a **Supervisión > Estado de cliente > Orígenes de datos de cliente**. Aquí puede seleccionar un período de tiempo que se aplicará al panel. A continuación, en la pantalla, puede seleccionar el grupo de límites o el paquete para el que desea ver información. Al ver la información, puede mantener el puntero sobre la superficie para ver más detalles sobre los distintos orígenes de contenido o directiva.  

 También puede usar un nuevo informe, **Orígenes de datos de cliente - Resumen**, para ver un resumen de los orígenes de datos de cliente de cada grupo de límites.   
**Requisitos para usar la caché del mismo nivel:**  

-   Debe configurar el sitio con una **Cuenta de acceso a la red** que tenga **Control total** sobre la carpeta de caché en cada cliente. De forma predeterminada, es **%windir%\ccmcache**  

-   Los clientes solo pueden transferir el contenido mediante la Caché del mismo nivel cuando son miembros del mismo grupo de límites.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar las opciones de cliente de la caché del mismo nivel de cliente  

1.  Ambas opciones se configuran en la misma página de la configuración de cliente. En la consola de Configuration Manager, vaya a **Administración > Configuración de cliente** y luego abra el objeto de configuración de cliente de dispositivo que quiera usar. También puede modificar el objeto Configuración de cliente predeterminada.  

2.  En la lista de configuraciones disponibles, seleccione **Configuración de caché de cliente**.  

3.  Para administrar el tamaño de la memoria caché, establezca **Configurar el tamaño de caché de cliente** en **Sí**. Luego puede configurar el tamaño máximo de la caché en megabytes y como un porcentaje del espacio de unidad de los clientes.  

4.  Para permitir a los clientes participar en la caché del mismo nivel de cliente, establezca **Habilitar el cliente de Configuration Manager en el SO completo para compartir contenido** en **Sí**. Luego puede configurar los puertos que usan los clientes, incluso si van a emplear HTTP o HTTPS.  

### <a name="try-it-out"></a>Haga la prueba  
 Intente realizar las siguientes tareas y después use la información de comentarios que se encuentra al principio de este tema para hacernos saber cómo ha funcionado:  

1.  Modificar la configuración de cliente para especificar un nuevo tamaño de la memoria caché de cliente y luego confirmar esta configuración en un cliente.  

2.  Usar la configuración de cliente para configurar el uso de la caché del mismo nivel por parte de varios clientes  

3.  Implementar contenido en clientes de manera que algunos o la mayoría obtengan ese contenido desde otro cliente mediante la caché del mismo nivel.  Puede confirmar el origen de contenido utilizado consultando el nuevo panel.  

    > [!NOTE]  
    >  Para completar esta tarea con la versión preliminar técnica y un único punto de distribución, configure el punto de distribución de manera que sea lento para la ubicación de red de todos los clientes. A continuación, distribuya el contenido a un único cliente.  Una vez de que el cliente obtiene el contenido, puede distribuirlo a clientes adicionales que deben buscar elementos locales del mismo nivel para usarlos como origen de contenido antes de utilizar el punto de distribución considerado lento desde la ubicación del cliente.  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a> Compatibilidad con Passport for Work como KSP  
 Configuration Manager permite la integración con Microsoft Passport for Work, que es un método alternativo de inicio de sesión que usa Active Directory, o una cuenta de Azure Active Directory, para reemplazar una contraseña, una tarjeta inteligente o una tarjeta inteligente virtual.  
Passport permite usar un gesto de usuario al iniciar sesión en lugar de una contraseña. Un gesto de usuario podría ser una autenticación biométrica de PIN simple, como Windows Hello, o un dispositivo externo como un lector de huellas digitales.  

-   Puede usar Configuration Manager para controlar qué gestos pueden y no pueden utilizar los usuarios para iniciar sesión, y para configurar los requisitos de complejidad del PIN.  

-   Puede almacenar certificados de autenticación en el proveedor de almacenamiento de claves (KSP) de Passport for Work.  

Cuando un usuario crea un PIN de Passport, Windows envía una notificación que escucha Configuration Manager.  De este modo, Configuration Manager puede conocer rápidamente qué usuarios han creado un PIN de Passport. Configuration Manager puede entonces emitir nuevos certificados a esos usuarios si Passport se usa como proveedor de almacenamiento de claves en un perfil de certificado.  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a> Atestación de estado del dispositivo local  
 Ahora es posible configurar la atestación de estado para dispositivos con Windows 10 a fin de establecer comunicación mediante la infraestructura local.  Los administradores pueden especificar si la notificación se realiza a través de la nube o de recursos locales.  Si se selecciona **local** para la notificación de atestación de estado, se puede especificar un URI para el servicio. Esto permite a los equipos cliente sin acceso a Internet habilitar y administrar dispositivos con la atestación de estado.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Habilitación de la atestación de estado para dispositivos locales  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración de cliente**y, después, establezca **Usar el servicio de atestación de estado local** en **Sí**.  

2.  Especifique el valor de **URL del servicio de atestación de estado local**y, después, haga clic en **Aceptar**.  

Para probarlo, configure el servicio de atestación de estado local mediante la configuración del agente de cliente.  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a> Configuración de SmartLock para dispositivos Android  
 Se ha agregado un nuevo valor, **Permitir Smart Lock y otros agentes de confianza**, al elemento de configuración **Android y Samsung KNOX** que le permite controlar la característica Smart Lock en dispositivos Android compatibles. Esta funcionalidad del teléfono, conocida también en ocasiones como agentes de confianza, le permite deshabilitar u omitir la contraseña de la pantalla de bloqueo del dispositivo si el dispositivo está en una ubicación de confianza, como cuando se conecta a un dispositivo Bluetooth específico o cuando está cerca de una etiqueta NFC. Puede utilizar esta opción para impedir que los usuarios finales configuren SmartLock.  
