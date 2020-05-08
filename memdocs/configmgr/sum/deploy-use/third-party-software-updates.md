---
title: Habilitar actualizaciones de terceros
titleSuffix: Configuration Manager
description: Habilite actualizaciones de terceros en Configuration Manager
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5461f888bfa2b749061eef4000f0d7c5f756b84
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906743"
---
# <a name="enable-third-party-updates"></a>Habilitar actualizaciones de terceros 

*Se aplica a: Configuration Manager (rama actual)*

A partir de la versión 1806, el nodo **Catálogos de actualizaciones de software de terceros** de la consola de Configuration Manager permite suscribirse a catálogos de terceros, publicar sus actualizaciones en el punto de actualización de software (SUP) e implementarlas posteriormente en los clientes.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> Configuration Manager no habilita esta característica de forma predeterminada. Antes de usarlo, habilite la característica opcional **Habilitar la compatibilidad con la actualización de terceros en los clientes**. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../core/servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="prerequisites"></a>Requisitos previos 
- Espacio en disco suficiente en la carpeta WSUSContent del punto de actualización de software de nivel superior para almacenar el contenido binario de origen de las actualizaciones de software de terceros.
    - La cantidad de almacenamiento necesaria varía según el proveedor, los tipos de actualizaciones y las actualizaciones específicas que se publican para la implementación.
    - Si necesita mover la carpeta WSUSContent a otra unidad con más espacio disponible, vea la entrada de blog sobre [cómo cambiar la ubicación donde WSUS almacena las actualizaciones localmente](https://docs.microsoft.com/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally).
- El servicio de sincronización de actualizaciones de software de terceros necesita acceso a Internet.
    - Para la lista de catálogos de asociados se necesita download.microsoft.com a través del puerto HTTPS 443. 
    -  Acceso de Internet a los catálogos de terceros y los archivos de contenido de actualización. Pueden ser necesarios puertos distintos al 443.
    - Las actualizaciones de terceros usan la misma configuración de proxy que el SUP.


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Requisitos adicionales cuando el SUP es remoto con respecto al servidor de sitio de nivel superior 

1. SSL debe estar habilitado en el SUP cuando es remoto. Para ello hace falta un certificado de autenticación de servidor generado a partir de una entidad emisora de certificados interna o a través de un proveedor público.
    - [Configurar SSL en WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - Al configurar SSL en WSUS, tenga en cuenta que algunos de los servicios web y los directorios virtuales siempre son HTTP y no HTTPS. 
        - Configuration Manager descarga el contenido de terceros de los paquetes de actualización de software desde el directorio de contenido de WSUS a través de HTTP.   
    - [Configurar SSL en el SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Cuando se establece la configuración de los certificados de firma de WSUS de actualizaciones de terceros en **Configuration Manager manages the certificate** (Configuration Manager administra el certificado) en las propiedades de componentes del punto de actualización de software, es necesario realizar estas configuraciones para permitir crear el certificado de firma de WSUS autofirmado: 
   - El Registro remoto debe habilitarse en el servidor del SUP.
   -  La **cuenta de conexión del servidor de WSUS** debe tener permisos de Registro remoto en el servidor de WSUS o SUP. 


3. Cree la siguiente clave del Registro en el servidor de sitio de Configuration Manager: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, cree un nuevo DWORD denominado **EnableSelfSignedCertificates** con un valor de `1`. 

4. Para permitir la instalación del certificado de firma de WSUS autofirmado en los almacenes Editores de confianza y Raíz de confianza del servidor de SUP remoto:
   - La **cuenta de conexión del servidor de WSUS** debe tener permisos de administración remota en el servidor de SUP.

     Si este requisito no es posible, exporte el certificado del almacén de WSUS del equipo local a los almacenes Editores de confianza y Raíz de confianza. 

> [!NOTE] 
>La **cuenta de conexión del servidor de WSUS** puede identificarse en la pestaña **Configuración de cuenta y proxy** de las propiedades del rol Sistema de sitio del SUP. Si no se especifica una cuenta, se usa la cuenta de equipo del servidor de sitio.

## <a name="enable-third-party-updates-on-the-sup"></a>Habilitar actualizaciones de terceros en el SUP
Si habilita esta opción, puede suscribirse a los catálogos de actualizaciones de terceros en la consola de Configuration Manager. Luego puede publicar esas actualizaciones en WSUS e implementarlas en clientes. Los pasos siguientes deben ejecutarse una vez por cada jerarquía para habilitar y configurar la característica. Si alguna vez reemplaza el servidor de WSUS del SUP de nivel superior, es posible que tenga que volver a ejecutar los pasos. 

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione el nodo **Sitios**.
2. Seleccione el sitio de nivel superior en la jerarquía. En la cinta, haga clic en **Configurar componentes de sitio** y seleccione **Punto de actualización de software**.
3. Cambie a la pestaña **Actualizaciones de terceros**. Seleccione la opción **Habilitar actualizaciones de software de terceros**.

    ![Captura de pantalla de propiedades del SUP de actualizaciones de terceros](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Configurar el certificado de firma de WSUS
Tiene que decidir si quiere que Configuration Manager administre automáticamente el certificado de firma de WSUS de terceros mediante un certificado autofirmado o si tiene que hacerlo manualmente. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Administrar automáticamente el certificado de firma de WSUS
Si no existe ningún requisito que le obligue a usar certificados PKI, puede administrar automáticamente los certificados de firma de las actualizaciones de terceros. La administración de certificados de WSUS se realiza como parte del ciclo de sincronización y se registra en `wsyncmgr.log`. 

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione el nodo **Sitios**.
2. Seleccione el sitio de nivel superior en la jerarquía. En la cinta, haga clic en **Configurar componentes de sitio** y seleccione **Punto de actualización de software**.
3. Cambie a la pestaña **Actualizaciones de terceros**. Seleccione la opción **Configuration Manager administra el certificado**. 
4. Se crea un nuevo certificado de tipo **Firma de WSUS de terceros** en el nodo **Certificados**, en la sección **Seguridad** del área de trabajo **Administración**.  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Administrar manualmente el certificado de firma de WSUS
Si tiene que configurar manualmente el certificado, por ejemplo, porque necesita usar un certificado PKI, debe usar [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) u otra herramienta para ello.  

1. Configure el certificado de firma mediante [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione el nodo **Sitios**.
3. Seleccione el sitio de nivel superior en la jerarquía. En la cinta, haga clic en **Configurar componentes de sitio** y seleccione **Punto de actualización de software**.
4. Cambie a la pestaña **Actualizaciones de terceros**. Seleccione la opción **Administrar manualmente el certificado**.


## <a name="enable-third-party-updates-on-the-clients"></a>Habilitar actualizaciones de terceros en los clientes
Habilite las actualizaciones de terceros en los clientes en la configuración de cliente. El valor establece la directiva del agente de Windows Update para [Permitir actualizaciones firmadas procedentes de una ubicación del servicio Microsoft Update en la intranet](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location). Este valor de cliente además instala el certificado de firma de WSUS en el almacén Editores de confianza del cliente. El registro de administración de certificados se ve en `updatesdeployment.log` en los clientes.  Ejecute estos pasos para cada valor de cliente personalizado que quiera usar para las actualizaciones de terceros. Para obtener más información, vea el artículo [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates).

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Configuración de cliente**.
2. Seleccione un valor de cliente personalizado existente o cree uno nuevo. 
3. Seleccione la pestaña **Actualizaciones de software** en el lado izquierdo. Si no tiene esta pestaña, asegúrese de que la casilla **Actualizaciones de software** esté activada.
4. Establezca **Habilitar actualizaciones de software de terceros** en **Sí**. 


## <a name="add-a-custom-catalog"></a>Agregar un catálogo personalizado
Los *catálogos de asociados* son catálogos de proveedores de software que tienen su información ya registrada en Microsoft. Puede suscribirse a los catálogos de asociados sin necesidad de especificar información adicional. Los catálogos que agrega se denominan *catálogos personalizados*. Puede agregar un catálogo personalizado de un proveedor de actualizaciones ajeno a Configuration Manager. Los catálogos personalizados deben usar https y las actualizaciones deben estar firmadas digitalmente. 

1. Vaya al área de trabajo **Biblioteca de actualizaciones de software**, expanda **Actualizaciones de software** y seleccione el nodo **Catálogos de actualizaciones de software de terceros**. 
   
     ![Captura de pantalla del nodo de actualizaciones de terceros](media/third-party-updates-node.PNG)
2. Haga clic en **Agregar catálogo personalizado** en la cinta de opciones. 

     ![Agregar catálogo personalizado de actualizaciones de terceros](media/third-party-updates-custom-catalog.png)
1. En la página **General**, especifique lo siguiente: 
    - **Dirección URL de descarga**: una dirección HTTPS válida del catálogo personalizado.
    - **Publicador**: el nombre de la organización que publica el catálogo. 
    - **Nombre**: nombre del catálogo que se va a mostrar en la consola de Configuration Manager. 
    - **Descripción**: una descripción del catálogo. 
    - **Dirección URL de soporte técnico** (opcional): dirección HTTPS válida de un sitio web para obtener ayuda sobre el catálogo. 
    - **Contacto de soporte técnico** (opcional): información de contacto para obtener ayuda sobre el catálogo. 
2. Haga clic en **Siguiente** para revisar el resumen del catálogo y continuar con el **asistente para catálogos personalizados de actualizaciones de software de terceros** hasta su finalización.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Suscribirse a un catálogo de terceros y sincronizar las actualizaciones
Cuando se suscribe a un catálogo de terceros en la consola de Configuration Manager, se sincronizan los metadatos de todas las actualizaciones del catálogo en los servidores de WSUS del SUP. La sincronización de los metadatos permite a los clientes determinar si alguna de las actualizaciones es aplicable. Realice los pasos siguientes para cada catálogo de terceros al que quiera suscribirse:  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Actualizaciones de software** y seleccione el nodo **Catálogos de actualizaciones de software de terceros**.  
2. Seleccione el catálogo al que quiere suscribirse y haga clic en **Suscribirse al catálogo** en la cinta de opciones. 
    ![Agregar catálogo personalizado de actualizaciones de terceros](media/third-party-updates-subscribe.png)
3. Revise y apruebe el certificado de catálogo.  
   > [!NOTE]
   > 
   > Cuando se suscribe a un catálogo de actualizaciones de software de terceros, el certificado que revisa y aprueba en el asistente se agrega al sitio. Este certificado es de tipo **Catálogo de actualizaciones de software de terceros**. Se puede administrar desde el nodo **Certificados** de la sección **Seguridad** en el área de trabajo de **Administración**.  
4. Complete el asistente. Después de la suscripción inicial, el catálogo debería empezar a descargarse en cuestión de minutos. 
    - El catálogo se sincroniza automáticamente cada siete días.
    - Haga clic en **Sincronizar ahora** en la cinta de opciones para forzar una sincronización.
5. Una vez descargado el catálogo, los metadatos del producto deben sincronizarse entre la base de datos de WSUS y la base de datos de Configuration Manager. [Inicie manualmente la sincronización de actualizaciones de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para sincronizar la información del producto.
6. Una vez sincronizada la información del producto, [configure el SUP para sincronizar el producto deseado](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) en Configuration Manager.  
7. [Inicie manualmente la sincronización de actualizaciones de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para sincronizar las actualizaciones del nuevo producto en Configuration Manager.  
8. Cuando la sincronización termina, se pueden ver las actualizaciones de terceros en el nodo **Todas las actualizaciones**. Estas actualizaciones se publican como actualizaciones de **solo metadatos** hasta que se decide publicarlas. 
     - El icono de la flecha azul representa una actualización de software de solo metadatos. ![Icono de actualización de software de solo metadatos](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Publicar e implementar actualizaciones de software de terceros 
Una vez que las actualizaciones de terceros están en el nodo **Todas las actualizaciones**, puede elegir qué actualizaciones se deben publicar para su implementación. Cuando se publica una actualización, los archivos binarios se descargan del proveedor y se colocan en el directorio WSUSContent del SUP de nivel superior. 

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Actualizaciones de software** y seleccione el nodo **Todas las actualizaciones de software**.
2. Haga clic en **Agregar criterios** para filtrar la lista de actualizaciones. Por ejemplo, agregue **Proveedor** en **HP** para ver todas las actualizaciones de HP.  
3. Seleccione las actualizaciones requeridas por la organización. Haga clic en **Publicar el contenido de la actualización de software de terceros**.
    - Esta acción descarga los archivos binarios de actualización del proveedor y los almacena en la carpeta WSUSContent del punto de actualización de software de nivel superior. 
4. [Inicie manualmente la sincronización de actualizaciones de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para cambiar el estado de las actualizaciones publicadas de solo metadatos a actualizaciones implementables con contenido. 
    >[!NOTE]
    >Al publicar contenido de la actualización de software de terceros, los certificados usados para firmar el contenido se agregan al sitio. Estos certificados son de tipo **Contenido de actualizaciones de software de terceros**. Se pueden administrar desde el nodo **Certificados** de la sección **Seguridad** en el área de trabajo de **Administración**.  

5. Revise el progreso en SMS_ISVUPDATES_SYNCAGENT.log. El registro se encuentra en el punto de actualización de software de nivel superior de la carpeta Logs del sistema de sitio.
6. Implemente las actualizaciones con el proceso [Administrar actualizaciones de software](../deploy-use/deploy-software-updates.md). 
7. En la página **Ubicaciones de descarga** del **Asistente para implementar actualizaciones de software**, seleccione la opción predeterminada para **Descargar actualizaciones de software de Internet**. En este escenario, el contenido ya está publicado en el punto de actualización de software, que se utiliza para descargar el contenido del paquete de implementación.
8. Los clientes tienen que ejecutar un análisis y evaluar las actualizaciones para ver los resultados de cumplimiento.  Para desencadenar manualmente este ciclo desde el panel de control de Configuration Manager en un cliente mediante, ejecute la acción **Ciclo de detecciones de actualizaciones de software**.


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a> Mejoras de las actualizaciones de terceros a partir de 1910
<!--4469002-->
Ahora, existen controles más granulares sobre la sincronización de catálogos de actualizaciones de terceros. A partir de la versión 1910 de Configuration Manager, puede configurar la programación de sincronización de cada catálogo de manera independiente. Al usar catálogos que incluyen actualizaciones clasificadas, puede configurar la sincronización de forma que incluya solo determinadas categorías de actualizaciones y, así, evitar la sincronización de todo el catálogo. Con los catálogos clasificados, cuando esté seguro de implementar una categoría, puede configurarla para que se descargue y publique automáticamente en WSUS.

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>Establecer la programación para un catálogo en una nueva suscripción de catálogo

1. Vaya al área de trabajo **Biblioteca de software**, expanda **Actualizaciones de software** y seleccione el nodo **Catálogos de actualizaciones de software de terceros**.
1. Seleccione el catálogo al que quiere suscribirse y haga clic en **Suscribirse al catálogo** en la cinta de opciones.
1. Elija sus opciones en la página **Programación** si desea invalidar la programación de sincronización predeterminada:
   - **Programación sencilla**:  elija el intervalo de horas, días o meses.
   - **Programación personalizada**: establezca una programación compleja.

### <a name="update-the-schedule-per-catalog"></a>Actualizar la programación por catálogo

1. Vaya al área de trabajo **Biblioteca de software**, expanda **Actualizaciones de software** y seleccione el nodo **Catálogos de actualizaciones de software de terceros**.
1. Haga clic con el botón derecho en el catálogo y seleccione **Propiedades**.
1. Elija sus opciones en la pestaña Programación: 
   - **Programación sencilla**:  elija el intervalo de horas, días o meses.
   - **Programación personalizada**: establezca una programación compleja.

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>Nueva suscripción a un catálogo de terceros v3

> [!IMPORTANT]
> Esta opción solo está disponible para los catálogos de actualizaciones de terceros v3, que admiten categorías de actualizaciones. Estas opciones están deshabilitadas para los catálogos que no se han publicado en el nuevo formato v3.


1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Actualizaciones de software** y seleccione el nodo **Catálogos de actualizaciones de software de terceros**.
1. Seleccione el catálogo al que quiere suscribirse y haga clic en **Suscribirse al catálogo** en la cinta de opciones.
1. Elija las opciones en la página **Seleccionar categorías**:

   - **Sincronizar todas las categorías de actualización** (valor predeterminado)
       - Sincroniza todas las actualizaciones del catálogo de actualizaciones de terceros en Configuration Manager.
   -  **Seleccionar categorías para la sincronización**
       - Elija qué categorías y categorías secundarias se van a sincronizar en Configuration Manager.

      ![Selección de las categorías de actualización para sincronizar en Configuration Manager](./media/4469002-select-categories-for-sync.png)
1. Elija si quiere **almacenar provisionalmente el contenido de actualización** para el catálogo. Al almacenar provisionalmente el contenido, todas las actualizaciones de las categorías seleccionadas se descargan de forma automática al punto de actualización de software de nivel superior, lo que significa que no es necesario asegurarse de que ya se hayan descargado antes de la implementación. Solo debería almacenar provisionalmente de forma automática el contenido para las actualizaciones que es probable que implemente, con el fin de evitar requisitos excesivo de ancho de banda y almacenamiento.

   - **No almacenar provisionalmente el contenido, sincronizar solo para examinar (recomendado)**
     - No descargar contenido para actualizaciones en el catálogo de aplicaciones de terceros
   - **Almacenar provisionalmente de forma automática el contenido de las categorías seleccionadas**
     - Elija las categorías de actualización que descargarán el contenido de forma automática.
     - El contenido de las actualizaciones de las categorías seleccionadas se descargará en el directorio de contenido de WSUS del punto de actualización de software de nivel superior.
      ![Selección de categorías de actualización para almacenar contenido](./media/4469002-stage-content.png)
1. Establezca su **Programación** para la sincronización de catálogos y, después, complete el asistente.

 

### <a name="edit-an-existing-subscription"></a>Edición de una suscripción existente

> [!IMPORTANT]
> Esta opción solo está disponible para los catálogos de actualizaciones de terceros v3, que admiten categorías de actualizaciones. Estas opciones están deshabilitadas para los catálogos que no se han publicado en el nuevo formato v3.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**. Expanda **Actualizaciones de software** y seleccione el nodo **Catálogos de actualizaciones de software de terceros**.
1. Haga clic con el botón derecho en el catálogo y seleccione **Propiedades**.
1. Elija las opciones en la pestaña **Seleccionar categorías**.
   - **Sincronizar todas las categorías de actualización** (valor predeterminado)
       - Sincroniza todas las actualizaciones del catálogo de actualizaciones de terceros en Configuration Manager.
   -  **Seleccionar categorías para la sincronización**
       - Elija qué categorías y categorías secundarias se van a sincronizar en Configuration Manager.
1. Elija las opciones en la pestaña **Stage update content** (Almacenar provisionalmente el contenido de actualización).
   - **No almacenar provisionalmente el contenido, sincronizar solo para examinar (recomendado)**
     - No descargar contenido para actualizaciones en el catálogo de aplicaciones de terceros
   - **Almacenar provisionalmente de forma automática el contenido de las categorías seleccionadas**
     - Elija las categorías de actualización que descargarán el contenido de forma automática.
     - El contenido de las actualizaciones de las categorías seleccionadas se descargará en el directorio de contenido de WSUS del punto de actualización de software de nivel superior. 

## <a name="monitoring-progress-of-third-party-software-updates"></a>Supervisión del progreso de las actualizaciones de software de terceros 

La sincronización de actualizaciones de software de terceros se controla mediante el componente SMS_ISVUPDATES_SYNCAGENT en el punto de actualización de software de nivel superior. Puede ver los mensajes de estado de este componente, o ver un estado más detallado en SMS_ISVUPDATES_SYNCAGENT.log. Este registro está en el punto de actualización de software de nivel superior de la carpeta Logs del sistema de sitio. De forma predeterminada, esta ruta de acceso es C:\Archivos de programa\Microsoft Configuration Manager\Logs. Para obtener más información sobre la supervisión del proceso general de administración de actualizaciones de software, vea [Supervisar actualizaciones de software](../deploy-use/monitor-software-updates.md) 

## <a name="known-issues"></a>Problemas conocidos

- El equipo donde se ejecuta la consola se usa para descargar las actualizaciones desde WSUS y agregarlas al paquete de actualizaciones. El certificado de firma de WSUS debe ser de confianza en el equipo de la consola. Si no lo es, pueden producirse problemas con la comprobación de firma durante la descarga de actualizaciones de terceros. 
- El servicio de sincronización de actualización de software de terceros no puede publicar contenido en las actualizaciones de solo metadatos que otra aplicación, herramienta o script —como SCUP— haya agregado a WSUS. La acción **Publicar el contenido de la actualización de software de terceros** genera un error en estas actualizaciones. Si necesita implementar actualizaciones de terceros aún no admitidas por esta característica, use en su totalidad el proceso existente para implementar esas actualizaciones.  
-  Configuration Manager tiene una nueva versión del formato de archivo cab de catálogo. La nueva versión incluye los certificados para los archivos binarios del proveedor. Estos certificados se agregan al nodo **Certificados** de la sección **Seguridad** del área de trabajo **Administración** una vez que se aprueba el catálogo y se considera de confianza.  
     - Puede seguir usando la versión anterior del archivo cab de catálogo siempre que la dirección URL de descarga sea https y las actualizaciones estén firmadas. El contenido no se publicará porque los certificados para los archivos binarios no están en el archivo cab ni se han aprobado aún. Puede solucionar este problema si busca el certificado en el nodo **Certificados**, lo desbloquea y luego vuelve a publicar la actualización. Si va a publicar varias actualizaciones firmadas con diferentes certificados, tiene que desbloquear cada certificado que se use.
     - Para obtener más información, vea los mensajes de estado 11523 y 11524 de la siguiente tabla de mensajes de estado.
-  Cuando el servicio de sincronización de actualizaciones de software de terceros en el punto de actualización de software de nivel superior requiera un servidor proxy para el acceso a Internet, las comprobaciones de firmas digitales podrían dar error. Para solucionar este problema, configure los ajustes del proxy WinHTTP en el sistema de sitio. Para obtener más información, consulte [Netsh commands for WinHTTP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731131(v=ws.10)) (Comandos Netsh para WinHTTP).
- Cuando se usa CMG para el almacenamiento de contenido, el contenido de las actualizaciones de terceros no se descarga en los clientes si está habilitada la [opción de cliente](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Descarga de contenido diferencial cuando esté disponible**. <!--6598587-->

## <a name="status-messages"></a>Mensajes de estado

| MessageID       | Gravedad           | Descripción | Causa posible| Solución posible
| ------------- |-------------| -----|----|----|
| 11516     | Error |No se ha publicado el contenido de la actualización "id. de actualización" porque está sin firmar.  Solo se puede publicar contenido con firmas válidas.  |Configuration Manager no permite publicar actualizaciones sin firmar.| Publique la actualización de alguna otra forma. </br></br>Vea si hay alguna actualización firmada disponible del proveedor.|
| 11523  | Advertencia |  El catálogo "X" no incluye certificados de firma de contenido; los intentos de publicar contenido de actualización para las actualizaciones de este catálogo pueden ser infructuosos hasta que se agreguen y se aprueben certificados de firma de contenido. | Este mensaje puede producirse cuando se importa un catálogo que está usando una versión anterior del formato de archivo cab.|Póngase en contacto con el proveedor del catálogo para obtener un catálogo actualizado que incluya los certificados de firma del contenido. </br> </br> Los certificados para los archivos binarios no están en el archivo cab, así que el contenido no se publica. Puede solucionar este problema si busca el certificado en el nodo **Certificados**, lo desbloquea y luego vuelve a publicar la actualización. Si va a publicar varias actualizaciones firmadas con diferentes certificados, tiene que desbloquear cada certificado que se use.|
| 11524| Error  | No se ha podido publicar la actualización "id." debido a que faltan metadatos de actualización. | Es posible que la actualización se haya sincronizado con WSUS fuera de Configuration Manager.| Sincronice la actualización con Configuration Manager antes de intentar publicar su contenido.  </br> </br>Si se ha usado una herramienta externa para publicar la actualización como de **solo metadatos**, emplee la misma herramienta para publicar el contenido de actualización.|



## <a name="working-with-third-party-updates-video"></a>Vídeo Trabajar con actualizaciones de terceros
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Paso siguiente
> [!div class="nextstepaction"]
> [Implementar actualizaciones de software](./deploy-software-updates.md)
