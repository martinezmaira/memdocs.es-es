---
title: Administración de cliente basada en Internet
titleSuffix: Configuration Manager
description: Cree un plan para administrar los clientes basados en Internet en Configuration Manager.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587220"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Planificación de la administración de cliente basada en Internet en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la administración de cliente basada en Internet (IBCM) para administrar clientes de Configuration Manager cuando no estén conectados a la red interna. Ventajas de usar IBCM:

- Control completo de los servidores y los roles que proporcionan el servicio.
- No hay dependencia de servicios en la nube.
- Es posible que no se necesite una red privada virtual (VPN).
- Todos los costos están asociados al servicio local.

Debido a los mayores requisitos de seguridad de la administración de equipos cliente en una red pública, IBCM requiere el uso de certificados PKI. Esta configuración garantiza que las conexiones se autentiquen mediante una entidad de certificación independiente. Cuando los clientes de IBCM y los servidores de sitio envían datos, están cifrados y seguros.  

## <a name="client-communications"></a>Comunicaciones cliente

Los roles de sistema de sitio siguientes en los sitios primarios admiten conexiones de clientes que se encuentran en ubicaciones que no son de confianza:

> [!NOTE]
> Mientras que IBCM se centra principalmente en el escenario basado en Internet, los mismos comportamientos se aplican a los clientes de un bosque de Active Directory que no es de confianza. Los sitios secundarios no admiten conexiones de cliente desde ubicaciones que no son de confianza.

- Punto de registro de certificados para el módulo de directivas de Configuration Manager (NDES)

- Punto de distribución

- Punto de distribución basado en la nube

- Punto de proxy de inscripción

- Punto de estado de reserva

- Punto de administración

- Punto de actualización de software

> [!NOTE]
> La compatibilidad de los roles de catálogo de aplicaciones ha finalizado con la versión 1910. Para más información, consulte [Eliminación del catálogo de aplicaciones](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). En el caso de las versiones 1906 de Configuration Manager y anteriores que todavía se admiten, el punto de sitios web del catálogo de aplicaciones puede aceptar conexiones de clientes basados en Internet.

### <a name="about-internet-facing-site-systems"></a>Sobre los sistemas de sitio con conexión a Internet

No es necesario tener una relación de confianza entre el bosque de un cliente y el de un servidor de sistema de sitio. Pero cuando el bosque que contiene un sistema de sitio con conexión a Internet confía en el bosque que contiene las cuentas de usuario, esta configuración admite directivas basadas en usuario para los dispositivos en Internet si se habilita la configuración de cliente de **directiva de cliente** **Habilitar solicitudes de directiva de usuario de clientes de Internet**.

Por ejemplo, las configuraciones siguientes ilustran cuándo IBCM admite directivas de usuario para dispositivos en Internet:

- El punto de administración basado en Internet se encuentra en la red perimetral. Esa red también tiene un controlador de dominio de solo lectura para autenticar al usuario. Un firewall entre el perímetro y las redes internas permite paquetes de Active Directory.

- La cuenta de usuario está en el bosque basado en intranet. El punto de administración basado en Internet se encuentra en el bosque basado en el perímetro. El bosque perimetral confía en el bosque interno. Un firewall entre el perímetro y las redes internas permite los paquetes de autenticación.

- La cuenta de usuario y el punto de administración basado en Internet están en el bosque basado en la intranet. El punto de administración se publica en Internet con un servidor proxy web.

### <a name="use-a-web-proxy-server"></a>Uso de un servidor proxy web

Puede colocar sistemas de sitio basados en Internet en la intranet al publicarlos en Internet con un servidor proxy web. Configure estos sistemas de sitio para conexiones de cliente solo desde Internet, o bien conexiones de cliente desde Internet e intranet. Cuando se usa un servidor proxy web, se puede configurar para protocolo de puente de Capa de sockets seguros (SSL) a SSL, o bien protocolo de túnel SSL.

#### <a name="ssl-bridging-to-ssl"></a>Protocolo de puente SSL a SSL

El protocolo de puente SSL a SSL es la configuración recomendada y más segura, ya que usa terminación SSL con autenticación. Autentica los equipos cliente con la autenticación de equipo. Los dispositivos móviles que se inscriben con Configuration Manager no son compatibles con el protocolo de puente SSL.

