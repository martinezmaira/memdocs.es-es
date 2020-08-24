---
title: Requisitos de acceso a Internet
titleSuffix: Configuration Manager
description: Obtenga información sobre los puntos de conexión de Internet para permitir la funcionalidad completa de las características de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbb5d524551f5ff2c0a04b62b0f494046eee7a45
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692694"
---
# <a name="internet-access-requirements"></a>Requisitos de acceso a Internet

Algunas características de Configuration Manager se basan en la conectividad de Internet para obtener la funcionalidad completa. Si la organización restringe la comunicación de red con Internet mediante un dispositivo proxy o firewall, asegúrese de permitir estos puntos de conexión.

<!-- SCCMDocs-pr #3403 -->

Configuration Manager usa estos servicios de reenvío de URL de Microsoft en todo el producto:

- `https://aka.ms`
- `https://go.microsoft.com`

Incluso si no aparecen explícitamente en las secciones siguientes, siempre debe permitir estos puntos de conexión.

## <a name="service-connection-point"></a><a name="bkmk_scp"></a> Punto de conexión de servicio

Estas configuraciones se aplican al equipo que hospeda el punto de conexión de servicio y cualquier firewall que haya entre ese equipo e Internet. Ambos deben permitir las comunicaciones a través de los puertos de salida **TCP 443** para HTTPS y **TCP 80** para HTTP a las ubicaciones de Internet siguientes.

El punto de conexión de servicio admite el uso de un proxy web (con o sin autenticación) para usar estas ubicaciones. Para obtener más información, vea [Compatibilidad de servidor proxy](proxy-server-support.md).

Para más información sobre el punto de conexión de servicio, consulte [Acerca del punto de conexión de servicio](../../servers/deploy/configure/about-the-service-connection-point.md).

Otras características de Configuration Manager pueden requerir puntos de conexión adicionales del punto de conexión de servicio. Para más información, consulte las demás secciones de este artículo:

