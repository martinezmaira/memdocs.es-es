---
title: Análisis de puntos de conexión (versión preliminar)
titleSuffix: Configuration Manager
description: Instrucciones de Análisis de puntos de conexión (versión preliminar).
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c7a99931db27b6a55c9e0722cc12c1d7a9cc9e80
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764244"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a> Análisis de puntos de conexión (versión preliminar)

> [!Note]  
> Esta información está relacionada con una característica en versión preliminar que se puede modificar sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada. 
>
> Para obtener más información sobre los cambios efectuados en Análisis de puntos de conexión, consulte [Novedades de Análisis de puntos de conexión](whats-new-endpoint-analytics.md). 
>
>Si desea unirse a la versión preliminar privada para Análisis de puntos de conexión, escriba los detalles [en este formulario](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9-ZzmlTlbJMh03eDDHtO81UOERLUkMzNFZKSlBaNFNFUVhFSlE0MzNYMS4u). Los inquilinos se lanzarán a medida que se expandan las aperturas para la versión preliminar.


## <a name="endpoint-analytics-overview"></a>Información general sobre Análisis de puntos de conexión

No es raro que los usuarios finales experimenten tiempos de arranque prolongados u otras interrupciones. Estas interrupciones se pueden deber a una combinación de:

- Hardware heredado
- Configuraciones de software que no están optimizadas para la experiencia del usuario final
- Problemas causados por actualizaciones y cambios de configuración

Estos y otros problemas de la experiencia del usuario final persisten porque el departamento de TI no tiene mucha visibilidad de la experiencia del usuario final. Por lo general, la única visibilidad de estos problemas procede de un canal de ayuda costoso y lento que habitualmente no proporciona información clara sobre lo que se debe optimizar. No es solo el soporte de TI el que se lleva el costo de estos problemas. También es costoso el tiempo que los trabajadores de la información dedican a solucionar problemas. Además, los problemas de rendimiento, confiabilidad y soporte técnico que reducen la productividad de los usuarios pueden tener un gran impacto en los resultados finales de una organización.

**Análisis de puntos de conexión** pretende mejorar la productividad de los usuarios y disminuir los costos de soporte técnico de TI al proporcionar información sobre la experiencia del usuario. La información permite que TI optimice la experiencia del usuario final con soporte técnico proactivo y detecte regresiones a la experiencia del usuario mediante la evaluación del impacto de los cambios de configuración en el usuario.

Esta versión inicial se centra en tres cosas:

