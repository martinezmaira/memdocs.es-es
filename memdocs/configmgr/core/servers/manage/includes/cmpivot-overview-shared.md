---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 8e95fce122a3e153f2aa391dcd5e40439f8e5820
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704584"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>Consultas

Las consultas se pueden usar para buscar términos, identificar tendencias, analizar patrones y proporcionar mucha más información basada en sus datos. CMPivot usa un subconjunto del modelo de flujo de datos de [Azure Log Analytics](/azure/kusto/query) para la instrucción de expresión tabular. La estructura típica de una instrucción de expresión tabular es una composición de entidades cliente y operadores de datos tabulares (como filtros y proyecciones). La composición se representa mediante el carácter de barra vertical (|), lo cual confiere a la instrucción un formato regular que representa visualmente el flujo de datos tabulares de izquierda a derecha. Cada operador acepta un conjunto de datos tabulares "de la canalización", así como entradas adicionales (incluidos otros conjuntos de datos tabulares) del cuerpo del operador y, después, emite un conjunto de datos tabulares para el operador siguiente: `entity | operator1 | operator2 | ...`

En el ejemplo siguiente, la entidad es `CCMRecentlyUsedApplications` (una referencia a las aplicaciones usadas recientemente) y el operador es where (que filtra los registros a partir de su entrada según ciertos predicados por registro):

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>Entities

Las entidades son objetos que se pueden consultar desde el cliente. Actualmente se admiten las siguientes entidades:


