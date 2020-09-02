---
title: 'Configuración de restricciones de dispositivos para Windows 10 en Microsoft Intune: Azure | Microsoft Docs'
description: Consulte una lista de todas las configuraciones y sus descripciones para crear restricciones de dispositivo en Windows 10 y dispositivos posteriores. Use estos valores en un perfil de configuración para controlar las capturas de pantalla, los requisitos de contraseña, la configuración de la pantalla completa, las aplicaciones de la tienda, el explorador Microsoft Edge, Microsoft Defender, el acceso a la nube, el menú de inicio y más en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38465f709cf07da97e26c36a9fabba232aca9ba2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912889"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Configuración de dispositivos con Windows 10 y versiones posteriores para permitir o restringir características mediante Intune

En este artículo se enumeran y describen todos los diferentes valores de configuración que puede controlar en los dispositivos con Windows 10 y versiones posteriores. Como parte de la solución de administración de dispositivos móviles (MDM), use estos valores para habilitar o deshabilitar características, establecer reglas de contraseña, personalizar la pantalla de bloqueo, usar Microsoft Defender, etc.

Estos valores se agregan a un perfil de configuración de dispositivo en Intune y luego se asignan o implementan en los dispositivos con Windows 10.

> [!Note]
> No todas las opciones están disponibles en todas las ediciones de Windows. Para ver las ediciones admitidas, consulte los [CSP de directiva](/windows/client-management/mdm/policy-configuration-service-provider) (se abre otro sitio web de Microsoft).
>  
> En un perfil de restricciones de dispositivos Windows 10, la mayoría de los valores configurables se implementan en el nivel de dispositivo mediante grupos de dispositivos. Las directivas implementadas en grupos de usuarios se aplican a los usuarios de destino y a los usuarios que tienen una licencia de Intune e inician sesión en ese dispositivo.

## <a name="before-you-begin"></a>Antes de comenzar

