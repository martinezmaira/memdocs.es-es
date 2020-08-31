---
title: Administración de las opciones de antivirus con directivas de seguridad de puntos de conexión en Microsoft Intune | Microsoft Docs
description: Configure e implemente directivas y use informes para los dispositivos administrados con la directiva de antivirus de seguridad de puntos de conexión en Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: 63400c81ee678a98a83ed17cf192335acf9c047b
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820310"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Directiva de antivirus para la seguridad de puntos de conexión en Intune

Las directivas de antivirus de seguridad de puntos de conexión de Intune ayudan a los administradores de seguridad a centrarse en administrar el grupo diferenciado de opciones de antivirus para dispositivos administrados. Para usar una directiva de antivirus, integre Intune con Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) como una solución de Mobile Threat Defense.

La directiva de antivirus incluye varios perfiles. Cada uno de ellos contiene solo la configuración pertinente para el antivirus de ATP de Microsoft Defender para macOS, Windows 10 o para la experiencia de usuario en la aplicación Seguridad de Windows en dispositivos Windows 10.

Encontrará las directivas de antivirus en **Administrar**, en el nodo Seguridad de los puntos de conexión del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Las directivas de antivirus incluyen la misma configuración que se encuentra en los perfiles de *protección de puntos de conexión* o *restricción de dispositivos* para la directiva de [configuración de dispositivos](../configuration/device-profile-create.md) y es similar a la de la directiva de [cumplimiento de dispositivos](../protect/device-compliance-get-started.md). Aun así, esos tipos de directivas incluyen categorías adicionales de configuración que no están relacionadas con el antivirus. La configuración adicional puede complicar la tarea de configurar el antivirus. Además, las opciones de configuración que se encuentra en la directiva de antivirus para macOS no están disponibles en los demás tipos de directivas. El perfil de antivirus de macOS reemplaza la necesidad de configurar las opciones mediante archivos `.plist`.

## <a name="prerequisites-for-antivirus-policy"></a>Requisitos previos de la directiva de antivirus

**General**:

- **macOS**
  - Cualquier versión compatible de macOS
  - Para que Intune administre la configuración de antivirus en un dispositivo, se debe instalar ATP de Microsoft Defender en ese dispositivo. Vea [ATP de Microsoft Defender para macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (en la documentación de ATP de Microsoft Defender)

- **Windows 10 y versiones posteriores**
  - No se necesitan requisitos previos adicionales.

**Compatibilidad con clientes de Configuration Manager** (*versión preliminar*)

*Este escenario se encuentra en versión preliminar y requiere el uso de la versión 2006 o posterior de la rama actual de Configuration Manager*.
<!--*This scenario is in preview and requires use of Configuration Manager Technical Preview version 2007 or later*.-->

- **Configuración de la asociación de inquilinos para dispositivos de Configuration Manager**: para admitir la implementación de directivas de antivirus en dispositivos administrados por Configuration Manager, configure la *asociación de inquilinos*. La configuración de la asociación de inquilinos incluye la configuración de colecciones de dispositivos de Configuration Manager para admitir directivas de seguridad de punto de conexión de Intune.

  Para configurar la asociación de inquilinos, consulte [Configuración de la asociación de inquilinos para admitir directivas de protección de puntos de conexión](../protect/tenant-attach-intune.md).

## <a name="antivirus-profiles"></a>Perfiles de antivirus

### <a name="devices-managed-by-intune"></a>Dispositivos administrados por Intune

Los siguientes perfiles se admiten para dispositivos administrados con Intune:

**macOS**:

- Plataforma: **macOS**

  - Perfil: **Antivirus**: administre la [configuración de directivas antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) para macOS.

    Cuando use [ATP de Microsoft Defender para Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac), puede configurar e implementar la configuración de antivirus en los dispositivos macOS administrados mediante Intune, en lugar de configurar estas opciones mediante archivos `.plist`.

**Windows 10**:

- Plataforma: **Perfiles de Windows 10**

  - Perfil: **Antivirus de Microsoft Defender**: administre la [configuración de directivas antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) para Windows 10.

    Antivirus de Defender es el componente de protección de última generación de Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender). La protección de próxima generación reúne tecnologías como aprendizaje automático e infraestructura en la nube para proteger los dispositivos de la organización.

    El perfil de *Antivirus de Microsoft Defender* es una instancia independiente de la configuración de antivirus que se encuentra en el *perfil de restricción de dispositivos* para la directiva de configuración de dispositivos.
  
    A diferencia de la configuración de antivirus de un *perfil de restricción de dispositivos*, puede usar esta configuración con dispositivos administrados conjuntamente. Para usar esta configuración, el [control deslizante de la carga de trabajo de administración conjunta](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) para Endpoint Protection debe establecerse en Intune.

  - Perfil: **Exclusiones del Antivirus de Microsoft Defender**: administra solo la configuración de directiva de las [exclusiones del antivirus](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions).
  
    Con esta directiva, puede administrar la configuración de los siguientes proveedores de servicios de configuración (CSP) del antivirus de Microsoft Defender que definen las exclusiones del antivirus:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    Estos CSP de la exclusión del antivirus también se administran mediante la directiva *Antivirus de Microsoft Defender*, que incluye configuraciones idénticas para las exclusiones. La configuración de ambos tipos de directivas (*Antivirus* y *Exclusiones del antivirus*) está sujeta a la [combinación de directivas](#policy-merge-for-settings) y crea un superconjunto de exclusiones para los dispositivos y usuarios correspondientes.

  - Perfil: **Experiencia de seguridad de Windows**: administra la [configuración de aplicaciones de seguridad de Windows](../protect/antivirus-security-experience-windows-settings.md) que los usuarios finales pueden ver en el centro de seguridad de Microsoft Defender y las notificaciones que reciben.

    Varias características de seguridad de Windows usan la aplicación Seguridad de Windows para proporcionar notificaciones sobre el mantenimiento y la seguridad del equipo. Las notificaciones de aplicaciones de seguridad incluyen firewalls, productos antivirus y SmartScreen de Windows Defender, entre otros.

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Dispositivos administrados por Configuration Manager *(en versión preliminar)*

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](includes/configmgr-antivirus-profiles.md)]

