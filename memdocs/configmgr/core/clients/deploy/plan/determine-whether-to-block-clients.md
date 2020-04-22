---
title: Bloqueo de clientes
titleSuffix: Configuration Manager
description: Bloquee el acceso de clientes para la seguridad del sistema mediante Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01fd7944d8a6ab726712f6ebeb4cb5374896072
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693743"
---
# <a name="determine-whether-to-block-clients-in-configuration-manager"></a>Determinar si se deben bloquear clientes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Si un equipo cliente o un dispositivo móvil cliente deja de ser de confianza, puede bloquear el cliente en la consola de System Center 2012 Configuration Manager. La infraestructura de Configuration Manager rechaza los clientes bloqueados para que no se puedan comunicar con los sistemas de sitio para descargar directivas, cargar datos de inventario o enviar mensajes de estado.  

 Debe bloquear y desbloquear a un cliente desde su sitio asignado en lugar de hacerlo desde un sitio secundario o un sitio de administración central.  

> [!IMPORTANT]  
>  Si bien el bloqueo en Configuration Manager puede ayudar a proteger el sitio de Configuration Manager, no se debe confiar en que esta característica protegerá el sitio contra equipos o dispositivos móviles que no son de confianza si permite que los clientes se comuniquen con sistemas de sitio mediante HTTP, ya que un cliente bloqueado puede volver a unirse al sitio con un nuevo certificado autofirmado y un nuevo identificador de hardware. En cambio, use la característica de bloqueo para bloquear medios de arranque perdidos o comprometidos que se usan para implementar sistemas operativos y cuando los sistemas de sitio acepten conexiones de cliente HTTPS.  

 No es posible bloquear los clientes que tienen acceso al sitio mediante el certificado de proxy de ISV. Para más información sobre el certificado de proxy de ISV, vea el kit de desarrollo de software (SDK) de Configuration Manager.  

 Si los sistemas de sitio aceptan conexiones de cliente HTTPS y la infraestructura de clave pública (PKI) admite una lista de revocación de certificados (CRL), considere siempre la revocación de certificados como la primera línea de defensa contra certificados que puedan estar comprometidos. El bloqueo de clientes en Configuration Manager ofrece una segunda línea de defensa para proteger la jerarquía.  

##  <a name="considerations-for-blocking-clients"></a><a name="BKMK_Block_vs_CRL"></a> Consideraciones para el bloqueo de clientes  

-   Esta opción está disponible para conexiones de cliente HTTP y HTTPS, pero brinda seguridad limitada cuando los clientes se conectan a los sistemas de sitio mediante HTTP.  

-   Los usuarios administrativos de Configuration Manager tienen autoridad para bloquear un cliente, y esta acción se realiza en la consola de Configuration Manager.  

-   La comunicación de cliente solo puede rechazarse desde la jerarquía de Configuration Manager.  

    > [!NOTE]  
    >  El mismo cliente podría registrarse en una jerarquía de Configuration Manager diferente.  

-   El cliente queda inmediatamente bloqueado en el sitio de Configuration Manager.  

-   Ayuda a proteger los sistemas de sitio contra equipos y dispositivos móviles potencialmente comprometidos.  

## <a name="considerations-for-using-certificate-revocation"></a>Consideraciones sobre el uso de la revocación de certificados  

-   Esta opción está disponible para las conexiones de cliente de Windows HTTPS si la infraestructura de clave pública es compatible con una lista de revocación de certificados (CRL).  

     Los clientes Mac siempre realizan una comprobación de CRL y esta funcionalidad no puede deshabilitarse.  

     Si bien los clientes de dispositivos móviles no usan listas de revocación de certificados para comprobar los certificados de los sistemas de sitio, Configuration Manager puede comprobar y revocar sus certificados.  

-   Los administradores de infraestructura de clave pública poseen la autoridad para revocar un certificado, y esta acción se realiza fuera de la consola de Configuration Manager.  

-   La comunicación de cliente puede rechazarse desde cualquier equipo o dispositivo móvil que requiere este certificado de cliente.  

-   Es probable que exista un retraso entre el momento en que se revoca un certificado y el momento en que los sistemas de sitio descargan la lista de revocación de certificados (CRL) modificada.  

-   Para muchas de las implementaciones de PKI, este retraso puede ser de un día o más. Por ejemplo, en Servicios de certificados de Active Directory, el período de expiración predeterminado es de una semana para una CRL completa y de un día para una CRL de diferencias.  

-   Ayuda a proteger los sistemas de sitio y los clientes contra equipos y dispositivos móviles potencialmente comprometidos.  

    > [!NOTE]  
    >  Puede proteger aún más los sistemas de sitio que ejecutan IIS contra clientes desconocidos mediante la configuración de una lista de certificados de confianza (CTL) en IIS.  
