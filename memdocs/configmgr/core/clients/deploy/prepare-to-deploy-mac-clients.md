---
title: Preparación de la implementación de clientes en equipos Mac
titleSuffix: Configuration Manager
description: Tareas de configuración previas a la implementación del cliente de Configuration Manager en Mac.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d0968a61be4e450bb145b309f61de0d6c212549
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694823"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Preparativos para la implementación de software cliente en Mac

*Se aplica a: Configuration Manager (rama actual)*

Siga estos pasos para asegurarse de que está listo para [implementar el cliente de Configuration Manager en equipos Mac](deploy-clients-to-macs.md).



## <a name="mac-prerequisites"></a>Requisitos previos de Mac

El paquete de instalación del cliente Mac no se suministra con los medios de Configuration Manager. Descargue los **clientes para sistemas operativos adicionales** del [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?LinkID=525184).  

Para obtener una lista de las versiones compatibles, vea [Sistemas operativos compatibles con clientes y dispositivos](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).



## <a name="certificate-requirements"></a>Requisitos de certificados

Para la instalación y la administración de clientes para equipos Mac se necesitan certificados de infraestructura de clave pública (PKI). Los certificados PKI protegen la comunicación entre los equipos Mac y el sitio de Configuration Manager mediante transferencias de datos cifrados y autenticación mutua. Configuration Manager puede solicitar e instalar un certificado de cliente de usuario. Utiliza servicios de certificados con una entidad de certificación empresarial y los puntos de inscripción y de proxy de inscripción de Configuration Manager. También puede solicitar e instalar un certificado de equipo independientemente de Configuration Manager. Este certificado debe cumplir los requisitos de certificado de Configuration Manager.  

Los clientes Mac de Configuration Manager siempre buscan una revocación de certificado. No se puede deshabilitar esta función.  

Si los clientes Mac no encuentran la lista de revocación de certificados (CRL), no pueden conectarse a sistemas de sitio de Configuration Manager. Especialmente para los clientes Mac en un bosque diferente a la entidad de certificación emisora, compruebe el diseño de la CRL. Asegúrese de que los clientes Mac puedan encontrar y descargar una CRL.  

Antes de instalar el cliente de Configuration Manager en un equipo Mac, decida cómo va a instalar el certificado de cliente:  

-   Usar la inscripción de Configuration Manager mediante la [herramienta CMEnroll](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll). El proceso de inscripción no admite la renovación automática de certificados. Vuelva a inscribir los equipos Mac antes de que expire el certificado.  

