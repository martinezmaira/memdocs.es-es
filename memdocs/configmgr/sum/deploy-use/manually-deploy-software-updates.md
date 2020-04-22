---
title: Implementar actualizaciones de software manualmente
titleSuffix: Configuration Manager
description: Cree manualmente las implementaciones de software para actualizar los clientes con las actualizaciones de software requeridas o para implementar actualizaciones fuera de banda.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: b7d6640beb9353d5c613cf38e3f880e7fd76b393
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699243"
---
# <a name="manually-deploy-software-updates"></a>Implementar actualizaciones de software manualmente  

*Se aplica a: Configuration Manager (rama actual)*

Una implementación de actualizaciones de software manual es el proceso de seleccionar actualizaciones de software desde la consola de Configuration Manager e iniciar manualmente el proceso de implementación. También se pueden agregar actualizaciones de software seleccionadas a un grupo de actualización para después implementar manualmente el grupo de actualización. Normalmente se utilizan las implementaciones manuales para actualizar los clientes con las actualizaciones de software. Después se utilizan las reglas de implementación automática (ADR) para administrar implementaciones de actualizaciones de software mensuales en curso. También se utiliza este método manual para implementar actualizaciones de software fuera de banda. Para obtener más información sobre qué método de implementación es el adecuado para usted, vea [Implementar actualizaciones de software](deploy-software-updates.md).



##  <a name="step-1-specify-search-criteria-for-software-updates"></a><a name="BKMK_1SearchCriteria"></a> Paso 1: Especificar criterios de búsqueda para las actualizaciones de software  

Dependiendo de las combinaciones de productos y clasificaciones que el sitio sincroniza, hay potencialmente miles de actualizaciones de software que se muestran en la consola de Configuration Manager. El primer paso del flujo de trabajo para implementar manualmente las actualizaciones de software es identificar aquéllas que desea implementar. Por ejemplo, se muestran todas las actualizaciones de software requeridas en más de 50 dispositivos cliente con una clasificación de **seguridad** o **crítica**.  

> [!IMPORTANT]  
>  Una única implementación de actualizaciones de software tiene un límite de 1000 actualizaciones de software.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Proceso para especificar criterios de búsqueda de actualizaciones de software  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Actualizaciones de software** y haga clic en **Todas las actualizaciones de software**. Este nodo muestra todas las actualizaciones de software sincronizadas.  

    > [!NOTE]  
    >  El nodo **Todas las actualizaciones de software** solo muestra actualizaciones de software con una clasificación de **Crítica** y **Seguridad** publicadas en los últimos 30 días.  

2.  En el panel de búsqueda, filtre para identificar las actualizaciones de software que necesita. Use una de las opciones siguientes o ambas:  

    -   En el cuadro de texto de búsqueda, escriba una cadena de búsqueda que filtre las actualizaciones de software. Por ejemplo, escriba el artículo o Id. de boletín para una actualización de software específica. También puede escribir una cadena que aparezca en el título de varias actualizaciones de software.  

    -   Haga clic en **Agregar criterios** y seleccione los criterios para filtrar las actualizaciones de software. Haga clic en **Agregar** y después proporcione los valores de los criterios.  

3.  Haga clic en **Buscar** para filtrar las actualizaciones de software.  

    > [!TIP]  
    >  Guarde los criterios de filtro usados con frecuencia. En la cinta, haga clic en la opción **Guardar búsqueda actual**. Recupere las búsquedas anteriores haciendo clic en **Búsquedas guardadas**.   



##  <a name="step-2-create-a-software-update-group-that-contains-the-software-updates"></a><a name="BKMK_2UpdateGroup"></a> Paso 2: Crear un grupo de actualizaciones de software que contenga las actualizaciones de software   

Los grupos de actualizaciones de software le permiten organizar las actualizaciones de software requeridas para la posterior implementación. Utilice el siguiente procedimiento para agregar manualmente actualizaciones de software a un grupo de actualizaciones de software nuevo.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Proceso para agregar manualmente las actualizaciones de software a un grupo de actualizaciones de software nuevo  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software** y haga clic en **Actualizaciones de software**. Seleccione las actualizaciones de software deseadas.  

2.  Haga clic en **Crear grupo de actualizaciones de software** en la cinta.  

