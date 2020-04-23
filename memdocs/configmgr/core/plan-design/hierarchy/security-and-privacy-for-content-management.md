---
title: Seguridad y privacidad de la administración de contenido
titleSuffix: Configuration Manager
description: Optimice la seguridad y privacidad para la administración de contenido en Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704483"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Seguridad y privacidad para la administración de contenido en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo contiene información sobre seguridad y privacidad para la administración de contenido en Configuration Manager. 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> Prácticas recomendadas de seguridad para la administración de contenido  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Ventajas y desventajas de HTTPS o HTTP para los puntos de distribución de intranet
Para los puntos de distribución en la intranet, tenga en cuenta las ventajas y desventajas de usar HTTPS y HTTP. En la mayoría de los escenarios, el uso de HTTP y cuentas de acceso de paquete para la autorización proporciona mayor seguridad que usar HTTPS con cifrado pero sin autorización. Sin embargo, si tiene datos confidenciales en el contenido que desea cifrar durante la transferencia, utilice HTTPS.  

-   **Cuando usa HTTPS para un punto de distribución**, Configuration Manager no usa cuentas de acceso de paquetes para autorizar el acceso al contenido, pero el contenido se cifra cuando se transfiere a través de la red.  

-   **Cuando usa HTTP para un punto de distribución**, puede usar cuentas de acceso de paquetes para la autorización, pero el contenido no se cifra cuando se transfiere a través de la red.  

A partir de la versión 1806, le recomendamos que habilite **HTTP mejorado** para el sitio. Esta característica permite a los clientes usar autenticación de Azure Active Directory para comunicarse de forma segura con un punto de distribución HTTP. Para obtener más información, vea [HTTP mejorado](enhanced-http.md).

#### <a name="protect-the-client-authentication-certificate-file"></a>Protección del certificado de autenticación de cliente
Si utiliza un certificado de autenticación de cliente de PKI en lugar de un certificado autofirmado para el punto de distribución, proteja el archivo de certificado (.pfx) con una contraseña fuerte. Si almacena el archivo en la red, proteja el canal de red al importar el archivo en el Configuration Manager.

Si requiere una contraseña para importar el certificado de autenticación de cliente que el punto de distribución usa para comunicarse con los puntos de administración, esta configuración ayuda a proteger el certificado contra posibles ataques. Use la firma del Bloque de mensajes del servidor (SMB) o IPsec entre la ubicación de red y el servidor de sitio para impedir que un atacante pueda manipular el archivo del certificado.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Eliminación del rol de punto de distribución desde el servidor de sitio
De forma predeterminada, el programa de instalación de Configuration Manager instala un punto de distribución en el servidor de sitio. Los clientes no tienen que comunicarse directamente con el servidor de sitio. Para reducir la superficie expuesta a ataques, asigne el rol de punto de distribución a otros sistemas de sitio y quítelo del servidor de sitio.  

