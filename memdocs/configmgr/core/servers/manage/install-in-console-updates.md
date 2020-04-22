---
title: Actualización en la consola
titleSuffix: Configuration Manager
description: Instalación de actualizaciones en Configuration Manager desde Microsoft Cloud
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fee0cdf72ae8975d26bebd4da765941116421c25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694593"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Instalar actualizaciones en consola para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager se sincroniza con el servicio de Microsoft Cloud para obtener actualizaciones. Después, puede instalar estas actualizaciones desde la consola de Configuration Manager.

## <a name="get-available-updates"></a>Obtención de actualizaciones disponibles

El sitio solo descargará actualizaciones válidas para su infraestructura y versión. Esta sincronización puede ser automática o manual, según cómo configure el punto de conexión de servicio para la jerarquía:

- En **modo en línea**, el punto de conexión de servicio se conecta al servicio en la nube de Microsoft automáticamente y descarga las actualizaciones aplicables.  

    De manera predeterminada, Configuration Manager busca nuevas actualizaciones cada 24 horas. Busque actualizaciones de forma manual en la consola de Configuration Manager. Vaya al área de trabajo **Administración**, seleccione el nodo **Actualizaciones y mantenimiento** y, después, haga clic en **Buscar actualizaciones** en la cinta de opciones.  

- En el **modo sin conexión**, el punto de conexión de servicio no se conecta al servicio en la nube de Microsoft. Para descargar y luego importar las actualizaciones disponibles, puede [usar la herramienta de conexión de servicio](use-the-service-connection-tool.md).  

> [!NOTE]  
> Si es necesario, puede importar correcciones fuera de banda en la consola. Para ello, use la [herramienta de registro de actualizaciones](use-the-update-registration-tool-to-import-hotfixes.md). Estas correcciones fuera de banda complementan las actualizaciones que obtendrá al sincronizar con el servicio de Microsoft Cloud.  

Cuando se sincronicen las actualizaciones, podrá verlas en la consola de Configuration Manager. Vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**.  

- Las actualizaciones no instaladas se muestran con el estado **Disponible**.  

- Las actualizaciones instaladas se muestran con el estado **Instalada**. Solo se muestra la última actualización instalada. Para ver las actualizaciones instaladas anteriormente, seleccione **Historial** en la cinta de opciones.  

Antes de configurar el punto de conexión de servicio, es conveniente conocer y planear sus usos adicionales. Los usos siguientes pueden afectar al modo en que se configura este rol de sistema de sitio:  