- [**Software recomendado**](#bkmk_uea_rs): recomendaciones para proporcionar la mejor experiencia del usuario
- [**Scripts de corrección proactiva**](#bkmk_uea_prs): corrija los problemas de soporte técnico comunes antes de que los usuarios finales los detecten
- [**Rendimiento del inicio**](#bkmk_uea_bp): ayuda al departamento de TI a lograr que los usuarios pongan en marcha su productividad rápidamente sin retrasos por arranque e inicio de sesión largos

Esta versión es solo el principio. Lanzaremos rápidamente nuevas perspectivas para otras experiencias de usuario clave, poco después de la versión inicial. Para obtener más información sobre los cambios efectuados en Análisis de puntos de conexión, consulte [Novedades de Análisis de puntos de conexión](whats-new-endpoint-analytics.md).

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a> Introducción

Para empezar a usar Análisis de puntos de conexión, compruebe los requisitos previos y, a continuación, empiece a recopilar datos. 

### <a name="technical-prerequisites"></a>Requisitos técnicos previos

En esta versión preliminar, puede inscribir dispositivos a través de Configuration Manager o Microsoft Intune. 

Para inscribir dispositivos mediante Intune, esta versión preliminar requiere lo siguiente:
- Dispositivos inscritos en Intune que ejecutan Windows 10
- La información del rendimiento de inicio solo está disponible para los dispositivos que ejecutan la versión 1903 o posterior de Windows 10 Enterprise (las ediciones Home y Pro no son actualmente compatibles), y los dispositivos deben estar unidos a Azure AD o Azure AD híbrido. Las máquinas unidas al espacio de trabajo no se admiten actualmente.
- Conectividad de red desde dispositivos a la nube pública de Microsoft. Para obtener más información, consulte [Puntos de conexión](#bkmk_uea_endpoints).
- El [rol Administrador del servicio de Intune](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) es necesario para [iniciar la recopilación de datos](#bkmk_uea_start).
   - Al hacer clic en **Inicio**, acepta y reconoce que los datos del cliente pueden almacenarse fuera de la ubicación seleccionada al aprovisionar el inquilino de Microsoft Intune.
   - Después de hacer clic en **Iniciar** para recopilar datos, los otros roles con permiso de solo lectura podrán ver los datos.

Para inscribir dispositivos a través de Configuration Manager, esta versión preliminar requiere lo siguiente:
- Configuration Manager, versión 2002 o posterior.
- Clientes actualizados a la versión 2002 o posterior.
- [Asociación de inquilinos de Microsoft Endpoint Manager](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) habilitada con una ubicación de inquilino de Azure de Norteamérica o Europa (pronto se ampliará a otras regiones).

Tanto si los dispositivos se inscriben a través de Intune como de Configuration Manager, el [**scripting de corrección proactiva**](#bkmk_uea_prs) tiene los requisitos siguientes:
- Los dispositivos deben estar unidos a Azure AD o Azure AD híbrido y cumplir una de las condiciones siguientes:
- Un dispositivo Windows 10 Enterprise, Professional o Education administrado por Intune
- Un dispositivo [con administración conjunta](../../comanage/overview.md) que ejecuta Windows 10 Enterprise, versión 1607 o posterior, con la [Carga de trabajo de aplicaciones cliente](../../comanage/workloads.md#client-apps) apuntado a Intune.
- Un dispositivo [con administración conjunta](../../comanage/overview.md) que ejecuta Windows 10 Enterprise, versión 1903 o posterior, con la [Carga de trabajo de aplicaciones cliente](../../comanage/workloads.md#client-apps) apuntado a Configuration Manager.

### <a name="licensing-prerequisites"></a>Requisitos previos de las licencias

Análisis de puntos de conexión se incluye en los siguientes planes: 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) o una versión posterior
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) o una versión posterior

Las correcciones proactivas también requieren una de las siguientes licencias para los dispositivos administrados:
- Windows 10 Enterprise E3 o E5 (incluido en Microsoft 365 F3, E3 o E5)
- Windows 10 Education A3 o A5 (incluido en Microsoft 365 A3 o A5)
- Acceso a Windows Virtual Desktop E3 o E5

### <a name="permissions"></a>Permisos

#### <a name="endpoint-analytics-permissions"></a>Permisos de análisis de puntos de conexión

Se usan los permisos siguientes para el análisis de puntos de conexión:
- **Leer** en la categoría **Configuraciones de dispositivo**.
- **Leer** en la categoría **Organización**. <!--temporary for pp-->
- Permisos adecuados para el rol del usuario en la categoría **Análisis de puntos de conexión**.

Un usuario de solo lectura solo necesitará el permiso **Leer** en las categorías **Configuraciones de dispositivo** y **Análisis de punto de conexión**. Normalmente, un administrador de Intune necesitará todos los permisos.

#### <a name="proactive-remediations-permissions"></a>Permisos de correcciones proactivas

En el caso de las correcciones proactivas, el usuario necesita permisos adecuados para su rol en la categoría **Configuraciones de dispositivo**.  Los permisos de la categoría **Análisis de puntos de conexión** no son necesarios si el usuario solo usa correcciones proactivas.

Se requiere un [Administrador del servicio Intune](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions) para confirmar los requisitos de licencia antes de usar las correcciones proactivas por primera vez.

## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a> Inicio de la recopilación de datos
- Si solo va a inscribir dispositivos administrados por Intune, vaya la sección [Incorporación al portal Análisis de puntos de conexión](#bkmk_uea_onboard).

- Si va a inscribir dispositivos administrados por Configuration Manager, tendrá que realizar los pasos siguientes:
   - [Habilitación de la recopilación de datos de Análisis de puntos de conexión en Configuration Manager](#bkmk_uea_cm_enroll)
   - [Habilitación de la carga de datos en Configuration Manager](#bkmk_uea_cm_upload)
   - [Incorporación al portal Análisis de puntos de conexión](#bkmk_uea_onboard)  

### <a name="enroll-devices-managed-by-configuration-manager"></a><a name="bkmk_uea_cm_enroll"></a> Inscripción de dispositivos administrados por Configuration Manager
<!--6051638, 5924760-->
Antes de inscribir dispositivos de Configuration Manager, compruebe los [requisitos previos](#bkmk_uea_prereq), incluida la habilitación de [Asociación de inquilinos de Microsoft Endpoint Manager](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions). 

#### <a name="enable-endpoint-analytics-data-collection-in-configuration-manager"></a><a name="bkmk_uea_cm_enable"></a> Habilitación de la recopilación de datos de Análisis de puntos de conexión en Configuration Manager

1. En la consola de Configuration Manager, vaya a **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.
1. Haga clic con el botón derecho, seleccione **Propiedades** y elija la opción **Agente de equipo**.
1. Establezca **Habilitar recopilación de datos del análisis de puntos de conexión** en **Sí**.
   > [!Important] 
   > Si tiene una opción de agente de cliente personalizada que se ha implementado en los dispositivos, tendrá que actualizar la opción **Habilitar recopilación de datos del análisis de puntos de conexión** en la opción personalizada y volver a implementarla en sus equipos para que surta efecto.

#### <a name="enable-data-upload-in-configuration-manager"></a><a name="bkmk_uea_cm_upload"></a> Habilitación de la carga de datos en Configuration Manager

1. En la consola de Configuration Manager, vaya a **Administración** > **Cloud Services** > **Administración conjunta**.
1. Seleccione **CoMgmtSettingsProd** y haga clic en **Propiedades**.
1. En la pestaña **Configure upload** (Configurar carga), active la opción **Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager** (Habilitar Análisis de conexión para dispositivos cargados en Microsoft Endpoint Manager).

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Habilitación de Análisis de puntos de conexión para los dispositivos cargados en Microsoft Endpoint Manager" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="onboard-in-the-endpoint-analytics-portal"></a><a name="bkmk_uea_onboard"></a> Incorporación al portal Análisis de puntos de conexión
La incorporación al portal Análisis de puntos de conexión se requiere para los dispositivos administrados de Configuration Manager y de Intune.

1. Vaya a `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. Haga clic en **Iniciar**. Se asignará automáticamente un perfil de configuración para recopilar datos de rendimiento sobre el arranque en todos los dispositivos elegibles. Puede [cambiar los dispositivos asignados](#bkmk_uea_profile) más adelante. Los datos de rendimiento de inicio pueden tardar hasta 24 horas en rellenarse desde los dispositivos inscritos en Intune después de que estos se reinicien.
   - Para obtener más información sobre problemas comunes, consulte [Solución de problemas de rendimiento de inicio en la inscripción de dispositivos](#bkmk_uea_enrollment_tshooter).

## <a name="overview-page"></a>Página de información general

Una vez que los datos estén listos, verá cierta información en la página **Información general**, que se explica con más detalles a continuación:

- La **Puntuación de la experiencia del usuario** es un promedio ponderador 50/50 del **Software recomendado** y de las **Puntuaciones de rendimiento de inicio**. Con el tiempo, vamos a expandir el conjunto de subpuntuaciones.

- Puede establecer una línea de base para comparar su puntuación actual con otras puntuaciones.
  - Tal como se describe en la sección de [línea de base](#bkmk_uea_baselines), hay una línea de base integrada para la *Mediana comercial* ta fin de ver cómo se compara con una empresa típica. Puede crear líneas de base nuevas en función de las métricas actuales para poder hacer un seguimiento del progreso o ver las regresiones a lo largo del tiempo.
   - Los marcadores de línea de base se muestran para la puntuación general y las subpuntuaciones. Si alguna de las puntuaciones se revirtió por más del umbral configurable de la línea de base seleccionada, la puntuación se mostrará en rojo y la puntuación de nivel superior se marcará como que necesita atención.
  - Un estado de **datos insuficientes** significa que no tiene dispositivos suficientes que informen para proporcionar una puntuación significativa. Actualmente se requieren al menos cinco dispositivos.

- Los **Filtros** le permitirán ver su puntuación en un subconjunto de dispositivos o usuarios. Sin embargo, la funcionalidad de filtro no está habilitada en esta versión preliminar.

- **Conclusiones y recomendaciones** es una lista ordenada por prioridad para mejorar la puntuación. Esta lista se filtra según el contexto del subnodo cuando navega a **Procedimientos recomendados** o **Software recomendado**.

[![Página de información general de Análisis de puntos de conexión](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a> Software recomendado

> [!Important]  
> El análisis de puntos de conexión calcula la puntuación de **adopción de software** para todos los dispositivos administrados por Intune, independientemente de si se han inscrito en el análisis de puntos de conexión o no.

Se sabe que cierto software mejora la experiencia del usuario final, independientemente de las métricas de estado de nivel inferior. Por ejemplo, Windows 10 tiene una puntuación Net Promoter Score mucho mayor que Windows 7. La puntuación de **Adopción de software** es un número entre 0 y 100 que representa un promedio ponderado del porcentaje de dispositivos que han implementado varios software recomendados. La ponderación actual es superior para Windows que para las otras métricas, ya que los usuarios interactúan con ellas con más frecuencia. Las métricas se describen a continuación: 

[![Página Software recomendado de Análisis de puntos de conexión](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a> Windows 10

Windows 10 ofrece una mejor experiencia del usuario que las versiones anteriores de Windows. Vea las [notas del producto de TEI](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf) para obtener más información.

Esta métrica mide el porcentaje de dispositivos en Windows 10 con respecto a una versión anterior de Windows.

La acción correctiva recomendada para mover dispositivos de versiones anteriores de Windows consiste en crear un plan de implementación mediante el [Análisis de escritorio](../../desktop-analytics/overview.md).

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a> Autopilot

Microsoft Autopilot proporciona una experiencia de aprovisionamiento inicial más simple para equipos Windows 10 que la experiencia nativa al reducir el número de pantallas de la Configuración rápida (OOBE) y proporcionar valores predeterminados a fin de garantizar que los dispositivos de los empleados se aprovisionan correctamente de fábrica o al restablecer.

Esta métrica mide el porcentaje de dispositivos Windows 10 registrados en Autopilot.

La acción correctiva recomendada consiste en registrar los dispositivos existentes en Autopilot mediante [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) proporciona a los usuarios numerosas ventajas de productividad que incluyen inicio de sesión único en el dispositivo en aplicaciones y servicios, inicio de sesión de Windows Hello, recuperación autoservicio de BitLocker e itinerancia de datos corporativa.

Esta métrica mide el porcentaje de dispositivos inscritos en Azure AD.

Los dispositivos administrados por Microsoft Intune ya están inscritos en Azure AD. La acción correctiva recomendada para los dispositivos administrados por Configuration Manager consiste en [inscribirlos en Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) o [administrarlos de manera conjunta](../../comanage/overview.md). La administración conjunta de dispositivos también mejora la puntuación de administración en la nube.

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a> Administración en la nube

Microsoft Intune proporciona a los usuarios varias ventajas de productividad que incluyen la habilitación de acceso a los recursos corporativos aunque estén fuera de la red corporativa y la eliminación de la necesidad de sobrecarga de rendimiento de directiva de grupo, lo que da lugar a una mejor experiencia del usuario final. Esta métrica mide el porcentaje de equipos inscritos en Microsoft Intune. Vea cómo [Microsoft está habilitando esta característica para los empleados](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

La acción correctiva recomendada para los dispositivos administrados por Configuration Manager que todavía no están inscritos en Intune consiste en [administrarlos de manera conjunta](../../comanage/overview.md).

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a> Sin mediana comercial

Actualmente, la línea de base integrada de la **Mediana comercial** no tiene métricas para las subpuntuaciones que aparecen en las secciones anteriores.

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a> Rendimiento de inicio

> [!NOTE]
> Si no ve los datos de rendimiento de inicio de todos los dispositivos, consulte [Solución de problemas con la inscripción de dispositivos Windows en Microsoft Intune](#bkmk_uea_enrollment_tshooter).

La puntuación de rendimiento de inicio ayuda al departamento de TI a lograr que los usuarios pongan en marcha su productividad rápidamente sin retrasos por arranque e inicio de sesión largos. La **Puntuación de inicio** es un número entre 0 y 100. Esta puntuación es un promedio ponderado de **Puntuación de arranque** y la puntuación de **inicio de sesión**, que se calcula de la manera siguiente:

- **Puntuación de arranque**: se basa en el tiempo que va desde el encendido al inicio de sesión. Observamos la hora del último arranque de cada dispositivo, excluida la fase de actualización, y se le asigna una puntuación de 0 (insuficiente) a 100 (excepcional). Estas puntuaciones se calculan para proporcionar una puntuación general del arranque del inquilino.
- **Puntuación de inicio de sesión**: se basa en el tiempo transcurrido desde que se han introducido las credenciales hasta que el usuario puede tener acceso a un escritorio con capacidad de respuesta (lo que significa que el escritorio se ha representado y el uso de CPU ha descendido por debajo del 50 % durante al menos 2 segundos). Observamos la hora del último inicio de sesión en cada dispositivo, excluidos los primeros inicios de sesión o los inicios de sesión inmediatamente después de una actualización de características, y se le asigna una puntuación de 0 (insuficiente) a 100 (excepcional). Estas puntuaciones se calculan para proporcionar una puntuación general del arranque del inquilino.

[![Página Rendimiento de inicio de Análisis de puntos de conexión](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>Información detallada

La página **Rendimiento de inicio** también proporciona una lista ordenada por prioridad de las **Conclusiones y recomendaciones** que vamos a describir en las secciones siguientes:

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a> Unidades de disco duro

El rendimiento de inicio brinda información sobre el número de dispositivos en los que la unidad de arranque es un disco duro. Por lo general, las unidades de disco duro generan un tiempo de arranque tres a cuatro veces mayor que las unidades de estado sólido. También se informa la mejora esperada en el rendimiento de inicio que se obtendría al cambiar a unidades de estado sólido.

Haga clic para ver la lista de dispositivos con unidades de disco duro. La acción recomendada es actualizar estos dispositivos a unidades de estado sólido.

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a> Directiva de grupo

El rendimiento de inicio proporciona información sobre el número de dispositivos con retrasos en los tiempos de arranque e inicio de sesión causados por la directiva de grupo. Al hacer clic, será dirigido a la vista de dispositivos. La vista se ordena por la hora de la directiva de grupo, por lo que puede ver los dispositivos afectados para solucionar el problema.

Si hace clic en un dispositivo determinado, puede ver su historial de arranque e inicio de sesión. El historial lo ayuda a determinar si el problema se debe a una regresión y cuándo posiblemente se produjo.

Aunque hay muchos artículos sobre cómo optimizar el rendimiento de las directivas de grupo, puede optar por migrar a la administración en la nube en su lugar. La migración a la administración en la nube permite usar [líneas de base de seguridad de Intune](https://docs.microsoft.com/intune/protect/security-baselines) y la herramienta Análisis de directivas que pronto se publicará.

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a> Tiempos de arranque e inicio de sesión lentos

El rendimiento de inicio proporciona información sobre el número de dispositivos con tiempos de arranque o inicio de sesión lentos. Una puntuación de arranque o de inicio de sesión de "0" significa que es lento. Al hacer clic, será dirigido a la vista de dispositivos. Los dispositivos se ordenan por hora de arranque del núcleo o por hora de inicio de sesión de mismo, de modo que puede ver los dispositivos afectados para solucionar el problema.

Si hace clic en un dispositivo determinado, puede ver su historial de arranque e inicio de sesión. El historial lo ayuda a determinar si el problema se debió a una regresión y cuándo posiblemente se produjo.

### <a name="reporting-tabs"></a>Pestaña informes

La página **Rendimiento de inicio** tiene pestañas de informes que brindan información, como las siguientes:
1. **Rendimiento del modelo**. Esta pestaña permite ver el rendimiento de arranque e inicio de sesión por modelo de dispositivo, lo que puede ayudarle a identificar si los problemas de rendimiento son exclusivos de determinados modelos.
1. **Rendimiento del dispositivo**. Esta pestaña proporciona métricas de arranque e inicio de sesión para todos los dispositivos. Puede ordenar por una métrica concreta (por ejemplo, la hora de inicio de sesión de la directiva de grupo) para ver los dispositivos que tienen las peores puntuaciones de esa métrica para ayudarle en la solución de problemas. También puede buscar un dispositivo por su nombre. Si hace clic en un dispositivo, puede ver su historial de inicio e inicio de sesión, lo que puede ayudarle a identificar si se ha producido una regresión reciente.
1. **Procesos de inicio**. Los procesos de inicio pueden afectar negativamente a la experiencia del usuario al aumentar el período de tiempo que los usuarios deben esperar a que el escritorio responda. Esta pestaña (si está visible; solo la hemos puesto a disposición de algunos usuarios porque nos encontramos aún en el proceso de desarrollo de esta característica) le mostrará qué procesos están afectando a la fase del "tiempo hasta que el escritorio responde" en el inicio de sesión; esto es, mantener la CPU por encima del 50 % una vez representado el escritorio. En la tabla solo se muestran los procesos que afectan a un mínimo de 10 dispositivos del inquilino.  

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a> Correcciones proactivas

Las correcciones proactivas son paquetes de scripts que pueden detectar y corregir problemas de soporte técnico comunes en el dispositivo de un usuario antes de que se enteren siquiera de que hay un problema. Estas correcciones pueden ayudar a disminuir las llamadas al soporte técnico. Puede crear su propio paquete de scripts o implementar uno de los paquetes de scripts que hemos escrito y usado en nuestro entorno para disminuir las incidencias de soporte técnico.

Cada paquete de scripts consta de un script de detección, un script de corrección y metadatos. A través de Intune, podrá implementar estos paquetes de scripts y ver informes sobre su eficacia. Estamos desarrollando activamente nuevos paquetes de scripts y nos gustaría conocer sus experiencias con estos scripts. Póngase en contacto con su persona de contacto de Análisis de puntos de conexión (versión preliminar) si tiene algún comentario sobre los paquetes de scripts.

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a> Obtención de los scripts de detección y corrección

1. Copie los scripts que aparecen en la parte inferior de este artículo en la sección [Scripts de PowerShell](#bkmk_uea_ps_scripts).
    - Los archivos de script cuyos nombres empiezan por `det` son scripts de detección. Los scripts de corrección empiezan por `rem`.
    - Para una descripción de los scripts, consulte las [Descripciones de los scripts](#bkmk_uea_scripts).
1. Guarde cada script con el nombre proporcionado. El nombre también se encuentra en los comentarios que están al principio de cada script.
    - Puede usar un nombre de script diferente, pero no coincidirá con el nombre que aparece en la sección [Descripciones de los scripts](#bkmk_uea_scripts).


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a> Implementación y supervisión de scripts
El servicio **Microsoft Intune Management Extension** obtiene los scripts de Intune y los ejecuta. Los scripts se vuelven a ejecutar cada 24 horas. Para implementar y supervisar los scripts, siga las instrucciones siguientes:

1. Vaya al nodo **Correcciones proactivas** en la consola.
1. Haga clic en el botón **Crear paquete de script** para crear un paquete de scripts.
     [![Página Correcciones proactivas de Análisis de puntos de conexión. Seleccione el vínculo Crear.](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. En el paso **Conceptos básicos**, asígnele un **Nombre** al paquete de scripts y, si quiere, una **descripción**. Es posible editar el campo **Editor**, pero el valor predeterminado es su nombre de inquilino. No se puede editar la **Versión**. 
1. En el paso **Configuración**, copie el texto de los scripts que descargó en los campos **Script de detección** y **Script de corrección**. 
   - Es necesario que el script de detección y corrección correspondiente esté en el mismo paquete. Por ejemplo, el script de detección `Detect_stale_Group_Policies.ps1` se corresponde con el script de remediación `Remediate_stale_GroupPolicies.ps1`.
       [![Página Configuración de los scripts de correcciones proactivas de Análisis de puntos de conexión.](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. Complete las opciones de la página **Configuración** con estas configuraciones recomendadas:
   - **Ejecutar este script con las credenciales de inicio de sesión**: esta configuración depende del script. Para más información, consulte las [Descripciones de los scripts](#bkmk_uea_scripts).
   - **Exigir comprobación de firma del script**: No
   - **Ejecutar script en PowerShell de 64 bits**: No
1. Haga clic en **Siguiente** y asigne cualquier **etiqueta de ámbito** que necesite.
1. En el paso **Asignaciones**, seleccione los grupos de dispositivos en los que quiere implementar el paquete de scripts.
1. Complete el paso **Revisión y creación** de la implementación.
1. En **Informes** > **Análisis de puntos de conexión - Correcciones proactivas** puede ver información general sobre el estado de detección y corrección.
       [![Informe de correcciones proactivas de Análisis de puntos de conexión, página de información general.](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. Haga clic en **Estado del dispositivo** para obtener los detalles de estado de cada dispositivo de la implementación.
       [![Estado del dispositivo de Correcciones proactivas de Análisis de puntos de conexión.](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a> Configuración de Análisis de puntos de conexión

En la página de configuración, puede seleccionar **General** o **Línea de base**. A continuación se describe cada una de estas opciones:

### <a name="general"></a><a name="bkmk_uea_gen"></a> General

La página **General** en **Configuración** permite ver si se ha habilitado la recopilación de datos de rendimiento de inicio de Intune. Se habilita automáticamente para todos los dispositivos de manera predeterminada al hacer clic en **Iniciar** para habilitar el análisis de la experiencia del usuario. Tiene la opción de ir al nodo de la directiva de recopilación de datos de Intune para cambiar el conjunto de dispositivos en los que se recopilan los registros de arranque e inicio de sesión.


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a> Directiva de recopilación de datos de Intune

Para asignar este valor a un subconjunto de dispositivos, [cree un perfil](/intune/configuration/device-profile-create#create-the-profile) con la información siguiente: 

  - **Nombre**: escriba un nombre descriptivo para el perfil, como **Directiva de recopilación de datos de Intune**.
   
  - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.
    
  - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
   
  - **Tipo de perfil**: seleccione **Seguimiento de estado de Windows**.
   
  - Ajuste la **configuración**:
   
       - **Seguimiento de estado**: seleccione **Habilitar** para recopilar la información sobre los eventos de los dispositivos Windows 10.
    
    - **Ámbito**: Seleccione **Rendimiento de arranque**. 

  - Use [etiquetas de ámbito](/intune/configuration/device-profile-create#scope-tags) y [reglas de aplicabilidad](/intune/configuration/device-profile-create#applicability-rules) para filtrar el perfil a grupos o dispositivos de TI en un grupo que cumpla un criterio concreto.

> [!NOTE]
> Hay un marcador de posición para las instrucciones sobre cómo configurar el conector de datos de Configuration Manager. Sin embargo, esta funcionalidad no se ha implementado en esta versión preliminar privada inicial.

  [![Página Configuración general de Análisis de puntos de conexión](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a> Administración de línea de base

Puede establecer una línea de base para comparar sus puntuaciones y subpuntuaciones actuales.

1. Hay una línea de base integrada para la **Mediana comercial**, que permite comparar sus puntuaciones con una empresa típica.
1. Puede crear líneas de base nuevas en función de las métricas actuales para hacer un seguimiento del progreso o ver las regresiones a lo largo del tiempo. Haga clic en el botón **Crear nuevo** y asigne un nombre a la línea de base nueva. Se recomienda un nombre que incluya la fecha, para que sea más fácil seleccionarla en la lista desplegable de las páginas de informes.
1. Hay un límite de 100 líneas de base por inquilino. Puede eliminar las líneas de base antiguas que ya no sean necesarias.
1. Las métricas actuales se marcarán en rojo y se mostrarán como con regresión si están por debajo de la línea de base actual en los informes. Dado que es absolutamente normal que las métricas fluctúen de un día a otro, puede establecer un umbral de regresión con un valor predeterminado de 10 %. Con este umbral, las métricas solo se marcan como con regresión si se revirtieron en más del 10 %.

   [![Página de configuración de línea de base de Análisis de puntos de conexión](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a> Solución de problemas

Las secciones siguientes le pueden ayudar a solucionar problemas que puedan surgir.

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a> Solución de problemas de rendimiento de inicio en la inscripción de dispositivos

Si en la página de información general aparece una puntuación de rendimiento de inicio cero acompañada de un banner que muestra que está esperando datos, o si en la pestaña Rendimiento del dispositivo del rendimiento de inicio se muestran menos dispositivos de los esperados, puede seguir unos pasos para solucionar el problema.

En primer lugar, se muestra a continuación un resumen rápido de las limitaciones de la recopilación de datos de rendimiento de inicio:
1. Los dispositivos deben ejecutar Windows 10, versión 1903 o posterior.
2. Los dispositivos deben estar unidos a Azure AD. Actualmente no se admiten dispositivos unidos al área de trabajo, aunque estamos investigando activamente la viabilidad de agregar esta funcionalidad a Windows.
3. Los dispositivos deben contar con la edición Windows 10 Enterprise. Windows 10 Home y Professional no se admiten actualmente, aunque estamos investigando activamente la viabilidad de agregar esta funcionalidad a Windows.

Tenga en cuenta que estas cuestiones no se aplicarán a los datos procedentes del próximo conector de Configuration Manager; podrá recopilar datos de cualquier equipo cliente de Configuration Manager, independientemente de la configuración de la versión, la edición o el directorio.

En segundo lugar, a continuación se muestra una lista de comprobación rápida para solucionar problemas:
1. Asegúrese de tener el perfil de supervisión de estado de Windows apuntando a todos los dispositivos de los que quiera obtener datos de rendimiento. Encontrará un vínculo a este perfil desde la página de configuración de Análisis de puntos de conexión, o bien puede acceder a él igual que con cualquier otro perfil de Intune. Fíjese en la pestaña Asignación para asegurarse de que está asignado al conjunto de dispositivos previsto. 
1. Observe qué dispositivos se han configurado correctamente para la recopilación de datos. También puede ver esta información en la página de información general de perfiles.  
   - Hay un problema conocido por el que los clientes pueden ver errores de asignación de perfiles, donde los dispositivos afectados muestran un código de error de `-2016281112 (Remediation failed)`. Estamos investigando este problema de forma activa.
1. Los dispositivos que se hayan configurado correctamente para la recopilación de datos deben reiniciarse después de que se haya habilitado la recopilación de datos. Después, deberá esperar hasta 24 horas para que el dispositivo aparezca en la pestaña Rendimiento del dispositivo.
1. Si el dispositivo se ha configurado correctamente para la recopilación de datos, se ha reiniciado posteriormente y, una vez transcurridas 24 horas, sigue sin verlo, es posible que el dispositivo no pueda acceder a nuestros puntos de conexión de la colección. Este problema puede producirse si su empresa usa un servidor proxy y los puntos de conexión no se han habilitado en el proxy. Para obtener más información, consulte [Solución de problemas de puntos de conexión](#bkmk_uea_endpoints).


### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a> Puntos de conexión

Para inscribir dispositivos en Análisis de puntos de conexión, se deben enviar los datos funcionales necesarios a Microsoft. Si su entorno usa un servidor proxy, utilice esta información para configurar el proxy.

Para habilitar el uso compartido de datos funcionales, configure el servidor proxy para permitir los siguientes puntos de conexión:

> [!Important]  
> De cara a la privacidad y la integridad de los datos, Windows comprueba si hay un certificado SSL de Microsoft (asignación de certificados) al comunicarse con los puntos de conexión de uso compartido de datos funcionales necesarios. No es posible la interceptación y la inspección de SSL. Para usar Análisis de puntos de conexión, excluya estos puntos de conexión de la inspección de SSL.<!-- BUG 4647542 -->

| Punto de conexión  | Función  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Se usan para enviar los [datos funcionales necesarios](#bkmk_uea_datacollection) al punto de conexión de recopilación de datos de Intune. |
| `https://graph.windows.net` | Se usa para recuperar automáticamente la configuración al asociar la jerarquía a Análisis de puntos de conexión (en el rol de servidor de Configuration Manager). Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Se usa para sincronizar la recopilación de dispositivos y los dispositivos con Análisis de puntos de conexión (solo en el rol del servidor de Configuration Manager). Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |


### <a name="proxy-server-authentication"></a>Autenticación del servidor proxy

Si en la organización se usa la autenticación de servidor proxy para el acceso a Internet, asegúrese de que no bloquee los datos debido a la autenticación. Si el proxy no permite que los dispositivos envíen estos datos, no se mostrarán en Análisis de escritorio.

#### <a name="bypass-recommended"></a>Desviar (recomendado)

Configure los servidores proxy para que no exijan la autenticación proxy del tráfico que entra en los puntos de conexión de uso compartido de datos. Esta opción es la solución más completa. Funciona en todas las versiones de Windows 10.  

#### <a name="user-proxy-authentication"></a>Autenticación proxy del usuario

Configure los dispositivos para que usen el contexto del usuario con sesión iniciada para la autenticación proxy. Este método requiere las siguientes configuraciones:

- Los dispositivos tienen la actualización de calidad actual para una versión compatible de Windows.

- Configure el proxy de nivel de usuario (proxy de WinINET) en **Configuración de proxy** en el grupo Red e Internet de la configuración de Windows. También puede usar el panel de control heredado de Opciones de Internet.

- Asegúrese de que los usuarios tengan permiso de proxy para comunicarse con los puntos de conexión de uso compartido de datos. Esta opción requiere que los dispositivos tengan usuarios de consola con permisos de proxy, de forma que no puede usar este método con dispositivos sin periféricos.

> [!IMPORTANT]
> El enfoque de autenticación proxy del usuario no es compatible con el uso de Azure Advanced Threat Protection de Microsoft Defender. Este comportamiento se debe a que esta autenticación se basa en la clave del Registro **DisableEnterpriseAuthProxy** establecida en `0`, mientras que ATP de Microsoft Defender requiere que se establezca en `1`. Para obtener más información, consulte [Configurar el proxy del equipo y la configuración de conectividad de Internet en ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

#### <a name="device-proxy-authentication"></a>Autenticación proxy del dispositivo

Este enfoque admite los escenarios siguientes:

- Dispositivos sin periféricos, donde ningún usuario inicia sesión o los usuarios del dispositivo no tienen acceso a Internet

- Servidores proxy autenticados que no usan la Autenticación integrada de Windows

- Uso conjunto con Protección contra amenazas avanzada de Microsoft Defender

Este enfoque es el más complejo porque requiere las siguientes configuraciones:

- Asegúrese de que los dispositivos puedan comunicarse con al servidor proxy a través de WinHTTP en el contexto del sistema local. Use una de las siguientes opciones para configurar este comportamiento:

  - Línea de comandos `netsh winhttp set proxy`

  - Protocolo de detección automática de proxy web (WPAD)

  - Proxy transparente

  - Configure el proxy WinINET para todo el dispositivo mediante la siguiente configuración de directiva de grupo: **Configuración de proxy por equipo y no por usuario** (ProxySettingsPerUser = `1`)

  - Conexión enrutada o que use la traducción de direcciones de red (NAT)

- Configure los servidores proxy para permitir que las cuentas de equipo de Active Directory accedan a los puntos de conexión de datos. Esta configuración requiere que los servidores proxy admitan la autenticación integrada de Windows.  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a> Preguntas más frecuentes

### <a name="will-my-endpoint-analytics-data-migrate-if-i-move-my-intune-tenant-to-a-different-tenant-location"></a>¿Se migrarán mis datos de Análisis de punto de conexión si se mueve mi inquilino de Intune a otra ubicación de inquilino?

Si migra el inquilino de Intune a una ubicación diferente, se perderán todos los datos de la solución de Análisis de punto de conexión en el momento de la migración. Dado que los puntos de conexión informan continuamente al Análisis de puntos de conexión, todos los eventos que se producen después de la migración se cargan automáticamente en la nueva ubicación de inquilinos y los informes empiezan a rellenarse, suponiendo que los dispositivos permanecen inscritos correctamente. 

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>¿Por qué los scripts salen con un código de 1?

Los scripts salen con un código de 1 para indicar a Intune que se debe realizar una corrección. En este caso, salir de un script de detección con 1 significa que se necesita una corrección. Muchos paquetes de scripts que se ejecutan únicamente en CM pueden mostrar que son compatibles, pero salen con un código de 1. En el caso de estos scripts, salir con un código de 1 no es algo alarmante, pero puede que quiera comprobar que el dispositivo se corrija correctamente.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>¿Por qué el script Actualizar directivas de grupo obsoletas se devuelve con el error 0x87D00321?

0x87D00321 es un error de tiempo de espera de la ejecución del script. Este error suele producirse con equipos que están conectados de manera remota. Una posible mitigación podría ser implementar solo en una recopilación dinámica de máquinas con conectividad de red interna.

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a> Descripciones de los scripts

En esta tabla se muestran los nombres de los scripts, sus descripciones, detecciones, correcciones y los elementos configurables. Los archivos de script cuyos nombres empiezan por `Detect` son scripts de detección. Los scripts de corrección empiezan por `Remediate`. Estos scripts se pueden copiar en la sección siguiente de este artículo.

|Nombre de script|Descripción|
|---|---|
|**Actualizar directivas de grupo obsoletas** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Detecta si la última actualización de las directivas de grupo ocurrió hace más de `7 days`.  </br>Para personalizar el umbral de 7 días, cambie el valor de `$numDays` en el script de detección. </br></br>Ejecuta `gpupdate /target:computer /force` y `gpupdate /target:user /force` para realizar la corrección.  </br> </br>Puede ayudar a disminuir las llamadas de soporte técnico relacionadas con la conectividad de red cuando los certificados y las configuraciones se entregan a través de una directiva de grupo. </br> </br> **Ejecutar el script con las credenciales de inicio de sesión**: Sí|
|**Reiniciar el servicio Hacer clic y ejecutar de Office** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| Detecta si el servicio Hacer clic y ejecutar está configurado para iniciarse automáticamente y si el servicio está detenido. </br> </br> Para realizar la corrección, establece que el servicio se inicie automáticamente e inicia el servicio si está detenido. </br></br> Ayuda a solucionar los problemas en los que no se iniciará Aplicaciones de Microsoft 365 para empresas de Win32 porque se detiene el servicio Hacer clic y ejecutar. </br> </br> **Ejecutar el script con las credenciales de inicio de sesión**: No|
|**Comprobación de los certificados de red** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Detecta los certificados emitidos por una entidad de certificación en el almacén personal de la máquina o del usuario que han expirado o que están a punto de expirar. </br> Para especificar la entidad de certificación, cambie el valor de `$strMatch` en el script de detección. Especifique 0 para `$expiringDays` para buscar certificados expirados, o bien especifique otro número de días para buscar certificados que estén por expirar.  </br></br>Realiza la corrección mediante la emisión de una notificación del sistema al usuario. </br> Especifique los valores de `$Title` y `$msgText` con el texto y el título del mensaje que quiere que vean los usuarios. </br> </br> Notifica a los usuarios los certificados expirados que posiblemente se deban renovar. </br> </br> **Ejecutar el script con las credenciales de inicio de sesión**: No|
|**Borrar certificados obsoletos** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Detecta los certificados expirados emitidos por una entidad de certificación en el almacén personal del usuario actual. </br> Para especificar la entidad de certificación, cambie el valor de `$certCN` en el script de detección. </br> </br> Para realizar la corrección, elimine los certificados expirados que emite una entidad de certificación del almacén personal del usuario actual. </br> Para especificar la entidad de certificación, cambie el valor de `$certCN` en el script de corrección. </br> </br> Busca y elimina los certificados expirados que emite una entidad de certificación del almacén personal del usuario actual. </br> </br> **Ejecutar el script con las credenciales de inicio de sesión**: Sí|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a> Scripts de PowerShell

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a> Privacidad de datos de Análisis de puntos de conexión

### <a name="data-flow"></a>Flujo de datos

En la ilustración siguiente se muestra cómo los datos funcionales necesarios fluyen desde dispositivos individuales a través de los servicios de datos, el almacenamiento transitorio y al inquilino. Los datos fluyen a través de las canalizaciones empresariales existentes sin depender de los datos de diagnóstico de Windows.

[![Diagrama de flujo de datos de experiencia del usuario](media/dataflow.png)](media/dataflow.png#lightbox)

1. Configure la directiva **Recolección de datos de Intune** para los dispositivos inscritos. De forma predeterminada, esta directiva se asigna a "Todos los dispositivos" al **iniciar** Análisis de puntos de conexión. Sin embargo, puede [cambiar esta asignación](#bkmk_uea_set) en cualquier momento a un subconjunto de dispositivos, o bien a ningún dispositivo.

2. Los dispositivos envían los datos funcionales necesarios.

    - En el caso de los dispositivos de Intune con la directiva asignada, los datos se envían desde la extensión de administración de Intune. Para obtener más información, consulte los [requisitos](#bkmk_uea_prereq).
    - En el caso de los dispositivos administrados de Configuration Manager, los datos también pueden fluir a Microsoft Endpoint Management mediante el conector de Configuration Manager. El conector de ConfigMgr está conectado a la nube. Solo requiere conexión a un inquilino de Intune, no activar la administración conjunta.

> [!Note]  
> Los datos necesarios para calcular la puntuación de inicio de un dispositivo se generan durante el arranque. En función de la configuración de energía y del comportamiento del usuario, es posible que pasen semanas antes de que se asigne a un dispositivo la directiva para mostrar la puntuación de inicio en la consola de administración.  

3. El servicio Administrador de puntos de conexión de Microsoft procesa los datos de cada dispositivo y publica los resultados para dispositivos individuales y datos agregados de una organización en la consola de administración mediante las API de Microsoft Graph.

El tiempo de latencia medio de extremo a extremo es de unas 12 horas y se canaliza con el tiempo que se tarda a realizar el procesamiento diario. El resto de las partes del flujo de datos es casi en tiempo real.

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a> Recopilación de datos

En estos momentos, la funcionalidad básica de Análisis de puntos de conexión recopila información asociada con los registros de rendimiento del arranque correspondientes a las categorías [identificados](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data) y [formato anónimo](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data). Los datos recopilados variarán como sea necesario a medida que agregamos funcionalidades adicionales. Principales puntos de datos que se recopilan actualmente:

#### <a name="identified-data"></a>Datos identificados

- Información de inventario de hardware
  - **make:** Fabricante del dispositivo
  - **model:** Modelo del dispositivo
  - **deviceClass:** Clasificación del dispositivo. Por ejemplo, Escritorio, Servidor o Móvil.
  - **Country:** Configuración regional del dispositivo.
- Inventario de aplicaciones, como
  - **name:** Windows
  - **ver:** Versión del sistema operativo actual.
  
#### <a name="pseudonymized-data"></a>Datos de formato anónimo

- Datos de uso, rendimiento y diagnóstico ligados a un usuario o dispositivo
  - **logOnId**
  - **bootId:** Identificador de arranque del sistema.
  - **coreBootTimeInMilliseconds:** Tiempo que tarda el núcleo en arrancar.
  - **totalBootTimeInMilliseconds:** Tiempo total de arranque.
  - **updateTimeInMilliseconds:** Tiempo que tardan en completarse las actualizaciones del sistema operativo.
  - **gpLogonDurationInMilliseconds**: Tiempo que tardan en procesarse las directivas de grupo.
  - **desktopShownDurationInMilliseconds:** Tiempo que tarda el escritorio (explorer.exe) en cargarse.
  - **desktopUsableDurationInMilliseconds:** Tiempo que tarda el escritorio (explorer.exe) en poder usarse.
  - **topProcesses:** Lista de procesos cargados durante el arranque, con nombre, estadísticas de uso de CPU y detalles de la aplicación (nombre, publicador y versión). Por ejemplo *{\"ProcessName\":\"svchost\",\"CpuUsage\":43,\"ProcessFullPath\":\"C:\\\\Windows\\\\System32\\\\svchost.exe\",\"ProductName\":\"Sistema operativo Microsoft&reg; Windows&reg; \",\"Publisher\":\"Microsoft Corporation\",\"ProductVersion\":\"10.0.18362.1\"}*
- Datos del dispositivo no asociados a un dispositivo o usuario (si estos datos están ligados a un dispositivo o usuario, Intune los trata como datos identificados)
  - **ID:** Identificador de dispositivo único usado por Windows Update.
  - **localId:** Identificador único del dispositivo definido localmente. No se trata del nombre del dispositivo escrito en lenguaje natural. Es muy probable que se trate del mismo valor que el que hay almacenado en HKLM\Software\Microsoft\SQMClient\MachineId.
  - **aaddeviceid:** Id. de dispositivo de Azure Active Directory
  - **orgId:** GUID único que representa el inquilino de Microsoft Office 365.
  
> [!Important]  
> Nuestras directivas de administración de datos se describen en la [Declaración de privacidad de Microsoft Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement). Solo usamos sus datos de cliente para proporcionarle los servicios para los que se ha registrado. Tal como está descrito en el proceso de incorporación, anonimizamos y agregamos las puntuaciones de todas la organizaciones inscritas para mantener actualizadas las líneas de base.


### <a name="resources"></a>Recursos

Para obtener más información sobre aspectos de privacidad, vea los artículos siguientes:

- [Declaración de privacidad de Microsoft Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 y cumplimiento de la privacidad](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Términos de licencia y documentación](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Seguridad y privacidad en centros de datos de Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  
- [Confíe en su nube](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Centro de confianza](https://www.microsoft.com/trustcenter)  
