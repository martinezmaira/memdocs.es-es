---
title: Uso de scripts de shell en dispositivos macOS en Microsoft Intune | Microsoft Docs
description: Cree, asigne, supervise y solucione problemas de scripts de shell para dispositivos macOS en Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36b85fa6713af5679e59382efaeb354bb4949705
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990587"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune"></a>Uso de scripts de shell en dispositivos macOS en Intune

Use scripts de shell para ampliar las funciones de administración de dispositivos en Intune más allá de lo que admite el sistema operativo macOS. 

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que se cumplen los siguientes requisitos previos al crear scripts de shell y asignarlos a dispositivos macOS. 
 - Los dispositivos ejecutan macOS 10.12 o una versión posterior.
 - Los dispositivos están administrados por Intune. 
 - Los scripts de shell comienzan por `#!` y deben estar en una ubicación válida, como `#!/bin/sh` o `#!/usr/bin/env zsh`.
 - Los intérpretes de línea de comandos para los shell correspondientes están instalados.

## <a name="important-considerations-before-using-shell-scripts"></a>Consideraciones importantes antes de usar scripts de shell
 - Los scripts de shell requieren que el agente de administración de Microsoft Intune se haya instalado correctamente en el dispositivo macOS. Para obtener más información, vea [Agente de administración de Microsoft Intune para macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
 - Los scripts de shell se ejecutan en paralelo en dispositivos como procesos independientes.
 - Los scripts de shell que se ejecuten como usuario que inició sesión se ejecutarán para todas las cuentas del usuario que inició sesión en el dispositivo en el momento de la ejecución.
 - Es preciso que un usuario final inicie sesión en el dispositivo para ejecutar scripts que se ejecutan como usuario que inició sesión.
 - Se precisan privilegios de usuario raíz si el script requiere la realización de cambios que una cuenta de usuario estándar no puede hacer.
 - Los scripts de shell intentarán ejecutarse con mayor frecuencia que la frecuencia de script elegida para ciertas condiciones, por ejemplo, si el disco está lleno, si se manipula la ubicación de almacenamiento, si se elimina la memoria caché local o si se reinicia el dispositivo Mac.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Creación y asignación de una directiva de script de shell
1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **macOS** > **Scripts** > **Agregar**.
3. En **Datos básicos**, escriba las propiedades siguientes y seleccione **Siguiente**:
   - **Nombre**: Escriba un nombre para el script de shell.
   - **Descripción**: Escriba una descripción para el script de shell. Esta configuración es opcional pero recomendada.
4. En **Configuración de script**, escriba las propiedades siguientes y seleccione **Siguiente**:
   - **Cargue el script**: Vaya al script de shell. El script debe tener un tamaño inferior a 200 KB.
   - **Ejecute el script como usuario que inició sesión**: Seleccione **Sí** para ejecutar el script con las credenciales del usuario en el dispositivo. Elija **No** (valor predeterminado) para ejecutar el script como usuario raíz. 
   - **Ocultar las notificaciones de scripts en los dispositivos**: De forma predeterminada, se muestran las notificaciones de script para cada script que se ejecuta. Los usuarios finales ven la notificación de *se está configurando el equipo* desde Intune en dispositivos macOS.
   - **Frecuencia del script:** seleccione la frecuencia con la que se va a ejecutar el script. Elija **No configurado** (valor predeterminado) para ejecutar un script una sola vez.
   - **Número máximo de reintentos en caso de error del script:** seleccione el número de veces que se debe ejecutar el script si devuelve un código de salida distinto de cero (cero significa que es correcto). Elija **No configurado** (valor predeterminado) para no volver a intentarlo cuando se produce un error en un script.
5. En **Etiquetas de ámbito**, agregue etiquetas de ámbito opcionalmente al script y seleccione **Siguiente**. Puede usar las etiquetas de ámbito para determinar quién puede ver scripts en Intune. Para obtener más información sobre las etiquetas de ámbito, consulte [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Uso del control de acceso basado en roles y de las etiquetas de ámbito para la TI distribuida).
6. Seleccione **Asignaciones** > **Seleccionar grupos para incluir**. Se muestra una lista existente de grupos de Azure AD. Seleccione uno o más grupos de usuarios o dispositivos que vayan a recibir el script. Elija **Seleccionar**. Los grupos que ha elegido se muestran en la lista y recibirán la directiva de script.
   > [!NOTE]
   > - Los scripts de shell asignados a grupos de usuarios se aplican a cualquier usuario que inicie sesión en el dispositivo Mac.  
   > - Al actualizar las asignaciones de scripts de shell también se actualizan las asignaciones de [Agente MDM de Microsoft Intune para macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).

7. En **Revisar y agregar**, se muestra un resumen de la configuración. Seleccione **Agregar** para guardar el script. Al seleccionar **Agregar**, la directiva de script se implementa en los grupos elegidos.

El script que ha creado aparece ahora en la lista de aplicaciones. 

## <a name="monitor-a-shell-script-policy"></a>Supervisión de una directiva de script de shell
Puede supervisar el estado de ejecución de todos los scripts asignados a usuarios y dispositivos eligiendo uno de los siguientes informes:
- **Scripts** > **seleccione el script que quiere supervisar** > **Estado del dispositivo**
- **Scripts** > **seleccione el script que quiere supervisar** > **Estado del usuario**

>[!IMPORTANT]
> Con independencia de la **frecuencia de script** seleccionada, el estado de ejecución del script solo se muestra la primera vez que se ejecuta un script. El estado de ejecución del script no se actualiza en las ejecuciones posteriores. Sin embargo, los scripts actualizados se tratan como nuevos scripts y notificarán de nuevo el estado de ejecución.

Una vez que se ejecuta un script, devuelve uno de los siguientes estados:
- Un estado de ejecución del script de **Con errores** indica que el script devolvió un código de salida distinto de cero o el script tiene un formato incorrecto. 
- Un estado de ejecución del script de **Correcto** indica que el script devolvió cero como código de salida. 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>Solución de problemas de directivas de script del shell en macOS mediante la recopilación de registros

Puede recopilar registros de dispositivos para ayudar a solucionar problemas con los scripts en dispositivos macOS. 

### <a name="requirements-for-log-collection"></a>Requisitos para la recopilación de registros
Los siguientes elementos son necesarios para recopilar registros en un dispositivo macOS:
- Debe especificar la ruta absoluta del archivo de registro.
- Las rutas de acceso de los archivos deben estar separadas mediante un punto y coma (;).
- Se puede cargar una recopilación de registros con un máximo de 25 archivos o 60 MB de tamaño comprimido, lo que ocurra primero.
- Los tipos de archivo que se permiten para la recopilación de registros incluyen las siguientes extensiones: *.log, .zip, .gz, .tar, .txt, .xml, .crash, .rtf*.

#### <a name="collect-device-logs"></a>Recopilación de registros de dispositivos
1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. En el informe **Estado del dispositivo** o **Estado de usuario**, seleccione un dispositivo.
3. Seleccione **Recopilar registros**, proporcione las rutas de acceso a las carpetas de archivos de registro separadas solo por un punto y coma (;), sin espacios o nuevas líneas entre ellas.<br>Por ejemplo, varias rutas de acceso se escribían como `/Path/to/logfile1.zip;/Path/to/logfile2.log`. 

   >[!IMPORTANT]
   > Si se escriben varias rutas de archivos de registro separadas mediante comas, puntos, nuevas líneas o comillas (con o sin espacios entre ellas), se producirá un error en la recopilación de registros. Tampoco se permite el uso de espacios como delimitadores entre las rutas de acceso.

4. Seleccione **Aceptar**. Los registros se recopilarán la próxima vez que el agente de administración de Intune en el dispositivo se sincronice con Intune. Esta sincronización suele producirse cada ocho horas.

   >[!NOTE]
   > 
   > - Los registros recopilados se cifran en el dispositivo, se transmiten y se almacenan en Microsoft Azure Storage durante 30 días. Los registros almacenados se descifran a petición y se descargan mediante el centro de administración de Microsoft Endpoint Manager.
   > - Además de los registros especificados por el administrador, los registros del agente de administración de Intune también se recopilan a partir de estas carpetas: `/Library/Logs/Microsoft/Intune` y `~/Library/Logs/Microsoft/Intune`. Los nombres de archivo de los registros del agente son `IntuneMDMDaemon date--time.log` y `IntuneMDMAgent date--time.log`. 
   > - Si falta algún archivo especificado por el administrador o algún archivo tiene una extensión incorrecta, encontrará los nombres de esos archivos enumerados en `LogCollectionInfo.txt`.     

### <a name="log-collection-errors"></a>Errores de recopilación de registros
Es posible que la recopilación de registros no se realice correctamente debido a alguna de las razones que se indican en la siguiente tabla. Para resolver estos errores, siga los pasos para la corrección.

| Código de error (hexadecimal) | Código de error (decimal) | Mensaje de error | Pasos para la corrección |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | El tamaño del archivo de registro no puede superar los 60 MB. | Asegúrese de que los registros comprimidos tengan un tamaño inferior a 60 MB. |
| 0X87D300D1 | 2016214831 | La ruta del archivo de registro que se ha proporcionado debe existir. La carpeta de usuario del sistema está en una ubicación no válida para los archivos de registro. | Asegúrese de que la ruta de acceso del archivo proporcionada sea válida y accesible. |
| 0X87D300D2 | 2016214830 | Error al cargar los archivos de la recopilación de registros debido a la expiración de la dirección URL de carga. | Vuelva a intentar la acción **Recopilar registros**. |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Error al cargar los archivos de la recopilación de registros debido a un error de cifrado. Intente cargar los registros de nuevo. | Vuelva a intentar la acción **Recopilar registros**. |
| | 2016214828 | El número de archivos de registro ha superado el límite permitido de 25 archivos. | Solo se puede recopilar un máximo de 25 archivos de registro a la vez. |
| 0X87D300D6 | 2016214826 | Error al cargar los archivos de la recopilación de registros debido a un error de ZIP. Intente cargar los registros de nuevo. | Vuelva a intentar la acción **Recopilar registros**. |
| | 2016214740 | No se han podido cifrar los registros porque no se han encontrado registros comprimidos. | Vuelva a intentar la acción **Recopilar registros**. |
| | 2016214739 | Los registros se han recopilado, pero no se han podido almacenar. | Vuelva a intentar la acción **Recopilar registros**. |

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>¿Por qué los scripts de shell asignados no se ejecutan en el dispositivo?
Pueden existir varias razones:
* Es posible que haya que sincronizar el agente para recibir scripts nuevos o actualizados. Este proceso de sincronización se produce cada ocho horas y es diferente de la sincronización de MDM. Asegúrese de que el dispositivo esté activo y conectado a una red para una sincronización correcta del agente y espere a que el agente se sincronice. También puede solicitar al usuario final que abra el Portal de empresa en el dispositivo Mac, seleccione el dispositivo y haga clic en **Comprobar configuración**.
* Es posible que el agente no esté instalado. Compruebe que el agente esté instalado en `/Library/Intune/Microsoft Intune Agent.app` en el dispositivo macOS.
* Es posible que el agente no esté en un estado correcto. El agente intentará realizar la recuperación durante 24 horas, y se quitará y volverá a instalar si todavía hay scripts de shell asignados.

### <a name="how-frequently-is-script-run-status-reported"></a>¿Con qué frecuencia se notifica el estado de ejecución del script?
El estado de ejecución del script se envía a la consola de administración de Microsoft Endpoint Manager en cuanto se completa la ejecución del script. Si un script está programado para ejecutarse periódicamente conforme a una frecuencia establecida, solo notifica el estado la primera vez que se ejecuta.

### <a name="when-are-shell-scripts-run-again"></a>¿Cuándo se ejecutan de nuevo los scripts de shell?
Un script solo se ejecuta de nuevo si se configura el valor **Número máximo de reintentos en caso de error del script** y el script no se ejecuta. Si el **Número máximo de reintentos en caso de error del script** no se configura y un script no se ejecuta, no se volverá a ejecutar y el estado de ejecución se notificará como **con errores**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>¿Qué permisos de rol de Intune se requieren para los scripts de shell?
El rol asignado en Intune requiere permisos de **configuraciones de dispositivo** para eliminar, asignar, crear, actualizar o leer scripts de shell.

## <a name="microsoft-intune-management-agent-for-macos"></a>Agente de administración de Microsoft Intune para macOS
 ### <a name="why-is-the-agent-required"></a>¿Por qué es necesario el agente?
Es necesario instalar el agente de administración de Microsoft Intune en dispositivos macOS administrados para habilitar funciones avanzadas de administración de dispositivos que no son compatibles con el sistema operativo macOS nativo.
 
 ### <a name="how-is-the-agent-installed"></a>¿Cómo se instala el agente?
 El agente se instala de forma automática y silenciosa en dispositivos macOS administrados por Intune a los que asigna al menos un script de shell en el Centro de administración de Microsoft Endpoint Manager. El agente se instala en `/Library/Intune/Microsoft Intune Agent.app` cuando es aplicable y no aparece en **Finder** > **Aplicaciones** en dispositivos macOS. El agente aparece como `IntuneMdmAgent` en **Monitor de actividad** cuando se ejecuta en dispositivos macOS.

### <a name="what-does-the-agent-do"></a>¿Qué hace el agente?
 - El agente se autentica de forma silenciosa ante los servicios de Intune antes de la sincronización para recibir los scripts de shell asignados al dispositivo macOS.
 - El agente recibe los scripts de shell asignados y los ejecuta según la programación configurada, los intentos de reintento, la configuración de notificaciones y otras opciones establecidas por el administrador.
 - El agente normalmente comprueba cada ocho horas si hay scripts nuevos o actualizados en los servicios de Intune. Este proceso de sincronización es independiente de la sincronización de MDM. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>¿Cómo puedo iniciar manualmente una sincronización del agente desde un equipo Mac?
En un dispositivo Mac administrado con el agente instalado, abra el **Portal de empresa**, seleccione el dispositivo local y haga clic en **Comprobar configuración**. Esto inicia una sincronización de MDM, así como una del agente.

Como alternativa, abra **Terminal** y ejecute el comando `sudo killall IntuneMdmAgent` para finalizar el proceso `IntuneMdmAgent`. El proceso de `IntuneMdmAgent` se reiniciará inmediatamente, lo que iniciará una sincronización con Intune.

> [!NOTE]
> La acción **Sincronizar** en los dispositivos de la Consola de administración del Administrador de puntos de conexión de Microsoft inicia una sincronización de MDM y no fuerza una sincronización del agente.

 ### <a name="when-is-the-agent-removed"></a>¿Cuándo se quita el agente?
 Hay varias condiciones que pueden hacer que el agente se quite del dispositivo como, por ejemplo:
 - No hay scripts de shell asignados al dispositivo. 
 - Ya no se administra el dispositivo macOS.
 - El agente permanece en un estado irrecuperable durante más de 24 horas (tiempo de activación del dispositivo).

 ### <a name="why-are-scripts-running-even-though-the-mac-is-no-longer-managed"></a>¿Por qué se ejecutan los scripts aunque el dispositivo Mac ya no se administre?
 Cuando un dispositivo Mac con scripts asignados ya no se administra, el agente no se quita de inmediato. El agente detecta que el dispositivo Mac no se administra en la siguiente sincronización del agente (normalmente, se realiza una cada 8 horas) y cancela las ejecuciones de scripts programadas. Por lo tanto, se ejecutan todos los scripts almacenados en local programados para ejecutarse con más frecuencia que la siguiente sincronización programada del agente. Si el agente no se puede sincronizar, vuelve a intentarlo durante un máximo de 24 horas (tiempo de activación del dispositivo) y luego se quita automáticamente del dispositivo Mac.
 
 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>¿Cómo desactivar el envío de datos de uso a Microsoft para los scripts de shell?
 Para desactivar el envío de datos de uso a Microsoft desde el agente de administración de Intune, abra el Portal de empresa y seleccione **Menú** > **Preferencias** > *desactive "Permitir que Microsoft recopile datos de uso"* . Se desactivará el envío de datos de uso al agente de administración de Intune y al Portal de empresa.

## <a name="known-issues"></a>Problemas conocidos
- **No hay estado de ejecución de script:** En el improbable caso de que se reciba un script en el dispositivo y este se quede sin conexión antes de que se notifique el estado de ejecución, el dispositivo no notificará el estado de ejecución del script en la consola de administración.

## <a name="next-steps"></a>Pasos siguientes

- [Creación de una directiva de cumplimiento en Microsoft Intune](..\protect\create-compliance-policy.md)
