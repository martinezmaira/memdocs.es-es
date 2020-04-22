---
title: Requisitos previos de la implementación de clientes de Windows
titleSuffix: Configuration Manager
description: Obtenga información sobre los requisitos previos para la implementación del cliente de Configuration Manager en equipos Windows.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d4cd7ffe38f7191a5361ad2e89817ea80f9f093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694793"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Requisitos previos para la implementación de clientes en equipos Windows con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La implementación de clientes de Configuration Manager en su entorno tiene las siguientes dependencias externas y dependencias dentro del producto. Además, cada método de implementación de cliente tiene sus propias dependencias, que se deben cumplir para que instalaciones de cliente se realicen correctamente.  

Para obtener más información sobre los requisitos mínimos de hardware y sistema operativo para el cliente de Configuration Manager, vea [Configuraciones admitidas](../../plan-design/configs/supported-configurations.md).  

> [!NOTE]  
> Los números de versión de software que se muestran en este artículo solo indican los números de versión mínimos necesarios.  


## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a> Requisitos previos para los clientes de Windows  

Use la información siguiente para determinar los requisitos previos para la instalación del cliente de Configuration Manager en dispositivos Windows.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  

|Componente|Descripción|  
|---|---|  
|Windows Installer versión 3.1.4000.2435|Necesario para admitir el uso de los archivos de actualización (.msp) de Windows Installer para paquetes y actualizaciones de software.|  
|Microsoft Background Intelligent Transfer Service (BITS) versión 2.5|Se requiere para permitir transferencias de datos limitadas entre el equipo cliente y los sistemas de sitio de Configuration Manager. BITS no se descarga automáticamente durante la instalación del cliente. Cuando se instala BITS en los equipos, normalmente es necesario reiniciarlo para completar la instalación.<br /><br /> La mayoría de los sistemas operativos incluyen BITS. En caso contrario, instale BITS antes de instalar el cliente de Configuration Manager.|  
|Programador de tareas de Microsoft|Habilite este servicio en el cliente para completar la instalación del cliente.|  
|Compatibilidad con la firma de código SHA-2|A partir de la versión 1906, los clientes requieren compatibilidad con el algoritmo de firma de código SHA-2. Para más información, consulte [Compatibilidad con la firma de código SHA-2](#bkmk_sha2).|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a> Compatibilidad con la firma de código SHA-2

<!--SCCMDocs-pr#3404-->
Debido a la vulnerabilidad del algoritmo SHA-1 y para estar en línea con los estándares del sector, Microsoft ahora solo firma archivos binarios de Configuration Manager con el algoritmo SHA-2, que es más seguro. Las versiones heredadas del sistema operativo Windows requieren una actualización para admitir la firma de código SHA-2. Para más información, consulte la información sobre el [requisito de compatibilidad con la firma de código SHA-2 para Windows y WSUS de 2019](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus).

Si no actualiza estas versiones del sistema operativo, no puede instalar la versión de cliente 1906 de Configuration Manager. Este comportamiento se aplica a cualquier instalación de cliente nueva o a su actualización a partir de una versión anterior.

Si tiene que administrar un cliente en una versión de Windows que no está actualizada o que es anterior a las versiones mencionadas, use la versión 1902 del cliente de interoperabilidad extendida (EIC) de Configuration Manager. Para más información, consulte [Cliente de interoperabilidad extendida](../../understand/interoperability-client.md).

> [!Tip]  
> Si no usa la [actualización automática de cliente](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) y actualiza los clientes con otro mecanismo, asegúrese de actualizar la versión de ccmsetup. Es posible que una versión anterior de ccmsetup no valide correctamente el nuevo certificado de firma de código SHA-2 en los archivos binarios de cliente de la versión 1906. Por ejemplo, si copia ccmsetup.exe en un recurso compartido o usa ccmsetup.msi con una directiva de grupo.<!-- 4963362 -->
>
> Los mecanismos de actualización de cliente siguientes no deberían verse afectados:
>
> - Instalación de inserción de cliente: usa el paquete de cliente del sitio.
> - Instalación basada en actualizaciones de software: la actualización del sitio se vuelve a publicar en WSUS.
> - Dispositivos Windows administrados por MDM con Intune: La versión compatible con este mecanismo ya admite la firma de código SHA-2, pero sigue siendo importante para usar la versión más reciente de ccmsetup.msi.

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a> Dependencias externas a Configuration Manager y descarga automática durante la instalación  

El cliente de Configuration Manager tiene dependencias externas. Estas dependencias dependen de la versión del sistema operativo y del software instalado en el equipo cliente.  

Si el cliente requiere estas dependencias para completar la instalación, las instala de forma automática.  

|Componente|Descripción|  
|---|---|  
|Windows Update Agent versión 7.0.6000.363|Necesario para que Windows admita la detección e implementación de actualizaciones.|  
|Microsoft Core XML Services (MSXML) versión 6.20.5002 o posterior|Necesario para admitir el procesamiento de documentos XML en Windows.|  
|Compresión diferencial remota de Microsoft (RDC)|Necesario para optimizar la transmisión de datos a través de la red.|  
|Microsoft Visual C++ 2013 Redistributable versión 12.0.21005.1|Necesario para admitir las operaciones de cliente. Cuando se instala esta actualización en los equipos cliente, es posible que sea necesario reiniciar para completar la instalación.|  
|Microsoft Visual C++ 2005 Redistributable versión 8.0.50727.42|Para la versión 1606 y anteriores, es necesario admitir las operaciones de Microsoft SQL Server Compact.|  
|API de creación de imágenes de Windows 6.0.6001.18000|Necesarias para permitir que Configuration Manager administre archivos de imagen de Windows (.wim).|  
|Microsoft Policy Platform 1.2.3514.0|Necesaria para permitir a los clientes evaluar la configuración de la conformidad.|  
|Microsoft .NET Framework versión 4.5.2.|Necesario para admitir las operaciones de cliente. Se instala automáticamente en el equipo cliente si este no tiene instalado Microsoft .NET Framework versión 4.5 o posterior. Para más información, consulte [Detalles adicionales sobre la versión 4.5.2 de Microsoft .NET Framework](#dotNet).|  
|Componentes de Microsoft SQL Server Compact 4.0 SP1|Necesarios para almacenar información relacionada con las operaciones de cliente.|  

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> Si sigue usando la experiencia de usuario del sitio web del catálogo de aplicaciones, el cliente requiere Microsoft Silverlight 5.1.41212.0. El cliente no instala Silverlight automáticamente. La funcionalidad principal del Catálogo de aplicaciones ahora se incluye en el Centro de software.<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a> Detalles adicionales sobre la versión 4.5.2 de Microsoft .NET Framework  

> [!NOTE]  
> Ya no se admiten .NET 4.0, 4.5 y 4.5.1. Para obtener más información, vea [Preguntas frecuentes del ciclo de vida: .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Es posible que sea necesario reiniciar en la versión 4.5.2 de Microsoft .NET Framework para completar la instalación. El usuario ve una notificación **Es necesario reiniciar** en la bandeja del sistema. Los escenarios comunes siguientes requieren el reinicio de los equipos cliente:  

- Aplicaciones o servicios .NET que estén en ejecución en el equipo.  

- Faltan una o varias actualizaciones de software necesarias para la instalación de .NET.  

- El equipo tiene pendiente un reinicio de la instalación anterior de actualizaciones de software de .NET Framework.  

Después de instalar .NET Framework 4.5.2, puede requerir actualizaciones adicionales. Estas actualizaciones posteriores pueden requerir reinicios adicionales.  

### <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

Para obtener más información, vea [Roles de sistema de sitio para clientes](plan/determine-the-site-system-roles-for-clients.md).  

|Componente|Descripción|  
|---|---|  
|Punto de administración|Para implementar al cliente de Configuration Manager, no se necesita un punto de administración. Los clientes requieren un punto de administración para transferir información con el sitio. Sin un punto de administración, no se pueden administrar los equipos cliente.|  
|Punto de distribución|El punto de distribución es un rol del sistema de sitio opcional, aunque recomendado para la implementación y administración de los clientes. Todos los puntos de distribución hospedan los archivos de origen de cliente. Los clientes buscan el punto de distribución más cercano desde el que se van a descargar los archivos de origen durante la implementación o actualización del cliente. Si el sitio no tiene un punto de distribución, los equipos descargan los archivos de origen del cliente desde su punto de administración.|  
|Punto de estado de reserva|El punto de estado de reserva es un rol del sistema de sitio opcional, aunque recomendado para la implementación de clientes. El punto de estado de reserva realiza el seguimiento de la implementación del cliente y permite a los equipos del sitio de Configuration Manager enviar mensajes de estado cuando no se pueden comunicar con un punto de administración.|  
|Punto de servicios de informes|El punto de servicios de informes es un rol de sistema de sitio opcional pero recomendado. Muestra los informes relacionados con la implementación y administración de cliente. Para obtener más información, vea [Introducción a los informes](../../servers/manage/introduction-to-reporting.md).|  

### <a name="installation-method-dependencies"></a>Dependencias de los métodos de instalación  

Los siguientes requisitos previos son específicos para los distintos métodos de instalación de cliente.  

#### <a name="client-push-installation"></a>Instalación de inserción de cliente  

- El sitio usa cuentas de instalación de inserción de cliente para conectarse a los equipos para instalar al cliente. Especifique estas cuentas en la pestaña **Cuentas** de las propiedades de instalación de inserción de cliente. La cuenta debe ser miembro del grupo de administradores locales del equipo de destino.  

    Si no se especifica una cuenta de instalación de inserción de cliente, se usa la cuenta de equipo del servidor de sitio.  

- El sitio debe detectar el equipo en el que se va a instalar al cliente. Se necesita al menos un método de detección de Configuration Manager.  

- El equipo tiene un recurso compartido ADMIN$.  

- Para insertar de forma automática el cliente de Configuration Manager en los recursos detectados, seleccione la opción **Habilitar la instalación de inserción de cliente en recursos asignados** en las propiedades de instalación de inserción de cliente.  

- El equipo cliente debe comunicarse con un punto de distribución o un punto de administración para descargar los archivos de código fuente.  

- Cuando se requiere autenticación mutua de Kerberos, los clientes deben estar en un bosque de Active Directory de confianza. Kerberos en Windows se basa en Active Directory para la autenticación mutua.<!--1358204-->  

Para usar la inserción de cliente, necesita los permisos de seguridad siguientes:  

- Para configurar la cuenta de instalación de inserción de cliente: Permiso **Modificar** y **Leer** para el objeto **Sitio**.  

- Para utilizar Inserción del cliente para instalar el cliente en colecciones, dispositivos y consultas: Permiso **Modificar recurso** y **Leer** para el objeto **Recopilación**.  

El rol de seguridad predeterminado **Administrador de infraestructura** incluye los permisos necesarios para administrar la instalación de inserción de cliente.  

#### <a name="software-update-point-based-installation"></a>Instalación basada en el punto de actualización de software  

- Si no se ha ampliado el esquema de Active Directory, o bien se están instalando los clientes desde otro bosque, use la directiva de grupo para aprovisionar los parámetros de instalación para CCMSetup.exe. Para obtener más información, vea [Cómo aprovisionar propiedades de instalación de cliente](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Publique el cliente de Configuration Manager en el punto de actualización de software.  

- Para descargar los archivos de código fuente, el equipo cliente debe comunicarse con un punto de distribución o un punto de administración.  

Para los permisos de seguridad necesarios para administrar actualizaciones de software de Configuration Manager, vea [Requisitos previos para las actualizaciones de software](../../../sum/plan-design/prerequisites-for-software-updates.md).  

#### <a name="group-policy-based-installation"></a>Instalación basada en directivas de grupo  

- Si no se ha ampliado el esquema de Active Directory, o bien se están instalando los clientes desde otro bosque, use la directiva de grupo para aprovisionar los parámetros de instalación para CCMSetup.exe. Para obtener más información, vea [Cómo aprovisionar propiedades de instalación de cliente](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Para descargar los archivos de código fuente, el equipo cliente debe comunicarse con un punto de distribución o un punto de administración.  

#### <a name="logon-script-based-installation"></a>Instalación de inicio de sesión basado en scripts  

Para descargar los archivos de código fuente, el equipo cliente debe comunicarse con un punto de distribución o un punto de administración. A menos que se especificara CCMSetup.exe con el parámetro de línea de comandos siguiente: `ccmsetup /source`.  

#### <a name="manual-installation"></a>Instalación manual  

Para descargar los archivos de código fuente, el equipo cliente debe comunicarse con un punto de distribución o un punto de administración. A menos que se especificara CCMSetup.exe con el parámetro de línea de comandos siguiente: `ccmsetup /source`.  

#### <a name="microsoft-intune-mdm-installation"></a>Instalación de MDM de Microsoft Intune

- Requiere una suscripción a Microsoft Intune y las licencias adecuadas.  

- Requiere que el dispositivo tenga acceso a Internet, incluso si no está basado en Internet.  

- Según el caso de uso, también se pueden requerir una o las dos tecnologías siguientes:  

    - Azure Active Directory  

    - Puerta de enlace de administración en la nube  

#### <a name="workgroup-computer-installation"></a>Instalación de equipo de grupo de trabajo  

Para acceder a los recursos en el dominio de servidor de sitio de Configuration Manager, configure una cuenta de acceso de red para el sitio.  

Para obtener más información sobre cómo configurar la cuenta de acceso a la red, vea [Conceptos básicos de administración de contenido](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Instalación de software basada en distribución (para actualizaciones únicamente)  

- Si no se ha ampliado el esquema de Active Directory, o bien se están instalando los clientes desde otro bosque, use la directiva de grupo para aprovisionar los parámetros de instalación para CCMSetup.exe. Para obtener más información, vea [Cómo aprovisionar propiedades de instalación de cliente](deploy-clients-to-windows-computers.md#BKMK_Provision).

- Para descargar los archivos de código fuente, el equipo cliente debe comunicarse con un punto de distribución o un punto de administración.  

Para consultar los permisos de seguridad necesarios para actualizar el cliente de Configuration Manager mediante la administración de aplicaciones, consulte [Seguridad y privacidad de la administración de aplicaciones](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

#### <a name="automatic-client-upgrades"></a>Actualizaciones de cliente automáticas  

Debe ser miembro del rol de seguridad **Administrador total** para configurar actualizaciones automáticas de cliente.  

### <a name="firewall-requirements"></a>Requisitos de firewall  

Si hay un firewall entre los servidores del sistema de sitio y los equipos en los que se quiere instalar el cliente de Configuration Manager, vea [Configuración de puertos y Firewall de Windows para clientes](windows-firewall-and-port-settings-for-clients.md).  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a> Requisitos previos para clientes de dispositivos móviles  

Cuando se instala el cliente de Configuration Manager en dispositivos móviles y se inscriben, use esta información para determinar los requisitos previos.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager

- Se requiere una entidad de certificación (CA) empresarial de Microsoft con plantillas de certificado para implementar y administrar los certificados necesarios para dispositivos móviles.  

    La entidad emisora debe aprobar automáticamente las solicitudes de certificados de los usuarios de dispositivos móviles durante el proceso de inscripción.  

    Para obtener más información sobre los requisitos de certificados, vea [Seguridad y privacidad de perfiles de certificados](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

- Un grupo de seguridad que contiene los usuarios que pueden inscribir sus dispositivos móviles.  

    Este grupo de seguridad se utiliza para configurar la plantilla de certificado que se utiliza durante la inscripción de dispositivos móviles.  

- Opcional pero recomendado: un alias DNS (registro CNAME), denominado **ConfigMgrEnroll**. Configure este alias para el nombre de servidor del punto de proxy de inscripción.  

    Este alias DNS es necesario para admitir la detección automática para el servicio de inscripción. Si no se configura este registro DNS, los usuarios deben especificar manualmente el nombre del punto de proxy de inscripción como parte del proceso de inscripción.  

- Dependencias del rol de sistema de sitio para los equipos que ejecutan los roles de sistema de sitio del punto de inscripción y del proxy de inscripción.  

    Para obtener más información, vea [Sistemas operativos compatibles con servidores de sistema de sitio](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager

Para obtener más información, vea [Roles de sistema de sitio para clientes](plan/determine-the-site-system-roles-for-clients.md).  

- Punto de administración que se configura para las conexiones de cliente HTTPS y se habilita para dispositivos móviles  

    Siempre es necesario un punto de administración para instalar el cliente de Configuration Manager en dispositivos móviles. Además de los requisitos de configuración de HTTPS y la habilitación para dispositivos móviles, el punto de administración se debe configurar con un FQDN de Internet y aceptar conexiones de cliente de Internet.  

- Punto de inscripción y punto de proxy de inscripción  

    Un punto de proxy de inscripción administra solicitudes de inscripción de dispositivos móviles. El punto de inscripción completa el proceso de inscripción. El punto de inscripción debe estar en el mismo bosque de Active Directory que el servidor de sitio, pero el punto de proxy de inscripción puede estar en otro bosque.  

- Configuración de cliente para la inscripción de dispositivo móvil  

    Configure las opciones de cliente para que los usuarios puedan inscribir dispositivos móviles y configurar como mínimo un perfil de inscripción.  

- Punto de servicios de informes  

    El punto de servicios de informes es un rol de sistema de sitio opcional pero recomendado que permite mostrar informes relacionados con la inscripción de dispositivos móviles y la administración de clientes.  

    Para obtener más información, vea [Introducción a los informes](../../servers/manage/introduction-to-reporting.md).  

- Para configurar la inscripción de dispositivos móviles, debe tener los permisos de seguridad siguientes:  

    - Para agregar, modificar y eliminar roles de sistema de sitio de inscripción: Permiso **Modificar** para el objeto **Sitio**.  

    - Para configurar las opciones de cliente para la inscripción: La configuración de cliente predeterminada requiere el permiso **Modificar** en el objeto **Sitio**, y la configuración de cliente personalizada requiere permisos **Agente cliente**.  

    El rol de seguridad **Administrador total** predeterminado incluye los permisos necesarios para configurar los roles de sistema de sitio de inscripción.  

- Para administrar dispositivos móviles inscritos, debe tener los permisos de seguridad siguientes:  

    - Para borrar o retirar un dispositivo móvil: **Eliminar recurso** para el objeto **Recopilación**.  

    - Para cancelar un comando de borrado o retirada: **Eliminar recurso** para el objeto **Recopilación**.  

    - Para permitir y bloquear dispositivos móviles: **Modificar recurso** para el objeto **Recopilación**.  

    - Para bloquear de forma remota o restablecer la contraseña de un dispositivo móvil: **Modificar recurso** para el objeto **Recopilación**.  

    El rol de seguridad **Administrador de operaciones** predeterminado incluye los permisos necesarios para administrar dispositivos móviles.  

    Para obtener más información sobre cómo configurar los permisos de seguridad, vea [Aspectos básicos de la administración basada en roles](../../understand/fundamentals-of-role-based-administration.md) y [Configurar la administración basada en roles](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Requisitos de firewall

Los dispositivos de red intermedios como los enrutadores, los firewalls y, si se corresponde, Firewall de Windows, deben permitir el tráfico relacionado con la inscripción de dispositivos móviles:  

- Entre los dispositivos móviles y el punto de proxy de inscripción: HTTPS (de forma predeterminada, TCP 443)  

- Entre el punto de proxy de inscripción y el punto de inscripción: HTTPS (de forma predeterminada, TCP 443)  

Si usa un servidor web proxy, se debe configurar para el protocolo de túnel SSL. No se admite el protocolo de puente SSL para dispositivos móviles.  
