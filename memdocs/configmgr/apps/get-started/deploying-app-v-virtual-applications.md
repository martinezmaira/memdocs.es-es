---
title: Implementación de aplicaciones virtuales de App-V
titleSuffix: Configuration Manager
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones virtuales.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bea7c2ef5c3d77932fcd91ca8d4d2b8baa62edd2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689813"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Implementación de aplicaciones virtuales de App-V con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Al usar Configuration Manager para administrar aplicaciones virtuales, disfrutará de las siguientes ventajas:  

-   Una sola infraestructura de administración  

-   Funciones de escalabilidad, implementación y distribución de contenido, como las colecciones y afinidad de dispositivo de usuario  

-   Funciones de administración avanzada de aplicaciones  

-   Implementación de sistema operativo, el inventario de hardware y software, la disponibilidad de software y Asset Intelligence para admitir aplicaciones virtuales  

Para más información acerca de cómo crear y secuenciar aplicaciones con Microsoft Application Virtualization (App-V), vea [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx) en la biblioteca de TechNet.  

Además de los otros requisitos y procedimientos de Configuration Manager para crear una aplicación, debe tener en cuenta las consideraciones siguientes al crear e implementar aplicaciones virtuales:

-   Para implementar aplicaciones virtuales en los equipos, debe tener el cliente de Configuration Manager y el cliente de App-V instalados en los equipos. Los dispositivos cliente pueden ser equipos portátiles, equipos de escritorio y clientes de Infraestructura de escritorio virtual (VDI). El software del cliente de App-V y el software de Configuration Manager trabajan conjuntamente para entregar, buscar e iniciar paquetes de aplicación virtual. El cliente de Configuration Manager administra la entrega de paquetes de aplicación virtual al cliente de App-V. El cliente de App-V ejecuta la aplicación virtual en el cliente.  

-   Para implementar una aplicación virtual, primero debe crear la aplicación virtual con Application Virtualization Sequencer. El secuenciador supervisa el proceso de instalación de una aplicación y registra la información necesaria para que la aplicación se ejecute en un entorno virtual. También puede utilizar el secuenciador para configurar los archivos y configuraciones que se aplicarán a todos los usuarios y las configuraciones que pueden personalizar los usuarios.  

-   Al secuenciar una aplicación, debe guardar el paquete en una ubicación a la que pueda tener acceso Configuration Manager. A continuación, puede crear una implementación de aplicación que contenga esta aplicación virtual.  

-   Configuration Manager no admite el uso de la función de la memoria caché compartida de solo lectura de App-V 4.6.  

-   Configuration Manager admite la característica de almacén de contenido compartido en App-V 5.  

-   Cuando cree un tipo de implementación para una aplicación virtual, Configuration Manager crea el tipo de implementación mediante los contenidos del archivo de manifiesto de la aplicación. Se trata de un archivo XML que tiene información acerca de la aplicación virtual. Además, Configuration Manager crea requisitos para el tipo de implementación en función de los contenidos del archivo .osd de App-V que tiene información acerca de los sistemas operativos admitidos para la aplicación virtual.  

-   Para implementar aplicaciones virtuales en Configuration Manager, los equipos cliente deben tener instalado, como mínimo, App-V 4.6 SP1 o una versión posterior del cliente.  

