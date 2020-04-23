---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1706.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e986827cee4911ac2204a8e2f50923dcdd71fed0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705153"
---
# <a name="capabilities-in-technical-preview-1706-for-configuration-manager"></a>Funciones de Technical Preview 1706 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1706 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, revise [Technical Preview de Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales del uso de este tipo de versiones y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Problemas conocidos de esta Technical Preview:**

- **Mover el punto de distribución**: no se pueden usar las opciones de la consola para mover un punto de distribución entre sitios con esta versión debido al límite establecido para Technical Preview de un solo sitio primario.

- **Configuración de cumplimiento de dispositivo**: podría experimentar un comportamiento opuesto al utilizar las dos nuevas configuraciones para el cumplimiento de dispositivo:
  - **Bloquear depuración USB en el dispositivo**
  - **Bloquear aplicaciones de orígenes desconocidos**

    Por ejemplo, si los administradores establecen **Bloquear depuración USB en el dispositivo** en **true**, todos los dispositivos que no tienen habilitada la depuración USB se marcan como no conformes.

**Estas son las nuevas características que puede probar con esta versión.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Mejoras de los grupos de límites para puntos de actualización de software
<!-- 1324591 -->
Esta versión incluye mejoras para el modo en que los puntos de actualización de software funcionan con grupos de límites. A continuación se resume el nuevo comportamiento de la reserva:
- La reserva para puntos de actualización de software usa ahora un tiempo configurable para aplicarse en los grupos de límites vecinos, con un tiempo mínimo de 120 minutos.

- Independientemente de la configuración de la reserva, un cliente intenta alcanzar el último punto de actualización de software que utilizó durante 120 minutos. Tras no conseguir alcanzar ese servidor durante 120 minutos, el cliente consulta su grupo de puntos de actualización de software disponibles para encontrar otro nuevo.

  - Todos los puntos de actualización de software del grupo de límites actual del cliente se agregan al grupo del cliente de inmediato.

  - Dado que un cliente intenta usar su servidor original durante 120 minutos antes de buscar uno nuevo, no se contacta con otros servidores hasta que no hayan transcurrido esas dos horas.

  - Si la reserva en un grupo vecino se configura durante el período mínimo de 120 minutos, los puntos de actualización de software de ese grupo de límites vecino formarán parte del grupo de servidores disponibles del cliente.

- Transcurridas dos horas sin conseguir alcanzar su servidor original, el cliente cambia a un ciclo más corto para establecer contacto con un nuevo punto de actualización de software.

  Esto significa que si un cliente no puede conectar con un nuevo servidor, selecciona rápidamente el siguiente servidor de su grupo de servidores disponibles e intenta ponerse en contacto con él.

  - Este ciclo continúa hasta que el cliente se conecte a un punto de actualización de software que pueda usar.
  - Hasta el momento en que el cliente encuentre un punto de actualización de software, los servidores adicionales se agregarán al grupo de servidores disponibles cuando se cumpla el tiempo de reserva para cada grupo de límites vecino.

