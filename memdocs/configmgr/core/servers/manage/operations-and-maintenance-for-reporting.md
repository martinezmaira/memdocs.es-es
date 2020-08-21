---
title: Operaciones y mantenimiento de informes
titleSuffix: Configuration Manager
description: Obtenga detalles sobre la administración de informes y suscripciones a informes en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 21bb81e9851ab80d7807df337a67005e5b6b292a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699660"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Operaciones y mantenimiento de informes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Cuando la infraestructura de generación de informes esté operativa en Configuration Manager, puede realizar una serie de operaciones habituales para administrar informes y suscripciones a informes.

> [!NOTE]
> Este artículo se centra en los informes de SQL Server Reporting Services. A partir de la versión 2002, puede integrar informes con Power BI Report Server. Para obtener más información, vea [Integración con Power BI Report Server](powerbi-report-server.md).

## <a name="run-a-report-from-reporting-services"></a>Ejecución de un informe desde Reporting Services

Configuration Manager almacena los informes en SQL Server Reporting Services. El informe recupera los datos de la base de datos del sitio de Configuration Manager. Puede acceder a los informes en la consola de Configuration Manager o mediante el Administrador de informes, a través de un explorador web. Abra los informes desde un explorador web en cualquier equipo con acceso al punto de servicios de informes y con un usuario que tenga derechos suficientes para ver los informes. Para ejecutar informes, necesita derechos de **lectura** para los permisos **Sitio** y **Ejecutar informe** para objetos específicos.

