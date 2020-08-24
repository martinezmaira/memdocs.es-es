---
title: Implementar aplicaciones
titleSuffix: Configuration Manager
description: Crear o simular una implementación de una aplicación en una recopilación de dispositivo o usuario
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2fcd583e860273e2fbfc9fcda1e08053336345
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127527"
---
# <a name="deploy-applications-with-configuration-manager"></a>Implementar aplicaciones con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Crear o simular una implementación de una aplicación en una recopilación de dispositivo o usuario en Configuration Manager. Esta implementación proporciona instrucciones para el cliente de Configuration Manager sobre cómo y cuándo instalar el software.

Antes de implementar una aplicación, cree al menos un tipo de implementación para la aplicación. Para obtener más información, consulte [Create applications](create-applications.md) (Creación de aplicaciones).

A partir de la versión 1906, puede crear un grupo de aplicaciones que puede enviar a una colección de usuarios o dispositivos como una sola implementación. Para más información, consulte [Crear grupos de aplicaciones](create-app-groups.md).

También puede simular la implementación de una aplicación. Esta simulación prueba la aplicabilidad de una implementación sin instalar o desinstalar la aplicación. Una implementación simulada evalúa el método de detección, los requisitos y las dependencias de un tipo de implementación y muestra los resultados en el nodo **Implementaciones** del área de trabajo **Supervisión**. Para obtener más información, consulte el artículo sobre [simular implementaciones de aplicaciones ](simulate-application-deployments.md).

> [!NOTE]
> Solo se puede simular la implementación de las aplicaciones obligatorias, pero no se pueden simular paquetes ni actualizaciones de software.
>
> Los dispositivos inscritos en MDM no admiten las implementaciones simuladas, la experiencia del usuario o la configuración de programación.

## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a> Implementar una aplicación

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones** o **Grupos de aplicaciones**.

1. Seleccione una aplicación o un grupo de aplicaciones de la lista que desea implementar. En la cinta de opciones, seleccione **Implementar**.  

