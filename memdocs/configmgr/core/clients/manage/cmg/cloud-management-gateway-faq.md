---
title: PREGUNTAS MÁS FRECUENTES SOBRE CLOUD MANAGEMENT GATEWAY
titleSuffix: Configuration Manager
description: Use este artículo para responder a las preguntas más frecuentes sobre Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: ecc91168cc90af58c40903ea3d288eeaa82be7a0
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502245"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Preguntas más frecuentes sobre Cloud Management Gateway

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se responden las preguntas más frecuentes sobre Cloud Management Gateway. Para obtener más información, vea [Plan for cloud management gateway](plan-cloud-management-gateway.md) (Plan para Cloud Management Gateway).

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="what-certificates-do-i-need"></a>¿Qué certificados necesito?

Para obtener más información, vea [certificates for cloud management gateway](certificates-for-cloud-management-gateway.md) (Certificados para Cloud Management Gateway).

### <a name="do-i-need-azure-expressroute"></a>¿Necesito Microsoft Azure ExpressRoute?

No. [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) permite ampliar la red local a la nube de Microsoft. No se necesita ExpressRoute, ni otras conexiones de red virtual de este tipo, para Cloud Management Gateway de Configuration Manager. El diseño de Cloud Management Gateway permite a los clientes basados en Internet comunicarse a través del servicio de Azure con sistemas de sitio locales sin ninguna configuración de red adicional. Para obtener más información, vea [Plan for cloud management gateway (Plan para Cloud Management Gateway)](plan-cloud-management-gateway.md).

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>¿Es necesario mantener las máquinas virtuales de Azure?

No se requiere ningún mantenimiento. El diseño de Cloud Management Gateway usa PaaS (plataforma como servicio) de Azure. Mediante la suscripción que se proporciona, Configuration Manager crea las máquinas virtuales (VM) necesarias, el almacenamiento y las redes. Azure protege y actualiza la máquina virtual. Estas máquinas virtuales no forman parte del entorno local, como sucede con la infraestructura como servicio (IaaS). Cloud Management Gateway es una PaaS que extiende el entorno de Configuration Manager a la nube. Para más información, vea [Protección de implementaciones de PaaS](/azure/security/security-paas-deployments).

### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>¿Cómo aseguro la continuidad del servicio durante las actualizaciones del servicio?

Al escalar CMG para incluir dos o más instancias, automáticamente se beneficia de dominios de actualización en Azure. Consulte [Actualización de un servicio en la nube](/azure/cloud-services/cloud-services-update-azure-service).

### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Ya uso IBCM. Si agrego Cloud Management Gateway, ¿cómo se comportarán los clientes?

Si ya ha implementado la [administración de clientes basada en Internet](../plan-internet-based-client-management.md) (IBCM), también puede implementar Cloud Management Gateway. Los clientes reciben la directiva para ambos servicios. A medida que se mueven hacia Internet, seleccionan y usan de manera aleatoria uno de estos servicios basados en Internet.

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a>¿Las cuentas de usuario deben estar en el mismo inquilino de Azure AD que la suscripción que hospeda el servicio en la nube de CMG?
<!--SCCMDocs-pr issue #2873-->
No, puede implementar CMG en cualquier suscripción que pueda hospedar servicios en la nube de Azure.

Para comprender mejor los términos:

- El _inquilino_ es el directorio de las cuentas de usuario y de los registros de aplicaciones. Un inquilino puede tener varias suscripciones.
- Una _suscripción_ separa la facturación, los recursos y los servicios. Está asociada a un único inquilino.

Esta pregunta es habitual en los escenarios siguientes:  

- Cuando tiene diferentes entornos de prueba y de producción de Active Directory y de Azure AD, pero una única suscripción de hospedaje de Azure centralizada.

- Su uso de Azure ha crecido orgánicamente en equipos diferentes.

Si usa una implementación de Resource Manager, incorpore el inquilino de Azure AD asociado con la suscripción. Esta conexión permite a Configuration Manager autenticarse en Azure para crear, implementar y administrar la instancia de CMG.  

Si está usando una autenticación de Azure AD para los usuarios y dispositivos administrados a través de CMG, incorpore ese inquilino de Azure AD. Para obtener más información sobre los servicios de Azure para la administración en la nube, vea [Configuración de servicios de Azure](../../../servers/deploy/configure/azure-services-wizard.md). Al incorporar cada inquilino de Azure AD, una sola instancia de CMG puede proporcionar autenticación de Azure AD para varios inquilinos, independientemente de la ubicación del hospedaje.

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>Ejemplo 1: Un inquilino con varias suscripciones

Las identidades de usuario, los registros de dispositivos y los registros de aplicaciones se encuentran en el mismo inquilino. Puede elegir la suscripción que usará CMG. Puede implementar varios servicios de CMG desde un sitio en suscripciones independientes. El sitio tiene una relación de uno a uno con el inquilino. Decida qué suscripciones se van a usar por diversos motivos, por ejemplo, facturación o separación lógica.

