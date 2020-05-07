---
title: Grupos de orquestaciones
titleSuffix: Configuration Manager
description: Cree grupos de orquestaciones e implemente actualizaciones en ellos.
ms.date: 04/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cddbebea-b418-4839-b0a8-7809486c8a4c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9a307df23900abb985535b2ab59a5ff172cafb7
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254918"
---
# <a name="orchestration-groups-in-configuration-manager"></a>Grupos de orquestaciones en Configuration Manager
<!--3098816-->
*Se aplica a: Configuration Manager (rama actual)*

A partir de la versión 2002 de Configuration Manager versión, se pueden crear grupos de orquestaciones. Cree un grupo de orquestaciones para controlar mejor la implementación de las actualizaciones de software en los dispositivos. Muchos administradores de servidores deben administrar cuidadosamente las actualizaciones de cargas de trabajo específicas y automatizar los comportamientos entre ellas.

Un grupo de orquestaciones ofrece la flexibilidad de actualizar los dispositivos en función de un porcentaje, un número específico o un orden explícito. También puede ejecutar un script de PowerShell antes y después de que los dispositivos ejecuten la implementación de actualización.

Los miembros de un grupo de orquestaciones pueden ser cualquier cliente de Configuration Manager, no solo servidores. Las reglas del grupo de orquestaciones se aplican a los dispositivos de todas las implementaciones de actualizaciones de software en cualquier colección que contenga un miembro del grupo de orquestaciones. Se siguen aplicando otros comportamientos de implementación. Por ejemplo, las ventanas de mantenimiento y las programaciones de implementación.

> [!NOTE]
> En esta versión de Configuration Manager, la creación de grupos de orquestaciones es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](../../core/servers/manage/pre-release-features.md).  
>
> La característica **Grupos de orquestaciones** es la evolución de la característica [Grupos de servidores](service-a-server-group.md). Un grupo de orquestación es un objeto de Configuration Manager.

## <a name="orchestration-group-usage-example"></a>Ejemplo de uso de un grupo de orquestación

- Como administrador de actualizaciones de software, administra todas las actualizaciones de su organización.
- Tiene una colección amplia para todos los servidores y una colección amplia para todos los clientes. Implementa todas las actualizaciones en estas recopilaciones.
- Los administradores de SQL desean controlar todo el software instalado en los servidores SQL Server. Quieren revisar cinco servidores en un orden específico. Su proceso actual consiste en detener manualmente servicios específicos antes de instalar las actualizaciones y, después de eso, reiniciar los servicios.
- Crea un grupo de orquestaciones y agrega los cinco servidores SQL Server. También agrega scripts previos y posteriores mediante los scripts de PowerShell proporcionados por los administradores de SQL.
- Durante el ciclo de actualización siguiente, las actualizaciones de software se crean e implementan de la manera habitual en la amplia colección de servidores. Los administradores de SQL ejecutan la implementación y el grupo de orquestaciones automatiza el orden y los servicios.

## <a name="prerequisites"></a>Requisitos previos

### <a name="site-server-and-permission-prerequisites"></a>Requisitos previos de permisos y servidores de sitio
- Para ver todos los grupos de orquestaciones y las actualizaciones de esos grupos, la cuenta debe ser **Administrador total**.
   - La administración basada en roles para los grupos de orquestaciones no está disponible actualmente.
