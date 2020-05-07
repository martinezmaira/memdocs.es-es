---
title: Comunicaciones entre puntos de conexión
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo se comunican los componentes y sistemas de sitio de Configuration Manager a través de una red.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f60d268e1f9bfad9c062041e810be2092da5508
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587241"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Comunicaciones entre puntos de conexión en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se describe cómo se comunican los clientes y sistemas de sitio de Configuration Manager a través de la red. Se incluyen las secciones siguientes:  

- [Comunicaciones entre sistemas de sitio de un sitio](#Planning_Intra-site_Com)  
  - [Servidor de sitio a punto de distribución](#bkmk_site2dp)  

- [Comunicaciones desde los clientes a los sistemas de sitio y servicios](#Planning_Client_to_Site_System)  
  - [Comunicaciones entre cliente y punto de administración](#bkmk_client2mp)  
  - [Comunicaciones entre cliente y punto de distribución](#bkmk_client2dp)  
  - [Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza](#BKMK_clientspan)  

- [Comunicaciones entre bosques de Active Directory](#Plan_Com_X-Forest)  
  - [Compatibilidad del bosque del servidor de sitio con equipos de dominio en un bosque que no es de confianza](#bkmk_noforesttrust)  
  - [Compatibilidad con los equipos de un grupo de trabajo](#bkmk_workgroup)  
  - [Escenarios para admitir un sitio o una jerarquía que abarca varios dominios y bosques](#bkmk_span)  

## <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a> Comunicaciones entre sistemas de sitio de un sitio  

Cuando los sistemas de sitio o los componentes de Configuration Manager se comunican a través de la red con otros sistemas de sitio u otros componentes del sitio, usan uno de los protocolos siguientes, según la configuración del sitio:  

- Bloque de mensajes del servidor (SMB)  

- HTTP  

- HTTPS  

Con la excepción de la comunicación desde el servidor de sitio a un punto de distribución, las comunicaciones entre los servidores de un sitio se pueden producir en cualquier momento. Estas comunicaciones no usan mecanismos para controlar el ancho de banda de red. Como no es posible controlar la comunicación entre los sistemas de sitio, asegúrese de instalar servidores de sistema de sitio en ubicaciones que cuenten con redes rápidas y bien conectadas.  

### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a> Servidor de sitio a punto de distribución

Para administrar la transferencia de contenido desde el servidor de sitio a los puntos de distribución, use las estrategias siguientes:  

- Configurar el punto de distribución para el control de ancho de banda de red y la programación. Estos controles son similares a las configuraciones que usan las direcciones entre sitios. Use esta configuración en lugar de instalar otro sitio de Configuration Manager cuando la transferencia de contenido a ubicaciones de red remotas sea la principal consideración de ancho de banda.  

- Es posible instalar un punto de distribución como un punto de distribución preconfigurado. Un punto de distribución preconfigurado le permite utilizar el contenido que se coloca manualmente en el servidor de punto de distribución y elimina el requisito de transferir archivos de contenido a través de la red.  

Para más información, vea [Administración del ancho de banda de red para la administración de contenido](manage-network-bandwidth.md).

## <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a> Comunicaciones desde los clientes a los sistemas de sitio y servicios

Los clientes inician comunicaciones con roles de sistema de sitio, con Servicios de dominio de Active Directory y con servicios en línea. A fin de permitir estas comunicaciones, los firewalls deben permitir el tráfico de red entre los clientes y el extremo de sus comunicaciones. Para obtener más información sobre los puertos y protocolos que los clientes usan al comunicarse con estos puntos de conexión, vea [Puertos usados en Configuration Manager](ports.md).  

Para que un cliente se pueda comunicar con un rol de sistema de sitio, el cliente usa la ubicación del servicio para buscar un rol que admita el protocolo del cliente (HTTP o HTTPS). De forma predeterminada, los clientes usan el método más seguro que tengan a su disposición. Para obtener más información, vea [Más información sobre cómo los clientes buscan servicios y recursos de sitio](understand-how-clients-find-site-resources-and-services.md).  

Para usar HTTPS, configure una de las opciones siguientes:  

- Use una infraestructura de clave pública (PKI) e instale certificados PKI en los clientes y servidores. Para obtener información sobre el uso de certificados, vea [Requisitos de certificados PKI](../network/pki-certificate-requirements.md).  

- A partir de la versión 1806, configure el sitio para **Usar los certificados generados por Configuration Manager para sistemas de sitios HTTP**. Para obtener más información, vea [HTTP mejorado](enhanced-http.md).  

Cuando se implementa un rol de sistema de sitio que usa Internet Information Services (IIS) y que admite la comunicación desde clientes, es necesario especificar si los clientes se conectan al sistema de sitio mediante HTTP o HTTPS. Si utiliza HTTP, también debe tener en cuenta las opciones de firma y cifrado. Para obtener más información, vea [Planear la firma y el cifrado](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption).  

### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a> Comunicaciones entre cliente y punto de administración

Existen dos fases cuando un cliente se comunica con un punto de administración: autenticación (transporte) y autorización (mensaje). Este proceso varía en función de los factores siguientes:

- Configuración del sitio: Solo HTTPS, permite HTTP o HTTPS, o bien permite HTTP o HTTPS con HTTP mejorado habilitado
- Configuración del punto de administración: HTTPS o HTTP
- Identidad de dispositivo para escenarios centrados en el dispositivo
- Identidad de usuario para escenarios centrados en el usuario

Use la tabla siguiente para obtener información sobre cómo funciona este proceso:  

| Tipo de PA  | Autenticación de cliente  | Autorización de cliente<br>Identidad del dispositivo  | Autorización de cliente<br>Identidad del usuario  |
|----------|---------|---------|---------|
| HTTP     | Anónima<br>Con HTTP mejorado, el sitio comprueba el token de *usuario* o *dispositivo* de Azure AD. | Solicitud de ubicación: Anónima<br>Paquete de cliente: Anónima<br>Registro, mediante uno de los métodos siguientes para demostrar la identidad del dispositivo:<br> - Anónimo (aprobación manual)<br> - Autenticación integrada en Windows<br> - Token de *dispositivo* de Azure AD (HTTP mejorado)<br>Después del registro, el cliente usa la firma de mensajes para demostrar la identidad del dispositivo | Para los escenarios centrados en el usuario, mediante uno de los métodos siguientes para demostrar la identidad del usuario:<br> - Autenticación integrada en Windows<br> - Token de *usuario* de Azure AD (HTTP mejorado) |
| HTTPS    | Mediante uno de los métodos siguientes:<br> - Certificado PKI<br> - Autenticación integrada en Windows<br> - Token de *usuario* o *dispositivo* de Azure AD | Solicitud de ubicación: Anónima<br>Paquete de cliente: Anónima<br>Registro, mediante uno de los métodos siguientes para demostrar la identidad del dispositivo:<br> - Anónimo (aprobación manual)<br> - Autenticación integrada en Windows<br> - Certificado PKI<br> - Token de *usuario* o *dispositivo* de Azure AD<br>Después del registro, el cliente usa la firma de mensajes para demostrar la identidad del dispositivo | Para los escenarios centrados en el usuario, mediante uno de los métodos siguientes para demostrar la identidad del usuario:<br> - Autenticación integrada en Windows<br> - Token de *usuario* de Azure AD |

> [!Tip]  
> Para obtener más información sobre la configuración del punto de administración para otros tipos de identidad de dispositivo y con la puerta de enlace de administración en la nube, vea [Habilitar un punto de administración para HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a> Comunicaciones entre cliente y punto de distribución

Cuando un cliente se comunica con un punto de distribución, solo necesita autenticarse antes de descargar el contenido. Use la tabla siguiente para obtener información sobre cómo funciona este proceso:

| Tipo de PD  | Autenticación de cliente  |
|----------|---------|
| HTTP     | - Anónima, si permite<br>- Autenticación integrada en Windows con la cuenta de equipo o la cuenta de acceso a la red<br> - Token de acceso de contenido (HTTP mejorado) |
| HTTPS    | - Certificado PKI<br> - Autenticación integrada en Windows con la cuenta de equipo o la cuenta de acceso a la red<br> - Token de acceso de contenido |

### <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a> Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza

Vea los siguientes artículos para más información:

- [Planear puerta de enlace de administración en la nube](../..//clients/manage/cmg/plan-cloud-management-gateway.md)

- [Planeamiento de la administración de clientes basada en Internet](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a> Comunicaciones entre bosques de Active Directory  

Configuration Manager es compatible con sitios y jerarquías que se distribuyen por bosques de Active Directory. También admite equipos de dominio que no están en el mismo bosque de Active Directory que el servidor de sitio, y equipos que están en grupos de trabajo.  

### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a> Compatibilidad del bosque del servidor de sitio con equipos de dominio en un bosque que no es de confianza

- Instalar roles de sistema de sitio en ese bosque que no es de confianza, con la opción para publicar información del sitio en ese bosque de Active Directory.  

- Administrar estos equipos como si fueran equipos de grupo de trabajo  

Cuando se instalan servidores de sistema de sitio en un bosque de Active Directory que no es de confianza, la comunicación entre cliente y servidor desde los clientes de dicho bosque se mantiene en ese bosque y Configuration Manager puede autenticar el equipo mediante Kerberos. Cuando se publica información del sitio en el bosque del cliente, los clientes se benefician de la posibilidad de recuperar información del sitio, como una lista de los puntos de administración disponibles, desde su bosque de Active Directory, en lugar de tener que descargar esta información desde su punto de administración asignado.  

> [!NOTE]  
> Si quiere administrar dispositivos que están en Internet, puede instalar roles de sistema de sitio basados en Internet en la red perimetral cuando los servidores de sistema de sitio estén en un bosque de Active Directory. Este escenario no requiere una confianza bidireccional entre la red perimetral y el bosque del servidor de sitio.  

### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a> Compatibilidad con los equipos de un grupo de trabajo  

- Aprobar manualmente los equipos del grupo de trabajo cuando usen conexiones de cliente HTTP en roles de sistema de sitio. Configuration Manager no puede autenticar estos equipos mediante Kerberos.  

- Configure los clientes del grupo de trabajo para usar la cuenta de acceso a la red para que estos equipos puedan recuperar contenido de los puntos de distribución.  

- Proporcione un mecanismo alternativo para que los clientes del grupo de trabajo puedan buscar los puntos de administración. Use publicación en DNS, WINS, o bien asigne directamente un punto de administración. Estos clientes no pueden recuperar la información de sitio de Active Directory Domain Services.  

Vea los siguientes artículos para más información:  

- [Administrar registros en conflicto](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

- [Cuenta de acceso a la red](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [Cómo instalar clientes de Configuration Manager en equipos de grupo de trabajo](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> Escenarios para admitir un sitio o una jerarquía que abarca varios dominios y bosques  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Escenario 1: Comunicación entre sitios en una jerarquía que abarca bosques

Este escenario requiere una confianza de bosque bidireccional que admita la autenticación Kerberos.  Si no dispone de una confianza de bosque bidireccional que admita la autenticación Kerberos, Configuration Manager no admitirá un sitio secundario en el bosque remoto.  

Configuration Manager admite la instalación de un sitio secundario en un bosque remoto que tenga la confianza bidireccional necesaria con el bosque del sitio primario. Por ejemplo, puede colocar un sitio secundario en un bosque diferente al del sitio primario principal siempre y cuando exista la confianza necesaria.  

> [!NOTE]  
> Un sitio secundario puede ser un sitio primario (donde el sitio de administración central es el sitio principal), o bien un sitio secundario.  

La comunicación entre sitios de Configuration Manager usa replicación de base de datos y transferencias basadas en archivos. Cuando se instala un sitio, se debe especificar una cuenta con la que instalar el sitio en el servidor designado. Esta cuenta también establece y mantiene la comunicación entre sitios. Una vez que el sitio se instala correctamente e inicia las transferencias basadas en archivos y la replicación de base de datos, no es necesario configurar nada más para la comunicación con el sitio.  

Cuando existe una confianza de bosque bidireccional, Configuration Manager no exige ningún paso de configuración adicional.  

De forma predeterminada, al instalar un sitio secundario nuevo, Configuration Manager configura los componentes siguientes:  

- Una ruta de replicación basada en archivos entre sitios en cada sitio que use la cuenta de equipo del servidor de sitio. Configuration Manager agrega la cuenta de equipo de cada equipo al grupo **SMS_SiteToSiteConnection_&lt;código de sitio\>** en el equipo de destino.  

- Una replicación de base de datos entre el servidor SQL Server de cada sitio.  

También se establecen las configuraciones siguientes:  

- Los firewalls y dispositivos de red que intervienen deben permitir los paquetes de red que Configuration Manager necesita.  

- La resolución de nombres debe funcionar entre los bosques.  

- Para instalar un sitio o un rol de sistema de sitio, debe especificar una cuenta que tenga permisos de administrador local en el equipo especificado.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Escenario 2: La comunicación en un sitio que abarca bosques

Este escenario no requiere una confianza de bosque bidireccional.  

Los sitios primarios admiten la instalación de roles de sistema de sitio en equipos de bosques remotos.  

- El punto de servicio web del catálogo de aplicaciones es la única excepción.  Solo se admite en el mismo bosque que el servidor de sitio.  

- Cuando el rol de sistema de sitio acepta conexiones de Internet, por motivos de seguridad se recomienda instalar los roles de sistema de sitio en una ubicación donde los límites del bosque proporcionen protección al servidor de sitio (por ejemplo, en una red perimetral).  

Para instalar un rol de sistema de sitio en un equipo de un bosque que no es de confianza:  

- Especifique una **cuenta de instalación del sistema de sitio**, que el sitio usa para instalar el rol de sistema de sitio. (Esta cuenta debe tener privilegios administrativos locales para la conexión). Después, instale los roles de sistema de sitio en el equipo especificado.  

- Seleccione la opción de sistema de sitio **Requerir al servidor de sitio iniciar conexiones a este sistema de sitio**. Esta configuración requiere que el servidor del sitio establezca conexiones con el servidor de sistema de sitio para transferir datos. Esta configuración impide que el equipo en la ubicación que no es de confianza inicie contacto con el servidor de sitio que está dentro de la red de confianza. Estas conexiones usan la **cuenta de instalación del sistema de sitio**.  

Para usar un rol de sistema de sitio instalado en un bosque que no es de confianza, los firewalls deben permitir el tráfico de red aunque el servidor de sitio inicie la transferencia de datos.  

Además, los siguientes roles de sistema de sitio requieren acceso directo a la base de datos del sitio. Por tanto, los firewalls deben permitir el tráfico pertinente desde el bosque que no es de confianza hasta SQL Server en el sitio:  

- Punto de sincronización de Asset Intelligence  

- Punto de Endpoint Protection  

- Punto de inscripción  

- Punto de administración  

- Punto de servicio de informes  

- Punto de migración de estado  

Para obtener más información, vea [Puertos usados en Configuration Manager](ports.md).  

Es posible que tenga que configurar el acceso del punto de administración y punto de inscripción a la base de datos del sitio.

- De forma predeterminada, cuando se instalan estos roles, Configuration Manager configura la cuenta de equipo del nuevo servidor de sistema de sitio como la cuenta de conexión para el rol de sistema de sitio. Después agrega la cuenta al rol de base de datos de SQL Server apropiado.  

- Cuando instale estos roles de sistema de sitio en un dominio que no es de confianza, configure la cuenta de conexión del rol de sistema de sitio para que permita al rol obtener información de la base de datos.  

Si configura una cuenta de usuario de dominio para que sea la cuenta de conexión para estos roles de sistema de sitio, asegúrese de que la cuenta de usuario de dominio tenga acceso adecuado a la base de datos de SQL Server en ese sitio:  

- Punto de administración: **cuenta de conexión a la base de datos del punto de administración**  

- Punto de inscripción: **cuenta de conexión de punto de inscripción**  

Tenga en cuenta la siguiente información adicional cuando planee roles de sistema de sitio en otros bosques:  

- Si ejecuta Firewall de Windows, configure los perfiles de firewall aplicables para que pueda haber comunicación entre el servidor de base de datos de sitio y los equipos instalados con roles de sistema de sitio remoto.

- Cuando el punto de administración basado en Internet confía en el bosque que contiene las cuentas de usuario, se admiten las directivas de usuario. Cuando no existe confianza, solo se admiten las directivas de equipo.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Escenario 3: comunicación entre clientes y roles de sistema de sitio cuando los clientes no están en el mismo bosque de Active Directory que su servidor de sitio

Configuration Manager admite los escenarios siguientes para los clientes que no están en el mismo bosque que el servidor de sitio de su sitio:  

- Hay una confianza de bosque bidireccional entre el bosque del cliente y el bosque del servidor de sitio.  

- El servidor de rol de sistema de sitio se encuentra en el mismo bosque que el cliente.  

- El cliente está en un equipo de dominio que no tiene una confianza de bosque bidireccional con el servidor de sitio, y los roles de sistema de sitio no están instalados en el bosque del cliente.  

- El cliente está en un equipo de grupo de trabajo.  

Los clientes de un equipo unido a un dominio pueden usar Servicios de dominio de Active Directory para la ubicación del servicio cuando su sitio se publica en el bosque de Active Directory.  

Para publicar información del sitio en otro bosque de Active Directory:  

- Especificar el bosque y, a continuación, habilitar la publicación en ese bosque en el nodo **Bosques de Active Directory** del área de trabajo **Administración** .  

- Configurar cada sitio para publicar sus datos en Servicios de dominio de Active Directory. Esta configuración permite a los clientes de ese bosque recuperar información del sitio y buscar puntos de administración. Para los clientes que no pueden usar Active Directory Domain Services para la ubicación del servicio, se puede usar DNS, WINS, o bien el punto de administración asignado del cliente.  

#### <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a> Escenario 4: Colocar el conector de Exchange Server en un bosque remoto  

Para admitir este escenario, asegúrese de que la resolución de nombres funciona entre los bosques. Por ejemplo, configure los reenvíos de DNS. Al configurar el conector de Exchange Server, especifique el nombre de dominio completo de la intranet de Exchange Server. Para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="see-also"></a>Vea también

- [Planear la seguridad](../security/plan-for-security.md)  

- [Seguridad y privacidad para los clientes de Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
