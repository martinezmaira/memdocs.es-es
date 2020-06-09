---
title: Caché conectada de Microsoft
titleSuffix: Configuration Manager
description: Uso del punto de distribución de Configuration Manager como servidor de caché local para la Optimización de distribución
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70d4930da712eccff8bdb1f1986a68aa5fe77644
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455283"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Caché de conexión de Microsoft en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--3555764-->

a partir de la versión 1906, puede instalar un servidor de caché con conexión de Microsoft en los puntos de distribución. Al almacenar en caché este contenido de forma local, los clientes pueden beneficiarse de la característica de Optimización de entrega y, además, puede ayudar a proteger los vínculos WAN.

> [!NOTE]
> A partir de la versión 1910, esta característica se llama **caché con conexión de Microsoft**. Antes se conocía como “caché en la red de Optimización de distribución”.

Este servidor de caché actúa como una caché transparente a petición para el contenido descargado mediante la Optimización de entrega. Use la configuración de cliente para asegurarse de que este servidor se ofrezca únicamente a los miembros del grupo de límites de Configuration Manager local.

Esta caché es independiente del contenido del punto de distribución de Configuration Manager. Si elige la misma unidad que el rol de punto de distribución, el contenido se almacenará por separado.

> [!Note]  
> El servidor de caché de conexión es una aplicación instalada en Windows Server. Esta aplicación está aún en fase de desarrollo.

## <a name="how-it-works"></a>Cómo funciona

Cuando se configuran los clientes para que usen el servidor de caché de conexión, ya no necesitan solicitar contenido administrado por Microsoft Cloud desde Internet, sino desde el servidor de caché instalado en el punto de distribución. El servidor local almacena en caché este contenido mediante la característica IIS de Enrutamiento de solicitud de aplicaciones (ARR). Después, el servidor de caché puede responder rápidamente a las solicitudes futuras del mismo contenido. Si el servidor de caché de conexión no está disponible o el contenido todavía no está almacenado en caché, los clientes descargan el contenido de Internet. Los clientes también usan la Optimización de distribución, por lo que debe descargar partes del contenido de los elementos del mismo nivel en su red.

![Diagrama de cómo funciona la caché de conexión](media/3555764-microsoft-connected-cache.png)

1. El cliente comprueba si hay actualizaciones y obtiene la dirección de la red de entrega de contenido (CDN).

2. Configuration Manager configura las opciones de la Optimización de distribución (DO) en el cliente, incluido el nombre del servidor de caché.

3. El cliente A solicita el contenido del servidor de caché de Optimización de distribución.

4. Si la caché no incluye el contenido, el servidor de caché de Optimización de distribución lo obtiene de la red CDN.

5. Si el servidor de caché no responde, el cliente descarga el contenido de la red CDN.

6. Los clientes utilizan la Optimización de distribución para obtener fragmentos del contenido de los elementos del mismo nivel.

## <a name="prerequisites-and-limitations"></a>Requisitos previos y limitaciones

- Un punto de distribución *local*, con las siguientes configuraciones:

  - Ejecución de Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 o Windows Server 2019

  - Sitio web predeterminado habilitado en el puerto 80

  - No preinstale la característica [Enrutamiento de solicitud de aplicaciones](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR). La caché de conexión instala ARR y configura sus valores. Microsoft no puede garantizar que la configuración de ARR de la caché de conexión no entre en conflicto con otras aplicaciones del servidor que también usan esta característica.

  - El punto de distribución requiere acceso a la nube de Microsoft a través de Internet. Las direcciones URL concretas pueden variar según el contenido específico habilitado para la nube. Asegúrese de permitir también los puntos de conexión para la optimización de la distribución. Para más información, consulte los [requisitos de acceso a Internet](../network/internet-endpoints.md).

  - A partir de la versión 2002, la aplicación Caché conectada puede usar un servidor proxy no autenticado para acceder a Internet. Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server).<!-- 5856396 -->

- Clientes que ejecutan Windows 10 versión 1709 y posteriores

## <a name="enable-connected-cache"></a>Habilitar la caché de conexión

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Puntos de distribución**.

1. Seleccione un punto de distribución *local* y, después, en la cinta de opciones, seleccione **Propiedades**.

