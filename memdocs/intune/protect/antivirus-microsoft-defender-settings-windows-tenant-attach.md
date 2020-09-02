---
title: Configuración de la directiva de Windows 10 de Antivirus de Microsoft Defender para dispositivos con asociación de inquilinos | Microsoft Docs
description: Vea una lista de los valores de configuración del perfil de Antivirus de Microsoft Defender para dispositivos Windows 10 administrados por Configuration Manager. Estos valores se pueden configurar como parte de la directiva de antivirus de seguridad de puntos de conexión en Microsoft Intune después de configurar la asociación de inquilinos para Configuration Manager.
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
ms.openlocfilehash: 3bb1d4806271ab40c60f0ad419e4e708d36bbc97
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194130"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Configuración de la directiva de Antivirus de Microsoft Defender para dispositivos con asociación de inquilinos en Microsoft Intune

Vea la configuración de Antivirus de Microsoft Defender que puede administrar con el perfil **Microsoft Defender Antivirus Policy (ConfigMgr)** (Directiva de Antivirus de Microsoft Defender [ConfigMgr]) de Intune. El perfil está disponible cuando se configura la [directiva de antivirus de seguridad de punto de conexión](../protect/endpoint-security-antivirus-policy.md) y esta se implementa en los dispositivos que se administran con Configuration Manager cuando se ha configurado el escenario de [asociación de inquilinos](../protect/tenant-attach-intune.md).

## <a name="cloud-protection"></a>Protección de la nube

- **Activar la protección que proporciona la nube**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  De forma predeterminada, Defender en dispositivos de escritorio de Windows 10 envía información a Microsoft sobre los problemas que encuentre. Microsoft analiza esa información para obtener detalles sobre los problemas que le afectan a usted y a otros clientes a fin de ofrecer soluciones mejoradas.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No permitido.** Desactiva Microsoft Active Protection Service.
  - **Permitido.**  Activa Microsoft Active Protection Service.

- **Nivel de protección que proporciona la nube**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure el modo en que el antivirus de Defender bloquea y examina archivos sospechosos.
  - **No configurado** (*opción predeterminada*): nivel de bloqueo de Defender predeterminado.
  - **Alto**: bloquea de forma agresiva los archivos desconocidos mientras efectúa una optimización del rendimiento, lo que incluye una mayor posibilidad de falsos positivos.
  - **Más elevado**: bloquea de forma agresiva los archivos desconocidos y aplica medidas de protección adicionales, lo cual podría afectar al rendimiento del cliente.
  - **Tolerancia cero**: bloquea todos los archivos ejecutables desconocidos.

- **Tiempo de espera extendido en la nube en segundos de Defender**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  El antivirus de Defender bloquea automáticamente los archivos sospechosos durante 10 segundos, de manera que puede examinarlos en la nube para asegurarse de que son seguros. Con esta opción, puede agregar hasta 50 segundos adicionales a este tiempo de espera.

## <a name="microsoft-defender-antivirus-exclusions"></a>Exclusiones del antivirus de Microsoft Defender

Puede expandir cada opción de este grupo, seleccionar **Agregar** y, a continuación, especificar un valor para la exclusión.