3.  Especifique el nombre para el grupo de actualizaciones de software y, opcionalmente, incluya una descripción. Utilice un nombre y una descripción que proporcione información suficiente para determinar qué tipo de actualizaciones incluye el grupo de actualizaciones de software. Haga clic en **Crear**.  

4.  Seleccione el nodo **Grupos de actualizaciones de software** y el grupo de actualizaciones de software nuevo. Para mostrar la lista de actualizaciones en el grupo, haga clic en **Mostrar miembros** en la cinta.  



##  <a name="step-3-download-the-content-for-the-software-update-group"></a><a name="BKMK_3DownloadContent"></a> Paso 3: Descargar el contenido para el grupo de actualizaciones de software  

Antes de implementar las actualizaciones de software, descargue el contenido para las actualizaciones en el grupo de actualizaciones de software. Este paso le permite comprobar la disponibilidad del contenido en los puntos de distribución antes de implementar las actualizaciones de software. También le ayuda a evitar problemas inesperados con la distribución de contenido. Si omite este paso, como parte del proceso de implementación el sitio descarga el contenido y lo distribuye a los puntos de distribución. Utilice el siguiente procedimiento para descargar el contenido para las actualizaciones de software del grupo de actualizaciones de software.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Proceso para descargar el contenido para el grupo de actualizaciones de software
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Proceso para supervisar el estado del contenido
1. Para supervisar el estado del contenido para las actualizaciones de software, vaya al área de trabajo **Supervisión** en la consola de Configuration Manager. Expanda **Estado de distribución** y después seleccione el nodo **Estado de contenido**.  

2. Seleccione el paquete de actualizaciones de software que identificó previamente para descargar las actualizaciones de software en el grupo de actualizaciones de software.  

3. Haga clic en **Ver estado** en la cinta.  



##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_4DeployUpdateGroup"></a> Paso 4: Implementar el grupo de actualizaciones de software  

Después de determinar las actualizaciones que quiere implementar y agregarlas a un grupo de actualizaciones de software, implemente manualmente el grupo de actualizaciones de software.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Proceso para implementar manualmente las actualizaciones de software en un grupo de actualizaciones de software  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Actualizaciones de software** y seleccione el nodo **Grupo de actualizaciones de software**.  

2. Seleccione el grupo de actualizaciones de software que quiere implementar. En la cinta, haga clic en **Implementar**.   

