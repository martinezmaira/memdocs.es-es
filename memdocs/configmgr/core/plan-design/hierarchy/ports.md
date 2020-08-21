---
title: Puertos usados para las conexiones
titleSuffix: Configuration Manager
description: Obtenga información sobre los puertos de red necesarios y personalizables que usa Configuration Manager para las conexiones.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2495c0d7b5b19b5d6f7741d3b28b6a9a0e213fc3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700153"
---
# <a name="ports-used-in-configuration-manager"></a>Puertos usados en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se enumeran los puertos de red que usa Configuration Manager. Algunas conexiones usan puertos que no se pueden configurar, mientras que otras admiten puertos personalizados. Si usa tecnología de filtrado de puertos, compruebe que los puertos necesarios estén disponibles. Estas tecnologías de filtrado de puertos incluyen firewalls, enrutadores, servidores proxy o IPsec.

> [!NOTE]  
> Si tiene compatibilidad con clientes basados en Internet mediante el protocolo de puente SSL, además de requisitos de puerto, es posible que también tenga que permitir que algunos verbos y encabezados HTTP atraviesen el firewall.

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Puertos configurables

Configuration Manager le permite configurar los puertos para los siguientes tipos de comunicación:  

- Punto de sitios web del catálogo de aplicaciones a punto de servicio web del catálogo de aplicaciones  

- Punto de proxy de inscripción a punto de inscripción  

- Cliente a sistema de sitio que ejecuta IIS  

- Cliente a Internet (como configuración de servidor proxy)  

- Punto de actualización de software a Internet (como configuración de servidor proxy)  

- Punto de actualización de software a servidor WSUS  

- Servidor de sitio a servidor de base de datos del sitio  

- Servidor de sitio a servidor de base de datos WSUS

- Puntos de servicios de informes  

  > [!NOTE]  
  > Los puertos que se usan para el rol de sistema de sitio de punto de servicios de informes se configuran en SQL Server Reporting Services. Configuration Manager usa estos puertos durante las comunicaciones con el punto de servicios de informes. Asegúrese de revisar estos puertos que definen la información de filtro IP para directivas IPsec o para configurar firewalls.  

De forma predeterminada, el puerto HTTP que se usa para la comunicación entre cliente y sistema de sitio es el puerto 80, y el puerto HTTPS predeterminado es el 443. Los puertos para la comunicación entre cliente y sistema de sitio a través de HTTP o HTTPS se pueden cambiar durante la instalación o en las propiedades del sitio en su sitio de Configuration Manager.  

Los puertos que se usan para el rol de sistema de sitio de punto de servicios de informes se configuran en SQL Server Reporting Services. Configuration Manager usa estos puertos durante las comunicaciones con el punto de servicios de informes. Asegúrese de revisar estos puertos al definir la información de filtro IP para directivas IPsec o para configurar firewalls.  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Puertos no configurables  

Configuration Manager no permite configurar puertos para los siguientes tipos de comunicación:  

- Sitio a sitio  

- Servidor de sitio a sistema de sitio  

- Consola de Configuration Manager con el proveedor de SMS  

- Consola de Configuration Manager a Internet  

- Conexiones a servicios de nube, como Microsoft Intune y puntos de distribución en la nube  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Puertos usados por clientes y sistemas de sitio de Configuration Manager  

En las secciones siguientes se detallan los puertos que se usan para la comunicación en Configuration Manager. En el título de la sección, las flechas representan la dirección de la comunicación:  

- --> Indica que un equipo inicia la comunicación y el otro siempre responde  

- &lt;--> Indica que cualquier equipo puede iniciar la comunicación  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> Punto de sincronización de Asset Intelligence --> Microsoft  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Punto de sincronización de Asset Intelligence --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Punto de servicio web del catálogo de aplicaciones --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Punto de sitios web del catálogo de aplicaciones --> Punto de servicio web del catálogo de aplicaciones  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80<sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Cliente --> Punto de sitios web del catálogo de aplicaciones  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80<sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Cliente --> Cliente  

