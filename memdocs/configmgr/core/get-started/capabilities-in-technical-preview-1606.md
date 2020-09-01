---
title: Funcionalidades de Technical Preview 1606
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1606.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 9278e6cb148768e993706fe112bbfd70121cc6b9
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995473"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Funciones de Technical Preview 1606 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1606 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager.      Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    

**Problemas conocidos de esta Technical Preview:**  
*  Cuando se actualiza de Technical Preview 1604 a 1605 y luego a la versión 1606, podría producirse un error en la actualización y se registraría un error similar al siguiente en **cmupdate.log**:

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    Si ocurre esto, en el nodo **Actualizaciones y mantenimiento**, haga clic en **Buscar actualizaciones** y luego **vuelva a intentar** la instalación de la actualización.
    ***

**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a> Clasificar automáticamente dispositivos en recopilaciones
Puede crear categorías de dispositivos, que se pueden usar para colocar automáticamente los dispositivos en colecciones de dispositivos cuando se usa Configuration Manager con Microsoft Intune. Después, cuando los usuarios inscriben un dispositivo en Intune, tienen que elegir una categoría de dispositivos. Además, puede cambiar la categoría de un dispositivo desde la consola de Configuration Manager.

**Importante:** Esta capacidad funciona con la versión de **junio de 2016** de Microsoft Intune. Asegúrese de haber actualizado a esta versión antes de probar estos procedimientos.

### <a name="try-it-out"></a>Haga la prueba

### <a name="create-a-set-of-device-categories"></a>Crear un conjunto de categorías de dispositivos
1.  En el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, expanda **Información general** y haga clic en **Colecciones de dispositivos**.
2.  En la pestaña **Inicio**, en el grupo **Categorías**, haga clic en **Administrar categorías de dispositivos**.
3.  En el cuadro de diálogo **Administrar categorías de dispositivos**, puede crear, editar o quitar categorías. Intente crear una nueva categoría.

### <a name="associate-a-collection-with-a-device-category"></a>Asociar una colección a una categoría de dispositivos
Cuando asocia una colección a una categoría de dispositivos, todos los dispositivos de la categoría que especifique se agregan a esa colección.
1.  En el cuadro de diálogo **Propiedades** de una colección de dispositivos, haga clic en **Agregar regla** > **Regla de categoría de dispositivos**.
2.  En el cuadro de diálogo **Crear regla de pertenencia de categoría de dispositivos**, seleccione la categoría que se vaya a aplicar a todos los dispositivos de la colección.
3.  Cierre el cuadro de diálogo **Crear regla de pertenencia de categoría de dispositivos** y el cuadro de diálogo de propiedades de la colección.

### <a name="change-the-category-of-a-device"></a>Cambiar la categoría de un dispositivo
1.  En el área de trabajo **Activos y compatibilidad** de la consola de Configuration Manager, expanda **Información general** y haga clic en **Dispositivos**.
2.  Seleccione un dispositivo de la lista **Dispositivos** y, luego, en la pestaña **Inicio**, en el grupo **Dispositivo**, haga clic en **Cambiar categoría**.
3.  En el cuadro de diálogo **Editar categoría de dispositivos**, elija la categoría que se va a aplicar a este dispositivo y haga clic en **Aceptar**.

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a> Período de gracia de cumplimiento para implementaciones de actualizaciones de software y aplicaciones requeridas

En algunos casos, es posible que quiera dar más tiempo a los usuarios para instalar las implementaciones de aplicaciones o las actualizaciones de software necesarias más allá de los plazos que estableció. Normalmente esto es necesario cuando un equipo ha estado apagado durante un largo período de tiempo y tiene que instalar muchas implementaciones de aplicaciones o actualizaciones.
Por ejemplo, si un usuario final acaba de volver de vacaciones, es posible que tenga que esperar bastante mientras se instalan las implementaciones de aplicaciones vencidas.
Para solucionar este problema, puede definir un período de gracia de cumplimiento mediante la implementación de la configuración de cliente de Configuration Manager en una colección.

### <a name="try-it-out"></a>Haga la prueba

Para configurar el período de gracia, haga lo siguiente:

1.  En la página **Agente de equipo** de la configuración de cliente, configure la nueva propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** con un valor entre **1** y **120** horas.
2.  En una nueva implementación de aplicación obligatoria o en las propiedades de una implementación existente, en la página **Programación**, active la casilla de verificación **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario** hasta el período de gracia definido en la configuración del cliente.
Todas las implementaciones que tienen activada esta casilla y que están destinadas a dispositivos en los que también se ha implementado la configuración de cliente usarán el período de gracia de cumplimiento.

