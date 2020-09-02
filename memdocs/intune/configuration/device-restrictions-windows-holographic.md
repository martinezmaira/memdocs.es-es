---
title: 'Configuración para dispositivos Windows Holographic for Business: Microsoft Intune: Azure | Microsoft Docs'
description: Lea y configure las opciones de restricción de dispositivos de Microsoft Intune y Windows Holographic for Business. Controle la cancelación de la suscripción, la geolocalización, las contraseñas, la instalación de aplicaciones desde App Store, las cookies y los elementos emergentes de Microsoft Edge, Microsoft Defender, la búsqueda, la nube y el almacenamiento, la conectividad de Bluetooth, la hora del sistema y los datos de uso.
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2cd769b8e3ca4497c095210ea266d225354db24c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912838"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Configuración para dispositivos Windows Holographic for Business para permitir o restringir características mediante Intune

En este artículo se enumeran y describen los distintos valores de configuración que puede controlar en los dispositivos Windows Holographic for Business, como Microsoft Hololens. Como parte de su solución de administración de dispositivos móviles (MDM), use estos valores de configuración para permitir o deshabilitar características, seguridad de control, y mucho más.

Como administrador de Intune, puede crear y asignar estas opciones de configuración a los dispositivos.

## <a name="before-you-begin"></a>Antes de comenzar