[Creación de un perfil de restricciones de dispositivos de Windows 10](device-restrictions-configure.md#create-the-profile)

## <a name="app-store"></a>Tienda de aplicaciones

Estas opciones de configuración usan [ApplicationManagement policy CSP](/windows/client-management/mdm/policy-csp-applicationmanagement) (CSP de directiva de ApplicationManagement), que también indica las ediciones de Windows compatibles.

- **Tienda de aplicaciones (solo móvil)** : **Bloquear** impide que los usuarios accedan a la tienda de aplicaciones en dispositivos móviles. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios acceder a la tienda de aplicaciones.
- **Actualizar automáticamente las aplicaciones de la tienda**: **Bloquear** impide que las actualizaciones se instalen automáticamente desde Microsoft Store. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que las aplicaciones instaladas desde Microsoft Store se actualicen automáticamente.

  [CSP de ApplicationManagement/AllowAppStoreAutoUpdate](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Instalación de aplicaciones de confianza**: elija si se pueden instalar aplicaciones que no sean de Microsoft Store, lo que también se conoce como transferencia local. La transferencia local consiste en instalar y luego ejecutar o probar una aplicación no certificada por Microsoft Store. Por ejemplo, una aplicación interna solo para la empresa. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Bloquear**: evita la transferencia local. No se pueden instalar aplicaciones que no sean de Microsoft Store.
  - **Permitir**: permite la transferencia local. Se pueden instalar aplicaciones que no sean de Microsoft Store.

- **Desbloqueo de desarrollador**: permita la configuración de desarrollador de Windows, por ejemplo, permita que los usuarios puedan modificar las aplicaciones transferidas localmente. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Bloquear**: evita el modo de desarrollador y la transferencia local de aplicaciones.
  - **Permitir**: permite el modo de desarrollador y la transferencia local de aplicaciones.

  [Habilitar el dispositivo para el desarrollo](/windows/uwp/get-started/enable-your-device-for-development) contiene más información sobre esta característica.
  
  [CSP de ApplicationManagement/AllowAllTrustedApps](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Datos de aplicación compartidos entre usuarios**: seleccione **Permitir** para compartir datos de aplicación entre distintos usuarios en el mismo dispositivo y con otras instancias de esa aplicación. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede impedir que se compartan datos con otros usuarios y otras instancias de la misma aplicación.

  [CSP de ApplicationManagement/AllowSharedUserAppData](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Usar solo una tienda privada**: **Permitir** solo permite que se descarguen aplicaciones de una tienda privada y no de la tienda pública, incluido un catálogo comercial. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que se descarguen aplicaciones de una tienda privada y de una pública.

  [CSP de ApplicationManagement/RequirePrivateStoreOnly](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Inicio de aplicaciones de la tienda**: **Bloquear** deshabilita todas las aplicaciones que se han instalado previamente en el dispositivo, o bien que se han descargado de Microsoft Store. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que se abran estas aplicaciones.

  [CSP de ApplicationManagement/DisableStoreOriginatedApps](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **Instalar los datos de aplicación en el volumen del sistema**: **Bloquear** evita que las aplicaciones almacenen datos en el volumen del sistema del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que las aplicaciones almacenen datos en el volumen de disco del sistema.

  [CSP de ApplicationManagement/RestrictAppDataToSystemVolume](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Instalar las aplicaciones en la unidad del sistema**: **Bloquear** evita que las aplicaciones se instalen en la unidad del sistema del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que las aplicaciones se instalen en la unidad del sistema.

  [CSP de ApplicationManagement/RestrictAppToSystemVolume](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **Game DVR (solo escritorio)** : **Bloquear** deshabilita la grabación y difusión de juegos de Windows. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir la grabación y retransmisión de juegos.

  [CSP de ApplicationManagement/AllowGameDVR](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Solo aplicaciones de la tienda**: esta opción determina la experiencia del usuario al instalar aplicaciones desde ubicaciones que no son Microsoft Store. No impide la instalación de contenido desde dispositivos USB, recursos compartidos de red u otros orígenes que no sean de Internet. Use un explorador de confianza para asegurarse de que estas protecciones funcionan según lo previsto.

  Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios instalar aplicaciones desde ubicaciones distintas de Microsoft Store, incluidas las aplicaciones definidas en otras configuraciones de directiva.  
  - **Cualquier sitio**: desactiva las recomendaciones de aplicaciones y permite a los usuarios instalar aplicaciones desde cualquier ubicación.  
  - **Solo Store**: la intención es evitar que el contenido malintencionado afecte a los dispositivos de usuario al descargar contenido ejecutable de Internet. Cuando los usuarios intentan instalar aplicaciones desde Internet, se bloquea la instalación. Los usuarios ven un mensaje que recomienda que descarguen aplicaciones de Microsoft Store.
  - **Recomendaciones**: al instalar una aplicación desde Internet que está disponible en Microsoft Store, los usuarios ven un mensaje que recomienda descargarla de la tienda.  
  - **Preferir Store**: advierte a los usuarios cuando instalan aplicaciones desde ubicaciones distintas a Microsoft Store.

  [SmartScreen/EnableAppInstallControl CSP](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **Control de usuario sobre las instalaciones**: **Bloquear** impide que los usuarios cambien las opciones de instalación que normalmente están reservadas a los administradores del sistema, como la especificación del directorio para instalar los archivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, Windows Installer puede impedir que los usuarios cambien estas opciones de instalación y se omitan algunas de las características de seguridad de Windows Installer.

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Instalar aplicaciones con privilegios elevados**: **Bloquear** indica a Windows Installer que use permisos elevados cuando instale cualquier programa en el sistema. Estos privilegios se extienden a todos los programas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema puede aplicar los permisos del usuario actual cuando instala programas que un administrador del sistema no implementa ni ofrece.

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Aplicaciones de inicio**: escriba una lista de las aplicaciones que deben abrirse después de que un usuario inicie sesión en el dispositivo. Asegúrese de usar una lista delimitada por punto y coma de nombres de familia de paquete (PFN) de aplicaciones Windows. Para que esta directiva funcione, el manifiesto de las aplicaciones Windows debe usar una tarea de inicio.

  [ApplicationManagement/LaunchAppAfterLogOn CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>Red de telefonía móvil y conectividad

Estas opciones de configuración usan los CSP de [directiva de conectividad](/windows/client-management/mdm/policy-csp-connectivity) y [directiva de Wi-Fi](/windows/client-management/mdm/policy-csp-wifi), que también enumeran las ediciones de Windows compatibles.

- **Canal de datos móviles**: elija si los usuarios pueden usar datos, por ejemplo, navegar por Internet, cuando están conectados a una red móvil. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. Los usuarios pueden desactivarlo.
  - **Bloquear**: no permita el canal de datos móviles. Los usuarios no pueden activarlo.
  - **Permitir (no editable)** : permite el canal de datos móviles. Los usuarios no pueden desactivarlo.

- **Itinerancia de datos**: **Bloquear** evita la itinerancia de datos móviles en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, se podría permitir la itinerancia entre redes al acceder a los datos.
- **VPN a través de la red de telefonía móvil**: **Bloquear** evita que el dispositivo acceda a conexiones VPN cuando se conecta a una red móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a la VPN usar cualquier conexión, incluida la móvil.
- **Itinerancia de VPN a través de la red de telefonía móvil**: **Bloquear** evita que el dispositivo acceda a conexiones VPN cuando está en itinerancia en una red móvil. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir conexiones VPN en itinerancia.
- **Servicio de dispositivos conectados**: **Bloquear** deshabilita el componente de plataforma de dispositivos conectados (CDP). CDP habilita la detección de otros dispositivos y la conexión a ellos (a través de Bluetooth/LAN o la nube) para permitir el inicio de aplicaciones remoto, la mensajería remota, las sesiones de aplicación remotas y otras experiencias en varios dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el servicio de dispositivos conectados, lo que habilita la detección de otros dispositivos Bluetooth y la conexión a ellos.
- **NFC**: **Bloquear** evita las capacidades de transmisión de datos en proximidad (NFC). Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios habilitar y configurar características de NFC en el dispositivo.
- **Wi-Fi**: **Bloquear** evita que los usuarios habiliten, configuren y usen conexiones Wi-Fi en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir las conexiones Wi-Fi.
- **Conectar automáticamente a zonas Wi-Fi**: **Bloquear** evita que los dispositivos se conecten automáticamente a zonas Wi-Fi. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los dispositivos se conecten automáticamente a zonas Wi-Fi gratuitas y acepten de forma automática los términos y condiciones para la conexión.
- **Configuración manual de Wi-Fi**: **Bloquear** evita que los dispositivos se conecten a Wi-Fi fuera de redes instaladas por el servidor MDM. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios agregar y configurar sus propios SSID de red de conexiones Wi-Fi.
- **Intervalo de detección de Wi-Fi**: especifique con qué frecuencia los dispositivos detectan redes Wi-Fi. Escriba un valor de 1 (más frecuente) a 500 (menos frecuente). El valor predeterminado es `0` (cero).

### <a name="bluetooth"></a>Bluetooth

Estas opciones de configuración usan [CSP de directiva de Bluetooth](/windows/client-management/mdm/policy-csp-bluetooth), que también indica las ediciones de Windows compatibles.

- **Bluetooth**: **Bloquear** evita que los usuarios habiliten Bluetooth. **Sin configurar** (valor predeterminado) permite Bluetooth en el dispositivo.
- **Detectabilidad de Bluetooth**: **Bloquear** evita que otros dispositivos con Bluetooth habilitado detecten el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que otros dispositivos con Bluetooth habilitado (por ejemplo, unos auriculares) detecten el dispositivo.

  [CSP de Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Emparejamiento previo Bluetooth**: **Bloquear** evita que dispositivos Bluetooth específicos se emparejen automáticamente con un dispositivo de host. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el emparejamiento automático con el dispositivo host.

  [CSP de Bluetooth/AllowPrepairing](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **Anuncios de Bluetooth**: **Bloquear** evita que el dispositivo envíe anuncios de Bluetooth. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el dispositivo envíe anuncios de Bluetooth.

  [CSP de Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **Conexiones Bluetooth próximas**: **Bloquear** impide que un dispositivo de usuario utilice Emparejamiento rápido y otros escenarios basados en proximidad. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que el dispositivo envíe anuncios de Bluetooth.

  [CSP Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Servicios Bluetooth permitidos**: **agregue** una lista de perfiles y servicios Bluetooth permitidos como cadenas hexadecimales, por ejemplo, `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.

  [ServicesAllowedList usage guide](/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) (Guía de uso de ServicesAllowedList) contiene más información sobre la lista de servicios.

  [CSP de Bluetooth/ServicesAllowedList](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## <a name="cloud-and-storage"></a>Nube y almacenamiento

Estas opciones de configuración usan [CSP de directiva de cuentas](/windows/client-management/mdm/policy-csp-accounts), que también indica las ediciones de Windows compatibles.

> [!IMPORTANT]
> Bloquear o deshabilitar estas opciones de cuenta de Microsoft puede afectar a los escenarios de inscripción que requieren que los usuarios inicien sesión en Azure AD. Por ejemplo, si usa [AutoPilot preferencial](/windows/deployment/windows-autopilot/white-glove). Normalmente, se muestra a los usuarios una ventana de inicio de sesión de Azure AD. Cuando esta configuración se establece en **Bloquear** o **Deshabilitar**, es posible que no se muestre la opción de inicio de sesión de Azure AD. En su lugar, se pide a los usuarios que acepten el CLUF y creen una cuenta local, que puede que no sea lo que se quiere.

- **Cuenta Microsoft**: **Bloquear** impide que los usuarios asocien una cuenta Microsoft al dispositivo. **Bloquear** puede tener impacto también en algunos escenarios de inscripción que dependen de que los usuarios completen el proceso de inscripción. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir agregar y usar una cuenta Microsoft.
- **Cuenta que no es Microsoft**: **Bloquear** impide que los usuarios agreguen cuentas que no son de Microsoft a través de la interfaz de usuario. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios agreguen cuentas de correo electrónico que no están asociadas a una cuenta Microsoft.
- **Sincronización de configuración de cuenta Microsoft**: **Bloquear** impide que la configuración de dispositivo y aplicación asociada a una cuenta Microsoft se sincronice entre los dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta sincronización.
- **Ayudante para el inicio de sesión de cuentas Microsoft**: Este servicio del sistema operativo permite a los usuarios iniciar sesión en su cuenta Microsoft. De forma predeterminada, el sistema operativo podría permitir a los usuarios iniciar y detener el servicio **Ayudante para el inicio de sesión de cuenta Microsoft** (wlidsvc).
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios iniciar y detener el servicio **Ayudante para el inicio de sesión de cuenta Microsoft** (wlidsvc).
  - **Disabled**: configura el servicio de Asistente para el inicio de sesión de cuenta Microsoft (wlidsvc) como deshabilitado e impide que los usuarios lo inicien manualmente.

      **Deshabilitar** puede tener impacto también en algunos escenarios de inscripción que dependen de que los usuarios completen la inscripción. Por ejemplo, si usa [AutoPilot preferencial](/windows/deployment/windows-autopilot/white-glove). Normalmente, se muestra a los usuarios una ventana de inicio de sesión de Azure AD. Cuando se establece en **Deshabilitar**, puede que la opción de inicio de sesión de Azure AD no se muestre. En su lugar, se pide a los usuarios que acepten el CLUF y creen una cuenta local, que puede que no sea lo que se quiere.

## <a name="cloud-printer"></a>Impresora en la nube

Estas opciones de configuración usan [CSP de directiva de EnterpriseCloudPrint](/windows/client-management/mdm/policy-csp-enterprisecloudprint), que también indica las ediciones de Windows compatibles.

- **URL de detección de impresoras**: especifique la URL para encontrar impresoras en la nube. Por ejemplo, escriba `https://cloudprinterdiscovery.contoso.com`.
- **URL de autoridad de acceso a impresoras**: especifique la dirección URL del punto de conexión de autenticación para obtener tokens de OAuth. Por ejemplo, escriba `https://azuretenant.contoso.com/adfs`.
- **GUID de aplicación cliente nativa de Azure**: especifique el GUID de una aplicación cliente autorizada para obtener tokens de OAuth desde OAuthAuthority. Por ejemplo, escriba `E1CF1107-FF90-4228-93BF-26052DD2C714`.
- **URI de recurso de servicio de impresión**: indique el URI de recurso de OAuth del servicio de impresión configurado en Azure Portal. Por ejemplo, escriba `http://MicrosoftEnterpriseCloudPrint/CloudPrint`.
- **N.º máximo de impresoras para consultar**: indique el número máximo de impresoras que quiere que se consulten. El valor predeterminado es `20`.
- **URI de recurso del servicio de detección de impresoras**: indique el URI de recurso de OAuth del servicio de detección de impresoras configurado en Azure Portal. Por ejemplo, escriba `http://MopriaDiscoveryService/CloudPrint`.

> [!TIP]
> Después de configurar la [impresión de Windows Server híbrida en la nube](/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview), puede configurar estas opciones e implementarlas en los dispositivos Windows.

## <a name="control-panel-and-settings"></a>Panel de control y configuración

- **Aplicación Configuración**: **Bloquear** impide que los usuarios accedan a la aplicación de configuración de Windows. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios abran la aplicación Configuración en el dispositivo.
  - **Sistema**: **Bloquear** evita el acceso al área Sistema de la aplicación Configuración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
    - **Modificación de la configuración de inicio/apagado y suspensión** (solo equipos de escritorio): **Bloquear** impide que los usuarios cambien la configuración de inicio/apagado y suspensión en el dispositivo. **Sin configurar** (valor predeterminado) permite que los usuarios cambien la configuración de inicio/apagado y suspensión.
  - **Dispositivos**: **Bloquear** evita el acceso al área Dispositivos de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Red e Internet**: **Bloquear** evita el acceso al área Red e Internet de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Personalización**: **Bloquear** evita el acceso al área Personalización de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Aplicaciones**: **Bloquear** evita el acceso al área Aplicaciones de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Cuentas**: **Bloquear** evita el acceso al área Cuentas de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Hora e idioma**: **Bloquear** evita el acceso al área Hora e idioma de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
    - **Modificación de la hora del sistema**: **Bloquear** impide que los usuarios cambien la configuración de fecha y hora en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Los usuarios pueden cambiar la configuración.
    - **Modificación de la configuración regional** (solo escritorio): **Bloquear** impide que los usuarios cambien la configuración regional en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Los usuarios pueden cambiar la configuración.
    - **Modificación de la configuración de idioma (solo equipos de escritorio)** : **Bloquear** impide que los usuarios cambien la configuración de idioma en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. Los usuarios pueden cambiar la configuración.

      [Settings policy CSP](/windows/client-management/mdm/policy-csp-settings) (CSP de directiva de configuración)

  - **Juegos**: **Bloquear** evita el acceso al área Juegos de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Accesibilidad**: **Bloquear** evita el acceso al área Accesibilidad de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Privacidad**: **Bloquear** evita el acceso al área Privacidad de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
  - **Actualización y seguridad**: **Bloquear** evita el acceso al área Actualización y seguridad de la aplicación Configuración en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

## <a name="display"></a>Pantalla

Estas opciones de configuración usan [CSP de directiva de pantalla](/windows/client-management/mdm/policy-csp-display), que también indica las ediciones de Windows compatibles.

El ajuste de escala de PPP de GDI permite a las aplicaciones sin reconocimiento de PPP lograr el reconocimiento de PPP por monitor.

- **Activar el ajuste de GDI para las aplicaciones**: **agregue** las aplicaciones heredadas que quiere que tengan activado el ajuste de escala de PPP de GDI. Por ejemplo, escriba `filename.exe` o `%ProgramFiles%\Path\Filename.exe`.

  El ajuste de escala de PPP de GDI se activa para todas las aplicaciones heredadas de la lista.

- **Desactivar el ajuste de GDI para las aplicaciones**: **agregue** las aplicaciones heredadas que quiere que tengan desactivado el ajuste de escala de PPP de GDI. Por ejemplo, escriba `filename.exe` o `%ProgramFiles%\Path\Filename.exe`.

  El ajuste de escala de PPP de GDI se desactiva para todas las aplicaciones heredadas de la lista.

También puede **Importar** un archivo .csv con la lista de aplicaciones.

## <a name="general"></a>General

Estas opciones de configuración usan [experience policy CSP](/windows/client-management/mdm/policy-csp-experience) (CSP de directiva de experiencia), que también indica las ediciones de Windows compatibles. 

- **Captura de pantalla** (solo móviles): **Bloquear** impide que los usuarios hagan capturas de pantalla en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Copiar y pegar (solo móvil)** : **Bloquear** impide que los usuarios usen Copiar y pegar entre aplicaciones en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Cancelar suscripción manualmente**: **Bloquear** impide que los usuarios eliminen la cuenta del área de trabajo a través del panel de control del área de trabajo en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  Esta configuración de directiva no se aplica si el equipo está unido a Azure AD y la inscripción automática está habilitada.

- **Instalación manual del certificado raíz** (solo móviles): **Bloquear** impide que los usuarios instalen manualmente certificados raíz y certificados CAP intermedios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Cámara**: **Bloquear** impide que los usuarios usen la cámara en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a la cámara del dispositivo.

  Intune solo administra el acceso a la cámara del dispositivo. No tiene acceso a imágenes o vídeos.

  [CSP de Cámara](/windows/client-management/mdm/policy-csp-camera)

- **Sincronización de archivos de OneDrive**: **Bloquear** impide que los usuarios sincronicen archivos con OneDrive desde el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de System/DisableOneDriveFileSync](/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **Almacenamiento extraíble**: **Bloquear** impide que los usuarios usen dispositivos de almacenamiento externo, como tarjetas SD, con el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Geolocalización**: **Bloquear** impide que los usuarios activen servicios de ubicación en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de System/AllowLocation](/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **Conexión compartida**: **Bloquear** evita el uso compartido de una conexión a Internet en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Restablecimiento del teléfono**: **Bloquear** impide que los usuarios borren o realicen un restablecimiento de fábrica en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Conexión USB**: **Bloquear** evita el acceso a dispositivos de almacenamiento externo mediante una conexión USB en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. La carga USB no se ve afectada por esta opción.

  [CSP de Connectivity/AllowUSBConnection](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **Modo antirrobo** (solo móviles): **Bloquear** impide que los usuarios seleccionen la preferencia de modo antirrobo en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Cortana**: **Bloquear** deshabilita el asistente de voz Cortana en el dispositivo. Si Cortana está desactivado, los usuarios pueden seguir buscando elementos en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el uso de Cortana.

  [CSP de Experience/AllowCortana](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

- **Grabación de voz** (solo móviles): **Bloquear** impide que los usuarios usen la grabadora de voz del dispositivo en este. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la grabación de voz de aplicaciones.
- **Modificación del nombre del dispositivo** (solo móvil): **Bloquear** impide que los usuarios cambien el nombre del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Agregar paquetes de aprovisionamiento**: **Bloquear** evita el agente de configuración en tiempo de ejecución que instala paquetes de aprovisionamiento en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Quitar paquetes de aprovisionamiento**: **Bloquear** evita el agente de configuración en tiempo de ejecución que quita paquetes de aprovisionamiento del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Detección de dispositivos**: **Bloquear** evita que otros dispositivos detecten este. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [Experience/AllowDeviceDiscovery](/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **Cambio de tarea** (solo móviles): **Bloquear** evita el cambio de tarea en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.
- **Cuadro de diálogo de error de tarjeta SIM** (sólo móviles): **Bloquee** la aparición de mensajes de error en el dispositivo si no se detecta ninguna tarjeta SIM. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría mostrar mensajes de error.
- **Ink Workspace** (Área de trabajo de Ink): elija si el usuario tiene acceso al área de trabajo de Ink y cómo. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría activar el área de trabajo de Ink, y los usuarios pueden usarla por encima de la pantalla de bloqueo.
  - **Deshabilitada en la pantalla de bloqueo**: el área de trabajo de Ink está habilitada y la característica está activada. Pese a ello, los usuarios no pueden acceder a ella por encima de la pantalla de bloqueo.
  - **Disabled**: el acceso al área de trabajo de Ink está deshabilitado. La característica está desactivada.

  [WindowsInkWorkspace policy CSP](/windows/client-management/mdm/policy-csp-windowsinkworkspace) (CSP de directiva de WindowsInkWorkspace)

- **Restablecimiento de Autopilot**: elija **Permitir** para que los usuarios con derechos administrativos puedan eliminar todos los datos y la configuración de usuario con **CTRL + Win + R** en la pantalla de bloqueo del dispositivo. El dispositivo se vuelve a configurar e inscribir automáticamente para la administración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría impedir esta característica.
- **Exigir que los usuarios se conecten a la red durante la configuración del dispositivo**: elija **Requerir** para que el dispositivo se conecte a una red antes de pasar de la página Red durante la configuración de Windows. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios pasar de la página Red, aunque no estén conectados a una red.

  La configuración se hace efectiva la próxima vez que se borra o restablece el dispositivo. Al igual que cualquier otra configuración de Intune, el dispositivo debe estar inscrito y administrado por Intune para recibir la configuración. Pero, una vez que se ha inscrito y recibe las directivas, al restablecer el dispositivo se fuerza la configuración durante la siguiente configuración de Windows.

  [CSP de TenantLockdown](/windows/client-management/mdm/tenantlockdown-csp)

- **Acceso directo a memoria**: **Bloquear** impide el acceso directo a memoria (DMA) a todos los puertos de bajada PCI de conexión instantánea hasta que un usuario inicia sesión en Windows. **Habilitado** (valor predeterminado) permite el acceso a DMA, incluso cuando un usuario no ha iniciado sesión.

  [DataProtection/AllowDirectMemoryAccess CSP](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **Finalizar procesos desde el Administrador de tareas**: esta configuración determina si los usuarios que no son administradores pueden usar el Administrador de tareas para finalizar tareas. Si selecciona **Bloquear**, se impide que los usuarios estándar (no administradores) usen el Administrador de tareas para finalizar un proceso o una tarea en el dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir que los usuarios estándar finalicen un proceso o una tarea con el Administrador de tareas.

  [CSP de TaskManager/AllowEndTask](/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## <a name="locked-screen-experience"></a>Experiencia de pantalla bloqueada

- **Notificaciones del centro de actividades (solo móviles)** : **Bloquear** evita que las notificaciones del centro de actividades aparezcan en la pantalla de bloqueo del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios elegir qué aplicaciones muestran notificaciones en la pantalla de bloqueo.

  [AboveLock/AllowActionCenterNotifications CSP](/windows/client-management/mdm/policy-configuration-service-provider#AboveLock_AllowActionCenterNotifications) (CSP de AboveLock/AllowActionCenterNotifications)

- **URL de imagen de pantalla de bloqueo (solo equipos de escritorio)** : escriba la dirección URL de una imagen en formato JPG, JPEG o PNG que se usa como fondo de pantalla de la pantalla de bloqueo de Windows. Por ejemplo, escriba `https://contoso.com/image.png`. Esta opción bloquea la imagen y no se puede cambiar posteriormente.

  [CSP de Personalization/LockScreenImageUrl](/windows/client-management/mdm/personalization-csp)

- **Tiempo de espera de la pantalla configurable por el usuario (solo dispositivos móviles)** : **Permitir** permite a los usuarios configurar el tiempo de espera de la pantalla. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no proporcionar esta opción a los usuarios.

  [DeviceLock/AllowScreenTimeoutWhileLockedUserConfig CSP](/windows/client-management/mdm/policy-configuration-service-provider#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig) (CSP de DeviceLock/AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana en pantalla bloqueada** (solo escritorio): **Bloquear** impide que los usuarios interactúen con Cortana cuando el dispositivo está en la pantalla de bloqueo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir la interacción con Cortana.

  [AboveLock/AllowCortanaAboveLock CSP](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock) (CSP de AboveLock/AllowCortanaAboveLock)

- **Notificaciones del sistema en pantalla bloqueada**: **Bloquear** evita que las notificaciones del sistema aparezcan en la pantalla de bloqueo del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir estas notificaciones.

  [AboveLock/AllowToasts CSP](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts) (CSP de AboveLock/AllowToasts)

- **Tiempo de espera de la pantalla (solo dispositivos móviles)** : establezca la duración (en segundos) desde que se bloquea la pantalla hasta que se apaga. Los valores admitidos son de 11 a 1800. Por ejemplo, escriba `300` para establecer este tiempo de espera en 5 minutos.

  [DeviceLock/ScreenTimeoutWhileLocked CSP](/windows/client-management/mdm/policy-configuration-service-provider#DeviceLock_ScreenTimeoutWhileLocked) (CSP de DeviceLock/ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Mensajería

Estas opciones de configuración usan [CSP de directiva de mensajería](/windows/client-management/mdm/policy-csp-messaging), que también indica las ediciones de Windows compatibles.

- **Sincronización de mensajes (solo móvil)** : **Bloquear** deshabilita la copia de seguridad y la restauración de los mensajes de texto, así como la sincronización de mensajes entre dispositivos Windows. La deshabilitación ayuda a evitar que la información se almacene en servidores fuera del control de la organización. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir a los usuarios cambiar esta opción y sincronizar sus mensajes.
- **MMS (solo móvil)** : **Bloquear** deshabilita la funcionalidad de envío y recepción de MMS en el dispositivo. En las empresas, use esta directiva para deshabilitar MMS en los dispositivos como parte del requisito de auditoría o administración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el envío y recepción de MMS.
- **RCS (solo móvil)** : **Bloquear** deshabilita la funcionalidad de envío y recepción de Rich Communication Services (RCS) en el dispositivo. En las empresas, use esta directiva para deshabilitar RCS en los dispositivos como parte del requisito de auditoría o administración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el envío y recepción de RCS.

## <a name="microsoft-edge-browser"></a>Explorador Microsoft Edge

Estas opciones de configuración usan [browser policy CSP](/windows/client-management/mdm/policy-csp-browser) (CSP de directiva de explorador), que también indica las ediciones de Windows compatibles.

> [!NOTE]
> El uso del CSP de directiva de explorador se aplica a la versión 45 y anteriores de Microsoft Edge. Para Microsoft Edge Enterprise versión 77 y posteriores, vea [Configuración de opciones de directiva de Microsoft Edge con Microsoft Intune](/DeployEdge/configure-edge-with-intune).

### <a name="use-microsoft-edge-kiosk-mode"></a>Usar el modo de pantalla completa de Microsoft Edge

Las opciones de configuración disponibles cambian en función de lo que elija. Las opciones son:

- **No** (valor predeterminado): Microsoft Edge no se ejecuta en pantalla completa. Toda la configuración de Microsoft Edge está disponible y puede cambiarla y configurarla.
- **Señal digital o interactiva (pantalla completa con una sola aplicación)** : filtra la configuración de Microsoft Edge que se aplica a la pantalla completa de Microsoft Edge de señal digital o interactiva para que solo se use en pantallas completas con una sola aplicación de Windows 10. Elija esta configuración para abrir una URL en pantalla completa y mostrar solo el contenido de ese sitio web. En [Configurar señales digitales](/windows/configuration/setup-digital-signage) se proporciona más información sobre esta característica.
- **Exploración pública InPrivate (pantalla completa con una sola aplicación)** : filtra la configuración de Microsoft Edge que se aplica a la pantalla completa de Microsoft Edge de exploración pública InPrivate para que se use en pantallas completas con una sola aplicación de Windows 10. Se ejecuta una versión de varias pestañas de Microsoft Edge.
- **Modo normal (pantalla completa con varias aplicaciones)** : filtra la configuración de Microsoft Edge que se aplica a la pantalla completa normal de Microsoft Edge. Se ejecuta una versión completa de Microsoft Edge con todas las características de exploración.
- **Exploración pública (pantalla completa con varias aplicaciones)** : filtra la configuración de Microsoft Edge que se aplica a la exploración pública en una pantalla completa con varias aplicaciones de Windows 10.  Se ejecuta una versión de varias pestañas de Microsoft Edge InPrivate.

> [!TIP]
> Para obtener más información sobre qué hacen estas opciones, consulte [Tipos de configuración del modo de pantalla completa de Microsoft Edge](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

Este perfil de restricciones de dispositivos está directamente relacionado con el perfil de pantalla completa que se crea mediante la [configuración de pantalla completa de Windows](kiosk-settings-windows.md). En resumen:

1. Cree el perfil de [configuración de pantalla completa de Windows](kiosk-settings-windows.md) para ejecutar el dispositivo en pantalla completa. Seleccione Microsoft Edge como la aplicación y establezca Pantalla completa de Microsoft Edge en el perfil de pantalla completa.
2. Cree el perfil de restricciones de dispositivos que se describe en este artículo y configure opciones y características específicas que se permiten en Microsoft Edge. Asegúrese de elegir el mismo tipo de pantalla completa de Microsoft Edge que el que ha seleccionado en el perfil de pantalla completa ([configuración de pantalla completa de Windows](kiosk-settings-windows.md)). 

    [Configuración de la pantalla completa admitida](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) es un excelente recurso.

> [!IMPORTANT] 
> Asegúrese de asignar este perfil de Microsoft Edge a los mismos dispositivos que su perfil de pantalla completa ([configuración de pantalla completa de Windows](kiosk-settings-windows.md)).

[CSP ConfigureKioskMode](/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>Inicio de la experiencia

- **Iniciar Microsoft Edge con**: elija qué páginas se abren cuando se inicia Microsoft Edge. Las opciones son:
  - **Páginas de inicio personalizadas**: escriba las páginas de inicio, como `http://www.contoso.com`. Microsoft Edge carga las páginas de inicio que se escriben.
  - **Página Nueva pestaña**: Microsoft Edge carga todo lo que se escribe en la opción **Dirección URL de nueva pestaña**.
  - **Página de última sesión**: Microsoft Edge carga la página de la última sesión.
  - **Páginas de inicio en la configuración de la aplicación local**: Microsoft Edge empieza con la página de inicio predeterminada que define el SO.

- **Permitir al usuario cambiar las páginas de inicio**: **Sí** (valor predeterminado), permite a los usuarios cambiar las páginas de inicio. Los administradores pueden usar `EdgeHomepageUrls` para escribir las páginas de inicio que los usuarios ven de manera predeterminada al abrir Microsoft Edge. **No** evita que los usuarios cambien las páginas de inicio.
- **Permitir contenido web en una página de nueva pestaña**: si se establece en **Sí** (valor predeterminado), Microsoft Edge abre la dirección URL especificada en la opción **Dirección URL de nueva pestaña**. Si la opción **Dirección URL de nueva pestaña** está en blanco, Microsoft Edge abre la página de nueva pestaña que aparece en la configuración de Microsoft Edge. Los usuarios pueden cambiarla. Si se establece en **No**, Microsoft Edge abre una nueva pestaña con una página en blanco. Los usuarios no pueden cambiarla.
- **Dirección URL de nueva pestaña**: escriba la dirección URL que quiera abrir en la página Nueva pestaña. Por ejemplo, escriba `https://www.bing.com` o `https://www.contoso.com`.

- **Botón Inicio**: elija lo que sucede al seleccionar el botón Inicio. Las opciones son:
  - **Páginas de inicio**: abre la opción elegida en **Iniciar Microsoft Edge con**.
  - **Página Nueva pestaña**: abre la dirección URL especificada en la opción **Dirección URL de nueva pestaña**.
  - **Dirección URL del botón de inicio**: escriba la dirección URL que se va a abrir. Por ejemplo, escriba `https://www.bing.com` o `https://www.contoso.com`.
  - **Ocultar botón Inicio**: se oculta el botón Inicio.
- **Permitir a los usuarios cambiar el botón Inicio**: **Sí** permite a los usuarios cambiar el botón Inicio. Los cambios del usuario reemplazan cualquier configuración del administrador en el botón Inicio. **No** (valor predeterminado) evita que los usuarios cambien la forma en que el administrador ha configurado el botón Inicio.
- **Mostrar la página Primera experiencia de ejecución (solo móvil)** : **Sí** (valor predeterminado) muestra la página de introducción del primer uso en Microsoft Edge. **No** evita que la página de introducción aparezca la primera vez que se ejecuta Microsoft Edge. Esta característica permite que las empresas (por ejemplo, aquellas organizaciones que usan configuraciones de cero emisiones) bloqueen esta página.
- **Ubicación de la lista de URL de Primera experiencia de ejecución** (solo Windows 10 Mobile): escriba la dirección URL que señala al archivo XML que contiene las direcciones URL de la página de primera ejecución. Por ejemplo, escriba `https://www.contoso.com/sites.xml`.

- **Actualizar el explorador después del tiempo de inactividad**: escriba el número de minutos de inactividad hasta que se actualiza el explorador, de 0 a 1440 minutos. El valor predeterminado es `5` minutos. Cuando se establece en `0` (cero), el explorador no se actualiza tras estar inactivo.

  Esta configuración solo está disponible cuando se ejecuta en [Exploración pública InPrivate (pantalla completa con una sola aplicación)](#use-microsoft-edge-kiosk-mode).

- **Permitir elementos emergentes** (solo escritorio): **Sí** (valor predeterminado) permite los elementos emergentes en el explorador web. **No** evita las ventanas emergentes en el explorador.
- **Enviar el tráfico de la intranet a Internet Explorer** (solo escritorio): **Sí** permite a los usuarios abrir sitios web de intranet en Internet Explorer en lugar de Microsoft Edge. Esta opción es para la compatibilidad con versiones anteriores. **No** (valor predeterminado) permite que los usuarios usen Microsoft Edge.
- **Ubicación de la lista de sitios del modo de empresa** (solo escritorio): escriba la dirección URL que señala al archivo XML que contiene una lista de los sitios web que se abren en el modo de empresa. Los usuarios no pueden cambiar esta lista. Por ejemplo, escriba `https://www.contoso.com/sites.xml`.
- **Mensaje al abrir sitios en Internet Explorer**: use este valor para configurar Microsoft Edge de modo que muestre una notificación antes de que se abra un sitio en Internet Explorer 11. Las opciones son:
  - **No volver a mostrar este mensaje**: se usa el comportamiento predeterminado del sistema operativo, que puede que no muestre un mensaje.
  - **Mostrar mensaje de que el sitio está abierto en Internet Explorer 11**: se muestra el mensaje al abrir sitios en Internet Explorer. Los sitios se abren en IE. 
  - **Mostrar el mensaje con la opción para abrir sitios en Microsoft Edge**: muestre el mensaje al abrir sitios en Microsoft Edge. El mensaje incluye un vínculo **Keep going in Microsoft Edge** (Seguir en Microsoft Edge) para que los usuarios puedan elegir Microsoft Edge en lugar de IE.

  > [!IMPORTANT]
  > Este valor exige usar la opción **Ubicación de la lista de sitios del modo de empresa**, **Enviar el tráfico de la intranet a Internet Explorer** o ambas.

- **Permitir lista de compatibilidad de Microsoft**: **Sí** (valor predeterminado) permite usar una lista de compatibilidad de Microsoft. **No** evita la lista de compatibilidad de Microsoft en Microsoft Edge. La lista de Microsoft ayuda a que Microsoft Edge muestre de manera correcta sitios con problemas de compatibilidad conocidos.
- **Precarga de páginas de inicio y páginas de nueva pestaña**: **Sí** (valor predeterminado) usa el comportamiento predeterminado del sistema operativo, que puede ser precargar estas páginas. La carga previa minimiza el tiempo de inicio de Microsoft Edge y carga nuevas pestañas. **No** evita que Microsoft Edge cargue previamente las páginas de inicio y la página Nueva pestaña.
- **Inicio previo de páginas de inicio y página Nueva pestaña**: **Sí** (valor predeterminado) usa el comportamiento predeterminado del sistema operativo, que puede ser preiniciar estas páginas. El inicio previo ayuda al rendimiento de Microsoft Edge y minimiza el tiempo necesario para iniciar Microsoft Edge. **No** evita que Microsoft Edge inicie previamente las páginas de inicio y la página Nueva pestaña.

### <a name="favorites-and-search"></a>Favoritos y búsqueda

- **Mostrar barra de favoritos**: elija qué le ocurre a la barra de favoritos en cualquier página de Microsoft Edge. Las opciones son:
  - **En el inicio y páginas de nueva pestaña**: muestra la barra de favoritos cuando se inicia Microsoft Edge y en todas las páginas de pestaña. Los usuarios pueden cambiar esta opción.
  - **En todas las páginas**: se muestra la barra de favoritos en todas las páginas. Los usuarios no pueden cambiar esta configuración.
  - **Oculto**: se oculta la barra de favoritos en todas las páginas. Los usuarios no pueden cambiar esta configuración.
- **Permitir cambios en favoritos**: **Sí** (valor predeterminado) usa el valor predeterminado del sistema operativo, lo que permite a los usuarios cambiar la lista. **No** impide que los usuarios agreguen, importen, ordenen o modifiquen la lista de favoritos.
  - **Lista de favoritos**: agregue una lista de direcciones URL al archivo de favoritos. Por ejemplo, agregue `http://contoso.com/favorites.html`.
- **Sincronizar favoritos entre exploradores de Microsoft** (solo escritorio): **Sí** obliga a Windows a sincronizar los favoritos entre Internet Explorer y Microsoft Edge. Las incorporaciones, eliminaciones, modificaciones y cambios de orden en los favoritos se comparten entre los distintos exploradores.  **No** (valor predeterminado) usa el valor predeterminado del sistema operativo, que puede dar a los usuarios la opción de sincronizar los favoritos entre los exploradores.
- **Motor de búsqueda predeterminado**: elija el motor de búsqueda predeterminado del dispositivo. Los usuarios pueden cambiar este valor en cualquier momento. Las opciones son:
  - Motor de búsqueda de la configuración del cliente de Microsoft Edge
  - Bing
  - Google
  - Yahoo
  - Valor personalizado: en **URL de archivo XML OpenSearch**, escriba una dirección URL HTTPS con el archivo XML que incluye el nombre corto y la dirección URL del motor de búsqueda, como mínimo. Por ejemplo, escriba `https://www.contoso.com/opensearch.xml`.
- **Mostrar sugerencias de búsqueda**: **Sí** (valor predeterminado) permite que el motor de búsqueda sugiera sitios a medida que escribe frases de búsqueda en la barra de direcciones. **No** evita esta característica.
- **Permitir cambios en el motor de búsqueda**: **Sí** (valor predeterminado) permite que los usuarios agreguen nuevos motores de búsqueda o cambien el motor de búsqueda predeterminado en Microsoft Edge. Elija **No** para impedir que los usuarios personalicen el motor de búsqueda.

  Esta configuración solo está disponible cuando se ejecuta en [Modo normal (pantalla completa con varias aplicaciones)](#use-microsoft-edge-kiosk-mode).

### <a name="privacy-and-security"></a>Privacidad y seguridad

- **Permitir exploración de InPrivate**: **Sí** (valor predeterminado) permite la exploración de InPrivate en Microsoft Edge. Después de cerrar todas las pestañas de InPrivate, Microsoft Edge elimina los datos de exploración del dispositivo. **No** impide que los usuarios abran sesiones de exploración de InPrivate.
- **Guardar historial de exploración**: **Sí** (valor predeterminado) permite guardar el historial de exploración en Microsoft Edge. **No** evita guardar el historial de exploración.
- **Borrar datos de navegación al salir** (solo escritorio): **Sí** borra el historial y los datos de exploración cuando los usuarios salen de Microsoft Edge. **No** (valor predeterminado) usa el valor predeterminado del sistema operativo, que puede almacenar en caché los datos de exploración.
- **Sincronizar la configuración del explorador entre los dispositivos del usuario**: elija cómo quiere sincronizar la configuración del explorador entre dispositivos. Las opciones son:
  - **Permitir**: permita la sincronización de la configuración del explorador Microsoft Edge entre los dispositivos del usuario.
  - **Bloquear y habilitar el reemplazo de usuarios**: bloquee la sincronización de la configuración del explorador Microsoft Edge entre los dispositivos del usuario. Los usuarios pueden reemplazar esta configuración.
  - **Bloquear**: bloquee la sincronización de la configuración del explorador Microsoft Edge entre los dispositivos del usuario. Los usuarios no pueden reemplazar esta configuración.

Si "Bloquear y habilitar el reemplazo de usuarios" está seleccionado, el usuario puede invalidar la designación de administrador.

- **Permitir administrador de contraseñas**: **Sí** (valor predeterminado) permite que Microsoft Edge use automáticamente el administrador de contraseñas, lo que permite a los usuarios guardar y administrar contraseñas en el dispositivo. **No** evita que Microsoft Edge use el administrador de contraseñas.
- **Cookies**: elija cómo se administran las cookies en el explorador web. Las opciones son:
  - **Permitir**: las cookies se almacenan en el dispositivo.
  - **Bloquear todas las cookies**: las cookies no se almacenan en el dispositivo.
  - **Bloquear solo cookies de terceros**: las cookies de terceros o de asociados no se almacenan en el dispositivo.
- **Permitir autorrelleno en los formularios**: **Sí** (valor predeterminado) permite a los usuarios cambiar la configuración de Autocompletar del explorador y rellenar automáticamente los campos de formulario. **No** deshabilita la característica Autorrelleno en Microsoft Edge.
- **Enviar encabezados de no seguimiento**: **Sí** envía encabezados de no seguimiento a los sitios web que solicitan información de seguimiento (recomendado). **No** (valor predeterminado) no envía los encabezados que permiten a los sitios web realizar un seguimiento del usuario. Los usuarios pueden configurar esta opción.
- **Mostrar dirección IP de localhost para WebRTC**: **Sí** (valor predeterminado) permite que la dirección IP de localhost de los usuarios se muestre cuando se hacen llamadas telefónicas a través de este protocolo. **No** evita que la dirección IP de localhost de los usuarios se muestre. 
- **Permitir recopilación de datos para iconos dinámicos**: **Sí** (valor predeterminado) permite que Microsoft Edge recopile información de los iconos dinámicos anclados al menú Inicio. **No** evita la recopilación de esta información, lo que puede limitar la experiencia de los usuarios.
- **User can override certificate errors** (El usuario puede invalidar los errores de certificado): **Sí** (valor predeterminado) permite a los usuarios acceder a sitios web que tienen errores de Capa de sockets seguros (SSL) o Seguridad de la capa de transporte (TLS). **No** (recomendado para una mayor seguridad) evita que los usuarios accedan a sitios web con errores de SSL o TLS.

### <a name="additional"></a>Adicional

- **Permitir el explorador de Microsoft Edge** (solo Mobile): **Sí** (valor predeterminado) permite usar el explorador web Microsoft Edge en el dispositivo móvil. **No** impide que Microsoft Edge pueda usarse en los dispositivos. Si elige **No**, la demás configuración individual solo se aplica a los equipos de escritorio.
- **Permitir la lista desplegable de la barra de direcciones**: **Sí** (valor predeterminado) permite que Microsoft Edge despliegue la barra de direcciones con una lista de sugerencias. **No** evita que Microsoft Edge muestre una lista de sugerencias desplegable cuando se escribe. Cuando se establece en **No**, puede:
  - Ayudar a minimizar el ancho de banda de red entre Microsoft Edge y los servicios de Microsoft.
  - Deshabilitar **Mostrar sugerencias de búsqueda y sitios al escribir** en Microsoft Edge > Configuración.
- **Permitir modo de pantalla completa**: **Sí** (valor predeterminado) permite que Microsoft Edge use el modo de pantalla completa, que muestra solo el contenido web y oculta la interfaz de usuario de Microsoft Edge. **No** evita el modo de pantalla completa en Microsoft Edge.
- **Permitir la página about flags**: **Sí** (valor predeterminado) usa el valor predeterminado del sistema operativo, que puede permitir el acceso a la página `about:flags`. La página `about:flags` permite a los usuarios cambiar la configuración de desarrollador y habilitar características experimentales. **No** impide que los usuarios accedan a la página `about:flags` en Microsoft Edge.
- **Permitir herramientas de desarrollo**: **Sí** (valor predeterminado) permite a los usuarios usar las herramientas de desarrollo F12 para compilar y depurar páginas web de forma predeterminada. **No** impide que los usuarios usen las herramientas de desarrollo F12.
- **Permitir JavaScript**: **Sí** (valor predeterminado) permite la ejecución de scripts, como JavaScript, en el explorador Microsoft Edge. **No** evita la ejecución de scripts de Java en el explorador.
- **El usuario puede instalar extensiones**: **Sí** (valor predeterminado) permite que los usuarios instalen extensiones de Microsoft Edge en los dispositivos. **No** evita la instalación.
- **Permitir la instalación de prueba de extensiones de desarrollador**: **Sí** (valor predeterminado) usa el valor predeterminado del sistema operativo, que puede permitir la instalación de prueba. La transferencia local instala y ejecuta extensiones sin comprobar. **No** evita que Microsoft Edge transfiera localmente mediante la característica **Cargar extensiones**. No evita la transferencia local de extensiones de otras maneras, como PowerShell.
- **Required extensions** (Extensiones obligatorias): elija cuáles son las extensiones que los usuarios no pueden desactivar en Microsoft Edge. Escriba los nombres de familia de paquete y seleccione **Agregar**. [Buscar un nombre de familia de paquete (PFN) para VPN por aplicación](/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) proporciona alguna orientación.

  También puede **Importar** un archivo .csv que incluya los nombres de familia de paquete. O bien puede **Exportar** los nombres de familia de paquete que especifique.

## <a name="network-proxy"></a>Proxy de red

Estas opciones de configuración usan [NetworkProxy policy CSP](/windows/client-management/mdm/networkproxy-csp) (CSP de directiva de NetworkProxy), que también indica las ediciones de Windows compatibles.

- **Detectar automáticamente configuración de proxy**: **Bloquear** impide que los dispositivos detecten automáticamente un script de configuración automática de proxy (PAC). Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede habilitar esta característica, y los dispositivos pueden intentar detectar la ruta de acceso a un script de PAC.
- **Usar script de proxy**: seleccione **Permitir** para especificar una ruta de acceso al script de PAC para configurar el servidor proxy. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. podríaDe forma predeterminada, el sistema operativo podría no permitir especificar la dirección URL de un script de PAC.
  - **URL del script de configuración**: escriba la URL de un script de configuración automática que quiera usar para configurar el servidor proxy.
- **Usar un servidor proxy manual**: seleccione **Permitir** para escribir manualmente el nombre o la dirección IP y el número de puerto TCP de un servidor proxy. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no permitir escribir manualmente detalles de un servidor proxy.
  - **Dirección**: escriba el nombre o la dirección IP del servidor proxy.
  - **Número de puerto**: escriba el número de puerto del servidor proxy.
  - **Excepciones del proxy**: escriba las direcciones URL que no deben usar el servidor proxy. Use un punto y coma (`;`) para separar cada elemento.
  - **Omitir el servidor proxy para direcciones locales**: **Permitir** no usa el servidor proxy con las direcciones de intranet locales. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede usar un servidor proxy con direcciones locales en la intranet.

## <a name="password"></a>Contraseña

Estas opciones de configuración usan [DeviceLock policy CSP](/windows/client-management/mdm/policy-csp-devicelock) (CSP de directiva de DeviceLock), que también indica las ediciones de Windows compatibles.

- **Contraseña**: **Requerir** obliga a los usuarios a escribir una contraseña para acceder al dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir el acceso a dispositivos sin una contraseña. Solo se aplica a cuentas locales. Las contraseñas de las cuentas de dominio siguen siendo configuradas por Active Directory (AD) y Azure AD.

  [CSP de DeviceLock/DevicePasswordEnabled](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - **Tipo de contraseña requerida**: elija el tipo de contraseña. Las opciones son:
    - **No configurado**: Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que la contraseña incluya números y letras.
    - **Alfanumérica**: la contraseña debe ser una combinación de letras y números.
    - **Numérica**: la contraseña solo debe contener números.

    [CSP de DeviceLock/AlphanumericDevicePasswordRequired](/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - **Longitud mínima de la contraseña**: escriba el número mínimo de caracteres requeridos, de 4 a 16. Por ejemplo, escriba `6` para exigir al menos seis caracteres de longitud de la contraseña. De forma predeterminada, el sistema operativo puede establecerla en `4`.
  
    [CSP de DeviceLock/MinDevicePasswordLength](/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > Cuando el requisito de contraseña se cambia en un escritorio de Windows, los usuarios se ven afectados la próxima vez que inician sesión, porque es entonces cuando los dispositivos pasan de inactivos a activos. Los usuarios con contraseñas que cumplan el requisito de todos modos tendrán que cambiarlas.

  - **Número de errores de inicio de sesión antes de borrar el dispositivo**: escriba el número de contraseñas incorrectas permitidas antes de que se borre el dispositivo (11 como máximo). El número válido que escriba depende de la edición. [CSP de DeviceLock/MaxDevicePasswordFailedAttempts](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) enumera los valores admitidos. `0` (cero) puede deshabilitar la funcionalidad de borrado del dispositivo.

    Esta opción también tiene un impacto diferente en función de la edición. Para obtener información detallada de esta configuración, vea [DeviceLock/MaxDevicePasswordFailedAttempts CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) (CSP de DeviceLock/MaxDevicePasswordFailedAttempts).

  - **Máximo de minutos de inactividad hasta que se bloquea la pantalla**: especifique el tiempo durante el que un dispositivo debe estar inactivo antes de que se bloquee la pantalla. Por ejemplo, escriba `5` para bloquear los dispositivos tras estar 5 minutos inactivos. Cuando se establece en **Sin configurar**, Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede establecerla en `0` (cero), que quiere decir sin tiempo de espera.

    [CSP de DeviceLock/MaxInactivityTimeDeviceLock](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **Expiración de la contraseña (días)** : especifique el periodo de tiempo en días tras el cual debe cambiarse la contraseña del dispositivo, de 1 a 365. Por ejemplo, escriba `90` para que la contraseña caduque pasados 90 días. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede establecerla en `0` (cero), que quiere decir sin expiración.

    [CSP de DeviceLock/DevicePasswordExpiration](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **Impedir la reutilización de contraseñas anteriores**: escriba el número de contraseñas usadas previamente que no se pueden volver a usar, de 1 a 24. Por ejemplo, escriba `5` para que los usuarios no puedan establecer una nueva contraseña en su contraseña actual o en cualquiera de sus cuatro contraseñas anteriores. Cuando el valor está en blanco, Intune no cambia ni actualiza esta configuración.

    [CSP de DeviceLock/DevicePasswordHistory](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **Requerir contraseña cuando el dispositivo vuelve de un estado de inactividad** (Mobile y Holographic): **Requerir** obliga a los usuarios a escribir una contraseña para desbloquear el dispositivo después de que este haya estado inactivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría no requerir un PIN o una contraseña después de que el dispositivo haya estado inactivo.

    [CSP de DeviceLock/AllowIdleReturnWithoutPassword](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **Contraseñas sencillas**: **Bloquear** impide que los usuarios creen contraseñas sencillas, como `1234` o `1111`. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios creen contraseñas sencillas. Esta configuración también impide el uso de contraseñas de imagen.

    [CSP de DeviceLock/AllowSimpleDevicePassword](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **Cifrado automático durante AADJ**: **Bloquear** impide el cifrado automático de dispositivos BitLocker cuando los dispositivos están preparados para el primer uso y cuando están unidos a Azure AD. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede habilitar el cifrado.

  Más información sobre el [cifrado de dispositivos de BitLocker](/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [CSP Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices](/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **Directiva del Estándar federal de procesamiento de información (FIPS)** : **Permitir** usa la directiva del Estándar federal de procesamiento de información (FIPS), que es un estándar del Gobierno de los Estados Unidos para el cifrado, las operaciones hash y la firma. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede no permitir el uso de FIPS.

  [CSP Cryptography/AllowFipsAlgorithmPolicy](/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Autenticación de dispositivos con Windows Hello**: **Permitir** deja que los usuarios usen un dispositivo complementario Windows Hello, como un teléfono, una pulsera de actividad o un dispositivo IoT, para iniciar sesión en un equipo Windows 10. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede impedir que los dispositivos complementarios de Windows Hello se autentiquen.

  [CSP Authentication/AllowSecondaryAuthenticationDevice](/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Dominio de inquilino de Azure AD preferido**: escriba un nombre de dominio existente en la organización de Azure AD. Cuando los usuarios de este dominio inicien sesión, no tendrán que escribir el nombre de dominio. Por ejemplo, escriba `contoso.com`. Los usuarios del dominio `contoso.com` pueden iniciar sesión con su nombre de usuario, como `abby`, en lugar de `abby@contoso.com`.

  [CSP Authentication/PreferredAadTenantDomainName](/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>Excepciones de privacidad para cada aplicación

**Agregue** aplicaciones que deben tener un comportamiento de privacidad diferente del definido en "Privacidad determinada".

- **Nombre del paquete**: nombre de familia de paquete de la aplicación.
- **Nombre de la aplicación**: nombre de la aplicación.

### <a name="exceptions"></a>Excepciones

- **Información de la cuenta**: defina si esta aplicación puede acceder al nombre de usuario, la imagen y otra información de contacto.
- **Aplicaciones en segundo plano**: defina si esta aplicación puede ejecutarse en segundo plano.
- **Calendario**: defina si esta aplicación puede acceder al calendario.
- **Historial de llamadas**: defina si esta aplicación puede acceder al historial de llamadas.
- **Cámara**: defina si esta aplicación puede acceder a la cámara.
- **Contactos**: defina si esta aplicación puede acceder a los contactos.
- **Correo electrónico**: defina si esta aplicación puede acceder al correo electrónico.
- **Ubicación**: defina si esta aplicación puede acceder a información de ubicación.
- **Mensajería**: defina si esta aplicación puede leer o enviar mensajes de texto o MMS.
- **Micrófono**: defina si esta aplicación puede usar el micrófono.
- **Movimiento**: defina si esta aplicación puede acceder a la información de movimiento del dispositivo.
- **Notificaciones**: defina si esta aplicación puede acceder a las notificaciones.
- **Teléfono**: defina si esta aplicación puede acceder al teléfono.
- **Radios**: algunas aplicaciones usan radios (por ejemplo, Bluetooth) en el dispositivo para enviar y recibir datos, y necesitan activar o desactivar estas radios. Define si esta aplicación puede controlar estas radios.
- **Tareas**: defina si esta aplicación puede acceder a las tareas.
- **Dispositivos de confianza**: elija si esta aplicación puede usar dispositivos de confianza. Es decir, hardware ya conectado o que se proporciona con el dispositivo. Por ejemplo, use televisores, proyectores, etc. como dispositivos de confianza.
- **Comentarios y diagnósticos**: defina si esta aplicación puede acceder a la información de diagnóstico.
- **Sincronizar con dispositivos**: elija si esta aplicación puede compartir y sincronizar automáticamente información con dispositivos inalámbricos que no se emparejan explícitamente con el dispositivo.

## <a name="personalization"></a>Personalization

Estas opciones de configuración usan [personalization policy CSP](/windows/client-management/mdm/personalization-csp) (CSP de directiva de personalización), que también indica las ediciones de Windows compatibles.

- **URL de imagen de fondo de escritorio (solo equipos de escritorio)** : escriba la dirección URL de una imagen en formato .jpg, .jpeg o .png que quiera usar como fondo de escritorio de Windows. Los usuarios no pueden cambiar la imagen. Por ejemplo, escriba `https://contoso.com/logo.png`.

  Cuando se deja en blanco, Intune no cambia ni actualiza esta configuración.

## <a name="printer"></a>Impresora

- **Impresoras**: agregue impresoras usando sus nombres de host de red (nombre DNS). El sistema operativo busca e instala los controladores de impresora coincidentes correspondientes a cada impresora en el dispositivo. Si no se especifica ningún valor, Intune no cambia ni actualiza esta configuración.

  [CSP de Education/PrinterNames](/windows/client-management/mdm/policy-csp-education#education-printernames)

- **Impresora predeterminada**: Escriba el nombre de host de red (nombre DNS) de una impresora instalada para usarla como impresora predeterminada. Si no se especifica ningún valor, Intune no cambia ni actualiza esta configuración.

  [CSP de Education/DefaultPrinterName](/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **Agregar nuevas impresoras**: **Bloquear** impide que los usuarios agreguen impresoras nuevas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que se agreguen impresoras nuevas.

  [CSP de Education/PreventAddingNewPrinters](/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## <a name="privacy"></a>Privacidad

Estas opciones de configuración usan [privacy policy CSP](/windows/client-management/mdm/policy-csp-privacy) (CSP de directiva de privacidad), que también indica las ediciones de Windows compatibles.

- **Experiencia de privacidad**: **Bloquear** impide que la experiencia de privacidad se abra cuando los usuarios inicien sesión, y tampoco se abrirá en el caso de los usuarios nuevos y actualizados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [Privacy/DisablePrivacyExperience](/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **Personalización de entrada**: **Bloquear** evita el uso de voz para dictado y que se hable a Cortana y otras aplicaciones que usan el reconocimiento de voz basado en la nube de Microsoft. Está deshabilitado y los usuarios no pueden habilitar el reconocimiento de voz en línea mediante la configuración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios elijan. Si permite estos servicios, Microsoft puede recopilar datos de voz para mejorar el servicio.

  [CSP de Privacy/AllowInputPersonalization](/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **Aceptación automática de los mensajes de consentimiento del usuario sobre emparejamiento y privacidad**: seleccione **Permitir** para que Windows pueda aceptar automáticamente los mensajes de consentimiento de privacidad y emparejamiento al ejecutar aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede impedir el uso de la aceptación automática.

  [CSP de Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts](/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **Publicar las actividades del usuario**: **Bloquear** impide que las aplicaciones y el sistema operativo publiquen actividades de usuario. También impide las experiencias compartidas y la detección de recursos usados recientemente en la fuente de actividades. Las actividades de usuario realizan un seguimiento del estado de las tareas de un usuario en una aplicación o en el sistema operativo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede habilitar esta característica para que las aplicaciones puedan publicar actividades de usuario.

  [CSP de Privacy/PublishUserActivities](/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **Solo actividades locales**: si elige **Bloquear**, se impiden las experiencias compartidas y la detección de recursos usados recientemente en el conmutador de tareas, según la actividad local únicamente. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

Puede configurar la información a la que pueden tener acceso todas las aplicaciones del dispositivo. También, puede definir excepciones para cada aplicación mediante **excepciones de privacidad de cada aplicación**.

### <a name="exceptions"></a>Excepciones

- **Información de la cuenta**: defina si esta aplicación puede acceder al nombre de usuario, la imagen y otra información de contacto.
- **Aplicaciones en segundo plano**: defina si esta aplicación puede ejecutarse en segundo plano.
- **Calendario**: defina si esta aplicación puede acceder al calendario.
- **Historial de llamadas**: defina si esta aplicación puede acceder al historial de llamadas.
- **Cámara**: defina si esta aplicación puede acceder a la cámara.
- **Contactos**: defina si esta aplicación puede acceder a los contactos.
- **Correo electrónico**: defina si esta aplicación puede acceder al correo electrónico.
- **Ubicación**: defina si esta aplicación puede acceder a información de ubicación.
- **Mensajería**: defina si esta aplicación puede leer o enviar mensajes de texto o MMS.
- **Micrófono**: defina si esta aplicación puede usar el micrófono.
- **Movimiento**: defina si esta aplicación puede acceder a la información de movimiento del dispositivo.
- **Notificaciones**: defina si esta aplicación puede acceder a las notificaciones.
- **Teléfono**: defina si esta aplicación puede acceder al teléfono.
- **Radios**: algunas aplicaciones usan radios (por ejemplo, Bluetooth) en el dispositivo para enviar y recibir datos, y necesitan activar o desactivar estas radios. Define si esta aplicación puede controlar estas radios.
- **Tareas**: defina si esta aplicación puede acceder a las tareas.
- **Dispositivos de confianza**: elija si esta aplicación puede usar dispositivos de confianza. Es decir, hardware ya conectado o que se proporciona con el dispositivo. Por ejemplo, use televisores, proyectores, etc. como dispositivos de confianza.
- **Comentarios y diagnósticos**: elija si esta aplicación puede acceder a la información de diagnóstico.
- **Sincronización con dispositivos**: define si esta aplicación puede compartir y sincronizar información automáticamente con dispositivos inalámbricos que no se emparejan explícitamente con este PC, tableta o teléfono.

## <a name="projection"></a>Proyección

Estas opciones de configuración usan [WirelessDisplay policy CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay) (CSP de directiva de WirelessDisplay), que también indica las ediciones de Windows compatibles.

- **Entrada de usuario desde receptores de pantalla inalámbricos**: **Bloquear** evita la entrada de usuario desde receptores de pantalla inalámbricos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que una pantalla inalámbrica envíe entradas de teclado, ratón, lápiz y táctiles de vuelta al dispositivo de origen.

  [CSP de WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **Proyección en este equipo**: **Bloquear** impide que otros dispositivos encuentren el equipo para proyección e impide la proyección a otros dispositivos. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los dispositivos sean detectables y que se pueda proyectar a estos por encima de la pantalla de bloqueo.

  [CSP de WirelessDisplay/AllowProjectionFromPC](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **Requerir PIN para emparejamiento**: **Requerir** siempre solicita un PIN al conectar con un dispositivo de proyección. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede no requerir un PIN para emparejar el dispositivo.

  [CSP de WirelessDisplay/RequirePinForPairing](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## <a name="reporting-and-telemetry"></a>Informes y telemetría

- **Compartir los datos de uso**: elija el nivel de datos de diagnóstico que se envía. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen el nivel que se envía. De forma predeterminada, el sistema operativo podría no compartir ningún dato.
  - **Seguridad**: información necesaria para ayudar a proteger Windows, incluidos datos sobre la configuración del componente Experiencia del usuario y telemetría asociadas, la Herramienta de eliminación de software malintencionado y Microsoft Defender.
  - **Básica**: información básica del dispositivo que incluye datos relacionados con la calidad, la compatibilidad de aplicaciones, datos de uso de aplicaciones y datos del nivel de seguridad.
  - **Mejorada**: información adicional que incluye: cómo se usan Windows, Windows Server, System Center y las aplicaciones, cómo funcionan, datos avanzados de confiabilidad y datos de los niveles Seguridad y Básica.
  - **Completa**: todos los datos necesarios para identificar y ayudar a solucionar problemas, además de datos de los niveles Seguridad, Básica y Mejorada.

  [System/AllowTelemetry CSP](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry) (CSP de System/AllowTelemetry)

- **Send Microsoft Edge browsing data to Microsoft 365 Analytics** (Enviar los datos de exploración de Microsoft Edge a Microsoft 365 Analytics): para usar esta característica, establezca la configuración **Share usage data** (Compartir los datos de uso) en **Mejorado** o **Completo**. Esta característica controla los datos que Microsoft Edge envía a Microsoft 365 Analytics para los dispositivos empresariales que tienen configurado un identificador comercial. Las opciones son:
  - **No configurado**: Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede no recopilar ni enviar datos del historial de exploración.
  - **Only send intranet data** (Solo enviar datos de la intranet): permite que el administrador envíe el historial de datos de la intranet.
  - **Only send internet data** (Solo enviar datos de Internet): permite que el administrador envíe el historial de datos de Internet.
  - **Send intranet and internet data** (Enviar datos de la intranet e Internet): permite que el administrador envíe el historial de datos de la intranet e Internet.

  [Browser/ConfigureTelemetryForMicrosoft365Analytics CSP](/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics) (CSP de Browser/ConfigureTelemetryForMicrosoft365Analytics)

- **Servidor proxy de telemetría**: escriba el nombre de dominio completo (FQDN) o la dirección IP de un servidor proxy para reenviar las solicitudes de Telemetría y experiencias del usuario conectado mediante una conexión de Capa de sockets seguros (SSL). El formato de esta configuración es *servidor*:*puerto*. Si se produce un error en el proxy mencionado o si no hay ningún proxy especificado, los datos de Telemetría y experiencias del usuario conectado no se envían y permanecen en el dispositivo local.

  Si no se especifica ningún valor, Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede enviar los datos de Telemetría y experiencias del usuario conectado a Microsoft usando la configuración de proxy predeterminada.

  Formatos de ejemplo:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [System/TelemetryProxy CSP](/windows/client-management/mdm/policy-csp-system#system-telemetryproxy) (CSP de System/TelemetryProxy)

## <a name="search"></a>Búsqueda

Estas opciones de configuración usan [search policy CSP](/windows/client-management/mdm/policy-csp-search) (CSP de directiva de búsqueda), que también indica las ediciones de Windows compatibles.

- **Búsqueda segura (solo móvil)** : se controla cómo Cortana filtra el contenido para adultos en los resultados de la búsqueda. Las opciones son:
  - **Definido por el usuario**: Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen su propia configuración.
  - **Estricto**: filtrado más alto del contenido para adultos.
  - **Moderado**: filtrado moderado del contenido para adultos. No se filtran los resultados de búsqueda válidos.
- **Mostrar los resultados de los sitios web en la búsqueda**: **Bloquear** impide que los usuarios usen Windows Search para buscar en Internet, y los resultados web no aparecen reflejados en la búsqueda. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir a los usuarios buscar en Internet, y los resultados se muestran en el dispositivo.
- **Diacríticos**: **Bloquear** impide que se muestren signos diacríticos en Windows Search. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar signos diacríticos.

  [CSP de Search/AllowUsingDiacritics](/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **Detección automática del idioma**: **Bloquear** impide que Windows Search detecte automáticamente el idioma al indexar contenido o propiedades. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.

  [CSP de Search/AlwaysUseAutoLangDetection](/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **Ubicación de la búsqueda**: **Bloquear** impide que Windows Search use la ubicación. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.

  [CSP de Search/AllowSearchToUseLocation](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **Retroceso del indexador**: **Bloquear** deshabilita la característica de retroceso del indexador de búsqueda. La indexación continúa a toda velocidad, aun cuando la actividad del sistema sea alta. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede usar la lógica de retroceso para limitar la actividad de indexación cuando la actividad del sistema sea alta.

  [CSP de Search/DisableBackoff](/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **Indexación de unidad extraíble**: **Bloquear** impide que las ubicaciones en unidades extraíbles se agreguen a las bibliotecas y se indexen. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo podría permitir esta característica.

  [CSP de Search/DisableRemovableDriveIndexing](/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **Indexación con espacio en disco insuficiente**: **Habilitar** permite la indexación automática, aun cuando el espacio en disco sea bajo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede desactivar la indexación automática cuando el espacio en disco duro sea igual o inferior a 600 MB. Si los dispositivos de la organización tienen un espacio en disco limitado, establezca esta opción en **No configurado**.

  [CSP de Search/PreventIndexingLowDiskSpaceMB](/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **Consultas remotas**: **Habilitar** permite las consultas remotas del índice del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede impedir que los usuarios consulten el índice del dispositivo remotamente.

  [CSP de Search/PreventRemoteQueries](/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## <a name="start"></a>Start

Estas opciones de configuración usan [start policy CSP](/windows/client-management/mdm/policy-csp-start) (CSP de directiva de inicio), que también indica las ediciones de Windows compatibles.  

- **Diseño del menú Inicio**: Cargue un archivo XML que incluya las personalizaciones, incluido el orden en que aparecen las aplicaciones, etc. El archivo XML invalida el diseño de inicio predeterminado. Los usuarios no pueden cambiar el diseño del menú Inicio que especifique.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Start/StartLayout](/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **Anclar los sitios web a iconos del menú Inicio**: importe imágenes de Microsoft Edge. Estas imágenes se muestran como vínculos en el menú Inicio de Windows de los dispositivos de escritorio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Start/ImportEdgeAssets](/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **Desanclar aplicaciones de la barra de tareas**: **Bloquear** evita que los usuarios desanclen aplicaciones de la barra de tareas. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios desanclen aplicaciones de la barra de tareas.

  [CSP de Start/NoPinningToTaskbar](/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **Cambio rápido de usuario**: **Bloquear** evita el cambio entre usuarios que han iniciado sesión al mismo tiempo sin cerrar la sesión. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar **Cambiar usuario** en el icono de usuario.

  [CSP de Start/HideSwitchAccount](/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **La mayoría de las aplicaciones usadas**: **Bloquear** oculta las aplicaciones más usadas en el menú Inicio. También deshabilita la alternancia correspondiente en la aplicación Configuración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar las aplicaciones más usadas.

  [CSP de Start/HideFrequentlyUsedApps](/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **Aplicaciones agregadas recientemente**: **Bloquear** oculta las aplicaciones agregadas recientemente en el menú Inicio. También deshabilita la alternancia correspondiente en la aplicación Configuración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar las aplicaciones agregadas recientemente en el menú Inicio.

  [CSP de Start/HideRecentlyAddedApps](/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **Modo de pantalla de inicio**: elija el tamaño de la pantalla de inicio. Las opciones son:
  - **Definido por el usuario**: Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios pueden establecer el tamaño.
  - **Pantalla completa**: fuerza un tamaño de pantalla completa de Inicio.
  - **Pantalla parcial**: fuerza un tamaño de pantalla parcial de Inicio.

  [CSP de Start/ForceStartSize](/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **Elementos abiertos recientemente en listas de accesos directos**: **Bloquear** oculta las listas de accesos directos recientes en el menú Inicio y la barra de tareas. También deshabilita la alternancia correspondiente en la aplicación Configuración. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar los elementos abiertos recientemente en las listas de accesos directos.

  [CSP de Start/HideRecentJumplists](/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **Lista de aplicaciones**: elija cómo se muestran las listas de todas las aplicaciones. Las opciones son:
  - **Definido por el usuario**: Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen cómo se muestra la lista de aplicaciones.
  - **Contraer**: oculta la lista de todas las aplicaciones.
  - **Contraer y deshabilitar la aplicación Configuración**: oculta la lista de todas aplicaciones y deshabilita **Mostrar lista de aplicaciones en el menú Inicio** en la aplicación Configuración.
  - **Quitar y deshabilitar la aplicación Configuración**: oculta la lista de todas las aplicaciones, quita el botón de todas las aplicaciones y deshabilita **Mostrar lista de aplicaciones en el menú Inicio** en la aplicación Configuración.

  [CSP de Start/HideAppList](/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **Botón de encendido**: **Bloquear** oculta el botón de encendido en el menú Inicio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar el botón de encendido.

  [CSP de Start/HidePowerButton](/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **Icono del usuario**: **Bloquear** oculta el icono del usuario en el menú Inicio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar el icono del usuario. Configure las siguientes opciones:
  - **Bloquear**: **Bloquear** oculta la opción **Bloquear** en el icono del usuario del menú Inicio.  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar el botón **Bloquear**.
  - **Cerrar sesión**: **Bloquear** oculta la opción **Cerrar sesión** en el icono del usuario del menú Inicio. **Sin configurar** (valor predeterminado) muestra la opción **Cerrar sesión**.

  [CSP de Start/HideUserTile](/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **Apagar**: **Bloquear** oculta las opciones **Actualizar y apagar** y **Apagar** en el botón de encendido del menú Inicio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Start/HideShutDown](/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **Suspender**: **Bloquear** oculta la opción **Suspender** en el botón de encendido del menú Inicio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Start/HideSleep](/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **Hibernar**: **Bloquear** oculta la opción **Hibernar** en el botón de encendido del menú Inicio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Start/HideHibernate](/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **Cambiar cuenta**: **Bloquear** oculta la opción **Cambiar cuenta** en el icono del usuario del menú Inicio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Start/HideSwitchAccount](/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Opciones de reinicio**:  **Bloquear** oculta las opciones **Actualizar y reiniciar** y **Reiniciar** en el botón de encendido del menú Inicio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

  [CSP de Start/HideRestart](/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **Documentos en Inicio**: oculte o muestre la carpeta Documentos en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderDocuments](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **Descargas en Inicio**: oculte o muestre la carpeta Descargas en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderDownloads](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **Explorador de archivos en Inicio**: oculte o muestre Explorador de archivos en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderFileExplorer](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **Grupo Hogar en Inicio**: oculte o muestre el acceso directo Grupo Hogar en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderHomeGroup](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **Música en Inicio**: oculte o muestre la carpeta Música en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderMusic](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **Red en Inicio**: oculte o muestre Red en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderNetwork](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **Carpeta Personal en Inicio**: oculte o muestre la carpeta Personal en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderPersonalFolder](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **Imágenes en Inicio**: oculte o muestre la carpeta de imágenes en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderPictures](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **Configuración en Inicio**: oculte o muestre el acceso directo Configuración en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderSettings](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **Vídeos en Inicio**: oculte o muestre la carpeta de vídeos en el menú Inicio de Windows. Las opciones son:
  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios eligen mostrar u ocultar el acceso directo.
  - **Ocultar**: el acceso directo se oculta y la opción se deshabilita en la aplicación Configuración.
  - **Mostrar**: el acceso directo se muestra y la opción se deshabilita en la aplicación Configuración.

  [CSP de Start/AllowPinnedFolderVideos](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## <a name="microsoft-defender-smartscreen"></a>SmartScreen de Microsoft Defender

- **SmartScreen para Microsoft Edge**: **Requerir** desactiva SmartScreen de Microsoft Defender y evita que los usuarios lo activen. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, es posible que el sistema operativo active SmartScreen y permita que los usuarios lo activen y desactiven.

  Microsoft Edge usa SmartScreen de Microsoft Defender (activado) para proteger a los usuarios de software malintencionado y posibles estafas de suplantación de identidad.

  [Browser/AllowSmartScreen CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen) (CSP de Browser/AllowSmartScreen)

- **Acceso a sitios malintencionados**: **Bloquear** evita que los usuarios omitan las advertencias del filtro SmartScreen de Microsoft Defender y no permite que vayan al sitio. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir a los usuarios omitir las advertencias e ir al sitio.

  [Browser/PreventSmartScreenPromptOverride CSP](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride) (CSP de Browser/PreventSmartScreenPromptOverride)

- **Descarga de archivos no comprobados**: **Bloquear** impide que los usuarios omitan las advertencias del filtro SmartScreen de Microsoft Defender, así como descargar archivos no comprobados. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede omitir las advertencias y seguir descargando los archivos no comprobados.

  [Browser/PreventSmartScreenPromptOverrideForFiles CSP](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles) (CSP de Browser/PreventSmartScreenPromptOverrideForFiles)

## <a name="windows-spotlight"></a>Contenido destacado de Windows

Estas opciones de configuración usan [experience policy CSP](/windows/client-management/mdm/policy-csp-experience) (CSP de directiva de experiencia), que también indica las ediciones de Windows compatibles.

- **Contenido destacado de Windows**: **Bloquear** desactiva Contenido destacado de Windows en la pantalla de bloqueo, las recomendaciones de Windows, las características de consumidor de Microsoft y otras características relacionadas. Si su objetivo es minimizar el tráfico de red procedente de los dispositivos, seleccione **Sí**. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir características de contenido destacado de Windows y que puedan controlarlas los usuarios.

  [CSP de Experience/AllowWindowsSpotlight](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  Cuando está establecido en **No configurado**, también puede permitir o bloquear las siguientes opciones:

  - **Contenido destacado de Windows en la pantalla de bloqueo**: **Bloquear** evita que Contenido destacado de Windows muestre información en la pantalla de bloqueo del dispositivo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar información de contenido destacado de Windows en la pantalla de bloqueo.

    [CSP de Experience/ConfigureWindowsSpotlightOnLockScreen](/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Sugerencias de terceros en Contenido destacado de Windows**: **Bloquear** evita que Contenido destacado de Windows sugiera contenido que no haya publicado Microsoft. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir las sugerencias de contenido y de aplicación procedentes de asociados, así como mostrar las aplicaciones sugeridas en el menú Inicio y en las sugerencias de Windows.

    [CSP de Experience/AllowThirdPartySuggestionsInWindowsSpotlight](/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **Características de consumidor**: **Bloquear** desactiva experiencias que suelen ser para consumidores, como las sugerencias de inicio, las notificaciones de suscripción, la instalación de aplicaciones tras la configuración rápida y los iconos de redireccionamiento. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración.

    [CSP de Experience/AllowWindowsConsumerFeatures](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Sugerencias de Windows**: **Bloquear** deshabilita las recomendaciones emergentes de Windows. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que se muestren sugerencias de Windows.

    [CSP de Experience/AllowWindowsTips](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **Contenido destacado de Windows en el centro de actividades**: **Bloquear** evita que las notificaciones de Contenido destacado de Windows aparezcan en el centro de actividades. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede mostrar notificaciones en el centro de actividades que sugieran aplicaciones o características para ayudar a los usuarios a ser más productivos en Windows.

    [CSP de Experience/AllowWindowsSpotlightOnActionCenter](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Personalización de Contenido destacado de Windows**: **Bloquear** impide que Windows use datos de diagnóstico para proporcionar experiencias personalizadas a los usuarios. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir a Microsoft usar datos de diagnóstico para proporcionar recomendaciones, sugerencias y ofertas personalizadas para adaptar Windows a las necesidades del usuario.

    [CSP de Experience/AllowTailoredExperiencesWithDiagnosticData](/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Experiencia de bienvenida de Windows**: **Bloquear** desactiva la característica de experiencia de bienvenida de Windows de Contenido destacado de Windows. La experiencia de bienvenida de Windows no muestra si hay actualizaciones y cambios para Windows y sus aplicaciones. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que la experiencia de bienvenida de Windows muestre a los usuarios información sobre características nuevas o actualizadas.

    [CSP de Experience/AllowWindowsSpotlightWindowsWelcomeExperience](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## <a name="microsoft-defender-antivirus"></a>Antivirus de Microsoft Defender

Estas opciones de configuración usan [defender policy CSP](/windows/client-management/mdm/policy-csp-defender) (CSP de directiva de Defender), que también indica las ediciones de Windows compatibles.

- **Supervisión en tiempo real**: **Habilitar** activa la detección de malware, spyware y otro tipo de software no deseado en tiempo real. Los usuarios no pueden desactivarlo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo activa esta característica y permite a los usuarios cambiarla.

  Si habilita esta opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Supervisión de comportamiento**: **Habilitar** activa la supervisión del comportamiento y comprueba determinados patrones conocidos de actividad sospechosa en los dispositivos. Los usuarios no pueden desactivar la supervisión de comportamiento. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede activar la supervisión de comportamiento y permitir a los usuarios cambiarla.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowBehaviorMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Sistema de inspección de red (NIS)** : NIS ayuda a proteger los dispositivos contra las vulnerabilidades de seguridad basadas en red. Usa las firmas de vulnerabilidades conocidas de Microsoft Endpoint Protection Center para ayudar a detectar y bloquear el tráfico malintencionado.

  - **Habilitar**: activa la protección y el bloqueo de red. Los usuarios no pueden desactivarlo. Cuando se habilita, los usuarios no pueden conectarse a vulnerabilidades conocidas.

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo activa NIS y permite a los usuarios cambiarlo.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Examinar todas las descargas**: **Habilitar** activa esta opción y Defender examina todos los archivos descargados de Internet. Los usuarios no pueden desactivar esta opción. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede activar esta opción y permitir a los usuarios cambiarla.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowIOAVProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Examinar scripts cargados en exploradores web de Microsoft**: **Habilitar** permite que Defender analice los scripts que se usan en Internet Explorer. Los usuarios no pueden desactivar esta opción. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede activar esta opción y permitir a los usuarios cambiarla.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowScriptScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Acceso de usuario final a Defender**: **Bloquear** oculta la interfaz de usuario de Microsoft Defender a los usuarios. También se suprimen todas las notificaciones de Microsoft Defender. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir el acceso de los usuarios a la interfaz de usuario de Microsoft Defender y les permite cambiarla.

  Si bloquea la opción y luego la vuelve a cambiar a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  Cuando esta configuración se modifica, surte efecto la próxima vez que el dispositivo se reinicie.

  [CSP de Defender/AllowUserUIAccess](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Intervalo de actualización de inteligencia de seguridad (en horas)** : especifique el intervalo conforme al que Defender busca nueva inteligencia de seguridad, de 0 a 24. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. El valor predeterminado del sistema operativo puede buscar actualizaciones cada 8 horas.
  - **No comprobar**: Defender no busca nuevas actualizaciones de inteligencia de seguridad.
  - **1-24**: `1` busca cada hora, `2` busca cada dos horas, `24` busca cada día, etc.
  
  [CSP de Defender/SignatureUpdateInterval](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Supervisar la actividad de archivos y programas**: Permite que Defender supervise la actividad de archivos y programas en los dispositivos. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. El valor predeterminado del sistema operativo puede supervisar todos los archivos.
  - **Supervisión deshabilitada**
  - **Supervisar todos los archivos**
  - **Supervisar solo los archivos entrantes**
  - **Supervisar solo los archivos salientes**

  [CSP de Defender/RealTimeScanDirection](/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Días antes de eliminar el malware en cuarentena**: siga realizando el seguimiento de malware resuelto durante el número de días especificado para poder comprobar de forma manual los dispositivos previamente afectados. 

  Si no configura esta opción o la establece en `0`días, el malware permanece en la carpeta de cuarentena y no se quita automáticamente. Cuando se establece en `90`, los elementos en cuarentena se almacenan durante 90 días en el sistema y luego se eliminan.

  [CSP de Defender/DaysToRetainCleanedMalware](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Límite de uso de la CPU durante un examen**: limite la cantidad de CPU que pueden usar los exámenes, de `0` a `100` por ciento. De forma predeterminada, el sistema operativo puede establecerla en 50 %.
- **Examinar archivos de almacenamiento**: **Habilitar** activa Defender para que examine los archivos de almacenamiento, como Zip o Cab. Los usuarios no pueden desactivar esta opción. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede activar este examen y permitir a los usuarios cambiarlo.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowArchiveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Examinar mensajes de correo entrante**: **Habilitar** permite que Defender examine los mensajes de correo electrónico en cuanto llegan a los dispositivos. Cuando se habilita, el motor analiza el buzón y los archivos de correo a fin de analizar el cuerpo del correo y los datos adjuntos. Puede examinar formatos .pst (Outlook), .dbx, .mbx, MIME (Outlook Express) y BinHex (Mac).

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo desactiva este análisis y permite a los usuarios cambiarlo.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowEmailScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Examinar unidades extraíbles durante un examen completo**: **Habilitar** activa los exámenes de unidades extraíbles de Defender durante un examen completo. Los usuarios no pueden desactivar esta opción. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que Defender examine unidades extraíbles, como dispositivos USB, y permitir a los usuarios cambiar esta configuración.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Durante un examen rápido, es posible que se analicen las unidades extraíbles.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowFullScanRemovableDriveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Examinar unidades de red asignadas durante un examen completo**: **Habilitar** permite que Defender examine archivos en unidades de red asignadas. Si los archivos de la unidad son de solo lectura, Defender no puede quitar el malware que se encuentre en ellos. Los usuarios no pueden desactivar esta opción.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo activa esta característica y permite a los usuarios cambiarla.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente. 

  Durante un examen rápido, es posible que se examinen las unidades de red asignadas.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowFullScanOnMappedNetworkDrives](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Examinar archivos abiertos desde carpetas de red**: **Habilitar** permite que Defender examine archivos abiertos desde carpetas de red o unidades de red compartidas, como los archivos a los que se accede desde una ruta de acceso UNC. Los usuarios no pueden desactivar esta opción. Si los archivos de la unidad son de solo lectura, Defender no puede quitar el malware que se encuentre en ellos.

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo examina los archivos abiertos desde carpetas de red y permite a los usuarios cambiar este comportamiento.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowScanningNetworkFiles](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Protección de la nube**: **Habilitar** permite que Microsoft Active Protection Service reciba información relativa a la actividad de malware de los dispositivos que administra. Los usuarios no pueden cambiar esta configuración. 

  Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo permite a Microsoft Active Protection Service recibir información y a los usuarios cambiar esta configuración.

  Si habilita la opción y luego vuelve a cambiarla a **No configurado**, Intune la deja en el estado configurado previamente.

  Intune no desactiva esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Preguntar a los usuarios antes de enviar muestras**: se controla si los archivos potencialmente malintencionados que podrían requerir un análisis en mayor profundidad se envían automáticamente a Microsoft. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. El valor predeterminado del sistema operativo puede enviar muestras seguras automáticamente.
  - **Preguntar siempre**
  - **Preguntar antes de enviar datos personales**
  - **No enviar datos nunca**
  - **Enviar todos los datos sin preguntar**: los datos se envían automáticamente.

  [CSP de Defender/SubmitSamplesConsent](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Hora a la que se realizará un examen rápido diario**: elija la hora a la que se va a ejecutar un examen rápido diario. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede ejecutar este examen a las 2 a.m.

  Si quiere personalizar más esta opción, configure el valor **Tipo de examen del sistema para realizar**.

  [Defender/ScheduleQuickScanTime CSP](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Tipo de examen del sistema para realizar**: programe un examen del sistema, incluido el nivel de examen, así como el día y la hora en que se va a ejecutar el examen. Las opciones son:
  - **No configurado**: Intune no cambia ni actualiza esta configuración. no se fuerza ninguna opción. Los usuarios pueden ejecutar exámenes manualmente según necesiten o quieran en sus dispositivos.
  - **Deshabilitar**: deshabilita cualquier examen del sistema en los dispositivos. Elija esta opción si usa una solución antivirus de un asociado que examina los dispositivos.
  - **Examen rápido**: examina ubicaciones comunes donde podría haber malware registrado, como las claves del Registro y las carpetas de inicio de Windows conocidas.
    - **Día programado**: elija el día en el que se va a ejecutar el examen.
    - **Hora programada**: elija la hora a la que se va a ejecutar el examen.
  - **Examen completo**: examina ubicaciones comunes donde podría haber malware registrado y también examina todos los archivos y las carpetas del dispositivo.
    - **Día programado**: elija el día en el que se va a ejecutar el examen.
    - **Hora programada**: elija la hora a la que se va a ejecutar el examen.

  > [!TIP]
  > Esta configuración podría entrar en conflicto con la configuración **Hora a la que se realizará un examen rápido diario**. Algunas recomendaciones:  
  >
  > - Si quiere programar un examen rápido diario y un examen completo semanal:
  >   1. Configure el valor **Hora a la que se realizará un examen rápido diario**.
  >   2. Configure **Tipo de examen del sistema para realizar** para realizar un examen completo.
  > 
  > - Si solo quiere hacer un examen rápido diario (sin examen completo), use cualquiera de estas opciones: **Hora a la que se realizará un examen rápido diario** o **Tipo de examen del sistema para realizar**. Por ejemplo, para ejecutar un examen rápido todos los martes a las 6:00, configure el valor **Tipo de examen del sistema para realizar**.
  > 
  > - No configure el valor **Hora a la que se realizará un examen rápido diario** simultáneamente con **Tipo de examen del sistema para realizar** establecido en **Examen rápido**. Esta configuración podría entrar en conflicto y puede que no se ejecute un examen.

  [CSP Defender/ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [CSP Defender/ScheduleScanDay](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [CSP Defender/ScheduleScanTime](/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **Detectar aplicaciones potencialmente no deseadas**: Esta característica identifica las aplicaciones potencialmente no deseadas e impide que se puedan descargar e instalar en la red. Estas aplicaciones no se consideran virus, malware ni ningún otro tipo de amenaza, pero pueden realizar acciones en los puntos de conexión que pueden afectar a su uso o rendimiento. Elija el nivel de protección cuando Windows detecte aplicaciones potencialmente no deseadas. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, Microsoft Defender puede deshabilitar esta característica.
  - **Desactivada**: protección de PUA desactivada.
  - **Habilitar**: Microsoft Defender detecta las aplicaciones potencialmente no deseadas, y los elementos detectados se bloquean. Estos elementos se muestran en el historial junto con otras amenazas.
  - **Auditar**: Microsoft Defender detecta las aplicaciones potencialmente no deseadas, pero no realiza ninguna acción. Puede revisar la información sobre las aplicaciones contra las que Microsoft Defender tomaría medidas. Por ejemplo, busque eventos creados por Microsoft Defender en el Visor de eventos.

  Para obtener más información sobre aplicaciones potencialmente no deseadas, vea [Detectar y bloquear aplicaciones potencialmente no deseadas](/windows/security/threat-protection/microsoft-defender-antivirus/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus).

  [CSP de Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Enviar consentimiento de muestras**: actualmente, esta opción no tiene ningún efecto. No la use. Puede que se quite en una versión futura.

- **Protección de acceso**: **Bloquear** impide el análisis de archivos a los que se ha accedido o que se han descargado. Los usuarios no pueden activarlo. Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede habilitar esta característica y permite a los usuarios cambiarla.

  Si bloquea la opción y luego la vuelve a cambiar a **Sin configurar**, Intune la deja en el estado configurado previamente por el sistema operativo.

  Intune no activa esta característica. Para deshabilitarla, use un URI personalizado.

  [CSP de Defender/AllowOnAccessProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Acciones para amenazas de malware detectadas**: seleccione **Habilitar** para elegir las acciones que quiere que Defender realice en cada nivel de amenaza que detecte (bajo, moderado, alto y grave). Cuando se establece en **Sin configurar** (valor predeterminado), Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede dejar que Microsoft Defender elija la mejor opción.

  Si la establece en **Habilitar**, seleccione la acción:
  
  - **Limpiar**
  - **Cuarentena**
  - **Quitar**
  - **Permitir**
  - **Definido por el usuario**
  - **Bloquear**

  Si la acción no es posible, Microsoft Defender elige la mejor opción para garantizar que se corrija la amenaza.

  [CSP de Defender/ThreatSeverityDefaultAction](/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Exclusiones del antivirus de Microsoft Defender

Puede excluir determinados archivos de los exámenes de antivirus de Microsoft Defender mediante la modificación de las listas de exclusión. **Por lo general, no es necesario aplicar exclusiones**. El antivirus de Microsoft Defender incluye una serie de exclusiones automáticas basadas en comportamientos de sistema operativo conocidos y en archivos de administración típicos, como los que se usan en la administración empresarial, la administración de bases de datos y otros escenarios y situaciones empresariales.

> [!WARNING]
> **La definición de exclusiones reduce la protección que ofrece el antivirus de Microsoft Defender**. Evalúe siempre los riesgos asociados a la implementación de exclusiones. Excluya solo los archivos que sabe que no son malintencionados.

- **Archivos y carpetas para excluir de exámenes y protección en tiempo real**: Agrega uno o varios archivos y carpetas como **C:\Path** o **%ProgramFiles%\Path\filename.exe** a la lista de exclusiones. Estos archivos y carpetas no se incluyen en ningún examen en tiempo real ni programado.
- **Extensiones de archivo para excluir de exámenes y protección en tiempo real**: Agrega una o varias extensiones de archivo como **jpg** o **txt** a la lista de exclusiones. Los archivos con estas extensiones no se incluyen en los exámenes en tiempo real ni programados.
- **Procesos para excluir de exámenes y protección en tiempo real**: Agrega uno o varios procesos del tipo **.exe**, **.com** o **.scr** a la lista de exclusiones. Estos procesos no se incluyen en los exámenes en tiempo real ni programados.

## <a name="power-settings"></a>Configuración de energía

Estas opciones de configuración usan [CSP de directiva de energía](/windows/client-management/mdm/policy-csp-power), que también indica las ediciones de Windows compatibles.

### <a name="battery"></a>Batería

- **Nivel de batería para activar el ahorro de energía**: si el dispositivo usa la energía de la batería, especifique el nivel de carga para que se active el ahorro de energía, de 0 a 100. Escriba un valor de porcentaje que indique el nivel de carga de la batería. Por ejemplo, si se establece en `80`, el ahorro de energía se activa cuando la batería tiene una carga del 80 % o menos disponible.

  Si no se especifica ningún valor, Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede establecerla en 70 %.

  [CSP de Power/EnergySaverBatteryThresholdOnBattery](/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Cerrar la tapa (solo móvil)** : si el dispositivo usa la energía de la batería, decida lo que sucede cuando se cierra la tapa. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios controlen esta configuración.
  - **Ninguna acción**: el dispositivo permanece encendido y continúa usando la energía de la batería.
  - **Suspender**: el dispositivo entra en modo de suspensión y usa una pequeña cantidad de carga de la batería. El equipo sigue encendido y las aplicaciones y los archivos abiertos se almacenan en la memoria de acceso aleatorio (RAM).
  - **Hibernar**: el dispositivo entra en modo de hibernación. Las aplicaciones y los archivos abiertos se almacenan en el disco duro y el dispositivo se apaga.
  - **Apagar**: el dispositivo se apaga. Las aplicaciones y los archivos abiertos se cierran sin guardar.

  [CSP de Power/SelectLidCloseActionOnBattery](/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Botón de encendido**: si el dispositivo usa la energía de la batería, decida lo que ocurre cuando se selecciona el botón de encendido. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios controlen esta configuración.
  - **Ninguna acción**: el dispositivo permanece encendido y continúa usando la energía de la batería.
  - **Suspender**: el dispositivo entra en modo de suspensión y usa una pequeña cantidad de carga de la batería. El equipo sigue encendido y las aplicaciones y los archivos abiertos se almacenan en la memoria de acceso aleatorio (RAM).
  - **Hibernar**: el dispositivo entra en modo de hibernación. Las aplicaciones y los archivos abiertos se almacenan en el disco duro y el dispositivo se apaga.
  - **Apagar**: el dispositivo se apaga. Las aplicaciones y los archivos abiertos se cierran sin guardar.

  [CSP de Power/SelectPowerButtonActionOnBattery](/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Botón de suspensión**: si el dispositivo usa la energía de la batería, decida lo que ocurre cuando se selecciona el botón de suspensión. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios controlen esta configuración.
  - **Ninguna acción**: el dispositivo permanece encendido y continúa usando la energía de la batería.
  - **Suspender**: el dispositivo entra en modo de suspensión y usa una pequeña cantidad de carga de la batería. El equipo sigue encendido y las aplicaciones y los archivos abiertos se almacenan en la memoria de acceso aleatorio (RAM).
  - **Hibernar**: el dispositivo entra en modo de hibernación. Las aplicaciones y los archivos abiertos se almacenan en el disco duro y el dispositivo se apaga.
  - **Apagar**: el dispositivo se apaga. Las aplicaciones y los archivos abiertos se cierran sin guardar.

  [CSP de Power/SelectSleepButtonActionOnBattery](/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Suspensión híbrida**: si el dispositivo está usando la energía de la batería, elija si permitir o no el modo de suspensión híbrida.

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios controlen esta configuración.
  - **Habilitar**: los dispositivos pueden entrar en modo de suspensión híbrida. Las aplicaciones y los archivos abiertos se almacenan en la memoria de acceso aleatorio (RAM) y en el disco duro. Usa una pequeña cantidad de carga de la batería.
  - **Deshabilitar**: impide que los dispositivos pasen al modo de suspensión híbrida.

  [CSP de Power/TurnOffHybridSleepOnBattery](/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>PluggedIn

- **Nivel de batería para activar el ahorro de energía**: si el dispositivo está enchufado, especifique el nivel de carga para que se active el ahorro de energía, de 0 a 100. Escriba un valor de porcentaje que indique el nivel de carga de la batería. Por ejemplo, si se establece en `80`, el ahorro de energía se activa cuando la batería tiene una carga del 80 % o menos disponible.

  Si no se especifica ningún valor, Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede establecerla en 70 %.

  [CSP de Power/EnergySaverBatteryThresholdPluggedIn](/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Cerrar la tapa (solo móvil)** : si el dispositivo está enchufado, decida lo que ocurre cuando se cierra la tapa. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Ninguna acción**: el dispositivo permanece encendido.
  - **Suspender**: el dispositivo entra en modo de suspensión. El equipo sigue encendido y las aplicaciones y los archivos abiertos se almacenan en la memoria de acceso aleatorio (RAM).
  - **Hibernar**: el dispositivo entra en modo de hibernación. Las aplicaciones y los archivos abiertos se almacenan en el disco duro y el dispositivo se apaga.
  - **Apagar**: el dispositivo se apaga. Las aplicaciones y los archivos abiertos se cierran sin guardar.
  
    [CSP de Power/SelectLidCloseActionPluggedIn](/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Botón de encendido**: si el dispositivo está enchufado, decida lo que ocurre cuando se selecciona el botón de encendido. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Ninguna acción**: el dispositivo permanece encendido.
  - **Suspender**: el dispositivo entra en modo de suspensión. El equipo sigue encendido y las aplicaciones y los archivos abiertos se almacenan en la memoria de acceso aleatorio (RAM).
  - **Hibernar**: el dispositivo entra en modo de hibernación. Las aplicaciones y los archivos abiertos se almacenan en el disco duro y el dispositivo se apaga.
  - **Apagar**: el dispositivo se apaga. Las aplicaciones y los archivos abiertos se cierran sin guardar.

  [CSP de Power/SelectPowerButtonActionPluggedIn](/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Botón de suspensión**: si el dispositivo está enchufado, decida lo que ocurre cuando se selecciona el botón de suspensión. Las opciones son:

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración.
  - **Ninguna acción**: el dispositivo permanece encendido.
  - **Suspender**: el dispositivo entra en modo de suspensión. El equipo sigue encendido y las aplicaciones y los archivos abiertos se almacenan en la memoria de acceso aleatorio (RAM).
  - **Hibernar**: el dispositivo entra en modo de hibernación. Las aplicaciones y los archivos abiertos se almacenan en el disco duro y el dispositivo se apaga.
  - **Apagar**: el dispositivo se apaga. Las aplicaciones y los archivos abiertos se cierran sin guardar.

  [CSP de Power/SelectSleepButtonActionPluggedIn](/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Suspensión híbrida**: si el dispositivo está enchufado, elija si permitir o no el modo de suspensión híbrida.

  - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. De forma predeterminada, el sistema operativo puede permitir que los usuarios controlen esta configuración.
  - **Habilitar**: los dispositivos pueden entrar en modo de suspensión híbrida. Las aplicaciones y los archivos abiertos se almacenan en la memoria de acceso aleatorio (RAM) y en el disco duro.
  - **Deshabilitar**: impide que los dispositivos pasen al modo de suspensión híbrida.

  [CSP de Power/TurnOffHybridSleepPluggedIn](/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Pasos siguientes

Para obtener detalles técnicos adicionales sobre cada configuración y sobre las ediciones de Windows compatibles, consulte [Windows 10 Policy CSP Reference](/windows/client-management/mdm/policy-configuration-service-provider) (Referencia sobre el CSP de directivas de Windows 10).

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).