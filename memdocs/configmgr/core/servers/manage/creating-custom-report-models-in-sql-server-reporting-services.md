---
title: Creación de informes personalizados
titleSuffix: Configuration Manager
description: Defina modelos de informe para satisfacer sus requisitos empresariales y, después, impleméntelos en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: fe570eeedc2c050bdaf27903d30ddffff63109d9
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879163"
---
# <a name="creating-custom-report-models-for-configuration-manager-in-sql-server-reporting-services"></a>Creación de modelos de informes personalizados de Configuration Manager en SQL Server Reporting Services

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager incluye modelos de informe de ejemplo, pero también se pueden definir otros modelos de informe para satisfacer sus requisitos empresariales y, después, implementarlos en Configuration Manager de modo que se usen al crear informes basados en modelos. La tabla siguiente proporciona los pasos para crear e implementar un modelo de informe básico.  

> [!NOTE]  
>  Para obtener los pasos para crear un modelo de informe más avanzado, consulte la sección [Pasos para crear un modelo de informe avanzado en SQL Server Reporting Services](#AdvancedReportModel) de este tema.  

|Paso|Descripción|Más información|  
|----------|-----------------|----------------------|  
|Comprobar que SQL Server Business Intelligence Development Studio está instalado|Los modelos de informe se diseñan y crean con SQL Server Business Intelligence Development Studio. Compruebe que SQL Server Business Intelligence Development Studio esté instalado en el equipo en que va a crear el modelo de informe personalizado.|Para obtener más información acerca de SQL Server Business Intelligence Development Studio, consulte la documentación de SQL Server 2008.|  
|Crear un proyecto de modelo de informe|Un proyecto de modelo de informe contiene la definición del origen de datos (un archivo .ds), la definición de una vista del origen de datos (un archivo .dsv) y el modelo de informe (un archivo .smdl).|Para obtener más información, consulte la sección [Para crear el proyecto de modelo de informe](#BKMK_CreateReportModelProject) de este tema.|  
|Definir un origen de datos para un modelo de informe|Después de crear un proyecto de modelo de informe, tendrá que definir un origen de datos desde el que extraer los datos empresariales. Normalmente, se trata de la base de datos de sitio de Configuration Manager.|Para obtener más información, consulte la sección [Para definir el origen de datos para el modelo de informe](#BKMK_DefineReportModelDataSource) de este tema.|  
|Definir una vista del origen de datos para un modelo de informe|Después de definir los orígenes de datos que se utilizan en el proyecto de modelo de informe, el siguiente paso es definir una vista del origen de datos para el proyecto. Una vista del origen de datos es un modelo de datos lógico basado en uno o varios orígenes de datos. Las vistas del origen de datos encapsulan el acceso a los objetos físicos, tales como tablas y vistas, contenidos en orígenes de datos subyacentes. SQL Server Reporting Services genera el modelo de informe desde la vista del origen de datos.<br /><br /> Las vistas del origen de datos facilitan el proceso de diseño del modelo ya que le proporcionan una representación útil de los datos especificados. Sin cambiar el origen de datos subyacente, puede cambiar el nombre de las tablas y los campos, y agregar campos de agregado y tablas derivadas en una vista del origen de datos. Para un modelo eficaz, agregue a la vista del origen de datos solo las tablas que va a utilizar.|Para obtener más información, consulte la sección [Para definir la vista del origen de datos para el modelo de informe](#BKMK_DefineReportModelDataSourceView) de este tema.|  
|Crear un modelo de informe|Un modelo de informe es una capa por encima de una base de datos que identifica los roles, los campos y las entidades empresariales. Cuando se publica, mediante el uso de estos modelos, los usuarios del Generador de informes pueden desarrollar informes sin necesidad de estar familiarizados con las estructuras de base de datos, o de entender y escribir consultas. Los modelos se componen de conjuntos de elementos de informe relacionados que se agrupan bajo un nombre descriptivo, con relaciones predefinidas entre estos elementos empresariales y con cálculos predefinidos. Los modelos se definen mediante el uso de un lenguaje XML llamado Lenguaje de definición de modelos semánticos (SMDL). La extensión de nombre de archivo para los archivos de modelo de informe es .smdl.|Para obtener más información, consulte la sección [Para crear el modelo de informe](#BKMK_CreateReportModel) de este tema.|  
|Publicar un modelo de informe|Para generar un informe mediante el modelo que acaba de crear, debe publicarlo en un servidor de informes. El origen de datos y la vista del origen de datos se incluyen en el modelo cuando se publica.|Para obtener más información, consulte la sección [Para publicar el modelo de informe para su uso en SQL Server Reporting Services](#BKMK_PublishReportModel) de este tema.|  
|Implementar el modelo de informe en Configuration Manager|Antes de usar un modelo de informe personalizado en el **Asistente para crear informes** para crear un informe basado en modelo, debe implementar el modelo de informe en Configuration Manager.|Para obtener más información, consulte la sección [Para implementar el modelo de informe personalizado en Configuration Manager](#BKMK_DeployReportModel) de este tema.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Pasos para crear un modelo de informe básico en SQL Server Reporting Services  
 Puede usar los procedimientos siguientes para crear un modelo de informe básico que podrán usar los usuarios de su sitio para generar informes particulares basados en modelo según los datos en una sola vista de la base de datos de Configuration Manager. Se crea un modelo de informe que presenta información acerca de los equipos cliente en su sitio para el autor del informe. Esta información se obtiene de la vista **v_R_System** en la base de datos de Configuration Manager.  

 En el equipo en que realice estos procedimientos, asegúrese de que tiene instalado SQL Server Business Intelligence Development Studio y de que el equipo tiene conectividad de red con el servidor de punto de servicios de informes. Para obtener información detallada acerca de SQL Server Business Intelligence Development Studio, consulte la documentación de SQL Server 2008.  

###  <a name="to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a> Para crear el modelo de informe  

1.  En el escritorio, haga clic en **Inicio**, en **Microsoft SQL Server 2008**y, a continuación, en **SQL Server Business Intelligence Development Studio**.  

2.  Cuando **SQL Server Business Intelligence Development Studio** se abra en Microsoft Visual Studio, haga clic en **Archivo**, en **Nuevo**y, a continuación, en **Proyecto**.  

3.  En el cuadro de diálogo **Nuevo proyecto** , seleccione **Proyecto de modelos de informe** en la lista **Plantillas** .  

4.  En el cuadro **Nombre** , especifique un nombre para este modelo de informe. Para este ejemplo, escriba **Simple_Model**.  

5.  Para crear el proyecto de modelo de informe, haga clic en **Aceptar**.  

6.  La solución **Simple_Model** se muestra en en **Explorador de soluciones**.  

    > [!NOTE]  
    >  Si no puede ver el panel **Explorador de soluciones** , haga clic en **Ver**y, a continuación, haga clic en **Explorador de soluciones**.  

###  <a name="to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a> Para definir el origen de datos para el modelo de informe  

1.  En el panel **Explorador de soluciones** de **SQL Server Business Intelligence Development Studio**, haga clic con el botón secundario en **Orígenes de datos** para seleccionar **Agregar nuevo origen de datos**.  

2.  En la página inicial del **Asistente para orígenes de datos** , haga clic en **Siguiente**.  

3.  En la página **Seleccione cómo definir la conexión** , compruebe que **Crear un origen de datos basado en una conexión nueva o existente** esté seleccionado y, a continuación, haga clic en **Nuevo**.  

4.  En el cuadro de diálogo **Administrador de conexiones** , especifique las siguientes propiedades de conexión para el origen de datos:  

    -   **Nombre del servidor**: escriba el nombre del servidor de base de datos de sitio de Configuration Manager o selecciónelo en la lista. Si está trabajando con una instancia con nombre en lugar de la instancia predeterminada, escriba &lt;*servidor de bases de datos*>\\&lt;*nombre de instancia*>.  

    -   Seleccione **Utilizar autenticación de Windows**.  

    -   En la lista **Seleccionar o escribir un nombre de base de datos**, seleccione el nombre de su base de datos de sitio de Configuration Manager.  

5.  Para comprobar la conexión de la base de datos, haga clic en **Conexión de prueba**.  

6.  Si la conexión se realiza correctamente, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Administrador de conexiones** . Si la conexión no se realiza correctamente, compruebe que la información indicada sea correcta y, a continuación, haga clic en **Conexión de prueba** de nuevo.  

7.  En la página **Seleccione cómo definir la conexión** , compruebe que **Crear un origen de datos basado en una conexión nueva o existente** esté seleccionado, compruebe que el origen de datos que acaba de especificar esté seleccionado en **Conexiones de datos**y, a continuación, haga clic en **Siguiente**.  

8.  En **Nombre de origen de datos**, especifique un nombre para el origen de datos y, a continuación, haga clic en **Finalizar**. Para este ejemplo, escriba **Simple_Model**.  

9. El origen de datos **Simple_Model.ds** se muestra ahora en el **Explorador de soluciones** , bajo el nodo **Orígenes de datos** .  

    > [!NOTE]  
    >  Para editar las propiedades de un origen de datos existente, haga doble clic en el origen de datos en la carpeta **Orígenes de datos** del panel **Explorador de soluciones** para mostrar las propiedades del origen de datos en el Diseñador de origen de datos.  

###  <a name="to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a> Para definir la vista del origen de datos para el modelo de informe  

1.  En el **Explorador de soluciones**, haga clic con el botón secundario en **Vistas del origen de datos** para seleccionar **Agregar nueva vista del origen de datos**.  

2.  En la página inicial del **Asistente para orígenes de datos** , haga clic en **Siguiente**. Se mostrará la página **Seleccionar un origen de datos** .  

3.  En la ventana **Orígenes de datos relacionales** , compruebe que esté seleccionado el origen de datos **Simple_Model** y, a continuación, haga clic en **Siguiente**.  

4.  En la página **Seleccionar tablas y vistas** , seleccione la vista siguiente en la lista **Objetos disponibles** para usar en el modelo de informe: **v_R_System (dbo)** .  

    > [!TIP]  
    >  Para ubicar las vistas más fácilmente en la lista **Objetos disponibles** , haga clic en el encabezado **Nombre** en la parte superior de la lista para ordenar los objetos por orden alfabético.  

5.  Después de seleccionar la vista, haga clic en **>** para transferir el objeto a la lista **Objetos incluidos** .  

6.  Si se muestra la página **Coincidencia de nombres** , acepte las selecciones predeterminadas y haga clic en **Siguiente**.  

7.  Cuando haya seleccionado los objetos que necesite, haga clic en **Siguiente**y, a continuación, especifique un nombre para la vista del origen de datos. Para este ejemplo, escriba **Simple_Model**.  

8.  Haga clic en **Finalizar**. La vista del origen de datos **Simple_Model.dsv** se mostrará en la carpeta **Vistas del origen de datos** del **Explorador de soluciones**.  

###  <a name="to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a> To create the report model  

1.  En el **Explorador de soluciones**, haga clic con el botón secundario en **Modelos de informe** para seleccionar **Agregar nuevo modelo de informe**.  

2.  En la página inicial del **Asistente para modelos de informe** , haga clic en **Siguiente**.  

3.  En la página **Seleccionar vistas del origen de datos** , seleccione la vista del origen de datos en la lista **Vistas del origen de datos disponibles** y, a continuación, haga clic en **Siguiente**. Para este ejemplo, seleccione **Simple_Model.dsv**.  

4.  En la página **Seleccionar reglas de generación de modelos de informe** , acepte los valores predeterminados y, a continuación, haga clic en **Siguiente**.  

5.  En la página **Recopilar estadísticas del modelo** , compruebe que esté seleccionado **Actualizar estadísticas del modelo antes de generar** y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Finalización del asistente** , especifique un nombre para el modelo de informe. Para este ejemplo, compruebe que se muestra **Simple_Model** .  

7.  Para completar el asistente y crear el modelo de informe, haga clic en **Ejecutar**.  

8.  Para salir del asistente, haga clic en **Finalizar**. El modelo de informe se muestra en la ventana de diseño.  

###  <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> Para publicar el modelo de informe para su uso en SQL Server Reporting Services  

1.  En el **Explorador de soluciones**, haga clic con el botón secundario en el modelo de informe y seleccione **Implementar**. Para este ejemplo, el modelo de informe es **Simple_Model.smdl**.  

2.  Examine el estado de la implementación en la esquina inferior izquierda de la ventana de **SQL Server Business Intelligence Development Studio** . Cuando haya terminado la implementación, se mostrará **Operación Implementar finalizada correctamente** . Si la implementación produce un error, el motivo del error se muestra en la ventana **Resultado** . El nuevo modelo de informe está ahora disponible en el sitio web de SQL Server Reporting Services.  

3.  Haga clic en **Archivo**, haga clic en **Guardar todo**y, a continuación, cierre **SQL Server Business Intelligence Development Studio**.  

###  <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1. Busque la carpeta en la que se creó el proyecto de modelo de informe. Por ejemplo, %*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\ *&lt;Nombre del proyecto\>.*  

2. Copie los archivos siguientes de la carpeta del proyecto de modelo de informe en una carpeta temporal en el equipo:  

   -   *&lt;Nombre del modelo\>* **.dsv**  

   -   *&lt;Nombre del modelo\>* **.smdl**  

3. Abra los archivos anteriores con un editor de texto, como el Bloc de notas.  

4. En el archivo _&lt;Nombre del modelo\>_ **.dsv**, busque la primera línea del archivo, que dice lo siguiente:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Edite esta línea para que quede como sigue:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`  

5. Copie todo el contenido del archivo en el Portapapeles de Windows.  

6. Cierre el archivo _&lt;Nombre del modelo\>_ **.dsv**.  

7. En el archivo _&lt;Nombre del modelo\>_ **.smdl**, busque las últimas tres líneas del archivo, que muestran lo siguiente:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Pegue el contenido del archivo _&lt;Nombre del modelo\>_ **.dsv** directamente antes de la última línea del archivo ( **&lt;SemanticModel\>** ).  

9. Guarde y cierre el archivo _&lt;Nombre del modelo\>_ **.smdl**.  

10. Copie el archivo _&lt;Nombre del modelo\>_ **.smdl** en la carpeta *%programfiles%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other en el servidor de sitio de Configuration Manager.  

    > [!IMPORTANT]  
    >  Después de copiar el archivo de modelo de informe en el servidor de sitio de Configuration Manager, debe salir y reiniciar la consola de Configuration Manager para poder usar el modelo de informe en el **Asistente para crear informes**.  

##  <a name="steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> Pasos para crear un modelo de informe avanzado en SQL Server Reporting Services  
 Puede usar los procedimientos siguientes para crear un modelo de informe avanzado que podrán usar los usuarios de su sitio para generar informes particulares basados en modelo según los datos en varias vistas de la base de datos de Configuration Manager. Se crea un modelo de informe que presenta a su autor la información sobre los equipos cliente y el sistema operativo instalado en estos equipos. Esta información se obtiene de las vistas siguientes de la base de datos de Configuration Manager:  

- **V_R_System**: contiene información sobre los equipos detectados y el cliente de Configuration Manager.  

- **V_GS_OPERATING_SYSTEM**: contiene información sobre el sistema operativo instalado en el equipo cliente.  

  Los elementos seleccionados en las vistas anteriores se consolidan en una sola lista, con nombres descriptivos y, a continuación, se presentan al autor del informe en el Generador de informes para su inclusión en informes particulares.  

  En el equipo en que realice estos procedimientos, asegúrese de que tiene instalado SQL Server Business Intelligence Development Studio y de que el equipo tiene conectividad de red con el servidor de punto de servicios de informes. Para obtener información detallada acerca de SQL Server Business Intelligence Development Studio, consulte la documentación de SQL Server.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  En el escritorio, haga clic en **Inicio**, en **Microsoft SQL Server 2008**y, a continuación, en **SQL Server Business Intelligence Development Studio**.  

2.  Cuando **SQL Server Business Intelligence Development Studio** se abra en Microsoft Visual Studio, haga clic en **Archivo**, en **Nuevo**y, a continuación, en **Proyecto**.  

3.  En el cuadro de diálogo **Nuevo proyecto** , seleccione **Proyecto de modelos de informe** en la lista **Plantillas** .  

4.  En el cuadro **Nombre** , especifique un nombre para este modelo de informe. Para este ejemplo, escriba **Advanced_Model**.  

5.  Para crear el proyecto de modelo de informe, haga clic en **Aceptar**.  

6.  La solución **Advanced_Model** se muestra en el **Explorador de soluciones**.  

    > [!NOTE]  
    >  Si no puede ver el panel **Explorador de soluciones** , haga clic en **Ver**y, a continuación, haga clic en **Explorador de soluciones**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>Para definir el origen de datos para el modelo de informe  

1.  En el panel **Explorador de soluciones** de **SQL Server Business Intelligence Development Studio**, haga clic con el botón secundario en **Orígenes de datos** para seleccionar **Agregar nuevo origen de datos**.  

2.  En la página inicial del **Asistente para orígenes de datos** , haga clic en **Siguiente**.  

3.  En la página **Seleccione cómo definir la conexión** , compruebe que **Crear un origen de datos basado en una conexión nueva o existente** esté seleccionado y, a continuación, haga clic en **Nuevo**.  

4.  En el cuadro de diálogo **Administrador de conexiones** , especifique las siguientes propiedades de conexión para el origen de datos:  

    -   **Nombre del servidor**: escriba el nombre del servidor de base de datos de sitio de Configuration Manager o selecciónelo en la lista. Si está trabajando con una instancia con nombre en lugar de la instancia predeterminada, escriba &lt;*servidor de bases de datos*>\\&lt;*nombre de instancia*>.  

    -   Seleccione **Utilizar autenticación de Windows**.  

    -   En la lista **Seleccionar o escribir un nombre de base de datos**, seleccione el nombre de su base de datos de sitio de Configuration Manager.  

5.  Para comprobar la conexión de la base de datos, haga clic en **Conexión de prueba**.  

6.  Si la conexión se realiza correctamente, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Administrador de conexiones** . Si la conexión no se realiza correctamente, compruebe que la información indicada sea correcta y, a continuación, haga clic en **Conexión de prueba** de nuevo.  

7.  En la página **Seleccione cómo definir la conexión** , compruebe que **Crear un origen de datos basado en una conexión nueva o existente** esté seleccionado, compruebe que el origen de datos que acaba de especificar esté seleccionado en el cuadro de lista **Conexiones de datos** y, a continuación, haga clic en **Siguiente**.  

8.  En **Nombre de origen de datos**, especifique un nombre para el origen de datos y, a continuación, haga clic en **Finalizar**. Para este ejemplo, escriba **Advanced_Model**.  

9. El origen de datos **Advanced_Model.ds** se muestra en el **Explorador de soluciones** , bajo el nodo **Orígenes de datos** .  

    > [!NOTE]  
    >  Para editar las propiedades de un origen de datos existente, haga doble clic en el origen de datos en la carpeta **Orígenes de datos** del panel **Explorador de soluciones** para mostrar las propiedades del origen de datos en el Diseñador de origen de datos.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>Para definir la vista del origen de datos para el modelo de informe  

1. En el **Explorador de soluciones**, haga clic con el botón secundario en **Vistas del origen de datos** para seleccionar **Agregar nueva vista del origen de datos**.  

2. En la página inicial del **Asistente para orígenes de datos** , haga clic en **Siguiente**. Se mostrará la página **Seleccionar un origen de datos** .  

3. En la ventana **Orígenes de datos relacionales** , compruebe que esté seleccionado el origen de datos **Advanced_Model** y, a continuación, haga clic en **Siguiente**.  

4. En la página **Seleccionar tablas y vistas** , seleccione las vistas siguientes en la lista **Objetos disponibles** para usar en el modelo de informe:  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     Después de seleccionar cada vista, haga clic en **>** para transferir el objeto a la lista **Objetos incluidos** .  

   > [!TIP]  
   >  Para ubicar las vistas más fácilmente en la lista **Objetos disponibles** , haga clic en el encabezado **Nombre** en la parte superior de la lista para ordenar los objetos por orden alfabético.  

5. Si se muestra el cuadro de diálogo **Coincidencia de nombres** , acepte las selecciones predeterminadas y haga clic en **Siguiente**.  

6. Cuando haya seleccionado los objetos que necesite, haga clic en **Siguiente**y, a continuación, especifique un nombre para la vista del origen de datos. Para este ejemplo, escriba **Advanced_Model**.  

7. Haga clic en **Finalizar**. La vista del origen de datos **Advanced_Model.dsv** se mostrará en la carpeta **Vistas del origen de datos** del **Explorador de soluciones**.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Para definir las relaciones en la vista del origen de datos  

1.  En el **Explorador de soluciones**, haga doble clic en **Advanced_Model.dsv** para abrir la ventana de diseño.  

2.  Haga clic con el botón secundario en la barra de título de la ventana **v_R_System** para seleccionar **Reemplazar tabla**y, a continuación, haga clic en **Con nueva consulta con nombre**.  

3.  En el cuadro de diálogo **Crear consulta con nombre** , haga clic en el icono **Agregar tabla** (normalmente el último icono de la cinta).  

4.  En el cuadro de diálogo **Agregar tabla** , haga clic en la pestaña **Vistas** , seleccione **V_GS_OPERATING_SYSTEM** en la lista y, a continuación, haga clic en **Agregar**.  

5.  Haga clic en **Cerrar** para cerrar el cuadro de diálogo **Agregar tabla** .  

6.  En el cuadro de diálogo **Crear consulta con nombre** , especifique la siguiente información:  

    -   **Nombre:** especifique el nombre de la consulta. Para este ejemplo, escriba **Advanced_Model**.  

    -   **Descripción:** especifique una descripción de la consulta. En este ejemplo, escriba **Modelo de Reporting Services de ejemplo**.  

7.  En la ventana **v_R_System** , seleccione los elementos siguientes en la lista de objetos que se mostrarán en el modelo de informe:  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  En el cuadro **v_GS_OPERATING_SYSTEM** , seleccione los elementos siguientes en la lista de objetos que se mostrarán en el modelo de informe:  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Para presentar los objetos de estas vistas como una lista al autor del informe, debe especificar una relación entre las dos tablas o vistas mediante una combinación. Se pueden combinar las dos vistas con la utilización del objeto **ResourceID**, que aparece en ambas vistas.  

10. En la ventana **v_R_System** , haga clic en el objeto **ResourceID** y manténgalo pulsado mientras lo arrastra al objeto **ResourceID** en la ventana **v_GS_OPERATING_SYSTEM** .  

11. Haga clic en **Aceptar**.  

12. La ventana **Advanced_Model** reemplaza la ventana **v_R_System** y contiene todos los objetos necesarios para el modelo de informe de las vistas **v_R_System** y **v_GS_OPERATING_SYSTEM** . Ahora puede eliminar la ventana **v_GS_OPERATING_SYSTEM** desde el Diseñador de vistas de origen de datos. Haga clic con el botón secundario en la barra de título de la ventana **v_GS_OPERATING_SYSTEM** para seleccionar **Eliminar tabla de vista de origen de datos**. En el cuadro de diálogo **Eliminar objetos** , haga clic en **Aceptar** para confirmar la eliminación.  

13. Haga clic en **Archivo**y, a continuación, en **Guardar todo**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  En el **Explorador de soluciones**, haga clic con el botón secundario en **Modelos de informe** para seleccionar **Agregar nuevo modelo de informe**.  

2.  En la página inicial del **Asistente para modelos de informe** , haga clic en **Siguiente**.  

3.  En la página **Seleccionar vista de origen de datos** , seleccione la vista del origen de datos en la lista **Vistas del origen de datos disponibles** y, a continuación, haga clic en **Siguiente**. Para este ejemplo, seleccione **Simple_Model.dsv**.  

4.  En la página **Seleccionar reglas de generación de modelos de informe** , no modifique los valores predeterminados y, a continuación, haga clic en **Siguiente**.  

5.  En la página **Recopilar estadísticas del modelo** , compruebe que esté seleccionado **Actualizar estadísticas del modelo antes de generar** y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Finalización del asistente** , especifique un nombre para el modelo de informe. Para este ejemplo, compruebe que se muestra **Advanced_Model** .  

7.  Para completar el asistente y crear el modelo de informe, haga clic en **Ejecutar**.  

8.  Para salir del asistente, haga clic en **Finalizar**.  

9. El modelo de informe se muestra en la ventana de diseño.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Para modificar los nombres de objetos en el modelo de informe  

1.  En el **Explorador de soluciones**, haga clic con el botón secundario en el modelo de informe para seleccionar **Diseñador de vistas**. Para este ejemplo, seleccione **Advanced_Model.smdl**.  

2.  En la vista de diseño del modelo de informe, haga clic con el botón secundario en cualquier nombre de objeto para seleccionar **Cambiar nombre**.  

3.  Escriba un nuevo nombre para el objeto seleccionado y, a continuación, presione Entrar. Por ejemplo, puede cambiar el nombre del objeto **CSD_Version_0** para leer **Versión del Service Pack de Windows**.  

4.  Cuando haya terminado de cambiar el nombre de objetos, haga clic en **Archivo**y, a continuación, en **Guardar todo**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>Para publicar el modelo de informe para su uso en SQL Server Reporting Services  

1.  En el **Explorador de soluciones**, haga clic con el botón secundario en **Advanced_Model.smdl** para seleccionar **Implementar**.  

2.  Examine el estado de la implementación en la esquina inferior izquierda de la ventana de **SQL Server Business Intelligence Development Studio** . Cuando haya terminado la implementación, se mostrará **Operación Implementar finalizada correctamente** . Si la implementación produce un error, el motivo del error se muestra en la ventana **Resultado** . El nuevo modelo de informe está ahora disponible en el sitio web de SQL Server Reporting Services.  

3.  Haga clic en **Archivo**, haga clic en **Guardar todo**y, a continuación, cierre **SQL Server Business Intelligence Development Studio**.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1. Busque la carpeta en la que se creó el proyecto de modelo de informe. Por ejemplo, %*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\ *&lt;Nombre del proyecto\>.*  

2. Copie los archivos siguientes de la carpeta del proyecto de modelo de informe en una carpeta temporal en el equipo:  

   -   *&lt;Nombre del modelo\>* **.dsv**  

   -   *&lt;Nombre del modelo\>* **.smdl**  

3. Abra los archivos anteriores con un editor de texto, como el Bloc de notas.  

4. En el archivo _&lt;Nombre del modelo\>_ **.dsv**, busque la primera línea del archivo, que dice lo siguiente:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Edite esta línea para que quede como sigue:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`

5. Copie todo el contenido del archivo en el Portapapeles de Windows.  

6. Cierre el archivo _&lt;Nombre del modelo\>_ **.dsv**.  

7. En el archivo _&lt;Nombre del modelo\>_ **.smdl**, busque las últimas tres líneas del archivo, que muestran lo siguiente:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Pegue el contenido del archivo _&lt;Nombre del modelo\>_ **.dsv** directamente antes de la última línea del archivo ( **&lt;SemanticModel\>** ).  

9. Guarde y cierre el archivo _&lt;Nombre del modelo\>_ **.smdl**.  

10. Copie el archivo _&lt;Nombre del modelo\>_ **.smdl** en la carpeta *%programfiles%* \Microsoft Endpoint Manager\AdminConsole\XmlStorage\Other en el servidor de sitio de Configuration Manager.  

    > [!IMPORTANT]  
    >  Después de copiar el archivo de modelo de informe en el servidor de sitio de Configuration Manager, debe salir y reiniciar la consola de Configuration Manager para poder usar el modelo de informe en el **Asistente para crear informes**.  
