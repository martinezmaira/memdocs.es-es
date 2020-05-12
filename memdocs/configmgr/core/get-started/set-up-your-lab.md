---
title: Configurar el laboratorio
titleSuffix: Configuration Manager
description: Configure un laboratorio para evaluar Configuration Manager con actividades simuladas de la vida real.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 216c61a671d7d06e434fa399bb3bae12e12f7275
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905161"
---
# <a name="set-up-a-configuration-manager-lab"></a>Configuración de un laboratorio de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las instrucciones de este tema le permitirán configurar un laboratorio para evaluar Configuration Manager con actividades simuladas de la vida real.  

> [!NOTE]
> Microsoft ofrece una versión preconfigurada de este laboratorio con una versión de evaluación de Configuration Manager. Para más información, consulte el [kit de laboratorio de administración e implementación de Windows y Office](https://docs.microsoft.com/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab). 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> Componentes principales  
 Para configurar el entorno para Configuration Manager, es necesario que algunos componentes principales admitan la instalación de Configuration Manager.    

-   **El entorno de laboratorio usa Windows Server 2012 R2**, donde se instalará Configuration Manager.  

     Puede descargar una versión de evaluación de Windows Server 2012 R2 desde el [centro de evaluación](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     Considere la posibilidad de modificar o deshabilitar la configuración de seguridad mejorada de Internet Explorer para facilitar el acceso a algunas de las descargas a las que se hace referencia a lo largo de estos ejercicios. Para obtener más información, consulte [Internet Explorer: configuración de seguridad mejorada](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10)).  

-   **El entorno del laboratorio utiliza SQL Server 2012 SP2** para la base de datos.  

     Puede descargar una versión de evaluación de SQL Server 2012 desde el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=43340).  

     SQL Server tiene [versiones compatibles de SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) que deben cumplirse para su uso con Configuration Manager.  

    -   Configuration Manager requiere una versión de 64 bits de SQL Server para hospedar la base de datos del sitio.  

    -   **SQL_Latin1_General_CP1_CI_AS** como la clase de **intercalación SQL** .  

    -   **La autenticación de Windows**es necesaria, [en lugar de la autenticación de SQL](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode?view=sql-server-ver15)es necesaria.  

    -   Se requiere una **instancia de SQL Server** dedicada.  

    -   No limite la **memoria direccionable del sistema** para SQL Server.  

    -   Configure la **cuenta de servicio SQL Server** para que se ejecute con una cuenta de usuario de dominio con derechos reducidos.  

    -   Debe instalar **SQL Server Reporting Services**.  

    -   **Las comunicaciones entre sitios** usan SQL Server Service Broker en el puerto predeterminado TCP 4022.  

    -   **Las comunicaciones dentro de los sitios** entre el motor de base de datos de SQL Server y los roles de sistema de sitio de Configuration Manager seleccionados usan el puerto predeterminado TCP 1433.  

-   **El controlador de dominio usa Windows Server 2008 R2** con Active Directory Domain Services instalado. El controlador de dominio también funciona como el host de los servidores DHCP y DNS para usar con un nombre de dominio completo.  

     Para obtener más información, vea la [información general de Active Directory Domain Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831484(v=ws.11)).  

-   **Hyper-V se usa con unas pocas máquinas virtuales** para comprobar que los pasos de administración realizados en estos ejercicios funcionan según lo esperado. Se recomienda un mínimo de tres máquinas virtuales, con Windows 10 instalado.  

     Para obtener más información, consulte la [información general sobre de Hyper-V](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).  

-   **Los permisos de administrador** serán necesarios para todos estos componentes.  

    -   Configuration Manager requiere un administrador con permisos locales dentro del entorno de Windows Server  

    -   Active Directory requiere un administrador con permisos para modificar el esquema  

    -   Las máquinas virtuales requieren permisos locales en las propias máquinas  

Aunque no es necesario en este laboratorio, puede consultar [Configuraciones admitidas para Configuration Manager](../../core/plan-design/configs/supported-configurations.md) para más información sobre los requisitos para implementar Configuration Manager. Consulte la documentación de las versiones de software que no se mencionan aquí.  

Después de instalar todos estos componentes, existen pasos adicionales que debe realizar para configurar el entorno de Windows para Configuration Manager:  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> Preparar el contenido de Active Directory para el laboratorio  
 Para este laboratorio, creará un grupo de seguridad y después le agregará un usuario de dominio.  