Si configura un período de gracia de cumplimiento y activa la casilla de verificación, una vez que se llegue a la fecha límite de instalación de la aplicación, esta se instalará en la primera ventana que no sea de empresa configurada por el usuario hasta ese período de gracia. No obstante, el usuario puede abrir el Centro de software e instalar la aplicación en cualquier momento que quiera. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas.
Se han agregado opciones similares al asistente para la implementación de actualizaciones de software, al asistente para reglas de implementación automática y a las páginas de propiedades.

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a> Uso de Configuration Manager como un instalador administrado con protección de dispositivos

Device Guard es una característica de Windows 10 que emplea características de hardware y software para controlar de forma estricta lo que se puede ejecutar en el dispositivo.

Para obtener más información, consulte [Introducción a Device Guard](/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control).

En esta versión, Configuration Manager puede interoperar con Device Guard y [Windows AppLocker](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd723678(v=ws.10)) para que los archivos ejecutables y DLL implementados con Configuration Manager se consideren de confianza automáticamente por proceder de un instalador administrado, lo que significa que se podrán ejecutar en el dispositivo de destino y no se permitirá ejecutar otro software a menos que se permita explícitamente mediante otras reglas de AppLocker.  

De momento, esta capacidad no se puede configurar desde la consola de Configuration Manager. La configuración de la directiva exige configurar una clave del Registro en cada cliente y configurar servicios de Windows en el cliente.
Una vez hecho esto, configure el archivo de directiva de AppLocker. Después de configurar el archivo de directiva, puede implementarlo en cualquier dispositivo de cliente compatible.


Como todas las directivas de AppLocker, las directivas con reglas de instalador administrado se pueden ejecutar de dos maneras:

- Modo auditoría: no se evita que las aplicaciones se ejecuten, pero todas aquellas que se hubieran bloqueado se notifican en un archivo de registro (esto se admitirá en una versión posterior de Configuration Manager).
- Cumplimiento habilitado: se evita que las aplicaciones se ejecuten.

Vea los siguientes artículos para más información:

- [Introducción a Device Guard](/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control)

