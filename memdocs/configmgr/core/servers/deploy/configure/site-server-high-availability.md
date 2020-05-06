---
title: Alta disponibilidad de servidor de sitio
titleSuffix: Configuration Manager
description: Cómo configurar la alta disponibilidad del servidor de sitio de Configuration Manager mediante la adición de un servidor de sitio de modo pasivo.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700903"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Alta disponibilidad de servidor de sitio en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<!--1128774-->

Históricamente, se podía agregar redundancia a la mayoría de los roles de Configuration Manager si había varias instancias de estos roles en el entorno, excepto para el servidor de sitio. La alta disponibilidad para el rol del servidor de sitio es una solución basada en Configuration Manager para instalar un servidor de sitio adicional en modo *pasivo*. Los sitios de administración central y los sitios primarios secundarios ahora pueden tener un servidor de sitio adicional en modo pasivo. El servidor de sitio en modo pasivo puede ser local o estar basado en la nube de Azure.

Esta característica proporciona las siguientes ventajas:

- Redundancia y alta disponibilidad para el rol del servidor de sitio  
- Cambiar más fácilmente el hardware o el sistema operativo del servidor de sitio  
- Migrar más fácilmente el servidor de sitio a IaaS de Azure  

El servidor de sitio en modo pasivo se suma al servidor de sitio existente que está en modo *activo*. Un servidor de sitio en modo pasivo está disponible para uso inmediato, cuando sea necesario. Incluya este servidor de sitio adicional como parte del diseño general para que el servicio de Configuration Manager sea de [alta disponibilidad](high-availability-options.md).  

Un servidor de sitio en modo pasivo:

- Utiliza la misma base de datos de sitio que el servidor de sitio en modo activo.
- No escribe datos en la base de datos de sitio cuando está en modo pasivo.
- Utiliza la misma biblioteca de contenido que el servidor de sitio en modo activo.

Para activar el servidor de sitio en modo pasivo, se *promueve* manualmente. Esta acción cambia el servidor de sitio en modo activo para que sea el servidor de sitio en modo pasivo. Los roles de sistema de sitio que están disponibles en el servidor de modo activo original siguen estando disponibles, siempre y cuando sea posible tener acceso a ese equipo. Solo el rol de servidor de sitio cambia entre los modos activo y pasivo.

El equipo de operaciones e ingeniería de servicios principales de Microsoft usó esta característica para migrar su sitio de administración central a Microsoft Azure. Para obtener más información, consulte el [artículo de Microsoft IT Showcase](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure).

## <a name="prerequisites"></a>Requisitos previos

- La biblioteca de contenido de sitio debe estar en un recurso compartido de red remoto. Ambos servidores de sitio necesitan permisos de control total en el recurso compartido y su contenido. Para obtener más información, vea [Manage content library](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote) (Administrar la biblioteca de contenido).<!--1357525-->  

  - La cuenta de equipo del servidor de sitio necesita permisos de **control total** para la ruta de acceso de red a la que se va a mover la biblioteca de contenido. Este permiso se aplica al recurso compartido y al sistema de archivos. No se instala ningún componente en el sistema remoto.

  - El servidor de sitio no puede tener el rol de punto de distribución. El punto de distribución también usa la biblioteca de contenido, y este rol no admite una biblioteca de contenido remota. Después de mover la biblioteca de contenido, no se puede agregar el rol de punto de distribución al servidor de sitio.  

- El servidor de sitio en modo pasivo puede ser local o estar basado en la nube de Azure.  

    > [!NOTE]
    > Un servidor de sitio en modo pasivo basado en la nube utiliza la infraestructura como servicio (IaaS) de Azure. Vea los siguientes artículos para más información:
    >
    >   - [Máquinas virtuales de Azure (para infraestructuras basadas en la nube)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Preguntas más frecuentes sobre Configuration Manager en Azure](../../../understand/configuration-manager-on-azure.md)  

- Ambos servidores de sitio deben estar unidos al mismo dominio de Active Directory.  

- Configuration Manager admite servidores de sitio en modo pasivo en una jerarquía. Los sitios de administración central y los sitios primarios secundarios ahora pueden tener un servidor de sitio adicional en modo pasivo.<!-- 3607755 -->  

