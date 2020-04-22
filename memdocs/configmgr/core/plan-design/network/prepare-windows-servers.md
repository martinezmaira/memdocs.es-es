---
title: Preparación de los servidores Windows
titleSuffix: Configuration Manager
description: Asegúrese de que un equipo cumpla los requisitos previos para su uso como servidor de sitio o servidor del sistema de sitio de Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8889c0ee306eaaf682563b2e8e72d5482054d1c7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690263"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Preparar los servidores de Windows para admitir Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para poder usar un equipo Windows como servidor de sistema de sitio para Configuration Manager, el equipo debe cumplir los requisitos previos para su uso previsto como servidor de sitio o servidor de sistema de sitio.  

- Estos requisitos previos suelen incluir una o varias características o roles de Windows, que se habilitan con el Administrador del servidor de los equipos.  

- Como el método para habilitar los roles y características de Windows difiere en las distintas versiones de sistemas operativos, consulte la documentación de la versión de su sistema operativo para obtener información detallada sobre cómo configurar el sistema operativo que usa.  

Este artículo proporciona información general sobre los tipos de configuraciones de Windows que son necesarios para admitir sistemas de sitio de Configuration Manager. Para obtener información detallada sobre la configuración de roles de sistema de sitio específicos, vea [Requisitos previos de sitio y sistema de sitio para System Center Configuration Manager](../configs/site-and-site-system-prerequisites.md).

##  <a name="windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a> Roles y características de Windows  
Al configurar los roles y las características de Windows en un equipo, puede tenga que reiniciar el equipo para completar la configuración. Por consiguiente, conviene identificar los equipos que hospedarán roles de sistema de sitio específicos antes de instalar un sitio o un servidor de sistema de sitio de Configuration Manager.

### <a name="features"></a>Funciones  
En determinados servidores de sistema de sitio se requieren las siguientes características de Windows, que deben configurarse antes de instalar un rol de sistema de sitio en ese equipo.  

- **.NET Framework**, que incluye:  

    - ASP.NET  
    - Activación de HTTP  
    - Activación que no sea HTTP  
    - Servicios de Windows Communication Foundation (WCF)  

    Los diferentes roles de sistema de sitio requieren diferentes versiones de .NET Framework.  

    Como .NET Framework 4.0 y versiones posteriores no pueden reemplazar la versión 3.5 y anteriores, si las distintas versiones se indican como necesarias, planee habilitar cada versión en el mismo equipo.  

- **Servicio de transferencia inteligente en segundo plano (BITS)** : Los puntos de administración requieren BITS y las opciones seleccionadas de forma automática para admitir la comunicación con los dispositivos administrados.  

- **BranchCache**: pueden configurarse puntos de distribución con BranchCache para admitir clientes que usen BranchCache.  

- **Desduplicación de datos**: los puntos de distribución pueden configurarse con desduplicación de datos para beneficiarse de ella.  

- **Compresión diferencial remota (RDC)** : cada equipo que hospeda un servidor de sitio o un punto de distribución requiere RDC. RDC se usa para generar firmas de paquete y realizar comparaciones de firma.  

### <a name="roles"></a>Roles  
Se requieren los siguientes roles de Windows para admitir determinadas funcionalidades, como las actualizaciones de software y las implementaciones de sistema operativo, mientras que los roles de sistema de sitio más comunes requieren IIS.  

- **Servicio de inscripción de dispositivos de red** (en Servicios de certificados de Active Directory): este rol de Windows es un requisito previo para el uso de perfiles de certificado en Configuration Manager.  

