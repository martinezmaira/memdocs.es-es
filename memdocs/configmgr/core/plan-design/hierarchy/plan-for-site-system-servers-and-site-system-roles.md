---
title: Planeamiento de roles de sistema de sitio
titleSuffix: Configuration Manager
description: Al planear la jerarquía de Configuration Manager, tenga en cuenta los servidores de sistema de sitio y los roles de sistema de sitio.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706503"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Planeamiento de servidores de sistema de sitio y roles de sistema de sitio para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En cada sitio de Configuration Manager que se instala, se incluye un servidor de sitio que es un **servidor de sistema de sitio**. El sitio también puede incluir servidores de sistema de sitio adicionales en equipos que están alejados del servidor de sitio (equipos remotos). Los servidores de sistema de sitio (el servidor de sitio o un servidor de sistema de sitio remoto) admiten **roles de sistema de sitio**.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a> Servidores de sistema de sitio  

Al instalar un rol de sistema de sitio en un equipo, ese equipo se convierte en un servidor de sistema de sitio. En cada sitio puede instalar a uno o más servidores de sistema de sitio adicionales. También puede elegir no instalar servidores de sistema de sitio adicionales y ejecutar todos los roles de sistema de sitio directamente en el equipo servidor de sitio. Cada sistema de sitio hospeda uno o varios roles de sistema de sitio. Si se usan más servidores, pueden ampliarse las funciones y la capacidad de un sitio al compartir la carga de procesamiento que aplican los roles de sistema de sitio en un servidor.  

Al plantearse la incorporación de un servidor de sistema de sitio, asegúrese de que el servidor cumple los requisitos previos para el uso previsto. Además, agréguelo a una ubicación de red que tenga un ancho de banda suficiente para comunicarse con los puntos de conexión esperados. Entre estos puntos de conexión, se incluyen el servidor de sitio, los recursos del dominio, una ubicación basada en la nube, servidores de sistema de sitio y clientes.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a> Roles de sistema de sitio  

Instale los roles de sistema de sitio en un servidor para proporcionar funciones adicionales al sitio. Algunos ejemplos son:  

- Puntos de administración adicionales para que el sitio pueda admitir más dispositivos, hasta alcanzar su capacidad máxima.  

- Puntos de distribución adicionales para expandir la infraestructura de contenido y mejorar así el rendimiento de las distribuciones de contenido a los usuarios y dispositivos.  

- Uno o varios roles de sistema de sitio específicos de la característica. Por ejemplo, un punto de actualización de software le permite administrar actualizaciones de software para dispositivos administrados. Un punto de servicios de informes le permite ejecutar informes para supervisar, comprender y compartir información sobre su entorno.  

Diferentes sitios de Configuration Manager pueden admitir distintos conjuntos de roles de sistema de sitio. El conjunto admitido de roles de sistema de sitio depende del tipo de sitio. (Entre los tipos de sitios, se incluyen un sitio de administración central, sitios primarios o sitios secundarios). La topología de la jerarquía puede limitar la colocación de algunos roles en determinados tipos de sitios. Por ejemplo, el punto de conexión de servicio solo se admite en el sitio de nivel superior de la jerarquía. El sitio de nivel superior puede ser un sitio de administración central o un sitio primario independiente. Este rol no se admite en un sitio primario secundario ni en los sitios secundarios.  

Una vez instalado un sitio, se puede mover la ubicación de algunos roles de sistema de sitio de su ubicación predeterminada en el servidor de sitio a otro servidor. Por ejemplo, los roles del punto de administración o del punto de distribución se instalan de forma predeterminada en un servidor de sitio primario o secundario. Además, instale más instancias de roles de sistema de sitio para expandir las funciones del sitio y adaptarse a sus requisitos empresariales. Algunos roles son necesarios, mientras que otros son opcionales.  

### <a name="configuration-manager-site-server"></a>Servidor de sitio de Configuration Manager

Este rol identifica el servidor donde se ejecuta el programa de instalación de Configuration Manager para instalar un sitio o el servidor donde se instala un sitio secundario. No se puede mover ni desinstalar este rol hasta que se desinstale el sitio.  

### <a name="configuration-manager-site-system"></a>Sistema de sitio de Configuration Manager

Este rol se asigna a cualquier equipo en el que se instale un sitio o un rol de sistema de sitio. No se puede mover ni desinstalar este rol hasta que se quite el último rol de sistema de sitio del equipo.  

### <a name="configuration-manager-component-site-system-role"></a>Rol de sistema de sitio de componente de Configuration Manager

Este rol identifica un sistema de sitio que ejecuta una instancia del servicio **SMS Executive**. Se necesita para admitir otros roles, como puntos de administración. Este rol no se puede mover ni desinstalar hasta que se quite el último rol de sistema de sitio válido del equipo.  

### <a name="configuration-manager-site-database-server"></a>Servidor de base de datos del sitio de Configuration Manager

