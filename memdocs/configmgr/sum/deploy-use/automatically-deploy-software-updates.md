---
title: Implementar actualizaciones de software automáticamente
titleSuffix: Configuration Manager
description: Implementación automática de actualizaciones de software usando reglas de implementación automática (ADR).
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: bf172c4cb34a17ac793ea5568b0505505baf97a0
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709441"
---
#  <a name="automatically-deploy-software-updates"></a>Implementar actualizaciones de software automáticamente  

*Se aplica a: Configuration Manager (rama actual)*

Use una regla de implementación automática (ADR) en lugar de agregar actualizaciones nuevas a un grupo de actualización de software existente. Normalmente, las ADR se usan para implementar actualizaciones de software mensuales (también conocidas como actualizaciones "Patch Tuesday") y para administrar las actualizaciones de definiciones de Endpoint Protection. Si necesita ayuda para determinar qué método de implementación es el adecuado para usted, vea [Deploy software updates](deploy-software-updates.md) (Implementación de actualizaciones de software).


##  <a name="create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Crear una regla de implementación automática (ADR)  
Las actualizaciones de software se pueden aprobar e implementar automáticamente mediante una ADR. La regla puede agregar las actualizaciones de software a un nuevo grupo de actualización de software cada vez que dicha regla se ejecute o agregar actualizaciones de software a un grupo existente. Cuando una regla se ejecuta y agrega actualizaciones de software a un grupo existente, la regla quita todas las actualizaciones del grupo. Después, agrega al grupo las actualizaciones que cumplen los criterios definidos. 

> [!WARNING]  
>  Antes de crear una ADR por primera vez, compruebe que el sitio ha completado la sincronización de las actualizaciones de software. Este paso es importante al ejecutar Configuration Manager en un idioma distinto del inglés. Las clasificaciones de actualizaciones de software se muestran en inglés antes de la primera sincronización y luego se muestran en el idioma localizado una vez completada la sincronización de las actualizaciones de software. Las reglas creadas antes de sincronizar las actualizaciones de software podrían no funcionar correctamente tras la sincronización porque la cadena de texto podría no coincidir.  


### <a name="process-to-create-an-adr"></a><a name="bkmk_adr-process"></a> Proceso para crear una ADR  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Actualizaciones de software** y seleccione el nodo **Reglas de implementación automática**.  

2.  En la cinta, haga clic en **Crear regla de implementación automática**.  

