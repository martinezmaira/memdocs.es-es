---
title: Configuración de la directiva antivirus de Windows 10 para el antivirus de Microsoft Defender para Intune | Microsoft Docs
description: Vea una lista de los valores de configuración en el perfil del antivirus de Microsoft Defender para Windows 10. Puede configurar estos valores como parte de la directiva del antivirus de seguridad de puntos de conexión en Microsoft Intune.
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
ms.openlocfilehash: ff5c8208cb1ee9357c501a3c457bc346879b241d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906708"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Configuración de la directiva antivirus de Microsoft Defender para Windows 10 en Microsoft Intune

Vea las opciones de directiva de antivirus de seguridad de puntos de conexión que se pueden configurar para el perfil de antivirus de Microsoft Defender para Windows 10 en Microsoft Intune como parte de una [directiva de seguridad de puntos de conexión](../protect/endpoint-security-policy.md).

## <a name="cloud-protection"></a>Protección de la nube

Esta configuración está disponible en los siguientes perfiles:

- Antivirus de Microsoft Defender

**Configuración**:

- **Activar la protección que proporciona la nube**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  De forma predeterminada, Defender en dispositivos de escritorio de Windows 10 envía información a Microsoft sobre los problemas que encuentre. Microsoft analiza esa información para obtener detalles sobre los problemas que le afectan a usted y a otros clientes a fin de ofrecer soluciones mejoradas.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: la protección en la nube está activa.  Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Nivel de protección que proporciona la nube**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure el modo en que el antivirus de Defender bloquea y examina archivos sospechosos.
  - **No configurado** (*opción predeterminada*): nivel de bloqueo de Defender predeterminado.
  - **Alto**: bloquea de forma agresiva los archivos desconocidos mientras efectúa una optimización del rendimiento, lo que incluye una mayor posibilidad de falsos positivos.
  - **Más elevado**: bloquea de forma agresiva los archivos desconocidos y aplica medidas de protección adicionales, lo cual podría afectar al rendimiento del cliente.
  - **Tolerancia cero**: bloquea todos los archivos ejecutables desconocidos.

- **Tiempo de espera extendido en la nube en segundos de Defender**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  El antivirus de Defender bloquea automáticamente los archivos sospechosos durante 10 segundos, de manera que puede examinarlos en la nube para asegurarse de que son seguros. Puede agregar hasta 50 segundos adicionales a este tiempo de espera.

## <a name="microsoft-defender-antivirus-exclusions"></a>Exclusiones del antivirus de Microsoft Defender

Esta configuración está disponible en los siguientes perfiles:

- Antivirus de Microsoft Defender
- Exclusiones del antivirus de Microsoft Defender

**Configuración**:

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

Esta configuración está disponible en los siguientes perfiles:

- Antivirus de Microsoft Defender

**Configuración**:

- **Activar la protección en tiempo real**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Requerir que Defender en dispositivos Windows 10 Escritorio use la funcionalidad de supervisión en tiempo real.
  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: forzar el uso de la supervisión en tiempo real. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Habilitar la protección de acceso**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Configure la protección antivirus que está activa de forma continua, a diferencia de la protección a petición.

  - **No configurado** (*opción predeterminada*): esta directiva no modifica el estado de esta opción en un dispositivo. El estado existente en el dispositivo permanece inalterado.
  - **No**: bloqueo de la protección de acceso de los dispositivos. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: la protección de acceso está activa en los dispositivos.

- **Supervisión de archivos entrantes y salientes**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Configure esta opción para determinar qué actividad de archivos y programas de NTFS se supervisa.
  - **Supervisar todos los archivos** (*valor predeterminado*)
  - **Supervisar solo los archivos entrantes**
  - **Supervisar solo los archivos salientes**