|Entidad|Descripción|
|---|---|
|AadStatus|Estado de Azure Active Directory|
|Administradores|Miembros del grupo de administradores local|
|AppCrash|Informes de bloqueos de aplicación recientes|
|AppVClientApplication|Aplicación de cliente de AppV|
|AppVClientPackage|Paquete de cliente de AppV|
|AutoStartSoftware|Software que se inicia automáticamente con o el sistema operativo o inmediatamente después|
|Placa base|Placa base|
|Batería|Batería|
|Bios|Información de BIOS del sistema|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|Detalles de cifrado de BitLocker|
|BitLockerPolicy|Directiva de BitLocker|
|BootConfiguration|Configuración de arranque|
|BrowserHelperObject|Objeto auxiliar de explorador|
|BrowserUsage|Uso del explorador|
|CcmLog()|Líneas en un plazo de 24 horas (de forma predeterminada) de un archivo de registro de CCM|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|Aplicaciones usadas recientemente|
|CCMWebAppInstallInfo|Aplicaciones web|
|CDROM|Unidad de CD-ROM|
|ClientEvents|Eventos de cliente|
|ComputerSystem|Sistema de equipo|
|ComputerSystemEx|Extensión del sistema del equipo|
|ComputerSystemProduct|Producto de sistema del equipo|
|ConnectedDevice|Dispositivo conectado|
|Conexión|Una conexión TCP activa dentro o fuera del dispositivo|
|Escritorio|Escritorio|
|DesktopMonitor|Monitor de escritorio|
|Dispositivo|Información básica sobre el dispositivo|
|Disco|Información del dispositivo de almacenamiento local en un equipo con Windows|
|DMA|DMA|
|DMAChannel|Canal DMA|
|DriverVxD|Controlador: VxD|
|EmbeddedDeviceInformation|Información de dispositivo incrustado|
|Entorno|Entorno|
|EPStatus|Estado del software antimalware en el equipo|
|EventLog()|Eventos en un plazo de 24 horas (de forma predeterminada) de un registro de eventos de Windows|
|File()|Información acerca de un archivo específico|
|FileShare|Información del recurso compartido de archivos activo|
|Firmware|Firmware|
|IDEController|Controlador IDE|
|InstalledExecutable|Ejecutable instalado|
|InstalledSoftware|Una aplicación instalada en el dispositivo|
|IPConfig|Obtiene la configuración de red, incluidas las interfaces, direcciones IP y servidores DNS utilizables.|
|IRQTable|Tabla IRQ|
|Teclado|Teclado|
|LoadOrderGroup|Cargar orden de grupo|
|LogicalDisk|Disco lógico|
|MDMDevDetail|Información del dispositivo|
|Memoria|Memoria|
|Módem|Módem|
|Placa base|Placa base|
|NetworkAdapter|Adaptador de red|
|NetworkAdapterConfiguration|Configuración del adaptador de red|
|NetworkClient|Cliente de red|
|NetworkLoginProfile|Perfil de inicio de sesión de red|
|NTEventlogFile|Archivo de registro de eventos NT|
|Configuraciones de Office 365 ProPlus|Configuraciones de Office 365 ProPlus|
|OfficeAddin|Complementos de Office|
|OfficeClientMetric|Métrica del cliente de Office|
|OfficeDeviceSummary|Resumen del dispositivo de Office|
|OfficeDocumentMetric|Métricas de documentos de Office|
|OfficeDocumentSolution|Solución del documento de Office|
|OfficeMacroError|Error de macro de Office|
|OfficeProductInfo|Información del producto de Office|
|OfficeVbaRuleViolation|Infracción de regla VBA de Office|
|OfficeVbaSummary|Resumen del examen de VBA de Office|
|OperatingSystem|Sistema operativo|
|OperatingSystemEx|Extensión del sistema operativo|
|OperatingSystemRecoveryConfiguration|Configuración de recuperación del sistema operativo|
|OptionalFeature|Característica opcional|
|Sistema operativo|Información básica sobre el sistema operativo|
|PageFileSetting|Configuración de archivo de página|
|ParallelPort|Puerto paralelo|
|Partición|Particiones de disco|
|PCMCIAController|Controladora PCMCIA|
|Disco físico|Disco físico|
|PhysicalMemory|Memoria física|
|PNPDEVICEDRIVER|Controlador de dispositivo PNP|
|PointingDevice|Dispositivo señalador|
|PortableBattery|Batería portátil|
|Puertos|Puertos|
|PowerCapabilities|Capacidades de energía|
|PowerClientOptOutSettings|Configuración de exclusión de administración de energía|
|PowerConfigurations|Configuración de energía|
|PowerManagementDaily|Datos diarios de administración de energía|
|PowerManagementInsomniaReasons|Motivos de activación de energía|
|PowerManagementMonthly|Datos mensuales de administración de energía|
|PowerSettings|Configuración de energía|
|PrinterConfiguration|Configuración de la impresora|
|PrinterDevice|Dispositivo de impresión|
|PrintJobs|Trabajos de impresión|
|Proceso|Un proceso en un sistema operativo|
|ProcessModule()|Módulos cargados por los procesos especificados|
|Procesador|Procesador|
|ProtectedVolumeInformation|Información de volumen protegido|
|Protocolo|Protocolo|
|QuickFixEngineering|Ingeniería de corrección rápida|
|SCSIController|Controladora SCSI|
|SerialPortConfiguration|Configuración de puerto serie|
|SerialPorts|Puertos serie|
|ServerFeature|Característica de servidor|
|Servicio|Un servicio en un sistema de equipos que ejecuta Windows|
|Servicios|Servicios|
|Recursos compartidos|Recursos compartidos|
|SMBConfig|Configuración SMB de un dispositivo|
|SMSAdvancedClientPorts|Puertos de cliente de Configuration Manager|
|SMSAdvancedClientSSLConfigurations|Configuraciones SSL de cliente de Configuration Manager|
|SMSAdvancedClientState|Estado del cliente de Configuration Manager|
|SMSDefaultBrowser|Explorador predeterminado|
|SMSSoftwareTag|Etiqueta de software|
|SMSWindows8Application|Aplicación de Windows|
|SMSWindows8ApplicationUserInfo|Información de usuarios de aplicaciones de Windows|
|SoftwareShortcut|Acceso directo de software|
|SoftwareUpdate|Una actualización de software aplicable, pero no instalada en el dispositivo|
|SoundDevices|Dispositivos de sonido|
|SWLicensingProduct|Producto de licencia de software|
|SWLicensingService|Servicio de licencias de software|
|SystemAccount|Cuenta del sistema|
|SystemBootData|Datos de arranque del sistema|
|SystemBootSummary|Resumen de arranque del sistema|
|SystemConsoleUsage|Uso de la consola del sistema|
|SystemConsoleUser|Usuario de la consola del sistema|
|SystemDevices|Dispositivos del sistema|
|SystemDrivers|Controladores del sistema|
|SystemEnclosure|Revestimiento de hardware del sistema|
|TapeDrive|Unidad de cinta|
|TimeZone|Zona horaria|
|TPM|TPM|
|TPMStatus|Estado de TPM|
|TSIssuedLicense|Licencia emitida de TS|
|TSLicenseKeyPack|Paquete de claves de licencia de TS|
|UninterruptiblePowerSupply|Sistema de alimentación ininterrumpida|
|USBController|Controladora USB|
|USBDevice|Dispositivo USB|
|Usuario|Una cuenta de usuario con una conexión activa al dispositivo|
|USMFolderRedirectionHealth|Mantenimiento de redirección de carpetas|
|USMUserProfile|Mantenimiento de perfil de usuario|
|VideoController|Controladora de vídeo|
|VirtualMachine|Máquina virtual|
|VirtualMachine64|Máquina virtual (64)|
|Volumen|Volumen|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Versión del agente de Windows Update|
|WinEvent()|Eventos en un plazo de 24 horas (de forma predeterminada) de un registro de eventos de Windows|
|WriteFilterState|Estado de filtro de escritura|

