---
title: Novedades de la versión 1910
titleSuffix: Configuration Manager
description: Obtenga detalles sobre los cambios y las nuevas funcionalidades incorporados en la versión 1910 de la rama actual de Configuration Manager.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 849dd0bdb0f6583d525df8af3f6d46f8a4a9aecf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904671"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Novedades de la versión 1910 de la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La actualización 1910 de la rama actual de Configuration Manager está disponible como una actualización en consola. Aplique esta actualización en los sitios que ejecuten la versión 1806 o versiones posteriores. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> En este artículo se resumen los cambios y las nuevas características de la versión 1910 de Configuration Manager.

Revise siempre la lista de comprobación más reciente para instalar esta actualización. Para más información, vea [Lista de comprobación para la instalación de la actualización 1910](../../servers/manage/checklist-for-installing-update-1910.md). Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).

Para aprovechar al máximo las nuevas características de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.

> [!TIP]
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a> Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager forma ahora parte de Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager es una solución integrada para administrar todos los dispositivos. Microsoft aúna Configuration Manager e Intune con licencias simplificadas. Siga aprovechando las inversiones existentes en Configuration Manager y saque partido de las ventajas de la eficacia de la nube de Microsoft a su propio ritmo.

Las siguientes soluciones de administración de Microsoft ahora forman parte de la marca Microsoft Endpoint Manager:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Análisis de escritorio](../../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Otras características de la [consola de administración de dispositivos](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760).

Para más información, consulte las siguientes entradas de Brad Anderson, vicepresidente corporativo de Microsoft para Microsoft 365:

- [Entrada de blog de anuncio](https://aka.ms/cmannounce)
- [Documento sobre la visión](https://aka.ms/MEMVisionPaper)
- [Vídeo de resumen del anuncio](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>¿Qué cambia en Configuration Manager con Microsoft Endpoint Manager?

Aparte del cambio de nombre, el funcionamiento de Configuration Manager en la versión 1910 sigue siendo el mismo. Algunos de los cambios de nombre podrían afectar al uso de los siguientes componentes:

- **Consola de Configuration Manager**: busque accesos directos a la consola y al **visor de control remoto** en el menú Inicio de Windows, en la carpeta **Microsoft Endpoint Manager**.

- **Centro de software**: busque el acceso directo al Centro de software en el menú Inicio de Windows, en la carpeta **Microsoft Endpoint Manager**.

![Iconos del menú Inicio de Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

Asegúrese de actualizar cualquier documentación interna que conserve para que refleje estas nuevas ubicaciones.

> [!TIP]
> En Windows 10, cuando abra el menú Inicio, escriba el nombre para encontrar el icono. Por ejemplo, escriba `Configuration Manager` o `Software Center`.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Infraestructura del sitio

### <a name="reclaim-sedo-lock"></a>Reclamación del bloqueo SEDO

<!--4786915-->

A partir de la [versión 1906 de la rama actual](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences), puede borrar el bloqueo en una secuencia de tareas. Ahora, puede borrar el bloqueo en cualquier objeto de la consola de Configuration Manager.

Para obtener más información, vea [Uso de la consola de Configuration Manager](../../servers/manage/admin-console.md#bkmk_sedo).

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Extensión y migración de un sitio local a Microsoft Azure
<!--3556022-->

Esta herramienta nueva lo ayuda a crear máquinas virtuales (VM) de Azure para Configuration Manager mediante programación. Se puede instalar con roles de sitio de configuración predeterminados, como un servidor de sitio pasivo, puntos de administración y puntos de distribución. Una vez validados los nuevos roles, úselos como sistemas de sitio adicionales para lograr alta disponibilidad. También puede quitar el rol de sistema de sitio local y mantener solo el rol de máquina virtual de Azure.

Para más información, vea [Extensión y migración de un sitio local a Microsoft Azure](../../support/azure-migration-tool.md).

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Análisis de escritorio

Para más información sobre los cambios mensuales en el servicio en la nube de Análisis de escritorio, vea [Novedades de Análisis de escritorio](../../../desktop-analytics/whats-new.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Administración en tiempo real

### <a name="optimizations-to-the-cmpivot-engine"></a>Optimizaciones del motor de CMPivot
<!--3197353-->
Hemos agregado algunas optimizaciones significativas al motor de CMPivot. Ahora, el cliente de Configuration Manager se puede encargar de un mayor procesamiento. Las optimizaciones reducen drásticamente la carga de CPU del servidor y de la red necesaria para ejecutar consultas de CMPivot. Con estas optimizaciones, ahora se pueden examinar los gigabytes de datos de cliente en tiempo real. 

Para más información, vea [Optimizaciones del motor de CMPivot](../../servers/manage/cmpivot.md#bkmk_optimization).

### <a name="additional-cmpivot-entities-and-enhancements"></a>Entidades y mejoras de CMPivot adicionales
<!--5410930-->
Hemos agregamos una serie entidades nuevas de CMPivot y mejoras de entidades a modo de ayuda en la solución de problemas y en las búsquedas. Hemos incluido las siguientes entidades de consulta:

- Registros de eventos de Windows ([WinEvent](../../servers/manage/cmpivot.md#bkmk_WinEvent))
- Contenido de archivo ([FileContent](../../servers/manage/cmpivot.md#bkmk_File))
- DLL cargados por procesos ([ProcessModule](../../servers/manage/cmpivot.md#bkmk_ProcessModule))
- Información de Azure Active Directory ([AADStatus](../../servers/manage/cmpivot.md#bkmk_AadStatus))
- Estado de protección de punto de conexión ([EPStatus](../../servers/manage/cmpivot.md#bkmk_EPStatus))

Esta versión también incluye muchas [otras mejoras](../../servers/manage/cmpivot.md#bkmk_Other) en CMPivot. Para más información, vea [CMPivot a partir de la versión 1910](../../servers/manage/cmpivot.md#bkmk_cmpivot1910).

## <a name="content-management"></a><a name="bkmk_content"></a> Administración de contenido

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Compatibilidad con la caché de conexión de Microsoft en aplicaciones Win32 de Intune

<!--5032900-->

Cuando se habilita la caché conectada de Microsoft en los puntos de distribución de Configuration Manager, ahora pueden suministrar aplicaciones Win32 de Microsoft Intune a los clientes administrados conjuntamente.

Para más información, vea [Caché con conexión de Microsoft en Configuration Manager](../hierarchy/microsoft-connected-cache.md#bkmk_intune).

> [!NOTE]
> La versión 1906 de la rama actual de Configuration Manager incluía la [caché en la red de Optimización de distribución](../hierarchy/microsoft-connected-cache.md) (DOINC), una aplicación instalada en Windows Server que todavía está en desarrollo. A partir de la versión 1910 de la rama actual, esta característica se llama caché conectada de Microsoft.
>
> Cuando se instala la caché conectada en un punto de distribución de Configuration Manager, se descarga el tráfico del servicio de optimización de entrega en los orígenes locales. Para lograr este comportamiento, la caché conectada almacena en caché de eficazmente el contenido en el nivel de intervalo de bytes.

## <a name="client-management"></a><a name="bkmk_client"></a> Administración de clientes

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Inclusión de líneas base de configuración personalizadas como parte de la evaluación de las directivas de cumplimiento
<!--3608345-->

Ahora puede agregar la evaluación de líneas base de configuración personalizadas como regla de evaluación de las directivas de cumplimiento. Al crear o editar una línea base de configuración, ahora existe la posibilidad de usar la opción **Evaluar la línea base como parte de la evaluación de las directivas de cumplimiento**. Al agregar o editar una regla de directivas de cumplimiento, tiene una condición denominada **Incluir las líneas base configuradas en la evaluación de las directivas de cumplimiento**.

Respecto a los dispositivos administrados conjuntamente, al configurar Intune para que tome los resultados de la evaluación de cumplimiento de Configuration Manager como parte del estado general de cumplimiento, esta información se envía a Azure Active Directory, lo cual le permite usarla para el acceso condicional a los recursos de Office 365.

Para más información, vea [Inclusión de líneas base de configuración personalizadas como parte de la evaluación de las directivas de cumplimiento](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Habilitar la directiva de usuario de sesiones múltiples de Windows 10 Enterprise

<!--4737447-->

La versión 1906 de la rama actual de Configuration Manager ha incluido compatibilidad con [Windows Virtual Desktop](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop). Este entorno de Microsoft Azure admite varias versiones de sistema operativo, algunas de las cuales permiten varias sesiones de usuario activas simultáneas (por ejemplo, la multisesión de Windows 10 Enterprise es una de estas versiones de SO).

Si requiere una directiva de usuario en estos dispositivos multisesión y acepta cualquier posible impacto en el rendimiento, ahora puede establecer una configuración de cliente para habilitar la directiva de usuario. En el grupo **Directiva de cliente**, configure la opción **Habilitar directiva de usuario para varias sesiones de usuario**.

Para obtener más información, vea [Cómo configurar el cliente](../../clients/deploy/configure-client-settings.md).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a> Administración de aplicaciones

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Implementación de Microsoft Edge, versión 77 y posteriores
<!--4561024-->
La nueva versión de Microsoft Edge está lista para empresas. Ahora, puede implementar Microsoft Edge, versión 77 y posteriores para los usuarios. Los administradores pueden elegir el canal de la versión beta, de desarrollo o estable, junto con una versión del cliente de Microsoft Edge que se va a implementar.

Para más información, vea [Implementación de Microsoft Edge, versión 77, y versiones posteriores](../../../apps/deploy-use/deploy-edge.md).

### <a name="improvements-to-application-groups"></a>Mejoras en los grupos de aplicaciones

<!--4760058-->

A partir de la versión 1906 de la rama actual, puede crear un grupo de aplicaciones para enviarlo a una colección de dispositivos como una sola implementación. Esta versión mejora esta característica:

- Los usuarios no pueden seleccionar **Desinstalar** en el grupo de aplicaciones en el Centro de software.
- Se puede implementar un grupo de aplicaciones en una **colección de usuarios**.

Para obtener más información general, consulte [Creación de grupos de aplicaciones](../../../apps/deploy-use/create-app-groups.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementación del sistema operativo

### <a name="improvements-to-the-task-sequence-editor"></a>Mejoras en el editor de secuencia de tareas

 El editor de secuencia de tareas incluye las siguientes mejoras:

- **Búsqueda en el editor de secuencias de tareas:**<!--4621085--> Si tiene una secuencia de tareas de gran tamaño con muchos pasos y grupos, encontrar pasos específicos puede ser difícil. Ahora, se pueden realizar búsquedas en el editor de secuencias de tareas. Esta acción le permite localizar más rápidamente los pasos en una secuencia de tareas.
- **Copia y pegado de las condiciones de una secuencia de tareas:**<!--4621098--> Si quiere reutilizar las condiciones de un paso de secuencia de tareas a otro, ahora puede copiar y pegar condiciones en el editor de secuencia de tareas.

Para más información, vea el nuevo artículo sobre cómo [usar el editor de secuencia de tareas](../../../osd/understand/task-sequence-editor.md).

### <a name="task-sequence-performance-improvements-power-plans"></a>Mejoras de rendimiento de las secuencias de tareas: planes de energía

<!--3555926-->

Ahora, puede ejecutar una secuencia de tareas con el plan de energía de alto rendimiento. Esta opción mejora la velocidad total de la secuencia de tareas. Configura Windows para usar el plan de energía de alto rendimiento integrado, que proporciona el máximo rendimiento con el consiguiente aumento del consumo de energía.

Para más información, vea [Mejoras en el rendimiento de los planes de energía](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf).

### <a name="task-sequence-download-on-demand-over-the-internet"></a>Descarga de secuencias de tareas a petición a través de Internet

<!--3601238-->

Puede usar la secuencia de tareas para implementar la actualización en contexto de Windows 10 a través de Cloud Management Gateway (CMG). Sin embargo, requiere que la implementación descargue todo el contenido localmente antes de iniciar la secuencia de tareas.

A partir de esta versión, el motor de secuencia de tareas puede descargar paquetes a petición desde una instancia de CMG habilitada para contenido o un punto de distribución de nube. Este cambio proporciona una flexibilidad adicional con las implementaciones de actualización en contexto de Windows 10 en dispositivos basados en Internet.

Para obtener más información, vea [Implementar una actualización local de Windows 10 a través de CMG](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-os-deployment"></a>Mejoras en la implementación del sistema operativo

Esta versión incluye las siguientes mejoras en las implementaciones de sistema operativo.

#### <a name="boot-image-keyboard-layout"></a>Distribución del teclado de imagen de arranque

<!--4910348-->

Configure la distribución del teclado predeterminada para una imagen de arranque. En la pestaña **Personalización** de una imagen de arranque, use la nueva opción **Establecer la distribución del teclado predeterminada en WinPE**. Si selecciona un idioma distinto de es-es, Configuration Manager sigue incluyéndolo en las configuraciones regionales disponibles. En el dispositivo, el diseño de teclado inicial es la configuración regional seleccionada, pero el usuario puede cambiar el dispositivo a es-es si es necesario.

Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../../../osd/get-started/manage-boot-images.md#customization).

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Importación de un índice único de un paquete de actualización de sistema operativo

<!--4931110-->

Al importar el paquete de actualización de un sistema operativo, se puede usar la opción **Extraer un índice de imágenes específico del archivo install.wim del paquete de actualización seleccionado**. Este comportamiento es similar a lo que ocurre con las [imágenes del sistema operativo](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages), excepto en que se sobrescribe el archivo install.wim existente en el paquete de actualización del sistema operativo. Extrae el índice de imágenes a una ubicación temporal y, luego, lo mueve al directorio de origen original.

Para más información, vea [Administrar paquetes de actualización de sistema operativo](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs).

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>Salida de los resultados de un paso Ejecutar línea de comandos en una variable durante una secuencia de tareas

<!--user story 4977616/bug 4798352-->

Ahora, el paso **Ejecutar línea de comandos** incluye una opción **Salida a la variable de secuencia de tareas**. Cuando se habilita esta opción, la secuencia de tareas guarda la salida del comando en una variable de secuencia de tareas personalizada que especifique.

Para obtener más información, consulte [Ejecutar línea de comandos](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine).

#### <a name="improvements-to-task-sequence-debugger"></a>Mejoras en el depurador de secuencias de tareas

En esta versión se incluyen las siguientes mejoras en el depurador de secuencias de tareas:

- Use la variable de secuencia de tareas nueva **TSDebugOnError** para iniciar automáticamente el depurador cuando la secuencia de tareas devuelve un error.<!-- 5012536 -->
- Si crea un punto de interrupción en el depurador y, a continuación, la secuencia de tareas reinicia el equipo, el depurador mantiene los puntos de interrupción después del reinicio.<!-- 5012509 -->

Para más información, vea [Depurador de secuencias de tareas](../../../osd/deploy-use/debug-task-sequence.md) y [Variables de secuencia de tareas: TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError).

#### <a name="improved-language-support-in-task-sequence"></a>Mejor compatibilidad de idiomas en la secuencia de tareas

<!--5411057, 5138936-->

En esta versión se agrega control sobre la configuración de idioma durante la implementación del sistema operativo. Si ya está aplicando esta configuración de idioma, este cambio puede ayudarlo a simplificar la secuencia de tareas de implementación del sistema operativo. En lugar de usar varios pasos por idioma o scripts separados, use una instancia por idioma del paso **Aplicar configuraciones de Windows** integrado con una condición para ese idioma.

Use el paso **Aplicar configuraciones de Windows** de la secuencia de tareas para ajustar la nueva configuración:

- Idioma de entrada (distribución del teclado predeterminada)
- Configuración regional del sistema
- Idioma de la UI
- Reserva del idioma de la UI
- Configuración regional del usuario

Para obtener más información, consulte [Aplicar configuraciones de Windows](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Variable nueva para la actualización local de Windows 10

<!--4680263-->

Para abordar las incidencias de temporización con la secuencia de tareas de la actualización local de Windows 10 en dispositivos de alto rendimiento cuando se completa la instalación de Windows, ahora puede establecer una nueva variable de secuencia de tareas, **SetupCompletePause**. Cuando asigna un valor en segundos a esta variable, el proceso de instalación de Windows retrasa la cantidad de tiempo antes de iniciar la secuencia de tareas. Este tiempo de espera proporciona el cliente de Configuration Manager tiempo adicional para la inicialización.

Para más información, vea [Variables de secuencia de tareas: SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> Actualizaciones de software

### <a name="additional-options-for-third-party-update-catalogs"></a>Opciones adicionales para los catálogos de actualizaciones de terceros
<!--4469002-->
Ahora, existen controles más granulares sobre la sincronización de catálogos de actualizaciones de terceros. A partir de la versión 1910 de Configuration Manager, puede configurar la programación de sincronización de cada catálogo de manera independiente. Al usar catálogos que incluyen actualizaciones clasificadas, puede configurar la sincronización de forma que incluya solo determinadas categorías de actualizaciones y, así, evitar la sincronización de todo el catálogo. Con los catálogos clasificados, cuando esté seguro de implementar una categoría, puede configurarla para que se descargue y publique automáticamente en Windows Server Update Services (WSUS).

Para obtener más información, vea [Habilitar actualizaciones de terceros](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910).

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Uso de Optimización de entrega para todas las actualizaciones de Windows
<!--4699118-->
Anteriormente, Optimización de distribución solo se podía usar con las actualizaciones rápidas. Con la versión 1910 de Configuration Manager, ahora se puede usar Optimización de distribución para la distribución de todo el contenido de Windows Update en clientes que ejecutan la versión 1709 o posterior de Windows 10.

Para obtener más información, vea:
- [Optimizar la distribución de actualizaciones de Windows 10](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [Configuración de cliente para las actualizaciones de software](../../clients/deploy/about-client-settings.md#software-updates)
- [Configuración de cliente para Optimización de distribución](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>Filtro de actualización de software adicional para ADR
<!--4852033-->
Ahora, puede usar **Implementado** como un filtro de actualización en las reglas de implementación automática (ADR). Este filtro ayuda a identificar las actualizaciones nuevas que se deben implementar en las colecciones de prueba o piloto.

Para más información, vea [Implementar actualizaciones de software automáticamente](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

## <a name="office-management"></a><a name="bkmk_o365"></a> Administración de Office


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Panel de estado y piloto de Office 365 ProPlus
<!--4488272, 4488301-->

Office 365 ProPlus Piloto y el panel de estado ayudan a planear, probar e implementar Office 365 ProPlus. El panel proporciona información sobre el estado de los dispositivos con Office 365 ProPlus para ayudar a identificar posibles problemas que puedan afectar a los planes de implementación. En el Panel de estado y piloto de Office 365 ProPlus se proporciona una recomendación para dispositivos piloto basada en el inventario de complementos.

Para más información, vea [Office 365 ProPlus Piloto y panel de estado](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot).

## <a name="protection"></a><a name="bkmk_protect"></a> Protección

### <a name="bitlocker-management"></a>Administración de BitLocker

<!--3601034-->

Ahora, Configuration Manager proporciona las siguientes capacidades de administración de Cifrado de unidad BitLocker:

- Implementación del cliente de BitLocker en dispositivos Windows administrados
- Administración de directivas de cifrado de dispositivos
- Informes de cumplimiento de certificados
- Uso de un sitio web de administración y supervisión para la recuperación de claves
- Acceso a un portal de autoservicio de usuario

Para más información, vea [Planeación de la administración de BitLocker](../../../protect/plan-design/bitlocker-management.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Consola de Configuration Manager

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Visualización de las consolas activas y envío de mensajes a administradores a través de Conexiones de la consola
<!--4923997-->
Hemos realizado las siguientes mejoras en **Conexiones de la consola**:

- La posibilidad de enviar mensajes a otros administradores de Configuration Manager mediante Microsoft Teams.
- La columna **Last Console Heartbeat** (Último latido de la consola) ha reemplazado a la columna **Hora de la última conexión**.
  - Una consola abierta en primer plano envía un latido cada 10 minutos para ayudar a determinar qué conexiones de consola están activas actualmente.

Para más información, vea [Visualización de las consolas conectadas recientemente](../../servers/manage/admin-console.md#bkmk_viewconnected) y [Mensajes a administradores](../../servers/manage/admin-console.md#bkmk_message).

### <a name="client-diagnostics-actions"></a>Acciones de diagnóstico del cliente

<!--4433455-->

Hay nuevas acciones de dispositivo de **Diagnósticos del cliente** en la consola de Configuration Manager:

- **Habilitar el registro detallado:** cambie el nivel de registro global del componente CCM a *detallado* y habilite el registro de depuración.
- **Deshabilitar el registro detallado:** cambie el nivel de registro global a *predeterminado* y deshabilite el registro de depuración.

Para más información, vea [Diagnósticos del cliente](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="improvements-to-console-search"></a>Mejoras en las búsquedas de consola
<!--4640570-->

Esta versión incluye las siguientes mejoras en las búsquedas realizadas en la consola de Configuration Manager:

- Ahora puede usar la opción de búsqueda **Todas las subcarpetas** de los nodos **Paquetes de controladores** y **Consultas**.<!--2841181,5424892-->
- Cuando una búsqueda devuelve más de 1000 resultados, seleccione el botón **Aceptar** en la barra de avisos para ver más resultados.<!--4640570-->

## <a name="other-updates"></a>Otras actualizaciones

Para más información sobre los cambios en los cmdlets de Windows PowerShell relativos a Configuration Manager, vea las [notas de la versión de PowerShell 1910](https://docs.microsoft.com/powershell/sccm/1910-release-notes?view=sccm-ps).

Para obtener más información sobre los cambios en la API REST del servicio de administración, consulte las [notas de la versión del servicio de administración](../../../develop/adminservice/release-notes.md#bkmk_1910).

Además de nuevas características, esta versión también incluye cambios adicionales como, por ejemplo, correcciones de errores. Para más información, vea [Resumen de cambios en la rama actual de Configuration Manager, versión 1910](https://support.microsoft.com/help/4535776).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
El siguiente paquete acumulativo de actualizaciones (4537079) está disponible en la consola desde el 18 de febrero de 2020: [Paquete acumulativo de actualizaciones para la rama actual de Microsoft Endpoint Configuration Manager, versión 1910](https://support.microsoft.com/help/4537079).



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Pasos siguientes

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
A partir del 20 de diciembre de 2019, la versión 1910 está disponible globalmente para que todos los clientes puedan instalarla.

Cuando esté listo para instalar esta versión, vea [Instalación de actualizaciones para Configuration Manager](../../servers/manage/updates.md) y [Lista de comprobación para la instalación de la actualización 1910](../../servers/manage/checklist-for-installing-update-1910.md).

> [!TIP]
> Para instalar un sitio nuevo, use una versión de línea de base de Configuration Manager.
>
> Más información acerca de:
>
> - [Instalación de nuevos sitios](../../servers/deploy/install/installing-sites.md) 
> - [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines) 

Para conocer los problemas conocidos e importantes, vea las [Notas de la versión](../../servers/deploy/install/release-notes.md).

Después de actualizar un sitio, revise también la [lista de comprobación posterior a la actualización](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).