Con la terminación SSL en el proxy, inspecciona los paquetes desde Internet antes de reenviarlos a la red interna. El proxy autentica la conexión desde el cliente, la termina y, después, abre una conexión autenticada nueva a los sistemas de sitio basados en Internet. Cuando los clientes de Configuration Manager usan un proxy, el cliente contiene de forma segura su identidad (GUID) en la carga de paquete. El punto de administración no tiene en cuenta que el proxy es el cliente. Configuration Manager no admite el protocolo de puente con HTTP a HTTPS o de HTTPS a HTTP.

> [!NOTE]
> Configuration Manager no admite el ajuste de opciones de configuración de puente de SSL de terceros. Por ejemplo, Citrix Netscaler o F5 BIG-IP. Póngase en contacto con su proveedor del dispositivo para configurarlo para su uso con Configuration Manager.

#### <a name="tunneling"></a>Protocolo de túnel

Si el servidor proxy web no es compatible con los requisitos del protocolo de puente SSL, Configuration Manager también admite el protocolo de túnel SSL. También puede usar el protocolo de túnel SSL para admitir dispositivos móviles que se inscriben con Configuration Manager. Es una opción menos segura porque el proxy reenvía los paquetes SSL desde Internet a los sistemas de sitio sin terminación SSL. El proxy no inspecciona si los paquetes incluyen contenido malintencionado. Cuando se utiliza el protocolo de túnel SSL, no hay ningún requisito de certificado para el servidor proxy web.

## <a name="plan-for-internet-based-clients"></a>Planeación de clientes basados en Internet

Decida si quiere configurar los clientes basados en Internet para la administración en la intranet e Internet, o bien solo para Internet. Solo puede configurar esta opción de administración durante la instalación del cliente. Para cambiarla después, vuelva a instalar el cliente.

> [!NOTE]
> Si configura un punto de administración para admitir clientes basados en Internet, los clientes que se conectan a este punto de administración serán compatibles con Internet cuando actualicen su lista de puntos de administración disponibles.
>
> No es necesario restringir la configuración de administración de cliente solamente a Internet. También se puede usar en la intranet.

Los clientes que configure para la administración de cliente basada únicamente en Internet solo se comunican con los sistemas de sitio que configure para conexiones de cliente de Internet. Use esta configuración en los escenarios siguientes:

- Para equipos que sabe que nunca se conectarán a la intranet. Por ejemplo, equipos de punto de venta en ubicaciones remotas.
- Para restringir la comunicación de cliente solo a HTTPS. Por ejemplo, para admitir firewall y directivas de seguridad restringidas.
- Cuando se instalan sistemas de sitio basados en Internet en una red perimetral y se quiere administrar estos servidores como clientes de Configuration Manager.

> [!NOTE]
> Si quiere administrar clientes de grupo de trabajo en Internet, instálelos como solo de Internet.
>
> Cuando se configura un dispositivo móvil para usar un punto de administración basado en Internet, se configura de forma automática como solo de Internet.

Puede configurar otros clientes para la administración de clientes de Internet e intranet. Cuando detectan un cambio de red, cambian automáticamente entre IBCM y administración de cliente de intranet. Si estos clientes pueden encontrar y conectarse a un punto de administración que admite conexiones de cliente en la intranet, se administrarán como clientes de intranet. Los clientes de intranet tienen todas las funciones de Configuration Manager. Si los clientes no pueden encontrar ni conectarse a un punto de administración que admita conexiones de cliente en la intranet, intentarán conectarse a un punto de administración basado en Internet. Si esta acción se realiza correctamente, estos clientes se administran mediante los sistemas de sitio basados en Internet en su sitio asignado.

La ventaja del cambio automático es que los clientes pueden usar todas las características cuando se conectan a la intranet y reciben la administración esencial cuando están en Internet. La descarga de contenido que comienza en Internet se puede reanudar sin problemas en la intranet y viceversa.

## <a name="prerequisites"></a>Requisitos previos

IBCM en Configuration Manager tiene las dependencias siguientes:

- Los clientes necesitan una conexión a Internet. Configuration Manager usa la conexión a Internet existente del dispositivo. Los dispositivos móviles deben tener una conexión directa a Internet. Los equipos cliente completos pueden tener una conexión directa a Internet o conectarse mediante un servidor proxy web.

