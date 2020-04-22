---
title: Configuration Manager en Azure
titleSuffix: Configuration Manager
description: Información sobre el uso de Configuration Manager en un entorno de Azure.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ced7d5347e4b8b9fbf0a3006063f507578a7b887
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701233"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Configuration Manager en Azure - Preguntas más frecuentes

*Se aplica a: Configuration Manager (rama actual)*

Las siguientes preguntas y respuestas pueden ayudarle a entender cuándo usar y cómo configurar Configuration Manager en Microsoft Azure.

## <a name="general-questions"></a>Preguntas generales
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Mi empresa está intentando migrar todos los servidores físicos posibles a Microsoft Azure, ¿puedo migrar servidores de Configuration Manager a Azure?
Sin duda, ese es un escenario admitido.  Vea [Compatibilidad con entornos de virtualización para Configuration Manager](../plan-design/configs/support-for-virtualization-environments.md).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Estupendo. Mi entorno necesita varios sitios. ¿Todos los sitios primarios y secundarios deben estar en Azure con el sitio de administración central o en local? ¿Qué pasa con los sitios secundarios?
Las comunicaciones de sitio a sitio (replicación basada en archivo y de base de datos) se benefician de la proximidad de estar hospedadas en Azure. Sin embargo, todo el tráfico relacionado con los clientes sería remoto con respecto a los servidores y sistemas de sitio. Si usa una conexión de red rápida y de confianza entre Azure y la intranet con un plan de servicio de datos ilimitado, hospedar toda la infraestructura en Azure es una opción.

Pero si usa un plan de datos según uso y el ancho de banda disponible o el costo suponen un problema, o la conexión de red entre la intranet y Azure no es rápida o puede ser poco confiable, considere la posibilidad de colocar sitios concretos (y sistemas de sitio) en local y, luego, use los controles de ancho de banda integrados en Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>¿El tener Configuration Manager en Azure es un escenario SaaS (software como servicio)?
No, es un escenario IaaS (infraestructura como servicio), dado que hospeda los servidores de infraestructura de Configuration Manager en máquinas virtuales de Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>¿A qué áreas debería prestar atención a la hora de plantearme la migración de mi infraestructura de Configuration Manager a Azure?
Buena pregunta, estas son las áreas más importantes a la hora de tomar esa decisión. Cada una se analiza en una sección independiente de este tema:
1. Redes
2. Disponibilidad
3. Pruebas
4. Coste
5. Experiencia del usuario

## <a name="networking"></a>Redes
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>¿Qué sucede con los requisitos de red? ¿Debo usar ExpressRoute o una puerta de enlace de VPN de Azure?
La red es una decisión muy importante. Las velocidades y la latencia de la red pueden afectar a la funcionalidad entre el servidor de sitio y los sistemas de sitio remotos y cualquier comunicación de cliente hacia los sistemas de sitio. Nuestra recomendación es usar ExpressRoute, pero no hay ninguna limitación de Configuration Manager que impida usar la puerta de enlace de VPN de Azure. Debe repasar cuidadosamente los requisitos (rendimiento, revisiones, distribución de software, implementación de sistema operativo) de esta infraestructura y luego tomar una decisión. Algunos aspectos que se deben tener en cuenta para cada solución son:

- **ExpressRoute** (recomendado)
  - Ampliación natural del centro de datos (puede unir varios centros de datos).
  - Conexiones privadas entre centros de datos de Azure y la infraestructura.
  - No pasa por la red pública de Internet.
  - Ofrece confiabilidad, velocidad, menor latencia, alta seguridad.
  - Ofrece velocidades de hasta 10 Gbps y opciones de plan de datos ilimitados.