-   Grupo de seguridad: **evaluación**  

    -   Ámbito del grupo: **universal**  

    -   Tipo de grupo: **Seguridad**  

-   Usuario del dominio: **ConfigUser**  

     En circunstancias normales, no se concedería acceso universal a todos los usuarios dentro del entorno. Con este usuario se hace así para optimizar la puesta en línea del laboratorio.  

Los pasos siguientes necesarios para habilitar que los clientes de Configuration Manager consulten Active Directory Domain Services para localizar recursos del sitio se detallan en los procedimientos siguientes.  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> Crear el contenedor System Management  
 Configuration Manager no creará de forma automática el contenedor System Management necesario en Active Directory Domain Services cuando se extiende el esquema. Por lo tanto, lo creará para el laboratorio. Para este paso será necesario que [instale el Editor ADSI](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc773354(v=ws.10)).

 Asegúrese de que ha iniciado sesión con una cuenta que tenga el permiso **Crear todos los objetos secundarios** en el contenedor **System** de los Servicios de dominio de Active Directory.  

#### <a name="to-create-the-system-management-container"></a>Cómo crear el contenedor System Management:  

1.  Ejecute el **Editor ADSI**y conéctese al dominio en que reside el servidor de sitio.  

2.  Expanda **Dominio&lt;nombre de dominio completo del equipo\>** , expanda **<nombre distintivo\>** , haga clic con el botón derecho en **CN=System**, haga clic en **Nuevo** y después haga clic en **Objeto**.  

3.  En el cuadro de diálogo **Crear objeto** , seleccione **Contenedor**y, a continuación, haga clic en **Siguiente**.  

4.  En el cuadro **Valor** , escriba **System Management**y después haga clic en **Siguiente**.  

5.  Haga clic en **Finalizar** para completar el procedimiento.  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> Establecer permisos de seguridad para el contenedor System Management  
 Conceda a la cuenta de equipo del servidor de sitio los permisos necesarios para publicar información del sitio en el contenedor. También utilizará el Editor ADSI para esta tarea.  

> [!IMPORTANT]  
>  Confirme que está conectado al dominio del servidor de sitio antes de comenzar el procedimiento siguiente.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Cómo establecer permisos de seguridad para el contenedor System Management:  

1.  En el panel de consola, expanda el **dominio del servidor de sitio**, expanda **DC=&lt;nombre distintivo del servidor\>** y luego expanda **CN=System**. Haga clic con el botón secundario en **CN=System Management**y, a continuación, haga clic en **Propiedades**.  

2.  En el cuadro de diálogo **Propiedades de CN=System Management** , haga clic en la pestaña **Seguridad** y luego haga clic en **Agregar** para agregar la cuenta de equipo del servidor de sitio. Conceda a la cuenta permisos de **Control total** .  

3.  Haga clic en **Opciones avanzadas**, seleccione la cuenta de equipo del servidor de sitio y después haga clic en **Editar**.  

4.  En la lista **Aplicar en** , seleccione **Este objeto y todos los descendientes**.  

