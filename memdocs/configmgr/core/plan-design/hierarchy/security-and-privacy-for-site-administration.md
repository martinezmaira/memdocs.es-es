---
title: Seguridad y privacidad de la administración de sitios
titleSuffix: Configuration Manager
description: Optimización de la seguridad y privacidad para la administración de sitios en Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35c2738b363895671528196e99b324fd2fe6f5a7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704583"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Seguridad y privacidad para la administración de sitios en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo contiene información sobre la seguridad y privacidad de la jerarquía y los sitios de Configuration Manager.

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a> Guía de seguridad para la administración de sitios

Use la siguiente guía para proteger los sitios y la jerarquía de Configuration Manager.  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>Ejecución del programa de instalación desde una fuente de confianza y protección de la comunicación

Con el fin de evitar que alguien altere los archivos de origen, ejecute el programa de instalación de Configuration Manager desde una fuente de confianza. Si almacena los archivos en la red, asegure la ubicación de red.  

Si ejecuta el programa de instalación desde una ubicación de red, para impedir que un atacante altere los archivos mientras se transmiten por la red, use la firma SMB o IPsec entre la ubicación de origen de los archivos de instalación y el servidor del sitio.  

Si usa el Descargador del programa de instalación para descargar los archivos que necesita el programa de instalación, asegúrese de que también protege la ubicación donde se almacenan estos archivos. Proteja también el canal de comunicación para esta ubicación cuando ejecute el programa de instalación.  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Extensión del esquema de Active Directory y publicación de sitios en el dominio  

Las extensiones de esquema no son necesarias para ejecutar Configuration Manager, pero crean un entorno más seguro. Los clientes y los servidores de sitio pueden recuperar información de una fuente de confianza.  

Si los clientes no están en un dominio de confianza, implemente los siguientes roles de sistema de sitio en los dominios de los clientes:  

- Punto de administración  

- Punto de distribución  

> [!NOTE]  
> Un dominio de confianza para Configuration Manager requiere la autenticación Kerberos. Si los clientes están en otro bosque que no tiene una confianza de bosque bidireccional con el bosque del servidor del sitio, se considera que estos clientes están en un dominio que no es de confianza. Una confianza externa no es suficiente para este propósito.  

### <a name="use-ipsec-to-secure-communications"></a>Uso de IPsec para proteger las comunicaciones

Aunque Configuration Manager protege la comunicación entre el servidor del sitio y el equipo que ejecuta SQL Server, Configuration Manager no protege las comunicaciones entre los roles de sistema de sitio y SQL Server. Solo puede configurar algunos sistemas del sitio con HTTPS para la comunicación entre sitios.  

Si no utiliza controles adicionales para proteger estos canales de servidor a servidor, los atacantes pueden utilizar diversos ataques de suplantación de identidad y de tipo "Man in the middle" contra los sistemas de sitio. Use la firma SMB cuando no pueda utilizar IPsec.  

> [!Important]  
> Proteja el canal de comunicación entre el servidor del sitio y el servidor de origen del paquete. Esta comunicación utiliza SMB. Si no se puede utilizar IPsec para proteger esta comunicación, use la firma SMB para asegurarse de que no se alteren los archivos antes de que los clientes los descarguen y ejecuten.  

### <a name="dont-change-the-default-security-groups"></a>No cambiar los grupos de seguridad predeterminados

No cambie los grupos de seguridad siguientes que Configuration Manager crea y administra para la comunicación del sistema de sitio:

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager crea y administra de forma automática estos grupos de seguridad. Este comportamiento incluye la eliminación de cuentas de equipo cuando se quita un rol de sistema de sitio.  

Para garantizar la continuidad del servicio y los privilegios mínimos, no modifique manualmente estos grupos.  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>Administración del proceso de aprovisionamiento de la clave raíz confiable