- **Puerta de enlace de VPN**
  - VPN de sitio a sitio o de punto a sitio.
  - El tráfico no pasa por la red pública de Internet.
  - Usa el protocolo de seguridad de Internet (IPsec) y el intercambio de claves por red (IKE).

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute tiene muchas opciones diferentes, como ilimitado frente a según uso, distintas opciones de velocidad y complemento premium. ¿Cuál debería elegir?
Las opciones que seleccione dependen del escenario que vaya a implementar y de cuántos datos piense distribuir. Es posible controlar la transferencia de datos de Configuration Manager entre servidores de sitio y puntos de distribución, pero no se puede controlar la comunicación entre servidor de sitio y servidor de sitio.   Cuando se usa un plan de datos según uso, el colocar sitios concretos (y sistemas de sitio) en local y usar los [controles integrados de ancho de banda de Configuration Manager](../plan-design/hierarchy/fundamental-concepts-for-content-management.md) puede ayudar a controlar el costo del uso de Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>¿Qué sucede con los requisitos de instalación como los dominios de Active Directory? ¿Sigo necesitando unir mis servidores de sitio a un dominio de Active Directory?
Sí. Al migrar a Azure, las [configuraciones admitidas](../plan-design/configs/supported-configurations.md) siguen siendo las mismas, incluidos los requisitos de Active Directory para la instalación de Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Entiendo que tengo que unir mis servidores de sitio a un dominio de Active Directory, pero ¿puedo usar Azure Active Directory?
No, Azure Active Directory no se admite de momento. Los servidores de sitio deben seguir siendo miembros de un [dominio de Windows Active Directory](../plan-design/configs/support-for-active-directory-domains.md).



## <a name="availability"></a>Disponibilidad
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Una de las razones por las que voy a migrar infraestructura a Azure es la promesa de alta disponibilidad. ¿Puedo aprovechar las opciones de alta disponibilidad, como los conjuntos de disponibilidad de VM de Azure, para las máquinas virtuales que usaré con Configuration Manager?
Sí. Los conjuntos de disponibilidad de VM de Azure pueden usarse para roles de sistema de sitio redundantes como los puntos de distribución o los puntos de administración.

También puede usarlos para los servidores de sitio de Configuration Manager. Por ejemplo, los sitios de administración central y los sitios primarios pueden estar en el mismo conjunto de disponibilidad, lo que puede ayudar a garantizar que no se reinicien al mismo tiempo.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>¿Cómo puedo hacer que mi base de datos sea de alta disponibilidad? ¿Puedo usar Azure SQL Database? ¿O tengo que usar Microsoft SQL Server en una máquina virtual?
Tiene que usar Microsoft SQL Server en una máquina virtual. Configuration Manager no admite Azure SQL Server de momento, si bien pueden usarse funciones como los grupos de disponibilidad AlwaysOn para SQL Server. Los [grupos de disponibilidad AlwaysOn](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) se recomiendan y se admiten oficialmente a partir de la versión 1602 de Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>¿Puedo usar equilibradores de carga de Azure con roles de sistema de sitio como los puntos de administración o los puntos de actualización de software?
Aunque no se ha probado Configuration Manager con los equilibradores de carga de Azure, si la funcionalidad es transparente para la aplicación, no debería tener efectos adversos sobre las operaciones normales.


## <a name="performance"></a>Pruebas
### <a name="what-factors-affect-performance-in-this-scenario"></a>¿Qué factores afectan al rendimiento en este escenario?
El [tipo y tamaño de VM de Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs), los discos de VM de Azure (se recomienda almacenamiento premium, especialmente para SQL Server), la latencia de red y la velocidad son las áreas más importantes.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Quiero saber más sobre las máquinas virtuales de Azure; ¿qué tamaño de máquina virtual debo usar?
En general, la potencia informática (CPU y memoria) tiene que satisfacer el [hardware recomendado para Configuration Manager](../plan-design/configs/recommended-hardware.md). Pero hay algunas diferencias entre el hardware informático normal y las máquinas virtuales de Azure, especialmente cuando se trata de los discos que usan estas máquinas.  El tamaño de las máquinas virtuales que use dependerá del tamaño del entorno, pero aquí tiene algunas recomendaciones:
- Para implementaciones de producción de un tamaño considerable se recomiendan máquinas virtuales de Azure de clase “**S**”. Esto es porque pueden aprovechar los discos Premium Storage.  Las máquinas virtuales que no son de clase “S” usan almacenamiento de blobs y en general no satisfarán los requisitos de rendimiento necesarios para una experiencia de producción aceptable.
- Para una escala mayor se deben usar varios discos Premium Storage, que se distribuirán en la consola de Windows Disk Management para una E/S máxima por segundo.  
- Durante la implementación del sitio inicial se recomienda usar mejores discos premium o varios de ellos (por ejemplo, P30 en lugar de P20 y 2 x P30 en un volumen seccionado en lugar de 1 x P30). Si más adelante el sitio necesita aumentar el tamaño de VM debido a la carga adicional, puede aprovechar la CPU y la memoria adicionales que proporciona un mayor tamaño de memoria virtual. También tendrá ya discos que pueden aprovechar el rendimiento adicional de E/S por segundo que ofrece el mayor tamaño de VM.