1. En las propiedades del rol de punto de distribución, en la pestaña **General**, configure las opciones siguientes:  

    1. Habilite la opción **Habilitar este punto de distribución para usarlo como servidor de caché con conexión de Microsoft**.  

        Lea y acepte los términos de licencia.

    2. **Unidad local que se usará**: seleccione el disco que se usará para la memoria caché. El valor predeterminado es **Automático**, que usa el disco con más espacio libre.<sup>[Nota 1](#bkmk_note1)</sup>  

        > [!Note]  
        > Puede cambiar esta unidad más adelante. Se pierde todo el contenido almacenado en caché, a menos que lo copie en la nueva unidad.

    3. **Espacio en disco**: seleccione la cantidad de espacio en disco que se va a reservar en GB o un porcentaje del espacio en disco total. De forma predeterminada, este valor es 100 GB.

        > [!Note]  
        > El tamaño de caché predeterminado debe ser suficiente para la mayoría de los clientes. Puede ajustar el tamaño de la memoria caché más adelante.
        >
        > Si el tamaño de la memoria caché en el disco supera el espacio asignado, ARR borrará espacio quitando contenido en función de su heurística integrada.<!-- SCCMDocs#2045 -->

    4. **Conservar la caché al deshabilitar el servidor de caché con conexión**: si quita el servidor de caché y habilita esta opción, el servidor mantiene el contenido de la caché en el disco.  

1. En la configuración de cliente, en el grupo **Optimización de distribución**, configure la opción **Permita que los dispositivos administrados por Configuration Manager usen servidores de caché con conexión de Microsoft para la descarga de contenido**.  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a> Nota 1: Acerca de la selección de unidades

Si selecciona **Automático**, cuando Configuration Manager instale el componente de caché de conexión, respetará el archivo **no_sms_on_drive.sms**. Por ejemplo, el punto de distribución tiene el archivo `C:\no_sms_on_drive.sms`. Incluso si la unidad C: es la que tiene más espacio disponible, Configuration Manager configura la caché de conexión para usar otra unidad como memoria caché.

Si selecciona una unidad específica que ya tenga el archivo **no_sms_on_drive.sms**, Configuration Manager ignora el archivo. La configuración de la caché de conexión para usar esa unidad es una intención explícita. Por ejemplo, el punto de distribución tiene el archivo `F:\no_sms_on_drive.sms`. Cuando se configuran explícitamente las propiedades del punto de distribución para usar la unidad **F:** , Configuration Manager configura la caché de conexión para que use la unidad F: como memoria caché.

Para cambiar la unidad después de instalar la caché de conexión:

- Configure manualmente las propiedades del punto de distribución para usar una letra de unidad específica.

- Si se establece en Automático, cree primero el archivo **no_sms_on_drive.sms**. Después, realice algún cambio en las propiedades del punto de distribución para desencadenar un cambio de configuración.

### <a name="automation"></a>Automation

<!-- SCCMDocs#1911 -->

Puede usar el SDK de Configuration Manager para automatizar la configuración de la configuración de la caché conectada de Microsoft en un punto de distribución. Como sucede en todos los roles de sitio, use la [clase de WMI SMS_SCI_SysResUse](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md). Para obtener más información, vea [Programación de los roles de sitio](../../../develop/osd/about-operating-system-deployment-site-role-configuration.md#programming-the-site-roles).

Cuando actualice la instancia de **SMS_SCI_SysResUse** para el punto de distribución, establezca las siguientes propiedades:

- **AgreeDOINCLicense**: configúrelo en `1` para aceptar los términos de licencia.
- **Flags**: habilite `|= 4`, deshabilite `&= ~4`.
- **DiskSpaceDOINC**: configúrelo en `Percentage` o `GB`.
- **RetainDOINCCache**: configúrelo en `0` o `1`.
- **LocalDriveDOINC**: configúrelo en `Automatic`, o una letra de unidad específica, como `C:` o `D:`.

## <a name="verify"></a>Comprobar

Cuando los clientes descargan contenido administrado en la nube, usan la Optimización de distribución del servidor de caché instalado en el punto de distribución. El contenido administrado en la nube incluye los tipos siguientes:

- Aplicaciones de Microsoft Store
- Características de Windows a petición, como idiomas
- Si habilita [directivas de Windows Update para empresas](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md): actualizaciones de características y de calidad de Windows 10
- Para las [cargas de trabajo de administración conjunta](../../../comanage/workloads.md):
  - Windows Update para empresas: actualizaciones de características y de calidad de Windows 10
  - Aplicaciones de Office Hacer clic y ejecutar: aplicaciones y actualizaciones de Office
  - Aplicaciones cliente: aplicaciones y actualizaciones de Microsoft Store
  - Endpoint Protection: actualizaciones de definiciones de Windows Defender

En Windows 10 versión 1809 o posteriores, compruebe este comportamiento con el cmdlet **Get-DeliveryOptimizationStatus** de Windows PowerShell. En la salida del cmdlet, revise el valor **BytesFromCacheServer**. Para más información, vea [Supervisar la optimización de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization).

Si el servidor de caché devuelve algún error HTTP, el cliente de Optimización de distribución recurre al origen inicial en la nube.

Para obtener información detallada, vea [Solución de problemas de la Caché con conexión de Microsoft en Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md).

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a> Compatibilidad con aplicaciones Win32 de Intune

<!--5032900-->

A partir de la versión 1910, cuando se habilita la caché de conexión en los puntos de distribución de Configuration Manager, estos pueden suministrar aplicaciones Win32 de Microsoft Intune a los clientes administrados conjuntamente.

### <a name="prerequisites"></a>Requisitos previos

#### <a name="client"></a>Cliente

- Actualice el cliente a la versión más reciente.

- El dispositivo cliente debe tener al menos 4 GB de memoria.

    > [!TIP]
    > Use la siguiente configuración de directiva de grupo: Configuración del equipo > Plantillas administrativas > Componentes de Windows > Optimización de distribución > **capacidad de RAM mínima (completa) necesaria para permitir el uso de la caché de sistema de mismo nivel (en GB)** .

#### <a name="site"></a>Sitio

- Habilite la caché conectada en un punto de distribución. Para más información, vea [Caché de conexión de Microsoft](microsoft-connected-cache.md).

- El cliente y el punto de distribución habilitado para la caché conectada debe estar en el mismo grupo de límites.

- Habilite la siguiente configuración de cliente en el grupo [**Optimización de distribución**](../../clients/deploy/about-client-settings.md#delivery-optimization):

  - **Use los grupos de límites de Configuration Manager para el identificador del grupo de optimización de entrega. Más información**
  - **Enable devices managed by Configuration Manager to use Microsoft Connected Cache servers for content download** (Permitir que los dispositivos administrados mediante Configuration Manager usen los servidores de la caché conectada de Microsoft para la descarga de contenido)

- Habilite la característica en versión preliminar **Client apps for co-managed devices** (Aplicaciones cliente para dispositivos administrados conjuntamente). Para más información, consulte [Características de versión preliminar](../../servers/manage/pre-release-features.md).

- Habilite la administración conjunta y cambie la carga de trabajo **Aplicaciones cliente** a **Intune piloto** o **Intune**. Vea los siguientes artículos para más información:

  - [Cargas de trabajo: aplicaciones cliente](../../../comanage/workloads.md#client-apps)
  - [Habilitación de la administración conjunta](../../../comanage/how-to-enable.md)
  - [Cambio de cargas de trabajo a Intune](../../../comanage/how-to-switch-workloads.md)

    Si está en Intune piloto, agregue el cliente a la colección piloto de las aplicaciones cliente.

#### <a name="intune"></a>Intune

- Esta característica solo admite el tipo de aplicación Win32 de Intune.

  - Cree y asigne (implemente) una nueva aplicación en Intune para este fin. (Las aplicaciones creadas antes de la versión 1811 de Intune no funcionan). Para más información, consulte [Administración de aplicaciones Win32 de Intune](https://docs.microsoft.com/intune/apps/apps-win32-app-management).

  - La aplicación debe tener un tamaño mínimo de 100 MB.
  
    > [!TIP]
    > Use la siguiente configuración de directiva de grupo: Configuración del equipo > Plantillas administrativas > Componentes de Windows > Optimización de distribución > **tamaño mínimo del archivo de contenido de caché de sistemas de mismo nivel (en MB)** .

## <a name="see-also"></a>Vea también

[Optimización de la distribución de actualizaciones de Windows 10 con Configuration Manager](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Solución de problemas de la caché de conexión de Microsoft en Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
