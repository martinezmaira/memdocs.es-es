---
title: Métodos de detección
titleSuffix: Configuration Manager
description: Obtenga información sobre los métodos de detección disponibles para buscar dispositivos en la red, desde Active Directory o Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 68e622d45de6575ec0f652f33934654cd1481dc2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705003"
---
# <a name="about-discovery-methods-for-configuration-manager"></a>Acerca de los métodos de detección en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los métodos de detección de Configuration Manager pueden encontrar otros dispositivos en la red, dispositivos y usuarios de Active Directory, o bien dispositivos y usuarios de Azure Active Directory (Azure AD). Para usar de manera eficiente un método de detección, necesita comprender las configuraciones disponibles y las limitaciones.  



##  <a name="active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a> Detección de bosques de Active Directory  
 **Configurable:** Sí  

 **Habilitado de manera predeterminada:** No  

 **Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de detección de bosques de Active Directory** (definida por el usuario)  

-   **Cuenta de equipo** del servidor de sitio  

A diferencia de otros métodos de detección de Active Directory, la detección de bosques de Active Directory no detecta recursos que se puedan administrar. En su lugar, este método detecta las ubicaciones de red que están configuradas en Active Directory. Pueden convertir esas ubicaciones en límites para su uso en toda la jerarquía.  

Al ejecutar este método, busca el bosque de Active Directory local, todos los bosques de confianza y todos los bosques adicionales que configure en el nodo **Bosques de Active Directory** de la consola de Configuration Manager.  

Use la detección de bosques de Active Directory para:  

-   Detectar sitios y subredes de Active Directory y, después, crear límites de Configuration Manager basados en esas ubicaciones de red.  

-   Identificar superredes asignadas a un sitio de Active Directory. Convertir cada superred en límites de intervalo de direcciones IP.  

-   Publicar en Active Directory Domain Services (AD DS) en un bosque cuando se habilita la publicación en ese bosque. La cuenta de bosque de Active Directory especificada debe tener permisos en ese bosque.  

Puede administrar la detección de bosques de Active Directory en la consola de Configuration Manager. Vaya al área de trabajo **Administración** y expanda **Configuración de jerarquía**.   

-   **Métodos de detección**: aquí puede habilitar la detección de bosques de Active Directory para que se ejecute en el sitio de primer nivel de la jerarquía. También puede especificar una programación simple para ejecutar la detección. Configúrelo para crear automáticamente los límites de las subredes IP y los sitios de Active Directory que detecte. No se puede ejecutar la detección de bosques de Active Directory en un sitio primario secundario ni en un sitio secundario.  

-   **Bosques de Active Directory**: configure los bosques adicionales que se van a detectar, especifique cada cuenta de bosque de Active Directory y configure la publicación en cada bosque. Supervise el proceso de detección. Agregue subredes IP y sitios de Active Directory como límites de Configuration Manager y miembros de grupos de límites.  

Para configurar la publicación de bosques de Active Directory para cada sitio de la jerarquía, conecte la consola de Configuration Manager al sitio de nivel superior de la jerarquía. En la pestaña **Publicación** del cuadro de diálogo **Propiedades** del sitio de Active Directory solo se puede mostrar el sitio actual y sus sitios secundarios. Cuando la publicación está habilitada para un bosque y el esquema de ese bosque se extiende para Configuration Manager, se publica la información siguiente de cada sitio habilitado para publicar en ese bosque de Active Directory:  

-    **SMS-Site-&lt;código de sitio>**

-   **SMS-MP-&lt;código de sitio>-&lt;nombre de servidor de sistema de sitio>**  

-   **SMS-SLP-&lt;código de sitio>-&lt;nombre de servidor de sistema de sitio>**  

-   **SMS-&lt;código de sitio>-&lt;subred o nombre de sitio de Active Directory>**  

> [!NOTE]  
>  Los sitios secundarios siempre utilizan la cuenta de equipo del servidor de sitio secundario para publicar en Active Directory. Si quiere que los sitios secundarios publiquen en Active Directory, asegúrese de que la cuenta de equipo de servidor de sitio secundario tenga permisos para publicar en Active Directory. Un sitio secundario no puede publicar datos en un bosque que no sea de confianza.  

> [!CAUTION]  
>  Al desactivar la opción para publicar un sitio en un bosque de Active Directory, toda la información publicada anteriormente para ese sitio (incluidos los roles de sistema de sitio disponibles) se eliminará de Active Directory.  

Las acciones de detección de bosques de Active Directory se registran en los registros siguientes:  

-   Todas las acciones (excepto las relacionadas con la publicación) se registran en el archivo **ADForestDisc.Log** de la carpeta **&lt;Ruta de instalación>\Logs** del servidor de sitio.  

