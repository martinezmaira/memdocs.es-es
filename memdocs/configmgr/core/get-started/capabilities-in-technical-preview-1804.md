---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Conozca las nuevas características disponibles en la versión Technical Preview 1804 de Configuration Manager.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b30386745244900e7f525f8f45b25a598628bf43
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078743"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Funciones de Technical Preview 1804 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en Technical Preview 1804 de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de versión preliminar técnica. 

Revise el artículo [Technical Preview para System Center Configuration Manager](technical-preview.md) antes de instalar esta actualización. Ese artículo le ayuda a familiarizarse con los requisitos generales y las limitaciones para usar una versión Technical Preview, cómo actualizar entre versiones y cómo proporcionar comentarios.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conocidos de esta Technical Preview

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a> El vínculo del programa de instalación para descargar las actualizaciones no funciona
<!--514334-->
Si ejecuta el programa de instalación desde un disco, la página inicial incluye un vínculo denominado **Obtener las actualizaciones de Configuration Manager más recientes**, que no funciona en esta versión. Es este vínculo es para descargar los archivos necesarios para el programa de instalación.

#### <a name="workaround"></a>Solución alternativa
Para descargar los archivos necesarios para el programa de instalación, ejecute el asistente para la instalación. En la página Descargas de requisitos previos, use la opción de **Descargar archivos requeridos**. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a> El punto de servicio web del catálogo de aplicaciones no se puede habilitar para HTTPS
<!--512637-->
Si el punto de servicio web del catálogo de aplicaciones está habilitado para HTTPS:

- Las aplicaciones implementadas como disponibles para los usuarios no se muestran en el Centro de software  

- Se muestra el siguiente error en awebsctl.log:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Solución alternativa
Vuelva a configurar el punto de servicio de web del catálogo de aplicaciones para que se comunique mediante conexiones HTTP.  




</br>

**Estas son las nuevas características que puede probar con esta versión.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Configuración de una biblioteca de contenido remoto para el servidor de sitio  
<!--1357525-->
Para liberar espacio de la unidad de disco duro en el servidor de sitio primario, cambie la ubicación de su [biblioteca de contenido](../plan-design/hierarchy/the-content-library.md) a otra ubicación de almacenamiento. Puede mover la biblioteca de contenido a otra unidad en el servidor de sitio, un servidor independiente o discos tolerantes a errores de una red de área de almacenamiento (SAN). Se recomienda una SAN, ya que proporciona almacenamiento elástico que aumenta o disminuye con el tiempo para satisfacer los requisitos variables del contenido. 

