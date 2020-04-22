---
title: Configurar la seguridad
titleSuffix: Configuration Manager
description: Configure las opciones relacionadas con la seguridad para Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701413"
---
# <a name="configure-security-in-configuration-manager"></a>Configuración de la seguridad en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la información de este artículo para configurar opciones relacionadas con la seguridad para Configuration Manager. Se tratan las opciones de seguridad siguientes:
- [Comunicación de equipo cliente](#BKMK_ConfigureClientPKI) para los certificados PKI de cliente  
- [Firma y cifrado](#BKMK_ConfigureSigningEncryption)  
- [Administración basada en roles](#BKMK_ConfigureRBA)  
- [Administración de cuentas](#BKMK_ManageAccounts)  
- [Configuración de Azure Active Directory](#bkmk_azuread)  
- [Configuración de la autenticación del proveedor de SMS](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> Configurar opciones de certificados PKI de cliente  

Si desea usar certificados de infraestructura de clave pública (PKI) para conexiones de cliente a sistemas de sitio que usan Internet Information Services (IIS), use el procedimiento siguiente para configurar las opciones de estos certificados.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Para configurar certificados PKI de cliente  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio primario que se va a configurar.  

2.  En la cinta, haga clic en **Propiedades**. Después, cambie a la pestaña **Comunicación de equipo cliente**.  

    > [!Note]
    > A partir de la versión 1906, esta pestaña se denomina **Communication Security** (Seguridad de la comunicación).<!-- SCCMDocs#1645 -->  

3.  Seleccione la configuración para los sistemas de sitio que usen IIS.  

    - **Solo HTTPS**: los clientes asignados al sitio siempre usan un certificado PKI de cliente al conectarse a sistemas de sitio en los que se usa IIS.  

    - **HTTPS o HTTP**: no es necesario que los clientes usen certificados PKI.  

    - **Use los certificados generados por Configuration Manager en sistemas de sitios HTTP**: Para obtener más información sobre esta opción, vea [HTTP mejorado](../hierarchy/enhanced-http.md).  

4.  Seleccione la configuración para los equipos cliente.  

    - **Usar un certificado PKI de cliente (función de autenticación de cliente) cuando esté disponible**: si elige la configuración del servidor de sitio **HTTPS o HTTP**, seleccione esta opción para usar un certificado PKI de cliente para las conexiones HTTP. El cliente utiliza este certificado en lugar de un certificado autofirmado para autenticarse en los sistemas de sitio. Si ha seleccionado **Solo HTTPS**, esta opción se selecciona de forma automática.  

    Cuando haya más de un certificado de cliente PKI disponible en un cliente, haga clic en **Modificar** para configurar el método de selección de certificado de cliente.  

    Para más información sobre el método de selección de certificados de cliente, vea [Planeación de la selección de certificados de cliente PKI](plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

    - **Los clientes comprueban la lista de revocación de certificados (CRL) para sistemas de sitio**: habilite esta opción para que los clientes comprueben si hay certificados revocados por la CRL de la organización.  

    Para más información sobre la comprobación de la CRL de los clientes, vea [Planeación de la revocación de certificados PKI](plan-for-security.md#BKMK_PlanningForCRLs).  

5.  Para importar, ver y eliminar los certificados de entidades de certificación raíz de confianza, haga clic en **Establecer**.  

    Para obtener más información, vea [Planeación de los certificados raíz de confianza PKI y la lista de emisores de certificados](plan-for-security.md#BKMK_PlanningForRootCAs).  


Repita este procedimiento para todos los sitios primarios de la jerarquía.  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> Configurar la firma y el cifrado  

Configure las opciones de firma y cifrado más seguras para los sistemas de sitio que pueden admitir todos los clientes en el sitio. Estas opciones son especialmente importantes cuando se permite a los clientes comunicarse con sistemas de sitio mediante certificados autofirmados a través de HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Para configurar la firma y el cifrado para un sitio  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio primario que se va a configurar.  

2.  En la cinta, haga clic en **Propiedades** y, después, cambie a la pestaña **Firma y cifrado**.  

    Esta pestaña está disponible solamente en un sitio primario. Si no puede ver la pestaña **Firma y cifrado**, asegúrese de que no está conectado a un sitio de administración central o a un sitio secundario.  

3.  Configure las opciones de firma y cifrado para que los clientes se comuniquen con el sitio.  

    - **Requerir firma**: los clientes firman los datos antes de enviarlos al punto de administración.  

    - **Requerir SHA-256**: los clientes usan el algoritmo SHA-256 al firmar los datos.  

    > [!WARNING]  
    >  No use **Requerir SHA-256** sin confirmar antes que todos los clientes admiten este algoritmo hash. Estos clientes incluyen los que es posible que se asignen al sitio en el futuro.  
    >   
    >  Si selecciona esta opción y los clientes con certificados autofirmados no admiten SHA-256, Configuration Manager los rechaza. El componente SMS_MP_CONTROL_MANAGER registra el identificador de mensaje 5443.  

    - **Usar cifrado**: los clientes cifran los mensajes de estado y datos de inventario de cliente antes de enviarlos al punto de administración. Usan el algoritmo 3DES.  

Repita este procedimiento para todos los sitios primarios de la jerarquía.  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> Configurar la administración basada en roles  

La administración basada en roles combina roles de seguridad, ámbitos de seguridad y recopilaciones asignadas para definir el ámbito administrativo de cada usuario administrativo. Un ámbito incluye los objetos que un usuario puede ver en la consola y las tareas relacionadas con esos objetos que tiene permiso para realizar. Las configuraciones de la administración basada en roles se aplican en cada sitio en una jerarquía.  

Para obtener más información, vea [Configurar la administración basada en roles](../../servers/deploy/configure/configure-role-based-administration.md). En este artículo se describen las acciones siguientes:  

- Crear roles de seguridad personalizados  

- Configurar roles de seguridad  

- Configurar ámbitos de seguridad para un objeto  

- Configurar recopilaciones para administrar la seguridad  

- Crear un nuevo usuario administrativo  

- Modificar el ámbito administrativo de un usuario administrativo  

> [!IMPORTANT]  
>  Su propio ámbito administrativo define los objetos y valores que se pueden asignar al configurar la administración basada en roles para otro usuario administrativo. Para obtener información sobre la planificación de la administración basada en roles, vea [Aspectos básicos de la administración basada en roles](../../understand/fundamentals-of-role-based-administration.md).  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a> Administración de las cuentas que usa Configuration Manager  

Configuration Manager es compatible con cuentas de Windows para muchos usos y tareas diferentes. Use el procedimiento siguiente para ver las cuentas que están configuradas para las diferentes tareas y administrar la contraseña que usa Configuration Manager para cada cuenta:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Para administrar las cuentas que usa Configuration Manager  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Seguridad** y, después, haga clic en el nodo **Cuentas**.  

2.  Para cambiar la contraseña de una cuenta, seleccione la cuenta en la lista. Después, haga clic en **Propiedades** en la cinta.  

3.  Haga clic en **Establecer** para abrir el cuadro de diálogo **Cuenta de usuario de Windows**. Especifique la contraseña nueva para que Configuration Manager la use para esta cuenta.  

    > [!NOTE]  
    >  La contraseña que especifique debe coincidir con la de esta cuenta en Active Directory.  

Para obtener más información, vea [Cuentas que se usan en Configuration Manager](../hierarchy/accounts.md).



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a> Configuración de Azure Active Directory

Integre Configuration Manager con Azure Active Directory (Azure AD) para simplificar y habilitar el entorno para la nube. Permita que el sitio y los clientes se autentiquen mediante Azure AD. Para obtener más información, vea el servicio **Administración en la nube** de [Configuración de servicios de Azure](../../servers/deploy/configure/azure-services-wizard.md).



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a> Configuración de la autenticación del proveedor de SMS

A partir de la versión 1810, puede especificar el nivel mínimo de autenticación para que los administradores accedan a sitios de Configuration Manager. Esta característica exige que los administradores inicien sesión en Windows con el nivel requerido. Para más información, vea [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth) (Planear el proveedor de SMS). <!--1357013-->  



## <a name="see-also"></a>Vea también

- [Planear la seguridad](plan-for-security.md)  

- [Seguridad y privacidad para los clientes de Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Comunicaciones entre puntos de conexión](../hierarchy/communications-between-endpoints.md)  

- [Referencia técnica de controles criptográficos](cryptographic-controls-technical-reference.md)  

- [Requisitos de certificados PKI](../network/pki-certificate-requirements.md)  
