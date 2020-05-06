---
title: Technical Preview 1707
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1707.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ddae3e4c4cf31cb05376bfa437d722f16652fad
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705143"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Funciones de Technical Preview 1707 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en Technical Preview 1707 de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, revise [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales del uso de este tipo de versiones y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Problemas conocidos de esta Technical Preview:**
- **Error al actualizar a la versión preliminar 1707 cuando hay un servidor de sitio en modo pasivo**. Si ejecuta la versión preliminar 1706 y tiene un [servidor de sitio principal en modo pasivo](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), debe desinstalar el servidor de sitio en modo pasivo para poder actualizar correctamente el sitio en versión preliminar a la versión 1707. Puede volver a instalar el servidor de sitio en modo pasivo después de que el sitio ejecuta la versión 1707.

  Para desinstalar el servidor de sitio en modo pasivo:
  1. En la consola vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles del sistema de sitios** y seleccione el servidor de sitio en modo pasivo.
  2. En el panel **Roles del sistema de sitio**, haga clic con el botón derecho en el rol **Servidor de sitio** y después elija **Quitar rol**.
  3. Haga clic con el botón derecho en el servidor de sitio en modo pasivo y después elija **Eliminar**.
  4. Después de que el servidor de sitio se desinstala, en el servidor de sitio principal activo, reinicie el servicio **CONFIGURATION_MANAGER_UPDATE**.



**Estas son las nuevas características que puede probar con esta versión.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Compatibilidad con la caché del mismo nivel de cliente para archivos de instalación rápida en Windows 10 y Office 365
<!-- 1352486 -->
A partir de esta versión, la caché del mismo nivel de cliente admite la distribución de archivos de instalación rápida de contenido para Windows 10, así como de archivos de actualización para Office 365. No se requiere ninguna configuración adicional.

## <a name="surface-device-dashboard"></a>Panel de Surface Device
<!--1355788-->
El panel de Surface Device proporciona información acerca de los dispositivos Surface de su entorno. En la consola, vaya a **Supervisión** > **Dispositivos Surface**. Puede ver la siguiente información:
- El porcentaje de dispositivos Surface
- El porcentaje de modelos Surface
- Las cinco primeras versiones de sistema operativo

Haga clic en una sección del gráfico **Modelos Surface** para obtener una lista completa de los dispositivos.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configuración e implementación de directivas de Protección de aplicaciones de Windows Defender
<!-- 1351960 -->

[Protección de aplicaciones de Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) es una nueva característica de Windows que ayuda a proteger a los usuarios al abrir los sitios web que no sean de confianza en un contenedor aislado seguro al que no puedan tener acceso otras partes del sistema operativo. En esta versión preliminar técnica, ya se admite la configuración de esta característica mediante las opciones de conformidad de Configuration Manager que establezca para, posteriormente, implementarla en una recopilación. Esta característica se publicará en la versión preliminar para la versión de 64 bits de Windows 10 Fall Creators Update (nombre de código: RS3). Para probar esta característica ahora debe estar utilizando una versión preliminar de esta actualización.

### <a name="before-you-start"></a>Antes de empezar

Para crear e implementar directivas de Protección de aplicaciones de Windows Defender, los dispositivos de Windows 10 en los que implementa la directiva deben configurarse con una directiva de aislamiento de red. Consulte [esta entrada de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97) para obtener más información. Esta funcionalidad solo es aplicable a compilaciones de Windows 10 Insider actuales. Para probarla, los clientes deben ejecutar una compilación reciente de Windows 10 Insider.

### <a name="try-it-out"></a>Haga la prueba

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Para crear una directiva y examinar la configuración disponible:

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad**, elija **Introducción** > **Endpoint Protection** > **Protección de aplicaciones de Windows Defender**.
3. En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear directiva de Protección de aplicaciones de Windows Defender**.
4. Con la entrada de blog como referencia, puede examinar y configurar las opciones disponibles para probar la característica.
5. En esta versión, hemos agregado la nueva página **Definición de red** al asistente. Aquí debe especificar la identidad corporativa y definir los límites de la red corporativa.<br>Los equipos con Windows 10 solo almacenan una lista de aislamiento de red en el cliente. En esta versión, puede crear dos tipos diferentes de listas de aislamiento de red (una de Windows Information Protection y otra de Windows Defender Application Guard) e implementarlas en el cliente. Si implementa ambas directivas, deben coincidir con estas listas de aislamiento de red. Si implementa listas que no coincidan con el mismo cliente, se producirá un error en la implementación.
Puede encontrar más información sobre cómo especificar definiciones de red en la [documentación de Windows Information Protection](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Cuando haya terminado, complete el asistente e implemente la directiva en uno o varios dispositivos de Windows 10.

### <a name="further-reading"></a>Lectura adicional
Para obtener más información acerca de Protección de aplicaciones de Windows Defender, consulte [esta entrada de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Además, para obtener más información sobre el modo independiente de Protección de aplicaciones de Windows Defender, consulte [esta entrada de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Agregar parámetros al implementar scripts de PowerShell desde Configuration Manager

<!-- 1236459 --->

En la última versión preliminar técnica, se ha introducido una nueva funcionalidad que permite [crear y ejecutar scripts de PowerShell desde la consola de Configuration Manager](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
En esta versión preliminar técnica, hemos ampliado esta capacidad. Ahora, Configuration Manager lee el script de PowerShell y muestra los parámetros en el Asistente para crear scripts. Puede proporcionar un valor para el parámetro en el asistente que se usará cuando se ejecute el script. Como alternativa, puede dejar este parámetro en blanco. Si lo hace, deberá proporcionar un valor para el parámetro al ejecutar el script.
En esta versión preliminar técnica, debe proporcionar todos los parámetros que un script necesita. En una versión futura, se prevé que la definición de los parámetros de script sea opcional.

### <a name="try-it-out"></a>Haga la prueba

1. Siga las instrucciones de [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. En la nueva página **Parámetros de script** del **Asistente para crear scripts**, elija un parámetro y, después, haga clic en **Editar**.
3. Proporcione un valor para el parámetro seleccionado y haga clic en **Aceptar**.
4. Complete el asistente.

Cuando se ejecute la secuencia de comandos, usará los valores de parámetro que haya configurado.
