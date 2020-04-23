---
title: Fundamentos de seguridad
titleSuffix: Configuration Manager
description: Obtenga información sobre los niveles de seguridad en Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707063"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Fundamentos de seguridad de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se resume los siguientes componentes de seguridad fundamentales de cualquier entorno de Configuration Manager:
- [Niveles de seguridad](#bkmk_layers)
- [Administración basada en roles](#bkmk_rba)
- [Protección de puntos de conexión de cliente](#bkmk_endpoints)
- [Cuentas y grupos de Configuration Manager](#bkmk_accounts)
- [Privacidad](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a> Niveles de seguridad

La seguridad en Configuration Manager consta de los niveles siguientes: 
- [Seguridad de red y del sistema operativo Windows](#bkmk_layer-windows)
- [Infraestructura de red: firewalls, detección de intrusiones, infraestructura de clave pública (PKI)](#bkmk_layer-network)
- [Controles de seguridad de Configuration Manager](#bkmk_layer-cm)
- [Proveedor de SMS](#bkmk_layer-provider)
- [Permisos de base de datos del sitio](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a> Seguridad de red y del sistema operativo Windows
El primer nivel procede de las características de seguridad de Windows para el sistema operativo y la red. Este nivel incluye los componentes siguientes:  

-   Uso compartido de archivos para transferir archivos entre componentes de Configuration Manager  

-   Listas de control de acceso (ACL) para proteger archivos y claves del Registro  

-   Protocolo de seguridad de Internet (IPsec) para ayudar a proteger las comunicaciones  

-   Directiva de grupo para establecer la directiva de seguridad  

-   Permisos de Modelo de objetos componentes distribuidos (DCOM) para aplicaciones distribuidas, como la consola de Configuration Manager  

-   Servicios de dominio de Active Directory para almacenar entidades de seguridad  

-   Seguridad de cuenta de Windows, incluidos varios grupos que se crean durante la instalación de Configuration Manager  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a> Infraestructura de red

Los componentes de seguridad adicionales, como firewalls y detección de intrusiones, proporcionan protección en todo el entorno. Los certificados emitidos por implementaciones de PKI estándar del sector permiten proporcionar autenticación, firma y cifrado.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a> Controles de seguridad de Configuration Manager

Además de la seguridad proporcionada por la infraestructura de red y Windows Server, Configuration Manager controla el acceso a su consola y sus recursos de varias maneras. De manera predeterminada, solo los administradores locales tienen derechos sobre los archivos y las claves del Registro que requiere la consola de Configuration Manager en los equipos en los que se instale.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a> Proveedor de SMS

La siguiente capa de seguridad se basa en el acceso a través del Instrumental de administración de Windows (WMI) y, específicamente, mediante el proveedor de SMS. El proveedor de SMS es un componente de Configuration Manager que concede a los usuarios acceso a la base de datos del sitio para consultar información. De forma predeterminada, el acceso al proveedor está limitado a los miembros del grupo de Administradores SMS. En principio, este grupo solo contiene el usuario que ha instalado Configuration Manager. Para conceder a otras cuentas permisos en el depósito del modelo de información común (CIM) y el proveedor de SMS, agréguelas al grupo Administradores de SMS.  

A partir de la versión 1810, puede especificar el nivel mínimo de autenticación para que los administradores accedan a sitios de Configuration Manager. Esta característica exige que los administradores inicien sesión en Windows con el nivel requerido. <!--1357013-->  

Para más información, vea [Plan for the SMS Provider](../plan-design/hierarchy/plan-for-the-sms-provider.md) (Planear el proveedor de SMS).

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a> Permisos de base de datos del sitio

La capa final de seguridad se basa en los permisos de objetos de la base de datos del sitio. De manera predeterminada, la cuenta de sistema local y la cuenta de usuario que ha usado para instalar Configuration Manager pueden administrar todos los objetos de la base de datos del sitio. Conceda y restrinja permisos a usuarios administrativos adicionales en la consola de Configuration Manager mediante la administración basada en roles.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a> Administración basada en roles  

 Configuration Manager usa la administración basada en roles para proteger objetos como recopilaciones, implementaciones y sitios. Este modelo de administración define y administra de manera centralizada la configuración de acceso de seguridad de la totalidad de la jerarquía para todos los sitios y sus configuraciones. 

 Un administrador asigna *roles de seguridad* a los usuarios administrativos y los permisos de grupo. Los permisos se conectan a diferentes tipos de objeto de Configuration Manager, por ejemplo para crear o cambiar la configuración de cliente. 

 Los *ámbitos de seguridad* agrupan instancias específicas de objetos que un usuario administrativo se encarga de administrar, como una aplicación que instala Microsoft Office. 

 La combinación de roles de seguridad, ámbitos de seguridad y recopilaciones define los objetos que un usuario administrativo puede ver y administrar. Configuration Manager instala algunos roles de seguridad predeterminados para tareas de administración habituales. Cree roles de seguridad propios para satisfacer requisitos empresariales específicos.  

 Para obtener más información, vea [Configurar la administración basada en roles](../servers/deploy/configure/configure-role-based-administration.md).  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a> Protección de puntos de conexión de cliente  

 Configuration Manager protege la comunicación de cliente a los roles de sistema de sitio mediante el uso de certificados PKI autofirmados o tokens de Azure Active Directory (Azure AD). Algunos escenarios requieren el uso de certificados PKI. Por ejemplo, la [administración de clientes basada en Internet](../clients/manage/plan-internet-based-client-management.md) y para los [clientes de dispositivos móviles](../../mdm/plan-design/plan-on-premises-mdm.md).  

 Puede configurar los roles de sistema de sitio a los que se conectan los clientes para la comunicación de cliente HTTPS o HTTP. Los equipos cliente siempre se comunican mediante el método más seguro disponible. Los equipos cliente solo recurren al método de comunicación menos seguro si tiene roles de sistema de sitio que permiten la comunicación HTTP.  

 Para obtener más información, vea [Planificar la seguridad](../plan-design/security/plan-for-security.md).



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a> Cuentas y grupos de Configuration Manager  

 Configuration Manager usa la cuenta del sistema local para la mayoría de las operaciones de sitio. Es posible que algunas tareas de administración requieran la creación y el mantenimiento de cuentas adicionales. Durante la instalación, Configuration Manager crea varios roles de SQL Server y grupos predeterminados. Es posible que tenga que agregar manualmente cuentas de equipo o usuario a los roles de SQL Server y grupos predeterminados.  

 Para obtener más información, vea [Cuentas que se usan en Configuration Manager](../plan-design/hierarchy/accounts.md).  



## <a name="privacy"></a><a name="bkmk_privacy"></a> Privacidad  

 Antes de implementar Configuration Manager, tenga en cuenta los requisitos de privacidad. Aunque los productos de administración empresarial ofrecen muchas ventajas ya que permiten administrar de forma eficaz una gran cantidad de clientes, es posible que este software afecte a la privacidad de los usuarios de la organización. Configuration Manager incluye un gran número de herramientas para la recopilación de datos y la supervisión de dispositivos. Es posible que algunas herramientas ocasionen problemas relacionados con la privacidad en la organización.  

 Por ejemplo, al instalar el cliente de Configuration Manager, se habilitan mucha opciones de administración de manera predeterminada. Esta configuración hace que el software cliente envíe información al sitio de Configuration Manager. El sitio almacena la información de cliente en la base de datos del sitio. La información del cliente no se envía directamente a Microsoft. Para obtener más información, vea [Diagnósticos y datos de uso](../plan-design/diagnostics/diagnostics-and-usage-data.md).



## <a name="see-also"></a>Vea también

- [Planear la seguridad](../plan-design/security/plan-for-security.md)  

- [Seguridad y privacidad para los clientes de Configuration Manager](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurar la seguridad](../plan-design/security/configure-security.md)   

- [Comunicaciones entre puntos de conexión](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Referencia técnica de controles criptográficos](../plan-design/security/cryptographic-controls-technical-reference.md)  
