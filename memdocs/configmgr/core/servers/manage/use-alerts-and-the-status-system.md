---
title: Alertas y el sistema de estado
titleSuffix: Configuration Manager
description: Configure alertas y use el sistema de estado para mantenerse informado del estado de la implementación de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c066a61380e09961192bcbe7192e2e945341c97c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704283"
---
# <a name="use-alerts-and-the-status-system-for-configuration-manager"></a>Usar alertas y el sistema de estado de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configure alertas y use el sistema de estado integrado para mantenerse informado del estado de la implementación de Configuration Manager.  


##  <a name="status-system"></a><a name="bkmk_Status"></a> Sistema de estado  
 Todos los componentes de sitio principales generan mensajes de estado que proporcionan comentarios sobre las operaciones de sitio y de jerarquía.    Esta información puede mantenerle informado sobre el estado de los distintos procesos de sitio. Puede ajustar el sistema de alertas para ignorar el ruido de los problemas conocidos y aumentar la visibilidad anticipada de otros problemas que pueden requerir su atención.  

 De forma predeterminada, el sistema de estado de Configuration Manager funciona sin necesidad de configuración mediante una configuración adecuada para la mayoría de los entornos. Sin embargo, puede configurar lo siguiente:  

-   **Generadores de resumen de estado:** puede editar los generadores de resumen de estado en cada sitio para controlar la frecuencia de los mensajes de estado que generan un cambio de indicador de estado para los cuatro generadores de resumen siguientes:  

    -   Generador de resumen de implementación de aplicación  

    -   Generador de resumen de estadísticas de aplicación  

    -   Generador de resumen de estado de componente  

    -   Generador de resumen de estado del sistema de sitio  

-   **Reglas de filtro de estado:** puede crear reglas de filtro de estado, modificar la prioridad de las reglas, deshabilitar o habilitar reglas y eliminar las no usadas en cada sitio.  

    > [!NOTE]  
    >  Las reglas de filtro de estado no son compatibles con el uso de variables de entorno para ejecutar comandos externos.  

-   **Notificación de estado:** puede configurar los informes de componentes de servidor y cliente para modificar cómo se notifican los mensajes de estado al sistema de estado de Configuration Manager, así como especificar a dónde se envían los mensajes de estado.  

    > [!WARNING]  
    >  La configuración de notificación predeterminada es adecuada en la mayoría de los entornos: cambie la configuración con precaución. Si se incrementa el nivel de notificación de estado mediante la selección de la notificación de todos los detalles de estado, puede aumentar la cantidad de mensajes de estado que se deben procesar, lo que conlleva un incremento de la carga de procesamiento del sitio de Configuration Manager. Si se disminuye el nivel de notificación de estado, es posible que se limite la utilidad de los generadores de resumen de estado.  

Dado que el sistema de estado mantiene configuraciones independientes para cada sitio, debe editar cada sitio individualmente.  

###  <a name="procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> Procedimientos para configurar el sistema de estado  

##### <a name="to-configure-status-summarizers"></a>Para configurar generadores de resumen de estado  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** >**Sitios** y, después, seleccione el sitio para el que quiere configurar el sistema de estado.  

2.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Generadores de resumen de estado**.  

3.  En el cuadro de diálogo **Generadores de resumen de estado** , seleccione el generador de resumen de estado que desea configurar y, a continuación, haga clic en **Editar** para abrir las propiedades de dicho generador de resumen de estado. Si está editando el generador de resumen de implementación de aplicación o el generador de resumen de estadísticas de aplicación, continúe con el paso 5. Si está editando el estado del componente, vaya al paso 6. Si está editando el generador de resumen de estado del sistema de sitio, vaya al paso 7.  

4.  Después de abrir la página de propiedades del generador de resumen de implementación de aplicación o el generador de resumen de estadísticas de aplicación, siga estos pasos:  

    1.  En la pestaña **General** de la página de propiedades de los generadores de resumen, configure los intervalos de resumen y, a continuación, haga clic en **Aceptar** para cerrar la página de propiedades.  

    2.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Generadores de resumen de estado** y completar este procedimiento.  

