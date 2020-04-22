---
title: Planeación de administración de aplicaciones
titleSuffix: Configuration Manager
description: Implemente y configure las dependencias necesarias para la implementación de aplicaciones en Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689053"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Planeamiento y configuración de la administración de aplicaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la información de este artículo como ayuda para implementar las dependencias necesarias para la implementación de aplicaciones en Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

Se requiere IIS en los servidores que ejecutan los siguientes roles del sistema de sitios:

- Punto de administración  
- Punto de distribución  

Para obtener más información, consulte [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  

> [!Note]  
> El catálogo de aplicaciones también requiere IIS. Sin embargo, su experiencia del usuario de Silverlight no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificados de aplicaciones con firma de código para dispositivos móviles

Cuando realice la firma de código de aplicaciones para implementarlas en dispositivos móviles, no use un certificado generado mediante una plantilla de versión 3 (**Windows Server 2008, Enterprise Edition**). Esta plantilla de certificado crea un certificado que no es compatible con aplicaciones de Configuration Manager para dispositivos móviles.

Si usa Servicios de certificados de Active Directory para la firma de código de aplicaciones de dispositivos móviles, no use plantillas de certificado de versión 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Auditoría de eventos de inicio de sesión para la afinidad entre usuario y dispositivo  

Si desea crear automáticamente afinidades entre usuario y dispositivo,configure los clientes para auditar los eventos de inicio de sesión.

Para determinar afinidades automáticas entre usuario y dispositivo, el cliente de Configuration Manager lee los eventos de inicio de sesión de tipo **Correcto** del registro de eventos de seguridad de Windows. Estos eventos se habilitan mediante las dos siguientes directivas de auditoría:

- **Auditar eventos de inicio de sesión de cuenta**
- **Auditar eventos de inicio de sesión**

Para crear automáticamente relaciones entre los usuarios y los dispositivos, asegúrese de que estas dos opciones están habilitadas en los equipos cliente. Puede usar la directiva de grupo de Windows para configurar estas opciones.

Para más información sobre la afinidad entre usuario y dispositivo, vea [Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  



## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager


### <a name="management-point"></a>Punto de administración

Los clientes se ponen en contacto con un punto de administración para descargar la directiva de cliente y buscar contenido.

A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario.

En la versión 1902 y anteriores, los clientes usan el punto de administración para conectarse al catálogo de aplicaciones. Si los clientes no pueden obtener acceso a un punto de administración, no podrán usar el catálogo de aplicaciones.

> [!Note]  
> A partir de la versión 1806, los roles del catálogo de aplicaciones ya no son necesarios para mostrar las aplicaciones disponibles para el usuario en el Centro de software. Para obtener más información, consulte [Configurar el centro de software](plan-for-software-center.md#bkmk_userex).<!--1358309-->  
>
> A partir de la versión 1906, no es posible instalar nuevos roles de catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
  

### <a name="distribution-point"></a>Punto de distribución

Para poder implementar aplicaciones en clientes, necesita al menos un punto de distribución en la jerarquía. De forma predeterminada, el servidor de sitio tiene un rol de sitio de punto de distribución habilitado durante una instalación estándar. El número y la ubicación de los puntos de distribución variarán según las necesidades de su entorno.

Para obtener más información sobre cómo instalar puntos de distribución y administrar contenido, consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administrar el contenido y la infraestructura de contenido).  


### <a name="reporting-services-point"></a>Punto de servicios de informes

Para usar los informes de Configuration Manager para la administración de aplicaciones, primero instale y configure un punto de servicios de informes.

Para obtener más información, vea [Introducción a los informes](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="client-settings"></a>Configuración de cliente

Varias configuraciones de cliente controlan cómo el cliente instala aplicaciones y la experiencia de usuario en el dispositivo. Estas configuraciones de cliente incluyen los grupos siguientes:

- Agente de equipo  
- Reinicio de equipo  
- Centro de software  
- Implementación de software  
- Afinidad entre usuario y dispositivo  

Vea los siguientes artículos para más información:

- [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md)  
- [Cómo establecer la configuración del cliente](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Permisos de seguridad para la administración de aplicaciones

- El rol de seguridad **Autor de aplicaciones** incluye los permisos necesarios para crear, modificar y retirar aplicaciones.  

- El rol de seguridad **Administrador de implementación de aplicaciones** incluye los permisos indicados para implementar aplicaciones.  

- El rol de seguridad **Administrador de aplicaciones** contiene todos los permisos de los roles de seguridad **Autor de aplicaciones** y **Administrador de implementación de aplicaciones** .  

Para obtener más información, vea [Configurar la administración basada en roles](../../core/servers/deploy/configure/configure-role-based-administration.md).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>Cliente de App-V 4.6 SP1 o posterior para ejecutar aplicaciones virtuales

Para crear aplicaciones virtuales en Configuration Manager, instale App-V 4.6 SP1 o posterior en los dispositivos.

Antes de implementar aplicaciones virtuales, actualice también el cliente de App-V con la revisión descrita en el [artículo 2645225](https://support.microsoft.com/help/2645225) del Soporte técnico de Microsoft.  


### <a name="application-catalog"></a>Catálogo de aplicaciones

> [!Important]  
> La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910. Para más información, consulte [Eliminación del catálogo de aplicaciones](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Punto de servicio web del catálogo de aplicaciones

El punto de servicio web del catálogo de aplicaciones es un rol de sistema de sitio que proporciona información acerca del software disponible desde la biblioteca de software al sitio web del catálogo de aplicaciones al que acceden los usuarios.

Para más información sobre cómo configurar este rol de sistema de sitio, consulte [Instalación y configuración del catálogo de aplicaciones](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Punto de sitios web del catálogo de aplicaciones

El punto de sitios web del catálogo de aplicaciones es un rol de sistema de sitio que proporciona a los usuarios una lista del software disponible.

Para más información sobre cómo configurar este rol de sistema de sitio, consulte [Instalación y configuración del catálogo de aplicaciones](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Cuentas de usuario detectadas para el catálogo de aplicaciones

Para que los usuarios puedan ver y solicitar aplicaciones del catálogo de aplicaciones, primero Configuration Manager debe detectar las cuentas de usuario. Para obtener más información, vea [Ejecutar la detección](../../core/servers/deploy/configure/run-discovery.md).  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a> Configurar el Centro de software  

Para más información sobre la configuración y la personalización de marca del Centro de software, consulte [Planeamiento del centro de software](plan-for-software-center.md).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a> Eliminación del catálogo de aplicaciones

<!-- SCCMDocs-pr issue 3051 -->

La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910. Para más información, consulte [Características en desuso y eliminadas](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). En la lista siguiente se resumen los cambios:

- A partir de la versión 1806, la **experiencia de usuario de Silverlight** del punto de sitios web del catálogo de aplicaciones ya no se admite.<!--1358309--> El rol de punto de servicio web del catálogo de aplicaciones ya no es *necesario*, pero todavía se *admite*.

- A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones.

- La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  

Estas mejoras iterativas en el Centro de software y en punto de administración son para simplificar la infraestructura y eliminar la necesidad del catálogo de aplicaciones para las implementaciones disponibles para los usuarios. Centro de software puede entregar todas las implementaciones de aplicaciones sin el catálogo de aplicaciones. Además, si habilita TLS 1.2 y utiliza HTTP con el catálogo de aplicaciones, los usuarios no podrán ver las implementaciones disponibles y dirigidas a los usuarios. Actualice Configuration Manager a la versión 1906 o posterior para aprovechar estas mejoras.

1. Actualice a todos los clientes a la versión 1806 o posterior. Se recomienda la versión 1906.  

1. Establezca la personalización de marca para el Centro de software, en lugar de en las propiedades del rol de sitio web del catálogo de aplicaciones. Para obtener más información, vea [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md#software-center).  

1. Revise la configuración del cliente, tanto personalizada como predeterminada. En el grupo **Agente de equipo**, asegúrese de que **Punto de sitios web del catálogo de aplicaciones predeterminado** es `(none)`.  

    En la versión 1902, el cliente solo cambia para utilizar el punto de administración cuando no hay roles de catálogo de aplicación en la jerarquía. De lo contrario, los clientes siguen utilizando una de las instancias del catálogo de aplicaciones en la jerarquía. Este comportamiento se aplica en todos los sitios principales independientes.  

1. Quite los roles de sistema del **sitio web del catálogo de aplicaciones** y del **servicio web de catálogo de aplicaciones** de todos los sitios principales.

Después de quitar los roles de catálogo de aplicaciones, el Centro de software comienza a utilizar el punto de administración para las implementaciones disponibles y dirigidas a los usuarios. En la versión 1902 y anteriores, este cambio puede tardar hasta 65 minutos en producirse. Para comprobar este comportamiento en un cliente específico, revise `SCClient_<username>.log`y busque una entrada similar a la siguiente línea:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a> Instalación y configuración del catálogo de aplicaciones  

> [!Important]  
> La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910. Para más información, consulte [Eliminación del catálogo de aplicaciones](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>Paso 1: certificado de servidor web para HTTPS

Si usa conexiones HTTPS, implemente un certificado de servidor web en los servidores de sistema de sitio para el punto de sitios web del catálogo de aplicaciones y el punto de servicio web del catálogo de aplicaciones.

Si desea que los clientes usen el catálogo de aplicaciones de Internet, implemente un certificado de servidor web en al menos un punto de administración. Configúrelo para las conexiones de cliente desde Internet.

Para más información sobre los requisitos de certificado, consulte [Requisitos de certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Paso 2: certificado de autenticación del cliente para HTTPS

Si usa un certificado PKI de cliente para las conexiones a los puntos de administración, implemente un certificado de autenticación de cliente en los equipos cliente. Si bien los clientes no usan un certificado de PKI de cliente para conectarse con el catálogo de aplicaciones, deben conectarse a un punto de administración antes de poder usar el catálogo de aplicaciones.

Implemente un certificado de autenticación del cliente en los equipos cliente en los siguientes escenarios:

- Todos los puntos de administración de la intranet aceptan únicamente conexiones de cliente HTTPS.
- Los clientes se conectan al catálogo de aplicaciones desde Internet.

Para más información sobre los requisitos de certificado, consulte [Requisitos de certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Paso 3: Instalación y configuración de los roles del catálogo de aplicaciones

Instale tanto el punto de servicio web del catálogo de aplicaciones como el punto de sitios web del catálogo de aplicaciones en el mismo sitio. No es necesario instalarlos en el mismo servidor ni en el mismo bosque de Active Directory. Sin embargo, el punto de servicio web del catálogo de aplicaciones debe estar en el mismo bosque que la base de datos del sitio.

Para obtener más información sobre la ubicación del servidor, vea [Planeamiento de servidores y roles de sistema de sitio](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

> [!NOTE]  
> Instale el catálogo de aplicaciones en un sitio principal. No puede instalarlo en un sitio secundario ni en un sitio de administración central.  

Instale el catálogo de aplicaciones en un servidor de sistema de sitio nuevo o un servidor existente en el sitio. Para más información sobre el proceso general, vea [Instalación de roles de sistema de sitio ](../../core/servers/deploy/configure/install-site-system-roles.md). En el Asistente para agregar un rol de sistema de sitio o crear un servidor de sistema de sitio, seleccione los siguientes roles de la lista:  

- **Punto de servicio web del catálogo de aplicaciones**  
- **Punto de sitios web del catálogo de aplicaciones**  

> [!TIP]  
> Si quiere que los equipos cliente tengan acceso al catálogo de aplicaciones a través de Internet, especifique el nombre de dominio completo (FQDN) de Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Comprobación de la instalación de estos roles de sistema de sitio  

- Mensajes de estado: use los componentes **SMS_PORTALWEB_CONTROL_MANAGER** y **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por ejemplo, el identificador de estado **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma que el Administrador de componentes de sitio ha instalado correctamente el punto de sitios web del catálogo de aplicaciones.  

- Archivos de registro: busque **SMSAWEBSVCSetup.log** y **SMSPORTALWEBSetup.log**.  

    Para más información, busque los archivos de registro **awebsvcMSI.log** y **portlwebMSI.log**.  


### <a name="step-4-configure-client-settings"></a>Paso 4: Configuración del cliente

Configure las opciones de cliente predeterminadas si desea que todos los usuarios tengan la misma configuración. De lo contrario, configure opciones de cliente personalizadas para recopilaciones específicas.

Vea los siguientes artículos para más información:

- [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md)  
    - Agente de equipo  
    - Reinicio de equipo  
    - Centro de software  
    - Implementación de software  
    - Afinidad entre usuario y dispositivo  
- [Cómo establecer la configuración del cliente](../../core/clients/deploy/configure-client-settings.md)  

El cliente de Configuration Manager configura dispositivos con estos ajustes la siguiente vez que descargue la directiva de cliente. Para desencadenar la recuperación de directivas para un solo cliente, vea [Cómo administrar clientes](../../core/clients/manage/manage-clients.md).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Paso 5: Comprobación de que el catálogo de aplicaciones esté operativo

Utilice los procedimientos siguientes para comprobar que el catálogo de aplicaciones esté funcionando.

> [!NOTE]  
> La experiencia de usuario del catálogo de aplicaciones requiere Microsoft Silverlight. Si utiliza el catálogo de aplicaciones directamente desde un explorador, verifique primero que Microsoft Silverlight esté instalado en el equipo.  

> [!TIP]  
> La falta de cumplimiento de los requisitos previos está entre uno de los motivos más frecuentes por los que el catálogo de aplicaciones no funciona correctamente después de su instalación. Confirme que se cumplen los requisitos previos del rol de sistema de sitio para los roles de sistema de sitio del catálogo de aplicaciones. Para obtener más información, consulte [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  

En un explorador, escriba la dirección del sitio web del catálogo de aplicaciones. Confirme que en la página web se muestran las tres pestañas: **Catálogo de aplicaciones**, **Mis solicitudes de aplicación** y **Mis dispositivos**.  

Use la dirección adecuada de las que se muestran en la siguiente lista para el catálogo de aplicaciones, donde `<server>` es el nombre del equipo, el FQDN de la intranet o el FQDN de Internet:  

- Conexiones de cliente HTTPS y configuración predeterminada de rol de sistema de sitio: `https://<server>/CMApplicationCatalog`  

- Conexiones de cliente HTTP y configuración predeterminada de rol de sistema de sitio: `http://<server>/CMApplicationCatalog`  

- Conexiones de cliente HTTPS y configuración personalizada de rol de sistema de sitio: `https://<server>:<port>/<web application name>`  

- Conexiones de cliente HTTP y configuración personalizada de rol de sistema de sitio: `http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Si ha iniciado sesión en el dispositivo con una cuenta de administrador de dominio, el cliente de Configuration Manager no muestra mensajes de notificación. Por ejemplo, mensajes que indican que hay nuevo software disponible.  
