---
title: Supervisión del estado de conexión
titleSuffix: Configuration Manager
description: Detalles sobre cómo supervisar el estado de la conexión y los estados de los dispositivos de Análisis de escritorio en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: db70eab54f319197f267173fe857d0fb147a7eba
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746568"
---
# <a name="monitor-connection-health"></a>Supervisión del estado de conexión

Use el panel **Estado de conexión** de Configuration Manager para profundizar en las categorías por estado de dispositivo. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda el nodo **Servicio de Análisis de escritorio** y seleccione el panel **Mantenimiento de la conexión**.  

[![Captura de pantalla del panel Estado de conexión de Configuration Manager](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

La primera vez que se configura Análisis de escritorio, es posible que estos gráficos no muestren datos completos. Los dispositivos activos pueden tardar entre 2 y 3 días en enviar datos de diagnóstico al servicio Análisis de escritorio, el servicio para procesar los datos y, luego, sincronizarlos con el sitio de Configuration Manager.<!-- 4098037 -->

## <a name="connection-details"></a>Detalles de conexión

Este icono muestra la siguiente información básica sobre la conexión de Configuration Manager a Análisis de escritorio:

- **Nombre de inquilino**: el nombre de la conexión de Análisis de escritorio en el nodo **Servicios de Azure**.

- **Colección de destino**: la misma *colección de destino* que especificó al conectar Configuration Manager a Análisis de escritorio. Esta recopilación incluye todos los dispositivos que configura Configuration Manager con el identificador comercial y la configuración de datos de diagnóstico. Es el conjunto completo de dispositivos que conecta Configuration Manager al servicio Análisis de escritorio.

- **Dispositivos de destino**: todos los dispositivos de la recopilación de destino, menos los siguientes tipos de dispositivos:

  - Dados de baja
  - Obsoletos
  - Inactivo
  - No administrados
  - Dispositivos que ejecutan las versiones de canal de mantenimiento a largo plazo (LTSC) de Windows 10
  - Equipos que ejecutan Windows Server.

    Para más información sobre estos estados de dispositivo, consulte [Acerca del estado de cliente](../core/clients/manage/monitor-clients.md#bkmk_about).

    > [!Note]  
    > Configuration Manager carga en Análisis de escritorio todos los dispositivos de la recopilación de destino menos los clientes obsoletos y dados de baja.

- **Dispositivos aptos para DA**: el número de dispositivos de destino menos los dispositivos que no son aptos para Análisis de escritorio. Por ejemplo, los dispositivos de la recopilación de destino que ejecutan el canal de mantenimiento a largo plazo (LTSC) de Windows Server o Windows 10.

## <a name="last-sync-details"></a>Detalles de la última sincronización

Este icono muestra cuándo se sincroniza Configuration Manager con el servicio en la nube de Análisis de escritorio y el número de dispositivos que se sincronizan.

- **Dispositivos sincronizados**: número de dispositivos aptos que Configuration Manager ha enviado a Análisis de escritorio. El servicio incluye estos dispositivos en la instantánea actualmente visible.

- **Última sincronización del servicio**: lo mismo que **Última actualización** en el portal de Análisis de escritorio.

- **Próxima sincronización del servicio**: cuándo puede esperar la siguiente instantánea diaria en Análisis de escritorio.

> [!Note]  
> La primera vez que se inscriben los dispositivos en Análisis de escritorio, los datos pueden tardar varios días en cargarse y procesarse. Durante este tiempo, el icono **Detalles de la última sincronización**  puede aparecer en blanco.
> Además, ninguno de los valores de este icono se actualiza automáticamente cuando se solicita una instantánea a petición. Para más información, consulte [Latencia de datos](troubleshooting.md#data-latency).

Si cree que algunos dispositivos no se muestran en Análisis de escritorio, asegúrese de que sean compatibles con este servicio. Para obtener más información, consulte [Requisitos previos](overview.md#prerequisites).

## <a name="connection-health"></a>Estado de conexión

En el gráfico **Estado de conexión** se muestra el número de dispositivos con los siguientes estados de mantenimiento:  

- [Inscrito correctamente](#properly-enrolled): el dispositivo aparece en Análisis de escritorio con un inventario completo.
- [No se puede inscribir](#unable-to-enroll): hay un problema de bloqueo que impide la inscripción del dispositivo.
- [Alerta de configuración](#configuration-alert): el dispositivo no aparece en Análisis de escritorio ni con un inventario incompleto. Configuration Manager también identificó un problema con la inscripción de los dispositivos.
- [Esperando la inscripción](#awaiting-enrollment): Configuration Manager configuró el dispositivo, pero todavía no aparece en Análisis de escritorio.
- [Estado pendiente](#status-pending): Configuration Manager todavía está configurando este dispositivo o no tiene suficientes datos del dispositivo para determinar su estado.
- [Faltan datos](#missing-data): Configuration Manager configuró el dispositivo, pero Análisis de escritorio solo tiene datos parciales.

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

El número total de dispositivos en este gráfico debe ser el igual al valor de **Dispositivos aptos para DA** del icono de detalles de la conexión.

Seleccione el sector en el gráfico para explorar en profundidad hasta una lista de dispositivos con ese estado. Para más información, consulte [Lista de dispositivos](#device-list).

Seleccione el nombre de la categoría en la leyenda que se va a quitar o agregar en el gráfico. Esta acción ayuda a ampliar el gráfico de forma que pueda ver los tamaños relativos de segmentos más pequeños.

### <a name="properly-enrolled"></a>Inscrito correctamente

El dispositivo tiene los siguientes atributos:

- Versión de cliente de Configuration Manager 1902 o posterior  
- No hay errores de configuración  
- Análisis de escritorio ha recibido datos de diagnóstico completos de este dispositivo en los últimos 28 días  
- Análisis de escritorio tiene un inventario completo de la configuración y de las aplicaciones instaladas del dispositivo.  

### <a name="unable-to-enroll"></a>No se puede inscribir

Configuration Manager detecta uno o más problemas de bloqueo que impiden la inscripción del dispositivo. Para más información, consulte la lista de [propiedades del dispositivo de Análisis de escritorio en Configuration Manager](#bkmk_config-issues).  

Por ejemplo, el cliente de Configuration Manager no tiene al menos la versión 1902 (5.0.8790). Actualice el cliente a la versión más reciente. Considere la posibilidad de habilitar la actualización automática del cliente en el sitio Configuration Manager. Para obtener más información, vea [Actualizar clientes](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

> [!TIP]
> Hay un problema conocido con la actualización de seguridad extendida (ESU) de abril de 2020 para Windows 7 que hace que los dispositivos informen equivocadamente de este error. Para obtener más información, consulte [Notas de la versión](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

A partir de la versión 2002, puede identificar más fácilmente los problemas de configuración del proxy de clientes en dos áreas:

- **Comprobaciones de conectividad del punto de conexión**: Si los clientes no se pueden conectar a un punto de conexión necesario, verá una alerta de configuración en el panel. Explore en profundidad los clientes que no pueden inscribirse para ver los puntos de conexión a los que los clientes no pueden conectarse debido a problemas de configuración de proxy. Para obtener más información, consulte [Comprobaciones de conectividad del punto de conexión](#endpoint-connectivity-checks).<!-- 4963230 -->

- **Estado de conectividad**: Si sus clientes usan un servidor proxy para acceder a Análisis de escritorio, Configuration Manager muestra los problemas de autenticación del proxy que tienen los clientes. Explore en profundidad para ver los clientes que no se pueden inscribir debido a problemas de autenticación del proxy. Para obtener más información, consulte [Estado de conectividad](#connectivity-status).<!-- 4963383 -->

### <a name="configuration-alert"></a>Alerta de configuración

El dispositivo no aparece en Análisis de escritorio ni con un inventario incompleto. Configuration Manager también identificó un problema con la inscripción de los dispositivos. Para más información, consulte la lista de [propiedades del dispositivo de Análisis de escritorio en Configuration Manager](#bkmk_config-issues).

Por ejemplo, el dispositivo no tiene conectividad con el servicio. Para más información, consulte [Conectividad del punto de conexión de diagnóstico de Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Esperando la inscripción

Análisis de escritorio no tiene datos de diagnóstico de este dispositivo. Este problema puede deberse a que ha agregado recientemente el dispositivo a la recopilación de destino y aún no ha enviado datos. También puede significar que el dispositivo no se comunica correctamente con el servicio y que los datos de diagnóstico más recientes tienen más de 28 días de antigüedad.

Asegúrese de que el dispositivo pueda comunicarse con el servicio. Para más información, consulte [Puntos de conexión](enable-data-sharing.md#endpoints).  

### <a name="status-pending"></a>Estado pendiente

Configuration Manager todavía está configurando este dispositivo o no tiene suficientes datos del dispositivo para determinar su estado.

### <a name="missing-data"></a>Faltan datos

Configuration Manager configuró correctamente el dispositivo, pero Análisis de escritorio no puede crear una evaluación de compatibilidad. No tiene un conjunto de datos completo de la configuración del dispositivo (censo) o de las aplicaciones instaladas (inventario).

Este problema se suele corregir automáticamente cuando el dispositivo vuelve a intentarlo. Si persiste, asegúrese de que el dispositivo pueda comunicarse con el servicio. Para más información, consulte [Puntos de conexión](enable-data-sharing.md#endpoints).  

## <a name="device-list"></a>Lista de dispositivos

Para ver una lista específica de dispositivos por estado, comience con el panel **Estado de conexión**. Seleccione uno de los segmentos del icono **Estado de conexión** y explore en profundidad hasta una lista de dispositivos en este estado. Esta vista de dispositivo personalizada muestra las siguientes columnas de Análisis de escritorio de forma predeterminada:

- Configuración de id. comercial
- Actualización de la compatibilidad mínima
- Participación en datos de diagnóstico de Windows
- Participación en los datos comerciales de Windows
- Conectividad del punto de conexión de diagnóstico de Windows
- Estado de conectividad (a partir de la versión 2002)
- Comprobaciones de conectividad del punto de conexión (a partir de la versión 2002)

Estas columnas corresponden a los [requisitos previos](overview.md#prerequisites) principales para que los dispositivos se comuniquen con Análisis de escritorio.

[![Captura de pantalla de No se puede inscribir la lista de dispositivos](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Seleccione un dispositivo para ver la lista completa de propiedades disponibles en el panel de detalles. También puede agregar cualquiera de estas propiedades como columnas a la lista de dispositivos.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a> Propiedades del dispositivo

Las siguientes propiedades del dispositivo de Análisis de escritorio están disponibles como columnas en la lista de dispositivos de Configuration Manager:

- [Comprobaciones de conectividad del punto de conexión](#endpoint-connectivity-checks) (a partir de la versión 2002)
- [Estado de conectividad](#connectivity-status) (a partir de la versión 2002)
- [Configuración del evaluador](#appraiser-configuration)  
- [Actualización de la compatibilidad mínima](#minimum-compatibility-update)  
- [Versión del evaluador](#appraiser-version)  
- [Última ejecución completa correcta del evaluador](#last-successful-full-run-of-appraiser)  
- [Recopilación de datos del evaluador](#appraiser-data-collection)  
- [Última ejecución correcta del censo](#last-successful-full-run-of-census)  
- [Recopilación de datos de recuento](#census-data-collection)  
- [Conectividad del punto de conexión de diagnóstico de Windows](#windows-diagnostic-endpoint-connectivity)  
- [Compruebe los datos de diagnóstico del usuario final](#check-end-user-diagnostic-data)  
- [Comprobar proxy de usuario](#check-user-proxy)  
- [Configuración de id. comercial](#commercial-id-configuration)  
- [Participación en los datos comerciales de Windows](#windows-commercial-data-opt-in)  
- [Compruebe el nombre de dispositivo en los datos de diagnóstico](#check-device-name-in-diagnostic-data)  
- [Configuración del servicio DiagTrack](#diagtrack-service-configuration)  
- [Versión de DiagTrack](#diagtrack-version)  
- [Recuperación del id. de SQM](#sqm-id-retrieval)  
- [Recuperación del identificador único de dispositivo](#unique-device-identifier-retrieval)  
- [Participación en datos de diagnóstico de Windows](#windows-diagnostic-data-opt-in)  

El icono **Most frequent enrollment blockers and configuration alerts** (Bloqueadores de inscripciones más frecuentes) del panel Estado de conexión muestra las propiedades que los dispositivos notifican con más frecuencia como problemáticas.

### <a name="endpoint-connectivity-checks"></a>Comprobaciones de conectividad del punto de conexión

A partir de la versión 2002,<!-- 4963230 --> para detectar problemas de autenticación de proxy, los clientes efectúan comprobaciones de conectividad en los puntos de conexión necesarios. Si un cliente no puede acceder a un punto de conexión necesario, esta propiedad muestra una lista numerada de puntos de conexión a los que no se puede conectar debido a problemas de configuración de proxy. Compare esta lista con la lista publicada de [puntos de conexión necesarios](enable-data-sharing.md#endpoints).

### <a name="connectivity-status"></a>Estado de conectividad

A partir de la versión 2002,<!-- 4963383 --> si los clientes usan un servidor proxy para acceder a Análisis de escritorio, esta propiedad muestra los problemas de autenticación de proxy. Incluye los siguientes detalles relacionados con la autenticación de proxy:

- Código de estado
- Código de retorno

Verá errores similares a los siguientes en el archivo de registro:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

Donde `%s` es la dirección URL de un punto de conexión requerido.

También puede ver mensajes de error no deterministas que no requieren atención hasta que los dispositivos tengan problemas de inscripción. Por ejemplo:

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Para obtener más información sobre cómo configurar servidores proxy para usar con Análisis de escritorio, vea [Autenticación del servidor proxy](enable-data-sharing.md#proxy-server-authentication).

### <a name="appraiser-configuration"></a>Configuración del evaluador

<!--20,21-->
El evaluador es el componente de Windows que corresponde a las [actualizaciones de compatibilidad](enroll-devices.md#update-devices). Evalúa las aplicaciones y los controladores del dispositivo para comprobar la compatibilidad con la versión más reciente de Windows.

Si esta comprobación se realiza correctamente, el componente evaluador está configurado correctamente en el dispositivo.

De lo contrario, podría mostrarse uno de los siguientes errores:

- No se puede configurar la recopilación de datos de compatibilidad de aplicaciones del dispositivo (SetRequestAllAppraiserVersions). Compruebe los registros para obtener los detalles de la excepción.  

- No se puede configurar la recopilación de datos de compatibilidad de aplicaciones del dispositivo (SetRequestAllAppraiserVersions). Compruebe los registros para obtener los detalles de la excepción.  

- No se puede escribir RequestAllAppraiserVersions en la clave del Registro `HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Appraiser`. Compruebe los permisos.  

Compruebe los permisos de esta clave del Registro. Asegúrese de que la cuenta del sistema local pueda acceder a esta clave para establecer el cliente de Configuration Manager.  

Para más información, revise M365AHandler.log en el cliente.  

### <a name="minimum-compatibility-update"></a>Actualización de la compatibilidad mínima

<!--18,19,32-->
La actualización de compatibilidad (appraiser.dll) no está instalada o no está actualizada en el dispositivo. Es más antigua que el requisito mínimo de Análisis de escritorio, 10.0.17763.

Instale la actualización de compatibilidad más reciente. Para más información, consulte [Actualizaciones de compatibilidad](enroll-devices.md#update-devices).

### <a name="appraiser-version"></a>Versión del evaluador

Esta propiedad muestra la versión actual del componente evaluador del dispositivo. Muestra la versión del archivo en `%windir%\System32\appraiser.dll`, sin los separadores decimales. Por ejemplo, la versión del archivo 10.0.17763 se muestra como 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Última ejecución completa correcta del evaluador

Esta propiedad muestra la fecha y la hora de la última vez que el dispositivo ejecutó el evaluador correctamente.

### <a name="appraiser-data-collection"></a>Recopilación de datos del evaluador

<!--Appraiser run status-->
<!--22,33-->
Esta propiedad muestra el resultado más reciente de la ejecución del componente evaluador en Windows.

Si no es correcto, podría mostrarse uno de los siguientes errores:

- No se pueden recopilar datos de compatibilidad de aplicaciones (RunAppraiser). Consulte los registros para obtener detalles.  

- La recopilación de datos de compatibilidad de aplicaciones (CompatTelRunner.exe) finalizó con un código de error.  

Para más información, revise M365AHandler.log en el cliente.

Compruebe el archivo siguiente: `%windir%\System32\CompatTelRunner.exe`. Si no existe, vuelva a instalar las [actualizaciones de compatibilidad](enroll-devices.md#update-devices) necesarias. Asegúrese de que ningún otro componente del sistema quita este archivo, como la directiva de grupo o un servicio antimalware.

Si el archivo M365AHandler.log en el cliente incluye uno de los siguientes errores:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Para solucionarlos, ejecute los siguientes comandos desde una consola de Windows PowerShell con privilegios elevados en el cliente afectado:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Última ejecución correcta del censo

Esta propiedad muestra la fecha y la hora de la última vez que el dispositivo ejecutó el censo correctamente.

### <a name="census-data-collection"></a>Recopilación de datos de recuento

<!-- Census run status -->
<!--51,52-->
El censo es el componente de Windows que realiza el inventario del dispositivo. Estos datos de inventario se usan para comprender el dispositivo y su configuración.

Esta propiedad muestra el resultado más reciente de la ejecución del componente de censo en Windows.

Si no es correcto, podría mostrarse uno de los siguientes errores:

- No se pueden recopilar datos sobre el dispositivo y su configuración (RunCensus). Compruebe los registros para obtener los detalles de la excepción.  

- No se encontró la herramienta de recopilación de datos de configuración y del dispositivo (devicecensus.exe).  

Para más información, revise M365AHandler.log en el cliente.

Compruebe el archivo siguiente: `%windir%\System32\DeviceCensus.exe`. Si no existe, vuelva a instalar las [actualizaciones de compatibilidad](enroll-devices.md#update-devices) necesarias. Asegúrese de que ningún otro componente del sistema quita este archivo, como la directiva de grupo o un servicio antimalware.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Conectividad del punto de conexión de diagnóstico de Windows

<!--12,15-->
Si esta comprobación se realiza correctamente, el dispositivo puede conectarse al punto de conexión Experiencia del usuario y telemetría asociadas (Vortex).

De lo contrario, se puede mostrar uno de los siguientes errores:  

- No se puede conectar con el punto de conexión de Experiencia del usuario y telemetría asociadas (Vortex). Compruebe la configuración de red y proxy.  

- No se puede comprobar la conectividad con el punto de conexión de Experiencia del usuario y telemetría asociadas (CheckVortexConnectivity). Compruebe los registros para obtener los detalles de la excepción.  

Los dispositivos comprueban la conectividad con una solicitud GET al siguiente punto de conexión en función de la versión del sistema operativo:

| Versión del sistema operativo | Punto de conexión |
|------------|----------|
| - Windows 10, versión 1809 o posterior<br/>- Windows 10, versión 1803 con la actualización acumulativa 2018-09 o posterior | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, versión 1803 *sin* la actualización acumulativa 2018-09 o posterior | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versión 1709 o anterior | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 o Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Asegúrese de que el dispositivo pueda comunicarse con el servicio. Esta comprobación valida algunos de los puntos de conexión necesarios, pero no todos. Para más información, consulte [Puntos de conexión](enable-data-sharing.md#endpoints).  

Para más información, revise M365AHandler.log en el cliente.  

### <a name="check-end-user-diagnostic-data"></a>Comprobar los datos de diagnóstico del usuario final

<!--1004-->
Si esta comprobación no se realiza correctamente, significa que el usuario seleccionó un nivel inferior de datos de diagnóstico de Windows en el dispositivo. También puede deberse al conflicto de un objeto de directiva de grupo. Para más información, consulte [Configuración de Windows](enroll-devices.md#windows-settings).

En función de los requisitos de su empresa, puede deshabilitar la elección del usuario a través de la directiva de grupo. Use la opción **Configure telemetry opt-in setting user interface** (Configurar la interfaz de usuario de establecimiento de participación en la telemetría). Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Comprobar proxy de usuario

<!--30,35-->
El valor DisableEnterpriseAuthProxy está habilitado de forma predeterminada en Windows 7. En equipos con Windows 8.1, Configuration Manager establece el valor DisableEnterpriseAuthProxy en 0 (no deshabilitado).

Esta propiedad puede mostrar los errores siguientes:

- El proxy de autenticación está habilitado. Establezca DisableEnterpriseAuthProxy en 0 en `HKLM:\Software\Policies\Microsoft\Windows\DataCollection`.

- No se puede comprobar el estado del proxy de autenticación. Compruebe los registros para obtener los detalles de la excepción.

Para más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del Registro. Asegúrese de que la cuenta del sistema local pueda acceder a esta clave para establecer el cliente de Configuration Manager. También puede deberse al conflicto de un objeto de directiva de grupo. Para más información, consulte [Configuración de Windows](enroll-devices.md#windows-settings).  

### <a name="commercial-id-configuration"></a>Configuración de id. comercial

<!--9, 11, 53-->
Microsoft usa un identificador comercial único para asignar información de los dispositivos al área de trabajo de Análisis de escritorio. Al integrar Configuration Manager con Análisis de escritorio, consulta automáticamente el servicio para encontrar este identificador. Configuration Manager debe aplicar este identificador automáticamente a los clientes a los que se dirige la configuración de Análisis de escritorio.

Si esta comprobación se realiza correctamente, el dispositivo se configura correctamente con un identificador comercial.

De lo contrario, se puede mostrar uno de los siguientes errores:

- No se puede escribir CommercialId en la clave del Registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Compruebe los permisos.  

- No se puede actualizar CommercialId en la clave del registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Compruebe los registros para obtener los detalles de la excepción.  

- Proporcione el valor de CommercialId correcto en `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`.  

Para más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del Registro. Asegúrese de que la cuenta del sistema local pueda acceder a esta clave para establecer el cliente de Configuration Manager. También puede deberse al conflicto de un objeto de directiva de grupo. Para más información, consulte [Configuración de Windows](enroll-devices.md#windows-settings).  

Hay un identificador diferente para el dispositivo. La directiva de grupo usa esta clave del Registro. Tiene prioridad sobre el identificador que se proporciona en Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a> Para ver el identificador comercial en el portal de Análisis de escritorio, use el siguiente procedimiento:

1. Vaya al portal de Análisis de escritorio y seleccione **Servicios conectados** en el grupo Configuración global.  

2. En el panel **Servicios conectados**, el panel **Inscribir dispositivos** está seleccionado de forma predeterminada. En el panel Inscribir dispositivos, la sección Información muestra la clave del identificador comercial.  

[![Captura de pantalla del identificador comercial en el portal de Análisis de escritorio](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Use solo **Obtener nueva clave de id.** cuando no pueda usar la actual. Si vuelve a generar el identificador comercial, [inscriba de nuevo los dispositivos con el nuevo identificador](enroll-devices.md#device-enrollment). Este proceso podría provocar la pérdida de datos de diagnóstico durante la transición.  

### <a name="windows-commercial-data-opt-in"></a>Participación en los datos comerciales de Windows

<!--64-->
Esta propiedad es específica de los dispositivos que ejecutan Windows 7 o Windows 8.1. Ejecuta pruebas similares a [Participación en datos de diagnóstico de Windows](#windows-diagnostic-data-opt-in), excepto el valor CommercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Comprobar el nombre del dispositivo en los datos de diagnóstico

<!--56,58-->
Si esta comprobación se realiza correctamente, el dispositivo está configurado correctamente para compartir su nombre.

De lo contrario, se puede mostrar uno de los siguientes errores:

- No se puede comprobar el nombre de dispositivo que se enviará a Microsoft como parte de los datos de diagnóstico de Windows. Compruebe los registros para obtener los detalles de la excepción.  

- No se puede escribir AllowDeviceNameInTelemetry en la clave del Registro `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Compruebe los permisos.  

Para más información, revise M365AHandler.log en el cliente.  

Compruebe los permisos de esta clave del Registro. Asegúrese de que la cuenta del sistema local pueda acceder a esta clave para establecer el cliente de Configuration Manager. También puede deberse al conflicto de un objeto de directiva de grupo. Para más información, consulte [Configuración de Windows](enroll-devices.md#windows-settings).  

Asegúrese de que otro mecanismo de directivas, como la directiva de grupo, no vaya a deshabilitar esta configuración.

### <a name="diagtrack-service-configuration"></a>Configuración del servicio DiagTrack

<!--44,45,50-->
Si esta comprobación se realiza correctamente, el componente DiagTrack está configurado adecuadamente en el dispositivo. La versión mínima requerida por Análisis de escritorio es 10010586 (10.0.10586).

De lo contrario, podría mostrarse uno de los siguientes errores:

- El componente Experiencia del usuario y telemetría asociadas (diagtrack.dll) está obsoleto. Compruebe los requisitos.  

    > [!TIP]
    > Hay un problema conocido con la actualización de seguridad extendida (ESU) de abril de 2020 para Windows 7 que hace que los dispositivos informen equivocadamente de este error. Para obtener más información, consulte [Notas de la versión](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

- No se encuentra el componente de Experiencia del usuario y telemetría asociadas (diagtrack.dll). Compruebe los requisitos.  

- Habilite e inicie el servicio Experiencia del usuario y telemetría asociadas para enviar datos a Microsoft.  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Instale las actualizaciones más recientes. Para más información, consulte [Actualizaciones de dispositivos](enroll-devices.md#update-devices).

Asegúrese de que el servicio **Experiencia del usuario y telemetría asociadas** se ejecuta en el dispositivo.

### <a name="diagtrack-version"></a>Versión de DiagTrack

Esta propiedad muestra la versión actual del componente Experiencia del usuario y telemetría asociadas en el dispositivo. Muestra la versión del archivo en `%windir%\System32\diagtrack.dll`, sin los separadores decimales. Por ejemplo, la versión del archivo 10.0.10586 se muestra como 10010586.

### <a name="sqm-id-retrieval"></a>Recuperación de identificador de SQM

<!--38-->
Esta propiedad es principalmente para dispositivos Windows 7. Se puede usar en versiones posteriores del sistema operativo como identificador de reserva del dispositivo.

Si no es correcta, puede aparecer el siguiente error:

- No se puede recuperar el identificador de telemetría de dispositivo heredado (id. de SQM)

Para más información, revise M365AHandler.log en el cliente.  

Asegúrese de que no tenga identificadores duplicados en su entorno. Por ejemplo, que los dispositivos se hayan implementado con una imagen del sistema operativo que no se generalizaba.

### <a name="unique-device-identifier-retrieval"></a>Recuperación del identificador único de dispositivo

<!--54-->
Análisis de escritorio usa el servicio de cuentas Microsoft para aumentar la confiabilidad de la identidad del dispositivo.

Asegúrese de que el servicio **Ayudante para el inicio de sesión de cuenta Microsoft** no esté deshabilitado. El tipo de inicio debe ser **Manual (desencadenar inicio)** .

Para deshabilitar el acceso a la cuenta Microsoft del usuario final, use la configuración de directiva en lugar de bloquear este punto de conexión. Para más información, consulte [La cuenta de Microsoft en la empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Participación en datos de diagnóstico de Windows

<!--8,40,55,62-->
Esta propiedad comprueba que Windows esté configurado correctamente para permitir datos de diagnóstico. Así, comprueba el valor AllowTelemetry en las siguientes claves del Registro:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Compruebe los permisos de estas claves del Registro. Asegúrese de que la cuenta del sistema local pueda acceder a estas claves para establecer el cliente de Configuration Manager. También puede deberse al conflicto de un objeto de directiva de grupo. Para más información, consulte [Configuración de Windows](enroll-devices.md#windows-settings).  

Para más información, revise M365AHandler.log en el cliente.  

## <a name="see-also"></a>Vea también

[Solución de problemas de Análisis de escritorio](troubleshooting.md)