- Los sistemas de sitio que admiten IBCM requieren una conexión a Internet y deben estar en un dominio de Active Directory. Los sistemas de sitio basados en Internet no requieren una relación de confianza con el bosque de Active Directory del servidor del sitio. Pero cuando el punto de administración basado en Internet puede autenticar al usuario mediante la autenticación de Windows, admite directivas de usuario. Si se produce un error en la autenticación de Windows, solo admite directivas de dispositivo.

    > [!NOTE]
    > Para admitir directivas de usuario, habilite también la siguiente configuración de cliente en el grupo **Directiva de cliente**:
    >
    > - **Habilitar sondeo de directiva de usuario en clientes**
    > - **Habilitar solicitudes de directiva de usuario de clientes de Internet**  

- Una infraestructura de clave pública (PKI) para implementar y administrar los certificados necesarios para los clientes basados en Internet y los servidores de sistema de sitio. Para obtener más información, vea [Requisitos de certificados PKI](../../plan-design/network/pki-certificate-requirements.md).

- Registre entradas de host DNS público para los nombres de dominio completos (FQDN) de Internet de los sistemas de sitio que admiten IBCM.

### <a name="client-communication-requirements"></a>Requisitos de comunicación de cliente

Los firewalls o servidores proxy que intervienen deben permitir la comunicación de cliente para los sistemas de sitio basados en Internet:

- Compatibilidad con HTTP 1.1  

- Permitir tipo de contenido HTTP de datos adjuntos de MIME de varias partes (multipart/mixed y application/octet-stream)  

#### <a name="verbs"></a>Verbos

Permita los verbos siguientes para los roles del servidor de sistema de sitio basados en Internet:

| Rol | Verbos |
|------|-------|
| Punto de administración | - HEAD<br>- CCM_POST<br>- BITS_POST<br>- GET<br>- PROPFIND |
| Punto de distribución | - HEAD<br>- GET<br>- PROPFIND |
| Punto de estado de reserva | POST |
| Punto de sitios web del catálogo de aplicaciones | -POST<br>-GET |

#### <a name="http-headers"></a>Encabezados HTTP

Permita los encabezados HTTP siguientes para los roles del servidor de sistema de sitio basados en Internet:

| Rol | Encabezados HTTP |
|------|--------------|
| Punto de administración | - Range:<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| Punto de distribución | Intervalo: |

Para obtener información sobre requisitos de comunicación similares cuando se usa el punto de actualización de software para conexiones de cliente de Internet, vea la documentación de Windows Server Update Services (WSUS).

## <a name="unsupported-features"></a>Características no admitidas

No todas las funciones de administración de cliente son apropiadas para Internet. Configuration Manager no admite algunas características para los clientes de Internet. Estas características no admitidas normalmente se basan en Active Directory Domain Services o no son apropiadas para una red pública.

No se admiten las características siguientes cuando los clientes se administran en Internet con IBCM:

- Implementación de cliente a través de Internet, como la inserción de cliente y la implementación de cliente basada en actualización de software. Use la instalación de cliente manual.

- Asignación automática de sitio

- Wake on LAN

- Implementación del sistema operativo. Pero puede implementar secuencias de tareas que no implementan un sistema operativo.

- Control remoto

- Implementación de software para los usuarios. Esta característica se basa en el catálogo de aplicaciones, que está en desuso.

- Itinerancia de cliente. La movilidad permite a los clientes buscar siempre los puntos de distribución más cercanos para descargar contenido. Los clientes seleccionan de manera no determinista uno de los sistemas de sitio basados en Internet, con independencia del ancho de banda o de la ubicación física.

Al configurar un punto de actualización de software para aceptar conexiones de Internet, los clientes basados en Internet siempre examinan este punto de actualización de software para determinar las actualizaciones de software que son necesarias. Cuando estos clientes se encuentran en Internet, primero intentan descargar las actualizaciones de software de Microsoft Update, en lugar de desde un punto de distribución basado en Internet. Si se produce un error en este comportamiento, intentan descargar las actualizaciones de software necesarias desde un punto de distribución basado en Internet.

> [!TIP]
> El cliente de Configuration Manager determina automáticamente si está en la intranet o en Internet. Si el cliente se puede contactar con un controlador de dominio o un punto de administración local, establece su tipo de conexión en "Actualmente *intranet*". De lo contrario, cambia a "Actualmente *Internet*" y se comunica con los sistemas de sitio asignados a su sitio.