En las tablas siguientes se indican los recuentos de disco iniciales sugeridos para los sitios primario y de administración central de varias instalaciones de tamaño:

**Base de datos de sitio colocalizada**: sitio de administración central o primario con la base de datos de sitio en el servidor de sitio:

| Clientes de escritorio    |Tamaño de VM recomendado|Discos recomendados|
|--------------------|-------------------|-----------------|
|**Hasta 25 k**       |   DS4_V2          |2xP30 (seccionado)  |
|**De 25 a 50 k**      |   DS13_V2         |2xP30 (seccionado)  |
|**De 50 a 100 k**     |   DS14_V2         |3xP30 (seccionado)  |


**Base de datos de sitio remota**: sitio de administración central o primario con la base de datos de sitio en el servidor remoto:

| Clientes de escritorio    |Tamaño de VM recomendado|Discos recomendados |
|--------------------|-------------------|------------------|
|**Hasta 25 k**       | Servidor de sitio: F4S </br>Servidor de bases de datos: DS12_V2 | Servidor de sitio: 1xP30 </br>Servidor de bases de datos: 2xP30 (seccionado)  |
|**De 25 a 50 k**      | Servidor de sitio: F4S </br>Servidor de bases de datos: DS13_V2 | Servidor de sitio: 1xP30 </br>Servidor de bases de datos: 2xP30 (seccionado)   |
|**De 50 a 100 k**     | Servidor de sitio: F8S </br>Servidor de bases de datos: DS14_V2 | Servidor de sitio: 2xP30 (seccionado)   </br>Servidor de bases de datos: 3xP30 (seccionado)   |

A continuación se muestra un ejemplo de la configuración de entre 50 000 y 100 000 clientes en DS14_V2 con tres discos P30 en un volumen seccionado con volúmenes lógicos independientes para los archivos de instalación y de base de datos de Configuration Manager: ![(Discos de máquina virtual)](media/vm_disks.png)  



## <a name="user-experience"></a>Experiencia del usuario
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Ha mencionado que la experiencia del usuario es una de las áreas más importantes, ¿por qué?
Las decisiones que tome con respecto a la red, la disponibilidad, el rendimiento y la colocación de los servidores de sitio de Configuration Manager pueden afectar directamente a los usuarios. Creemos que una migración a Azure debe ser transparente para los usuarios para que no experimenten un cambio en sus interacciones diarias con Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>Vale, lo entiendo. Pienso instalar un único sitio primario independiente en una máquina virtual de Azure y quiero asegurarme de que los costos sean bajos. ¿Debo colocar sistemas de sitio (remotos) como puntos de administración, puntos de distribución y puntos de actualización de software también en máquinas virtuales de Azure o en local?
Excepto la comunicación desde el servidor de sitio a un punto de distribución, estas comunicaciones entre servidores de un sitio se pueden producir en cualquier momento y no usan mecanismos para controlar el empleo de ancho de banda de red. Puesto que no puede controlar la comunicación entre sistemas de sitio, debe tener en cuenta los gastos asociados a estas comunicaciones.

Otros factores que debe tener en cuenta son la velocidad y la latencia de red. Unas redes lentas o poco confiables pueden afectar a la funcionalidad entre el servidor de sitio y los sistemas de sitio remotos, además de a cualquier comunicación de cliente con los sistemas de sitio. También se debe pensar en el número de clientes administrados que usan un sistema de sitio, así como en las características que se usan activamente.
En general, puede aprovechar la orientación normal en lo referente a los vínculos WAN y los sistemas de sitio como punto de partida. Idealmente, el rendimiento de red que seleccione y reciba entre Azure y la intranet será coherente con una WAN que esté bien conectada con una red rápida.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>¿Qué pasa con la distribución y la administración de contenido? ¿Los puntos de distribución estándar deben estar en Azure o en local? ¿Debo usar BranchCache o puntos de distribución de extracción en local? ¿O bien debería usar exclusivamente puntos de distribución en la nube?
El enfoque para la administración de contenido es en gran medida igual que para los servidores y los sistemas de sitio.
- Si usa una conexión de red rápida y de confianza entre Azure y la intranet con un plan de datos ilimitados, una opción podría ser hospedar los puntos de distribución estándar en Azure.
- Si usa un plan de datos según uso y el costo del ancho de banda constituye un problema o la conexión de red entre la intranet y Azure no es rápida o puede ser poco confiable, podría considerar otros enfoques. Estos incluyen colocar puntos de distribución estándar o de extracción en local y usar BranchCache. El empleo de puntos de distribución basados en la nube también es una opción, pero hay algunos límites con respecto a los tipos de contenido admitidos (por ejemplo, no se admiten paquetes de actualizaciones de software).

