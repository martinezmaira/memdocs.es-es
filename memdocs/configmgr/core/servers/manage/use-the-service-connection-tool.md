---
title: Herramienta de conexión de servicio
titleSuffix: Configuration Manager
description: Obtenga información sobre esta herramienta que le permite conectarse al servicio en la nube de Configuration Manager para cargar manualmente la información de uso.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e535653e0f31e186a6bdbde8da77750f2afdfdb0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690303"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Uso de la herramienta de conexión de servicio con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la **herramienta de conexión de servicio** cuando el punto de conexión de servicio esté en modo sin conexión o cuando los servidores de sistema de sitio de Configuration Manager no estén conectados a Internet. La herramienta puede ayudarle a mantener actualizado el sitio con las últimas actualizaciones de Configuration Manager.  

Cuando se ejecuta, la herramienta se conecta manualmente al servicio en la nube de Configuration Manager para cargar información de uso de la jerarquía y descargar actualizaciones. La carga de los datos de uso es necesaria para habilitar el servicio en la nube para proporcionar las actualizaciones correctas para su implementación.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Requisitos previos para usar la herramienta de conexión de servicio
A continuación se indican los requisitos previos y los problemas conocidos.

**Requisitos previos:**

- Tener instalado un punto de conexión de servicio, que estará establecido en **Sin conexión, conexión a petición**.  

- La herramienta se debe ejecutar desde un símbolo del sistema.  

- Cada equipo en el que se ejecuta la herramienta (el equipo de punto de conexión de servicio y el equipo que está conectado a Internet) debe ser un sistema de x64 bits y tener instalado lo siguiente:  

  - Los archivos de x86 y x64 de **Visual C++ Redistributable** .   De forma predeterminada, Configuration Manager instala la versión x64 en el equipo que hospeda el punto de conexión de servicio.  

    Para descargar una copia de los archivos de Visual C++, visite [Paquetes redistribuibles de Visual C++ para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) en el Centro de descarga de Microsoft.  

  - .NET Framework 4.5.2 o una versión posterior.  

- La cuenta que utilice para ejecutar la herramienta debe tener:
  - Permisos de**administrador local** en el equipo que hospeda el punto de conexión de servicio (donde se ejecuta la herramienta).
  - Permisos de**Lectura** para la base de datos del sitio.  



- Necesitará una unidad USB con suficiente espacio libre para almacenar los archivos y las actualizaciones, u otro método para transferir archivos entre el equipo de punto de conexión de servicio y el equipo que tiene acceso a Internet. (En este escenario se supone que su sitio y los equipos administrados no tienen una conexión directa a Internet).  



## <a name="use-the-service-connection-tool"></a>Uso de la herramienta de conexión de servicio  

 Encontrará la herramienta de conexión de servicio (**serviceconnectiontool.exe**) en los medios de instalación de Configuration Manager, en la carpeta **%path%\smssetup\tools\ServiceConnectionTool**. Use siempre la herramienta de conexión de servicio que coincida con la versión de Configuration Manager que use.


 En este procedimiento, los ejemplos de línea de comandos usan los siguientes nombres de archivo y ubicaciones de carpeta (no es necesario usar estas rutas de acceso y nombres de archivo, puede usar otros alternativos en su lugar que coincidan con su entorno y preferencias):  

- La ruta de acceso a un Stick USB donde se almacenan los datos para la transferencia entre servidores:  **D:\USB\\**  

- El nombre del archivo .cab que contiene los datos exportados desde su sitio: **UsageData.cab**  

- El nombre de la carpeta vacía donde se almacenarán las actualizaciones descargadas de Configuration Manager para la transferencia entre servidores: **UpdatePacks**  

En el equipo que hospeda el punto de conexión de servicio:  

- Abra un símbolo del sistema con privilegios administrativos y, a continuación, cambie los directorios a la ubicación que contiene **serviceconnectiontool.exe**.  

  De forma predeterminada, encontrará esta herramienta en los medios de instalación de Configuration Manager, en la carpeta **%path%\smssetup\tools\ServiceConnectionTool**. Todos los archivos en esta carpeta deben estar en la misma carpeta para que funcione la herramienta de conexión de servicio.  

Al ejecutar el comando siguiente, la herramienta prepara un archivo .cab que contiene la información de uso y la copia a una ubicación que especifique. Los datos del archivo .cab se basan en el nivel de datos de uso de diagnóstico que recopilará el sitio de acuerdo con su configuración. (Vea [Diagnósticos y datos de uso para Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)).  Ejecute el siguiente comando para crear el archivo .cab:  

- **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

También necesitará copiar la carpeta ServiceConnectionTool con todo su contenido en la unidad USB o, de lo contrario, habilitarla en el equipo que utilizará para los pasos 3 y 4.  

### <a name="overview"></a>Introducción
#### <a name="there-are-three-primary-steps-to-using-the-service-connection-tool"></a>Hay tres pasos principales para usar la herramienta de conexión de servicio  

