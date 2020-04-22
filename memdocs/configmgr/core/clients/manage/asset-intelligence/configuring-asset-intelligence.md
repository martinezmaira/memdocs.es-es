---
title: Configuración de Asset Intelligence
titleSuffix: Configuration Manager
description: Configure Asset Intelligence en Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56a65a0a4e1dd9a96e5725ea8c68cc435947bb08
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694763"
---
# <a name="configure-asset-intelligence-in-configuration-manager"></a>Configuración de Asset Intelligence en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Asset Intelligence realiza el inventario y administra el uso de licencias de software.   

## <a name="steps-to-configure-asset-intelligence"></a>Pasos para configurar Asset Intelligence  
   

- **Paso 1**: para recopilar los datos de inventario necesarios para los informes de Asset Intelligence, tiene que habilitar el agente del cliente de inventario de hardware como se describe en [Cómo ampliar el inventario de hardware](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Paso 2**: [habilitar clases de informes de inventario de hardware de Asset Intelligence](#BKMK_EnableAssetIntelligence).  
- **Paso 3**: [instalar un punto de sincronización de Asset Intelligence](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Paso 4**: [habilitar la auditoría de los eventos de inicio de sesión correctos](#BKMK_EnableSuccessLogonEvents)  
- **Paso 5**: [importar la información de la licencia de software](#BKMK_ImportSoftwareLicenseInformation)  
- **Paso 6**: [configurar las tareas de mantenimiento de Asset Intelligence](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Para habilitar Asset Intelligence en sitios de Configuration Manager, debe habilitar una o varias clases de informes de inventario de hardware de Asset Intelligence. Puede habilitar las clases en la página principal de **Asset Intelligence** , o bien en el área de trabajo **Administración** , en el nodo **Configuración de cliente** , en las propiedades de configuración de cliente. Utilice uno de los procedimientos siguientes.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Cómo habilitar las clases de informes de inventario de hardware de Asset Intelligence desde la página principal de Asset Intelligence  

1.  En la consola de Configuration Manager, pulse **Activos y compatibilidad** > **Asset Intelligence**.  

3.  En la pestaña **Inicio**, en el grupo **Asset Intelligence**, pulse **Editar clases de inventario**.   

4.  Para habilitar los informes de Asset Intelligence, seleccione **Habilitar todas las clases de informes de Asset Intelligence** o **Habilitar solo las clases de informes de Asset Intelligence seleccionadas**, y seleccione al menos una clase de informes de las que se muestran.  

    > [!NOTE]  
    >  Los informes de Asset Intelligence que dependan de las clases de inventario de hardware que se habiliten mediante este procedimiento no muestran datos hasta que los clientes hayan analizado y devuelto el inventario de hardware.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Cómo habilitar las clases de informes de inventario de hardware de Asset Intelligence desde las propiedades de configuración del cliente  

1.  En la consola de Configuration Manager, pulse **Administración** >  **Configuración de cliente** > **Configuración predeterminada del agente cliente**. Si ha creado una configuración de cliente personalizada, puede seleccionarla en su lugar.  

3.  En la pestaña **Inicio** > grupo **Propiedades**, pulse **Propiedades**.   

4.  Pulse **Inventario de hardware** > **Establecer clases**. .  

5.  Pulse **Filtrar por categoría** > **Clases de informes de Asset Intelligence**. La lista de clases se actualiza solo con las clases de informes de inventario de hardware de Asset Intelligence.  

6.  Seleccione al menos una clase de informes de la lista.  

    > [!NOTE]  
    >  Los informes de Asset Intelligence que dependan de las clases de inventario de hardware que se habiliten mediante este procedimiento no muestran datos hasta que los clientes hayan analizado y devuelto el inventario de hardware.  
  

###  <a name="install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

El rol de sistema de sitio de punto de sincronización de Asset Intelligence se usa para conectar sitios de Configuration Manager con System Center Online para sincronizar la información del catálogo de Asset Intelligence. El punto de sincronización de Asset Intelligence solo puede instalarse en un sistema de sitio que se encuentre en el sitio de nivel superior de la jerarquía de Configuration Manager y necesita acceso a Internet para sincronizarse con System Center Online mediante el puerto TCP 443.

Además de descargar la nueva información del catálogo Asset Intelligence, el punto de sincronización de Asset Intelligence puede cargar la información de títulos de software personalizado en System Center Online para su categorización. Microsoft trata todos los títulos de software cargados como información pública. Asegúrese de que los títulos de software personalizado no contienen información confidencial o de propiedad. Para más información sobre las solicitudes de categorización de títulos de software, vea [Solicitar una actualización del catálogo para títulos de software sin categoría](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Cómo instalar un rol de sistema de sitio de punto de sincronización de Asset Intelligence  

1.  En la consola de Configuration Manager, elija **Administración**> **Configuración de sitio** > **Servidores y roles del sistema de sitios**.  

3.  Agregue el rol de sistema de sitio de punto de sincronización de Asset Intelligence a un servidor de sistema de sitio nuevo o existente:  

    -  Para un **nuevo servidor del sistema de sitio**: en la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear servidor del sistema de sitio** para iniciar el asistente.   

        > [!NOTE]  
        >  De forma predeterminada, cuando Configuration Manager instala un rol de sistema de sitio, los archivos de instalación se instalan en la primera unidad de disco duro con formato NTFS disponible que tenga más espacio disponible en disco. Para evitar que Configuration Manager se instale en unidades concretas, cree un archivo vacío denominado No_sms_on_drive.sms y cópielo en la carpeta raíz de la unidad antes de instalar el servidor de sistema de sitio.  

    -  **Servidor de sistema de sitio existente**: haga clic en el servidor donde quiera instalar el rol de sistema de sitio de punto de sincronización de Asset Intelligence. Al seleccionar un servidor, se muestra en el panel de detalles una lista de los roles de sistema de sitio que ya están instalados en el servidor.  

         En la pestaña **Inicio**, en el grupo **Servidor**, pulse **Agregar rol de sistema de sitio** para iniciar el Asistente.  

4.  Complete la página **General**. Cuando agregue el punto de sincronización de Asset Intelligence a un servidor de sistema de sitio existente, compruebe los valores configurados previamente.  

5.  En la página **Selección de rol del sistema**, seleccione **Punto de sincronización de Asset Intelligence** en la lista de roles disponibles.  

6.  En la página **Configuración de conexión de punto de sincronización de Asset Intelligence**, pulse **Siguiente**.  

     De forma predeterminada, la opción **Usar este punto de sincronización de Asset Intelligence** está seleccionada y no se puede configurar en esta página. System Center Online acepta tráfico de red solo a través del puerto TCP 443 y, por tanto, la opción **Número de puerto SSL** no se puede configurar en esta página del asistente.  

7.  Opcionalmente, puede especificar una ruta de acceso al archivo de certificado de autenticación de System Center Online (.pfx). Normalmente, no se especifica una ruta de acceso para el certificado porque el certificado de conexión se aprovisiona automáticamente durante la instalación del rol de sitio.  

8.  En la página **Configuración del servidor proxy**, especifique si el punto de sincronización de Asset Intelligence usará un servidor proxy al conectarse a System Center Online para sincronizar el catálogo y si se deben usar credenciales para conectarse al servidor proxy.  

    > [!WARNING]  
    >  Si se requiere un servidor proxy para conectarse a System Center Online, puede que el certificado de conexión también se elimine si expira la contraseña de la cuenta de usuario configurada para la autenticación del servidor proxy.  

9. En la página **Programación de sincronización** , especifique si quiere sincronizar el catálogo Asset Intelligence según una programación. Si se habilita la programación de la sincronización, es posible configurar una programación de sincronización simple o personalizada. Durante la sincronización programada, el punto de sincronización de Asset Intelligence se conecta a System Center Online para recuperar el último catálogo Asset Intelligence. Puede sincronizar manualmente el catálogo de Asset Intelligence desde el nodo Asset Intelligence de la consola de Configuration Manager. Puede consultar los pasos para sincronizar manualmente el catálogo de Asset Intelligence en la sección [Para sincronizar manualmente el catálogo de Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) de [Operaciones de Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Completar el asistente 

###  <a name="enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Cuatro informes de Asset Intelligence muestran información recopilada de los registros de eventos de seguridad de Windows en los equipos cliente. Aquí se muestra cómo configurar la configuración de inicio de sesión de la directiva de seguridad de equipo para habilitar la auditoría de eventos de inicio de sesión correctos.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Cómo habilitar el registro de eventos de inicio de sesión correctos mediante una directiva de seguridad local  

1.  En un equipo cliente de Configuration Manager, pulse **Inicio** > **Herramientas administrativas** > **Directiva de seguridad local**.  

2.  En el cuadro de diálogo **Directiva de seguridad local**, en **Configuración de seguridad**, expanda **Directivas locales** y, después, pulse **Directiva de auditoría**.  

3.  En el panel de resultados, haga doble clic en **Auditar eventos de inicio de sesión**, asegúrese de que la casilla **Correcto** está seleccionada y, luego, pulse **Aceptar**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Cómo habilitar el registro de eventos de inicio de sesión correctos mediante una directiva de seguridad de dominio de Active Directory  

1.  En un equipo de controlador de dominio, pulse **Inicio**, seleccione **Herramientas administrativas** y, luego, pulse **Directiva de seguridad de dominio**.  

2.  En el cuadro de diálogo **Directiva de seguridad local**, en **Configuración de seguridad**, expanda **Directivas locales** y, después, pulse **Directiva de auditoría**.  

3.  En el panel de resultados, haga doble clic en **Auditar eventos de inicio de sesión**, asegúrese de que la casilla **Correcto** está seleccionada y, luego, pulse **Aceptar**.  

###  <a name="import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 En las secciones siguientes se explican los procedimientos necesarios para importar información de licencias de software general y de Microsoft en la base de datos de sitio de Configuration Manager mediante el Asistente para importar licencias de software. Cuando se importa información de licencia de software en la base de datos del sitio a partir de archivos de declaración de licencias, la cuenta de equipo del servidor de sitio requiere permisos de **Control total** del sistema de archivos NTFS del recurso compartido de archivos que se usa para importar información de licencia de software.  

> [!IMPORTANT]  
>  Cuando se importa información de licencia de software en la base de datos del sitio, se sobrescribe la información de licencia de software existente. Asegúrese de que el archivo de información de licencia de software que se utiliza con el Asistente para importar licencias de software contiene una lista completa de toda la información de licencia de software necesaria.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Cómo importar información de licencia de software en el catálogo Asset Intelligence  

1.  En el área de trabajo **Activos y compatibilidad**, pulse **Asset Intelligence**.  

2.  En la pestaña **Inicio**, en el grupo **Asset Intelligence**, pulse **Importar licencias de software**.   

4.  En la página **Importar** , especifique si está importando un archivo de licencias por volumen de Microsoft (MVLS) (.xml o .csv) o un archivo de declaración de licencia general (.csv). Para más información sobre cómo crear un archivo de declaración de licencia general, vea [Crear un archivo de información de declaración de licencia general para importación](#BKMK_CreateGeneralLicenseStatement) más adelante en este tema.  

    > [!WARNING]  
    >  Para descargar un archivo MVLS en formato .csv que pueda importar en el catálogo Asset Intelligence, consulte [Centro de servicios de licencias por volumen de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=226547). Para acceder a esta información, debe tener una cuenta registrada en el sitio web. Debe ponerse en contacto con su representante de cuenta de Microsoft para recibir información sobre cómo obtener el archivo MVLS en formato .xml.  

5.  Escriba la ruta de acceso UNC al archivo de declaración de licencia o pulse **Examinar** para seleccionar un archivo y una carpeta compartidos en la red.  

    > [!NOTE]  
    >  La carpeta compartida debe protegerse correctamente para evitar el acceso no autorizado al archivo de información de licencia y la cuenta del equipo en el que se está ejecutando el asistente debe tener permisos de Control total del recurso compartido que contiene el archivo de importación de licencia.  

6. Complete el asistente.  

###  <a name="create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Crear un archivo de información de declaración de licencia general para importación  
 Una declaración de licencia general también se puede importar en el catálogo Asset Intelligence mediante un archivo de importación de licencia creado manualmente con un formato de archivo delimitado por comas (.csv).  

> [!NOTE]  
>  Aunque solo es necesario que contengan datos los campos **Nombre**, **Publicador**, **Versión**y **EffectiveQuantity** , se deben especificar todos los campos en la primera fila del archivo de importación de licencia. Todos los campos de fecha necesitan mostrarse en el formato siguiente: día/mes/año, por ejemplo, 04/08/2008.  

Asset Intelligence coincide con los productos que se especifican en la declaración de licencia general mediante el nombre y la versión del producto, pero no el nombre del publicador. Debe utilizar un nombre de producto en la declaración de licencia general que sea exactamente igual al nombre del producto almacenado en la base de datos del sitio. Asset Intelligence toma el número **EffectiveQuantity** especificado en la declaración de licencia general y lo compara con el número de productos instalados que se encuentra en el inventario de Configuration Manager.  

> [!TIP]  
>  Para obtener una lista completa de los nombres de producto almacenados en la base de datos del sitio de Configuration Manager, puede ejecutar la consulta siguiente en la base de datos del sitio: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Puede especificar versiones exactas de un producto o especificar parte de la versión, como por ejemplo solamente la versión principal. Los ejemplos siguientes proporcionan las coincidencias de versiones resultantes de una entrada de versión de la declaración de licencia general de un producto concreto.  

|Entrada de la declaración de licencia general|Entradas de la base de datos del sitio coincidentes|  
|-------------------------------------|------------------------------------|  
|Nombre: "MySoftware", ProductVersion0:"2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|Nombre: "MySoftware", Version "2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Nombre: "Mysoftware", Version "2"<br /><br /> Nombre: "Mysoftware", Version "2.05"|Error durante la importación. Se produce un error en la importación cuando hay más de una entrada que coincide con la misma versión del producto.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Cómo crear un archivo de importación de declaración de licencia general mediante Microsoft Excel  

1.  Abra Microsoft Excel y cree una nueva hoja de cálculo.  

2.  En la primera fila de la nueva hoja de cálculo, escriba los nombres de todos los campos de datos de licencias de software.  

3.  En las filas segunda y posteriores de la hoja de cálculo nueva, escriba la información de licencia de software según sea necesario. Asegúrese de que se especifiquen al menos todos los campos de datos de las licencias de software necesarias en las filas posteriores por cada licencia de software que se quiera importar. El nombre del título de software especificado en la hoja de cálculo debe ser el mismo que el título de software que se muestre en el Explorador de recursos de un equipo cliente después de que se haya ejecutado el inventario de hardware.  

4.  Guarde el archivo en formato .csv.  

5.  Copie el archivo .csv en el recurso compartido de archivos que se use para importar información de licencia de software en el catálogo Asset Intelligence.  

6.  En la consola de Configuration Manager, use el Asistente para importar licencias de software para importar el archivo .csv recién creado.  

7.  Ejecute la **Licencia 15A - Informe de conciliación de licencias generales** de Asset Intelligence para comprobar que la información de licencia se haya importado correctamente en el catálogo Asset Intelligence.  

> [!NOTE]  
>  Para obtener un ejemplo de un archivo de licencia de software general que puede usar para realizar pruebas, vea [Ejemplo de archivo de importación de licencia general de Asset Intelligence](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabla de ejemplo para describir licencias de software  
 Cuando se crea un archivo de importación de declaración de licencia general, la información de la tabla siguiente puede utilizarse para describir las licencias de software que se importarán en el catálogo Asset Intelligence.  

|Nombre de columna|Tipo de datos|Requerido|Ejemplo|  
|-----------------|---------------|--------------|-------------|  
|Nombre|Hasta 255 caracteres|Sí|Título de software|  
|Publicador|Hasta 255 caracteres|Sí|Publicador de software|  
|Version|Hasta 255 caracteres|Sí|Versión del título de software|  
|Lenguajes|Hasta 255 caracteres|Sí|Idioma del título de software|  
|EffectiveQuantity|Valor entero|Sí|Número de licencias adquiridas|  
|PONumber|Hasta 255 caracteres|No|Información del pedido de compra|  
|ResellerName|Hasta 255 caracteres|No|Información del distribuidor|  
|DateOfPurchase|Valor de fecha en el siguiente formato: DD/MM/AAAA|No|Informes de adquisición de la licencia|  
|SupportPurchased|Valor de bit|No|0 o 1: escriba 0 para indicar sí; 1 para no|  
|SupportExpirationDate|Valor de fecha en el siguiente formato: DD/MM/AAAA|No|Fecha de finalización del soporte técnico adquirido|  
|Comentarios|Hasta 255 caracteres|No|Comentarios opcionales|  

###  <a name="configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Las tareas de mantenimiento siguientes están disponibles para Asset Intelligence.  

-   **Comprobar título de la aplicación con información de inventario**: comprueba que el título de software indicado en el inventario de software coincide con el título de software en el catálogo Asset Intelligence. De forma predeterminada, esta tarea está habilitada y programada para ejecutarse el sábado después de las 12:00 a. m. y antes de las 5:00 a. m. Esta tarea de mantenimiento solo está disponible en el sitio de nivel superior de la jerarquía de Configuration Manager.  

-   **Resumir datos de software instalado**: proporciona la información que se muestra en el área de trabajo **Activos y compatibilidad** del nodo **Software inventariado** en el nodo **Asset Intelligence**. Cuando se ejecuta la tarea, Configuration Manager realiza un recuento de todos los títulos de software inventariado en el sitio primario. De forma predeterminada, esta tarea está habilitada y programada para ejecutarse todos los días después de las 12:00 a. m. y antes de las 5:00 a. m. Esta tarea de mantenimiento solo está disponible en los sitios primarios.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Cómo configurar tareas de mantenimiento de Asset Intelligence  

1.  En la consola de Configuration Manager, pulse **Administración** > **Configuración del sitio** > **Sitios**.  

3.  Seleccione el sitio en el que quiere configurar la tarea de mantenimiento de Asset Intelligence.  

4.  En la pestaña **Inicio**, en el grupo **Configuración**, pulse **Mantenimiento del sitio**. Seleccione una tarea y pulse **Editar** para modificar la configuración. 

    Le recomendamos que establezca el período de tiempo en horas de poca actividad del sitio. El período de tiempo es el intervalo de tiempo en el que puede ejecutar la tarea. Se define mediante las opciones **Iniciar después de** y **Hora de inicio más tardía** que se especifican en el cuadro de diálogo **Propiedades de la tarea** .  

    Puede iniciar la tarea inmediatamente si selecciona el día actual y configura la hora de **Iniciar después de** a un par de minutos después de la hora actual.  

7.  Pulse **Aceptar** para guardar la configuración. La tarea se ejecuta ahora según la programación.  

    > [!NOTE]  
    >  Si una tarea no se puede ejecutar en el primer intento, Configuration Manager intenta volverla a ejecutar hasta que se ejecuta correctamente o hasta que pasa el período de tiempo en el que la tarea se puede ejecutar.  
