---
title: Flujo de trabajo de autenticación de Azure AD
titleSuffix: Configuration Manager
description: Detalles del proceso de instalación del cliente de Configuration Manager en un dispositivo Windows 10 con la autenticación de Azure Active Directory.
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695003"
---
# <a name="azure-ad-authentication-workflow"></a>Flujo de trabajo de autenticación de Azure AD

*Se aplica a: Configuration Manager (rama actual)*

Este artículo es una referencia técnica para el proceso de instalación del cliente de Configuration Manager en un dispositivo Windows 10 unido a Azure Active Directory (Azure AD). Detalla el proceso de flujo de trabajo para la autenticación del dispositivo y la instalación del cliente.  
 

## <a name="azure-ad-token-request-workflow"></a>Flujo de trabajo de solicitud de token de Azure AD

![Diagrama de flujo de trabajo de CCMSetup de Azure AD](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Solicitud de token de Azure AD

Un cliente unido al dominio de Azure AD de Windows 10 usa parámetros de Azure AD para solicitar un token. Las entradas siguientes se registran en **ccmsetup.log**:

- Solicite un token de dispositivo de Azure AD:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Si no puede obtener un token de dispositivo, solicita un token de usuario de Azure AD:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> Un cliente debe obtener un certificado de unión al área de trabajo (WPJ) cuando se une a Azure AD. Si no se encuentra un certificado de unión al área de trabajo, el cliente no intenta crear la solicitud con el canal de comunicación del servicio de token de seguridad (CCM_STS). Este comportamiento se debe a que el cliente no puede agregar un token de Azure AD a la solicitud. Habitualmente, el dispositivo no tiene este certificado cuando el cliente no está unido correctamente a Azure AD.
>
> Además, si el token no es válido, Cloud Management Gateway (CMG) no reenvía la solicitud a los roles de sitio internos. El token puede no ser válido si el inquilino no está registrado como un servicio de administración en la nube en Configuration Manager.


### <a name="2-configuration-manager-client-token-request"></a>2. Solicitud de token del cliente de Configuration Manager

Una vez que el cliente tiene un token de Azure AD, solicita un token del cliente de Configuration Manager (CCM).

Las entradas siguientes se registran en **ccmsetup.log** de la máquina virtual de CMG:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 CMG recibe la solicitud

Las entradas siguientes se registran en **IIS.log**:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 CMG reenvía la solicitud al punto de conexión de CMG

Las entradas siguientes se registran en **CMGService.log**:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 El punto de conexión de CMG transforma la solicitud del cliente de CMG en una solicitud del cliente del punto de administración

Las entradas siguientes se registran en **SMS_CLOUD_PROXYCONNECTOR.log**:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 El punto de administración comprueba el token de usuario en la base de datos del sitio

Las entradas siguientes se registran en **CCM_STS.log**:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Solicitud de ubicación de contenido

Una vez que el cliente recibe una respuesta con el token de CCM, lo almacena en caché y lo usa para solicitar la ubicación del contenido y la información del sitio a través de CMG. Las entradas siguientes se registran en **ccmsetup.log**:

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Instalación de cliente

El dispositivo descarga el contenido del cliente e inicia la instalación.

### <a name="communication-validation"></a>Validación de la comunicación

- CMG valida el token de cliente a través de CMG, el punto de conexión de CMG y HTTP(s) y la solicitud de base de datos del punto de administración.
- El cliente comprueba el certificado de administración o el certificado de servicio de CMG
- PKI para el certificado de servicio de CMG: El cliente requiere la entidad de certificación raíz (CA) del certificado de CMG en el almacén local
- Certificado de servicio de CMG de terceros: Los clientes validan automáticamente un certificado con su CA raíz publicado en Internet


## <a name="common-issues"></a>Problemas comunes

- No hay CA raíz
- Comprobación de CRL habilitada: publique la CRL en Internet o use la opción **/NoCRLcheck** en la línea de comandos
- No se encuentra el certificado de WPJ: el cliente está registrado con Azure AD, pero no está unido a él.

Usar /NoCRLCheck solo se usa para el arranque de ccmsetup. Para que los clientes cuenten con todas las funcionalidades, debe publicar la CRL en Internet. Como solución alternativa, puede deshabilitar la comprobación de CRL en la configuración de la comunicación del cliente del sitio. En caso contrario, después de que el servicio de ubicación actualiza la configuración de seguridad, los clientes dejarán de comunicarse con el servidor.


## <a name="client-registration"></a>Registro de cliente

![Diagrama del flujo de trabajo de registro de Azure AD](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. Registro de solicitudes de cliente de Configuration Manager

Las siguientes entradas se registran en **ClientIDManagerStartup.log**:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. Token de Azure AD de la solicitud de Configuration Manager para registrar el cliente

Las siguientes entradas se registran en **ADALOperationProvider.log**:

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2.1. El cliente de Configuration Manager está registrado.  

Las siguientes entradas se registran en **ClientIDManagerStartup.log**:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> Durante el registro del cliente, siempre se ejecuta la validación de certificados. Este proceso se produce incluso si usa el método de autenticación de Azure AD para registrar el cliente.


### <a name="3-configuration-manager-client-token-request"></a>3. Solicitud de token del cliente de Configuration Manager

Una vez que el cliente se registra en el sitio, el cliente solicita un token CCM. El token CCM se cifra para la cuenta de sistema local (S-1-5-18) y se almacena en caché durante ocho horas. Al cabo de este tiempo, el token expira y el cliente solicita su renovación.

Las siguientes entradas se registran en **ClientIDManagerStartup.log**:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3.1. CMG recibe la solicitud

Las entradas siguientes se registran en **IIS.log**:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3.2. CMG reenvía la solicitud al punto de conexión de CMG

Las entradas siguientes se registran en **CMGService.log**:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3.3. El punto de conexión de CMG transforma la solicitud del cliente de CMG en una solicitud del cliente del punto de administración

Las entradas siguientes se registran en **SMS_CLOUD_PROXYCONNECTOR.log**:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3.4. El punto de administración comprueba el token del usuario en la base de datos del sitio

Las entradas siguientes se registran en **CCM_STS.log**:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
