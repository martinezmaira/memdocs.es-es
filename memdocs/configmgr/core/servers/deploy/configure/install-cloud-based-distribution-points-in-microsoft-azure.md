---
title: Instalación de puntos de distribución de nube
titleSuffix: Configuration Manager
description: Siga estos pasos para configurar un punto de distribución de nube en Configuration Manager.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35379aed71544a25a98ec4dfa421be70c1bae851
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427734"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Instalación de un punto de distribución de nube para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> Ha cambiado la implementación para compartir contenido de Azure. Use una puerta de enlace de administración de la nube habilitada para el contenido al habilitar la opción de **Permitir a CMG funcionar como un punto de distribución de nube y servir contenido desde Azure Storage**. Para obtener más información, vea [Modify a CMG](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg) (Modificar una instancia de CMG).
>
> No podrá crear un punto de distribución en la nube tradicional en el futuro. Para más información, consulte [Características en desuso y eliminadas](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

En este artículo se detallan los pasos para instalar un punto de distribución de nube de Configuration Manager en Microsoft Azure. Se incluyen las secciones siguientes:

- [Antes de comenzar](#bkmk_before)
- [Configuración](#bkmk_setup)
- [Configuración de DNS](#bkmk_dns)
- [Configuración del proxy de servidor de sitio](#bkmk_proxy)
- [Distribución de contenido y configuración de clientes](#bkmk_client)
- [Administración y supervisión](#bkmk_monitor)
- [Modificar](#bkmk_modify)
- [Solución de problemas avanzada](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a> Antes de comenzar

Empiece por leer el artículo [Uso de un punto de distribución de nube](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Ese artículo ayuda a planear y diseñar los puntos de distribución de nube.

Use la lista de comprobación siguiente para asegurarse de que tiene la información necesaria y los requisitos previos para crear un punto de distribución de nube:  

- El servidor de sitio se puede conectar a Azure. Si la red usa un proxy, [configure el rol de sistema de sitio](#bkmk_proxy).  

- El **entorno de Azure** que se va a usar. Por ejemplo, la nube pública de Azure o la nube de Azure US Government.  

- A partir de la versión 1806, se *recomienda* utilizar la **implementación de Azure Resource Manager**. Los requisitos son los siguientes:<!--1322209-->  

    - Integración con [Azure Active Directory](azure-services-wizard.md) para la **administración en la nube**. La detección de usuarios de Azure AD no es necesaria.  

    - El **Id. de suscripción** de Azure.  

    - El **Grupo de recursos** de Azure.  

    - Durante el asistente, debe iniciar sesión una **cuenta de administrador de suscripción**.  

- Un **certificado de autenticación de servidor**, exportado como un archivo .PFX.  

- Un **nombre del servicio** único global para el punto de distribución de nube.  

    > [!TIP]  
    > Antes de solicitar el certificado de autenticación de servidor que usa este nombre de servicio, confirme que el nombre de dominio de Azure deseado sea único. Por ejemplo, *WallaceFalls.CloudApp.Net*.
    >
    > 1. Inicie sesión en [Azure Portal](https://portal.azure.com).
    > 1. Seleccione **Todos los recursos** y, luego, seleccione **Agregar**.
    > 1. Busque el **servicio en la nube**. Seleccione **Crear**.
    > 1. En el campo **Nombre DNS**, escriba el prefijo que quiere, por ejemplo, *WallaceFalls*. La interfaz mostrará si el nombre de dominio está disponible o si ya está en uso por otro servicio.
    >
    > No cree el servicio en el portal, simplemente use este proceso para comprobar si el nombre está disponible.

- La **región** de Azure para esta implementación.  

- Si todavía necesita usar la **implementación del servicio clásico** de Azure en la versión 1810 o anteriores de Configuration Manager, necesita estos requisitos:  

    > [!Important]  
    > A partir de la versión 1810, las implementaciones de servicio clásico de Azure estarán en desuso en Configuration Manager. Empiece a usar las implementaciones de Azure Resource Manager para el punto de distribución de nube. Para obtener más información, vea [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager).  
    >
    > A partir de la versión 1902 de Configuration Manager, Azure Resource Manager es el único mecanismo de implementación para instancias nuevas del punto de distribución de nube.<!-- 3605704 -->

    - El **Id. de suscripción** de Azure.  

    - Un **certificado de administración** de Azure, exportado como archivo .CER y .PFX. Un administrador de suscripción de Azure tiene que agregar el certificado de administración .CER a la suscripción en [Azure Portal](https://portal.azure.com).  

### <a name="branchcache"></a>BranchCache

Para habilitar un punto de distribución de nube para que use Windows BranchCache, instale la característica BranchCache en el servidor de sitio.<!-- SCCMDocs-pr#4054 -->

- Si el servidor de sitio tiene un rol de sistema de sitio de punto de distribución local, configure la opción de las propiedades de ese rol en **Habilitar y configurar BranchCache**. Para obtener más información, vea [Configuración de puntos de distribución](install-and-configure-distribution-points.md#bkmk_config-general).

- Si el servidor de sitio no tiene un rol de punto de distribución, instale la característica BranchCache en Windows. Para más información, vea [Instalación de la característica BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

Si ya ha distribuido contenido a un punto de distribución de nube y después decide habilitar BranchCache, instale primero la característica. Después, vuelva a distribuir el contenido al punto de distribución de nube.

> [!NOTE]  
> En la versión 1810 de Configuration Manager y versiones anteriores, si tiene más de un punto de distribución de nube, debe establecer manualmente la frase de contraseña de la clave de BranchCache. Para más información, vea [KB 4458143 de Soporte técnico de Microsoft](https://support.microsoft.com/help/4458143).

## <a name="set-up"></a><a name="bkmk_setup"></a> Configuración  

Realice este procedimiento en el sitio para hospedar este punto de distribución de nube, según lo determinado por el [diseño](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology).  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione **Puntos de distribución de nube**. En la cinta, haga clic en **Crear punto de distribución de nube**.  

2. En la página **General** del Asistente para crear punto de distribución de nube, configure las opciones siguientes:  

    1. En primer lugar, especifique el **entorno de Azure**.  

    2. A partir de la versión 1806, se *recomienda* seleccionar la **implementación de Azure Resource Manager** como método de implementación. Haga clic en **Iniciar sesión** para autenticarse con una cuenta de administrador de suscripción de Azure. El asistente rellena automáticamente los campos restantes con la información almacenada durante el requisito previo de integración de Azure AD. Si tiene varias suscripciones, seleccione el **Id. de suscripción** de la suscripción deseada que se va a usar.  

    > [!Note]  
    > A partir de la versión 1810, las implementaciones de servicio clásico de Azure estarán en desuso en Configuration Manager.
    >
    > Si necesita usar una implementación de servicio clásico, seleccione esa opción en esta página. Primero escriba su **id. de suscripción** de Azure. Después, haga clic en **Examinar** y seleccione el archivo .PFX para el certificado de administración de Azure.  

3. Seleccione **Siguiente**. Espere mientras el sitio prueba la conexión a Azure.  

4. En la página **Configuración**, especifique las opciones siguientes y, después, haga clic en **Siguiente**:  

    - **Región**: seleccione la región de Azure donde quiera crear el punto de distribución de nube.  

    - **Grupo de recursos** (solo para el método de implementación de Azure Resource Manager)  

        - **Usar existente**: seleccione un grupo de recursos existente en la lista desplegable.  

        - **Crear nuevo**: escriba el nombre del grupo de recursos nuevo que se va a crear en la suscripción de Azure.  

    - **Sitio primario**: seleccione el sitio primario para distribuir contenido a este punto de distribución.

    - **Archivo de certificado**: haga clic en **Examinar** y seleccione el archivo .PFX para el certificado de autenticación de servidor de este punto de distribución de nube. El nombre común de este certificado rellena los campos **FQDN de servicio** y **Nombre de servicio** necesarios.  

        > [!NOTE]  
        > El certificado de autenticación de servidor de punto de distribución de nube admite caracteres comodín. Si usa un certificado comodín, reemplace el asterisco (`*`) en el campo **FQDN de servicio** por el nombre de host deseado para el servicio.  

5. En la página **Alertas**, configure cuotas de almacenamiento, cuotas de transferencia y el porcentaje de estas cuotas en el que quiere que Configuration Manager genere alertas. A continuación, seleccione **Siguiente**.  

6. Complete el asistente.  

### <a name="monitor-installation"></a>Supervisión de la instalación  

El sitio empieza a crear un nuevo servicio hospedado para el punto de distribución de nube. Después de cerrar el asistente, supervise el progreso de instalación del punto de distribución de nube en la consola de Configuration Manager. Supervise también el archivo **CloudMgr.log** en el servidor de sitio primario. Si es necesario, supervise el aprovisionamiento del servicio en la nube en Azure Portal.  

> [!NOTE]  
> Se puede tardar hasta 30 minutos en aprovisionar un nuevo punto de distribución en Azure. El archivo **CloudMgr.log** repite el mensaje siguiente hasta que se aprovisione la cuenta de almacenamiento:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Después de que aprovisione la cuenta de almacenamiento, se crea el servicio y se configura.  

### <a name="verify-installation"></a>Comprobación de la instalación

Compruebe que se ha completado la instalación del punto de distribución de nube mediante los métodos siguientes:  

- En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Cloud Services** y haga clic en el nodo **Puntos de distribución de nube**. Busque el nuevo punto de distribución de nube en la lista. En la columna Estado debe aparecer **Listo**.  

- En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Expanda **Estado del sistema** y haga clic en el nodo **Estado del componente**. Muestre todos los mensajes del componente **SMS_CLOUD_SERVICES_MANAGER** y busque el identificador de mensaje de estado **9409**.  

- Si es necesario, vaya a Azure Portal. La **Implementación** del punto de distribución de nube muestra un estado de **Listo**.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a> Configuración de DNS  

Antes de que los clientes puedan usar el punto de distribución de nube, deben ser capaces de resolver su nombre en una dirección IP que administra Azure. El punto de administración les proporciona el **FQDN de servicio** del punto de distribución de nube. El punto de distribución de nube existe en Azure como el **nombre del servicio**. Puede ver estos valores en la pestaña **Configuración** de las propiedades del punto de distribución de nube.

> [!Note]  
> En el nodo **Puntos de distribución de nube** de la consola se incluye una columna denominada **Nombre del servicio**, pero realmente se muestra el valor de **FQDN de servicio**. Para ver ambos valores, abra las **propiedades** del punto de distribución de nube y cambie a la pestaña **Configuración**.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

El nombre común del certificado de autenticación de servidor debe incluir el nombre de dominio. Este nombre es obligatorio al comprar un certificado de un proveedor público. Se recomienda cuando se emite este certificado desde la PKI. Por ejemplo, `WallaceFalls.contoso.com`. Al especificar este certificado en el Asistente para crear punto de distribución de nube, el nombre común rellena la propiedad **FQDN de servicio** (`WallaceFalls.contoso.com`). El **Nombre del servicio** toma el mismo nombre de host (`WallaceFalls`) y lo anexa al nombre de dominio de Azure, `cloudapp.net`. En este escenario, los clientes necesitan resolver el **FQDN de servicio** del dominio (`WallaceFalls.contoso.com`) en el **Nombre del servicio** de Azure (`WallaceFalls.cloudapp.net`). Cree un alias CNAME para asignar estos nombres.

### <a name="create-cname-alias"></a>Creación de un alias CNAME

Cree un registro de nombre canónico (CNAME) en el DNS público con conexión a Internet de la organización. Este registro crea un alias para la propiedad **FQDN de servicio** del punto de distribución de nube que los clientes reciben, en el **Nombre del servicio** de Azure. Por ejemplo, cree un nuevo registro CNAME para `WallaceFalls.contoso.com` en `WallaceFalls.cloudapp.net`.  

### <a name="client-name-resolution-process"></a>Proceso de resolución de nombres de cliente

En el proceso siguiente se muestra cómo un cliente resuelve el nombre del punto de distribución de nube:  

1. El cliente obtiene el **FQDN de servicio** del punto de distribución de nube en la lista de orígenes de contenido. Por ejemplo, `WallaceFalls.contoso.com`.  

2. Realiza una consulta DNS, que resuelve el FQDN de servicio con el alias CNAME en el **Nombre del servicio** de Azure. Por ejemplo, `WallaceFalls.cloudapp.net`.  

3. Vuelve a realizar una consulta DNS, que resuelve el nombre del servicio de Azure en la dirección IP pública de Azure.  

4. El cliente usa esta dirección IP para iniciar la comunicación con el punto de distribución de nube.  

5. El punto de distribución de nube presenta el certificado de autenticación de servidor al cliente. El cliente usa la cadena de confianza del certificado para la validación.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a> Configuración del proxy de servidor de sitio  

El servidor de sitio primario que administra el punto de distribución de nube debe comunicarse con Azure. Si en la organización se usa un servidor proxy para controlar el acceso a Internet, configure el servidor de sitio primario para usar este proxy.  

Para obtener más información, vea [Compatibilidad de servidor proxy](../../../plan-design/network/proxy-server-support.md).  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a> Distribución de contenido y configuración de clientes

La distribución del contenido al punto de distribución de nube es igual que en cualquier otro punto de distribución local. El punto de administración no incluye el punto de distribución de nube en la lista de ubicaciones de contenido a menos que tenga el contenido que los clientes solicitan. Para obtener más información, vea [Distribute and manage content](deploy-and-manage-content.md) (Distribución y administración de contenido).

El punto de distribución de nube se administra como cualquier otro punto de distribución local. Estas acciones incluyen la asignación a un grupo de puntos de distribución y la administración de paquetes de contenido. Para obtener más información, vea [Instalación y configuración de puntos de distribución](install-and-configure-distribution-points.md).

La configuración predeterminada del cliente habilita automáticamente a los clientes para usar puntos de distribución de nube. El acceso a todos los puntos de distribución de nube de la jerarquía se controla mediante la configuración de cliente siguiente:  

- En el grupo **Configuración de nube**, modifique la opción **Permitir acceso al punto de distribución de nube**.  

    - De forma predeterminada, esta opción está establecida en **Sí**.  

    - Modifique e implemente esta opción para los usuarios y los dispositivos.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a> Administración y supervisión  

La supervisión del contenido que se distribuye a un punto de distribución de nube es igual que la de cualquier otro punto de distribución local. Para obtener más información, vea [Supervisión del contenido](monitor-content-you-have-distributed.md).

Al ver la lista de puntos de distribución de nube en la consola, puede agregar otras columnas a la lista. Por ejemplo, la columna **Salida de datos** muestra la cantidad de clientes de datos descargados del servicio en los últimos 30 días.<!-- SCCMDocs#755 -->

### <a name="alerts"></a><a name="bkmk_alerts"></a> Alertas  

Configuration Manager comprueba periódicamente el servicio de Azure. Si el servicio no está activo, o bien si hay problemas de certificados o de la suscripción, Configuration Manager genera una alerta.

Configure umbrales para la cantidad de datos que quiere almacenar en el punto de distribución de nube, y para la cantidad de datos que los clientes descargan desde el punto de distribución. Use alertas para estos umbrales para ayudarle a decidir cuándo se debe detener el servicio en la nube, ajustar el contenido que se almacena en el punto de distribución de nube o modificar los clientes que pueden usar el servicio.

- **Umbral de alerta de almacenamiento**: el umbral de alerta de almacenamiento establece un límite superior en GB para la cantidad de datos o de contenido que se quiere almacenar en el punto de distribución de nube. De forma predeterminada, este umbral es de 2.000 GB. Configuration Manager genera alertas críticas y de advertencia cuando el espacio libre restante alcanza los niveles que se hayan especificado. De forma predeterminada, estas alertas se producen en el 50 % y 90 % del umbral.  

- **Umbral de alerta de transferencia**: el umbral de alerta de transferencia mensual permite supervisar la cantidad de contenido que se transfiere desde el punto de distribución a los clientes durante un período de 30 días. De forma predeterminada, este umbral es de 10.000 GB. El sitio genera alertas críticas y de advertencia cuando las transferencias alcanzan los valores que se definen. De forma predeterminada, estas alertas se producen en el 50 % y 90 % del umbral.  

    > [!IMPORTANT]  
    > Configuration Manager supervisa la transferencia de datos, pero no detiene la transferencia cuando se supera el valor establecido en el umbral de alerta de transferencia.  

Especifique los umbrales para cada punto de distribución de nube durante la instalación, o bien use la pestaña **Alertas** de las propiedades del punto de distribución de nube.  

> [!NOTE]  
> Las alertas para un punto de distribución de nube dependen de las estadísticas de uso de Azure, que pueden tardar hasta 24 horas en estar disponibles. Para obtener más información sobre Storage Analytics para Azure, vea [Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

En un ciclo de una hora, el sitio primario que supervisa el punto de distribución de nube descarga los datos de transacciones desde Azure. Almacena estos datos de transacción en el archivo `CloudDP-<ServiceName>.log` del servidor de sitio. Después, Configuration Manager evalúa esta información en función de las cuotas de transferencia y almacenamiento de cada punto de distribución de nube. Si la transferencia de datos alcanza o supera el volumen especificado de alertas de advertencia o de alertas críticas, Configuration Manager generará la alerta correspondiente.  

> [!WARNING]  
> Como el sitio descarga la información sobre las transferencias de datos desde Azure cada hora, es posible que el uso supere un umbral de advertencia o crítico antes de que Configuration Manager pueda acceder a los datos y generar una alerta.  


## <a name="modify"></a><a name="bkmk_modify"></a> Modificación

La información general sobre el punto de distribución se puede ver en el nodo **Puntos de distribución de nube** en **Cloud Services** en el área de trabajo **Administración** de la consola de Configuration Manager. Seleccione un punto de distribución y haga clic en **Propiedades** para ver más detalles.  

Al modificar las propiedades de un punto de distribución en la nube, las pestañas siguientes incluyen opciones de configuración que se pueden editar:  

#### <a name="settings"></a>Configuración

- **Descripción**  

- **Archivo de certificado**: antes de que expire el certificado de autenticación de servidor, emita un certificado nuevo con el mismo nombre común. Después, agregue aquí el certificado nuevo para que el servicio empiece a usarlo. Si el certificado expira, los clientes no confiarán ni usarán el servicio.  

#### <a name="alerts"></a>Alertas

Ajuste los umbrales de datos para las alertas de almacenamiento y transferencia mensual.  

#### <a name="content"></a>Content

Administre el contenido igual que en un punto de distribución local.  

### <a name="redeploy-the-service"></a>Volver a implementar el servicio

Los cambios más importantes, como las configuraciones siguientes, requieren volver a implementar el servicio:

- Método de implementación clásica en Azure Resource Manager
- Suscripción
- Nombre del servicio
- PKI privada a pública
- Región de Azure

A partir de la versión 1806, si tiene un punto de distribución de nube existente en el método de implementación clásico, debe implementar un punto de distribución de nube nuevo para usar el método de implementación de Azure Resource Manager. Hay dos opciones:

- Si quiere reutilizar el mismo nombre de servicio:  

    1. En primer lugar, elimine el punto de distribución de nube clásico. Si no hay otro punto de distribución de nube, es posible que los clientes no puedan obtener el contenido.  

    2. Cree un punto de distribución de nube mediante una implementación de Resource Manager. Reutilice el mismo certificado de autenticación de servidor.  

    3. Distribuya el contenido del paquete de software necesario para el nuevo punto de distribución de nube.  

- Si quiere usar un nombre de servicio nuevo:  

    1. Cree un punto de distribución de nube mediante una implementación de Resource Manager. Use un certificado de autenticación de servidor nuevo.  

    2. Distribuya el contenido del paquete de software necesario para el nuevo punto de distribución de nube.  

    3. Elimine el punto de distribución de nube clásico.

> [!Tip]  
> Para determinar el modelo de implementación actual de un punto de distribución de nube:<!--SCCMDocs issue #611-->  
>
> 1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Puntos de distribución en la nube**.  
> 2. Añada el atributo **Modelo de implementación** como una columna a la vista de lista. Para implementar Resource Manager, este atributo es **Azure Resource Manager**.  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>Detener o iniciar el servicio de nube a petición

Detenga un punto de distribución de nube en cualquier momento en la consola de Configuration Manager. Esta acción impide de forma inmediata que los clientes descarguen contenido adicional del servicio. Reinicie el servicio en la nube desde la consola de Configuration Manager para restaurar el acceso para los clientes. Por ejemplo, detenga un servicio en la nube cuando alcance un umbral de datos.  

Cuando se detiene un punto de distribución de nube, el servicio en la nube no elimina el contenido de la cuenta de almacenamiento. Tampoco impide que el servidor de sitio transfiera contenido adicional al punto de distribución de nube. El punto de administración todavía devuelve el punto de distribución de nube a los clientes como un origen de contenido válido.

Siga los pasos siguientes para detener un punto de distribución de nube:  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Cloud Services** y haga clic en el nodo **Puntos de distribución de nube**.  

2. Seleccione el punto de distribución de nube. Para detener el servicio de nube que se ejecuta en Azure, haga clic en **Detener servicio** en la cinta.  

3. Haga clic en **Iniciar servicio** para reiniciar el punto de distribución de nube.  

### <a name="delete-a-cloud-distribution-point"></a>Eliminar un punto de distribución de nube

Para desinstalar un punto de distribución de nube, selecciónelo en la consola de Configuration Manager y, después, haga clic en **Eliminar**.  

Cuando se elimina un punto de distribución de nube de una jerarquía, Configuration Manager quita el contenido del servicio en la nube en Azure.

Quitar manualmente cualquier componente en Azure hace que el sistema sea incoherente. Este estado deja información huérfana y se pueden producir comportamientos inesperados.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a> Solución de problemas avanzada

Si tiene que recopilar el registro de diagnóstico de las máquinas virtuales de Azure para ayudar a solucionar problemas relacionados con el punto de distribución de nube, use el ejemplo de PowerShell siguiente para habilitar la extensión de diagnóstico de servicio para la suscripción:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

El ejemplo siguiente es un archivo **diagnostics.wadcfgx** de ejemplo como se hace referencia en la variable **public_config** en el script de PowerShell anterior. Para obtener más información, vea [Historial de versiones del esquema de configuración de la extensión Azure Diagnostics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