#### <a name="example-2-multiple-tenants"></a>Ejemplo 2: Varios inquilinos

En otras palabras, el entorno tiene más de una instancia de Azure AD. Si necesita admitir identidades de usuario y de dispositivo en ambos inquilinos, debe asociar el sitio a cada inquilino. Este proceso requiere una cuenta administrativa de cada inquilino para crear los registros de aplicaciones en ese inquilino. Un sitio puede hospedar servicios de CMG en varios inquilinos. Puede crear una instancia de CMG en cualquier suscripción de la que se disponga en cualquiera de los inquilinos. Los dispositivos unidos a Azure AD o a Azure AD híbrido podrían usar una instancia de CMG.

Si las identidades de usuario y de dispositivo se encuentran en un inquilino, pero la suscripción de CMG se encuentra en otro, debe asociar el sitio a ambos inquilinos. Técnicamente, la aplicación cliente no es necesaria en el segundo inquilino que solo tiene el servicio CMG. La aplicación cliente solo proporciona autenticación de usuario y de dispositivo para los clientes que usan el servicio CMG.<!-- SCCMDocs#1902 -->

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>¿Cómo afecta CMG a mis clientes conectados a través de una VPN?

Los clientes móviles que se conectan a su entorno a través de una VPN normalmente se detectan como orientados a la intranet. Intentan conectarse a su infraestructura local, por ejemplo, a los puntos de administración y de distribución. Algunos clientes prefieren administrar estos clientes móviles con un servicio en la nube, incluso aunque se conecten a través de una VPN. A partir de la versión 1902, puede asociar CMG a un grupo de límites. Esta acción obliga a dichos clientes a no usar los sistemas de sitio en el entorno local. Para obtener más información, vea [Configuración de grupos de límites](setup-cloud-management-gateway.md#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Si habilito una instancia de CMG, ¿mis clientes solo se conectarán al punto de administración habilitado para CMG cuando estén conectados a la intranet?

Con el fin de proteger el tráfico confidencial enviado a través de CMG, configure un punto de administración HTTPS o use el protocolo HTTP mejorado.

Si decide implementar CMG y usar certificados PKI para la comunicación HTTPS en el punto de administración habilitado para CMG, seleccione la opción para **permitir los clientes solo de Internet** en las propiedades del punto de administración. Esta configuración garantiza que los clientes internos continuarán utilizando puntos de administración HTTP en su entorno.

Si opta por el protocolo HTTP mejorado, no es necesario que configure esta opción. Los clientes seguirán usando HTTP al comunicarse directamente con el punto de administración habilitado para CMG. Para obtener más información, vea [HTTP mejorado](../../../plan-design/hierarchy/enhanced-http.md).

### <a name="what-are-the-differences-with-client-authentication-between-azure-ad-and-certificates"></a>¿Cuáles son las diferencias con la autenticación de cliente entre Azure AD y los certificados?
<!-- MEMDocs#277 -->
Puede usar Azure AD o un [certificado de autenticación de cliente](certificates-for-cloud-management-gateway.md#bkmk_clientauth) para que los dispositivos se autentiquen en el servicio CMG.

Si administra clientes tradicionales de Windows con la identidad unida a un dominio de Active Directory, necesitan certificados PKI para proteger el canal de comunicación. Estos clientes pueden incluir Windows 8.1 y Windows 10. Puede usar todas las características compatibles con CMG, pero la distribución de software solo se limita a los dispositivos. Instale el cliente de Configuration Manager antes de que el dispositivo se desplace a Internet, o con la versión 2002 o posterior, use la autenticación de tokens.

También puede administrar clientes de Windows 10 con identidad moderna, tanto híbridos como unidos a un dominio en la nube pura con Azure AD. Los clientes usan Azure AD para la autenticación, en lugar de certificados PKI. Azure AD es más fácil de instalar, configurar y mantener que los sistemas PKI más complejos. Puede realizar las mismas actividades de administración más la distribución de software para el usuario. También permite métodos adicionales para instalar el cliente en un dispositivo remoto.

Microsoft recomienda conectar los dispositivos con Azure AD. Los dispositivos basados en Internet pueden usar Azure AD para autenticarse con Configuration Manager. También habilita los escenarios de usuario y dispositivo tanto si el dispositivo está usando Internet como si está conectado a la red interna. Para obtener más información, consulte [Instalar y registrar el cliente con la identidad de Azure AD](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="next-steps"></a>Pasos siguientes

- [Planear puerta de enlace de administración en la nube](plan-cloud-management-gateway.md)
- [Configurar puerta de enlace de administración en la nube](setup-cloud-management-gateway.md)
- [Certificados para la puerta de enlace de administración en la nube](certificates-for-cloud-management-gateway.md)
- [Seguridad y privacidad de la puerta de enlace de administración en la nube](security-and-privacy-for-cloud-management-gateway.md)
- [Números de tamaño y escala de System Center Configuration Manager](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
