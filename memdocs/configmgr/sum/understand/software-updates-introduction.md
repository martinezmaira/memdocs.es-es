---
title: Introducción a las actualizaciones de software
titleSuffix: Configuration Manager
description: Conozca los conceptos básicos de las actualizaciones de software en Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: bd384edafd6464073b33a593a56bc88ba2fb0b87
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906761"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Introducción a las actualizaciones de software en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las actualizaciones de software de Configuration Manager proporcionan un conjunto de herramientas y recursos que pueden ayudar a administrar la compleja tarea de realizar un seguimiento de las actualizaciones de software y aplicarlas en equipos cliente de la empresa. Un proceso de administración de actualizaciones de software eficaz es necesario para mantener la eficiencia operativa, superar los problemas de seguridad y mantener la estabilidad de la infraestructura de red. Sin embargo, debido a la naturaleza cambiante de la tecnología y la aparición continua de nuevas amenazas de seguridad, la administración de las actualizaciones de software, para ser efectiva, requiere atención constante y continua.  

Para ver un escenario de ejemplo que muestra cómo podría implementar actualizaciones de software en su entorno, consulte [Example scenario to deploy security software updates](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md) (Escenario de ejemplo para implementar actualizaciones de software de seguridad).  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a> Sincronización de las actualizaciones de software  
 La sincronización de las actualizaciones de software en Configuration Manager se conecta a Microsoft Update para recuperar los metadatos de actualizaciones de software. El sitio de nivel superior (sitio de administración central o sitio primario independiente) se sincroniza con Microsoft Update según una programación o cuando el usuario inicia la sincronización de forma manual desde la consola de Configuration Manager. Cuando Configuration Manager finaliza la sincronización de las actualizaciones de software en el sitio de nivel superior, la sincronización de actualizaciones de software comienza en los sitios secundarios que haya. Cuando se completa la sincronización en cada uno de los sitios, primarios o secundarios, se crea una directiva de todo el sitio que proporciona a los equipos cliente la ubicación de los puntos de actualización de software.  