- Los dos servidores de sitio deben usar la misma base de datos.  

  - La base de datos puede ser remota con respecto al servidor de sitio. A partir de la versión 1810, el proceso de instalación de Configuration Manager ya no impide la instalación del rol de servidor de sitio en un equipo con el rol de Windows para clústeres de conmutación por error. SQL Always On requiere este rol, por lo que anteriormente no se podía colocar la base de datos del sitio en el servidor de sitio. Con este cambio, puede crear un sitio de alta disponibilidad con menos servidores usando SQL Always On y un servidor de sitio en modo pasivo.<!-- SCCMDocs issue 1074 -->  

  - El servidor SQL Server que hospeda la base de datos de sitio puede utilizar una instancia predeterminada, una instancia con nombre, el [clúster de SQL Server](use-a-sql-server-cluster-for-the-site-database.md) o un [grupo de disponibilidad de SQL Server AlwaysOn](sql-server-alwayson-for-a-highly-available-site-database.md).  

  - Ambos servidores de sitio necesitan el rol de seguridad **sysadmin** en la instancia de SQL Server que hospeda la base de datos de sitio. El servidor de sitio original ya debería tener estos roles, así que agréguelos al nuevo servidor de sitio. Por ejemplo, el siguiente script SQL agrega estos roles al nuevo servidor de sitio **VM2** en el dominio Contoso:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Los dos servidores de sitio necesitan acceso a la base de datos en la instancia de SQL Server. El servidor de sitio original ya debería tener este acceso, así que agréguelo al nuevo servidor de sitio. Por ejemplo, el siguiente script SQL agrega un inicio de sesión a la base de datos **CM_ABC** para el nuevo servidor de sitio **VM2** en el dominio Contoso:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - El servidor de sitio en modo pasivo está configurado para utilizar la misma base de datos de sitio que el servidor de sitio en modo activo. El servidor de sitio en modo pasivo solo lee en la base de datos. No escribe en la base de datos hasta que se promueva al modo activo.  

- El servidor de sitio en modo pasivo:  

  - Debe cumplir los requisitos previos para instalar un sitio primario. Por ejemplo, .NET Framework, Compresión diferencial remota y Windows ADK. Para obtener más información, consulte [Sitio y requisitos previos de sistema de sitio para Configuration Manager](../../../plan-design/configs/site-and-site-system-prerequisites.md).<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > Asegúrese de instalar SQL Server Native Client. Si no lo instala, el comprobador de requisitos previos durante la instalación de Configuration Manager le informará en un error de que faltan los permisos de SQL Server.<!-- SCCMDocs#2290 -->

  - Su cuenta de equipo debe estar en el grupo de administradores locales del servidor de sitio en modo activo.<!--516036-->

  - Debe realizar la instalación con archivos de origen que coinciden con la versión del servidor de sitio en modo activo.  

  - No puede tener un rol de sistema de sitio de ningún sitio antes de instalar el servidor de sitio en el rol de modo pasivo.  

