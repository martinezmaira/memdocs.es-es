---
title: Support Center
titleSuffix: Configuration Manager
description: Solucione problemas de clientes de Configuration Manager con el Centro de soporte técnico.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 788c48599ac8a94b8690f3a88f9761b9ae8ac742
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699439"
---
# <a name="support-center-for-configuration-manager"></a>Centro de soporte técnico de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--1357489-->
A partir de la versión 1810, use el Centro de soporte técnico para solucionar los problemas de los clientes, visualizar los registros en tiempo real o capturar el estado de un equipo cliente de Configuration Manager para su posterior análisis. Support Center es una única herramienta para consolidar muchas herramientas de solución de problemas del administrador.


## <a name="about"></a>Acerca de

El Centro de soporte técnico aspira a disminuir los retos y la frustración a la hora de solucionar problemas en equipos cliente de Configuration Manager. Anteriormente, cuando se trabajaba con el equipo de soporte técnico para resolver un problema con clientes de Configuration Manager, había que recopilar los archivos de registro y otra información manualmente a fin de ayudar a solucionar el problema. Era muy fácil olvidar un archivo de registro fundamental accidentalmente, lo que suponía más dolores de cabeza tanto para el usuario como para el personal de soporte técnico con el que se trabajaba.

Use el Centro de soporte técnico para optimizar la experiencia de soporte. Le permite:

- Crear un paquete de solución de problemas (archivo .zip) que contiene los archivos de registro del cliente de Configuration Manager. Así solo hay que enviar un archivo al personal de soporte técnico.  

- Ver archivos de registro, certificados, configuraciones del Registro, volcados de depuración y directivas del cliente de Configuration Manager.  

- Diagnosticar en tiempo real el inventario (reemplaza a ContentSpy), la directiva (reemplaza a PolicySpy) y la caché del cliente.  

### <a name="support-center-viewer"></a>Visor del Centro de soporte técnico

El Centro de soporte técnico incluye la herramienta Visor del Centro de soporte técnico, que admite el uso personal para abrir el paquete de archivos creado con el Centro de soporte técnico. El recopilador de datos del Centro de soporte técnico recopila y empaqueta los registros de diagnóstico de un cliente local o remoto de Configuration Manager. Para ver paquetes del recopilador de datos, use la aplicación Visor.

### <a name="support-center-log-file-viewer"></a>Visor de archivos de registro del Centro de soporte técnico

El Centro de soporte técnico incluye un moderno visor de registros. Esta herramienta reemplaza a CMTrace y proporciona una interfaz personalizable que admite pestañas y ventanas acoplables. Tiene una capa de presentación rápida y puede cargar archivos de registro de gran tamaño en segundos.

### <a name="support-center-onetrace-preview"></a>Centro de soporte técnico OneTrace (versión preliminar)

<!--3555962-->
A partir de la versión 1906, **OneTrace** es un nuevo visor de registros del Centro de soporte técnico. Funciona de manera similar a CMTrace, pero con mejoras. Para obtener más información, consulte [Centro de soporte técnico OneTrace](support-center-onetrace.md).

### <a name="powershell-cmdlets"></a>Cmdlets de PowerShell

El centro de soporte técnico también incluye [cmdlets de PowerShell](/powershell/sccm/overview?view=sccm-ps). Use estos cmdlets para crear una conexión remota a otro cliente de Configuration Manager, para configurar las opciones de recopilación de datos y para iniciar la recopilación de datos.


## <a name="prerequisites"></a>Requisitos previos

Instale los componentes siguientes en el servidor o en el equipo cliente en el que instale el Centro de soporte técnico:

- Una versión del sistema operativo compatible con Configuration Manager. Para obtener más información, vea [Sistemas operativos compatibles con clientes y dispositivos](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md). El Centro de soporte técnico no es compatible con los dispositivos móviles.  

- Se requiere .NET Framework 4.5.2 en el equipo en el que se ejecutan el Centro de soporte técnico y sus componentes.  


## <a name="install"></a>Instalar

Busque el instalador del Centro de soporte técnico en la siguiente ruta de acceso del servidor de sitio: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Una vez instalado, busque los siguientes elementos en el menú Iniciar del grupo **Microsoft System Center**:  

- Support Center (ConfigMgrSupportCenter.exe)  
- Support Center Log File Viewer (CMLogViewer.exe)  
- Support Center Viewer (ConfigMgrSupportCenterViewer.exe)  


## <a name="known-issues"></a>Problemas conocidos

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>No se puede instalar la versión más reciente si ya está instalada una versión anterior

<!--SCCMDocs-pr issue #3090-->
*Se aplica a las versiones 1810 y 1902*

Si ya tiene una versión anterior del Centro de soporte técnico instalada, se produce un error en el programa de instalación. Este problema se debe al control de versiones de los archivos en relación con la versión original y la versión más reciente. Para solucionar este problema, desinstale primero la versión anterior del centro de soporte técnico. Luego, instale la versión más reciente.

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Las conexiones remotas deben incluir el nombre del equipo o el dominio como parte del nombre de usuario.

Si se conecta a un cliente remoto desde el Centro de soporte técnico, cuando establezca la conexión debe proporcionar el nombre del equipo o el nombre de dominio de la cuenta de usuario. Si usa un nombre abreviado de equipo o de dominio (como `.\administrator`), la conexión se realiza correctamente, pero el Centro de soporte técnico no recopila datos del cliente.

Para evitar este problema, use los siguientes formatos de nombre de usuario para conectarse a un cliente remoto:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Puede ser necesario quitar conexiones de Bloque de mensajes del servidor incluidas en script a clientes remotos

Al conectarse a clientes remotos mediante el cmdlet de PowerShell [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542), el Centro de soporte técnico crea una conexión de Bloque de mensajes del servidor (SMB) a cada cliente remoto. Conserva esas conexiones después de completar la recopilación de datos. Para evitar superar el número máximo de conexiones remotas de Windows, use el comando `net use` para ver el conjunto activo de conexiones remotas. Luego deshabilite las conexiones innecesarias mediante el comando siguiente: `net use <connection_name> /d`
donde `<connection_name>` es el nombre de la conexión remota.

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>La solicitud del ciclo de evaluación de implementación de aplicación no se envía correctamente a máquinas remotas

<!--2849356-->
*Se aplica a la versión 1810*

En el Centro de soporte técnico, si selecciona **Application deployment evaluation** (Evaluación de implementación de aplicaciones) en la acción **Invoke trigger** (Invocar desencadenador) de la pestaña **Contenido**, esta acción inicia una tarea que evalúa las aplicaciones implementadas. Si está conectado a un cliente local, se evalúan tanto las implementaciones de aplicaciones de máquina como de usuario. Sin embargo, si está conectado a un cliente remoto, solo se evalúan las implementaciones de aplicaciones de máquina.


## <a name="next-steps"></a>Pasos siguientes

[Inicio rápido del Centro de soporte técnico](support-center-quickstart.md)