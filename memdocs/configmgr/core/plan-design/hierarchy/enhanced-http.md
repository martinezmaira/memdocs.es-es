---
title: HTTP mejorado
titleSuffix: Configuration Manager
description: Use la autenticación moderna para proteger la comunicación de cliente sin necesidad de certificados PKI.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1a6ec98bd350eb0ac8643254f64a9480f156bb13
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2020
ms.locfileid: "86239766"
---
# <a name="enhanced-http"></a>HTTP mejorado

*Se aplica a: Configuration Manager (rama actual)*

<!--1356889,1358460-->

> [!Tip]  
> Esta característica se introdujo por primera vez en la versión 1806 como una [característica de versión preliminar](../../servers/manage/pre-release-features.md). A partir de la versión 1810, ya no es una característica de versión preliminar.  

Microsoft recomienda usar la comunicación HTTPS para todas las vías de comunicación de Configuration Manager, pero es un reto para algunos clientes debido a la sobrecarga de administración de los certificados PKI.

En la versión 1806 de Configuration Manager se incluyen mejoras en la forma en que los clientes se comunican con los sistemas de sitio. Hay dos objetivos principales para estas mejoras:  

- Puede proteger la comunicación de cliente confidencial sin necesidad de certificados de autenticación de servidor PKI.  

- Los clientes pueden acceder de forma segura a contenido desde puntos de distribución sin necesidad de una cuenta de acceso a la red, un certificado PKI de cliente y autenticación de Windows.  

Todas las comunicaciones de cliente se realizan a través de HTTP. HTTP mejorado no es lo mismo que habilitar HTTPS para la comunicación del cliente o un sistema de sitio.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> Los certificados PKI siguen siendo una opción válida para los clientes con los requisitos siguientes:  
>
> - Todas las comunicaciones de cliente se realizan a través de HTTPS  
> - Control avanzado de la infraestructura de firma
>
> Además, si ya usa PKI, se usará el certificado PKI enlazado en IIS, incluso aunque el HTTP mejorado esté activado.



## <a name="scenarios"></a><a name="bkmk_scenario"></a>Escenarios

Los siguientes escenarios aprovechan estas mejoras:  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a> Escenario 1: Cliente a punto de administración

<!--1356889-->
[Los dispositivos unidos a Azure Active Directory (Azure AD)](/azure/active-directory/devices/concept-azure-ad-join) se pueden comunicar con un punto de administración configurado para HTTP. El servidor de sitio genera un certificado para el punto de administración para que pueda comunicarse a través de un canal seguro.

> [!Note]  
> Este comportamiento se ha cambiado a partir de la versión 1802 de la rama actual de Configuration Manager, que requiere un punto de administración habilitado para HTTPS para los clientes unidos a Azure AD que se comunican a través de una instancia de Cloud Management Gateway. Para obtener más información, vea [Enable management point for HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps) (Habilitar el punto de administración para HTTPS).  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a> Escenario 2: Cliente a punto de distribución

<!--1358228-->
Un grupo de trabajo o un cliente unido a Azure AD se puede autenticar y descargar contenido a través de un canal seguro desde un punto de distribución configurado para HTTP. Estos tipos de dispositivos también se pueden autenticar y descargar contenido desde un punto de distribución configurado para HTTPS sin necesidad de un certificado PKI en el cliente. Agregar un certificado de autenticación de cliente a un grupo de trabajo o un cliente unido a Azure AD es un desafío.

Este comportamiento incluye escenarios de implementación de sistema operativo con una secuencia de tareas que se ejecuta desde el medios de arranque, PXE o el Centro de software. Para obtener más información, vea [Cuenta de acceso a la red](accounts.md#network-access-account).<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a> Escenario 3: Identidad del dispositivo de Azure AD

<!--1358460-->
Un dispositivo unido a Azure AD o un [dispositivo de Azure AD híbrido](/azure/active-directory/devices/concept-azure-ad-join-hybrid) sin un usuario de Azure AD con sesión iniciada se puede comunicar de forma segura con su sitio asignado. La identidad del dispositivo basado en la nube ahora es suficiente para autenticarse con el punto de administración y CMG en escenarios centrados en el dispositivo. (Un token de usuario sigue siendo necesario para los escenarios centrados en el usuario).  


## <a name="features"></a>Funciones

Las características siguientes de Configuration Manager admiten o requieren HTTP mejorado:

- [Puerta de enlace de administración en la nube](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Implementación del SO sin una cuenta de acceso de red](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Habilitación de la administración conjunta para los nuevos dispositivos Windows 10 basados en Internet](../../../comanage/tutorial-co-manage-new-devices.md)
- [Aprobaciones de aplicaciones a través de correo electrónico](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Servicio de administración](../../../develop/adminservice/overview.md)
- [Consulta de las consolas conectadas recientemente](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> El punto de actualización de software y los escenarios relacionados siempre han admitido el tráfico HTTP seguro con clientes, así como también Cloud Management Gateway. Usa un mecanismo con el punto de administración que es distinto de la autenticación basada en certificados o basada en tokens.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Requisitos previos  

- Un punto de administración configurado para conexiones de cliente HTTP. Establezca esta opción en la pestaña **General** de las propiedades del rol de punto de administración.  

- Un punto de distribución configurado para conexiones de cliente HTTP. Establezca esta opción en la pestaña **Comunicación** de las propiedades del rol de punto de distribución. No habilite la opción **Permitir a los clientes conectarse de forma anónima**.  

- Incorpore el sitio a Azure AD para administración en la nube.  

- *Solo para el [escenario 3](#bkmk_scenario3)* : Un cliente con Windows 10 versión 1803 o posterior y unido a Azure AD. El cliente requiere esta configuración para la autenticación de dispositivos de Azure AD.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Configuración del sitio

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y haga clic en el nodo **Sitios**. Seleccione el sitio y haga clic en **Propiedades** en la cinta.  

2. Cambie a la pestaña **Comunicación de equipo cliente**.

    > [!Note]
    > A partir de la versión 1906, esta pestaña se denomina **Communication Security** (Seguridad de la comunicación).<!-- SCCMDocs#1645 -->  

    Seleccione la opción para **HTTPS o HTTP**. A continuación, habilite la opción **Usar los certificados generados por Configuration Manager para sistemas de sitios HTTP**.

> [!Tip]
> Espere hasta 30 minutos para que el punto de administración reciba y configure el nuevo certificado desde el sitio.

<!--3798957-->
A partir de la versión 1902, también puede habilitar HTTP mejorado para el sitio de administración central. Use este mismo proceso y abra las propiedades del sitio de administración central. Esta acción solo habilita HTTP mejorado para los roles de proveedor de SMS en el sitio de administración central. No es una configuración global que se aplica a todos los sitios de la jerarquía.

Puede ver estos certificados en la consola de Configuration Manager. Vaya al área de trabajo **Administración**, expanda **Seguridad** y seleccione el nodo **Certificados**. Busque el certificado raíz **SMS Issuing** (Emisión de SMS), así como los certificados de rol del servidor de sitio emitidos por la raíz SMS Issuing (Emisión de SMS).

Para obtener más información sobre cómo se comunica el cliente con el punto de administración y punto de distribución con esta configuración, vea [Comunicaciones desde los clientes a los sistemas de sitio y servicios](communications-between-endpoints.md#Planning_Client_to_Site_System).


## <a name="see-also"></a>Vea también

- [Planear la seguridad](../security/plan-for-security.md)  

- [Seguridad y privacidad para los clientes de Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurar la seguridad](../security/configure-security.md)  

- [Comunicaciones entre puntos de conexión](communications-between-endpoints.md)  