3. En la página **General** del Asistente para implementar actualizaciones de software, configure las siguientes opciones:  

   -   **Nombre**: especifique el nombre de la implementación. La implementación debe tener un nombre único que describa su propósito y la diferencie respecto a otras implementaciones del sitio. Este campo de nombre tiene un límite de 256 caracteres. De forma predeterminada, Configuration Manager asigna automáticamente un nombre para la implementación con el siguiente formato: `Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Descripción**: especifique una descripción para la implementación. La descripción es opcional, pero proporciona información general sobre la implementación. Incluya cualquier otra información relevante que ayude a identificarla y diferenciarla entre otras en el sitio. El campo de descripción tiene un límite de 256 caracteres y tiene un valor en blanco de forma predeterminada.  

   -   **Actualización de software/Grupo de actualizaciones de software**: compruebe que la actualización de software que se muestra o el grupo de actualizaciones de software es el correcto.  

   -   **Seleccionar plantilla de implementación**: especifique si desea aplicar una plantilla de implementación guardada anteriormente. Configure una plantilla de implementación para guardar las propiedades de implementación de actualización de software comunes. Después aplíquela al implementar las actualizaciones de software en el futuro. Estas plantillas permiten ahorrar tiempo y garantizar la coherencia en implementaciones similares.  

   -   **Colección**: especifique la colección para la implementación. Los dispositivos de la colección reciben las actualizaciones de software en esta implementación.  

4. En la página **Configuración de implementación**, configure las siguientes opciones:  

   -   **Tipo de implementación**: especifique el tipo de implementación para la implementación de actualizaciones de software.  

       > [!IMPORTANT]  
       >  Una vez creada la implementación de actualización de software, no podrá cambiar el tipo de implementación.  

        - Seleccione **Requerida** para crear una implementación de actualizaciones de software obligatoria. Las actualizaciones de software se instalan automáticamente en los clientes antes de configurar la fecha límite de instalación.  

        - Seleccione **Disponible** para crear una implementación de actualizaciones de software opcional. Esta implementación está disponible para que los usuarios la instalen desde el Centro de software.  

       > [!NOTE]  
       >  Cuando implemente un grupo de actualizaciones de software implementado como **Requerido**, el cliente descarga el contenido en segundo plano y se respetará la configuración de BITS, si se ha configurado.  
       > 
       > Para los grupos de actualizaciones de software implementados como **Disponible**, el cliente descarga el contenido en primer plano y omite la configuración de BITS.  

   -   **Usar Wake-on-LAN para activar clientes para las implementaciones requeridas**: especifica si se debe habilitar Wake on LAN en la fecha límite. Wake on LAN envía paquetes de reactivación a equipos que requieran una o varias actualizaciones de software en la implementación. El sitio activa cualquier equipo que esté en modo de suspensión en la fecha límite de instalación para que se pueda iniciar la instalación. Los clientes que están en modo de suspensión, pero no requieren actualizaciones de software de la implementación, no se iniciarán. De forma predeterminada, esta opción no está habilitada. Solo está disponible para las implementaciones **requeridas**. Para poder usar esta opción, configure los equipos y las redes para Wake on LAN. Para obtener más información, vea [Cómo configurar Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

   -   **Nivel de detalle**: especifique el nivel de detalle de los mensajes de estado que los clientes notifican al sitio.  

5. En la página **Programación**, configure las siguientes opciones:  

   -   **Programar evaluación**: especifique cuándo evalúa Configuration Manager la hora disponible y las horas de fecha límite de instalación. Puede elegir entre usar Hora universal coordinada (UTC) o la hora local del equipo que ejecuta la consola de Configuration Manager.  

       - Al seleccionar **Hora local del cliente** aquí y luego **Lo antes posible** para **Horas de disponibilidad del software**, la hora actual en el equipo que ejecuta la consola de Configuration Manager se usa para evaluar cuándo hay actualizaciones disponibles. Este comportamiento es el mismo con la **fecha límite de instalación** y la hora a la que se instalan las actualizaciones en un cliente. Si el cliente está en otra zona horaria, estas acciones se producirán cuando la hora del cliente llegue a la hora de evaluación.  

   -   **Horas de disponibilidad del software**: seleccione una de las siguientes opciones para especificar cuándo estarán disponibles las actualizaciones de software para los clientes:  

       -   **Lo antes posible**: hace que las actualizaciones de software de la implementación estén disponibles para los clientes lo antes posible. Si se crea la implementación con esta opción seleccionada, Configuration Manager actualiza la directiva del cliente. En el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación y las actualizaciones de software están disponibles para la instalación.  

       -   **Hora específica**: hace que las actualizaciones de software incluidas en la implementación estén disponibles para los clientes en una fecha y hora concretas. Si se crea la implementación con esta opción habilitada, Configuration Manager actualiza la directiva del cliente. Con el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación. En cambio, las actualizaciones de software de la implementación no están disponibles para la instalación hasta después de la fecha y hora configurada.  

   -   **Fecha límite de instalación**: estas opciones solo están disponibles para las implementaciones **Requeridas**. Seleccione una de las siguientes opciones para especificar la fecha límite de instalación de las actualizaciones de software de la implementación  

       -   **Lo antes posible**: seleccione esta opción para que se instalen automáticamente las actualizaciones de software incluidas en la implementación lo antes posible.  

       -   **Hora específica**: seleccione esta opción para que las actualizaciones de software de la implementación se instalen automáticamente a una hora y en una fecha específicas.  

           - La hora de la fecha límite de instalación real es la hora de la fecha límite más una cantidad aleatoria de tiempo de hasta dos horas. La selección aleatoria reduce el posible impacto de los clientes de la recopilación que instalan las actualizaciones en la implementación a la misma hora.   

           - Para deshabilitar el retraso de la selección aleatoria de instalación para las actualizaciones de software requeridas, establezca la opción del cliente en **Deshabilitar selección aleatoria de fecha límite** en el grupo **Agente de equipo**. Para obtener más información, vea [Configuración de cliente de Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent).  

   -  **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario hasta el período de gracia definido en la configuración del cliente**: habilite esta opción para dar más tiempo a los usuarios para instalar las actualizaciones de software necesarias más allá de la fecha límite.  

       - Este comportamiento es normalmente necesario cuando un equipo ha estado apagado durante mucho tiempo y necesita instalar muchas aplicaciones o actualizaciones de software. Por ejemplo, cuando un usuario vuelve de vacaciones, tiene que esperar mucho tiempo mientras el cliente instala las implementaciones atrasadas.  

       - Configure este período de gracia con la propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** en la configuración del cliente. Para obtener más información, consulte la sección [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent). El período de gracia de cumplimiento se aplica a todas las implementaciones que tienen habilitada esta opción y que están destinadas a dispositivos en los que también se ha implementado la configuración del cliente.  

       - Después de la fecha límite, el cliente instala las actualizaciones de software en la primera ventana que no sea de empresa, configurada por el usuario, hasta ese período de gracia. No obstante, el usuario puede abrir el Centro de software e instalar las actualizaciones de software en cualquier momento. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas.  

6. En la página **Experiencia del usuario**, configure las siguientes opciones:  

   -   **Notificaciones de usuario**: especifique si quiere mostrar una notificación en el Centro de software según las **Horas de disponibilidad del software** configuradas. Esta opción también controla si se notifica a los usuarios en los equipos cliente. Para las implementaciones **disponibles**, no se puede seleccionar la opción **Ocultar en el Centro de software y ocultar todas las notificaciones**.  

   -   **Comportamiento de la fecha límite**: esta opción solo es configurable para las implementaciones **Requeridas**. Especifique los comportamientos cuando la implementación de actualizaciones de software alcanza la fecha límite fuera de las ventanas de mantenimiento definidas. Las opciones incluyen la posibilidad de instalar las actualizaciones de software y de realizar un reinicio del sistema tras la instalación. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md). 
  
       > [!Note]
       > Esto se aplica únicamente cuando la ventana de mantenimiento está configurada para el dispositivo cliente. Si no hay ninguna ventana de mantenimiento definida en el dispositivo, la actualización de la instalación y el reinicio siempre se realizarán después de la fecha límite.

   -   **Comportamiento de reinicio de dispositivo**: esta opción solo es configurable para las implementaciones **Requeridas**. Especifique si se debe suprimir el reinicio del sistema necesario para completar la instalación de actualizaciones en servidores y estaciones de trabajo.  

       > [!WARNING]  
       >  Suprimir los reinicios del sistema puede ser útil en entornos de servidor o si no quiere que los equipos de destino se reinicien de forma predeterminada. En cambio, esta opción puede dejar los equipos en un estado poco seguro. Permitir un reinicio forzado ayuda a asegurar la finalización inmediata de la instalación de la actualización de software.  

   -   **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: esta opción controla el comportamiento de instalación en los dispositivos Windows Embedded habilitados con un filtro de escritura. Elija esta opción para que los cambios se confirmen en la fecha límite de instalación o durante una ventana de mantenimiento. Al seleccionar esta opción, se necesita un reinicio y los cambios persisten en el dispositivo. En caso contrario, la actualización se instala, se aplica a la superposición temporal y se confirmará más tarde.  

       -  Al implementar una actualización de software en un dispositivo de Windows Embedded, asegúrese de que el dispositivo sea miembro de una colección que tenga configurada una ventana de mantenimiento.  

   - **Comportamiento de reevaluación de implementación de actualizaciones de software tras el reinicio**: seleccione esta opción para configurar las implementaciones de actualizaciones de software para que los clientes ejecuten un examen de cumplimiento de las actualizaciones de software inmediatamente después de que un cliente las instale y reinicie. Esta opción permite al cliente comprobar las actualizaciones adicionales que entran en vigor después de que el cliente se reinicie y luego las instala durante la misma ventana de mantenimiento.  

7. En la página **Alertas**, configure la forma en que Configuration Manager genera las alertas para esta implementación. Revise las alertas de las actualizaciones de software recientes de Configuration Manager en el nodo **Actualizaciones de software** del área de trabajo **Biblioteca de software**. Si también usa System Center Operations Manager, configure también sus alertas. Configure solo las alertas de las implementaciones **requeridas**.  

8. En la página **Configuración de descarga**, configure las siguientes opciones:  

    > [!NOTE]  
    >  Los clientes solicitan la ubicación del contenido desde un punto de administración para las actualizaciones de software de una implementación. El comportamiento de descarga depende de cómo se hayan configurado el punto de distribución, el paquete de implementación y las opciones de esta página.  

    - Especifique si los clientes deben descargar e instalar las actualizaciones al usar un punto de distribución desde un grupo vecino o los grupos de límites predeterminados del sitio.  

    - Especifique si los clientes deben descargar e instalar las actualizaciones desde un punto de distribución en el grupo de límites predeterminados del sitio, cuando el contenido para las actualizaciones de software no está disponible desde un punto de distribución en el grupo actual o en los grupos de límites vecinos.  

    - **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: especifique si desea habilitar el uso de BranchCache para descargas de contenido. Para obtener más información, vea [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). A partir de la versión 1802, BranchCache siempre está habilitado en los clientes. Esta configuración se eliminó, ya que los clientes usan BranchCache si el punto de distribución lo admite.  

    - **Si las actualizaciones de software no están disponibles en un punto de distribución del grupo de límites actual, vecino o del sitio, descargar el contenido de Microsoft Update**: seleccione esta opción para que los clientes conectados a la intranet descarguen las actualizaciones de software desde Microsoft Update si no están disponibles en los puntos de distribución. Los clientes basados en Internet siempre van a Microsoft Update para obtener el contenido de las actualizaciones de software.

    - Especifique si quiere permitir que los clientes descarguen después de la fecha límite de instalación cuando utilizan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión de uso medido.  

9. En la página **Paquete de implementación**, seleccione una de las siguientes opciones:  

    > [!Note]  
    > Si ya ha realizado el [Paso 3: Descargar el contenido para el grupo de actualizaciones de software](#BKMK_3DownloadContent), el asistente no mostrará las páginas **Paquete de implementación**, **Puntos de distribución** y **Selección del idioma**. Vaya a la página [Resumen](#bkmk_summary) del asistente.  
    > 
    >  Las actualizaciones de software que ya se descargaron en la biblioteca de contenido del servidor del sitio no se descargan de nuevo. Este comportamiento es verdadero, aunque se cree un paquete de implementación nuevo para las actualizaciones de software. Si ya se descargaron todas las actualizaciones de software, el asistente pasa a la página [Resumen](#bkmk_summary).  

    - **Seleccione un paquete de implementación**: agregue estas actualizaciones a un paquete de implementación existente.  

    - **Crear un nuevo paquete de implementación**: agregue estas actualizaciones a un paquete de implementación nuevo. Configure las siguientes opciones adicionales:  

        -  **Nombre**: especifique el nombre del paquete de implementación. Use un nombre único que describa el contenido del paquete. Está limitado a 50 caracteres.  

        -  **Descripción**: especifique una descripción que proporcione información sobre el paquete de implementación. La descripción opcional está limitada a 127 caracteres.  

        -  **Origen del paquete**: especifique la ubicación de los archivos de origen de la actualización de software. Escriba una ruta de acceso a la red para la ubicación de origen (por ejemplo, `\\server\sharename\path`) o haga clic en **Examinar** para buscar la ubicación de red. Cree la carpeta compartida para los archivos de origen del paquete de implementación antes de continuar con la página siguiente.  

            - No se puede usar la ubicación especificada como origen de otro paquete de implementación de software.  

            - Puede cambiar la ubicación de origen del paquete en las propiedades del paquete de implementación después de que Configuration Manager cree el paquete de implementación. Si lo hace, copie primero el contenido desde el origen del paquete original a la nueva ubicación de origen del paquete.  

            -  La cuenta de equipo del proveedor de SMS y el usuario que ejecuta el asistente para descargar actualizaciones de software deben tener permisos de **Escritura** en la ubicación de descarga. Restrinja el acceso a la ubicación de descarga. Esta restricción reduce el riesgo de que los atacantes alteren los archivos de origen de actualización de software.  

        -  **Prioridad de envío**: especifique la prioridad de envío del paquete de implementación. Configuration Manager usa esta prioridad cuando envía el paquete a los puntos de distribución. Los paquetes de implementación se envían en orden de prioridad: alta, media o baja. Los paquetes con prioridades idénticas se envían en el orden en que se crearon. Si no hay ningún trabajo pendiente, el paquete se procesa inmediatamente sin tener en cuenta su prioridad.  

        - **Habilitar replicación diferencial binaria**: habilite esta opción para minimizar el tráfico de red entre sitios. La replicación diferencial binaria (BDR) solo actualiza el contenido que ha cambiado en el paquete, en lugar de actualizar todo el contenido del paquete. Para obtener más información, vea [Replicación diferencial binaria](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Sin paquete de implementación**: a partir de la versión 1806, las actualizaciones de software se implementan en los dispositivos sin antes descargar y distribuir el contenido a los puntos de distribución. Esta configuración es útil cuando se trabaja con contenido de actualización extremadamente grande. También puede usarla cuando quiera que los clientes siempre obtengan contenido desde el servicio en la nube de Microsoft Update. En este escenario, los clientes también pueden descargar el contenido desde los equipos del mismo nivel que ya tienen el contenido necesario. El cliente de Configuration Manager sigue administrando la descarga del contenido, por lo que puede usar la característica de caché del mismo nivel de Configuration Manager u otras tecnologías como, por ejemplo, Optimización de distribución. Esta característica es compatible con cualquier tipo de actualización admitida por la administración de actualizaciones de software de Configuration Manager, incluidas las actualizaciones de Windows y Office.<!--1357933-->  

10. En la página **Puntos de distribución**, especifique los puntos de distribución o los grupos de puntos de distribución que hospedan los archivos de actualización de software. Para más información sobre los puntos de distribución, vea [Distribution point configurations (Configuraciones de puntos de distribución)](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!Note]  
    > Si ya ha realizado el [Paso 3: Descargar el contenido para el grupo de actualizaciones de software](#BKMK_3DownloadContent), el asistente no mostrará las páginas **Paquete de implementación**, **Puntos de distribución** y **Selección del idioma**. Vaya a la página [Resumen](#bkmk_summary) del asistente.  

11. En la página **Ubicación de descarga**, especifique si los archivos de actualización de software se van a descargar desde Internet o desde la red local. Configure las siguientes opciones:  

    -   **Descargar actualizaciones de software de Internet**: seleccione esta opción para descargar las actualizaciones de software desde una ubicación especificada de Internet. Esta opción está habilitada de forma predeterminada.  

    -   **Descargar actualizaciones de software de una ubicación en mi red**: seleccione esta opción para descargar las actualizaciones de software desde un directorio local o una carpeta compartida. Esta opción es útil si el equipo que ejecuta el asistente no tiene acceso a Internet. Cualquier equipo con acceso a Internet puede descargar de forma preliminar las actualizaciones de software. Después, almacénelas en una ubicación en la red local que sea accesible desde el equipo que ejecuta al asistente.  

12. En la página **Selección del idioma**, seleccione los idiomas para los que el sitio descarga las actualizaciones de software seleccionadas. El sitio solo descarga estas actualizaciones si están disponibles en los idiomas seleccionados. Las actualizaciones de software que no son específicas de un idioma se descargan siempre. De forma predeterminada, el asistente selecciona los idiomas que se han configurado en las propiedades del punto de actualización de software. Debe seleccionar, como mínimo, un idioma para poder pasar a la página siguiente. Si solo se seleccionan idiomas que una actualización de software no admite, la descarga no se completa para esa actualización.  

    > [!Note]  
    > Si ya ha realizado el [Paso 3: Descargar el contenido para el grupo de actualizaciones de software](#BKMK_3DownloadContent), el asistente no mostrará las páginas **Paquete de implementación**, **Puntos de distribución** y **Selección del idioma**. Vaya a la página [Resumen](#bkmk_summary) del asistente.  

13. <a name="bkmk_summary"></a> En la página **Resumen**, revise la configuración. Para guardar la configuración en una plantilla de implementación, haga clic en **Guardar como plantilla**. Escriba un nombre, seleccione la configuración que quiere incluir en la plantilla y, después, haga clic en **Guardar**. Para cambiar una configuración, haga clic en la página correspondiente del asistente y cámbiela.  

    -  El nombre de plantilla puede incluir caracteres ASCII alfanuméricos, `\` (barra diagonal inversa) o `'` (comillas tipográficas).  

14. Haga clic en **Siguiente** para implementar la actualización de software.  

    Después de completar el asistente, Configuration Manager descarga las actualizaciones de software en la biblioteca de contenido en el servidor de sitio. Luego, distribuye el contenido a los puntos de distribución configurados e implementa el grupo de actualizaciones de software en clientes de la colección de destino. Para obtener más información sobre el proceso de implementación, consulte [Proceso de implementación de actualizaciones de software](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Pasos siguientes
[Supervisar actualizaciones de software](monitor-software-updates.md)