- **Servidor web (IIS)** : que incluye:  
    - Características HTTP comunes  
          - Redirección HTTP  
    - Desarrollo de aplicaciones  
          - Extensibilidad de .NET  
          - ASP.NET  
          - Extensiones ISAPI  
          - Filtros ISAPI  
    - Herramientas de administración  
          - Compatibilidad con la administración de IIS 6  
          - Compatibilidad con la metabase de IIS 6  
          - Compatibilidad de Instrumental de administración de Windows (WMI) con IIS 6  
    - Seguridad  
          - Filtrado de solicitudes  
          - Autenticación de Windows  

  Los siguientes roles de sistema de sitio usan una o varias de las configuraciones de IIS que se muestran:  
  - Punto de servicio web del catálogo de aplicaciones  
  - Punto de sitios web del catálogo de aplicaciones  
  - Punto de distribución  
  - Punto de inscripción  
  - Punto de proxy de inscripción  
  - Punto de estado de reserva  
  - Punto de administración  
  - Punto de actualización de software  
  - Punto de migración de estado     

  La versión mínima de IIS requerida es la versión suministrada con el sistema operativo del servidor de sitio.  

  Además de estas configuraciones de IIS, quizás tenga que configurar [Filtrado de solicitudes IIS para puntos de distribución](#BKMK_IISFiltering).  

- **Servicios de implementación de Windows**: este rol se usa con la implementación del sistema operativo.  

- **Windows Server Update Services**: este rol es necesario para las actualizaciones de software.  


##  <a name="iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a> Filtrado de solicitudes IIS para puntos de distribución  
De forma predeterminada, IIS usa el filtrado de solicitudes para impedir el acceso a varias extensiones de nombre de archivo y ubicaciones de carpetas mediante la comunicación HTTP o HTTPS. En un punto de distribución, esto impide que los clientes descarguen paquetes que tienen extensiones o ubicaciones de carpeta bloqueadas.  

Cuando los archivos de origen de paquete tienen extensiones bloqueadas en IIS por la configuración del filtrado de solicitudes, debe configurar el filtrado de solicitudes de modo que las permita. Para ello, [edite la característica Filtrado de solicitudes](https://technet.microsoft.com/library/hh831621.aspx) en el Administrador de IIS en los equipos de los puntos de distribución.  

Además, Configuration Manager usa las siguientes extensiones de nombre de archivo para paquetes y aplicaciones. Asegúrese de que la configuración de Filtrado de solicitudes no bloquea estas extensiones de archivo:  

- .PCK  
- .PKG  
- .STA  
- .TAR  

Por ejemplo, puede que los archivos de origen de una implementación de software incluyan una carpeta llamada **bin** o tengan un archivo con la extensión de nombre de archivo **.mdb** .  

- De forma predeterminada, el filtrado de solicitudes de IIS bloquea el acceso a estos elementos (**bin** se bloquea como segmento oculto y **.mdb** se bloquea como extensión de nombre de archivo).  

- Cuando se usa la configuración de IIS predeterminada en un punto de distribución, los clientes que usan BITS no pueden descargar esta implementación de software desde el punto de distribución e indican que están esperando contenido.  

- Para que los clientes puedan descargar este contenido, en cada punto de distribución correspondiente, modifique la opción **Filtrado de solicitudes** en el Administrador de IIS para permitir el acceso a las extensiones de archivo y las carpetas incluidas en los paquetes y las aplicaciones que implemente.  

> [!IMPORTANT]  
> Las modificaciones que se realicen en el filtro de solicitudes pueden aumentar la superficie del equipo expuesta a ataques.  
> 
> - Las modificaciones que se realicen en el nivel de servidor se aplican a todos los sitios web del servidor.   
>     - Las modificaciones que se realicen en sitios web individuales se aplican solo a ese sitio web.  
> 
> Como recomendación de seguridad, se aconseja ejecutar Configuration Manager en un servidor web dedicado. Si debe ejecutar otras aplicaciones en el servidor web, use un sitio web personalizado para Configuration Manager. Para obtener más información, vea [Sitios web para servidores de sistema de sitio](websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>Verbos HTTP
**Puntos de administración:** para garantizar que los clientes puedan comunicarse correctamente con un punto de administración, en el servidor de punto de administración, asegúrese de que los verbos HTTP enumerados a continuación estén permitidos:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Puntos de distribución:** los puntos de distribución requieren que los verbos HTTP enumerados a continuación estén permitidos:
- GET
- HEAD
- PROPFIND

Para obtener más información, vea [Configure request filtering in IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs) (Configurar el filtrado de solicitudes en IIS). 