- Ambos servidores de sitio pueden ejecutar distintas versiones del sistema operativo o del Service Pack, siempre que ambos sean [compatibles con Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

- No hospede el rol de punto de conexión de servicio en cualquier servidor de sitio configurado para alta disponibilidad. Si está actualmente en el servidor de sitio original, quítelo e instálelo en otro servidor de sistema de sitio. Para obtener más información, consulte [About the service connection point](about-the-service-connection-point.md) (Sobre el punto de conexión del servicio).  

- Permisos de la [cuenta de instalación del sistema de sitio](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)  

  - De forma predeterminada, muchos clientes usan la cuenta de equipo del servidor de sitio para instalar nuevos sistemas de sitio. El requisito es agregar la cuenta de equipo del servidor de sitio local al grupo **Administradores** en el sistema de sitio remoto. Si su entorno usa esta configuración, asegúrese de agregar la cuenta de equipo del nuevo servidor de sitio a este grupo local en todos los sistemas de sitio remoto. Por ejemplo, todos los puntos de distribución remotos.  

  - La configuración más segura y recomendada es usar una cuenta de servicio para instalar el sistema de sitio. La configuración más segura consiste en usar una cuenta de servicio local. Si su entorno usa esta configuración, no es necesario ningún cambio.  

## <a name="limitations"></a>Limitaciones

- En cada sitio primario se admite un solo servidor de sitio en modo pasivo.  

- No se admite un servidor de sitio en modo pasivo en un sitio secundario.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > Todavía se admiten sitios secundarios en un sitio primario con servidores de sitio de alta disponibilidad.

- La promoción del servidor de sitio en modo pasivo al modo activo es manual. No hay ninguna conmutación automática por error.  

- No se pueden instalar roles de sistema de sitio en el nuevo servidor antes de agregar el servidor de sitio en modo pasivo.  

    > [!NOTE]
    > Cuando instale el servidor de sitio en modo pasivo, puede agregar roles adicionales según sea necesario. Por ejemplo, un punto de administración en un sitio primario.

- En el caso de roles como el punto de notificación que utilizan una base de datos, hospede la base de datos en un servidor que sea remoto para los dos servidores de sitio.  

- La consola de Configuration Manager no se instala automáticamente en el servidor de sitio en modo pasivo.  

## <a name="add-a-site-server-in-passive-mode"></a>Adición de un servidor de sitio en el modo pasivo

Para más información sobre el proceso general de la adición de roles, vea [Install site system roles](install-site-system-roles.md) (Instalar roles de sistema de sitio).

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio**, seleccione el nodo **Sitios** y, en la cinta, haga clic en **Crear servidor del sistema de sitio**.

2. En la página **General** del Asistente para crear servidor de sistema de sitio, especifique el servidor que va a hospedar el servidor de sitio en modo pasivo. El servidor que especifique no puede hospedar ningún rol de sistema de sitio para que se pueda instalar un servidor de sitio en modo pasivo.  

3. En la página **Selección de rol del sistema**, seleccione únicamente **Site server in passive mode** (Servidor de sitio en modo pasivo).  

    > [!NOTE]  
    > El asistente realiza las siguientes comprobaciones de requisitos previos iniciales en esta página:
    >
    > - El servidor seleccionado no es un servidor de sitio secundario
    > - El servidor seleccionado no es ya un servidor de sitio en modo pasivo
    > - La biblioteca de contenido del sitio se encuentra en una ubicación remota  
    >  
    > Si las comprobaciones de requisitos previos iniciales no se realizan, no podrá continuar más allá de esta página del asistente.  

4. En la página **Servidor de sitio en modo pasivo**, especifique la siguiente información, que sirve para ejecutar el programa de instalación e instalar el rol de servidor de sitio, en el servidor especificado:

     - Elija una de las siguientes opciones:  

         - **Copiar archivos de origen de la instalación mediante la red desde el servidor de sitio en modo activo**: esta opción crea un paquete comprimido y lo envía al nuevo servidor de sitio.  

         - **Usar archivos de origen de la ubicación siguiente en el servidor de sitio en modo pasivo**: por ejemplo, una ruta de acceso local donde ya haya copiado los archivos de origen. Asegúrese de que este contenido tiene la misma versión que el servidor de sitio en modo activo.  

         - (*Recomendado*) **Usar los archivos de origen de la siguiente ubicación de red**: especifique la ruta de acceso directo al contenido de la carpeta **CD.Latest** desde el servidor del sitio en el modo activo. Por ejemplo, `\\Server\SMS_ABC\CD.Latest`, donde "*Server*" es el nombre del servidor de sitio en modo activo y "*ABC*" es el código de sitio.  

     - Especifique la ruta de acceso local en el nuevo servidor de sitio donde se va a instalar Configuration Manager. Por ejemplo: `C:\Program Files\Configuration Manager`  

5. Complete el asistente. Configuration Manager instala entonces el servidor de sitio en modo pasivo en el servidor especificado.

Para obtener información detallada sobre el estado de la instalación, vaya al área de trabajo **Supervisión** de la consola y seleccione el nodo **Estado del servidor de sitio**. El estado del servidor de sitio en modo pasivo aparece como **Instalando**. Para más información, seleccione el servidor y haga clic en **Mostrar estado**. Esta acción abre la ventana de estado de instalación del servidor de sitio. Una vez completado el proceso, se muestra el estado **Correcto** para ambos servidores.

Para más información sobre el proceso de instalación, vea [Diagrama de flujo: configuración de un servidor de sitio en modo pasivo](passive-site-server-flowchart.md).

Después de agregar un servidor de sitio en modo pasivo, vea ambos servidores de sitio en la pestaña **Nodos** del nodo **Sitios** de la consola.

Todos los componentes del servidor de sitio de Configuration Manager se encuentran en modo de espera en el servidor de sitio en modo pasivo. Los servicios de Windows siguen ejecutándose.

## <a name="site-server-promotion"></a>Promoción del servidor de sitio  

Del mismo modo que con copia de seguridad y recuperación, planee y practique el proceso para cambiar los servidores de sitio. Plantéese los siguientes puntos en el plan de promoción:  

- Practique una promoción planeada, donde ambos servidores de sitio están en línea. Practique también una conmutación por error no planificada, desconectando o apagando de manera forzada el servidor del sitio en modo activo.  

- Determine los procesos operativos durante la conmutación por error y lo que se comunica a otros administradores de Configuration Manager.  

- Antes de una promoción planeada:  

  - Compruebe el estado general del sitio y los componentes del sitio. Asegúrese de que todo está correcto como de costumbre en su entorno.  

  - Compruebe el estado de contenido de los paquetes que se repliquen activamente entre sitios.  

  - Compruebe el estado del sitio secundario y la replicación del sitio.

  - No inicie nuevos trabajos de distribución de contenido o de mantenimiento en servidores de sitio secundarios.

    > [!NOTE]
    > Si durante la conmutación por error hay una replicación de archivos o bases de datos entre sitios en curso, el nuevo servidor de sitio no puede recibir el contenido replicado. Si esto ocurre, redistribuya el contenido de software cuando el nuevo servidor de sitio esté activo.<!--515436--> Para la replicación de bases de datos, debe reinicializar un sitio secundario después de la conmutación por error.<!-- SCCMDocs issue 808 -->

  - Reduzca o quite otras actividades programadas al mismo tiempo. Por ejemplo, no planee promover un servidor de sitio inmediatamente después de actualizar el sitio a una nueva versión. La actualización de un sitio conlleva otras tareas que podrían entrar en conflicto con la promoción del servidor de sitio.

    > [!TIP]
    > A continuación encontrará un ejemplo de cómo otras actividades pueden entrar en conflicto con la promoción del servidor de sitio:
    >
    > - Lunes: actualice el sitio a la versión más reciente. Habilite las actualizaciones de cliente automáticas con programas piloto de cliente.
    > - Martes: promueva el servidor de sitio en modo pasivo para que sea el servidor de sitio activo.
    >
    > El miércoles o el jueves, esta acción podría provocar que *todos* los clientes se actualizaran, no solo la recopilación piloto. Este comportamiento puede provocar un uso significativo de la red y una carga inesperada en los puntos de distribución.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Proceso de promoción del servidor de sitio en modo pasivo al modo activo

En esta sección se describe cómo cambiar el servidor de sitio en modo pasivo al modo activo. Para tener acceso al sitio y realizar este cambio, ha de tener acceso a una instancia del proveedor de SMS. Para más información, vea [Use multiple SMS Providers](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv) (Usar varios proveedores de SMS).  

> [!IMPORTANT]  
> Si todas las instancias del proveedor de SMS están sin conexión, no podrá conectarse al sitio porque no hay ningún proveedor disponible. Al agregar el servidor de sitio en modo pasivo, el programa de instalación instala una instancia del proveedor de SMS en este servidor.<!-- SCCMDocs#1613 -->
>
> La consola de Configuration Manager solicita la lista de proveedores de SMS de WMI disponibles en el servidor de sitio. Cuando se instalan varios proveedores de SMS en un sitio, el sitio asigna de forma aleatoria cada nueva solicitud de conexión para que use un proveedor de SMS instalado. No se puede especificar la ubicación del proveedor de SMS para utilizarla con una sesión de conexión específica. Si la consola no puede conectarse al sitio porque el servidor de sitio actual está sin conexión, especifique el otro servidor del sitio en la ventana de conexión de sitio.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio y luego cambie a la pestaña **Nodos**. Seleccione el servidor de sitio en modo pasivo y luego, en la cinta, haga clic en **Promover a activo**. Haga clic en **Sí** para confirmar y continuar.
  
2. Actualice el nodo de la consola. La columna **Estado** del servidor que se promueve aparece en la pestaña **Nodos** como **Promoviendo**.  

3. Una vez completada la promoción, la columna **Estado** muestra el estado **Correcto** tanto para el nuevo servidor de sitio en modo activo como para el nuevo servidor de sitio en modo pasivo. La columna **Nombre del servidor** del sitio muestra ahora el nombre del nuevo servidor de sitio en modo activo.

Para obtener información detallada sobre el estado, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del servidor de sitio**. La columna **Modo** identifica qué servidor está *Activo* o *Pasivo*. Al promover un servidor en modo pasivo a modo activo, seleccione el servidor de sitio que va a promover y, en la cinta, elija **Mostrar estado**. Se abrirá la ventana Site Server Promotion Status (Estado de promoción del servidor de sitio), que muestra otros detalles sobre el proceso.

Cuando un servidor de sitio en modo activo cambia a modo pasivo, únicamente el rol de sistema de sitio pasa a pasivo. Todos los demás roles de sistema de sitio instalados en ese equipo permanecen activos y accesibles para los clientes.

Para más información sobre el proceso de promoción *planeada*, vea [Diagrama de flujo: promoción del servidor de sitio (planeada)](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Conmutación por error no planeada

Si el servidor de sitio en modo activo actual está sin conexión, el servidor de sitio en promoción intenta ponerse en contacto con él durante 30 minutos. Si el servidor sin conexión se recupera antes de ese tiempo, se notifica correctamente y el cambio se realiza sin problemas. En caso contrario, el servidor de sitio en promoción actualiza de manera forzada la configuración del sitio para que esté activo. Si el servidor sin conexión se recupera después de este tiempo, comprueba primero el estado actual de la base de datos del sitio. Luego continúa con las disminución de su nivel al servidor de sitio en modo pasivo.

Durante este período de espera de 30 minutos, el sitio no tiene ningún servidor de sitio en modo activo. Los clientes todavía se comunican con los roles de cara al cliente, tales como puntos de administración, puntos de actualización de software y puntos de distribución. Los usuarios pueden instalar software que ya se ha implementado. No es posible ninguna administración de sitios en este período de tiempo. Para más información, vea [Impactos de errores de sitio](../../manage/site-failure-impacts.md).  

Si el servidor sin conexión está dañado, de tal forma que no puede recuperarse, elimine este servidor de sitio de la consola. Cree luego un nuevo servidor de sitio en modo pasivo para restaurar un servicio de alta disponibilidad.

Para más información sobre el proceso de conmutación por error *no planeada*, vea [Diagrama de flujo: promoción del servidor de sitio (no planeada)](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Tareas adicionales después de la promoción del servidor de sitio  

Después de cambiar de servidor de sitio, no tiene que realizar la mayoría de las demás tareas necesarias al [recuperar un sitio](../../manage/recover-sites.md#post-recovery-tasks). Por ejemplo, no es necesario restablecer las contraseñas ni volver a conectarse a su suscripción a Microsoft Intune.

Puede que se requieran los siguientes pasos si es necesario en su entorno:  

- Si importa certificados PKI de puntos de distribución, vuelva a importar el certificado de los servidores afectados. Para más información, vea [Regeneración de los certificados para puntos de distribución](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- Si Configuration Manager se integra con Microsoft Store para Empresas, vuelva a configurar esa conexión. Para más información, vea [Manage apps from the Microsoft Store for Business](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) (Administrar aplicaciones desde Microsoft Store para Empresas).  

## <a name="daily-monitoring"></a>Supervisión diaria

Cuando haya un servidor de sitio en modo pasivo, supervíselo diariamente. Asegúrese de que su estado sigue siendo Correcto y está listo para su uso. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del servidor de sitio**. Vea ambos servidores de sitio y su estado actual. Vea también el estado en el área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio y luego cambie a la pestaña **Nodos**.

> [!NOTE]
> Al actualizar el sitio a una nueva versión de Configuration Manager, también actualiza el servidor de sitio en modo pasivo. <!-- SCCMDocs-pr#4293 -->