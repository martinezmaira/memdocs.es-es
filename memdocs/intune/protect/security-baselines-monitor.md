---
title: 'Comprobación del éxito o error de las líneas de base de seguridad en Microsoft Intune: Azure | Microsoft Docs'
description: Compruebe el estado de error, conflicto y éxito al implementar líneas base de seguridad para usuarios y dispositivos en MDM de Microsoft Intune. Vea cómo solucionar problemas mediante registros de cliente y las características de informes en Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ccf9801c7a5977485c6c1864a69be2e46a4af55
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914878"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Supervisión de las líneas base de seguridad y los perfiles en Microsoft Intune

Intune ofrece varias opciones para supervisar las líneas base de seguridad. Puede:

- Supervisar una línea base de seguridad y todos los dispositivos que coincidan (o no) con los valores recomendados.
- Supervisar el perfil de las líneas base de seguridad que se aplica a los usuarios y dispositivos.
- Ver cómo se establecen las opciones de configuración de un perfil seleccionado en un dispositivo determinado.

También puede ver las *opciones de configuración de seguridad de los puntos de conexión* que se aplican a los dispositivos individuales, que incluyen las líneas base de seguridad.

Este artículo le guiará a través de estas opciones de supervisión.

Las [líneas de base de seguridad en Intune](security-baselines.md) proporcionan más detalles sobre la característica de las líneas de base de seguridad en Microsoft Intune.

## <a name="monitor-the-baseline-and-your-devices"></a>Supervisión de la línea base y los dispositivos

Al supervisar una línea base, obtiene conclusiones sobre el estado de seguridad de los dispositivos según las recomendaciones de Microsoft. Para ver esta información, inicie sesión en el [centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), vaya a **Seguridad de los puntos de conexión** > **Líneas base de seguridad** y seleccione un tipo de línea base de seguridad, como la *línea base de seguridad de MDM*. Después, en el panel *Perfil*, seleccione la instancia del perfil cuyos detalles quiera consultar. Esto abrirá el panel *Propiedades* de los perfiles, donde puede seleccionar cualquiera de los informes del perfil en la sección *Supervisión*. 

Los datos tardan hasta 24 horas en aparecer después de asignar una línea base en primer lugar. Los cambios posteriores tardan hasta seis horas en aparecer.

A medida que explore los informes y los dispositivos, habrá una serie de detalles disponibles.

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>Supervisión del perfil

La supervisión del perfil proporciona conclusiones sobre el estado de implementación de los dispositivos, pero no sobre el de la seguridad según las recomendaciones de las líneas base.

1. En Intune, seleccione **Líneas base de seguridad**, elija una línea base para abrir el panel y, luego, *Perfiles*.

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. En **Administrar** > **Propiedades**, se muestra una lista de todas las configuraciones de la línea de base. También puede cambiar cualquiera de estas configuraciones:

   ![Visualización y actualización de la configuración en el perfil de las líneas de base de seguridad](./media/security-baselines-monitor/manage-settings.png)

