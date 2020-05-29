---
title: Acerca de los archivo de registro
titleSuffix: Configuration Manager
description: Use los archivos de registro para solucionar problemas con los clientes y sistemas de sitio de Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 588bccc533909f2438dc61d6f25b39c3a582c71b
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879024"
---
# <a name="about-log-files-in-configuration-manager"></a>Acerca de los archivos de registro en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En Configuration Manager, los componentes de cliente y servidor de sitio registran información de proceso en archivos de registro individuales. Se puede usar la información de estos archivos de registro para facilitar la solución de los problemas que puedan producirse. De forma predeterminada, Configuration Manager habilita el registro para los componentes de cliente y servidor.

En este artículo se proporciona información general sobre los archivos de registro de Configuration Manager. Incluye las herramientas a usar, cómo configurar los registros y dónde encontrarlos. Para obtener más información sobre archivos de registro específicos, consulte [Referencia del archivo de registro](log-files.md).


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a> Cómo funciona

La mayoría de los procesos de Configuration Manager escriben información operativa en un archivo de registro dedicado al proceso de que se trate. Los archivos de registro se identifican mediante las extensiones de archivo **.log** o **.lo_** . Configuration Manager escribe en un archivo .log hasta que dicho registro alcanza su tamaño máximo. Cuando el registro está lleno, el archivo .log se copia en un archivo con el mismo nombre pero con la extensión .lo_, y el proceso o el componente continúa escribiendo en el archivo .log. Cuando el archivo .log vuelve a alcanzar el tamaño máximo, se sobrescribe el archivo .lo_ y el proceso se repite. Algunos componentes establecen un historial de archivos de registro al anexar una marca de fecha y hora al nombre del archivo de registro y al conservar la extensión .log.


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a> Herramientas del visor de registros

