---
title: Configuración de informes
titleSuffix: Configuration Manager
description: Configuración de la generación de informes en la jerarquía de Configuration Manager, incluida la información acerca de SQL Server Reporting Services.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e53c61052b8ee1b217a5268e8877dc4f4415f477
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692628"
---
# <a name="configure-reporting-in-configuration-manager"></a>Configuración de la generación de informes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para crear, modificar y ejecutar informes en la consola de Configuration Manager, debe completar varias tareas de configuración. Use este artículo como guía para configurar la generación de informes en la jerarquía de Configuration Manager.  

Antes de instalar y configurar SQL Server Reporting Services en la jerarquía, lea los siguientes artículos dedicados a la generación de informes de Configuration Manager:  

- [Introducción a los informes](introduction-to-reporting.md)  

- [Planeación de informes](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services es una plataforma de generación de informes basada en servidor que proporciona exhaustivas funciones de informes para diferentes tipos de orígenes de datos. El punto de servicios de informes en Configuration Manager se comunica con SQL Server Reporting Services para:

- Copiar los informes de Configuration Manager en una carpeta de informes especificada
- Configurar los parámetros de Reporting Services
- Configurar los parámetros de seguridad de Reporting Services

Cuando se ejecuta un informe, el componente de Reporting Services se conecta con la base de datos de sitio de Configuration Manager para recuperar los datos.  

Para poder instalar el punto de servicios de informes en un sitio de Configuration Manager, instale y configure SQL Server Reporting Services en el sistema de sitio de destino. Para obtener más información, consulte [Instalación de SQL Server Reporting Services](/sql/reporting-services/install-windows/install-reporting-services).  

### <a name="verify-sql-server-reporting-services-installation"></a>Comprobación de la instalación de SQL Server Reporting Services

Utilice el procedimiento siguiente para comprobar que SQL Server Reporting Services está instalado y se ejecuta correctamente.

1. Vaya al menú **Inicio** en el sistema de sitio y abra **Administrador de configuración de Reporting Services**. Puede encontrarlo en la sección **Herramientas de configuración** del grupo **Microsoft SQL Server**.

2. En la ventana **Conexión de configuración de Reporting Services**, escriba el nombre del servidor que hospeda SQL Server Reporting Services. Seleccione la instancia de SQL Server en la que instaló SQL Reporting Services. Luego, seleccione **Conectar** para abrir el Administrador de configuración de Reporting Services.  

3. En la página **Estado del servidor de informes**, compruebe que **Estado del servidor de informes** está configurado en **Iniciado**. Si no está en este estado, seleccione **Iniciar**.  

4. En la página **Dirección URL del servicio web**, seleccione la dirección URL en **Direcciones URL del servicio web de del servicio de informes**. Esta acción prueba la conexión a la carpeta de informes. El explorador podría solicitar las credenciales. Compruebe que la página web se abre correctamente.

5. En la página **Base de datos**, compruebe que la opción **Modo del servidor de informes** está configurada en **Nativo**.  

6. En la página **Dirección URL del Administrador de informes**, seleccione la dirección URL en **Identificación del sitio del Administrador de informes**. Esta acción prueba la conexión al directorio virtual para el Administrador de informes. El explorador podría solicitar las credenciales. Compruebe que la página web se abre correctamente.

    > [!NOTE]  
    > La generación de informes en Configuration Manager no requiere el Administrador de informes de Reporting Services. Solo lo necesita si desea ejecutar informes en el explorador o administrar informes mediante el Administrador de informes.  

7. Seleccione **Salir** para cerrar el Administrador de configuración de Reporting Services.  

## <a name="configure-reporting-to-use-report-builder-30"></a>Configuración de informes para usar el Generador de informes 3.0

1. En el equipo que ejecuta la consola de Configuration Manager, abra el editor del Registro de Windows.  

2. Vaya a `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting`.

3. Abra la clave **ReportBuilderApplicationManifestName** para editar los datos del valor.  

4. Cambie el valor a `ReportBuilder_3_0_0_0.application` y, luego, seleccione **Aceptar** para guardar.

5. Cierre el editor del Registro de Windows.  

## <a name="install-a-reporting-services-point"></a>Instalar un punto de servicios de informes

Para administrar informes en un sitio, instale el punto de servicios de informes. El punto de servicios de informes:

- copia los informes y las carpetas de informes en SQL Server Reporting Services.
- aplica la directiva de seguridad para los informes y las carpetas.
- establece la configuración en Reporting Services.

### <a name="requirements-and-limitations"></a>Limitaciones y requisitos

Para poder ver o administrar informes en la consola de Configuration Manager, necesita un punto de servicios de informes. Configure este rol de sistema de sitio en un servidor con Microsoft SQL Server Reporting Services. Para más información, consulte [Requisitos previos de los informes](prerequisites-for-reporting.md).  

- Cuando selecciona un sitio para instalar el punto de servicios de informes, los usuarios que accederán a los informes deben estar en el mismo ámbito de seguridad que el sitio en el se instala el rol.  

- Una vez instalado un punto de servicios de informes en un sistema de sitio, no cambie la dirección URL del servidor de informes.

    Pongamos, por ejemplo, que crea el punto de servicios de informes. A continuación, modifica la dirección URL del servidor de informes en el Administrador de configuración de Reporting Services. La consola de Configuration Manager sigue utilizando la dirección URL anterior. En este caso, no puede ejecutar, editar ni crear informes desde la consola.

    Si necesita cambiar la dirección URL del servidor de informes, quite primero el punto de servicios de informes existente. Cambie la dirección URL y, a continuación, vuelva a instalar el punto de servicios de informes.  

- Cuando instale un punto de servicios de informes, especifique una [cuenta para el punto de servicios de informes](../../plan-design/hierarchy/accounts.md#reporting-services-point-account). Para que los usuarios de un dominio diferente ejecuten un informe, cree una relación de confianza bidireccional entre los dominios. De lo contrario, el informe no se ejecutará.

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" /> Instalación del punto de servicios de informes en un sistema de sitio  

Para obtener más información sobre cómo configurar sistemas de sitio, consulte [Instalación de roles de sistema de sitio](../deploy/configure/install-site-system-roles.md).  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Servidores y roles del sistema de sitios**.  

1. Agregue el punto de servicios de informes a un servidor de sistema de sitio nuevo o existente:  

    - *Sistema de sitio nuevo*: En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Crear servidor del sistema de sitio**. Se abre el **Asistente para crear servidor de sistema de sitio** .  

    - *Sistema de sitio existente*: Seleccione el servidor de destino. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Servidor**, seleccione **Agregar rol de sistema de sitio**. Se abre el **Asistente para agregar roles de sistema de sitio** .  

1. En la página **General** , especifique la configuración general para el servidor de sistema de sitio. Cuando se agrega el punto de servicios de informes a un servidor existente, compruebe los valores que se habían configurado previamente.  

1. En la página **Selección de rol del sistema**, seleccione **Punto de servicios de informes** en la lista de roles disponibles y, a continuación, seleccione **Siguiente**.  

1. En la página **Punto de servicios de informes**, configure las siguientes opciones:  

    - **Nombre de servidor de base de datos del sitio**: especifique el nombre del servidor que hospeda la base de datos de sitio de Configuration Manager. Normalmente, el asistente recupera el nombre de dominio completo (FQDN) del servidor. Para especificar una instancia de base de datos, use el formato &lt;*nombre de servidor*>\&lt;*nombre de instancia*>. Por ejemplo, `sqlserver\named1`.

    - **Nombre de la base de datos**: Especifique el nombre de la base de datos del sitio de Configuration Manager. Seleccione **Comprobar** para confirmar que el asistente tiene acceso a la base de datos del sitio.  

        > [!IMPORTANT]  
        > La cuenta de usuario que use para crear el punto de servicios de informes debe tener acceso de **lectura** a la base de datos del sitio. Si se produce un error en la prueba de conexión, aparecerá un icono de advertencia rojo. El texto contextual que aparece al pasar el puntero contiene los detalles del error. Corrija el error y, a continuación, seleccione **Prueba** otra vez.  

    - **Nombre de la carpeta**: Especifique el nombre de la carpeta que se crea y se usa para los informes de Configuration Manager en Reporting Services.  

    - **Instancia de servidor de Reporting Services**: Seleccione la instancia de SQL Server para Reporting Services. Si esta página no muestra ninguna instancia, compruebe que SQL Server Reporting Services se ha instalado, configurado e iniciado.  

        > [!IMPORTANT]  
        > Configuration Manager realiza una conexión en el contexto del usuario actual con el WMI en el sistema de sitio seleccionado. Utiliza esta conexión para recuperar la instancia de SQL Server para Reporting Services. El usuario actual debe tener acceso de **lectura** a WMI en el sistema de sitio; o el asistente no puede obtener las instancias de Reporting Services.  

    - **Cuenta de punto de Reporting Services**: Seleccione **Establecer** y, a continuación, seleccione la cuenta que se va a usar. SQL Server Reporting Services en el punto de servicios de informes usa esta cuenta para conectarse a la base de datos de sitio de Configuration Manager. Esta conexión sirve para recuperar los datos de un informe. Seleccione **Cuenta existente** para especificar una cuenta de usuario de Windows configurada previamente como cuenta de Configuration Manager. Seleccione **Nueva cuenta** para especificar una cuenta de usuario de Windows que no está configurada actualmente para su uso. Configuration Manager concede automáticamente acceso al usuario especificado a la base de datos del sitio.  

        La cuenta que ejecuta Reporting Services debe pertenecer al grupo de seguridad local de dominio **Grupo de acceso de autorización de Windows**. Esto concede a la cuenta los permisos **Permitir lectura** en el atributo **tokenGroupsGlobalAndUniversal** para todos los objetos de usuario dentro del dominio. Los usuarios de un dominio distinto al de la cuenta de punto de servicios de informes necesita una relación de confianza bidireccional entre los dominios para la correcta ejecución de los informes.

        La cuenta de usuario de Windows especificada y la contraseña se cifran, y se almacenan en la base de datos de Reporting Services. Reporting Services recupera los datos de los informes de la base de datos del sitio mediante el uso de esta cuenta y contraseña.  

        > [!IMPORTANT]  
        > La cuenta que especifique debe tener permiso de **Inicio de sesión local** en el equipo que hospeda la base de datos de Reporting Services.  

1. Complete el asistente.

Una vez completado el asistente, Configuration Manager crea las carpetas de informes en Reporting Services. Después, copia sus informes en las carpetas de informes especificadas.  

> [!TIP]  
> Para que aparezcan solo los sistemas de sitio que hospedan el rol de sitio de punto de servicios de informes, haga clic con el botón derecho en **Servidores y roles del sistema de sitios** y seleccione el **Punto de servicios de informes**.  

### <a name="languages-for-reports"></a><a name="bkmk_languages" /> Idiomas para los informes

<!-- SCCMDocs#1067 -->

Cuando Configuration Manager crea las carpetas de informes y copia los informes en el servidor de informes, determina el idioma apropiado para los objetos.

- Crear carpetas de informes, copiar informes

  - Crear objetos con la configuración regional del sistema operativo del servidor de sitio

  - Si el paquete de idioma específico no está disponible, el valor predeterminado es inglés (ENU).

- Ver informes en un explorador web

  - Nombres de carpetas e informes: la misma configuración regional que el servidor de sitio
  
  - Contenido del informe: dinámico según la configuración regional del explorador

- Ver informes en la consola de Configuration Manager

  - Nombres de carpetas y informes: dinámico según la configuración regional de la consola
  
  - Contenido del informe: dinámico según la configuración regional de la consola

Cuando se instala un punto de servicios de informes en un sitio sin paquetes de idioma, los informes se instalan en inglés. Si instala un paquete de idioma tras instalar el punto de servicios de informes, debe desinstalar y reinstalar el punto de servicios de informes para que los informes estén disponibles en el idioma del paquete de idioma apropiado.  

Para obtener más información, consulte [Paquetes de idioma](../deploy/install/language-packs.md).

### <a name="file-installation-and-report-folder-security-rights"></a>Derechos de seguridad de carpeta de informes e instalación de archivos

Configuration Manager realiza las acciones siguientes para instalar el punto de servicios de informes y configurar Reporting Services:  

> [!IMPORTANT]  
> El sitio realiza estas acciones en el contexto de la cuenta configurada para el servicio SMS_Executive. Normalmente, esta cuenta es la cuenta del sistema local del servidor de sitio.  

- Instala el rol de sitio del punto de servicios de informes.  

- Crea el origen de datos en Reporting Services con las credenciales almacenadas que se especificó en el asistente. Esta cuenta es la contraseña y la cuenta de usuario de Windows que utiliza Reporting Services para conectarse con la base de datos del sitio cuando ejecuta informes.  

- Crea la carpeta raíz de Configuration Manager en Reporting Services.  

- Agrega los roles de seguridad **Usuarios de informes de Configuration Manager** y **Administradores de informes de Configuration Manager** en Reporting Services.  

- Crea subcarpetas y, a continuación, implementa los informes de Configuration Manager desde `%ProgramFiles%\SMS_SRSRP` en el servidor de sitio para Reporting Services.  

- Agrega el rol **Usuarios de informes de Configuration Manager** de Reporting Services a las carpetas raíz para todas las cuentas de usuario de Configuration Manager que tengan derechos de **lectura del sitio**.  

- Agrega el rol **Administradores de informes de Configuration Manager** de Reporting Services a las carpetas raíz para todas las cuentas de usuario de Configuration Manager que tengan derechos de **modificación del sitio**.  

- Recupera la asignación entre las carpetas de informes y los tipos de objeto protegidos de Configuration Manager. Configuration Manager mantiene esta asignación en la base de datos del sitio.  

- Configura los siguientes derechos para los usuarios administrativos de Configuration Manager en carpetas de informes específicas de Reporting Services:  

  - Agrega usuarios y asigna el rol **Usuarios de informes de Configuration Manager** a la carpeta de informes asociada para los usuarios administrativos que tengan los permisos **Ejecutar informe** para el objeto de Configuration Manager.  

  - Agrega usuarios y asigna el rol **Administradores de informes de Configuration Manager** a la carpeta de informes asociada para los usuarios administrativos que tengan los permisos **Modificar informe** para el objeto de Configuration Manager.  

Configuration Manager se conecta a Reporting Services y establece los permisos para los usuarios en las carpetas raíz de Configuration Manager y Reporting Services, y en carpetas de informes específicas. Tras la instalación inicial del punto de servicios de informes, Configuration Manager se conecta a Reporting Services cada 10 minutos para comprobar que los derechos de usuario configurados en las carpetas de informes son los derechos asociados que están establecidos para los usuarios de Configuration Manager. Cuando se agregan usuarios o se modifican derechos de usuario en la carpeta de informes mediante el uso del Administrador de informes de Reporting Services, Configuration Manager sobrescribe estos cambios por medio del uso de asignaciones basadas en roles almacenadas en la base de datos del sitio. Configuration Manager también quita los usuarios que no tienen derechos de generación de informes en Configuration Manager.  

### <a name="reporting-services-security-roles"></a>Roles de seguridad de Reporting Services

Cuando Configuration Manager instala el punto de servicios de informes, agrega los siguientes roles de seguridad en Reporting Services:  

- **Usuarios de informes de Configuration Manager**: los usuarios a los que se les asigna este rol de seguridad solo pueden ejecutar informes de Configuration Manager.  

- **Administradores de informes de Configuration Manager**: Los usuarios a los que se les asigna este rol de seguridad pueden realizar todas las tareas relacionadas con informes en Configuration Manager.  

## <a name="verify-installation"></a><a name="bkmk_verify"></a> Comprobación de la instalación

Compruebe la instalación del punto de servicios de informes mediante la visualización de entradas del archivo de registro y mensajes de estado específicos. Utilice el siguiente procedimiento para comprobar que la instalación del punto de servicios de informes se realizó correctamente.  

> [!Note]  
> Si ve informes en la subcarpeta **Informes** del nodo **Informes** del área de trabajo **Supervisión** de la consola de Configuration Manager, puede omitir este procedimiento.

### <a name="verify-installation-by-status-message"></a>Comprobación de la instalación por mensaje de estado

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado del sistema** y haga clic en el nodo **Estado del componente**.  

1. Seleccione el componente **SMS_SRS_REPORTING_POINT**.  

1. En la pestaña **Inicio** de la cinta, en el grupo **Componente**, seleccione **Mostrar mensajes** y luego elija **Todos**.  

1. Especifique una fecha y una hora para un período anterior a la instalación del punto de servicios de informes y, a continuación, seleccione **Aceptar**.  

1. Compruebe el identificador del mensaje de estado **1015**. Este mensaje de estado indica que el punto de servicios de informes se instaló correctamente.

### <a name="verify-installation-by-log-file"></a>Comprobación de la instalación por archivo de registro

Abra el archivo **Srsrp.log**, ubicado en el directorio **Registros** de la ruta de instalación de Configuration Manager. Busque la cadena `Installation was successful`.

Lea este archivo de registro a partir de la hora en la que se instaló correctamente el punto de servicios de informes. Compruebe que se crearon las carpetas de informes, se implementaron los informes, y se confirmó la directiva de seguridad en todas las carpetas. Después de la última línea de las confirmaciones de la directiva de seguridad, busque la cadena `Successfully checked that the SRS web service is healthy on server`.  

## <a name="configure-a-certificate-to-author-reports"></a>Configuración de un certificado para crear informes

Existen muchas opciones para crear informes de SQL Server Reporting Services. Cuando se crean o editan informes en la consola de Configuration Manager, Configuration Manager abre el Generador de informes para usarlo como entorno de creación. Independientemente de cómo cree los informes de Configuration Manager, necesita un certificado autofirmado para la autenticación del servidor en el servidor de base de datos del sitio.

> [!NOTE]  
> Para obtener más información acerca de la creación de informes con SQL Server Reporting Services, consulte [Entorno de creación del Generador de informes](/sql/reporting-services/tools/report-builder-authoring-environment-ssrs).  

Configuration Manager instala automáticamente el certificado en el servidor de sitio y los roles del Proveedor de SMS. Puede crear o modificar informes desde la consola de Configuration Manager cuando esta se ejecuta desde uno de estos servidores.

Al crear o modificar informes desde una consola de Configuration Manager en otro equipo, exporte el certificado desde el servidor de sitio. El nombre descriptivo del certificado específico es el nombre de dominio completo del servidor de sitio en el almacén de certificados **Personas de confianza**. Agregue el certificado al almacén de certificados **Personas de confianza** en el equipo que ejecuta la consola de Configuration Manager.  

## <a name="modify-reporting-services-point-settings"></a>Modificación de la configuración del punto de servicios de informes

Una vez instalado este rol, puede modificar la conexión de base de datos del sitio y la configuración de autenticación en las propiedades del punto de servicios de informes.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Servidores y roles del sistema de sitios**.  

    > [!TIP]  
    > Para que aparezcan solo los sistemas de sitio que hospedan el punto de servicios de informes, haga clic con el botón derecho en el nodo **Servidores y roles del sistema de sitios** y seleccione el **Punto de servicios de informes**.  

1. Seleccione el sistema de sitio que hospeda el punto de servicios de informes. A continuación, seleccione los roles del sistema de sitio del **Punto de servicio de informes** en el panel de detalles.

1. En la pestaña **Rol del sitio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.  

1. Puede modificar las opciones siguientes en las **propiedades del punto de servicios de informes**:  

    - **Nombre de servidor de base de datos del sitio**

    - **Nombre de la base de datos**

    - **Cuenta de usuario**

1. Seleccione **Aceptar** para guardar los cambios y cerrar las propiedades.  

Para obtener más información acerca de esta configuración, consulte las descripciones de la sección para [instalar el punto de servicio de informes en un sistema de sitio](#bkmk_install).

## <a name="power-bi-report-server"></a>Power BI Report Server

A partir de la versión 2002, puede integrar informes con Power BI Report Server. Para obtener más información sobre su configuración, vea [Integración con Power BI Report Server](powerbi-report-server.md).

## <a name="upgrade-sql-server"></a>Actualización de SQL Server

Para actualizar SQL Server y SQL Server Reporting Services, quite primero el punto de servicios de informes del sitio. Después de actualizar SQL Server, vuelva a instalar el punto de servicios de informes en Configuration Manager.

Si no sigue este proceso, verá errores al ejecutar o editar informes desde la consola de Configuration Manager. Puede continuar con la ejecución y edición de informes correctamente desde un explorador web.  

## <a name="configure-report-options"></a>Configuración de las opciones de informes

Puede seleccionar el punto de servicios de informes predeterminado que utiliza para administrar informes. El sitio puede tener más de un punto de servicios de informes, pero solo usa el servidor predeterminado para administrar informes. Utilice el siguiente procedimiento para configurar las opciones de informes para su sitio.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y seleccione el nodo **Informes**.  

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Configuración**, seleccione **Opciones de informes**.  

1. Seleccione el servidor de informes predeterminado en la lista y, a continuación, seleccione **Aceptar**.

Si no muestra ningún servidor, compruebe que instaló y configuró un punto de servicios de informes en el sitio. Para obtener más información, vea [Comprobación de la instalación](#bkmk_verify).

Asegúrese de que el equipo ejecuta una versión del Generador de informes de SQL Server que coincide con la versión de SQL Server que usa para el servidor de informes. De lo contrario verá un error, el servidor de informes predeterminado no se guardará y no podrá crear ni editar informes.<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>Pasos siguientes

[Operaciones y mantenimiento de informes](operations-and-maintenance-for-reporting.md)