Para obtener más información, vea [Puntos de actualización de software](../servers/deploy/configure/boundary-groups.md#software-update-points) en el tema de Configuración de grupos de límites para la Rama actual.


## <a name="site-server-role-high-availability"></a>Alta disponibilidad del rol del servidor de sitio
<!-- 1128774 -->
La alta disponibilidad para el rol del servidor de sitio es una solución basada en Configuration Manager para instalar un servidor de sitio primario adicional en modo *Pasivo*. El servidor de sitio en modo pasivo se suma al servidor de sitio primario existente que está en modo *Activo*. Un servidor de sitio en modo pasivo está disponible para su uso inmediato, cuando se requiera.

Un servidor de sitio primario en el modo pasivo:
- Utiliza la misma base de datos de sitio que el servidor de sitio activo.
- Recibe una copia de la biblioteca de contenido de los servidores de sitio activos, que, a continuación, se mantiene sincronizada.
- No escribe datos en la base de datos de sitio mientras esté en modo pasivo.
- No admite la instalación o la desinstalación de roles de sistema de sitio opcionales mientras esté en modo pasivo.

Para convertir el servidor de sitio en modo pasivo en el servidor de sitio en modo activo, debe promoverlo de manera manual. De este modo se cambia el servidor de sitio activo para que sea el servidor de sitio pasivo. Los roles de sistema de sitio que están disponibles en el servidor de modo activo original siguen estando disponibles, siempre y cuando sea posible tener acceso a ese equipo. Únicamente el rol de servidor del sitio cambia entre el modo activo y pasivo.

Para instalar un servidor de sitio en modo pasivo, use el **Asistente para crear servidor de sistema de sitio** para configurar un servidor de sitio nuevo con un tipo de **Servidor de sitio primario** y un modo **Pasivo**. El asistente ejecuta entonces el programa de instalación de Configuration Manager en el servidor especificado para instalar el nuevo servidor de sitio en modo pasivo. Una vez completada la instalación, el servidor de sitio en modo activo mantiene el servidor de sitio en modo pasivo y su biblioteca de contenido sincronizados con los cambios o configuraciones que realice en el servidor de sitio activo.

### <a name="prerequisites-and-limitations"></a>Requisitos previos y limitaciones
- En cada sitio primario se admite un solo servidor de sitio en modo pasivo.

- El servidor de sitio en modo pasivo puede ser local o estar basado en la nube de Azure.

- Tanto el servidor de sitio en modo activo como el servidor de sitio en modo pasivo deben estar en el mismo dominio.

- Ambos servidores de sitio deben utilizar la misma base de datos de sitio, que debe ser remota en relación con los equipos de cada uno de ellos.

    - El servidor SQL Server que hospeda la base de datos puede utilizar una instancia predeterminada, una instancia con nombre, el clúster de SQL Server o un grupo de disponibilidad AlwaysOn.

    - El servidor de sitio en modo pasivo está configurado para utilizar la misma base de datos de sitio que el servidor de sitio en modo activo. Sin embargo, el servidor de sitio en modo pasivo no utilizará esa base de datos hasta que se le promueva al modo activo.

- El equipo que ejecutará el servidor de sitio en modo pasivo:

    - Debe cumplir los [requisitos previos para instalar un sitio primario](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    - Se instala mediante archivos de origen que coinciden con la versión del servidor de sitio en modo activo.

    - No puede tener un rol de sistema de sitio de ningún sitio antes de instalar el sitio en modo pasivo.

- Los equipos de servidor de sitio en modo activo y pasivo pueden ejecutar diferentes sistemas operativos o versiones de Service Pack, siempre y cuando sigan siendo compatibles con su versión de Configuration Manager.

- La promoción del servidor del sitio en modo pasivo al servidor en modo activo es manual. No hay ninguna conmutación automática por error.

- Los roles de sistema de sitio pueden instalarse solo en el servidor de sitio que se encuentra en modo activo.

    - Un servidor de sitio en modo activo admite todos los roles de sistema de sitio. No puede instalar roles de sistema de sitio en el servidor cuando se encuentra en modo pasivo.

    - Los roles de sistema de sitio que usan una base de datos (por ejemplo, el punto de notificación) deben tener esa base de datos en un servidor que sea remoto en relación con los servidores de sitio en modo activo y en modo pasivo.

    - El proveedor de SMS no se instala en el servidor de sitio en modo pasivo. Dado que debe conectarse a un proveedor de SMS para que el sitio promueva manualmente el servidor de sitio en modo pasivo al modo activo, se recomienda [instalar al menos otra instancia del proveedor](../plan-design/hierarchy/plan-for-the-sms-provider.md) en un equipo adicional.

**Problema conocido**:   
Con esta versión, el **estado** de las condiciones siguientes aparecen en la consola como valores numéricos en lugar de texto legible:
- 131071: no se pudo realizar la instalación del servidor de sitio
- 720895: no se pudo realizar la desinstalación del rol del servidor de sitio
- 851967: no se pudo realizar la conmutación por error

### <a name="add-a-site-server-in-passive-mode"></a>Adición de un servidor de sitio en el modo pasivo
1. En la consola, vaya a **Administración** > **Configuración del sitio** > **Sitios** e inicie el [Asistente para agregar roles de sistema de sitio](../servers/deploy/configure/install-site-system-roles.md). También puede usar el **Asistente para crear servidor de sistema de sitio**.

2. En la página **General**, especifique el servidor que hospedará el servidor de sitio en modo pasivo. El servidor que especifique no puede hospedar ningún rol de sistema de sitio antes de instalar un servidor de sitio en modo pasivo.

3. En la página **Selección de rol del sistema**, seleccione solo **Primary site server in passive mode** (Servidor de sitio primario en modo pasivo).

4. Para completar al asistente, debe proporcionar la siguiente información, que se usa para ejecutar el programa de instalación e instalar el rol de servidor de sitio en el servidor especificado:
    - Elija copiar los archivos de instalación desde el servidor de sitio activo en el nuevo servidor de sitio en modo pasivo, o especifique una ruta de acceso a una ubicación que incluya el contenido de la carpeta **CD.Latest** del servidor de sitio activo.

    - Especifique el mismo servidor de base de datos de sitio y nombre de la base de datos utilizados en el servidor de sitio en modo activo.

5. Configuration Manager instala entonces el servidor de sitio en modo pasivo en el servidor especificado.

Para conocer el estado de instalación de manera detallada, vaya a **Administración** > **Configuración del sitio** > **Sitios**.
- El estado del servidor de sitio en modo pasivo aparece como **Installing** (Instalando).

- Seleccione el servidor y, a continuación, haga clic en **Mostrar estado** para abrir **Site Server Installation Status** (Estado de instalación del servidor de sitio) para obtener más información.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Promoción del servidor de sitio en modo pasivo a modo activo
Cuando desee cambiar el servidor de sitio en modo pasivo al modo activo, vaya al panel **Nodos** en **Administración** > **Configuración del sitio** > **Sitios**. Siempre que pueda tener acceso a una instancia del proveedor de SMS, podrá acceder al sitio para realizar este cambio.
1. En el panel **Nodos** de la consola de Configuration Manager, seleccione el servidor de sitio en modo pasivo y, a continuación, en la cinta de opciones, elija **Promover a activo**.

2. El **Estado** para el servidor que está promoviendo aparece en el panel **Nodos** como **Promoting** (Promoviendo).

3. Una vez completada la promoción, la columna **Estado** muestra el estado **OK** (Correcto) tanto para el nuevo servidor de sitio en modo *Activo* como para el nuevo servidor de sitio en modo *Pasivo*.

4. En **Administración** > **Configuración del sitio** > **Sitios**, el nombre del servidor del sitio primario ahora muestra el nombre del nuevo servidor de sitio en modo *Activo*.
Para conocer el estado detallado, vaya a **Supervisión** > **Site Server Status** (Estado del servidor de sitio).
    - La columna **Modo** identifica qué servidor está *Activo* o *Pasivo*.

    - Al promocionar un servidor de modo pasivo a modo activo, seleccione el servidor de sitio que se está promocionando a activo y, a continuación, elija **Mostrar estado** en la cinta de opciones. Se abrirá la ventana **Site Server Promotion Status** (Estado de promoción del servidor de sitio), que muestra los detalles adicionales sobre el proceso.

Cuando un servidor de sitio en modo activo cambia a modo pasivo, únicamente el rol de sistema de sitio pasa a pasivo. Todos los demás roles de sistema de sitio instalados en ese equipo permanecen activos y accesibles para los clientes.


### <a name="daily-monitoring"></a>Supervisión diaria
Si tiene un sitio primario en modo pasivo, supervíselo diariamente para garantizar que permanece sincronizado con el servidor de sitio en modo activo y listo para usar. Para ello, vaya a **Supervisión** > **Site Server Status** (Estado del servidor de sitio). Aquí puede ver tanto el servidor de sitio en modo activo como el servidor de sitio en modo pasivo.

La pestaña **Resumen**:
- La columna **Modo** identifica qué servidor está Activo o Pasivo.
- La columna **Estado** muestra el mensaje **OK** (Correcto) si el servidor en modo pasivo está sincronizado con el servidor en modo activo.
- Para ver detalles adicionales sobre el estado de sincronización del contenido, haga clic en **Mostrar estado** en Content Sync State (Estado de sincronización del contenido). De este modo se abre la pestaña Biblioteca de contenido, donde puede intentar corregir problemas de sincronización de contenido.

La pestaña **Biblioteca de contenido**:
- Vea el **Estado** del contenido que se sincroniza desde el servidor de sitio activo en el servidor de sitio en modo pasivo.
- Puede seleccionar el contenido con el estado de **Failed** (Error) y luego elegir **Sync selected items** (Sincronizar los elementos seleccionados) en la cinta de opciones. Esta acción intenta volver a sincronizar ese contenido desde el origen del contenido en el servidor de sitio en modo pasivo. Durante la recuperación, el estado se muestra como **In progress** (En curso) y, una vez completada la sincronización, aparece como **Success** (Correcto).

### <a name="try-it-out"></a>Haga la prueba
Intente realizar las tareas siguientes y luego envíenos sus **comentarios** desde la pestaña **Inicio** de la cinta para comunicarnos si funcionó:
- Puedo instalar un sitio primario en el modo pasivo.
- Puedo usar la consola para promover el servidor de sitio en modo pasivo para que sea el servidor de sitio en modo activo y confirmar el cambio de estado de ambos servidores de sitio.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Inclusión de la confianza para determinados archivos y carpetas en una directiva de Device Guard
<!-- 1324676 -->
En esta versión, hemos agregado más funcionalidades para la administración de directivas de [Device Guard](../../protect/deploy-use/use-device-guard-with-configuration-manager.md).

Ahora tiene la posibilidad de agregar confianza para determinados archivos y carpetas en una directiva de Device Guard. Esto le permite:

1. Solucionar problemas con los comportamientos de instalador administrado
2. Confiar en aplicaciones de línea de negocio que no se pueden implementar con Configuration Manager
3. Confiar en aplicaciones que se incluyen en una imagen de implementación de sistema operativo

### <a name="try-it-out"></a>Haga la prueba

1. Mientras está creando una directiva de Device Guard, en la pestaña Inclusiones del Asistente para crear directiva de Device Guard, haga clic en **Agregar**.
2. En el cuadro de diálogo **Agregar archivo o carpeta de confianza**, especifique la información sobre el archivo o la carpeta en que desea confiar. Puede especificar una ruta de acceso de archivo o carpeta local o conectarse a un dispositivo remoto para el que tiene permiso para conectarse y especificar una ruta de acceso de archivo o carpeta en dicho dispositivo.
3. Complete el asistente.


## <a name="hide-task-sequence-progress"></a>Ocultación del progreso de la secuencia de tareas
<!-- 1354291 -->
En esta versión, puede controlar cuándo se muestra el progreso de la secuencia de tareas a los usuarios finales mediante una variable nueva. En la secuencia de tareas, use el paso **Configurar variable de secuencia de tareas** para establecer el valor de la variable **TSDisableProgressUI** a fin de ocultar o mostrar el progreso de la secuencia de tareas. Puede usar el paso Configurar variable de secuencia de tareas varias veces en una secuencia de tareas para cambiar el valor de la variable. Esto le permite ocultar o mostrar el progreso de la secuencia de tareas en secciones diferentes de la secuencia de tareas.

#### <a name="to-hide-task-sequence-progress"></a>Para ocultar el progreso de la secuencia de tareas
En el editor de la secuencia de tareas, use el paso [Configurar variable de secuencia de tareas](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) para establecer el valor de la variable **TSDisableProgressUI** en **True** para ocultar el progreso de la secuencia de tareas.

#### <a name="to-display-task-sequence-progress"></a>Para mostrar el progreso de la secuencia de tareas
En el editor de la secuencia de tareas, use el paso [Configurar variable de secuencia de tareas](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) para establecer el valor de la variable **TSDisableProgressUI** en **False** para mostrar el progreso de la secuencia de tareas.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Especificación de una ubicación de contenido diferente para el contenido de instalación y el contenido de desinstalación
<!-- 1097546 -->
Actualmente, en Configuration Manager se especifica la ubicación de instalación que contiene los archivos de instalación de una aplicación. Al especificar una ubicación de instalación, esta se usa también como ubicación de desinstalación para el contenido de la aplicación.
Según sus comentarios, cuando se va a desinstalar una aplicación implementada y el contenido de la aplicación no está en el equipo cliente, el cliente descarga todos los archivos de instalación de la aplicación de nuevo antes de desinstalar la aplicación.
Para solucionar este problema, ahora puede especificar tanto una ubicación para el contenido de instalación como una ubicación opcional para el contenido de desinstalación. Además, puede optar por no especificar una ubicación para el contenido de desinstalación.

### <a name="try-it-out"></a>¡Haga la prueba!

1. En las propiedades del tipo de implementación de una aplicación, haga clic en la pestaña **Contenido**.
2. Configure el valor de **Install content location** (Ubicación del contenido de instalación) como suele hacerlo.
3. Para **Uninstall content settings** (Configuración del contenido de desinstalación), elija una de las opciones siguientes:
   - **Same as install content** (Igual que el contenido de instalación): se utilizará la misma ubicación de contenido, con independencia de si se va a instalar o desinstalar la aplicación.
   - **No uninstall content** (Sin contenido de desinstalación): elija esta opción si no desea proporcionar una ubicación de contenido de desinstalación para la aplicación.
   - **Different from install content** (Diferente del contenido de instalación): elija esta opción si desea especificar una ubicación de contenido de desinstalación que sea diferente de la ubicación de contenido de instalación.
5. Si seleccionó **Different from install content** (Diferente del contenido de instalación), busque o escriba la ubicación del contenido de aplicación que se usará para desinstalarla.
6. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de las propiedades del tipo de implementación.


## <a name="accessibility-improvements"></a>Mejoras de accesibilidad  
<!--1253000 -->
Esta versión preliminar incluye varias mejoras para las [características de accesibilidad](../understand/accessibility-features.md) en la consola de Configuration Manager. Entre ellos, se incluye:     

**Nuevos métodos abreviados de teclado para desplazarse por la consola:**
- CTRL + M: establece el foco en el panel principal (central).
- CTRL + T: establece el foco en el nodo superior del panel de navegación. Si el foco ya estaba en dicho panel, este se establece en el último nodo que visitó.
- CTRL + I: establece el foco en la barra de ruta de navegación, debajo de la cinta de opciones.
- CTRL + L: establece el foco en el campo **Búsqueda**, si está disponible.
- CTRL + D: establece el foco en el panel de detalles, si está disponible.
- ALT: cambia el foco dentro y fuera de la cinta de opciones.

**Mejoras generales:**
- Navegación mejorada en el panel de navegación al escribir las letras de un nombre de nodo.
- La navegación con el teclado a través de la vista principal y la cinta de opciones ahora es circular.
- La navegación con el teclado en el panel de detalles ahora es circular. Para volver al objeto o panel anterior, utilice Ctrl + D y luego Mayús + Tab.
- Después de actualizar una vista del área de trabajo, se establece el foco en el panel principal de esa área de trabajo.
- Solución de un problema para permitir que los lectores de pantalla anuncien los nombres de elementos de lista.
- Incorporación de nombres accesibles para varios controles en la página que permite a los lectores de pantalla anunciar información importante.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Cambios en el Asistente para servicios de Azure para admitir Upgrade Readiness
<!-- 1353331 -->
A partir de esta versión, use el Asistente para servicios de Azure para configurar una conexión desde Configuration Manager en Upgrade Readiness. El uso del asistente simplifica la configuración del conector mediante un asistente común para los servicios de Azure relacionados.   

Si bien el método para configurar la conexión ha cambiado, los requisitos previos para la conexión y el modo en que se utiliza Upgrade Readiness permanecen inalterados.   

### <a name="prerequisites-for-upgrade-readiness"></a>Requisitos previos para Upgrade Readiness
Los requisitos previos para una conexión a Upgrade Readiness son los mismos que se detallan para la rama actual de Configuration Manager. Se repiten aquí para su comodidad:  

**Requisitos previos**
- Para agregar la conexión, el entorno de Configuration Manager debe configurar primero un [punto de conexión de servicio](../servers/deploy/configure/about-the-service-connection-point.md) en un [modo en línea](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes). Al agregar la conexión en el entorno, también se instala Microsoft Monitoring Agent en el equipo que ejecuta este rol de sistema de sitio.
- Registre Configuration Manager como una herramienta de administración de "Aplicación web o API web" y obtenga el [identificador de cliente de este registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Cree una clave de cliente para la herramienta de administración registrada en Azure Active Directory.
- En Azure Portal, indique la aplicación web registrada con permiso para acceder a OMS.

> [!IMPORTANT]       
> Al configurar el permiso para acceder a OMS, asegúrese de elegir el rol **Colaborador** y asignarle permisos al grupo de recursos de la aplicación registrada.

Una vez configurados los requisitos previos, estará listo para usar al Asistente para crear la conexión.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Uso del Asistente para servicios de Azure para configurar Upgrade Readiness
1. En la consola, vaya a **Administración** > **Introducción** > **Cloud Services** > **Servicios de Azure** y, después, elija **Configurar servicios de Azure** en la pestaña **Inicio** de la cinta de opciones para iniciar el **Asistente para servicios de Azure**.

2. En la página **Servicios de Azure**, seleccione el **Conector de Upgrade Readiness** y, a continuación, haga clic en **Siguiente**.

3. En la página **Aplicación**, especifique el **entorno de Azure** (Technical Preview admite solo la nube pública). A continuación, haga clic en **importación** para abrir la ventana **Importar aplicaciones**.

4. En la ventana **Importar aplicaciones**, especifique los detalles para una aplicación web que ya existe en su instancia de Azure AD.
    - Proporcione un nombre descriptivo para el nombre del inquilino de Azure AD. A continuación, especifique el identificador de inquilino, el nombre de la aplicación, el identificador de cliente, la clave secreta de la aplicación web de Azure y el URI del identificador de la aplicación.
    - Haga clic en **Comprobar** y, si la operación se completa correctamente, haga clic en **Aceptar** para continuar.

5.  En la página **Configuración**, especifique la suscripción, el grupo de recursos y el área de trabajo de Windows Analytics que desea usar con esta conexión a Upgrade Readiness.  

6. Haga clic en **Siguiente** para ir a la página **Resumen** y, a continuación, complete el asistente para crear la conexión.


## <a name="new-client-settings-for-cloud-services"></a>Nueva configuración de cliente para Cloud Services
<!-- 1319883 -->

En esta versión, hemos agregado dos nuevas opciones de cliente en Configuration Manager. Las encontrará en la sección **Cloud Services**.  Estas opciones ofrecen las siguientes funcionalidades:

- Controlar los clientes de Configuration Manager que pueden tener acceso a una instancia de Cloud Management Gateway configurada.
- Registrar automáticamente los clientes de Configuration Manager unidos mediante dominio a Windows 10 en Azure Active Directory.

Gracias a estas nuevas opciones de configuración podrá disfrutar de las funcionalidades descritas en la versión[Configuration Manager 1705 Technical Preview](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Antes de empezar

Debe haber instalado y configurado Azure AD Connect entre su instancia de Active Directory local y su inquilino de Azure AD.

Si quita la conexión, no se anulará el registro de los dispositivos, pero no se registrarán nuevos dispositivos.

### <a name="try-it-out"></a>Haga la prueba

1. Establezca la siguiente sección de configuración de cliente (que se encuentra en Cloud Services) con la información de [Cómo configurar el cliente](../clients/deploy/configure-client-settings.md).
   - **Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory**: establézcalo en **Sí** (valor predeterminado) o **No**.
   - **Permite que los clientes usen una puerta de enlace de administración en la nube**: establézcalo en **Sí** (valor predeterminado) o **No**.
2. Implemente la configuración del cliente en la recopilación de dispositivo requerida.

Para confirmar que el dispositivo está unido a Azure AD, ejecute el comando **dsregcmd.exe /status** en una ventana del símbolo del sistema. El campo **AzureAdjoined** de los resultados mostrará el valor **YES** si el dispositivo se ha unido a Azure AD.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager
<!-- 1236459 -->

En Configuration Manager, puede implementar scripts en dispositivos de cliente mediante paquetes y programas. En esta Technical Preview, hemos agregado nueva funcionalidad que permite realizar las siguientes acciones:

- Importar scripts de PowerShell en Configuration Manager.
- Editar los scripts desde la consola de Configuration Manager (solo para scripts sin firmar).
- Marcar scripts como aprobados o denegados, para mejorar la seguridad.
- Ejecutar scripts en recopilaciones de equipos cliente de Windows y equipos de Windows administrados locales. No se implementan los scripts, sino que se ejecutan casi en tiempo real en los dispositivos cliente.
- Examine los resultados devueltos por el script en la consola de Configuration Manager.


### <a name="prerequisites"></a>Requisitos previos

Para utilizar scripts, debe ser miembro del rol de seguridad de Configuration Manager adecuado.

- **Para importar y crear scripts**: la cuenta debe tener permisos **Crear** para **scripts SMS** en el rol de seguridad **Administrador total**.
- **Para aprobar o denegar scripts**: la cuenta debe tener permisos **Aprobar** para **scripts SMS** en el rol de seguridad **Administrador total**.
- **Para ejecutar scripts**: la cuenta debe tener el permiso **Ejecutar script** para las **Recopilaciones** en el rol de seguridad **Administrador de la configuración de cumplimiento**.

Para obtener más información sobre los roles de seguridad de Configuration Manager, consulte [Conceptos básicos de la administración basada en roles](../understand/fundamentals-of-role-based-administration.md).

De forma predeterminada, los usuarios no pueden aprobar un script que hayan creado. Dado que los scripts son eficaces y versátiles y se pueden implementar en varios dispositivos, hemos introducido un nuevo concepto por el que se proporciona la capacidad de separar los roles de la persona que crea el script y la persona que aprueba el script. Esto proporciona un nivel adicional de seguridad frente a la ejecución de un script sin supervisión. Puede desactivar esta aprobación secundaria, para facilitar las pruebas, particularmente en la versión Technical Preview.

Para permitir que los usuarios aprueben sus propios scripts:

1. En la consola de Configuration Manager, haga clic en **Administración**.
2. En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.
3. En la lista de sitios, elija el sitio y, a continuación, en la pestaña **Inicio** del grupo **Sitios**, haga clic en **Configuración de jerarquía**.
4. En la pestaña **General** del cuadro de diálogo **Propiedades de configuración de jerarquía**, desactive la casilla **Do not allow script authors to approve their own scripts** (No permitir que los autores de scripts aprueben sus propios scripts).


### <a name="try-it-out"></a>Haga la prueba

#### <a name="import-and-edit-a-script"></a>Importación y modificación de un script

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.
2. En el área de trabajo **Biblioteca de software**, haga clic en **Scripts**.
3. En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear script**.
4. En la página **Script** del Asistente para la **creación de script** asistente, configure lo siguiente:
   - **Nombre de script**: escriba un nombre para el script. Aunque puede crear varios scripts con el mismo nombre, esto dificultará la búsqueda del script que necesite en la consola de Configuration Manager.
   - **Lenguaje de script**: actualmente, solo se admiten scripts de **PowerShell**.
   - **Importar**: se importa un script de PowerShell en la consola. El script se muestra en el campo **Script**.
   - **Borrar**: se quita el script actual del campo **Script**.
   - **Script**: se muestra el script importado actualmente. Puede editar el script en este campo según sea necesario.
5. Complete el asistente. El nuevo script se muestra en la lista **Script** con el estado **En espera de aprobación**. Para poder ejecutar este script en los dispositivos cliente, debe aprobarlo.


#### <a name="approve-or-deny-a-script"></a>Aprobación o denegación de un script



Para ejecutar un script, es necesario aprobarlo. Para aprobar un script:

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.
2. En el área de trabajo **Biblioteca de software**, haga clic en **Scripts**.
3. En la lista **Script**, elija el script que desea aprobar o rechazar y, a continuación, en la pestaña **Inicio**, en el grupo **Script**, haga clic en **Aprobar o denegar**.
4. En el cuadro de diálogo **Approve or deny script** (Aprobar o denegar script), **apruebe** o **deniegue** el script y, opcionalmente, escriba un comentario sobre su decisión. Si se deniega un script, este no se puede ejecutar en los dispositivos cliente.
5. Complete el asistente. En la lista **Script**, podrá ver el cambio de la columna **Estado de la aprobación** en función de la acción llevada a cabo.

#### <a name="run-a-script"></a>Ejecutar un script

Una vez que se ha aprobado un script, podrá ejecutarse en la recopilación que elija.

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.
3. En la lista **Recopilaciones de dispositivos**, haga clic en la recopilación de dispositivos en la que desea ejecutar el script.
3. En la pestaña **Inicio**, en el grupo **Todos los sistemas**, haga clic en **Ejecutar script**.
4. En la página **Script** del Asistente para **ejecutar script**, elija un script de la lista. Se muestran solo los scripts aprobados. Haga clic en **Siguiente** y complete el asistente.

#### <a name="monitor-a-script"></a>Supervisión de un script

Después de ejecutar un script en los dispositivos cliente, siga este procedimiento para supervisar si la operación se ha completado correctamente.

1. En la consola de Configuration Manager, haga clic en **Supervisión**.
2. En el área de trabajo **Supervisión**, haga clic en **Script Results** (Resultados del script).
3. En la lista **Script Results** (Resultados del script) aparecen los resultados para cada script ejecutado en los dispositivos cliente. Un código de salida de script de **0** suele indicar que el script se ejecutó correctamente.

## <a name="pxe-network-boot-support-for-ipv6"></a>Compatibilidad con el arranque de red de PXE para IPv6
<!-- 1269793 -->
Ahora puede habilitar la compatibilidad con el arranque de red de PXE para IPv6 para iniciar una implementación de sistema operativo de la secuencia de tareas. Cuando se usa esta opción, los puntos de distribución habilitados para PXE admitirán tanto IPv4 como IPv6. Esta opción no requiere WDS y detendrá WDS si está presente.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Para habilitar la compatibilidad con el arranque de red de PXE para IPv6
Utilice el siguiente procedimiento para habilitar la opción de compatibilidad con IPv6 para PXE.

1. En la consola de Configuration Manager, vaya a **Administración** > **Introducción** > **Puntos de distribución** y haga clic en **Propiedades** para los puntos de distribución habilitados para PXE.
2. En la pestaña **PXE**, seleccione **Support IPv6** (Compatibilidad con IPv6) para habilitar la compatibilidad de IPv6 para PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Administración de las actualizaciones de controladores de Microsoft Surface
<!-- 1098490 -->
Ahora puede usar Configuration Manager para administrar las actualizaciones de controladores de Microsoft Surface.

### <a name="prerequisites"></a>Requisitos previos
Todos los puntos de actualización de software deben ejecutar Windows Server 2016.

### <a name="try-it-out"></a>Haga la prueba
Intente realizar las tareas siguientes y luego envíenos sus **comentarios** desde la pestaña **Inicio** de la cinta para comunicarnos si funcionó:
1. Habilite la sincronización para controladores de Microsoft Surface. Siga el procedimiento de [Configurar las clasificaciones y los productos](../../sum/get-started/configure-classifications-and-products.md) y seleccione **Incluir actualizaciones de controladores y firmware de Microsoft Surface** en la pestaña **Clasificaciones** para habilitar los controladores de Surface.
2. [Sincronice los controladores de Microsoft Surface](../../sum/get-started/synchronize-software-updates.md).
3. [Implemente los controladores de Microsoft Surface sincronizados](../../sum/deploy-use/deploy-software-updates.md).

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configuración de directivas de aplazamiento de Windows Update para empresas
<!-- 1290890 -->
Ahora puede configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas. Puede administrar las directivas de aplazamiento en el nuevo nodo **Directivas de Windows Update para empresas**, en **Biblioteca de Software** > **Mantenimiento de Windows 10**.

### <a name="prerequisites"></a>Requisitos previos
Los dispositivos con Windows 10 administrados por Windows Update para empresas deben tener conectividad a Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para crear una directiva de aplazamiento para Windows Update para empresas
1. En **Biblioteca de Software** > **Mantenimiento de Windows 10** > **Directivas de Windows Update para empresas**
2. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Create Windows Update for Business Policy** (Crear directiva de Windows Update para empresas) para abrir el Asistente para creación de directiva de Windows Update para empresas.
3. En la página **General**, proporcione un nombre y una descripción para la directiva.
4. En la página **Deferral Policies** (Directivas de aplazamiento), configure si se van a aplazar o pausar las actualizaciones de características.    
    Las actualizaciones de características son generalmente nuevas características de Windows. Después de configurar el parámetro **Nivel de preparación de la rama**, puede definir si le gustaría aplazar la recepción de actualizaciones de características después de que se pongan a disposición de los usuarios por parte de Microsoft, y por cuánto tiempo.
    - **Nivel de preparación de la rama**: configure la rama para la que el dispositivo recibirá actualizaciones de Windows (Rama actual o Rama actual para empresas).
    - **Período de aplazamiento (días)** :  especifique el número de días durante los que se aplazarán las actualizaciones de características. Puede aplazar la recepción de estas actualizaciones de características durante un período de 180 días a partir de su lanzamiento.
    - **Pausar el inicio de las actualizaciones de características:** : seleccione si quiere pausar la recepción de actualizaciones de características para los dispositivos durante un período de hasta 60 días a partir del momento en que se pausen las actualizaciones. Una vez que transcurra el máximo de días, la funcionalidad de pausa expirará automáticamente y el dispositivo buscará actualizaciones aplicables en Windows Update. Después de este análisis, puede pausar las actualizaciones de nuevo. Puede quitar la pausa de las actualizaciones de características desactivando la casilla.   
5. Elija si desea aplazar o pausar las actualizaciones de calidad.     
    Las actualizaciones de calidad suelen ser correcciones y mejoras en la funcionalidad de Windows existente y normalmente se publican el primer martes de cada mes, aunque pueden publicarse en cualquier momento por parte de Microsoft. Puede definir si desea aplazar la recepción de actualizaciones de calidad después de su lanzamiento, y por cuánto tiempo.
    - **Período de aplazamiento (días)** : especifique el número de días durante los que se aplazarán las actualizaciones de características. Puede aplazar la recepción de estas actualizaciones de características durante un período de 180 días a partir de su lanzamiento.
    - **Pausar el inicio de actualizaciones de calidad:** : seleccione si quiere pausar la recepción de actualizaciones de calidad para los dispositivos durante un período de hasta 35 días a partir del momento en que se pausen las actualizaciones. Una vez que transcurra el máximo de días, la funcionalidad de pausa expirará automáticamente y el dispositivo buscará actualizaciones aplicables en Windows Update. Después de este análisis, puede pausar las actualizaciones de nuevo. Puede quitar la pausa de las actualizaciones de calidad desactivando la casilla.
6. Seleccione **Instalar actualizaciones de otros productos de Microsoft** para habilitar el parámetro de directiva de grupo que permite que la configuración de aplazamiento sea aplicable a Microsoft Update, así como a las actualizaciones de Windows Update.
7. Seleccione **Include drivers with Windows Update** (Incluir controladores con Windows Update) para actualizar automáticamente los controladores desde las actualizaciones de Windows Update. Si desactiva esta opción, no se descargan las actualizaciones de controladores desde Windows Update.
8. Complete el asistente para crear la nueva directiva de aplazamiento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Para implementar una directiva de aplazamiento para Windows Update para empresas
1. En **Biblioteca de Software** > **Mantenimiento de Windows 10** > **Directivas de Windows Update para empresas**
2. En la pestaña **Inicio** del grupo **Implementación**, seleccione **Implementar la directiva de Windows Update for Business**.
3. Configure las siguientes opciones:
    - **Directiva de configuración que desea implementar**: seleccione la directiva de Windows Update para empresas que quiere implementar.
    - **Colección**: haga clic en **Examinar** para seleccionar la colección en la que quiere implementar la directiva.
    - **Corregir las reglas no compatibles cuando se admita**: seleccione esta opción para corregir de forma automática las reglas que no sean compatibles con Instrumental de administración de Windows (WMI), el Registro, los scripts y toda la configuración de los dispositivos móviles que Configuration Manager haya inscrito.
    - **Permitir la corrección fuera de la ventana de mantenimiento**: si se ha configurado una ventana de mantenimiento para la colección en la que se va a implementar la directiva, habilite esta opción para permitir que la configuración de cumplimiento corrija el valor fuera de la ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../clients/manage/collections/use-maintenance-windows.md).
    - **Generar una alerta**: configura una alerta que se genera si la compatibilidad de la línea base de configuración es inferior a un determinado porcentaje en una hora y fecha especificadas. También puede especificar si desea que se envíe una alerta a System Center Operations Manager.
    - **Retraso aleatorio (horas)** : especifica una ventana de retraso lo suficientemente grande para evitar un procesamiento excesivo en el Servicio de inscripción de dispositivos de red. El valor predeterminado es 64 horas.
    - **Programación**: especifique la programación de evaluación de cumplimiento según la cual se evalúa el perfil implementado en los equipos cliente. La programación puede ser simple o personalizada. Los equipos cliente evalúan el perfil cuando el usuario inicia sesión.
4.  Complete el asistente para implementar el perfil.



## <a name="support-for-entrust-certification-authorities"></a>Compatibilidad con entidades de certificación de Entrust
<!-- 1350740 -->
Configuration Manager ahora es compatible con entidades de certificación de Entrust; esto habilita la entrega de certificados PFX a dispositivos inscritos en Microsoft Intune.

Puede configurar Entrust como entidad de certificación al agregar un rol de Punto de registro de certificados en Configuration Manager. Al agregar un nuevo perfil de certificado que emite certificados PFX, puede seleccionar una entidad de certificación de Microsoft o Entrust.

**Problema conocido**: en la versión 1706 de Technical Preview no se emiten certificados PFX para entidades de certificación de Microsoft. Esto no afecta a los certificados PFX o los perfiles de SCEP importados.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Compatibilidad de Cisco (IPsec) con perfiles de VPN de iOS
<!-- 1321367 -->

Puede crear un perfil de VPN de iOS con Cisco (IPsec) como tipo de conexión. Para obtener más información, vea [Crear perfiles de VPN](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile).


## <a name="new-windows-configuration-item-settings"></a>Nuevas opciones para elementos de configuración de Windows
<!-- 1354715 -->

En esta versión, hemos agregado los siguientes nuevos parámetros que puede usar en los elementos de configuración de Windows:

### <a name="password"></a>Contraseña

- **Cifrado del dispositivo**

### <a name="device"></a>Dispositivo

- **Modificación de la configuración regional (solo escritorio)**
- **Modificación de la configuración de inicio/apagado y suspensión**
- **Modificación de la configuración de idioma**
- **Modificación de la hora del sistema**
- **Modificación del nombre del dispositivo**

### <a name="store"></a>Tienda

- **Actualizar automáticamente las aplicaciones de la tienda**
- **Usar solo una tienda privada**
- **Inicio de aplicaciones de la tienda**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Bloquear acceso a about:flags**
- **Invalidación de avisos de SmartScreen**
- **Invalidación de avisos de SmartScreen para archivos**
- **Dirección IP de Localhost para WebRTC**
- **Motor de búsqueda predeterminado**
- **URL de archivo XML OpenSearch**
- **Páginas principales (solo escritorio)**

Para obtener más información acerca de la configuración de cumplimiento, consulte [Garantizar el cumplimiento de dispositivos](../../compliance/understand/ensure-device-compliance.md).


## <a name="new-device-compliance-policy-rules"></a>Nuevas reglas de directiva de cumplimiento de dispositivos

* **Tipo de contraseña requerida**. Especifica si el usuario debe crear una contraseña numérica o alfanumérica. En el caso de las contraseñas alfanuméricas, puede especificar también el número mínimo de juegos de caracteres que debe tener la contraseña. Los conjuntos de cuatro caracteres son los siguientes: letras minúsculas, letras mayúsculas, símbolos y números.

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
<br></br>
* **Bloquear depuración USB en el dispositivo**. No es necesario configurar este parámetro porque la depuración USB ya está deshabilitada en los dispositivos Android for Work.

  **Compatible con:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Bloquear aplicaciones de orígenes desconocidos**. Los dispositivos deben impedir la instalación de aplicaciones de orígenes desconocidos. No es necesario configurar este valor, ya que los dispositivos Android for Work siempre restringen la instalación de orígenes desconocidos.

  **Compatible con:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Requerir examen de amenazas en las aplicaciones**. Este valor especifica que la característica Verificar aplicaciones está habilitada en el dispositivo.

  **Compatible con:**
  * Android 4.2 hasta 4.4
  * Samsung KNOX Standard 4.0+


## <a name="new-mobile-application-management-policy-settings"></a>Configuración de nueva directiva de administración de aplicaciones móviles
A partir de esta versión, puede usar tres nuevas opciones de configuración para la directiva de Administración de aplicaciones móviles:

- **Bloquear captura de pantalla (solo en dispositivos Android):** Especifica que las funciones de captura de pantalla del dispositivo se bloquean cuando se usa esta aplicación.

- **Deshabilitar sincronización de contactos:** impide que la aplicación guarde los datos en la aplicación de contactos nativa del dispositivo.

- **Deshabilitar la impresión:** impide que la aplicación imprima datos profesionales o educativos.

## <a name="android-and-ios-enrollment-restrictions"></a>Restricciones de inscripción de iOS y Android
<!-- 1290826 -->
A partir de esta versión, los administradores pueden especificar que los usuarios no inscriban los dispositivos personales de Android o iOS en su entorno híbrido. Esto le permite limitar los dispositivos inscritos a aquellos declarados con anterioridad que pertenezcan a la empresa o a aquellos dispositivos iOS inscritos solo con el Programa de inscripción de dispositivos.

### <a name="try-it-out"></a>Haga la prueba
1. En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripción a Microsoft Intune**.
2. En la pestaña **Inicio** del grupo **Suscripción**, seleccione **Configurar plataformas** y luego seleccione**Android** o **iOS**.
3. Seleccione **Block personally owned devices** (Bloquear dispositivos personales).

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Directiva de administración de aplicaciones de Android for Work para copiar y pegar
Hemos actualizado las descripciones de los parámetros de los elementos de configuración de Android for Work para la opción **Permitir uso compartido de datos entre el perfil de trabajo y el perfil personal**.

|Antes de 1706 Technical Preview | Nuevo nombre de opción | Comportamiento|
|-|-|-|
|Impedir uso compartido más allá de los límites| Restricciones de uso compartido predeterminadas| Trabajo a personal: predeterminado (se espera que esté bloqueado en todas las versiones). <br>Personal a trabajo: predeterminado (permitido en 6.x+, bloqueado en 5.x).|
|Sin restricciones| Las aplicaciones del perfil personal pueden atender solicitudes de intercambio del perfil de trabajo| Trabajo a personal: Permitido  <br>Personal a trabajo: Permitido|
|Las aplicaciones del perfil de trabajo pueden atender solicitudes de intercambio del perfil personal |Las aplicaciones del perfil de trabajo pueden atender solicitudes de intercambio del perfil personal |Trabajo a personal: Predeterminado<br>Personal a trabajo: Permitido<br>(Solo es útil en 5.x, donde personal a trabajo está bloqueado)|

Ninguna de estas opciones evita directamente el comportamiento de copiar y pegar. Hemos agregado un parámetro personalizado al servicio y la aplicación de Portal de empresa en 1704 que puede configurarse para evitar el proceso de copiar y pegar. Se puede establecer a través del URI personalizado.

- OMA-URI:  ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Tipo de valor: Boolean

Si se establece DisallowCrossProfileCopyPaste en true, se impide el comportamiento de copiar y pegar entre perfiles personales y profesionales de Android for Work.

### <a name="try-it-out"></a>Haga la prueba
1. En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Introducción** > **Configuración de cumplimiento** > **Elementos de configuración**.
2. Elija **Crear** para crear un nuevo elemento de configuración y especifique **Nombre** y **Android for Work**.
3. En los grupos de parámetros de dispositivo para configurar, seleccione **Perfil de trabajo** y elija **Siguiente**.
4. Seleccione el valor de **Permitir uso compartido de datos entre perfiles de trabajo y perfiles personales** y luego complete el asistente.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Evaluación de Atestación de estado de dispositivo para las directivas de cumplimiento de acceso condicional
<!-- 1097546 -->
A partir de esta versión, puede utilizar el estado de Atestación de estado de dispositivo como una regla de directiva de cumplimiento para el acceso condicional a los recursos de la empresa.

### <a name="try-it-out"></a>Haga la prueba
Seleccione una regla de Atestación de estado de dispositivo como parte de la evaluación de la directiva de cumplimiento.