Si los clientes no pueden consultar el catálogo global de información de Configuration Manager, deben emplear la clave raíz confiable para autenticar puntos de administración válidos. La clave raíz confiable se almacena en el registro del cliente. Se puede establecer mediante la directiva de grupo o la configuración manual.  

Si el cliente no tiene una copia de la clave raíz confiable antes de contactar con un punto de administración por primera vez, confiará en el primer punto de administración con el que se comunique. Para reducir el riesgo de que un atacante dirija erróneamente los clientes a un punto de administración no autorizado, puede aprovisionar los clientes previamente con la clave raíz confiable. Para obtener más información, consulte [Planeación de la clave raíz confiable](../security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="use-non-default-port-numbers"></a>Uso de números de puerto no predeterminados

El uso de números de puerto no predeterminados puede proporcionar seguridad adicional. Hacen que sea más difícil para los atacantes explorar el entorno para preparar un ataque. Si decide usar puertos no predeterminados, planéelos antes de instalar Configuration Manager. Úselos de forma coherente en todos los sitios de la jerarquía. Los puertos de solicitud de cliente y Wake on LAN son ejemplos donde se pueden usar números de puerto no predeterminados.  

### <a name="use-role-separation-on-site-systems"></a>Uso de la separación de roles en sistemas de sitio

Aunque puede instalar todos los roles de sistema de sitio en un único equipo, esta práctica se utiliza muy poco en redes de producción. Crea un único punto de error.  

### <a name="reduce-the-attack-profile"></a>Reducción del perfil de ataque

El aislamiento de cada rol de sistema de sitio en un servidor diferente reduce la posibilidad de que un ataque contra las vulnerabilidades de un sistema de sitio se use contra un sistema de sitio diferente. Muchos roles requieren la instalación de Internet Information Services (IIS) en el sistema de sitio, lo que necesita un aumento de la superficie de ataque. Si debe combinar roles para reducir los gastos en hardware, combine roles de IIS únicamente con otros roles que requieran IIS.  

> [!IMPORTANT]  
> El rol de punto de estado de reserva es una excepción. Como este rol de sistema de sitio acepta datos no autenticados de los clientes, no asigne nunca el rol de punto de estado de reserva a ningún otro rol de sistema de sitio de Configuration Manager.  

### <a name="configure-static-ip-addresses-for-site-systems"></a>Configuración de direcciones IP estáticas para los sistemas de sitio

Las direcciones IP estáticas son más fáciles de proteger frente a ataques de resolución de nombre.  

Las direcciones IP estáticas también facilitan la configuración de IPsec. El uso de IPsec es una práctica recomendada de seguridad para proteger la comunicación entre sistemas de sitio en Configuration Manager.  

### <a name="dont-install-other-applications-on-site-system-servers"></a>No instalar otras aplicaciones en los servidores de sistema de sitio

Al instalar otras aplicaciones en servidores de sistema de sitio, aumenta la superficie de ataque de Configuration Manager. También corre el riesgo de sufrir problemas de incompatibilidad.  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>Exigir la firma y habilitar el cifrado como una opción de sitio

Habilite las opciones de firma y cifrado para el sitio. Asegúrese de que todos los clientes pueden admitir el algoritmo hash SHA-256 y, después, habilite la opción **Requerir SHA-256**.  

### <a name="restrict-and-monitor-administrative-users"></a>Restricción y supervisión de los usuarios administrativos

Conceda acceso administrativo a Configuration Manager solo a los usuarios de confianza. Después, concédales los permisos mínimos que necesiten mediante los roles de seguridad integrados o la personalización de los roles de seguridad. Los usuarios administrativos que pueden crear, modificar e implementar software y configuraciones pueden controlar potencialmente los dispositivos en la jerarquía de Configuration Manager.  

Audite periódicamente las asignaciones de usuarios administrativos y su nivel de autorización para comprobar los cambios necesarios.  

Para obtener más información, vea [Configurar la administración basada en roles](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="secure-configuration-manager-backups"></a>Protección de las copias de seguridad de Configuration Manager

Cuando realiza una copia de seguridad de Configuration Manager, esta información incluye los certificados y otros datos confidenciales que un atacante podría usar para la suplantación.  

Al transferir estos datos a través de la red, utilice la firma SMB o IPsec y asegure la ubicación de copia de seguridad.  

### <a name="secure-locations-for-exported-objects"></a>Protección de las ubicaciones de los objetos exportados

Al exportar o importar objetos desde la consola de Configuration Manager a una ubicación de red, proteja la ubicación y el canal de red.

Restrinja quién puede tener acceso a la carpeta de red.  

Para impedir que un atacante altere los datos exportados, utilice la firma SMB o IPsec entre el servidor del sitio y la ubicación de red. Proteja también la comunicación entre el equipo que ejecuta la consola de Configuration Manager y el servidor del sitio. Use IPsec para cifrar los datos en la red y así evitar la revelación de información.  

### <a name="manually-remove-certificates-from-failed-servers"></a>Quitar manualmente los certificados de los servidores con errores

Si un sistema de sitio no se puede desinstalar correctamente o deja de funcionar y no se puede restaurar, quite de forma manual los certificados de Configuration Manager para este servidor desde otros servidores de Configuration Manager.

Para quitar la confianza de mismo nivel establecida originalmente con el sistema de sitio y los roles de sistema de sitio, quite de forma manual los certificados de Configuration Manager del servidor que ha dado error en el almacén de certificados de **Personas de confianza** en otros servidores de sistema de sitio. Esta acción es importante si reutiliza el servidor sin cambiar el formato.  

Para más información, vea [Controles criptográficos para la comunicación de servidor](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication).  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>No configurar sistemas de sitio basados en Internet para enlazar la red perimetral

No configure servidores de sistema de sitio para que sean de hosts múltiples, para que se conecten a la red perimetral y la intranet. Aunque esta configuración permite que los sistemas de sitio basados en Internet acepten conexiones de clientes desde Internet y la intranet, se elimina un límite de seguridad entre la red perimetral y la intranet.  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>Configuración del servidor del sitio para iniciar conexiones a las redes perimetrales

Si un sistema de sitio se encuentra en una red que no es de confianza, como una red perimetral, configure el servidor del sitio para iniciar conexiones al sistema de sitio.

De forma predeterminada, los sistemas de sitio inician conexiones con el servidor del sitio para transferir datos. Esta configuración puede suponer un riesgo de seguridad cuando el inicio de la conexión procede de una red que no es de confianza a la red de confianza. Cuando los sistemas de sitio aceptan conexiones desde Internet o residen en un bosque que no es de confianza, configure la opción de sistema de sitio para **Requerir al servidor del sitio iniciar conexiones a este sistema de sitio**. Después de la instalación del sistema de sitio y de cualquier rol, el servidor del sitio inicia todas las conexiones desde la red de confianza.  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>Uso del puente SSL y la terminación con autenticación

Si utiliza un servidor proxy web para la administración de cliente basada en Internet, utilice el protocolo de puente de SSL a SSL, mediante el uso de la terminación con autenticación.

Cuando configure la terminación SSL en el servidor proxy web, los paquetes de Internet están sujetos a inspección antes de que se reenvíen a la red interna. El servidor proxy web autentica la conexión desde el cliente, la termina y, después, abre una conexión autenticada nueva a los sistemas de sitio basados en Internet.  

Cuando los equipos cliente de Configuration Manager usan un servidor proxy web para conectarse a sistemas de sitio basados en Internet, la identidad del cliente (GUID) se incluye de forma segura en la carga de paquete. Después, el punto de administración no tiene en cuenta que el servidor proxy web es el cliente.

Si el servidor proxy web no es compatible con los requisitos del protocolo de puente SSL, también se admite el protocolo de túnel SSL. Esta opción es menos segura. Los paquetes SSL de Internet se reenvían a los sistemas de sitio sin terminación. No se pueden inspeccionar en busca de contenido malintencionado.  

> [!WARNING]  
> Los dispositivos móviles inscritos por Configuration Manager no pueden usar el protocolo de puente SSL. Solo deben usar el protocolo de túnel SSL.  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>Configuraciones usadas si configura el sitio para reactivar equipos para instalar software

- Si usa paquetes de reactivación tradicionales, use la unidifusión en lugar de difusiones dirigidas a la subred.  

- Si tiene que usar difusiones dirigidas a la subred, configure los enrutadores para permitir solo difusiones dirigidas de IP desde el servidor de sitio y solo en un número de puerto no predeterminado.  

Para obtener más información sobre las diferentes tecnologías de Wake on LAN, vea [Planear la reactivación de clientes en System Center Configuration Manager](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>Si utiliza la notificación por correo electrónico, configure el acceso autenticado al servidor SMTP de correo electrónico

Siempre que sea posible, utilice un servidor de correo que admita el acceso autenticado. Use la cuenta del equipo del servidor del sitio para la autenticación. Si debe especificar una cuenta de usuario para la autenticación, utilice una cuenta que tenga los privilegios mínimos.  


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> Guía de seguridad del servidor del sitio

Use la siguiente guía para ayudarle a proteger el servidor del sitio de Configuration Manager.  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>Instalación de Configuration Manager en un servidor miembro en lugar de en un controlador de dominio

No es necesario instalar los sistemas de sitio ni el servidor del sitio de Configuration Manager en un controlador de dominio. Los controladores de dominio no tienen una base de datos de administración de cuentas de seguridad (SAM) local distinta de la base de datos de dominio. Cuando se instala Configuration Manager en un servidor miembro, se pueden mantener las cuentas de Configuration Manager en la base de datos SAM local en lugar de en la base de datos de dominio.  

Esta práctica permite además reducir la superficie expuesta a ataques en los controladores de dominio.  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>Instalación de sitios secundarios sin copiar los archivos a través de la red

Cuando ejecute el programa de instalación y cree un sitio secundario, no seleccione la opción de copiar los archivos del sitio primario en el sitio secundario. Tampoco use una ubicación de origen de red. Si copia los archivos a través de la red, un atacante experimentado podría secuestrar el paquete de instalación del sitio secundario y alterar los archivos antes de que se instalen. Resultaría difícil sincronizar este tipo de ataque. Este ataque se puede mitigar mediante el uso de IPsec o SMB al transferir los archivos.  

En lugar de copiar los archivos a través de la red, en el servidor de sitio secundario, copie los archivos de origen desde la carpeta de medios a una carpeta local. Después, cuando ejecute el programa de instalación para crear un sitio secundario, en la página **Archivos de origen de instalación**, seleccione **Usar los archivos de origen de la siguiente ubicación del equipo de sitio secundario (opción más segura)** y especifique esta carpeta.  

Para obtener más información, vea [Instalar un sitio secundario](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary).

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>La instalación del rol del sitio hereda los permisos de la raíz de la unidad

<!-- SCCMDocs#1380 -->
Asegúrese de configurar correctamente los permisos de la unidad del sistema antes de instalar el primer rol de sistema de sitio en cualquier servidor. Por ejemplo, `C:\SMS_CCM` hereda los permisos de `C:\`. Si la raíz de la unidad no está protegida correctamente, los usuarios con derechos reducidos pueden acceder al contenido de la carpeta de Configuration Manager o modificarlo.


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> Guía de seguridad de SQL Server

Configuration Manager usa SQL Server como base de datos back-end. Si la base de datos está en peligro, los atacantes podrían omitir Configuration Manager. Si acceden a SQL Server directamente, pueden lanzar ataques a través de Configuration Manager. Tenga en cuenta que los ataques contra SQL Server son de alto riesgo y deben mitigarse de forma adecuada.  

Use la siguiente guía de seguridad para proteger SQL Server para Configuration Manager.  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>No usar el servidor de base de datos de sitio de Configuration Manager para ejecutar otras aplicaciones de SQL Server

Al ampliar el acceso al servidor de base de datos de sitio de Configuration Manager, esta acción incrementa el riesgo de los datos de Configuration Manager. Si la base de datos de sitio de Configuration Manager se ve comprometida, también estarán en peligro las demás aplicaciones del mismo equipo con SQL Server.  

### <a name="configure-sql-server-to-use-windows-authentication"></a>Configuración de SQL Server para utilizar la autenticación de Windows

Aunque Configuration Manager acceda a la base de datos de sitio mediante una cuenta y la autenticación de Windows, aún se puede configurar SQL Server para que use el modo mixto de SQL Server. El modo mixto de SQL Server permite inicios de sesión de SQL adicionales para acceder a la base de datos. Esta configuración no es necesaria y aumenta la superficie de ataque.  

### <a name="update-sql-server-express-at-secondary-sites"></a>Actualización de SQL Server Express en los sitios secundarios

Cuando se instala un sitio primario, Configuration Manager descarga SQL Server Express desde el Centro de descarga de Microsoft. Después, copia los archivos en el servidor del sitio primario. Cuando se instala un sitio secundario y se selecciona la opción que permite instalar SQL Server Express, Configuration Manager instala la versión descargada anteriormente. No comprueba si hay nuevas versiones disponibles. Para asegurarse de que el sitio secundario tiene las últimas versiones, realice una de las tareas siguientes:  

- Una vez instalado el sitio secundario, ejecute Windows Update en el servidor del sitio secundario.  

- Antes de instalar el sitio secundario, instale manualmente SQL Server Express en el servidor del sitio secundario. Asegúrese de instalar la última versión y las actualizaciones de software. Después, instale el sitio secundario y seleccione la opción de usar una instancia de SQL Server existente.  

Ejecute periódicamente Windows Update para todas las versiones instaladas de SQL Server. Esta práctica garantiza que dispongan de las últimas actualizaciones de software.  

### <a name="follow-general-guidance-for-sql-server"></a>Seguimiento de la guía general de SQL Server

Identifique y siga la guía general de la versión de SQL Server. En cambio, tenga en cuenta los siguientes requisitos de Configuration Manager:  

- La cuenta de equipo del servidor de sitio debe ser miembro del grupo de administradores del equipo que ejecuta SQL Server. Si sigue la recomendación de SQL Server de "aprovisionar entidades de seguridad de administración explícitamente", la cuenta usada para ejecutar el programa de instalación en el servidor de sitio debe ser miembro del grupo de usuarios de SQL.  

- Si instala SQL Server mediante una cuenta de usuario de dominio, asegúrese de que la cuenta de equipo del servidor del sitio está configurada para un nombre de entidad de seguridad de servicio (SPN) publicado en Active Directory Domain Services. Sin el SPN, se producirá un error en la autenticación Kerberos y se producirá un error en la instalación de Configuration Manager.  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> Guía de seguridad de los sistemas de sitio que ejecutan IIS

Varios roles de sistema de sitio en Configuration Manager requieren IIS. El proceso de protección de IIS permite a Configuration Manager funcionar correctamente y reducir el riesgo de que se produzcan ataques de seguridad. Cuando resulte práctico, minimice el número de servidores que requieren IIS. Por ejemplo, ejecute solo el número de puntos de administración que requiera para su base de clientes, teniendo en cuenta la alta disponibilidad y el aislamiento de red para la administración de cliente basada en Internet.  

Use la siguiente guía de seguridad para proteger los sistemas de sitio que ejecutan IIS.  

### <a name="disable-iis-functions-that-you-dont-require"></a>Deshabilitar las funciones de IIS innecesarias

Instale sólo las funciones de IIS mínimas necesarias para el rol de sistema de sitio que vaya a instalar. Para obtener más información, consulte [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  

### <a name="configure-the-site-system-roles-to-require-https"></a>Configuración de los roles de sistema de sitio para que se requiera HTTPS

Cuando los clientes se conectan a un sistema de sitio mediante HTTP en lugar de HTTPS, utilizan la autenticación de Windows. Este comportamiento puede revertir al uso de la autenticación NTLM en lugar de la autenticación Kerberos. Cuando se utiliza la autenticación NTLM, podría ocurrir que los clientes se conecten a un servidor no autorizado.  

La excepción a esta guía pueden ser los puntos de distribución. Las cuentas de acceso de los paquetes no funcionan cuando el punto de distribución está configurado para HTTPS. Las cuentas de acceso de paquetes conceden autorización para el contenido, de modo que puede restringir qué usuarios pueden acceder al contenido. Para obtener más información, consulte [Prácticas recomendadas de seguridad para la administración de contenido](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>Configuración de una lista de certificados de confianza (CTL) en IIS para los roles de sistema de sitio

Roles de sistema de sitio:  

- Un punto de distribución configurado para HTTPS  

- Un punto de administración configurado para HTTPS y compatible con los dispositivos móviles

Una lista de certificados de confianza (CTL) es una lista definida de entidades de certificación raíz de confianza. Cuando se usa una CTL con una directiva de grupo y la implementación de una infraestructura de clave pública (PKI), una CTL le permite complementar las entidades de certificación raíz de confianza existentes que están configuradas en la red. Por ejemplo, las entidades de certificación que se instalan automáticamente con Microsoft Windows o que se agregan con las entidades de certificación raíz de Windows Enterprise. Cuando se configura una CTL en IIS, esta define un subconjunto de dichas entidades de certificación raíz de confianza.  

Este subconjunto ofrece mayor control sobre la seguridad. La CTL limita los certificados de cliente para que solo se acepten los emitidos por la lista de entidades de certificación de la CTL. Por ejemplo, Windows se comercializa con varios certificados de conocidas entidades de certificación de terceros, como VeriSign y Thawte.

De forma predeterminada, el equipo que ejecuta IIS confía en los certificados vinculados a estas entidades de certificación conocidas. Si no configura IIS con una CTL con una CTL para los roles de sistema de sitio enumerados, el sitio acepta como cliente válido cualquier dispositivo que tenga un certificado de cliente emitido por estas entidades. Si se configura IIS con una CTL que no incluya estas entidades de certificación, el sitio rechazará las conexiones de cliente si el certificado está vinculado a estas entidades de certificación. Para que se acepten los clientes de Configuration Manager para los roles de sistema de sitio enumerados, debe configurar IIS con una CTL que especifique las entidades de certificación usadas por los clientes de Configuration Manager.  

> [!NOTE]  
> Solo los roles de sistema de sitio enumerados requieren la configuración de una CTL en IIS. La lista de emisores de certificados que Configuration Manager usa para los puntos de administración proporciona la misma funcionalidad para los equipos cliente cuando se conectan a puntos de administración de HTTPS.  

Para más información sobre cómo configurar una lista de entidades de certificación de confianza en IIS, vea la documentación de IIS.  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>No colocar el servidor del sitio en un equipo con IIS

La separación de roles ayuda a reducir el perfil de ataque y a mejorar la capacidad de recuperación. La cuenta de equipo del servidor del sitio suele tener privilegios administrativos en todos los roles de sistema de sitio. También puede tener estos privilegios en los clientes de Configuration Manager, si utiliza la instalación de inserción de cliente.  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Uso de los servidores IIS dedicados para Configuration Manager

Aunque puede hospedar varias aplicaciones web en los servidores IIS que también usa Configuration Manager, esto puede ocasionar un aumento significativo de la superficie expuesta a ataques. La configuración incorrecta de una aplicación podría facilitar que un atacante asuma el control de un sistema de sitio de Configuration Manager. Esta vulneración podría ocasionar que un atacante asuma el control de la jerarquía.  

Si debe ejecutar otras aplicaciones web en los sistemas de sitio de Configuration Manager, cree un sitio web personalizado para los sistemas de sitio de Configuration Manager.  

### <a name="use-a-custom-website"></a>Uso de un sitio web personalizado

Para los sistemas de sitio que ejecutan IIS, configure Configuration Manager para que use un sitio web personalizado en lugar del sitio web predeterminado. Si tiene que ejecutar otras aplicaciones web en el sistema de sitio, debe usar un sitio web personalizado. Se trata de una configuración para todo el sitio en lugar de una configuración para un sistema de sitio específico.  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>Al usar sitios web personalizados, quitar los directorios virtuales predeterminados

Cuando se pasa de usar el sitio web predeterminado a usar un sitio web personalizado, Configuration Manager no quita los directorios virtuales antiguos. Quite los directorios virtuales que Configuration Manager creó originalmente en el sitio web predeterminado.  

Por ejemplo, quite los siguientes directorios virtuales de un punto de distribución:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>Seguimiento de la guía de seguridad del servidor IIS

Identifique y siga la guía general de la versión del servidor IIS. Tenga en cuenta cualquier requisito que Configuration Manager tenga en cuanto a los roles de sistema de sitio específicos. Para obtener más información, consulte [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> Guía de seguridad del punto de administración

Los puntos de administración son la interfaz principal entre los dispositivos y Configuration Manager. Tenga en cuenta que los ataques contra el punto de administración y el servidor en el que se ejecuta son de alto riesgo y deben mitigarse de forma adecuada. Aplique todas las instrucciones de seguridad apropiadas y supervise si se detecta alguna actividad inusual.  

Use la siguiente guía de seguridad para proteger un punto de administración de Configuration Manager.  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>Asignación del cliente de un punto de administración al mismo sitio

Evite el escenario en el que un cliente de Configuration Manager que está en un punto de administración se asigne a un sitio que no sea el sitio del punto de administración.  

Si va a migrar desde una versión anterior a la rama actual de Configuration Manager, migre el cliente del punto de administración en el nuevo sitio tan pronto como sea posible.  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> Guía de seguridad del punto de estado de reserva

Si instala un punto de estado de reserva en Configuration Manager, use la siguiente guía de seguridad:

Para obtener más información sobre las consideraciones de seguridad al instalar un punto de estado de reserva, consulte [Determinar si necesita un punto de estado de reserva](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>No ejecutar ningún otro rol en el mismo sistema de sitio

El punto de estado de reserva está diseñado para aceptar la comunicación no autenticada desde cualquier equipo. Si ejecuta este rol de sistema de sitio con otros roles o con un controlador de dominio, el riesgo para ese servidor aumenta considerablemente.  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>Instalación del punto de estado de reserva antes de instalar los clientes con certificados PKI

Si los sistemas de sitio de Configuration Manager no aceptan la comunicación del cliente HTTP, podría ignorar que los clientes no se administran a causa de problemas de certificados relacionados con PKI. Si asigna los clientes a un punto de estado de reserva, notificarán estos problemas de certificados mediante el punto de estado de reserva.  

Por motivos de seguridad, no se puede asignar un punto de estado de reserva a los clientes después de la instalación. Solo se puede asignar este rol durante la instalación del cliente.  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>Evitar usar el punto de estado de reserva en la red perimetral

Por motivos de diseño, el punto de estado de reserva acepta datos de cualquier cliente. Aunque un punto de estado de reserva en la red perimetral puede ayudarle a solucionar problemas de clientes basados en Internet, busque el equilibrio entre las ventajas que comporta la solución de problemas y el riesgo que implica un sistema de sitio que acepta datos no autenticados en una red de acceso público.  

Si instala el punto de estado de reserva en la red perimetral o en una red que no es de confianza, configure el servidor del sitio para iniciar las transferencias de datos. No utilice la configuración predeterminada que permite al punto de estado de reserva iniciar una conexión con el servidor del sitio.  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a> Problemas de seguridad para la administración de sitios

Revise los siguientes problemas de seguridad de Configuration Manager:  

- Configuration Manager no tiene ninguna defensa contra usuarios administrativos que usan Configuration Manager para atacar la red. Los usuarios administrativos no autorizados plantean un alto riesgo de seguridad. Podrían iniciar muchos ataques, entre los que se incluyen las estrategias siguientes:  

    - Usar la implementación de software para instalar y ejecutar de forma automática software malintencionado en cada equipo cliente de Configuration Manager de la organización.  

    - Controlar de forma remota un cliente de Configuration Manager sin permiso del cliente.  

    - Configure intervalos de sondeo rápidos y cantidades de inventario excesivas. Esta acción crea ataques de denegación de servicio contra clientes y servidores.  

    - Utilizar un sitio en la jerarquía para escribir datos en los datos de Active Directory de otro sitio.  

    La jerarquía de sitios es el límite de seguridad. Considere que los sitios solo son límites de administración.  

    Audite la actividad de todos los usuarios administrativos y revise los registros de auditoría con regularidad. Requiera la realización de comprobaciones de antecedentes de todos los usuarios administrativos de Configuration Manager. Exija comprobaciones periódicas como requisito contractual.  

- Si el punto de inscripción está en peligro, un atacante podría obtener certificados para la autenticación. También podría robar las credenciales de los usuarios que hayan inscrito sus dispositivos móviles.  

    El punto de inscripción se comunica con una entidad de certificación. Puede crear, modificar y eliminar objetos de Active Directory. Nunca instale el punto de inscripción en la red perimetral. Supervise siempre si hay alguna actividad inusual.  

- Si permite directivas de usuario para la administración de clientes basada en Internet, aumentará el perfil de ataque.  

    Además de utilizar certificados PKI para las conexiones de cliente a servidor, estas configuraciones requieren la autenticación de Windows. Puede tener que utilizar la autenticación NTLM en lugar de Kerberos. La autenticación NTLM es vulnerable a ataques de suplantación de identidad y reproducción. Para autenticar correctamente a un usuario en Internet, debe permitir una conexión del sistema de sitio basado en Internet a un controlador de dominio.  

- Se requiere el recurso compartido **Admin$** en servidores de sistema de sitio.  

    El servidor del sitio de Configuration Manager usa el recurso compartido Admin$ para conectarse y realizar operaciones de servicio en sistemas de sitio. No deshabilite ni quite este recurso compartido.  

- Configuration Manager usa servicios de resolución de nombres para conectarse a otros equipos. Estos servicios son difíciles de proteger contra los siguientes ataques de seguridad:
    - Suplantación de identidad
    - Alteración
    - Rechazo
    - Divulgación de información
    - Denegación de servicio
    - Elevación de privilegios

    Identifique y siga la guía de seguridad de la versión de DNS que utiliza para la resolución de nombres.  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> Información de privacidad para la detección

La detección crea registros de recursos de red y los almacena en la base de datos de Configuration Manager. Los registros de datos de detección contienen información del equipo como direcciones IP, versiones de sistemas operativos y nombres de equipo. También puede configurar los métodos de detección de Active Directory para devolver cualquier información que su organización almacena en Active Directory Domain Services.  

El único método de detección que Configuration Manager habilita de forma predeterminada es la detección de latido. Este método solo detecta equipos que ya tienen instalado el software cliente de Configuration Manager.  

La información de detección no se envía directamente a Microsoft. Se almacena en la base de datos de Configuration Manager. Configuration Manager conserva la información en la base de datos hasta que se elimina. Este proceso se realiza cada 90 días con la tarea de mantenimiento del sitio **Eliminar datos de detección antiguos**.  
