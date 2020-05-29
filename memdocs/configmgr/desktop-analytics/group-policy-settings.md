---
title: Configuración de la directiva de grupo
titleSuffix: Configuration Manager
description: Descripción de la configuración de la directiva de grupo y local en Windows usada por Configuration Manager y Análisis de escritorio
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 4536adad3114b944baa6c75ac4e246ecddf4a2d2
ms.sourcegitcommit: 555cb8102715afbe06c4de5fdbc943608f00b52c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153460"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Configuración de la directiva de grupo para Análisis de escritorio

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se detalla la configuración de la directiva de grupo y local en Windows que usan Configuration Manager y Análisis de escritorio.

Cuando Configuration Manager inscribe dispositivos en Análisis de escritorio, establece directivas de Windows para configurar el dispositivo. En la mayoría de los casos, use solo Configuration Manager para definir estos valores.

## <a name="windows-settings"></a>Configuración de Windows

Configuration Manager establece las directivas de Windows en una o ambas claves de Registro siguientes:

- Objeto de directiva de grupo (**GPO**): `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- Preferencia de directiva **local**: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Directiva | Path | Se aplica a | Valor |
|--------|------|------------|-------|
| **CommercialId** | Local | Todas las versiones de Windows | Para que un dispositivo se muestre en Análisis de escritorio, configúrelo con el identificador comercial de su organización. |
| **AllowTelemetry**  | GPO | Windows 10 | Establezca el nivel de los datos de diagnóstico del modo siguiente: `1` para **Básico**, `2` para **Mejorado** o `3` para **Completo**. Aunque Análisis de escritorio necesita como mínimo datos de diagnóstico básicos, Microsoft recomienda usar el nivel Mejorado (limitado). Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10, versión 1803 y posteriores | esta configuración solo se aplica cuando el valor de AllowTelemetry está establecido en `2`. Limita los eventos de datos de diagnóstico mejorados enviados a Microsoft a solo los que necesita Análisis de escritorio. Para más información, consulte [Campos y eventos de datos de diagnóstico de Windows 10 recopilados mediante la directiva de datos de diagnóstico mejorados](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields). |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10, versión 1803 y posteriores | Permite que los dispositivos envíen el nombre del dispositivo. De forma predeterminada, el nombre del dispositivo no se envía a Microsoft. Si no envía el nombre del dispositivo, aparece en Análisis de escritorio como "desconocido". Para más información, consulte [Nombre del dispositivo](enroll-devices.md#device-name). |
| **CommercialDataOptIn** | Local | Windows 8.1 y versiones anteriores | Análisis de escritorio requiere un valor de `1`. Para más información, consulte [Participación en los datos comerciales de Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Ambos | Windows 8.1 y versiones anteriores | Análisis de escritorio requiere un valor de `1` para que la recopilación de datos funcione correctamente. |
| **DisableEnterpriseAuthProxy** | GPO | Todas las versiones de Windows | Si su entorno requiere un proxy autenticado por el usuario con la autenticación integrada de Windows para el acceso a Internet, Análisis de escritorio requiere un valor de `0` para que la recopilación de datos funcione correctamente. Para más información, consulte [Compatibilidad del servidor proxy](enable-data-sharing.md#proxy-server-authentication). |

> [!IMPORTANT]
> En la mayoría de los casos, use solo Configuration Manager para definir estos valores. No aplique también esta configuración en los objetos de directiva de grupo de dominio. Para más información, consulte [Resolución de conflictos](enroll-devices.md#conflict-resolution).

### <a name="settings-from-upgrade-readiness"></a>Configuración de Upgrade Readiness

Windows Analytics también establece las siguientes directivas a través del script de Upgrade Readiness:

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

Si ejecutó el script de incorporación de Upgrade Readiness en un dispositivo, es posible que esta configuración de directiva todavía exista. No use el script heredado. Antes de inscribir el dispositivo en Análisis de escritorio, elimine esta configuración de directiva anterior.

## <a name="group-policy-settings"></a>Configuración de la directiva de grupo

En general, use recopilaciones de Configuration Manager como destino para la configuración y la inscripción de Análisis de escritorio. Use la pertenencia directa o las consultas para incluir o excluir dispositivos de la recopilación. Para obtener más información, vea [Creación de recopilaciones](../core/clients/manage/collections/create-collections.md).

Configuration Manager configura las opciones de identificador comercial y datos de diagnóstico en la colección de destino. Si necesita configurar diferentes opciones de datos de diagnóstico para distintos grupos de dispositivos, use la configuración de la directiva de grupo para reemplazar la configuración de Configuration Manager. Por ejemplo, debe establecer el nivel  **Mejorado (limitado)** para algunos dispositivos y el **Básico** para otros. Algunos dispositivos pueden tener una configuración de [autenticación del servidor proxy](enable-data-sharing.md#proxy-server-authentication) diferente.

Las configuración de la directiva de grupo correspondiente se encuentran en la siguiente ruta de acceso: **Configuración del equipo** > **Plantillas administrativas** > **Componentes de Windows** > **Recopilación de datos y versiones preliminares**.

La configuración de la directiva de grupo solo modifica la configuración del registro en la siguiente clave: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> Al usar la configuración de la directiva de grupo para habilitar escenarios complejos, preste especial atención a las opciones de la directiva que puede provocar conflictos de configuración. Configuration Manager solo configura las [opciones de Windows](#windows-settings)  *si el valor aún no existe*. Las opciones de la directiva de grupo tienen prioridad sobre las opciones de Configuration Manager, por lo que determinadas configuraciones de directiva de grupo podrían causar problemas con Análisis de escritorio.

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Opciones de la directiva de grupo que podrían entrar en conflicto con las opciones de Configuration Manager para Análisis de escritorio

Las opciones de la directiva de grupo de la tabla siguiente son las que tienen más posibilidades de generar conflictos con las opciones de Windows que Configuration Manager establece en los dispositivos que inscribe en Análisis de escritorio:

| Nombre para mostrar | Valor del Registro | Efecto en los dispositivos inscritos en Análisis de escritorio |
|--------------|----------------|-------------------------------------------------|
| **Configurar el identificador comercial** | CommercialId | Si establece esta directiva en un valor diferente, reemplazará el identificador comercial establecido por Configuration Manager. Si no es el mismo identificador, es posible que los dispositivos configurados no aparezcan en Análisis de escritorio. |
| **Permitir la telemetría** | AllowTelemetry | Si establece esta directiva en un valor diferente, reemplazará el nivel de datos de diagnóstico global que estableció en Configuration Manager para la recopilación de destino. |
| **Limitar los datos de diagnóstico mejorados al mínimo requerido por Windows Analytics** | LimitEnhancedDiagnosticDataWindowsAnalytics | Esta directiva depende de la opción AllowTelemetry anterior. Según el nivel establecido en Configuration Manager o con la directiva de grupo, esta directiva puede cambiar el nivel de datos de diagnóstico en el dispositivo a **Mejorado** o **Mejorado (limitado)** . Esta directiva solo se aplica si AllowTelemetry está establecido en `2` (**Mejorado**). |
| **Permitir el envío del nombre del dispositivo en los datos de diagnóstico de Windows** | AllowDeviceNameInTelemetry | Si opta por enviar los nombres de los dispositivos en Configuration Manager, puede invalidarlo configurando esta directiva como deshabilitada. Al deshabilitar esta opción, los nombres de los dispositivos aparecen como "Desconocido" en Análisis de escritorio. Para más información, consulte [Nombre del dispositivo](enroll-devices.md#device-name). |
| **Configurar el uso del proxy autenticado para el servicio de Experiencia del usuario y telemetría asociadas** | DisableEnterpriseAuthProxy | Si configura los dispositivos de Configuration Manager para que usen el proxy autenticado por el usuario (`0`), si posteriormente configura esta directiva en **Deshabilitar el uso de proxy autenticado** (`1`), el dispositivo envía datos de diagnóstico en el contexto del sistema en lugar del contexto del usuario. Si no configura el dispositivo con un proxy en el contexto del sistema, o si el dispositivo no se puede autenticar en el proxy, Windows no puede enviar datos de diagnóstico a Análisis de escritorio. |

> [!NOTE]
> La directiva heredada **Configurar Experiencia del usuario y telemetría asociadas** (TelemetryProxy) permite a Windows reenviar datos de diagnóstico a un proxy dedicado, en lugar de usar el proxy de usuario (WinINET) o de dispositivo (WinHTTP). Algunos componentes de Windows no admiten esta directiva. Si utiliza esta directiva, es posible que se produzcan problemas de calidad de datos en Análisis del escritorio.

#### <a name="behavior-of-disabled-settings"></a>Comportamiento de las opciones deshabilitadas

Si configura estas opciones de la directiva de grupo con el valor **Deshabilitado**, tiene efectos diferentes en el comportamiento del sistema.

- Al deshabilitar la directiva **CommercialId**, Windows elimina el valor del registro. La opción de Configuration Manager para el identificador comercial, que se establece en la ruta de acceso del registro de la directiva local, se aplica al dispositivo.

- En el caso de las directivas que Configuration Manager establece en la misma ubicación del registro que la directiva de grupo, al deshabilitar la opción en la directiva de grupo, Windows elimina el valor del registro. Configuration Manager volverá a establecerlo en el siguiente ciclo de procesamiento de directivas y, posteriormente, Windows lo eliminará en la siguiente actualización de directiva de grupo. Este cambio constante en la configuración puede producir comportamientos no deseados con Análisis del escritorio.

  - Si establece estas opciones de la directiva de grupo con el valor **No configurado**, Windows elimina el valor una vez, pero no sigue eliminándolo. Esta configuración permite a Configuration Manager aplicar sus valores según lo previsto.

### <a name="group-policy-settings-to-customize-the-user-experience"></a>Configuración de la directiva de grupo para personalizar la experiencia del usuario

Configuration Manager o Análisis de escritorio no necesitan esta configuración de la directiva de grupo. Se puede configurar en la directiva de grupo para configurar la experiencia de los usuarios con los datos de diagnóstico de Windows.

| Nombre para mostrar | Valor del Registro | Efecto en los dispositivos inscritos en Análisis de escritorio |
|--------------|----------------|-------------------------------------------------|
| **Configurar las notificaciones de cambio de participación en la telemetría** | DisableTelemetryOptInChangeNotification | A partir de Windows 10, versión 1803, Windows envía una notificación a los usuarios cuando cambia el nivel de datos de diagnóstico. Use esta directiva para deshabilitar las notificaciones. |
| **Configurar la interfaz de usuario de establecimiento de participación en la telemetría** | DisableTelemetryOptInSettingsUx | Al configurar el nivel de datos de diagnóstico, se establece el límite superior para el dispositivo. A partir de Windows 10, versión 1803, los usuarios pueden establecer un nivel inferior. Use esta directiva para evitar que los usuarios cambien el nivel de diagnóstico. Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management). |
| **Deshabilitar la eliminación de datos de diagnóstico** | DisableDeviceDelete | A partir de la versión 1809 de Windows 10, los usuarios pueden eliminar los datos de diagnóstico de la página de configuración de **Diagnóstico y comentarios**. Use esta directiva para evitar la eliminación de los datos de diagnóstico que Microsoft recopila del dispositivo. |
| **Deshabilitar el visor de datos de diagnóstico** | DisableDiagnosticDataViewer | A partir de la versión 1809 de Windows 10, los usuarios pueden habilitar y abrir el visor de datos de diagnóstico desde la página de configuración de **Diagnóstico y comentarios**. Use esta directiva para deshabilitar el visor de datos de diagnóstico en la configuración de Windows y evitar que muestre los datos de diagnóstico que Microsoft recopila del dispositivo.|
