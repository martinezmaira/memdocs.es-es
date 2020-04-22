---
title: Tamaño y escala
titleSuffix: Configuration Manager
description: Determine el número de roles de sistema de sitio y los sitios que necesitará para admitir los dispositivos en el entorno.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0861bb73769beb6c7595b896afc8d0e156eef94d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688623"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Números de tamaño y escala para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Cada implementación de Configuration Manager tiene un número máximo de sitios, roles de sistema de sitio y dispositivos que puede admitir. Estos números varían en función de la estructura de la jerarquía, los tipos y números de sitios que se usen y los roles de sistema de sitio que se implementen. La información de este artículo puede ayudar a identificar el número de roles de sistema de sitio y los sitios que se necesitan para admitir los dispositivos que se esperan administrar.

Vea los siguientes artículos para más información:

- [Hardware recomendado](recommended-hardware.md)
- [Sistemas operativos compatibles con servidores de sistema de sitio](supported-operating-systems-for-site-system-servers.md)  
- [Supported operating systems for clients and devices](supported-operating-systems-for-clients-and-devices.md) (Sistemas operativos compatibles con clientes y dispositivos)
- [Requisitos previos de sitio y sistema de sitio](site-and-site-system-prerequisites.md)

Estos números de compatibilidad se basan en el uso del hardware recomendado para Configuration Manager. También se basan en la configuración predeterminada para todas las características disponibles de Configuration Manager. Si no usa el hardware recomendado o usa una configuración personalizada más agresiva, el rendimiento de los sistemas de sitio puede verse afectado. Es posible que los sistemas de sitio no cumplan los niveles de compatibilidad indicados. (Un ejemplo de configuración de cliente más agresiva es la ejecución de inventario de hardware o software con más frecuencia que los valores predeterminados de una vez cada siete días).

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a> Tipos de sitio  

### <a name="central-administration-site"></a>Sitio de administración central  

- Un sitio de administración central admite hasta 25 sitios primarios o secundarios.  

### <a name="primary-site"></a>Sitio primario  

- Cada sitio primario admite hasta 250 sitios secundarios.  