Esta biblioteca de contenido remoto es un nuevo requisito previo para la [alta disponibilidad del rol de servidor de sitio](capabilities-in-technical-preview-1706.md#site-server-role-high-availability). 

> [!Note]  
> Esta acción solo mueve la biblioteca de contenido en el servidor de sitio. No afecta a la ubicación de la biblioteca de contenido en los puntos de distribución. 

### <a name="prerequisites"></a>Requisitos previos  
- La cuenta de equipo del servidor de sitio necesita **leer** y **escribir** los permisos para la ruta de acceso de red a la que va a mover la biblioteca de contenido. No se instala ningún componente en el sistema remoto. 

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, cambie al área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione **Sitios**. En la pestaña **Resumen** de la parte inferior del panel de detalles, observará una nueva columna **Biblioteca de contenido**.  

2. Haga clic en **Administrar la biblioteca de contenido** en la cinta de opciones.  

3. Seleccione **On a network share** (En un recurso compartido de red) y escriba una ruta de acceso de red válida. Esta ruta de acceso es la ubicación a la que el sitio mueve la biblioteca de contenido. Haga clic en **Aceptar**.  

4. Observe la propiedad **Status** de la columna Biblioteca de contenido en el panel de detalles. Se actualiza para mostrar el progreso del sitio cuando se mueve la biblioteca de contenido. Cuando esta operación está en curso, se muestra el porcentaje completado. Si se produce un estado de error, se muestra el error. Los errores comunes incluyen `access denied` o `disk full`. Cuando ha finalizado, se muestra `OK`. Consulte **distmgr.log** para más información. Para más información, consulte [Registros de servidor de sistema de sitio y servidor de sitio](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog).  

Si tiene que devolver la biblioteca de contenido al servidor de sitio, repita este proceso, pero selecciona la opción **Local to the site server** (Local al servidor de sitio).  

> [!Tip]  
> Para mover el contenido a otra unidad en el servidor de sitio, use la herramienta **Content Library Transfer**. Para más información, consulte [Kit de herramientas de Configuration Manager](#configuration-manager-toolkit).  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a> Envío de comentarios desde la consola de Configuration Manager  
<!--1357542-->

Enviar una sonrisa Ahora puede contar directamente al equipo de Configuration Manager sus experiencias. Enviar comentarios es fácil desde la consola de Configuration Manager. Nos gustaría recibir todos sus comentarios: sugerencias, problemas y elogios.  

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus **comentarios** para que sepamos cómo le ha ido.  

1. En la consola de Configuration Manager, haga clic en el botón de sonrisa en la esquina superior derecha encima de la cinta de opciones.  

2. En la lista desplegable, seleccione una de las opciones disponibles:  

   - **Enviar una sonrisa**: significa que le gustó algo. En esta opción, especifique los detalles de sus comentarios. Luego, puede incluir, si quiere, una captura de pantalla y la dirección de correo electrónico.  

   - **Enviar un ceño fruncido**: significa que encontró un problema en la consola o que algo no ha funcionado como esperaba. En esta opción, especifique los detalles del posible problema con el producto. Puede incluir, si quiere, una captura de pantalla, la dirección de correo electrónico y datos de diagnóstico.  

   - **Enviar una sugerencia**: significa que tiene una idea para cambiar y mejorar Configuration Manager. Esta opción abre nuestro sitio de [UserVoice](https://configurationmanager.uservoice.com) en el explorador web.  

Esta información va directamente al equipo de producto de Microsoft de Configuration Manager. Si bien aún se admite el uso del centro de opiniones de Windows 10, le recomendamos que use el mecanismo de comentarios incluido en la consola.  

La siguiente información anónima siempre se incluye con el comentario para que sirva de contexto:  

- Versión e idioma de la consola de Configuration Manager  

- Versión del sitio de Configuration Manager  

- Identificador de soporte técnico, también conocido como identificador de jerarquía  

- Versión e idioma del sistema operativo del sistema en el que se ejecuta la consola  

- La ubicación exacta en la consola desde la que hizo clic en la sonrisa  

Estos datos son coherentes con la recopilación de nuestros datos de uso y diagnóstico. Para obtener más información, vea [Diagnósticos y datos de uso](../plan-design/diagnostics/diagnostics-and-usage-data.md).

### <a name="known-issues"></a>Problemas conocidos

Si intenta enviar comentarios desde un dispositivo que no puede tener acceso a Internet, la aplicación podría cerrarse inesperadamente. Para enviar una sonrisa o una desaprobación, asegúrese de que el dispositivo pueda acceder a petrol.office.microsoft.com.



## <a name="support-center"></a>Support Center
<!--1357489-->

Use Support Center para solucionar los problemas de los clientes, visualizar los registros en tiempo real o capturar el estado de un equipo cliente de Configuration Manager para su posterior análisis. Support Center es una única herramienta para consolidar muchas herramientas de solución de problemas del administrador. Puede encontrar una versión preliminar de la versión más reciente de Support Center y una versión preliminar de nuestro nuevo visor de registros en la versión preliminar técnica. Puede encontrar el programa de instalación de Support Center en el servidor de sitio en la carpeta **cd.latest\SMSSETUP\Tools\SupportCenter**.

 > [!Tip]  
 > Puede encontrar documentación heredada sobre la funcionalidad existente en Support Center en [TechNet](https://technet.microsoft.com/library/dn688621.aspx). Hay información importante en proceso para migrar a la biblioteca de docs.microsoft.com.  

### <a name="new-support-center-features"></a>Nuevas características de Support Center  

- Un nuevo visor de registros, OneTrace. Funciona de forma similar a CMTrace, e incluye mejoras, como una vista con pestañas y ventanas acoplables.  

- Una nueva característica de recopilador de datos recopila registros de diagnóstico del cliente de Configuration Manager local o remoto. Proporciona diagnósticos en tiempo real del inventario (sustituye a Cliente Spy), la directiva (sustituye a Policy Spy) y la caché del cliente.  



## <a name="configuration-manager-toolkit"></a>Kit de herramientas de Configuration Manager
<!--1357145-->

Las herramientas de servidor y cliente de Configuration Manager ahora se incluyen en la versión preliminar técnica. Búsquelas en la carpeta **cd.latest\SMSSETUP\Tools** en el servidor de sitio. No se necesita ninguna otra instalación.

#### <a name="server-tools"></a>Herramientas de servidor  

- **DP Job Manager**: soluciona los problemas de los trabajos de distribución de contenido a los puntos de distribución  

- **Collection Evaluation Viewer**: vea detalles de la evaluación de colecciones  

- **Content Library Explorer**: permite ver el contenido del almacén de instancia única de la biblioteca de contenido  

- **Content Library Transfer**: transfiere la biblioteca de contenido entre unidades  

- **Content Ownership Tool**: cambia la propiedad de los paquetes huérfanos. Estos paquetes existen en el sitio sin un servidor de sitio propietario.  

- **Role-based Administration and Auditing Tool**: ayuda a los administradores a auditar la configuración de roles  

#### <a name="client-tools"></a>Herramientas cliente

- **CMTrace**: vea registros  

- **Deployment Monitoring Tool**: permite solucionar los problemas de aplicaciones, actualizaciones e implementaciones de línea de base  

- **Policy Spy**: vea asignaciones de directiva  

- **Power Viewer Tool**: permite ver el estado de la característica de administración de energía  

- **Send Schedule Tool**: desencadena programaciones y evaluaciones de líneas de base de DCM  

> [!Important]  
> [Support Center](#support-center) es la recomendada en la mayoría de los casos, dado que incluye la misma funcionalidad o mejorada de las siguientes herramientas:  
> - Cliente Spy
> - CMTrace<sup>1</sup> 
> - Deployment Monitoring Tool
> - Policy Spy
> - Send Schedule Tool
> 
> <sup>1</sup> CMTrace no depende de .NET o Windows Presentation Foundation (WPF), así que aún se usa en imágenes de arranque de Windows PE.

### <a name="known-issues"></a>Problemas conocidos
Algunas herramientas de cliente y servidor pueden cerrarse inesperadamente al iniciar. Este problema se debe a un archivo que falta en el soporte físico. Como solución, copie el archivo **Microsoft.Diagnostics.Tracing.EventSource.dll** desde el directorio AdminConsole\bin en los directorios SMSSETUP\Tools\ClientTools y ServerTools. Este archivo debe ser de la misma versión que usa la consola de Configuration Manager. Es posible que otras versiones no funcionen. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Desinstalación de aplicaciones al revocarse la aprobación
<!--1357891-->

El comportamiento de revocar la aprobación de una aplicación ha cambiado. Ahora cuando se deniega la solicitud de la aplicación, el cliente desinstala la aplicación del dispositivo del usuario. 

### <a name="prerequisites"></a>Requisitos previos
- Habilite la característica **Approve application requests for users per device** (Aprobar solicitudes de aplicación de usuarios por dispositivo).

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, implemente una aplicación en un usuario que requiera aprobación. En la pestaña **Configuración de implementación** de la implementación, habilite la opción **An administrator must approve a request for this application on the device** (Un administrador debe aprobar una solicitud de esta aplicación en el dispositivo).  

2. En el cliente de Configuration Manager en el Centro de software, el usuario solicita aprobación para instalar la aplicación.  

3. En la consola de Configuration Manager, apruebe la solicitud de este usuario de instalar la aplicación en el dispositivo. Las solicitudes de aprobación de aplicación se muestran en el área de trabajo **Biblioteca de software**, en **Administración de aplicaciones**, en el nodo **Solicitudes de aprobación**.  

4. En el cliente en el Centro de software, el usuario instala la aplicación.  

5. En la consola de Configuration Manager, deniegue la solicitud del usuario de la aplicación en el dispositivo.  

### <a name="known-issues"></a>Problemas conocidos
- Después de que el usuario instala la aplicación en el cliente, actualice la directiva de usuario. En el Centro de software, cambie a la pestaña **Options** (Opciones), expanda **Computer maintenance** (Mantenimiento de equipos) y haga clic en **Sync Policy** (Directiva de sincronización).<!--480609-->  

- El punto de servicio web del catálogo de aplicaciones debe ser HTTP. Para más información, consulte [Problemas conocidos de esta Technical Preview](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Exclusión de contenedores de Active Directory de la detección
<!--1358143-->
Para reducir el número de objetos detectados, ahora puede excluir determinados contenedores de la detección del sistema de Active Directory. Esta característica es el resultado de sus [comentarios en UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Configuración de jerarquía** y seleccione **Métodos de detección**. Seleccione **Detección de sistema de Active Directory** y haga clic en **Propiedades** en la cinta de opciones.  

2. Haga clic en el icono Nuevo para especificar un nuevo contenedor de Active Directory.   

3. En el cuadro de diálogo Contenedor de Active Directory, busque o escriba la **ruta de acceso** en la sección Ubicación para iniciar la detección.  

4. En la sección Opciones de búsqueda, habilite la opción **Buscar recursivamente contenedores secundarios de Active Directory**. A continuación, haga clic en **Agregar** para seleccionar los subcontenedores que se excluirán de esta detección.  

5. En el cuadro de diálogo Seleccionar nuevo contenedor, seleccione un contenedor secundario para excluir. Haga clic en **Aceptar** para cerrar el cuadro de diálogo Seleccionar nuevo contenedor.  

6. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de Contenedor de Active Directory.  

7. En la ventana Propiedades de Detección de sistema de Active Directory, vea la ruta de acceso del contenedor de Active Directory en el que se inicia la detección. La columna **Recursivo** muestra **Sí** y la nueva columna **Has Exclusions** (Tiene exclusiones) también muestra **Sí**. Haga clic en **Aceptar** para cerrar la ventana Propiedades de Detección de sistema de Active Directory.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especificación de la visibilidad del vínculo al sitio web del catálogo de aplicaciones en el Centro de software
<!--1358214-->

Ahora, puede controlar si el vínculo para **abrir el sitio web del catálogo de aplicaciones** aparece en el nodo **Installation status** (Estado de instalación) del Centro de software.  

> [!Note]  
> La compatibilidad con la experiencia del usuario con el sitio web del catálogo de aplicaciones finaliza con la primera actualización publicada después del 1 de junio de 2018. Para más información, consulte [Características en desuso y eliminadas](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

### <a name="try-it-out"></a>Haga la prueba
 Intente completar las tareas. Y, luego, envíenos sus [comentarios](#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, área de trabajo **Administración**, nodo **Configuración de cliente**, cree una directiva de configuración de dispositivos cliente personalizada.  

2. Seleccione el grupo **Centro de software**.  

3. Para **Configuración del Centro de software**, haga clic en **Personalizar**.  

4. Habilite la opción para **ocultar el vínculo al sitio web del catálogo de aplicaciones en el Centro de software**.   

Para más información sobre la configuración de cliente, consulte [Configuración del cliente](../clients/deploy/configure-client-settings.md).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrado de las reglas de implementación automáticas por arquitectura de actualización de software
 <!--1322266-->
Ahora puede filtrar las reglas de implementación automática para excluir arquitecturas como Itanium y ARM64.

### <a name="try-it-out"></a>Haga la prueba
Intente completar las tareas. Y, luego, envíenos sus [comentarios](#bkmk_feedback) para que sepamos cómo le ha ido.

1. En la consola de Configuration Manager, cambie al área de trabajo **Biblioteca de software**. Expanda **Actualizaciones de software** y seleccione **Reglas de implementación automática**. En la cinta de opciones, seleccione **Crear regla de implementación automática**.  

2. Rellene la configuración adecuada en las pestañas **General** y **Configuración de implementación**.  

3. En la pestaña **Actualizaciones de software**, seleccione **Arquitectura** y luego haga clic en **items to find** (Elementos para buscar) en **Criterios de búsqueda**.  

4. Seleccione las arquitecturas que quiere incluir en la regla de implementación automática.  

5. Haga clic en **Siguiente** y continúe con la creación de la regla de implementación automática.  

> [!IMPORTANT]  
> Recuerde que hay aplicaciones de 32 bits (x86) y componentes que se ejecutan en sistemas de 64 bits (x64). A menos que esté seguro de que no necesita x86, habilítelo también cuando elija x64.  

### <a name="known-issues"></a>Problemas conocidos
Después de agregar los criterios de arquitectura, la página de propiedades de reglas de implementación automática muestra **Título** en los criterios de búsqueda. La regla de implementación automática aún funciona según lo previsto y selecciona las actualizaciones de software correctas. Sin embargo, no se pueden incluir los criterios **Arquitectura** y **Título** por el momento. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Mejoras en la implementación del sistema operativo
Se han realizado las siguientes mejoras en la implementación del sistema operativo, algunas de las cuales son el resultado de los comentarios de los usuarios en UserVoice.  

- [Enmascaramiento de la información confidencial almacenada en variables de secuencia de tareas](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): en el paso [Configurar variable de secuencia de tareas](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable), seleccione la nueva opción **Do not display this value** (No mostrar este valor). Por ejemplo, al especificar una contraseña.<!--1358330--> Cuando se habilita esta opción, se aplican los comportamientos siguientes:
  - El valor de la variable no se muestra en el archivo smsts.log.
  - La consola de Configuration Manager y el proveedor de SMS administran este valor igual que otros secretos, como las contraseñas.
  - El valor no se incluye cuando se exporta la secuencia de tareas.
  - El editor de secuencias de tareas no lee este valor cuando se edita el paso. Vuelva a escribir el valor entero para realizar cambios.

  > [!Important]  
  > Las variables y sus valores se guardan con la secuencia de tareas como XML y se ofuscan en la base de datos. Cuando el cliente solicita una directiva de secuencia de tareas desde el punto de administración, se cifra en tránsito y cuando se almacena en el cliente. Sin embargo, todos los valores de variables son texto sin formato en el entorno de la secuencia de tareas en memoria durante el tiempo de ejecución en el cliente. Si la secuencia de tareas incluye un paso para generar el valor de la variable de salida, esta salida está en texto sin formato. Este comportamiento requiere la acción explícita del administrador de incluir un paso de este tipo en la secuencia de tareas. 


- [Enmascaramiento del nombre del programa durante el paso Ejecutar comando de una secuencia de tareas](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): para evitar la visualización o el registro de información posiblemente confidencial, establezca la variable de secuencia de tareas **OSDDoNotLogCommand** en `TRUE`. Esta variable enmascara el nombre del programa en el archivo smsts.log durante un paso de secuencia de tareas [Ejecutar línea de comandos](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine). <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Mejoras en la consola de Configuration Manager
- La información del usuario primario ahora es visible cuando se visualizan los miembros de una recopilación en **Assets and Compliance** (Recursos y cumplimiento), **Recopilaciones de dispositivos**.<!--510252-->  



## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview de Configuration Manager](technical-preview.md).    
