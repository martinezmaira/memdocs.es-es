---
title: Configuración de la directiva antivirus de Windows 10 para la experiencia de Seguridad de Windows para Intune | Microsoft Docs
description: Configuración de la directiva antivirus de seguridad de los puntos de conexión para la aplicación Seguridad de Windows en Microsoft Intune
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
ms.openlocfilehash: 089303b76f674d47767afdff72341d09f7f227d4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431740"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Configuración del perfil de la experiencia de Seguridad de Windows en Microsoft Intune

Vea la configuración de la directiva antivirus que puede establecer para el perfil de **Experiencia de Seguridad de Windows** para Windows 10 en Microsoft Intune como parte de una [directiva de seguridad de puntos de conexión](../protect/endpoint-security-policy.md).

**Seguridad de Windows**

- **Habilitar la protección contra alteraciones para impedir que Microsoft Defender se deshabilite**  
  [Evitar cambios de la configuración de seguridad con Protección contra alteraciones](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Sin configurar** (*valor predeterminado*): cuando existe el estado *Habilitar* o *Deshabilitar* en un cliente, la implementación de *Sin configurar* no tiene ningún efecto en la configuración. 
  - **Habilitar**: habilita las restricciones de Protección contra alteraciones. Para cambiar el estado de habilitado o deshabilitado, implemente el valor opuesto para que surta efecto.
  - **Deshabilitar**: deshabilita las restricciones de Protección contra alteraciones. Para cambiar el estado de habilitado o deshabilitado, implemente el valor opuesto para que surta efecto.

- **Ocultar el área de protección contra virus y amenazas en la aplicación Seguridad de Windows**  
  CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso de usuario y las notificaciones.
  - **Sí**: se oculta a los usuarios finales el área de protección contra virus y amenazas en la aplicación Seguridad de Windows. Se suprimen las notificaciones relacionadas con la protección contra virus y amenazas.

  - **Ocultar la opción de recuperación de datos por ataque de ransomware en la aplicación Seguridad de Windows**  
    CSP: [](https://go.microsoft.com/fwlink/?linkid=873664)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso de usuario y las notificaciones.
  - **Sí**: se oculta a los usuarios finales el área de recuperación de datos por ataque de ransonware en la aplicación Seguridad de Windows. Se suprimen las notificaciones relacionadas con el ransomware.

- **Ocultar el área Protección de cuentas en la aplicación Seguridad de Windows**  
  CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso de usuario y las notificaciones.
  - **Sí**: se oculta a los usuarios finales el área de protección de cuentas en la aplicación Seguridad de Windows. Se suprimen las notificaciones relacionadas con la protección de cuentas.

- **Ocultar el área de firewall y protección de red en la aplicación Seguridad de Windows**  
  CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso de usuario y las notificaciones.
  - **Sí**: se oculta a los usuarios finales el área de firewall y protección de red en la aplicación Seguridad de Windows. Se suprimen las notificaciones relacionadas con el firewall y la protección de red.

- **Ocultar el área de control de aplicaciones y explorador en la aplicación Seguridad de Windows**  
  CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso de usuario y las notificaciones.
  - **Sí**: se oculta a los usuarios finales el área de control de aplicaciones y explorador en la aplicación Seguridad de Windows. Se suprimen las notificaciones relacionadas con el control de aplicaciones y explorador.

- **Ocultar el área Seguridad de dispositivos en la aplicación Seguridad de Windows**  
  CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso de usuario y las notificaciones.
  - **Sí**: se oculta a los usuarios finales el área de protección de hardware en la aplicación Seguridad de Windows. Se suprimen las notificaciones relacionadas con la protección de hardware.
  
- **Ocultar el área Rendimiento y estado del dispositivo en la aplicación Seguridad de Windows**  
  CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso de usuario y las notificaciones.
  - **Sí**: se oculta a los usuarios finales el área de rendimiento y estado del dispositivo en la aplicación Seguridad de Windows. Se suprimen las notificaciones relacionadas con el rendimiento y estado del dispositivo.

- **Ocultar el área Opciones de familia en la aplicación Seguridad de Windows**  
  CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso de usuario y las notificaciones.
  - **Sí**: se oculta a los usuarios finales el área de opciones de familia en la aplicación Seguridad de Windows. Además, se suprimen las notificaciones relacionadas con las opciones de familia.

- **Notificaciones de la aplicación Seguridad de Windows**  
  CSP: [](https://go.microsoft.com/fwlink/?linkid=873675)

  Use esta opción para bloquear las notificaciones de Seguridad de Windows para los usuarios relacionadas con todos los valores de características anteriores. Como alternativa, puede administrar las notificaciones de la aplicación Seguridad de Windows por característica mediante los valores siguientes.

  - **Sin configurar** (*valor predeterminado*): se permiten todas las notificaciones de la aplicación Seguridad de Windows que no están controladas por otro valor.
  - **Bloquear las notificaciones no críticas**: se bloquean notificaciones, como las finalizaciones de exámenes.
  - **Bloquear todas las notificaciones**: se bloquean las notificaciones críticas y no críticas de todas las características de Seguridad de Windows.

- **Ocultar el icono de Seguridad de Windows en el área de notificación**  
  CSP: [HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  Para que este valor surta efecto, el usuario debe cerrar la sesión y volver a iniciarla, o bien reiniciar el equipo.
  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es mostrar el icono.
  - **Sí**: se oculta el icono de Seguridad de Windows en la bandeja del sistema de los usuarios.
  
- **Deshabilitar la opción Quitar TPM en la aplicación Seguridad de Windows**  
  CSP: [DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es permitir el acceso al botón.
  - **Sí**: se deshabilita el acceso al botón Quitar TPM en la aplicación Seguridad de Windows.

- **Pedir a los usuarios que actualicen el firmware de TPM si se detecta una vulnerabilidad**  
  CSP: [DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **Sin configurar** (*valor predeterminado*): la opción devuelve al valor predeterminado del cliente, que es no preguntar a los usuarios.
  - **Sí**: permite a Windows preguntar a los usuarios finales cuando se detecta una posible vulnerabilidad en el firmware de TPM. Se les anima a ejecutar actualizaciones del firmware para corregir la vulnerabilidad.

- **Información de contacto de soporte técnico de la organización**  
  CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  Indique dónde quiere que se muestre la información de la organización de TI en las notificaciones y la aplicación Seguridad de Windows.
  - **Sin configurar** (*valor predeterminado*).
  - **Mostrar en la aplicación y en las notificaciones**
  - **Mostrar solo en la aplicación**
  - **Mostrar solo en las notificaciones**