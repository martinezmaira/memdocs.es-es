---
title: Instalar y configurar un punto de actualización de software
titleSuffix: Configuration Manager
description: Los sitios primarios requieren un punto de actualización de software en el sitio de administración central para la evaluación del cumplimiento de las actualizaciones de software y para implementar las actualizaciones de software en los clientes.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 0cddb8df51624a562597da17ea310db0a26081f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696933"
---
# <a name="install-and-configure-a-software-update-point"></a>Instalar y configurar un punto de actualización de software  

*Se aplica a: Configuration Manager (rama actual)*


> [!IMPORTANT]  
>  Antes de instalar el rol de sistema de sitio de punto de actualización de software (SUP), debe comprobar que el servidor cumple las dependencias necesarias y determina la infraestructura de punto de actualización de software en el sitio. Para obtener más información sobre cómo planear las actualizaciones de software y determinar la infraestructura de punto de actualización de software, consulte [Plan for software updates (Planear las actualizaciones de software)](../plan-design/plan-for-software-updates.md).  

 El punto de actualización de software se necesita en el sitio de administración central y en los sitios primarios para habilitar la evaluación del cumplimiento de las actualizaciones de software, e implementar las actualizaciones de software en los clientes. El punto de actualización de software es opcional en los sitios secundarios. El rol de sistema de sitio de punto de actualización de software debe crearse en un servidor que tenga WSUS instalado. El punto de actualización de software interactúa con los servicios de WSUS para configurar las opciones de las actualizaciones de software y solicitar la sincronización de los metadatos de las actualizaciones de software. Si tiene una jerarquía de Configuration Manager, instale y configure primero el punto de actualización de software en el sitio de administración central y, después, en los sitios primarios secundarios. Después, si quiere, puede hacerlo en los sitios secundarios. Cuando tenga un sitio primario independiente, no un sitio de administración central, instale y configure primero el punto de actualización de software en el sitio primario y, a continuación, si lo desea, en los sitios secundarios. Algunas configuraciones solo están disponibles cuando se configura el punto de actualización de software en un sitio de nivel superior. Existen diferentes opciones que debe tener en cuenta en función del lugar en el que instaló el punto de actualización de software.  

> [!IMPORTANT]  
>  Puede instalar más de un punto de actualización de software en un sitio. El primer punto de actualización de software que se instala se configura como el origen de la sincronización, que sincroniza las actualizaciones desde Microsoft Update o desde el origen de la sincronización del canal de subida. Los demás puntos de actualización de software del sitio se configuran como réplicas del primer punto de actualización de software. Por este motivo algunas opciones no están disponibles tras instalar y configurar el punto de actualización de software inicial.  