-   Para poder implementar correctamente aplicaciones virtuales, debe actualizar el cliente de App-V con la revisión descrita en el artículo [2645225](https://support.microsoft.com/kb/2645225) de Knowledge Base.  

-   Cuando use grupos de conexión en App-V 5.0, las aplicaciones virtuales implementadas pueden compartir el mismo sistema de archivos y el Registro en equipos cliente. A diferencia de las aplicaciones virtuales estándar, estas aplicaciones pueden compartir datos entre sí. Además, los grupos de conexión conservan la configuración de usuario para las aplicaciones que contienen. Los entornos virtuales de App-V en Configuration Manager se usan para configurar grupos de conexiones en equipos cliente. Los entornos virtuales se crean o modifican en equipos cliente cuando se instala la aplicación o cuando los clientes vuelven a evaluar sus aplicaciones instaladas. Puede priorizar estas aplicaciones para que cuando varias aplicaciones intenten modificar un valor del Registro o del sistema de archivos, la aplicación con la prioridad más elevada tenga prioridad. Para obtener más información, consulte [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Crear entornos virtuales de App-V).  

##  <a name="supported-app-v-versions"></a>Versiones de App-V admitidas  
 Configuration Manager admite las siguientes versiones de App-V:  

-   **App-V 4.6**: para poder usar aplicaciones virtuales en Configuration Manager, los equipos cliente necesitan tener instalado el cliente de App-V 4.6 SP1, App-V 4.6 SP2 o App-V 4.6 SP3.  

     También debe actualizar el cliente de App-V 4.6 SP1 con la revisión descrita en el artículo [2645225](https://go.microsoft.com/fwlink/p/?LinkId=237322) de Knowledge Base para poder implementar correctamente aplicaciones virtuales.  

-   **App-V 5, App-V 5.0 SP1, App-V 5.0 SP2, App-V 5.0 SP3 y App-V 5.1**: para App-V 5.0 SP2, necesita instalar [Revisión 5](https://support.microsoft.com/en-us/kb/2963211) o usar App-V 5.0 SP3.  
-   **App-V 5.2**: se integra en Windows 10 Education (versión 1607 y posteriores), Windows 10 Enterprise (versión 1607 y posteriores) y Windows Server 2016.

Para obtener más información sobre App-V en Windows 10, vea los temas siguientes:

- [What's new in App-V](https://technet.microsoft.com/itpro/windows/manage/appv-about-appv) (Novedades en App-V)
- [Getting Started with App-V for Windows 10](https://technet.microsoft.com/itpro/windows/manage/appv-getting-started) (Introducción a App-V para Windows 10)
- [Upgrading to App-V for Windows 10 from an existing installation](https://technet.microsoft.com/itpro/windows/manage/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation) (Actualizar a App-V para Windows 10 desde una instalación existente)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Pasos para administrar aplicaciones virtuales de App-V  
 Para administrar aplicaciones virtuales de App-V, siga estos pasos:  

1.   **Secuencia**: la secuenciación es el proceso de convertir una aplicación en una aplicación virtual mediante el secuenciador de App-V.

2.   **Crear**: use el Asistente para crear tipos de implementación para importar la aplicación secuenciada en un tipo de implementación de Configuration Manager que pueda, después, agregar a una aplicación. También puede crear entornos virtuales que permitan que varias aplicaciones virtuales compartan la configuración.

3.   **Distribuir**: la distribución es el proceso de hacer que las aplicaciones de App-V estén disponibles en los puntos de distribución de Configuration Manager.

4.   **Implementar**: la implementación es el proceso de hacer que la aplicación esté disponible en los equipos cliente. Esto se conoce como publicación y streaming en una infraestructura completa de App-V.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Métodos de entrega de aplicaciones virtuales en Configuration Manager  
Configuration Manager admite dos métodos para la entrega de aplicaciones virtuales a los clientes: entrega por streaming y entrega local (descarga y ejecución).

Cuando decida qué método de entrega va a autilizar, compare el requisitos de espacio en disco reducido para la entrega mediante la transmisión por secuencias, frente a la disponibilidad garantizada de aplicaciones de App-V que ofrece la entrega local. El aumento de espacio en el disco del cliente que se requiere para la entrega local podría ser mejor que transmitir contenido para que los usuarios tengan siempre la aplicación disponible desde cualquier ubicación.  

###  <a name="streaming-delivery"></a>Entrega mediante transmisión por secuencias
Al usar Configuration Manager para administrar el cliente de App-V, admite el streaming de aplicaciones virtuales a través de HTTP o HTTPS desde un punto de distribución. La transmisión por secuencias a través de HTTP o HTTPS está habilitada de forma predeterminada, y se configura en el cuadro de diálogo de propiedades del punto de distribución. Cuando implementa una aplicación virtual en equipos cliente y un usuario la ejecuta, el cliente de Configuration Manager se pone en contacto con un punto de administración para determinar qué punto de distribución se va a usar. Después, la aplicación se transmite por streaming desde el punto de distribución.  

Utilice la información de esta table como guía para decidir si la entrega en streaming es el mejor método de entrega para usted:

|Ventajas|Desventajas|  
|----------------|-------------------|  
|Este método utiliza los protocolos de red estándar para transmitir el contenido del paquete desde puntos de distribución.<br /><br /> Accesos directos al programa para aplicaciones virtuales invocan una conexión al punto de distribución; por lo tanto, la entrega de la aplicación virtual se realiza a petición.<br /><br /> Este método es apropiado para clientes que tengan conexiones de ancho de banda alto a los puntos de distribución.<br /><br /> Las aplicaciones virtuales actualizadas distribuidas en toda la empresa estarán disponibles cuando los clientes reciben la directiva que les informa de la sustitución de la versión actual, y que van a descargar sólo los cambios realizados desde la versión anterior.<br /><br /> Se definen permisos de acceso al punto de distribución para que los usuarios no tengan acceso a aplicaciones ni paquetes no autorizados.|Las aplicaciones virtuales no se transmiten por secuencias hasta que el usuario ejecuta la aplicación por primera vez. En este escenario, un usuario podría recibir los accesos directos a programas para las aplicaciones virtuales y, a continuación, desconectarse de la red antes de ejecutar las aplicaciones virtuales por primera vez. Si el usuario intenta ejecutar la aplicación virtual mientras el cliente está sin conexión, el usuario verá un error y no podrá ejecutar la aplicación virtualizada porque no hay ningún punto de distribución de Configuration Manager disponible para transmitir por streaming la aplicación. La aplicación estará disponible hasta que el usuario se vuelve a conectar a la red y ejecute la aplicación.<br /><br /> Para evitarlo, puede usar el método de entrega local de aplicaciones virtuales a clientes o habilitar la administración de clientes basados en Internet para completar una entrega mediante transmisión por secuencias.|  

###  <a name="local-delivery-download-and-execute"></a>Entrega local (descargar y ejecutar)  
La descarga y ejecución es el método más común cuando se usa Configuration Manager, ya que es el que mejor imita cómo se entregan otros formatos de aplicación con Configuration Manager. Cuando utiliza el método de entrega local, el cliente de Configuration Manager primero descarga el paquete de aplicación virtual completo en la caché de cliente de Configuration Manager. Configuration Manager indica a continuación al cliente de App-V que transmita la aplicación desde la caché de Configuration Manager en la caché de App-V. Si implementa una aplicación virtual en equipos cliente y su contenido no está en la memoria caché de App-V, el cliente de App-V transmite por streaming el contenido de la aplicación desde la memoria caché del cliente de Configuration Manager a la memoria caché de App-V y, luego, ejecuta la aplicación. Una vez ejecutada correctamente la aplicación, puede configurar el cliente de Configuration Manager para que elimine las versiones anteriores del paquete durante el siguiente ciclo de eliminación, o para que las mantenga en la memoria caché del cliente de Configuration Manager. Conservar el contenido localmente puede sacar partido de métodos de optimización de entrega de contenido de paquetes como BranchCache y caché del mismo nivel.

Utilice la información de esta table como guía para decidir si la entrega local es el mejor método de entrega para usted:   

|Ventajas|Desventajas|  
|----------------|-------------------|  
|La funcionalidad de punto de distribución estándar se utiliza para descargar el paquete mediante el Servicio de transferencia inteligente en segundo plano (BITS, por sus siglas en inglés).<br /><br /> El contenido del paquete de aplicación virtual se entrega localmente al cliente. Esto significa que los usuarios pueden ejecutarlo cuando su equipo no está conectado a la red.<br /><br /> Este método es adecuado para las conexiones de red lentas o poco confiables, y en equipos que se conectan a la red solo ocasionalmente.<br /><br /> Configuration Manager usa Compresión diferencial remota (RDC, por sus siglas en inglés) para enviar a los clientes solo los bytes de los archivos que cambiaron cuando se actualizó el contenido del paquete de aplicación virtual. El cliente de Configuration Manager usa RDC para generar una versión nueva del paquete de aplicación virtual basada en la versión actual del paquete y, en su caso, en los cambios que se enviaron al cliente.<br /><br /> Este método proporciona resistencia a la aplicación para usuarios móviles o desconectados. Los administradores pueden optar por mantener el paquete en la memoria caché de Configuration Manager tras la entrega si la aplicación virtual se implementó con una acción Instalar. El paquete de la memoria caché del cliente de Configuration Manager sirve como origen local y confiable de streaming, de tal modo que el cliente de App-V extraiga el paquete y lo ubique en su memoria caché.|Para mantener la aplicación virtual en la memoria caché de Configuration Manager se requiere un espacio en el disco del cliente de, como mínimo, el doble del tamaño del paquete de aplicación virtual.|  

###  <a name="deployment-from-an-image"></a>Implementación desde una imagen

También puede preinstalar aplicaciones virtuales en un equipo y, a continuación, crear una imagen de dicho equipo para su implementación en otros equipos. Sin embargo, si el paquete de aplicación virtual se creó en otro sitio, la replicación de diferencias de binarios no se utilizará para descargar actualizaciones a la aplicación. Esta opción puede ser útil en una infraestructura de escritorio virtual cuando se desea que las aplicaciones estén disponibles inmediatamente, en lugar de descargar las aplicaciones una vez que el usuario inicia sesión.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>Migración de una infraestructura de App-V a una infraestructura de Configuration Manager y App-V  
Use la siguiente tabla como guía para planear una migración de una infraestructura de App-V existente a la administración de aplicaciones virtuales con Configuration Manager.  

|Paso|Más información|  
|----------|----------------------|  
|Examinar las aplicaciones virtuales actuales para elegir las aplicaciones que se van a migrar a la infraestructura de Configuration Manager.|No hay información adicional.|  
|Evaluar los usuarios y dispositivos en los que se van a implementar las aplicaciones virtuales.|Cree recopilaciones de Configuration Manager para agrupar a los usuarios y los dispositivos en los que va a implementar las aplicaciones virtuales. Vea [Introducción a las colecciones](../../core/clients/manage/collections/introduction-to-collections.md).|  
|Migrar grupos de conexiones de App-V 5 a entornos virtuales de Configuration Manager.|Vea la sección [Migrar grupos de conexiones de App-V 5 a entornos virtuales de Configuration Manager](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments) de este tema.|  
|Investigar para averiguar si alguna de las aplicaciones virtuales existen como aplicaciones completas en la infraestructura de Configuration Manager.|Para facilitar la administración, puede agregar la aplicación virtual como tipo de implementación nuevo en la aplicación completa existente. Consulte [Create applications](../../apps/deploy-use/create-applications.md) (Creación de aplicaciones).|  
|Crear aplicaciones para reemplazar los paquetes de App-V existentes.|Consulte [Introducción a la administración de aplicaciones](../understand/introduction-to-application-management.md) y [Creación de aplicaciones](../../apps/deploy-use/create-applications.md).|  
|Configuration Manager empieza la administración de aplicaciones virtuales en un cliente tras la primera implementación de una aplicación virtual. Después, Configuration Manager debe administrar todas las aplicaciones de App-V del equipo.|No hay información adicional.|  
|Distribuir el contenido a los puntos de distribución adecuados para habilitar la entrega local de aplicaciones.|Consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración de contenido e infraestructura de contenido).|  
|Implementar la aplicación en clientes de Configuration Manager.<br /><br /> Si se creó la aplicación de App-V con una versión anterior del secuenciador que no crea un archivo de manifiesto XML, puede abrirla y guardarla en una versión más reciente del secuenciador para crear el archivo. Se requiere este archivo para implementar las aplicaciones virtuales con Configuration Manager.<br /><br /> App-V admite los paquetes de aplicación virtual creados con las versiones SoftGrid 4.1 SP1 o 4.2 del secuenciador.<br /><br /> Si las aplicaciones ya se instalaron localmente, debe desinstalarlas antes de implementar una versión virtual de la aplicación.|Consulte [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implementación de aplicaciones).|  
|Configuration Manager ya no admite el uso de paquetes y programas que contengan aplicaciones virtuales. Al migrar de Configuration Manager 2007 a la rama actual de Configuration Manager, Configuration Manager convierte estos paquetes en aplicaciones.<br /><br /> Los anuncios de Configuration Manager 2007 se convierten en los siguientes tipos de implementación:<br /><br /> - Migración de paquetes de App-V sin anuncio:  un tipo de implementación que utiliza la configuración predeterminada de tipo de implementación.<br /><br /> - Migración de paquetes de App-V con un anuncio: un tipo de implementación que usa la misma configuración que el anuncio de <br />                Configuration Manager 2007.<br /><br /> - Migración de paquetes de App-V con varios anuncios: un tipo de implementación para cada anuncio de <br />                Configuration Manager 2007, que usa la configuración de dicho anuncio.|Vea [Planear la migración de objetos de Configuration Manager a la rama actual de Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migración de grupos de conexión de App-V 5 a entornos virtuales de Configuration Manager  
Los entornos virtuales de App-V en Configuration Manager permiten que las aplicaciones virtuales implementadas compartan el sistema de archivos y el Registro en equipos cliente. Esto significa que, a diferencia de las aplicaciones virtuales estándar, estas aplicaciones pueden compartir datos entre sí. Los entornos virtuales se crean o modifican en equipos cliente cuando se instala la aplicación o cuando los clientes vuelven a evaluar sus aplicaciones instaladas. Los entornos virtuales son similares a los grupos de conexiones en App-V 5 independiente.  

Cuando migra grupos de conexiones desde App-V 5 independiente a entornos virtuales de Configuration Manager, debe procurar que Configuration Manager administre correctamente los grupos de conexiones que ya existen en los equipos cliente y, también, que se conserve el entorno de usuario en dichos grupos de conexiones.  

Para convertir grupos de conexión de App-V 5 en entornos virtuales de Configuration Manager:  

1.  Cree aplicaciones de Configuration Manager para todas las aplicaciones que existían en App-V.  

2.  Implemente las aplicaciones en los usuarios o los dispositivos con un propósito de implementación **Requerido**. Las implementaciones en usuarios deben implementarse en los mismos usuarios que utilizaron la aplicación en App-V. Las implementaciones en equipos deben implementarse en los mismos equipos que tenían la aplicación en App-V.  

3.  Una vez completada la implementación, cree entornos virtuales que coincidan con los grupos de conexión que se publican en App-V independiente. El entorno virtual debe tener los mismos paquetes, en concreto, los tipos de implementación de App-V 5, en el mismo orden.  

Para obtener información sobre cómo crear un entorno virtual de App-V, consulte [How to create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Cómo crear entornos virtuales de App-V).  

Como alternativa, puede eliminar todos los grupos de conexiones del cliente de App-V antes de empezar a implementar aplicaciones con Configuration Manager. Sin embargo, se perderá la configuración guardada por los usuarios en los grupos de conexión de App-V.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Dynamic Suite Composition en App-V 4.6  
Dynamic Suite Composition es una característica que le permite definir un paquete de aplicación virtual como si tuviera una dependencia en otro paquete de aplicación virtual. Cuando se ejecuta la aplicación, el cliente de App-V hospeda el paquete primario y el paquete dependiente en el mismo entorno virtual de la aplicación.  

Para usar esta función con Configuration Manager, ambos paquetes se deben implementar y registrar con el cliente de App-V. Para asegurarse de que el contenido de paquete dependiente se hospeda localmente en el equipo cliente, configure la implementación de aplicaciones para entrega local (descarga y ejecución).  

Para más información sobre Dynamic Suite Composition de App-V, consulte la documentación de App-V.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>Conversión de aplicaciones de App-V 4.6 a aplicaciones de App-V 5  
El formato de paquete de aplicación ha cambiado entre App-V 4.6 y App-V 5. Ya no se admiten las aplicaciones secuenciadas mediante App-V 4.6. Sin embargo, App-V 5 tiene una herramienta de conversión de paquetes que se puede utilizar para convertir aplicaciones. Para más información, consulte su [documentación de App-V 5](https://technet.microsoft.com/library/jj713472.aspx).  

Utilice los pasos siguientes para convertir aplicaciones de App-V 4.6 en aplicaciones de App-V 5:  

1.  Convierta o vuelva a secuenciar paquetes de App-V 4.6 en formato App-V 5.  

2.  Implemente el cliente de App-V 5 en equipos de la jerarquía.  

3.  Cree nuevas aplicaciones que contengan tipos de implementación para las aplicaciones de App-V 5 y cree reglas de sustitución para sustituir a las aplicaciones de App-V 4.6.  

4.  Cree entornos virtuales según sea necesario.  

5.  Implemente las nuevas aplicaciones de App-V 5 en los equipos.  

##  <a name="user-and-deployment-configuration-files"></a>Archivos de configuración de implementación y de usuario  
Los archivos de configuración de implementación y de usuario tienen valores que controlan el comportamiento de una aplicación. Puede utilizar estos archivos para cambiar la configuración de la aplicación sin volver a secuenciarla.  

Una aplicación típica de App-V 5 podría contener los siguientes archivos:  

-   Un archivo de paquete de aplicación (.appv)  

-   Un archivo de configuración de usuario  

-   Un archivo de configuración de implementación  

El archivo de configuración de usuario tiene opciones que se aplican solo al usuario que ha iniciado la sesión. Por ejemplo, puede editar los archivos de configuración para cambiar la información acerca de el acceso directo de la aplicación que se implementará en los usuarios. También puede crear una aplicación de Configuration Manager con varios tipos de implementación. Cada tipo de implementación puede contener un archivo de configuración de usuario distinto y usar reglas de requisitos para garantizar que se instalan en los usuarios correspondientes.  

El archivo de configuración de implementación tiene valores que se aplican al equipo, como la configuración del Registro. El archivo también puede tener la configuración de usuario, que se aplicará a todos los usuarios.  

Si quiere implementar aplicaciones virtuales de App-V 5 con Configuration Manager, los tres archivos deben figurar en la misma carpeta cuando se crea el tipo de implementación de App-V 5. Si hay varios archivos en la carpeta, Configuration Manager usará el más reciente.  

Para más información, consulte su [documentación de App-V 5](https://technet.microsoft.com/library/jj713466.aspx).  

##  <a name="app-v-local-interaction"></a>Interacción local de App-V  
En algunos escenarios de implementación de aplicaciones, unas aplicaciones se instalan localmente en equipos cliente y otras se implementan como aplicaciones virtuales en el mismo equipo cliente. De forma predeterminada, las aplicaciones instaladas localmente no pueden ver o comunicarse directamente con aplicaciones virtualizadas. Este es el comportamiento previsto del aislamiento de aplicaciones de App-V. La interacción local es una característica del cliente de App-V que se puede habilitar en cada aplicación para permitir que las aplicaciones instaladas localmente que se ejecutan en un equipo cliente vean y se comuniquen con aplicaciones virtualizadas. Configuration Manager y App-V son totalmente compatibles con la interacción local.  

Para más información acerca de la función de interacción local de App-V, vea la documentación de App-V.  

##  <a name="app-v-5-shared-content-store"></a>Almacén de contenido compartido de App-V 5  
Configuration Manager admite la función de almacén de contenido compartido en App-V 5. Para más información, consulte [Planeación para implementar el secuenciador y el cliente de App-V 5.0](https://technet.microsoft.com/library/jj713431.aspx).  

##  <a name="monitoring-virtual-applications"></a>Supervisión de aplicaciones virtuales  

### <a name="virtual-application-reports"></a>Informes de aplicación virtual  
Puede usar los siguientes informes para supervisar App-V en su entorno de Configuration Manager:  

|Nombre del informe|Descripción|  
|-----------------|-----------------|  
|Resultados del entorno virtual de App-V|Muestra información acerca de un entorno virtual que se encuentra en un determinado estado para una recopilación seleccionada (solo App-V 5).|  
|Resultados de entorno virtual de App-V para activo|Muestra información acerca de un entorno virtual seleccionado para un determinado activo y los tipos de implementación para el entorno virtual seleccionado (solo App-V 5).|  
|Estado del entorno virtual de App-V|Muestra información de cumplimiento de un entorno virtual seleccionado para una colección determinada. La columna **Retenido** en este informe muestra los activos en los que un entorno virtual configurado anteriormente ya no es aplicable pero se conserva para mantener la configuración de usuario en aplicaciones que se ejecutan en el entorno virtual (solo App-V 5).|  
|Equipos con una aplicación virtual específica|Muestra un resumen de los equipos que tienen el acceso de directo especificado de App-V creado por Application Virtualization Management Sequencer (solo App-V 4.6).|  
|Equipos con un paquete de aplicación virtual específico|Muestra una lista de equipos que tienen el paquete de aplicación de App-V instalado (solo App-V 4.6).|  
|Recuento de todas las instancias de paquetes de aplicación virtual|Muestra un recuento de todos los paquetes de aplicación virtual de App-V detectados (solo App-V 4.6).|  
|Recuento de todas las instancias de aplicaciones virtuales|Muestra un recuento de todas las aplicaciones de App-V detectadas (solo App-V 4.6).|  

### <a name="log-files"></a>Archivos de registro  
Configuration Manager registra información sobre las implementaciones de aplicaciones virtuales en archivos de registro. Para información acerca de los archivos de registro que usan las aplicaciones virtuales y la administración de aplicaciones de Configuration Manager, consulte [Referencia del archivo de registro](../../core/plan-design/hierarchy/log-files.md).  

Para Windows 8.1, puede ver los registros para el cliente de App-V en C:\ProgramData\Microsoft\Application Virtualization Client.  
