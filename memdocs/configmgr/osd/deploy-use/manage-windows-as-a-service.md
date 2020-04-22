---
title: Administración de Windows como servicio
titleSuffix: Configuration Manager
description: Vea el estado de Windows como servicio (WaaS) mediante Configuration Manager, cree planes de mantenimiento para formar anillos de implementación y vea alertas cuando los clientes de Windows 10 estén próximos al final del soporte técnico.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690333"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>Administración de Windows como servicio mediante Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En Configuration Manager, puede ver el estado de Windows como servicio (WaaS) en su entorno. Puede crear planes de mantenimiento para formar anillos de implementación y asegurarse de que los sistemas Windows 10 se mantienen actualizados cuando se publican nuevas compilaciones. También puede ver alertas cuando los clientes de Windows 10 se encuentran cerca de la finalización del soporte para su compilación de Canal semianual.

Para más información sobre las opciones de mantenimiento de Windows 10, vea [Información general de Windows como servicio](/windows/deployment/update/waas-overview#servicing-channels).

Use las secciones siguientes para administrar Windows como servicio:

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a> Requisitos previos

Para ver los datos en el panel de mantenimiento de Windows 10, debe realizar estas acciones:

- Los equipos con Windows 10 deben usar las actualizaciones de software de Configuration Manager con Windows Server Update Services (WSUS) para la administración de las actualizaciones de software. Cuando los equipos usan Windows Update para empresas (o Windows Insider) para la administración de actualizaciones de software, el equipo no se evalúa en los planes de mantenimiento de Windows 10. Para obtener más información, consulte [Integración con Windows Update for Business en Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md) (Integración con Windows Update for Business en Windows 10).

- Use una versión compatible de WSUS:
  - WSUS 10.0.14393 (rol de Windows Server 2016)
  - WSUS 10.0.17763 (rol de Windows Server 2019) (requiere Configuration Manager 1810 o posterior)
  - WSUS 6.2 y 6.3 (rol de Windows Server 2012 y Windows Server 2012 R2)
    - [KB 3095113 y KB 3159706 (o una actualización equivalente) deben estar instalados](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012) en WSUS 6.2 y 6.3.

- Habilitar la detección de latidos Los datos que se muestran en el panel de mantenimiento de Windows 10 se buscaron mediante esta detección. Para obtener más información, vea [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc) (Configuración de la detección de latidos).

    La información del canal y la compilación de Windows 10 se detecta y se almacena en estos atributos:  

    - **Rama de preparación del sistema operativo**: especifica el canal del sistema operativo. Por ejemplo, **0** = canal semianual (dirigido) (no se aplazan actualizaciones), **1** = canal semianual (se aplazan actualizaciones), **2** = canal de servicio a largo plazo (LTSC)

    - **Compilación del sistema operativo**: especifica la compilación del sistema operativo. Por ejemplo, **10.0.10240** (RTM) o **10.0.10586** (versión 1511)

- El punto de conexión de servicio debe estar instalado y configurado para el modo de **conexión persistente en línea** para ver los datos en el panel de mantenimiento de Windows 10. Cuando esté en modo sin conexión, no verá las actualizaciones de datos en el panel hasta que obtenga las actualizaciones de mantenimiento de Configuration Manager. Para obtener más información, consulte [About the service connection point](../../core/servers/deploy/configure/about-the-service-connection-point.md) (Sobre el punto de conexión del servicio).

- Internet Explorer 9 o una versión posterior debe estar instalado en el equipo que ejecuta la consola de Configuration Manager.

- Las actualizaciones de software deben estar configuradas y sincronizadas. Seleccione la clasificación de **Actualizaciones** y sincronizar las actualizaciones de software antes de que las actualizaciones de características de Windows 10 estén disponibles en la consola de Configuration Manager. Para obtener más información, consulte [Prepare for software updates management](../../sum/get-started/prepare-for-software-updates-management.md) (Preparación para la administración de actualizaciones de software).

- A partir de la versión 1902 de Configuration Manager, compruebe la [configuración de cliente](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)**Especificar la prioridad de subproceso para las actualizaciones de características** para asegurarse de que es apropiada para su entorno.

- A partir de la versión 1906 de Configuration Manager, compruebe la **configuración de cliente**[Habilitar la actualización dinámica para las actualizaciones de características](../../core/clients/deploy/about-client-settings.md#bkmk_du) para asegurarse de que es apropiada para su entorno. <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Panel de mantenimiento de Windows 10

El panel de mantenimiento de Windows 10 le proporciona información acerca de los equipos con Windows 10 de su entorno, los planes de mantenimiento activos, la información de cumplimiento, etc. Los datos del panel de mantenimiento de Windows 10 dependen de si el punto de conexión de servicio está instalado. El panel presenta los iconos siguientes:

- **Icono de Uso de Windows 10**: proporciona un desglose de las compilaciones públicas de Windows 10. Las compilaciones de Windows Insiders figuran como **otros**, así como las demás compilaciones que todavía no son conocidas para el sitio. El punto de conexión de servicio descarga los metadatos que informan acerca de las compilaciones de Windows y, después, estos datos se comparan con los datos de detección.

- **Icono de Anillos de Windows 10**: proporciona un desglose de Windows 10 por canal de disponibilidad y rama. El segmento LTSC incluye todas las versiones de LTSC. El primer icono desglosa las versiones específicas, como por ejemplo, Windows 10 LTSC 2015.

- **Icono Crear plan de servicio**: proporciona una forma rápida de crear un plan de mantenimiento. Debe especificar el nombre, la recopilación (solo muestra las primeras diez recopilaciones por tamaño, la más pequeña primero), el paquete de implementación (solo muestra los diez primeros paquetes modificados más recientemente) y el estado de disponibilidad. Los valores predeterminados se usan para las demás opciones de configuración. Haga clic en **Configuración avanzada** para iniciar el Asistente para crear planes de mantenimiento, donde puede configurar todas las opciones de configuración del plan de mantenimiento.

- **Icono Expirado**: muestra el porcentaje de dispositivos que están en una compilación de Windows 10 que ha superado el final del ciclo de vida. Configuration Manager determina el porcentaje a partir de los metadatos que el punto de conexión del servicio descarga y los compara con los datos de detección. Una compilación que superó el final del ciclo de vida ya no recibe más actualizaciones acumulativas mensuales, incluidas las actualizaciones de seguridad. Los equipos de esta categoría deben actualizarse a la versión de compilación siguiente. Configuration Manager se redondea al número entero siguiente. Por ejemplo, si tiene 10 000 equipos y solo uno en una compilación expirada, el icono muestra 1 %.

- **Icono Expira pronto**: muestra el porcentaje de equipos que están en una compilación que se acerca al final del ciclo de vida (en un plazo aproximado de cuatro meses) y es similar al icono **Expirado**. Configuration Manager se redondea al número entero siguiente.

- **Icono Alertas**: muestra las alertas activas.

- **Icono Service Plan Monitoring**: muestra los planes de mantenimiento que ha creado y un gráfico de cumplimiento de cada uno. Este icono ofrece una visión general rápida del estado actual de las implementaciones de plan de mantenimiento. Si un canal de implementación anterior cumple sus expectativas de cumplimiento, puede seleccionar un plan de mantenimiento posterior (canal de implementación) y hacer clic en **Implementar ahora** en lugar de esperar a que las reglas del plan de mantenimiento se activen automáticamente.

- **Icono Windows 10 Builds**: muestra una línea de tiempo de imagen fija que proporciona una visión general de las compilaciones de Windows 10 publicadas actualmente y le ofrece una idea general de cuándo cambia el estado de las compilaciones. Este icono se ha eliminado a partir de la versión 1902 de Configuration Manager, ya que se ofrece información más detallada en el [panel de ciclo de vida del producto](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md). <!--3446861-->

> [!IMPORTANT]
> La información que se muestra en el panel de mantenimiento de Windows 10 (por ejemplo, el ciclo de vida de soporte técnico para las versiones de Windows 10) se proporciona para su comodidad y solo para uso interno en su empresa. No debe confiar exclusivamente en esta información para comprobar el cumplimiento de la actualización. Asegúrese de comprobar la exactitud de la información proporcionada.

## <a name="drill-through-required-updates"></a>Obtención de detalles de actualizaciones necesarias
<!--4224414-->
*(Se introdujo en la versión 1906)*

Se pueden obtener detalles de las estadísticas de compatibilidad para ver qué dispositivos requieren una actualización de características de Office 10 específica. Para ver la lista de dispositivos, necesita permiso para ver las actualizaciones y las colecciones a las que pertenecen los dispositivos. Para explorar en profundidad la lista de dispositivos:

1. Vaya a **Biblioteca de software** > **Mantenimiento de Windows 10** > **Todas las actualizaciones de Windows 10**.
1. Seleccione las actualizaciones que requiera al menos un dispositivo.
1. En la pestaña **Resumen** encontrará un gráfico circular bajo **Estadísticas**.
1. Seleccione el hipervínculo **Vista necesaria** situado junto al gráfico circular para obtener los detalles de la lista de dispositivos.
1. Esta acción le llevará a un nodo temporal en **Dispositivos** donde podrá ver los dispositivos que requieren la actualización. También puede realizar acciones para el nodo, como crear una colección a partir de la lista.

## <a name="servicing-plan-workflow"></a>Flujo de trabajo del plan de mantenimiento

Los planes de mantenimiento de Windows 10 en Configuration Manager son muy similares a las reglas de implementación automática de las actualizaciones de software. Se crea un plan de mantenimiento con los siguientes criterios evaluados por Configuration Manager:

- **Clasificación de actualizaciones**: solo se evalúan las actualizaciones de la clasificación **Actualizaciones**.

- **Estado de disponibilidad**: el estado de disponibilidad definido en el plan de mantenimiento se compara con el estado de disponibilidad de la actualización. Los metadatos de la actualización se recuperan cuando el punto de conexión de servicio busca actualizaciones.

- **Aplazamiento de tiempo**: cantidad de días que se especifica en **Cantidad de días después de que Microsoft publique una nueva actualización que quiere esperar antes de la implementación en su entorno** en el plan de mantenimiento. Si la fecha actual es posterior a la fecha de lanzamiento más el número de días configurado, Configuration Manager evalúa si se debe incluir una actualización en la implementación.

  Cuando una actualización cumple los criterios, el plan de mantenimiento agrega la actualización al paquete de implementación, distribuye el paquete a los puntos de distribución e implementa la actualización a la recopilación basándose en los valores configurados en el plan de mantenimiento. Puede supervisar las implementaciones en el icono Service Plan Monitoring del panel de mantenimiento de Windows 10. Para obtener más información, consulte [Monitor software updates](../../sum/deploy-use/monitor-software-updates.md) (Supervisión de las actualizaciones de software).

> [!NOTE]
> **Windows 10, versión 1903 y posteriores** se ha agregado a Microsoft Update como un producto propio en lugar de formar parte del producto **Windows 10** como en las versiones anteriores. Este cambio le obligaba a realizar una serie de pasos manuales para asegurarse de que los clientes veían estas actualizaciones. Se ha intentado reducir el número de pasos manuales que debe seguir para el nuevo producto en Configuration Manager, versión 1906. Para obtener más información, vea [Configuración de productos para versiones de Windows 10](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later).<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Plan de mantenimiento de Windows 10

A medida que implementa el canal semianual de Windows 10, puede crear uno o varios planes de mantenimiento para definir los canales de implementación que quiere en su entorno, así como supervisarlos en el panel de mantenimiento de Windows 10. Los planes de mantenimiento solo usan la clasificación de actualizaciones de software **Actualizaciones** , no las actualizaciones acumulativas de Windows 10. Este tipo de actualizaciones deberá seguir implementándose mediante el flujo de trabajo de las actualizaciones de software. La experiencia del usuario final con un plan de mantenimiento es la misma que con las actualizaciones de software, incluida la configuración del plan de mantenimiento.  

> [!NOTE]
> Puede usar una secuencia de tareas para implementar una actualización para cada compilación de Windows 10, pero requiere más trabajo manual. Debería importar los archivos de origen actualizados como un paquete de actualización de sistema operativo y, después, crear e implementar la secuencia de tareas en el conjunto de equipos adecuado. Sin embargo, una secuencia de tareas proporciona opciones personalizadas adicionales, como las acciones anteriores y posteriores a la implementación.

Puede crear un plan de mantenimiento básico desde el panel de mantenimiento de Windows 10. Después de especificar el nombre, la recopilación (solo muestra las primeras diez recopilaciones por tamaño, la más pequeña primero), el paquete de implementación (solo muestra los diez primeros paquetes modificados más recientemente) y el estado de disponibilidad, Configuration Manager crea el plan de mantenimiento con los valores predeterminados de las demás configuraciones. También puede iniciar el Asistente para crear planes de mantenimiento para configurar todos los valores. Use el procedimiento siguiente para crear un plan de mantenimiento mediante el Asistente para crear planes de mantenimiento.  

> [!NOTE]  
> Puede administrar el comportamiento de las implementaciones de alto riesgo. Una implementación de alto riesgo es una implementación que se instala automáticamente y puede provocar resultados no deseados. Por ejemplo, una secuencia de tareas con el propósito **Requerido** que implementa Windows 10 se considera una implementación de alto riesgo. Para obtener más información, consulte [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo).

### <a name="to-create-a-windows-10-servicing-plan"></a>Para crear un plan de mantenimiento de Windows 10

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.

1. En el área de trabajo Biblioteca de software, expanda **Mantenimiento de Windows 10**y, después, haga clic en **Planes de mantenimiento**.

1. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear plan de mantenimiento**. Se abre el Asistente para crear planes de mantenimiento.

1. En la página **General** , configure las siguientes opciones:

    - **Nombre**: especifique el nombre del plan de mantenimiento. El nombre debe ser único, describir el objetivo de la regla e identificarla entre el resto de reglas del sitio de Configuration Manager.

    - **Descripción**: especifique una descripción para el plan de mantenimiento. La descripción debería proporcionar información general del plan de mantenimiento, además de cualquier otra información relevante que permita identificar y diferenciarlo del resto de resto de planes del sitio de Configuration Manager. El campo de descripción es opcional, tiene un límite de 256 caracteres y tiene un valor en blanco de forma predeterminada.

1. En la página Plan de mantenimiento, especifique la **Recopilación de destino**. los miembros de la recopilación reciben las actualizaciones de Windows 10 definidas en el plan de mantenimiento.

    - Al realizar una implementación de alto riesgo, como un plan de mantenimiento, en la ventana **Seleccionar recopilación** solo se muestran las recopilaciones personalizadas que cumplen con la configuración de comprobación de implementación que está configurada en las propiedades del sitio.

    - Las implementaciones de alto riesgo siempre se limitan a las recopilaciones personalizadas, las recopilaciones que cree y la recopilación integrada **Equipos desconocidos** . Si crea una implementación de alto riesgo, no podrá seleccionar una recopilación integrada como **Todos los sistemas**. Desactive **Ocultar recopilaciones con un número de miembros superior a la configuración de tamaño mínimo del sitio** para ver todas las recopilaciones personalizadas que contienen menos clientes que el tamaño máximo configurado. Para obtener más información, consulte [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo).

    - La configuración de comprobación de implementación se basa en la pertenencia actual de la recopilación. Después de implementar el plan de mantenimiento, la pertenencia a la recopilación no se vuelve a evaluar para la configuración de implementación de alto riesgo.

      - Por ejemplo, supongamos que establece el **Tamaño predeterminado** en 100 y el **Tamaño máximo** en 1000. Al crear una implementación de alto riesgo, la ventana **Seleccionar recopilación** solo mostrará las recopilaciones que contengan menos de 100 clientes. Si desactiva la configuración **Ocultar recopilaciones con un recuento de miembros mayor que la configuración de tamaño mínimo del sitio**, la ventana mostrará las recopilaciones que contienen menos de 1000 clientes.  
      Al seleccionar una recopilación que contiene un rol de sitio, se aplican estos criterios:
        - Si la recopilación contiene un servidor de sistema de sitio y establece la configuración de comprobación de implementación para bloquear las recopilaciones con servidores de sistema de sitio, se producirá un error y no podrá continuar.
        - El Asistente para implementar software mostrará una advertencia de alto riesgo cuando la recopilación contenga un servidor de sistema de sitio y establezca la configuración de comprobación de implementación para advertirle si las recopilaciones tienen servidores de sistema de sitio, si la recopilación supera el valor de tamaño predeterminado o si la recopilación contiene un servidor. Debe aceptar la creación de una implementación de alto riesgo y se creará un mensaje de estado de auditoría.

1. En la página Canal de implementación, configure las siguientes opciones:

   - **Especificar el estado de disponibilidad de Windows al que debería aplicarse este plan de mantenimiento**: Seleccione una de las siguientes opciones:

      - **Canal semianual (dirigido)** : en este modelo de mantenimiento, las actualizaciones de las características están disponibles en cuanto Microsoft las publica.

      - **Canal semianual**: este canal de mantenimiento normalmente se usa para una implementación amplia. Los clientes de Windows 10 en el canal semianual reciben la misma versión de Windows 10 que los dispositivos en el canal dirigido, solo que más tarde.

        Para más información sobre los canales de mantenimiento y qué opciones son las más adecuadas en su caso, vea [Canales de mantenimiento](/windows/deployment/update/waas-overview#servicing-channels).

   - **Cantidad de días después de que Microsoft publique una nueva actualización que quiere esperar antes de la implementación en su entorno**: Si la fecha actual es posterior a la fecha de lanzamiento más el número de días configurado para este valor, Configuration Manager evalúa si se debe incluir una actualización en la implementación.

1. En la página Actualizaciones, configure los criterios de búsqueda para filtrar las actualizaciones que se agregarán al plan de mantenimiento. Solo se agregarán a la implementación asociada las actualizaciones que cumplan con los criterios especificados. Están disponibles los filtros de propiedades siguientes: <!--3098809, 3113836, 3204570 -->

   - **Arquitectura** (a partir de la versión 1810)
   - **Idioma**
   - **Categoría de producto** (a partir de la versión 1810)
   - **Requerido**
      > [!IMPORTANT]
      > Como parte de los criterios de búsqueda, recomendamos que establezca el campo **Requerido** con un valor de **>=1**. El uso de este criterio garantiza que solo se agreguen las actualizaciones aplicables al plan de mantenimiento.
   - **Reemplazado** (a partir de la versión 1810)
   - **Título**

    Haga clic en **Vista previa** para ver las actualizaciones que cumplen los criterios especificados.

1. En la página Programación de implementación, configure las siguientes opciones:

   - **Programar evaluación**: especifique si Configuration Manager evalúa la hora disponible y las horas límite de instalación mediante la hora UTC o la hora local del equipo que ejecuta la consola de Configuration Manager.

       > [!NOTE]
       > Al seleccionar la hora local y luego **Lo antes posible** para **Horas de disponibilidad del software** o **Fecha límite de instalación**, la hora actual en el equipo que ejecuta la consola de Configuration Manager se usa para evaluar cuándo hay actualizaciones disponibles o cuándo se instalan en un cliente. Si el cliente está en una zona horaria distinta, estas acciones se producirán cuando la hora del cliente llegue a la hora de evaluación.

   - **Horas de disponibilidad del software**: seleccione una de las siguientes opciones para especificar cuándo estarán disponibles las actualizaciones de software para los clientes:

        - **Lo antes posible**: seleccione esta opción para que las actualizaciones de software incluidas en la implementación estén disponibles para los equipos cliente lo antes posible. Si se crea la implementación con esta opción seleccionada, Configuration Manager actualiza la directiva del cliente. Luego, en el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación y pueden obtener las actualizaciones disponibles para la instalación.

        - **Hora específica**: seleccione esta opción para que las actualizaciones de software incluidas en la implementación estén disponibles para los equipos cliente en una fecha y a una hora específicas. Si se crea la implementación con esta opción habilitada, Configuration Manager actualiza la directiva del cliente. Con el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación. En cambio, las actualizaciones de software de la implementación no están disponibles para la instalación hasta después de la fecha y hora configurada.

   - **Fecha límite de instalación**: seleccione una de las siguientes opciones para especificar la fecha límite de instalación de las actualizaciones de software de la implementación:

        - **Lo antes posible**: seleccione esta opción para que se instalen automáticamente las actualizaciones de software incluidas en la implementación lo antes posible.

        - **Hora específica**: seleccione esta opción para que las actualizaciones de software de la implementación se instalen automáticamente a una hora y en una fecha específicas. Configuration Manager determina la fecha límite para instalar actualizaciones de software, para lo cual agrega el intervalo **Hora específica** establecido a **Horas de disponibilidad del software**.

           > [!NOTE]
           > La hora de la fecha límite de instalación real es la hora de la fecha límite más una cantidad aleatoria de tiempo de hasta dos horas. Se minimiza, así, el efecto negativo que podría producirse si todos los equipos cliente de la recopilación de destino instalan las actualizaciones de software de la implementación a la misma hora.
           >
           > Puede establecer la opción **Deshabilitar selección aleatoria de fecha límite** de la configuración de cliente **Agente de equipo** para deshabilitar el retraso de la selección aleatoria de instalación para las actualizaciones necesarias. Para obtener más información, vea [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent).

        - **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario hasta el período de gracia definido en la configuración del cliente**: seleccione para respetar la opción del cliente [**Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** ](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours).

1. En la página Experiencia del usuario, configure las siguientes opciones:  

    - **Notificaciones de usuario**: especifique si quiere mostrar una notificación de las actualizaciones en el Centro de software del equipo cliente en **Horas de disponibilidad del software**, y si quiere mostrar las notificaciones de usuario en los equipos cliente.

    - **Comportamiento de la fecha límite**: especifique el comportamiento que se debe producir cuando se alcanza la fecha límite para la implementación de la actualización. Especifique si desea instalar las actualizaciones en la implementación. Especifique también si el sistema se debe reiniciar tras la instalación de las actualizaciones, independientemente de si existe una ventana de mantenimiento configurada. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  

    - **Comportamiento de reinicio de dispositivo**: especifique si se debe suprimir el reinicio del sistema necesario para completar la instalación de las actualizaciones en servidores y estaciones de trabajo.

    - **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: cuando implemente actualizaciones en dispositivos de Windows Embedded habilitados para filtro de escritura, puede especificar que la actualización se instale en la superposición temporal, y confirmar los cambios más tarde, confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.
        - Cuando implemente una actualización en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada.

    - **Comportamiento de reevaluación de implementación de actualizaciones de software tras el reinicio**: para forzar otro ciclo de evaluación de implementación de actualizaciones tras el reinicio, seleccione la opción **Si alguna actualización de esta implementación requiere un reinicio del sistema, ejecute el ciclo de evaluación de implementación de actualizaciones tras el reinicio**.

1. En la página Paquete de implementación, seleccione un paquete de implementación existente, no seleccione ninguno o configure las opciones siguientes para crear un nuevo paquete de implementación:

    1. **Nombre**: especifique el nombre del paquete de implementación. Debe ser un nombre único que describa el contenido del paquete. Está limitado a 50 caracteres.

    1. **Descripción**: especifique una descripción que proporcione información sobre el paquete de implementación. La descripción está limitada a 127 caracteres.

    1. **Origen del paquete**: especifica la ubicación de los archivos de origen de la actualización de software. Escriba una ruta de red para la ubicación de origen, por ejemplo, **\\\servidor\\nombre de recurso compartido\\ruta**, o haga clic en **Examinar** para buscar la ubicación de red. Cree la carpeta compartida para los archivos de origen del paquete de implementación antes de continuar con la página siguiente.
        - Ningún otro paquete de implementación de software podrá usar la ubicación de origen del paquete de implementación que especifique.
        - Tanto la cuenta de equipo del proveedor de SMS como el usuario que ejecuta el asistente para descargar actualizaciones de software deben tener permisos NTFS de **escritura** en la ubicación de descarga. Debe restringir cuidadosamente el acceso a la ubicación de descarga para reducir el riesgo de alteración de los archivos de origen de la actualización de software por parte de atacantes.
        - Puede cambiar la ubicación de origen del paquete en las propiedades del paquete de implementación después de que Configuration Manager cree el paquete de implementación. Pero si lo hace, primero debe copiar el contenido desde el origen del paquete original a la nueva ubicación de origen del paquete.

    1. **Prioridad de envío**: especifique la prioridad de envío del paquete de implementación. Configuration Manager usa la prioridad de envío para el paquete de implementación cuando envía el paquete a los puntos de distribución. Los paquetes de implementación se envían en orden de prioridad: Alta, Media o Baja. Los paquetes con prioridades idénticas se envían en el orden en que se crearon. Si no hay ningún trabajo pendiente, el paquete se procesa inmediatamente sin tener en cuenta su prioridad.

    1. **Habilitar replicación diferencial binaria**: habilite esta opción si quiere usar replicación diferencial binaria.

1. En la página Puntos de distribución, especifique los puntos de distribución o los grupos de puntos de distribución que hospedan los archivos de actualización. Para más información sobre los puntos de distribución, vea [Configurar un punto de distribución](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).

    > [!NOTE]
    > Esta página sólo está disponible cuando se crea un nuevo paquete de implementación de actualizaciones de software.  

1. En la página Ubicación de descarga, especifique si los archivos de actualización se van a descargar desde Internet o desde la red local. Configure las siguientes opciones:

    - **Descargar actualizaciones de software de Internet**: seleccione esta opción para descargar las actualizaciones desde una ubicación especificada de Internet. Esta opción está habilitada de forma predeterminada.

    - **Descargar actualizaciones de software de una ubicación en mi red**: seleccione esta opción para descargar las actualizaciones desde un directorio local o una carpeta compartida. Esta opción es útil si el equipo que ejecuta el asistente no tiene acceso a Internet. Cualquier equipo con acceso a Internet puede descargar de forma preliminar las actualizaciones y almacenarlas en una ubicación de la red local a la que se pueda acceder desde el equipo que ejecuta el asistente.

1. En la página Selección del idioma, seleccione los idiomas para los que se descargan las actualizaciones seleccionadas. Las actualizaciones solo se descargan si están disponibles en los idiomas seleccionados. Las actualizaciones que no son específicas de un idioma se descargan siempre. De forma predeterminada, el asistente selecciona los idiomas que se han configurado en las propiedades del punto de actualización de software. Debe seleccionar, como mínimo, un idioma para poder pasar a la página siguiente. Si solo selecciona idiomas que una actualización no admite, la descarga no se completa para esa actualización.

1. En la página Resumen, revise la configuración y haga clic en **Siguiente** para crear el plan de mantenimiento.  

Cuando ha completado al asistente, se ejecutará el plan de mantenimiento. Este agrega las actualizaciones que cumplen los criterios especificados a un grupo de actualizaciones de software, descarga estas actualizaciones en la biblioteca de contenido del servidor de sitio, las distribuye a los puntos de distribución configurados y, después, implementa el grupo de actualizaciones de software en clientes de la recopilación de destino.

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> Modificar un plan de mantenimiento

Después de crear un plan de mantenimiento básico desde el panel de mantenimiento de Windows 10 o si necesita cambiar la configuración de un plan de mantenimiento existente, puede hacerlo a través de las propiedades del plan de mantenimiento.

> [!NOTE]
> Puede configurar las opciones en las propiedades para el plan de mantenimiento que no están disponibles en el asistente al crear el plan de mantenimiento. El asistente utiliza una configuración predeterminada para la configuración para lo siguiente: configuración de descarga, configuración de implementación y alertas.  

Use el siguiente procedimiento para modificar las propiedades de un plan de mantenimiento. 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Para modificar las propiedades de un plan de mantenimiento

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.

1. En el área de trabajo Biblioteca de software, expanda **Mantenimiento de Windows 10**, haga clic en **Planes de mantenimiento** y seleccione el plan de mantenimiento que quiere modificar.

1. En la pestaña **Inicio** , haga clic en **Propiedades** para abrir las propiedades del plan de mantenimiento seleccionado.

    Las siguientes opciones están disponibles en las propiedades del plan de mantenimiento que no estaban configuradas en el asistente:

    **Configuración de implementación**: En la pestaña Configuración de implementación, configure las opciones siguientes:

    - **Usar Wake-on-LAN para activar clientes para las implementaciones requeridas**: especifique si desea habilitar Wake on LAN en la fecha límite para enviar paquetes de reactivación a equipos que requieran una o varias actualizaciones de software en la implementación. Los equipos que están en modo de suspensión en la fecha límite de instalación se activan para que se pueda iniciar la instalación de las actualizaciones de software. Los clientes que están en modo de suspensión, pero no requieren actualizaciones de software de la implementación, no se iniciarán. De forma predeterminada, esta opción no está habilitada.

        > [!WARNING]
        > Para poder utilizar esta opción, los equipos y las redes deben configurarse para Wake on LAN.

    - **Nivel de detalle**: especifique el nivel de detalle de los mensajes de estado que notifican los equipos cliente.

    **Configuración de descarga**: En la pestaña Configuración de descarga, configure las opciones siguientes:

    - Especifique si el cliente descargará e instalará las actualizaciones de software cuando esté conectado a una red lenta o si usará una ubicación de contenido de reserva.

    - Especifique si el cliente debe descargar e instalar las actualizaciones de software desde un punto de distribución de reserva cuando el contenido de las actualizaciones de software no está disponible en un punto de distribución preferido.

    - **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: especifique si desea habilitar el uso de BranchCache para descargas de contenido. Para obtener más información sobre BranchCache, vea [Conceptos básicos de la administración de contenido](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

    - Especifique si los clientes deben descargar las actualizaciones de software desde Microsoft Update si las actualizaciones no están disponibles en los puntos de distribución.
        > [!IMPORTANT]
        > No use esta configuración para las actualizaciones del Servicio de actualización de Windows 10. Se produce un error cuando Configuration Manager (al menos hasta la versión 1610) intenta descargar las actualizaciones del Servicio de actualización de Windows 10 desde Microsoft Update.

    - Especifique si desea permitir que los clientes descarguen después de la fecha límite de instalación cuando utilizan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión a Internet de uso medido.

    **Alertas**: en la pestaña Alertas, configure cómo generarán Configuration Manager y System Center Operations Manager las alertas para esta implementación.
    - Puede revisar las alertas de las actualizaciones de software recientes en el área de trabajo **Biblioteca de software** del nodo **Actualizaciones de software** .

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea [Aspectos básicos de Configuration Manager como servicio y de Windows como servicio](../../core/understand/configuration-manager-and-windows-as-service.md).
