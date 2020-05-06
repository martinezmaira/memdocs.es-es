---
title: Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1710.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 503bb6d2293b4b5efb1d84980225a9d7052e1656
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705113"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Funciones de Technical Preview 1710 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1710 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, revise [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales del uso de este tipo de versiones y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conocidos de esta Technical Preview:**
- **Compatibilidad con Windows 10, versión 1709 (también conocida como Fall Creators Update)** .  A partir de esta versión de Windows, Windows Media incluye varias ediciones. Al configurar una secuencia de tareas para usar un paquete de actualizaciones del sistema operativo o una imagen del sistema operativo, no olvide seleccionar una [edición que se pueda usar con Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **La actualización a una nueva versión preliminar no se puede realizar cuando hay un servidor de sitio en modo pasivo**. Si ejecuta una versión preliminar que tiene un [servidor de sitio primario en modo pasivo](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), debe desinstalarlo para poder actualizar correctamente el sitio en versión preliminar a esta nueva versión preliminar. Puede volver a instalar el servidor de sitio en modo pasivo después de que el sitio finalice la actualización.

  Para desinstalar el servidor de sitio en modo pasivo:
  1. En la consola vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles del sistema de sitios** y seleccione el servidor de sitio en modo pasivo.
  2. En el panel **Roles del sistema de sitio**, haga clic con el botón derecho en el rol **Servidor de sitio** y después elija **Quitar rol**.
  3. Haga clic con el botón derecho en el servidor de sitio en modo pasivo y después elija **Eliminar**.
  4. Después de que el servidor de sitio se desinstala, en el servidor de sitio principal activo, reinicie el servicio **CONFIGURATION_MANAGER_UPDATE**.

**Estas son las nuevas características que puede probar con esta versión.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Mejoras en la implementación de scripts de PowerShell desde Configuration Manager
Con esta versión, los scripts de PowerShell que implemente ahora admiten el uso de las siguientes mejoras: 
- **Ámbitos de seguridad**.  Ahora, los scripts usan ámbitos de seguridad para controlar la creación y ejecución de scripts. Esto se realiza mediante la asignación de etiquetas que representan grupos de usuarios. Para más información, vea [Configuración de la administración basada en roles de Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Supervisión en tiempo real**. Al supervisar la ejecución de un script, ahora se realiza en tiempo real.
- **Validación de parámetros**. Cada parámetro de script tiene un cuadro de diálogo **Script Parameter Properties** (Propiedades de parámetros de script) con el objetivo de agregar validación para ese parámetro. Después de agregar la validación, debería obtener errores si va a especificar un valor para un parámetro que no cumple su validación.

La implementación de scripts de PowerShell se introdujo por primera vez en la versión preliminar técnica [Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console). En [Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) y, luego, en [Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) llegaron más mejoras.


### <a name="try-it-out"></a>Haga la prueba

Para probar el uso de la funcionalidad de ejecución de scripts, consulte [Creación y ejecución de scripts](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitación de los datos mejorados de Windows 10 al envío únicamente de datos pertinentes para el Estado de dispositivos de Windows Analytics
<!-- 1356148 -->

Con esta versión, ahora puede establecer el nivel de recopilación de datos de diagnóstico de Windows 10 en **Mejorado (limitado)** . Esta configuración le permite obtener información práctica sobre los dispositivos de su entorno sin que los dispositivos informen de todos los datos del nivel **Mejorado** con Windows 10, versión 1709 o una versión posterior.

El nivel Mejorado (limitado) incluye métricas del nivel Básico, así como un subconjunto de datos recopilados del nivel **Mejorado** que resulta pertinente para Windows Analytics.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>El Centro de software ya no distorsiona los iconos que tienen un tamaño superior a 250 x 250  
<!-- 1356194 -->

Con esta versión, el Centro de software ya no distorsiona los iconos con un tamaño superior a 250 x 250. Esos iconos aparecían antes borrosos. Ahora puede configurar un icono con una dimensión de píxel de hasta 512 x 512 sin que se muestre distorsionado.

### <a name="try-it-out"></a>Haga la prueba
Agregue un icono para su aplicación en el Centro de software. Para probarlo, consulte [Crear aplicaciones](../../apps/deploy-use/create-applications.md).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Comprobación del cumplimiento del Centro de software en dispositivos administrados conjuntamente
<!-- 1356374 -->
En esta versión, los usuarios pueden usar el Centro de software para comprobar el cumplimiento de sus dispositivos Windows 10 administrados conjuntamente, incluso cuando se administra el acceso condicional mediante Intune. Para más información, consulte [Administración conjunta para dispositivos de Windows 10](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Compatibilidad con la Protección contra vulnerabilidades de seguridad
Esta versión agrega compatibilidad con la Protección contra vulnerabilidades de seguridad de Windows Defender. Puede configurar e implementar directivas que administran los cuatro componentes de la Protección contra vulnerabilidades de seguridad. Estos componentes incluyen:
-   Reducción de la superficie expuesta a ataques
-   Acceso controlado a carpetas
-   Protección contra vulnerabilidades
-   Protección de redes

Los datos de cumplimiento de la implementación de la directiva de Protección contra vulnerabilidades de seguridad están disponibles en la consola de Configuration Manager.

Para más información sobre la Protección contra vulnerabilidades de seguridad y las reglas y los componentes específicos, consulte [Protección contra vulnerabilidades de seguridad de Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) en la biblioteca de documentación de Windows.

### <a name="prerequisites"></a>Requisitos previos
Los dispositivos administrados deben ejecutar Windows 10 1709 Fall Creators Update o una versión posterior y cumplir los siguientes requisitos, según las reglas y los componentes configurados:

|Componente Protección contra vulnerabilidades de seguridad |Requisitos previos adicionales|
|------------------------|------------------------|
| Reducción de la superficie expuesta a ataques  | Los dispositivos deben tener habilitada la [protección en tiempo real de Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).  |
| Acceso controlado a carpetas  | Los dispositivos deben tener habilitada la [protección en tiempo real de Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).   |
| Protección contra vulnerabilidades  | Ninguno  |
| Protección de redes  |  Los dispositivos deben tener habilitada la [protección en tiempo real de Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Creación de una directiva de Protección contra vulnerabilidades de seguridad  <!--1355468 -->
1. En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Endpoint Protection** y, a continuación, haga clic en **Protección contra vulnerabilidades de seguridad de Windows Defender**.
2. En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Create Exploit Policy** (Crear directiva para vulnerabilidades).
3. En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.
4. A continuación, seleccione los componentes de la Protección contra vulnerabilidades de seguridad que quiere administrar con esta directiva. Para cada componente que seleccione, puede configurar detalles adicionales.
   - **Reducción de la superficie expuesta a ataques:** configure las amenazas de Office, de scripting y de correo electrónico que quiera bloquear o auditar. También puede excluir determinados archivos o carpetas de esta regla.
   - **Acceso controlado a carpetas:** configure el bloqueo o la auditoría, y luego agregue las aplicaciones que pueden omitir esta directiva.  También puede especificar carpetas adicionales que no estén protegidas de forma predeterminada.
   - **Protección contra vulnerabilidades:**  especifique un archivo XML que contenga la configuración para mitigar las vulnerabilidades de las aplicaciones y los procesos del sistema. Puede exportar esta configuración desde la aplicación Centro de seguridad de Windows Defender en un dispositivo Windows 10.
   - **Protección de red:** configure la protección de red para bloquear o auditar el acceso a dominios sospechosos.
5. Complete el Asistente para crear la directiva, que más tarde puede implementar en los dispositivos.

### <a name="deploy-an-exploit-guard-policy"></a>Implementación de una directiva de Protección contra vulnerabilidades de seguridad     
Después de crear directivas de Protección contra vulnerabilidades de seguridad, use al asistente correspondiente para implementarlas. Para ello, abra la consola de Configuration Manager en **Activos y compatibilidad** > **Endpoint Protection** y, a continuación, haga clic en **Deploy Exploit Guard Policy** (Implementar directiva de Protección contra vulnerabilidades de seguridad).

## <a name="limited-support-for-cng-certificates"></a>Compatibilidad limitada con certificados CNG
<!-- 1356191 -->
A partir de esta versión, ahora se pueden usar plantillas de certificado [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) en los escenarios siguientes:

- Registro de cliente y comunicación con un punto de administración de HTTPS.   
- Distribución de software e implementación de aplicaciones con un punto de distribución de HTTPS.   
- Implementación de sistema operativo.  
- SDK de mensajería de cliente (con la actualización más reciente) y proxy de ISV.   
- Configuración de Cloud Management Gateway.  

Para usar certificados CNG, la entidad de certificación (CA) debe proporcionar plantillas de certificado CNG para las máquinas de destino.  Los detalles de la plantilla varían según el escenario; sin embargo, se requieren las siguientes propiedades:

- Pestaña **Compatibilidad**

    - La **entidad de certificación** debe ser Windows Server 2008 o posterior. (Se recomienda Windows Server 2012).

    - El **destinatario del certificado** debe ser Windows Vista o Server 2008 o posterior. (Se recomienda Windows 8/Windows Server 2012).

- Pestaña **Criptografía**

    - La **categoría del proveedor** debe ser **Proveedor de almacenamiento de claves**.  (Requerido)

Para obtener mejores resultados, se recomienda crear el nombre del sujeto a partir de la información de Active Directory.  Use el nombre de DNS como **formato de nombre de sujeto** e inclúyalo en el nombre de sujeto alternativo.  De lo contrario, tendrá que proporcionar esta información cuando el dispositivo se inscriba en el perfil de certificado.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Descripciones mejoradas para reinicios de equipo pendientes   <!--1356283 -->
En [Technical Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console), se ha agregado la posibilidad de identificar dispositivos que están pendientes de un reinicio en la consola de Configuration Manager.

A partir de esta versión preliminar técnica, la consola muestra detalles adicionales que proporcionan información sobre el proceso o la acción que solicitan el reinicio.

## <a name="device-guard-policy-changes----1355092---"></a>Cambios en la directiva de Device Guard <!-- 1355092 -->
Con la compilación de Technical Preview 1710, se han realizado los siguientes tres cambios en relación con las directivas de Device Guard:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Las directivas de Device Guard se llaman ahora directivas de Windows Defender Application Control
Las directivas de Device Guard se llaman ahora directivas de Windows Defender Application Control. Así, por ejemplo, el **Asistente para la creación de directivas de Device Guard** ahora se llama **Asistente para la creación de directivas de Windows Defender Application Control**.

### <a name="restart-is-not-required-to-apply-policies"></a>No es necesario reiniciar para aplicar las directivas
A partir de Windows Fall Creators Update, versión 1709, los dispositivos que usan la nueva versión de Windows no necesitan reiniciarse para aplicar las directivas de Control de aplicaciones de Windows Defender.

El reinicio es el valor predeterminado.

#### <a name="try-it-out"></a>Haga la prueba  

Si desea desactivar los reinicios, siga estos pasos:

1.  Abra el **Asistente para la creación de directivas de Windows Defender Application Control**.
2.  En la página **General**, desactive la casilla **Forzar un reinicio de los dispositivos para poder aplicar esta directiva a todos los procesos**.
3.  Haga clic en **Siguiente** hasta que finalice el asistente.

En versiones anteriores de Windows, se sigue aplicando un reinicio automatizado.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Ejecución automática de software en el que confía Intelligent Security Graph

Ahora, los administradores tienen la opción de permitir que los dispositivos bloqueados ejecuten software de confianza con una buena reputación, según determina Microsoft Intelligent Security Graph (ISG). El ISG está formado por Windows Defender SmartScreen y otros servicios de Microsoft.

Los dispositivos deben ejecutar Windows Defender SmartScreen para que el software sea de confianza.

#### <a name="try-it-out"></a>Haga la prueba  

Para permitir que un dispositivo que ejecuta Windows Defender SmartScreen ejecute software de confianza, siga estos pasos:

1.  Abra el **Asistente para la creación de directivas de Windows Defender Application Control**.
2.  En la página **Inclusiones**, active la casilla **Autorizar el software de confianza para Intelligent Security Graph**.
3.  En el cuadro **Archivos o carpetas de confianza**, agregue los archivos y las carpetas que quiere que sean de confianza.
4.  Haga clic en **Siguiente** hasta que finalice el asistente.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Configuración e implementación de directivas de Protección de aplicaciones de Windows Defender <!-- 1351960 -->

[Protección de aplicaciones de Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) es una nueva característica de Windows que ayuda a proteger a los usuarios al abrir los sitios web que no sean de confianza en un contenedor aislado seguro al que no puedan tener acceso otras partes del sistema operativo. En esta versión preliminar técnica, ya se admite la configuración de esta característica mediante las opciones de conformidad de Configuration Manager que establezca para, posteriormente, implementarla en una recopilación. Esta característica se publicará en la versión preliminar para la versión de 64 bits de Windows 10 Creators Update. Para probar esta característica ahora debe estar utilizando una versión preliminar de esta actualización.

### <a name="before-you-start"></a>Antes de empezar
Para crear e implementar directivas de Protección de aplicaciones de Windows Defender, los dispositivos de Windows 10 en los que implementa la directiva deben configurarse con una directiva de aislamiento de red. Para más información, consulte la entrada de blog a la que se hace referencia más adelante. Esta funcionalidad solo es aplicable a compilaciones de Windows 10 Insider actuales. Para probarla, los clientes deben ejecutar una compilación reciente de Windows 10 Insider.

### <a name="try-it-out"></a>Haga la prueba

Para comprender los aspectos básicos acerca de Windows Defender Application Guard, lea [la entrada del blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

Para crear una directiva y examinar la configuración disponible:
1. En la consola de **Configuration Manager**, elija **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad**, elija **Introducción** > **Endpoint Protection** > **Protección de aplicaciones de Windows Defender**.
3. En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear directiva de Protección de aplicaciones de Windows Defender**.
4. Con la entrada de blog como referencia, puede examinar y configurar las opciones disponibles para probar la característica.
5. En esta versión, hemos agregado la nueva página Definición de red al asistente. Especifique aquí la identidad corporativa y defina los límites de la red corporativa.

    > [!NOTE]
    > Los equipos con Windows 10 solo almacenan una lista de aislamiento de red en el cliente. En esta versión, puede crear dos tipos diferentes de listas de aislamiento de red (una de Windows Information Protection y otra de Windows Defender Application Guard) e implementarlas en el cliente. Si implementa ambas directivas, deben coincidir con estas listas de aislamiento de red. Si implementa listas que no coincidan con el mismo cliente, se producirá un error en la implementación.

    Puede encontrar más información sobre cómo especificar definiciones de red en la [documentación de Windows Information Protection]- [Proteger los datos de la empresa con Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Cuando haya terminado, complete el asistente e implemente la directiva en uno o varios dispositivos de Windows 10.

### <a name="further-reading"></a>Lectura adicional

Para obtener más información acerca de Protección de aplicaciones de Windows Defender, consulte [esta entrada de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Además, para obtener más información sobre el modo independiente de Protección de aplicaciones de Windows Defender, consulte [esta entrada de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