5.  Haga clic en **Aceptar** para cerrar la consola del **Editor ADSI** y completar el procedimiento.  

     Para obtener más información, consulte [Extender el esquema de Active Directory para Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> Extender el esquema de Active Directory mediante extadsch.exe  
 Extenderá el esquema de Active Directory para este laboratorio, ya que esto le permite usar todas las características y funcionalidades de Configuration Manager con la menor cantidad de trabajo administrativo. La extensión del esquema de Active Directory es una configuración que abarca todo el bosque y solo puede realizarse una vez por bosque. La extensión del esquema modifica de forma permanente el conjunto de clases y atributos de la configuración base de Active Directory. Esta acción es irreversible. La extensión del esquema permite que Configuration Manager obtenga acceso a componentes que permitirán que funcione de la forma más eficaz en el entorno del laboratorio.  

> [!IMPORTANT]  
>  Asegúrese de que inició sesión en el controlador de dominio del maestro del esquema con una cuenta que pertenezca al grupo de seguridad **Administradores de esquema** . Se producirá un error si se intentan utilizar credenciales alternativas.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Cómo extender el esquema de Active Directory mediante extadsch.exe:  

1.  Cree una copia de seguridad del estado del sistema del controlador de dominio maestro del esquema. Para más información sobre la copia de seguridad controlador del dominio del maestro, revise [Copias de seguridad de Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770757(v=ws.11))  

2.  Vaya a **\SMSSETUP\BIN\X64** en los medios de instalación.  

3.  Ejecute **extadsch.exe**.  

4.  Compruebe que la extensión del esquema se realizó correctamente revisando el archivo **extadsch.log** ubicado en la carpeta raíz de la unidad del sistema.  

     Para obtener más información, consulte [Extender el esquema de Active Directory para Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> Otras tareas necesarias  
 También debe completar las tareas siguientes antes de la instalación.  

 **Crear una carpeta para almacenar todas las descargas**  

 Habrá varias descargas necesarias para los componentes de los medios de instalación a lo largo de este ejercicio. Antes de comenzar los procedimientos de instalación, determine una ubicación que no requiera mover estos archivos hasta que quiera desactivar el laboratorio. Se recomienda una sola carpeta con subcarpetas independientes para almacenar estas descargas.  

 **Instale .NET y active Windows Communication Foundation**  

 Necesitará instalar dos versiones de .NET Framework: primero .NET 3.5.1 y después .NET 4.5.2+. También deberá activar Windows Communication Foundation (WCF). WCF está diseñado para ofrecer un enfoque administrable para la computación distribuida, una amplia interoperabilidad y una compatibilidad directa para la orientación al servicio, a la vez que simplifica el desarrollo de aplicaciones conectadas a través de un modelo de programación orientada a servicios. Para obtener más información, vea [Novedades de Windows Communication Foundation](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms731082(v=vs.90)).

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>Cómo instalar .NET y activar Windows Communication Foundation:  

1.  Abra **Server Manager**y después vaya a **Administrar**. Haga clic en **Agregar Roles y características** para abrir el **Asistente para agregar roles y características.**  

2.  Revise la información proporcionada en el panel **Antes de comenzar** y luego haga clic en **Siguiente**.  

3.  Seleccione **Instalación basada en características o roles**y luego haga clic en **Siguiente**.  

4.  Seleccione el servidor del **Grupo de servidores**y después haga clic en **Siguiente**.  

5.  Revise el panel **Roles de servidor** y luego haga clic en **Siguiente**.  

6.  Agregue las **características** siguientes seleccionándolas en la lista:  

    -   **Características de .NET Framework 3.5**  

        -   **Características de .NET Framework 3.5 (incluye .NET 2.0 y 3.0)**  

    -   **Características de .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4,5**  

        -   **Servicios WCF**  

            -   **Activación HTTP**  

            -   **Uso compartido de puertos TCP**  

7.  Revise las pantallas **Rol de servidor web (IIS)** y **Servicios de rol** y luego haga clic en **Siguiente**.  

8.  Revise la pantalla **Confirmación** y después haga clic en **Siguiente**.  

9. Haga clic en **Instalar** y compruebe que la instalación se completó correctamente en el panel **Notificaciones** del **Administrador de servidores**.  

10. Cuando se complete la instalación base de. NET, vaya al [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=42643) para obtener el instalador web de .NET Framework 4.5.2. Haga clic en el botón **Descargar** y después en **Ejecutar** para iniciar el programa de instalación. Detectará e instalará automáticamente los componentes necesarios en el idioma seleccionado.  

**Habilitar BITS, IIS y RDC**  

El [Servicio de transferencia inteligente en segundo plano (BITS)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282296(v=ws.11)) se utiliza para las aplicaciones que necesitan transferir archivos de forma asincrónica entre un cliente y un servidor. Mediante la medición del flujo de transferencias en primer plano y en segundo plano, BITS conserva la capacidad de respuesta de las demás aplicaciones de red. También reanudará automáticamente las transferencias de archivos si se interrumpe una sesión de transferencia.  

Instalará BITS para este laboratorio, ya que el servidor de sitio también se usará como un punto de administración.  

Internet Information Services (IIS) es un servidor web flexible y escalable que puede utilizarse para hospedar cualquier cosa en la web. Configuration Manager lo usa para distintos roles de sistema de sitio. Para más información sobre IIS, vea [Sitios web para servidores de sistema de sitio](../../core/plan-design/network/websites-for-site-system-servers.md).  

[Compresión diferencial remota (RDC)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754372(v=ws.11)) es un conjunto de API que las aplicaciones pueden utilizar para determinar si se han realizado cambios en un conjunto de archivos. RDC permite que la aplicación solo replique las partes modificadas de un archivo, manteniendo el tráfico de red al mínimo.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>Cómo habilitar los roles de servidor de sitio de BITS, IIS y RDC:  

1.  En el servidor de sitio, abra **Server Manager**. Vaya a **Administrar**. Haga clic en **Agregar Roles y características** para abrir el **Asistente para agregar roles y características**.  

2.  Revise la información proporcionada en el panel **Antes de comenzar** y luego haga clic en **Siguiente**.  

3.  Seleccione **Instalación basada en características o roles**y luego haga clic en **Siguiente**.  

4.  Seleccione el servidor del **Grupo de servidores**y después haga clic en **Siguiente**.  

5.  Agregue los **roles de servidor** siguientes seleccionándolos en la lista:  

    -   **Servidor web (IIS)**  

        -   **Características HTTP comunes**  

            -   **Documento predeterminado**  

            -   **Examen de directorios**  

            -   **Errores HTTP**  

            -   **Contenido estático**  

            -   **Redirección HTTP**  

        -   **Estado y diagnóstico**  

            -   **Registro HTTP**  

            -   **Herramientas de registro**  

            -   **Monitor de solicitudes**  

            -   **Seguimiento**  

    -   **Rendimiento**  

        -   **Compresión de contenido estático**  

        -   **Compresión de contenido dinámico**  

    -   **Security**  

        -   **Filtrado de solicitudes**  

        -   **Autenticación básica**  

        -   **Autenticación de asignaciones de certificados de clientes**  

        -   **Restricciones de IP y dominio**  

        -   **Autorización de URL**  

        -   **Autenticación de Windows**  

    -   **Desarrollo de aplicaciones**  

        -   **Extensibilidad de .NET 3.5**  

        -   **Extensibilidad de .NET 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4,5**  

        -   **Extensiones ISAPI**  

        -   **Filtros ISAPI**  

        -   **Inclusión del lado servidor**  

    -   **Servidor FTP**  

        -   **Servicio FTP**  

    -   **Herramientas de administración**  

        -   **Consola de administración de IIS**  

        -   **Compatibilidad con la administración de IIS 6**  

            -   **Compatibilidad con la metabase de IIS 6**  

            -   **Consola de administración de IIS 6**  

            -   **Herramientas de scripting de IIS 6**  

            -   **Compatibilidad con WMI de IIS 6**  

        -   **Herramientas y scripts de administración de IIS 6**  

        -   **Management Service**  

6.  Agregue las **características** siguientes seleccionándolas en la lista:  

    -   **Servicio de transferencia inteligente en segundo plano (BITS)**  

          -   **Extensión de servidor IIS**  

    -   **Herramientas de administración remota del servidor**  

          -   **Herramientas de administración de características**  

          -   **Herramientas de extensiones de servidor BITS**  

7.  Haga clic en **Instalar** y compruebe que la instalación se completó correctamente en el panel **Notificaciones** del **Administrador de servidores**.  

De forma predeterminada, IIS bloquea el acceso a varios tipos de ubicaciones y extensiones de archivos mediante comunicación HTTP o HTTPS. Para habilitar que estos archivos se distribuyan a los sistemas cliente, debe configurar el filtrado de solicitudes de IIS en el punto de distribución. Para obtener más información, consulte [Filtrado de solicitudes IIS para puntos de distribución](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Cómo configurar el filtrado de IIS en puntos de distribución:  

1.  Abra **IIS Manager** y seleccione el nombre del servidor en la barra lateral. Esto le llevará a la pantalla **Inicio** .  

2.  Compruebe que la opción **Vista características** está seleccionada en la parte inferior de la pantalla **Inicio** . Vaya a **IIS** y abra **Filtrado de solicitudes**.  

3.  En el panel **Acciones** , haga clic en **Permitir extensión de nombre de archivo...**  

4.  Escriba **.msi** en el cuadro de diálogo y haga clic en **Aceptar**.  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Instalación de Configuration Manager  
Creará un [Determinar cuándo utilizar un sitio primario](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) para administrar directamente los clientes. Esto permitirá que el entorno de laboratorio admita la administración de [Escala de sistema de sitio](../plan-design/configs/size-and-scale-numbers.md) de posibles dispositivos.  
Durante este proceso, también se instalará la consola de Configuration Manager, que se usará para administrar los dispositivos de evaluación a partir de ahora.  

Antes de comenzar la instalación, inicie el [Comprobador de requisitos previos](../servers/deploy/install/prerequisite-checker.md) en el servidor con Windows Server 2012 para confirmar que todas las configuraciones se han habilitado correctamente.  

#### <a name="to-download-and-install-configuration-manager"></a>Cómo descargar e instalar Configuration Manager:  

1.  Vaya a la página [Evaluaciones de System Center](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) para descargar la versión de evaluación más reciente de Configuration Manager.  

2.  Descomprima el medio de descarga en la ubicación predefinida.  

3.  Siga el procedimiento de instalación que encontrará en [Instalar un sitio con el Asistente para instalación de Configuration Manager](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md). En ese procedimiento, escribirá lo siguiente:  

    |Paso en el procedimiento de instalación de sitio|Selección|  
    |-----------------------------------------|---------------|  
    |Paso 4: la página **Clave de producto**|Seleccione **Evaluación**.|  
    |Paso 7:  **descargas de requisitos previos**|Seleccione **Descargar los archivos requeridos** y especifique la ubicación predefinida.|  
    |Paso 10: **configuración de sitio e instalación**|-   **Código de sitio:LAB**<br />-   **Nombre de sitio:Evaluation**<br />-   **Carpeta de instalación:** especifique la ubicación predefinida.|  
    |Paso 11: **instalación de sitio primario**|Seleccione **Instalar el sitio primario como un sitio independiente**y después haga clic en **Siguiente**.|  
    |Paso 12: **instalación de la base de datos**|-   **Nombre de SQL Server (FQDN):** escriba su FQDN aquí.<br />-   **Nombre de instancia:** déjelo en blanco, ya que usará la instancia predeterminada de SQL que instaló anteriormente.<br />-   **Puerto de Service Broker:** deje el puerto predeterminado 4022.|  
    |Paso 13: **instalación de la base de datos**|Deje esta configuración como el valor predeterminado.|  
    |Paso 14: **Proveedor de SMS**|Deje esta configuración como el valor predeterminado.|  
    |Paso 15: **configuración de la comunicación con el cliente**|Confirme que la opción **Los roles de sistema de sitio aceptan solo comunicación HTTPS de los clientes** no está seleccionada|  
    |Paso 16: **roles de sistema de sitio**|Escriba su FQDN y confirme que la selección de **Los roles de sistema de sitio aceptan solo comunicación HTTPS de los clientes** sigue desactivada.|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a> Habilitar la publicación para el sitio de Configuration Manager  
Cada sitio de Configuration Manager publica su propia información específica del sitio en el contenedor System Management dentro de su partición de dominio en el esquema de Active Directory. Los canales bidireccionales para la comunicación entre Active Directory y Configuration Manager deben estar abiertos para controlar este tráfico. También habilitará la detección de bosques para determinar varios componentes de la infraestructura de red y de Active Directory.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Para configurar los bosques de Active Directory para la publicación:  

1.  En la esquina inferior izquierda de la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración de jerarquía**y luego haga clic en **Métodos de detección**.  

3.  Seleccione **Detección de bosques de Active Directory** y haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** , seleccione **Habilitar la detección de bosques de Active Directory**. Cuando esté activada, seleccione **Crear automáticamente límites de sitio de Active Directory cuando se detecten**. Aparecerá un cuadro de diálogo que indica **¿Desea ejecutar la detección completa lo antes posible?** Haga clic en **Sí**.  

5.  En el grupo **Método de detección** de la parte superior de la pantalla, haga clic **Ejecutar detección de bosque ahora**después vaya a **Bosques de Active Directory** en la barra lateral. El bosque de Active Directory se debería mostrar en la lista de los bosques detectados.  

6.  Desplácese a la parte superior de la pantalla, a la pestaña **General** .  

7.  En el área de trabajo **Administración** , expanda **Configuración de jerarquía**y luego haga clic en **Bosques de Active Directory**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Para habilitar que un sitio de Configuration Manager publique información del sitio en el bosque de Active Directory:  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  Va a configurar un bosque nuevo que aún no se haya detectado.  

3.  En el área de trabajo **Administración** , haga clic en **Bosques de Active Directory**.  

4.  En la pestaña **Publicación** de las propiedades del sitio, seleccione el bosque conectado y después haga clic en **Aceptar** para guardar la configuración.
