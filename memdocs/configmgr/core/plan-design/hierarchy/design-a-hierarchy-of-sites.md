---
title: Diseño de una jerarquía de sitios
titleSuffix: Configuration Manager
description: Comprenda las opciones de administración y las topologías disponibles en Configuration Manager para planear la jerarquía de sitios.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3c642e97589ff345e4eb3a17b63b3fdfbc2891f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703593"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Diseñar una jerarquía de sitios para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de instalar el primer sitio de una nueva jerarquía de Configuration Manager, le recomendamos que comprenda lo siguiente:  

- Las topologías disponibles en Configuration Manager.  

- Los tipos de sitios disponibles y sus relaciones entre sí.  

- El ámbito de administración que proporciona cada tipo de sitio.  

- Las opciones de administración de contenidos que pueden reducir el número de sitios que necesita instalar.  

Después, planee una topología que se adapte de manera eficiente a sus necesidades empresariales actuales y que, más adelante, pueda expandirla para administrar el crecimiento futuro.  

Al realizar el planeamiento, tenga en cuenta las limitaciones para agregar sitios a una jerarquía o a un sitio independiente:  

- Instale un nuevo sitio primario debajo de un sitio de administración central hasta alcanzar el [número máximo admitido de sitios primarios](../configs/size-and-scale-numbers.md) para la jerarquía.  

- [Expanda un sitio primario independiente para instalar un nuevo sitio de administración central](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) y, después, instale otros sitios primarios.  

- Instale nuevos sitios secundarios debajo de un sitio primario, hasta alcanzar el [número máximo admitido del sitio primario](../configs/size-and-scale-numbers.md) y la jerarquía general.  

- No se puede agregar un sitio instalado anteriormente a una jerarquía existente para combinar dos sitios independientes. Configuration Manager solo admite la instalación de nuevos sitios en una jerarquía de sitios existente.  


> [!NOTE]  
> Al planear una nueva instalación de Configuration Manager, tenga en cuenta las [notas de la versión](../../servers/deploy/install/release-notes.md) que detallan los problemas actuales en las versiones activas. Las notas de la versión se aplican a todas las ramas de Configuration Manager. Al usar la [rama de la versión preliminar técnica](../../get-started/technical-preview.md), encuentre problemas específicos para esa rama en la documentación de cada versión de la vista preliminar técnica.  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a> Topología de la jerarquía  

Hay distintos tipos de topologías de jerarquía:  

- Más sencilla: un único sitio primario independiente.  

- Más compleja: un grupo de sitios primarios y secundarios conectados a un sitio de administración central en el sitio de primer nivel de la jerarquía.  

El factor decisivo sobre el tipo y el número de sitios que use en una jerarquía suele depender del número y el tipo de dispositivos que tendrá que admitir.   

### <a name="standalone-primary-site"></a>Sitio primario independiente

Use un sitio primario independiente cuando pueda admitir la administración de todos los dispositivos y usuarios. Para obtener más información, vea [Números de tamaño y escala](../configs/size-and-scale-numbers.md). Esta topología también da buenos resultados cuando las ubicaciones geográficas de su compañía pueden servirse mediante un único sitio primario. Para facilitar la administración del tráfico de red, use varios puntos de administración en grupos de límites y una infraestructura de contenido planeada detenidamente. Para obtener más información, vea [Configurar grupos de límites](../../servers/deploy/configure/boundary-groups.md) y [Conceptos fundamentales para la administración de contenidos](fundamental-concepts-for-content-management.md).  

Esta topología proporciona las ventajas siguientes:  

- Simplificación del trabajo administrativo  

- Simplificación de la asignación del sitio cliente y la detección de servicios y recursos disponibles.  

- Eliminación de posibles retrasos introducidos por la replicación de base de datos entre sitios.  

- Opción de expandir un sitio primario independiente a una jerarquía de mayor tamaño con un sitio de administración central. Esta opción le permite instalar después nuevos sitios primarios para expandir la escala de su implementación.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Sitio de administración central con uno o varios sitios primarios secundarios 