[Creación de un perfil de configuración de restricciones de dispositivos de Windows 10](device-restrictions-configure.md#create-the-profile).

Al crear un perfil de configuración de restricciones de dispositivos de Windows 10, hay más opciones de configuración de las que se enumeran en este artículo. La configuración de este artículo es compatible con dispositivos Windows Holographic for Business.

## <a name="app-store"></a>Tienda de aplicaciones

- **Actualizar automáticamente las aplicaciones de la tienda**: **Bloquear** impide que las actualizaciones se instalen automáticamente desde Microsoft Store. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que las aplicaciones instaladas desde Microsoft Store se actualicen automáticamente.

  [CSP de ApplicationManagement/AllowAppStoreAutoUpdate](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Instalación de aplicaciones de confianza**: elija si se pueden instalar aplicaciones que no sean de Microsoft Store, lo que también se conoce como transferencia local. La transferencia local consiste en instalar y luego ejecutar o probar una aplicación no certificada por Microsoft Store. Por ejemplo, una aplicación interna solo para la empresa. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Bloquear**: evita la transferencia local. No se pueden instalar aplicaciones que no sean de Microsoft Store.
  - **Permitir**: permite la transferencia local. Se pueden instalar aplicaciones que no sean de Microsoft Store.

  [CSP de ApplicationManagement/AllowAllTrustedApps](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Desbloqueo de desarrollador**: permita la configuración de desarrollador de Windows, por ejemplo, permita que los usuarios puedan modificar las aplicaciones transferidas localmente. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Bloquear**: evita el modo de desarrollador y la transferencia local de aplicaciones.
  - **Permitir**: permite el modo de desarrollador y la transferencia local de aplicaciones.

  [CSP de ApplicationManagement/AllowDeveloperUnlock](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Red de telefonía móvil y conectividad

- **Bluetooth**: **Bloquear** evita que los usuarios habiliten Bluetooth. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de Bluetooth en el dispositivo.

  [CSP de Connectivity/AllowBluetooth](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Detectabilidad de Bluetooth**: **Bloquear** evita que otros dispositivos con Bluetooth habilitado detecten el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que otros dispositivos con Bluetooth habilitado (por ejemplo, unos auriculares) detecten el dispositivo.

  [CSP de Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Anuncios de Bluetooth**: **Bloquear** evita que el dispositivo envíe anuncios de Bluetooth. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el dispositivo envíe anuncios de Bluetooth.

  [CSP de Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Nube y almacenamiento

- **Cuenta Microsoft**: **Bloquear** impide que los usuarios asocien una cuenta Microsoft al dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir agregar y usar una cuenta Microsoft.

  [CSP de Accounts/AllowMicrosoftAccountConnection](/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Panel de control y configuración

- **Modificación de la hora del sistema**: **Bloquear** impide que los usuarios cambien la configuración de fecha y hora en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios cambien la configuración.

  [CSP de Settings/AllowDateTime](/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>General

- **Cancelar suscripción manualmente**: **Bloquear** impide que los usuarios eliminen la cuenta del área de trabajo a través del panel de control del área de trabajo en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Experience/AllowManualMDMUnenrollment](/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Geolocalización**: **Bloquear** impide que los usuarios activen servicios de ubicación en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Experience/AllowFindMyDevice](/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: **Bloquear** deshabilita el asistente de voz Cortana en el dispositivo. Si Cortana está desactivado, los usuarios pueden seguir buscando elementos en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de Cortana.

  [CSP de Experience/AllowCortana](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Explorador Microsoft Edge

- **Iniciar experiencia** > **Permitir elementos emergentes**: **Sí** (valor predeterminado) permite los elementos emergentes en el explorador web. **No** evita las ventanas emergentes en el explorador.

  [CSP de Browser/AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Favoritos y búsqueda** > **Mostrar sugerencias de búsqueda**: **Sí** (valor predeterminado) permite que el motor de búsqueda sugiera sitios a medida que se escriben frases de búsqueda en la barra de direcciones. **No** evita esta característica.

  [CSP de Browser/AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Privacidad y seguridad** > **Permitir administrador de contraseñas**: **Sí** (valor predeterminado) permite que Microsoft Edge use automáticamente el administrador de contraseñas, lo que permite a los usuarios guardar y administrar contraseñas en el dispositivo. **No** evita que Microsoft Edge use el administrador de contraseñas.

  [CSP de Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Privacidad y seguridad** > **Cookies**: elija cómo se administran las cookies en el explorador web. Las opciones son:
  - **Permitir**: las cookies se almacenan en el dispositivo.
  - **Bloquear todas las cookies**: las cookies no se almacenan en el dispositivo.
  - **Bloquear solo cookies de terceros**: las cookies de terceros o de asociados no se almacenan en el dispositivo.

  [CSP de Browser/AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Privacidad y seguridad** > **Enviar encabezados de no seguimiento**: **Sí** envía encabezados de no seguimiento a los sitios web que solicitan información de seguimiento (recomendado). **No** (valor predeterminado) no envía los encabezados que permiten a los sitios web realizar un seguimiento del usuario. Los usuarios pueden configurar esta opción.

  [CSP de Browser/AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>SmartScreen de Microsoft Defender

- **SmartScreen para Microsoft Edge**: **Requerir** desactiva SmartScreen de Microsoft Defender y evita que los usuarios lo activen. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo active SmartScreen y permita que los usuarios lo activen y desactiven.

  [Browser/AllowSmartScreen CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen) (CSP de Browser/AllowSmartScreen)

## <a name="password"></a>Contraseña

- **Contraseña**: **Requerir** obliga a los usuarios a escribir una contraseña para acceder al dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a dispositivos sin una contraseña. Solo se aplica a cuentas locales. Las contraseñas de las cuentas de dominio siguen siendo configuradas por Active Directory (AD) y Azure AD.

  [CSP de DeviceLock/DevicePasswordEnabled](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Requerir una contraseña cuando el dispositivo vuelva de un estado de inactividad**: **Requerir** obliga a los usuarios a escribir una contraseña para desbloquear el dispositivo después de que este haya estado inactivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no requerir un PIN o una contraseña después de que el dispositivo haya estado inactivo.

  [CSP de DeviceLock/AllowIdleReturnWithoutPassword](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Informes y telemetría

- **Compartir los datos de uso**: elija el nivel de datos de diagnóstico que se envía. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen el nivel que se envía. De forma predeterminada, el sistema operativo podría no compartir ningún dato.
  - **Seguridad**: información necesaria para ayudar a proteger Windows, incluidos datos sobre la configuración del componente Experiencia del usuario y telemetría asociadas, la Herramienta de eliminación de software malintencionado y Microsoft Defender.
  - **Básica**: información básica del dispositivo que incluye datos relacionados con la calidad, la compatibilidad de aplicaciones, datos de uso de aplicaciones y datos del nivel de seguridad.
  - **Mejorada**: información adicional que incluye: cómo se usan Windows, Windows Server, System Center y las aplicaciones, cómo funcionan, datos avanzados de confiabilidad y datos de los niveles Seguridad y Básica.
  - **Completa**: todos los datos necesarios para identificar y ayudar a solucionar problemas, además de datos de los niveles Seguridad, Básica y Mejorada.

  [System/AllowTelemetry CSP](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry) (CSP de System/AllowTelemetry)

## <a name="search"></a>Búsqueda

- **Ubicación de la búsqueda**: **Bloquear** impide que Windows Search use la ubicación. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.

  [CSP de Search/AllowSearchToUseLocation](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).