5.  Después de abrir las páginas de propiedades del generador de resumen de estado de componente, siga estos pasos:  

    1.  En la pestaña **General** de la página de propiedades de los generadores de resumen, configure los valores de los periodos de replicación y umbral.  

    2.  En la pestaña **Umbrales** , seleccione el **Tipo de mensaje** que desea configurar y, a continuación, haga clic en el nombre de un componente de la lista **Umbrales** .  

    3.  En el cuadro de diálogo **Propiedades de umbral de estado** , edite los valores de los umbrales críticos y de advertencia y, a continuación, haga clic en **Aceptar**.  

    4.  Repita los pasos 6.b y 6.c según sea necesario. Cuando haya terminado, haga clic en **Aceptar** para cerrar las propiedades del generador de resumen.  

    5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Generadores de resumen de estado** y completar este procedimiento.  

6.  Después de abrir las páginas de propiedades del generador de resumen de estado del sistema de sitio, siga estos pasos:  

    1.  En la pestaña **General** de la página de propiedades de los generadores de resumen, configure los valores de replicación y programación.  

    2.  En la pestaña **Umbrales** , especifique los valores de **Umbrales predeterminados** para configurar umbrales predeterminados para las notificaciones de estado crítico y de advertencia.  

    3.  Para editar los valores de determinados **objetos de almacenamiento**, seleccione el objeto de la lista **Umbrales específicos** y, a continuación, haga clic en el botón **Propiedades** para acceder y editar los umbrales críticos y de advertencia de los objetos de almacenamiento. Haga clic en **Aceptar** para cerrar las propiedades de los objetos de almacenamiento.  

    4.  Para crear un nuevo objeto de almacenamiento, haga clic en el botón **Crear objeto** y especifique los valores del objeto de almacenamiento. Haga clic en **Aceptar** para cerrar las propiedades del objeto.  

    5.  Para eliminar un objeto de almacenamiento, selecciónelo y, a continuación, haga clic en el botón **Eliminar** .  

    6.  Repita los pasos de 7.b a 7.e según sea necesario. Cuando haya terminado, haga clic en **Aceptar** para cerrar las propiedades del generador de resumen.  

    7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Generadores de resumen de estado** y completar este procedimiento.  

##### <a name="to-create-a-status-filter-rule"></a>Para crear una regla de filtro de estado  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** >**Sitios** y, después, seleccione el sitio donde quiere configurar el sistema de estado.  

2.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Reglas de filtro de estado**. Se abre el cuadro de diálogo **Reglas de filtro de estado** .  

3.  Haga clic en **Crear**.  

4.  En el **Asistente de creación de reglas de filtro de estado**, en la página **General** , especifique un nombre para la nueva regla de filtro de estado y un criterio de coincidencia de mensajes para la regla y, a continuación, haga clic en **Siguiente**.  

5.  En la página **Acciones** , especifique las acciones que se deben llevar a cabo cuando un mensaje de estado coincide con la regla de filtro y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Resumen** , revise los detalles de la nueva regla y, a continuación, complete el asistente.  

    > [!NOTE]  
    >  Configuration Manager solo requiere que la nueva regla de filtro de estado tenga un nombre. Si se crea la regla pero no se especifica ningún criterio para procesar los mensajes de estado, la regla de filtro de estado no tendrá ningún efecto. Este comportamiento permite crear y organizar las reglas antes de configurar los criterios de filtro de estado para cada regla.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Para modificar o eliminar una regla de filtro de estado  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** >**Sitios** y, después, seleccione el sitio donde quiere configurar el sistema de estado.  

2.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Reglas de filtro de estado**.  