Use esta topología cuando necesite que más de un sitio primario admita la administración de todos sus dispositivos y usuarios. Es obligatorio cuando necesita usar más de un solo sitio primario. 

Esta topología proporciona las ventajas siguientes:  

- Admite hasta 25 sitios primarios, lo que le permite extender la escala de la jerarquía.    

- Siempre usa el sitio de administración central, excepto si reinstala los sitios. Esta opción es permanente. No se puede desasociar un sitio primario secundario para convertirlo en un sitio primario independiente.  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a> Determinar cuándo usar un sitio de administración central  

Utilice un sitio de administración central para configurar toda la jerarquía y supervisar todos los sitios y objetos de la jerarquía. Este tipo de sitio no administra directamente los clientes. Coordina la replicación de datos de sitio a sitio, lo que incluye la configuración de sitios y clientes en toda la jerarquía.  

La siguiente información puede ayudarle a decidir cuándo instalar un sitio de administración central:  

- El sitio de administración central es el sitio de nivel superior de una jerarquía.  

- Al configurar una jerarquía que tenga más de un sitio primario, instale un sitio de administración central.  

     - Si necesita de inmediato dos o más sitios primarios, instale primero el sitio de administración central.  

     - Si ya tiene un sitio primario y, después, quiere instalar un sitio de administración central, [expanda el sitio primario independiente](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) para instalar el sitio de administración central.  

- El sitio de administración central admite sólo sitios primarios como sitios secundarios.  

- El sitio de administración central no puede tener clientes asignados.  

- El sitio de administración central no es compatible con roles de sistema de sitio que admitan directamente los clientes, como puntos de administración y puntos de distribución.  

- Administre todos los clientes de la jerarquía y realice todas las tareas de administración de sitios desde la consola de Configuration Manager que esté conectada al sitio de administración central. Entre estas tareas, se incluye la instalación de puntos de administración u otros roles de sistema de sitio en sitios primarios secundarios o en sitios secundarios.  

- Si usa un sitio de administración central, será el único lugar donde verá datos de sitio de todos los sitios de la jerarquía. Estos datos incluyen información como mensajes de estado y datos de inventario.  

- Configure operaciones de detección en toda la jerarquía desde el sitio de administración central. Desde el sitio de administración central, asigne métodos de detección para que se ejecuten en sitios primarios individuales.  

- Para administrar la seguridad en toda la jerarquía, asigne diferentes roles de seguridad, ámbitos de seguridad y colecciones a los usuarios administrativos. Estas configuraciones se aplican en cada sitio de la jerarquía.  

- Configure la replicación para controlar la comunicación entre los sitios en la jerarquía. Programe la replicación de base de datos para los datos de sitios y administre el ancho de banda para la transferencia de datos basados en archivos entre sitios.  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a> Determinar cuándo usar un sitio primario  

Utilice los sitios primarios para administrar clientes. Instale un sitio primario como un sitio secundario debajo de un sitio de administración central, o bien como el primer sitio de una nueva jerarquía. Un sitio primario que es el primer sitio donde una jerarquía crea un sitio primario independiente. Tanto los sitios primarios secundarios como los sitios primarios independientes admiten los sitios secundarios.  

Puede agregar más sitios primarios por los motivos siguientes:  

- Para incrementar el número de dispositivos, use una única jerarquía.  

- Para satisfacer los requisitos de administración organizativa. Por ejemplo, puede instalar un sitio primario en una ubicación remota para administrar la transferencia de contenido de implementación a través de una red de ancho de banda bajo.  

     - En su lugar, puede usar opciones para limitar el ancho de banda de red al transferir datos a un punto de distribución. Esta capacidad de administración de contenido puede sustituir la necesidad de instalar sitios adicionales.  


La siguiente información puede resultarle útil para decidir cuándo instalar un sitio primario:  

- Un sitio primario puede ser un sitio primario independiente o un sitio primario secundario en una jerarquía más amplia. Si un sitio primario es miembro de una jerarquía con un sitio de administración central, los sitios utilizan la replicación de base de datos para replicar datos entre sitios. Excepto si necesita admitir más clientes y dispositivos de los que admite un único sitio primario, puede instalar un sitio primario independiente. Después de instalar un sitio primario independiente, expándalo si es necesario en el futuro para que dependa de un nuevo sitio de administración central con el fin de escalar verticalmente su implementación.  

