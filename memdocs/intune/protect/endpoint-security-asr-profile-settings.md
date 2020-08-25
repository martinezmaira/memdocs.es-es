---
title: Configuración de la reducción de la superficie expuesta a ataques de Seguridad de los puntos de conexión de Intune | Microsoft Docs
description: Configuración de la directiva de reducción de la superficie expuesta a ataques de Seguridad de los puntos de conexión en Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
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
ms.openlocfilehash: 36dca5ce8bb0fc3523bcd72441e3ecf22931609b
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146038"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Configuración de la directiva de reducción de la superficie expuesta a ataques de Seguridad de los puntos de conexión en Intune

Vea la configuración que puede definir en los perfiles de la directiva de *reducción de la superficie expuesta a ataques* en el nodo Seguridad de los puntos de conexión de Intune como parte de una [directiva de seguridad de puntos de conexión](../protect/endpoint-security-policy.md).

Perfiles y plataformas compatibles:

- **Windows 10 y versiones posteriores**:
  - Perfil: **Aislamiento de aplicaciones y navegador**
  - Perfil: **Protección web**
  - Perfil: **Control de la aplicación**
  - Perfil: **Reglas de reducción de la superficie expuesta a ataques**
  - Perfil: **Control de dispositivos**
  - Perfil: **Protección contra vulnerabilidades**

## <a name="app-and-browser-isolation-profile"></a>Perfil de aislamiento de aplicaciones y navegador

### <a name="app-and-browser-isolation"></a>Aislamiento de aplicaciones y navegador

