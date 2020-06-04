---
title: Configuración de firewall para la seguridad de los puntos de conexión de Intune | Microsoft Docs
description: Configuración de la directiva de firewall para la seguridad de los puntos de conexión para Windows y macOS en Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: d90870a60ea292939926816bb74b5d285dc6a09f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431610"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Configuración de la directiva de firewall para la seguridad de los puntos de conexión en Intune

Vea los parámetros que se pueden configurar en los perfiles de la directiva de *firewall*, en el nodo seguridad de los puntos de conexión de Intune, como parte de una [directiva de seguridad para los puntos de conexión](../protect/endpoint-security-policy.md).

Perfiles y plataformas compatibles:

- **macOS**:
  - Perfil: **Firewall de macOS**

- **Windows 10 y versiones posteriores**:
  - Perfil: **Firewall de Microsoft Defender**

## <a name="macos-firewall-profile"></a>Perfil de firewall de macOS

### <a name="firewall"></a>Firewall

Los siguientes valores se configuran como [Directiva de seguridad para los puntos de conexión de firewall de macOS](../protect/endpoint-security-firewall-policy.md).

- **Habilitar firewall**

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: habilite el firewall.
  
  Si se establece en *Sí*, se pueden configurar estos valores.  

  - **Bloquear todas las conexiones entrantes**

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: bloquee todas las conexiones entrantes, excepto las necesarias para los servicios básicos de Internet, como DHCP, Bonjour e IPSec. Esta opción bloquea todos los servicios de uso compartido.

  - **Habilitar el modo sigiloso**

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: impida que el equipo responda a las solicitudes de sondeo. El equipo seguirá respondiendo a las solicitudes entrantes de las aplicaciones autorizadas.

  - **Aplicaciones de firewall**: expanda la lista desplegable y, después, seleccione **Agregar** para especificar las aplicaciones y las reglas para las conexiones entrantes de la aplicación.
    - **Permitir conexiones entrantes**
      - No configurado
      - Bloquear
      - Allow

    - **Id. de conjunto**: el id. identifica la aplicación. Por ejemplo, *com.apple.app*.

## <a name="microsoft-defender-firewall-profile"></a>Perfil de firewall de Microsoft Defender

### <a name="microsoft-defender-firewall"></a>Firewall de Microsoft Defender

Los siguientes valores se configuran como [Directiva de seguridad para los puntos de conexión de firewall de Windows 10](../protect/endpoint-security-firewall-policy.md).