1.  **Preparar:**  este paso se ejecuta en el equipo que hospeda el punto de conexión de servicio. Cuando la herramienta se ejecuta, coloca los datos de uso en un archivo .cab y lo almacena en una unidad USB (o la ubicación alternativa de transferencia que especifique).  

2.  **Conectar**: para este paso, debe ejecutar la herramienta en un equipo remoto que se conecte a Internet para poder cargar datos de uso y descargar actualizaciones.  

3.  **Importar**: este paso se ejecuta en el equipo que hospeda el punto de conexión de servicio. Cuando se ejecuta, la herramienta importa las actualizaciones descargadas y las agrega al sitio para que pueda verlas e instalarlas desde la consola de Configuration Manager.  

A partir de la versión 1606, al conectarse a Microsoft puede cargar varios archivos .cab a la vez (cada uno desde una jerarquía distinta) y especificar un servidor proxy y un usuario para el servidor proxy.   

#### <a name="to-upload-multiple-cab-files"></a>Para cargar varios archivos .cab
- Coloque cada archivo .cab que exporte de jerarquías independientes en la misma carpeta. El nombre de cada archivo debe ser único y puede cambiarlo manualmente si lo precisa.
- Después, al ejecutar el comando para cargar datos a Microsoft, especifique la carpeta que contiene los archivos .cab. (Antes de la actualización 1606, solo puede cargar datos desde una única jerarquía a la vez y la herramienta requerirá que especifique el nombre del archivo .cab en la carpeta).
- Más adelante, cuando ejecute la tarea de importación en el punto de conexión de servicio de una jerarquía, la herramienta importa automáticamente solo los datos de esa jerarquía.  

#### <a name="to-specify-a-proxy-server"></a>Para especificar un servidor proxy
Puede utilizar los siguientes parámetros opcionales para especificar un servidor proxy (para más información acerca del uso de estos parámetros, consulte la sección de parámetros de línea de comandos de este tema):
- **-proxyserveruri [FQDN_of_proxy_server]**  Utilice este parámetro para especificar el servidor proxy para esta conexión.
- **-proxyusername [nombreDeUsuario]**  Utilice este parámetro cuando deba especificar un usuario para el servidor proxy.

#### <a name="specify-the-type-of-updates-to-download"></a>Especificar el tipo de actualizaciones que quiere descargar
A partir de la versión 1706, se ha modificado el comportamiento de descarga de herramientas predeterminado, así como las opciones de compatibilidad con herramientas para controlar los archivos descargados.
- De forma predeterminada, la herramienta descarga únicamente la última actualización disponible que sea válida para la versión de su sitio. No descarga ninguna revisión.

Para modificar este comportamiento, use uno de los parámetros siguientes para cambiar qué archivos se descargarán. 

> [!NOTE]
> La versión de su sitio se determina a partir de los datos del archivo .cab que se carga al ejecutar la herramienta.
>
> Puede comprobar la versión buscando el archivo *SiteVersion*.txt dentro del archivo. cab.

- **-downloadall**: esta opción descarga todo, incluidas las actualizaciones y las revisiones, independientemente de la versión de su sitio.
- **-downloadhotfix**: esta opción descarga todas las revisiones independientemente de la versión de su sitio.
- **-downloadsiteversion**: esta opción descarga todas las actualizaciones y revisiones con una versión posterior a la de su sitio.

Ejemplo de una línea de comandos que usa *-downloadsiteversion*:
- **serviceconnectiontool.exe -connect  *-downloadsiteversion* -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**




### <a name="to-use-the-service-connection-tool"></a>Para usar la herramienta de conexión de servicio  

1. En el equipo que hospeda el punto de conexión de servicio:  

   - Abra un símbolo del sistema con privilegios administrativos y, a continuación, cambie los directorios a la ubicación que contiene **serviceconnectiontool.exe**.   

2. Ejecute el comando siguiente para que la herramienta prepare un archivo .cab que contiene la información de uso y la copia a una ubicación que especifique:  

   - **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

   Si va a cargar los archivos .cab de más de una jerarquía al mismo tiempo, cada archivo .cab de la carpeta debe tener un nombre único. Puede cambiar manualmente el nombre de los archivos que agregue a la carpeta.

   Si desea ver la información de uso que se recopila para cargarse en el servicio en la nube de Configuration Manager, ejecute el siguiente comando para exportar los mismos datos como un archivo .csv que puede ver con una aplicación como Excel:  

   - **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3. Una vez completado el paso de preparación, mueva la unidad USB (o transfiera los datos exportados mediante otro método) a un equipo que tenga acceso a Internet.  

4. En el equipo con acceso a Internet, abra un símbolo del sistema con privilegios administrativos y, a continuación, cambie los directorios a la ubicación que contiene una copia de la herramienta  **serviceconnectiontool.exe** y los archivos adicionales de esa carpeta.  

