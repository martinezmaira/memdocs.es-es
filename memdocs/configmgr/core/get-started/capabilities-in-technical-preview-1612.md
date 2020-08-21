---
title: Funcionalidades de Technical Preview 1612
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1612.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9cd0df25c64c4ca1e0d2ce98de5d2915f7564241
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693036"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Funciones de Technical Preview 1612 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*



En este artículo se presentan las características disponibles en la versión 1612 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.    


**Estas son las nuevas características que puede probar con esta versión.**  

## <a name="the-data-warehouse-service-point"></a>El punto de servicio de almacenamiento de datos
A partir de la versión 1612 de Technical Preview, el punto de servicio de almacenamiento de datos le permite almacenar y generar informes de datos históricos a largo plazo para su implementación de Configuration Manager. Esto se consigue mediante sincronizaciones automatizadas desde la base de datos del sitio de Configuration Manager a una base de datos de almacenamiento de datos. Puede acceder a esta información desde su punto de servicios de informes.

De manera predeterminada, cuando instala el nuevo rol de sistema de sitio, Configuration Manager crea la base de datos de almacenamiento de datos en una instancia de SQL Server que especifique. El almacenamiento de datos admite hasta 2 TB de datos, con marcas de tiempo para el seguimiento de cambios.  De manera predeterminada, los datos que se sincronizan desde la base de datos del sitio incluyen los grupos de datos para los datos globales, datos del sitio, proxy global, datos de nube y vistas de base de datos. También puede modificar lo que se sincroniza para incluir tablas adicionales o excluir tablas específicas de los conjuntos de replicación predeterminados.
Los datos predeterminados que se sincronizan incluyen información sobre:
- Mantenimiento de infraestructura
- Seguridad
- Cumplimiento
- Malware   
- Implementaciones de software
- Detalles de inventario (en cambio, el historial de inventario no se sincroniza)

Además de instalar y configurar la base de datos de almacenamiento de datos, se instalan varios informes nuevos, por lo que puede buscar y generar informes fácilmente en estos datos.

### <a name="data-warehouse-dataflow"></a>Flujo de datos de almacenamiento de datos   
![flujo_almacenamientoDeDatos](./media/datawarehouse.png)

| Paso         | Detalles  |
|:------:|-----------|  
| **1** | El servidor de sitio transfiere y almacena datos en la base de datos del sitio.  |  
| **2** | Basándose en su programación y configuración, el punto de servicio de almacenamiento de datos obtiene datos de la base de datos del sitio.  |  
| **3** | El punto de servicio de almacenamiento de datos transfiere y almacena una copia de los datos sincronizados en la base de datos de almacenamiento de datos. |  
| **A** | Con los informes integrados se realiza una solicitud de datos que se pasa al punto de servicios de informes mediante SQL Server Reporting Services. |  
| **B** | La mayoría de los informes se refieren a información actual y estas solicitudes se ejecutan en la base de datos del sitio. |  
| **C** | Cuando un informe solicita datos históricos, mediante uno de los informes con una *Categoría* de **Almacenamiento de datos**, la solicitud se ejecuta en la base de datos de almacenamiento de datos.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Requisitos previos de la base de datos y del punto de servicio de almacenamiento de datos
- Su jerarquía debe tener instalado un rol de sistema de sitio del punto de servicios de informes.
- El equipo en el que instale el rol de sistema de sitio necesita .NET Framework 4.5.2 o versiones posteriores.
- La cuenta de equipo del equipo en el que instale el rol de sistema de sitio debe tener permisos de administrador local en el equipo que hospedará la base de datos de almacenamiento de datos.
- La cuenta administrativa que use para instalar el rol de sistema de sitio debe ser un propietario de la base de datos (DBO) en la instancia de SQL Server que hospedará la base de datos de almacenamiento de datos.  
- La base de datos se admite:
  - Con SQL Server 2012 o versiones posteriores, edición Enterprise o Datacenter.
  - En una instancia con nombre o predeterminada
  - En un *clúster de SQL Server*. Aunque esta configuración debe funcionar, no se ha probado y el soporte técnico es la mejor opción.
  - Cuando se colocaliza con la base de datos del sitio o la base de datos del punto de servicios de informes. En cambio, recomendamos que se instale en un servidor independiente.  
