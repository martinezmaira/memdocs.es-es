---
title: Administrar dispositivos con MDM local
titleSuffix: Configuration Manager
description: Proteja los datos del dispositivo con borrado completo, eliminación selectiva, bloqueo remoto o restablecimiento de código de acceso mediante Configuration Manager la administración de dispositivos móviles (MDM) local.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724729"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>Administrar dispositivos y proteger los datos con MDM local en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los dispositivos móviles pueden almacenar datos confidenciales y facilitar el acceso a muchos recursos de la organización. Para ayudar a proteger los dispositivos y los datos, use Configuration Manager para las siguientes acciones de administración de dispositivos:

- **Borrado completo**: restaure el dispositivo a su configuración de fábrica

- **Borrado selectivo**: quitar solo los datos de la organización

- **Restablecimiento de código**de acceso: quitar o restablecer el código de acceso cuando un usuario lo olvida

- **Bloqueo remoto**: ayuda a proteger un dispositivo que podría perderse

## <a name="full-wipe"></a>Eliminación completa  

Si necesita proteger un dispositivo perdido o si retira un dispositivo del uso activo, puede iniciar un borrado completo en él. Esta acción restaura el dispositivo a sus valores predeterminados de fábrica. Quita todos los datos y la configuración de los usuarios y la organización.

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** y elija el nodo **dispositivos** . También puede elegir **recopilaciones de dispositivos** y seleccionar una recopilación de la que el dispositivo es miembro.

1. Seleccione el dispositivo que desea borrar.

1. En la cinta de opciones, en el grupo dispositivo, seleccione **acciones de dispositivo remoto**y, a continuación, elija **retirar/borrar**.

1. En la ventana **retirar de Configuration Manager** , seleccione la opción para **borrar el dispositivo móvil y retirarlo de Configuration Manager**.

## <a name="selective-wipe"></a>Borrado selectivo

Para quitar solo los datos de la organización de un dispositivo, inicie un borrado selectivo.

### <a name="behaviors-by-os-version"></a>Comportamientos por versión del sistema operativo

En las tablas siguientes se describen los datos que se quitan y el efecto en los datos que permanecen en el dispositivo después de una eliminación selectiva.

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10, Windows 8.1, Windows RT 8.1 y Windows RT

|Contenido|Comportamiento de eliminación selectiva|  
|-------|--------|
|Aplicaciones y datos asociados instalados por Configuration Manager|Desinstala las aplicaciones y quita las claves de instalación de prueba. Revoca la clave de cifrado para las aplicaciones que usan el borrado selectivo de Windows y ya no se puede tener acceso a los datos.|
|Perfiles de VPN y Wi-Fi|Quita los perfiles.|
|Certificados|Quita y revoca los certificados|
|Configuración|Quita los requisitos|
|Perfiles de correo electrónico|Quita el correo electrónico habilitado para EFS, que incluye la aplicación de correo para el correo electrónico y los datos adjuntos de Windows.|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 Mobile, Windows Phone 8.0 y Windows Phone 8.1

|Contenido|Comportamiento de eliminación selectiva|  
|-------|--------|
|Aplicaciones de empresa y datos asociados instalados por Configuration Manager|Desinstala las aplicaciones y quita los datos de la aplicación de la organización.|
|Perfiles de VPN y Wi-Fi|Quita los perfiles para Windows 10 Mobile y Windows Phone 8,1|
|Certificados|Quita los certificados para Windows Phone 8,1|
|Perfiles de correo electrónico|Quita los perfiles (excepto Windows Phone 8,0)|

La siguiente configuración también se quita de los dispositivos Windows 10 Mobile y Windows Phone 8.1:  

- **Requerir una contraseña para desbloquear dispositivos móviles**  
- **Permitir contraseñas sencillas**  
- **Longitud mínima de la contraseña**  
- **Tipo de contraseña requerida**
- **Expiración de la contraseña (días)**  
- **Recordar el historial de contraseñas**  
- **Número de errores de inicio de sesión consecutivos permitidos antes de que se borre el dispositivo**  
- **Minutos de inactividad antes de que se requiera la contraseña**  
- **Tipo de contraseña requerida: número mínimo de conjuntos de caracteres**  
- **Permitir cámara**
- **Requerir cifrado en el dispositivo móvil**  
- **Permitir almacenamiento extraíble**  
- **Permitir explorador web**  
- **Permitir almacén de aplicaciones**  
- **Permitir captura de pantalla**  
- **Permitir geolocalización**  
- **Permitir cuenta de Microsoft**  
- **Permitir copiar y pegar**  
- **Permitir tethering Wi-Fi**  
- **Permitir conexión automática a zonas Wi-Fi gratuitas**  
- **Permitir informar de zonas Wi-Fi**  
- **Permitir el restablecimiento de la configuración de fábrica**
- **Permitir Bluetooth**  
- **Permitir NFC**
- **Permitir Wi-Fi**

