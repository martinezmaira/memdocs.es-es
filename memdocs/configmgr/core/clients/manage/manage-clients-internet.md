---
title: Administrar clientes en Internet
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar clientes con Cloud Management Gateway y la administración de clientes basados en Internet en Configuration Manager.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715601"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Administrar clientes en Internet con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Normalmente en Configuration Manager, la mayoría de los equipos y servidores administrados se encuentran físicamente en la misma red interna que los servidores de sistema de sitio que realizan funciones de administración. Pero los clientes se pueden administrar fuera de la red interna si están conectados a Internet. Esta capacidad no requiere que los clientes se conecten a través de VPN para tener acceso a los servidores de sistema de sitio.

Configuration Manager proporciona dos maneras de administrar los clientes conectados a Internet:

- Puerta de enlace de administración en la nube

- Administración de cliente basada en Internet

> [!NOTE]
> Puede tener una combinación de ambos servicios para un único sitio. Si un dispositivo obtiene la directiva del sitio para IBCM y CMG, usa para la comunicación uno u otro de forma aleatoria. El único mecanismo disponible para controlar la comunicación es la autenticación del cliente. Por ejemplo, si un cliente unido a Azure AD no confía en el certificado de autenticación del servidor del punto de administración basado en Internet, solo puede usar la instancia de CMG. Si un cliente unido a un dominio no confía en el certificado de autenticación del servidor de CMG, solo puede usar el punto de administración basado en Internet.<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>Puerta de enlace de administración en la nube

Cloud Management Gateway (CMG) proporciona administración de clientes basados en Internet. Usa una combinación de un servicio en la nube de Microsoft Azure y un rol del sistema de sitio local que se comunica con ese servicio. Los clientes basados en Internet usan el servicio en la nube para comunicarse con la instancia local de Configuration Manager.

### <a name="cmg-advantages"></a>Ventajas de CMG

- No se necesita ninguna inversión local adicional en infraestructura.  

- No expone la infraestructura local en Internet.  

- Las máquinas virtuales en la nube que ejecutan el servicio se administran completamente con Azure y no necesitan mantenimiento.  

- Se instala y configura fácilmente en la consola de Configuration Manager.  

### <a name="cmg-disadvantages"></a>Desventajas de CMG  

- Costo de la suscripción en la nube.  

- Los datos de administración se envían a través del servicio en la nube.  

Para obtener más información, consulte [Plan for cloud management gateway (Plan para la puerta de enlace de administración en la nube)](cmg/plan-cloud-management-gateway.md).  

## <a name="internet-based-client-management"></a>Administración de cliente basada en Internet

Este método se basa en los servidores del sistema de sitio accesible desde Internet con los que se comunican los clientes directamente con fines de administración. Requiere que los clientes y los servidores del sistema de sitio se configuren para la administración basada en Internet (IBCM).

### <a name="ibcm-advantages"></a>Ventajas de IBCM

- No hay dependencia de servicio en la nube.  

- No hay ningún costo adicional asociado con una suscripción a la nube.  

- Control completo de los servidores y los roles que proporcionan el servicio.  

### <a name="ibcm-disadvantages"></a>Desventajas de IBCM

- Se necesita una inversión adicional en infraestructura.  

- Costos generales y operativos de la infraestructura adicional.  

- La infraestructura se debe exponer en Internet.  

Para obtener más información, vea [Plan para la administración de cliente basada en Internet](plan-internet-based-client-management.md).  