- Un sitio primario admite un solo sitio de administración central como sitio principal.  

- Un sitio primario solo admite sitios secundarios (uno o varios).  

- Los sitios primarios son responsables de procesar todos los datos de cliente de los clientes asignados.  

- Los sitios primarios usan replicación de base de datos para comunicarse directamente con su sitio de administración central. Este comportamiento se configura automáticamente cuando se instala un nuevo sitio.  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a> Determinar cuándo usar un sitio secundario  

Utilice sitios secundarios para administrar la transferencia de contenido de implementación y datos de cliente a través de redes de ancho de banda bajo.  

Es posible administrar un sitio secundario desde un sitio de administración central o desde el sitio primario principal directo del sitio secundario. Los sitios secundarios están asociados a un sitio primario. No se pueden mover a otro sitio principal sin desinstalarlos y, después, reinstalarlos como sitios secundarios por debajo del nuevo sitio primario.

Sin embargo, es posible distribuir contenido entre dos sitios secundarios del mismo nivel para facilitar la administración de la replicación basada en archivos de contenido de implementación. Para transferir datos de cliente a un sitio primario, el sitio secundario utiliza replicación basada en archivos. Un sitio secundario también utiliza replicación de base de datos para comunicarse con su sitio primario principal.  

Considere la posibilidad de instalar un sitio secundario si se cumple alguna de las condiciones siguientes:  

- No se necesita un punto local de conectividad para un usuario administrativo.  

- Necesita administrar la transferencia de contenido de implementación a los sitios en posiciones inferiores de la jerarquía.  

- Necesita administrar la información de los clientes que se envía a sitios en posiciones más altas de la jerarquía.  

Si no quiere instalar un sitio secundario y tiene clientes en ubicaciones remotas, tenga en cuenta las opciones siguientes:  

- Use tecnologías de punto a punto, como Windows BranchCache.  

- Habilite puntos de distribución para controlar y programar el ancho de banda.   