#### <a name="secure-content-at-the-package-access-level"></a>Protección del contenido en el nivel de acceso de paquete
El recurso compartido de punto de distribución permite acceso de lectura a todos los usuarios. Para restringir qué usuarios pueden acceder al contenido, utilice cuentas de acceso de paquete si el punto de distribución está configurado para HTTP. Esta configuración no se aplica a los puntos de distribución de nube, que no admiten cuentas de acceso de paquetes. Para obtener más información, vea [Cuentas de acceso de paquetes](accounts.md#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Configuración de IIS en el rol de punto de distribución
Si Configuration Manager instala IIS cuando se agrega un rol de sistema de sitio de punto de distribución, quite la redirección HTTP o las herramientas y scripts de administración de IIS cuando termine la instalación del punto de distribución. El punto de distribución no requiere redirección HTTP ni herramientas y scripts de administración de IIS. Para reducir la superficie expuesta a ataques, quite estos servicios de rol del rol de servidor web.  Para obtener más información sobre los servicios de rol para el rol de servidor web para puntos de distribución, vea [Sitio y requisitos previos de sistema de sitio](../configs/site-and-site-system-prerequisites.md).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Establezca permisos de acceso de paquete al crear el paquete
Dado que los cambios que se hagan en las cuentas de acceso en los archivos de paquete entran en vigencia solo cuando se redistribuye el paquete, defina los permisos de acceso de paquete cuidadosamente al crear el paquete. Esta configuración es especialmente importante cuando el paquete es grande o se distribuye a muchos puntos de distribución, y la capacidad de ancho de banda de red para la distribución de contenido es limitada.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implemente controles de acceso para proteger los medios que tienen contenido preconfigurado
El contenido preconfigurado está comprimido pero no cifrado. Un atacante podría leer y modificar los archivos que se descargan a los dispositivos. Los clientes de Configuration Manager rechazan el contenido que se ha alterado, pero lo descargan igualmente.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Importación de contenido preconfigurado con ExtractContent
Importe contenido preconfigurado solo mediante la herramienta de línea de comandos ExtractContent.exe. Para evitar la manipulación y la elevación de privilegios, use solo la herramienta de línea de comandos autorizada que se suministra con Configuration Manager.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Proteja el canal de comunicación entre el servidor de sitio y la ubicación de origen del paquete
Use la firma SMB o IPsec entre el servidor de sitio y la ubicación de origen del paquete al crear aplicaciones y paquetes. Esta configuración ayuda a evitar que un atacante pueda manipular los archivos de origen.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Eliminación de los directorios virtuales predeterminados para el sitio web personalizado con el rol de punto de distribución
Si cambia la opción de configuración de sitio para usar un sitio web personalizado en lugar del predeterminado después de instalar un rol de punto de distribución, quite los directorios virtuales predeterminados. Cuando se cambia del sitio web predeterminado a uno personalizado, Configuration Manager no quita los directorios virtuales antiguos. Quite los directorios virtuales siguientes que Configuration Manager ha creado originalmente en el sitio web predeterminado:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Para los puntos de distribución de nube, proteja los detalles de la suscripción de Azure y los certificados
Si usa puntos de distribución de nube, proteja los elementos de gran valor siguientes:
- El nombre de usuario y la contraseña para la suscripción de Azure
- El certificado de administración de Azure 
- El certificado de servicio de punto de distribución de nube

Almacene los certificados de forma segura. Si llega hasta ellos a través de la red al configurar el punto de distribución de nube, use la firma SMB o IPsec entre el servidor de sitio y la ubicación de origen.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Para la continuidad del servicio, supervise la fecha de expiración de los certificados de punto de distribución de nube.
Configuration Manager no le avisa cuando los certificados importados para el punto de distribución de nube están a punto de expirar. Supervise las fechas de expiración con independencia de Configuration Manager. Asegúrese de renovar y después importar los nuevos certificados antes de la fecha de expiración. Esta acción es importante si adquiere un certificado de autenticación de servidor de un proveedor público externo, porque podría necesitar tiempo adicional para adquirir un certificado renovado.  

 Si el certificado expira, el Administrador de servicios de nube genera el identificador de mensaje de estado **9425**. El archivo CloudMgr.log contiene una entrada para indicar que el certificado **está en estado expirado** y la fecha de expiración también se registra en UTC.  



## <a name="security-considerations-for-content-management"></a>Consideraciones de seguridad para la administración de contenido  

Tenga en cuenta los puntos siguientes al planear la administración de contenido:  

-   Los clientes no validan el contenido hasta después de descargarlo.  

     Los clientes de Configuration Manager validan el hash de contenido solo después de descargarlo en su caché cliente. Si un atacante manipula la lista de archivos que se van a descargar o el contenido en sí, el proceso de descarga puede ocupar un ancho de banda considerable hasta que el cliente después vea que debe desechar el contenido al detectar un hash no válido.  

-   Cuando usa puntos de distribución de nube, el acceso al contenido se restringe de forma automática a la empresa. No se puede restringir más a usuarios o grupos seleccionados.  

-   Si usa puntos de distribución de nube, los clientes son autenticados por el punto de administración y luego usan un token de Configuration Manager para acceder a los puntos de distribución de nube. El token es válido durante ocho horas. Este comportamiento significa que, si se bloquea un cliente porque deja de ser de confianza, puede seguir descargando contenido desde un punto de distribución de nube hasta que expire el período de validez de este token. En ese momento, el punto de administración no emitirá otro token para el cliente porque el cliente está bloqueado.  

     Para evitar que un cliente bloqueado descargue contenido en este período de ocho horas, detenga el servicio de nube. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Puntos de distribución en la nube**.  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Información de privacidad para la administración de contenido  

 Configuration Manager no incluye ningún dato de usuario en los archivos de contenido, aunque es posible que un usuario administrativo decida realizar esta acción.  



## <a name="see-also"></a>Vea también

- [Conceptos básicos de la administración de contenido](fundamental-concepts-for-content-management.md)  

- [Seguridad y privacidad de la administración de aplicaciones](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [Seguridad y privacidad de las actualizaciones de software](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [Seguridad y privacidad para la implementación de sistema operativo](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