## <a name="policy-merge-for-settings"></a>Combinación de directivas para configuraciones

Algunas configuraciones de directiva admiten *combinación de directivas*. La combinación de directivas ayuda a evitar conflictos cuando se aplican varias directivas a los mismos dispositivos y se configuran los mismos valores. Para cada usuario o dispositivo, Intune evalúa la configuración que admite esa combinación de directivas, de entre todas las directivas aplicables. Después, esos valores se combinan en un superconjunto de directivas único.

Por ejemplo, se crean tres directivas de antivirus independientes que definen diferentes exclusiones de rutas de acceso de archivos antivirus. Finalmente, las tres directivas se asignan al mismo usuario. Dado que el CSP de exclusión de rutas de acceso de archivos de Microsoft Defender admite combinación de directivas, Intune evalúa y combina las exclusiones de archivos de todas las directivas aplicables al usuario. Las exclusiones se agregan a un superconjunto y la lista única de exclusiones se entrega en el dispositivo de los usuarios.

Cuando no se admite combinación de directivas para un valor de configuración, se puede producir un conflicto. Los conflictos pueden dar lugar a que el usuario o el dispositivo no reciban ninguna directiva para la configuración. Por ejemplo, la combinación de directivas no admite que el CSP impida la instalación de identificadores de dispositivo coincidentes (*PreventInstallationOfMatchingDeviceIDs*). Las configuraciones de este CSP no se combinan y se procesan por separado.

Cuando esto sucede, los conflictos de las directivas se resuelven de la siguiente manera:

1. Se aplica la directiva más segura.
2. Ante dos directivas igualmente seguras, se aplica la última directiva modificada.
3. Si la última directiva modificada no puede resolver el conflicto, no se entregará ninguna directiva al dispositivo.

### <a name="settings-and-csps-that-support-policy-merge"></a>Configuraciones y CSP que admiten combinación de directivas

La siguiente configuración admite combinación de directivas:

[Directivas de Antivirus de Microsoft Defender](../protect/antivirus-microsoft-defender-settings-windows.md)

- **Procesos que se van a excluir en Defender**, CSP: [Defender/ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **Extensiones de archivo para excluir de exámenes y protección en tiempo real**, CSP: [Defender/ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Archivos y carpetas que se van a excluir en Defender**, CSP: [Defender/ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## <a name="antivirus-policy-reports"></a>Informes de directivas antivirus

Los informes de directivas de antivirus muestran detalles de estado sobre las directivas de antivirus de seguridad de los puntos de conexión y el estado del dispositivo. Estos informes están disponibles en el nodo de seguridad de los puntos de conexión del Centro de administración del Microsoft Endpoint Manager.

Para ver los informes, en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), vaya a Seguridad de los puntos de conexión y seleccione **Antivirus**. Al seleccionar Antivirus, se abre la página Resumen. Hay más vistas de informe y estado disponibles como páginas adicionales.

### <a name="summary"></a>Resumen

En la página **Resumen**, puede [crear directivas](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) y ver una lista de las directivas que se crearon previamente. La lista incluye detalles de alto nivel sobre el perfil que incluye la directiva (tipo de directiva) y si se asigna la directiva.

![Página de resumen de la directiva de antivirus](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Al seleccionar una directiva de la lista, se abre la página de *Información general* de esa instancia de directiva y se muestra más información. Al seleccionar un icono de esta vista, Intune muestra detalles adicionales para ese perfil, si están disponibles.

![Página de información general de la directiva de antivirus](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Puntos de conexión incorrectos de Windows 10

En la página **Windows 10 unhealthy endpoints** (Puntos de conexión incorrectos de Windows 10), puede ver información sobre el estado del antivirus de los dispositivos Windows 10 administrados por MDM. Esta información se devuelve desde la instancia de Antivirus de Windows Defender que se ejecuta en el dispositivo como *Estado del agente de amenazas*.

En esta vista solo aparecen los dispositivos en los que se han detectado problemas. No se muestran los detalles de los dispositivos identificados como limpios.

![Página de puntos de conexión en mal estado de la directiva de antivirus](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Pasos siguientes

[Configuración de directivas de seguridad de los puntos de conexión](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