- **Activar la supervisión de comportamiento**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  De forma predeterminada, Defender en dispositivos Windows 10 Escritorio usa la funcionalidad de supervisión de comportamiento.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: forzar el uso de la supervisión de comportamiento en tiempo real. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Activar la protección de red**  
  CSP: [EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Proteja a los usuarios de dispositivos para que al usar cualquier aplicación no accedan a estafas de suplantación de identidad (phishing), sitios de hospedaje de vulnerabilidades y contenido malintencionado en Internet. Esta protección incluye impedir que exploradores de terceros se conecten a sitios peligrosos.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: la protección de red está activada. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Examinar todos los archivos y datos adjuntos descargados**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Configure Defender para examinar todos los archivos y datos adjuntos descargados.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: Defender examina todos los archivos y datos adjuntos descargados. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Examinar scripts que se usan en los exploradores de Microsoft**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Configure Defender para examinar scripts.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: Defender examina los scripts. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Examinar archivos de red**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Configure Defender para examinar archivos de red.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: activar el análisis de los archivos de red. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Examinar correos electrónicos**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Configure Defender para examinar el correo entrante.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: activar el análisis de correo electrónico. Los usuarios de los dispositivos no pueden cambiar esta opción.

## <a name="remediation"></a>Corrección

Esta configuración está disponible en los siguientes perfiles:

- Antivirus de Microsoft Defender

**Configuración**:

- **Número de días (0-90) para mantener el malware en cuarentena**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Especifique un número de días (de cero a noventa) que el sistema almacena los elementos en cuarentena antes de que se quiten automáticamente. Un valor de cero mantiene los elementos en cuarentena y no los quita automáticamente.

- **Enviar consentimiento de muestras**  

  - **Sin configurar** (*valor predeterminado*).
  - **Enviar muestras seguras automáticamente**
  - **Preguntar siempre**
  - **No enviar nunca**
  - **Enviar todas las muestras automáticamente**

- **Acción que se realiza en las aplicaciones potencialmente no deseadas**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Especifique el nivel de detección de aplicaciones potencialmente no deseadas (PUA). Defender alerta a los usuarios cuando se está descargando o intentando instalar software potencialmente no deseado en un dispositivo.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema (desactivado).
  - **Deshabilitar**
  - **Habilitar**: los elementos detectados se bloquean y se muestran en el historial junto con otras amenazas.
  - **Modo de auditoría**: Defender detecta aplicaciones potencialmente no deseadas pero no toma ninguna medida. Puede revisar la información sobre las aplicaciones para las que Defender habría tomado medidas buscando eventos creados por Defender en el Visor de eventos.

- **Acciones para las amenazas detectadas**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Especifique la acción que Defender realiza para el malware detectado según el nivel de amenaza del malware.
  
  Defender clasifica el malware que detecta con uno de los siguientes niveles de gravedad:
  - **Gravedad baja**
  - **Gravedad moderada**
  - **Gravedad alta**
  - **Gravedad muy alta**

  Para cada nivel, especifique la acción que se va a realizar. El valor predeterminado para cada nivel de gravedad es *No configurado*.

  - **No configurado**.
  - **Limpiar**: el servicio intenta recuperar los archivos y desinfectarlos.
  - **Poner en cuarentena**: mueve los archivos a la cuarentena.
  - **Quitar**: quita archivos del dispositivo.
  - **Permitir**: permite el archivo y no toma otras medidas.
  - **Definido por el usuario**: el usuario del dispositivo toma la decisión sobre la acción que se debe realizar.
  - **Bloquear**: bloquea la ejecución de archivos.

## <a name="scan"></a>Examinar

Esta configuración está disponible en los siguientes perfiles:

- Antivirus de Microsoft Defender

**Configuración**:

- **Examinar archivos de almacenamiento**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Configure Defender para examinar archivos de almacenamiento, como archivos ZIP o CAB.

  - **No configurado** (*valor predeterminado*): el valor vuelve al predeterminado del cliente, que es examinar los archivos almacenados, aunque el usuario puede deshabilitarlo.
Obtener más información
  - **No**: los archivos de almacenamiento no se examinan. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: habilitar los exámenes de los archivos de almacenamiento. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Usar la prioridad baja de CPU para los exámenes programados**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Configure la prioridad de CPU para los exámenes programados.
  - **No configurado** (*opción predeterminada*): la configuración vuelve al valor predeterminado del sistema, en el que no se realiza ningún cambio en la prioridad de la CPU.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: la prioridad de la CPU baja se usará durante los exámenes programados. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Deshabilitar el análisis completo de puesta al día**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Configure los análisis de puesta al día para exámenes completos programados. Un examen de puesta al día es un examen que se inicia porque se ha perdido un examen programado regularmente. Normalmente, estos exámenes programados se pierden porque se apagó el equipo a la hora programada.

  - **No configurado** (*opción predeterminada*): el valor se devuelve al valor predeterminado del cliente, que consiste en habilitar los análisis de puesta al día para exámenes completos, pero el usuario puede desactivarlos.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: se aplican los análisis de puesta al día de los exámenes completos programados y el usuario no los puede deshabilitar. Si un equipo está sin conexión durante dos exámenes programados consecutivos, se inicia un examen de puesta al día la próxima vez que alguien inicia sesión en el equipo. Si no hay ningún examen programado configurado, no se ejecutará el análisis de puesta al día. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Deshabilitar examen rápido de puesta al día**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Configure los análisis de puesta al día para exámenes rápidos programados. Un examen de puesta al día es un examen que se inicia porque se ha perdido un examen programado regularmente. Normalmente, estos exámenes programados se pierden porque se apagó el equipo a la hora programada.

  - **No configurado** (*opción predeterminada*): el valor se devuelve al valor predeterminado del cliente, que consiste en habilitar los análisis de puesta al día rápidos, pero el usuario puede desactivarlos.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: se aplican los análisis de puesta al día de los exámenes rápidos programados y el usuario no los puede deshabilitar. Si un equipo está sin conexión durante dos exámenes programados consecutivos, se inicia un examen de puesta al día la próxima vez que alguien inicia sesión en el equipo. Si no hay ningún examen programado configurado, no se ejecutará el análisis de puesta al día. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Límite de uso de CPU por examen**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Especificado como porcentaje de 0 a 100, es el factor de carga promedio de la CPU para el examen de Defender.

- **Examinar unidades de red asignadas durante examen completo**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Configure Defender para examinar unidades de red asignadas.

  - **No configurado** (*opción predeterminada*): la opción se restaura al valor predeterminado del sistema, que deshabilita el examen en unidades de red asignadas.
  - **No**: la opción está deshabilitada. Los usuarios de los dispositivos no pueden cambiar esta opción.
  - **Sí**: habilitar los exámenes de las unidades de red asignadas. Los usuarios de los dispositivos no pueden cambiar esta opción.

- **Ejecutar un análisis rápido diario a las**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Seleccione la hora del día a la que se ejecutan los exámenes rápidos de Defender.
  De forma predeterminada, este valor es **No configurado**.

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
  - **No**
  - **Sí**

## <a name="updates"></a>Actualizaciones

Esta configuración está disponible en los siguientes perfiles:

- Antivirus de Microsoft Defender

**Configuración**:

- **Escriba la frecuencia (0-24 horas) para comprobar las actualizaciones de inteligencia de seguridad**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Especifique el intervalo de 0 a 24 (en horas) que se usa para comprobar las firmas. Un valor de cero se traduce en no comprobar las nuevas firmas. Un valor de 2 comprobará cada dos horas, etc.

- **Definir recursos compartidos de archivos para descargar actualizaciones de definiciones**  
  CSP: [SignatureUpdateFallbackOrder](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

  Administre ubicaciones, por ejemplo, un recurso compartido de archivos UNC,como origen de la descarga para obtener actualizaciones de las definiciones. Una vez que se hayan descargado correctamente las actualizaciones de las definiciones de un origen especificado, no se contactarán los orígenes restantes de la lista.

  Puede **Agregar** ubicaciones individuales o **Importar** una lista de ubicaciones como un archivo .csv.

- **Definir orden de los orígenes para descargar actualizaciones de definiciones**  
  CSP: [SignatureUpdateFileSharesSources](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)

  Especifique el orden en el que hay que contactar con las ubicaciones de origen que ha especificado para obtener actualizaciones de las definiciones. Una vez que se hayan descargado correctamente las actualizaciones de las definiciones de un origen especificado, no se contactarán los orígenes restantes de la lista.

## <a name="user-experience"></a>Experiencia del usuario

Esta configuración está disponible en los siguientes perfiles:

- Antivirus de Microsoft Defender

**Configuración**:

- **Permitir el acceso de usuarios a la aplicación de Microsoft Defender**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **No configurado** (*opción predeterminada*): la configuración vuelve al valor predeterminado del cliente en el que se permiten la interfaz de usuario y las notificaciones.
  - **No**: no se puede acceder a la interfaz de usuario (IU) de Defender y se suprimen las notificaciones.
  - **Sí**