- El número de sitios secundarios por cada sitio primario se basa en conexiones de red de área extensa (WAN) confiables y continuamente conectadas. Para las ubicaciones que tienen menos de 500 clientes, considere la posibilidad de un punto de distribución en lugar de un sitio secundario.  

  Para obtener más información sobre el número de clientes y dispositivos que un sitio primario puede admitir, vea [Número de clientes para sitios y jerarquías](#bkmk_clientnumbers).  

### <a name="secondary-site"></a>Sitio secundario  

- Los sitios secundarios no admiten otros sitios secundarios.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Roles de sistema de sitio

### <a name="application-catalog-web-service-point"></a>Punto de servicio web del catálogo de aplicaciones  

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- Puede instalar varias instancias del punto de servicio web del catálogo de aplicaciones en los sitios primarios.  

### <a name="application-catalog-website-point"></a>Punto de sitios web del catálogo de aplicaciones  

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- Puede instalar varias instancias del punto de sitios web del catálogo de aplicaciones en los sitios primarios.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a> Cloud Management Gateway

- Se pueden instalar varias instancias de Cloud Management Gateway (CMG) en los sitios primarios o el sitio de administración central.  

    > [!Tip]  
    > En una jerarquía, cree la instancia de CMG en el sitio de administración central.  

  - Una instancia de CMG admite hasta 16 instancias de máquina virtual (VM) en el servicio de nube de Azure.  

  - Cada instancia de VM de CMG admite 6000 conexiones de cliente simultáneas. Cuando CMG soporta una carga elevada debido a que el número de clientes es mayor que el admitido, sigue administrando las solicitudes, pero pueden producirse retrasos.  

Para obtener más información, vea [Rendimiento y escalabilidad](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) de CMG.

### <a name="cloud-management-gateway-connection-point"></a>Punto de conexión de Cloud Management Gateway

- Se pueden instalar varias instancias del punto de conexión de Cloud Management Gateway en los sitios primarios.  

- Un punto de conexión de CMG puede admitir una instancia de CMG con hasta cuatro instancias de máquina virtual. Si la instancia de CMG tiene más de cuatro instancias de máquina virtual, agregue un segundo punto de conexión de CMG para equilibrar la carga. Una instancia de CMG con 16 instancias de máquina virtual debe estar vinculada a cuatro puntos de conexión de CMG.

Para obtener más información, vea [Rendimiento y escalabilidad](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) de CMG.

> [!NOTE]
> Al recapitular los requisitos de hardware para el punto de conexión de CMG, vea [Hardware recomendado para servidores de sistema de sitio remoto](recommended-hardware.md#bkmk_RemoteSiteSystem).<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Punto de distribución  

- Puntos de distribución por sitio:  

  - Cada sitio primario y secundario admite hasta 250 puntos de distribución.  

  - Cada sitio primario y secundario admite hasta 2000 puntos de distribución adicionales configurados como puntos de distribución de extracción. **Por ejemplo**, un único sitio primario admite 2250 puntos de distribución cuando 2000 de esos puntos de distribución se configuran como puntos de distribución de extracción.  

  - Cada punto de distribución admite conexiones de hasta 4.000 clientes.  

  - Un punto de distribución de extracción actúa como un cliente cuando tiene acceso a contenido desde un punto de distribución de origen.  

- Cada sitio primario admite un total combinado de hasta 5.000 puntos de distribución. Este total incluye todos los puntos de distribución en el sitio primario y todos los puntos de distribución que pertenecen a los sitios secundarios del sitio primario.  

- Cada punto de distribución es compatible con un total combinado de hasta 10.000 paquetes y aplicaciones.  

> [!WARNING]  
> El número real de clientes que puede admitir un punto de distribución depende de la velocidad de la red y la configuración de hardware del servidor.  
>
> El número de puntos de extracción que puede admitir un punto de distribución de origen depende también de la velocidad de la red y la configuración de hardware del punto de distribución de origen. Pero este número también se ve afectado por la cantidad de contenido que haya implementado. Este efecto se debe a que, a diferencia de los clientes que suelen tener acceso a contenido en distintos momentos durante una implementación, todos los puntos de distribución de extracción solicitan el contenido al mismo tiempo. Los puntos de distribución de extracción pueden solicitar todo el contenido disponible, no solo el contenido que les corresponde. Cuando se coloca una carga de procesamiento elevada en un punto de distribución de origen, se pueden producir retrasos inesperados al distribuir el contenido a los puntos de distribución de destino.  

### <a name="fallback-status-point"></a>Punto de estado de reserva  

- Cada punto de estado de reserva puede admitir hasta 100.000 clientes.  

### <a name="management-point"></a>Punto de administración  

- Cada sitio primario admite hasta 15 puntos de administración.  

    > [!TIP]  
    > No instale puntos de administración en servidores que atraviesen un vínculo lento desde el servidor de sitio primario o el servidor de base de datos del sitio.  

- Cada sitio secundario admite un solo punto de administración que se debe instalar en el servidor de sitio secundario.  

Para obtener más información sobre el número de clientes y dispositivos que un punto de administración puede admitir, vea la sección [Puntos de administración](#bkmk_mp).  

### <a name="software-update-point"></a>Punto de actualización de software  

Utilice las siguientes recomendaciones como una línea de base. Esta línea de base le ayuda a determinar la información para la planeación de la capacidad de las actualizaciones de software que sea adecuada para su organización. Los requisitos reales de capacidad pueden variar respecto a los incluidos en las recomendaciones de este artículo, en función de los siguientes criterios:

- El entorno de red específico
- El hardware que se usa para hospedar el punto de actualización de software del sistema de sitio
- El número de clientes administrados
- Los otros roles de sistema de sitio instalados en el servidor  

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Planeación de la capacidad para el punto de actualización de software  

El número de clientes admitidos depende de la versión de Windows Server Update Services (WSUS) que se ejecuta en el punto de actualización de software. También depende de si el rol de sistema de sitio del punto de actualización de software coexiste con otro rol de sistema de sitio:  

- El punto de actualización de software puede admitir hasta 25 000 clientes cuando WSUS se ejecuta en el servidor del punto de actualización de software y este punto coexiste con otro rol de sistema de sitio.  

- El punto de actualización de software puede admitir hasta 150 000 clientes cuando un servidor remoto cumple los requisitos de WSUS, WSUS se utiliza con Configuration Manager y configura las siguientes opciones:

  Grupos de aplicaciones de IIS:

  - Aumente la longitud de cola de WsusPool a 2000
  - Cuadriplique el límite de memoria privada de WsusPool o defínalo en 0 (ilimitado). Por ejemplo, si el límite predeterminado es 1 843 200 KB, auméntelo a 7 372 800. Para más información, vea esta [entrada del blog del equipo de soporte técnico de Configuration Manager](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Para más información sobre los requisitos de hardware para el punto de actualización de software, vea [Requisitos recomendados para sistemas de sitio](recommended-hardware.md#bkmk_ScaleSieSystems).  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a> Planeación de la capacidad para los objetos de actualizaciones de software  

Utilice la siguiente información de capacidad para planear los objetos de actualizaciones de software:  

- **Límite de 1000 actualizaciones de software en una implementación**: limite el número de actualizaciones de software a 1000 por cada implementación de actualización de software. Cuando crea una regla de implementación automática (ADR), especifique un criterio que limite el número de actualizaciones de software. La regla de implementación automática produce un error cuando los criterios especificados devuelven más de 1000 actualizaciones de software. Compruebe el estado de la ADR desde el nodo **Reglas de implementación automática** de la consola de Configuration Manager. Al implementar manualmente las actualizaciones de software, no seleccione más de 1000 actualizaciones para implementar.  

  Limite también el número de actualizaciones de software a 1000 en una línea base de configuración. Para obtener más información, consulte [Crear una línea base de configuración](../../../compliance/deploy-use/create-configuration-baselines.md).

- **Límite de 580 ámbitos de seguridad para las reglas de implementación automática** -:<!--ado 4962928-->
limite el número de ámbitos de seguridad en reglas de implementación automática (ADR) a menos de 580. Al crear una ADR, se agregan automáticamente los ámbitos de seguridad que tienen acceso a ella. Si hay más de 580 ámbitos de seguridad establecidos, la ADR no podrá ejecutarse y se registrará un error en ruleengine.log.

### <a name="sms-provider"></a>Proveedor de SMS

<!-- SCCMDocs#1958 -->

Cada instancia del proveedor de SMS admite conexiones simultáneas de varias solicitudes. Las únicas limitaciones de estas conexiones son el número de conexiones de servidor disponibles en Windows y los recursos disponibles en el servidor para atender las solicitudes de conexión.

Para más información, vea [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md) (Planear el proveedor de SMS).

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Número de clientes para sitios y jerarquías

Use la siguiente información para determinar cuántos clientes, y de qué tipo, se pueden admitir en un sitio o en una jerarquía.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Jerarquía con un sitio de administración central

Un sitio de administración central admite un número total de dispositivos que incluye el número máximo de dispositivos indicados para los tres grupos siguientes:  

- 700 000 escritorios de Windows. Consulte también la compatibilidad con [los dispositivos con Windows Embedded](#embedded).

- 25 000 dispositivos que ejecutan Mac y Windows CE 7.0  

- 100 000 dispositivos que administra mediante la administración de dispositivos móviles (MDM)

Por ejemplo, en una jerarquía puede admitir 700 000 equipos de escritorio, hasta 25 000 dispositivos Mac y Windows CE 7.0, y hasta 100 000 dispositivos administrados por MDM local. Esta jerarquía admite un total de 825 000 dispositivos.

> [!IMPORTANT]  
> En una jerarquía donde el sitio de administración central usa SQL Server Standard Edition, la jerarquía admite un máximo de 50 000 equipos de escritorio y dispositivos. Para admitir más de 50 000 equipos de escritorio y dispositivos, debe usar una edición Enterprise de SQL Server. Este requisito solo se aplica a un sitio de administración central. No se aplica a un sitio primario independiente o un sitio primario secundario. La edición de SQL Server que se usa para un sitio primario no limita su capacidad para admitir el número de clientes indicado.

La edición de SQL Server que se usa en un sitio primario independiente no limita la capacidad del sitio para admitir el número de clientes indicado.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a> Sitio primario secundario

Cada sitio primario secundario de una jerarquía con un sitio de administración central admite el número de clientes siguiente:  

- 150 000 clientes y dispositivos en total, sin limitarse a un grupo o tipo específico, siempre y cuando no se supere el número admitido para la jerarquía. Consulte también la compatibilidad con [los dispositivos con Windows Embedded](#embedded).

Por ejemplo, un sitio primario admite 25 000 dispositivos Mac y Windows CE 7.0. Este número es el límite de una jerarquía. Después, este sitio primario puede admitir 125 000 equipos de escritorio adicionales. El número total de dispositivos admitidos por el sitio primario secundario es el límite máximo admitido de 150 000.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a> Sitio primario independiente

Un sitio primario independiente admite el siguiente número de dispositivos:  

- 175 000 clientes y dispositivos en total, en esta proporción:  

  - 150 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX) Consulte también la compatibilidad con [los dispositivos con Windows Embedded](#embedded).

  - 25 000 dispositivos que ejecutan Mac y Windows CE 7.0

  - 50 000 dispositivos que administra mediante MDM local  

Por ejemplo, un sitio primario independiente que admite 150 000 equipos PC y 10 000 equipos Mac solo puede admitir otros 15 000 dispositivos móviles administrados por MDM local.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a> Sitios principales y dispositivos con Windows Embedded

Los sitios principales admiten dispositivos con Windows Embedded que tienen habilitados los filtros de escritura basados en archivos (FBWF). Cuando los dispositivos insertados no tienen filtros de escritura habilitados, un sitio primario puede admitir una serie de dispositivos insertados, hasta el máximo permitido para ese sitio. Cuando los dispositivos incrustados tienen FBWF o filtros de escritura unificados (UWF) habilitados, un sitio primario puede admitir un máximo de 10 000 dispositivos incrustados de Windows. Estos dispositivos se deben configurar con las excepciones enumeradas en la nota importante que se encuentra en [Planeamiento de la implementación de clientes en dispositivos de Windows Embedded](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md). Un sitio principal admite solo 3000 dispositivos con Windows Embedded que tienen habilitado EWF y que no están configurados para las excepciones.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a> Sitios secundarios

Los sitios secundarios admiten el número de dispositivos siguiente:  

- 15 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX)  

### <a name="management-points"></a><a name="bkmk_mp"></a> Puntos de administración

Cada punto de administración puede admitir el siguiente número de dispositivos:  

- 25 000 clientes y dispositivos en total, en esta proporción:  

  - 25 000 equipos de escritorio (equipos que ejecutan Windows, Linux y UNIX)  

  - Uno de los siguientes (no ambos):  

    - 10 000 dispositivos que administra mediante MDM local  

    - 10 000 dispositivos que ejecutan clientes Mac y Windows CE 7.0
