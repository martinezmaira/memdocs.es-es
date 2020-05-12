---
title: Instalador de revisiones
titleSuffix: Configuration Manager
description: Averigüe cuándo y cómo instalar actualizaciones mediante el instalador de revisiones para Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8eed671b723091f2a43350f42ca82d90e0d9da3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906131"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-configuration-manager"></a>Uso del instalador de revisiones para instalar actualizaciones de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Algunas actualizaciones para Configuration Manager no están disponibles desde el servicio en la nube de Microsoft y solo se obtienen de un origen externo. Un ejemplo es la versión limitada de una revisión para resolver un problema específico.   
Si necesita instalar una actualización (o revisión) procedente de Microsoft y el nombre de archivo de la actualización termina con una extensión **.exe** (en lugar de **update.exe**), debe usar el instalador de revisiones que se incluye en la descarga de la revisión para instalar la actualización directamente en el servidor de sitio de Configuration Manager.  

Si la revisión tiene la extensión de archivo **.update.exe**, vea [Uso de la herramienta de registro de actualizaciones para importar revisiones a Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
> En este tema se proporcionan instrucciones generales sobre cómo instalar las revisiones que actualizan Configuration Manager. Para obtener información más detallada acerca de una actualización específica, consulte su correspondiente artículo de Knowledge Base (KB) en Soporte técnico de Microsoft.  

##  <a name="overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a> Información general sobre revisiones de Configuration Manager  
Las revisiones para Configuration Manager son similares a las de otros productos de Microsoft, como SQL Server, contienen una revisión individual o un paquete (un paquete acumulativo de revisiones) y se describen en un artículo de Microsoft Knowledge Base.  

Las actualizaciones individuales contienen una única actualización diseñada para una versión específica de Configuration Manager.  
Las agrupaciones de actualizaciones contienen varias actualizaciones diseñadas para una versión específica de Configuration Manager.  
Si una actualización es una agrupación, no puede instalar actualizaciones individuales de dicha agrupación.  

Si tiene pensado crear implementaciones para instalar actualizaciones en otros equipos, debe instalar la agrupación de actualizaciones en un servidor de sitio de administración central o en un servidor de sitio principal.  

Al ejecutar la agrupación de actualizaciones, ocurre lo siguiente:  

- Se extraen de la agrupación de actualizaciones los archivos de actualización de cada componente aplicable.  

- Inicia un asistente que le guía a través del proceso de configuración de las actualizaciones y las opciones de implementación para las actualizaciones.  

- Cuando se completa el asistente, las actualizaciones de la agrupación que se aplican al servidor de sitio se instalan en el servidor de sitio.  

El asistente también crea implementaciones que puede utilizar para instalar las actualizaciones en otros equipos. Puede implementar las actualizaciones en otros equipos mediante un método de implementación admitido, como un paquete de implementación de software o Microsoft System Center Updates Publisher 2011.  

Cuando se ejecuta el asistente, este crea un archivo **.cab** en el servidor de sitio para usarlo con Updates Publisher 2011. Si lo desea, puede configurar el asistente para crear uno o varios paquetes para la implementación de software. Puede usar estas implementaciones para instalar actualizaciones de componentes, como clientes o la consola de Configuration Manager. También puede instalar las actualizaciones manualmente en equipos que no ejecuten el cliente de Configuration Manager.  

Se pueden actualizar los tres grupos siguientes de Configuration Manager:  

- Roles de servidor de Configuration Manager, que incluyen:  

  - Sitio de administración central  

  - Sitio primario  

  - Sitio secundario  

  - Proveedor de SMS remoto  

- Consola de Configuration Manager  

- Cliente de Configuration Manager  

> [!NOTE]  
> Las **actualizaciones para los roles de sistema de sitio** (incluidas las actualizaciones para los puntos de distribución basados en la nube y la base de datos del sitio) las instala el Administrador de componentes de sitio como parte de la actualización de los servicios y servidores de sitio.  
>   
> Sin embargo, de los puntos de distribución de extracción de actualizaciones se ocupa el administrador de distribución y no el Administrador de componentes de sitio.  

Cada agrupación de actualizaciones de Configuration Manager es un archivo .exe autoextraíble (SFX) que contiene los archivos necesarios para instalar la actualización de los componentes aplicables de Configuration Manager. Normalmente, el archivo SFX puede contener los siguientes archivos:  

|Archivo|Detalles|  
|----------|-------------|  
|&lt;Versión del producto\>-QFE-KB&lt;identificador del artículo de KB\>-&lt;plataforma\>-&lt;idioma\>.exe|Este es el archivo de actualización. Updatesetup.exe administra la línea de comandos de este archivo.<br /><br /> Por ejemplo:<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|Este contenedor .msi administra la instalación de la agrupación de actualizaciones.<br /><br /> Al ejecutar la actualización, Updatesetup.exe detecta el idioma de visualización del equipo donde se ejecuta. De forma predeterminada, la interfaz de usuario para la actualización está en inglés. Sin embargo, cuando se admite el idioma de visualización, la interfaz de usuario se muestra en el idioma local del equipo.|  
|License_&lt;idioma\>.rtf|Cuando es aplicable, cada actualización contiene uno o varios archivos de licencia para los idiomas compatibles.|  
|&lt;ProductoYTipoDeActualización>-&lt;versión del producto\>-&lt;identificador del artículo de KB\>-&lt;plataforma\>.msp|Cuando la actualización se aplica a la consola o los clientes de Configuration Manager, la agrupación de actualizaciones contiene archivos de revisión de Windows Installer (.msp) independientes.<br /><br /> Por ejemplo:<br /><br /> **Actualización de la consola de Configuration Manager:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Actualización de cliente:** ConfigMgr1511-client-KB1234567-i386.msp<br />ConfigMgr1511-client-KB1234567-x64.msp|  

De manera predeterminada, la agrupación de actualizaciones registra sus acciones en un archivo .log en el servidor de sitio. El archivo de registro tiene el mismo nombre que la agrupación de actualizaciones y se crea en la carpeta **%SystemRoot%/Temp** .  

Cuando ejecuta la agrupación de actualizaciones, se extrae un archivo con el mismo nombre que la agrupación de actualizaciones en una carpeta temporal del equipo y, a continuación, se ejecuta Updatesetup.exe. Updatesetup.exe inicia el Asistente para actualización de software de Configuration Manager &lt;versión del producto\> &lt;número de KB\>.  

Si procede para el propósito de la actualización, el asistente crea una serie de carpetas en la carpeta de instalación de Configuration Manager del servidor de sitio. La estructura de las carpetas es similar a esta:   
**\\\\&lt;Nombre de servidor\>\SMS_&lt;Código de sitio\>\Revisión\\&lt;Número de KB\>\\&lt;Tipo de actualización\>\\&lt;Plataforma\>** .  

En la tabla siguiente se proporcionan detalles acerca de las carpetas en la estructura de carpetas.  

|Nombre de la carpeta|Más información|  
|-----------------|----------------------|  
|&lt;Nombre de servidor\>|Se trata del nombre del servidor de sitio donde se ejecuta la agrupación de actualizaciones.|  
|SMS_&lt;Código de sitio\>|Se trata del nombre de recurso compartido de la carpeta de instalación de Configuration Manager.|  
|&lt;Número de KB\>|Se trata del número de identificación del artículo de Knowledge Base para esta agrupación de actualizaciones.|  
|&lt;Tipo de actualización\>|Estos son los tipos de actualizaciones de Configuration Manager. El asistente crea una carpeta independiente para cada tipo de actualización incluida en la agrupación de actualizaciones. Los nombres de carpeta representan los tipos de actualización. Incluyen los siguientes:<br /><br /> **Servidor**: incluye actualizaciones de los servidores de sitio, servidores de base de datos del sitio y equipos que ejecutan el proveedor de SMS.<br /><br /> **Cliente**: incluye actualizaciones del cliente de Configuration Manager.<br /><br /> **AdminConsole**: incluye actualizaciones de la consola de Configuration Manager.<br /><br /> Además de los tipos de actualización anteriores, el asistente crea una carpeta denominada **SCUP**. Esta carpeta no representa un tipo de actualización, sino que contiene el archivo .cab para Updates Publisher.|  
|&lt;Plataforma\>|Se trata de una carpeta específica de la plataforma. Contiene archivos de actualización que son específicos de un tipo de procesador.  Estas carpetas incluyen:<br /><br />- x64<br /><br /> - I386|  

##  <a name="how-to-install-updates"></a><a name="bkmk_Install"></a> Instalación de actualizaciones  
Para poder instalar las actualizaciones, primero debe instalar la agrupación de actualizaciones en un servidor de sitio. Cuando instala una agrupación de actualizaciones, inicia un asistente de instalación para dicha actualización. Este asistente hace lo siguiente:  

- Extrae los archivos de actualización.  

- Le ayuda a configurar las implementaciones.  

- Instala las actualizaciones correspondientes en los componentes del servidor del equipo local.  

Una vez que la agrupación de actualizaciones esté instalada en un servidor de sitio, podrá actualizar otros componentes de Configuration Manager. En la tabla siguiente se describen las acciones de actualización para estos diversos componentes.  

|Componente|Instrucciones|  
|---------------|------------------|  
|Servidor de sitio|Implemente actualizaciones en un servidor de sitio remoto cuando elija no instalar la agrupación de actualizaciones directamente en ese servidor de sitio remoto.|  
|Base de datos del sitio|Para los servidores de sitio remoto, implemente actualizaciones de servidor que incluyan una actualización de la base de datos del sitio si no instala la agrupación de actualizaciones directamente en ese servidor de sitio remoto.|  
|Consola de Configuration Manager|Tras la instalación inicial de la consola de Configuration Manager, puede instalar actualizaciones de la consola de Configuration Manager en cada uno de los equipos en los que se ejecuta la consola. No puede modificar los archivos de instalación de la consola de Configuration Manager para que apliquen las actualizaciones durante la instalación inicial de la consola.|  
|Proveedor de SMS remoto|Instale actualizaciones en cada instancia del proveedor de SMS que se ejecute en un equipo que no sea el servidor de sitio donde instaló la agrupación de actualizaciones.|  
|Clientes de Configuration Manager|Tras la instalación inicial del cliente de Configuration Manager, puede instalar actualizaciones del cliente de Configuration Manager en cada uno de los equipos en los que se ejecuta el cliente.|  

> [!NOTE]  
> Las actualizaciones solo se pueden implementar en los equipos que ejecutan el cliente de Configuration Manager.  

Si vuelve a instalar un cliente, una consola de Configuration Manager o un proveedor de SMS, también debe volver a instalar las actualizaciones de esos componentes.  

Use la información de las secciones siguientes para instalar actualizaciones en cada uno de los componentes de Configuration Manager.  

###  <a name="update-servers"></a><a name="bkmk_servers"></a> Actualización de servidores  
Las actualizaciones de servidores pueden incluir actualizaciones de los **sitios**, la **site database**y los equipos que ejecutan una instancia del **proveedor de SMS**:  

####  <a name="update-a-site"></a><a name="bkmk_site"></a> Actualizar un sitio  
Para actualizar un sitio de Configuration Manager, puede instalar la agrupación de actualizaciones directamente en el servidor de sitio o implementar las actualizaciones en un servidor de sitio después de instalar la agrupación en otro sitio.  

Cuando instala una actualización en un servidor de sitio, el proceso de instalación de la actualización administra acciones adicionales que son necesarias para aplicar la actualización, como la actualización de los roles de sistema de sitio. La excepción a esto es la base de datos del sitio. La siguiente sección contiene información acerca de cómo actualizar la base de datos del sitio.  

####  <a name="update-a-site-database"></a><a name="bkmk_database"></a> Actualizar una base de datos del sitio  
Para actualizar la base de datos del sitio, el proceso de instalación ejecuta un archivo denominado **update.sql** en la base de datos del sitio. Puede configurar el proceso de actualización para actualizar automáticamente la base de datos del sitio o puede actualizar manualmente la base de datos del sitio más adelante.  

**Actualización automática de la base de datos del sitio**  

Cuando se instala la agrupación de actualizaciones en un servidor de sitio, puede elegir actualizar automáticamente la base de datos del sitio cuando se instala la actualización del servidor. Esta decisión solo se aplica al servidor de sitio cuando instala la agrupación de actualizaciones y no se aplica a las implementaciones creadas para instalar las actualizaciones en servidores de sitio remotos.  

> [!NOTE]  
> Cuando se decide actualizar automáticamente la base de datos del sitio, el proceso actualiza una base de datos sin importar si la base de datos se encuentra en el servidor de sitio o en un equipo remoto.  

> [!IMPORTANT]  
> Antes de actualizar la base de datos del sitio, cree una copia de seguridad de la misma. No puede desinstalar una actualización de la base de datos del sitio. Para más información sobre cómo crear copias de seguridad de Configuration Manager, vea [Copia de seguridad y recuperación de Configuration Manager](backup-and-recovery.md).  

**Actualización manual de la base de datos del sitio**  

Si decide no actualizar automáticamente la base de datos del sitio al instalar la agrupación de actualizaciones en el servidor de sitio, la actualización del servidor no modifica la base de datos en el servidor de sitio en que se ejecuta la agrupación de actualizaciones. Sin embargo, las implementaciones que utilizan el paquete que se creó para la implementación de software o que se instala siempre actualizan la base de datos del sitio.  

> [!WARNING]  
> Cuando la actualización incluye actualizaciones en el servidor de sitio y en la base de datos del sitio, no está operativa hasta que se completa tanto para el servidor de sitio como para la base de datos del sitio. Hasta que la actualización no se aplique a la base de datos del sitio, el sitio se encuentra en un estado no compatible.  

**Para actualizar una base de datos del sitio manualmente:**  

1.  Detenga el servicio SMS_SITE_COMPONENT_MANAGER en el servidor de sitio y, a continuación, detenga el servicio SMS_EXECUTIVE.  

2.  Cierre la consola de Configuration Manager.  

3.  Ejecute el script de actualización denominado **update.sql** en la base de datos del sitio. Para más información sobre cómo ejecutar un script para actualizar una base de datos de SQL Server, consulte la documentación de la versión de SQL Server que use para el servidor de base de datos del sitio.  

4.  Reinicie los servicios que se detuvieron en pasos anteriores.  

5.  Cuando se instala la agrupación de actualizaciones, extrae **update.sql** en la siguiente ubicación en el servidor de sitio:  **\\\\&lt;Nombre de servidor\>\SMS_&lt;Código de sitio\>\Hotfix\\&lt;Número de KB\>\update.sql**  

####  <a name="update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a> Actualizar un equipo que ejecuta el proveedor de SMS  
Después de instalar una agrupación de actualizaciones que incluye actualizaciones para el proveedor de SMS, debe implementar la actualización en cada equipo que ejecuta el proveedor de SMS. La única excepción es la instancia del proveedor de SMS que se instaló previamente en el servidor de sitio en el que se instala la agrupación de actualizaciones. La instancia local del proveedor de SMS en el servidor de sitio se actualiza cuando se instala la agrupación de actualizaciones.  

Si quita y vuelve a instalar el proveedor de SMS en un equipo, debe volver a instalar la actualización del proveedor de SMS en ese equipo.  

###  <a name="update-clients"></a><a name="BKMK_clients"></a> Actualizar clientes  
Al instalar una actualización que incluye actualizaciones para el cliente de Configuration Manager, se le ofrecerá la opción de actualizar automáticamente los clientes con la instalación de actualización, o bien actualizar manualmente los clientes en un momento posterior. Para más información sobre la actualización automática de clientes, consulte [Actualizar clientes de equipos Windows con System Center Configuration Manager](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Puede implementar las actualizaciones con Updates Publisher o con un paquete de implementación de software. También puede instalar manualmente la actualización en dicho cliente. Para más información sobre el uso de implementaciones para instalar actualizaciones, consulte la sección [Implementación de actualizaciones de Configuration Manager](#BKMK_Deploy) de este tema.  

> [!IMPORTANT]  
> Si instala actualizaciones para clientes y la agrupación de actualizaciones incluye actualizaciones de servidores, asegúrese de instalar las actualizaciones de servidor en el sitio primario al que están asignados los clientes.  

Para instalar manualmente la actualización de cliente, debe ejecutar **Msiexec.exe** y hacer referencia al archivo .msp de actualización de cliente de la plataforma correspondiente en cada cliente de Configuration Manager.  

Por ejemplo, puede utilizar la siguiente línea de comandos para realizar una actualización del cliente. Esta línea de comandos ejecuta MSIEXEC en el equipo cliente y hace referencia al archivo .msp que la agrupación de actualizaciones extrajo en el servidor de sitio: **msiexec.exe /p \\\\&lt;NombreDelServidor\>\SMS_&lt;CódigoDelSitio\>\Revisión\\&lt;Número de KB\>\Cliente\\&lt;Plataforma\>\\&lt;msp\> /L\*v &lt;archivoDeRegistro\>REINSTALLMODE=mous REINSTALL=ALL**.  

###  <a name="update-configuration-manager-consoles"></a><a name="BKMK_console"></a> Actualizar consolas de Configuration Manager  
Para actualizar una consola de Configuration Manager, debe instalar la actualización en el equipo que ejecuta la consola al finalizar la instalación de la misma.  

> [!IMPORTANT]  
> Si instala actualizaciones para la consola de Configuration Manager y la agrupación contiene actualizaciones para los servidores, no olvide instalar las actualizaciones de los servidores en el sitio que use con la consola de Configuration Manager.  

Si el equipo que está actualizando ejecuta el cliente de Configuration Manager:  

- Puede utilizar una implementación para instalar la actualización. Para más información sobre el uso de implementaciones para instalar actualizaciones, consulte la sección [Implementación de actualizaciones de Configuration Manager](#BKMK_Deploy) de este tema.  

- Si está conectado directamente en el equipo de cliente, puede ejecutar la instalación de forma interactiva.  

- Puede instalar la actualización manualmente en cada equipo. Para instalar manualmente la actualización de la consola de Configuration Manager, debe ejecutar Msiexec.exe en cada uno de los equipos en los que se ejecute la consola de Configuration Manager y hacer referencia al archivo .msp de la actualización de la consola de Configuration Manager.  

Por ejemplo, puede usar la siguiente línea de comandos para actualizar una consola de Configuration Manager. Esta línea de comandos ejecuta MSIEXEC en el equipo y hace referencia al archivo .msp que la agrupación de actualizaciones extrajo en el servidor de sitio: **msiexec.exe /p \\\\&lt;NombreDelServidor\>\SMS_&lt;CódigoDelSitio\>\Revisión\\&lt;Número de KB\>\AdminConsole\\&lt;Plataforma\>\\&lt;msp\> /L\*v &lt;archivoDeRegistro\>REINSTALLMODE=mous REINSTALL=ALL**.  

##  <a name="deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Implementación de actualizaciones de Configuration Manager  
Después de instalar la agrupación de actualizaciones en un servidor de sitio, puede usar uno de los tres métodos siguientes para implementar actualizaciones en otros equipos.  

###  <a name="use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a> Usar Updates Publisher 2011 para instalar actualizaciones  
Cuando se instala la agrupación de actualizaciones en un servidor de sitio, el Asistente para instalación crea un archivo de catálogo para Updates Publisher que puede usar para implementar las actualizaciones en los equipos correspondientes. El asistente siempre crea este catálogo, incluso cuando la opción **Use package and program to deploy this update**.  

El catálogo de Updates Publisher se llama **SCUPCatalog.cab** y se encuentra en la ubicación siguiente en el equipo donde se ejecute la agrupación de actualizaciones: **\\\\&lt;Nombre de servidor\>\SMS_&lt;Código de sitio\>\Hotfix\\&lt;Número de KB\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
> Ya que el archivo SCUPCatalog.cab se crea mediante rutas de acceso específicas del servidor de sitio en el que se instala la agrupación de actualizaciones, no se puede usar en otros servidores de sitio.  

Cuando el asistente termine, podrá importar el catálogo en Updates Publisher y usar las actualizaciones de software de Configuration Manager para implementar las actualizaciones. Para obtener más información sobre Updates Publisher, consulte [Updates Publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

Utilice el siguiente procedimiento para importar el archivo SCUPCatalog.cab en Updates Publisher y publicar las actualizaciones.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Para importar las actualizaciones a Updates Publisher 2011  

1.  Inicie la consola de Updates Publisher y haga clic en **Importar**.  

2.  En la página **Tipo de importación** del Asistente para importar catálogo de actualizaciones de software, seleccione **Especifique la ruta al catálogo que desea importar**y, a continuación, especifique el archivo SCUPCatalog.cab.  

3.  Haga clic en **Siguiente**y, a continuación, haga clic en **Siguiente** de nuevo.  

4.  En el cuadro de diálogo **Advertencia de seguridad - validación de catálogo** , haga clic en **Aceptar**. Cierre al asistente cuando finalice.  

5.  En la consola de Updates Publisher, seleccione la actualización que quiere implementar y, luego, haga clic en **Publicar**.  

6.  En la página **Opciones de publicación** del Asistente para publicar actualizaciones de software, seleccione **Todo el contenido**y, a continuación, haga clic en **Siguiente**.  

7.  Complete el asistente para publicar las actualizaciones.  

###  <a name="use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a> Usar la implementación de software para instalar actualizaciones  
Cuando instala la agrupación de actualizaciones en el servidor de sitio de un sitio primario o de un sitio de administración central, puede configurar el Asistente de instalación para crear paquetes de actualizaciones para la implementación de software. A continuación, puede implementar cada paquete en la recopilación de equipos que desea actualizar.  

Para crear un paquete de implementación de software, en la página **Configurar implementación de actualización de software** del asistente, active la casilla de cada tipo de paquete de actualización que desee actualizar. Los tipos disponibles pueden ser servidores, consolas de Configuration Manager y clientes. Se crea un paquete independiente para cada tipo de actualización que se selecciona.  

> [!NOTE]  
> El paquete para servidores contiene actualizaciones de los siguientes componentes:  
>   
> - Servidor de sitio  
> - Proveedor de SMS  
> - Base de datos del sitio  

A continuación, en la página **Configurar método de implementación de actualización de software** del asistente, seleccione la opción **Usaré la distribución de software**. Esta selección hace que el asistente cree los paquetes de implementación de software.  

Al finalizar el asistente, puede ver los paquetes creados en la consola de Configuration Manager en el nodo **Paquetes** en el área de trabajo **Biblioteca de software**. Después, puede usar el proceso estándar para implementar paquetes de software en los clientes de Configuration Manager. Cuando un paquete se ejecuta en un cliente, instala las actualizaciones en los componentes correspondientes de Configuration Manager del equipo cliente.  

Para más información sobre cómo implementar paquetes en clientes de Configuration Manager, vea [Paquetes y programas](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a> Crear recopilaciones para implementar actualizaciones en Configuration Manager  
Puede implementar determinadas actualizaciones en los clientes correspondientes. La siguiente información puede ayudarle a crear recopilaciones de dispositivos para los componentes de Configuration Manager.  

|Componentes de Configuration Manager|Instrucciones|  
|----------------------------------------|------------------|  
|Servidor de sitio de administración central|Cree una consulta de pertenencia directa y agregue el equipo del servidor de sitio de administración central.|  
|Todos los servidores de sitio primario|Cree una consulta de pertenencia directa y agregue todos los equipos de servidor de sitio primario.|  
|Todos los servidores de sitio secundario|Cree una consulta de pertenencia directa y agregue todos los equipos de servidor de sitio secundario.|  
|Todos los clientes x86|Cree una recopilación con los siguientes criterios de consulta:<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X86-based PC"**|  
|Todos los clientes x64|Cree una recopilación con los siguientes criterios de consulta:<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X64-based PC"**|  
|Todos los equipos que ejecutan la consola de Configuration Manager|Cree una consulta de pertenencia directa y agregue todos los equipos.|  
|Equipos remotos que ejecutan una instancia del proveedor de SMS|Cree una consulta de pertenencia directa y agregue todos los equipos.|  

> [!NOTE]  
> Para actualizar una base de datos del sitio, implemente la actualización en el servidor de sitio para ese sitio.  

Para más información sobre cómo crear recopilaciones, vea [Cómo crear recopilaciones](../../../core/clients/manage/collections/create-collections.md).  