El sitio asigna este rol a servidores de sistema de sitio que contienen una instancia de la base de datos del sitio. Solo se puede mover este rol a un nuevo servidor si se ejecuta el programa de instalación para modificar el sitio y configurarlo de forma que use otra instancia de SQL Server para hospedar la base de datos del sitio.  

### <a name="sms-provider"></a>Proveedor de SMS

El sitio asigna este rol a cada equipo que hospede una instancia del proveedor de SMS. El proveedor es la interfaz entre una consola de Configuration Manager y la base de datos del sitio. De forma predeterminada, este rol se instala automáticamente en el servidor de sitio de un sitio de administración central y sitios primarios. Puede instalar más instancias en cada sitio para proporcionar acceso a otros usuarios administrativos o para redundancia.  

Para instalar proveedores de SMS adicionales, tiene que ejecutar el programa de instalación de Configuration Manager en el servidor de sitio para [administrar el proveedor de SMS](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Después, puede instalar proveedores adicionales en otros equipos. Solo se puede instalar una instancia del proveedor de SMS en un equipo. Ese equipo tiene que estar en el mismo dominio que el servidor de sitio.  

### <a name="application-catalog-web-service-point"></a>Punto de servicio web del catálogo de aplicaciones

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Rol de sistema de sitio que proporciona información del software al sitio web del catálogo de aplicaciones desde la biblioteca de software. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

### <a name="application-catalog-website-point"></a>Punto de sitios web del catálogo de aplicaciones

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Rol del sistema de sitio que proporciona a los usuarios una lista de software disponible desde el catálogo de aplicaciones. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

### <a name="asset-intelligence-synchronization-point"></a>Punto de sincronización de Asset Intelligence

Rol de sistema de sitio que se conecta a Microsoft para descargar información del catálogo de Asset Intelligence. Este rol también carga títulos sin clasificar para que Microsoft pueda tener en cuenta para su futura inclusión en el catálogo. Una jerarquía solo admite una única instancia de este rol en el sitio de nivel superior de la jerarquía. Si expande un sitio primario independiente a una jerarquía más grande, desinstale este rol del sitio principal. Después, instálelo en el sitio de administración central.

Para obtener más información, vea [Asset Intelligence en Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

### <a name="certificate-registration-point"></a>Punto de registro de certificados

Rol de sistema de sitio que se comunica con un servidor que ejecute el Servicio de inscripción de dispositivos de red (NDES). Este rol administra las solicitudes de certificado de dispositivo que usan el Protocolo de inscripción de certificados simple (SCEP). Este rol solo se admite en los sitios primarios y el sitio de administración central.

Aunque un único punto de registro de certificados puede proporcionar funcionalidad a toda una jerarquía, tal vez prefiera instalar varias instancias de este rol en un sitio y en varios sitios de la misma jerarquía. Este diseño facilita el equilibrio de carga. Cuando existen varias instancias en una jerarquía, los clientes se asignan aleatoriamente a uno de los puntos de registro de certificado.  

Cada punto de registro de certificado necesita acceder a una instancia de NDES separada. No se pueden configurar dos o más puntos de registro de certificado para que usen la misma instancia de NDES. Además, no instale el punto de registro de certificado en el mismo servidor donde se ejecute NDES.  

### <a name="cloud-management-gateway-connection-point"></a>Punto de conexión de Cloud Management Gateway

Rol de sistema de sitio para comunicarse con la [puerta de enlace de administración en la nube](../../clients/manage/cmg/plan-cloud-management-gateway.md).  

### <a name="data-warehouse-service-point"></a>Punto de servicio de almacenamiento de datos

Use el punto de servicio de almacenamiento de datos para almacenar y generar informes de datos históricos a largo plazo para su entorno de Configuration Manager. Para obtener más información, vea [Almacenamiento de datos](../../servers/manage/data-warehouse.md).  

### <a name="distribution-point"></a>Punto de distribución

Rol de sistema de sitio que contiene archivos de origen para que los clientes puedan descargarlos, por ejemplo:

- Contenido de aplicaciones
- Paquetes de software
- Actualizaciones de software
- Imágenes de SO
- Imágenes de arranque  

De forma predeterminada, este rol se instala en el servidor de sitio al instalar un nuevo sitio primario o secundario. Este rol no se admite en un sitio de administración central. Se pueden instalar varias instancias de este rol en un sitio admitido y en varios sitios de la misma jerarquía. Para obtener más información, vea [Conceptos fundamentales de la administración de contenidos](fundamental-concepts-for-content-management.md) y [Administrar el contenido y la infraestructura de contenido](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="endpoint-protection-point"></a>Punto de Endpoint Protection

Rol del sistema de sitio que Configuration Manager utiliza para aceptar los términos de la licencia de Endpoint Protection y configurar la pertenencia predeterminada a Microsoft Active Protection Service. Una jerarquía solo admite una única instancia de este rol y tiene que encontrarse en el sitio de nivel superior. Si expande un sitio primario independiente a una jerarquía más grande, desinstale el rol del sitio primario y, después, instálelo en el sitio de administración central. Para obtener más información, vea [Endpoint Protection en Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="enrollment-point"></a>Punto de inscripción

Rol de sistema de sitio que usa certificados PKI en Configuration Manager para inscribir dispositivos móviles y equipos con macOS. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

Si un usuario inscribe dispositivos móviles mediante Configuration Manager y su cuenta de Active Directory se encuentra en un bosque que no es de confianza para el bosque del servidor de sitio, tiene que instalarse un punto de inscripción en el bosque del usuario. Después, Configuration Manager podrá autenticar al usuario.  

### <a name="enrollment-proxy-point"></a>Punto de proxy de inscripción

Rol de sistema de sitio que administra solicitudes de inscripción de Configuration Manager por parte de dispositivos móviles y equipos con macOS. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio o en varios sitios de la misma jerarquía.  

Al admitir dispositivos móviles en Internet, instale un punto de proxy de inscripción en una red perimetral e instale otro en la intranet.

### <a name="exchange-server-connector"></a>Conector de Exchange Server

Para obtener información sobre este rol, vea [Administrar dispositivos móviles mediante Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="fallback-status-point"></a>Punto de estado de reserva

Un rol de sistema de sitio que le permite supervisar la instalación de clientes. Identifica los clientes no administrados porque no pueden establecer comunicación con el punto de administración. Aunque este rol solo se admite en sitios primarios, puede instalar varias instancias de él en un sitio y en varios sitios de la misma jerarquía.

### <a name="management-point"></a>Punto de administración

Un rol de sistema de sitio que proporciona información de ubicación del servicio y directivas a los clientes. También recibe datos de configuración de los clientes.  

De forma predeterminada, este rol se instala en el servidor de sitio al instalar un nuevo sitio primario o secundario. Los sitios primarios admiten varias instancias de este rol. Los sitios secundarios solo admiten un único punto de administración. También se conoce como punto de administración proxy; este rol, cuando se encuentra en un sitio secundario, proporciona un punto de contacto local para que los clientes puedan obtener directivas de usuario y equipo.  

Configure los puntos de administración para que sean compatibles con HTTP o HTTPS. También son compatibles con dispositivos móviles inscritos con la Administración de dispositivos móviles (MDM) local de Configuration Manager. Para reducir la carga de procesamiento del servidor de base de datos del sitio cuando los puntos de administración procesan solicitudes de clientes, use [Réplicas de base de datos para puntos de administración](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="reporting-services-point"></a>Punto de servicios de informes

Rol de sistema de sitio que se integra con SQL Server Reporting Services para crear y administrar informes para Configuration Manager. Este rol se admite en sitios primarios y en el sitio de administración central. Se pueden instalar varias instancias de él en un sitio admitido. Para obtener más información, vea [Planeamiento de informes](../../servers/manage/planning-for-reporting.md).  

### <a name="service-connection-point"></a>Punto de conexión de servicio

Rol de sistema de sitio que carga los datos de uso del sitio y es necesario para realizar las actualizaciones de Configuration Manager disponibles en la consola. Una jerarquía solo admite una única instancia de este rol y tiene que encontrarse en el sitio de nivel superior de su jerarquía. Si expande un sitio primario independiente a una jerarquía más grande, desinstale el rol del sitio primario y, después, instálelo en el sitio de administración central. Para obtener más información, consulte [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md) (Sobre el punto de conexión del servicio).  

### <a name="software-update-point"></a>Punto de actualización de software

Rol de sistema de sitio que se integra con Windows Server Update Services (WSUS) para proporcionar actualizaciones de software a los clientes de Configuration Manager. Este rol se admite en todos los sitios:  

- Instale este sistema de sitio en el sitio de administración central para la sincronización con WSUS.  

- Configure cada instancia de este rol en sitios primarios secundarios para la sincronización con el sitio de administración central.  

- También puede instalar un punto de actualización de software en sitios secundarios cuando la transferencia de datos por la red sea lenta.  

Para obtener más información, vea [Planear actualizaciones de software](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Punto de migración de estado

Al migrar un equipo a un nuevo sistema operativo, este rol de sistema de sitio almacena datos de estado de usuario. Este rol se admite en sitios primarios y sitios secundarios. Se pueden instalar varias instancias de este rol en un sitio y en varios sitios de la misma jerarquía. Para obtener más información sobre cómo almacenar el estado de usuario al implementar un sistema operativo, vea [Administrar el estado del usuario](../../../osd/get-started/manage-user-state.md).  


## <a name="next-steps"></a>Pasos siguientes

Algunos roles de sistema de sitio de Configuration Manager necesitan conexiones a Internet. Si su entorno necesita tráfico de Internet para usar un servidor proxy, configure estos roles de sistema de sitio para que usen el proxy. Para obtener más información, vea [Compatibilidad de servidor proxy](../network/proxy-server-support.md).  