> [!NOTE]  
>  Las actualizaciones de software están habilitadas de forma predeterminada en la configuración de cliente. No obstante, si estable la opción de configuración de cliente **Habilitar actualizaciones de software en clientes** en **No** para deshabilitar las actualizaciones de software en una recopilación o en la configuración predeterminada, la ubicación de los puntos de actualización de software no se envía a los clientes asociados. Para obtener detalles, consulte la [configuración de cliente de las actualizaciones de software](../../core/clients/deploy/about-client-settings.md#software-updates).  

 Una vez que el cliente recibe la directiva, el cliente inicia un análisis para comprobar el cumplimiento de las actualizaciones de software y escribe la información en Instrumental de administración de Windows (WMI). Luego, la información de cumplimiento se envía al punto de administración que, a continuación, envía la información al servidor de sitio. Para más información sobre la evaluación de cumplimiento, consulte la sección [Software updates compliance assessment](#BKMK_SUMCompliance) en este tema.  

 Puede instalar varios puntos de actualización de software en un sitio primario. El primer punto de actualización de software que se instala se configura como origen de sincronización. Este punto se sincroniza mediante Microsoft Update o un servidor WSUS que no está en la jerarquía de Configuration Manager. Los demás puntos de actualización de software del sitio usan el primer punto de actualización de software como origen de sincronización.  

> [!NOTE]  
>  Cuando el proceso de sincronización de las actualizaciones de software se completa en el sitio de nivel superior, los metadatos de actualizaciones de software se replican a los sitios secundarios mediante la replicación de base de datos. Si conecta una consola de Configuration Manager a un sitio secundario, Configuration Manager muestra los metadatos de actualizaciones de software. En cambio, hasta que se instale y se configure un punto de actualización de software en el sitio, los clientes no detectarán si hay cumplimiento de las actualizaciones de software, no informarán de los datos de cumplimiento a Configuration Manager y no será posible implementar correctamente actualizaciones de software.  

### <a name="synchronization-on-the-top-level-site"></a>Sincronización en el sitio de nivel superior  
 El proceso de sincronización de actualizaciones de software en el sitio de nivel superior recupera de Microsoft Update los metadatos de actualizaciones de software que cumplen con los criterios especificados en las propiedades de componente de punto de actualización de software. Solo se configuran los criterios en el sitio de nivel superior.  

> [!NOTE]  
>  Puede especificar que el origen de sincronización, en lugar de ser Microsoft Update, sea un servidor WSUS existente que no está en la jerarquía de Configuration Manager.  

 La lista siguiente describe los pasos básicos para el proceso de sincronización en el sitio de nivel superior:  

1.  Se inicia la sincronización de las actualizaciones de software.  

2.  El administrador de sincronización de WSUS envía una solicitud al WSUS que se ejecuta en el punto de actualización de software para que inicie la sincronización con Microsoft Update.  

3.  Los metadatos de actualizaciones de software se sincronizan desde Microsoft Update, y todos los cambios se insertan o se actualizan en la base de datos de WSUS.  

4.  Una vez que WSUS finaliza la sincronización, el administrador de sincronización de WSUS sincroniza los metadatos de actualizaciones de software desde la base de datos de WSUS en la base de datos de Configuration Manager, y todo cambio que hubiese después de la última sincronización se inserta o se actualiza en la base de datos del sitio. Los metadatos de actualizaciones de software se almacenan en la base de datos del sitio como un elemento de configuración.  

5.  Los elementos de configuración de actualización de software se envían a los sitios secundarios mediante la replicación de base de datos.  

6.  Una vez finalizada la sincronización correctamente, el administrador de sincronización de WSUS crea el mensaje de estado 6702.  

7.  El administrador de sincronización de WSUS envía una solicitud de sincronización a todos los sitios secundarios.  

8.  El administrador de sincronización de WSUS envía una solicitud, de a una por vez, a cada WSUS que se ejecute en otros puntos de actualización de software del sitio. Los servidores WSUS de los otros puntos de actualización de software se configuran como réplicas del WSUS que se ejecuta en el punto de actualización de software predeterminado del sitio.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Sincronización en los sitios primarios secundarios y secundarios  
 Durante el proceso de sincronización de las actualizaciones de software en el sitio de nivel superior, los elementos de configuración de actualización de software se replican a los sitios secundarios mediante la replicación de base de datos. Al final del proceso, el sitio de nivel superior, envía una solicitud de sincronización al sitio secundario y el sitio secundario inicia la sincronización de WSUS. La lista siguiente describe los pasos básicos para el proceso de sincronización en un sitio primario secundario o un sitio secundario:  

1.  El administrador de sincronización de WSUS recibe una solicitud de sincronización del sitio de nivel superior.  

2.  Se inicia la sincronización de las actualizaciones de software.  

3.  El administrador de sincronización de WSUS envía una solicitud al WSUS que se ejecuta en el punto de actualización de software para que inicie la sincronización.  

4.  El WSUS que se ejecuta en el punto de actualización de software en el sitio secundario sincroniza los metadatos de actualizaciones de software desde el WSUS que se ejecuta en el punto de actualización de software en el sitio primario.  

5.  Una vez finalizada la sincronización correctamente, el administrador de sincronización de WSUS crea el mensaje de estado 6702.  

6.  Desde un sitio primario, el administrador de sincronización de WSUS envía una solicitud de sincronización a cualquier sitio secundario. El sitio secundario inicia la sincronización de las actualizaciones de software con el sitio primario principal. El sitio secundario se configura como una réplica del WSUS que se ejecuta en el sitio primario.  

7.  El administrador de sincronización de WSUS envía una solicitud, de a una por vez, a cada WSUS que se ejecute en otros puntos de actualización de software del sitio. Los servidores WSUS de los otros puntos de actualización de software se configuran como réplicas del WSUS que se ejecuta en el punto de actualización de software predeterminado del sitio.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a> Software updates compliance assessment  
 Antes de implementar las actualizaciones de software en equipos cliente de Configuration Manager, inicie una detección para comprobar el cumplimiento de las actualizaciones de software en los equipos cliente. Para cada actualización de software, se crea un mensaje de estado que contiene el estado de cumplimiento para la actualización. Los mensajes de estado se envían de forma masiva al punto de administración y, a continuación, al servidor de sitio, donde el estado de cumplimiento se inserta en la base de datos del sitio. El estado de cumplimiento de las actualizaciones de software se muestra en la consola de Configuration Manager. Puede implementar e instalar las actualizaciones de software en equipos que requieren las actualizaciones. Las secciones siguientes proporcionan información acerca de los estados de cumplimiento y describen el proceso de análisis para comprobar el cumplimiento de las actualizaciones de software.  

### <a name="software-updates-compliance-states"></a>Estados de cumplimiento de las actualizaciones de software  
 La tabla siguiente enumera y describe cada estado de cumplimiento que se muestra en la consola de Configuration Manager en relación con las actualizaciones de software.  

-   **Requerido**  

     Especifica que la actualización de software es aplicable y requerida en el equipo cliente. Cualquiera de las siguientes condiciones podría existir cuando el estado de actualización de software es **Requerido**:  

    -   La actualización de software no se implementó en el equipo cliente.  

    -   La actualización de software se instaló en el equipo cliente. Sin embargo, el mensaje de estado más reciente no se ha insertado aún en la base de datos del servidor de sitio. El equipo cliente vuelve a buscar la actualización una vez finalizada la instalación. Es posible que haya un retraso de hasta dos minutos antes de que el cliente envíe el estado actualizado al punto de administración que, a continuación, reenvía el estado actualizado al servidor de sitio.  

    -   La actualización de software se instaló en el equipo cliente. Sin embargo, la instalación de la actualización de software requiere un reinicio del equipo para completar la actualización.  

    -   La actualización de software se implementó en el equipo cliente, pero aún no se ha instalado.  

-   **No se requiere**  

     Especifica que la actualización de software no es aplicable en el equipo cliente. Por lo tanto, la actualización de software no se requiere.  

-   **Instalado**  

     Especifica que la actualización de software es aplicable en el equipo cliente y que el equipo cliente ya tiene instalada la actualización de software.  

-   **Desconocida**  

     Especifica que el servidor de sitio no recibió un mensaje de estado desde el equipo cliente, normalmente por una de las siguientes razones:  

    -   El equipo cliente no analizó correctamente el cumplimiento de las actualizaciones de software.  

    -   El análisis finalizó correctamente en el equipo cliente. Sin embargo, el mensaje de estado no se procesó todavía en el servidor de sitio, posiblemente, debido mensajes de estado pendientes.  

    -   El análisis finalizó correctamente en el equipo cliente, pero no se recibió el mensaje de estado desde el sitio secundario.  

    -   El análisis finalizó correctamente en el equipo cliente, pero el archivo de mensajes de estado se dañó de alguna manera y no se pudo procesar.  

### <a name="scan-for-software-updates-compliance-process"></a>Proceso de examen de cumplimiento de las actualizaciones de software  
 Cuando se instala y se sincroniza el punto de actualización de software, se crea una directiva de máquina de todo el sitio que informa a los equipos cliente que se han habilitado las actualizaciones de software de Configuration Manager para el sitio. Cuando un cliente recibe la directiva de equipo, se programa un análisis de evaluación de cumplimiento para que se inicie aleatoriamente dentro de las dos horas siguientes. Cuando se inicia el análisis, un agente de cliente de actualizaciones de software borra el historial de análisis, envía una solicitud para buscar el servidor WSUS que debería usarse para el análisis y actualiza la directiva de grupo local con la ubicación del servidor WSUS.  

> [!NOTE]  
>  Los clientes basados en Internet se deben conectar al servidor WSUS mediante SSL.  

 Se envía una solicitud de examen al Agente de Windows Update (WUA). El WUA se conecta entonces a la ubicación del servidor WSUS que se indica en la directiva local, recupera los metadatos de las actualizaciones de software que se sincronizaron en el servidor WSUS y realiza un examen de las actualizaciones del equipo cliente. El proceso del Agente cliente de actualizaciones de software permite detectar la finalización del examen de cumplimiento así como crear mensajes de estado para cada actualización de software cuyo estado de cumplimiento cambió después del último examen. Los mensajes de estado se envían al punto de administración en masa cada 15 minutos. A continuación, el punto de administración reenvía los mensajes de estado al servidor de sitio, donde los mensajes de estado se insertan en la base de datos del servidor de sitio.  

 Después del examen inicial de cumplimiento de las actualizaciones de software, el examen se inicia según la programación de exámenes configurada. Sin embargo, si el cliente examinó el cumplimiento de las actualizaciones de software en el plazo de tiempo indicado por el valor de período de vida (TTL), el cliente utiliza los metadatos de las actualizaciones de software almacenados de manera local. Si el último examen se realiza fuera del TTL, el cliente se debe conectar al WSUS que se ejecuta en el punto de actualización de software y actualizar los metadatos de las actualizaciones de software almacenados en el cliente  

 Con inclusión de la programación de exámenes, el examen de cumplimiento de las actualizaciones de software se puede iniciar de las siguientes maneras:  

-   **Programación de exploración de actualización de software**: la exploración de cumplimiento de las actualizaciones de software se inicia en la programación de exploración definida en la configuración del Agente cliente de actualizaciones de software. Para obtener más información sobre cómo configurar el cliente de actualizaciones de software, consulte la [configuración de cliente de las actualizaciones de software](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Acción de Propiedades de Configuration Manager**: el usuario puede iniciar la acción **Ciclo de detecciones de actualizaciones de software** o **Ciclo de evaluación de implementación de actualizaciones de software** en la pestaña **Acción** del cuadro de diálogo **Propiedades de Configuration Manager** en el equipo cliente.  

-   **Programación de reevaluación de implementación**: la evaluación de la implementación y el examen de cumplimiento de las actualizaciones de software se inician según la programación de reevaluación de implementación definida en la configuración del Agente cliente de actualizaciones de software. Para obtener más información sobre el cliente de actualizaciones de software, consulte la [configuración de cliente de las actualizaciones de software](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Antes de descargar los archivos de actualización**: cuando un equipo cliente recibe una directiva de asignación de una nueva implementación necesaria, el Agente cliente de actualizaciones de software descarga los archivos de actualización de software en la caché del cliente local. Antes de descargar los archivos de actualización de software, el agente cliente inicia un examen para comprobar que la actualización de software sigue siendo necesaria.  

-   **Antes de la instalación de las actualizaciones de software**: justo antes de la instalación de las actualizaciones de software, el Agente cliente de actualizaciones de software inicia un examen para comprobar si son necesarias.  

-   **Después de la instalación de las actualizaciones de software**: justo después de completarse la instalación de una actualización de software, el Agente cliente de actualizaciones de software inicia un examen para comprobar que las actualizaciones de software ya no son necesarias y crea un mensaje de estado que indica que la actualización de software está instalada. Si la instalación finalizó pero es necesario reiniciar el equipo, el mensaje de estado indica que el equipo cliente tiene pendiente un reinicio.  

-   **Después del reinicio del sistema**: cuando un equipo cliente tiene pendiente un reinicio del sistema para que finalice la instalación de la actualización de software, el Agente cliente de actualizaciones de software inicia un examen después del reinicio para comprobar que la actualización de software ya no es necesaria y crea un mensaje de estado que indica que la actualización de software está instalada.  

#### <a name="time-to-live-value"></a>Valor de período de vida  
 El software actualiza los metadatos necesarios para que el examen de cumplimiento de las actualizaciones de software se almacene en el equipo cliente local y, de forma predeterminada, sea válido hasta 24 horas. Este valor se denomina período de vida (TTL).  

#### <a name="scan-for-software-updates-compliance-types"></a>Tipos de examen de cumplimiento de las actualizaciones de software  
 El cliente realiza un examen de cumplimiento de las actualizaciones de software mediante un examen en línea o fuera de línea y un examen forzado o no forzado, en función de la manera en la que se inicia el examen de cumplimiento de las actualizaciones de software. A continuación se indica qué métodos de inicio del examen están en línea o fuera de línea y si el examen es forzado o no forzado.  

-   **Programación de exámenes de actualizaciones de software** (examen en línea no forzado)  

     Según la programación de exámenes configurada, el cliente se conecta al WSUS que se ejecuta en el punto de actualización de software para recuperar los metadatos de las actualizaciones de software sólo si el último examen se realizó fuera del TTL.  

-   **Ciclo de exámenes de actualizaciones de software** o **Ciclo de evaluación de implementación de actualizaciones de software** (examen en línea forzado)  

     El equipo cliente se conecta siempre al WSUS que se ejecuta en el punto de actualización de software para recuperar los metadatos de las actualizaciones de software antes de que el equipo cliente realice el examen de cumplimiento de las actualizaciones de software. Una vez finalizado el examen, se restablece el contador del TTL. Por ejemplo, si el TTL es de 24 horas, una vez que un usuario inicia un examen de cumplimiento de las actualizaciones de software, el TTL se restablece a 24 horas.  

-   **Programación de reevaluación de implementación** (examen en línea no forzado)  

     Según la programación de reevaluación de implementación configurada, el cliente se conecta al WSUS que se ejecuta en el punto de actualización de software para recuperar los metadatos de las actualizaciones de software sólo si el último examen se realizó fuera del TTL.  

-   **Antes de descargar los archivos de actualización** (examen en línea no forzado)  

     Para poder descargar los archivos de actualización en las implementaciones necesarias, el cliente se conecta al WSUS que se ejecuta en el punto de actualización de software para recuperar los metadatos de las actualizaciones de software sólo si el último examen se realizó fuera del TTL.  

-   **Antes de la instalación de las actualizaciones de software** (examen en línea no forzado)  

     Para poder instalar las actualizaciones de software en las implementaciones necesarias, el cliente se conecta al WSUS que se ejecuta en el punto de actualización de software para recuperar los metadatos de las actualizaciones de software sólo si el último examen se realizó fuera del TTL.  

-   **Después de la instalación de las actualizaciones de software** (examen fuera de línea forzado)  

     Después de la instalación de una actualización de software, el Agente cliente de actualizaciones de software inicia un examen mediante el uso de los metadatos locales. El cliente nunca se conecta al WSUS que se ejecuta en el punto de actualización de software para recuperar los metadatos de las actualizaciones de software.  

-   **Después del reinicio del sistema** (examen fuera de línea forzado)  

     Después de la instalación de una actualización de software y del reinicio del equipo, el Agente cliente de actualizaciones de software inicia un examen mediante el uso de los metadatos locales. El cliente nunca se conecta al WSUS que se ejecuta en el punto de actualización de software para recuperar los metadatos de las actualizaciones de software.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a> Paquetes de implementación de actualizaciones de software  
 Un paquete de implementación de actualizaciones de software es el vehículo utilizado para descargar actualizaciones de software en una carpeta compartida de red y copiar los archivos de origen de las actualizaciones de software en la biblioteca de contenido de los servidores de sitio así como en los puntos de distribución definidos en la implementación. Con el Asistente para descargar actualizaciones puede descargar las actualizaciones de software y agregarlas a los paquetes de implementación antes de su implementación. Este asistente le permite aprovisionar las actualizaciones de software en los puntos de distribución y comprobar que esta parte del proceso de implementación se realiza correctamente antes de implementar las actualizaciones de software en los clientes.  

 Cuando se implementan las actualizaciones de software descargadas mediante el Asistente para implementar actualizaciones de software, la implementación utiliza automáticamente el paquete de implementación que contiene las actualizaciones de software. Cuando se implementan actualizaciones de software que no se descargaron, se debe especificar un paquete de implementación nuevo o existente en el Asistente para implementar actualizaciones de software, y las actualizaciones de software se descargarán cuando finalice el Asistente.  

> [!IMPORTANT]  
>  Se debe crear manualmente la carpeta compartida de red para los archivos de origen del paquete de implementación antes de especificarla en el Asistente. Cada paquete de implementación debe utilizar una carpeta compartida de red diferente.  

> [!IMPORTANT]  
>  Tanto la cuenta de equipo de proveedor de SMS como el usuario administrativo que en realidad descarga las actualizaciones de software requieren permisos de **escritura** para el origen del paquete. Restrinja el acceso al origen del paquete para reducir el riesgo de que un atacante altere los archivos de origen de las actualizaciones de software en el origen del paquete.  

 Cuando se crea un nuevo paquete de implementación, la versión del contenido se establece en 1 antes de descargar las actualizaciones de software. Cuando se descargan los archivos de actualización de software mediante el paquete, la versión del contenido se incrementa a 2. Por lo tanto, todos los nuevos paquetes de implementación se inician con una versión del contenido de 2. Cada vez que cambia el contenido en un paquete de implementación, la versión del contenido se incrementa en 1. Para obtener más información, consulte [Fundamental concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Conceptos fundamentales de la administración de contenido).  

 Los clientes instalan las actualizaciones de software de una implementación mediante cualquier punto de distribución que tenga las actualizaciones de software disponibles, independientemente del paquete de distribución. Aunque se elimine un paquete de implementación de una implementación activa, los clientes seguirán siendo capaces de instalar las actualizaciones de software en la implementación siempre y cuando cada actualización se descargue al menos en otro paquete de implementación y esté disponible en un punto de distribución al que se pueda acceder desde el cliente. Si se elimina el último paquete de implementación que contiene una actualización de software, los equipos cliente no pueden recuperar la actualización de software hasta que la actualización se vuelve a descargar en un paquete de implementación. Las actualizaciones de software aparecen con una flecha roja en la consola de Configuration Manager cuando los archivos de actualización no están en ningún paquete de implementación. Las implementaciones aparecen con una flecha roja doble si contienen actualizaciones que se encuentran en este estado.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a> Flujos de trabajo de implementación de actualizaciones de software  
 Hay dos escenarios principales de implementación de las actualizaciones de software en su entorno, la implementación manual y la implementación automática. Normalmente, las actualizaciones de software se implementan manualmente para crear una línea de base para los equipos cliente y, a continuación, las actualizaciones de software se administran en los clientes mediante la implementación automática. En las secciones siguientes se facilita un resumen del flujo de trabajo de la implementación manual y automática de las actualizaciones de software.  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Implementación manual de las actualizaciones de software  
 La implementación manual de las actualizaciones de software es un proceso que incluye la selección de las actualizaciones de software en la consola de Configuration Manager y el inicio manual del proceso de implementación. Este método de implementación se utiliza normalmente para que los equipos cliente tengan todas las actualizaciones de software necesarias antes de que se creen las reglas de implementación automática que administran las implementaciones de las actualizaciones de software mensuales continuas, así como para implementar los requisitos de las actualizaciones de software fuera de banda. En la lista siguiente se indica el flujo de trabajo general de la implementación manual de las actualizaciones de software:  

1.  Filtre las actualizaciones de software que utilicen requisitos específicos. Por ejemplo, podría especificar criterios para la recuperación de todas las actualizaciones de software de seguridad o imprescindibles que se requieran en más de 50 equipos cliente.  

2.  Cree un grupo de actualizaciones de software que contenga las actualizaciones de software.  

3.  Descargue el contenido de las actualizaciones de software en el grupo de actualizaciones de software.  

4.  Implemente manualmente el grupo de actualizaciones de software.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Implementación automática de las actualizaciones de software  
 La implementación automática de las actualizaciones de software se configura mediante una regla de implementación automática (ADR). Este método de implementación se utiliza normalmente para las actualizaciones de software mensuales (que se conocen como "Patch Tuesday") y para administrar las actualizaciones de definiciones. Cuando la regla se ejecuta, se quitan las actualizaciones de software del grupo de actualizaciones de software (si se está usando un grupo existente); las actualizaciones de software que cumplan los criterios especificados (por ejemplo, todas las actualizaciones de software de seguridad publicadas en la última semana) se agregan a un grupo de actualizaciones de software; los archivos de contenido de las actualizaciones de software se descargan y copian en los puntos de distribución, y las actualizaciones de software se implementan en equipos cliente de la colección de destino. En la lista siguiente se indica el flujo de trabajo general de la implementación automática de las actualizaciones de software:  

1. Cree una ADR que especifique la configuración de implementación, por ejemplo:  

   -   Recopilación de destino  

   -   Decida si desea habilitar la implementación o notificar el cumplimiento de las actualizaciones de software para los equipos cliente de la recopilación de destino  

   -   Criterios de actualizaciones de software  

   -   Programaciones de evaluación e implementación  

   -   Experiencia del usuario  

   -   Propiedades de descarga  

2. Las actualizaciones de software se agregan a un grupo de actualizaciones de software.  

3. El grupo de actualizaciones de software se implementa en los equipos cliente de la recopilación de destino (si se ha especificado).  

   Debe determinar la estrategia de implementación que se utilizará en su entorno. Por ejemplo, podría crear la ADR y seleccionar una recopilación de destino de clientes de prueba. Después de comprobar que las actualizaciones de software estén instaladas en el grupo de prueba, puede agregar una nueva implementación a la regla o cambiar la recopilación de la implementación existente por una recopilación de destino que incluya un conjunto de clientes más amplio. Los objetos de actualización de software que se crean mediante reglas ADR son interactivos.  

- Las actualizaciones de software que se implementaron mediante una ADR se implementan automáticamente en los nuevos clientes agregados a la recopilación de destino.  

- Las nuevas actualizaciones de software que se agregan a un grupo de actualizaciones de software se implementan automáticamente en los clientes de la recopilación de destino.  

- Puede habilitar o deshabilitar las implementaciones en cualquier momento para la ADR.  

  Después de crear una ADR, puede agregar implementaciones adicionales a la regla. Esto puede ayudarle a administrar la complejidad de la implementación de varias actualizaciones en diferentes recopilaciones. Cada nueva implementación ofrece todas las funcionalidades y la experiencia completa de supervisión de la implementación, y todas las implementaciones nuevas que agrega:  

- Usan el mismo grupo y paquete de actualizaciones que se creó la primera vez que se ejecutó el ADR.  

- Pueden especificar una recopilación diferente.  

- Admiten propiedades de implementación únicas, como:  

  -   Hora de activación  

  -   Fecha límite  

  -   Mostrar u ocultar la experiencia del usuario final  

  -   Alertas independientes para esta implementación  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a> Proceso de implementación de actualizaciones de software  
 Después de implementar las actualizaciones de software o cuando una regla de implementación automática se ejecuta e implementa actualizaciones de software, se agrega una directiva de asignación de implementación a la directiva de equipo del sitio. Las actualizaciones de software se descargan desde la ubicación de descarga, Internet, o la carpeta compartida de red, en el origen del paquete. Las actualizaciones de software se copian desde el origen del paquete en la biblioteca de contenido del servidor del sitio y, a continuación, se copian en la biblioteca de contenido del punto de distribución.  

 Cuando un equipo cliente de la recopilación de destino de la implementación recibe la directiva de equipo, el Agente cliente de actualizaciones de software inicia un examen de evaluación. El agente cliente descarga el contenido de las actualizaciones de software necesarias desde un punto de distribución en la caché del cliente local en la opción **Horas de disponibilidad del software** para la implementación antes de que las actualizaciones de software estén disponibles para la instalación. Las actualizaciones de software de las implementaciones opcionales (implementaciones que no tienen una fecha límite de instalación) no se descargan hasta que un usuario inicia manualmente la instalación.  

 Cuando pasa la fecha límite configurada, el Agente cliente de actualizaciones de software realiza un examen para comprobar que las actualizaciones de software siguen siendo necesarias. A continuación, comprueba la caché local del equipo cliente para comprobar que los archivos de origen de las actualizaciones de software siguen estando disponibles. Por último, el cliente instala las actualizaciones de software. Si se eliminó el contenido de la caché del cliente para dejar espacio a otra implementación, el cliente vuelve a descargar las actualizaciones de software desde el punto de distribución en la caché del cliente. Las actualizaciones de software siempre se descargan en la memoria caché del cliente, con independencia del tamaño de memoria caché de cliente máximo configurado. Una vez completada la instalación, el agente cliente comprueba que las actualizaciones de software ya no son necesarias y, a continuación, envía un mensaje de estado al punto de administración para indicar que las actualizaciones de software ya están instaladas en el cliente.  

### <a name="required-system-restart"></a>Reinicio obligatorio del sistema  
 De forma predeterminada, cuando las actualizaciones de software de una implementación necesaria se instalan en un equipo cliente y se requiere un reinicio del sistema para que finalice la instalación, se inicia el reinicio del sistema. En el caso de las actualizaciones de software que se instalaron antes de la fecha límite, el reinicio automático del sistema se pospone hasta la fecha límite, a menos que el equipo se reinicie antes por algún otro motivo. El reinicio del sistema se puede suprimir en el caso de los servidores y estaciones de trabajo. Estas opciones se configuran en la página **Experiencia del usuario** del Asistente para implementar actualizaciones de software o el Asistente para crear regla de implementación automática.  

### <a name="deployment-reevaluation-cycle"></a>Ciclo de reevaluación de la implementación  
 De forma predeterminada, los equipos cliente inician un ciclo de reevaluación de implementación cada 7 días. Durante este ciclo de evaluación, el equipo cliente busca las actualizaciones de software que se implementaron e instalaron previamente. Si faltan actualizaciones de software, las actualizaciones de software se vuelven a instalar desde la caché local. Si alguna actualización de software ya no está disponible en la caché local, se descarga desde un punto de distribución y, a continuación, se instala. Puede configurar la programación de reevaluación en la página **Actualizaciones de software** de la configuración de cliente del sitio.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a> Compatibilidad con dispositivos de Windows Embedded que usan filtros de escritura  
 Cuando se implementan actualizaciones de software en dispositivos de Windows Embedded con filtros de escritura habilitados, se puede especificar si se desea deshabilitar el filtro de escritura en el dispositivo durante la implementación y luego reiniciar el dispositivo después de la misma. Si no se deshabilita el filtro de escritura, el software se implementa en una superposición temporal y ya no estará instalado cuando el dispositivo se reinicie a menos que otra implementación fuerce la conservación de los cambios.  

> [!NOTE]  
>  Cuando implemente una actualización de software en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada. Esto le permite administrar cuándo se deshabilita y habilita el filtro de escritura, y cuándo se reinicia el dispositivo.  

 La opción de la experiencia del usuario que permite controlar el comportamiento de los filtros de escritura es la casilla **Confirmar cambios dentro de la fecha límite o en una ventana de mantenimiento (reinicio necesario)** .  

 Para obtener más información sobre cómo Configuration Manager administra los dispositivos insertados que usan filtros de escritura, consulte [Planeación de implementación de cliente en dispositivos de Windows Embedded](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a> Extender las actualizaciones de software en Configuration Manager  
 Use System Center Updates Publisher para administrar las actualizaciones de software que no estén disponibles en Microsoft Update. Después de publicar las actualizaciones de software en el servidor de actualización y sincronizarlas en Configuration Manager, puede implementar las actualizaciones de software en los clientes de Configuration Manager. Para obtener más información sobre Updates Publisher, consulte [Updates Publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

## <a name="next-steps"></a>Pasos siguientes
[Planear las actualizaciones de software](../plan-design/plan-for-software-updates.md)