> [!NOTE]
> Al ver las propiedades de una implementación existente, las secciones siguientes se corresponden con pestañas de la ventana de propiedades de la implementación:  
>
> - [General](#bkmk_deploy-general)
> - [Contenido](#bkmk_deploy-content)
> - [Configuración de implementación](#bkmk_deploy-settings)
> - [Programación](#bkmk_deploy-sched)
> - [Experiencia del usuario](#bkmk_deploy-ux)
> - [Alertas](#bkmk_deploy-alerts)

### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a> Información **general** sobre implementaciones

En la página **General** del Asistente para implementar software, especifique la información siguiente:  

- **Software**: este valor muestra la aplicación que se va a implementar. Seleccione **Examinar** para elegir otra aplicación.  

- **Colección**: seleccione **Examinar** para elegir la recopilación de destino de la implementación de esta aplicación.

- **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación**: almacene el contenido de la aplicación en el grupo de puntos de distribución predeterminado de la colección. Si no ha asociado la colección seleccionada a un grupo de puntos de distribución, esta opción estará atenuada.  

- **Distribuir contenido automáticamente para las dependencias**: si alguno de los tipos de implementación de la aplicación tiene dependencias, el sitio también enviará contenido de aplicaciones dependientes a los puntos de distribución.  

    >[!NOTE]
    > Si actualiza la aplicación dependiente después de implementar la aplicación principal, el sitio no distribuye automáticamente ningún contenido nuevo para la dependencia.

- **Comentarios (opcional)** : Especifique, si lo desea, un nombre y una descripción para este tipo de implementación.

### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a> Opciones de **contenido** de implementación

En la página **Contenido**, seleccione **Agregar** para distribuir el contenido para esta aplicación a un punto de distribución o a un grupo de puntos de distribución.

Si ha seleccionado la opción **Usar puntos de distribución predeterminados asociados a esta colección** en la página General, esta opción estará rellenada automáticamente. Solo un miembro del rol de seguridad **Administrador de aplicaciones** puede modificarla.

Si el contenido de aplicaciones ya se ha distribuido, se mostrará aquí.

### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a> **Configuración de implementación**

En la página **Configuración de implementación**, especifique la siguiente información:  

- **Acción**: en la lista desplegable, seleccione si la implementación va a **Instalar** o **Desinstalar** la aplicación.  

    > [!NOTE]  
    > Si crea una implementación para **Instalar** una aplicación y otra implementación para **Desinstalar** la misma aplicación en el mismo dispositivo, tendrá prioridad la implementación para **Instalar**.  

    Después de crear la acción de una implementación, no se puede cambiar.  

- **Finalidad**: en la lista desplegable, elija una de las siguientes opciones:  

  - **Disponible**: el usuario ve la aplicación en el Centro de software. Puede instalarla a petición.  

  - **Obligatorio**: el cliente instala automáticamente la aplicación según la programación que establezca. Si la aplicación no está oculta, un usuario puede realizar el seguimiento de su estado de implementación. También puede usar el Centro de software para instalar la aplicación antes de la fecha límite.  

    > [!NOTE]  
    > Al establecer la acción de implementación en **Desinstalar**, el propósito de implementación se establecerá automáticamente en **Obligatoria**. Este comportamiento no se puede cambiar.  

- **Permitir a los usuarios finales reparar esta aplicación**: a partir de la versión 1810, si ha creado la aplicación con una línea de comandos de reparación, habilite esta opción. Los usuarios ven una opción en el Centro de software para **reparar** la aplicación.<!--1357866-->  

- **Implementar previamente el software en el dispositivo primario del usuario**: si la implementación va dirigida a un usuario, seleccione esta opción para implementar la aplicación en el dispositivo primario del usuario. Esta opción no exige que el usuario inicie sesión antes de que se ejecute la implementación. Si el usuario necesita interactuar con la instalación, no seleccione esta opción. Esta opción solo está disponible cuando la implementación es **Obligatoria**.  

- **Enviar paquetes de reactivación**: si la implementación es **obligatoria**, Configuration Manager envía un paquete de reactivación a los equipos antes de que el cliente ejecute la implementación. Este paquete reactiva el equipo a la hora límite de instalación. Para poder usar esta opción, los equipos y las redes deben configurarse para Wake On LAN. Para obtener más información, vea [Planear la reactivación de clientes](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

- **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costos adicionales**: Esta opción solo está disponible cuando la implementación tiene un propósito **Requerido**.  

- **Actualizar automáticamente cualquier versión reemplazada de esta aplicación**: el cliente actualiza cualquier versión reemplazada de la aplicación con la aplicación de sustitución.

    > [!NOTE]
    > Esta opción siempre funciona, independientemente de la aprobación del administrador. Si un administrador ya aprobó la versión reemplazada, no necesitará aprobar también la versión que sustituye. La aprobación solo es necesaria para nuevas solicitudes, no para actualizaciones que reemplazan.<!--515824-->  
    >
    > Esta opción se puede habilitar o deshabilitar para el propósito de instalación **Disponible**. <!--1351266-->

#### <a name="approval-settings"></a><a name="bkmk_approval"></a> Configuración de aprobación

El comportamiento de aprobación de aplicación depende de si se habilita la característica opcional recomendada, **Aprobar solicitudes de aplicación de usuarios por dispositivo**.

- **Un administrador debe aprobar una solicitud para esta aplicación en el dispositivo**: si habilita la característica opcional, el administrador aprueba las solicitudes de usuario de la aplicación para que el usuario pueda instalarla en el dispositivo solicitado. Si el administrador aprueba la solicitud, el usuario solo tiene la posibilidad de instalar la aplicación en ese dispositivo. El usuario debe enviar otra solicitud para instalar la aplicación en otro dispositivo. La opción está atenuada cuando el propósito de implementación es **Obligatorio**, o bien cuando se implementa la aplicación en una colección de dispositivos.

- **Solicitar aprobación del administrador si los usuarios solicitan esta aplicación**: si no habilita la característica opcional, el administrador aprueba las solicitudes de usuario de la aplicación para que el usuario pueda instalarla. La opción está atenuada cuando el propósito de implementación es **Obligatorio**, o bien cuando se implementa la aplicación en una colección de dispositivos.  

Para obtener más información, vea [Aprobar aplicaciones](app-approval.md).

#### <a name="deployment-properties-deployment-settings"></a>Configuración de **propiedades de implementación**

Al ver las propiedades de una implementación, si la tecnología del tipo de implementación lo admite, se mostrará la siguiente opción en la pestaña **Configuración de implementación**:

**Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**. Para obtener más información, vea [Comprobar archivos ejecutables en ejecución antes de instalar una aplicación](#bkmk_exe-check).

### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a> Configuración de la **programación** de implementaciones

En la página **Programación**, establezca la hora en que se implementará esta aplicación o estará disponible para los dispositivos cliente.

De forma predeterminada, Configuration Manager hace que la directiva de implementación esté disponible para los clientes de forma inmediata. Si quiere crear la implementación, pero no quiere que esté disponible para los clientes hasta una fecha posterior, establezca la opción en **Programar la aplicación para que esté disponible**. Después, seleccione la fecha y hora, y especifique si se basan en UTC o en la hora local del cliente.

Si la implementación es **Obligatoria**, especifique también la **Fecha límite de instalación**. De forma predeterminada, esta fecha límite es lo antes posible.

Por ejemplo, necesita implementar una nueva aplicación de línea de negocio. Todos los usuarios necesitan instalarla antes de un momento específico, pero quiere proporcionarles la opción de instalarla de forma opcional anteriormente. Además, necesita asegurarse de que el sitio distribuya el contenido a todos los puntos de distribución. Programe la aplicación para que esté disponible en un plazo de cinco días desde el día actual. Esta programación le proporciona tiempo para distribuir el contenido y confirmar su estado. Después, establezca la fecha límite de instalación en un mes a partir del día actual. Los usuarios verán la aplicación en el Centro de software cuando esté disponible en un plazo de cinco días. Si no realiza ninguna acción, el cliente instalará automáticamente la aplicación en la fecha límite de instalación.

Si la aplicación que quiere implementar sustituye a otra aplicación, establezca la fecha límite de instalación cuando los usuarios reciban la nueva aplicación. Establezca la **Fecha límite de instalación** para actualizar los usuarios con la aplicación sustituida.

#### <a name="delay-enforcement-with-a-grace-period"></a>Retrasar el cumplimiento con un período de gracia

Puede que quiera ofrecer más tiempo a los usuarios para instalar las aplicaciones obligatorias *más allá* de las fechas límite que establezca. Este comportamiento suele ser necesario cuando un equipo está desactivado durante un tiempo prolongado y es necesario instalar un gran número de aplicaciones. Por ejemplo, cuando un usuario vuelve de vacaciones, tiene que esperar mucho tiempo mientras el cliente instala las implementaciones atrasadas. Para solucionar este problema, defina un período de gracia de cumplimiento.

- Primero, configure este período de gracia con la propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** en la configuración del cliente. Para obtener más información, vea el grupo [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent). Especifique un valor entre **1** y **120** horas.  

- En la página **Programación** de una implementación de aplicación obligatoria, habilite la opción **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario hasta el período de gracia definido en la configuración del cliente**. El período de gracia de cumplimiento se aplica a todas las implementaciones que tienen habilitada esta opción y que están destinadas a dispositivos en los que también se ha implementado la configuración del cliente.

Después de la fecha límite, el cliente instalará la aplicación en la primera ventana fuera del horario laboral que haya configurado el usuario, hasta ese período de gracia. Pero el usuario aún podrá abrir el Centro de software e instalar la aplicación en cualquier momento. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas.

:::image type="content" source="media/grace-period.svg" alt-text="Diagrama de escala de tiempo del período de gracia":::

<!-- SCCMDocs issue #1599 -->

> [!NOTE]
> La mayoría de las veces, esta característica aborda el escenario de cuando el dispositivo está apagado mientras el usuario está fuera de la oficina. Técnicamente, el período de gracia se inicia cuando el cliente obtiene la directiva después de la fecha límite de implementación. El mismo comportamiento se produce si detiene el servicio de cliente de Configuration Manager (CcmExec) y luego o reinicia en algún momento después de la fecha límite de implementación.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a> Configuración de la **experiencia del usuario** de implementación

En la página **Experiencia del usuario**, especifique información sobre cómo los usuarios pueden interactuar con la instalación de aplicaciones.

- **Notificaciones de usuario**: especifique si quiere mostrar una notificación en el Centro de software según las horas de disponibilidad configuradas. Esta opción también controla si se notifica a los usuarios en los equipos cliente. Para las implementaciones disponibles, no se puede seleccionar la opción **Ocultar en el Centro de software y ocultar todas las notificaciones**.  

  - **Cuando se requieren cambios de software, mostrar al usuario una ventana de cuadro de diálogo en lugar de una notificación del sistema**:<!--3555947-->: a partir de la versión 1902, seleccione esta opción para cambiar la experiencia del usuario para que sea más intrusiva. Solo se aplica a implementaciones necesarias. Para más información, consulte [Planeamiento del centro de software](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Instalación de software** y **Reinicio del sistema**: configure estas opciones únicamente para las implementaciones requeridas. Estas opciones especifican los comportamientos cuando la implementación alcanza la fecha límite más allá de las ventanas de mantenimiento definidas. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  

- **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: esta opción controla el comportamiento de instalación en los dispositivos Windows Embedded habilitados con un filtro de escritura. Elija esta opción para que los cambios se confirmen en la fecha límite de instalación o durante una ventana de mantenimiento. Al seleccionar esta opción, se necesita un reinicio y los cambios persisten en el dispositivo. De lo contrario, la aplicación se instala en la superposición temporal y se confirma más tarde.  

  - Al implementar una actualización de software en un dispositivo de Windows Embedded, asegúrese de que el dispositivo sea miembro de una colección que tenga configurada una ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento y los dispositivos de Windows Embedded, vea [Creación de aplicaciones de Windows Embedded](../get-started/creating-windows-embedded-applications.md).  

### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a> Alertas de **implementación**

En la página **Alertas**, configure la forma en que Configuration Manager genera las alertas para esta implementación. Si también usa System Center Operations Manager, configure también sus alertas. Solo se pueden configurar algunas alertas para las implementaciones necesarias.

## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a> Creación de una implementación por fases

<!--1358147-->
Las Implementaciones por fases permiten organizar un lanzamiento de software coordinado y secuencial según criterios y grupos personalizables. Por ejemplo, implemente la aplicación en una colección piloto y luego continúe automáticamente con la implementación según los criterios de éxito.

Vea los siguientes artículos para más información:  

- [Creación de una implementación por fases](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Administración y supervisión de implementaciones por fases](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a> Eliminar una implementación

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones** o **Grupos de aplicaciones**.  

1. Seleccione la aplicación o el grupo de aplicaciones que incluye la implementación que quiere eliminar.  

1. Cambie a la pestaña **Implementaciones** del panel de detalles y seleccione la implementación.  

1. En la cinta de opciones, en la pestaña **Implementación** del grupo **Implementación**, seleccione **Eliminar**.  

Al eliminar una implementación de aplicaciones, no se desinstalarán las instancias de la aplicación que los clientes ya hayan instalado. Para desinstalar estas aplicaciones, implemente la aplicación en los equipos con la opción **Desinstalar**. Si elimina la implementación de una aplicación, la aplicación ya no estará visible en el Centro de software. El mismo comportamiento se produce cuando se quita un recurso de la recopilación de destino para la implementación.

## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a> Notificaciones de usuario para implementaciones obligatorias

Cuando los usuarios reciben software obligatorio y seleccionan la opción **Posponer y volver a recordármelo**, pueden seleccionar entre las opciones siguientes:  

- **Más adelante**: especifica que las notificaciones se programan según la configuración de notificación establecida en la configuración del cliente.  

- **Hora fija**: especifica que la notificación se programa para mostrarse de nuevo después de la hora seleccionada. Por ejemplo, si selecciona 30 minutos, la notificación se mostrará de nuevo transcurrido ese tiempo.  

:::image type="content" source="media/ComputerAgentSettings.png" alt-text="Grupo Agente de equipo en la configuración de cliente predeterminada":::

El tiempo de aplazamiento máximo siempre se basa en los valores de notificación establecidos en la configuración del cliente en cada momento a lo largo de la escala de tiempo de implementación. Por ejemplo:  

- El valor **La fecha límite de la implementación es de más de 24 horas. Recordar al usuario cada (horas)** se configura en la página **Agente de equipo** para 10 horas.  

- El cliente muestra el cuadro de diálogo de notificación más de 24 horas antes de la fecha límite de la implementación.  

- En el cuadro de diálogo se muestran las opciones de aplazamiento hasta 10 horas, pero nunca más.  

- Cuando se acerca la fecha límite de la implementación, en el cuadro de diálogo se muestran menos opciones. Estas opciones son coherentes con la configuración de cliente relevante para cada componente de la escala de tiempo de implementación.  

En una implementación de alto riesgo, como una secuencia de tareas que implementa un sistema operativo, la experiencia de notificación del usuario es más intrusiva. En lugar de una notificación transitoria en la barra de tareas, en un cuadro de diálogo como el siguiente se muestra cada vez que se le notifica que se necesita mantenimiento de software crítico:

:::image type="content" source="media/client-toast-notification.png" alt-text="Cuadro de diálogo Software requerido en el que se notifica el mantenimiento de software crítico":::

## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a> Comprobar archivos ejecutables en ejecución

Configure una implementación para comprobar si determinados archivos ejecutables se están ejecutando en el cliente. Use esta opción para comprobar los procesos que podrían interrumpir la instalación de la aplicación. Si uno de estos archivos ejecutables está ejecutándose, el cliente impedirá la instalación del tipo de implementación. El usuario debe cerrar el archivo ejecutable en ejecución antes de que el cliente pueda instalar el tipo de implementación. Para las implementaciones con un propósito de Requerido, el cliente puede cerrar automáticamente el archivo ejecutable en ejecución.

1. Abra las **Propiedades** del tipo de implementación.

1. Vaya a la pestaña **Comportamiento de instalación** y seleccione **Agregar**.

1. En la ventana **Agregar archivo ejecutable**, escriba el nombre del archivo ejecutable de destino. De manera opcional, escriba un nombre descriptivo para la aplicación que le ayude a identificarla en la lista.

1. Seleccione **Aceptar** para guardar y cerrar la ventana de las propiedades del tipo de implementación.

1. Al implementar la aplicación, seleccione la opción **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**. Esta opción se encuentra en la pestaña **Configuración de implementación** de las propiedades de la implementación.  

> [!NOTE]
> Si configura una aplicación para comprobar los archivos ejecutables en ejecución y la incluye en el paso de secuencia de tareas [Instalar aplicación](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication), la secuencia de tareas no podrá instalarla. Si no configura este paso de secuencia de tareas para continuar después de un error, se produce un error en toda la secuencia de tareas.

### <a name="client-behaviors-and-user-notifications"></a>Comportamientos de cliente y notificaciones de usuario

Después de que los clientes reciban la implementación, se aplica el comportamiento siguiente:  

- Si ha implementado la aplicación como **Disponible** y un usuario intenta instalarla, el cliente le pedirá al usuario que cierre los archivos ejecutables especificados que estén ejecutándose antes de continuar con la instalación.  

- Si ha implementado la aplicación como **Obligatoria** y ha especificado la opción **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**, se mostrará una notificación en el cliente. Informará al usuario de que los archivos ejecutables especificados se cerrarán automáticamente cuando se alcance la fecha límite de instalación de la aplicación.  

  - Programe estos cuadros de diálogo en el grupo **Agente de equipo** de la configuración del cliente. Para obtener más información, vea [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent).  

  - Si no quiere que el usuario vea estos mensajes, seleccione la opción **Ocultar en el Centro de software y ocultar todas las notificaciones** en la pestaña **Experiencia del usuario** de las propiedades de la implementación. Para obtener más información, vea [Configuración de la experiencia del usuario de implementación](#bkmk_deploy-ux).  

- Si la aplicación se implementó como **Requerido** y no se especificó **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**, se produce un error en la instalación de la aplicación si una o varias de las aplicaciones especificadas está en ejecución.  

## <a name="deploy-user-available-applications"></a>Implementación de aplicaciones disponibles para el usuario

Al implementar aplicaciones como **Disponibles** para las recopilaciones de usuarios, los usuarios pueden examinar el Centro de software e instalar las aplicaciones que necesitan. En el caso de los clientes unidos a un dominio local, el Centro de software usa las credenciales de dominio del usuario para obtener la lista de aplicaciones disponibles desde el punto de administración.

Hay requisitos adicionales para los clientes basados en Internet, unidos a Azure Active Directory (Azure AD) o ambos.

### <a name="azure-ad-joined-devices"></a>Dispositivos unidos a Azure AD
<!-- 1322613 -->

Si implementa aplicaciones como disponibles para los usuarios, puede examinarlas e instalarlas a través del Centro de software en dispositivos de Azure AD. Configure los siguientes requisitos previos para habilitar este escenario:

- Habilitar el HTTPS en el punto de administración  

- Integrar el sitio con [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) para **administración en la nube**  

  - Configurar la [detección de usuarios de Azure AD](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

- Implementar una aplicación como disponible para una colección de usuarios desde Azure AD  

- Habilitar la configuración de cliente **Usar nuevo Centro de software** en el grupo [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent)  

- El sistema operativo de cliente debe ser Windows 10 y estar unido a Azure AD. Puede estar unido a un dominio en la nube pura o a Azure AD híbrido.  

- Para admitir clientes basados en Internet:  

  - [Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG)

  - Distribuir cualquier contenido de aplicaciones a un CMG habilitado para contenido o a un [punto de distribución en la nube](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

  - Habilite la configuración de cliente: **habilite solicitudes de directiva de usuario de clientes de Internet** en el grupo [Directiva de cliente](../../core/clients/deploy/about-client-settings.md#client-policy).  

- Para admitir clientes en la intranet:  

  - Agregar el CMG habilitado para contenido o el punto de distribución en la nube a un grupo de límites utilizado por los clientes  

  - Los clientes necesitan resolver el nombre de dominio completo (FQDN) del punto de administración habilitado para HTTPS.  

  > [!NOTE]
  > Para un cliente detectado como en la intranet pero que se comunica a través de Cloud Management Gateway (CMG), en la versión 2002 y anterior de Configuration Manager, el Centro de software usa la autenticación de Windows. Al intentar obtener la lista de aplicaciones disponibles para el usuario a través de CMG, se produciría un error. A partir de la versión 2006, usa la identidad de Azure Active Directory (Azure AD) para los dispositivos unidos a Azure AD. Estos dispositivos pueden estar unidos a la nube o a híbrido.<!--6935376-->

## <a name="next-steps"></a>Pasos siguientes

- [Supervisar aplicaciones](monitor-applications-from-the-console.md)
- [Solución de problemas de implementación de aplicaciones](troubleshoot-application-deployment.md)
- [Tareas de administración para aplicaciones](management-tasks-applications.md)
- [Manual del usuario del Centro de software](../../core/understand/software-center.md)
