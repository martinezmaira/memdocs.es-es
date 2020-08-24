---
title: Cambios y sugerencias de la consola de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre los cambios en la consola de Configuration Manager y las sugerencias para usarla.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0a434f013da48d660efa78f5e2cdca6ced0826d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700725"
---
# <a name="configuration-manager-console-changes-and-tips"></a>Cambios y sugerencias de la consola de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la información siguiente para obtener información sobre los cambios en la consola de Configuration Manager y las sugerencias para usarla:

## <a name="general-tips"></a>Sugerencias generales

### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Mejoras en la búsqueda de la consola
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

### <a name="role-based-administration-for-folders"></a>Administración de las carpetas basada en roles
<!--3600867-->
*(Se introdujo en la versión 1906)*

Puede establecer los ámbitos de seguridad en las carpetas. Si tiene acceso a un objeto de la carpeta pero no a la carpeta, no podrá ver el objeto. De forma similar, si tiene acceso a una carpeta pero no a un objeto incluido en su interior, no verá ese objeto. Haga clic con el botón derecho en una carpeta, elija **Establecer ámbitos de seguridad** y, luego, elija los ámbitos de seguridad que quiere aplicar.

### <a name="views-sort-by-integer-values"></a>Ordenar las vistas por valores enteros

*(Se introdujo en la versión 1902)*

Realizamos mejoras en la forma en que varias vistas orden los datos. Por ejemplo, en el nodo **Implementaciones** del área de trabajo **Supervisión**, ahora las columnas siguientes se ordenan como números en lugar de como valores de cadena:  

- Enumerar errores
- Enumerar en progreso
- Enumerar otros
- Enumerar correctos
- Enumerar desconocidos  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Mover la advertencia de un número de resultados elevado

*(Se introdujo en la versión 1902)*

Cuando en la consola hace clic en un nodo que devuelve más de 1.000 resultados, Configuration Manager muestra la advertencia siguiente:

> Configuration Manager devolvió un gran número de resultados. Puede restringir los resultados mediante las características de búsqueda. O hacer clic aquí para ver un número máximo de 100 000.

Ahora hay un espacio en blanco adicional entre esta advertencia y el campo de búsqueda. Este cambio ayuda a evitar que se seleccione accidentalmente la advertencia para mostrar más resultados.

### <a name="send-feedback"></a>Enviar comentarios

*(Se introdujo en la versión 1806)*
<!--1357542-->

Envíe los comentarios sobre el producto desde la consola.  

- **Enviar una sonrisa**: envíe comentarios sobre lo que le ha gustado.  

- **Enviar un ceño fruncido**: envíe comentarios sobre lo que no le ha gustado.  

- **Enviar una sugerencia**: le lleva a UserVoice para compartir sus ideas.  