4. En **Monitor**, puede ver el estado de implementación del perfil en dispositivos individuales, el estado de cada usuario y el estado de cada valor de configuración en la línea de base:

   ![Visualización de diferentes opciones de supervisión para un perfil de las líneas de base de seguridad](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Vista de la configuración de los perfiles que se aplican a un dispositivo

Puede seleccionar un perfil para una línea base de seguridad y explorarlo a fin de ver una lista de las opciones de configuración de ese perfil a medida que se aplican a un dispositivo individual.  Para ver esa lista, explore **Seguridad de los puntos de conexión** > **Líneas base de seguridad** > *seleccione el tipo de línea base de seguridad* > *seleccione el perfil que quiere ver* > **Estado del dispositivo**. También puede ver la lista yendo a **Seguridad de los puntos de conexión** > **Todos los dispositivos** > *seleccione un dispositivo* > **Configuración de seguridad de los puntos de conexión** > *seleccione una versión de línea base*.

Después de seleccionar un dispositivo, el centro de administración de Microsoft Endpoint Manager muestra una lista de los valores de configuración de ese perfil, incluidos el estado de configuración en el dispositivo y la categoría de la que procede la configuración. Los estados de configuración incluyen los valores siguientes:

- **Correcto**: la configuración en el dispositivo coincide con el valor configurado en el perfil. Este es el valor predeterminado de las líneas base y el recomendado, o un valor personalizado que ha especificado un administrador cuando se ha configurado el perfil.
- **Conflicto**: la configuración está en conflicto con otra directiva, tiene un error o está pendiente de una actualización.
- **No aplicable**: el perfil no ha aplicado la configuración.

> [!NOTE]
> Los valores de estado de la configuración se actualizarán en una versión futura para proporcionar detalles más pormenorizados.

## <a name="view-endpoint-security-configurations-per-device"></a>Visualización de configuraciones de seguridad de los puntos de conexión por dispositivo

Vea detalles sobre las configuraciones de seguridad que se aplican a un dispositivo individual, lo que puede ayudarle a aislar los valores configurados incorrectamente.

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vaya a **Dispositivos** > **Todos los dispositivos** y seleccione el dispositivo que quiera ver.

3. En la categoría *Supervisión*, seleccione **Configuración de seguridad de los puntos de conexión** para ver la lista de configuraciones de seguridad que se aplican a ese dispositivo.

4. Puede seleccionar una configuración de seguridad de los puntos de conexión para profundizar y ver detalles adicionales sobre la evaluación de esa configuración de seguridad en el dispositivo.

## <a name="troubleshoot-using-per-setting-status"></a>Solución de problemas utilizando el estado por valor de configuración

Ha implementado una línea de base de seguridad, pero el estado de implementación muestra un error. Los pasos siguientes ofrecen algunas instrucciones sobre cómo solucionar el error.

1. En Intune, seleccione **Líneas base de seguridad**, una línea base y **Perfiles**.

2. Seleccione un perfil > **Monitor** > **Estado por valor**.

3. La tabla muestra todas las configuraciones y el estado de cada valor de configuración. Seleccione la columna **Error** o la columna **Conflicto** para ver el valor de configuración que causa el error.

### <a name="mdm-diagnostic-information"></a>Información de diagnóstico MDM

Ahora conoce el valor de configuración problemático. El siguiente paso es averiguar por qué este valor de configuración está causando un error o conflicto.

En dispositivos con Windows 10, hay un informe de detalles de diagnóstico integrado de MDM. Este informe incluye valores predeterminados, valores actuales, enumera la directiva, muestra si se implementa en el dispositivo o el usuario, etc. Use este informe para ayudar a determinar por qué el valor de configuración está causando un conflicto o error.

1. En el dispositivo, vaya a **Configuración** > **Cuentas** > **Obtener acceso a trabajo o escuela**.

2. Seleccione la cuenta > **Información** > **Advanced Diagnostic Report (Informe de diagnóstico avanzado)**  > **Crear informe**.

3. Elija **Exportar** y abra el archivo generado.

4. En el informe, busque el error o el valor de configuración conflictivo en las diferentes secciones del informe.

  Por ejemplo, busque en las secciones **Enrolled configuration sources and target resources** (Recursos de destino y orígenes de configuración inscritos) o **Unmanaged policies** (Directivas no administradas). Puede hacerse una idea de por qué está causando un error o conflicto.

En [Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) (Diagnósticos de errores MDM en Windows 10) se proporciona más información sobre este informe integrado.

> [!TIP]
>
> - Algunas configuraciones también enumeran el GUID. Puede buscar este GUID en el registro local (regedit) para cualquier valor establecido.
> - Los registros del Visor de eventos también pueden incluir alguna información de error sobre el valor de configuración problemático (**Visor de eventos** > **Registros de aplicaciones y servicios** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider** > **Admin**).

## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre las líneas de base de seguridad](security-baselines.md)
- [Evitación de conflictos](security-baselines.md#avoid-conflicts)
- [Supervisar perfiles de dispositivo](../configuration/device-profile-monitor.md) 
- [Problemas comunes y sus soluciones](../configuration/device-profile-troubleshoot.md)
- [Solución de problemas de directivas y perfiles en Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)