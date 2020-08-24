---
title: Consola de Configuration Manager
titleSuffix: Configuration Manager
description: Obtenga información sobre la navegación a través de la consola de Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126517"
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


## <a name="next-steps"></a>Pasos siguientes

- [Notificaciones de la consola](admin-console-notifications.md)
- [Sugerencias de la consola](admin-console-tips.md)
- [Características de accesibilidad](../../understand/accessibility-features.md)
- [Editor de secuencias de tareas](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
