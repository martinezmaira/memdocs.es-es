---
title: Compatibilidad con dominios de Active Directory
titleSuffix: Configuration Manager
description: Obtenga información sobre los requisitos para un sistema de sitio de Configuration Manager en un dominio de Active Directory.
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688583"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Compatibilidad con los dominios de Active Directory en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Todos los sistemas de sitio de Configuration Manager deben ser miembros de un dominio de Active Directory compatible. Los equipos cliente de Configuration Manager pueden ser miembros del dominio o miembros del grupo de trabajo.  

## <a name="requirements-and-limitations"></a>Limitaciones y requisitos

- La pertenencia a un dominio también se aplica a los sistemas de sitio que admiten la administración de cliente basada en Internet en una red perimetral. (Estas redes también se conocen como DMZ, zona desmilitarizada y subred filtrada).  

- No se permite cambiar las configuraciones siguientes en un equipo que hospeda un rol de sistema de sitio:  

  - Pertenencia a dominio, incluido si se quita un sistema de sitio del dominio y se vuelve a unir al mismo dominio.

  - Nombre de dominio  

  - Nombre del equipo  

  Antes de realizar estos cambios, desinstale el rol de sistema de sitio. Para realizar estos cambios en un servidor de sitio, desinstale primero el sitio. También puede crear un [servidor de sitio en modo pasivo](../../servers/deploy/configure/site-server-high-availability.md) para ayudar a administrar este cambio en un servidor de sitio.

- Configuration Manager admite el nivel funcional de dominio y de bosque de Windows Server 2008 R2 o versiones posteriores.<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Espacio de nombres no contiguo

Se pueden instalar clientes y sistemas de sitio de Configuration Manager en un dominio que tenga un *espacio de nombres separado*.  

En un espacio de nombres separado, el sufijo DNS principal de un equipo no coincide con el nombre de dominio DNS de Active Directory de ese equipo. Otro escenario de espacio de nombres separado se produce si el nombre de dominio NetBIOS de un controlador de dominio no coincide con el nombre de dominio DNS de Active Directory.  

### <a name="disjoint-scenarios"></a>Escenarios separados

En las secciones siguientes se identifican los escenarios admitidos para un espacio de nombres separado.  

#### <a name="scenario-1"></a>Escenario 1

El sufijo DNS principal del controlador de dominio difiere del nombre de dominio DNS de Active Directory. Los equipos que son miembros del dominio pueden estar separados o no separados.

El controlador de dominio está separado en este escenario. Los equipos que son miembros del dominio, como servidores de sitio y equipos, pueden tener un sufijo DNS principal que coincida con lo siguiente:

- El sufijo DNS principal del controlador de dominio
- El nombre de dominio DNS de Active Directory

#### <a name="scenario-2"></a>Escenario 2

Un equipo miembro en un dominio de Active Directory es separado, aun cuando el controlador de dominio no es separado.

En este escenario, el sufijo DNS principal de un sistema de sitio difiere del nombre de dominio DNS de Active Directory. El sufijo DNS principal del controlador de dominio es el mismo que el nombre de dominio DNS de Active Directory. Los equipos miembro que son clientes de Configuration Manager pueden tener un sufijo DNS principal que coincida con lo siguiente:

- El sufijo DNS principal del servidor de sistema de sitio separado
- El nombre de dominio DNS de Active Directory

### <a name="configure-disjoint-namespace"></a>Configuración del espacio de nombres separado

Para permitir que un equipo tenga acceso a controladores de dominio separados, cambie el atributo de Active Directory **msDS-AllowedDNSSuffixes** en el contenedor de objetos del dominio. Agregue ambos sufijos DNS al atributo.  

Para asegurarse de que la *lista de búsqueda de sufijos DNS* contiene todos los espacios de nombres DNS de la organización, configure la lista de búsqueda para cada equipo en el dominio separado. Incluya los sufijos siguientes en la lista de espacios de nombres:

- El sufijo DNS principal del controlador de dominio.
- El nombre de dominio DNS.
- Los espacios de nombres adicionales de otros servidores con los que Configuration Manager podría comunicarse.

Puede usar la directiva de grupo para configurar la lista **Búsqueda de sufijos de Sistema de nombres de dominio (DNS)** .  

> [!IMPORTANT]  
> Al hacer referencia a un equipo en Configuration Manager, escriba el equipo con el sufijo DNS principal. Este sufijo debe coincidir con el nombre de dominio completo registrado como el atributo de **dnsHostName** en el dominio de Active Directory y el nombre de entidad de seguridad de servicio asociado con el sistema.  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> Dominios de una sola etiqueta

Configuration Manager admite clientes y sistemas de sitio en un dominio de una sola etiqueta cuando se cumplen los criterios siguientes:  

- Configure el dominio de una sola etiqueta en Active Directory Domain Services con un espacio de nombres DNS separado que tenga un dominio de nivel superior válido.  

  **Por ejemplo:** El dominio de una sola etiqueta de Contoso está configurado para tener un espacio de nombres separado en DNS de contoso.com. Al especificar el sufijo DNS en Configuration Manager para un equipo en el dominio Contoso, especifique "Contoso.com" y no "Contoso".  

- Las conexiones del Modelo de objetos componentes distribuido (DCOM) entre los servidores de sitio en el contexto del sistema deben ser correctas mediante el uso de la autenticación Kerberos.  