## <a name="table-operators"></a>Operadores de tabla

Los operadores de tabla se pueden usar para filtrar, resumir y transformar flujos de datos. Actualmente, son compatibles los siguientes operadores:

|Operadores de tabla|Descripción|
|---|---|
|count|Devuelve una tabla con un solo registro que contiene el número de registros.|
|distinct|Genera una tabla con las distintas combinaciones de las columnas proporcionadas de la tabla de entrada.|
|join|Combina las filas de dos tablas para formar una nueva tabla mediante la coincidencia de fila para el mismo dispositivo|
|order by|Ordena las filas de la tabla de entrada por una o más columnas.|
|project|Selecciona las columnas que se van a incluir, cambiar de nombre o colocar e inserta las nuevas columnas calculadas.|
|summarize|Genera una tabla que agrega el contenido de la tabla de entrada.|
|take|Devuelve hasta el número de filas especificado.|
|top|Devuelve los primeros N registros ordenados por las columnas especificadas.|
|where|Filtra una tabla al subconjunto de filas que cumplen un predicado.|

## <a name="scalar-operators"></a>Operadores escalares

La siguiente tabla resume los operadores:

|Operadores|Descripción|Ejemplo
|---|---|---|
|==|Igual|`1 == 1, 'aBc' == 'AbC'`|
|!=|No es igual|`1 != 2, 'abc' != 'abcd'`|
|< |Menor|`1 < 2, 'abc' < 'DEF'`|
|> |Mayor|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Menor o igual a|`1 <= 2, 'abc' <= 'abc'`|
|>=|Mayor o igual a|`2 >= 1, 'abc' >= 'ABC'`|
|+|Agregar|`2 + 1, now() + 1d`|
|-|Restar|`2 - 1, now() - 1h`|
|*|Multiplicar|`2 * 2`|
|/|Dividir|`2 / 1`|
|%|Módulo|`2 % 1`|
|like|El lado izquierdo (LHS) contiene a una coincidencia con el lado derecho (RHS)|`'abc' like '%B%'`|
|!like|LHS no contiene ninguna coincidencia para RHS|`'abc' !like '_d_'`|
|contiene|RHS ocurre como una subsecuencia de LHS|`'abc' contains 'b'`|
|!contains|RHS no se produce en LHS|`'team' !contains 'i'`|
|startswith|RHS es una subsecuencia inicial de LHS|`'team' startswith 'tea'`|
|!startswith|RHS no es una subsecuencia inicial de LHS|`'abc' !startswith 'bc'`|
|endswith|RHS es una subsecuencia de cierre de LHS|`'abc' endswith 'bc'`|
|!endswith|RHS no es una subsecuencia de cierre de LHS|`'abc' !endswith 'a'`|
|y|True solo si RHS y LHS son true|`(1 == 1) and (2 == 2)`|
|o bien|True solo si RHS o LHS son true|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>Funciones de agregación