Para obtener más información, vea [Comentarios sobre el producto](../../understand/find-help.md#BKMK_1806Feedback).


## <a name="assets-and-compliance-workspace"></a>Área de trabajo Activos y compatibilidad

### <a name="real-time-actions-from-device-lists"></a>Acciones en tiempo real desde las listas de dispositivos
<!--4616810-->
*(Se introdujo en la versión 1906)*

Hay varias maneras de mostrar una lista de dispositivos en el nodo **Dispositivos** del área de trabajo **Activos y compatibilidad**.

- En el área de trabajo **Activos y compatibilidad**, seleccione el nodo **Recopilaciones de dispositivos**. Seleccione una recopilación de dispositivos y elija la acción **Mostrar miembros**. Esta acción abre un subnodo del nodo **Dispositivos** con una lista de dispositivos para esa colección.  

  - Al seleccionar el subnodo de la recopilación, ahora se puede iniciar **CMPivot** desde el grupo Recopilación de la cinta.  

- En el área de trabajo **Supervisión**, seleccione el nodo **Implementaciones**. Seleccione una implementación y elija la acción **Ver estado** en la cinta. En el panel de estado de la implementación, haga doble clic en el total de recursos para obtener los detalles de una lista de dispositivos.  

  - Al seleccionar un dispositivo en esta lista, ahora se puede iniciar **CMPivot** y **Ejecutar scripts** desde el grupo Dispositivo de la cinta.  


### <a name="collections-tab-in-devices-node"></a>Pestaña Colecciones en el nodo Dispositivos
<!--4616810-->
*(Se introdujo en la versión 1906)*

En el área de trabajo **Activos y compatibilidad**, vaya al nodo **Dispositivos** y seleccione un dispositivo. En el panel de detalles, cambie a la nueva pestaña **Colecciones**. En esta pestaña se enumeran las colecciones que incluyen este dispositivo. 

> [!Note]  
> - Esta pestaña no está actualmente disponible en un subnodo de dispositivos bajo el nodo **Recopilaciones de dispositivos**. Por ejemplo, cuando selecciona la opción **Mostrar miembros** en una colección.
> - Es posible que esta pestaña no se rellene como se esperaba para algunos usuarios. Para ver la lista completa de colecciones a las que pertenece un dispositivo, debe tener el rol de seguridad **Administrador total**. Este es un problema conocido. <!--5107309--> <!--5107309-->


### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Incorporación de una columna GUID de SMBIOS a los nodos de recopilación de dispositivos y dispositivos

*(Se introdujo en la versión 1906)*

<!--4526580-->
En los nodos **Dispositivos** y **Recopilaciones de dispositivos**, ahora puede agregar una nueva columna para **GUID de SMBIOS**. Este valor es el mismo que la propiedad **GUID de BIOS** de la clase de recurso del sistema. Es un identificador único para el hardware del dispositivo.

### <a name="search-device-views-using-mac-address"></a>Vistas de búsqueda de dispositivos mediante dirección MAC

<!--3600878-->
*(Se introdujo en la versión 1902)*

Puede buscar una dirección MAC en la vista de un dispositivo de la consola de Configuration Manager. Esta propiedad es útil para los administradores de implementaciones de sistema operativo durante la solución de problemas de implementaciones de PXE. Cuando vea una lista de dispositivos, agregue la columna **Dirección MAC** a la vista. Use el campo de búsqueda para agregar los criterios de búsqueda de **Dirección MAC**.

### <a name="view-users-for-a-device"></a>Ver los usuarios de un dispositivo

A partir de la versión 1806, las siguientes columnas están disponibles en el nodo **Dispositivos**:  

- **Usuarios primarios** <!--1357280-->  

- **Usuario que ha iniciado sesión actualmente** <!--1358202-->  

    > [!NOTE]  
    > Para poder ver el usuario que ha iniciado sesión actualmente, necesitará la [detección de usuarios](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) y la [afinidad entre usuario y dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Para obtener más información sobre cómo mostrar una columna no predeterminada, vea [Uso de la consola de administración](admin-console.md#columns).

### <a name="improvement-to-device-search-performance"></a>Mejora de rendimiento de la búsqueda de dispositivos

<!-- 3614690 -->
A partir de la versión 1806, al realizar búsquedas en una recopilación de dispositivos, no se busca la palabra clave en todas las propiedades del objeto. Cuando no especifique lo que hay que buscar, busca a través de las cuatro propiedades siguientes:

- Nombre
- Usuarios primarios
- Usuario que ha iniciado sesión actualmente
- Nombre de usuario de último inicio de sesión

Este comportamiento mejora significativamente el tiempo necesario para buscar por nombre, especialmente en un entorno grande. Las búsquedas personalizadas según criterios específicos no se ven afectadas.


## <a name="software-library-workspace"></a>Área de trabajo de la Biblioteca de software

### <a name="order-by-program-name-in-task-sequence"></a>Ordenar por nombre de programa en la secuencia de tareas
<!--4616810-->
*(Se introdujo en la versión 1906)*

En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en el nodo **Secuencias de tareas**. Edite una secuencia de tareas y seleccione o agregue el paso [Instalar paquete](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage). Si un paquete tiene más de un programa, ahora en la lista desplegable los programas se ordenan alfabéticamente.

### <a name="task-sequences-tab-in-applications-node"></a>Pestaña Secuencias de tareas en el nodo Aplicaciones
<!--4616810-->
*(Se introdujo en la versión 1906)*

Vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones**, vaya al nodo **Aplicaciones** y seleccione una aplicación. En el panel de detalles, cambie a la nueva pestaña **Secuencias de tareas**. En esta pestaña se enumeran las secuencias de tareas que hacen referencia a esta aplicación.

### <a name="drill-through-required-updates"></a>Obtención de detalles de actualizaciones necesarias
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
> A partir del 21 de abril de 2020, el nombre de Office 365 ProPlus cambia a **Aplicaciones de Microsoft 365 para empresas**. Para obtener más información, vea [Cambio de nombre para Office 365 ProPlus](/deployoffice/name-change). Es posible que siga viendo referencias al nombre anterior en la consola de Configuration Manager y la documentación complementaria mientras se está actualizando la consola.

### <a name="maximize-the-browse-registry-window"></a>Maximizar la ventana Examinar registro

<!--3594151 includes all MMS 1902 console changes-->
*(Se introdujo en la versión 1902)*

1. En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y haga clic en el nodo **Aplicaciones**.
1. Seleccione una aplicación que tenga un tipo de implementación con un método de detección. Por ejemplo, un método de detección de Windows Installer.
1. En el panel de detalles, cambie a la pestaña **Tipos de implementación**.
1. Abra las propiedades de un tipo de implementación y cambie a la pestaña **Método de detección**. Haga clic en **Agregar cláusula**.
1. Cambiar **Tipo de configuración** a **Registro** y haga clic en **Examinar** para abrir la ventana **Examinar registro**. Ahora puede maximizar esta ventana.  

### <a name="edit-a-task-sequence-by-default"></a>Editar una secuencia de tareas de forma predeterminada

*(Se introdujo en la versión 1902)*

En el área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y haga clic en el nodo **Secuencias de tareas**. **Editar** es ahora la acción predeterminada cuando se abre una secuencia de tareas. Anteriormente, la acción predeterminada era **Propiedades**.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Ir a la colección desde una implementación de aplicación

*(Se introdujo en la versión 1902)*

1. En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y haga clic en el nodo **Aplicaciones**.
1. Seleccione una aplicación. En el panel de detalles, cambie a la pestaña **Implementaciones**.
1. Seleccione una implementación y, después, haga clic en la nueva opción **Colección** en la cinta de la pestaña Implementación. Esta acción cambia la vista a la colección que es el destino de la implementación.
   - Esta acción también está disponible en el menú contextual de la implementación de esta vista.


## <a name="monitoring-workspace"></a>Área de trabajo de supervisión

### <a name="correct-names-for-client-operations"></a>Nombres correctos para las operaciones de cliente
<!--4616810-->
*(Se introdujo en la versión 1906)*

En el área de trabajo **Supervisión**, seleccione **Operaciones de cliente**. La operación para **Cambiar al siguiente punto de actualización de software** ahora tiene el nombre correcto.

### <a name="show-collection-name-for-scripts"></a>Mostrar el nombre de la recopilación para los scripts
<!--4616810-->
*(Se introdujo en la versión 1906)*

En el área de trabajo **Supervisión**, seleccione el nodo **Estado del script**. Ahora se muestra el **Nombre de la recopilación** además el identificador.

### <a name="remove-content-from-monitoring-status"></a>Quitar contenido del estado de supervisión

*(Se introdujo en la versión 1902)*

1. En el área de trabajo **Supervisión**, expanda **Estado de distribución** y haga clic en **Estado de contenido**.
1. Seleccione un elemento en la lista y haga clic en la nueva opción **Ver estado** de la cinta.
1. En el panel Detalles del activo, haga clic con el botón derecho en un punto de distribución y seleccione la nueva opción **Quitar**. Esta acción quita este contenido del punto de distribución seleccionado.

### <a name="copy-details-in-monitoring-views"></a>Copiar detalles en las vistas de supervisión

*(Se introdujo en la versión 1806)*
<!--1357856-->
Se puede copiar información desde el panel **Detalles del activo** para los siguientes nodos de supervisión:  

- **Estado de distribución de contenido**  

- **Estado de implementación**  

![Vista del estado de implementación, detalles del activo de copia](media/1810-deployment-status.PNG)

## <a name="administration-workspace"></a>Área de trabajo Administración

<!--4223683-->
A partir de la versión 1906, puede habilitar algunos nodos en el nodo **Seguridad** para usar el servicio de administración. Este cambio permite que la consola se comunique con el proveedor de SMS a través de HTTPS en lugar de WMI. Para obtener más información, consulte cómo [configurar el servicio de administración](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Pasos siguientes

- [Uso del a consola](admin-console.md)
- [Notificaciones de la consola](admin-console-notifications.md)
- [Características de accesibilidad](../../understand/accessibility-features.md)