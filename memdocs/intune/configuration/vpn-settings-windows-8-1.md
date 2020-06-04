---
title: 'Configuración de VPN para dispositivos Windows 8.1 en Microsoft Intune: Azure | Microsoft Docs'
description: Agregue o cree un perfil de configuración de VPN con las opciones de configuración de red privada virtual (VPN), incluidos los detalles de conexión, la configuración de proxy con una dirección IP o FQDN y un puerto TCP en Microsoft Intune, en dispositivos que ejecutan Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556360"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Configuración de VPN para dispositivos Windows 8.1 en Microsoft Intune

En este artículo, se muestra la configuración de Intune que puede usar para configurar conexiones VPN en dispositivos que ejecutan Windows 8.1.

Según la configuración que elija, no todos los valores de la lista siguiente se podrán configurar.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de dispositivo VPN de Windows 8.1](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Configuración de VPN base

- **Nombre de la conexión**: escriba un nombre para esta conexión. Los usuarios ven este nombre cuando exploran su dispositivo para ver la lista de conexiones VPN disponibles. Por ejemplo, escriba `Contoso VPN`.
- **Servidores**: agregue uno o varios servidores VPN a los que se conectarán los dispositivos. Cuando se agrega un servidor, se escribe la siguiente información:
  - **Descripción**: escriba un nombre descriptivo para el servidor, por ejemplo, **Servidor VPN de Contoso**.
  - **Dirección IP o FQDN**: indique la dirección IP o el nombre de dominio completo (FQDN) del servidor VPN al que se van a conectar los dispositivos. Por ejemplo, escriba `192.168.1.1` o `vpn.contoso.com`.
  - **Servidor predeterminado**: **True** establece este servidor como el servidor predeterminado que los dispositivos van a usar para establecer la conexión. Establezca un solo servidor como predeterminado.
  - **Importar**: vaya a un archivo delimitado por comas con la lista de servidores en el formato siguiente: descripción, dirección IP o FQDN, servidor predeterminado. Elija **Aceptar** para importar estos servidores en la lista **Servidores**.
  - **Exportar**: exporta la lista de servidores a un archivo de valores separados por comas (csv).

- **Tipo de conexión**: seleccione el tipo de conexión VPN. Las opciones son:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Grupo o dominio de inicio de sesión** (solo SonicWall Mobile Connect): especifique el nombre del grupo o dominio de inicio de sesión al que quiera conectarse.

- **Rol** (solo Pulse Secure): especifique el nombre del rol de usuario que puede acceder a esta conexión. Un rol de usuario define la configuración personal y las opciones, y habilita o deshabilita ciertas características de acceso.

- **Dominio kerberos** (solo Pulse Secure): especifique el nombre de dominio de autenticación que quiera usar. Un dominio de autenticación es una agrupación de recursos de autenticación que usa el tipo de conexión Pulse Secure.

- **XML personalizado**: escriba cualquier comando XML personalizado que configure la conexión VPN.

  **Ejemplo de Pulse Secure**:

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **Ejemplo de CheckPoint Mobile VPN**:

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **Ejemplo de SonicWall Mobile Connect**:

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **Ejemplo de F5 Edge Client**:

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  Para obtener más información sobre la escritura de comandos XML personalizados, vea la documentación de la VPN del fabricante.

- **Tunelización dividida**: **Habilitar** permite que los dispositivos decidan qué conexión van a usar en función del tráfico. Por ejemplo, un usuario en un hotel usará la conexión VPN para acceder a los archivos de trabajo, pero usará la red normal del hotel para la exploración web habitual. Si quiere que todo el tráfico use el túnel de VPN cuando la conexión VPN está activa, establezca esta opción en **Deshabilitar**.

## <a name="proxy-settings"></a>Configuración del proxy

- **Script de configuración automática**: use un archivo para configurar el servidor proxy. Escriba la **URL del servidor proxy** que contiene el archivo de configuración. Por ejemplo, escriba `http://proxy.contoso.com`.
- **Dirección**: escriba la dirección del servidor proxy, por ejemplo, una dirección IP o `vpn.contoso.com`.
- **Número de puerto**: escriba el número de puerto TCP que el servidor proxy ha usado.
- **Detectar automáticamente configuración de proxy**: Si el servidor VPN requiere un servidor proxy para la conexión, elija si quiere que los dispositivos detecten automáticamente la configuración de la conexión. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Habilitar**: detecta automáticamente la configuración de la conexión.
  - **Deshabilitar**: no detecta automáticamente la configuración de la conexión.
- **Omitir proxy para direcciones locales**: decida si usar el servidor proxy con las direcciones locales. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Habilitar**: no se usa un servidor proxy con las direcciones locales.
  - **Deshabilitar**: se usa un servidor proxy con las direcciones locales.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

Configure las opciones de VPN en dispositivos [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md) y [Windows 10](vpn-settings-windows-10.md).