-   [Usar una solicitud de certificado y un método de instalación independiente de Configuration Manager](deploy-clients-to-macs.md#bkmk_external).  

Para obtener más información sobre los requisitos del certificado de cliente Mac, vea [Requisitos de certificados PKI para Configuration Manager](../../plan-design/network/pki-certificate-requirements.md).  

Los clientes Mac se asignan automáticamente al sitio de Configuration Manager que los administra. Los clientes Mac se instalan como clientes de solo Internet, incluso si la comunicación está restringida a la intranet. Esta configuración indica que se comunican con puntos de distribución y puntos de administración habilitados para Internet en su sitio asignado. Los equipos Mac no se comunican con sistemas de sitio fuera del sitio al que están asignados.  

> [!IMPORTANT]  
>  El cliente para macOS de Configuration Manager no se puede usar para conectarse con un punto de administración que está configurado para usar una [réplica de base de datos](../../servers/deploy/configure/database-replicas-for-management-points.md).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implementar un certificado de servidor web en servidores de sistema de sitio  

Si estos sistemas de sitio no tienen un certificado de servidor web, debe implementarlo en los equipos que tengan estos roles de sistema de sitio:  

-   Punto de administración  

-   Punto de distribución  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

El certificado de servidor web debe incluir el FQDN de Internet que se especifica en las propiedades del sistema de sitio. No es necesario que el servidor sea accesible desde Internet para admitir equipos Mac. Si no requiere administración de cliente basada en Internet, puede especificar el FQDN de la intranet para el FQDN de Internet.  

Especifique el FQDN de Internet del sistema de sitio en el certificado de servidor web para el punto de administración, el punto de distribución y el punto de proxy de inscripción.

Para obtener más información sobre una implementación de ejemplo, vea [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implementar un certificado de autenticación de cliente en servidores de sistema de sitio  

Si estos sistemas de sitio no tienen un certificado de autenticación de cliente, impleméntelo en los equipos que tengan estos roles de sistema de sitio:  

-   Punto de administración  

-   Punto de distribución  

Para obtener una implementación de ejemplo en la que se crea y se instala el certificado de cliente para puntos de administración, vea [Implementación del certificado de cliente para equipos Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

Para obtener una implementación de ejemplo en la que se crea y se instala el certificado de cliente para puntos de distribución, vea [Implementación del certificado de cliente para puntos de distribución](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  Para implementar el cliente en dispositivos que ejecutan macOS Sierra, el nombre de asunto del certificado de punto de administración se debe configurar correctamente mediante. Por ejemplo, use el FQDN del servidor de punto de administración.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Preparar la plantilla de certificado de cliente para equipos Mac  

La plantilla de certificado debe tener permisos de **lectura** e **inscripción** para la cuenta de usuario que inscriba el certificado en el equipo Mac.  

Para obtener más información, vea [Implementación del certificado de cliente para equipos Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Configurar el punto de administración y el punto de distribución  

Configure los puntos de administración para las siguientes opciones:  

-   HTTPS  

-   Permitir conexiones de cliente desde Internet. Este valor de configuración es necesario para administrar equipos Mac. Pero eso no significa que los servidores del sistema de sitio deben ser accesibles desde Internet.  

-   Permitir a los dispositivos móviles y equipos Mac usar este punto de administración  

Los puntos de distribución no son necesarios para instalar el cliente para Mac. Si quiere implementar software en estos equipos después de instalar el cliente, configure los puntos de distribución para permitir conexiones de cliente desde Internet.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar puntos de administración y puntos distribución para admitir equipos Mac  

Antes de iniciar este procedimiento, asegúrese de configurar el punto de administración y el punto de distribución con un FQDN de Internet. Si estos servidores no admiten la administración de cliente basada en Internet, especifique el FQDN de intranet como FQDN de Internet.

Los roles de sistema de sitio deben estar en un sitio primario.  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Servidores y roles del sistema de sitios**. Después seleccione el servidor que tenga los roles de sistema de sitio adecuados.  

2.  En el panel de detalles, seleccione el rol **Punto de administración** y haga clic en **Propiedades** en la cinta. En la ventana **Propiedades del punto de administración**, configure estas opciones:  

    1.  Elija **HTTPS**.  

    2.  Elija **Permitir conexiones de cliente solo de Internet** o **Permitir conexiones de cliente a la intranet y a Internet**. Estas opciones requieren un FQDN de Internet o de intranet.  

    3.  Seleccione **Permitir a los dispositivos móviles y equipos Mac usar este punto de administración**.  

    4. Haga clic en **Aceptar** para guardar esta configuración.  

3.  En el panel de detalles del nodo Roles de servidores y de sistema, seleccione el rol **Punto de distribución** y haga clic en **Propiedades** en la cinta de opciones. En la ventana **Propiedades del punto de distribución**, configure estas opciones:  

    -   Elija **HTTPS**.  

    -   Elija **Permitir conexiones de cliente solo de Internet** o **Permitir conexiones de cliente a la intranet y a Internet**. Estas opciones requieren un FQDN de Internet o de intranet.  

    -   Seleccione **Importar certificado**, busque el archivo del certificado del punto de distribución de cliente exportado y, después, especifique la contraseña.  

4.  Repita este procedimiento para todos los puntos de administración y puntos de distribución de los sitios primarios que administran equipos Mac.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurar el punto de proxy de inscripción y el punto de inscripción  

Instale ambos roles en el mismo sitio. No es necesario instalarlos en el mismo servidor de sistema de sitio ni en el mismo bosque de Active Directory.  

Para más información sobre la ubicación del rol de sistema de sitio y consideraciones al respecto, vea [Roles de sistema de sitio](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles).  

Para agregar los roles de sistema de sitio para admitir equipos Mac, vea [instalar roles de sistema de sitio](../../servers/deploy/configure/install-site-system-roles.md).

En la página **Selección de rol del sistema**, seleccione **Punto de proxy de inscripción** y **Punto de inscripción** en la lista de roles disponibles.  



## <a name="install-the-reporting-services-point"></a>instalar el punto de servicios de informes  

Para más información, vea [Instalar el punto de servicios de informes](../../servers/manage/configuring-reporting.md).  



## <a name="next-steps"></a>Pasos siguientes

[Implementación del cliente de Configuration Manager en equipos Mac](deploy-clients-to-macs.md)  