- La cuenta que se usa como *Cuenta de punto de Reporting Services* debe tener el permiso **db_datareader** para la base de datos del almacenamiento de datos.  
- La base de datos no se admite en un *grupo de disponibilidad AlwaysOn de SQL Server*.

### <a name="install-the-data-warehouse"></a>Instalar el almacenamiento de datos
Instale el rol de sistema de sitio de almacenamiento de datos en un sitio de administración central o en un sitio primario con el **Asistente para agregar roles de sistema de sitio** o el **Asistente para crear servidor de sistema de sitio**. Para obtener más información, consulte [Instalación de roles de sistema de sitio para System Center Configuration Manager](../servers/deploy/configure/install-site-system-roles.md). Una jerarquía admite varias instancias de este rol, pero solo se admite una instancia en cada sitio.  

Cuando instala el rol, Configuration Manager crea la base de datos de almacenamiento de datos en la instancia de SQL Server que especifique. Si especifica el nombre de una base de datos existente (como haría si [moviera la base de datos de almacenamiento de datos a un servidor de SQL Server nuevo](#move-the-data-warehouse-database)), Configuration Manager no crea una base de datos nueva sino que usa la que especifique.

#### <a name="configurations-used-during-installation"></a>Configuraciones que se han usado durante la instalación
Use la siguiente información para completar la instalación del rol de sistema de sitio:

Página **Selección de rol del sistema**:  
Antes de que el Asistente muestre una opción para seleccionar e instalar el punto de servicio de almacenamiento de datos, debe tener instalado un punto de servicios de informes.

Página **General**: se necesita la siguiente información general:
- **Configuración de la base de datos de Configuration Manager:**   
  - **Nombre del servidor**: especifique el FQDN del servidor que hospeda la base de datos del sitio. Si no usa una instancia predeterminada de SQL Server, debe especificar la instancia después del FQDN con el siguiente formato: ***&lt;Sqlserver_FQDN>\&lt;nombre_instancia>***
  - **Nombre de la base de datos**: especifique el nombre de la base de datos del sitio.
  - **Comprobar**: haga clic en **Comprobar** para asegurarse de que la conexión a la base de datos del sitio se ha realizado correctamente.
</br></br>
- **Configuración de la base de datos de almacenamiento de datos:**
  - **Nombre del servidor**: especifique el FQDN del servidor que hospeda el punto de servicio de almacenamiento de datos y la base de datos. Si no usa una instancia predeterminada de SQL Server, debe especificar la instancia después del FQDN con el siguiente formato: ***&lt;Sqlserver_FQDN>\&lt;nombre_instancia>***
  - **Nombre de la base de datos**: especifique el FQDN de la base de datos de almacenamiento de datos.  Configuration Manager creará la base de datos con este nombre. Si especifica un nombre de base de datos que ya existe en la instancia de SQL Server, Configuration Manager usará esa base de datos.
  - **Comprobar**: haga clic en **Comprobar** para asegurarse de que la conexión a la base de datos del sitio se ha realizado correctamente.

Página **Configuración de sincronización**:   
- **Configuración de datos:**
  - **Grupos de replicación que se van a sincronizar**: seleccione los grupos de datos que quiere sincronizar. Para obtener información sobre los diferentes tipos de grupos de datos, consulte [Replicación de base de datos](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) y **Vistas distribuidas** en [Transferencias de datos entre sitios en System Center Configuration Manager](../plan-design/hierarchy/data-transfers-between-sites.md).
  - **Tablas incluidas que se van a sincronizar**: especifique el nombre de cada tabla adicional que quiera sincronizar. Separe varias tablas con una coma. Estas tablas se sincronizarán de la base de datos del sitio además de los grupos de replicación que seleccione.
  - **Tablas excluidas que se van a sincronizar**: especifique el nombre de tablas individuales de los grupos de replicación que sincroniza. Las tablas que especifique se excluirán. Separe varias tablas con una coma.
- **Configuración de sincronización:**
  - **Intervalo de sincronización (minutos)** : especifique un valor en minutos. Después de que se alcance el intervalo, se iniciará una nueva sincronización. Se admite un intervalo de 60 a 1440 minutos (24 horas).
  - **Programación**: especifique los días que quiere que se ejecute la sincronización.

**Acceso de punto de Reporting**:   
Después de instalar el rol de almacenamiento de datos, asegúrese de que la cuenta que se usa como *Cuenta de punto de Reporting Services* tiene el permiso **db_datareader** para la base de datos del almacenamiento de datos.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Solución de problemas de instalación y sincronización de datos
Use los siguientes registros para investigar problemas con la instalación del punto de servicio de almacenamiento de datos o con la sincronización de datos:
- **DWSSMSI.log** y **DWSSSetup.log**: use estos registros para investigar errores al instalar el punto de servicio de almacenamiento de datos.
- **Microsoft.ConfigMgrDataWarehouse.log**: use este registro para investigar la sincronización de datos entre la base de datos del sitio y la base de datos de almacenamiento de datos.

### <a name="reporting"></a>Generación de informes
Después de que instala un rol de sistema de sitio de almacenamiento de datos, los siguientes informes están disponibles en su punto de servicios de informes con una *Categoría* de **Almacenamiento de datos:**

|Informe                   | Detalles                                  |
|-------------------------|------------------------------------------|
| **Informe de implementación de aplicaciones** | Vea los detalles de la implementación de aplicaciones para una máquina y una aplicación determinada.|
| **Informe de cumplimiento de las actualizaciones de software y Endpoint Protection**   | Vea los equipos a los que les faltan actualizaciones de software.|
| **Informe de inventario de hardware general**  | Vea todo el inventario de hardware para un equipo específico.|
| **Informe de inventario de software general**  | Vea todo el inventario de software para un equipo específico.|
| **Información general del mantenimiento de infraestructura**  |Muestra información general del mantenimiento de su infraestructura de Configuration Manager.|
| **Lista de malware detectado**  |Vea el malware que se ha detectado en la organización.|
| **Informe de resumen de distribución de software** | Un resumen de distribución de software para un equipo y anuncio específico.|

### <a name="move-the-data-warehouse-database"></a>Mover la base de datos de almacenamiento de datos
Use los siguientes pasos para mover la base de datos de almacenamiento de datos a un servidor de SQL Server nuevo:

1. Revise la configuración de la base de datos actual y registre los detalles de configuración, incluidos:  
   - Los grupos de datos que sincroniza
   - Las tablas que incluye o excluye de la sincronización       

   Volverá a configurar estos grupos de datos y tablas después de que restaure la base de datos en un nuevo servidor y vuelva a instalar el rol de sistema de sitio.  

2. Use SQL Server Management Studio para realizar una copia de seguridad de la base de datos de almacenamiento de datos y, después, restaure esa base de datos en un servidor de SQL en el nuevo equipo que hospedará el almacenamiento de datos.

   Después de restaurar la base de datos en el nuevo servidor, asegúrese de que los permisos de acceso de la base de datos son los mismos en la nueva base de datos de almacenamiento de datos que en la base de datos de almacenamiento de datos original.

3. Use la consola de Configuration Manager para quitar el rol de sistema de sitio del punto de servicio de almacenamiento de datos del servidor actual.

4. Instale un nuevo punto de servicio de almacenamiento de datos y especifique el nombre del nuevo servidor de SQL Server y la instancia que hospeda la base de datos de almacenamiento de datos que ha restaurado.

5. Después de que se instale el rol de sistema de sitio, se completa el movimiento.

Puede revisar los siguientes registros de Configuration Manager para confirmar que el rol de sistema de sitio se ha reinstalado correctamente:  
- **DWSSMSI.log** y **DWSSSetup.log**: use estos registros para investigar errores al instalar el punto de servicio de almacenamiento de datos.
- **Microsoft.ConfigMgrDataWarehouse.log**: use este registro para investigar la sincronización de datos entre la base de datos del sitio y la base de datos de almacenamiento de datos.


## <a name="content-library-cleanup-tool"></a>Herramienta de limpieza de la biblioteca de contenido
A partir de la versión 1612 de Technical Preview, puede usar una nueva herramienta de línea de comandos (**ContentLibraryCleanup.exe**) para quitar contenido que ya no está asociado con ningún paquete o aplicación de un punto de distribución (contenido huérfano). Esta herramienta se denomina la herramienta de limpieza de la biblioteca de contenido.

Esta herramienta solo afecta al contenido del punto de distribución que especifique cuando ejecute la herramienta y no puede quitar contenido de la biblioteca de contenido en el servidor de sitio.

Después de instalar la versión 1612 de Technical Preview, puede buscar **ContentLibraryCleanup.exe** en la carpeta *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* del servidor de sitio de Technical Preview.

La herramienta que se incluye en esta versión de Technical Preview está diseñada para reemplazar las versiones anteriores de herramientas similares para los productos antiguos de Configuration Manager. Aunque esta versión de la herramienta dejará de funcionar después del 1 de marzo de 2017, se presentarán nuevas versiones con las futuras versiones de Technical Preview hasta que esta herramienta se presente como parte de la rama actual o como una versión extraordinaria lista para la producción.

### <a name="requirements"></a>Requisitos  
- La herramienta puede ejecutarse directamente en el equipo que hospeda el punto de distribución o de manera remota desde otro servidor. La herramienta solo puede ejecutarse en un único punto de distribución a la vez.
- La cuenta de usuario que ejecuta la herramienta debe tener directamente los permisos de administración basada en roles que son iguales a los de Administrador total en la jerarquía de Configuration Manager.  La herramienta no funciona cuando a la cuenta de usuario se le conceden permisos como un miembro de un grupo de seguridad de Windows que tiene los permisos de Administrador total.

### <a name="modes-of-operation"></a>Modos de operación
La herramienta puede ejecutarse en dos modos:
1. **Modo de hipótesis**:   
   Cuando no especifica el modificador **/delete**, la herramienta se ejecuta en el modo de hipótesis e identifica el contenido que se eliminaría del punto de distribución, pero realmente no elimina ningún dato.

   - Cuando la herramienta se ejecuta en este modo, la información sobre el contenido que se eliminaría se escribe automáticamente en el archivo de registro de herramientas. No se solicita al usuario que confirme cada eliminación potencial.
   - De manera predeterminada, el archivo de registro se escribe en la carpeta temporal de los usuarios del equipo en el que ejecuta la herramienta. En cambio, puede usar el modificador /log para redirigir el archivo de registro a otra ubicación.  
   </br>

   Recomendamos que ejecute la herramienta en este modo y revise el archivo de registro resultante antes de ejecutar la herramienta con el modificador /delete.  

2. **Modo de eliminación**: Cuando ejecuta la herramienta con el modificador **/delete**, la herramienta se ejecuta en el modo de eliminación.

   - Cuando la herramienta se ejecuta en este modo, el contenido huérfano que se ha detectado en el punto de distribución especificado puede eliminarse de la biblioteca de contenido del punto de distribución.
   -  Antes de eliminar cada archivo, se le pide al usuario su confirmación de que el archivo debe eliminarse.  Puede seleccionar **S** para sí, **N** para no o **Sí a todo** para omitir mensajes adicionales y eliminar todo el contenido huérfano.  
   </br>

   Recomendamos que ejecute la herramienta en el modo de hipótesis y revise el archivo de registro resultante antes de ejecutar la herramienta con el modificador /delete.  

Cuando la herramienta de limpieza de la biblioteca de contenido se ejecuta en cualquier modo, crea automáticamente un registro con un nombre que incluye el modo en el que se ejecuta la herramienta, el nombre del punto de distribución, la fecha y la hora de la operación. El archivo de registro se abre automáticamente cuando finaliza la herramienta. De manera predeterminada, este registro se escribe en la carpeta **temporal** de los usuarios del equipo en el que ejecuta la herramienta. En cambio, puede usar un modificador de línea de comandos para redirigir el archivo de registro a otra ubicación, incluido un recurso compartido de red.   


### <a name="run-the-tool"></a>Ejecutar la herramienta
Para ejecutar la herramienta:
1. Abra un símbolo del sistema administrativo en una carpeta que contenga **ContentLibraryCleanup.exe**.  
2. Después, escriba una línea de comandos que incluya los modificadores de línea de comandos necesarios y modificadores opcionales que quiera usar.

**Problema conocido** Cuando se ejecuta la herramienta, se podría devolver un error similar al siguiente cuando se produce cualquier error en algún paquete o implementación, o bien cuando está en progreso:
-  *System.InvalidOperationException: esta biblioteca de contenido no puede limpiarse ahora porque el paquete \<packageID> no está totalmente instalado.*

**Solución alternativa:** Ninguna. La herramienta no puede identificar archivos huérfanos con confianza cuando la implementación del contenido está en curso o si se ha producido algún error en dicho proceso. Por lo tanto, la herramienta no le permitirá limpiar contenido hasta que se solucione el problema.



### <a name="command-line-switches"></a>Modificadores de línea de comandos  
Los siguientes modificadores de línea de comandos se pueden usar en cualquier orden.   

|Modificador|Detalles|
|---------|-------|
|**/delete**  |**Opcional** </br> Use este modificador cuando quiera eliminar contenido del punto de distribución. Se le preguntará antes de que se elimine el contenido. </br></br> Cuando este modificador no se usa, la herramienta registra los resultados del contenido que se habría eliminado, pero no elimina ningún contenido del punto de distribución. </br></br> Ejemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Ejecute la herramienta en el modo silencioso que suprime todos los mensajes (como los avisos cuando está eliminando contenido) y no abre automáticamente el archivo de registro. </br></br> Ejemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN del punto de distribución>**  | **Requerido** </br> Especifique el nombre de dominio completo (FQDN) del punto de distribución que quiere limpiar. </br></br> Ejemplo:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;FQDN del sitio primario>**       | **Opcional** al limpiar contenido de un punto de distribución en un sitio primario.</br>**Requerido** al limpiar contenido de un punto de distribución en un sitio secundario. </br></br> Especifique el FQDN del sitio primario al que pertenece el punto de distribución, o del primario principal cuando el punto de distribución se encuentra en un sitio secundario. </br></br> Ejemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código del sitio primario>**  | **Opcional** al limpiar contenido de un punto de distribución en un sitio primario.</br>**Requerido** al limpiar contenido de un punto de distribución en un sitio secundario. </br></br> Especifique el código del sitio del sitio primario al que pertenece el punto de distribución, o del sitio primario principal cuando el punto de distribución se encuentra en un sitio secundario.</br></br> Ejemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log \<log file directory>**       |**Opcional** </br> Especifique un directorio en el que colocar los archivos de registro. Este puede ser una unidad local o un recurso compartido de red.</br></br> Cuando este modificador no se usa, los archivos de registro se colocan automáticamente en la carpeta temporal de los usuarios.</br></br> Ejemplo de unidad local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Ejemplo de recurso compartido de red: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;recurso compartido>\&lt;carpeta>***|


## <a name="improvements-for-in-console-search"></a>Mejoras de búsqueda en consola
En función de los comentarios de User Voice, hemos agregado las siguientes mejoras a la búsqueda en la consola:
- **Ruta del objeto:**  
  Ahora muchos objetos admiten una columna nueva denominada **Ruta del objeto**.  Cuando busca e incluye esta columna en los resultados mostrados, puede ver la ruta de cada objeto. Por ejemplo, si ejecuta una búsqueda de aplicaciones en el nodo Aplicaciones y también está buscando subnodos, la columna *Ruta del objeto* del panel de resultados le mostrará la ruta de cada objeto devuelto.   

- **Conservación del texto de búsqueda:**  
  Ahora, cuando escribe texto en el cuadro de texto de búsqueda y luego cambia entre buscar en un subnodo y el nodo actual, el texto que escribió se conserva y permanece disponible para una nueva búsqueda sin tener que volver a escribirlo.

- **Conservación de su decisión para buscar subnodos:**  
  La opción que seleccione para buscar el *nodo actual* o *todos los subnodos* ahora se mantiene cuando cambia el nodo en el que está trabajando.   Este nuevo comportamiento significa que no necesita restablecer constantemente la decisión al desplazarse por la consola.  De manera predeterminada, cuando abre la consola, la opción es la de buscar solo en el nodo actual.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Impedir la instalación de una aplicación si se está ejecutando un programa específico.
Ahora puede configurar una lista de archivos ejecutables (con la extensión .exe) en las propiedades del tipo de implementación que, si se ejecutan, bloquearán la instalación de una aplicación. Después de que se intente la instalación, los usuarios verán un cuadro de diálogo solicitándoles cerrar los procesos que están bloqueando la instalación.

### <a name="try-it-out"></a>Haga la prueba
Para configurar una lista de archivos ejecutables
1. En la página de propiedades de cualquier tipo de implementación, pulse la pestaña **Installer Handling (Control del instalador)** .
2. Haga clic en **Agregar** para agregar uno de los archivos ejecutables a la lista (por ejemplo, **Edge.exe**).
3. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de las propiedades del tipo de implementación.

Ahora, cuando implemente esta aplicación en un usuario o dispositivo, y uno de los ejecutables que ha agregado se esté ejecutando, el usuario final verá un cuadro de diálogo del Centro de software indicándole que se ha producido un error en la instalación porque una aplicación se está ejecutando.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nueva notificación de Windows Hello para empresas para los usuarios finales

Una nueva notificación de Windows 10 informa a los usuarios finales de que deben realizar acciones adicionales para completar la configuración de Windows Hello para empresas (por ejemplo, configurar un PIN).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Compatibilidad con la Tienda Windows para empresas en Configuration Manager

Ahora puede implementar aplicaciones con licencia en línea con un propósito de implementación de **Disponible** desde la Tienda Windows para empresas en equipos que ejecutan el cliente de Configuration Manager.
Para más información, vea [Administración de aplicaciones desde la Tienda Windows para empresas con Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

La compatibilidad de esta característica solo está disponible en estos momentos para equipos que ejecutan la versión preliminar de Windows 10 RS2.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Volver a la página anterior cuando se produce un error en una secuencia de tareas
Ahora puede volver a la página anterior cuando ejecuta una secuencia de tareas y se produce un error. Antes de esta versión, tenía que reiniciar la secuencia de tareas si se producía un error. Por ejemplo, puede usar el botón **Anterior** en los siguientes escenarios:

- Cuando un equipo se inicia en Windows PE, el cuadro de diálogo de arranque de la secuencia de tareas puede mostrarse antes de que la secuencia de tareas esté disponible. Cuando hace clic en Siguiente en este escenario, la página final de la secuencia de tareas se muestra con un mensaje de que no existe ninguna secuencia de tareas disponible. Ahora, puede hacer clic en **Anterior** para buscar de nuevo secuencias de tareas disponibles. Puede repetir este proceso hasta que la secuencia de tareas esté disponible.
- Cuando ejecuta una secuencia de tareas, pero los paquetes de contenido dependientes todavía no están disponibles en los puntos de distribución, se produce un error en la secuencia de tareas. Ahora puede distribuir el contenido que falta (si no se ha distribuido todavía) o esperar a que el contenido esté disponible en los puntos de distribución y, después, hacer clic en **Anterior** para reanudar la búsqueda de la secuencia de tareas para el contenido.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Compatibilidad con archivos de instalación rápida de actualizaciones de Windows 10
Hemos agregado compatibilidad con archivos de instalación rápida en Configuration Manager para las actualizaciones de Windows 10. Cuando use una versión compatible con Windows 10, ahora puede usar la configuración de Configuration Manager para descargar solo la diferencia entre la actualización acumulativa de Windows 10 del mes actual y la actualización del mes anterior. En estos momentos en la rama actual de Configuration Manager, la actualización acumulativa completa de Windows 10 (incluidas todas las actualizaciones de los meses anteriores) se descarga cada mes. Usar los archivos de instalación rápida proporciona descargas más pequeñas y tiempos de instalación más rápidos en los clientes.

> [!IMPORTANT]
> Aunque la configuración para admitir el uso de los archivos de instalación rápida está disponible en Configuration Manager, esta característica solo se admite en la versión 1607 de Windows 10 con una actualización del Agente de Windows Update incluida en las actualizaciones publicadas el 10 de enero de 2017 (Patch Tuesday). Para obtener más información sobre estas actualizaciones, consulte el [artículo de soporte técnico 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Puede aprovechar las ventajas de los archivos de instalación rápida cuando se publique el siguiente conjunto de actualizaciones el 14 de febrero de 2017. La versión 1607 de Windows 10 sin la actualización y las versiones anteriores no admiten los archivos de instalación rápida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Para habilitar la descarga de archivos de instalación rápida para las actualizaciones de Windows 10 en el servidor
Para iniciar la sincronización de los metadatos de los archivos de instalación rápida de Windows 10, debe habilitarlos en las propiedades de punto de actualización de software.
1. En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** > **Sitios**.
2. Seleccione el sitio de administración central o el sitio primario independiente.
3. En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y, a continuación, haga clic en **Punto de actualización de software**. En la pestaña **Archivos de actualización**, seleccione **Download full files for all approved updates and express installation files for Windows 10 (Descargar archivos completos para todas las actualizaciones aprobadas y los archivos de instalación rápida de Windows 10)** .

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para habilitar la compatibilidad para que los clientes descarguen e instalen archivos de instalación rápida
Para habilitar la compatibilidad de los archivos de instalación rápida en los clientes, debe habilitar los archivos de instalación rápida en los clientes en la sección Actualizaciones de software de la configuración de cliente. Esto crea una nueva escucha HTTP que escucha las solicitudes para descargar los archivos de instalación rápida en el puerto que especifique. Una vez que implemente la configuración de cliente para habilitar esta característica en el cliente, intentará descargar la diferencia entre la actualización acumulativa de Windows 10 del mes actual y la actualización del mes anterior (los clientes deben ejecutar una versión de Windows 10 que admita los archivos de instalación rápida).
1. Habilite la compatibilidad para los archivos de instalación rápida en las propiedades de componente de punto de actualización de software (procedimiento anterior).
2. En la consola de Configuration Manager, vaya a **Administración** > **Configuración de cliente**.
3. Seleccione la configuración de cliente adecuada y, después, en la pestaña **Inicio**, haga clic en **Propiedades**.
4. Seleccione la página **Actualizaciones de software**, configure **Sí** para la opción **Enable installation of Express Updates on clients (Habilitar la instalación de actualizaciones rápidas en clientes)** y configure el puerto que ha usado la escucha HTTP en el cliente para la opción **Port used to download content for Express Updates (Puerto usado para descargar el contenido de las actualizaciones rápidas)** .


## <a name="odata-endpoint-data-access"></a>Acceso a datos del punto de conexión de OData

 Ahora Configuration Manager proporciona un punto de conexión de RESTful OData para tener acceso a los datos de Configuration Manager. El punto de conexión es compatible con la versión 4 de OData, que permite que herramientas como Excel y Power BI tengan acceso fácilmente a los datos de Configuration Manager mediante un único punto de conexión. La versión 1612 de Technical Preview solo admite el acceso de lectura a objetos en Configuration Manager.  

Los datos que están actualmente disponibles en el [Proveedor de WMI de Configuration Manager](../../develop/reference/configuration-manager-reference.md) también están accesibles ahora con el nuevo punto de conexión de RESTful OData. Los conjuntos de entidades expuestos mediante el punto de conexión de OData le permiten enumerar los mismos datos que puede consultar con el proveedor de WMI.

### <a name="try-it-out"></a>Haga la prueba

Antes de que pueda usar el punto de conexión de OData, debe habilitarlo en el sitio.

1.  Vaya a **Administración** > **Configuración de sitio** > **Sitios**.
2.  Seleccione el sitio primario y haga clic en **Propiedades**.
3.  En la pestaña General de la hoja de propiedades del sitio primario, haga clic en **Enable REST endpoint for all providers on this site (Habilitar punto de conexión REST para todos los proveedores de este sitio)** y, después, haga clic en **Aceptar**.

En su visor de consultas de OData favorito, pruebe consultas similares a los siguientes ejemplos para devolver varios objetos en Configuration Manager:

| Finalidad | Consulta de OData |
|---|---|
| Obtener todas las colecciones | `http://localhost/CMRestProvider/Collection` |
| Obtener una colección | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Obtener los 100 dispositivos principales de la colección | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Obtener un dispositivo con un id. de recurso de la colección | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Obtener el sistema operativo del dispositivo de la colección | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Obtener los usuarios de la colección | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> Las consultas de ejemplo que se muestran en la tabla usan *localhost* como el nombre de host en la dirección URL y pueden usarse en el equipo que ejecuta el proveedor de SMS. Si está ejecutando las consultas desde un equipo diferente, reemplace localhost por el FQDN del servidor con el proveedor de SMS instalado.

## <a name="azure-active-directory-onboarding"></a>Incorporación de Azure Active Directory

La incorporación de Azure Active Directory (AD) crea una conexión entre Configuration Manager y Azure Active Directory que se va a usar con otros servicios en la nube. Esto puede usarse actualmente para crear la conexión necesaria para la puerta de enlace de administración en la nube.

Realice esta tarea con un administrador de Azure, ya que necesitará credenciales de administrador de Azure.

#### <a name="to-create-the-connection"></a>Para crear la conexión:

2. En el área de trabajo **Administración**, pulse **Cloud Services** > **Azure Active Directory** > **Agregar Azure Active Directory**.
2. Pulse **Iniciar sesión** para crear la conexión con Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Requisitos de cliente de Configuration Manager

Existen varios requisitos para habilitar la creación de directivas de usuario en la puerta de enlace de administración en la nube.

- El proceso de incorporación de Azure AD debe estar completo, y el cliente tiene que estar conectado inicialmente a la red corporativa para obtener la información de conexión.
- Los clientes deben estar unidos a dominio (registrados en Active Directory) y unidos a dominio en la nube (registrados en Azure AD).
- Debe ejecutar [Detección de usuarios de Active Directory](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Debe modificar el cliente de Configuration Manager para permitir solicitudes de directivas de usuarios en Internet, e implementar el cambio en el cliente. Como este cambio en el cliente tiene lugar *en el dispositivo cliente*, puede implementarse mediante la puerta de enlace de administración en la nube aunque no haya completado los cambios de configuración necesarios en la directiva de usuario.
- El punto de administración debe estar configurado para usar HTTPS para proteger el token en la red, y debe tener instalado .NET 4.5.

Después de que realice estos cambios de configuración, puede crear una directiva de usuario y mover los clientes a Internet para probar la directiva. Las solicitudes de directiva de usuario mediante la puerta de enlace de administración en la nube se autenticarán con la autenticación basada en token de Azure AD.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Cambiar para configurar Multi-Factor Authentication para la inscripción de dispositivos

Ahora que puede configurar Multi-Factor Authentication (MFA) para la inscripción de dispositivos en Azure Portal, la opción de MFA se ha quitado de la consola de Configuration Manager. Puede encontrar más información sobre la configuración de MFA para la inscripción [en este tema de Microsoft Intune](../../../intune/enrollment/multi-factor-authentication.md).