3.  En el cuadro de diálogo **Reglas de filtro de estado** , seleccione la regla que desea modificar y, a continuación, realice una de las siguientes acciones:  

    -   Haga clic en **Aumentar prioridad** o **Reducir prioridad** para cambiar el orden de procesamiento de la regla de filtro de estado. A continuación, seleccione otra acción o vaya al paso 8 de este procedimiento para completar esta tarea.  

    -   Haga clic en **Deshabilitar** o en **Habilitar** para cambiar el estado de la regla. Después de cambiar el estado de la regla, seleccione otra acción o vaya al paso 8 de este procedimiento para completar esta tarea.  

    -   Haga clic en **Eliminar** para eliminar la regla de filtro de estado y, a continuación, haga clic en **Sí** para confirmar la acción. Después de eliminar una regla, seleccione otra acción o vaya al paso 8 de este procedimiento para completar esta tarea.  

    -   Haga clic en **Editar** si desea cambiar los criterios para la regla de mensaje de estado y continúe en el paso 5 de este procedimiento.  

4.  En la pestaña **General** del cuadro de diálogo de propiedades de la regla de filtro de estado, modifique la regla y los criterios de coincidencia de mensajes.  

5.  En la pestaña **Acciones** , modifique las acciones que se realizarán si un mensaje de estado coincide con la regla de filtro.  

6.  Haga clic en **Aceptar** para guardar los cambios.  

7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Reglas de filtro de estado** .  

##### <a name="to-configure-status-reporting"></a>Para configurar la notificación de estado  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** > **Sitios** y, después, seleccione el sitio donde quiere configurar el sistema de estado.  

2.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y, a continuación, seleccione **Notificación de estado**.  

3.  En el cuadro de diálogo **Propiedades de componente de informes de estado** , especifique los mensajes de estado de componente de cliente y servidor que desea notificar o registrar:  

    1.  Configure **Informe** para enviar mensajes de estado al sistema de mensajes de estado de Configuration Manager.  

    2.  Configure **Registro** para escribir el tipo y la gravedad de los mensajes de estado en el registro de eventos de Windows.  

4.  Haga clic en **Aceptar**.  

###  <a name="monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a> Supervisar el sistema de estado de Configuration Manager  
 **Estado del sistema** de Configuration Manager proporciona una introducción a las operaciones generales de los sitios y a las operaciones del servidor de sitio de la jerarquía. Puede revelar problemas operativos de los componentes o servidores de sistema de sitio, y puede usar el estado de sistema para consultar detalles específicos de las diferentes operaciones de Configuration Manager. Puede supervisar el estado de sistema desde el nodo **Estado de sistema** del área de trabajo **Supervisión** en la consola de Configuration Manager.  

 La mayoría de los componentes y roles de sistema de sitio de Configuration Manager generan mensajes de estado. Los detalles de los mensajes de estado se registran en cada registro operativo de componentes, pero también se envían a la base de datos de sitio donde se resumen y presentan en un resumen general de cada componente o del estado de los sistemas de sitio. En estos paquetes de mensajes de estado se facilita información de operaciones regulares y advertencias y detalles de errores. Puede configurar los umbrales con que se activan advertencias o errores, y ajustar el sistema para garantizar que la información del paquete ignora problemas conocidos que no sean relevantes en su caso, mientras se centra la atención en los problemas reales de los servidores o en operaciones de componentes que desea investigar.  

 El estado de sistema se replica en otros sitios de una jerarquía como datos de sitio, no como datos globales. Esto significa que solo puede ver el estado del sitio con que se conecta la consola de Configuration Manager, y todos los sitios secundarios por debajo de dicho sitio. Por tanto, considere la posibilidad de conectar la consola de Configuration Manager al sitio de alto nivel de la jerarquía cuando ve el estado de sistema.  

 Utilice la siguiente tabla para identificar las diferentes vistas de estado de sistema y cuándo utilizar cada una.  