Al ejecutar un informe, el título, la descripción y la categoría del informe se muestran en el idioma del sistema operativo local. Para obtener más información, consulte [Idiomas para los informes](configuring-reporting.md#-languages-for-reports).

> [!NOTE]  
> El Administrador de informes es una herramienta de administración y acceso a informes basada en web. Puede usarlo para administrar una única instancia del servidor de informes a través de una conexión HTTPS. Use el Administrador de informes para las tareas operativas, es decir, ver los informes, modificar las propiedades de los informes y administrar suscripciones a informes asociados. En este artículo se indican los pasos que hay que seguir para ver un informe y modificar sus propiedades en el Administrador de informes. Para obtener más información sobre otras opciones del Administrador de informes, consulte [Administrador de informes](/sql/reporting-services/report-server/manage-a-reporting-services-native-mode-report-server).

Utilice los procedimientos siguientes para ejecutar un informe de Configuration Manager.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Ejecución de un informe en la consola de Configuration Manager

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Expanda **Creación de informes** y seleccione **Informes**. En este nodo se muestran los informes disponibles.

    > [!TIP]
    > Si no aparece ningún informe en el nodo, compruebe que el punto de servicios de informes está instalado y configurado. Para más información, consulte [Configuración de informes](configuring-reporting.md).

1. Seleccione el informe que quiere ejecutar. En la pestaña **Inicio** de la cinta de opciones, en la sección **Grupo de informes**, seleccione **Ejecutar** para abrir el informe.

1. Si se necesitan parámetros, especifíquelos y seleccione **Ver informe**.

### <a name="run-a-report-in-a-web-browser"></a>Ejecución de un informe en un explorador web

1. En el explorador web, vaya a la dirección URL del Administrador de informes, por ejemplo, `https://Server1/Reports`. Encontrará la dirección URL en la página **Report Manager URL** (Dirección URL del Administrador de informes) del Administrador de configuración de Reporting Services.

1. En el Administrador de informes, seleccione la carpeta de informes de Configuration Manager, por ejemplo, **ConfigMgr_CAS**.

    > [!TIP]
    > Si no aparece ningún informe en el Administrador de informes, compruebe que el punto de servicios de informes está instalado y configurado. Para más información, consulte [Configuración de informes](configuring-reporting.md).

1. Seleccione la categoría de informe del informe que quiere ejecutar y, luego, el informe específico. El informe se abre en el Administrador de informes.

1. Si se necesitan parámetros, especifíquelos y seleccione **Ver informe**.

## <a name="modify-the-properties-of-a-report"></a>Modificación de las propiedades de un informe

Las propiedades del informe incluyen el nombre y la descripción del informe. Puede ver las propiedades de un informe en la consola de Configuration Manager.

Para cambiar las propiedades, use el Administrador de informes:

1. En el explorador web, vaya a la dirección URL del Administrador de informes, por ejemplo, `https://Server1/Reports`.

1. En el Administrador de informes, seleccione la carpeta de informes de Configuration Manager, por ejemplo, **ConfigMgr_CAS**.

1. Seleccione la categoría de informe y, luego, el informe específico. El informe se abre en el Administrador de informes.

1. Seleccione la pestaña **Propiedades**. Modifique el nombre y la descripción del informe y seleccione **Aplicar**.

El Administrador de informes guarda las propiedades del informe en el servidor de informes. En la consola de Configuration Manager se muestran las propiedades actualizadas del informe.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a> Modificación de un informe

Si un informe de Configuration Manager no recupera la información que le interesa, modifíquelo en el Generador de informes. También puede usar el Generador de informes para cambiar la presentación o el diseño del informe. Aunque se puede modificar directamente un informe predeterminado, es mejor clonarlo. Abra el informe para editarlo y seleccione **Guardar como**.

Para editar un informe, necesita los permisos de **modificación del sitio** y de **modificación de informes** en los objetos específicos del informe.

> [!IMPORTANT]
> Las actualizaciones del sitio conservan los informes integrados. Si modifica un informe estándar, cuando el sitio se actualice, el nombre del informe se cambiará por un prefijo de subrayado (`_`). Este comportamiento garantiza que la actualización del sitio no sobrescriba el informe modificado por el informe estándar.
>
> Si modifica informes predefinidos, antes de instalar una actualización del sitio, realice una copia de seguridad de los informes personalizados. Después de la actualización, restaure el informe en Reporting Services. Si va a realizar cambios importantes en un informe predefinido, cree uno nuevo en su lugar. No se sobrescriben los nuevos informes creados antes de actualizar un sitio.

Use el siguiente procedimiento para editar las propiedades de un informe de Configuration Manager.

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. Expanda **Creación de informes** y seleccione el nodo **Informes**.

1. Seleccione el informe que quiere modificar. En la pestaña **Inicio** de la cinta de opciones, en la sección **Grupo de informes**, seleccione **Editar**. Es posible que se le pida que escriba las credenciales. Si el Generador de informes no está instalado en el equipo, Configuration Manager le pedirá que lo instale. Se requiere el Generador de informes para modificar y crear informes.

1. En el Generador de informes, modifique la configuración de informes correspondiente. Seleccione **Guardar** para guardar el informe en el servidor de informes.

## <a name="create-reports"></a>Crear informes

Se pueden crear dos tipos de informes:

- Un **informe basado en modelo** le permite seleccionar de forma interactiva los elementos que quiere incluir en el informe. Para obtener más información sobre cómo crear modelos de informes personalizados, vea [Creación de modelos de informes personalizados de Configuration Manager en SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).

- Un **informe basado en SQL** le permite recuperar los datos basados en una instrucción SQL del informe.

> [!IMPORTANT]
> Para crear un informe, la cuenta necesita el permiso de **modificación del sitio**. Solo puede crear un informe en las carpetas para las que tenga permisos de **modificación de informes**.

### <a name="create-a-model-based-report"></a>Creación de un informe basado en modelo

Use los procedimientos siguientes para crear un informe de Configuration Manager basado en modelo.

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y seleccione el nodo **Informes**.

1. En la pestaña **Inicio** de la cinta de opciones, en la sección **Crear**, seleccione **Crear informe**. Esta acción abre el **Asistente para crear informes**.

1. En la página **Información** , configure las siguientes opciones:

    - **Tipo**: Seleccione **Informe basado en modelo**.

    - **Nombre**: especifique un nombre para el informe.

    - **Descripción**: especifique una descripción para el informe.

    - **Servidor**: muestra el nombre del servidor de informes en el que se crea este informe.

    - **Ruta de acceso**: seleccione **Examinar** para especificar una carpeta en la que almacenar el informe.

1. En la página **Selección de modelo**, seleccione un modelo disponible en la lista para crear este informe. En la sección **Vista previa** se muestran las vistas y entidades de SQL Server que están disponibles en este modelo de informe.

1. Complete el Asistente para crear informes.

1. Abra el Generador de informes para configurar las opciones del informe. Para obtener más información, vea [Edición de un informe de Configuration Manager](#bkmk_edit).

1. En el Generador de informes, cree el diseño del informe, seleccione datos en las vistas de SQL Server disponibles y agregue parámetros al informe.

1. Seleccione **Ejecutar** para ejecutar el informe. Compruebe que el informe proporciona la información esperada. Si es necesario, seleccione **Diseño** para modificar todavía más el informe.

1. Seleccione **Guardar** para guardar el informe en el servidor de informes.

### <a name="create-a-sql-based-report"></a>Creación de un informe basado en SQL

Al crear una instrucción SQL para un informe personalizado, no haga referencia directamente a las tablas de SQL Server. Haga referencia siempre a las vistas de informes de SQL Server compatibles desde la base de datos del sitio. Estas vistas tienen nombres que empiezan por `v_`. Para obtener más información, consulte cómo [crear informes personalizados mediante vistas de SQL Server en Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

También puede hacer referencia a procedimientos almacenados públicos desde la base de datos del sitio. Estos procedimientos almacenados tienen nombres que empiezan por `sp_`.

Use los procedimientos siguientes para crear un informe de Configuration Manager basado en SQL.

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y seleccione el nodo **Informes**.

1. En la pestaña **Inicio** de la cinta de opciones, en la sección **Crear**, seleccione **Crear informe**. Esta acción abre el **Asistente para crear informes**.

1. En la página **Información** , configure las siguientes opciones:

    - **Tipo**: Seleccione **Informe basado en SQL**.

    - **Nombre**: especifique un nombre para el informe.

    - **Descripción**: especifique una descripción para el informe.

    - **Servidor**: muestra el nombre del servidor de informes en el que se crea este informe.

    - **Ruta de acceso**: seleccione **Examinar** para especificar una carpeta en la que almacenar el informe.

1. Complete el Asistente para crear informes.

1. Abra el Generador de informes para configurar las opciones del informe. Para obtener más información, vea [Edición de un informe de Configuration Manager](#bkmk_edit).

1. En el Generador de informes, proporcione la instrucción SQL para el informe. También puede generar la instrucción SQL mediante el uso de columnas de las vistas disponibles. Si es necesario, agregue parámetros al informe.

1. Seleccione **Ejecutar** para ejecutar el informe. Compruebe que el informe proporciona la información esperada. Si es necesario, seleccione **Diseño** para modificar todavía más el informe.

1. Seleccione **Guardar** para guardar el informe en el servidor de informes.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a> Administrar suscripciones a informes

Las suscripciones a informes en SQL Server Reporting Services permiten configurar la entrega automática de determinados informes a través de correo electrónico o de un recurso compartido de archivos en intervalos programados. Para configurar suscripciones de informes, use el **Asistente para crear suscripciones** en Configuration Manager.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Creación de una suscripción de informe para la entrega de un informe a un recurso compartido de archivos

Cuando se crea una suscripción de informe para la entrega de un informe a un recurso compartido de archivos, Reporting Services copia el informe en el formato especificado en el recurso compartido de archivo que se ha seleccionado. Solo puede realizar la suscripción y la solicitud de entrega de un único informe a la vez.

Cuando cree una suscripción que usa un recurso compartido de archivos, especifique como destino una carpeta compartida existente. El servidor de informes no crea la carpeta o el recurso compartido de red. Cuando especifique la carpeta de destino en una suscripción, use una ruta de acceso UNC y no incluya barras diagonales inversas (`\`) en la ruta de la carpeta. El ejemplo siguiente es una ruta de acceso UNC válida para la carpeta de destino: `\\server\reportfiles\operations\2001`.

> [!NOTE]
> Cuando cree la suscripción, especifique un nombre de usuario y una contraseña. Esta cuenta necesita acceso a este recurso compartido con permisos de **escritura** en la carpeta de destino.

Reporting Services puede representar informes en diferentes formatos de archivo, como MHTML o Excel. Seleccione el formato al crear la suscripción. Aunque es posible seleccionar cualquier formato de representación admitido, la representación de archivos funciona mejor en algunos formatos que en otros.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Limitaciones de las suscripciones de informe en un recurso compartido de archivos

La lista siguiente incluye las limitaciones de las suscripciones de informe en un recurso compartido de archivos:

- A diferencia de los informes que se hospedan y se administran en un servidor de informes, Reporting Services entrega los informes como archivos estáticos en una carpeta compartida.

- Las características interactivas del informe no funcionan con los informes almacenados como archivos. El informe representa las características interactivas como elementos estáticos.

- Si el informe incluye gráficos, usa la presentación predeterminada.

- Si el informe se vincula a otro informe, representa el vínculo como texto estático.

Si quiere conservar las características interactivas en un informe entregado, use la entrega a través de correo electrónico. Para obtener más información, consulte [Para crear una suscripción de informe para entregar un informe por correo electrónico](#bkmk_subscription-email).

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Proceso para crear una suscripción de informe para un recurso compartido de archivos

Utilice el procedimiento siguiente para crear una suscripción de informe para entregar un informe a un recurso compartido de archivos.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y seleccione el nodo **Informes**.

1. Seleccione una carpeta de informes y elija el informe al que quiere suscribirse. En la pestaña **Inicio** de la cinta de opciones, en la sección **Grupo de informes**, seleccione **Crear suscripción**. Esta acción abre el **Asistente para crear suscripciones**.

1. En la página **Entrega de suscripción** , configure las siguientes opciones:  

    - **Informe entregado por**: Seleccione **Recurso compartido de archivos de Windows**.

    - **Nombre de archivo**: especifique el nombre de archivo del informe. De forma predeterminada, el archivo de informe no incluye una extensión de nombre de archivo. Seleccione **Agregar extensión de archivo al crearse** para agregar automáticamente una extensión de nombre de archivo en función del formato.

    - **Ruta de acceso**: Especifique una ruta de acceso UNC a una carpeta existente en la que quiera entregar este informe. Por ejemplo, `\\server\reportfiles\operations`.

    - **Formato de representación**: seleccione uno de los formatos siguientes para el archivo de informe:

      - **Archivo XML con datos de informe**
      - **CSV (delimitado por comas)**
      - **Archivo TIFF**
      - **Archivo de Acrobat (PDF)**
      - **HTML 4.0**
        > [!NOTE]
        > Si el informe tiene imágenes, el formato HTML 4.0 no las incluirá.
      - **MHTML (archivo web)**
      - **Representador de RPL** (diseño de página de informe)
      - **Excel**
      - **Word**

    - **Nombre de usuario**: especifique una cuenta de usuario de Windows con permisos de *escritura* en la **ruta de acceso** especificada.

    - **Contraseña**: especifique la contraseña de la anterior cuenta de usuario de Windows.

    - **Opción de sobrescritura**: Seleccione una de las siguientes opciones para configurar el comportamiento si ya existe un archivo con el mismo nombre en la carpeta de destino:

      - **Sobrescribir archivos existentes con nuevas versiones**
      - **No sobrescribir archivos existentes**
      - **Incrementar nombres de archivo al agregarse nuevas versiones**: esta opción anexa un número al nombre de archivo del nuevo informe para distinguirlo de las versiones anteriores.

    - **Descripción**: opcionalmente, especifique información adicional sobre esta suscripción de informe.

1. En la página **Programación de suscripción** , seleccione una de las siguientes opciones de programación de entrega para la suscripción de informe:

    - **Usar programación compartida**: una programación compartida es una programación definida previamente que puede ser utilizada por otras suscripciones de informes. Al seleccionar esta opción, elija también una programación compartida. Si no hay programaciones compartidas, seleccione la opción para crear una programación.

    - **Crear nueva programación**: configure la programación de ejecución de este informe. La programación incluye el intervalo, la hora y fecha de inicio y la fecha de finalización de esta suscripción. De forma predeterminada, las suscripciones nuevas crean una programación para su ejecución cada hora a partir de la fecha y hora actuales.

1. En página **Parámetros de suscripción**, especifique los parámetros que requiere este informe para ejecutarse sin supervisión. Si el informe no tiene parámetros, el asistente no mostrará esta página.

1. Complete el asistente.

1. Compruebe que Configuration Manager haya creado correctamente la suscripción de informe. Seleccione el nodo **Suscripciones** para ver y modificar las suscripciones de informe.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a> Creación de una suscripción de informe para la entrega de un informe a través del correo electrónico

Cuando crea una suscripción de informe para entregar un informe por correo electrónico, Reporting Services envía un correo electrónico a los destinatarios configurados. El correo electrónico incluye el informe como datos adjuntos. El servidor de informes no valida las direcciones de correo electrónico ni las obtiene de un servidor de correo electrónico. Puede enviar informes a través del correo electrónico a cualquier cuenta de correo electrónico válida dentro o fuera de su organización.

> [!NOTE]
> Para habilitar la opción de suscripción **Correo electrónico**, debe configurar las opciones de correo electrónico en Reporting Services. Para obtener más información, consulte [Entrega por correo electrónico en Reporting Services](/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services).

Puede seleccionar las dos opciones de entrega de correo electrónico siguientes:

- Enviar una notificación con un vínculo al informe generado.

- Enviar un informe adjunto o incrustado. El formato de representación y el explorador determinan si el informe se inserta o se adjunta.

  - Si el explorador es compatible con HTML 4.0 y MHTML y se selecciona el formato **MHTML (archivo web)** , el correo electrónico inserta el informe en el mensaje.
  - Todos los demás formatos proporcionan los informes como datos adjuntos.
  - Reporting Services no comprueba el tamaño de los datos adjuntos o del mensaje antes de enviar el informe. Si los datos adjuntos o el mensaje superan el límite máximo que permite el servidor de correo electrónico, el informe no se entregará.

Utilice el procedimiento siguiente para crear una suscripción de informe para entregar un informe a través de correo electrónico.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y seleccione el nodo **Informes**.

1. Seleccione una carpeta de informes y elija el informe al que quiere suscribirse. En la pestaña **Inicio** de la cinta de opciones, en la sección **Grupo de informes**, seleccione **Crear suscripción**. Esta acción abre el **Asistente para crear suscripciones**.

1. En la página **Entrega de suscripción** , configure las siguientes opciones:  

    - **Informe entregado por**: Seleccione **Correo electrónico**.

    - **Para**: especifique una dirección de correo electrónico válida como destinatario.

        > [!NOTE]
        > Para especificar varios destinatarios, separe cada dirección de correo electrónico con un punto y coma (`;`).

    - **CC**: opcionalmente, especifique una dirección de correo electrónico para que reciba una copia de este informe.

    - **CCO**: opcionalmente, especifique una dirección de correo electrónico para que reciba una copia oculta de este informe.

    - **Responder a**: especifique la dirección de respuesta. Si el destinatario responde al mensaje de correo electrónico, la respuesta se enviará a esta dirección.

    - **Asunto**: especifique una línea de asunto del mensaje de correo electrónico de suscripción.

    - **Prioridad**: seleccione la marca de prioridad del mensaje de correo electrónico: **Baja**, **Normal** o **Alta**. Microsoft Exchange usa esta marca para indicar la importancia del mensaje de correo electrónico.

    - **Comentario**: especifique el texto del cuerpo del mensaje de correo electrónico de suscripción.

    - **Descripción**: opcionalmente, especifique información adicional sobre esta suscripción de informe.

    - **Incluir vínculo**: incluya la dirección URL de este informe en el cuerpo del mensaje de correo electrónico.

    - **Incluir informe**: adjunte el informe al mensaje de correo electrónico. Use la opción **Formato de representación** para especificar el formato del informe que se va a adjuntar.

    - **Formato de representación**: seleccione uno de los siguientes formatos para el archivo del informe adjunto:

      - **Archivo XML con datos de informe**
      - **CSV (delimitado por comas)**
      - **Archivo TIFF**
      - **Archivo de Acrobat (PDF)**
      - **MHTML (archivo web)**
      - **Excel**
      - **Word**

1. En la página **Programación de suscripción** , seleccione una de las siguientes opciones de programación de entrega para la suscripción de informe:

    - **Usar programación compartida**: una programación compartida es una programación definida previamente que puede ser utilizada por otras suscripciones de informes. Al seleccionar esta opción, elija también una programación compartida. Si no hay programaciones compartidas, seleccione la opción para crear una programación.

    - **Crear nueva programación**: configure la programación de ejecución de este informe. La programación incluye el intervalo, la hora y fecha de inicio y la fecha de finalización de esta suscripción. De forma predeterminada, las suscripciones nuevas crean una programación para su ejecución cada hora a partir de la fecha y hora actuales.

1. En página **Parámetros de suscripción**, especifique los parámetros que requiere este informe para ejecutarse sin supervisión. Si el informe no tiene parámetros, el asistente no mostrará esta página.

1. Complete el asistente.

1. Compruebe que Configuration Manager haya creado correctamente la suscripción de informe. Seleccione el nodo **Suscripciones** para ver y modificar las suscripciones de informe.