---
title: Alta disponibilidad
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar Configuration Manager mediante el uso de opciones que mantienen un alto nivel de servicio disponible.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf8714aff7235736628d44238561eea82b896698
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073320"
---
# <a name="high-availability-options-for-configuration-manager"></a>Opciones de alta disponibilidad para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se explica cómo implementar Configuration Manager mediante el uso de opciones que mantienen un alto nivel de servicio disponible.

Las siguientes opciones de Configuration Manager permiten la alta disponibilidad:

- Configure cualquier sitio principal independiente con un servidor de sitio adicional en modo pasivo.  

- Configure un grupo de disponibilidad Always On de SQL Server para la base de datos de sitio de los sitios primarios y el sitio de administración central.

- Los sitios admiten varias instancias de roles de sistema de sitio que ofrecen servicios importantes a los clientes. Por ejemplo, puntos de administración y puntos de distribución.  

- Los sitios de administración central y los sitios primarios admiten la copia de seguridad de la base de datos del sitio. La base de datos de sitio almacena todas las configuraciones de sitios y clientes. Los sitios de una jerarquía compartan estos datos de configuración.  

- Las opciones de recuperación del sitio integradas pueden reducir el tiempo de inactividad del servidor. Estas opciones avanzadas simplifican la recuperación cuando se tiene una jerarquía con un sitio de administración central.  

- Los clientes pueden corregir automáticamente los problemas más frecuentes sin intervención administrativa.  

- Los sitios generan alertas acerca de los clientes que no pueden enviar datos recientes, lo que alerta a los administradores sobre posibles problemas.  

- Configuration Manager proporciona varios informes y paneles integrados. Úselos para identificar problemas y tendencias antes de que se conviertan en problemas para las operaciones del cliente o el servidor.  

Configuration Manager incluye varias características que prestan servicio prácticamente en tiempo real. Si estas características son fundamentales para satisfacer los requisitos de la empresa, planee y configure los sitios y las jerarquías para lograr alta disponibilidad. Por ejemplo:  

- [Acciones de notificación de cliente](../../../clients/manage/manage-clients.md), como reinicio, inicio de exámenes de Windows Defender o escritorio remoto.  

- Mensajes basados en estado para la supervisión de características como las actualizaciones de software y Endpoint Protection.

