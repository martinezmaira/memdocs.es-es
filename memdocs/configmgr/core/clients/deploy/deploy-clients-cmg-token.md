---
title: Autenticación basada en tokens para CMG
titleSuffix: Configuration Manager
description: Registre un cliente de un solo token en la red interna o cree un token de registro masivo para dispositivos basados en Internet.
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 55997c9185a221d105aa8ad40bbb14021463d07b
ms.sourcegitcommit: da5bfbe16856fdbfadc40b3797840e0b5110d97d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512706"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Autenticación basada en tokens para Cloud Management Gateway

*Se aplica a: Configuration Manager (rama actual)*

<!--5686290-->

Las puertas de enlace de administración en la nube (CMG) admiten muchos tipos de clientes, pero, incluso con un protocolo [HTTP mejorado](../../plan-design/hierarchy/enhanced-http.md), estos clientes requieren un [certificado de autenticación de cliente](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway). Este requisito de certificado puede ser difícil de aprovisionar en clientes basados en Internet que no se suelen conectar a la red interna, no consiguen conectar con Azure Active Directory (Azure AD) y no disponen de ningún método para instalar un certificado emitido con PKI.

Para superar estos desafíos, a partir de la versión 2002, Configuration Manager amplía su compatibilidad de dispositivos emitiendo sus propios tokens de autenticación a los dispositivos. Para aprovechar al máximo esta característica, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Este escenario no funciona completamente hasta que la versión del cliente es también la más reciente. Si es necesario, asegúrese de [promover el nuevo cliente a producción](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production).

 Los clientes se registran inicialmente para estos tokens mediante uno de los dos métodos siguientes:

- Red interna

- Registro masivo