|Nodo|Más información|  
|----------|----------------------|  
|Estado del sitio|Utilice este nodo para ver un resumen del estado de cada sistema del sitio para revisar el estado de cada servidor de sistema de sitio. El estado del sistema de sitio se determina con umbrales que se configuran para cada sitio en el **Generador de resumen de estado del sistema de sitio**.<br /><br /> Puede ver mensajes de estado de cada sistema de sitio, establecer umbrales para los mensajes de estado y administrar el funcionamiento de los componentes en los sistemas de sitio con el **Administrador de servicios de Configuration Manager**.|  
|Estado del componente|Use este nodo para ver un resumen del estado de cada componente de Configuration Manager a fin de consultar el estado operativo del componente. El estado del componente se determina con umbrales que se configuran para cada sitio en el **Generador de resumen de estado de componente**.<br /><br /> Puede ver mensajes de estado de cada componente, establecer umbrales para los mensajes de estado y administrar el funcionamiento de los componentes con el **Administrador de servicios de Configuration Manager**.|  
|Registros en conflicto|Utilice este nodo para ver los mensajes de estado acerca de los clientes que puedan tener registros en conflicto.<br /><br /> Configuration Manager usa el identificador de hardware para tratar de identificar los clientes que puedan estar duplicados y alertarle así de los registros en conflicto. Por ejemplo, si tiene que reinstalar un equipo, el identificador de hardware podría ser el mismo, pero el GUID que usa Configuration Manager podría cambiar.|  
|Consultas de mensaje de estado|Utilice este nodo para consultar mensajes de estado de eventos específicos y detalles relacionados. Puede utilizar consultas de mensaje de estado para encontrar mensajes de estado relacionados con eventos específicos.<br /><br /> A menudo, puede usar consultas de mensaje de estado para identificar cuándo se modificó un componente específico, una operación o un objeto de Configuration Manager, así como qué cuenta se usó para realizar la modificación. Por ejemplo, puede ejecutar la consulta integrada **Recopilaciones creadas, modificadas o eliminadas** para identificar cuándo se ha creado una recopilación específica y qué cuenta de usuario se ha utilizado para crear le recopilación.|  

####  <a name="manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> Administrar el estado del sitio y el estado del componente  
 Utilice la siguiente información para administrar el estado del sitio y el estado del componente:  