3.  En la página **General** del Asistente para crear regla de implementación automática, configure las siguientes opciones:  

    -   **Nombre**: especifica el nombre de la ADR. El nombre debe ser único, describir el objetivo de la regla e identificarla entre el resto de reglas del sitio de Configuration Manager.  

    -   **Descripción**: especifica una descripción para la ADR. La descripción debería proporcionar información general de la regla implementación y otra información relevante que ayude a diferenciar esta regla de otras. El campo de descripción es opcional, tiene un límite de 256 caracteres y tiene un valor en blanco de forma predeterminada.  

    -   **Plantilla**: seleccione una plantilla de implementación para especificar si se deben aplicar configuraciones de ADR que se guardaron anteriormente. Configure una plantilla de implementación que contenga varias propiedades de implementación de actualización comunes que pueda usar para crear ADR adicionales. Estas plantillas permiten ahorrar tiempo y garantizar la coherencia en implementaciones similares. Seleccione una de las siguientes plantillas de implementación de actualización de software integradas:  

         - La plantilla **Patch Tuesday** proporciona opciones de configuración comunes para implementar actualizaciones de software en un ciclo mensual.  

         - La plantilla **Actualizaciones de cliente de Office 365** proporciona opciones de configuración comunes que se usarán al implementar las actualizaciones para los clientes de Office 365 Pro Plus.
             > [!Note]
             > A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Si las ADR se basan en la propiedad "Title", deberá editarlo a partir del 9 de junio de 2020. `Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)` es un ejemplo del nuevo título. Para más información sobre cómo modificar las reglas de implementación automática (ADR) para el cambio de título, consulte el artículo sobre [canales de actualización para aplicaciones de Microsoft 365](manage-office-365-proplus-updates.md#bkmk_channel). Para más información sobre el cambio de nombre, consulte [Cambio de nombre para Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change).

         - La plantilla **Actualizaciones de SCEP y Antivirus de Windows Defender** proporciona opciones de configuración comunes que se usarán cuando implemente actualizaciones de definiciones de Endpoint Protection.  

    -   **Colección**: especifica la recopilación de destino que se utilizará para la implementación. los miembros de la recopilación reciben las actualizaciones de software definidas en la implementación.  

    -   Decida si desea agregar las actualizaciones de software a un grupo de actualizaciones de software nuevo o a uno existente. En la mayoría de los casos, elegirá crear un nuevo grupo de actualizaciones de software cuando se ejecuta la regla de implementación automática. Si la regla se ejecuta con una programación más exigente, podría optar por un grupo existente. Por ejemplo, si ejecuta la regla diariamente para las actualizaciones de definiciones, podría agregar las actualizaciones de software a un grupo de actualizaciones de software existente.  

    -   **Habilitar la implementación después de ejecutar la regla**: indica si se habilitará la implementación de actualizaciones de software después de la ejecución de la ADR. Considere las opciones siguientes para esta configuración:  

        -   Cuando se habilita la implementación, las actualizaciones que cumplen los criterios definidos de la regla se agregan a un grupo de actualizaciones de software. El contenido de actualización de software se descarga según sea necesario. El contenido se copia en los puntos de distribución especificados y las actualizaciones se implementan en los clientes de la recopilación de destino.  

        -   Cuando no habilita la implementación, las actualizaciones que cumplen los criterios definidos de la regla se agregan a un grupo de actualizaciones de software. El contenido de implementación de actualización de software se descarga, según sea necesario, y se distribuye a los puntos de distribución especificados. El sitio crea una implementación deshabilitada en el grupo de actualizaciones de software para impedir que las actualizaciones se implementen en los clientes. Esta opción proporciona tiempo para preparar la implementación de las actualizaciones, comprobar que las actualizaciones que cumplen los criterios son adecuadas y habilitar la implementación.  

4.  En la página **Configuración de implementación**, configure las siguientes opciones:  

    -   **Usar Wake on LAN para activar clientes para las implementaciones necesarias**: especifica si se debe habilitar Wake on LAN en la fecha límite. Wake on LAN envía paquetes de reactivación a equipos que requieran una o varias actualizaciones de software en la implementación. El sitio activa cualquier equipo que esté en modo de suspensión en la fecha límite de instalación para que se pueda iniciar la instalación. Los clientes que están en modo de suspensión, pero no requieren actualizaciones de software de la implementación, no se iniciarán. De forma predeterminada, esta opción no está habilitada. Para poder usar esta opción, configure los equipos y las redes para Wake on LAN. Para obtener más información, vea [Cómo configurar Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    -   **Nivel de detalle**: especifique el nivel de detalle de los mensajes de estado de aplicación de actualizaciones que notifican los clientes.  

        > [!IMPORTANT]  
        >  Cuando implemente actualizaciones de definiciones, establezca el nivel de detalle en **Solo error** para que el cliente notifique un mensaje de estado solo cuando se produzca un error en la actualización de definiciones. De lo contrario, el número de mensajes de estado que notifique el cliente podría afectar al rendimiento en el servidor del sitio.  
        
        > [!NOTE]  
        > El nivel de detalle **Solo error** no envía los mensajes de estado de cumplimiento requeridos para el seguimiento de los reinicios pendientes.

    -   **Configuración de términos de licencia**: especifique si desea implementar automáticamente actualizaciones de software con los términos de licencia asociados. Algunas actualizaciones de software incluyen términos de licencia. Cuando se implementan automáticamente actualizaciones de software, no se muestran los términos de licencia, y no se da la opción de aceptarlos. Puede elegir implementar automáticamente todas las actualizaciones de software independientemente de si tienen términos de licencia asociados, o bien implementar solo las actualizaciones que no tengan términos de licencia asociados.  

         - Para revisar los términos de licencia de una actualización de software, selecciónela en el nodo **Todas las actualizaciones de software** del área de trabajo **Biblioteca de software**. En la cinta, haga clic en **Revisar la licencia**.    

         - Para buscar actualizaciones de software con términos de licencia asociados, agregue la columna **Términos de licencia** al panel de resultados del nodo **Todas las actualizaciones de software**. Haga clic en el encabezado de la columna para ordenar por actualizaciones de software con términos de licencia.  

5.  En la página **Actualizaciones de software**, configure los criterios para las actualizaciones de software que la regla de implementación automática recupera y agrega al grupo de actualizaciones de software.  

     - El límite para las actualizaciones de software en la regla de implementación automática es de 1000 actualizaciones de software.  

     - Si es necesario, filtre por el tamaño del contenido de las actualizaciones de software en las reglas de implementación automática. Para más información, vea [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems (Configuration Manager y mantenimiento simplificado de Windows en sistemas operativos de nivel inferior)](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056).  

     - A partir de la versión 1910, puede usar **Implementado** como un filtro de actualización en las reglas de implementación automática (ADR). Este filtro ayuda a identificar las actualizaciones nuevas que se deben implementar en las colecciones de prueba o piloto. El filtro de actualización de software también puede ayudar a evitar volver a implementar actualizaciones anteriores. 
         - Cuando se usa **Implementado** como filtro, tenga en cuenta que es posible que ya haya implementado la actualización en otra colección, como una colección de prueba o piloto. <!--4852033-->
     - A partir de la versión 1806, está disponible un filtro de propiedad para **Arquitectura**. Use este filtro para excluir arquitecturas como Itanium y ARM64 que son menos comunes. Recuerde que hay aplicaciones de 32 bits (x86) y componentes que se ejecutan en sistemas de 64 bits (x64). A menos que esté seguro de que no necesita x86, habilítelo también cuando elija x64.<!--1322266-->  

    > [!NOTE]  
    > **Windows 10, versión 1903 y posteriores** se ha agregado a Microsoft Update como un producto propio en lugar de formar parte del producto **Windows 10** como en las versiones anteriores. Este cambio le obligaba a realizar una serie de pasos manuales para asegurarse de que los clientes veían estas actualizaciones. Se ha intentado reducir el número de pasos manuales que debe seguir para el nuevo producto en Configuration Manager, versión 1906. Para obtener más información, vea [Configuración de productos para versiones de Windows 10](../get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later). <!--4682946-->


6. En la página **Programación de evaluación**, especifique si quiere habilitar la regla de implementación automática para que se ejecute en función de una programación. Si la habilita, haga clic en **Personalizar** para configurar la programación periódica.  

    - La configuración de la hora de inicio para la programación se basa en la hora local del equipo que ejecuta la consola de Configuration Manager.  

    - La evaluación de regla de implementación automática puede ejecutar tres veces al día.  

    - No establezca nunca la programación de evaluación con una frecuencia que supere la programación de sincronización de actualizaciones de software. Esta página muestra la programación de sincronización de punto de actualización de software para que se pueda determinar la frecuencia de la programación de evaluación.  

    - Para ejecutar manualmente la regla de implementación automática, seleccione la regla en el nodo **Regla de implementación automática** de la consola y después haga clic en **Ejecutar ahora** en la cinta.  

    - A partir de la versión 1802, se pueden programar ADR para evaluar el desplazamiento con respecto a un día base. Por ejemplo, si Patch Tuesday en su caso cae en miércoles, establezca la programación de evaluación para el segundo martes del mes con un desplazamiento de un día.<!--1357133-->  
        - Al programar la evaluación con un desplazamiento durante la última semana del mes, si el desplazamiento elegido continúa al mes siguiente, el sitio programará la evaluación para el último día del mes.<!--506731-->  
        ![Desplazamiento de la programación de evaluación personalizada de ADR desde el día base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  En la página **Programación de implementación**, configure las siguientes opciones:  

    -   **Programar evaluación**: especifique cuándo evalúa Configuration Manager la hora disponible y las horas de fecha límite de instalación. Puede elegir entre usar Hora universal coordinada (UTC) o la hora local del equipo que ejecuta la consola de Configuration Manager.  

          - Al seleccionar **Hora local del cliente** aquí y luego **Lo antes posible** para **Horas de disponibilidad del software**, la hora actual en el equipo que ejecuta la consola de Configuration Manager se usa para evaluar cuándo hay actualizaciones disponibles. Este comportamiento es el mismo con la **fecha límite de instalación** y la hora a la que se instalan las actualizaciones en un cliente. Si el cliente está en otra zona horaria, estas acciones se producirán cuando la hora del cliente llegue a la hora de evaluación.  

    -   **Horas de disponibilidad del software**: seleccione una de las siguientes opciones para especificar cuándo estarán disponibles las actualizaciones de software para los clientes:  

        -   **Lo antes posible**: hace que las actualizaciones de software de la implementación estén disponibles para los clientes lo antes posible. Si se crea la implementación con esta opción seleccionada, Configuration Manager actualiza la directiva del cliente. En el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación y las actualizaciones de software están disponibles para la instalación.  

        -   **Hora específica**: hace que las actualizaciones de software incluidas en la implementación estén disponibles para los clientes en una fecha y hora concretas. Si se crea la implementación con esta opción habilitada, Configuration Manager actualiza la directiva del cliente. Con el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación. En cambio, las actualizaciones de software de la implementación no están disponibles para la instalación hasta después de la fecha y hora configurada.  

    -   **Fecha límite de instalación**: seleccione una de las siguientes opciones para especificar la fecha límite de instalación de las actualizaciones de software de la implementación:  

        -   **Lo antes posible**: seleccione esta opción para que se instalen automáticamente las actualizaciones de software incluidas en la implementación lo antes posible.  

        -   **Hora específica**: seleccione esta opción para que las actualizaciones de software de la implementación se instalen automáticamente a una hora y en una fecha específicas. Configuration Manager determina la fecha límite para instalar actualizaciones de software, para lo cual agrega el intervalo **Hora específica** establecido a **Horas de disponibilidad del software**.  

             - La hora de la fecha límite de instalación real es la hora de la fecha límite más una cantidad aleatoria de tiempo de hasta dos horas. La selección aleatoria reduce el posible impacto de los clientes de la recopilación que instalan las actualizaciones en la implementación a la misma hora.  

             - Para deshabilitar el retraso de la selección aleatoria de instalación para las actualizaciones de software requeridas, establezca la opción del cliente en **Deshabilitar selección aleatoria de fecha límite** en el grupo **Agente de equipo**. Para obtener más información, vea [Configuración de cliente de Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    -  **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario hasta el período de gracia definido en la configuración del cliente**: habilite esta opción para dar más tiempo a los usuarios para instalar las actualizaciones de software necesarias más allá de la fecha límite.  

        - Este comportamiento es normalmente necesario cuando un equipo ha estado apagado durante mucho tiempo y necesita instalar muchas aplicaciones o actualizaciones de software. Por ejemplo, cuando un usuario vuelve de vacaciones, tiene que esperar mucho tiempo mientras el cliente instala las implementaciones atrasadas.  

        - Configure este período de gracia con la propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** en la configuración del cliente. Para obtener más información, consulte la sección [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent). El período de gracia de cumplimiento se aplica a todas las implementaciones que tienen habilitada esta opción y que están destinadas a dispositivos en los que también se ha implementado la configuración del cliente.  

        - Después de la fecha límite, el cliente instala las actualizaciones de software en la primera ventana que no sea de empresa, configurada por el usuario, hasta ese período de gracia. No obstante, el usuario puede abrir el Centro de software e instalar las actualizaciones de software en cualquier momento. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas.  

8. En la página **Experiencia del usuario**, configure las siguientes opciones:  

    -   **Notificaciones de usuario**: especifique si quiere mostrar una notificación en el Centro de software según las **Horas de disponibilidad del software** configuradas. Esta configuración también controla si se debe notificar a los usuarios en los clientes.  

    -   **Comportamiento de la fecha límite**: Especifique los comportamientos cuando la implementación de actualizaciones de software alcanza la fecha límite fuera de las ventanas de mantenimiento definidas. Las opciones incluyen la posibilidad de instalar las actualizaciones de software y de realizar un reinicio del sistema tras la instalación. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  
        
        > [!Note]
        > Esto se aplica únicamente cuando la ventana de mantenimiento está configurada para el dispositivo cliente. Si no hay ninguna ventana de mantenimiento definida en el dispositivo, la actualización de la instalación y el reinicio siempre se realizarán después de la fecha límite.

    -   **Comportamiento de reinicio de dispositivo**: Especifique si se debe suprimir el reinicio del sistema necesario para completar la instalación de actualizaciones en servidores y estaciones de trabajo.  

        > [!WARNING]  
        >  Suprimir los reinicios del sistema puede ser útil en entornos de servidor o si no quiere que los equipos de destino se reinicien de forma predeterminada. En cambio, esta opción puede dejar los equipos en un estado poco seguro. Permitir un reinicio forzado ayuda a asegurar la finalización inmediata de la instalación de la actualización de software.  

    -   **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: esta opción controla el comportamiento de instalación en los dispositivos Windows Embedded habilitados con un filtro de escritura. Elija esta opción para que los cambios se confirmen en la fecha límite de instalación o durante una ventana de mantenimiento. Al seleccionar esta opción, se necesita un reinicio y los cambios persisten en el dispositivo. En caso contrario, la actualización se instala, se aplica a la superposición temporal y se confirmará más tarde.  

           -  Al implementar una actualización de software en un dispositivo de Windows Embedded, asegúrese de que el dispositivo sea miembro de una colección que tenga configurada una ventana de mantenimiento.  

    - **Comportamiento de reevaluación de implementación de actualizaciones de software tras el reinicio**: seleccione esta opción para configurar las implementaciones de actualizaciones de software para que los clientes ejecuten un examen de cumplimiento de las actualizaciones de software inmediatamente después de que un cliente las instale y reinicie. Esta opción permite al cliente comprobar las actualizaciones adicionales que entran en vigor después de que el cliente se reinicie y luego las instala durante la misma ventana de mantenimiento.  

9. En la página **Alertas**, configure la forma en que Configuration Manager genera las alertas para esta implementación. Revise las alertas de las actualizaciones de software recientes de Configuration Manager en el nodo **Actualizaciones de software** del área de trabajo **Biblioteca de software**. Si también usa System Center Operations Manager, configure también sus alertas.  

10. En la página **Configuración de descarga**, configure las siguientes opciones:  

    - Especifique si los clientes deben descargar e instalar las actualizaciones al usar un punto de distribución desde un grupo vecino o los grupos de límites predeterminados del sitio.  

    - Especifique si los clientes deben descargar e instalar las actualizaciones desde un punto de distribución en el grupo de límites predeterminados del sitio, cuando el contenido para las actualizaciones de software no está disponible desde un punto de distribución en el grupo actual o en los grupos de límites vecinos.  

    - **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: especifique si desea habilitar el uso de BranchCache para descargas de contenido. Para obtener más información, vea [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). A partir de la versión 1802, BranchCache siempre está habilitado en los clientes. Esta configuración se eliminó, ya que los clientes usan BranchCache si el punto de distribución lo admite.  

    - **Si las actualizaciones de software no están disponibles en un punto de distribución del grupo de límites actual, vecino o del sitio, descargar el contenido de Microsoft Update**: seleccione esta opción para que los clientes conectados a la intranet descarguen las actualizaciones de software desde Microsoft Update si no están disponibles en los puntos de distribución. Los clientes basados en Internet siempre van a Microsoft Update para obtener el contenido de las actualizaciones de software.  

    - Especifique si quiere permitir que los clientes descarguen después de la fecha límite de instalación cuando utilizan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión de uso medido.  

    > [!NOTE]  
    >  Los clientes solicitan la ubicación del contenido desde un punto de administración para las actualizaciones de software de una implementación. El comportamiento de descarga depende de cómo se hayan configurado el punto de distribución, el paquete de implementación y las opciones de esta página.   

11. En la página **Paquete de implementación**, seleccione una de las siguientes opciones:  

    - **Seleccione un paquete de implementación**: agregue estas actualizaciones a un paquete de implementación existente.  

    - **Crear un nuevo paquete de implementación**: agregue estas actualizaciones a un paquete de implementación nuevo. Configure las siguientes opciones adicionales:  

        -  **Nombre**: especifique el nombre del paquete de implementación. Use un nombre único que describa el contenido del paquete. Está limitado a 50 caracteres.  

        -  **Descripción**: especifique una descripción que proporcione información sobre el paquete de implementación. La descripción opcional está limitada a 127 caracteres.  

        -  **Origen del paquete**: especifica la ubicación de los archivos de origen de la actualización de software. Escriba una ruta de acceso a la red para la ubicación de origen (por ejemplo, `\\server\sharename\path`) o haga clic en **Examinar** para buscar la ubicación de red. Cree la carpeta compartida para los archivos de origen del paquete de implementación antes de continuar con la página siguiente.  

            - No se puede usar la ubicación especificada como origen de otro paquete de implementación de software.  

            - Puede cambiar la ubicación de origen del paquete en las propiedades del paquete de implementación después de que Configuration Manager cree el paquete de implementación. Si lo hace, copie primero el contenido desde el origen del paquete original a la nueva ubicación de origen del paquete.  

            -  La cuenta de equipo del proveedor de SMS y el usuario que ejecuta el asistente para descargar actualizaciones de software deben tener permisos de **Escritura** en la ubicación de descarga. Restrinja el acceso a la ubicación de descarga. Esta restricción reduce el riesgo de que los atacantes alteren los archivos de origen de actualización de software.  

        -  **Prioridad de envío**: especifique la prioridad de envío del paquete de implementación. Configuration Manager usa esta prioridad cuando envía el paquete a los puntos de distribución. Los paquetes de implementación se envían en orden de prioridad: alta, media o baja. Los paquetes con prioridades idénticas se envían en el orden en que se crearon. Si no hay ningún trabajo pendiente, el paquete se procesa inmediatamente sin tener en cuenta su prioridad.  

        - **Habilitar replicación diferencial binaria**: habilite esta opción para minimizar el tráfico de red entre sitios. La replicación diferencial binaria (BDR) solo actualiza el contenido que ha cambiado en el paquete, en lugar de actualizar todo el contenido del paquete. Para obtener más información, vea [Replicación diferencial binaria](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Sin paquete de implementación**: a partir de la versión 1806, las actualizaciones de software se implementan en los dispositivos sin antes descargar y distribuir el contenido a los puntos de distribución. Esta configuración es útil cuando se trabaja con contenido de actualización extremadamente grande. También puede usarla cuando quiera que los clientes siempre obtengan contenido desde el servicio en la nube de Microsoft Update. En este escenario, los clientes también pueden descargar el contenido desde los equipos del mismo nivel que ya tienen el contenido necesario. El cliente de Configuration Manager sigue administrando la descarga del contenido, por lo que puede usar la característica de caché del mismo nivel de Configuration Manager u otras tecnologías como, por ejemplo, Optimización de distribución. Esta característica es compatible con cualquier tipo de actualización admitida por la administración de actualizaciones de software de Configuration Manager, incluidas las actualizaciones de Windows y Office.<!--1357933-->  

        > [!Note]  
        > Una vez que seleccione esta opción y aplique la configuración, ya no podrá cambiarse. Las demás opciones están atenuadas.<!--SCCMDocs-pr issue 3003-->  

12. En la página **Puntos de distribución**, especifique los puntos de distribución o los grupos de puntos de distribución que hospedan los archivos de actualización de software. Para más información sobre los puntos de distribución, vea [Distribution point configurations (Configuraciones de puntos de distribución)](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Esta página sólo está disponible cuando se crea un nuevo paquete de implementación de actualizaciones de software.  
  

13. En la página **Ubicación de descarga**, especifique si los archivos de actualización de software se van a descargar desde Internet o desde la red local. Configure las siguientes opciones:  

    -   **Descargar actualizaciones de software de Internet**: seleccione esta opción para descargar las actualizaciones de software desde una ubicación especificada de Internet. Esta opción está habilitada de forma predeterminada.  

    -   **Descargar actualizaciones de software de una ubicación en mi red**: seleccione esta opción para descargar las actualizaciones de software desde un directorio local o una carpeta compartida. Esta opción es útil si el equipo que ejecuta el asistente no tiene acceso a Internet. Cualquier equipo con acceso a Internet puede descargar de forma preliminar las actualizaciones de software. Después, almacénelas en una ubicación en la red local que sea accesible desde el equipo que ejecuta al asistente. Otro escenario podría ser cuando se descarga contenido publicado a través de System Center Updates Publisher o una solución de revisión de terceros. El recurso compartido de contenido de WSUS en el punto de actualización de software de nivel superior se puede especificar como la ubicación de red desde la que se va a descargar, como, por ejemplo, `\\server\WsusContent`. <!--memdocs-issue-211-->

14. En la página **Selección del idioma**, seleccione los idiomas para los que el sitio descarga las actualizaciones de software seleccionadas. El sitio solo descarga estas actualizaciones si están disponibles en los idiomas seleccionados. Las actualizaciones de software que no son específicas de un idioma se descargan siempre. De forma predeterminada, el asistente selecciona los idiomas que se han configurado en las propiedades del punto de actualización de software. Debe seleccionar, como mínimo, un idioma para poder pasar a la página siguiente. Si solo se seleccionan idiomas que una actualización de software no admite, la descarga no se completa para esa actualización.  

15. En la página **Resumen** , revise la configuración. Para guardar la configuración en una plantilla de implementación, haga clic en **Guardar como plantilla**. Escriba un nombre, seleccione la configuración que quiere incluir en la plantilla y, después, haga clic en **Guardar**. Para cambiar una configuración, haga clic en la página correspondiente del asistente y cámbiela.  

    -  El nombre de plantilla puede incluir caracteres ASCII alfanuméricos, `\` (barra diagonal inversa) o `'` (comillas tipográficas).  

16. Haga clic en **Siguiente** crear la regla de implementación automática (ADR).  

Después de completar el asistente, se ejecuta la ADR. Agrega las actualizaciones de software que cumplen los criterios especificados a un grupo de actualizaciones de software. Después, la ADR descarga las actualizaciones de la biblioteca de contenido en el servidor de sitio y las distribuye a los puntos de distribución configurados. Luego, la ADR implementa el grupo de actualizaciones de software en los clientes de la recopilación de destino.  



##  <a name="add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a> Agregar una nueva implementación a una ADR existente  

Después de crear una ADR, agregue implementaciones adicionales a la regla. Esta acción le ayuda a administrar la complejidad de la implementación de varias actualizaciones en diferentes recopilaciones. Cada nueva implementación ofrece todas las funcionalidades y la experiencia completa de supervisión de la implementación.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Proceso para agregar una nueva implementación a una ADR existente  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Actualizaciones de software**, seleccione el nodo **Reglas de implementación automática** y después seleccione la regla deseada.  

2.  En la cinta, haga clic en **Agregar implementación**.   

3.  En la página **Colección** del Asistente para agregar implementación, configure las opciones disponibles de forma similar a la página **General** del Asistente para crear regla de implementación automática. Para obtener más información, consulte la sección anterior en el [Proceso para crear una ADR](#bkmk_adr-process). El resto del Asistente para agregar implementación incluye las páginas siguientes, que también coinciden con una descripción detallada anterior:  

     - Configuración de implementación
     - Programación de implementación
     - Experiencia del usuario
     - Alertas
     - Configuración de descarga  

Las implementaciones también se pueden agregar mediante programación con los cmdlets de Windows PowerShell. Para obtener una descripción completa del uso de este método, vea [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment).

Para obtener más información sobre el proceso de implementación, consulte [Proceso de implementación de actualizaciones de software](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Pasos siguientes
[Supervisar actualizaciones de software](monitor-software-updates.md)