- [Planificación e introducción al proceso de implementación de controles de aplicaciones de Windows Defender](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a> Varios puntos de administración de dispositivos para la administración local de dispositivos móviles  
  Con Technical Preview 1606, la administración local de dispositivos móviles (MDM) admite una nueva capacidad de Windows 10 Anniversary Update que automáticamente configura un dispositivo inscrito para que tenga más de un punto de administración de dispositivos disponible. Esta capacidad permite al dispositivo retroceder a otro punto de administración de dispositivos cuando el que usa normalmente no está disponible. Esta capacidad solo funciona con equipos que tienen instalado Windows 10 Anniversary Update.  

### <a name="try-it-out"></a>Haga la prueba  

1.  Instale más de un punto de administración de dispositivos en la jerarquía.  

2.  Inscriba un dispositivo de Windows 10 Anniversary Update para la administración local de dispositivos móviles.  

Para más información sobre cómo preparar el sitio e inscribir dispositivos para la administración local de dispositivos móviles, vea [Administrar dispositivos móviles con la infraestructura local en Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a> Servicio de proxy en la nube para administrar clientes en Internet

El servicio de proxy en la nube ofrece una manera sencilla de administrar clientes de Configuration Manager en Internet. El servicio, que se implementa en Microsoft Azure y exige una suscripción de Azure, se conecta a la infraestructura local de Configuration Manager con un nuevo rol denominado punto de conexión del proxy en la nube. Una vez implementado y configurado por completo, los clientes podrán acceder a los roles de sistema de sitio locales de Configuration Manager independientemente de si están conectados a la red interna privada o a Internet.

Use la consola de Configuration Manager para implementar el servicio en Azure, agregar el rol de punto de conexión del proxy en la nube y configurar roles de sistema de sitio para permitir el tráfico del proxy en la nube. El servicio de proxy en la nube de momento solo admite los roles de punto de administración, punto de distribución y punto de actualización de software.

Se necesitan certificados de cliente y de capa de sockets seguros (SSL) para autenticar los equipos y cifrar las comunicaciones entre los diferentes niveles del servicio. Los equipos cliente normalmente reciben un certificado de cliente mediante la aplicación de directivas de grupo. Para cifrar el tráfico entre los clientes y el servidor de sistema de sitio que hospeda los roles, tiene que crear un certificado SSL personalizado de la CA. Además de estos dos tipos de certificados, también debe configurar un certificado de administración en Azure que permita a Configuration Manager implementar el servicio de proxy en la nube.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Requisitos del servicio de proxy en la nube en TP 1606
- Equipos cliente y servidor de sistema de sitio que ejecuten el punto de conexión del proxy en la nube.
- Certificados SSL personalizados de la CA interna: se usan para cifrar la comunicación de los equipos cliente y para autenticar la identidad del servicio de proxy en la nube.
- Suscripción de Azure para los servicios en la nube.
- Certificado de administración de Azure: se usa para autenticar Configuration Manager con Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Limitaciones del servicio de proxy en la nube en TP 1606

- Solo admite los roles de punto de administración, punto de distribución y punto de actualización de software.
- No se admiten directivas de usuario.
- No se puede usar con la [administración local de dispositivos móviles](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) en Configuration Manager.
- Solo se admite en la plataforma de nube pública de Azure.


### <a name="try-it-out"></a>Haga la prueba

El proceso de implementación del servicio de proxy en la nube incluye los siguientes pasos:

1. Crear y emitir un certificado SSL personalizado para el servicio de proxy en la nube.
1. Exportar la raíz del certificado de cliente.
2. Cargar el certificado de administración en Azure.
3. Configurar el servicio de proxy en la nube en la consola de Configuration Manager.
4. Configurar el sitio primario para usar autenticación de certificados de cliente.
5. Agregar el punto de conexión del proxy en la nube al sitio.
6. Configurar los roles de sistema de sitio para aceptar tráfico del proxy en la nube.

En las secciones siguientes se proporciona más información para realizar estos pasos.

#### <a name="create-a-custom-ssl-certificate"></a>Crear un certificado SSL personalizado

Puede crear un certificado SSL personalizado para el servicio de proxy en la nube de la misma manera que si fuera para un punto de distribución basado en la nube. Siga las instrucciones de [Deploying the Service Certificate for Cloud-Based Distribution Points (Implementación del certificado de servicio para puntos de distribución basados en la nube)](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012), pero con las siguientes diferencias:

* Al configurar la nueva plantilla de certificado, asigne los permisos **Leer** e **Inscribir** al grupo de seguridad que configure para los servidores de Configuration Manager.

#### <a name="export-the-client-certificates-root"></a>Exportar la raíz del certificado de cliente

La manera más sencilla de exportar la raíz de los certificados de cliente usados en la red es abrir un certificado de cliente en uno de los equipos unidos a dominio que tenga uno y copiarlo.

>[!NOTE]
>Los certificados de cliente son necesarios en cualquier equipo que quiera administrar con el servicio de proxy en la nube y en el servidor de sistema de sitio que hospeda el punto de conexión del proxy en la nube. Si necesita agregar un certificado de cliente a cualquiera de estas máquinas, vea [Deploying the Client Certificate for Windows Computers (Implementación del certificado de cliente para equipos Windows)](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).

1. En la ventana Ejecutar, escriba **mmc** y presione ENTRAR.
2. En el menú Archivo de la consola de administración, haga clic en **Agregar o quitar complemento...**
3. En el cuadro de diálogo Agregar o quitar complementos, haga clic en **Certificados**, **Agregar >** , **Cuenta de equipo**, **Siguiente**, **Equipo local** y, luego, en **Finalizar**. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.
4. Vaya a **Certificados > Personal > Certificados**.
5. Haga doble clic en el certificado para la autenticación de cliente en el equipo, haga clic en la pestaña Ruta de certificación y haga doble clic en la entidad de certificación raíz (al principio de la ruta de acceso).
6.  Haga clic en la pestaña Detalles y luego en **Copiar en archivo...**
7. Complete el Asistente para exportar certificados con el formato de certificado predeterminado. Anote el nombre y la ubicación del certificado raíz que ha creado, ya que lo necesitará para configurar el servicio de proxy en la nube en un paso posterior.

#### <a name="upload-the-management-certificate-to-azure"></a>Cargar el certificado de administración en Azure

Se necesita un certificado de administración de Azure para que Configuration Manager acceda a la API de Azure y para configurar el servicio de proxy en la nube. Para obtener más información e instrucciones sobre cómo cargar un certificado de administración, vea los artículos siguientes de la documentación de Azure:
- [Introducción a los certificados para los servicios en la nube de Azure](/azure/cloud-services/cloud-services-certs-create)
- [Carga de un certificado de administración de API de Administración de Azure](/previous-versions/azure/azure-api-management-certs).

Asegúrese de copiar el identificador de suscripción asociado al certificado de administración, dado que lo necesitará para configurar el servicio de proxy en la nube en la consola de Configuration Manager.

#### <a name="set-up-cloud-proxy-service"></a>Configurar el servicio de proxy en la nube

1. En la consola de Configuration Manager, vaya a **Administración > Servicios de nube > Servicio de proxy en la nube**.
2. Haga clic en **Crear servicio de proxy en la nube**.
3. En el Asistente para crear servicio de proxy en la nube, escriba el identificador de suscripción de Azure (copiado desde el portal de administración de Azure), haga clic en Examinar y seleccione el archivo de certificado que usó para cargarlo como un certificado de administración de Azure. Haga clic en **Siguiente**. Espere unos instantes mientras que la consola se conecta a Azure.
4. Rellene los detalles adicionales en el asistente:
    - Especifique la clave privada (archivo .pfx) que ha exportado desde el certificado SSL personalizado.
    - Especifique el certificado raíz exportado desde el certificado de cliente.
    - Especifique el mismo FQDN de servicio que usó cuando creó la nueva plantilla de certificado.
    - Desactive la casilla situada junto a **Comprobar revocación de certificado de cliente** (a menos que vaya a publicar la información de CRL públicamente).
    - Haga clic en **Siguiente** cuando haya terminado.
5. Revise la configuración y haga clic en **Siguiente**. Configuration Manager comienza a configurar el servicio. Cuando finalice el asistente, puede hacer clic en **Cerrar**, aunque llevará entre 5 y 15 minutos aprovisionar el servicio por completo en Azure. Compruebe la columna **Estado** del servicio de proxy en la nube recién configurado para determinar si está listo.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Configurar un sitio primario para la autenticación de certificados de cliente

1. En la consola de Configuration Manager, vaya a **Administración > Configuración del sitio > Sitios**.
2. Seleccione el sitio primario de los clientes que quiere administrar mediante el servicio de proxy en la nube y haga clic en **Propiedades**.
3. En la pestaña Comunicaciones de equipo cliente de la hoja de propiedades del sitio primario, active la casilla situada junto a **Usar un certificado de cliente PKI (capacidad de autenticación de cliente) cuando esté disponible**.
4. Asegúrese de desactivar la casilla situada junto a **Los clientes comprueban la lista de revocación de certificados (CRL) para sistemas de sitio**. Esta opción solo sería necesaria si fuera a publicar la CRL públicamente.
5. Haga clic en **Aceptar**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Agregar el punto de conexión del proxy en la nube

El punto de conexión del proxy en la nube es un nuevo rol de sistema de sitio para la comunicación con el servicio de proxy en la nube. Para agregar el punto de conexión del proxy en la nube, siga las instrucciones de [Agregar roles de sistema de sitio en Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Configurar roles para el tráfico del proxy en la nube

El último paso de la configuración del servicio de proxy en la nube es configurar los roles de sistema de sitio para que acepten tráfico del proxy en la nube. En Tech Preview 1606, solo son compatibles con el servicio de proxy en la nube los roles de punto de administración, punto de distribución y punto de actualización de software. Debe configurar cada rol por separado.

1. En la consola de Configuration Manager, vaya a **Administración > Configuración del sitio > Servidores y roles del sistema de sitios**.
2. Haga clic en el servidor de sistema de sitio del rol que quiere configurar para el tráfico del proxy en la nube.
3. Haga clic en el rol y luego en **Propiedades**.
4. En la hoja Propiedades del rol, en Conexiones de cliente, elija **HTTPS**, active la casilla situada junto a **Permitir el tráfico del proxy en la nube de Configuration Manager** y luego haga clic en **Aceptar**. Repita estos pasos para los roles restantes.

#### <a name="check-status-on-a-client-on-the-internet"></a>Comprobar el estado en un cliente en Internet

Una vez configurados por completo el servicio y los roles, los clientes internos obtendrán la ubicación del servicio de proxy en la nube en la siguiente solicitud de ubicación. Después, los clientes con información de ubicación actualizada pueden comunicarse con Configuration Manager en Internet. El ciclo de sondeo de las solicitudes de ubicación es cada 24 horas. Si no quiere esperar a la solicitud de ubicación normalmente programada, puede forzar la solicitud si reinicia el servicio Host de agente de SMS (ccmexec.exe) en el equipo.

Una vez que los clientes tengan la nueva información de ubicación del servicio de proxy en la nube, vuelva a comprobar el estado de los clientes que ya no estén en la red privada interna pero que tengan acceso a Internet. También puede supervisar el tráfico en el servicio de proxy en la nube si va a **Administración > Servicios de nube > Servicio de proxy en la nube**, selecciona el servicio en el panel de lista y ve la información de tráfico en el panel de detalles.   

## <a name="manage-the-microsoft-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>Administración del agente cliente de Microsoft 365 en Configuration Manager  

A partir de Technical Preview 1606, puede usar una configuración del agente cliente de Configuration Manager, en lugar de la directiva de grupo, para permitir que los clientes de Microsoft 365 reciban actualizaciones de Configuration Manager. Después de configurar esta opción e implementar las actualizaciones de Microsoft 365, el agente cliente de Configuration Manager se comunica con el agente cliente de Microsoft 365 para descargar las actualizaciones de Microsoft 365 desde un punto de distribución e instalarlas. Configuration Manager también realiza un inventario de la configuración del agente cliente.

Para obtener más información, consulte [Administración de actualizaciones de Aplicaciones de Microsoft 365 para empresas](../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Establecer la configuración del cliente de Configuration Manager para administrar el agente cliente de Office 365
1.  En la consola de Configuration Manager, haga clic en **Administración** > **Información general** > **Configuración de cliente**.
2. Abra la configuración de dispositivo adecuada para habilitar el agente cliente. Para más información sobre las configuraciones de cliente predeterminadas y personalizadas, consulte [Cómo establecer la configuración de cliente](../../core/clients/deploy/configure-client-settings.md).
3. Haga clic en **Actualizaciones de software** y seleccione **Sí** para el valor **Habilitar administración del Agente cliente de Office 365**.  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a> La variable de secuencia de tareas OSDPreserveDriveLetter ha dejado de usarse
La variable de secuencia de tareas OSDPreserveDriveLetter determina si la secuencia de tareas usará o no la letra de unidad capturada en el archivo WIM de imagen de sistema operativo al aplicar esa imagen a un equipo de destino.
- En Technical Preview 1606, esta variable de secuencia de tareas deja de usarse.

Ahora, durante una implementación del sistema operativo, el programa de instalación de Windows determina, de forma predeterminada, cuál es la mejor letra de unidad (normalmente C:). Si quiere especificar otra unidad, puede cambiar la ubicación en el paso de secuencia de tareas Aplicar el sistema operativo. Vaya al valor **Seleccione la ubicación en la que desea aplicar este sistema operativo**, seleccione **Letra de unidad lógica específica** y elija la unidad que quiere usar. Debe haber una unidad asignada con la letra que elija en el equipo de destino. 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a> Cambios en el nodo de actualizaciones y mantenimiento
Con Technical Preview 1606 se han presentado varios cambios que se aplican a Actualizaciones y mantenimiento en la consola de Configuration Manager:
- **Cambio de nombre de nodo:**

    En el área de trabajo **Supervisión**, el nombre del nodo **Estado de mantenimiento del sitio** ha cambiado a **Actualizaciones y estado de mantenimiento**.
- **Estado de instalación más extenso:**

    Al ver el estado de instalación de actualización de un sitio, ahora la consola muestra detalles independientes para las siguientes acciones:
    - **Descargar** (se aplica únicamente al sitio de nivel superior en el que está instalado el rol de sistema de sitio del punto de conexión de servicio)
    - **replicación**
    - **Comprobación de requisitos previos**
    - **Instalación**

  Además, ahora hay información más detallada para cada paso, incluso en qué archivo de registro puede ver más información.  
-   **Nueva opción para omitir errores de requisitos previos:**

    En las áreas de trabajo **Administración** y **Supervisión**, el nodo **Actualizaciones y mantenimiento** incluye un nuevo botón en la cinta de opciones denominado **Omitir advertencias de requisitos previos**.

    Cuando instale actualizaciones sin usar la opción Omitir advertencias de requisitos previos (desde el Asistente para actualizaciones) y esa instalación de actualización se detenga con un estado **advertencia sobre requisitos previos**, puede seleccionar **Omitir advertencias de requisitos previos** en la cinta de opciones para desencadenar una continuación automática de la instalación de la actualización que omita las advertencias sobre requisitos previos.  



- **Vista más clara de las actualizaciones:**

    Cuando abra el nodo **Actualizaciones y mantenimiento**, ahora verá solo la actualización instalada más reciente y las nuevas actualizaciones disponibles para instalar. Para ver actualizaciones instaladas previamente, haga clic en el nuevo botón **Historial** que aparece en la cinta de opciones.  

-   **Cambio de nombre de la opción de preproducción:**

    En el nodo Actualizaciones y mantenimiento, el botón denominado **Opciones de cliente** ahora se denomina **Promover el cliente de preproducción**.