-   Las acciones de publicación de detección de bosques de Active Directory se registran en los archivos **hman.log** y **sitecomp.log** de la carpeta **&lt;Ruta de instalación>\Logs** del servidor de sitio.  

Para obtener más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección](configure-discovery-methods.md#BKMK_ConfigADForestDisc).  



##  <a name="active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a> Detección de grupos de Active Directory  
**Configurable:** Sí  

**Habilitado de manera predeterminada:** No  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de detección de grupos de Active Directory** (definida por el usuario)  

-   **Cuenta de equipo** del servidor de sitio  

> [!TIP]  
>  Además de la información de esta sección, vea [Características comunes de la detección de grupos, sistemas y usuarios de Active Directory](#bkmk_shared).  

Use este método para buscar en Active Directory Domain Services e identificar:  

-   Grupos de seguridad locales, globales y universales.  

-   La pertenencia a grupos.  

-   Información limitada sobre equipos y usuarios de miembros de grupos, incluso si otro método de detección no ha detectado anteriormente esos equipos y usuarios.  

Este método de detección está pensado para identificar grupos y las relaciones de grupo de miembros de grupos. De forma predeterminada, solo se detectan grupos de seguridad. Si también quiere buscar la pertenencia a grupos de distribución, tiene que activar la casilla de la opción **Detectar la pertenencia de los grupos de distribución** en la pestaña **Opción** del cuadro de diálogo **Propiedades de detección de grupos de Active Directory**.  

La detección de grupos de Active Directory no es compatible con los atributos extendidos de Active Directory que se pueden identificar mediante la detección de sistemas de Active Directory o la detección de usuarios de Active Directory. Como este método de detección no está optimizado para detectar recursos de equipos y usuarios, tenga en cuenta la posibilidad de ejecutar este método de detección después de ejecutar la detección de sistemas de Active Directory y la detección de usuarios de Active Directory. Esta sugerencia se debe a que este método de detección crea un registro de datos de detección (DDR) completo para los grupos, pero solo un DDR limitado para los equipos y usuarios que son miembros de los grupos.  

Puede configurar los siguientes ámbitos de detección que controlan cómo busca información este método:  

-   **Ubicación**: utilice una ubicación si desea buscar en uno o varios contenedores de Active Directory. Esta opción de ámbito es compatible con una búsqueda recursiva de los contenedores de Active Directory especificados. Este proceso busca en todos los contenedores secundarios del contenedor que se especifique. Continúa hasta que no se encuentren más contenedores secundarios.  

-   **Grupos**: utilice grupos si desea buscar en uno o varios grupos específicos de Active Directory. Puede configurar el **Dominio de Active Directory** para que use el dominio y el bosque predeterminados, o bien puede limitar la búsqueda a un controlador de dominio específico. Además, puede especificar uno o más grupos en los que realizar la búsqueda. Si no especifica al menos un grupo, la búsqueda se realizará en todos los grupos que se encuentren en el **Dominio de Active Directory** especificado.  

> [!CAUTION]  
>  Al configurar un ámbito de detección, seleccione solo los grupos que necesita detectar. Esta recomendación se debe a que la detección de grupos de Active Directory intenta detectar todos los miembros de cada grupo del ámbito de detección. La detección de grupos grandes puede requerir un uso considerable de ancho de banda y de recursos de Active Directory.  

> [!NOTE]  
>  Para crear colecciones basadas en atributos extendidos de Active Directory (y para garantizar resultados de detección precisos para equipos y usuarios), ejecute la detección de sistemas o de usuarios de Active Directory, según lo que quiera detectar.  

Las acciones de detección de grupos de Active Directory se registran en el archivo **adsgdis.log** de la carpeta **&lt;Ruta de instalación\>\LOGS** del servidor de sitio.  

Para obtener más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a> Detección de sistemas de Active Directory  
**Configurable:** Sí  

**Habilitado de manera predeterminada:** No  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de detección de sistemas de Active Directory** (definida por el usuario)  

-   **Cuenta de equipo** del servidor de sitio  

> [!TIP]  
>  Además de la información de esta sección, vea [Características comunes de la detección de grupos, sistemas y usuarios de Active Directory](#bkmk_shared).  

Use este método de detección para buscar en las ubicaciones especificadas de Active Directory Domain Services los recursos informáticos que se pueden usar para crear colecciones y consultas. También puede instalar el cliente de Configuration Manager en un dispositivo detectado mediante la instalación de inserción de cliente.  

De forma predeterminada, este método detecta información básica sobre el equipo, incluidos los atributos siguientes:  

-   Nombre del equipo  

-   Sistema operativo y versión  

-   Nombre de contenedor de Active Directory  

-   Dirección IP  

-   Sitio de Active Directory  

-   Marca de tiempo del último inicio de sesión  

Para crear correctamente un DDR para un equipo, la detección de sistemas de Active Directory necesita identificar la cuenta de equipo y, después, resolver el nombre del equipo en una dirección IP.  

En el cuadro de diálogo **Propiedades de detección de sistemas de Active Directory**, en la pestaña **Atributos de Active Directory**, puede ver la lista completa de atributos de objeto predeterminados que detecta. También puede configurar el método para detectar atributos adicionales (extendidos).  

Las acciones de detección de sistemas de Active Directory se registran en el archivo **adsysdis.log** de la carpeta **&lt;Ruta de instalación\>\LOGS** del servidor de sitio.  

Para obtener más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a> Detección de usuario de Active Directory  
**Configurable:** Sí  

**Habilitado de manera predeterminada:** No  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de detección de usuarios de Active Directory** (definida por el usuario)  

-   **Cuenta de equipo** del servidor de sitio  

> [!TIP]  
>  Además de la información de esta sección, vea [Características comunes de la detección de grupos, sistemas y usuarios de Active Directory](#bkmk_shared).  

Use este método de detección para buscar en Active Directory Domain Services (AD DS) e identificar cuentas de usuario y atributos asociados. De forma predeterminada, este método detecta información básica sobre la cuenta de usuario, incluidos los atributos siguientes:  

-   Nombre de usuario  

-   Nombre de usuario único (incluye el nombre de dominio)  

-   Dominio  

-   Nombres de contenedor de Active Directory  

En el cuadro de diálogo **Propiedades de detección de usuarios de Active Directory**, en la pestaña **Atributos de Active Directory**, puede ver la lista completa predeterminada de los atributos de objeto que detecta. También puede configurar el método para detectar atributos adicionales (extendidos).

Las acciones de detección de usuarios de Active Directory se registran en el archivo **adusrdis.log** de la carpeta **&lt;Ruta de instalación\>\LOGS** del servidor de sitio.  

Para obtener más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



## <a name="azure-active-directory-user-discovery"></a><a name="azureaddisc"></a> Detección de usuarios de Azure Active Directory

Use la detección de usuarios de Azure Active Directory (Azure AD) para buscar la suscripción de Azure AD para los usuarios con una identidad de nube moderna. La detección de usuarios de Azure AD puede encontrar los atributos siguientes:

- objectId
- DisplayName
- mail
- mailNickname
- onPremisesSecurityIdentifier
- userPrincipalName
- tenantID de AAD
- onPremisesDomainName
- onPremisesSamAccountName
- onPremisesDistinguishedName

Este método es compatible con la sincronización completa y de diferencias de atributos de usuario de Azure AD. Esta información puede utilizarse con los datos de detección que recopile de los otros métodos de detección.

Las acciones para la detección de usuarios de Azure AD se registran en el archivo **SMS_AZUREAD_DISCOVERY_AGENT.log** del servidor de sitio de nivel superior de la jerarquía.

Para configurar la detección de usuarios de Azure AD, vea [Configuración de servicios de Azure](azure-services-wizard.md) para la administración en la nube. Para obtener más información sobre cómo configurar este método de detección, consulte la sección [Configuración de la detección de usuarios de Azure AD](configure-discovery-methods.md#azureaadisc).

## <a name="azure-active-directory-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a> Detección de grupos de usuarios de Azure Active Directory
<!--3611956-->
*(Presentada como una [característica de versión preliminar](../../manage/pre-release-features.md) en la versión 1906)*

Puede descubrir grupos de usuarios y miembros de esos grupos desde Azure Active Directory (Azure AD). La detección de grupos de usuarios de Azure AD puede encontrar los atributos siguientes:

- objectId
- DisplayName
- mailNickname
- onPremisesSecurityIdentifier
- tenantID de AAD

Las acciones para la detección de grupos de usuarios de Azure AD se registran en el archivo **SMS_AZUREAD_DISCOVERY_AGENT.log** del servidor del sitio de nivel superior de la jerarquía. Para más información sobre cómo configurar este método de detección, vea [Configuración de la detección de grupos de usuarios de Azure AD](configure-discovery-methods.md#bkmk_azuregroupdisco).

##  <a name="heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a> Detección de latidos  
**Configurable:** Sí  

**Habilitado de manera predeterminada:** Sí  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de equipo** del servidor de sitio  

La detección de latidos difiere de otros métodos de detección de Configuration Manager. Está habilitada de forma predeterminada y se ejecuta en cada equipo cliente (en lugar de ejecutarse en un servidor de sitio) para crear un DDR. En el caso de los clientes de dispositivos móviles, el DDR lo creará el punto de administración usado por el cliente del dispositivo móvil. Para mantener el registro de base de datos de los clientes de Configuration Manager, no deshabilite la detección de latidos. Además de mantener el registro de base de datos, este método puede forzar la detección de un equipo como un registro de recursos nuevo. También puede volver a llenar el registro de base de datos de un equipo que se eliminó de la base de datos.  

La detección de latidos se ejecuta según una programación configurada para todos los clientes en la jerarquía. La programación predeterminada para la detección de latidos se establece en cada siete días. Si modifica el intervalo de detección de latidos, asegúrese de que se ejecuta con mayor frecuencia que la tarea de mantenimiento del sitio **Eliminar datos de detección antiguos**. Esta tarea elimina los registros de cliente inactivos en la base de datos del sitio. Puede configurar la tarea **Eliminar datos de detección antiguos** solo para sitios primarios. 

También se puede invocar manualmente la detección de latidos en un cliente específico. Ejecute el **Ciclo de recopilación de datos de descubrimiento** en la pestaña **Acción** del panel de control de Configuration Manager de un cliente.  

Al ejecutar la detección de latidos, esta crea un DDR que contiene la información actual del cliente. Después, el cliente copia este pequeño archivo (de aproximadamente 1 KB de tamaño) en un punto de administración para que un sitio primario pueda procesarlo. El archivo contiene la información siguiente:  

-   Ubicación de red  

-   Nombre NetBIOS  

-   Versión del agente cliente  

-   Detalles del estado operativo  

La detección de latidos es el único método de detección que proporciona detalles sobre el estado de instalación del cliente. Para ello, actualiza el atributo de cliente de un recurso del sistema para establecer un valor igual a **Sí**.  

> [!NOTE]  
>  Incluso cuando se deshabilita la detección de latidos, todavía se crean y se envían DDR a clientes de dispositivos móviles activos. Este comportamiento garantiza que la tarea **Eliminar datos de detección antiguos** no afecta a los dispositivos móviles activos. Cuando la tarea **Eliminar datos de detección antiguos** elimina un registro de base de datos para un dispositivo móvil, también revoca el certificado del dispositivo. Esta acción impide a este dispositivo conectarse con los puntos de administración.  

Las acciones de detección de latidos se registran en las siguientes ubicaciones:  

-   En los clientes de equipos, las acciones de detección de latidos se registran en el cliente en el archivo **InventoryAgent.log** de la carpeta *%Windir%\CCM\Logs*.  

-   En los clientes de dispositivos móviles, las acciones de detección de latidos se registran en el archivo **DMPRP.log** de la carpeta *%Program Files%\CCM\Logs* del punto de administración que use el cliente del dispositivo móvil.  

Para obtener más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección](configure-discovery-methods.md#BKMK_ConfigHBDisc).  



##  <a name="network-discovery"></a><a name="bkmk_aboutNetwork"></a> Detección de redes  
**Configurable:** Sí  

**Habilitado de manera predeterminada:** No  

**Cuentas** que se pueden usar para ejecutar este método:  

-   **Cuenta de equipo** del servidor de sitio  

Use este método para detectar la topología de la red y para detectar dispositivos de la red que tengan una dirección IP. Detección de redes busca en la red recursos habilitados para IP consultando las entidades siguientes: 
- Servidores que ejecutan una implementación de Microsoft de DHCP.
- Memorias caché de protocolo de resolución de direcciones (ARP) en enrutadores de red.
- Dispositivos habilitados para SNMP
- Dominios de Active Directory.  

Para usar la detección de redes, debe especificar el *nivel* de detección que se va a ejecutar. También puede configurar uno o más mecanismos de detección que permiten a Detección de redes consultar segmentos o dispositivos de red. Puede configurar asimismo las opciones que ayudan a controlar las acciones de detección en la red. Por último, puede definir una o más programaciones para la ejecución de Detección de redes.  

Para que este método detecte correctamente un recurso, la detección de redes necesita identificar la dirección IP y la máscara de subred del recurso. Se usan los siguientes métodos para identificar la máscara de subred de un objeto:  

-   **Caché ARP del enrutador:** La detección de redes consulta la caché ARP de un enrutador para buscar información de subred. Normalmente, los datos de una caché ARP del enrutador tienen un corto período de vida. Por lo tanto, cuando la detección de redes consulta la caché ARP, puede que esta ya no contenga información sobre el objeto solicitado.  

-   **DHCP:** La detección de redes consulta cada servidor DHCP especificado para detectar los dispositivos para los que el servidor DHCP ha proporcionado una concesión. La detección de redes sólo admite servidores DHCP en que se ejecuta la implementación de DHCP de Microsoft.  

-   **Dispositivo SNMP:** la detección de redes puede consultar directamente un dispositivo SNMP. Para que la detección de redes consulte un dispositivo, este último debe tener instalado un agente SNMP local. Configure también la detección de redes para usar el nombre de la comunidad que usa el agente SNMP.  

Cuando la detección identifica un objeto accesible por IP y puede determinar la máscara de subred del objeto, crea un DDR para ese objeto. Como otros tipos de dispositivos se conectan a la red, la detección de redes detecta recursos que no son compatibles con el cliente de Configuration Manager. Por ejemplo, entre los dispositivos que se pueden detectar, pero no administrar, se incluyen impresoras y enrutadores.  

La detección de redes puede devolver varios atributos como parte del registro de detección que se crea. Estos atributos incluyen lo siguiente:  

-   Nombre NetBIOS  

-   Direcciones IP  

-   Dominio de recursos  

-   Roles del sistema  

-   Nombre de comunidad SNMP  

-   Direcciones MAC  

La actividad de la detección de redes se registra en el archivo **Netdisc.log** de *&lt;Ruta de instalación\>\Logs* del servidor de sitio que ejecuta la detección.  

 Para obtener más información sobre cómo configurar este método de detección, vea [Configurar métodos de detección](configure-discovery-methods.md#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Las redes complejas y las conexiones de ancho de banda reducido pueden provocar que la detección de redes se ejecute con lentitud y genere un volumen importante de tráfico de red. Como práctica recomendada, ejecute Detección de redes solo cuando los otros métodos de detección no puedan encontrar los recursos que debe detectar. Por ejemplo, puede utilizar Detección de redes si debe detectar equipos de grupos de trabajo. Otros métodos de detección no detectan equipos de grupo de trabajo.  

###  <a name="levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a> Niveles de detección de redes  
Al configurar Detección de redes, se puede especificar uno de los tres niveles de detección:  

|Nivel de detección|Detalles|  
|------------------------|-------------|  
|Topología|Este nivel detecta los enrutadores y subredes, pero no identifica una máscara de subred para los objetos.|  
|Topología y cliente|Además de la topología, este nivel detecta posibles clientes (como equipos) y recursos (como impresoras y enrutadores). Este nivel de detección intenta identificar la máscara de subred de los objetos que encuentra.|  
|Topología, cliente y sistema operativo de cliente|Además de la topología y los posibles clientes, este nivel intenta detectar el nombre y la versión del sistema operativo del equipo. Este nivel utiliza el Explorador de Windows y las llamadas a redes de Windows.|  

 Con cada nivel de incremento, Detección de redes aumenta su actividad y el uso de ancho de banda de red. Tenga en cuenta el tráfico de red que puede generarse antes de habilitar todos los aspectos de Detección de redes.  

 Por ejemplo, cuando se utiliza Detección de redes por primera vez, puede comenzar únicamente por el nivel de topología para identificar la infraestructura de red. Después, vuelva a configurar Detección de redes para que se detecten objetos y sus sistemas operativos de dispositivos. También puede configurar otras opciones que limitan la detección de redes a un intervalo específico de segmentos de red. De este modo, se detectan objetos en las ubicaciones de red que se necesitan y se evita tráfico de red innecesario. Este proceso también permite detectar objetos desde enrutadores perimetrales o desde fuera de la red.  

###  <a name="network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a> Opciones de detección de redes  
Para que Detección de redes pueda buscar dispositivos IP direccionables, configure una o varias de estas opciones.  

> [!NOTE]  
>  Detección de redes se ejecuta en el contexto de la cuenta de equipo del servidor de sitio que ejecuta la detección. Si la cuenta de equipo no tiene permisos para un dominio que no es de confianza, es posible que las configuraciones de dominio y de servidor DHCP no puedan detectar recursos.  

#### <a name="dhcp"></a>DHCP  

Especifique cada servidor DHCP que desea que consulte Detección de redes. (La detección de redes solo admite servidores DHCP que ejecutan la implementación de DHCP de Microsoft).  

-   Detección de redes recupera información mediante llamadas a procedimiento remoto en la base de datos del servidor DHCP.  

-   Detección de redes puede consultar servidores DHCP de 32 y 64 bits para obtener una lista de los dispositivos que están registrados en cada servidor.  

-   Para que Detección de redes consulte correctamente un servidor DHCP, la cuenta de equipo del servidor que ejecuta la detección debe ser miembro del grupo Usuarios de DHCP del servidor DHCP. Por ejemplo, este nivel de acceso existe cuando se cumple una de las instrucciones siguientes:  

    -   El servidor DHCP especificado es el servidor DHCP del servidor que ejecuta la detección.  

    -   El equipo que ejecuta la detección y el servidor DHCP están en el mismo dominio.  

    -   Existe una confianza bidireccional entre el equipo que ejecuta la detección y el servidor DHCP.  

    -   El servidor de sitio es miembro del grupo de usuarios de DHCP.  

-   Cuando Detección de redes enumera un servidor DHCP, no siempre detecta direcciones IP estáticas. La detección de redes no encuentra direcciones IP que pertenezcan a un intervalo excluido de direcciones IP en el servidor DHCP. Tampoco detecta direcciones IP que estén reservadas para la asignación manual.  

#### <a name="domains"></a>Dominios  

Especifique cada dominio que desea que consulte Detección de redes.  

-   La cuenta de equipo del servidor de sitio que ejecute la detección debe tener permisos para leer los controladores de dominio en cada dominio especificado.  

-   Para detectar equipos del dominio local, es necesario habilitar el servicio Explorador de equipos como mínimo en un equipo. Este equipo se debe encontrar en la misma subred que el servidor de sitio que ejecuta Detección de redes.  

-   Detección de redes puede detectar cualquier equipo que se pueda ver desde el servidor de sitio al examinar la red.  

-   Detección de redes recupera la dirección IP. Después usa una solicitud de eco del Protocolo de mensajes de control de Internet (ICMP) para hacer ping en cada dispositivo que encuentra. El comando **ping** ayuda a determinar qué equipos están activos actualmente.  

#### <a name="snmp-devices"></a>Dispositivos SNMP  

Especifique cada dispositivo SNMP que desea que consulte Detección de redes.  

-   La detección de redes recupera el valor ipNetToMediaTable desde cualquier dispositivo SNMP que responda a la consulta. Este valor devuelve matrices de direcciones IP que son equipos cliente u otros recursos (como impresoras, enrutadores u otros dispositivos accesibles por IP).  

-   Para consultar un dispositivo necesita especificar la dirección IP o el nombre NetBIOS del mismo.  

-   Configure Detección de redes para que use el nombre de comunidad del dispositivo o el dispositivo rechazará la consulta basada en SNMP.  


###  <a name="limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a> Limitación de la detección de redes  
Cuando Detección de redes consulta un dispositivo SNMP en el perímetro de la red, puede identificar información sobre las subredes y los dispositivos SNMP que se encuentran fuera de la red inmediata. Use la siguiente información para limitar la detección de redes mediante la configuración de los dispositivos SNMP con los que se puede comunicar la detección y mediante la especificación de los segmentos de red que se van a consultar.  

#### <a name="subnets"></a>Subredes  

Configure las subredes en que la detección de redes realiza consultas cuando utiliza las opciones DHCP y SNMP. Estas dos opciones solo buscan en las subredes habilitadas.  

Por ejemplo, una solicitud DHCP puede devolver los dispositivos desde ubicaciones de toda la red. Si solo quiere detectar dispositivos de una subred concreta, especifique y habilite esa subred en la pestaña **Subredes** del cuadro de diálogo **Propiedades de Detección de redes**. Al especificar y habilitar las subredes, se limitan las futuras tareas de detección DHCP y SNMP en esas subredes.  

> [!NOTE]  
>  La configuración de las subredes no limita los objetos detectados con la opción de detección de **Dominios**.  

#### <a name="snmp-community-names"></a>Nombres de comunidad SNMP  

Para habilitar Detección de redes para consultar correctamente un dispositivo SNMP, configure Detección de redes con el nombre de comunidad del dispositivo. Si la detección de redes no está configurada con el nombre de comunidad del dispositivo SNMP, este último rechaza la consulta.  

#### <a name="maximum-hops"></a>Número máximo de saltos  

Cuando se configura el número máximo de saltos de enrutador, se limita el número de segmentos de red y enrutadores que puede consultar la detección de redes con SNMP.  

El número de saltos configurado limita el número de segmentos de red y dispositivos adicionales que puede consultar la detección de red.  

Por ejemplo, una detección de solo topología con **0** (cero) saltos de enrutador detecta la subred donde reside el servidor de origen e incluye todos los enrutadores de esa subred.  

En el diagrama siguiente se muestra lo que encuentra una consulta de detección de redes de solo topología cuando se ejecuta en el servidor 1 con 0 saltos de enrutador especificados: subred D y enrutador 1.  

 ![Imagen de detección con cero saltos de enrutador](media/Disc-0.gif)  

 En el diagrama siguiente se muestra lo que encuentra una consulta de detección de redes de clientes y topologías cuando se ejecuta en el servidor 1 con 0 saltos de enrutador especificados: subred D y enrutador 1, así como todos los posibles clientes en la subred D.  

 ![Imagen de detección con un salto de enrutador](media/Disc-1.gif)  

 Para hacerse una idea más clara de cómo los saltos de enrutador adicionales pueden aumentar la cantidad de recursos de red detectados, tenga en cuenta la siguiente red:  

 ![Imagen de detección con dos saltos de enrutador](media/Disc-2.gif)  

 Al ejecutar una detección de redes de solo topología desde el servidor 1 con un salto de enrutador, se detectan las entidades siguientes:  

-   Enrutador 1 y subred 10.1.10.0 (encontrados con cero saltos).  

-   Subredes 10.1.20.0 y 10.1.30.0, subred A y enrutador 2 (encontrados en el primer salto).  

> [!WARNING]  
>  Cada incremento del número de saltos de enrutador puede aumentar significativamente el número de recursos detectables y el ancho de banda de red que consume la detección de redes.  



##  <a name="server-discovery"></a><a name="bkmk_aboutServer"></a> Detección de servidores  
**Configurable:** No  

Además de los métodos de detección configurables por el usuario, Configuration Manager también usa un proceso denominado **Detección de servidores** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Este método de detección crea registros de recursos para los equipos que son sistemas de sitio (por ejemplo, un equipo que esté configurado como un punto de administración).  



##  <a name="common-features-of-active-directory-group-discovery-system-discovery-and-user-discovery"></a><a name="bkmk_shared"></a> Características comunes de la detección de grupos, detección de sistemas y detección de usuarios de Active Directory  
En esta sección se proporciona información sobre las características que son comunes a los siguientes métodos de detección:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

> [!NOTE]  
>  La información de esta sección no se aplica a la detección de bosques de Active Directory.  

Estos tres métodos de detección funcionan y se configuran de manera similar. Pueden detectar equipos, usuarios e información sobre pertenencia a grupos de los recursos almacenados en Active Directory Domain Services. Un agente de detección administra el proceso de detección. El agente se ejecuta en el servidor de sitio en cada sitio donde se configura la ejecución de la detección. Puede configurar cada uno de estos métodos de detección para buscar una o más ubicaciones de Active Directory como instancias de ubicación en el bosque local o los bosques remotos.  

Cuando la detección busca recursos en un bosque que no es de confianza, el agente de detección debe ser capaz de resolver lo siguiente para tener éxito:  

-   Para detectar un recurso de equipo con la detección de sistemas de Active Directory es necesario que el agente de detección pueda resolver el FQDN del recurso. Si no puede resolver el FQDN, intenta resolver el recurso por su nombre NetBIOS.  

-   Para detectar un recurso de usuario o grupo con la detección de usuarios de Active Directory o la detección de grupos de Active Directory, es necesario que el agente de detección pueda resolver el FQDN del nombre de controlador de dominio que especifique para la ubicación de Active Directory.  

Por cada ubicación que especifique, puede configurar opciones de búsqueda individuales (por ejemplo, habilitar una búsqueda recursiva de los contenedores secundarios de Active Directory de la ubicación). También puede configurar una cuenta única para usarla cuando realice una búsqueda en esa ubicación. Esta cuenta proporciona flexibilidad a la hora de configurar un método de detección en un sitio para buscar varias ubicaciones de Active Directory en varios bosques. No es necesario configurar una cuenta única que tenga permisos para todas las ubicaciones.  

Cuando estos tres métodos de detección se ejecutan en un sitio específico, el servidor de sitio de Configuration Manager del sitio establece contacto con el controlador de dominio más próximo del bosque de Active Directory especificado para buscar los recursos de Active Directory. El dominio y el bosque pueden estar en cualquier modo de Active Directory admitido. La cuenta que asigne a cada instancia de ubicación necesita tener permisos de acceso de **lectura** a las ubicaciones de Active Directory especificadas.

La detección busca objetos en las ubicaciones especificadas y, después, intenta recopilar información sobre los objetos. Cuando se puede identificar suficiente información acerca de un recurso, se crea un DDR. La información necesaria varía en función del método de detección que se utilice.  

Si configura el mismo método de detección para que se ejecute en diferentes sitios de Configuration Manager a fin de sacar partido de la consulta de servidores locales de Active Directory, puede configurar cada sitio con un único conjunto de opciones de detección. Dado que los datos de detección se comparten con cada sitio de la jerarquía, evite la superposición entre estas configuraciones para detectar de forma eficaz una sola vez cada recurso.

En entornos más pequeños, considere la posibilidad de ejecutar cada método de detección en un solo sitio de la jerarquía. Esta configuración reduce la sobrecarga administrativa y la posibilidad de que varias acciones de detección vuelvan a detectar los mismos recursos. Al reducir el número de sitios que ejecutan la detección, se reduce el ancho de banda de red general que usa la detección. También puede reducir el número general de DDR creados y que tienen que procesar los servidores de sitios.  

Muchas de las configuraciones del método de detección se explican por sí mismas. Utilice las siguientes secciones para obtener más información acerca de las opciones de detección que pueden requerir información adicional antes de configurarlas.  

Las siguientes opciones están disponibles con varios métodos de detección de Active Directory:  

-   [Detección de diferencias](#bkmk_delta)  

-   [Filtrar registros informáticos obsoletos por inicio de sesión de dominio](#bkmk_stalelogon)  

-   [Filtrar registros obsoletos por contraseña de equipo](#bkmk_stalepassword)  

-   [Buscar atributos personalizados de Active Directory](#bkmk_customAD)  


###  <a name="delta-discovery"></a><a name="bkmk_delta"></a> Detección de diferencias  
Disponible para:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

La detección de diferencias no es un método de detección independiente, sino una opción disponible para los métodos de detección aplicables. La detección de diferencias busca cambios en atributos específicos de Active Directory realizados desde el último ciclo de detección completo del método de detección correspondiente. Los cambios de atributos se envían a la base de datos de Configuration Manager para actualizar el registro de detección del recurso.  

De forma predeterminada, la detección de diferencias se ejecuta en un ciclo de cinco minutos. Esta programación es mucho más frecuente que la programación típica de un ciclo de detección completo. Esta frecuencia es posible porque la detección de diferencias usa menos recursos de servidor de sitio y red que un ciclo de detección completo. Cuando use la detección de diferencias, puede reducir la frecuencia del ciclo de detección completo de ese método de detección.  

Los cambios siguientes son los cambios más comunes que encuentra la detección de diferencias:  

-   Nuevos equipos o usuarios agregados a Active Directory  

-   Cambios en la información básica de equipos y usuarios  

-   Nuevos equipos o usuarios que se agregan a un grupo  

-   Equipos o usuarios que se quitan de un grupo  

-   Cambios en los objetos de grupo del sistema  

Aunque la detección de diferencias puede detectar nuevos recursos y cambios en la pertenencia a grupos, no puede detectar si se ha eliminado un recurso de Active Directory. Los DDR creados por la detección de diferencias se procesan de forma similar a los DDR que se crean mediante un ciclo de detección completo.  

La detección de diferencias se configura en la pestaña **Programación de sondeo** de las propiedades para cada método de detección.  


###  <a name="filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a> Filtrar registros informáticos obsoletos por inicio de sesión de dominio  
Disponible para:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

Se puede configurar la detección para que excluya a los equipos con un registro informático obsoleto. Esta exclusión se basa en el último inicio de sesión de dominio del equipo. Cuando esta opción está habilitada, la detección de sistemas de Active Directory evalúa cada equipo que identifica. La detección de grupos de Active Directory evalúa cada equipo que es miembro de un grupo que se detecta.  

Para usar esta opción:  

-   Los equipos deben estar configurados para actualizar el atributo **lastLogonTimeStamp** en Active Directory Domain Services.  

-   El nivel funcional de dominio de Active Directory debe estar establecido en Windows Server 2003 o posterior.  

Al configurar el tiempo después del último inicio de sesión que quiera usar para esta configuración, tenga en cuenta el intervalo para la replicación entre controladores de dominio.  

Configure el filtrado en la pestaña **Opción** de los cuadros de diálogo **Propiedades de detección de sistemas de Active Directory** y **Propiedades de detección de grupos de Active Directory**. Seleccione **Detectar solo los equipos que iniciaron sesión en un dominio en un determinado período de tiempo**.  

> [!WARNING]  
>  Al configurar este filtro y la opción **Filtrar registros obsoletos por contraseña de equipo**, se excluyen de la detección los equipos que cumplan los criterios de uno de los filtros.  


###  <a name="filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a> Filtrar registros obsoletos por contraseña de equipo  
Disponible para:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

Se puede configurar la detección para que excluya a los equipos con un registro informático obsoleto. Esta exclusión se basa en la última actualización de contraseña de cuenta de equipo por el equipo. Cuando esta opción está habilitada, la detección de sistemas de Active Directory evalúa cada equipo que identifica. La detección de grupos de Active Directory evalúa cada equipo que es miembro de un grupo que se detecta.  

Para usar esta opción:  

-   Los equipos deben estar configurados para actualizar el atributo **pwdLastSet** en Active Directory Domain Services.  

Cuando configure esta opción, tenga en cuenta el intervalo para las actualizaciones de este atributo. También tenga en cuenta el intervalo de replicación entre los controladores de dominio.  

Configure el filtrado en la pestaña **Opción** de los cuadros de diálogo **Propiedades de detección de sistemas de Active Directory** y **Propiedades de detección de grupos de Active Directory**. Seleccione **Detectar solo los equipos que actualizaron su contraseña de cuenta de equipo en un determinado período de tiempo**.  

> [!WARNING]  
>  Al configurar este filtro y la opción **Filtrar registros obsoletos por inicio de sesión de dominio**, se excluyen de la detección los equipos que cumplan los criterios de uno de los filtros.  


###  <a name="search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a> Buscar atributos personalizados de Active Directory  
 Disponible para:  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

Cada método de detección es compatible con una lista única de atributos de Active Directory que se pueden detectar.  

Puede ver y configurar la lista de atributos personalizados en la pestaña **Atributos de Active Directory** de los cuadros de diálogo **Propiedades de detección de sistemas de Active Directory** y **Propiedades de detección de usuarios de Active Directory**.  