- **Activación de la Protección de aplicaciones para Microsoft Edge (opciones)**  
  CSP: [AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Sin configurar** (*valor predeterminado*).
  - **Habilitado para Edge**: Protección de aplicaciones abre los sitios no aprobados en un contenedor de exploración virtualizado de Hyper-V.

  Cuando se establece en *Habilitado para Edge*, están disponibles las opciones siguientes:
  
  - **Comportamiento del Portapapeles**  
    CSP: [ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Seleccione qué acciones de copiar y pegar están permitidas desde el equipo local y un explorador virtual de Protección de aplicaciones.
    - **Sin configurar** (*valor predeterminado*).
    - **Bloquear copiar y pegar entre el PC y el explorador**
    - **Permitir copiar y pegar solo del explorador al PC**
    - **Permitir copiar y pegar solo del PC al explorador**
    - **Permitir copiar y pegar entre el PC y el explorador**

  - **Bloquear contenido externo de sitios aprobados que no son de la empresa**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: bloquea la carga de contenido de sitios web no aprobados.

  - **Recopilar registros de eventos que se producen dentro de una sesión de exploración virtual de Protección de aplicaciones**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: recopila registros de eventos que se producen dentro de una sesión de exploración virtual de Protección de aplicaciones.

  - **Permitir que se guarden los datos del explorador generados por el usuario**  
    CSP: [AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: permite que se guarden los datos de usuario que se crean durante una sesión de exploración virtual de Protección de aplicaciones. Los ejemplos de datos de usuario incluyen contraseñas, favoritos y cookies.

  - **Habilitar la aceleración de gráficos de hardware**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: en la sesión de exploración virtual de Protección de aplicaciones, use una unidad de procesamiento de gráficos virtual para cargar de forma más rápida los sitios web con gran cantidad de gráficos.

  - **Permitir a los usuarios descargar archivos en el host**  
    CSP: [SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: permite a los usuarios descargar archivos del explorador virtualizado al sistema operativo host.

- **Permiso de impresión en impresoras locales de Protección de aplicaciones**  

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: permite imprimir en impresoras locales.

- **Permiso de impresión en impresoras de red de Protección de aplicaciones**  

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: permite la impresión en impresoras de red.

- **Permiso de impresión en PDF de Protección de aplicaciones**  

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: permite la impresión en PDF.

- **Permiso de impresión en XPS de Protección de aplicaciones**  

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: permite la impresión en XPS.

- **Directiva de aislamiento de red de Windows**  
  
  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: configura la directiva de aislamiento de red de Windows.  
  
  Si se establece en *Sí*, se pueden configurar estos valores.

  - **Intervalos IP**  
    Expanda la lista desplegable, seleccione **Agregar** y especifique una *dirección inferior* y luego una *dirección superior*.

  - **Recursos de nube**  
    Expanda la lista desplegable, seleccione **Agregar** y especifique una *Dirección IP o FQDN* y un *Proxy*.

  - **Dominios de red**  
   Expanda la lista desplegable, seleccione **Agregar** y especifique *Dominios de red*.

  - **Servidores proxy**  
    Expanda la lista desplegable, seleccione **Agregar** y especifique *Servidores proxy*.

  - **Servidores proxy internos**  
    Expanda la lista desplegable, seleccione **Agregar** y especifique *Servidores proxy internos*.

  - **Recursos neutros**  
    Expanda la lista desplegable, seleccione **Agregar** y especifique *Recursos neutros*.

  - **Deshabilitar la detección automática de otros servidores proxy de empresa**  
    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: deshabilita la detección automática de otros servidores proxy de empresa.

  - **Deshabilitar la detección automática de otros intervalos IP empresariales**  
    - **Sin configurar** (*valor predeterminado*).
    - **Sí**: deshabilita la detección automática de otros intervalos IP empresariales.

## <a name="web-protection-profile"></a>Perfil de protección web

### <a name="web-protection"></a>Protección web

- **Habilitar la protección de red**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es deshabilitada.
  - **Definido por el usuario**
  - **Habilitar**: la protección de red está habilitada para todos los usuarios del sistema.
  - **Modo de auditoría**: no se bloquean los usuarios de dominios peligrosos y se generan eventos de Windows en su lugar.

- **Require SmartScreen for Microsoft Edge** (Requerir SmartScreen para Microsoft Edge)  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Sí**: se usa SmartScreen para proteger a los usuarios frente a posibles correos de suplantación de identidad (phishing) y software malintencionado.
  - **Sin configurar** (*valor predeterminado*).

- **Block malicious site access** (Bloquear el acceso a sitios malintencionados)  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Sí**: evita que los usuarios omitan las advertencias del filtro SmartScreen de Microsoft Defender y bloquea su acceso al sitio.
  - **Sin configurar** (*valor predeterminado*).

- **Block unverified file download** (Bloquear la descarga de archivos no comprobados)  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Sí**: evita que los usuarios omitan las advertencias del filtro SmartScreen de Microsoft Defender y bloquea la descarga de archivos no comprobados.
  - **Sin configurar** (*valor predeterminado*).

## <a name="application-control-profile"></a>Perfil de control de aplicaciones

### <a name="microsoft-defender-application-control"></a>Control de aplicaciones de Microsoft Defender

- **Control de aplicaciones de AppLocker**  
  CSP: [AppLocker](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

  - **Sin configurar** (*valor predeterminado*).
  - **Aplicar componentes y aplicaciones de Store**
  - **Auditar componentes y aplicaciones de Store**
  - **Aplicar componentes, aplicaciones de Store y Smartlocker**
  - **Auditar componentes, aplicaciones de Store y Smartlocker**
   

- **Impedir que los usuarios descarten advertencias de SmartScreen**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **No configurado** (*predeterminado*): los usuarios pueden ignorar las advertencias de SmartScreen sobre aplicaciones y archivos malintencionados.
  - **Sí**: SmartScreen está habilitado y los usuarios no pueden ignorar las advertencias sobre aplicaciones y archivos malintencionados.

- **Activar Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Sin configurar** (*valor predeterminado*): devuelve la opción al valor predeterminado de Windows, que es habilitar SmartScreen, aunque los usuarios pueden cambiar este valor. Para deshabilitar SmartScreen, use un URI personalizado.
  - **Sí**: se fuerza el uso de SmartScreen para todos los usuarios.

## <a name="attack-surface-reduction-rules-profile"></a>Perfil de reglas de reducción de la superficie expuesta a ataques

### <a name="attack-surface-reduction-rules"></a>Reglas de reducción de la superficie expuesta a ataques

- **Marcar el robo de credenciales desde el subsistema de autoridad de seguridad local de Windows (lsass.exe)**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874499)

  Esta regla de reducción de la superficie expuesta a ataques (ASR) se controla mediante el siguiente GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Definido por el usuario**
  - **Habilitar**: se bloquean los intentos de robo de credenciales a través de lsass.exe.
  - **Modo de auditoría**: no se bloquean los usuarios de dominios peligrosos y se generan eventos de Windows en su lugar.

- **Impedir que Adobe Reader cree procesos secundarios**  
  [Reducir las superficies de ataque con reglas de reducción de la superficie expuesta a ataques](https://go.microsoft.com/fwlink/?linkid=853979)
  
  Esta regla de ASR se controla a través del siguiente GUID: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Sin configurar** (*valor predeterminado*): se restaura el valor predeterminado de Windows, que es no bloquear la creación de procesos secundarios.
  - **Definido por el usuario**
  - **Habilitar**: se evita que Adobe Reader cree procesos secundarios.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquear los procesos secundarios.

- **Impedir que las aplicaciones de Office inserten código en otros procesos**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872974)

  Esta regla de ASR se controla a través del siguiente GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: evita que las aplicaciones de Office inserten código en otros procesos.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Impedir que las aplicaciones de Office creen contenido ejecutable**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872975)

  Esta regla de ASR se controla a través del siguiente GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: evita que las aplicaciones de Office creen contenido ejecutable.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Impedir que todas las aplicaciones de Office creen procesos secundarios**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872976)

  Esta regla de ASR se controla a través del siguiente GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: evita que las aplicaciones de Office creen procesos secundarios.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Impedir llamadas API de Win32 desde macros de Office**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872977)

  Esta regla de ASR se controla a través del siguiente GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: evita que las macros de Office usen llamadas API de Win32.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Impedir que las aplicaciones de comunicación de Office creen procesos secundarios**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874499)  

  Esta regla de ASR se controla a través del siguiente GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Sin configurar** (*valor predeterminado*): se restaura el valor predeterminado de Windows, que es no bloquear la creación de procesos secundarios.
  - **Definido por el usuario**
  - **Habilitar**: evita que las aplicaciones de comunicación de Office creen procesos secundarios.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquear los procesos secundarios.