-   Para configurar umbrales para el sistema de estado, consulte [Procedimientos para configurar el sistema de estado](#bkmk_configstatus).  

-   Para administrar componentes individuales en Configuration Manager, use el **Administrador de servicios de Configuration Manager**.  

####  <a name="view-status-messages"></a><a name="bkmk_view"></a> Ver los mensajes de estado  
 Puede ver los mensajes de estado de los componentes y servidores de sistema de sitio individuales.  

 Para ver los mensajes de estado en la consola de Configuration Manager, seleccione un componente o servidor de sistema de sitio específico y, después, haga clic en **Mostrar mensajes**. Cuando aparezcan los mensajes, tiene la opción de ver tipos de mensajes específicos o mensajes desde un período de tiempo establecido, y puede filtrar los resultados en función de los detalles de los mensajes de estado.  

##  <a name="alerts"></a><a name="bkmk_Alerts"></a> Alertas  
 Algunas operaciones generan alertas de Configuration Manager cuando se da una condición específica.  

- Por lo general, se generan alertas cuando se produce un error que debe resolver.  

- Las alertas pueden generarse para advertirle de que existe una condición, para que pueda continuar con la supervisión de la situación  

- Algunas alertas las configura el usuario, como las alertas de estado de cliente y de Endpoint Protection, mientras que otras alertas se configuran automáticamente  

- Puede configurar suscripciones para las alertas, que luego pueden enviar detalles por correo electrónico, lo que aumenta la concienciación de los problemas clave  

  Use la tabla siguiente para buscar información sobre cómo configurar alertas y suscripciones a alertas en Configuration Manager:  


|Acción|Más información|  
|------------|----------------------|  
|Configurar alertas de Endpoint Protection para una recopilación|Vea **Cómo configurar alertas de Endpoint Protection en Configuration Manager** en [Configurar Endpoint Protection en Configuration Manager](../../../protect/deploy-use/endpoint-protection-configure.md).|  
|Configurar alertas de estado de cliente para una recopilación|Vea [Cómo configurar el estado de cliente](../../../core/clients/deploy/configure-client-status.md).|  
|Administrar alertas de Configuration Manager|Consulte la sección [Management tasks for alerts](#BKMK_Manage) en este tema.|  
|Configurar suscripciones de correo electrónico para las alertas|Consulte la sección [Management tasks for alerts](#BKMK_Manage) en este tema.|  
|Supervisar alertas|Consulte la sección [Supervisar alertas](#BKMK_MonitorAlerts)|  

###  <a name="management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Para administrar alertas generales  

1. En la consola de Configuration Manager, vaya a **Supervisión** > **Alertas** y, después, seleccione una tarea de administración.  

   Utilice la tabla siguiente para obtener más información acerca de las tareas de administración que pueden requerir información para poder seleccionarlas.  

|Tarea de administración|Detalles|  
    |---------------------|-------------|  
    |**Configure**|Abre el cuadro de diálogo **Propiedades** de *&lt;nombre de la alerta*\> donde puede modificar el nombre, la gravedad y los umbrales de la alerta seleccionada. Si cambia la gravedad de la alerta, esta configuración afecta al modo en que las alertas se muestran en la consola de Configuration Manager.|  
    |**Editar comentario**|Escriba un comentario para las alertas seleccionadas. Estos comentarios se muestran con la alerta en la consola de Configuration Manager.|  
    |**Posponer**|Suspende la supervisión de la alerta hasta que se alcanza la fecha especificada. En ese momento, se actualiza el estado de la alerta.<br /><br /> Una alerta solo se puede posponer si está habilitada.|  
    |**Crear suscripción**|Abre el cuadro de diálogo **Nueva suscripción** donde puede crear una suscripción de correo electrónico para la alerta seleccionada.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Para configurar alertas de estado de cliente para una recopilación  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** >   **Recopilaciones de dispositivos**.  

2.  En la lista **Recopilaciones de dispositivos** , seleccione la recopilación para la que desea configurar las alertas y, a continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

    > [!NOTE]  
    >  No puede configurar alertas para recopilaciones de usuario.  

3.  En la pestaña **Alertas** del cuadro de diálogo *&lt;Nombre de recopilación*\>**Propiedades**, haga clic en **Agregar**.  

    > [!NOTE]  
    >  La pestaña **Alertas** solo es visible si el rol de seguridad con el que está asociado tiene permisos para alertas.  

4.  En el cuadro de diálogo **Agregar nuevas alertas de recopilación** , seleccione las alertas que desea que se generen cuando el umbral de estado de cliente cae por debajo de un determinado valor y, a continuación, haga clic en **Aceptar**.  

5.  En la lista **Condiciones** de la pestaña **Alertas** , seleccione cada alerta de estado de cliente y, a continuación, especifique la información siguiente.  

    -   **Nombre de alerta**: acepte el nombre predeterminado o escriba un nombre nuevo para la alerta.  

    -   **Gravedad de alerta**: seleccione el nivel de la alerta de la lista desplegable que se mostrará en la consola de Configuration Manager.  

    -   **Generar alerta**: especifique el porcentaje de umbral para la alerta.  

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo *&lt;Nombre de recopilación*\>**Propiedades**.  

##### <a name="to-configure-email-notification-for-alerts"></a>Para configurar la notificación por correo electrónico para las alertas  

1.  En la consola de Configuration Manager, vaya a **Supervisión** > **Alertas** > **Suscripciones**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Configurar notificación por correo electrónico**.  

3.  En el cuadro de diálogo **Propiedades de componente de notificación por correo electrónico** , especifique la siguiente información:  

    -   **Habilitar notificación de correo electrónico para las alertas**: active esta casilla para que Configuration Manager use un servidor SMTP para enviar alertas por correo electrónico.  

    -   **FQDN o dirección IP del servidor SMTP para enviar alertas por correo electrónico**: escriba el nombre de dominio completo (FQDN) o la dirección IP y el puerto SMTP del servidor de correo electrónico que quiera usar para estas alertas.  

    -   **Cuenta de conexión del servidor SMTP**: especifique el método de autenticación que quiere que Configuration Manager use para conectarse al servidor de correo electrónico.  

    -   **Dirección de remitente para alertas por correo electrónico**: especifique la dirección de correo electrónico desde la que se deben enviar los mensajes de alerta.  

    -   **Probar servidor SMTP**: envía un mensaje de prueba a la dirección de correo electrónico especificada en **Dirección de remitente para alertas por correo electrónico**.  

4.  Haga clic en **Aceptar** para guardar la configuración y cerrar el cuadro de diálogo **Propiedades de componente de notificación por correo electrónico** .  

##### <a name="to-subscribe-to-email-alerts"></a>Para suscribirse a alertas por correo electrónico  

1.  En la consola de Configuration Manager, vaya a **Supervisión** > **Alertas**.  

2.  Seleccione una alerta y, a continuación, en la ficha **Inicio** , en el grupo **Suscripción** , haga clic en **Crear suscripción**.  

3.  En el cuadro de diálogo **Nueva suscripción** , especifique la información siguiente:  

    -   **Nombre**: escriba un nombre para identificar la suscripción por correo electrónico. Puede usar hasta 255 caracteres.  

    -   **Dirección de correo electrónico**: escriba las direcciones de correo electrónico a las que quiera enviar la alerta. Separe varias direcciones de correo electrónico con punto y coma.  

    -   **Idioma del correo electrónico**: en la lista, especifique el idioma para el correo electrónico.  

4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Nueva suscripción** y crear la suscripción de correo electrónico.  

    > [!NOTE]  
    >  Puede eliminar y editar suscripciones en el área de trabajo **Supervisión** al expandir el nodo **Alertas** y hacer clic en el nodo **Suscripciones** .  

###  <a name="monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a> Supervisar alertas  
 Puede ver las alertas en el nodo **Alertas** del área de trabajo **Supervisión** . Las alertas tienen alguno de los siguientes estados de alerta:  

- **Nunca desencadenado**: no se ha cumplido la condición de la alerta.  

- **Activo**: se cumple la condición de la alerta.  

- **Cancelada**: ya no se cumple la condición de una alerta activa. Este estado indica que la condición que provocó la alerta se ha resuelto.  

- **Pospuesto**: un usuario administrativo ha configurado Configuration Manager para que evalúe el estado de la alerta más adelante.  

- **Disabled**: un usuario administrativo ha deshabilitado la alerta. Si una alerta tiene este estado, Configuration Manager no la actualiza aunque el estado cambie.  

  Puede realizar alguna de las siguientes acciones cuando Configuration Manager genera una alerta:  

- Resuelva la condición que generó la alerta; por ejemplo, solucione un problema de red o un problema de configuración que generó la alerta. Después de que Configuration Manager detecte que ha desaparecido el problema, el estado de la alerta cambia a **Cancelar**.  

- Si la alerta se corresponde con un problema conocido, puede posponerla durante un tiempo determinado. En ese momento, Configuration Manager actualiza la alerta a su estado actual.  

   Puede posponer una alerta sólo cuando está activa.  

- Puede editar el **comentario** de una alerta para que otros usuarios administrativos puedan ver que está al corriente de la alerta. Por ejemplo, en el comentario puede identificar cómo solucionar la condición, ofrecer información acerca del estado actual de la condición o explicar por qué ha pospuesto la alerta.  