- **Procesos que se van a excluir en Defender**  
  CSP: [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Especifique una lista de archivos abiertos por los procesos que se van a omitir durante un examen. El propio proceso no se excluye del examen.

- **Extensiones de archivo para excluir de exámenes y protección en tiempo real**  
  CSP: [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Especifique una lista de extensiones de tipo que se va a omitir durante un examen.

- **Archivos y carpetas que se van a excluir en Defender**  
  CSP: [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Especifique una lista de extensiones de archivos y rutas de acceso de directorio que se van a omitir durante un examen.

## <a name="real-time-protection"></a>Protección en tiempo real

- **Activar la protección en tiempo real**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Requerir que Defender en dispositivos Windows 10 Escritorio use la funcionalidad de supervisión en tiempo real.
  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No permitido.** Desactiva el servicio de supervisión en tiempo real.
  - **Permitido.** Activa y ejecuta el servicio de supervisión en tiempo real.

- **Habilitar la protección de acceso**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Configure la protección antivirus que está activa de forma continua, a diferencia de la protección a petición.

  - **No configurado** (*opción predeterminada*): esta directiva no modifica el estado de esta opción en un dispositivo. El estado existente en el dispositivo permanece inalterado.
  - **No permitido.** Desactiva el servicio de supervisión en tiempo real.
  - **Permitido.**

- **Supervisión de archivos entrantes y salientes**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Configure esta opción para determinar qué actividad de archivos y programas de NTFS se supervisa.
  - **Supervisar todos los archivos (bidireccional).** (*predeterminado*)
  - **Supervisar archivos entrantes.**
  - **Supervisar archivos salientes.**

- **Activar la supervisión de comportamiento**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  De forma predeterminada, Defender en dispositivos Windows 10 Escritorio usa la funcionalidad de supervisión de comportamiento.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No permitido.** Desactiva la supervisión del comportamiento.
  - **Permitido.** Activa la supervisión del comportamiento en tiempo real.

- **Permitir sistema de prevención de intrusiones**  
  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No permitido.**
  - **Permitido.**

- **Examinar todos los archivos y datos adjuntos descargados**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Configure Defender para examinar todos los archivos y datos adjuntos descargados.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No permitido.**
  - **Permitido.**

- **Examinar scripts que se usan en los exploradores de Microsoft**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Configure Defender para examinar scripts.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No permitido.**
  - **Permitido.**

- **Examinar archivos de red**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Configure Defender para examinar archivos de red.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No permitido.** Desactiva el examen de archivos de red.
  - **Permitido.** Examina los archivos de red.

- **Examinar correos electrónicos**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Configure Defender para examinar el correo entrante.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No permitido.** Desactiva el examen del correo electrónico.
  - **Permitido.** Activa el examen del correo electrónico.

## <a name="remediation"></a>Corrección

- **Número de días (0-90) para mantener el malware en cuarentena**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Especifique un número de días (de cero a noventa) que el sistema almacena los elementos en cuarentena antes de que se quiten automáticamente. Un valor de cero mantiene los elementos en cuarentena y no los quita automáticamente.

- **Enviar consentimiento de muestras**  

  - **Sin configurar** (*valor predeterminado*).
  - **Preguntar siempre.**
  - **Enviar muestras seguras automáticamente.**
  - **No enviar nunca.**
  - **Enviar todas las muestras automáticamente.**

- **Acción que se realiza en las aplicaciones potencialmente no deseadas**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Especifique el nivel de detección de aplicaciones potencialmente no deseadas (PUA). Defender alerta a los usuarios cuando se está descargando o intentando instalar software potencialmente no deseado en un dispositivo.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema (desactivado).
  - **PUA Protection off** (Protección de PUA desactivada). Windows Defender no protege frente a aplicaciones potencialmente no deseadas.
  - **PUA Protection on** (Protección de PUA activada). Los elementos detectados están bloqueados. Estos elementos se muestran en el historial junto con otras amenazas.
  - **Modo de auditoría.** Defender detecta aplicaciones potencialmente no deseadas, pero no toma ninguna medida. Puede revisar la información sobre las aplicaciones para las que Defender habría tomado medidas buscando eventos creados por Defender en el Visor de eventos.

- **Create a system restore point before computers are cleaned** (Crear un punto de restauración del sistema antes de limpiar los equipos)  
  - **Sí** (*valor predeterminado*)
  - **No**
  - **Not Configured** (No configurado)

- **Acciones para las amenazas detectadas**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Especifique la acción que Defender realiza para el malware detectado según el nivel de amenaza del malware.
  
  Defender clasifica el malware que detecta con uno de los siguientes niveles de gravedad:
  - **Low threat** (Amenaza baja)
  - **Moderate threat** (Amenaza moderada)
  - **High threat** (Amenaza alta)
  - **Severe threat** (Amenaza grave)

  Para cada nivel, especifique la acción que se va a realizar. El valor predeterminado para cada nivel de gravedad es *No configurado*.

  - **Sin configurar** (*valor predeterminado*).
  - **Limpiar**: el servicio intenta recuperar los archivos y desinfectarlos.
  - **Poner en cuarentena**: mueve los archivos a la cuarentena.
  - **Quitar**: quita archivos del dispositivo.
  - **Permitir**: permite el archivo y no toma otras medidas.
  - **Definido por el usuario**: el usuario del dispositivo toma la decisión sobre la acción que se debe realizar.
  - **Bloquear**: bloquea la ejecución de archivos.

## <a name="scan"></a>Examinar

- **Examinar archivos de almacenamiento**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Configure Defender para examinar archivos de almacenamiento, como archivos ZIP o CAB.

  - **No configurado** (*valor predeterminado*): el valor vuelve al valor predeterminado del cliente, que es examinar los archivos almacenados, aunque el usuario puede deshabilitar el examen.
Más información
  - **No permitido.** Desactiva el examen en archivos almacenados.
  - **Permitido.** Examina los archivos de almacenamiento.

- **Enable low CPU priority for scheduled scans** (Habilitar prioridad de CPU baja para exámenes programados)  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Configure la prioridad de CPU para los exámenes programados.
  - **No configurado** (*opción predeterminada*): la configuración vuelve al valor predeterminado del sistema, en el que no se realiza ningún cambio en la prioridad de la CPU.
  - **Deshabilitada**
  - **Habilitado**

- **Deshabilitar el análisis completo de puesta al día**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Configure los análisis de puesta al día para exámenes completos programados. Un análisis de puesta al día es un examen que se inicia porque falta un examen programado regularmente. Normalmente, estos exámenes programados se pierden porque se apagó el equipo a la hora programada.

  - **No configurado** (*opción predeterminada*): el valor se devuelve al valor predeterminado del cliente, que consiste en habilitar los análisis de puesta al día para exámenes completos, pero el usuario puede desactivarlos.
  - **Deshabilitada**
  - **Habilitado**

- **Deshabilitar examen rápido de puesta al día**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Configure los análisis de puesta al día para exámenes rápidos programados. Un análisis de puesta al día es un examen que se inicia porque falta un examen programado regularmente. Normalmente, estos exámenes programados se pierden porque se apagó el equipo a la hora programada.

  - **No configurado** (*opción predeterminada*): el valor se devuelve al valor predeterminado del cliente, que consiste en habilitar los análisis de puesta al día rápidos, pero el usuario puede desactivarlos.
  - **Deshabilitada**
  - **Habilitado**

- **CPU usage limit (0-100 percent) per scan** (Límite de uso de CPU [0-100 por ciento] por examen)  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Especificado como porcentaje de 0 a 100, es el factor de carga promedio de la CPU para el examen de Defender.

- **Enable mapped network drives be scanned during a full scan** (Habilitar la exploración de unidades de red asignadas durante un examen completo)  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Configure Defender para examinar unidades de red asignadas.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema, que deshabilita el examen en unidades de red asignadas.
  - **No permitido.** Deshabilita el examen en unidades de red asignadas.
  - **Permitido.** Examina las unidades de red asignadas.

- **Ejecutar un análisis rápido diario a las**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Seleccione la hora del día a la que se ejecutan los exámenes rápidos de Defender.
  De forma predeterminada, esta opción es **No configurado**.

- **Tipo de examen**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Seleccione el tipo de examen que ejecuta Defender.

  - **No configurado** *(valor predeterminado)*
  - **Examen rápido**
  - **Examen completo**

- **Día de la semana para ejecutar un examen programado**  
  - **No configurado** (*valor predeterminado*)

- **Hora del día para ejecutar un examen programado**  
  - **No configurado** *(valor predeterminado)*

- **Comprobar las actualizaciones de las firmas antes de ejecutar el examen**  
  - **No configurado** (*valor predeterminado*)
  - **Deshabilitada**
  - **Habilitado**

- **Randomize scheduled scan and security intelligence update start times** (Aleatorizar las horas de inicio de examen programado y actualización de inteligencia de seguridad)  
  -**No configurado** (*valor predeterminado*) -**Sí**
  -**No**

- **Examinar unidades extraíbles durante examen completo**
  - **No configurado** (*valor predeterminado*)
  - **No permitido.** Desactiva el examen en unidades extraíbles.
  - **Permitido.** Examina las unidades extraíbles.

## <a name="updates"></a>Actualizaciones

- **Escriba la frecuencia (0-24 horas) para comprobar las actualizaciones de inteligencia de seguridad**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Especifique el intervalo de 0 a 24 (en horas) que se usa para comprobar las firmas. Un valor de cero se traduce en no comprobar las nuevas firmas. Un valor de 2 comprobará cada dos horas, etc.

- **Signature Update Fallback Order (Device)** (Orden de reserva de actualización de firma [dispositivo])

- **Signature Update File Shares Sources (Device)** (Orígenes de recursos compartidos de archivos de actualización de firmas [dispositivo])

- **Security Intelligence Location (Device)** (Ubicación de inteligencia de seguridad [dispositivo])  

## <a name="user-experience"></a>Experiencia del usuario

- **Bloquear el acceso de usuarios a la aplicación de Microsoft Defender**  
  - **No configurado** (*valor predeterminado*)
  - **No permitido.** Impide que los usuarios tengan acceso a la interfaz de usuario.
  - **Permitido.** Permite que los usuarios tengan acceso a la interfaz de usuario.

- **Show notifications messages on the client computer when the user needs to run a full scan, update security intelligence, or run Windows Defender Offline** (Mostrar mensajes de notificación en el equipo cliente cuando el usuario necesite ejecutar un examen completo, actualizar la inteligencia de seguridad o ejecutar Windows Defender sin Conexión)  
  - **No configurado** (*valor predeterminado*)
  - **Sí**
  - **No**

- **Disable the client user interface** (Deshabilitar la interfaz de usuario del cliente)  
  - **No configurado** (*valor predeterminado*)
  - **Sí**
  - **No**

- **Allow users to view full History results** (Permitir que los usuarios vean los resultados completos del historial)
  - **No configurado** (*valor predeterminado*)
  - **Sí**
  - **No**