- **Bloquear la ejecución de scripts potencialmente alterados (js/vbs/ps)**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872978)

  Esta regla de ASR se controla a través del siguiente GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: Defender evita la ejecución de scripts ofuscados.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Impedir que JavaScript o VBScript inicien el contenido ejecutable descargado**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872979)

   Esta regla de ASR se controla a través del siguiente GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: Defender evita que se ejecuten los archivos JavaScript o VBScript que se han descargado de Internet.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Bloquear creaciones del proceso que se originan desde comandos PSExec y WMI**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874500)

  Esta regla de ASR se controla por medio del siguiente GUID: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: se bloquea la creación de procesos mediante comandos de PSExec o WMI.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Bloquear la ejecución desde USB de procesos que no sean de confianza y estén sin firmar**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874502)

  Esta regla de ASR se controla a través del siguiente GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: evita que los procesos que no sean de confianza y estén sin firmar se ejecuten desde una unidad USB.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Bloquear los archivos ejecutables si no cumplen ciertos criterios de la lista de confianza, antigüedad o prevalencia**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874503)

  Esta regla de ASR se controla a través del siguiente GUID: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Bloquear contenido ejecutable del cliente de correo electrónico y el correo web**  
  [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Bloquear**: se bloquea el contenido ejecutable descargado desde clientes de correo electrónico y correo web.
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Usar la protección avanzada frente a ransomware**  
   [Proteger los dispositivos frente a vulnerabilidades](https://go.microsoft.com/fwlink/?linkid=874504)

  Esta regla de ASR se controla por medio del siguiente GUID: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado de Windows, que es desactivado.
  - **Definido por el usuario**
  - **Habilitar**
  - **Modo de auditoría**: se generan eventos de Windows en lugar de bloquearse.

- **Habilitar protección de carpetas**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Sin configurar** (*valor predeterminado*): este valor devuelve al valor predeterminado, que es no bloquear las lecturas ni las escrituras.
  - **Habilitar**: en las aplicaciones que no son de confianza, Defender bloquea los intentos de modificar o eliminar archivos de carpetas protegidas o de escribir en sectores del disco. Defender determina automáticamente qué aplicaciones son de confianza. Como alternativa, puede definir una lista propia de aplicaciones de confianza.
  - **Modo de auditoría**: se generan eventos de Windows cuando aplicaciones que no son de confianza acceden a carpetas controladas, pero no se aplica ningún bloqueo.
  - **Bloquear la modificación del disco**: solo se bloquean los intentos de escribir en sectores del disco.
  - **Auditar la modificación del disco**: se generan eventos de Windows en lugar de bloquear los intentos de escritura en sectores del disco.
  
- **Excluir archivos y rutas de las reglas de reducción de la superficie expuesta a ataques**  
  CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  Expanda la lista desplegable y seleccione **Agregar** para definir una **Ruta de acceso** a un archivo o carpeta que quiera excluir de las reglas de reducción de la superficie expuesta a ataques.

## <a name="device-control-profile"></a>Perfil de control de dispositivos

### <a name="device-control"></a>Control de dispositivos

- **Hardware device installation by device identifiers** (Instalación de dispositivos de hardware mediante identificadores de dispositivo)  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Este valor permite especificar una lista de identificadores de hardware Plug and Play e identificadores compatibles para dispositivos que Windows no puede instalar. Esta configuración de directiva tiene prioridad sobre cualquier otra configuración de directiva que permita a Windows instalar dispositivos.  Si habilita esta configuración de directiva en un servidor de escritorio remoto, esta afectará a la redirección de los dispositivos especificados desde un cliente de escritorio remoto al servidor de escritorio remoto.

  - **No configurado**.
  - **Permitir la instalación del dispositivo de hardware**: se podrán instalar o actualizar dispositivos según lo que permitan o impidan otras configuraciones de directiva.
  - **Bloquear la instalación de dispositivos de hardware** (*valor predeterminado*): Windows no podrá instalar un dispositivo cuyo identificador de hardware o identificador compatible aparezca en una lista que se define.

  Cuando se establece en *Bloquear la instalación de dispositivos de hardware*, se pueden configurar las siguientes opciones:

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

- **Examinar unidades extraíbles durante examen completo**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que examina las unidades extraíbles, aunque el usuario puede deshabilitar este examen.
  - **Sí**: durante un examen completo, se analizan las unidades extraíbles (como las unidades flash USB).

- **Block direct memory access** (Bloquear el acceso directo a memoria)  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)

  Esta configuración de directiva solo se aplica cuando está habilitado BitLocker o el cifrado de dispositivos.

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: impida el acceso directo a memoria (DMA) a todos los puertos PCI de bajada de conexión instantánea hasta que un usuario inicie sesión en Windows. Cuando un usuario inicie sesión, Windows mostrará los dispositivos PCI conectados a los puertos PCI de conexión de host. Cada vez que el usuario bloquee el equipo, DMA se bloquea en los puertos PCI de conexión instantánea sin dispositivos secundarios, hasta que el usuario inicie sesión de nuevo. Los dispositivos que ya aparecían cuando se ha desbloqueado la máquina seguirán funcionando hasta que se desconecten.

- **Enumeración de los dispositivos externos compatibles con Kernel DMA Protection**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Esta directiva puede proporcionar seguridad adicional contra los dispositivos compatibles con DMA externos. Permite mayor control sobre la enumeración de dispositivos externos compatibles con DMA incompatibles con la reasignación de DMA o el aislamiento de la memoria de dispositivo y el espacio aislado.

  Esta directiva solo surte efecto cuando la característica Kernel DMA Protection se admite y está habilitada por el firmware del sistema. Kernel DMA Protection es una característica de plataforma que debe ser compatible con el sistema en el momento de la fabricación. Para comprobar si el sistema admite Kernel DMA Protection, revise el campo Kernel DMA Protection en la página de resumen de MSINFO32.exe.

  - **No configurado**: (*valor predeterminado*)
  - **Bloquear todo**
  - **Permitir todo**

- **Bloquear conexiones Bluetooth**  
  CSP: [Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: bloquear las conexiones Bluetooth hacia el dispositivo y desde este.

- **Bloquear detectabilidad de Bluetooth**  
  CSP: [Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: impide que otros dispositivos con Bluetooth habilitado detecten el dispositivo.

- **Bloquear emparejamiento previo Bluetooth**  
  CSP: [Bluetooth/AllowPrepairing](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing).

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: impide que dispositivos Bluetooth específicos se emparejen automáticamente con el dispositivo de host.

- **Bloquear anuncios de Bluetooth**  
  CSP: [Bluetooth/AllowAdvertising](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: impide que el dispositivo envíe anuncios de Bluetooth.  

- **Bloquear conexiones Bluetooth próximas**  
  CSP: [Bluetooth/AllowPromptedProximalConnections](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections); impide que los usuarios usen la característica Emparejamiento rápido y otros escenarios basados en proximidad.

  - **Sin configurar** (*valor predeterminado*).
  - **Sí**: impide que un usuario del dispositivo utilice la característica Emparejamiento rápido y otros escenarios basados en proximidad.  

  [CSP Bluetooth/AllowPromptedProximalConnections](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Servicios Bluetooth permitidos**  
  CSP: [Bluetooth/ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist).  
  Para obtener más información sobre la lista de servicios, vea [Guía de uso de ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide).

  - **Agregar**: especifique los servicios y perfiles de Bluetooth permitidos como cadenas hexadecimales, por ejemplo, `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.
  - **Importar**: importe un archivo .csv que contenga una lista de servicios y perfiles Bluetooth como cadenas hexadecimales, por ejemplo, `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.

## <a name="exploit-protection-profile"></a>Perfil de protección contra vulnerabilidades

### <a name="exploit-protection"></a>Protección contra vulnerabilidades

- **Cargar XML**  
  CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  Permite a los administradores de TI enviar a todos los dispositivos de la organización una configuración que representa las opciones de mitigación deseadas del sistema y las aplicaciones. La configuración se representa por medio de un archivo XML. La protección contra vulnerabilidades ayuda a proteger los dispositivos frente al malware que usa las vulnerabilidades para infectar y propagar. Use la aplicación de seguridad de Windows o PowerShell para crear un conjunto de mitigaciones (conocido como una configuración). Después, puede exportar esta configuración como un archivo XML y compartirlo con varios equipos en la red para que todos tengan el mismo conjunto de opciones de mitigación. También puede convertir e importar un archivo XML de configuración EMET en un archivo XML de configuración de protección contra vulnerabilidades.

  Seleccione **Seleccionar archivo XML**, especifique la carga del archivo XML y haga clic en **Seleccionar**.
  - **Sin configurar** (*valor predeterminado*).
  - **Sí**

- **Bloquear a los usuarios para que no editen la interfaz de Protección contra vulnerabilidades de seguridad**  
  CSP: [DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Sin configurar** (*valor predeterminado*): los usuarios locales pueden realizar cambios en el área de configuración de protección contra vulnerabilidades.
  - **Sí**: evita que los usuarios realicen cambios en el área de configuración de protección contra vulnerabilidades del Centro de seguridad de Microsoft Defender.

## <a name="next-steps"></a>Pasos siguientes

[Directiva de seguridad de puntos de conexión para ASR](../protect/endpoint-security-asr-policy.md)