- El punto de conexión de servicio se usa para cargar la información de uso sobre su sitio. Esta información ayuda al servicio en la nube de Microsoft a identificar las actualizaciones que están disponibles para la versión actual de su infraestructura. Para obtener más información, vea [Diagnósticos y datos de uso](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Para entender mejor lo que ocurre cuando se descargan las actualizaciones, vea los siguientes diagramas de flujo:  

- [Diagrama de flujo: descargar actualizaciones](download-updates-flowchart.md)  

- [Diagrama de flujo: replicación de actualización](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Asignar permisos para ver y administrar actualizaciones y características

Para que un usuario vea las actualizaciones en la consola, debe tener asignado un rol de seguridad de administración basado en roles que incluya la clase de seguridad **Paquetes de actualización**. Esta clase concede acceso para ver y administrar las actualizaciones en la consola de Configuration Manager.

### <a name="about-the-update-packages-class"></a>Sobre la clase Paquetes de actualización

De forma predeterminada, la clase **Paquetes de actualización** (SMS_CM_Updatepackages) forma parte de los siguientes roles de seguridad integrados con los permisos indicados:  

- **Administrador total** con permisos **Modificar** y **Lectura** :  

  - Un usuario con este rol de seguridad y acceso al ámbito de seguridad **Todo** puede ver e instalar las actualizaciones. El usuario también puede habilitar características durante la instalación y habilitar características individuales cuando se actualice el sitio.  

  - Un usuario con este rol de seguridad y acceso al ámbito de seguridad **Predeterminado** puede ver e instalar las actualizaciones. El usuario también puede habilitar características durante la instalación y ver características cuando se actualice el sitio. Pero este usuario no podrá habilitar las características cuando se actualice el sitio.  

- **Analista de solo lectura** con permisos **Lectura** :  

  - Un usuario con este rol de seguridad y acceso al ámbito **Predeterminado** puede ver actualizaciones pero no instalarlas. Este usuario también podrá ver características después de actualizar el sitio, pero no podrá habilitarlas.  

### <a name="permissions-required-for-updates-and-servicing"></a>Permisos necesarios para las actualizaciones y el mantenimiento

- Use una cuenta que tenga asignado un rol de seguridad con la clase **Paquetes de actualización** y los permisos **Modificar** y **Lectura**.  

- Asigne la cuenta al ámbito **Predeterminado**.  

### <a name="permissions-to-only-view-updates"></a>Permisos para solo ver las actualizaciones

- Use una cuenta que tenga asignado un rol de seguridad con la clase **Paquetes de actualización** y que tenga solo con el permiso **Lectura**.  

- Asigne la cuenta al ámbito **Predeterminado**.  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Permisos necesarios para habilitar características cuando se actualice el sitio

- Use una cuenta que tenga asignado un rol de seguridad con la clase **Paquetes de actualización** y los permisos **Modificar** y **Lectura**.  

- Asigne la cuenta al ámbito **Todo**.  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Antes de instalar una actualización en la consola  

Revise los pasos siguientes antes de instalar una actualización desde la consola de Configuration Manager.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Paso 1: revisar la lista de comprobación de actualización  

Revise la lista de comprobación de actualización aplicable para las acciones que deben realizarse antes de iniciar la actualización:

- [Lista de comprobación para la instalación de la actualización 2002](checklist-for-installing-update-2002.md)

- [Lista de comprobación para la instalación de la actualización 1910](checklist-for-installing-update-1910.md)  

- [Lista de comprobación para la instalación de la actualización 1906](checklist-for-installing-update-1906.md)  

- [Lista de comprobación para la instalación de la actualización 1902](checklist-for-installing-update-1902.md)

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a> Paso 2: ejecutar el comprobador de requisitos previos antes de instalar una actualización  

Antes de instalar una actualización, puede ejecutar la comprobación de requisitos previos para la actualización. Si ejecuta la comprobación de requisitos previos antes de instalar una actualización:  

- Los archivos de actualización se replican en otros sitios antes de instalar la actualización.  

- La comprobación de requisitos previos se volverá a ejecutar automáticamente cuando instale la actualización.  

> [!NOTE]  
> Al iniciar una comprobación de requisitos previos y, después, ver el estado, parecerá que la fase **Instalación** está activa. Pero, en realidad, no se instalará la actualización en el sitio. Para ejecutar la comprobación de requisitos previos, el proceso de actualización extrae el paquete de la biblioteca de contenido. Después, copia el paquete en una carpeta de almacenamiento provisional, donde puede acceder a las comprobaciones de requisitos previos actuales. El mismo proceso también se ejecuta al instalar una actualización. Este comportamiento se debe a que la fase de instalación se muestra con el estado **En curso**. En la categoría de instalación solo se muestra el paso *Extraer paquete de actualización*.  

Más adelante, cuando instale la actualización, puede configurarla para omitir las advertencias de comprobación de requisitos previos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para ejecutar el Comprobador de requisitos previos antes de instalar una actualización  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**.  

2. Haga clic con el botón derecho en el paquete de actualización para el que quiera ejecutar la comprobación de requisitos previos.  

3. Seleccione **Ejecutar comprobación de requisitos previos** en la cinta de opciones.  

    Cuando se ejecuta la comprobación de requisitos previos, el contenido de la actualización se replica a los sitios secundarios. Puede ver el archivo **distmgr.log** en el servidor de sitio para confirmar que el contenido se replique correctamente.  

4. Para ver los resultados de la comprobación de requisitos previos:  

    1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**.  

    2. Seleccione el nodo **Actualizaciones y estado de mantenimiento** y busque el estado de los requisitos previos.  

    3. Para obtener más información, vea el archivo **ConfigMgrPrereq.log** en el servidor de sitio.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a> Instalación de actualizaciones en la consola  

Cuando esté listo para instalar actualizaciones en la consola de Configuration Manager, empiece con el sitio de primer nivel de la jerarquía. Este sitio puede ser el sitio de administración central o un sitio primario independiente.  

Le recomendamos que instale la actualización fuera del horario comercial habitual para cada sitio con el fin de minimizar el efecto sobre las operaciones empresariales. El motivo es que, al instalar actualizaciones, pueden realizarse acciones como la reinstalación de componentes de sitio y roles del sistema de sitio.  

- Los sitios primarios secundarios inician la actualización automáticamente cuando el sitio de administración central termina de instalarla. Este es el proceso recomendado y predeterminado. Para controlar el momento en que un sitio primario instala actualizaciones, use [Períodos para tareas administrativas para servidores de sitios](service-windows.md).  

- Cuando se complete la actualización del sitio principal primario, actualice de forma manual los sitios secundarios desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.  

- Cuando se usa una consola de Configuration Manager después de actualizar el sitio, también se le pide que actualice la consola.  

- Después de que el servidor de sitio completa correctamente la instalación de una actualización, actualiza automáticamente todos los roles de sistema de sitio aplicables. Pero no se reinstalan todos los puntos de distribución y pasan a estar sin conexión para actualizar al mismo tiempo. En su lugar, el servidor de sitio usa la configuración de distribución de contenido del sitio para distribuir la actualización a un subconjunto de puntos de distribución a la vez. El resultado es que solo algunos puntos de distribución se desconectan para instalar la actualización. Los puntos de distribución que todavía no han empezado a actualizarse o que han completado la actualización permanecen en línea y pueden proporcionar contenido a los clientes.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Información general sobre la instalación de actualizaciones en la consola  

#### <a name="1-when-the-update-installation-starts"></a>1. Cuando se inicia la instalación de la actualización

Verá el asistente para actualizaciones, donde se muestra una lista de las áreas de producto que se corresponden con la actualización.  

- En la página **General** del asistente, puede configurar **Advertencias de requisitos previos** según sea necesario:  

  - Los errores de requisitos previos siempre detienen la instalación de la actualización. Solucione los errores para poder reintentar la instalación de la actualización de manera satisfactoria. Para obtener más información, consulte [Reintento de la instalación de una actualización con errores](#bkmk_retry).  

  - Las advertencias de requisitos previos también pueden detener la instalación de la actualización. Solucione las advertencias antes de reintentar la instalación de la actualización. Para obtener más información, consulte [Reintento de la instalación de una actualización con errores](#bkmk_retry).  

  - **Pase por alto las advertencias de las comprobaciones de requisitos previos e instale esta actualización aunque falten requisitos**: establece una condición para la instalación de actualizaciones que omite las advertencias de requisitos previos. Esta opción permite continuar con la instalación de la actualización. Si no selecciona esta opción, la instalación de actualizaciones se detiene cuando el proceso se encuentra una advertencia. A menos que ya haya ejecutado anteriormente la comprobación de requisitos previos y haya resuelto las advertencias de requisitos previos para un sitio, no le recomendamos que use esta opción.  

    En las áreas de trabajo **Administración** y **Supervisión**, el nodo Actualizaciones y mantenimiento tiene un botón en la cinta de opciones denominado **Omitir advertencias de requisitos previos**. Este botón está disponible cuando se produce un error al completar la instalación de un paquete de actualización debido a las advertencias de comprobación de los requisitos previos. Por ejemplo, instale una actualización sin utilizar la opción para ignorar las advertencias de requisitos previos (desde el Asistente para actualizaciones). La instalación de actualización se detiene con un estado de advertencia de requisitos previos, pero sin errores. Más tarde, seleccione **Omitir advertencias de requisitos previos** en la cinta de opciones. Esta acción desencadena una continuación automática de esa instalación de actualizaciones que omite las advertencias de requisitos previos. Cuando se usa esta opción, la instalación de la actualización continúa automáticamente después de unos minutos.  

- Si hay una actualización válida para el cliente de Configuration Manager, pruebe la actualización de cliente con un conjunto limitado de clientes. Para obtener más información, vea [Cómo probar las actualizaciones de cliente en una recopilación de preproducción](../../clients/manage/upgrade/test-client-upgrades.md).  

#### <a name="2-during-the-update-installation"></a>2. Durante la instalación de la actualización

Como parte de la instalación de actualizaciones, Configuration Manager realiza las acciones siguientes:  

- Vuelve a instalar los componentes afectados, como los roles de sistema de sitio o la consola de Configuration Manager.  

- Administra las actualizaciones de los clientes en función de las selecciones realizadas para las comprobaciones piloto de clientes y para las [actualizaciones de cliente automáticas](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).  

- Normalmente, los servidores de sistema de sitio no necesitan reiniciarse como parte de la actualización. Si un rol usa .NET y el paquete actualiza ese componente de requisitos previos, puede que se reinicie el sistema de sitio.  

> [!TIP]  
> Al instalar actualizaciones de Configuration Manager, el sitio también actualiza la carpeta CD.Latest. Para obtener más información, vea [La carpeta CD.Latest](the-cd.latest-folder.md).  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Supervisar el progreso de las actualizaciones mientras se instalan

Para supervisar el progreso, siga este procedimiento:  

- En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**. En este nodo se muestra el estado de instalación de todos los paquetes de actualización.  

- En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Actualizaciones y estado de mantenimiento**. En este nodo, solo se muestra el estado de la instalación del paquete de actualización que el sitio esté instalando.  

    La instalación de actualizaciones se divide en varias fases para facilitar la supervisión. Por cada una de las fases siguientes, en los detalles adicionales del estado de la instalación, se indica qué archivo de registro contiene más información:  

  - **Descargar**: esta fase solo se aplica en el sitio de primer nivel con el punto de conexión de servicio.

  - **replicación**

  - **Comprobación de requisitos previos**

  - **Instalación**

  - **Después de la instalación**: Para obtener más información, vea [Tareas posteriores a la instalación](#post-installation-tasks).  

- Vea el archivo **CMUpdate.log** en `<ConfigMgr_Installation_Directory>\Logs` en el servidor de sitio.  

>[!NOTE]
> A partir de la versión 1906, puede ver el estado de la tarea **Actualización de la base de datos de ConfigMgr** durante la fase de **instalación**.
>
> - Si se bloquea la actualización de la base de datos, se le proporcionará la advertencia **En curso, requiere atención**.
>   - En cmupdate.log se registrará el nombre del programa y el identificador de sesión de SQL que bloquea la actualización de la base de datos.
> - Cuando la actualización de la base de datos deje de estar bloqueada, el estado se restablecerá a **En curso** o **Completado**.
>   - Cuando la actualización de la base de datos está bloqueada, se realiza una comprobación cada cinco minutos para ver el bloqueo persiste.

#### <a name="4-when-the-update-installation-completes"></a>4. Cuando se completa la instalación de la actualización

Después de que se completa la primera actualización del sitio:  

- Los sitios primarios secundarios instalan la actualización automáticamente. No es necesario hacer nada.  

- Necesita actualizar manualmente los sitios secundarios desde la consola de Configuration Manager. Para obtener más información, vea [Iniciar la instalación de actualizaciones en un sitio secundario](#bkmk_secondary).  

- Hasta el momento en que todos los sitios de la jerarquía estén actualizados a la nueva versión, la jerarquía funciona en modo de versión mixta. Para obtener más información, vea [Interoperabilidad entre diferentes versiones](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### <a name="5-update-configuration-manager-consoles"></a>5. Actualizar consolas de Configuration Manager

Cuando se actualice un sitio de administración central o un sitio primario, también tendrán que actualizarse todas las consolas de Configuration Manager que se conecten a ese sitio. Se le pedirá que actualice una consola:  

- Cuando abre la consola.  

- Cuando se desplaza a un nuevo nodo en una consola abierta.  

Actualice la consola inmediatamente después de que se actualice el sitio.  

Cuando se actualice la consola, compruebe que la versión de la consola y del sitio sean correctas. Vaya a **Acerca de Configuration Manager** en la esquina superior izquierda de la consola.  

> [!Note]  
> La versión de la consola es ligeramente distinta de la versión del sitio. La versión secundaria de la consola corresponde a la versión de lanzamiento de Configuration Manager. Por ejemplo, en Configuration Manager versión 1802, la versión de sitio inicial es 5.0.8634.1000 y la versión inicial de la consola es 5. **1802**.1082.1700. Los números de compilación (1082) y revisión (1700) pueden cambiar con futuras revisiones.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a> Para iniciar la instalación de actualizaciones en el sitio de primer nivel  

En el sitio de primer nivel de la jerarquía, en la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**. Seleccione una actualización con el estado **Disponible** y, después, elija **Instalar el paquete de actualización** en la cinta de opciones.  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Para iniciar la instalación de la actualización en un sitio secundario  

Cuando se actualice el sitio primario principal de un sitio secundario, actualice el sitio secundario desde la consola de Configuration Manager. Para ello, utilice el **Asistente para actualizar sitios secundarios**.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio secundario que quiera actualizar y, después, elija **Actualizar** en la cinta de opciones.  

2. Haga clic en **Sí** para iniciar la actualización del sitio secundario.  

Para supervisar la instalación de actualizaciones en un sitio secundario, seleccione el sitio secundario y elija **Mostrar estado de instalación** en la cinta de opciones. También puede agregar la columna **Versión** al nodo Sitios para ver la versión de cada sitio secundario.  

En algunos casos, el estado de la consola no se actualiza ni sugiere que la actualización produce errores. Después de actualizar correctamente un sitio secundario, use la opción **Volver a intentar la instalación**. Esta opción no reinstala la actualización del sitio secundario que instaló correctamente la actualización, sino que obliga a la consola a actualizar el estado.

### <a name="post-installation-tasks"></a>Tareas posteriores a la instalación

Cuando un sitio instala una actualización, hay varias tareas que no se pueden iniciar hasta que la actualización finalice la instalación en el servidor de sitio. Esta lista contiene las tareas posteriores a la instalación que son críticas para las operaciones de sitio y jerarquía. Como son críticas, se supervisan activamente. Entre las tareas adicionales que no se supervisan directamente, se encuentra la reinstalación de los roles de sistema de sitio. Para ver el estado de las tareas críticas posteriores a la instalación, seleccione la tarea **Postinstalación** durante la supervisión de la instalación de actualizaciones para un sitio.

No todas las tareas se completan de inmediato. Algunas tareas no se inician hasta que cada sitio complete la instalación de la actualización. La nueva funcionalidad que cabría esperar puede retrasarse hasta que se completen estas tareas. La activación de nuevas características no se inicia hasta que todos los sitios completen la instalación de actualizaciones, por lo que es posible que las nuevas características no estén visibles durante algún tiempo.

Entre las tareas posteriores a la instalación figuran las siguientes:

- **Instalación del servicio SMS_EXECUTIVE**

  - Servicio crítico que se ejecuta en el servidor de sitio.
  - La reinstalación de este servicio se debe completar rápidamente.

- **Instalación del componente SMS_DATABASE_NOTIFICATION_MONITOR**

  - Subproceso de componente de sitio crítico del servicio SMS_EXECUTIVE.
  - La reinstalación de este servicio se debe completar rápidamente.

- **Instalación del componente SMS_HIERARCHY_MANAGER**

  - Componente de sitio crítico que se ejecuta en el servidor de sitio.
  - Responsable de la reinstalación de los roles de sistema de sitio en los servidores de sistema de sitio. No se muestra el estado de la reinstalación del rol de sistema de sitio individual.
  - La reinstalación de este servicio se debe completar rápidamente.

    > [!Note]
    > Algunos roles de sitio de Configuration Manager comparten el marco del cliente. Por ejemplo, el punto de administración y el punto de distribución de extracción. Cuando estos roles se actualizan, la versión del cliente en estos servidores se actualiza al mismo tiempo. Para obtener más información, vea [Actualizar clientes](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **Instalación del componente SMS_REPLICATION_CONFIGURATION_MONITOR**

  - Componente de sitio crítico que se ejecuta en el servidor de sitio.
  - La reinstalación de este servicio se debe completar rápidamente.

- **Instalación del componente SMS_POLICY_PROVIDER**

  - Componente de sitio crítico que se ejecuta solo en sitios primarios.
  - La reinstalación de este servicio se debe completar rápidamente.

- **Supervisando inicialización de replicación**

  - Esta tarea se muestra solo en el sitio de administración central y los sitios primarios secundarios.
  - Depende de SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Debe completarse rápidamente.

- **Actualizando el paquete de preproducción del cliente de Configuration Manager**

  - Esta tarea se muestra incluso cuando la preproducción del cliente (también llamada piloto de cliente) no está habilitada para su uso.
  - No se inicia hasta que todos los sitios de la jerarquía terminan de instalar la actualización.

- **Actualizando la carpeta Client en el servidor de sitio**

  - Esta tarea no se muestra si usa el cliente en preproducción.  
  - Debe completarse rápidamente.

- **Actualizando el paquete del cliente de Configuration Manager**

  - Esta tarea no se muestra si usa el cliente en preproducción.  
  - Finaliza solo después de que todos los sitios instalan la actualización.  

- **Activación de características**

  - Esta tarea se muestra únicamente en el sitio de nivel superior de la jerarquía.
  - No se inicia hasta que todos los sitios de la jerarquía terminan de instalar la actualización.
  - No se muestran las características individuales.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Reintento de la instalación de una actualización con errores  

Si no puede instalar una actualización, revise los comentarios en la consola para identificar las soluciones de errores y las advertencias. Para obtener más información, vea el archivo **ConfigMgrPrereq.log** en el servidor de sitio. Antes de reintentar la instalación de una actualización, debe solucionar los errores y las advertencias.  

> [!TIP]  
> Si una actualización tiene problemas de descarga o replicación, use la [herramienta de restablecimiento de actualizaciones](update-reset-tool.md).  

Cuando esté listo para reintentar la instalación de una actualización, seleccione la actualización con errores y elija una opción adecuada. El comportamiento del reintento de instalación de la actualización depende del nodo desde el que se inicia el reintento y de la opción de reintento que se usa.  

### <a name="retry-installation-for-the-hierarchy"></a>Volver a intentar la instalación en la jerarquía

Puede volver a intentar la instalación de una actualización en toda la jerarquía si la actualización se encuentra en alguno de los estados siguientes:  

- Las comprobaciones de requisitos previos se han superado con una o más advertencias y la opción de omitir las advertencias de comprobación de requisitos previos no se ha establecido en el Asistente para actualización. (El valor de actualización de **Ignorar advertencia sobre requisitos previos** en el nodo **Actualizaciones y mantenimiento** es **No**).

- Errores en la comprobación de requisitos previos

- Error de instalación  

- Error en la replicación del contenido en el sitio

Vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**. Seleccione la actualización y, después, elija una de estas opciones:  

- **Reintentar**: al **Reintentar** desde **Actualizaciones y mantenimiento**, la instalación de la actualización vuelve a empezar y omite automáticamente las advertencias de requisitos previos. Si la réplica de contenido ha producido errores anteriormente, el contenido de la actualización se volverá a replicar.  

- **Omitir advertencias de requisitos previos**: si se detiene la instalación de la actualización debido a una advertencia, puede seleccionar **Omitir advertencias de requisitos previos**. Esta acción permite que la instalación de la actualización continúe en unos minutos y usa la opción para omitir las advertencias de requisitos previos.

### <a name="retry-installation-for-the-site"></a>Volver a intentar la instalación en el sitio

Puede reintentar la instalación de una actualización en un sitio específico si la actualización se encuentra en alguno de los estados siguientes:  

- Las comprobaciones de requisitos previos se han superado con una o más advertencias y la opción de omitir las advertencias de comprobación de requisitos previos no se ha establecido en el Asistente para actualización. (El valor de actualizaciones de **Ignorar advertencia sobre requisitos previos** en el nodo Actualizaciones y mantenimiento es **No**).  

- Errores en la comprobación de requisitos previos

- Error de instalación

Vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado de mantenimiento del sitio**. Seleccione la actualización y, después, elija una de estas opciones:  

- **Reintentar**: al **Reintentar** desde **Estado de mantenimiento del sitio**, se reinicia la instalación de la actualización solo en ese sitio. A diferencia de ejecutar **Reintentar** en el nodo **Actualizaciones y mantenimiento**, este reintento no omite las advertencias de requisitos previos.  

- **Omitir advertencias de requisitos previos**: si se detiene la instalación de la actualización debido a una advertencia, puede seleccionar **Omitir advertencias de requisitos previos**. Esta acción permite que la instalación de la actualización continúe en unos minutos y usa la opción para omitir las advertencias de requisitos previos.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Después de que un sitio instala una actualización  

Una vez que se actualice el sitio, revise la lista de comprobación posterior a la actualización para la versión correspondiente:  

- [Lista de comprobación posterior a la actualización para la versión 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Lista de comprobación posterior a la actualización para la versión 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Lista de comprobación posterior a la actualización para la versión 1906](checklist-for-installing-update-1906.md#post-update-checklist)  

- [Lista de comprobación posterior a la actualización para la versión 1902](checklist-for-installing-update-1902.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Habilitar características opcionales de las actualizaciones  

Cuando una actualización incluye una o varias características opcionales, tiene la oportunidad de habilitar esas características en la jerarquía. Puede habilitar características cuando se instale la actualización, o bien puede volver a la consola posteriormente y habilitar las características opcionales.

Para ver las características disponibles y su estado, en la consola, vaya al área de trabajo **Administración**, expanda **Actualizaciones y mantenimiento** y, después, seleccione el nodo **Características**.

Cuando una característica no es opcional, se instala automáticamente. No aparece en el nodo **Características**.  

> [!Important]  
> En una jerarquía multisitio, solo se pueden habilitar características opcionales o de versión preliminar desde el sitio de administración central. Con este comportamiento se procura que no haya ningún conflicto en la jerarquía. <!--507197-->  

Al habilitar una característica nueva o de versión preliminar, el Administrador de jerarquía de Configuration Manager (HMAN) debe procesar el cambio antes de que dicha característica esté disponible. El procesamiento del cambio suele ser inmediato. Según el ciclo de procesamiento de HMAN, puede tardar hasta 30 minutos en completarse. Una vez procesado el cambio, reinicie la consola antes de usar la característica.

A partir de la versión 2002,<!--5834830--> cuando haya nuevas características basadas en la nube disponibles en el centro de administración de Microsoft Endpoint Manager u otros servicios en la nube asociados para la instalación local de Configuration Manager, puede seleccionar estas nuevas características en la consola de Configuration Manager.

### <a name="list-of-optional-features"></a>Lista de características opcionales

Las siguientes características son opcionales en la versión más reciente de Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Administración de BitLocker](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Sincronización de los resultados de pertenencia a recopilaciones con Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Detección de grupos de usuarios de Azure Active Directory](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Grupos de aplicaciones](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Depurador de secuencia de tareas](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Administrador de conversión de paquetes](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [Aplicaciones cliente para dispositivos administrados conjuntamente](../../../comanage/workloads.md#client-apps) (antes denominadas *aplicaciones móviles para dispositivos administrados conjuntamente*) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C-->
- [Actualizaciones de software de terceros](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Aprobación de solicitudes de aplicación para los usuarios por dispositivo](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Creación y ejecución de scripts](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Actualizaciones de controladores de Surface](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Puerta de enlace de administración en la nube](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [Creación de PFX](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Conector de Log Analytics de Azure](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Directiva de Protección contra vulnerabilidades de seguridad de Windows Defender](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN para Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Mantenimiento de una recopilación compatible con clústeres (grupos de servidores)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows Hello para empresas](../../../protect/deploy-use/windows-hello-for-business-settings.md) (conocido anteriormente como *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!Tip]  
> Para obtener más información sobre las características cuya habilitación requiere consentimiento, consulte las [características de versión preliminar](pre-release-features.md).  
>
> Para más información sobre las características que solo están disponibles en la rama de Technical Preview, vea [Technical Preview](../../get-started/technical-preview.md).

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Uso de las características de versión preliminar de las actualizaciones

Las características de versión preliminar se incluyen en la Rama actual para realizar pruebas anticipadamente en un entorno de producción. Para obtener más información, vea [Características de versión preliminar](pre-release-features.md).

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Preguntas más frecuentes

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>¿Por qué no se ven determinadas actualizaciones en la consola?

Si no encuentra una actualización específica en la consola después de una sincronización correcta con el servicio en la nube de Microsoft, este comportamiento podría deberse a uno de los motivos siguientes:  

- La actualización necesita una configuración que no usa la infraestructura, o bien la versión del producto actual no cumple un requisito previo para recibir la actualización.  

    Si cree que tiene las configuraciones necesarias y otros requisitos previos para una actualización que falta, confirme que su punto de conexión de servicio se encuentre en el modo en línea. Después, use la opción **Buscar actualizaciones** en el nodo **Actualizaciones y mantenimiento** para forzar una comprobación. Cuando el punto de conexión de servicio está en el modo sin conexión, se usa la herramienta de conexión de servicio para ejecutar manualmente la sincronización con el servicio en la nube.  

- La cuenta no dispone de los permisos de administración basada en roles correctos para ver las actualizaciones en la consola de Configuration Manager. Para obtener más información, vea [Permisos para administrar actualizaciones](#assign-permissions-to-view-and-manage-updates-and-features).  
