---
title: Configuración de las líneas de base de seguridad de Intune para Advanced Threat Protection de Microsoft Defender
titleSuffix: Microsoft Intune
description: Configuración de la línea de base de seguridad compatible con Intune para administrar Advanced Threat Protection de Microsoft Defender
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: 8046318c55e2a9791f01fca4a5a54de3f1487782
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022199"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Configuración de la línea de base de Advanced Threat Protection de Microsoft Defender

Vea la configuración de línea de base de Advanced Threat Protection de Microsoft Defender compatible con Microsoft Intune. Los valores predeterminados de línea de base de Advanced Threat Protection (ATP) representan la configuración recomendada para ATP y podrían no coincidir con los valores predeterminados para otras líneas de base de seguridad.

::: zone pivot="atp-april-2020"

Los detalles de este artículo se aplican a la versión 4 de la línea de base de ATP de Microsoft Defender, publicada el 21 de abril de 2020. Para comprender lo que ha cambiado en esta versión de línea de base con respecto a las versiones anteriores, use la acción [Comparar líneas de base](../protect/security-baselines.md#compare-baseline-versions) que está disponible al ver el panel *Versiones* para esta línea de base.

::: zone-end
::: zone pivot="atp-march-2020"

Los detalles de este artículo se aplican a la versión 3 de la línea de base de ATP de Microsoft Defender, publicada el 1 de marzo de 2020. Para comprender lo que ha cambiado en esta versión de línea de base con respecto a las versiones anteriores, use la acción [Comparar líneas de base](../protect/security-baselines.md#compare-baseline-versions) que está disponible al ver el panel *Versiones* para esta línea de base.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


La línea base de [Advanced Threat Protection de Microsoft Defender](advanced-threat-protection.md#prerequisites) está disponible si el entorno cumple con los requisitos previos para su uso.

La línea de base se optimiza para dispositivos físicos y actualmente no se recomienda su uso en máquinas virtuales (VM) ni puntos de conexión de VDI. Ciertas configuraciones de base de referencia pueden afectar a las sesiones interactivas remotas en entornos virtualizados. Para obtener más información, vea [Aumento del cumplimiento de la base de referencia de seguridad de ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) en la documentación de Windows.


## <a name="application-guard"></a>Protección de aplicaciones

Para más información, vea [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) (CSP de WindowsDefenderApplicationGuard) en la documentación de Windows.  

Al utilizar Microsoft Edge, Protección de aplicaciones de Microsoft Defender protege su entorno de sitios que no son de confianza para su organización. Cuando los usuarios visitan sitios que no aparecen en el límite de red aislada, estos se abren en una sesión de exploración virtual de Hyper-V. Los sitios de confianza se definen mediante un límite de red.  

- **Activación de la Protección de aplicaciones para Microsoft Edge (opciones)**  
  CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Habilitado para Edge** (*valor predeterminado*): Protección de aplicaciones abre los sitios no aprobados en un contenedor de exploración virtualizado de Hyper-V.
  - **No configurado**: cualquier sitio (de confianza y no de confianza) se abre en el dispositivo, y no en un contenedor virtualizado.  
  
  Si se establece en *Habilitado para Edge*, se puede configurar *Bloquear contenido externo de sitios aprobados que no son de la empresa* y *Comportamiento del Portapapeles*.

  - **Bloquear contenido externo de sitios aprobados que no son de la empresa**  
    CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Sí** (*valor predeterminado*): impide que se cargue contenido de sitios web no aprobados.
    - **No configurado**: se pueden abrir sitios que no sean de empresa en el dispositivo.

  - **Comportamiento del Portapapeles**  
    CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Seleccione qué acciones de copiar y pegar se permiten entre el equipo local y el explorador virtual de la Protección de aplicaciones. Las opciones son:
    - **Not Configured** (No configurado)  
    - **Bloquear copiar y pegar entre el PC y el explorador** (*valor predeterminado*): se bloquean ambos. No se pueden transferir datos entre el equipo y el explorador virtual.
    - **Permitir copiar y pegar solo del explorador al PC**: no se pueden transferir datos del PC al explorador virtual.
    - **Permitir copiar y pegar solo del PC al explorador**: no se pueden transferir datos del explorador virtual al PC host.
    - **Permitir copiar y pegar entre el PC y el explorador**: no existen bloqueos del contenido.

- **Directiva de aislamiento de red de Windows**  
  CSP: [CSP de directiva: NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation)

  Especifique una lista de *Dominios de red*, que son recursos de empresa hospedados en la nube que Protección de aplicaciones trata como sitios empresariales.
  - **Configurar** (*valor predeterminado*)
  - **No configurado**.

  Si se establece en *Configurar*, puede definirse *Dominios de red*.

  - **Dominios de red**  
    Seleccione **Agregar** y especifique los dominios, los intervalos de direcciones IP y los límites de red. *securitycenter.windows.com* está configurada de manera predeterminada.

## <a name="bitlocker"></a>BitLocker

Para más información, vea [Configuración de las directivas de grupo de BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) en la documentación de Windows.

- **Exigir cifrado de tarjeta de almacenamiento (solo dispositivos móviles)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Esta opción solo se aplica a dispositivos de SKU de Windows Mobile y Mobile Enterprise.
  - **Sí** (*valor predeterminado*): se requiere cifrado en tarjetas de almacenamiento para dispositivos móviles.
  - **No configurado**: está opción vuelve al valor predeterminado del sistema operativo, que no requiere cifrado de tarjeta de almacenamiento.

- **Habilitar el cifrado de disco completo para las unidades de datos fijas y de sistema operativo**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Si la unidad se cifró antes de aplicar esta directiva, no se realiza ninguna acción adicional. Si el método y las opciones de cifrado coinciden con los de esta directiva, la configuración debe devolver un valor correcto. Si una opción de configuración de BitLocker en contexto no coincide con esta directiva, es probable que la configuración devuelva un error.
  
  Para aplicar esta directiva a un disco ya cifrado, descifre la unidad y vuelva a aplicar la directiva MDM. El valor predeterminado de Windows es no requerir cifrado de unidad BitLocker, aunque es posible que el cifrado automático de registro/inicio de sesión en Unión a Azure AD y la cuenta de Microsoft (MSA) apliquen la habilitación de BitLocker en el cifrado XTS-AES de 128 bits.

  - **Sí** (*valor predeterminado*): se aplica el uso de BitLocker.
  - **No configurado**: no se produce la aplicación de BitLocker.

- **Directiva de unidad del sistema de BitLocker**  
  [Configuración de directiva de grupo de BitLocker](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configurar** (*valor predeterminado*)
  - **No configurado**.

  Si se establece en *Configurar*, se puede configurar *Cifrado para unidades del sistema operativo*.

  - **Cifrado para unidades del sistema operativo**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Esta opción está disponible cuando *Directiva de unidad del sistema de BitLocker* se establece en *Configurar*.  

    Configure el método de cifrado y la intensidad de cifrado para las unidades del sistema.  *XTS-AES de 128 bits* es el método de cifrado predeterminado de Windows y el valor recomendado.

    - **Sin configurar** (*valor predeterminado*).
    - **CBC-AES de 128 bits**
    - **AES-CBC de 256 bits**
    - **XTS-AES de 128 bits**
    - **AES-XTS de 256 bits**

- **Directiva de unidad fija de BitLocker**  
  [Configuración de directiva de grupo de BitLocker](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Configurar** (*valor predeterminado*)
  - **No configurado**.

  Si se establece en *Configurar*, se puede configurar *Denegar acceso de escritura a unidad de datos fija no protegida con BitLocker* y *Cifrado para unidades de datos fijas*.

  - **Denegar acceso de escritura a unidad de datos fija no protegida con BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Esta opción está disponible cuando *Directiva de unidades fijas de BitLocker* se establece en *Configurar*.

    - **No configurado** (*valor predeterminado*): pueden escribirse datos en unidades fijas no cifradas.
    - **Sí**: Windows no permitirá que se escriban datos en unidades fijas que no estén protegidas con BitLocker. Si no se cifra una unidad fija, el usuario ha de completar el Asistente para la instalación de BitLocker para la unidad antes de que se conceda acceso de escritura.

  - **Cifrado para unidades de datos fijas**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Esta opción está disponible cuando *Directiva de unidades fijas de BitLocker* se establece en *Configurar*.

    Configure el método de cifrado y la intensidad de cifrado para los discos de unidades de datos fijas. *XTS-AES de 128 bits* es el método de cifrado predeterminado de Windows y el valor recomendado.

    - **Sin configurar** (*valor predeterminado*).
    - **CBC-AES de 128 bits**
    - **AES-CBC de 256 bits**
    - **XTS-AES de 128 bits**
    - **AES-XTS de 256 bits**

- **Directiva de unidad extraíble de BitLocker**  
  [Configuración de directiva de grupo de BitLocker](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Configurar** (*valor predeterminado*)
  - **No configurado**.

  Si se establece en *Configurar*, se puede configurar *Cifrado para unidades de datos extraíbles* y *Denegar acceso de escritura a discos de datos extraíbles no protegidos con BitLocker*.

  - **Cifrado para unidades de datos extraíbles**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Esta opción está disponible cuando *Directiva de unidades extraíbles de BitLocker* se establece en *Configurar*.

    Configure el método de cifrado y la intensidad de cifrado para los discos de unidades de datos extraíbles. *XTS-AES de 128 bits* es el método de cifrado predeterminado de Windows y el valor recomendado.

    - **No configurado**.
    - **CBC-AES de 128 bits**
    - **AES-CBC de 256 bits** (*valor predeterminado*)
    - **XTS-AES de 128 bits**
    - **AES-XTS de 256 bits**

  - **Denegar acceso de escritura a discos de datos extraíbles no protegidos con BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    Esta opción está disponible cuando *Directiva de unidades extraíbles de BitLocker* se establece en *Configurar*.

    - **No configurado** (*valor predeterminado*): pueden escribirse datos en unidades extraíbles no cifradas.  
    - **Sí**: Windows no permitirá que se escriban datos en unidades extraíbles que no estén protegidas por BitLocker. Si no se cifra una unidad extraíble, el usuario ha de completar el Asistente para la instalación de BitLocker para la unidad antes de que se conceda acceso de escritura.

## <a name="browser"></a>Explorador

- **Require SmartScreen for Microsoft Edge** (Requerir SmartScreen para Microsoft Edge)  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Sí** (*valor predeterminado*): se usa SmartScreen para proteger a los usuarios frente a posibles correos de suplantación de identidad (phishing) y software malintencionado.
  - **No configurado**.

- **Block malicious site access** (Bloquear el acceso a sitios malintencionados)  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Sí** (*valor predeterminado*): impide que los usuarios omitan las advertencias del filtro SmartScreen de Microsoft Defender y no les permite que vayan al sitio.
  - **No configurado**.

- **Block unverified file download** (Bloquear la descarga de archivos no comprobados)  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Sí** (*valor predeterminado*): impide que los usuarios omitan las advertencias del filtro SmartScreen de Microsoft Defender y no les permite que descarguen archivos no comprobados.
  - **No configurado**.

## <a name="data-protection"></a>Protección de datos

- **Block direct memory access** (Bloquear el acceso directo a memoria)  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  Esta configuración de directiva solo se aplica cuando está habilitado BitLocker o el cifrado de dispositivos.

  - **Sí** (*valor predeterminado*): impide el acceso directo a memoria (DMA) a todos los puertos de bajada PCI de conexión instantánea hasta que un usuario inicie sesión en Windows. Cuando un usuario inicie sesión, Windows mostrará los dispositivos PCI conectados a los puertos PCI de conexión de host. Cada vez que el usuario bloquee el equipo, DMA se bloquea en los puertos PCI de conexión instantánea sin dispositivos secundarios, hasta que el usuario inicie sesión de nuevo. Los dispositivos que ya aparecían cuando se desbloqueó el equipo seguirán funcionando hasta que se desconecten.
  - **No configurado**.

## <a name="device-guard"></a>Device Guard  

- **Activar Credential Guard**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard usa el hipervisor de Windows para proporcionar protecciones, lo que requiere un arranque seguro y protecciones DMA que funcionen, para lo que es necesario que se cumplan los requisitos de hardware.

  - **No configurado**: deshabilita el uso de Credential Guard, que es el valor predeterminado de Windows.
  - **Habilitar con bloqueo UEFI** (*valor predeterminado*): habilita Credential Guard y no permite que se deshabilite de forma remota, ya que la configuración persistente de UEFI debe borrarse manualmente.
  - **Habilitar sin bloqueo UEFI**: habilitar Credential Guard y permitir que se apague sin acceso físico a la máquina.

## <a name="device-installation"></a>Instalación de dispositivos

- **Hardware device installation by device identifiers** (Instalación de dispositivos de hardware mediante identificadores de dispositivo)  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Esta configuración de directiva le permite especificar una lista de identificadores de hardware Plug and Play e identificadores compatibles para dispositivos que Windows no puede instalar. Esta configuración de directiva tiene prioridad sobre cualquier otra configuración de directiva que permita a Windows instalar dispositivos.  Si habilita esta configuración de directiva en un servidor de escritorio remoto, esta afectará a la redirección de los dispositivos especificados desde un cliente de escritorio remoto al servidor de escritorio remoto.

  - **No configurado**.
  - **Permitir la instalación del dispositivo de hardware**: se podrán instalar o actualizar dispositivos según lo que permitan o impidan otras configuraciones de directiva.
  - **Bloquear la instalación de dispositivos de hardware** (*valor predeterminado*): Windows no podrá instalar un dispositivo cuyo identificador de hardware o identificador compatible aparezca en una lista que se define.

  Si se establece en *Bloquear la instalación de dispositivos de hardware*, puede configurar *Quitar los dispositivos de hardware coincidentes* y *Identificadores de dispositivos de hardware que están bloqueados*.

  - **Remove matching hardware devices** (Quitar dispositivos de hardware que coinciden)

    Esta opción solo está disponible cuando *Hardware device installation by device identifiers* (Instalación de dispositivos de hardware mediante identificadores de dispositivo) se establece en *Bloquear la instalación de dispositivos de hardware*.
    - **Sí**
    - **No configurado**.

  - **Hardware device identifiers that are blocked** (Identificadores de dispositivo de hardware que están bloqueados)  
    
    Esta opción solo está disponible cuando *Hardware device installation by device identifiers* (Instalación de dispositivos de hardware mediante identificadores de dispositivo) se establece en *Bloquear la instalación de dispositivos de hardware*.

    Seleccione **Agregar** y especifique el identificador de dispositivo de hardware que quiere bloquear.

- **Hardware device installation by setup classes** (Instalación de dispositivos de hardware mediante clases de instalación)  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Esta configuración de directiva permite especificar una lista de identificadores únicos globales (GUID) de clases de instalación de dispositivos para los controladores de dispositivos que no se pueden instalar en Windows. Esta configuración de directiva tiene prioridad sobre cualquier otra configuración de directiva que permita a Windows instalar dispositivos. Si habilita esta configuración de directiva en un servidor de escritorio remoto, esta afectará a la redirección de los dispositivos especificados desde un cliente de escritorio remoto al servidor de escritorio remoto.

  - **No configurado**.
  - **Permitir la instalación del dispositivo de hardware**: Windows puede instalar o actualizar dispositivos según lo permitan o impidan otras configuraciones de directiva.
  - **Bloquear la instalación de dispositivos de hardware** (*valor predeterminado*): Windows no podrá instalar un dispositivo cuyos GUID de clase de instalación aparezcan en una lista que se define.

  Si se establece en *Bloquear la instalación de dispositivos de hardware*, puede configurar *Quitar los dispositivos de hardware coincidentes* y *Identificadores de dispositivos de hardware que están bloqueados*.

  - **Remove matching hardware devices** (Quitar dispositivos de hardware que coinciden)

    Esta opción solo está disponible cuando *Hardware device installation by device identifiers* (Instalación de dispositivos de hardware mediante identificadores de dispositivo) se establece en *Bloquear la instalación de dispositivos de hardware*.
    - **Sí**
    - **No configurado**.

  - **Hardware device identifiers that are blocked** (Identificadores de dispositivo de hardware que están bloqueados)

    Esta opción solo está disponible cuando *Hardware device installation by device identifiers* (Instalación de dispositivos de hardware mediante identificadores de dispositivo) se establece en *Bloquear la instalación de dispositivos de hardware*.

    Seleccione **Agregar** y especifique el identificador de dispositivo de hardware que quiere bloquear.

## <a name="dma-guard"></a>Protección de DMA

- **Enumeración de los dispositivos externos compatibles con Kernel DMA Protection**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Esta directiva puede proporcionar seguridad adicional contra los dispositivos compatibles con DMA externos. Permite mayor control sobre la enumeración de dispositivos externos compatibles con DMA incompatibles con la reasignación de DMA o el aislamiento de la memoria de dispositivo y el espacio aislado.
  
  Esta directiva solo surte efecto cuando la característica Kernel DMA Protection se admite y está habilitada por el firmware del sistema. Kernel DMA Protection es una característica de plataforma que debe ser compatible con el sistema en el momento de la fabricación. Para comprobar si el sistema admite Kernel DMA Protection, revise el campo Kernel DMA Protection en la página de resumen de MSINFO32.exe.

  - **No configurado**: (*valor predeterminado*)
  - **Bloquear todo**
  - **Permitir todo**

## <a name="endpoint-detection-and-response"></a>Endpoint Detection and Response

Para más información sobre la siguiente configuración, consulte [WindowsAdvancedThreatProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) en la documentación de Windows.

- **Uso compartido de muestras para todos los archivos**  
  CSP: [Configuration/SampleSharing](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Devuelve o establece el parámetro de configuración de uso compartido de muestras de Advanced Threat Protection de Microsoft Defender.  
  
  - **Sí** (*valor predeterminado*)
  - **No configurado**.

- **Frecuencia de informes de telemetría urgentes**  
  CSP: [Configuration/TelemetryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Frecuencia de informes de telemetría de Advanced Threat Protection de Microsoft Defender urgentes.  

  - **Sí** (*valor predeterminado*)
  - **No configurado**.

## <a name="firewall"></a>Firewall

Para más información, vea [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP de Firewall) en la documentación de Windows.

- **Deshabilitación del Protocolo de transferencia de archivos con estado (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Sí** (*valor predeterminado*)
  - **No configurado**: el firewall usará FTP para inspeccionar y filtrar las conexiones de red secundarias, lo que puede provocar que se ignoren las reglas de firewall.

- **Número de segundos que una asociación de seguridad puede estar inactiva antes de eliminarla**  
CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Especifique durante cuánto tiempo se conservarán las asociaciones de seguridad cuando ya no se vea el tráfico de red. Si no se configura, el sistema elimina una asociación de seguridad después de que haya estado inactiva durante *300* segundos (el valor predeterminado).
  
  El número debe estar comprendido entre **300** y **3600** segundos.

- **Codificación de clave previamente compartida**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   Si no necesita UTF-8, las claves previamente compartidas se codificarán inicialmente con UTF-8. Después, los usuarios del dispositivo pueden elegir otro método de codificación.

  - **No configurado**.
  - **Ninguno**
  - **UTF8** (*valor predeterminado*)

- **Comprobación de la lista de revocación de certificados (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Establece un valor para la forma de aplicar la comprobación de la lista de revocación de certificados (CRL).  

  - **No configurado** (*valor predeterminado*): se deshabilita la comprobación de CRL.
  - **Ninguno**
  - **Intento**
  - **Requerir**

- **Puesta de paquetes en cola**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Especifique cómo se habilita el escalado para el software en el lado de recepción para la recepción cifrada y el reenvío no cifrado para un escenario de puerta de enlace de túnel de IPsec. Esta opción garantiza que se conserve el orden de los paquetes.

  - **No configurado** (*valor predeterminado*): la puesta de paquetes en cola vuelve al valor predeterminado del cliente, que está deshabilitado.
  - **Deshabilitado**
  - **Poner en cola entrantes**
  - **Poner en cola salientes**
  - **Poner ambos en cola**

- **Perfil privado del firewall**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Configurar** (*valor predeterminado*)
  - **No configurado**.

  Si se establece en *Configurar*, puede configurar las siguientes opciones adicionales.

  - **Inbound connections blocked** (Conexiones entrantes bloqueadas)  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Unicast responses to multicast broadcasts required** (Respuestas de unidifusión a tráfico de difusión o multidifusión requeridas)  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Stealth mode required** (Modo sigiloso requerido)  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Outbound connections required** (Conexiones salientes requeridas)  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Inbound notifications blocked** (Notificaciones entrantes bloqueadas)  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Global port rules from group policy merged** (Reglas de puerto globales de la directiva de grupo combinadas)  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Stealth mode blocked** (Modo sigiloso bloqueado)  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Firewall habilitado**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **No configurado**.
    - **Bloqueado**
    - **Permitido** (*valor predeterminado*)

  - **Authorized application rules from group policy not merged** (Reglas de aplicación autorizadas de la directiva de grupo no combinadas)  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Connection security rules from group policy not merged** (Reglas de seguridad de conexión de la directiva de grupo no combinadas)  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Incoming traffic required** (Tráfico entrante requerido)  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Policy rules from group policy not merged** (Reglas de directiva de la directiva de grupo no combinadas)  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

- **Perfil público del firewall**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Configurar** (*valor predeterminado*)
  - **No configurado**.

  Si se establece en *Configurar*, puede configurar las siguientes opciones adicionales.

  - **Inbound connections blocked** (Conexiones entrantes bloqueadas)  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Unicast responses to multicast broadcasts required** (Respuestas de unidifusión a tráfico de difusión o multidifusión requeridas)  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Stealth mode required** (Modo sigiloso requerido)  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Outbound connections required** (Conexiones salientes requeridas)  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Authorized application rules from group policy not merged** (Reglas de aplicación autorizadas de la directiva de grupo no combinadas)  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Inbound notifications blocked** (Notificaciones entrantes bloqueadas)  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Global port rules from group policy merged** (Reglas de puerto globales de la directiva de grupo combinadas)  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Stealth mode blocked** (Modo sigiloso bloqueado)  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Firewall habilitado**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **No configurado**.
    - **Bloqueado**
    - **Permitido** (*valor predeterminado*)

  - **Connection security rules from group policy not merged** (Reglas de seguridad de conexión de la directiva de grupo no combinadas)  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Incoming traffic required** (Tráfico entrante requerido)  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Policy rules from group policy not merged** (Reglas de directiva de la directiva de grupo no combinadas)  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

- **Dominio de Perfil del firewall**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Unicast responses to multicast broadcasts required** (Respuestas de unidifusión a tráfico de difusión o multidifusión requeridas)  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Authorized application rules from group policy not merged** (Reglas de aplicación autorizadas de la directiva de grupo no combinadas)  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.  

  - **Inbound notifications blocked** (Notificaciones entrantes bloqueadas)  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Global port rules from group policy merged** (Reglas de puerto globales de la directiva de grupo combinadas)  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Stealth mode blocked** (Modo sigiloso bloqueado)  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Firewall habilitado**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **No configurado**.
    - **Bloqueado**
    - **Permitido** (*valor predeterminado*)

  - **Connection security rules from group policy not merged** (Reglas de seguridad de conexión de la directiva de grupo no combinadas)  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

  - **Policy rules from group policy not merged** (Reglas de directiva de la directiva de grupo no combinadas)  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Sí** (*valor predeterminado*)
    - **No configurado**.

## <a name="microsoft-defender"></a>Microsoft Defender

- **Ejecutar un análisis rápido diario a las**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Configure cuándo se ejecuta el examen rápido diario. De forma predeterminada, la ejecución del examen está establecida para realizarse a las **2:00**.

- **Hora de inicio del examen programada**  
  
  De forma predeterminada, está establecida para realizarse a las **2:00**.

- **Configurar la prioridad baja de CPU para los exámenes programados**  
  CSP: [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Sí** (*valor predeterminado*)
  - **No configurado**.

- **Impedir que las aplicaciones de comunicación de Office creen procesos secundarios**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874499)  

  Esta regla de ASR se controla a través del siguiente GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **No configurado**: se restaura el valor predeterminado de Windows, que es no bloquear la creación de procesos secundarios.
  - **Definido por el usuario**
  - **Habilitar** (*valor predeterminado*): impide que las aplicaciones de comunicación de Office creen procesos secundarios.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquear los procesos secundarios.

- **Impedir que Adobe Reader cree procesos secundarios**  
  [Reducir las superficies de ataque con reglas de reducción de la superficie expuesta a ataques](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **No configurado**: se restaura el valor predeterminado de Windows, que es no bloquear la creación de procesos secundarios.
  - **Definido por el usuario**
  - **Habilitar** (*valor predeterminado*): impide que Adobe Reader cree procesos secundarios.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquear los procesos secundarios.

- **Examinar mensajes de correo entrante**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Sí** (*valor predeterminado*): se analizan los archivos de correo y buzón del correo electrónico tales como PST, DBX, MNX, MIME y BINHEX.
  - **No configurado**: la opción vuelve al valor predeterminado del cliente de archivos de correo electrónico que no se examinan.

- **Activar la protección en tiempo real**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Sí** (*valor predeterminado*): se aplica la supervisión en tiempo real y el usuario no puede deshabilitarla.
  - **No configurado**: la opción vuelve al valor predeterminado del cliente, que es activado, pero el usuario puede cambiarlo. Para deshabilitar la supervisión en tiempo real, use un URI personalizado.

- **Número de días (0-90) para mantener el malware en cuarentena**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Configure el número de días que se deben conservar los elementos en la carpeta de cuarentena antes de eliminarse. El valor predeterminado es cero (**0**), lo que hace que los archivos en cuarentena no se quiten nunca.

- **Programación de exámenes de sistema de Defender**  
  CSP: [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Programe el día en que Defender examina los dispositivos. De forma predeterminada, el examen está **definido por el usuario**, pero se puede establecer en *Todos los días*, cualquier día de la semana o *No hay ningún examen programado*.

- **Cantidad de tiempo adicional (0-50 segundos) para ampliar el tiempo de espera de protección en la nube**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  El antivirus de Defender bloquea automáticamente los archivos sospechosos durante 10 segundos, de manera que puede examinarlos en la nube para asegurarse de que son seguros. Con esta opción, puede agregar hasta 50 segundos adicionales a este tiempo de espera.  De forma predeterminada, el tiempo de espera se establece en cero (**0**).

- **Examinar unidades de red asignadas durante un examen completo**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Sí** (*valor predeterminado*): durante un examen completo, se incluyen las unidades de red asignadas.
  - **No configurado**: el cliente vuelve a su valor predeterminado, que deshabilita el examen en unidades de red asignadas.

- **Activar la protección de red**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Sí** (*valor predeterminado*): bloquea el tráfico malintencionado detectado por las firmas del Sistema de inspección de red (NIS).
  - **No configurado**.

- **Examinar todos los archivos y datos adjuntos descargados**  
  CSP: [Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Sí** (*valor predeterminado*): se examinan todos los archivos y datos adjuntos descargados. La opción vuelve al valor predeterminado del cliente, que es activado, pero el usuario puede cambiarlo. Para deshabilitar esta opción, use un URI personalizado.
  - **No configurado**: la opción vuelve al valor predeterminado del cliente, que es activado, pero el usuario puede cambiarlo. Para deshabilitar esta opción, use un URI personalizado.

::: zone-end
::: zone pivot="atp-april-2020"

- **Bloquear la protección de acceso**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Sí**
  - **Sin configurar** (*valor predeterminado*).

::: zone-end
::: zone pivot="atp-march-2020"

- **Bloquear la protección de acceso**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Sí** (*valor predeterminado*)
  - **No configurado**.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Examinar los scripts del explorador**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Sí** (*valor predeterminado*): se aplica la funcionalidad de examen de scripts de Microsoft Defender y el usuario no puede desactivarla.
  - **No configurado**: la opción vuelve al valor predeterminado del cliente, que es habilitar el examen de scripts, pero el usuario puede desactivarlo.

- **Bloquear el acceso de usuarios a la aplicación de Microsoft Defender**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **No** (*valor predeterminado*): no se puede acceder a la interfaz de usuario de Defender y se suprimen las notificaciones.
  - **No configurado**: si se establece en Sí, no se podrá acceder a la interfaz de usuario de Windows Defender y se suprimirán las notificaciones. Si se establece en No configurado, la opción vuelve al valor predeterminado del cliente en el que se permiten la interfaz de usuario y las notificaciones.

- **Uso de CPU máximo permitido (0-100 por ciento) por examen**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Especifique como porcentaje la cantidad máxima de CPU que se va a usar para un examen. El valor predeterminado es **50**.

- **Tipo de examen**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Definido por el usuario**
  - **Deshabilitado**
  - **Examen rápido** (*valor predeterminado*)
  - **Examen completo**

- **Escriba la frecuencia (0-24 horas) para comprobar las actualizaciones de inteligencia de seguridad**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Especifique la frecuencia de comprobación de firmas actualizadas, en horas. Por ejemplo, un valor de 1 realizará la comprobación cada hora. Un valor de 2 comprobará cada dos horas, etc.

  Si no se define ningún valor, los dispositivos usan el valor predeterminado del cliente de **8** horas.

- **Consentimiento de envío de muestra de Microsoft Defender**  
  CSP: [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Comprueba el nivel de consentimiento del usuario en Microsoft Defender para enviar datos. Si ya se ha concedido el consentimiento requerido, Microsoft Defender los envía. En caso contrario (y si el usuario ha especificado que no se pida nunca) se inicia la interfaz de usuario para solicitar el consentimiento del usuario (cuando *Protección que proporciona la nube* está configurado en *Sí*) antes de enviar los datos.

  - **Enviar muestras seguras automáticamente** (*valor predeterminado*)
  - **Preguntar siempre**
  - **No enviar nunca**
  - **Enviar todas las muestras automáticamente**

- **Nivel de protección que proporciona la nube**  
  CSP: [CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Configure el modo en que el antivirus de Defender bloquea y examina archivos sospechosos.
  - **No configurado** (*opción predeterminada*): nivel de bloqueo de Defender predeterminado.
  - **Alto**: bloquea de forma agresiva los archivos desconocidos mientras efectúa una optimización del rendimiento, lo que incluye una mayor posibilidad de falsos positivos.
  - **Más elevado**: bloquea de forma agresiva los archivos desconocidos y aplica medidas de protección adicionales, lo cual podría afectar al rendimiento del cliente.
  - **Tolerancia cero**: bloquea todos los archivos ejecutables desconocidos.

- **Examinar archivos de almacenamiento**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Sí** (*valor predeterminado*): se aplica el análisis de archivos de almacenamiento tales como archivos ZIP o CAB.
  - **No configurado**: la opción vuelve al valor predeterminado del cliente, que es examinar los archivos archivados, aunque el usuario puede deshabilitar el examen.

- **Activar la supervisión de comportamiento**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Sí** (*valor predeterminado*): se aplica la supervisión del comportamiento y el usuario no puede deshabilitarla.
  - **No configurado**: la opción vuelve al valor predeterminado del cliente, que es activado, pero el usuario puede cambiarlo. Para deshabilitar la supervisión en tiempo real, use un URI personalizado.
  
- **Examinar unidades extraíbles durante examen completo**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Sí** (*valor predeterminado*): durante un examen completo, se analizan las unidades extraíbles (como las unidades flash USB).
  - **No configurado**: la opción vuelve al valor predeterminado del cliente, que examina las unidades extraíbles, pero el usuario puede deshabilitar este examen.
  
- **Examinar archivos de red**  
  CSP: [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Sí** (*valor predeterminado*): Microsoft Defender examina los archivos de red.
  - **No configurado**: el cliente vuelve a su valor predeterminado, que deshabilita el examen de los archivos de red.
  
- **Defender potentially unwanted app action** (Acción frente a aplicaciones potencialmente no deseadas de Windows Defender)  
  CSP: [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Especifique el nivel de detección de aplicaciones potencialmente no deseadas (PUA). Defender alerta a los usuarios cuando se está descargando o intentando instalar software potencialmente no deseado en un dispositivo.
  - **Valor predeterminado de dispositivo**
  - **Bloquear** (*valor predeterminado*): los elementos detectados se bloquean y se muestran en el historial junto con otras amenazas.
  - **Auditar**: Microsoft Defender detecta aplicaciones potencialmente no deseadas, pero no toma ninguna medida. Puede revisar la información sobre las aplicaciones para las que Defender habría tomado medidas buscando eventos creados por Defender en el Visor de eventos.

- **Activar la protección que proporciona la nube**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  De forma predeterminada, Defender en dispositivos de escritorio de Windows 10 envía información a Microsoft sobre los problemas que encuentre. Microsoft analiza esa información para obtener detalles sobre los problemas que le afectan a usted y a otros clientes a fin de ofrecer soluciones mejoradas.

  - **Sí** (*valor predeterminado*): la protección que proporciona la nube está activa.  Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **No configurado**: la opción se restaura al valor predeterminado del sistema.

- **Impedir que las aplicaciones de Office inserten código en otros procesos**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872974)

  Esta regla de ASR se controla a través del siguiente GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear** (*valor predeterminado*): impide que las aplicaciones de Office inserten código en otros procesos.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Impedir que las aplicaciones de Office creen contenido ejecutable**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872975)

  Esta regla de ASR se controla a través del siguiente GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear** (*valor predeterminado*): impide que las aplicaciones de Office creen contenido ejecutable.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.
  
- **Impedir que JavaScript o VBScript inicien el contenido ejecutable descargado**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872979)

   Esta regla de ASR se controla a través del siguiente GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear** (*valor predeterminado*): Defender impide que se ejecuten los archivos JavaScript o VBScript que se han descargado de Internet.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.
  
- **Habilitar la protección de red**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que está deshabilitado.
  - **Definido por el usuario**
  - **Habilitar**: la protección de red está habilitada para todos los usuarios del sistema.
  - **Modo de auditoría** (*valor predeterminado*): no se bloquean los usuarios de dominios peligrosos y se generan eventos de Windows en su lugar.

- **Bloquear la ejecución desde USB de procesos que no sean de confianza y estén sin firmar**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874502)

  Esta regla de ASR se controla a través del siguiente GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear** (*valor predeterminado*): impide que los procesos que no sean de confianza y estén sin firmar se ejecuten en una unidad USB.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Marcar el robo de credenciales desde el subsistema de autoridad de seguridad local de Windows (lsass.exe)**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874499)

  Esta regla de ASR se controla a través del siguiente GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que está desactivado.
  - **Definido por el usuario**
  - **Habilitar** (*valor predeterminado*): se bloquean los intentos de robo de credenciales a través de lsass.exe.
  - **Modo de auditoría**: no se bloquean los usuarios de dominios peligrosos y se generan eventos de Windows en su lugar.

- **Bloquear contenido ejecutable del cliente de correo electrónico y el correo web**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872980)

  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear** (*valor predeterminado*): se bloquea el contenido ejecutable descargado desde clientes de correo electrónico y correo electrónico basado en web.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Impedir que todas las aplicaciones de Office creen procesos secundarios**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872976)

  Esta regla de ASR se controla a través del siguiente GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear** (*valor predeterminado*)
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Bloquear la ejecución de scripts potencialmente alterados (js/vbs/ps)**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872978)

  Esta regla de ASR se controla a través del siguiente GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear** (*valor predeterminado*): Defender impedirá la ejecución de scripts alterados.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Impedir llamadas API de Win32 desde macros de Office**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872977)

  Esta regla de ASR se controla a través del siguiente GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **No configurado**: la opción vuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear** (*valor predeterminado*): impide que las macros de Office usen llamadas API de Win32.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

## <a name="microsoft-defender-security-center"></a>Centro de seguridad de Microsoft Defender

- **Bloquear a los usuarios para que no editen la interfaz de Protección contra vulnerabilidades de seguridad**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Sí** (*valor predeterminado*): impide que los usuarios realicen cambios en el área de configuración de protección contra vulnerabilidades del Centro de seguridad de Microsoft Defender.
  - **No configurado**: los usuarios locales pueden realizar cambios en el área de configuración de Protección contra vulnerabilidades.

## <a name="smart-screen"></a>SmartScreen

- **Impedir que los usuarios descarten advertencias de SmartScreen**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Esta configuración requiere que la opción "Activar Windows SmartScreen" esté establecida en "Sí".
  - **Sí** (*predeterminado*): SmartScreen está habilitado y los usuarios no pueden ignorar las advertencias sobre archivos o aplicaciones malintencionados.
  - **No configurado**: los usuarios pueden ignorar las advertencias de SmartScreen sobre archivos y aplicaciones malintencionados.

- **Requerir solo aplicaciones de la tienda**  

  - **Sí** (*valor predeterminado*)
  - **No configurado**.

- **Activar Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Sí** (*valor predeterminado*): se aplica el uso de SmartScreen para todos los usuarios.
  - **No configurado**: devuelve la opción al valor predeterminado de Windows, que es habilitar SmartScreen, pero los usuarios pueden cambiar este valor. Para deshabilitar SmartScreen, use un URI personalizado.

## <a name="windows-hello-for-business"></a>Windows Hello para empresas

Para más información, vea [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) (CSP de PassportForWork) en la documentación de Windows.

- **Bloquear Windows Hello para empresas**  

   Windows Hello para empresas es un método alternativo para iniciar sesión en dispositivos Windows mediante la sustitución de contraseñas, tarjetas inteligentes y tarjetas inteligentes virtuales.

  - **No configurado**: los dispositivos aprovisionan Windows Hello para empresas, que es el valor predeterminado de Windows.
  - **Deshabilitado** (*valor predeterminado*): los dispositivos aprovisionan Windows Hello para empresas.
  - **Habilitado**: los dispositivos no aprovisionan Windows Hello para empresas para ningún usuario.

  Si se establece en *Deshabilitar*, se pueden configurar las siguientes opciones:

  - **Letras minúsculas en el PIN**  
    - **No permitido**
    - **Requerido**
    - **Permitido** (*valor predeterminado*)

  - **Caracteres especiales en el PIN**
    - **No permitido**
    - **Requerido**
    - **Permitido** (*valor predeterminado*)

  - **Letras mayúsculas en el PIN**
    - **No permitido**
    - **Requerido**
    - **Permitido** (*valor predeterminado*)

::: zone-end

## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre las líneas de base de seguridad](security-baselines.md)
- [Evitación de conflictos](security-baselines.md#avoid-conflicts)
- [Solución de problemas de directivas y perfiles en Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)