- Habilite la característica **Grupos de orquestaciones**. Para más información, consulte [Habilitar características opcionales](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
   - Cuando habilita los **grupos de orquestaciones**, el sitio deshabilita la característica **Grupos de servidores**. Este comportamiento evita cualquier conflicto entre las dos características.

### <a name="client-prerequisites"></a>Requisitos previos del cliente

- Actualice los dispositivos de destino a la última versión del cliente de Configuration Manager.
- Los miembros de un grupo de orquestación deben asignarse al mismo sitio.
- Los dispositivos no pueden estar en más de un grupo de orquestación.
   - Los dispositivos que ya estén en un grupo de orquestación no se podrán seleccionar al agregar nuevos miembros.


## <a name="limitations"></a>Limitaciones

- Puede tener hasta 1000 miembros en un grupo de orquestación.
- Los grupos de orquestaciones no funcionan en el modo de interoperabilidad. Para obtener más información, vea [Interoperabilidad entre diferentes versiones de Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#bkmk_mixed). <!--6389000-->
- Si los usuarios inician actualizaciones desde el Centro de software, se omitirá la orquestación. <!--6362887-->

## <a name="server-groups-are-automatically-updated-to-orchestration-groups"></a>Actualización automática de grupos de servidores a grupos de orquestaciones

La característica **Grupos de orquestaciones** es la evolución de la característica [Grupos de servidores](service-a-server-group.md). Cuando instala Configuration Manager 2002 o una versión posterior y tiene grupos de servidores habilitados, estos grupos se mueven automáticamente a grupos de orquestaciones.

## <a name="create-an-orchestration-group"></a>Creación de un grupo de orquestación

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Grupo de orquestaciones**.

1. En la cinta de opciones, seleccione **Create Orchestration Group** (Crear grupo de orquestaciones) para abrir el **Asistente para la creación de un grupo de orquestaciones**.

1. En la página **General**, asigne un **Nombre** al grupo de orquestaciones y, de manera opcional, una **Descripción**. Especifique los valores para los siguientes elementos:
   - **Tiempo de espera del grupo de orquestación (en minutos)** : Límite de tiempo para que todos los miembros del grupo completen la instalación de actualizaciones.
   - **Tiempo de espera del miembro del grupo de orquestación (en minutos)** : Límite de tiempo para que un único dispositivo del grupo complete la instalación de la actualización.

1. En la página **Selección de miembro**, especifique primero el **Código de sitio**. Luego, seleccione **Examinar** para agregar recursos de dispositivos como miembros de este grupo de orquestación. **Busque** dispositivos por nombre y, luego, **agréguelos**. También puede filtrar la búsqueda a una sola recopilación mediante **Buscar en la recopilación**.  Seleccione **Aceptar** cuando termine de agregar dispositivos a la lista de recursos seleccionada.
   - Al seleccionar recursos para el grupo, solo se muestran los clientes válidos. Se realizan comprobaciones para comprobar el código de sitio, que el cliente esté instalado y que los recursos no estén duplicados.

1. En la página **Rule Selection** (Selección de regla), seleccione una de estas opciones:

   - **Allow a percentage of the machines to be updated at the same time** (Permitir que un porcentaje de las máquinas se actualice al mismo tiempo) y seleccione o escriba un número para este porcentaje. Use esta opción para permitir a futuro un tamaño flexible del grupo de orquestaciones. Por ejemplo, el grupo de orquestaciones contiene 50 dispositivos y establece este valor en 10. Durante una implementación de actualizaciones de software, Configuration Manager permite que cinco dispositivos ejecuten la implementación de manera simultánea. Si más tarde aumenta el tamaño del grupo de orquestaciones a 100 dispositivos, se actualizarán 10 dispositivos a la vez.

   - **Allow a number of the machines to be updated at the same time** (Permitir que un número de las máquinas se actualice al mismo tiempo) y seleccione o escriba un número para este recuento específico. Use esta opción para limitar siempre a un número específico de dispositivos, independientemente del tamaño total del grupo de orquestaciones.

   - **Specify the maintenance sequence** (Especificar la secuencia de mantenimiento) y ordene los recursos seleccionados según corresponda. Use esta opción para definir explícitamente el orden en el que los dispositivos ejecutan la implementación de actualizaciones de software.

1. En la página **Script previo**, escriba un script de PowerShell para ejecutarlo en cada dispositivo *antes* de que se ejecute la implementación. El script debe devolver un valor de `0` si se completa correctamente o `3010`, si se completa correctamente pero requiere reiniciar.

1. En la página **Script posterior**, escriba un script de PowerShell para ejecutarlo en cada dispositivo *después* de que se ejecute la implementación. De lo contrario, el comportamiento es el mismo que con PreScript.

1. Complete el asistente.

> [!WARNING]
> Asegúrese de que los scripts previos y posteriores se prueban antes de usarlos con los grupos de orquestaciones. Los scripts previos y posteriores no tienen tiempo de espera y se ejecutarán hasta que se alcanza el tiempo de espera del miembro del grupo de orquestación.

## <a name="view-orchestration-groups-and-members"></a>Visualización de grupos y miembros de orquestación

En el área de trabajo **Activos y compatibilidad**, seleccione el nodo **Grupo de orquestación**. Para ver los miembros, seleccione un grupo de orquestación y luego **Mostrar miembros** en la cinta de opciones. Para obtener más información acerca de las columnas disponibles para los nodos, consulte [Supervisión de los miembros y los grupos de orquestación](#bkmk_orch_monitor).

## <a name="edit-or-delete-an-orchestration-group"></a>Edición o eliminación de un grupo de orquestación

Para eliminar un grupo de orquestación, selecciónelo y, después, haga clic en la opción **Eliminar** situada en la cinta, o bien desde el menú contextual. Para editar un grupo de orquestación, selecciónelo y, después, haga clic en la opción **Propiedades** situada en la cinta, o bien desde el menú contextual. Cambie la configuración de las pestañas siguientes:

   - **General**: 
      - **Nombre**: nombre del grupo de orquestación.
      - **Descripción**: descripción del grupo de orquestación (opcional).
      - **Tiempo de espera del grupo de orquestación (en minutos)** : Límite de tiempo para que todos los miembros del grupo completen la instalación de actualizaciones.
      - **Tiempo de espera del miembro del grupo de orquestación (en minutos)** : Límite de tiempo para que un único dispositivo del grupo complete la instalación de la actualización.

  - **Selección de miembros**:
     - **Código de sitio**: código de sitio del grupo de orquestación.
     - **Miembros**: haga clic en **Agregar** para seleccionar dispositivos adicionales para el grupo de orquestación. Haga clic en **Quitar** para quitar el dispositivo seleccionado.

   - **Selección de reglas**:
      - **Allow a percentage of the machines to be updated at the same time** (Permitir que un porcentaje de las máquinas se actualice al mismo tiempo) y seleccione o escriba un número para este porcentaje. Use esta opción para permitir a futuro un tamaño flexible del grupo de orquestaciones. Por ejemplo, el grupo de orquestaciones contiene 50 dispositivos y establece este valor en 10. Durante una implementación de actualizaciones de software, Configuration Manager permite que cinco dispositivos ejecuten la implementación de manera simultánea. Si más tarde aumenta el tamaño del grupo de orquestaciones a 100 dispositivos, se actualizarán 10 dispositivos a la vez.
      - **Allow a number of the machines to be updated at the same time** (Permitir que un número de las máquinas se actualice al mismo tiempo) y seleccione o escriba un número para este recuento específico. Use esta opción para limitar siempre a un número específico de dispositivos, independientemente del tamaño total del grupo de orquestaciones.
      - **Indique la secuencia de mantenimiento**: ordene los recursos seleccionados en el orden adecuado. Use esta opción para definir explícitamente el orden en el que los dispositivos ejecutan la implementación de actualizaciones de software.

   - **Script previo**: 
       - escriba un script de PowerShell para ejecutarlo en cada dispositivo *antes* de que se ejecute la implementación. El script debe devolver un valor de `0` si se completa correctamente o `3010`, si se completa correctamente pero requiere reiniciar.
       
   - **Script posterior**:
      - escriba un script de PowerShell para ejecutarlo en cada dispositivo *después* de que se ejecute la implementación. El script debe devolver un valor de `0` si se completa correctamente o `3010`, si se completa correctamente pero requiere reiniciar.
   > [!WARNING]
   > Asegúrese de que los scripts previos y posteriores se prueban antes de usarlos con los grupos de orquestaciones. Los scripts previos y posteriores no tienen tiempo de espera y se ejecutarán hasta que se alcanza el tiempo de espera del miembro del grupo de orquestación.


## <a name="start-orchestration"></a>Inicio de la orquestación

1. [Implemente las actualizaciones de software](deploy-software-updates.md) en una recopilación que contenga los miembros del grupo de orquestación.

1. La orquestación se inicia cuando cualquier cliente del grupo intenta instalar una actualización de software dentro de la fecha límite o durante una ventana de mantenimiento. Se inicia para todo el grupo y se asegura de que los dispositivos se actualicen siguiendo las reglas del grupo de orquestaciones.
1. Puede iniciar manualmente la orquestación seleccionándola en el nodo **Grupo de orquestación** y, a continuación, eligiendo **Iniciar orquestación** en la cinta de opciones o en el menú contextual.
1. Si un grupo de orquestación se encuentra en un estado *con errores*:
   1. Determine por qué se produjo un error en la orquestación y resuelva los problemas.
   1. [Restablezca el estado de la orquestación para los miembros del grupo](#bkmk_reset).
   1. En el nodo **Grupo de orquestación**, haga clic en el botón **Iniciar orquestación** para reiniciarla.
   [![Iniciar orquestación](./media/3098816-start-orchestration.png)](./media/3098816-start-orchestration.png#lightbox)


> [!TIP]
> - Los grupos de orquestaciones solo se aplican a las implementaciones de actualizaciones de software. No se aplican a otras implementaciones.
> - Puede hacer clic con el botón derecho en un miembro del grupo de orquestación y seleccionar **Restablecer miembro del grupo de orquestación**. Esto le permite volver a ejecutar la orquestación.


## <a name="monitor-orchestration-groups"></a><a name="bkmk_orch_monitor"></a> Supervisión de grupos de orquestaciones

En el área de trabajo **Activos y compatibilidad**, seleccione el nodo **Grupo de orquestación**. Agregue cualquiera de las columnas siguientes para obtener información acerca de los grupos:

- **Nombre de orquestación**: nombre del grupo de orquestación.
- **Código de sitio**: código de sitio para el grupo.
- **Tipo de orquestación**: es uno de los tipos siguientes:
   - Número
   - Porcentaje
   - Secuencia

- **Valor de orquestación**: cantidad o porcentaje de miembros que pueden obtener un bloqueo simultáneamente. **Valor de la orquestación** solo se rellena cuando **Tipo de orquestación** es un *Número* o un *Porcentaje*.  
- **Estado de orquestación**: en curso durante la orquestación. inactivo cuando no está en curso.
- **Hora de inicio de orquestación**: fecha y hora de inicio de la orquestación.
- **Número de secuencia actual**: indica para qué miembro de la orquestación de grupo está activa. Este número corresponde al **número de secuencia** para el miembro.  
- **Tiempo de espera de la orquestación (en minutos)** : Valor del **tiempo de espera del grupo de orquestación (en minutos)** establecido en la página **General** al crear el grupo, o en la pestaña **General** al editar el grupo.
- **Tiempo de espera del miembro del grupo de orquestación (en minutos)** : el valor de **tiempo de espera del miembro del grupo de orquestación (en minutos)** establecido en la página **General** al crear el grupo, o en la pestaña **General** al editar el grupo.
- **Identificador de grupo de orquestación**: identificador del grupo, el identificador se usa en los registros y en la base de datos.
- **Identificador único del grupo de orquestación**: Identificador único del grupo, el identificador único se utiliza en los registros y en la base de datos.

## <a name="monitor-orchestration-group-members"></a>Supervisión de los miembros del grupo de orquestación

En el nodo **Grupo de orquestaciones**, seleccione un grupo de orquestaciones. En la cinta de opciones, seleccione **Mostrar miembros**. Puede ver los miembros del grupo y su estado de orquestación. Agregue cualquiera de las columnas siguientes para obtener información sobre los miembros:

- **Nombre**: nombre de dispositivo del miembro del grupo de orquestación.
- **Estado actual**: proporciona el estado del dispositivo miembro.
   - **En curso** durante la orquestación.
   - **En espera**: indica que el cliente está esperando el bloqueo de su turno para instalar las actualizaciones.
   - **Inactivo** cuando la orquestación está completa o no se está ejecutando.
- **Código de estado**: Puede hacer clic con el botón derecho en el miembro del grupo de orquestación y seleccionar **Restablecer miembro del grupo de orquestación**. Este restablecimiento le permite volver a ejecutar la orquestación. Los estados incluyen: 
   - Inactivo
   - En espera, el dispositivo está esperando su turno
   - En curso, instalando una actualización
   - Failed
   - Reinicio pendiente
- **Hora del bloqueo adquirido**: el cliente solicita los bloqueos en función de su directiva. Una vez que el cliente adquiere un bloqueo, la orquestación se desencadena en él.  
-**Hora del último estado notificado**: hora en que el miembro comunicó por última vez un estado.
- **Número de secuencia**: ubicación del cliente en la cola para la instalación de actualizaciones.
- **Código de sitio**: código de sitio para el miembro.
- **Actividad de cliente**: indica si el cliente está activo o inactivo.
- **Usuarios primarios**: qué usuarios son primarios para el dispositivo.
- **Tipo de cliente**: qué tipo de dispositivo es el cliente.
- **Usuario que ha iniciado sesión actualmente**: usuario que ha iniciado sesión actualmente en el dispositivo.
- **Identificador de OG**: identificador del grupo de orquestación al que pertenece el miembro.
- **Identificador exclusivo de OG**: identificador exclusivo del grupo de orquestación al que pertenece el miembro.
- **Identificador de recurso**: identificador de recurso del dispositivo.

## <a name="reset-the-orchestration-state-for-a-group-member"></a><a name="bkmk_reset"></a> Restablecimiento del estado de la orquestación para un miembro del grupo

Si quiere volver a ejecutar la orquestación en un miembro del grupo, puede borrar los estados *completados* o *con errores*. Para borrar el estado, haga clic con el botón derecho en el miembro del grupo de orquestación y seleccione **Restablecer miembro del grupo de orquestación**. También puede hacer clic en **Restablecer miembro del grupo de orquestación** en la cinta de opciones. Antes de restablecer el estado, debe comprobar el cliente para ver por qué se ha producido un error y debe corregir los problemas encontrados.
   [![Restablecer miembro del grupo de orquestación](./media/3098816-reset-group-member.png)](./media/3098816-reset-group-member.png#lightbox)

## <a name="log-files"></a>Archivos de registro

Use los archivos de registro siguientes en el servidor de sitio para ayudar a supervisar y solucionar problemas:

### <a name="site-server"></a>Servidor de sitio

- **Policypv.log**: muestra que el sitio tiene apunta el grupo de orquestación a los clientes.
- **SMS_OrchestrationGroup.log**: muestra los comportamientos del grupo de orquestación.

### <a name="client"></a>Cliente

- **MaintenanceCoordinator.log**: muestra la adquisición de bloqueos, la instalación de actualizaciones, los scripts previos y posteriores y el proceso de liberación del bloqueo.
- **UpdateDeployment.log**: muestra el proceso de instalación de la actualización.
- **PolicyAgent.log**: Comprueba si el cliente está en un grupo de orquestación.

## <a name="next-steps"></a>Pasos siguientes

[Implementar actualizaciones de software](deploy-software-updates.md)