Las funciones de agregación se pueden usar con el operador de tabla summarize para calcular valores resumidos. Actualmente se admiten las funciones de agregación siguientes:

|Función|Descripción|
|---|---|
|avg()|Devuelve la media de los valores de todo el grupo|
|count()|Devuelve un recuento de los registros por grupo de resumen|
|countif()|Devuelve un recuento de las filas para las que el predicado se evalúa como true|
|dcount()|Devuelve el número de valores distintos en el grupo|
|max()|Devuelve el valor máximo de todo el grupo|
|min()|Devuelve el valor mínimo de todo el grupo|
|percentile()|Devuelve una estimación para el percentil más próximo a la clasificación especificada de la población definida por la expresión|
|sum()|Devuelve la suma de los valores de todo el grupo|
|sumif()|Devuelve una suma de Expresión para la que Predicado se evalúa como true|

## <a name="scalar-functions"></a>Funciones escalares

Las funciones escalares se pueden usar en expresiones. Actualmente se admiten las funciones escalares siguientes:

|Función|Descripción|
|---|---|
|ago()|resta el intervalo de tiempo dado de la hora UTC actual.|
|bin()|Redondea valores a la baja a un número de fecha y hora múltiplo del tamaño de una ubicación determinada.|
|case()|Evalúa una lista de predicados y devuelve la primera expresión de resultado cuyo predicado se cumpla|
|datetime_add()|Calcula un nuevo valor datetime partir de un valor datepart especificado que se multiplica por una cantidad determinada y se suma a un valor datetime indicado.|
|datetime_diff()|Calcula la diferencia entre dos valores de fecha y hora.|
|iif()|Evalúa el primer argumento y devuelve el valor del segundo o tercer argumento en función de si el predicado se ha evaluado como true (el segundo) o false (el tercero)|
|indexof()|La función notifica el índice de base cero de la primera repetición de una cadena especificada dentro de la cadena de entrada|
|isnotnull()|Evalúa su único argumento y devuelve un valor booleano que indica si el argumento se evalúa como valor no NULL.|
|isnull()|Evalúa su único argumento y devuelve un valor booleano que indica si el argumento se evalúa como valor NULL.|
|now()|devuelve la hora de reloj UTC actual.|
|strcat()|Concatena entre 1 y 64 argumentos|
|strlen()|Devuelve la longitud, en caracteres, de la cadena de entrada|
|substring()|Extrae una subcadena de una cadena de origen desde un índice hasta el final de la cadena|
|tostring()|Convierte la entrada en una representación de cadena.|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Entidades, operadores y funciones adicionales para CMPivot desde Configuration Manager

> [!Important]
> Estos elementos no se admiten al ejecutar CMPivot desde el centro de administración de Microsoft Endpoint Manager.

|Tipo|Elemento|Descripción|
|--|--|---|
|Entidad|AccountSID|SID de cuenta|
|Entidad|FileContent()|Contenido de un archivo específico|
|Entidad|NAPClient|Cliente NAP|
|Entidad|NAPSystemHealthAgent|Agente de mantenimiento del sistema de NAP|
|Entidad|Registry()|Todos los valores de una clave del Registro específica<!--7371183-->|
|Operador de tabla|render|Representa los resultados como salida gráfica|