Todos los archivos de registro de Configuration Manager son texto sin formato, de modo que puede verlos con cualquier lector de texto como, por ejemplo, el Bloc de notas. Los registros usan un formato único que se visualiza mejor con una de las siguientes herramientas especializadas:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Visor de registros del Centro de soporte técnico](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

Para ver los registros, use la herramienta del visor de registros de Configuration Manager **CMTrace**. Se encuentra en la carpeta `\SMSSetup\Tools` del medio de origen de Configuration Manager. La herramienta CMTrace también se agrega a todas las imágenes de arranque que se agregan a la Biblioteca de software. La herramienta de visualización de registros CMTrace se instala automáticamente junto con el cliente de Configuration Manager.<!--1357971--> Para obtener más información, vea [CMTrace](../../support/cmtrace.md).

### <a name="onetrace"></a>OneTrace

A partir de la versión 1906, **OneTrace** es un nuevo visor de registros del Centro de soporte técnico. Funciona de manera similar a CMTrace, pero con mejoras. Para obtener más información, consulte [Centro de soporte técnico OneTrace](../../support/support-center-onetrace.md).

### <a name="support-center-log-viewer"></a>Visor de registros del Centro de soporte técnico

El **Centro de soporte técnico** incluye un moderno visor de registros. Esta herramienta reemplaza a CMTrace y proporciona una interfaz personalizable que admite pestañas y ventanas acoplables. Tiene una capa de presentación rápida y puede cargar archivos de registro de gran tamaño en segundos. Para obtener más información, consulte [Referencia del visor de registros del Centro de soporte técnico](../../support/support-center-ui-reference.md#bkmk_log-viewer).

> [!Note]  
> El Centro de soporte técnico y OneTrace usan Windows Presentation Foundation (WPF). Este componente no está disponible en Windows PE. Siga usando CMTrace en las imágenes de arranque con implementaciones de secuencia de tareas.


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a> Configuración de opciones de registro

Puede cambiar la configuración de los archivos de registro, como el nivel detallado, el tamaño y el historial. Hay varias formas de cambiar esta configuración:

- [Durante la instalación de cliente](#bkmk_logoptions-clientprop)
- [Uso del Administrador de servicios de Configuration Manager](#bkmk_logoptions-sm)
- [Uso del Registro de Windows](#bkmk_logoptions-registry)
- [En la consola de Configuration Manager](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a> Configuración de opciones de registro durante la instalación de cliente

Puede establecer la configuración de los archivos de registro del cliente durante la instalación. Use las propiedades siguientes:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

Para obtener más información, vea [Acerca de las propiedades de instalación de clientes](../../clients/deploy/about-client-installation-properties.md#clientMsiProps).

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a> Configuración de opciones de registro mediante el Administrador de servicios de Configuration Manager

Puede cambiar dónde almacena Configuration Manager los archivos de registro y su tamaño.  

Para modificar el tamaño de los archivos de registro, cambiar el nombre y la ubicación de estos archivos y forzar a varios componentes a escribir en un único archivo de registro, siga estos pasos:  

#### <a name="modify-logging-for-a-component"></a>Modificación del registro de un componente  

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado del sistema** y, a continuación, seleccione **Estado del sitio** o **Estado del componente**.  

2. En la cinta de opciones, seleccione **Inicio** y, a continuación, **Administrador de servicios de Configuration Manager**.  

3. Cuando se abra el Administrador de servicios de Configuration Manager, conéctese al sitio que quiere administrar. Si no aparece el sitio que quiere administrar, seleccione **Sitio**, **Conectar** y, luego, escriba el nombre del servidor de sitio del sitio correcto.  

4. Expanda el sitio y vaya a **Componentes** o **Servidores**, según la ubicación de los componentes que quiera administrar.  

5. En el panel derecho, seleccione uno o más componentes.  

6. En el menú **Componente**, seleccione **Registro**.  

7. En el cuadro de diálogo **Registro de componentes de Configuration Manager** , complete las opciones de configuración disponibles para la selección.  

8. Seleccione **Aceptar** para guardar la configuración.  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a> Configuración de opciones de registro mediante el Registro de Windows

<!-- SCCMDocs#992 -->
Use el Registro de Windows en los servidores o clientes para cambiar las siguientes opciones de registro:

- Nivel detallado
- Historial máximo
- Tamaño máximo

Al solucionar un problema, puede habilitar el registro detallado para que Configuration Manager escriba detalles adicionales en los archivos de registro.

> [!Warning]
> Un error en esta configuración puede hacer que Configuration Manager registre grandes cantidades de información o nada en absoluto. Aunque estos datos pueden resultar beneficiosos a la hora de solucionar los problemas, tenga cuidado al cambiar estos valores en los sitios de producción. Pruebe siempre estos cambios primero en un entorno de laboratorio. Puede producirse un registro excesivo, lo que podría hacer que resultase difícil encontrar información relevante en los archivos de registro.

Una vez que realice cambios en esta configuración del Registro, reinicie el componente:

- Si cambia la configuración de cliente, reinicie el servicio **Host de agente de SMS** (CcmExec).
- Si cambia la configuración del servidor, reinicie el servicio **SMS Executive**.

La configuración del Registro varía dependiendo del componente:

- [Cliente y punto de administración](#bkmk_reg-client)
- [Servidor de sitio](#bkmk_reg-site)
- [Rol de sistema de sitio](#bkmk_reg-role)
- [Consola de Configuration Manager](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a> Opciones de registro de cliente y punto de administración

Para configurar opciones de registro para todos los componentes de un sistema de sitio de cliente o punto de administración, configure estos valores **REG_DWORD** en la siguiente clave del Registro de Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Nombre  |Valores  |Descripción  |
|---------|---------|---------|
|LogLevel|`0`: Detallado<br>`1`: Predeterminado<br>`2`: Advertencias y errores<br>`3`: Solo errores|El nivel de detalle que se va a escribir en los archivos de registro.|
|LogMaxHistory|Cualquier entero mayor o igual que cero, por ejemplo:<br>`0`: No hay historial<br>`1`: Predeterminado|Cuando un archivo de registro alcanza el tamaño máximo, el cliente le cambia el nombre como si fuera una copia de seguridad y crea un archivo de registro. Especifique cuántas versiones anteriores desea conservar.|
|LogMaxSize|Cualquier entero mayor o igual que 10 000, por ejemplo:<br>250 000|El tamaño máximo del archivo de registro en bytes. Cuando un registro crece hasta el tamaño especificado, el cliente le cambia el nombre como si fuera un archivo de historial y crea un archivo. El valor predeterminado es 250 000 bytes.|

> [!Note]  
> No cambie otros valores que puedan existir en esta clave del Registro.

Para la depuración avanzada, también puede agregar este valor **REG_SZ** en la siguiente clave del Registro de Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Nombre  |Valores  |Descripción  |
|---------|---------|---------|
|Habilitado | `True`: habilita los registros de depuración<br>`False`: deshabilita los registros de depuración |Habilita el registro de depuración para solucionar los problemas.|

Esta configuración hace que el cliente registre información de bajo nivel para la solución de problemas. Evite usar esta configuración en los sitios de producción. Puede producirse un registro excesivo, lo que podría hacer que resultase difícil encontrar información relevante en los archivos de registro. Asegúrese de desactivar esta configuración después de resolver el problema.

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a> Opciones de registro del servidor de sitio

Puede definir la configuración globalmente o para un componente específico del servidor de sitio de Configuration Manager.

Configure estos valores en la siguiente clave del Registro de Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Nombre  |Valores  |Tipo  |Descripción
|---------|---------|---------|---------|
|SqlEnabled| `1`: habilita el seguimiento de SQL<br> `0`: deshabilita el seguimiento de SQL |REG_DWORD|Agregue el registro de seguimiento de SQL a todos los registros de servidor de sitio.|
|ArchiveEnabled| `1`: habilita archivos de registro<br> `0`: deshabilita archivos de registro | REG_DWORD |Archive registros de servidor de sitio en una ubicación independiente para la conservación histórica.|
|ArchivePath| Una ruta de acceso de carpeta válida, por ejemplo `C:\Logs\Archive` | REG_SZ |La ruta de acceso para archivar registros de servidor de sitio.|

Habilite solo el seguimiento de SQL para solucionar los problemas. Evite usarlo en los sitios de producción. Puede producirse un registro excesivo, lo que podría hacer que resultase difícil encontrar información relevante en los archivos de registro. Asegúrese de desactivar esta configuración después de resolver el problema.

> [!Note]  
> No cambie otros valores que puedan existir en esta clave del Registro.

Para configurar opciones de registro para un componente de servidor específico, configure estos valores **REG_DWORD** en la siguiente clave del Registro de Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Nombre  |Valores  |Descripción  |
|---------|---------|---------|
|LoggingLevel|`0`: Detallado<br>`1`: Predeterminado<br>`2`: Advertencias y errores<br>`3`: Solo errores|El nivel de detalle que se va a escribir en los archivos de registro.|
|LogMaxHistory|Cualquier entero mayor o igual que cero, por ejemplo:<br>`0`: No hay historial<br>`1`: Predeterminado|Cuando un archivo de registro alcanza el tamaño máximo, el servidor le cambia el nombre como si fuera una copia de seguridad y crea un archivo de registro. Especifique cuántas versiones anteriores desea conservar.|
|MaxFileSize|Cualquier entero mayor o igual que 10 000, por ejemplo:<br>250 000|El tamaño máximo del archivo de registro en bytes. Cuando un registro crece hasta el tamaño especificado, el cliente le cambia el nombre como si fuera un archivo de historial y crea un archivo. El valor predeterminado es 250 000 bytes.|
|DebugLogging| `1`: habilita los registros de depuración<br>`0`: deshabilita los registros de depuración |Habilita el registro de depuración para solucionar los problemas.|

La opción DebugLogging hace que el servidor registre información de bajo nivel para la solución de problemas. Evite usar esta configuración en los sitios de producción. Puede producirse un registro excesivo, lo que podría hacer que resultase difícil encontrar información relevante en los archivos de registro. Asegúrese de desactivar esta configuración después de resolver el problema.

> [!Note]  
> No cambie otros valores que puedan existir en esta clave del Registro.

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a> Opciones de registro de rol de sistema de sitio

Puede definir la configuración globalmente o para un componente específico de un servidor de sitio que hospede un rol del servidor de Configuration Manager.

Para configurar opciones de registro para un componente de servidor específico, configure estos valores **REG_DWORD** en la siguiente clave del Registro de Windows:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

Por ejemplo, para el rol de punto de distribución:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Nombre  |Valores  |Descripción  |
|---------|---------|---------|
|LogLevel|`0`: Detallado<br>`1`: Predeterminado<br>`2`: Advertencias y errores<br>`3`: Solo errores|El nivel de detalle que se va a escribir en los archivos de registro.|
|LogMaxHistory|Cualquier entero mayor o igual que cero, por ejemplo:<br>`0`: No hay historial<br>`1`: Predeterminado|Cuando un archivo de registro alcanza el tamaño máximo, el servidor le cambia el nombre como si fuera una copia de seguridad y crea un archivo de registro. Especifique cuántas versiones anteriores desea conservar.|
|LogMaxSize|Cualquier entero mayor o igual que 10 000, por ejemplo:<br>250 000|El tamaño máximo del archivo de registro en bytes. Cuando un registro crece hasta el tamaño especificado, el servidor le cambia el nombre como si fuera un archivo de historial y crea un archivo. El valor predeterminado es 250 000 bytes.|

> [!Note]  
> No cambie otros valores que puedan existir en esta clave del Registro.

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a> Opciones de registro de consolas de Configuration Manager

Para cambiar el nivel detallado del AdminUI.log para la consola de Configuration Manager, use el siguiente procedimiento:

1. Abra el archivo de configuración de la consola, **Microsoft.ConfigurationManagement.exe.config**, en un editor XML como el Bloc de notas. El archivo de configuración predeterminado está en la siguiente ubicación: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

    > [!IMPORTANT]
    > A partir de la versión 1910, esta ruta de acceso cambió para usar la carpeta `Microsoft Endpoint Manager`. Asegúrese de que no usa una versión anterior del archivo que pudiera existir en otra carpeta.

1. En el elemento **system.diagnostics** > **orígenes** > **origen**, cambie el atributo **switchValue** de `Error` a `Verbose`. Por ejemplo:

    Original: `<source name="SmsAdminUISnapIn" switchValue="Error">` Nuevo: `<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Guarde el archivo y reinicie la consola.

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a> Configuración de opciones de registro en la consola de Configuration Manager

<!-- 4433455 -->

A partir de la versión 1910, el registro detallado de un cliente o de una colección se puede habilitar o deshabilitar desde la consola:

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y cumplimiento**, seleccione el nodo **Dispositivos** y elija un dispositivo de destino.

1. En la cinta, en el grupo **Dispositivos** de la pestaña **Inicio**, seleccione **Diagnóstico de cliente**. Elija una de las acciones disponibles.

Para más información, vea [Diagnósticos del cliente](../../clients/manage/client-notification.md#client-diagnostics).

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a> Búsqueda de archivos de registro

Configuration Manager y los componentes dependientes almacenan los archivos de registro en diversas ubicaciones. Estas ubicaciones dependen del proceso que crea el archivo de registro y la configuración del entorno.

Las siguientes ubicaciones son los valores predeterminados. Si ha personalizado los directorios de instalación en el entorno, las rutas de acceso reales pueden variar.

- Cliente: `C:\Windows\CCM\logs`
- Servidor: `C:\Program Files\Microsoft Configuration Manager\Logs`
- Punto de administración: `C:\SMS_CCM\Logs`
- Consola de Configuration Manager: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog`
- IIS: `C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>Ubicaciones de registro de secuencia de tareas

La ubicación del archivo de registro de secuencia de tareas **smsts.log** varía en función de la fase de la secuencia de tareas:

- En Windows PE antes del paso [Formatear y crear particiones en el disco](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk): `X:\Windows\temp\smstslog\smsts.log` (X es la unidad RAM de Windows PE)
- En Windows PE después del paso **Formatear y crear particiones en el disco**: `X:\smstslog\smsts.log`, se copia a continuación en `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` cuando la unidad está lista
- En el nuevo SO Windows antes de la instalación del cliente: `C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- En Windows después de la instalación del cliente: `C:\Windows\CCM\Logs\smstslog\smsts.log`
- En Windows después de completarse la secuencia de tareas: `C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> La variable de secuencia de tareas de solo lectura [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) siempre contiene la ruta de acceso del archivo de registro actual.


## <a name="see-also"></a>Vea también

- [Referencia del archivo de registro](log-files.md)

- [Centro de soporte técnico OneTrace](../../support/support-center-onetrace.md)

- [Visor de archivos de registro del Centro de soporte técnico](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
