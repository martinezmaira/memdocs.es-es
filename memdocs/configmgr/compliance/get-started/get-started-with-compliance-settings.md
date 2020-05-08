---
title: Introducción a la configuración de cumplimiento
titleSuffix: Configuration Manager
description: Obtenga información sobre los conceptos básicos y cómo funciona la configuración de cumplimiento.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9143c224082f00b882d3cb557b47b737012393fa
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906340"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>Introducción a la configuración de cumplimiento en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de crear la configuración de cumplimiento de Configuration Manager, obtenga información sobre los conceptos básicos y cómo funcionan.  



## <a name="how-compliance-settings-work"></a>Funcionamiento de la configuración de cumplimiento  
La configuración de cumplimiento permite administrar la configuración y el cumplimiento de los clientes de la organización.  

Los elementos de configuración se clasifican en dos categorías principales:  

- **Configuración para dispositivos administrados con el cliente de Configuration Manager**: suelen ser dispositivos en los que ha instalado software de cliente de Configuration Manager para permitirle administrar el dispositivo.  

- **Configuración para dispositivos administrados sin el cliente de Configuration Manager**: suelen ser dispositivos administrados con Microsoft Intune o con la administración de dispositivo local de Configuration Manager.  



## <a name="what-devices-are-supported"></a>¿Qué dispositivos son compatibles?  

| Tipo de dispositivo | Más información |  
|------------|----------------------|  
| Equipos con Windows (con el cliente de Configuration Manager) | Cree elementos de configuración personalizados para evaluar elementos como las claves del Registro, los archivos y los atributos de Active Directory.<br /><br /> Si se usa el tipo de elemento de configuración de Windows 10, seleccione las opciones en una lista predefinida. |  
| PC Windows (inscritos con MDM local) | Seleccione la configuración de una lista predefinida. |  
| Dispositivos Windows Phone (inscritos con MDM local) | Seleccione la configuración de una lista predefinida. |  
| Equipos Mac (con el cliente de Configuration Manager) | Cree elementos de configuración personalizados para evaluar objetos como las preferencias de macOS y los resultados devueltos por un script. |  



## <a name="what-is-a-configuration-item"></a>¿Qué es un elemento de configuración?  
Un elemento de configuración es un contenedor que almacena información específica. La información que se configure depende del tipo de elemento de configuración. Los elementos de configuración pueden incluir la información siguiente:

- **Información de método de detección** es solo para los elementos de configuración de Windows que contienen la configuración de la aplicación. Detecta si una aplicación está instalada. Esta detección usa el archivo de Windows Installer para la aplicación, o bien un script personalizado.  

- **Configuración** representa las condiciones de negocio o técnicas para evaluar el cumplimiento en los dispositivos cliente. Establezca una configuración nueva o vaya a una configuración existente en un equipo de referencia.  

- Las **reglas de cumplimiento** especifican las condiciones que definen el cumplimiento de una opción de elemento de configuración. Antes de que el cliente evalúe una configuración de cumplimiento, debe tener al menos una regla de cumplimiento. Algunas configuraciones corrigen valores no compatibles. Cree reglas o busque una configuración existente en cualquier elemento de configuración y seleccione las reglas que contenga.  

- Las **plataformas admitidas** son las plataformas de dispositivo definidas en las que el cliente evalúa el cumplimiento de los elementos de configuración. Si se implementa un elemento de configuración en un dispositivo que no está en la lista de plataformas admitidas, no evalúa el cumplimiento.  



## <a name="what-is-a-configuration-baseline"></a>¿Qué es una línea base de configuración?  
Defina una línea base de configuración en la que se incluyan los elementos de configuración que se van a evaluar. Incluya también la configuración y las reglas que describen el nivel de cumplimiento requerido. Importe estos datos de configuración desde los paquetes de configuración de Configuration Manager. Microsoft y otros proveedores definen estos paquetes de configuración. O bien, cree elementos de configuración y líneas base de configuración.  