> [!TIP]  
> El punto de conexión de servicio usa el servicio de Microsoft Intune cuando se conecta a `go.microsoft.com` o `manage.microsoft.com`. Hay un problema conocido por el que el conector de Intune experimenta problemas de conectividad si no está instalado el certificado raíz de Baltimore CyberTrust, si ha expirado o si está dañado en el punto de conexión de servicio. Para más información, consulte [KB 3187516: Service connection point doesn't download updates](https://support.microsoft.com/help/3187516) (El punto de conexión de servicio no descarga las actualizaciones).  

A partir de la versión 2002, si el sitio de Configuration Manager no se puede conectar a los puntos de conexión necesarios para un servicio en la nube, genera un mensaje de estado crítico con el identificador 11488. Si no se puede conectar al servicio, el estado del componente SMS_SERVICE_CONNECTOR cambia a crítico. Consulte el estado detallado en el nodo [Estado del componente](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) de la consola de Configuration Manager.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a> Actualizaciones y servicio

Para más información sobre esta función, consulte [Actualizaciones y servicio para Configuration Manager](../../servers/manage/updates.md).

> [!Tip]  
> Habilite estos puntos de conexión para la regla de [conclusiones de administración](../../servers/manage/management-insights.md), **Connect the site to the Microsoft cloud for Configuration Manager updates** (Conectar el sitio a la nube de Microsoft para obtener las actualizaciones de Configuration Manager).

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Servicio de actualización de Windows 10

Para más información sobre esta función, consulte [Administración de Windows como servicio](../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Servicios de Azure

Para más información sobre esta función, consulte [Configuración de servicios de Azure para utilizarlos con Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md).

- `management.azure.com` (nube pública de Azure)
- `management.usgovcloudapi.net` (nube de Azure US Government)

## <a name="co-management"></a>Administración conjunta

Si inscribe dispositivos de Windows 10 en Microsoft Intune para realizar una administración conjunta, asegúrese de que esos dispositivos puedan acceder a los puntos de conexión que Intune requiere. Para más información, consulte [Puntos de conexión de red de Microsoft Intune](/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Microsoft Store para Empresas

Si integra Configuration Manager con [Microsoft Store para Empresas](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md), asegúrese de que el punto de conexión de servicio y los dispositivos de destino puedan acceder al servicio en la nube. Para más información, consulte [Configuración del proxy de Microsoft Store para Empresas](/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="delivery-optimization"></a>Optimización de entrega

Si usa la optimización de la distribución, los clientes deben comunicarse con su servicio en la nube: `*.do.dsp.mp.microsoft.com`.

Los puntos de distribución que admiten la caché conectada de Microsoft también requieren dichos puntos de conexión.

Vea los siguientes artículos para más información:

- [Preguntas más frecuentes sobre la optimización de la distribución](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Aspectos básicos de la administración de contenido en Configuration Manager](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Caché de conexión de Microsoft en Configuration Manager](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> Servicios en la nube

<!-- SCCMDocs-pr #3402 -->

En esta sección se tratan las características siguientes:

- Cloud Management Gateway (CMG)
- Punto de distribución de nube (CDP)
- Integración de Azure Active Directory (Azure AD)
- Detección basada en Azure AD

Para más información sobre CMG, consulte [Planear para Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).

En las secciones siguientes se enumeran los puntos de conexión por rol. Algunos puntos de conexión hacen referencia a un servicio por `<name>`, que es el nombre del servicio en la nube de CMG o CDP. Por ejemplo, si CMG es `GraniteFalls.CloudApp.Net`, el punto de conexión de almacenamiento real es `GraniteFalls.blob.core.windows.net`.<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>Punto de conexión de servicio

Para implementar el servicio CMG o CDP, el punto de conexión de servicio necesita acceso a:

- Los puntos de conexión específicos de Azure son diferentes para cada entorno, en función de la configuración. Configuration Manager almacena estos puntos de conexión en la base de datos del sitio. Consulte la tabla **AzureEnvironments** de SQL Server para obtener la lista de puntos de conexión de Azure.

- [Servicios de Azure](#azure-services)

- Detección de usuarios de Azure AD:

  - Versión 1902 y posteriores: Punto de conexión de Microsoft Graph `https://graph.microsoft.com/`

  - Versión 1810 y anteriores: Punto de conexión de Azure AD Graph `https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>Punto de conexión de CMG

El punto de conexión de CMG necesita acceso a los puntos de conexión de servicio siguientes:

- Nombre del servicio en la nube (para CMG o CDP):
  - `<name>.cloudapp.net` (nube pública de Azure)
  - `<name>.usgovcloudapp.net` (nube de Azure US Government)

- Punto de conexión de la administración de servicios: `https://management.core.windows.net/`  

- Punto de conexión de almacenamiento (para CMG o CDP habilitados para contenido):
  - `<name>.blob.core.windows.net` (nube pública de Azure)
  - `<name>.blob.core.usgovcloudapi.net` (nube de Azure US Government)
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

El sistema de sitio del punto de conexión de CMG admite el uso de un proxy web. Para obtener más información sobre cómo configurar este rol para un proxy, vea [Compatibilidad de servidor proxy](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). El punto de conexión de CMG solo necesita conectarse a los puntos de conexión de servicio de CMG. No necesita acceso a otros puntos de conexión de Azure.

### <a name="configuration-manager-client"></a>Cliente de Configuration Manager

- Nombre del servicio en la nube (para CMG o CDP):
  - `<name>.cloudapp.net` (nube pública de Azure)
  - `<name>.usgovcloudapp.net` (nube de Azure US Government)

- Punto de conexión de almacenamiento (para CMG o CDP habilitados para contenido):
  - `<name>.blob.core.windows.net` (nube pública de Azure)
  - `<name>.blob.core.usgovcloudapi.net` (nube de Azure US Government)

- Para la recuperación de tokens de Azure AD, el punto de conexión de Azure AD:
  - `login.microsoftonline.com` (nube pública de Azure)
  - `login.microsoftonline.us` (nube de Azure US Government)

### <a name="configuration-manager-console"></a>Consola de Configuration Manager

- Para la recuperación de tokens de Azure AD, el punto de conexión de Azure AD:

  - Nube pública de Azure
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Nube de Azure US Government
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a> Actualizaciones de software

Permita que el punto de actualización de software activo acceda a los puntos de conexión siguientes para que WSUS y las actualizaciones automáticas se puedan comunicar con el servicio en la nube de Microsoft Update:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://ntservicepack.microsoft.com`  

Para más información sobre las actualizaciones de software, consulte [Planear las actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md).

### <a name="intranet-firewall"></a>Firewall de intranet

Es posible que tenga que agregar puntos de conexión a un firewall que se encuentra entre dos sistemas de sitio en los casos siguientes:

- Si los sitios secundarios tienen un punto de actualización de software
- Si hay un punto de actualización de software basado en Internet activo remoto en un sitio

#### <a name="software-update-point-on-the-child-site"></a>Punto de actualización de software del sitio secundario

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-microsoft-365-apps"></a>Administración de Aplicaciones de Microsoft 365

> [!NOTE]
> A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](/deployoffice/name-change). Es posible que siga viendo referencias al nombre anterior en la consola de Configuration Manager y la documentación complementaria mientras se está actualizando la consola.

Si usa Configuration Manager para implementar y actualizar Aplicaciones de Microsoft 365 para empresas, permita los siguientes puntos de conexión:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` para sincronizar el punto de actualización de software para actualizaciones de cliente de Aplicaciones de Microsoft 365 para empresas

- `config.office.com` para crear configuraciones personalizadas para implementaciones de Aplicaciones de Microsoft 365 para empresas

- `contentstorage.osi.office.net` para admitir la evaluación de la preparación de complementos de Office<!-- MEMDocs#410 -->

## <a name="configuration-manager-console"></a>Consola de Configuration Manager

Los equipos con la consola de Configuration Manager requieren acceso a los puntos de conexión de Internet siguientes para características específicas:

### <a name="in-console-feedback"></a>Comentarios en la consola

- `http://petrol.office.microsoft.com`

Para más información sobre esta característica, consulte [Comentarios sobre el producto](../../understand/find-help.md#product-feedback).

### <a name="community-workspace"></a>Área de trabajo de la comunidad

#### <a name="documentation-node"></a>Nodo de documentación

Para más información sobre este nodo de la consola, consulte [Uso de la consola de Configuration Manager](../../servers/manage/admin-console.md).

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>Centro de la comunidad

Para más información sobre esta característica, consulte [Centro de comunidad](../../servers/manage/community-hub.md).

- `https://github.com`

- `https://communityhub.microsoft.com`

### <a name="monitoring-workspace-site-hierarchy-node"></a>Área de trabajo Supervisión, nodo Jerarquía de sitios

Si usa la **vista geográfica**, permita el acceso al punto de conexión siguiente:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Análisis de escritorio

Para más información, consulte [Habilitación del uso compartido de datos](../../../desktop-analytics/enable-data-sharing.md#endpoints).

[!INCLUDE [Internet endpoints for Desktop Analytics](includes/internet-endpoints-desktop-analytics.md)]

## <a name="tenant-attach"></a>Asociación de inquilinos

Para más información, consulte [Habilitación de la asociación de inquilinos](../../../tenant-attach/device-sync-actions.md).

[!INCLUDE [Internet endpoints for tenant attach](includes/internet-endpoints-tenant-attach.md)]

## <a name="endpoint-analytics"></a>Análisis de puntos de conexión

Para más información, consulte [Configuración del proxy de Análisis de puntos de conexión](../../../../analytics/troubleshoot.md#bkmk_endpoints).

[!INCLUDE [Internet endpoints for Endpoint analytics](includes/internet-endpoints-endpoint-analytics.md)]

## <a name="asset-intelligence"></a>Asset Intelligence

<!-- memdocs#470 -->
Si usa [Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md), permita estos puntos de conexión para que el servicio se sincronice:

- `https://sc.microsoft.com`
- `https://ssu2.manage.microsoft.com`

## <a name="microsoft-public-ip-addresses"></a>Direcciones IP públicas de Microsoft

Para más información sobre los intervalos de direcciones IP de Microsoft, consulte [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602) (Espacio de direcciones IP públicas de Microsoft). Estas direcciones se actualizan periódicamente. No hay granularidad por servicio, por lo que se podría usar cualquier dirección IP dentro de estos intervalos.

## <a name="see-also"></a>Vea también

- [Puertos usados en Configuration Manager](../hierarchy/ports.md)

- [Compatibilidad con servidores proxy en Configuration Manager](proxy-server-support.md)