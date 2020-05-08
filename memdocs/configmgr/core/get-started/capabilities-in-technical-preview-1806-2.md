---
title: Technical Preview 1806.2
titleSuffix: Configuration Manager
description: Conozca las nuevas características disponibles en la versión Technical Preview 1806.2 de Configuration Manager.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b7643c73d2e9dad00e926bdc3db905016c45860a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905216"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Funciones de Technical Preview 1806.2 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en Technical Preview 1806.2 de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de versión preliminar técnica. 

Revise el artículo [Technical Preview para System Center Configuration Manager](technical-preview.md) antes de instalar esta actualización. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## <a name="known-issues-in-this-technical-preview"></a>Problemas conocidos de esta Technical Preview

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a> Los clientes no se actualizan automáticamente
<!--518760-->
Al actualizar a la versión 1806.2, el sitio también actualiza SQL Native Client, que puede activar un reinicio pendiente en el servidor de sitio. Este retraso hace que determinados archivos no se actualicen, lo que influye en la actualización automática del cliente.

#### <a name="workarounds"></a>Soluciones alternativas
Evite este problema con la actualización manual de SQL Native Client *antes de actualizar* Configuration Manager a la versión 1806.2. Para más información, vea [Última actualización de mantenimiento disponible para Microsoft SQL Server 2012 Native Client](https://www.microsoft.com/download/details.aspx?id=50402).

Si ya ha actualizado el sitio, la actualización automática del cliente y la inserción de cliente no funcionarán. Deberá actualizar los clientes para probar completamente la mayoría de las nuevas características. Actualice manualmente los clientes de Technical Preview con el siguiente proceso:  

1. Busque los archivos de origen del cliente en la carpeta **CMUClient** del directorio de instalación de Configuration Manager en el servidor de sitio. Por ejemplo, `C:\Program Files\Configuration Manager\CMUClient`.  

2. Copie la carpeta completa de CMUClient en el dispositivo de cliente. Por ejemplo, `C:\Temp\CMUClient`.  

    Esta ubicación puede ser un recurso compartido de red al que se puede acceder desde los clientes.  

3. Ejecute la línea de comandos siguiente desde un símbolo del sistema con permisos elevados: `C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Si va a instalar un nuevo cliente en el sitio de Technical Preview 1806.2, use este mismo proceso. 

> [!Important]  
> No use el parámetro de línea de comandos `/MP` en este escenario. Este parámetro tiene prioridad sobre `/source` y hace que ccmsetup descargue el contenido de cliente desde el punto de distribución o el punto de administración.
> 
> Se pueden usar las propiedades de línea de comandos, como SMSSITECODE o CCMLOGLEVEL, pero no deberían ser necesarias al actualizar un cliente existente. 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a> La versión 1806.2 aparece como la versión 1806 en Acerca de Configuration Manager
<!--518148-->
Después de actualizar a la versión 1806.2 de Technical Preview, si abre la ventana **Acerca de Configuration Manager** desde la esquina superior izquierda de la consola, aún aparece como **Versión 1806**. 

#### <a name="workaround"></a>Solución alternativa
Use la propiedad **Versión del sitio** para determinar la diferencia entre 1806 y 1806.2:

| Versión del sitio  | Version
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**Estas son las nuevas características que puede probar con esta versión.**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a> Mejoras en las implementaciones por fases

Esta versión incluye las siguientes mejoras para las [implementaciones por fases](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md):
- [Estado de la implementación por fases](#bkmk_pod-monitor)
- [Implementación de aplicaciones por fases](#bkmk_pod-app)
- [Lanzamiento gradual durante las implementaciones por fases](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a> Estado de la implementación por fases
<!--1358577-->
Las implementaciones por fases ahora tienen una experiencia de supervisión nativa. En el nodo **Implementaciones** del área de trabajo **Supervisión**, seleccione una implementación por fases y luego haga clic en **Estado de implementación por fases** en la cinta de opciones.

![Panel de estado de implementación por fases que muestra el estado de dos fases](media/1358577-phased-deployment-status.png)

Este panel muestra la siguiente información para cada fase de la implementación:  

- **Dispositivos en total**: número de dispositivos que abarca esta fase.  

- **Estado**: indica el estado actual de esta fase. Cada fase puede tener uno de los siguientes estados:  

    - **Implementación creada**: la implementación por fases creó una implementación del software en la colección para esta fase. Los clientes son destinos activos con este software.  

    - **En espera**: la fase anterior aún no ha alcanzado los criterios de idoneidad para que la implementación continúe en esta fase.  

    - **Suspendida**: un administrador ha suspendido la implementación.  

- **Progreso**: estados de implementación con códigos de color de los clientes. Por ejemplo: Correcto, En curso, Error, Requisitos no cumplidos y Desconocido. 


#### <a name="known-issue"></a>Problema conocido
El panel de estado de la implementación por fases puede mostrar varias filas para la misma fase.<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a> Implementación de aplicaciones por fases
<!--1358147-->
Cree implementaciones por fases para las aplicaciones. Las Implementaciones por fases permiten organizar un lanzamiento de software coordinado y secuencial según criterios y grupos personalizables.

En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione **Aplicaciones**. Seleccione una aplicación y después haga clic en **Crear una implementación por fases** en la cinta de opciones. 

El comportamiento de una implementación de aplicaciones por fases es el mismo que para las secuencias de tareas. Para más información, vea [Creación de implementaciones por fases para una secuencia de tareas](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

#### <a name="prerequisite"></a>Requisito previo
Distribuya el contenido de la aplicación a un punto de distribución antes de crear la implementación por fases.<!--518293-->

#### <a name="known-issue"></a>Problema conocido
No se pueden crear las fases de una aplicación manualmente. El asistente crea automáticamente dos fases para las implementaciones de aplicaciones.


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a> Lanzamiento gradual durante las implementaciones por fases
<!--1358578-->
Durante una implementación por fases, el lanzamiento de cada fase ahora puede realizarse de forma gradual. Este comportamiento ayuda a mitigar el riesgo de problemas de implementación y disminuye la carga en la red provocada por la distribución de contenido a los clientes. El sitio puede habilitar la disponibilidad del software de forma gradual en función de la configuración de cada fase. Cada cliente de una fase tiene una fecha límite en relación con el tiempo de disponibilidad del software. La ventana de tiempo entre el tiempo disponible y la fecha límite es la misma para todos los clientes de una fase. 

Al crear una implementación por fases y configurar una fase manualmente, en la página **Configuración de fase** del Asistente para agregar fases o en la página **Configuración** del Asistente para crear una implementación por fases, configure la opción: **Poner este software a disposición de los usuarios gradualmente en este período de tiempo (en días)** . El valor predeterminado de esta configuración es **0**, por lo que de forma predeterminada la implementación no está limitada.

> [!Note]  
> Esta opción solo está disponible actualmente para las implementaciones por fases de las secuencias de tareas.  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a> Compatibilidad con nuevos formatos de paquete de aplicaciones de Windows
<!--1357427-->
Configuration Manager admite ahora la implementación de nuevos formatos del paquete de la aplicación (.msix) y del lote de aplicaciones (.msixbundle) de Windows 10. La compatibilidad con estos formatos está disponible en la [versión preliminar de Windows Insider](https://insider.windows.com/).

Para obtener información general de MSIX, consulte [A closer look at MSIX](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix) (Análisis exhaustivo de MSIX).

Para crear una aplicación MSIX, vea [MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376) (Compatibilidad de MSIX introducida en la compilación 17682 de Insider).

### <a name="prerequisites"></a>Requisitos previos
- Un cliente de Windows 10 que ejecute al menos la compilación 17682 de Windows Insider Preview
- Un paquete de aplicación de Windows con el formato MSIX

### <a name="try-it-out"></a>Haga la prueba
Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, [cree una aplicación](../../apps/deploy-use/create-applications.md). 
2. Seleccione el **Tipo** de archivo de instalación de la aplicación como **Paquete de aplicación de Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** .
3. [Implemente la aplicación](../../apps/deploy-use/deploy-applications.md) en el cliente que ejecuta la última compilación de Windows Insider Preview.



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a> Mejora de seguridad de inserción de cliente
<!--1358204-->
Cuando se usa el método de [inserción de cliente](../clients/deploy/plan/client-installation-methods.md#client-push-installation) para instalar el cliente de Configuration Manager, el servidor de sitio crea una conexión remota al cliente para iniciar la instalación. A partir de esta versión, el sitio puede requerir la autenticación mutua de Kerberos al no permitir el retroceso a NTLM antes de establecer la conexión. Esta mejora ayuda a proteger la comunicación entre el servidor y el cliente. 

En función de las directivas de seguridad, puede que el entorno ya prefiera o requiera Kerberos en lugar de la autenticación NTLM anterior. Para más información sobre las consideraciones de seguridad de estos protocolos de autenticación, vea la [configuración de la directiva de seguridad de Windows para restringir NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Requisito previo

Para usar esta característica, los clientes deben estar en un bosque de Active Directory de confianza. Kerberos en Windows se basa en Active Directory para la autenticación mutua. 


### <a name="try-it-out"></a>Haga la prueba

Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

Al actualizar el sitio, se conserva el comportamiento existente. Una vez *abiertas* las propiedades de instalación de inserción de cliente, el sitio habilita automáticamente la comprobación de Kerberos. Si es necesario, puede permitir que la conexión revierta al uso de una conexión NTLM menos segura, aunque no es recomendable. 

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda el nodo **Configuración del sitio** y haga clic en **Sitios**. Seleccione el sitio de destino. En la cinta de opciones, haga clic en **Configuración de instalación de cliente** y seleccione **Instalación de inserción de cliente**.  

2. El sitio ahora ha habilitado la comprobación de Kerberos para la inserción de cliente. Haga clic en **Aceptar** para cerrar la ventana.  

3. Si es necesario para su entorno, en la ventana Propiedades de instalación de inserción de cliente de la pestaña **General**, vea la opción **Allow connection fallback to NTLM** (Permitir reversión de conexión a NTLM). Esta opción está deshabilitada de forma predeterminada. 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a> Información de administración para un mantenimiento proactivo
<!--1352184,et al-->
En esta versión se encuentra disponible información adicional sobre administración para resaltar posibles problemas de configuración. Revise las siguientes reglas en el nuevo grupo **Mantenimiento proactivo**:  

- **Elementos de configuración no utilizados**: elementos de configuración que no forman parte de una línea base de configuración y tienen más de 30 días.  

- **Imágenes de arranque no utilizadas**: imágenes de arranque a las que no hay ninguna referencia para el uso de la secuencia de tareas o del arranque PXE.  

- **Grupos de límites sin sistemas de sitio asignados**: sin los sistemas de sitio asignados, los grupos de límites solo pueden usarse para la asignación de sitio.  

- **Grupos de límites sin miembros**: los grupos de límites no son aplicables a la asignación de sitio ni a la búsqueda de contenido si no tienen ningún miembro.  

- **Puntos de distribución que no proporcionan contenido a los clientes**: puntos de distribución que no han proporcionado contenido a los clientes en los treinta últimos días. Estos datos se basan en los informes de los clientes de su historial de descargas.  

- **Actualizaciones expiradas encontradas**: las actualizaciones expiradas no son aplicables a las implementaciones.   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a> Carga de trabajo de aplicaciones móviles de transición para los dispositivos administrados conjuntamente
<!--1357892-->
Administre las aplicaciones móviles con Microsoft Intune, a la vez que sigue usando Configuration Manager para implementar aplicaciones de escritorio de Windows. Para realizar la transición de la carga de trabajo de aplicaciones modernas, vaya a la página de propiedades de administración conjunta. Mueva la barra del control deslizante de Configuration Manager a Piloto o a Todos. 

Después de realizar la transición de esta carga de trabajo, las aplicaciones disponibles implementadas desde Intune están disponibles en el Portal de empresa. Las aplicaciones implementadas desde Configuration Manager están disponibles en el Centro de software. 

Vea los siguientes artículos para más información:  

- [Administración conjunta para dispositivos Windows 10](../../comanage/overview.md)  

- [¿Qué es la administración de aplicaciones de Microsoft Intune?](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a> Opciones de grupo de límites para descargas del mismo nivel
<!--1356193-->
Los grupos de límites ahora incluyen valores de configuración adicionales para ofrecerle mayor control sobre la distribución de contenido en su entorno. Esta versión agrega las siguientes opciones:  

- **Permitir descargas del mismo nivel en este grupo de límites**: Esta opción está habilitada de forma predeterminada. El punto de administración proporciona a los clientes una lista de ubicaciones de contenido que incluye orígenes del mismo nivel. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Hay dos escenarios comunes en que debe considerar la deshabilitación de esta opción:  

    - Si tiene un grupo de límites que incluye límites de ubicaciones dispersas geográficamente, como una VPN. Dos clientes pueden estar en el mismo grupo de límites porque se conectan a través de la VPN, pero en ubicaciones muy diferentes que resultan inapropiadas para el uso compartido de contenido del mismo nivel.  

    - Si utiliza un único grupo de límites grande para la asignación de sitio, no hace referencia a ningún punto de distribución.  

- **Durante las descargas del mismo nivel, use solo elementos del mismo nivel dentro de la misma subred**: Esta configuración depende de la anterior. Si habilita esta opción, el punto de administración solo se incluye en los orígenes del mismo nivel de la lista de ubicaciones de contenido que se encuentran en la misma subred que el cliente.

    Escenarios comunes para habilitar esta opción:

    - El diseño del grupo de límites para la distribución de contenido incluye un grupo de límites grande que se superpone a otros más pequeños. Con esta nueva configuración, la lista de orígenes de contenido que el punto de administración proporciona a los clientes solo incluye los orígenes del mismo nivel de la misma subred.

    - Tiene un único grupo de límites grande para todas las ubicaciones de oficinas remotas. Habilite esta opción, que permite que los clientes solo compartan contenido dentro de la subred en la ubicación de la oficina remota, en lugar de arriesgarse a compartir contenido entre ubicaciones.


### <a name="known-issue"></a>Problema conocido
Si el cliente del origen del mismo nivel tiene más de una dirección IP (IPv4, IPv6 o ambas), no funciona el almacenamiento en caché del mismo nivel. La nueva opción, **Durante las descargas del mismo nivel, use solo elementos del mismo nivel dentro de la misma subred**, no tiene ningún efecto si el origen del mismo nivel tiene más de una dirección IP.<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a> Soporte técnico de actualizaciones de software de terceros para catálogos personalizados
<!--1358714-->
En esta versión se amplía la compatibilidad con las actualizaciones de software de terceros como resultado de los [comentarios de UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co) de los clientes. [La versión 1806 de Technical Preview](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) proporcionaba compatibilidad con los *catálogos de asociados*, que son catálogos registrados de proveedores de software. Los catálogos que proporciona y que no están registrados en Microsoft se denominan *catálogos personalizados*. Agregue catálogos personalizados en la consola de Configuration Manager.  


### <a name="prerequisites"></a>Requisitos previos 

- Configure las [actualizaciones de software de terceros](capabilities-in-technical-preview-1806.md#bkmk-3pupdate). Complete la fase 1: Habilitar y configurar la característica.   

- Un catálogo personalizado firmado digitalmente que contenga actualizaciones de software con firma digital.  

- El administrador requiere los permisos siguientes:  

    - Sitio: Crear, Modificar  


### <a name="try-it-out"></a>Haga la prueba

Intente completar las tareas. Y, luego, envíenos sus [comentarios](capabilities-in-technical-preview-1804.md#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Actualizaciones de software** y seleccione el nodo **Catálogos de actualizaciones de software de terceros**. Haga clic en **Agregar catálogo personalizado** en la cinta de opciones.  

2. En la página **General**, especifique los siguientes detalles:  

    - **Dirección URL de descarga**: una dirección HTTPS válida del catálogo personalizado.  

    - **Publicador**: el nombre de la organización que publica el catálogo.  

    - **Nombre**: nombre del catálogo que se va a mostrar en la consola de Configuration Manager.  

    - **Descripción**: una descripción del catálogo.  

    - **Dirección URL de soporte técnico** (opcional): dirección HTTPS válida de un sitio web para obtener ayuda sobre el catálogo.  

    - **Contacto de soporte técnico** (opcional): información de contacto para obtener ayuda sobre el catálogo.  

3. Complete el asistente. El asistente agrega el nuevo catálogo en un estado de suscripción cancelada.  

4. Suscríbase al catálogo personalizado con la acción existente **Suscribirse al catálogo**. Para más información, vea [Fase 2: Suscribirse a un catálogo de terceros y sincronizar las actualizaciones](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> No puede agregar catálogos con la misma dirección URL de descarga, y no puede editar las propiedades del catálogo. Si especifica propiedades incorrectas de un catálogo personalizado, elimine el catálogo antes de volver a agregarlo.  


#### <a name="unsubscribe-from-a-catalog"></a>Cancelar la suscripción a un catálogo
Para cancelar la suscripción a un catálogo, seleccione el catálogo deseado en la lista y haga clic en **Cancelar la suscripción del catálogo** en la cinta de opciones. Si anula la suscripción a un catálogo, se producen las siguientes acciones y comportamientos: 
- El sitio detiene la sincronización de nuevas actualizaciones 
- El sitio bloquea los certificados asociados para la firma del catálogo y el contenido de actualización. 
- Las actualizaciones existentes no se quitan, pero es posible que no pueda publicarlas o implementarlas.

#### <a name="delete-a-custom-catalog"></a>Eliminación de un catálogo personalizado
Elimine catálogos personalizados desde el mismo nodo que la consola. Seleccione un catálogo personalizado en un estado *Suscripción cancelada* y haga clic en **Eliminar catálogo personalizado**. Si ya está suscrito al catálogo, primero anule la suscripción antes de eliminarlo. No puede eliminar catálogos de asociados. Si elimina un catálogo personalizado, también lo eliminará de la lista de catálogos. Esta acción no afecta a las actualizaciones de software publicadas en el punto de actualización de software.


### <a name="known-issue"></a>Problema conocido
La acción de eliminación de los catálogos personalizados se atenúa, por lo que no puede eliminar catálogos personalizados de la consola. Para dar una solución alternativa a este problema, use la herramienta **wbemtest** en el servidor de sitio. Consulte la instancia que desea eliminar con el nombre o la dirección URL de descarga; por ejemplo: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`. En la ventana de resultados de la consulta, seleccione el objeto y haga clic en **Eliminar**.<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a> Mejoras de las características de administración en la nube

Esta versión incluye las siguientes mejoras:  

- Las siguientes características ahora admiten el uso de la nube de administración pública estadounidense de Azure:<!--511980-->  

    - Incorporación del sitio para **Administración en la nube** mediante [Servicios de Azure](../servers/deploy/configure/azure-services-wizard.md)  

    - Implementación de una instancia de [Cloud Management Gateway con Azure Resource Manager](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)  

    - Implementación de un [punto de distribución en la nube con Azure Resource Manager](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  

- Los clientes usan Windows AutoPilot para aprovisionar Windows 10 en dispositivos unidos a Azure Active Directory que están conectados a la red local. Para instalar o actualizar el cliente de Configuration Manager en estos dispositivos, ahora no es necesario un punto de distribución en la nube o punto de distribución local configurado para **permitir a los clientes conectarse de forma anónima**. En su lugar, habilite la opción del sitio para **usar certificados generados por Configuration Manager para sistemas de sitio HTTP**, que permite a un cliente unido a un dominio en la nube comunicarse con un punto de distribución local habilitado para HTTP. Para más información, vea [Comunicaciones de cliente seguras mejoradas](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a> Informe de cumplimiento de nuevas actualizaciones de software
<!--1357775-->
La visualización de informes de cumplimiento de actualizaciones de software suele incluir datos de clientes que no han contactado recientemente con el sitio. Un nuevo informe le permite filtrar los resultados de cumplimiento de un grupo específico de actualizaciones de software por clientes "correctos". Este informe muestra el estado de cumplimiento más realista de los clientes activos del entorno. 
 
Para ver el informe, vaya al área de trabajo **Supervisión**, expanda **Generación de informes**, **Informes** y **Actualizaciones de software - A Cumplimiento** y seleccione **Cumplimiento 9 - Mantenimiento general y cumplimiento**. Especifique el estado **Grupo de actualizaciones**, **Nombre de recopilación** y **Estado de cliente**.

El informe incluye las siguientes partes:
- **Clientes correctos frente a clientes totales**: en este gráfico de barras se comparan los clientes "correctos" que se han comunicado con el sitio en el período de tiempo especificado frente al número total de clientes de la colección especificada.
- **Información general de cumplimiento**: en este gráfico circular se muestra el estado de cumplimiento general de un grupo de actualizaciones de software específico de clientes activos de la colección especificada.
- **Cinco principales actualizaciones no conformes por identificador de artículo**: en este gráfico de barras se muestran las cinco principales actualizaciones de software del grupo especificado no conformes de los clientes activos de la colección especificada.
- En la parte inferior del informe se muestra una tabla con detalles adicionales, en la que se enumeran las actualizaciones de software del grupo especificado.



## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