- [Scripts](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Otras características de Configuration Manager no prestan servicio en tiempo real. Estas características incluyen, pero no se limitan a, la configuración de cliente, el inventario de hardware y software, las implementaciones de software y la configuración de cumplimiento. Es de esperar que funcionen con cierta latencia de datos. Es poco común en la mayoría de escenarios que implican una interrupción temporal del servicio que se conviertan en un problema crítico. Para minimizar el tiempo de inactividad, mantener la autonomía de las operaciones y proporcionar un alto nivel de servicio, configure los sitios y las jerarquías teniendo en mente la alta disponibilidad.  

Por ejemplo, los clientes de Configuration Manager suelen funcionar de forma autónoma mediante el uso de programaciones y configuraciones conocidas de operaciones, y programaciones para enviar datos al sitio para su procesamiento.  

- Cuando los clientes no pueden ponerse en contacto con el sitio, almacenan en caché los datos que se van a enviar hasta que pueden ponerse en contacto con el sitio.  

- Los clientes que no pueden ponerse en contacto con el sitio siguen funcionando. Usan las últimas programaciones conocidas y la información almacenada en caché hasta que pueden ponerse en contacto con el sitio y recibir nuevas directivas. Por ejemplo, un cliente puede mantener una aplicación descargada previamente que se debe ejecutar o instalar.

- El sitio supervisa sus sistemas de sitio y sus clientes para conocer las actualizaciones de estado periódicas. Puede generar alertas si no se registran estos componentes.  

- Los informes integrados proporcionan información sobre las operaciones en curso, las operaciones históricas y las tendencias actuales. Configuration Manager también admite mensajes basados en el estado que proporcionan información casi en tiempo real de las operaciones en curso.  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a> Alta disponibilidad de sitios y jerarquías  

### <a name="use-a-site-server-in-passive-mode"></a>Usar un servidor de sitio en modo pasivo

Instale un servidor de sitio adicional en modo *pasivo* para un sitio principal independiente. El servidor de sitio en modo pasivo se suma al servidor de sitio existente en modo *activo*. Un servidor de sitio en modo pasivo está disponible para uso inmediato, cuando sea necesario. Para obtener más información, vea [Alta disponibilidad de servidor de sitio](site-server-high-availability.md).  

### <a name="use-a-remote-content-library"></a>Usar una biblioteca de contenido remota

Mueva la biblioteca de contenido del sitio a una ubicación remota que proporcione almacenamiento de alta disponibilidad. Esta característica es un requisito para la alta disponibilidad del servidor de sitio. Para obtener más información, vea [La biblioteca de contenido](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="centralize-content-sources"></a>Centralizar orígenes de contenido

Todo el contenido de software de Configuration Manager necesita una ubicación de origen del paquete en la red. Use almacenamiento centralizado de alta disponibilidad para hospedar una ubicación de origen del paquete común para todo el contenido.

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Usar un grupo de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos del sitio

Hospede la base de datos de sitio de los sitios primarios y el sitio de administración central en grupos de disponibilidad Always On de SQL Server. Para obtener más información, vea [Preparación para usar grupos de disponibilidad AlwaysOn de SQL Server](sql-server-alwayson-for-a-highly-available-site-database.md).  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Utilizar un clúster de SQL Server para hospedar la base de datos del sitio

Cuando se utiliza un clúster de SQL Server para la base de datos en un sitio de administración central o un sitio primario, se utiliza la compatibilidad con la conmutación por error integrada en SQL Server.  

Los sitios secundarios no pueden usar un clúster de SQL Server ni son compatibles con la copia de seguridad ni la restauración de su base de datos de sitio. Recupere un sitio secundario volviendo a instalarlo desde su sitio primario principal.  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Implementar una jerarquía de sitios con un sitio de administración central y uno o varios sitios primarios secundarios

Esta configuración puede proporcionar tolerancia a errores cuando los sitios administran segmentos de la red que se superponen. Además, ofrece una opción de recuperación adicional para usar la información de la base de datos compartida disponible en otro sitio, para volver a crear la base de datos del sitio en el sitio recuperado. Use esta opción para reemplazar una copia de seguridad con errores o no disponible de la base de datos del sitio con errores.  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Crear copias de seguridad periódicas en sitios de administración central y sitios primarios

Al crear y probar una copia de seguridad de sitio periódica, se garantiza contar con los datos necesarios para recuperar un sitio. Además se realiza la recuperación de un sitio en la mínima cantidad de tiempo.  

### <a name="install-multiple-instances-of-site-system-roles"></a>Instalar varias instancias de roles de sistema de sitio

Al instalar varias instancias de roles de sistema de sitio críticos, se proporcionan puntos de contacto redundantes para los clientes. Por ejemplo, varios puntos de administración y puntos de distribución proporcionan servicios redundantes en caso de que un servidor determinado se encuentre sin conexión.  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Instalar varias instancias del proveedor de SMS en un sitio

El proveedor de SMS proporciona el punto de contacto administrativo para una o varias consolas de Configuration Manager. Para proporcionar redundancia a puntos de contacto para administrar el sitio y la jerarquía, instale varios proveedores de SMS.  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a> Alta disponibilidad para los roles de sistema de sitio

En cada sitio, se implementan roles de sistema de sitio para proporcionar los servicios que desea que los clientes utilicen en ese sitio. La base de datos del sitio contiene la información de configuración del sitio y de todos los clientes. Utilice una o varias de las opciones disponibles para proporcionar alta disponibilidad de la base de datos del sitio y la recuperación del sitio y de la base de datos de sitio si es necesario.  

### <a name="redundancy-for-important-site-system-roles"></a>Redundancia de roles de sistema de sitio importantes

- Punto de servicio web del catálogo de aplicaciones  

- Punto de sitios web del catálogo de aplicaciones  

- Punto de distribución  

- Punto de administración  

- Punto de actualización de software  

- Punto de migración de estado  

Para proporcionar redundancia a informes en sitios y clientes, instale varias instancias del punto de servicios de informes.

Para la compatibilidad de conmutación por error con el punto de actualización de software, use Windows PowerShell para instalar este rol en un clúster de equilibrio de carga de red de Windows (NLB).  

### <a name="built-in-site-backup"></a>Copia de seguridad de sitio integrada

Configuration Manager incluye una tarea de copia de seguridad integrada para ayudarle a crear una copia de seguridad de su sitio y de la información crítica según una programación periódica. Además, el Asistente para instalación de Configuration Manager admite acciones de restauración del sitio para ayudarle a restaurar un sitio para que funcione de nuevo.  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Publicación en Active Directory Domain Services y DNS

Configure cada sitio para publicar datos sobre el sitio en Active Directory Domain Services y DNS. Esta publicación permite a los clientes identificar el servidor más accesible de la red. Los clientes además la usan para identificar cuando los servidores de sitio del nuevo sitio están disponibles para proporcionar servicios importantes, como puntos de administración.  

### <a name="sms-provider-and-configuration-manager-console"></a>Proveedor de SMS y consola de Configuration Manager

Configuration Manager admite la instalación de varios proveedores de SMS en servidores independientes como varios puntos de acceso para la consola. Si el servidor de un proveedor de SMS está desconectado, puede seguir viendo y administrando sitios y clientes.  

Cuando una consola de Configuration Manager se conecta a un sitio, se conecta a una instancia del proveedor de SMS en ese sitio. La instancia del proveedor de SMS se selecciona de forma aleatoria. Si el proveedor de SMS seleccionado no está disponible, tiene las siguientes opciones:  

- Vuelva a conectar la consola al sitio. A cada nueva solicitud de conexión se le asigna aleatoriamente una instancia del proveedor de SMS. Es posible que a la nueva conexión se le asigne una instancia disponible.  

- Conecte la consola a otro sitio de Configuration Manager y administre la configuración desde esa conexión. Esta opción conlleva un ligero retraso de los cambios de configuración de no más de unos minutos. Una vez que el proveedor de SMS del sitio esté conectado, vuelva a conectar la consola de Configuration Manager directamente al sitio que quiere administrar.  

Instale la consola de Configuration Manager en varios equipos para que la usen los administradores. Cada proveedor de SMS admite conexiones de más de una consola.  

### <a name="management-point"></a>Punto de administración

Instale varios puntos de administración en cada sitio primario y habilite los sitios para publicar datos del sitio en su infraestructura de Active Directory y en DNS.  

Varios puntos de administración ayudan a equilibrar la carga del uso de cualquier punto de administración único por parte de varios clientes. Además considere la posibilidad de instalar una o varias réplicas de base de datos para puntos de administración. Esta configuración reduce las operaciones que hacen un uso intensivo del procesador del punto de administración. También aumenta la disponibilidad de este rol de sistema de sitio crítico.  

Los sitios secundarios solo admiten la instalación de un punto de administración, que debe estar ubicado en el servidor de sitio secundario. No se considera que los puntos de administración de sitios secundarios tengan una configuración de alta disponibilidad.  

> [!NOTE]  
> Los dispositivos administrados mediante la administración de dispositivos móviles local se conectan a un único punto de administración en un sitio primario. Configuration Manager asigna el punto de administración al dispositivo móvil durante la inscripción y, después, no cambia. Al instalar varios puntos de administración y habilitar más de uno para dispositivos móviles, el punto de administración que se asigna a un cliente de dispositivo móvil no es determinista.  
>
> Si el punto de administración que usa un cliente de dispositivo móvil deja de estar disponible, debe resolver el problema con este punto de administración o borrar el dispositivo móvil y volver a inscribirlo de forma que pueda asignarse a un punto de administración operativa habilitado para dispositivos móviles.  

### <a name="distribution-point"></a>Punto de distribución

Instale varios puntos de distribución y distribuya contenido a varios puntos de distribución. Agregue más de un punto de distribución por grupo de límites para asegurarse de que los clientes obtengan varias opciones en su solicitud de contenido. Configure las relaciones de los grupos de límites de modo que tengan un comportamiento de reserva de predicción para otro grupo de límites o punto de distribución en la nube. Para obtener más información, vea [Configuración de grupos de límites](boundary-groups.md).  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Punto de servicio web del catálogo de aplicaciones y punto de sitios web del catálogo de aplicaciones

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. La compatibilidad de los roles de catálogo de aplicaciones finaliza en la versión 1910.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Características eliminadas y en desuso](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Instale más de una instancia de cada rol de sistema de sitio. Para obtener el mejor rendimiento posible, implemente uno de cada en el mismo servidor de sistema de sitio.  

Cada rol de sistema de sitio del catálogo de aplicaciones proporciona la misma información que las otras instancias de ese rol, independientemente de su ubicación en la jerarquía. Si un cliente realiza una solicitud al catálogo de aplicaciones y ha configurado los clientes de modo que detecten automáticamente el punto de sitios web del catálogo de aplicaciones predeterminado, se dirige al cliente a una instancia disponible. Los clientes prefieren instancias del catálogo de aplicaciones locales, en función de la ubicación de red actual del cliente.  

Para más información sobre esta opción de cliente y del funcionamiento de la detección automática, vea la opción de cliente [Agente de equipo](../../../clients/deploy/about-client-settings.md#computer-agent).  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a> Alta disponibilidad para clientes  

### <a name="client-operations-are-autonomous"></a>Las operaciones de cliente son autónomas

La autonomía del cliente de Configuration Manager incluye los siguientes comportamientos:  

- Los clientes no necesitan un contacto continuo con ningún servidor de sistema de sitio concreto. Usan configuraciones conocidas para realizar acciones preconfiguradas según una programación.  

- Los clientes pueden usar cualquier instancia disponible de un rol de sistema de sitio que proporcione servicios a los clientes. Intentan ponerse en contacto con servidores conocidos hasta que encuentran un servidor disponible.  

- Los clientes pueden ejecutar inventario, implementaciones de software y acciones programadas similares independientemente del contacto directo con los servidores de sistema de sitio.  

- Los clientes que están configurados para usar un punto de estado de reserva, pueden enviar detalles al punto de estado de reserva cuando no se pueden comunicar con un punto de administración.  

### <a name="clients-can-repair-themselves"></a>Los clientes pueden repararse a sí mismos

Los clientes corrigen automáticamente los problemas más comunes sin intervención administrativa directa.  

- Periódicamente, los clientes autoevalúan su estado. Toman medidas para corregir los problemas habituales mediante una caché local de pasos de corrección y archivos de origen para las reparaciones.  

- Cuando un cliente no puede enviar información de estado a su sitio, el sitio puede generar una alerta. Los usuarios administrativos que reciban estas alertas pueden emprender acciones inmediatas para restaurar el funcionamiento normal del cliente.  

### <a name="clients-cache-information-to-use-in-the-future"></a>Los clientes almacenan en caché información para utilizarla en el futuro

Cuando un cliente se comunica con un punto de administración, puede obtener y almacenar en caché la información siguiente:  

- Configuración de cliente  

- Programaciones de cliente  

- Información acerca de las implementaciones de software y una descarga del software que el cliente está programado para instalar, cuando la implementación está configurada para realizar esta acción.  

Cuando un cliente no puede ponerse en contacto con un punto de administración, los clientes almacenan en caché localmente el estado y la información del cliente que envían al sitio. El cliente transfiere estos datos una vez que establece contacto con un punto de administración.  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>El cliente puede enviar el estado a un punto de estado de reserva

Cuando se configura un cliente para que use un punto de estado de reserva, se proporciona un punto adicional de contacto para que el cliente pueda enviar detalles importantes sobre su funcionamiento. Los clientes configurados para usar un punto de estado de reserva siguen enviando el estado de sus operaciones al rol de sistema de sitio, incluso cuando el cliente no se puede comunicar con un punto de administración.  

### <a name="central-management-of-client-data-and-client-identity"></a>Administración central de los datos del cliente y la identidad del cliente

La base de datos del sitio, en lugar del cliente individual, conserva información importante sobre la identidad de cada cliente y asocia esos datos a un equipo específico o usuario.  

- Los archivos de origen de cliente en un equipo se pueden desinstalar y volver a instalar sin que afecte a los registros históricos del equipo donde está instalado el cliente.  

- Un error en un equipo cliente no afecta a la integridad de la información almacenada en la base de datos. Esta información puede estar disponible en los informes.  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a> Opciones de sitios y roles de sistema de sitio que no tienen alta disponibilidad

Varios sistemas de sitio no admiten distintas instancias en un sitio o en la jerarquía. Esta información puede ayudarle a prepararse para cuando estos sistemas de sitio se desconecten.  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Punto de sincronización de Asset Intelligence (jerarquía)

Este rol de sistema de sitio no se considera crítico y ofrece una funcionalidad opcional en Configuration Manager. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

- Corrija la causa de la desconexión del sistema de sitio.  

- Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  

### <a name="endpoint-protection-point-hierarchy"></a>Punto de Endpoint Protection (jerarquía)

Este rol de sistema de sitio no se considera crítico y ofrece una funcionalidad opcional en Configuration Manager. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

- Corrija la causa de la desconexión del sistema de sitio.  

- Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  

### <a name="enrollment-point-site"></a>Punto de inscripción (sitio)

Este rol de sistema de sitio no se considera crítico y ofrece una funcionalidad opcional en Configuration Manager. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

- Corrija la causa de la desconexión del sistema de sitio.  

- Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  

### <a name="enrollment-proxy-point-site"></a>Punto de proxy de inscripción (sitio)

Este rol de sistema de sitio no se considera crítico y ofrece una funcionalidad opcional en Configuration Manager. Sin embargo, puede instalar varias instancias de este rol de sistema de sitio en un sitio y en varios sitios en la jerarquía. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

- Corrija la causa de la desconexión del sistema de sitio.  

- Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  

Si hay más de un servidor proxy de inscripción en un sitio, utilice un alias DNS para el nombre del servidor. Si utiliza esta configuración, el round robin de DNS proporciona cierta tolerancia a errores y equilibrio de carga cuando los usuarios inscriben sus dispositivos móviles.  

### <a name="fallback-status-point-site-or-hierarchy"></a>Punto de estado de reserva (sitio o jerarquía)

Este rol de sistema de sitio no se considera crítico y ofrece una funcionalidad opcional en Configuration Manager. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

- Corrija la causa de la desconexión del sistema de sitio.  

- Desinstale el rol del servidor actual e instale el rol en un nuevo servidor. Dado que el punto de estado de reserva se asigna a los clientes durante la instalación, debe modificar los clientes existentes para usar el nuevo servidor de sistema de sitio.  

### <a name="service-connection-point-hierarchy"></a>Punto de conexión de servicio (jerarquía)

Aunque este rol de sistema de sitio es crítico para mantener actualizada la rama actual de Configuration Manager, por lo general no se usa con frecuencia. Si este sistema se desconecta, use una de las opciones siguientes:

- Corrija la causa de la desconexión del sistema de sitio.  

- Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  


## <a name="see-also"></a>Vea también

- [Configuraciones admitidas](../../../plan-design/configs/supported-configurations.md)  

- [Hardware recomendado](../../../plan-design/configs/recommended-hardware.md)  

- [Sistemas operativos compatibles con servidores de sistema de sitio](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Requisitos previos de sitio y sistema de sitio](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Impactos del error de sitio](../../manage/site-failure-impacts.md)  
