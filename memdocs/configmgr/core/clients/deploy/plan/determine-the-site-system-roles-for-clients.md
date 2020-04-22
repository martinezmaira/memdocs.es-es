---
title: Roles de sistema de sitio para clientes
titleSuffix: Configuration Manager
description: Determine roles de sistema de sitio para los clientes en Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693753"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>Determinar los roles de sistema de sitio para clientes de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo puede ayudarlo a determinar los roles del sistema de sitio que necesita para implementar clientes de Configuration Manager.

Para más información sobre en qué parte de la jerarquía instalar estos roles, consulte [Diseñar una jerarquía de sitios](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

Para más información sobre cómo instalar y configurar estos roles, consulte [Instalar roles de sistema de sitio](../../../servers/deploy/configure/install-site-system-roles.md).  

## <a name="management-point"></a>Punto de administración

De manera predeterminada, todos los equipos cliente de Windows usan un punto de distribución para instalar el cliente de Configuration Manager. Pueden recurrir a un punto de administración cuando un punto de distribución no está disponible. No obstante, puede instalar clientes de Windows en equipos de otro origen mediante la propiedad de línea de comandos de CCMSetup `/source:<Path>`. Por ejemplo, podría llevar a cabo esta acción si instala clientes en Internet. Otro escenario se produce cuando se quiere evitar el envío de paquetes de red entre el equipo y el punto de administración durante la instalación de cliente. Este escenario se debe a que un firewall bloquea los puertos requeridos o porque tiene una conexión de bajo ancho de banda. Pero todos los clientes deben comunicarse con un punto de administración para asignarse a un sitio y para que Configuration Manager los administre.  

Para más información sobre las propiedades de la línea de comando del cliente, consulte [Acerca de las propiedades de instalación de clientes](../about-client-installation-properties.md).  

Cuando se instala más de un punto de administración de la jerarquía, los clientes se conectan automáticamente a un punto, según su ubicación de red y la pertenencia al bosque. No se puede instalar más de un punto de administración en un sitio secundario.  

Los clientes de equipos Mac y los clientes de dispositivos móviles inscritos con Configuration Manager siempre requieren un punto de administración para la instalación de cliente. Este punto de administración debe estar en un sitio primario, debe estar configurado para admitir dispositivos móviles y debe aceptar conexiones de clientes desde Internet. Estos clientes no pueden utilizar puntos de administración en sitios secundarios o conectarse a puntos de administración de otros sitios primarios.  

## <a name="distribution-point"></a>Punto de distribución

No es necesario un punto de distribución para instalar clientes de Configuration Manager en equipos de Windows. De manera predeterminada, Configuration Manager usa un punto de distribución para instalar los archivos de origen de cliente en los equipos Windows. Puede recurrir a descargar estos archivos desde un punto de administración. Los puntos de distribución no se usan para instalar clientes de dispositivos móviles inscritos por Configuration Manager, pero se usan para instalar el cliente heredado de dispositivo móvil. Si instala el cliente de Configuration Manager como parte de una implementación de sistema operativo, la imagen del sistema operativo se almacena y recupera desde un punto de distribución.

Aunque es posible que no sean necesarios puntos de distribución para instalar la mayoría de los clientes de Configuration Manager, serán necesarios para instalar software como aplicaciones y actualizaciones de software en los clientes.  

## <a name="fallback-status-point"></a>Punto de estado de reserva

Puede utilizar un punto de estado de reserva para supervisar la implementación del cliente para equipos de Windows. También puede identificar los clientes de equipos de Windows que no están administrados porque no se pueden comunicar con un punto de administración.

Estos tipos de cliente no usan un punto de estado de reserva:

- Equipos Mac
- Dispositivos móviles inscritos por Configuration Manager
- Dispositivos móviles que se administran con el conector de Exchange Server

Un punto de estado de reserva no es necesario para supervisar la actividad y el estado del cliente.  

El punto de estado de reserva siempre se comunica con los clientes mediante HTTP, que utiliza conexiones no autenticadas y envía los datos en texto no cifrado. Este comportamiento hace que el punto de estado de reserva sea vulnerable a un ataque, especialmente cuando se utiliza con la administración de clientes basada en Internet. Para ayudar a disminuir la superficie expuesta a ataques, dedique siempre un servidor para ejecutar el punto de estado de reserva. No instale otros roles de sistema de sitio en el mismo servidor en un entorno de producción.  

Instale un punto de estado de reserva si se cumplen todas las condiciones siguientes:  

- Desea que los errores de comunicación de cliente de los equipos Windows se envíen al sitio, aunque estos equipos cliente no puedan comunicarse con un punto de administración.  

- Quiere usar los informes de implementación de cliente de Configuration Manager, que muestran los datos que envía el punto de estado de reserva.  

- Dispone de un servidor dedicado para este rol de sistema de sitio y de medidas de seguridad adicionales para ayudar a proteger el servidor contra los ataques.  

- Las ventajas de utilizar un punto de estado de reserva son mayores que los riesgos de seguridad asociados con conexiones no autenticadas y transferencias de texto no cifrado sobre tráfico HTTP.  

No instale un punto de estado de reserva si los riesgos de seguridad de la ejecución de un sitio web con conexiones no autenticadas y transferencias de texto no cifrado superan a las ventajas de identificar problemas de comunicación de clientes.  

## <a name="reporting-services-point"></a>Punto de servicios de informes

Configuration Manager proporciona muchos informes para ayudarle a supervisar la instalación, asignación y administración de clientes en la consola de Configuration Manager. Algunos de los informes de implementación de cliente requieren que los clientes se asignen a un punto de estado de reserva.  

Los informes no son necesarios para implementar clientes. Puede ver algo de información de implementación en la consola de Configuration Manager o usar los archivos de registro de cliente para información detallada. Sin embargo, los informes de cliente brindan información valiosa para ayudar a supervisar la implementación de cliente y solucionar sus problemas.  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>Punto de inscripción y punto de proxy de inscripción

Configuration Manager requiere el punto de inscripción y el punto de proxy de inscripción para inscribir dispositivos móviles y certificados para equipos Mac. Estos roles de sistema de sitio no son necesarios en las situaciones siguientes:

- Cuando planea administrar dispositivos móviles mediante el conector de Exchange Server.
- Cuando instala el cliente heredado de dispositivo móvil, por ejemplo, Windows CE.
- Cuando solicita e instala el certificado de cliente en equipos Mac de manera independiente desde Configuration Manager.

## <a name="application-catalog"></a>Catálogo de aplicaciones

> [!Important]  
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>Punto de conexión de puerta de enlace de administración en la nube.

Necesita un punto de conector de puerta de enlace de administración en la nube si está configurando una [puerta de enlace de administración en la nube](../../manage/cmg/plan-cloud-management-gateway.md) para [administrar clientes en Internet](../../manage/manage-clients-internet.md).