Después de definir una línea base de configuración, impleméntela en las recopilaciones de dispositivos y usuarios. Después, el cliente evalúa la configuración de línea base de cumplimiento según una programación. Se puede implementar más de una línea base de configuración en los dispositivos. Este nivel de detalle proporciona mayor control del cumplimiento. 

Los dispositivos cliente evalúan su cumplimiento con cada línea base de configuración implementadas y notifican inmediatamente los resultados al sitio mediante mensajes de estado. Si un dispositivo está actualmente desconectado de la red, pero descargó la línea base de configuración, seguirá evaluando el cumplimiento de los elementos de configuración. Envía la información de cumplimiento cuando se vuelve a conectar.  

### <a name="monitoring-configuration-baselines"></a>Supervisión de líneas base de configuración
- Supervise los resultados de la evaluación de cumplimiento en la consola de Configuration Manager, en el área de trabajo **Supervisión**, en el nodo **Implementaciones**. Por ejemplo:
  - Causas comunes de no cumplimiento
  - Errores
  - El número de dispositivos y usuarios afectados
- Ejecute informes de configuración de cumplimiento con detalles adicionales. Por ejemplo:
  - Qué dispositivos son compatibles o no compatibles
  - Qué elemento de la línea base de configuración está causando que un equipo sea no compatible
- Vea los resultados de evaluación de cumplimiento de los equipos Windows en los que se ejecuta al cliente de Configuration Manager. Abra el panel de control de **Configuration Manager** y cambie a la pestaña **Configuraciones**.  



## <a name="user-data-and-profiles-configuration-items"></a>Elementos de configuración de perfiles y datos de usuario  
Los elementos de configuración de perfiles y datos de usuario incluyen opciones que controlan cómo los usuarios de equipos que ejecutan Windows 8 y versiones posteriores administran lo siguiente:  
- Redirección de carpetas
- Archivos sin conexión
- Perfiles móviles  

Implemente estos elementos de configuración en recopilaciones de usuarios. Supervise su cumplimiento desde el nodo **Supervisión** de la consola de Configuration Manager. A diferencia de otros elementos de configuración, no los agregue a las líneas base de configuración antes de implementarlos. Impleméntelos directamente haciendo clic en **Implementar** en la cinta.  

Para obtener más información, vea [Creación de elementos de configuración de perfiles y datos de usuario](../deploy-use/create-user-data-and-profiles-configuration-items.md).  



## <a name="remote-connection-profiles"></a>Perfiles de conexión remota  
Los perfiles de conexión remota proporcionan un conjunto de herramientas y recursos para ayudar a crear, implementar y supervisar la configuración de conexión remota. Mediante la implementación de estas opciones en los dispositivos, se minimiza el esfuerzo que necesitan los usuarios finales para conectar sus equipos a la red corporativa.  

Para más información, consulte [Perfiles de conexión remota en System Center Configuration Manager](../deploy-use/create-remote-connection-profiles.md).  



## <a name="windows-edition-upgrade"></a>Actualización de edición de Windows
La directiva de actualización de edición actualiza automáticamente a una versión más reciente los dispositivos que ejecutan determinadas versiones de Windows 10. Esta directiva proporciona una clave de producto nueva o un archivo de licencia que el dispositivo usa para la actualización.

Para obtener más información, vea [Actualizar dispositivos de Windows con la directiva de actualización de edición en System Center Configuration Manager](../deploy-use/upgrade-windows-version.md).



## <a name="microsoft-edge-browser-profiles"></a>Perfiles del explorador Microsoft Edge
<!-- 1357310 -->
A partir de la versión 1802, para los clientes que usan el explorador web [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) en los clientes de Windows 10, cree una directiva de configuración de cumplimiento para configurar varias opciones de Microsoft Edge. 

Para obtener más información, vea [Microsoft Edge browser profiles](../deploy-use/browser-profiles.md) (Perfiles del explorador Microsoft Edge).