5. Ejecute el siguiente comando para iniciar la carga de información de uso y la descarga de actualizaciones de Configuration Manager:  

   - **serviceconnectiontool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**

   Para obtener más ejemplos de esta línea de comandos, consulte la sección [Opciones de línea de comandos](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) más adelante en este tema.

   > [!NOTE]  
   >  Cuando se ejecuta la línea de comandos para conectar con el servicio en la nube de Configuration Manager, podría producirse un error similar al siguiente:  
   >   
   > - Excepción no controlada: System.UnauthorizedAccessException:  
   >   
   >      El acceso a la ruta de acceso 'C:\  
   >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' se ha denegado.  
   >   
   > Este error puede omitirse sin problemas, puede cerrar la ventana de error y continuar.  

6. Cuando se complete la descarga de actualizaciones para Configuration Manager, mueva la unidad USB (o transfiera los datos exportados mediante otro método) al equipo que hospeda el punto de conexión de servicio.  

7. En el equipo que hospeda el punto de conexión de servicio, abra un símbolo del sistema con privilegios administrativos, cambie los directorios a la ubicación que contiene **serviceconnectiontool.exe**y, a continuación, ejecute el siguiente comando:  

   - **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8. Una vez finalizada la importación, puede cerrar el símbolo del sistema. (Solo se importan las actualizaciones para la jerarquía aplicable).  

9. Abra la consola de Configuration Manager y vaya a **Administración** > **Actualizaciones y mantenimiento**. Ahora están disponibles para instalar las actualizaciones que se han importado. (Antes de la versión 1702, la opción Actualizaciones y mantenimiento se encontraba en **Administración** > **Cloud Services**).

   Para más información sobre cómo instalar actualizaciones, vea [Instalación de actualizaciones en la consola de Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

## <a name="log-files"></a><a name="bkmk_cmd"></a> Archivos de registro

**ServiceConnectionTool.log**

Cada vez que se ejecute la herramienta de conexión de servicio, se generará un archivo de registro en la misma ubicación que la herramienta denominada **ServiceConnectionTool.log**.  Este archivo de registro proporcionará detalles simples sobre la ejecución de la herramienta en función de qué comandos se usan.  Un archivo de registro existente se sustituirá cada vez que ejecute la herramienta.

**ConfigMgrSetup.log**

Al utilizar la herramienta para conectarse y descargar actualizaciones, se generará un archivo de registro en la raíz de la unidad del sistema denominado **ConfigMgrSetup.log**.  Este archivo de registro le proporcionará información más detallada, como qué archivos se descargan y extraen, y si las comprobaciones del hash se realizan correctamente.

## <a name="command-line-options"></a><a name="bkmk_cmd"></a> opciones de línea de comandos  
Para ver la información de ayuda para la herramienta de punto de conexión de servicio, abra el símbolo del sistema para la carpeta que contiene la herramienta y ejecute el comando:  **serviceconnectiontool.exe**.  


|Opciones de línea de comandos|Detalles|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [unidad:][ruta][nombrearchivo.cab]**|Este comando almacena los datos de uso actuales en un archivo .cab.<br /><br /> Ejecute este comando como **administrador local** en el servidor que hospeda el punto de conexión de servicio.<br /><br /> Ejemplo:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [unidad:][rutaAcceso] -updatepackdest [unidad:][rutaAcceso] -proxyserveruri [nombreCompletoServidorProxy] -proxyusername [nombreUsuario]** <br /> <br /> Si utiliza una versión de Configuration Manager anterior a 1606, debe especificar el nombre del archivo .cab y no podrá utilizar las opciones de un servidor proxy.  Los parámetros de comando admitidos son los siguientes: <br /> **connect -usagedatasrc [unidad:][rutaAcceso][nombreDeArchivo] -updatepackdest [unidad:][rutaAcceso]** |Este comando se conecta al servicio en la nube de Configuration Manager para cargar los archivos .cab de datos de uso desde la ubicación especificada y descargar los paquetes de actualización disponibles y el contenido de la consola. Las opciones para los servidores proxy son opcionales.<br /><br /> Ejecute este comando como **administrador local** en un equipo que pueda conectarse a Internet.<br /><br /> Ejemplo de la conexión sin un servidor proxy: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Ejemplo para la conexión cuando se utiliza un servidor proxy: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Si utiliza una versión anterior a 1606, debe especificar un nombre de archivo para el archivo .cab y no se puede especificar un servidor proxy. Use la siguiente línea de comandos de ejemplo: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [unidad:][ruta]**|Este comando importa los paquetes de actualización y el contenido de la consola que ha descargado anteriormente a la consola de Configuration Manager.<br /><br /> Ejecute este comando como **administrador local** en el servidor que hospeda el punto de conexión de servicio.<br /><br /> Ejemplo:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [unidad:][ruta][nombrearchivo.csv]**|Este comando exporta los datos de uso a un archivo .csv, que puede ver.<br /><br /> Ejecute este comando como **administrador local** en el servidor que hospeda el punto de conexión de servicio.<br /><br /> Ejemplo: **-export -dest D:\USB\usagedata.csv**|  