El cliente de Configuration Manager junto con el punto de administración administra este token, por lo que no hay ninguna dependencia de la versión del sistema operativo. Esta característica está disponible para cualquier [versión del sistema operativo de cliente compatible](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> Estos métodos solo admiten escenarios de administración centrados en dispositivos.
>
> Microsoft recomienda conectar los dispositivos con Azure AD. Los dispositivos basados en Internet pueden usar Azure AD para autenticarse con Configuration Manager. También habilita los escenarios de usuario y dispositivo tanto si el dispositivo está usando Internet como si está conectado a la red interna. Para obtener más información, consulte [Instalar y registrar el cliente con la identidad de Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="internal-network-registration"></a>Registro de red interna

Este método requiere que el cliente primero se registre con el punto de administración en la red interna. Habitualmente, el registro de cliente se lleva a cabo justo después de la instalación. El punto de administración proporciona al cliente un único token que indica que está usando un certificado autofirmado. Cuando el cliente usa un perfil itinerante en Internet, para conectar con la CMG vincula su certificado autofirmado con el token emitido con el punto de administración.

El sitio habilita este comportamiento de forma predeterminada.

## <a name="bulk-registration-token"></a>Token de registro masivo

Si no puede instalar ni registrar clientes en la red interna, cree un token de registro masivo. Use este token cuando el cliente haga la instalación en un dispositivo basado en Internet y se registre mediante la CMG. El token de registro masivo tiene un período de validez breve y no se almacena en el cliente ni el sitio. Permite al cliente generar un token único que, si se vincula con su certificado autofirmado, permite autenticarse con la CMG.

> [!NOTE]
> No confunda los tokens de registro masivo con los que Configuration Manager emite a los clientes individuales. El token de registro masivo permite que el cliente se instale inicialmente y se comunique con el sitio. Esta comunicación inicial es lo suficientemente larga para que el sitio emita al cliente su propio y exclusivo token de autenticación de cliente. Después, el cliente usa su token de autenticación para todas las comunicaciones con el sitio mientras está en Internet. Más allá del registro inicial, el cliente no usa ni almacena el token de registro masivo.

Para crear un token de registro masivo para su uso durante la instalación del cliente en dispositivos basados en Internet, realice las siguientes acciones:

1. Inicie sesión en el servidor de sitio de nivel superior en la jerarquía con privilegios de administrador local.

1. Abra un símbolo del sistema como administrador.

1. Ejecute la herramienta de la carpeta `\bin\X64` del directorio de instalación de Configuration Manager en el servidor de sitio `BulkRegistrationTokenTool.exe`. Cree un token nuevo con el parámetro `/new`. Por ejemplo, `BulkRegistrationTokenTool.exe /new`. Para obtener más información, consulte la sección [Uso de la herramienta de tokens de registro masivo](#bulk-registration-token-tool-usage).

1. Copie el token y guárdelo en una ubicación segura.

1. Instale el cliente de Configuration Manager en un dispositivo basado en Internet. Incluya el parámetro de instalación del cliente: [ **/regtoken**](about-client-installation-properties.md#regtoken). La línea de comandos que hay a continuación incluye el resto de las propiedades y los parámetros necesarios:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Para obtener más información sobre esta línea de comandos, vea [Instalar y registrar el cliente con la identidad de Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Este proceso es similar, pero no utiliza las propiedades de Azure AD.

Para comprobarlo, revise el siguiente archivo de registro y busque una entrada similar a la siguiente:<!-- bug 7357499 -->

```ClientLocation.log
Rotating internet management point, new management point [1] is: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 (0) with capabilities: <Capabilities SchemaVersion ="1.0"><Property Name="SSL" Version="1" /></Capabilities>
```

Para solucionar problemas de instalación, revise `%WinDir%\ccmsetup\logs\ccmsetup.log` en el cliente. Después de la instalación, revise `%WinDir%\ccm\logs\ClientIDManagerStartup.log`.

En el servidor, revise los registros siguientes:

- [Registros de CMG](../../plan-design/hierarchy/log-files.md#cloud-management-gateway)
- Punto de administración
  - CCM_STS.log
  - MP_RegistrationManager.log
  - ClientAuth.log

### <a name="known-issues"></a>Problemas conocidos

No se puede crear un token de registro masivo en un sitio que tiene un servidor de sitio en modo pasivo.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Uso de la herramienta de tokens de registro masivo

La herramienta `BulkRegistrationTokenTool.exe` se encuentra en la carpeta `\bin\X64` del directorio de instalación de Configuration Manager en el servidor de sitio. Inicie sesión en el servidor de sitio y ejecute la herramienta como administrador. Es compatible con los siguientes parámetros de línea de comandos:

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Muestra información acerca del uso.

Ejemplo: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/new

Crea un nuevo token de registro masivo.

Ejemplo: `BulkRegistrationTokenTool.exe /new`

La herramienta muestra la siguiente información:
  
- GUID que el sitio usa para realizar un seguimiento de los tokens emitidos.
- El período de validez del token, que es tres días de forma predeterminada.
- El token de registro masivo.

El token no se almacena en el cliente ni en el sitio. Asegúrese de copiar el token desde el símbolo del sistema y de guardarlo en una ubicación segura.

#### <a name="lifetime"></a>/lifetime

Se usa con el parámetro `/new` para especificar el período de validez del token. Especifique un valor entero en minutos. El valor predeterminado es 4320 minutos (tres días). El valor máximo es de 10 080 (7 días).

Ejemplo: `BulkRegistrationTokenTool.exe /lifetime 4320`

## <a name="bulk-registration-token-management"></a>Administración de tokens de registro masivo

Puede ver los tokens de registro masivo creados anteriormente con su duración en la consola de Configuration Manager y bloquear su uso si es necesario. Aunque la base de datos del sitio no almacena tokens de registro masivo.

### <a name="review-a-bulk-registration-token"></a>Revisión de un token de registro masivo

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**.

2. Expanda **Seguridad** y seleccione el nodo **Certificados**. La consola muestra todos los certificados relacionados con el sitio y los tokens de registro masivo en el panel de detalles.

3. Seleccione el token de registro masivo que se quiere a revisar.

Puede filtrar u ordenar el contenido según la columna **Tipo**. Identifique tokens de registro masivo específicos en función de su GUID. Al crear un token de registro masivo, la herramienta muestra el GUID.

### <a name="block-a-bulk-registration-token"></a>Bloqueo de un token de registro masivo

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**.

2. Expanda **Seguridad**, seleccione el nodo **Certificados** y elija el token de registro masivo que quiera bloquear.

3. En la pestaña **Inicio** de la barra de la cinta o en el menú contextual, seleccione **Bloquear**. Para desbloquear tokens de registro masivos bloqueados anteriormente, seleccione la acción **Desbloquear**.

## <a name="token-renewal"></a>Renovación de tokens

El cliente renueva su token único emitido por Configuration Manager una vez al mes y es válido durante 90 días. No es necesario que un cliente se conecte a la red interna para renovar el token. Siempre que el token siga siendo válido, es suficiente conectar con el sitio mediante una CMG. Si el token no se renueva en 90 días, el cliente debe conectarse directamente a un punto de administración en una red interna para recibir un nuevo token.

No se puede renovar un token de registro masivo. Una vez que expire un token de registro masivo, genere otro nuevo para el registro de dispositivos basado en Internet mediante una CMG.

## <a name="see-also"></a>Vea también

- [Planificación de Cloud Management Gateway](../manage/cmg/plan-cloud-management-gateway.md)

- [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](deploy-clients-cmg-azure.md).