Use estas opciones de administración de contenidos con o sin sitios secundarios. Permiten reducir el tamaño de su infraestructura de Configuration Manager. Para obtener más información sobre las opciones de administración de contenidos en Configuration Manager, vea [Determinar cuándo usar las opciones de administración de contenidos](#BKMK_ChooseSecondaryorDP).  


La siguiente información puede ayudarle a decidir cuándo instalar un sitio secundario:  

- Si no hay disponible una instancia local de SQL Server, los servidores de sitios secundarios instalarán automáticamente SQL Server Express durante la instalación del sitio.  

- La instalación del sitio secundario se inicia desde la consola de Configuration Manager, en lugar de ejecutar la configuración directamente en un equipo.  

- Los sitios secundarios usan un subconjunto de la información en la base de datos del sitio. Este comportamiento reduce la cantidad de datos que SQL replica entre el sitio primario principal y el sitio secundario.  

- Los sitios secundarios admiten la distribución de contenido basado en archivos a otros sitios secundarios que tienen un sitio primario principal común.  

- Las instalaciones de sitios secundarios instalarán automáticamente el punto de administración y los roles de sistema de sitio del punto de distribución en el servidor de sitio secundario.  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a> Determinar cuándo usar las opciones de administración de contenido  

Si tiene clientes en ubicaciones de red remotas, considere el uso de una o varias opciones de administración de contenido en lugar de un sitio primario o secundario. Con frecuencia, las opciones siguientes eliminan la necesidad de instalar un sitio:  

- Optimización de entrega para Windows 10  

- Caché del mismo nivel de Configuration Manager  

- Windows BranchCache  

- Configurar puntos de distribución para controlar el ancho de banda  

- Copiar de forma manual contenido en puntos de distribución (preconfigurar contenido)  


Si se produce alguna de las siguientes condiciones, puede implementar un punto de distribución en lugar de instalar otro sitio:  

- Su ancho de banda de red es suficiente para que los equipos cliente en la ubicación remota se comuniquen con un punto de administración en el sitio primario. Los clientes se comunican con un punto de administración para descargar la directiva de cliente, enviar inventarios, enviar informes de estado y enviar información de detección.  

- El Servicio de transferencia inteligente en segundo plano (BITS) no ofrece un control de ancho de banda suficiente para sus requisitos de red.  

Para obtener más información sobre las opciones de administración de contenidos en Configuration Manager, vea [Conceptos fundamentales para la administración de contenido](fundamental-concepts-for-content-management.md).  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a> Más allá de la topología de la jerarquía  

Además de su topología de jerarquía inicial, tenga en cuenta las preguntas siguientes:  

- ¿Qué roles de sistema de sitio proporcionan servicios o funciones desde distintos sitios en la jerarquía?  

- ¿Cómo administrará las configuraciones de toda la jerarquía y las funciones en su infraestructura?  


Las siguientes consideraciones comunes se describen en artículos separados. Esta información es importante y puede afectar al diseño de su jerarquía:  

- Al prepararse para [administrar equipos y dispositivos](../../clients/manage/manage-clients.md), tenga en cuenta si los dispositivos se encuentran en un entorno local o en la nube, o bien si se incluyen dispositivos que pertenecen al usuario (BYOD). Además, tenga en cuenta cómo administrará los dispositivos que admiten varias opciones de administración. Por ejemplo, administre dispositivos con Windows 10 con Configuration Manager o mediante la integración con Microsoft Intune. Para obtener más información, vea [Seleccionar una solución de administración de dispositivos](../choose-a-device-management-solution.md).  

- Obtenga información sobre cómo su infraestructura de red disponible podría afectar al flujo de datos entre ubicaciones remotas. Para obtener más información, vea [Preparar el entorno de red](../network/configure-firewalls-ports-domains.md). Además, tenga en cuenta la ubicación geográfica de los usuarios y dispositivos, y si pueden acceder a su infraestructura mediante la red local o Internet.  

- Planee una infraestructura de contenido para distribuir de manera eficiente el contenido que quiera implementar en los dispositivos que administre. Este contenido pueden ser aplicaciones, actualizaciones de software o sistemas operativos. Para obtener más información, consulte [Manage content and content infrastructure](../../servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración del contenido y de la infraestructura de contenido).  

- Determine las [características y funciones de Configuration Manager](../changes/features-and-capabilities.md) que tiene previsto usar. Diferentes características necesitan infraestructuras de Windows o roles de sistema de sitio distintos. En una jerarquía de varios sitios, decida dónde implementarlos para usar de la forma más eficiente la red y los recursos de servidor.  

- Tenga en cuenta la seguridad de los datos y dispositivos, incluido el uso de una infraestructura de clave pública (PKI). Para obtener más información, vea [Requisitos de certificados PKI](../network/pki-certificate-requirements.md).  


Revise los artículos siguientes para obtener información sobre configuraciones específicas de sitios:  

- [Planear el proveedor de SMS](plan-for-the-sms-provider.md)  

- [Planear la base de datos del sitio](plan-for-the-site-database.md)  

- [Planear servidores de sistema de sitio y roles de sistema de sitio](plan-for-site-system-servers-and-site-system-roles.md)  

- [Planear la seguridad](../security/plan-for-security.md)  

- [Managing network bandwidth](manage-network-bandwidth.md) (Administrar el ancho de banda de red) cuando se implementa contenido dentro de un sitio  


Configuraciones que abarcan sitios y jerarquías  

- [Opciones de alta disponibilidad](../../servers/deploy/configure/high-availability-options.md) para sitios y jerarquías

- [Extender el esquema de Active Directory](../network/extend-the-active-directory-schema.md) y configurar sitios para [publicar datos de sitios](../../servers/deploy/configure/publish-site-data.md)  

- [Transferencias de datos entre sitios](data-transfers-between-sites.md)  

- [Aspectos básicos de la administración basada en roles](../../understand/fundamentals-of-role-based-administration.md)  

- [Administración de clientes en Internet](../../clients/manage/manage-clients-internet.md)  

