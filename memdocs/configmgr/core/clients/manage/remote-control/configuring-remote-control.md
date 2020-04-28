---
title: Configuración del control remoto
titleSuffix: Configuration Manager
description: Configure el control remoto en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78f74a9659a011defd50e6ab0e9e1cfe85eec16b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076737"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>Configuración del control remoto en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

 En este procedimiento se describe cómo definir la configuración predeterminada de cliente para el control remoto. Esta configuración se aplica a todos los equipos de la jerarquía. Si quiere que esta configuración solo se aplique a algunos equipos, asigne una configuración de cliente de dispositivo personalizada a una colección que contenga esos equipos. Para más información, vea [Cómo configurar el cliente](../../../../core/clients/deploy/configure-client-settings.md). 

Para usar Asistencia remota o Escritorio remoto, debe estar instalado y configurado en el equipo que ejecuta la consola de Configuration Manager. Para obtener más información sobre cómo instalar y configurar la Asistencia remota o el Escritorio remoto, consulte la documentación de Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para habilitar el control remoto y configurar el cliente  

1. En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

2. En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

3. En el cuadro de diálogo **Predeterminado**, elija **Herramientas remotas**.  

4. Defina la configuración de cliente del control remoto, la Asistencia remota y el Escritorio remoto. Para obtener una lista de la configuración de cliente de las herramientas remotas que puede configurar, vea [Herramientas remotas](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   Puede cambiar el nombre de la compañía que aparece en el cuadro de diálogo **Control remoto de ConfigMgr** mediante la configuración de un valor para **Nombre de organización mostrado en el Centro de software** en la configuración de cliente del **Agente de equipo** .  

   Los equipos cliente se configuran con estas opciones la próxima vez que descargan directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Cómo administrar clientes](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Habilitar traducción del teclado

De manera predeterminada, Configuration Manager transmite la posición de la tecla desde la ubicación del lector a la ubicación del colaborador. Esto puede ser problemático para las configuraciones de teclado que difieren entre lector y colaborador. Por ejemplo, un lector con un teclado inglés escribiría una "A", pero el teclado francés del colaborador proporcionaría una "Q". Ahora tiene la opción de configurar el control remoto para que sea el propio carácter el que se transmita desde el teclado del lector al del colaborador y para que sea lo que el lector intenta escribir lo que llegue al colaborador.

Para activar la traducción de teclado, en **Control remoto de Configuration Manager**, elija **Acción** y, luego, **Habilitar traducción del teclado** para transmitir la posición de las teclas.

> [!NOTE]
>
> Las teclas especiales, como ~!#@$%, no se traducirán correctamente.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Métodos abreviados de teclado del visor de control remoto

|Método abreviado de teclado|Descripción|  
|-----------------------|-----------------|  
|Alt+Re Pág|Cambia entre programas de izquierda a derecha.|  
|Alt+Av Pág|Cambia entre programas de derecha a izquierda.|  
|Alt+Insertar|Recorre en iteración los programas en ejecución en el orden en que se abrieron.|  
|Alt+Inicio|Muestra el menú **Inicio** .|  
|Ctrl+Alt+Fin|Muestra el cuadro de diálogo de seguridad de Windows (Ctrl+Alt+Supr).|  
|Alt+Supr|Muestra el menú de Windows.|  
|Ctrl+Alt+Signo menos (en el teclado numérico)|Copia la ventana activa del equipo local en el Portapapeles del equipo remoto.|  
|Ctrl+Alt+Signo más (en el teclado numérico)|Copia el área completa de la ventana del equipo local en el Portapapeles del equipo remoto.|  