### <a name="start-a-selective-wipe"></a>Iniciar un borrado selectivo

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** y elija el nodo **dispositivos** . También puede elegir **recopilaciones de dispositivos** y seleccionar una recopilación de la que el dispositivo es miembro.

1. Seleccione el dispositivo que desea borrar.

1. En la cinta de opciones, en el grupo dispositivo, seleccione **acciones de dispositivo remoto**y, a continuación, elija **retirar/borrar**.

1. En la ventana **retirar de Configuration Manager** , seleccione la opción siguiente: **borrar el contenido de la compañía y retirar el dispositivo móvil de Configuration Manager**.

### <a name="recommendations-for-selective-wipe"></a>Recomendaciones para el borrado selectivo

- Para un borrado correcto de correo electrónico, configure los perfiles de correo electrónico en Windows Phone dispositivos 8,1.

- Para lograr un borrado correcto de aplicaciones, asegúrese de que estas se distribuyen a través de la administración de aplicaciones de dispositivos móviles.

## <a name="passcode-reset"></a>Restablecimiento de la contraseña

Si un usuario olvida su contraseña, use esta acción para forzar una nueva contraseña temporal en el dispositivo. También puede quitar el código de acceso por completo. En la tabla siguiente se muestra cómo se puede restablecer la contraseña en distintas plataformas móviles.

| Versión del SO | Restablecimiento de la contraseña |
|------------|----------------|
| Windows 10 | No compatible |
| Windows 10 Mobile | Compatible, excepto los dispositivos Unidos a Azure Active Directory |
| Windows Phone 8 y Windows Phone 8.1 | Compatible |
| Windows RT 8.1 | No compatible |
| Windows 8.1 | No compatible |

> [!Note]
> Inicie la acción de restablecimiento del código de acceso desde el sitio de nivel superior. Por ejemplo, si usa un sitio de administración central, solo puede realizar la acción en ese sitio. Si utiliza un sitio primario independiente, solo puede realizar la acción desde ese sitio.

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>Restablecer el código de acceso de forma remota en un dispositivo móvil

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** y elija el nodo **dispositivos** . También puede elegir **recopilaciones de dispositivos** y seleccionar una recopilación de la que el dispositivo es miembro.

1. Seleccione el dispositivo o los dispositivos en los que se va a restablecer el código de acceso.

1. En la cinta de opciones, en el grupo dispositivo, seleccione **acciones de dispositivo remoto**y, a continuación, elija **restablecimiento de código**de acceso.  

### <a name="show-the-state-of-the-passcode-reset"></a>Mostrar el estado del restablecimiento del código de acceso  

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** y elija el nodo **dispositivos** . También puede elegir **recopilaciones de dispositivos** y seleccionar una recopilación de la que el dispositivo es miembro.

1. Seleccione el dispositivo o los dispositivos en los que se va a mostrar el estado de restablecimiento de código de acceso.

1. En la cinta de opciones, en el grupo dispositivo, seleccione **acciones de dispositivo remoto**y, a continuación, elija **Mostrar estado de código**de acceso.  

## <a name="remote-lock"></a>Bloqueo remoto

Si un usuario pierde su dispositivo, es posible bloquearlo de forma remota. La tabla siguiente muestra el modo en que se puede usar el bloqueo remoto en distintas plataformas móviles.  

|Versión del SO|Bloqueo remoto|
|----------|-----------|
|Windows 10|No compatible|
|Windows Phone 8 y Windows Phone 8.1|Compatible|
|Windows RT 8.1|Compatible, si el usuario actual del dispositivo es el mismo usuario que inscribió el dispositivo.|
|Windows 8.1|Compatible, si el usuario actual del dispositivo es el mismo usuario que inscribió el dispositivo.|

> [!Note]
> Inicie la acción de bloqueo remoto desde el sitio de nivel superior. Por ejemplo, si usa un sitio de administración central, solo puede realizar la acción en ese sitio. Si utiliza un sitio primario independiente, realice la acción de ese sitio.

### <a name="remotely-lock-a-mobile-device"></a>Bloquear de forma remota un dispositivo móvil

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** y elija el nodo **dispositivos** . También puede elegir **recopilaciones de dispositivos** y seleccionar una recopilación de la que el dispositivo es miembro.

1. Seleccione el dispositivo o los dispositivos para bloquear.

1. En la cinta de opciones, en el grupo dispositivo, seleccione **acciones de dispositivo remoto**y, a continuación, elija **bloqueo remoto**. Confirme la acción.

### <a name="show-the-state-of-the-remote-lock"></a>Mostrar el estado del bloqueo remoto

1. En la consola de Configuration Manager, vaya al área de trabajo **activos y compatibilidad** y elija el nodo **dispositivos** . También puede elegir **recopilaciones de dispositivos** y seleccionar una recopilación de la que el dispositivo es miembro.

1. Seleccione el dispositivo en el que se va a mostrar el estado del bloqueo remoto.

1. En la cinta de opciones, en el grupo dispositivo, seleccione **acciones de dispositivo remoto**y, a continuación, seleccione **Mostrar estado de bloqueo remoto**.
