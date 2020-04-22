---
title: Plan para el proveedor de SMS
titleSuffix: Configuration Manager
description: Obtenga información sobre el rol de sistema de sitio del proveedor de SMS en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01ea9b089da3cfcfc3e8d23e7ad25d27ab2fec7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692763"
---
# <a name="plan-for-the-sms-provider"></a>Plan para el proveedor de SMS

*Se aplica a: Configuration Manager (rama actual)*

Para administrar Configuration Manager, use una consola de Configuration Manager que se conecte a una instancia del **proveedor de SMS**. De forma predeterminada, se instala un proveedor de SMS en el servidor de sitio al instalar un sitio de administración central o sitio primario.

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> Acerca del proveedor de SMS  

El proveedor de SMS es un proveedor de Instrumental de administración de Windows (WMI) que asigna acceso de **lectura** y **escritura** a la base de datos de Configuration Manager en un sitio.  

- Cada sitio de administración central y cada sitio principal requiere al menos un proveedor de SMS. Puede instalar a proveedores adicionales según sea necesario.  

- El grupo de seguridad **Administradores de SMS** permite acceder al proveedor de SMS. Configuration Manager crea automáticamente este grupo en el servidor de sitio y en todos los equipos donde instale una instancia del proveedor de SMS. Para obtener más información, vea [Administradores de SMS](accounts.md#sms-admins).  

- Los sitios secundarios no admiten el rol de proveedor de SMS.  

Los usuarios administrativos de Configuration Manager usan un proveedor de SMS para acceder a la información almacenada en la base de datos. Para hacerlo, los administradores pueden usar la consola de Configuration Manager, el Explorador de recursos, herramientas y scripts personalizados. El proveedor de SMS no interactúa con clientes de Configuration Manager. Cuando una consola de Configuration Manager se conecta a un sitio, consulta a WMI en el servidor de sitio para localizar una instancia del proveedor de SMS que se va a usar.  

El proveedor de SMS ayuda a reforzar la seguridad de Configuration Manager. Devuelve solo la información que el usuario de la consola está autorizado a ver.  

El proveedor de SMS también proporciona acceso de interoperabilidad a la API a través de HTTPS, que se denomina **servicio de administración**. Esta API REST puede usarse en lugar de un servicio web personalizado para acceder a información desde el sitio. Para más información, vea [¿Qué es el servicio de administración?](../../../develop/adminservice/overview.md)

> [!IMPORTANT]  
> Cuando todas las instancias del proveedor de SMS que contienen un proveedor de SMS para un sitio están sin conexión, las consolas de Configuration Manager no se pueden conectar al sitio.  

Para obtener más información sobre cómo administrar el proveedor de SMS, vea [Administración del proveedor de SMS](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).  

## <a name="installation-prerequisites"></a>Requisitos previos de instalación  

Para ser compatible con el proveedor de SMS, el servidor de destino debe cumplir los siguientes requisitos previos:  

- En el mismo dominio que el servidor de sitio y los sistemas de sitio de la base de datos de sitio  

- No puede tener un rol de sistema de sitio de un sitio diferente.  

- No puede tener un proveedor de SMS de cualquier sitio.  

- Debe ejecutar una versión de sistema operativo admitido.  

- Debe tener al menos 650 MB de espacio libre en disco para admitir los componentes de Windows ADK. Para más información sobre Windows ADK y el proveedor de SMS, vea [Requisitos de implementación de sistema operativo](#BKMK_WAIKforSMSProv).  

- Para la API de REST del [servicio de administración](../../../develop/adminservice/overview.md):

  - .NET 4.5 o posterior

  - Habilitar rol de servidor de Windows **servidor web (IIS)**

    > [!Note]  
    > Cada proveedor de SMS intenta instalar el servicio de administración, lo que requiere un certificado. Este servicio tiene una dependencia en IIS para enlazar ese certificado al puerto HTTPS 443. Si habilita [HTTP mejorado](enhanced-http.md), el sitio enlaza ese certificado mediante las API de IIS. Si en el sitio se usa PKI, tendrá que enlazar manualmente un certificado PKI en IIS en el proveedor de SMS. A partir de la versión 2002, el sitio usa automáticamente el certificado autofirmado del sitio.

## <a name="locations"></a><a name="bkmk_location"></a> Ubicaciones  

Al instalar un sitio, instalará automáticamente el primer proveedor de SMS para el sitio. Puede especificar cualquiera de las siguientes ubicaciones compatibles para el proveedor de SMS:  

- El servidor de sitio  

- El servidor de base de datos del sitio  

- Otro servidor, que cumpla los [requisitos previos de instalación](#installation-prerequisites)  

Para ver las ubicaciones de cada proveedor de SMS para un sitio:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y después haga clic en el nodo **Sitios**.  

2. Seleccione el sitio deseado en la lista y después haga clic en **Propiedades** en la cinta de opciones.  

3. En la pestaña **General** de las **Propiedades** del sitio, vea el campo **Ubicación del proveedor de SMS**.  

Cada proveedor de SMS admite conexiones simultáneas de varias solicitudes. Las únicas limitaciones de estas conexiones son el número de conexiones de servidor disponibles en Windows y los recursos disponibles en el servidor para atender las solicitudes de conexión.  

Después de instalar un sitio, puede ejecutar de nuevo el programa de instalación de Configuration Manager en el servidor de sitio. Use el programa de instalación para cambiar la ubicación de un proveedor de SMS existente, o para instalar proveedores de SMS adicionales en ese sitio. Instale solo un proveedor de SMS en un equipo. Un equipo no puede hospedar un proveedor de SMS de más de un sitio.  

### <a name="choosing-a-location"></a>Elegir una ubicación

En las siguientes secciones se describen las ventajas y desventajas de instalar un proveedor de SMS en cada ubicación admitida:  

#### <a name="configuration-manager-site-server"></a>Servidor de sitio de Configuration Manager

- **Ventajas:**  

  - El proveedor de SMS no utiliza los recursos de sistema del equipo de base de datos de sitio.  

  - Esta ubicación puede proporcionar un mejor rendimiento que un proveedor de SMS que se encuentre en un equipo que no sea el servidor de sitio o el equipo de base de datos de sitio.  

- **Desventajas:**  

  - El proveedor de SMS utiliza los recursos de red y de sistema que podrían estar dedicados a las operaciones de servidor de sitio.  

#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server que hospeda la base de datos del sitio

- **Ventajas:**  

  - El proveedor de SMS no usa recursos de sistema en el servidor de sitio.  

  - Esta ubicación puede proporcionar el mejor rendimiento de las tres ubicaciones, si hay disponibles suficientes recursos de servidor.  

- **Desventajas:**  

  - El proveedor de SMS utiliza los recursos de red y de sistema que podrían estar dedicados a las operaciones de base de datos de sitio.  

  - Cuando la base de datos del sitio está hospedada en una instancia en clúster de SQL Server, no se puede usar esa ubicación.  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Equipo distinto al servidor de sitio o servidor de base de datos del sitio

- **Ventajas:**  

  - El proveedor de SMS no utiliza recursos de servidor de sitio o de sistema de base de datos de sitio.  

  - Este tipo de ubicación le permite implementar proveedores de SMS adicionales para proporcionar alta disponibilidad para las conexiones.  

- **Desventajas:**  

  - El rendimiento del proveedor de SMS puede reducirse. Este comportamiento se debe a la actividad de red adicional necesaria para coordinar con el servidor de sitio y el equipo de base de datos del sitio.  

  - Este servidor necesita ser siempre accesible para el servidor de base de datos del sitio y todos los equipos que tengan instalada la consola de Configuration Manager.  

  - Esta ubicación puede utilizar recursos del sistema que de lo contrario se dedicarían a otros servicios.  

## <a name="authentication"></a><a name="bkmk_auth"></a> Autenticación

<!--1357013-->
A partir de la versión 1810, puede especificar el nivel mínimo de autenticación para que los administradores accedan a sitios de Configuration Manager. Esta característica exige que los administradores inicien sesión en Windows con el nivel requerido. Se aplica a todos los componentes que acceden al proveedor de SMS. Por ejemplo, la consola de Configuration Manager, los métodos del SDK y los cmdlets de Windows PowerShell.

### <a name="configure-authentication"></a>Configurar la autenticación

Para configurar esta opción, primero inicie sesión en Windows con el nivel de autenticación deseado.

> [!Important]  
> Esta opción es una configuración de toda la jerarquía. Antes de cambiar esta configuración, asegúrese de que todos los administradores de Configuration Manager pueden iniciar sesión en Windows con el nivel de autenticación requerido.

Para configurar esta opción, siga los pasos que se indican a continuación:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Haga clic en **Configuración de jerarquía** en la cinta de opciones.  

3. Cambie a la pestaña **Autenticación**. Seleccione el [nivel de autenticación](#authentication-levels) deseado y después haga clic en **Aceptar**.  

    - Solo cuando sea necesario, haga clic en **Agregar** para excluir a usuarios o grupos específicos. Para obtener más información, vea [Exclusiones](#exclusions).  

### <a name="authentication-levels"></a>Niveles de autenticación

Están disponibles los siguientes niveles:

- **Autenticación de Windows**: requiere la autenticación con credenciales de dominio de Active Directory. Esta configuración es el comportamiento anterior y el valor predeterminado actual. Cuando se actualiza el sitio, no hay ningún cambio en el nivel de autenticación.  

- **Autenticación de certificado**: requiere la autenticación con un certificado válido emitido por una entidad de certificación PKI de confianza. No configure este certificado en Configuration Manager. Configuration Manager requiere que el administrador inicie sesión en Windows mediante PKI.  

- **Autenticación de Windows Hello para empresas**: requiere la autenticación sólida en dos fases vinculada a un dispositivo y usa biometrías o un PIN. Para obtener más información, vea [Windows Hello para empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="exclusions"></a>Exclusiones

En la pestaña **Autenticación** de Configuración de jerarquía, también puede excluir determinados usuarios o grupos. Utilice esta opción con moderación. Por ejemplo, cuando usuarios específicos requieren acceso a la consola de Configuration Manager, pero no pueden autenticarse en Windows con el nivel requerido. También puede ser necesario para la automatización o los servicios que se ejecutan en el contexto de una cuenta del sistema.

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> Información sobre los idiomas del proveedor de SMS  

El proveedor de SMS funciona independientemente del idioma de visualización del servidor en el que lo instale.  

Cuando un usuario administrativo o un proceso de Configuration Manager solicitan datos a través del proveedor de SMS, este intenta devolver los datos en un formato que coincida con el idioma del sistema operativo del equipo que realiza la solicitud.

La forma en la que intenta hacer coincidir el idioma es indirecta. El proveedor de SMS no traduce la información de un idioma a otro. Al devolver datos para su visualización en la consola de Configuration Manager, el idioma de visualización de los datos depende del origen del objeto y del tipo de almacenamiento.  

Cuando Configuration Manager almacena los datos de un objeto en la base de datos, los idiomas disponibles dependen de los siguientes factores:  

- Configuration Manager almacena objetos que crea usando el soporte para varios idiomas. Almacena el objeto en la base de datos de sitio mediante los idiomas que configure para el sitio al ejecutar el programa de instalación. La consola de Configuration Manager muestra estos objetos en el idioma de visualización del equipo que realiza la solicitud, cuando ese idioma está disponible para el objeto. Si la consola no puede mostrar el objeto en el idioma de visualización del equipo que realiza la solicitud, muestra el idioma predeterminado, que es el inglés.  

- Configuration Manager almacena los objetos creados por un usuario administrativo en el idioma que se utilizó para crear el objeto. Estos objetos se muestran en la consola de Configuration Manager en este mismo idioma. El proveedor de SMS no puede traducirlos y no tiene distintas opciones de idioma.  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> Uso de proveedores de SMS múltiples  

Cuando un sitio completa la instalación, puede instalar proveedores de SMS adicionales para el sitio. Para instalar proveedores de SMS adicionales, ejecute el programa de instalación de Configuration Manager en el servidor del sitio.

Considere la posibilidad de instalar proveedores de SMS adicionales cuando se cumpla cualquiera de las siguientes condiciones:  

- Muchos usuarios administrativos tienen que utilizar la consola de Configuration Manager y se conectarán a un sitio al mismo tiempo.  

- Va a usar el SDK de Configuration Manager u otros productos, que podrían introducir llamadas frecuentes al proveedor de SMS.  

- Tiene un requisito empresarial para alta disponibilidad del proveedor de SMS.  

Cuando se instalan varios proveedores de SMS en un sitio y se establece una solicitud de conexión, el sitio asigna de forma aleatoria cada nueva solicitud de conexión para que use un proveedor de SMS instalado. No se puede especificar el proveedor de SMS para usarlo con una sesión de conexión específica.  

> [!NOTE]  
> Tenga en cuenta las ventajas e inconvenientes de cada ubicación de proveedor de SMS. Para obtener más información, vea [Ubicaciones](#bkmk_location). Compare estas consideraciones con la información que no puede controlar el proveedor de SMS que se usará para cada nueva conexión.  

La primera vez que conecta una consola de Configuration Manager a un sitio, la conexión consulta a WMI en el servidor de sitio. Esta consulta identifica una instancia del proveedor de SMS que utiliza la consola. La consola sigue usando esta instancia específica del proveedor de SMS hasta que finaliza la sesión. Si la sesión finaliza porque el servidor del proveedor de SMS no está disponible en la red, la consulta inicial se repite al volver a conectar la consola al sitio. Es posible que el sitio asigne la misma instancia de proveedor de SMS que no está disponible. Si se produce este comportamiento, intente volver a conectar la consola hasta que el sitio devuelva un proveedor de SMS disponible.  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> Información sobre el espacio de nombres del proveedor de SMS  

El esquema de WMI de Configuration Manager define la estructura del proveedor de SMS. Los espacios de nombres del esquema describen la ubicación de los datos de Configuration Manager dentro del esquema del proveedor de SMS. La tabla siguiente contiene algunos de los espacios de nombres comunes que utiliza el proveedor de SMS:  

|Espacio de nombres|Descripción|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|El proveedor de SMS, que se usa con frecuencia en la consola de Configuration Manager, el Explorador de recursos, las herramientas de Configuration Manager y los scripts.|  
|`Root\SMS\SMS_ProviderLocation`|La ubicación de los equipos del proveedor de SMS de un sitio.|  
|`Root\CIMv2`|La ubicación inventariada de la información del espacio de nombres WMI durante el inventario de hardware y software.|  
|`Root\CCM`|Directivas de configuración del cliente de Configuration Manager y datos de cliente.|  
|`Root\CIMv2\SMS`|La ubicación de clases de informes de inventario que el agente cliente de inventario recopila. Los clientes compilan estas opciones durante la evaluación de la directiva de equipo. Esta configuración se basa en la configuración del cliente para el equipo.|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a> Requisitos para la implementación del sistema operativo

El equipo en el que va a instalar una instancia del proveedor de SMS requiere una versión compatible de Windows ADK.  

Para obtener más información sobre este requisito, vea [Requisitos de infraestructura para la implementación del sistema operativo](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10) y [Compatibilidad con Windows 10](../configs/support-for-windows-10.md).  

Al administrar implementaciones de sistema operativo, Windows ADK permite al proveedor de SMS completar varias tareas, como las siguientes:  

- Ver detalles de archivo WIM  

- Agregar archivos de controladores a imágenes de arranque existentes  

- Crear archivos ISO de arranque  

La instalación de Windows ADK puede requerir hasta 650 MB de espacio libre en disco en cada equipo en el que se instala al proveedor de SMS. Estos importantes requisitos de espacio de disco son necesarios para que Configuration Manager pueda instalar las imágenes de arranque de Windows PE.  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a> Servicio de administración

<!--3607711, fka 1321523-->

El proveedor de SMS proporciona acceso de interoperabilidad de API a través de una conexión HTTPS OData, denominada **servicio de administración**. Esta API REST puede usarse en lugar de un servicio web personalizado para acceder a información desde el sitio.

Para más información, vea [¿Qué es el servicio de administración?](../../../develop/adminservice/overview.md)
