---
title: Propiedades de instalación de cliente en Active Directory
titleSuffix: Configuration Manager
description: Publique propiedades de instalación de cliente de Configuration Manager en Active Directory Domain Services.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692073"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services

*Se aplica a: Configuration Manager (rama actual)*

Cuando extiende el esquema de Active Directory para Configuration Manager y el sitio se publica en Active Directory Domain Services, muchas propiedades de instalación de cliente se publican en Active Directory Domain Services. Si un equipo puede ubicar estas propiedades de instalación de cliente, puede usarlas durante la implementación de cliente de Configuration Manager.  

 Las ventajas de utilizar Servicios de dominio de Active Directory para publicar propiedades de instalación de cliente incluyen:  

-   La instalación de cliente basada en punto de actualización de software y las instalaciones de cliente de directiva de grupo no requieren que los parámetros de instalación se configuren en cada equipo.  

-   Dado que esta información se genera automáticamente, se elimina el riesgo de error humano asociado con escribir manualmente las propiedades de la instalación.  

> [!NOTE]  
>  Para más información sobre cómo extender el esquema de Active Directory para Configuration Manager y cómo publicar un sitio, vea [Extensiones de esquema para Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Propiedades de instalación de cliente publicadas en Active Directory Domain Services  
La siguiente es una lista de las propiedades de instalación de cliente. Para más información sobre cada uno de los elementos siguientes, vea [Acerca de las propiedades de instalación de cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

- Código de sitio de Configuration Manager.  

- El certificado de firma de servidor de sitio.  

- La clave raíz confiable.  

- Los puertos de comunicación de cliente para HTTP y HTTPS.  

- El punto de estado de reserva. Si el sitio tiene varios puntos de estado de reserva, se publicará en Active Directory Domain Services solo el primero que se instaló.  

- Un valor para indicar que el cliente debe comunicarse solo mediante HTTPS.  

- Configuración relacionada con certificados PKI:  

  -   Si se utiliza un certificado PKI de cliente.  

  -   Los criterios de selección para la selección de certificados. Esto puede ser necesario porque el cliente tiene más de un certificado PKI válido que se puede usar para Configuration Manager.  

  -   Una opción para determinar el certificado que se va a usar si el cliente tiene varios certificados válidos después del proceso de selección de certificado.  

  -   La lista de emisores de certificados que contiene una lista de certificados de CA raíz confiables.  

- Propiedades de instalación de client.msi especificados en la pestaña **Cliente** del cuadro de diálogo **Propiedades de instalación de inserción de cliente** .

La instalación de cliente (CCMSetup) usa las propiedades publicadas en Active Directory Domain Services solo si no se especifican otras propiedades mediante cualquiera de los métodos siguientes:  

-   El método de instalación manual (que se describe más adelante en este artículo).

-   El método de instalación de directiva de grupo (que se describe más adelante en este artículo).

> [!NOTE]  
>  Las propiedades de instalación de cliente se usan para instalar el cliente. Estas propiedades se pueden sobrescribir con nuevas configuraciones del correspondiente sitio asignado después de que el cliente se haya instalado y se haya asignado correctamente a un sitio de Configuration Manager.  

 Aplique la información de las secciones siguientes para determinar qué métodos de instalación de cliente de Configuration Manager usan Active Directory Domain Services para obtener las propiedades de instalación de cliente.  

## <a name="client-push-installation"></a>Instalación de inserción de cliente  
 La instalación de inserción de cliente no usa Servicios de dominio de Active Directory para obtener las propiedades de instalación.  

 En vez de ello, puede especificar las propiedades de instalación de cliente en la pestaña **Propiedades de instalación** del cuadro de diálogo **Propiedades de instalación de inserción de cliente**. Estas opciones y la configuración de sitio relacionada con el cliente se almacenan en un archivo que el cliente lee durante la instalación de cliente.  

> [!NOTE]  
>  No es necesario que especifique ninguna propiedad de CCMSetup para la instalación de inserción de cliente, el punto de estado de reserva o la clave raíz confiable en la pestaña **Propiedades de instalación**. Estos valores se suministran automáticamente a los clientes cuando se instalan mediante la instalación de inserción de cliente.
Además de las propiedades de Client.msi, CCMSetup admite estos parámetros: forcereboot, /skipprereq, /logon, /BITSPriority, /downloadtimeout, /forceinstall

 Las propiedades especificadas en la pestaña **Propiedades de instalación** se publican en Active Directory Domain Services si el sitio se publica ahí. Las instalaciones de cliente leen esta configuración cuando se ejecuta CCMSetup sin propiedades de instalación.  

## <a name="software-update-point-based-installation"></a>Instalación basada en el punto de actualización de software  
 El método de instalación basada en el punto de actualización de software no es compatible con la incorporación de propiedades de instalación en la línea de comandos de CCMSetup.  

 Si no se ha aprovisionado ninguna propiedad de línea de comandos en el equipo cliente mediante una directiva de grupo, CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory.  

## <a name="group-policy-installation"></a>Instalación de directiva de grupo  
 El método de instalación de directiva de grupo no es compatible con la incorporación de propiedades de instalación en la línea de comandos de CCMSetup.  

 Si no se ha aprovisionado ninguna propiedad de línea de comandos en el equipo cliente, CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory.  

## <a name="manual-installation"></a>Instalación manual  
 CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory en las siguientes circunstancias:  

-   No se especifican propiedades de línea de comandos después del comando CCMSetup.exe.  

-   El equipo no se ha aprovisionado con propiedades de instalación mediante una directiva de grupo.  

## <a name="logon-script-installation"></a>Instalación de script de inicio de sesión  
 CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory en las siguientes circunstancias:  

-   No se especifican propiedades de línea de comandos después del comando CCMSetup.exe.  

-   El equipo no se ha aprovisionado con propiedades de instalación mediante una directiva de grupo.  

## <a name="software-distribution-installation"></a>Instalación de distribución de software  
 CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory en las siguientes circunstancias:  

-   No se especifican propiedades de línea de comandos después del comando CCMSetup.exe.  

-   El equipo no se ha aprovisionado con propiedades de instalación mediante una directiva de grupo.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Instalaciones para clientes que no pueden tener acceso a Active Directory Domain Services  
Estos equipos cliente no pueden leer ni tener acceso a las propiedades de instalación publicadas desde Active Directory Domain Services.

 Entre estos clientes se incluyen:  

-   Equipos de grupo de trabajo.  

-   Clientes asignados a un sitio de Configuration Manager que no está publicado en Active Directory Domain Services.  

-   Clientes que se instalan cuando están en Internet.  