Un proxy de reactivación también usa los mensajes de solicitud de eco ICMP de un cliente a otro. Los clientes usan esta comunicación para confirmar si el otro cliente está activo en la red. ICMP se conoce a veces como comandos ping. ICMP no tiene un número de protocolo UDP o TCP y, por lo tanto, no aparece en la tabla siguiente. Sin embargo, los firewalls basados en host en estos equipos cliente o los dispositivos de red intermedios en la subred deberán permitir el tráfico ICMP para que la comunicación de proxy de reactivación se realice correctamente.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|--|  
|Proxy de reactivación|25536 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|--|  
|Difusión de caché del mismo nivel de Windows PE|8004|--|  
|Descarga de caché del mismo nivel de Windows PE|--|8003|  

Para más información, consulte [Windows PE Peer Cache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements) (Caché del mismo nivel de Windows PE).

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> Cliente --> Módulo de directivas del servicio de inscripción de dispositivos de red de Configuration Manager (SCEP)

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Cliente --> Punto de distribución en la nube  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para más información, vea [Puertos y flujo de datos](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> Cliente --> Cloud Management Gateway (CMG)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para más información, vea [Puertos y flujo de datos de CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> Cliente -> Punto de distribución, tanto estándar como de extracción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80<sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|
|Actualizaciones rápidas|--|8005 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> Use la configuración de cliente para configurar el puerto alternativo para las actualizaciones rápidas. Para obtener más información, vea [Puerto que los clientes usan para recibir solicitudes para el contenido diferencial](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content).

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> Cliente --> Punto de distribución configurado para la multidifusión, tanto estándar como de extracción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Protocolo de multidifusión|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> Cliente --> Punto de distribución configurado para entorno PXE, tanto estándar como de extracción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 y 68|--|  
|TFTP|69 <sup>[Nota 4](#bkmk_note4)</sup> |--|  
|Capa de negociación de información de inicio (BINL)|4011|--|  

> [!Important]  
> Si habilita un firewall basado en host, asegúrese de que las reglas permiten que el servidor envíe y reciba en estos puertos. Al habilitar un punto de distribución del entorno de ejecución previo al arranque, Configuration Manager puede habilitar las reglas de entrada (recepción) en el Firewall de Windows. No configura las reglas de salida (envío).<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Cliente --> Punto de estado de reserva  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80<sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Cliente --> Controlador de dominio del catálogo global

Los clientes de Configuration Manager no contactan con un servidor de catálogo global si son equipos de grupo de trabajo o están configurados para comunicarse solo a través de Internet.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP de catálogo global|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a> Cliente --> Punto de administración  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Notificación de cliente (comunicación predeterminada antes de usar HTTP o HTTPS)|--|10123 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|HTTP|--|80<sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Cliente --> Punto de actualización de software  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 o 8530 <sup>[Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 o 8531 <sup>[Nota 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Cliente --> Punto de migración de estado  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80<sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|Bloque de mensajes del servidor (SMB)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> Punto de conexión de CMG --> Servicio en la nube de CMG  

Configuration Manager usa estas conexiones para crear el canal de CMG. Para más información, vea [Puertos y flujo de datos de CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (opción preferida)|--|10140-10155|  
|HTTPS (reserva con una máquina virtual)|--|443|  
|HTTPS (reserva con dos máquinas virtuales o más)|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a> Punto de conexión de CMG --> Punto de administración  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Para más información, vea [Puertos y flujo de datos de CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> Punto de conexión de CMG --> Punto de actualización de software  

El puerto concreto depende de la configuración del punto de actualización de software.

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Para más información, vea [Puertos y flujo de datos de CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Consola de Configuration Manager --> Cliente  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Control remoto (control)|--|2701|  
|Asistencia remota (RDP y RTC)|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Consola de Configuration Manager --> Internet  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

La consola de Configuration Manager usa el acceso a Internet para las acciones siguientes:

- La descarga de actualizaciones de software de Microsoft Update para los paquetes de implementación.
- El elemento Comentarios de la barra de herramientas.
- Vínculos a la documentación de la consola.
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Consola de Configuration Manager --> Punto de servicios de informes  

|Descripción|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|80<sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Consola de Configuration Manager --> Servidor de sitio  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (conexión inicial a WMI para localizar el sistema proveedor)|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Consola de Configuration Manager --> Proveedor de SMS  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Módulo de directivas del servicio de inscripción de dispositivos de red de Configuration Manager (SCEP) --> Punto de registro de certificados  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> Punto de servicio de almacenamiento de datos --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a> Punto de distribución, tanto estándar como de extracción --> Punto de administración

Un punto de distribución se comunica con el punto de administración en los siguientes escenarios:  

- Para informar del estado de contenido preconfigurado  

- Para informar de los datos de resumen de uso  

- Para informar de la validación de contenido  

- Para informar del estado de las descargas de paquetes (solo punto de distribución de extracción)

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80<sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Punto de Endpoint Protection --> Internet  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Punto de Endpoint Protection --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Punto de proxy de inscripción --> Punto de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Punto de inscripción --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Conector de Exchange Server --> Exchange Online  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Administración remota de Windows a través de HTTPS|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Conector de Exchange Server --> Exchange Server local  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Administración remota de Windows a través de HTTP|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Equipo Mac --> Punto de proxy de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Punto de administración --> Controlador de dominio  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo ligero de acceso a directorios (LDAP)|389|389|  
|LDAP seguro (LDAPS, para firmar y enlazar)|636|636|  
|LDAP de catálogo global|--|3268|  
|Asignador de extremos de RPC|--|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a> Punto de administración &lt;--> Servidor de sitio

<sup>[Nota 5](#bkmk_note5)</sup>

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Asignador de extremos de RPC|--|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  
|Bloque de mensajes del servidor (SMB)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Punto de administración --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Dispositivo móvil --> Punto de proxy de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Punto de servicios de informes --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a> Punto de conexión del servicio --> Azure (CMG)  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS para la implementación del servicio CMG|--|443|

Para más información, vea [Puertos y flujo de datos de CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Servidor de sitio &lt; --> Punto de servicio web del catálogo de aplicaciones  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Servidor de sitio &lt; --> Punto de sitios web del catálogo de aplicaciones  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Servidor de sitio &lt; --> Punto de sincronización de Asset Intelligence  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a> Servidor de sitio --> Cliente  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Servidor de sitio --> Punto de distribución en la nube  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para más información, vea [Puertos y flujo de datos](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> Servidor de sitio --> Punto de distribución, tanto estándar como de extracción

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Servidor de sitio --> Controlador de dominio  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo ligero de acceso a directorios (LDAP)|389|389|
|LDAP seguro (LDAPS, para firmar y enlazar)|636|636|
|LDAP de catálogo global|--|3268|  
|Asignador de extremos de RPC|--|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Servidor de sitio &lt;--> Punto de registro de certificados  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a> Servidor de sitio &lt;--> Punto de conexión de CMG

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Servidor de sitio &lt;--> Punto de Endpoint Protection  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Servidor de sitio &lt;--> Punto de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Servidor de sitio &lt;--> Punto de proxy de inscripción  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Servidor de sitio &lt;--> Punto de estado de reserva

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> Servidor de sitio --> Internet  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Nota 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Servidor de sitio &lt;--> Entidad de certificación emisora (CA)

Esta comunicación se utiliza al implementar perfiles de certificados utilizando el punto de registro del certificado. La comunicación no se usa para todos los servidores de sitios de la jerarquía, sino que solo se usa para el servidor de sitio que está situado en la parte superior de la jerarquía.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Asignador de extremos de RPC|135|135|  
|RPC (DCOM)|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> Servidor de sitio --> Servidor que hospeda el recurso compartido de biblioteca de contenido remoto

Puede cambiar la biblioteca de contenido a otra ubicación de almacenamiento para liberar espacio de disco duro en los servidores de sitio primario o de administración central. Para obtener más información, consulte [Configuración de una biblioteca de contenido remoto para el servidor de sitio](the-content-library.md#bkmk_remote).

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a> Servidor de sitio &lt;--> Punto de conexión del servicio

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Servidor de sitio &lt;--> Punto de servicios de informes

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a> Servidor de sitio &lt;--> Servidor de sitio  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Servidor de sitio --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

Durante la instalación de un sitio que use un servidor SQL Server remoto para hospedar la base de datos del sitio, debe abrir los puertos siguientes entre el servidor de sitio y SQL Server:  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> Servidor de sitio --> SQL Server para WSUS  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 3](#bkmk_note3) Puerto alternativo disponible</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Servidor de sitio --> Proveedor de SMS  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  
|RPC|--|DINÁMICA <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Servidor de sitio &lt;--> Punto de actualización de software

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|HTTP|--|80 o 8530 <sup>[Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 o 8531 <sup>[Nota 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Servidor de sitio &lt;--> Punto de migración de estado

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  
|Asignador de extremos de RPC|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> Proveedor de SMS --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Punto de actualización de software --> Internet  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Nota 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Punto de actualización de software --> Servidor WSUS ascendente  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 o 8530 <sup>[Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 o 8531 <sup>[Nota 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server

La replicación de base de datos entre sitios requiere que el servidor SQL Server de un sitio se comunique directamente con el servidor SQL Server de su sitio primario o secundario.  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Servicio de SQL Server|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  
|SQL Server Service Broker|--|4022 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

> [!TIP]  
> Configuration Manager no necesita SQL Server Browser, que usa el puerto UDP 1434.  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Punto de migración de estado --> SQL Server  

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|SQL a través de TCP|--|1433 <sup>[Nota 2](#bkmk_note2) Puerto alternativo disponible</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Notas para los puertos usados por clientes y sistemas de sitio de Configuration Manager  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> Nota 1: Puerto del servidor proxy

Este puerto no se puede configurar, pero puede enrutarse a través de un servidor proxy configurado.  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> Nota 2: Puerto alternativo disponible

Puede definir un puerto alternativo en Configuration Manager para este valor. Si define un puerto personalizado, úselo en la información del filtro IP para las directivas IPsec o para configurar firewalls.  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> Nota 3: Windows Server Update Services (WSUS)

WSUS puede instalarse para usar los puertos 80/443 o los puertos 8530/8531 para la comunicación de cliente. Cuando se ejecuta WSUS en Windows Server 2012 o Windows Server 2016, WSUS se configura de forma predeterminada para usar el puerto 8530 para HTTP y el puerto 8531 para HTTPS.  

Después de la instalación, puede cambiar el puerto. No es necesario usar el mismo número de puerto en toda la jerarquía del sitio.  

- Si el puerto HTTP es 80, el puerto HTTPS debe ser 443.  

- Si el puerto HTTP es cualquier otro, el puerto HTTPS debe ser 1 o un valor mayor (por ejemplo, 8530 y 8531).

    > [!NOTE]  
    >  Al configurar el punto de actualización de software para usar HTTPS, también debe estar abierto el puerto HTTP. Los datos sin cifrar, como los términos de licencia de las actualizaciones específicas, usan el puerto HTTP.

- El servidor de sitio establece una conexión con el servidor SQL Server que hospeda el SUSDB cuando se habilitan las opciones siguientes para la limpieza de WSUS:
  - Adición de índices no agrupados a la base de datos de WSUS para mejorar el rendimiento de la limpieza de WSUS
  - Quitar las actualizaciones obsoletas de la base de datos de WSUS
  
  Si el puerto de SQL Server predeterminado se cambia a un puerto alternativo con el Administrador de configuración de SQL Server, asegúrese de que el servidor de sitio se puede conectar mediante el puerto definido. Configuration Manager no admite los puertos dinámicos. De manera predeterminada, las instancias con nombre de SQL Server usan puertos dinámicos para las conexiones al motor de base de datos. Cuando use una instancia con nombre, configure manualmente el puerto estático.

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> Nota 4: Demonio FTP trivial (TFTP)

El servicio de sistema Demonio FTP Trivial (TFTP) no necesita un nombre de usuario o una contraseña, y es una parte integral de los Servicios de implementación de Windows (WDS). El servicio Demonio FTP Trivial implementa la compatibilidad con el protocolo TFTP definido por las siguientes RFC:  

- RFC 1350: TFTP  

- RFC 2347: extensión de opción  

- RFC 2348: opción de tamaño de bloque  

- RFC 2349: opciones de tamaño de transferencia e intervalo de tiempo de espera  

TFTP está diseñado para admitir entornos de arranque sin disco. Los demonios TFTP escuchan en el puerto UDP 69 pero responden desde un puerto alto asignado dinámicamente. Si habilita este puerto, al servicio TFTP puede recibir solicitudes TFTP entrantes, pero el servidor seleccionado no puede responder a esas solicitudes. No se puede habilitar el servidor seleccionado para que responda a solicitudes TFTP entrantes a menos que configure el servidor TFTP para responder desde el puerto 69.  

El punto de distribución habilitado con PXE y el cliente en Windows PE seleccionan puertos altos asignados dinámicamente para las transferencias de TFTP. Microsoft define estos puertos entre el 49152 y el 65535. Para más información, vea [Introducción al servicio y requisitos del puerto de red para Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).

Sin embargo, durante el arranque de PXE real, la tarjeta de red del dispositivo selecciona el puerto alto asignado dinámicamente que usa durante la transferencia TFTP. La tarjeta de red del dispositivo no está enlazada a los puertos altos asignados dinámicamente definidos por Microsoft. Solo está enlazada a los puertos definidos en RFC 1350. Este puerto puede ser cualquiera entre el 0 y el 65535. Para obtener más información sobre qué puertos altos asignados dinámicamente usan la tarjeta de red, póngase en contacto con el fabricante del hardware del dispositivo.

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> Nota 5: Comunicación entre el servidor de sitio y los sistemas de sitio

De forma predeterminada, la comunicación entre el servidor de sitio y los sistemas de sitio es bidireccional. El servidor de sitio inicia la comunicación para configurar el sistema de sitio y, después, la mayoría de los sistemas de sitio se conectan al servidor de sitio para enviar información de estado. Los puntos de servicios de informes y los puntos de distribución no envían información de estado. Si selecciona **Requerir al servidor de sitio iniciar conexiones a este sistema de sitio** en las propiedades del sistema de sitio después de instalarlo, el sistema de sitio no iniciará la comunicación con el servidor de sitio. En su lugar, el servidor de sitio inicia la comunicación. Usa la cuenta de instalación del sistema de sitio para la autenticación con el servidor de sistema de sitio.  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> Nota 6: Puertos dinámicos

Estos puertos usan una serie de números de puerto que está definidos por la versión del SO. Estos puertos también se conocen como puertos efímeros. Para obtener más información acerca de los intervalos de puertos predeterminados, consulte [Introducción al servicio y requisitos del puerto de red para el sistema Windows Server](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Listas adicionales de puertos  

En las secciones siguientes se proporciona información adicional sobre los puertos que usa Configuration Manager.

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Cliente a recursos compartidos de servidor

Los clientes utilizan Bloque de mensajes del servidor (SMB) cada vez que se conectan a recursos compartidos UNC. Por ejemplo:

- Instalación manual de cliente que especifica la propiedad de la línea de comandos CCMSetup.exe **/source:** .  

- Clientes de Endpoint Protection que descargan archivos de definición de una ruta de acceso UNC.

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|Bloque de mensajes del servidor (SMB)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Conexiones a Microsoft SQL Server

Para la comunicación con el motor de base de datos de SQL Server y para la replicación entre sitios, puede utilizar el puerto de SQL Server predeterminado o especificar puertos personalizados:  

- Uso de las comunicaciones entre sitios:  

  - SQL Server Service Broker, que usa de forma predeterminada el puerto TCP 4022.  

  - Servicio SQL Server, que usa de forma predeterminada el puerto TCP 1433.  

- La comunicación entre sitios entre el motor de base de datos de SQL Server y varios roles de sistema de sitio de Configuration Manager tienen el puerto TCP 1433 como predeterminado.  

- Configuration Manager usa los mismos puertos y protocolos para comunicarse con cada réplica de grupo de disponibilidad de SQL que hospeda la base de datos del sitio que si la réplica fuera una instancia independiente de SQL Server.

Cuando use Azure y la base de datos del sitio esté detrás de un equilibrador de carga interno o externo, configure los siguientes componentes:

- Excepciones del firewall en cada réplica
- Reglas de equilibrio de carga

Configure los puertos siguientes:

- SQL a través de TCP: TCP 1433
- SQL Server Service Broker: TCP 4022
- Bloque de mensajes del servidor (SMB): TCP 445
- Asignador de extremos de RPC: TCP 135

> [!WARNING]  
> Configuration Manager no admite los puertos dinámicos. De forma predeterminada, las instancias con nombre de SQL Server usan puertos dinámicos para las conexiones al motor de base de datos. Cuando use una instancia con nombre, configure manualmente el puerto estático para la comunicación entre sitios.  

Los siguientes roles de sistema de sitio se comunican directamente con la base de datos de SQL Server:  

- Punto de servicio web del catálogo de aplicaciones  

- Rol de punto de registro de certificado  

- Rol de punto de inscripción  

- Punto de administración  

- Servidor de sitio  

- Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

- Proveedor de SMS  

- SQL Server --> SQL Server  

Si un SQL Server hospeda una base de datos de más de un sitio, cada base de datos debe usar una instancia independiente de SQL Server. Configure cada instancia con un conjunto de puertos único.  

Si habilita un firewall basado en host en SQL Server, configúrelo para que permita los puertos correctos. También puede configurar los firewalls de red entre los equipos que se comunican con SQL Server.  

Para obtener un ejemplo de cómo configurar SQL Server para usar un determinado puerto, consulte [Configurar un servidor para que escuche en un puerto TCP específico](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> Detección y publicación

Configuration Manager usa los siguientes puertos para la detección y la publicación de información de sitios:

- Protocolo ligero de acceso a directorios (LDAP): 389
- LDAP seguro (LDAPS, para firmar y enlazar): 636
- LDAP de catálogo global: 3268
- Asignador de extremos de RPC: 135
- RPC: puertos TCP altos asignados dinámicamente
- TCP: 1024: 5000
- TCP:  49152: 65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Conexiones externas establecidas por Configuration Manager

Los clientes o sistemas de sitio de Configuration Manager en el entorno local pueden establecer las siguientes conexiones externas:  

- [Punto de sincronización de Asset Intelligence --&gt; Microsoft](#BKMK_PortsAI)  

- [Punto de Endpoint Protection --&gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

- [Cliente --&gt; Controlador de dominio del catálogo global](#BKMK_PortsClient-GCDC)  

- [Consola de Configuration Manager --&gt; Internet](#BKMK_PortsConsole-Internet)  

- [Punto de administración --&gt; Controlador de dominio](#BKMK_PortsMP-DC)  

- [Servidor de sitio --&gt; Controlador de dominio](#BKMK_PortsSite-DC)  

- [Servidor de sitio &lt; --&gt; Entidad de certificación emisora (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [Punto de actualización de software --&gt; Internet](#BKMK_PortsSUP-Internet)  

- [Punto de actualización de software --&gt; Servidor WSUS ascendente](#BKMK_PortsSUP-WSUS)  

- [Punto de conexión del servicio --> Azure](#bkmk_scp-cmg)  

- [Punto de conexión de CMG --> Servicio en la nube de CMG](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Requisitos de instalación de sistemas de sitio que admiten clientes basados en Internet

> [!Note]  
> Esta sección solo se aplica a la administración de clientes basados en Internet (IBCM), pero no a la puerta de enlace de administración en la nube. Para más información, vea [Administrar clientes en Internet](../../clients/manage/manage-clients-internet.md).  

Los puntos de administración y de distribución basados en Internet que admiten clientes basados en Internet, el punto de actualización de software y el punto de estado de reserva usan los puertos siguientes para la instalación y la reparación:  

- Servidor de sitio --> sistema de sitio: Asignador de extremos RPC con los puertos UDP y TCP 135.  

- Servidor de sitio --> sistema de sitio: Puertos TCP dinámicos de RPC  

- Servidor de sitio &lt; --> sistema de sitio: Bloques de mensajes de servidor (SMB) mediante el puerto TCP 445

Las instalaciones de aplicación y paquete en puntos de distribución requieren los siguientes puertos RPC:  

- Servidor de sitio --> Punto de distribución: Asignador de extremos RPC con los puertos UDP y TCP 135

- Servidor de sitio --> Punto de distribución: Puertos TCP dinámicos de RPC  

Utilice IPsec para proteger el tráfico entre el servidor de sitio y los sistemas de sitio. Si debe restringir los puertos dinámicos que se usan con RPC, puede utilizar la herramienta de configuración de RPC de Microsoft (rpccfg.exe). Use la herramienta para configurar un conjunto limitado de puertos para estos paquetes RPC. Para obtener más información, vea [Configuración de RPC para usar determinados puertos y cómo asegurar esos puertos con IPsec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]
> Antes de instalar estos sistemas de sitio, asegúrese de que el servicio de registro remoto se ejecuta en el servidor de sistema de sitio y que ha especificado una cuenta de instalación del sistema de sitio si el sistema de sitio está en un bosque de Active Directory sin una relación de confianza. Por ejemplo, se usa el servicio de registro remoto en servidores que ejecutan sistemas de sitio como puntos de distribución (tanto de extracción como estándar), servidores SQL remotos y el catálogo de aplicaciones.

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Puertos usados por la instalación de cliente de Configuration Manager

Los puertos que Configuration Manager usa durante la instalación de cliente dependen del método de implementación.

- Para consultar una lista de los puertos usados para cada método de implementación de cliente, vea [Puertos usados durante la implementación de cliente de Configuration Manager](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment).  

- Para obtener más información sobre cómo configurar Firewall de Windows en el cliente para la instalación de cliente y la comunicación posterior a la instalación, vea [Configuración de puertos y Firewall de Windows para clientes](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Puertos usados por la migración

El servidor de sitio que ejecuta la migración usa varios puertos para conectarse a los sitios aplicables en la jerarquía de origen. Para más información, vea [Configuraciones necesarias para la migración](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations).  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Puertos usados por Windows Server

En la tabla siguiente se incluyen algunos de los puertos clave que usa Windows Server.

|Descripción|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 y 68|--|  
|Resolución de nombres NetBIOS|137|--|  
|Servicio de datagramas de NetBIOS|138|--|  
|Servicio de sesión de NetBIOS|--|139|  
|Autenticación de Kerberos|--|88|

Vea los siguientes artículos para más información:

- [Introducción a los servicios y requisitos de puerto de red para el sistema Windows Server](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

- [Cómo configurar un firewall para dominios y confianzas](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)