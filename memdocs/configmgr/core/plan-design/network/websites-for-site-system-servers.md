---
title: Sitios web para sistemas de sitio
titleSuffix: Configuration Manager
description: Obtenga información sobre los sitios web predeterminados y personalizados para servidores de sistema de sitio en Configuration Manager.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 344ba7f6a6b0ee7683c3ac7661338f01be601a10
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701453"
---
# <a name="websites-for-site-system-servers-in-configuration-manager"></a>Websites para servidores de sistema de sitio en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Varios roles de sistema de sitio de Configuration Manager requieren Microsoft Internet Information Services (IIS) y usan el sitio web de IIS predeterminado para hospedar los servicios de sistema de sitio. Si debe ejecutar otras aplicaciones web en el mismo servidor y la configuración no es compatible con Configuration Manager, considere la posibilidad de usar un sitio web personalizado para Configuration Manager.  

> [!TIP]  
>  Como medida de seguridad, le recomendamos dedicar un servidor a los sistemas de sitio de Configuration Manager que necesitan IIS. Al ejecutar otras aplicaciones en un sistema de sitio de Configuration Manager, se aumenta la superficie expuesta a ataques del equipo.  




##  <a name="what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a> Qué debe saber antes de decidirse a usar sitios web personalizados  
 De forma predeterminada, los roles de sistema de sitio usan el **sitio web predeterminado** en IIS. Esto se configura automáticamente al instalar el rol de sistema de sitio. Sin embargo, en los sitios primarios, puede usar en su lugar sitios web personalizados. Al usar sitios web personalizados:  

-   Los sitios web personalizados están habilitados para todo el sitio, en lugar de solo para roles o servidores de sistema de sitio individuales.  

-   En los sitios primarios, cada equipo que hospedará un rol de sistema de sitio apto tiene que configurarse con un sitio web personalizado denominado **SMSWEB**. Hasta que se cree este sitio web y los roles de sistema de sitio en el equipo se configuren para usar el sitio web personalizado, los clientes no podrán comunicarse con los roles de sistema de sitio en ese equipo.  

-   Como los sitios secundarios se configuran automáticamente para usar un sitio web personalizado cuando su sitio primario principal está configurado para ello, también tendrá que crear sitios web personalizados en IIS en cada servidor de sistema de sitio secundario que necesite IIS.  


  **Requisitos previos para usar sitios web personalizados:**  

 Antes de habilitar la opción de usar sitios web personalizados en un sitio, debe hacer lo siguiente:  

-   Cree un sitio web personalizado denominado **SMSWEB** en IIS en cada servidor de sistema de sitio que requiera IIS. Haga esto en el sitio primario y en todos los sitios secundarios.  

-   Configure el sitio web personalizado para que responda al mismo puerto configurado para la comunicación de cliente de Configuration Manager (puerto de solicitud de cliente).  

-   Por cada sitio web personalizado o predeterminado que use una carpeta personalizada, coloque una copia del tipo de documento predeterminado que use en la carpeta raíz que hospeda el sitio web. Por ejemplo, en un equipo con Windows Server 2008 R2 con las configuraciones predeterminadas, **iisstart.htm** es uno de los distintos tipos de documentos predeterminados. Encontrará este archivo en el directorio raíz del sitio web predeterminado. Coloque una copia de este archivo (o una copia del tipo de documento predeterminado que use) en la carpeta raíz que hospeda el sitio web personalizado SMSWEB. Para más información sobre los tipos de documento predeterminados, vea [Default Document &lt;defaultDocument\> for IIS](https://www.iis.net/configreference/system.webserver/defaultdocument) (Documento predeterminado <defaultDocument> para IIS).  

**Acerca de los requisitos de IIS:** 
**Los siguientes roles de sistema de sitio requieren IIS y un sitio web para hospedar los servicios de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de distribución  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Punto de administración  

-   Punto de actualización de software  

-   Punto de migración de estado  

Consideraciones adicionales:  

-   Cuando un sitio primario tiene habilitados sitios web personalizados, los clientes asignados a ese sitio se dirigen para que se comuniquen con los sitios web personalizados, en lugar de comunicarse con los sitios web predeterminados en los servidores de sistema de sitio aptos.  

-   Si usa sitios web personalizados para un sitio primario, puede usar sitios web personalizados para todos los sitios primarios de la jerarquía para asegurarse de que los clientes puedan moverse correctamente en la jerarquía. (La movilidad significa que un equipo cliente se mueve a un nuevo segmento de red que está administrado por otro sitio. La itinerancia puede afectar a los recursos a los que puede acceder un cliente de forma local, en lugar de acceder con un vínculo WAN).  

-   Los roles de sistema de sitio que usan IIS, pero que no aceptan conexiones de cliente (como el punto de servicios de informes), también usan el sitio web SMSWEB en lugar del sitio web predeterminado.  

-   Para sitios web personalizados, necesitará asignar números de puerto distintos de los que usa el sitio web predeterminado del equipo. El sitio web predeterminado y el sitio web personalizado no se pueden ejecutar al mismo tiempo si ambos sitios tratan de usar los mismos puertos TCP/IP.  

-   Los puertos TCP/IP que se configuran en IIS para el sitio web personalizado tienen que coincidir con los puertos de solicitud de cliente del sitio.  

## <a name="switch-between-default-and-custom-websites"></a>Cambiar entre sitios web predeterminados y personalizados  
Aunque puede activar o desactivar la casilla para usar sitios web personalizados en un sitio primario en cualquier momento (la casilla se encuentra en la pestaña General de las Propiedades del sitio), planee detenidamente el cambio antes de realizarlo. Al cambiar esta configuración, es necesario desinstalar y reinstalar todos los roles de sistema de sitio correspondientes en el sitio primario y en los sitios secundarios:  

Los siguientes roles **se reinstalan automáticamente**:  

-   Punto de administración  

-   Punto de distribución  

-   Punto de actualización de software  

-   Punto de estado de reserva  

-   Punto de migración de estado  

Los siguientes roles deben **reinstalarse manualmente**:  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

Además:  

-   Cuando se pasa de usar el sitio web predeterminado a usar un sitio web personalizado, Configuration Manager no quita los directorios virtuales antiguos. Si quiere quitar los archivos que usó Configuration Manager, debe eliminar manualmente los directorios virtuales que se crearon en el sitio web predeterminado.  

-   Si cambia el sitio para que use sitios web personalizados, será necesario volver a configurar los clientes que ya estén asignados al sitio para que usen los nuevos puertos de solicitud de cliente para los sitios web personalizados. Vea [Cómo configurar puertos de comunicación de cliente](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Configuración de sitios web personalizados  
Dado que los pasos para crear un sitio web personalizado varían según las versiones del sistema operativo, debe consultar la documentación de la versión de su sistema operativo para conocer los pasos exactos, pero puede usar la información siguiente cuando sea aplicable:  

-   El nombre del sitio web tiene que ser: **SMSWEB**.  

-   Al configurar el protocolo HTTPS, necesita especificar un certificado SSL para guardar la configuración.  

-   Después de crear el sitio web personalizado, quite los puertos de sitio web personalizado que use desde otros sitios web en IIS:  

    1.  Edite los **enlaces** de los demás sitios web para quitar los puertos que coincidan con los asignados al sitio web **SMSWEB**.  

    2.  Inicie el sitio web **SMSWEB**.  

    3.  Reinicie el servicio **SMS_SITE_COMPONENT_MANAGER** en el servidor de sitio.  
