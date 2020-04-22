---
title: Planeamiento de la implementación de clientes en equipos Linux y UNIX
titleSuffix: Configuration Manager
description: Planee la implementación de cliente en equipos Linux y UNIX en Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693733"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Planeamiento de la implementación de cliente en equipos Linux y UNIX en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> A partir de la versión 1902, Configuration Manager no admite clientes Linux o UNIX. 
> 
> Para administrar servidores Linux, considere la posibilidad de usar la administración de Microsoft Azure. Las soluciones de Azure tienen una amplia compatibilidad con Linux que, en la mayoría de los casos, supera la funcionalidad de Configuration Manager, incluida la administración de revisiones de un extremo a otro para Linux.

Puede instalar el cliente de Configuration Manager en equipos que ejecutan Linux o UNIX. Este cliente está diseñado para servidores que funcionan como un equipo de grupo de trabajo, y no admite la interacción con usuarios que han iniciado sesión. Una vez que se ha instalado el software cliente y el cliente establece comunicación con el sitio de Configuration Manager, el cliente se administra mediante la consola de Configuration Manager y los informes.  

> [!NOTE]
>  El cliente de Configuration Manager en los equipos UNIX y Linux no admite las siguientes capacidades de administración:  
> 
> - Instalación de inserción de cliente  
>   -   Implementación de sistema operativo  
>   -   Implementación de aplicaciones; en lugar de implementar software mediante paquetes y programas.  
>   -   Inventario de software  
>   -   Actualizaciones de software  
>   -   Configuración de cumplimiento  
>   -   Control remoto  
>   -   Administración de energía  
>   -   Comprobación y corrección de cliente del estado de cliente  
>   -   Administración de cliente basada en Internet  

 Para más información sobre las distribuciones de Linux y UNIX admitidas y el hardware necesario para admitir el cliente de Linux y UNIX, vea [Hardware recomendado para Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Use la información en este artículo para ayudarle a planear la implementación del cliente de Configuration Manager para Linux y UNIX.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a> Requisitos previos para la implementación del cliente en servidores UNIX y Linux  
 Utilice la siguiente información para determinar los requisitos previos para que debe tener correctamente en su lugar instalación al cliente para Linux y UNIX.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a> Dependencias externas a Configuration Manager:  
 En las tablas siguientes se indican los requisitos de los sistemas operativos UNIX y Linux y las dependencias de los paquetes de software.  

 **Red Hat Enterprise Linux Server versión 5.1 (Tikanga)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas estándar C|2.5-12|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8b-8.3.el5|  
|PAM|Módulos de autenticación conectables|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server versión 6**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas estándar C|2.12-1.7|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|1.0.0-4|  
|PAM|Módulos de autenticación conectables|1.1.1-4|  

 **Red Hat Enterprise Linux Server versión 7**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas estándar C|2.17|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|1.0.1|  
|PAM|Módulos de autenticación conectables|1.1.1-4|  

 **Solaris 10 SPARC**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Revisión del sistema operativo|Pérdida de memoria de PAM|117463-05|  
|SUNWlibC|libC incluido en compiladores Sun Workshop (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Bibliotecas de Math & Microtasking (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Bibliotecas de Math & Microtasking (raíz) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Bibliotecas de Core Solaris (raíz) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Bibliotecas de Core Solaris (raíz) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|Bibliotecas de SUNopenssl (Usr)<br /><br /> Sun proporciona las bibliotecas OpenSSL para Solaris 10 SPARC. Están incluidas en el sistema operativo.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Módulos de autenticación conectables<br /><br /> SUNWcsr, Core Solaris, (raíz) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Revisión del sistema operativo|Pérdida de memoria de PAM|117464-04|  
|SUNWlibC|Sun Workshop libc incluido en compiladores (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Bibliotecas de Math & Microtasking (raíz) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (bibliotecas compartidas) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Bibliotecas de Core Solaris (raíz) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|Bibliotecas de SUNWopenssl; Bibliotecas OpenSSL (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Módulos de autenticación conectables<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|libC incluido en compiladores Sun Workshop|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliotecas de Math y Microtasking (raíz)|5.11, REV=2011.04.11|  
|SUNWcslr|Bibliotecas de Core Solaris (raíz)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (bibliotecas compartidas)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (raíz)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|Bibliotecas OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------|-----------|---------------|  
|SUNWlibC|libC incluido en compiladores Sun Workshop|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliotecas de Math y Microtasking (raíz)|5.11, REV=2011.04.11|  
|SUNWcslr|Bibliotecas de Core Solaris (raíz)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (bibliotecas compartidas)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (raíz)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|Bibliotecas OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|Biblioteca compartida estándar C|2.4-31.30|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8a-18,15|  
|PAM|Módulos de autenticación conectables|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Biblioteca compartida estándar C|2.9-13.2|  
|PAM|Módulos de autenticación conectables|pam-1.0.2-20.1|  

 **Universal Linux (Debian package) Debian, Ubuntu Server**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|libc6|Biblioteca compartida estándar C|2.3.6|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8 o 1.0|  
|PAM|Módulos de autenticación conectables|0.79-3|  

 **Universal Linux (RPM package) CentOS, Oracle Linux**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Biblioteca compartida estándar C|2.5-12|  
|Openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8 o 1.0|  
|PAM|Módulos de autenticación conectables|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Versión del sistema operativo|Versión de sistema operativo|AIX 6.1, cualquier nivel de tecnología y Service Pack|  
|xlC.rte|Tiempo de ejecución en XL C/C++|9.0.0.5|  
|OpenSSL/openssl.base|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|Versión del sistema operativo|Versión de sistema operativo|AIX 7.1, cualquier nivel de tecnología y Service Pack|  
|xlC.rte|Tiempo de ejecución en XL C/C++||  
|OpenSSL/openssl.base|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras||  


 **HP-UX 11i v3 IA64**  

|Paquete necesario|Descripción|Versión mínima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|Entorno operativo HP-UX Foundation|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Bibliotecas de desarrollo de IA específico|B.11.31|  
|SysMgmtMin|Herramientas de implementación de software mínimo|B.11.31.0709|  
|SysMgmtMin.openssl|Bibliotecas OpenSSL; Protocolo de comunicaciones de red seguras|A.00.09.08d.002|  
|PAM|Módulos de autenticación conectables|En HP-UX, PAM forma parte de los principales componentes del sistema operativo. No hay otras dependencias.|  

 **Dependencias de Configuration Manager:** en la tabla siguiente se enumeran los roles de sistema de sitio que admiten clientes Linux y UNIX. Para más información sobre estos roles de sistema de sitio, vea [Determinar los roles de sistema de sitio para Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Sistema de sitio de Configuration Manager|Más información|  
|---------------------------------------|----------------------|  
|Punto de administración|Si bien no es necesario un punto de administración para instalar un cliente de Configuration Manager para Linux y UNIX, debe tener un punto de administración para transferir información entre equipos cliente y servidores de Configuration Manager. Sin un punto de administración, no se pueden administrar los equipos cliente.|  
|Punto de distribución|No es necesario el punto de distribución para instalar un cliente de Configuration Manager para Linux y UNIX. Sin embargo, la función de sistema de sitio es necesaria si implementa software en servidores Linux y UNIX.<br /><br /> Dado que el cliente de Configuration Manager para Linux y UNIX no es compatible con las comunicaciones que usan SMB, los puntos de distribución que se utilizan con el cliente deben admitir la comunicación HTTP o HTTPS.|  
|Punto de estado de reserva|El punto de estado de reserva no es necesario para instalar un cliente de Configuration Manager para Linux y UNIX. Sin embargo, permite a los equipos del sitio de Configuration Manager enviar mensajes de estado cuando no se pueden comunicar con un punto de administración. Cliente también puede enviar su estado de instalación en el punto de estado de reserva.|  

 **Requisitos de firewall**: Asegúrese de que los firewalls no bloquean las comunicaciones a través de los puertos que especifique como puertos de solicitud de cliente. El cliente para Linux y UNIX se comunica directamente con los puntos de administración, los puntos de distribución y los puntos de estado de reserva.  

 Para obtener información sobre los puertos de solicitud y comunicación del cliente, consulte [Configurar al cliente para Linux y UNIX buscar puntos de administración](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a> Planeamiento para la comunicación a través de confianzas de bosque para servidores Linux y UNIX  
 Los servidores Linux y UNIX que administre con Configuration Manager funcionan como clientes de grupo de trabajo y requieren configuraciones similares como clientes basados en Windows que se encuentran en un grupo de trabajo. Para información sobre las comunicaciones desde los equipos que están en grupos de trabajo, consulte [Comunicaciones entre bosques de Active Directory](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a> Ubicación del servicio por el cliente para Linux y UNIX  
 La tarea de localizar un servidor de sistema de sitio que proporciona servicio a los clientes se conoce como ubicación del servicio. A diferencia de los clientes basados en Windows, el cliente para Linux y UNIX no utiliza Active Directory para la ubicación del servicio. Además, el cliente de Configuration Manager para Linux y UNIX no admite una propiedad de cliente que especifique el sufijo de dominio de un punto de administración. En su lugar, el cliente obtiene información acerca de los servidores de sistema de sitio adicionales que proporcionan servicios a los clientes desde un punto de administración conocidos que al instalar el software cliente se asigna.  

 Para más información, consulte [Ubicación del servicio y cómo los clientes determinan su punto de administración asignado](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a> Planeamiento de seguridad y certificados para servidores Linux y UNIX  
 Para las comunicaciones autenticadas y seguras con los sitios de Configuration Manager, el cliente de Configuration Manager para Linux y UNIX usa el mismo modelo de comunicación que el cliente para Windows.  

 Cuando se instala el cliente Linux y UNIX, puede asignar al cliente un certificado PKI que le permite usar HTTPS para comunicarse con los sitios de Configuration Manager. Si no asigna un certificado PKI, el cliente crea un certificado autofirmado y se comunica solo por HTTP.  

 Los clientes que se proporcionan un certificado PKI cuando instala usan HTTPS para comunicarse con los puntos de administración. Cuando un cliente no puede localizar un punto de administración que admite HTTPS, se derivará para utilizar HTTP con el certificado PKI proporcionado.  

 Cuando un cliente Linux o UNIX utiliza un certificado PKI, no tiene que aprobarlo. Cuando un cliente usa un certificado autofirmado, revise la configuración de la jerarquía de aprobación de cliente en la consola de Configuration Manager. Si el método de aprobación de cliente no es **Aprobar automáticamente todos los equipos (no recomendados)** , el cliente debe aprobar manualmente.  

 Para más información sobre cómo aprobar manualmente el cliente, consulte [Administrar clientes desde el nodo Dispositivos](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 Para información sobre el uso de certificados en Configuration Manager, consulte los [requisitos de certificados PKI](../../../plan-design/network/pki-certificate-requirements.md).  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a> Acerca de los certificados para su uso por servidores Linux y UNIX  
 El cliente de Configuration Manager para Linux y UNIX usa un certificado autofirmado o un certificado de PKI X.509 igual que los clientes basados en Windows. No hay ningún cambio en los requisitos de la PKI para los sistemas de sitio de Configuration Manager para administrar los clientes de UNIX y Linux.  

 Los certificados que usa para los clientes de UNIX y Linux que se comunican con los sistemas de sitio de Configuration Manager deben tener un formato Public Key Certificate Standard (PKCS #12) y debe conocerse la contraseña para que pueda especificársela al cliente cuando se especifica el certificado PKI.  

 El cliente de Configuration Manager para Linux y UNIX admite un único certificado PKI y no admite varios certificados. Por lo tanto, no se aplican los criterios de selección de certificados que configure para un sitio de Configuration Manager.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a> Configurar certificados para servidores Linux y UNIX  
 Para configurar un cliente de Configuration Manager para servidores Linux y UNIX para que use las comunicaciones HTTPS, debe configurar el cliente para que use un certificado PKI en el momento de instalar el cliente. No se puede aprovisionar un certificado antes de la instalación del software cliente.  

 Cuando se instale un cliente que utiliza un certificado PKI, use el parámetro de línea de comandos `-UsePKICert` para especificar la ubicación y el nombre de un archivo PKCS #12 que contenga el certificado PKI. Además, debe utilizar el parámetro de línea de comandos `-certpw` para especificar la contraseña del certificado.  

 Si no se especifica `-UsePKICert`, el cliente genera un certificado autofirmado e intenta comunicarse con servidores de sistema de sitio solo mediante HTTP.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a> Versiones que no admiten SHA-256  
 Los siguientes sistemas operativos Linux y UNIX que se admiten como clientes para Configuration Manager se publicaron con versiones de OpenSSL que no admiten SHA-256:  

-   Versión 10 de Solaris (SPARC/x86)  


 Para administrar estos sistemas operativos con Configuration Manager, debe instalar el cliente de Configuration Manager para Linux y UNIX con un modificador de línea de comandos que indique al cliente que omita la validación de SHA-256. Los clientes de Configuration Manager que se ejecutan en estas versiones de sistema operativo funcionan en un modo menos seguro que los clientes que admiten SHA-256. Este modo de operación menos seguro tiene el siguiente comportamiento:  

-   Los clientes no validan la firma del servidor de sitio asociada con la directiva que solicitan desde un punto de administración.  

-   Los clientes no validan el hash de los paquetes que descargan desde un punto de distribución.  

> [!IMPORTANT]  
>  La opción `ignoreSHA256validation` le permite ejecutar el cliente para equipos Linux y UNIX en un modo menos seguro. Esto está pensado para su uso en plataformas anteriores que no incluía compatibilidad con SHA-256. Esto es un reemplazo de seguridad y no se recomienda por Microsoft, pero se puede usar en un entorno de centro de datos segura y de confianza.  

 Cuando se instala el cliente de Configuration Manager para Linux y UNIX, la secuencia de comandos de instalación comprueba la versión del sistema operativo. De forma predeterminada, si la versión del sistema operativo se identifica como que se ha publicado sin una versión de OpenSSL que admita SHA-256, la instalación del cliente de Configuration Manager produce un error.  

 Para instalar el cliente de Configuration Manager en los sistemas operativos Linux y UNIX que no se hayan publicado con una versión de OpenSSL que admita SHA-256, debe usar el modificador de instalación de la línea de comandos `ignoreSHA256validation`. Cuando se usa esta opción de línea de comandos en un sistema operativo Linux o UNIX aplicable, el cliente de Configuration Manager omitirá la validación de SHA-256 y, después de la instalación, el cliente no usará SHA-256 para firmar los datos que envía a los sistemas de sitio mediante HTTP. Para información sobre cómo configurar los clientes de Linux y UNIX para usar certificados, consulte [Planeamiento de seguridad y certificados para servidores Linux y UNIX](#BKMK_SecurityforLnU). Para más información sobre cómo solicitar SHA-256, consulte [Configurar la firma y el cifrado](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  La opción de línea de comandos `ignoreSHA256validation` se omite en los equipos que ejecutan una versión de Linux y UNIX que se publicó con versiones de OpenSSL que admiten SHA-256.  