> [!IMPORTANT]  
>  No se admite la instalación del rol de sistema de sitio del punto de actualización de software en un servidor que se ha configurado y utilizado como un servidor WSUS independiente o mediante un punto de actualización de software para administrar directamente clientes WSUS. Los servidores WSUS existentes solo se admiten como orígenes de sincronización ascendentes para el punto de actualización de software activo. Vea [Sincronizar desde una ubicación de origen de datos ascendente](#BKMK_wsussync).

 Puede agregar el rol de sistema de sitio de punto de actualización de software a un servidor de sistema de sitio existente o puede crear uno nuevo. En la página **Selección de rol del sistema** del **Asistente para crear servidor de sistema de sitio** o el **Asistente para agregar roles de sistema de sitio** , en función de si agrega el rol de sistema de sitio a un servidor de sitio nuevo o existente, seleccione **Punto de actualización de software** y, después, configure las opciones del punto de actualización de software en el asistente. Las opciones varían según la versión de Configuration Manager que usa. Para obtener más información sobre cómo instalar roles de sistema de sitio, consulte [Install site system roles (Instalar roles de sistema de sitio)](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Utilice las siguientes secciones para obtener información acerca de la configuración del punto de actualización de software en un sitio.  

## <a name="proxy-server-settings"></a>Configuración de servidor proxy  
 Puede configurar las opciones del servidor proxy en distintas páginas del **Asistente para crear servidor de sistema de sitio** o el **Asistente para agregar roles de sistema de sitio** según la versión de Configuration Manager que use.  

-   Debe configurar el servidor proxy y, a continuación, especificar cuándo se debe utilizar el mismo para las actualizaciones de software. Configure las siguientes opciones:  

    -   Configure las opciones del servidor proxy en la página **Proxy** del asistente o en la pestaña **Proxy** de Propiedades de sistema de sitio. La configuración del servidor proxy es específica del sistema de sitio, lo que significa que todos los roles de sistema de sitio usan la configuración del servidor proxy que especifica.  

    -   Especifique si quiere que se use el servidor proxy cuando Configuration Manager sincroniza las actualizaciones de software y descarga contenido mediante una regla de implementación automática. Configure las opciones del servidor proxy de punto de actualización de software en la página **Configuración de cuenta y proxy** del asistente o en la pestaña **Configuración de cuenta y proxy** en Propiedades de punto de actualización de software.  

        > [!NOTE]  
        >  La opción **Usar un servidor proxy cuando se descargue contenido mediante reglas de implementación automática** está disponible pero no se utiliza para un punto de actualización de software en un sitio secundario. Solo el punto de actualización de software en el sitio de administración central y el sitio primario descarga contenido de la página de Microsoft Update.  

> [!IMPORTANT]  
>  De forma predeterminada, la cuenta **Sistema local** para el servidor en el que se creó una regla de implementación automática se utiliza para conectarse a Internet y descargar actualizaciones de software cuando se ejecutan las reglas de implementación automática. Cuando esta cuenta no tiene acceso a Internet, las actualizaciones de software no se descargan y se registra la siguiente entrada en ruleengine.log: **No se pudo descargar la actualización de Internet. Error = 12007**. Configure las credenciales para conectarse al servidor proxy cuando la cuenta de sistema local no tiene acceso a Internet.  


## <a name="wsus-settings"></a>Configuración de WSUS  
 Tiene que configurar las opciones de WSUS en varias páginas del **Asistente para crear servidor de sistema de sitio** o del **Asistente para agregar roles de sistema de sitio** en función de la versión de Configuration Manager que use y, en algunos casos, solo en las propiedades del punto de actualización de software, también conocidas como propiedades de componente de punto de actualización de software. Utilice la información de las siguientes secciones para configurar las opciones de WSUS.  

### <a name="wsus-port-settings"></a><a name="BKMK_wsusport"></a>Configuración del puerto de WSUS  
 Debe configurar las opciones del puerto de WSUS en la página Punto de actualización de software del asistente o en las propiedades del punto de actualización de software. Use uno de los procedimientos siguientes para determinar la configuración de puerto usada por WSUS.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Para determinar la configuración de puerto usada en IIS  

 1.  En el servidor WSUS, abra el Administrador de Internet Information Services (IIS).  

 2.  Expanda **Sitios**, haga clic con el botón secundario en el sitio web del servidor WSUS y, a continuación, haga clic en **Modificar enlaces**. En el cuadro de diálogo Enlaces de sitio, se muestran los valores de los puertos HTTP y HTTPS en la columna **Puerto** .


### <a name="configure-ssl-communications-to-wsus"></a>Configuración de las comunicaciones SSL con WSUS  
 Puede configurar las comunicaciones SSL en la página **General** del asistente o en la pestaña **General** en Propiedades de componente de punto de actualización de software.  

 Para obtener más información sobre el uso de SSL, consulte [Decidir si configurar WSUS para usar SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### <a name="wsus-server-connection-account"></a>Cuenta de conexión del servidor WSUS  
 Puede configurar una cuenta para que la utilice el servidor de sitio cuando se conecte a WSUS que se ejecuta en el punto de actualización de software. Cuando no se configura esta cuenta, Configuration Manager usa la cuenta de equipo del servidor de sitio para conectarse a WSUS. Configure la cuenta de conexión del servidor WSUS en la página **Configuración de cuenta y proxy** del asistente o en la pestaña **Configuración de cuenta y proxy** en Propiedades de punto de actualización de software.  Puede configurar la cuenta en distintas partes del asistente en función de la versión de Configuration Manager que usa.  

 Para obtener más información sobre las cuentas de Configuration Manager, consulte [Cuentas usadas](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Origen de la sincronización  
 Es posible configurar el origen de la sincronización ascendente para la sincronización de actualizaciones de software en la página **Origen de la sincronización** del asistente, o en la pestaña **Configuración de sincronización**, en Propiedades de componente de punto de actualización de software. Las opciones para el origen de la sincronización varían dependiendo del sitio.  

 Utilice la siguiente tabla que incluye las opciones disponibles para configurar el punto de actualización de software en un sitio.  

|Sitio|Opciones de origen de sincronización disponibles|  
|----------|----------------------------------------------|  
|-   Sitio de administración central<br />-   Sitio primario independiente|-   Sincronizar desde el sitio web de Microsoft Update<br />-   Sincronizar desde una ubicación de origen de datos ascendente<br />-   No sincronizar desde Microsoft Update o desde el origen de datos ascendente|  
|-   Puntos de actualización de software adicionales en un sitio<br />-   Sitio primario secundario<br />-   Sitio secundario|-   Sincronizar desde una ubicación de origen de datos ascendente|  

 En la lista siguiente se proporciona más información acerca de cada opción que puede utilizar como origen de la sincronización:  

-   **Sincronizar desde Microsoft Update**: Utilice esta opción para sincronizar los metadatos de las actualizaciones de software desde Microsoft Update. El sitio de administración central debe tener acceso a Internet; de lo contrario, se producirá un error de sincronización. Esta opción solo está disponible cuando se configura el punto de actualización de software en el sitio de nivel superior.  

    > [!NOTE]  
    >  Si hay un firewall entre el punto de actualización de software e Internet, tal vez sea necesario configurar el firewall para aceptar los puertos HTTP y HTTPS que se usan para el sitio web de WSUS. También es posible restringir el acceso en el firewall a dominios limitados. Para obtener más información sobre la planeación de un firewall que admita actualizaciones de software, consulte [Configurar firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **<a name="BKMK_wsussync"></a>Sincronizar desde una ubicación de origen de datos que preceden en la cadena**: Utilice esta opción para sincronizar los metadatos de las actualizaciones de software desde el origen de la sincronización ascendente. Los sitios primarios secundarios y los sitios secundarios se configuran automáticamente para utilizar la dirección URL del sitio primario para esta opción. Tiene la posibilidad de sincronizar las actualizaciones de software desde un servidor WSUS existente. Especifique una dirección URL, como por ejemplo `https://WSUSServer:8531`, donde 8531 es el puerto que se usa para conectarse al servidor WSUS.  

-   **No sincronizar desde Microsoft Update o desde el origen de datos que preceden en la cadena**: Utilice esta opción para sincronizar manualmente las actualizaciones de software cuando se desconecte de Internet el punto de actualización de software en el sitio de nivel superior. Para obtener más información, consulte [Sincronizar actualizaciones de software desde un punto de actualización de software desconectado](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  Si hay un firewall entre el punto de actualización de software e Internet, tal vez sea necesario configurar el firewall para aceptar los puertos HTTP y HTTPS que se usan para el sitio web de WSUS. También es posible restringir el acceso en el firewall a dominios limitados. Para obtener más información sobre la planeación de un firewall que admita actualizaciones de software, consulte [Configurar firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 También es posible configurar si se van a crear eventos de informe de WSUS en la página **Origen de la sincronización** del asistente, o en la pestaña **Configuración de sincronización**, en Propiedades de componente de punto de actualización de software. Configuration Manager no usa estos eventos. Por lo tanto, generalmente le convendrá elegir el valor predeterminado **No crear eventos de informe de WSUS**.  

## <a name="synchronization-schedule"></a>Programación de sincronización  
 Configure la programación de sincronización en la página **Programación de sincronización** del asistente o en las Propiedades de componente de punto de actualización de software. Esta opción solo se configura en el punto de actualización de software del sitio de nivel superior.  

 Si se habilita la programación, es posible configurar una programación de sincronización periódica simple o personalizada. Cuando se configura una programación simple, la hora de inicio se basa en la hora local del equipo que ejecuta la consola de Configuration Manager en el momento de crear la programación. Cuando se configura la hora de inicio de una programación personalizada, esta se basa en la hora local del equipo que ejecuta la consola de Configuration Manager.  

> [!TIP]  
>  Programe la sincronización de las actualizaciones de software para que se ejecuten en un intervalo de tiempo adecuado para su entorno. Un escenario típico es configurar la programación de sincronización de actualizaciones de software para que se ejecute poco tiempo después del lanzamiento de las actualizaciones de seguridad periódicas de Microsoft los segundos martes de cada mes, lo que normalmente se conoce como "Patch Tuesday". Otro escenario típico es configurar la programación de sincronización de actualizaciones de software para que se ejecuten diariamente cuando se usen actualizaciones de software para suministrar actualizaciones de motor y de definiciones de Endpoint Protection.  

> [!NOTE]  
>  Cuando elija no habilitar la sincronización de actualizaciones de software en una programación, podrá sincronizar manualmente las actualizaciones de software desde el nodo **Todas las actualizaciones de software** o **Grupos de actualizaciones de software** del área de trabajo Biblioteca de software. Para obtener más información, consulte [Synchronize software updates (Sincronizar actualizaciones de software)](synchronize-software-updates.md).  

## <a name="supersedence-rules"></a>Reglas de sustitución  
 Configure los parámetros de sustitución en la página **Reglas de sustitución** del asistente o en la pestaña **Reglas de sustitución** , en Propiedades de componente de punto de actualización de software. Las reglas de sustitución solo se pueden configurar en el sitio de nivel superior. A partir de la versión 1810 de Configuration Manager, puede especificar el comportamiento de reglas de sustitución para las **actualizaciones de características** por separado de las **actualizaciones que no son de características**. <!--3098809, 2977644-->

 En esta página, es posible especificar que las actualizaciones de software sustituidas expiran inmediatamente, lo que evita que se incluyan en nuevas implementaciones, además de marcar a las implementaciones existentes para que indiquen que las actualizaciones de software sustituidas contienen una o más actualizaciones de software expiradas. Igualmente, es posible especificar un período de tiempo antes de que las actualizaciones de software sustituidas expiren, lo que le permite continuar con las implementaciones. Para obtener más información, consulte [Reglas de sustitución](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  La página **Reglas de sustitución** del asistente solo está disponible cuando se configura el primer punto de actualización de software en el sitio. Esta página no se muestra cuando se instalan puntos de actualización de software adicionales.  

## <a name="classifications"></a>Clasificaciones  
 Configure los parámetros de clasificación en la página **Clasificaciones** del asistente o en la pestaña **Clasificaciones**, en Propiedades de componente de punto de actualización de software. Para obtener más información sobre las clasificaciones de actualizaciones de software, consulte [Actualizar clasificaciones](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  La página **Clasificaciones** del asistente solo está disponible cuando se configura el primer punto de actualización de software en el sitio. Esta página no se muestra cuando se instalan puntos de actualización de software adicionales.  

> [!TIP]  
>  Cuando instale por primera vez el punto de actualización de software en el sitio de nivel superior, desactive todas las clasificaciones de actualizaciones de software. Una vez realizada la sincronización de actualizaciones de software inicial, configure las clasificaciones a partir de una lista actualizada y, a continuación, vuelva a iniciar la sincronización. Esta opción solo se configura en el punto de actualización de software del sitio de nivel superior.  

## <a name="products"></a>Productos  
 Configure los parámetros de producto en la página **Productos** del asistente o en la pestaña **Productos**, en Propiedades de componente de punto de actualización de software.  

> [!NOTE]  
>  La página **Productos** del asistente solo está disponible cuando se configura el primer punto de actualización de software en el sitio. Esta página no se muestra cuando se instalan puntos de actualización de software adicionales.  

> [!TIP]  
>  Cuando instale por primera vez el punto de actualización de software en el sitio de nivel superior, desactive todos los productos. Una vez realizada la sincronización de actualizaciones de software inicial, configure los productos a partir de una lista actualizada y, a continuación, vuelva a iniciar la sincronización. Esta opción solo se configura en el punto de actualización de software del sitio de nivel superior.  

## <a name="languages"></a>Idiomas  
 Configure los parámetros de idioma en la página **Idiomas** del asistente o en la pestaña **Idiomas**, en Propiedades de componente de punto de actualización de software. Especifique los idiomas para los que desea sincronizar archivos de actualización de software y detalles de resumen. La opción **Archivo de actualización de software** se configura en cada punto de actualización de software de la jerarquía de Configuration Manager. Los parámetros de **Resumen de detalles** se configuran solo en el punto de actualización de software de nivel superior. Para obtener más información, consulte [Idiomas](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  La página **Idiomas** del asistente solo está disponible cuando se instala el punto de actualización de software en el sitio de administración central. Es posible configurar los idiomas del archivo de actualización de software en los sitios secundarios de la pestaña **Idiomas** , en Propiedades de componente de punto de actualización de software.  

## <a name="third-party-updates"></a>Actualizaciones de terceros
A partir de Configuration Manager versión 1802, puede habilitar las actualizaciones de terceros para los clientes de Configuration Manager. Cuando usa la opción Habilitar actualizaciones de software de terceros en las propiedades de componente de SUP, este descargará el certificado de firma usado por WSUS para las actualizaciones de terceros. Esta opción no está disponible durante la instalación del punto de actualización de software y debe configurarse una vez instalado el SUP. Para habilitar la configuración de cliente para las actualizaciones de terceros, vea el artículo [Acerca de la configuración de cliente en System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates).

## <a name="next-steps"></a>Pasos siguientes
Ha instalado el punto de actualización de software comenzando por el sitio de nivel superior de la jerarquía de Configuration Manager. Repita los procedimientos de este artículo para instalar el punto de actualización de software en los sitios secundarios.

Una vez que tenga los puntos de actualización de software instalados, vaya a [Synchronize software updates (Sincronizar actualizaciones de software)](synchronize-software-updates.md).