> [!NOTE]
>  Si se necesita compatibilidad con PXE o con la multidifusión, debe usar puntos de distribución locales (estándar o de extracción) para responder a las solicitudes de inicio.


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Aunque no tengo problemas con las limitaciones de los puntos de distribución basados en la nube, no quiero colocar mi punto de administración en una red perimetral, aunque sea necesario para admitir a mis clientes basados en Internet. ¿Tengo alguna otra opción?
Sí. Con la versión 1610 de Configuration Manager, hemos presentado la [puerta de enlace de administración en la nube](../clients/manage/manage-clients-internet.md#cloud-management-gateway) como una característica de versión preliminar. (Esta característica apareció por primera vez en la versión 1606 de Technical Preview como [Servicio de proxy en la nube](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)).

**Cloud Management Gateway** proporciona una manera sencilla de administrar clientes de Configuration Manager en Internet. El servicio, que se implementa en Microsoft Azure y exige una suscripción de Azure, se conecta a la infraestructura local de Configuration Manager con un nuevo rol denominado punto de conexión de la puerta de enlace de administración en la nube. Una vez implementado y configurado, los clientes pueden acceder a los roles de sistema de sitio de Configuration Manager locales, con independencia de si están conectados a la red interna privada o a Internet.

Puede empezar a usar la puerta de enlace de administración en la nube en su entorno y proporcionarnos comentarios para que la mejoremos. Para obtener más información sobre las características de versión preliminar, vea [Uso de las características de versión preliminar de las actualizaciones](../servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>También he oído que hay otra característica nueva denominada caché del mismo nivel presentada como una característica de versión preliminar en la versión 1610. ¿Es diferente de BranchCache? ¿Cuál debería elegir?
Sí, son totalmente diferentes. La [caché del mismo nivel](../plan-design/hierarchy/client-peer-cache.md) es una tecnología 100 % nativa de Configuration Manager, mientras que BranchCache es una característica de Windows. Ambas le pueden resultar útiles; BranchCache usa una difusión para buscar el contenido necesario, mientras que la caché del mismo nivel usa la configuración del grupo de límites del flujo de trabajo de distribución normal de Configuration Manager.

Puede configurar cualquier cliente como origen de caché del mismo nivel. Luego, cuando los puntos de administración proporcionan a los clientes información sobre las ubicaciones de orígenes de contenido, proporcionan detalles sobre los puntos de distribución y los orígenes de caché del mismo nivel que tienen el contenido que el cliente necesita.


## <a name="cost"></a>Coste
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>Vale, quisiera saber un poco sobre el costo. ¿Es una solución rentable para mí?
Es difícil de decir, ya que cada entorno es diferente. Lo mejor es hacer el cálculo con su entorno con la calculadora de precios de Microsoft Azure: https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Recursos adicionales
**Conceptos básicos:** https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Tipos de máquinas virtuales de Azure:**
- Tamaños de máquinas de Azure: https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
- Precios de VM: https://azure.microsoft.com/pricing/details/virtual-machines/  
- Precios de almacenamiento: https://azure.microsoft.com/pricing/details/storage/

**Consideraciones de rendimiento del disco:**    
- Introducción a de disco Premium: https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Más información de disco Premium: https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- Práctica recopilación de gráficos de tamaños máximos y destinos de rendimiento del almacenamiento: https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- Otra introducción + algunos estupendos datos de expertos sobre los entresijos de funcionamiento de Premium Storage: https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Disponibilidad:**
- SLA de tiempo de actividad de IaaS de Azure: https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- Conjuntos de disponibilidad explicados: https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Conectividad:**
- ExpressRoute frente a VPN de Azure: https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- Precios de Express Route: https://azure.microsoft.com/pricing/details/expressroute/
- Más información sobre Express Route: https://azure.microsoft.com/documentation/articles/expressroute-introduction/
