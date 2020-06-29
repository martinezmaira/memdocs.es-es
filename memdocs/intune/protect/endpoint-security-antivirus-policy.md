---
title: Administración de las opciones de antivirus con directivas de seguridad de puntos de conexión en Microsoft Intune | Microsoft Docs
description: Configure e implemente directivas y use informes para los dispositivos administrados con la directiva de antivirus de seguridad de puntos de conexión en Microsoft Endpoint Manager.
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
ms.openlocfilehash: bfefdee7e949faf9e484ea20e7fc203ee72a9784
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879654"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Directiva de antivirus para la seguridad de puntos de conexión en Intune

Las directivas de antivirus de seguridad de puntos de conexión de Intune ayudan a los administradores de seguridad a centrarse en administrar el grupo diferenciado de opciones de antivirus para dispositivos administrados. Para usar una directiva de antivirus, integre Intune con Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) como una solución de Mobile Threat Defense.

La directiva de antivirus incluye varios perfiles. Cada uno de ellos contiene solo la configuración pertinente para el antivirus de ATP de Microsoft Defender para macOS, Windows 10 o para la experiencia de usuario en la aplicación Seguridad de Windows en dispositivos Windows 10.

Encontrará las directivas de antivirus en **Administrar**, en el nodo Seguridad de los puntos de conexión del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Las directivas de antivirus incluyen la misma configuración que se encuentra en los perfiles de *Endpoint Protection* o *restricción de dispositivos* para la directiva de [configuración de dispositivos](../configuration/device-profile-create.md) y son similares a la configuración de la directiva de [cumplimiento de dispositivos](../protect/device-compliance-get-started.md). Aun así, esos tipos de directivas incluyen categorías adicionales de configuración que no están relacionadas con el antivirus. La configuración adicional puede complicar la tarea de configurar el antivirus. Además, las opciones de configuración que se encuentra en la directiva de antivirus para macOS no están disponibles en los demás tipos de directivas. El perfil de antivirus de macOS reemplaza la necesidad de configurar las opciones mediante archivos `.plist`.

## <a name="prerequisites-for-antivirus-policy"></a>Requisitos previos de la directiva de antivirus

- **macOS**
  - Cualquier versión compatible de macOS
  - Para que Intune administre la configuración de antivirus en un dispositivo, se debe instalar ATP de Microsoft Defender en ese dispositivo. Vea [ATP de Microsoft Defender para macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (en la documentación de ATP de Microsoft Defender)

- **Windows 10 y versiones posteriores**
  - Para que Intune administre la configuración de antivirus en un dispositivo, se debe instalar ATP de Microsoft Defender en ese dispositivo. Vea [Uso de ATP de Microsoft Defender para Windows](../protect/advanced-threat-protection.md) en la documentación de Intune.
  - La aplicación Seguridad de Windows está instalada en todos los dispositivos que ejecutan Windows 10 y no conlleva ningún requisito previo adicional.

## <a name="antivirus-profiles"></a>Perfiles de antivirus

**Perfiles de macOS**:

- **Antivirus**: administre la [configuración de directivas antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) para macOS.

  Cuando use [ATP de Microsoft Defender para Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac), puede configurar e implementar la configuración de antivirus en los dispositivos macOS administrados mediante Intune, en lugar de configurar estas opciones mediante archivos `.plist`.

**Perfiles de Windows 10**:

- **Antivirus de Microsoft Defender**: administre la [configuración de directivas antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) para Windows 10.

  Antivirus de Defender es el componente de protección de última generación de Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender). La protección de última generación aúna el aprendizaje automático, el análisis de macrodatos, la investigación detallada sobre la resistencia a las amenazas y la infraestructura en la nube para proteger los dispositivos de la organización empresarial.

  El perfil de *Antivirus de Microsoft Defender* es una instancia independiente de la configuración de antivirus que se encuentra en el *perfil de restricción de dispositivos* para la directiva de configuración de dispositivos.
  
  A diferencia de la configuración de antivirus de un *perfil de restricción de dispositivos*, puede usar esta configuración con dispositivos administrados conjuntamente. Para usar esta configuración, el [control deslizante de la carga de trabajo de administración conjunta](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) para Endpoint Protection debe establecerse en Intune.

- **Experiencia de seguridad de Windows**: administre la [configuración de la aplicación Seguridad de Windows](../protect/antivirus-security-experience-windows-settings.md) que los usuarios finales pueden ver en el centro de seguridad de Microsoft Defender y las notificaciones que reciben. Varias características de seguridad de Windows usan la aplicación Seguridad de Windows para proporcionar notificaciones sobre el mantenimiento y la seguridad del equipo. Las notificaciones de aplicaciones de seguridad incluyen firewalls, productos antivirus y SmartScreen de Windows Defender, entre otros.

## <a name="antivirus-policy-reports"></a>Informes de directivas antivirus

Los informes de directivas de antivirus muestran detalles de estado sobre las directivas de antivirus de seguridad de los puntos de conexión y el estado del dispositivo. Estos informes están disponibles en el nodo de seguridad de los puntos de conexión del Centro de administración del Microsoft Endpoint Manager.

Para ver los informes, en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), vaya a Seguridad de los puntos de conexión y seleccione **Antivirus**. Al seleccionar Antivirus, se abre la página Resumen. Hay más vistas de informe y estado disponibles como páginas adicionales.

### <a name="summary"></a>Resumen

En la página **Resumen**, puede [crear directivas](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) y ver una lista de las directivas que se crearon previamente. La lista incluye detalles de alto nivel sobre el perfil que incluye la directiva (tipo de directiva) y si se asigna la directiva.

![Página de información general de la directiva de antivirus](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Al seleccionar una directiva de la lista, se abre la página de *Información general* de esa instancia de directiva y se muestra más información. Al seleccionar un icono de esta vista, Intune muestra detalles adicionales para ese perfil, si están disponibles.

![Página de información general de la directiva de antivirus](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Puntos de conexión incorrectos de Windows 10

En la página **Windows 10 unhealthy endpoints** (Puntos de conexión incorrectos de Windows 10), puede ver información sobre el estado del antivirus de los dispositivos Windows 10 administrados por MDM. Esta información se devuelve desde la instancia de Antivirus de Windows Defender que se ejecuta en el dispositivo como *Estado del agente de amenazas*.

En esta vista solo aparecen los dispositivos en los que se han detectado problemas. No se muestran los detalles de los dispositivos identificados como limpios.

![Página de información general de la directiva de antivirus](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Pasos siguientes

[Configuración de directivas de seguridad de los puntos de conexión](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