- **Deshabilitación del Protocolo de transferencia de archivos con estado (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **No configurado** (*valor predeterminado*): el firewall usa FTP para inspeccionar y filtrar las conexiones de red secundarias, lo que puede provocar que se ignoren las reglas de firewall.
  - **Sí**
  
- **Número de segundos que una asociación de seguridad puede estar inactiva antes de eliminarla**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Especifique el tiempo (entre 300 y 3600 segundos) durante el que se conservarán las asociaciones de seguridad cuando ya no haya tráfico.
  
  Si no se especifica ningún valor, el sistema eliminará una asociación de seguridad después de que haya estado inactiva durante 300 segundos.
  
- **Codificación de clave previamente compartida**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  Si no se necesita *UTF-8*, las claves previamente compartidas se codificarán inicialmente con UTF-8. Después, los usuarios del dispositivo pueden elegir otro método de codificación.

  - **Sin configurar** (*valor predeterminado*).
  - **Ninguno**
  - **UTF8**

- **Las exenciones de IPsec del firewall permiten la detección de vecinos**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: las exenciones de IPsec del firewall permiten la detección de vecinos.

- **Las exenciones de IPsec del firewall permiten ICMP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: las exenciones de IPsec del firewall permiten ICMP.

- **Las exenciones de IPsec del firewall permiten la detección de enrutadores**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: las exenciones de IPsec del firewall permiten la detección de enrutadores.

- **Las exenciones de IPsec del firewall permiten DHCP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: las exenciones de IPsec del firewall permiten DHCP.

- **Comprobación de la lista de revocación de certificados (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Establece un valor para la forma de aplicar la comprobación de la lista de revocación de certificados (CRL).
  - **No configurado** (*valor predeterminado*): el valor predeterminado del cliente es deshabilitar la comprobación de CRL.
  - **Ninguno**
  - **Intento**
  - **Requerir**

- **Requerir que los módulos de generación de claves solo ignoren los conjuntos de autenticación que no admiten**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: los módulos de generación de claves ignoran los conjuntos de autenticación no admitidos.

- **Puesta de paquetes en cola**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Especifique cómo habilitar el escalado para el software en el lado de recepción para la recepción cifrada y el reenvío de texto no cifrado en un escenario de puerta de enlace de túnel de IPsec. Esto garantiza que se conserve el orden de los paquetes.
  - **No configurado** (*valor predeterminado*): la puesta de paquetes en cola volverá al valor predeterminado del cliente, que está deshabilitado.
  - **Deshabilitado**
  - **Poner en cola entrantes**
  - **Poner en cola salientes**
  - **Poner ambos en cola**

- **Activar el firewall de Microsoft Defender para redes de dominio**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **No configurado** (*valor predeterminado*): el cliente vuelve al valor predeterminado, que es habilitar el firewall.
  - **Sí**: el firewall de Microsoft Defender para el tipo de red de **dominio** está activado y aplicado.
  - **No**: deshabilite el firewall.

- **Activar el firewall de Microsoft Defender para redes privadas**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **No configurado** (*valor predeterminado*): el cliente vuelve al valor predeterminado, que es habilitar el firewall.
  - **Sí**: el firewall de Microsoft Defender para el tipo de red **privada** está activado y aplicado.
  - **No**: deshabilite el firewall.

- **Activar el firewall de Microsoft Defender para redes públicas**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **No configurado** (*valor predeterminado*): el cliente vuelve al valor predeterminado, que es habilitar el firewall.
  - **Sí**: el firewall de Microsoft Defender para el tipo de red **pública** está activado y aplicado.
  - **No**: deshabilite el firewall.

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Reglas de firewall de Microsoft Defender

*Este perfil está en versión preliminar*.

Los siguientes valores se configuran como [Directiva de seguridad para los puntos de conexión de firewall de Windows 10](../protect/endpoint-security-firewall-policy.md).

#### <a name="windows-firewall-rule"></a>Regla de firewall de Windows

- **Nombre**  
  Especifique un nombre descriptivo para la regla. Este nombre aparecerá en la lista de reglas para ayudarle a identificarla.

- **Descripción**  
  Proporcione una descripción de la regla.

- **Dirección**  
  - **No configurado** (*valor predeterminado*): esta regla tiene como valor predeterminado el tráfico saliente.
  - **Salida**: esta regla se aplica al tráfico saliente.
  - **Entrada**: esta regla se aplica al tráfico entrante.

- **Acción**  
  - **No configurado** (*valor predeterminado*): el valor predeterminado de la regla es permitir el tráfico.
  - **Bloqueado**: el tráfico está bloqueado en la *dirección* que se ha configurado.
  - **Permitido**: el tráfico está permitido en la *dirección* que se ha configurado.

- **Tipo de red**  
  Especifique el tipo de red al que pertenece la regla. Puede elegir varias de las opciones siguientes. Si no selecciona ninguna opción, la regla se aplicará a todos los tipos de red.
  - **Dominio**
  - **Privado**
  - **Público**
  - **No configurado**

- **Nombre de familia del paquete**  
  [Get-AppxPackage](https://docs.microsoft.com/previous-versions//hh856044(v=technet.10))

  Para recuperar los nombres de familia del paquete, ejecute el comando Get-AppxPackage de PowerShell.

- **Ruta de acceso de archivo**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)

  Para especificar la ruta de acceso de un archivo de una aplicación, escriba la ubicación de las aplicaciones en el dispositivo cliente. Por ejemplo, `C:\Windows\System\Notepad.exe` o `%WINDIR%\Notepad.exe`.

- **Nombre del servicio**  
  [FirewallRules/FirewallRuleName/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)

  Use un nombre corto de servicio de Windows cuando un servicio, no una aplicación, envía o recibe tráfico. Los nombres cortos de servicio se recuperan mediante la ejecución del comando `Get-Service` desde PowerShell.

- **Protocolo**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)

  Especifique el protocolo para esta regla de puerto.
  - Los protocolos de nivel de transporte como *TCP(6)* y *UDP(17)* permiten especificar puertos o intervalos de puertos.
  - En el caso de los protocolos personalizados, escriba un número, entre *0* y *255* que represente el protocolo IP.
  - Si no se especifica ningún valor, la regla tendrá como valor predeterminado **Cualquiera**.

- **Tipos de interfaz**  
  Especifique los tipos de interfaz a los que pertenece la regla. Puede elegir varias de las opciones siguientes. Si no selecciona ninguna opción, la regla se aplicará a todos los tipos de interfaz:
  - **Acceso remoto**
  - **Inalámbrica**
  - **Red de área local**
  - **No configurado**.

- **Usuarios autorizados**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Especifique una lista de usuarios locales autorizados para esta regla. No se puede especificar una lista de usuarios autorizados si en esta directiva se establece *Nombre del servicio* como un servicio de Windows. Si no se especifica ningún usuario autorizado, el valor predeterminado es *Todos los usuarios*.

- **Cualquier dirección local**  
  **No configurado** (*valor predeterminado*): use la configuración siguiente, *Intervalos de direcciones locales**, para configurar un intervalo de direcciones que se admitan.
  - **Sí**: admita cualquier dirección local y no configure ningún intervalo de direcciones.

- **Intervalos de direcciones locales**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Agregue una o más direcciones en una lista separada por comas de las direcciones locales que cubre la regla. Las entradas válidas (tokens) incluyen las opciones siguientes:
  - **Un asterisco**: este símbolo (\*) indica cualquier dirección local. Si está presente, el asterisco debe ser el único token incluido.
  - **Una subred**: especifique las subredes con la notación de máscara de subred o de prefijo de red. Si no se especifica ninguna máscara de subred ni ningún prefijo de red, el valor predeterminado de la máscara de subred será 255.255.255.255.
  - **Una dirección IPv6 válida**
  - **Un intervalo de direcciones IPv4**: los intervalos IPv4 deben estar en el formato *dirección inicial - dirección final* sin incluir espacios, donde la dirección inicial es menor que la final.
  - **Un intervalo de direcciones IPv6**: los intervalos IPv6 deben estar en el formato *dirección inicial - dirección final* sin incluir espacios, donde la dirección inicial es menor que la final.

  Si no se especifica ningún valor, se establecerá como valor predeterminado usar *Cualquier dirección*.

- **Cualquier dirección remota**  
  **No configurado** (*valor predeterminado*): use la configuración siguiente, *Intervalos de direcciones remotas**, para configurar un intervalo de direcciones que se admitan.
  - **Sí**: admita cualquier dirección remota y no configure ningún intervalo de direcciones.

- **Intervalos de direcciones remotas**  
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Agregue una o más direcciones en una lista separada por comas de las direcciones remotas que cubre la regla. Las entradas válidas (tokens) incluyen lo siguiente y no distinguen mayúsculas de minúsculas:
  - **Un asterisco**: este símbolo (\*) indica cualquier dirección remota. Si está presente, el asterisco debe ser el único token incluido.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet**: compatible con dispositivos que ejecuten Windows 1809 o una versión posterior.
  - **RmtIntranet**: compatible con dispositivos que ejecuten Windows 1809 o una versión posterior.
  - **Ply2Renders**: compatible con dispositivos que ejecuten Windows 1809 o una versión posterior.
  - **LocalSubnet**: indica cualquier dirección local en la subred local.
  - **Una subred**: especifique las subredes con la notación de máscara de subred o de prefijo de red. Si no se especifica ninguna máscara de subred ni ningún prefijo de red, el valor predeterminado de la máscara de subred será 255.255.255.255.
  - **Una dirección IPv6 válida**
  - **Un intervalo de direcciones IPv4**: los intervalos IPv4 deben estar en el formato *dirección inicial - dirección final* sin incluir espacios, donde la dirección inicial es menor que la final.
  - **Un intervalo de direcciones IPv6**: los intervalos IPv6 deben estar en el formato *dirección inicial - dirección final* sin incluir espacios, donde la dirección inicial es menor que la final.

  Si no se especifica ningún valor, se establecerá como valor predeterminado usar *Cualquier dirección*.

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>Pasos siguientes

[Directiva para la seguridad de los puntos de conexión para firewalls](../protect/endpoint-security-firewall-policy.md)
