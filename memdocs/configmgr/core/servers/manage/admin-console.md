---
title: Consola de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre la navegación a través de la consola de Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ac5b3ca8e8e2231bb421838fa56b20253ddfcb74
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878371"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Cómo usar la consola de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los administradores usan la consola de Configuration Manager para administrar el entorno de Configuration Manager. Este artículo trata los aspectos básicos de navegación de la consola.  

## <a name="open-the-console"></a><a name="bkmk_open"></a> Abrir la consola

La consola del Configuration Manager siempre se instala en cada servidor de sitio. También se puede instalar en otros equipos. Para obtener más información, consulte [Instalar la consola de Configuration Manager](../deploy/install/install-consoles.md).

El método más sencillo de abrir la consola en un equipo Windows 10 consiste en presionar **Inicio** y empezar a escribir `Configuration Manager console`. Posiblemente no tenga que escribir la cadena completa para que Windows encuentre la mejor coincidencia.

Si examina el menú Inicio, busque el icono de la **consola de Configuration Manager** en el grupo **Microsoft Endpoint Manager**.

![Iconos del menú Inicio de Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> La ruta de acceso del menú Inicio ha cambiado en la versión 1910. En la versión 1906 y anteriores, el nombre de la carpeta es **System Center**. Cuando actualice Configuration Manager a la versión 1910 o posterior, asegúrese de actualizar cualquier documentación interna que conserve para que refleje esta nueva ubicación.

## <a name="connect-to-a-site-server"></a>Conexión a un servidor de sitio

La consola se conecta al servidor de sitio de administración central o a los servidores de sitio primarios. No se puede conectar una consola de Configuration Manager a un sitio secundario. Durante la instalación, especificó el nombre de dominio completo (FQDN) del servidor de sitio al que se conecta la consola.

Para conectarse a otro servidor de sitio, siga estos pasos:

1. Haga clic en la flecha situada en la parte superior de la [cinta](#ribbon) y elija **Conectar a un nuevo sitio**.  

    ![Conexión de la consola a un sitio nuevo](media/connect-to-a-new-site.png)  

2. Escriba el FQDN del servidor del sitio. Si se ha conectado anteriormente al servidor de sitio, seleccione el servidor en la lista desplegable.  

    ![Ventana de conexión de sitio, especifique el FQDN del servidor de sitio](media/site-server-fqdn.png)  

3. Seleccione **Conectar**.  

A partir de la versión 1810, puede especificar el nivel mínimo de autenticación para que los administradores accedan a sitios de Configuration Manager. Esta característica exige que los administradores inicien sesión en Windows con el nivel requerido. Para más información, vea [Plan for the SMS Provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth) (Planear el proveedor de SMS). <!--1357013-->  

## <a name="navigation"></a>Navegación

Algunas áreas de la consola pueden no estar visibles en función del rol de seguridad asignado. Para obtener más información sobre roles, vea [Conceptos básicos de la administración basada en roles](../../understand/fundamentals-of-role-based-administration.md).

### <a name="workspaces"></a>Áreas de trabajo

La consola de Configuration Manager tiene cuatro **áreas de trabajo**:  

- **Activos y compatibilidad**  

- **Biblioteca de software**  

- **Supervisión**  

- **Administración**  

![Áreas de trabajo de Configuration Manager con el menú contextual](media/configuration-manager-workspaces.png)  

Cambie el orden de los botones del área de trabajo; para ello, haga clic en la flecha hacia abajo y elija **Opciones de Panel de navegación**. Seleccione un elemento que quiera **Subir** o **Bajar**. Haga clic en **Restablecer** para restaurar el orden de botones predeterminado.  

![Ventana de Opciones del Panel de navegación para cambiar el orden de las áreas de trabajo](media/navigation-pane-options.png)  

Minimice un botón del área de trabajo seleccionando **Mostrar menos botones**. La última área de trabajo de la lista se minimiza primero. Seleccione un botón minimizado y elija **Mostrar más botones** para restaurar el botón a su tamaño original.

![Áreas de trabajo minimizadas en la consola de Configuration Manager](media/workspace-buttons.png)  

### <a name="nodes"></a>Nodos

Las áreas de trabajo son una colección de **nodos**. Un ejemplo de un nodo es el nodo **Grupos de actualizaciones de software** en el área de trabajo **Biblioteca de software**.

Una vez que se encuentran en el nodo, puede hacer clic en la flecha para minimizar el panel de navegación.  

![Nodo de ejemplo y flecha de minimizar resaltado](media/software-update-groups-node.png)  

Use la **barra de navegación** para desplazarse por la consola al minimizar el panel de navegación.  

![Configuration Manager minimizado en el panel de navegación](media/minimized-navigation-pane.png)  

En la consola, los nodos a veces se organizan en carpetas. Al seleccionar la carpeta, normalmente se muestra un **índice de navegación** o un **panel**.  

![Índice de navegación de las actualizaciones de software de Configuration Manager](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Cinta de opciones

La cinta está en la parte superior de la consola de Configuration Manager. La cinta puede tener más de una pestaña y se puede minimizar usando la flecha situada a la derecha. Los botones de la cinta de opciones cambian en función del nodo. La mayoría de los botones de la cinta también están disponibles en los menús que verá en los menús contextuales.  

![Cinta de opciones de ejemplo, flecha para resaltar varias pestañas y minimizar](media/ribbon.png)

### <a name="details-pane"></a>Panel de detalles

Puede obtener información adicional sobre los elementos revisando el panel de detalles. El panel de detalles puede tener una o más pestañas. Las pestañas varían según el nodo.  

![Panel de detalles de ejemplo de Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Columnas

Puede agregar columnas, quitarlas, reordenarlas y cambiar su tamaño. Estas acciones le permiten mostrar los datos que prefiera. Las columnas disponibles varían en función del nodo. Para agregar o quitar una columna de la vista, haga clic con el botón derecho en un encabezado de columna existente y seleccione un elemento. Reordene las columnas arrastrando el encabezado de columna donde desee que esté ubicado.  

![Columna para agregar en Configuration Manager](media/add-columns.png)  

En la parte inferior del menú contextual de la columna puede ordenar o agrupar por una columna. Además, también puede ordenar por columna seleccionando el encabezado.  

![Agrupar por columna en Configuration Manager](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a> Reclamación de bloqueo para editar objetos

<!--4786915-->

Si la consola de Configuration Manager deja de responder, podría quedarse bloqueado y no poder realizar más cambios hasta que expire el bloqueo al cabo de 30 minutos. Este bloqueo forma parte del sistema SEDO (edición serializada de objetos distribuidos) de Configuration Manager. Para obtener más información, vea [Configuration Manager SEDO](../../../develop/core/understand/sedo.md) (SEDO de Configuration Manager).

A partir de la [versión 1906 de la rama actual](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences), puede borrar el bloqueo en una secuencia de tareas. A partir de la versión 1910, se puede borrar el bloqueo de cualquier objeto de la consola de Configuration Manager.

Esta acción solo se aplica a la cuenta de usuario que tiene el bloqueo, en el mismo dispositivo desde el que el sitio concedió el bloqueo. Cuando intente obtener acceso a un objeto bloqueado, ahora podrá **Descartar los cambios** y seguir editando el objeto. Estos cambios se perderían de todos modos al expirar el bloqueo.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a> Consulta de las consolas conectadas recientemente

<!--3699367-->
A partir de la versión 1902, puede ver las conexiones más recientes de la consola de Configuration Manager. La vista incluye las conexiones activas y aquellas que se conectaron recientemente. Siempre verá la conexión actual de la consola en la lista. Solo se muestran las conexiones desde la consola de Configuration Manager, no las conexiones de PowerShell ni otras conexiones basadas en el SDK al proveedor de SMS. El sitio quita las instancias de la lista que tienen más de 30 días.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a> Requisitos previos para ver las consolas conectadas

- La cuenta debe tener el permiso **Lectura** en el objeto **SMS_Site**.

- Configure la API REST del servicio de administración. Consulte [¿Qué es el servicio de administración?](../../../develop/adminservice/overview.md) para obtener más información.

### <a name="view-connected-consoles"></a>Consulta de las consolas conectadas

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**.  

2. Expanda **Seguridad** y seleccione el nodo **Conexiones de la consola**.  

3. Vea las conexiones recientes con estas propiedades:  

    - Nombre de usuario
    - Nombre de máquina
    - Código de sitio conectado
    - Versión de la consola
    - Hora de la última conexión: momento en el que el usuario *abrió* la consola por última vez
    - A partir de la versión 1910, la columna **Último latido de la consola** ha reemplazado a la columna **Hora de la última conexión**. <!--4923997-->
       - Una consola abierta en primer plano envía un latido cada 10 minutos.

![Consulta de las conexiones de la consola de Configuration Manager](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a> Iniciar chat de Microsoft Teams desde las conexiones de la consola
<!--4923997-->
*(Se incluyó en la versión 1910)*

A partir de la versión 1910, se pueden enviar mensajes otros administradores de Configuration Manager desde el nodo **Conexiones de la consola** usando Microsoft Teams. Cuando se elige **iniciar un chat de Microsoft Teams** con un administrador, Microsoft Teams se inicia y se abre un chat con el usuario en cuestión.

### <a name="prerequisites"></a>Requisitos previos

- Para iniciar una conversación con un administrador, la cuenta con la que desea conversar debe haberse detectado con la [detección de usuarios de AD o Azure AD](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Microsoft Teams debe estar instalado en el dispositivo desde el que se ejecuta la consola.
nota
- Todos los [requisitos previos para ver las consolas conectadas](#bkmk_connections-prereq).

### <a name="start-microsoft-teams-chat"></a>Inicio del chat de Microsoft Teams

1. Vaya a **Administración** > **Seguridad** > **Conexiones de la consola**.
1. Haga clic con el botón derecho en la conexión de la consola de un usuario y seleccione **Iniciar el chat de Microsoft Teams**.
    - Si no se encuentra el nombre principal de usuario para el administrador seleccionado, la opción **Iniciar el chat de Microsoft Teams** aparecerá atenuada.
    - Si Microsoft Teams no está instalado en el dispositivo desde el que se ejecuta la consola, aparece un mensaje de error, junto con un vínculo de descarga.
    - Si Microsoft Teams está instalado en el dispositivo desde el que se ejecuta la consola, se abrirá un chat con el usuario.

### <a name="known-issues"></a>Problemas conocidos

El mensaje de error que le notifica que Microsoft Teams no está instalado no se mostrará si no existe la siguiente clave del Registro:

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Para solucionar el problema, cree manualmente la clave del Registro.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a> Notificaciones de la consola de Configuration Manager

<!--3556016, fka 1318035-->
A partir de la versión 1902 de Configuration Manager, la consola lo notifica en caso de los siguientes eventos:

- Cuando hay una actualización disponible para el propio Configuration Manager
- Cuando se producen eventos de ciclo de vida y mantenimiento en el entorno

Esta notificación es una barra en la parte superior de la ventana de la consola, debajo de la cinta. Reemplaza a la experiencia anterior cuando había disponibles actualizaciones de Configuration Manager. Estas notificaciones en consola aún muestran información crítica, pero no interfieren con el trabajo en la consola. No se pueden descartar las notificaciones críticas. La consola muestra todas las notificaciones en una nueva área de notificación de la barra de título.

![Barra de notificación y marca en consola](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Configuración de un sitio para que muestre notificaciones no críticas

Puede configurar cada sitio para que muestre las notificaciones no críticas en las propiedades del sitio.

1. En el área de trabajo **Administración**, expanda **Configuración del sitio** y, a continuación, seleccione el nodo **Sitios**.
1. Seleccione el sitio que quiere configurar para las notificaciones no críticas.
1. En la cinta, seleccione **Propiedades**.
1. En la pestaña **Alertas**, seleccione la opción de **habilitar las notificaciones de la consola para cambios de estado de sitio no críticos**.
   - Si habilita esta opción, todos los usuarios de la consola ven notificaciones críticas, de advertencia e informativas. Esta opción está habilitada de forma predeterminada.  
   - Si deshabilita esta opción, los usuarios de la consola solo ven las notificaciones críticas.  

La mayoría de las notificaciones de consola son por sesión. La consola evalúa las consultas cuando un usuario la inicia. Para ver los cambios en las notificaciones, reinicie la consola. Si un usuario descarta una notificación no crítica, vuelve a notificar cuando se reinicia la consola, si sigue siendo aplicable.

Las siguientes notificaciones se vuelven a evaluar cada cinco minutos:

- El sitio está en modo de mantenimiento  
- El sitio está en modo de recuperación  
- El sitio está en modo de actualización  

Las notificaciones siguen los permisos de la administración basada en roles. Por ejemplo, si un usuario no tiene permisos para ver las actualizaciones de Configuration Manager, no ve esas notificaciones.

Algunas notificaciones tienen una acción relacionada. Por ejemplo, si la versión de la consola no coincide con la versión del sitio, seleccione **Instalar la nueva versión de la consola**. Esta acción inicia el instalador de la consola.

Las siguientes notificaciones son más aplicables a la rama de Technical Preview:  

- La versión de evaluación expira en 30 días (advertencia): faltan 30 días desde la fecha actual para la fecha de expiración de la versión de evaluación  
- La versión de evaluación ha expirado (crítico): la fecha actual es posterior a la fecha de expiración de la versión de evaluación  
- Discrepancia de versiones de consola (crítico): la versión de la consola no coincide con la versión del sitio  
- Actualización de sitio disponible (advertencia): hay un nuevo paquete de actualización disponible  

Para obtener más información y ayuda para la solución de problemas, vea el archivo **SmsAdminUI.log** en el equipo de la consola. De forma predeterminada, este archivo de registro está en la ruta de acceso siguiente: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a> Panel de documentación en consola

<!--3556019 FKA 1357546-->
A partir de la versión 1902 de Configuration Manager, hay un nodo de **Documentación** en la nueva área de trabajo **Comunidad**. Este nodo incluye información actualizada acerca de los artículos de soporte técnico y la documentación de Configuration Manager. Se incluyen las secciones siguientes:  

### <a name="product-documentation-library"></a>Biblioteca de documentación del producto

- **Recomendado**: lista mantenida manualmente de artículos importantes.
- **Tendencias**: los artículos más populares del último mes.
- **Actualizado recientemente**: artículos revisados en el último mes.

### <a name="support-articles"></a>Artículos de soporte técnico

- **Artículos de solución de problemas**: tutoriales guiados que le ayudarán a solucionar problemas de características y componentes de Configuration Manager.
- **Artículos de soporte técnico nuevos y actualizados**: artículos que son nuevos o se han actualizado en los últimos dos meses.

### <a name="troubleshooting-connection-errors"></a>Solución de errores de conexión
El nodo **Documentación** no tiene ninguna configuración de proxy explícita. Usa cualquier proxy definido por el sistema operativo en el applet del panel de control **Opciones de Internet**. Para volver a intentarlo después de un error de conexión, actualice el nodo **Documentación**.


## <a name="command-line-options"></a>Opciones de línea de comandos

La consola de Configuration Manager tiene las opciones de línea de comandos siguientes:

|Opción|Descripción|  
|------------|-----------------|  
|`/sms:debugview=1`|Se incluye un elemento DebugView en todos los elementos ResultView que especifican una vista. DebugView muestra las propiedades sin procesar (nombres y valores).|  
|`/sms:NamespaceView=1`|Muestra la vista del espacio de nombres en la consola.|  
|`/sms:ResetSettings`|La consola pasa por alto los estados de vista y conexión seguidas por el usuario. No se restablece el tamaño de la ventana.|  
|`/sms:IgnoreExtensions`|Deshabilita las extensiones de Configuration Manager.|  
|`/sms:NoRestore`|La consola omite la anterior navegación por nodos persistente.|  


## <a name="tips"></a>Sugerencias

### <a name="general"></a>General

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Mejoras en la búsqueda de la consola
<!--4640570-->
*(Se incluyó en la versión 1910)*

- Puede usar la opción de búsqueda **Todas las subcarpetas** de los nodos **Paquetes de controladores** y **Consultas**.<!--2841181,5424892--> A partir de la versión 2002, use también esta opción los nodos **Elementos de configuración** y **Líneas de base de configuración**.<!--5891241-->

- Cuando una búsqueda devuelve más de 1000 resultados, seleccione el botón **Aceptar** en la barra de avisos para ver más resultados.<!--4640570-->

    ![Captura de pantalla de la barra de avisos para demasiados resultados de la búsqueda](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > El límite predeterminado de los resultados de la búsqueda es 1000. Este valor predeterminado se puede cambiar. En la consola de Configuration Manager, vaya a la pestaña de la cinta **Buscar**. En el grupo **Opciones**, seleccione **Configuración de búsqueda**. Cambie el valor de **Resultados de la búsqueda**. Si selecciona un número mayor de resultados de búsqueda, puede tardar más tiempo en mostrarse.
    >
    > De forma predeterminada, el límite superior máximo es 100 000. Para cambiar este límite, establezca el valor DWORD **QueryResultCountMaximum** en la clave del registro siguiente:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > La configuración en la consola corresponde al valor **QueryResultCountLimit** en la misma clave. Un administrador puede configurar estos valores en el subárbol HKLM para todos los usuarios del dispositivo. El valor HKCU invalida la configuración HKLM.

#### <a name="role-based-administration-for-folders"></a>Administración de las carpetas basada en roles
<!--3600867-->
*(Se introdujo en la versión 1906)*

Puede establecer los ámbitos de seguridad en las carpetas. Si tiene acceso a un objeto de la carpeta pero no a la carpeta, no podrá ver el objeto. De forma similar, si tiene acceso a una carpeta pero no a un objeto incluido en su interior, no verá ese objeto. Haga clic con el botón derecho en una carpeta, elija **Establecer ámbitos de seguridad** y, luego, elija los ámbitos de seguridad que quiere aplicar.

#### <a name="views-sort-by-integer-values"></a>Ordenar las vistas por valores enteros

*(Se introdujo en la versión 1902)*

Realizamos mejoras en la forma en que varias vistas orden los datos. Por ejemplo, en el nodo **Implementaciones** del área de trabajo **Supervisión**, ahora las columnas siguientes se ordenan como números en lugar de como valores de cadena:  

- Enumerar errores
- Enumerar en progreso
- Enumerar otros
- Enumerar correctos
- Enumerar desconocidos  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>Mover la advertencia de un número de resultados elevado

*(Se introdujo en la versión 1902)*

Cuando en la consola hace clic en un nodo que devuelve más de 1.000 resultados, Configuration Manager muestra la advertencia siguiente:

> Configuration Manager devolvió un gran número de resultados. Puede restringir los resultados mediante las características de búsqueda. O hacer clic aquí para ver un número máximo de 100 000.

Ahora hay un espacio en blanco adicional entre esta advertencia y el campo de búsqueda. Este cambio ayuda a evitar que se seleccione accidentalmente la advertencia para mostrar más resultados.

#### <a name="send-feedback"></a>Enviar comentarios

*(Se introdujo en la versión 1806)*
<!--1357542-->

Envíe los comentarios sobre el producto desde la consola.  

- **Enviar una sonrisa**: envíe comentarios sobre lo que le ha gustado.  

- **Enviar un ceño fruncido**: envíe comentarios sobre lo que no le ha gustado.  

- **Enviar una sugerencia**: le lleva a UserVoice para compartir sus ideas.  

Para obtener más información, vea [Comentarios sobre el producto](../../understand/find-help.md#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Área de trabajo Activos y compatibilidad

#### <a name="real-time-actions-from-device-lists"></a>Acciones en tiempo real desde las listas de dispositivos
<!--4616810-->
*(Se introdujo en la versión 1906)*

Hay varias maneras de mostrar una lista de dispositivos en el nodo **Dispositivos** del área de trabajo **Activos y compatibilidad**.

- En el área de trabajo **Activos y compatibilidad**, seleccione el nodo **Recopilaciones de dispositivos**. Seleccione una recopilación de dispositivos y elija la acción **Mostrar miembros**. Esta acción abre un subnodo del nodo **Dispositivos** con una lista de dispositivos para esa colección.  

  - Al seleccionar el subnodo de la recopilación, ahora se puede iniciar **CMPivot** desde el grupo Recopilación de la cinta.  

- En el área de trabajo **Supervisión**, seleccione el nodo **Implementaciones**. Seleccione una implementación y elija la acción **Ver estado** en la cinta. En el panel de estado de la implementación, haga doble clic en el total de recursos para obtener los detalles de una lista de dispositivos.  

  - Al seleccionar un dispositivo en esta lista, ahora se puede iniciar **CMPivot** y **Ejecutar scripts** desde el grupo Dispositivo de la cinta.  


#### <a name="collections-tab-in-devices-node"></a>Pestaña Colecciones en el nodo Dispositivos
<!--4616810-->
*(Se introdujo en la versión 1906)*

En el área de trabajo **Activos y compatibilidad**, vaya al nodo **Dispositivos** y seleccione un dispositivo. En el panel de detalles, cambie a la nueva pestaña **Colecciones**. En esta pestaña se enumeran las colecciones que incluyen este dispositivo. 

> [!Note]  
> - Esta pestaña no está actualmente disponible en un subnodo de dispositivos bajo el nodo **Recopilaciones de dispositivos**. Por ejemplo, cuando selecciona la opción **Mostrar miembros** en una colección.
> - Es posible que esta pestaña no se rellene como se esperaba para algunos usuarios. Para ver la lista completa de colecciones a las que pertenece un dispositivo, debe tener el rol de seguridad **Administrador total**. Este es un problema conocido. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Incorporación de una columna GUID de SMBIOS a los nodos de recopilación de dispositivos y dispositivos

*(Se introdujo en la versión 1906)*

<!--4526580-->
En los nodos **Dispositivos** y **Recopilaciones de dispositivos**, ahora puede agregar una nueva columna para **GUID de SMBIOS**. Este valor es el mismo que la propiedad **GUID de BIOS** de la clase de recurso del sistema. Es un identificador único para el hardware del dispositivo.

#### <a name="search-device-views-using-mac-address"></a>Vistas de búsqueda de dispositivos mediante dirección MAC

<!--3600878-->
*(Se introdujo en la versión 1902)*

Puede buscar una dirección MAC en la vista de un dispositivo de la consola de Configuration Manager. Esta propiedad es útil para los administradores de implementaciones de sistema operativo durante la solución de problemas de implementaciones de PXE. Cuando vea una lista de dispositivos, agregue la columna **Dirección MAC** a la vista. Use el campo de búsqueda para agregar los criterios de búsqueda de **Dirección MAC**.

#### <a name="view-users-for-a-device"></a>Ver los usuarios de un dispositivo

A partir de la versión 1806, las siguientes columnas están disponibles en el nodo **Dispositivos**:  

- **Usuarios primarios** <!--1357280-->  

- **Usuario que ha iniciado sesión actualmente** <!--1358202-->  

    > [!NOTE]  
    > Para poder ver el usuario que ha iniciado sesión actualmente, necesitará la [detección de usuarios](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) y la [afinidad entre usuario y dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Para obtener más información sobre cómo mostrar una columna no predeterminada, vea [Columnas](#columns).

#### <a name="improvement-to-device-search-performance"></a>Mejora de rendimiento de la búsqueda de dispositivos

<!-- 3614690 -->
A partir de la versión 1806, al realizar búsquedas en una recopilación de dispositivos, no se busca la palabra clave en todas las propiedades del objeto. Cuando no especifique lo que hay que buscar, busca a través de las cuatro propiedades siguientes:

- Nombre
- Usuarios primarios
- Usuario que ha iniciado sesión actualmente
- Nombre de usuario de último inicio de sesión

Este comportamiento mejora significativamente el tiempo necesario para buscar por nombre, especialmente en un entorno grande. Las búsquedas personalizadas según criterios específicos no se ven afectadas.


### <a name="software-library-workspace"></a>Área de trabajo de la Biblioteca de software

#### <a name="order-by-program-name-in-task-sequence"></a>Ordenar por nombre de programa en la secuencia de tareas
<!--4616810-->
*(Se introdujo en la versión 1906)*

En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en el nodo **Secuencias de tareas**. Edite una secuencia de tareas y seleccione o agregue el paso [Instalar paquete](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage). Si un paquete tiene más de un programa, ahora en la lista desplegable los programas se ordenan alfabéticamente.

#### <a name="task-sequences-tab-in-applications-node"></a>Pestaña Secuencias de tareas en el nodo Aplicaciones
<!--4616810-->
*(Se introdujo en la versión 1906)*

Vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones**, vaya al nodo **Aplicaciones** y seleccione una aplicación. En el panel de detalles, cambie a la nueva pestaña **Secuencias de tareas**. En esta pestaña se enumeran las secuencias de tareas que hacen referencia a esta aplicación.

#### <a name="drill-through-required-updates"></a>Obtención de detalles de actualizaciones necesarias
<!--4224414-->
*(Se introdujo en la versión 1906)*

1. Vaya a una de las ubicaciones siguientes en la consola de Configuration Manager:

   - **Biblioteca de software** > **Actualizaciones de software** > **Todas las actualizaciones de software**
   - **Biblioteca de software** > **Mantenimiento de Windows 10** > **Todas las actualizaciones de Windows 10**
   - **Biblioteca de software** > **Administración de clientes de Office 365** > **Actualizaciones de Office 365**

1. Seleccione las actualizaciones que requiera al menos un dispositivo.
1. En la pestaña **Resumen** encontrará un gráfico circular bajo **Estadísticas**.
1. Seleccione el hipervínculo **Vista necesaria** situado junto al gráfico circular para obtener los detalles de la lista de dispositivos.
1. Esta acción le llevará a un nodo temporal en **Dispositivos** donde podrá ver los dispositivos que requieren la actualización. También puede realizar acciones para el nodo, como crear una colección a partir de la lista.

> [!NOTE]
> A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Es posible que siga viendo referencias al nombre anterior en la consola de Configuration Manager y la documentación complementaria mientras se está actualizando la consola.

#### <a name="maximize-the-browse-registry-window"></a>Maximizar la ventana Examinar registro

<!--3594151 includes all MMS 1902 console changes-->
*(Se introdujo en la versión 1902)*

1. En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y haga clic en el nodo **Aplicaciones**.
1. Seleccione una aplicación que tenga un tipo de implementación con un método de detección. Por ejemplo, un método de detección de Windows Installer.
1. En el panel de detalles, cambie a la pestaña **Tipos de implementación**.
1. Abra las propiedades de un tipo de implementación y cambie a la pestaña **Método de detección**. Haga clic en **Agregar cláusula**.
1. Cambiar **Tipo de configuración** a **Registro** y haga clic en **Examinar** para abrir la ventana **Examinar registro**. Ahora puede maximizar esta ventana.  

#### <a name="edit-a-task-sequence-by-default"></a>Editar una secuencia de tareas de forma predeterminada

*(Se introdujo en la versión 1902)*

En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en el nodo **Secuencias de tareas**. **Editar** es ahora la acción predeterminada cuando se abre una secuencia de tareas. Anteriormente, la acción predeterminada era **Propiedades**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Ir a la colección desde una implementación de aplicación

*(Se introdujo en la versión 1902)*

1. En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y haga clic en el nodo **Aplicaciones**.
1. Seleccione una aplicación. En el panel de detalles, cambie a la pestaña **Implementaciones**.
1. Seleccione una implementación y, después, haga clic en la nueva opción **Colección** en la cinta de la pestaña Implementación. Esta acción cambia la vista a la colección que es el destino de la implementación.
   - Esta acción también está disponible en el menú contextual de la implementación de esta vista.


### <a name="monitoring-workspace"></a>Área de trabajo de supervisión

#### <a name="correct-names-for-client-operations"></a>Nombres correctos para las operaciones de cliente
<!--4616810-->
*(Se introdujo en la versión 1906)*

En el área de trabajo **Supervisión**, seleccione **Operaciones de cliente**. La operación para **Cambiar al siguiente punto de actualización de software** ahora tiene el nombre correcto.

#### <a name="show-collection-name-for-scripts"></a>Mostrar el nombre de la recopilación para los scripts
<!--4616810-->
*(Se introdujo en la versión 1906)*

En el área de trabajo **Supervisión**, seleccione el nodo **Estado del script**. Ahora se muestra el **Nombre de la recopilación** además el identificador.

#### <a name="remove-content-from-monitoring-status"></a>Quitar contenido del estado de supervisión

*(Se introdujo en la versión 1902)*

1. En el área de trabajo **Supervisión**, expanda **Estado de distribución** y haga clic en **Estado de contenido**.
1. Seleccione un elemento en la lista y haga clic en la nueva opción **Ver estado** de la cinta.
1. En el panel Detalles del activo, haga clic con el botón derecho en un punto de distribución y seleccione la nueva opción **Quitar**. Esta acción quita este contenido del punto de distribución seleccionado.

#### <a name="copy-details-in-monitoring-views"></a>Copiar detalles en las vistas de supervisión

*(Se introdujo en la versión 1806)*
<!--1357856-->
Se puede copiar información desde el panel **Detalles del activo** para los siguientes nodos de supervisión:  

- **Estado de distribución de contenido**  

- **Estado de implementación**  

![Vista del estado de implementación, detalles del activo de copia](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Área de trabajo Administración

<!--4223683-->
A partir de la versión 1906, puede habilitar algunos nodos en el nodo **Seguridad** para usar el servicio de administración. Este cambio permite que la consola se comunique con el proveedor de SMS a través de HTTPS en lugar de WMI. Para obtener más información, consulte cómo [configurar el servicio de administración](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Pasos siguientes

[Características de accesibilidad](../../understand/accessibility-features.md)

[Editor de secuencias de tareas](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
