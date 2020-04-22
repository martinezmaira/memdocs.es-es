---
title: Conceptos básicos de administración de contenido
titleSuffix: Configuration Manager
description: Use herramientas y opciones en Configuration Manager para administrar el contenido que implemente.
ms.date: 12/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb3639a1d6734bf63b270e252c39862a33f13401
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697033"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Aspectos básicos de la administración de contenido en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager admite un sólido sistema de herramientas y opciones para administrar contenido de software. Todas las implementaciones de software (como aplicaciones, paquetes, actualizaciones de software e implementaciones del sistema operativo) necesitan contenido. Configuration Manager almacena el contenido en servidores de sitio y puntos de distribución. Este contenido requiere una gran cantidad de ancho de banda de red cuando se transfiere entre ubicaciones. Para planear y usar de manera eficaz la infraestructura de administración de contenidos, primero necesita comprender las opciones y configuraciones disponibles. Después, considere la posibilidad de cómo usarlas para ajustar mejor las necesidades de implementación de contenido y el entorno de red.  

> [!TIP]  
> Para obtener más información sobre el proceso de distribución de contenido y para buscar ayuda para diagnosticar y solucionar problemas generales de distribución de contenido, vea [Descripción y solución de problemas de distribución de contenido en Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Las secciones siguientes son conceptos clave para la administración de contenido. Cuando un concepto requiere información adicional o compleja, se proporcionan vínculos para dirigirle a ella.


## <a name="accounts-used-for-content-management"></a>Cuentas usadas para la administración de contenido

Las cuentas siguientes pueden usarse con la administración de contenido:  

### <a name="network-access-account"></a>Cuenta de acceso a la red

La usan los clientes para conectarse a un punto de distribución y acceder al contenido. De forma predeterminada, se intenta usar en primer lugar la cuenta de equipo.  

Esta cuenta también la usan los puntos de distribución de extracción para descargar el contenido de un punto de distribución de origen en un bosque remoto.  

A partir de la versión 1806, en algunos escenarios ya no se requiere una cuenta de acceso a la red. Puede habilitar el sitio para usar HTTP mejorado con la autenticación de Azure Active Directory.<!--1358228-->

Para obtener más información, vea [Cuenta de acceso a la red](accounts.md#network-access-account).

### <a name="package-access-account"></a>Cuenta de acceso de paquetes

De forma predeterminada, Configuration Manager concede acceso al contenido en un punto de distribución a los usuarios y los administradores de cuentas de acceso genéricas. Sin embargo, puede configurar permisos adicionales para restringir el acceso.

Para obtener más información, vea [Cuenta de acceso de paquetes](accounts.md#package-access-account).


## <a name="bandwidth-throttling-and-scheduling"></a>Programación y límite de ancho de banda

La programación y el límite son opciones que le ayudan a controlar cuándo se distribuye el contenido de un servidor de sitio en puntos de distribución. Estas funciones son similares a los controles de ancho de banda para la replicación basada en archivos de sitio a sitio, aunque no están directamente relacionadas.  

Para obtener más información, consulte [Administración del ancho de banda de red](manage-network-bandwidth.md).


## <a name="binary-differential-replication"></a>Replicación diferencial binaria

Configuration Manager usa la replicación diferencial binaria (BDR) para actualizar el contenido que ha distribuido anteriormente a otros sitios o a puntos de distribución remotos. Para admitir la reducción de uso de ancho de banda de BDR, instale la característica **Compresión diferencial remota** en los puntos de distribución. Para más información, vea [Requisitos previos de puntos de distribución](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq).

La BDR minimiza el ancho de banda de red que se usa para enviar actualizaciones de contenido distribuido. Solo se vuelve a enviar el contenido nuevo o que ha cambiado en lugar del conjunto completo de archivos de origen de contenido cada vez que se cambian esos archivos.  

Cuando se usa la BDR, Configuration Manager identifica los cambios que se producen en los archivos de origen de cada conjunto de contenido distribuido anteriormente.  

- Cuando cambian los archivos del contenido de origen, el sitio crea una versión incremental del contenido. Después, solamente replica los archivos que han cambiado en los sitios de destino y puntos de distribución. Se considera que un archivo ha cambiado cuando se ha cambiado el nombre, se ha movido o se ha modificado su contenido. Por ejemplo, si se sustituye un solo archivo de controlador de un paquete de controladores distribuido anteriormente a varios sitios, solo se replica el archivo de controlador cambiado.  

- Configuration Manager admite hasta cinco versiones incrementales de un conjunto de contenido antes de volver a enviar todo el conjunto de contenido. Después de la quinta actualización, el siguiente cambio en el conjunto de contenido hace que el sitio cree una versión del conjunto de contenido. Configuration Manager distribuye la nueva versión del conjunto de contenido para reemplazar el conjunto anterior y cualquiera de sus versiones incrementales. Después de distribuir el nuevo conjunto de contenido, la BDR replicará de nuevo los cambios incrementales siguientes en los archivos de origen.  

La BDR es compatible entre cada sitio principal y secundario de una jerarquía. Dentro de un sitio, la BDR es compatible entre el servidor de sitio y sus puntos de distribución normales. Pero los puntos de distribución de extracción y los puntos de distribución de nube no son compatibles con BDR para la transferencia de contenido. Los puntos de distribución de extracción admiten deltas de nivel de archivo, transferir archivos nuevos, pero no los bloques dentro de un archivo.

Las aplicaciones siempre usan la replicación diferencial binaria. BDR es opcional para los paquetes y no está habilitada de forma predeterminada. Para usar la BDR para paquetes, habilite esta funcionalidad en cada paquete. Seleccione la opción **Habilitar replicación diferencial binaria** al crear o modificar un paquete.


### <a name="bdr-or-delta-replication"></a>Replicación diferencial o BDR

<!-- SCCMDocs#1209 -->
En las listas siguientes se resumen las diferencias entre la *replicación diferencial binaria* (BDR) y la *replicación diferencial*.

#### <a name="summary-of-binary-differential-replication"></a>Resumen de la replicación diferencial binaria

- Término de Configuration Manager para **Compresión diferencial remota** de Windows
- Diferencias de nivel de *bloque*
- Siempre habilitada para las aplicaciones
- Opcional en los paquetes heredados
- Si ya existe un archivo en el punto de distribución y hay un cambio, el sitio usará BDR para replicar el cambio de nivel de bloque en lugar de todo el archivo.

#### <a name="summary-of-delta-replication"></a>Resumen de la replicación diferencial

- Diferencias de nivel de *archivo*
- Activada de forma predeterminada, no configurable
- Al cambiar un paquete, el sitio comprueba si hay cambios en los archivos individuales en lugar de en todo el paquete.
    - Si un archivo cambia, use BDR para realizar el trabajo
    - Si hay un nuevo archivo, cópielo


## <a name="peer-caching-technologies"></a>Tecnologías de caché de sistemas de mismo nivel

<!-- SCCMDocs#1044 -->

Configuration Manager admite varias opciones para administrar contenido entre dispositivos del mismo nivel en la misma red:

- [BranchCache](#branchcache)
- [Optimización de entrega](#delivery-optimization)
- [Caché del mismo nivel de Configuration Manager](#peer-cache)

Use la siguiente tabla para comparar las principales características de estas tecnologías:

| Característica  | Caché&nbsp;del mismo nivel  | Optimización&nbsp;de entrega  | BranchCache  |
|---------|---------|---------|---------|
| Entre subredes | Sí | Sí | No |
| Ancho de banda del umbral | Sí (BITS) | Sí (nativa) | Sí (BITS) |
| Contenido parcial | Sí | Sí | Sí |
| Control del tamaño en disco de la caché | Sí | Sí | Sí |
| Detección de origen del mismo nivel | Manual (configuración de cliente) | Automático | Automático |
| Detección de elemento del mismo nivel | Mediante el punto de administración con grupos de límites | Servicio en la nube de Optimización de entrega | Difusión |
| Generación de informes | Panel de orígenes de datos de cliente | Panel de orígenes de datos de cliente | Panel de orígenes de datos de cliente |
| Control del uso de WAN | Grupos de límites | GroupID de Optimización de entrega | Subred solamente |
| Contenido admitido | Todo el contenido de ConfigMgr | Actualizaciones de Windows, controladores, aplicaciones de la Tienda | Todo el contenido de ConfigMgr |
| Control de directivas | Configuración de agente de cliente | Configuración de agente de cliente (parcial) | Configuración de agente de cliente |

### <a name="recommendations"></a>Recomendaciones

- Administración moderna: si ya usa herramientas modernas como Intune, implemente Optimización de entrega.

- Configuration Manager y administración conjunta: use una combinación de caché del mismo nivel y Optimización de entrega. Use la caché del mismo nivel con puntos de distribución locales y Optimización de entrega para escenarios de nube.

- BranchCache existente implementado: use las tres tecnologías en paralelo. Use la caché del mismo nivel y Optimización de entrega para escenarios que no sean compatibles con BranchCache.


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) es una tecnología de Windows. Los clientes que admiten BranchCache y que han descargado una implementación configurada para BranchCache, después actúan como un origen de contenido para otros clientes habilitados para BranchCache.  

Por ejemplo, tiene un punto de distribución en el que se ejecuta Windows Server 2012 o una versión posterior, y está configurado como un servidor de BranchCache. Cuando el primer cliente habilitado para BranchCache solicita contenido desde este servidor, el cliente descarga el contenido y lo almacena en caché.  

- Después, ese cliente puede hacer que el contenido esté disponible para otros clientes habilitados para BranchCache en la misma subred, que también pueden almacenar en caché el contenido.  
- Otros clientes en la misma subred no tendrán que descargar el contenido desde el punto de distribución.  
- El contenido se distribuye entre varios clientes para futuras transferencias.  

Para obtener más información, vea [Compatibilidad con Windows BranchCache](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache).

## <a name="delivery-optimization"></a>Optimización de entrega

<!-- 1324696 -->
Los grupos de límites de Configuration Manager se usan para definir y regular la distribución de contenido a través de la red corporativa y en las oficinas remotas. La [optimización de distribución de Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) es una tecnología entre iguales basada en la nube para compartir contenido entre los dispositivos de Windows 10. Configure Optimización de entrega para usar los grupos de límites al compartir contenido entre iguales. La configuración de cliente aplica el identificador del grupo de límites como el identificador del grupo de optimización de entrega en el cliente. Cuando el cliente se comunica con el servicio en la nube de Optimización de entrega, utiliza este identificador para buscar elementos del mismo nivel con el contenido. Para obtener más información, vea la configuración de cliente de [optimización de distribución](../../clients/deploy/about-client-settings.md#delivery-optimization).

La Optimización de distribución es la tecnología recomendada para optimizar la distribución de actualizaciones de Windows 10 de archivos de instalación rápida para actualizaciones de calidad de Windows 10. A partir de la versión 1910 de Configuration Manager, el acceso al servicio en la nube Optimización de distribución a través de Internet es un requisito para usar su funcionalidad punto a punto. Para obtener información sobre los puntos de conexión de Internet necesarios, vea [Preguntas más frecuentes sobre Optimización de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). La optimización se puede usar para todas las actualizaciones de Windows. Para obtener más información, vea [Optimización de la distribución de actualizaciones de Windows 10](../../../sum/deploy-use/optimize-windows-10-update-delivery.md).


## <a name="microsoft-connected-cache"></a>Caché conectada de Microsoft

<!--3555764-->
A partir de la versión 1906, puede instalar un servidor de caché con conexión de Microsoft en los puntos de distribución. Al almacenar en caché este contenido de forma local, los clientes pueden beneficiarse de la característica de Optimización de entrega y, además, puede ayudar a proteger los vínculos WAN.

> [!NOTE]
> A partir de la versión 1910, esta característica se llama **caché con conexión de Microsoft**. Antes se conocía como “caché en la red de Optimización de distribución (DOINC)”.

Este servidor de caché actúa como una caché transparente a petición para el contenido descargado mediante la Optimización de entrega. Use la configuración de cliente para asegurarse de que este servidor se ofrezca únicamente a los miembros del grupo de límites de Configuration Manager local.

Esta caché es independiente del contenido del punto de distribución de Configuration Manager. Si elige la misma unidad que el rol de punto de distribución, el contenido se almacenará por separado.

Para más información, vea [Caché con conexión de Microsoft en Configuration Manager](microsoft-connected-cache.md).


## <a name="peer-cache"></a>Almacenamiento en caché del mismo nivel

El almacenamiento en caché del mismo nivel de cliente ayuda a administrar la implementación de contenido en los clientes en ubicaciones remotas. El almacenamiento en caché del mismo nivel es una solución integrada de Configuration Manager que permite a los clientes compartir contenido con otros clientes directamente desde su caché local.

Primero, implemente la configuración de cliente que habilite la caché de sistemas del mismo nivel en una colección. Después, los miembros de esa colección pueden actuar como un origen de contenido del mismo nivel para otros clientes del mismo grupo de límites.

A partir de la versión 1806, los orígenes de caché de sistemas del mismo nivel de clientes pueden dividir el contenido en varias partes. Estas partes reducen al mínimo la transferencia de red para usar menos WAN. El punto de administración proporciona un seguimiento más detallado de las partes de contenido e intenta eliminar más de una descarga del mismo contenido por grupo de límites.<!--1357346-->

Para obtener más información, vea [Caché del mismo nivel para clientes de Configuration Manager](client-peer-cache.md).


## <a name="windows-pe-peer-cache"></a>Almacenamiento en caché del mismo nivel de Windows PE

Al implementar un sistema operativo nuevo con Configuration Manager, los equipos que ejecutan la secuencia de tareas pueden usar el almacenamiento en caché del mismo nivel de Windows PE. Descargan el contenido desde un origen de almacenamiento en caché del mismo nivel en lugar de un punto de distribución. Este comportamiento minimiza el tráfico WAN en escenarios de sucursales donde no existe un punto de distribución local.

Para obtener más información, consulte [Almacenamiento en caché del mismo nivel de Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="windows-ledbat"></a>Windows LEDBAT

<!--1358112-->
Windows Low Extra Delay Background Transport (LEDBAT) es una característica de control de congestión de la red de Windows Server que permite administrar transferencias de red en segundo plano. En los puntos de distribución que se ejecuten en versiones compatibles de Windows Server, habilite una opción para ayudar a ajustar el tráfico de red. Después, los clientes solo usarán el ancho de banda de red cuando esté disponible.

Para obtener información general sobre Windows LEDBAT, vea la entrada de blog [Nuevos avances en transporte](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726).

Para obtener más información sobre cómo usar Windows LEDBAT con puntos de distribución de Configuration Manager, vea la opción **Ajustar la velocidad de descarga para usar el ancho de banda de red sin usar (Windows LEDBAT)** al [Configurar las opciones generales de un punto de distribución](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).


## <a name="client-locations"></a>Ubicaciones del cliente

A continuación se indican las ubicaciones desde las que los clientes tienen acceso a contenido:  

- **Intranet** (local):  

    - Los puntos de distribución pueden usar HTTP o HTTPS.  

    - Use un punto de distribución de nube como reserva solo cuando los puntos de distribución locales no estén disponibles.  

- **Internet**:  

    - Se necesitan puntos de distribución accesibles desde Internet para aceptar conexiones HTTPS.  

    - Puede usar un punto de distribución de nube o Cloud Management Gateway (CMG).  

        A partir de la versión 1806, una CMG también puede servir contenido a los clientes. Esta funcionalidad reduce los certificados necesarios y el costo de máquinas virtuales de Azure. Para obtener más información, vea [Modify a CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md) (Modificar una instancia de CMG).

- **Grupo de trabajo**:  

    - Requiere que los puntos de distribución acepten HTTPS.  

    - Se puede usar un punto de distribución de nube o una instancia de CMG.  


## <a name="content-source-priority"></a>Prioridad de origen de contenido

Cuando un cliente necesita contenido, realiza una solicitud de ubicación de contenido al punto de administración. El punto de administración devuelve una lista de ubicaciones de origen que son válidas para el contenido solicitado. Esta lista varía según el escenario específico, las tecnologías usadas, el diseño del sitio, los grupos de límites y la configuración de implementación. La lista siguiente contiene todas las posibles ubicaciones de orígenes de contenido que un cliente puede usar en el orden en que se prioricen:  

1. El punto de distribución en el mismo equipo que el cliente
2. Un origen del mismo nivel en la misma subred de red
3. Un punto de distribución en la misma subred de red
4. Un origen del mismo nivel en el mismo grupo de límites
5. Un punto de distribución en el grupo de límites actual
6. Un punto de distribución en un grupo de límites próximo configurado como reserva
7. Un punto de distribución en el grupo de límites del sitio predeterminado
8. El servicio en la nube de Windows Update
9. Un punto de distribución accesible desde Internet
10. Un punto de distribución de nube en Azure

> [!Note]  
> <!-- SCCMDocs#1607 -->Optimización de entrega no es aplicable a esta priorización de origen. En esta lista se indica cómo busca contenido el cliente de Configuration Manager. El Agente de Windows Update descarga contenido para Optimización de entrega. Si el Agente de Windows Update no encuentra el contenido, el cliente de Configuration Manager usará esta lista para buscarla.

## <a name="content-library"></a>Biblioteca de contenido

La biblioteca de contenido es el almacén de instancia única del contenido en Configuration Manager. Esta biblioteca reduce el tamaño total del contenido que se distribuye.  

- Obtenga más información sobre la [biblioteca de contenido](the-content-library.md).
- Utilice la herramienta [Content Library Cleanup Tool](content-library-cleanup-tool.md) para quitar contenido cuando deja de estar asociado con una aplicación.  


## <a name="distribution-points"></a>Puntos de distribución

Configuration Manager usa puntos de distribución para almacenar los archivos necesarios para la ejecución de software en los equipos cliente. Los clientes deben tener acceso al menos a un punto de distribución desde el cual puedan descargar los archivos del contenido que implemente.  

El punto de distribución básico (no especializado) suele denominarse punto de distribución estándar. Hay dos variaciones en el punto de distribución estándar que reciben atención especial:  

- **Punto de distribución de extracción**: variación de un punto de distribución donde el punto de distribución obtiene contenido de otro punto de distribución (un punto de distribución de origen). Este proceso es similar a la manera en que los clientes descargan contenido desde los puntos de distribución. Los puntos de distribución de extracción pueden ayudarle a evitar los cuellos de botella en el ancho de banda de red que se producen cuando el servidor de sitio debe distribuir directamente el contenido a cada punto de distribución. [Usar un punto de distribución de extracción](use-a-pull-distribution-point.md).

- **Punto de distribución de nube**: variación de un punto de distribución que se instala en Microsoft Azure. [Obtenga información sobre cómo usar un punto de distribución de nube](use-a-cloud-based-distribution-point.md).  

Los puntos de distribución estándar admiten una variedad de configuraciones y características:  

- Use controles como las **programaciones** o el **límite de ancho de banda** para ayudar a controlar esta transferencia.  

- Use otras opciones, incluido el **contenido preconfigurado** y los **puntos de distribución de extracción** para minimizar y controlar el consumo de red.  

- **BranchCache**, **Caché del mismo nivel** y **Optimización de distribución** son tecnologías punto a punto para reducir el ancho de banda de red que se usa al implementar contenido.  

- Existen otras configuraciones para implementaciones de sistema operativo, como **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** y **[Multidifusión](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** .  

- Opciones para **dispositivos móviles**  
  
Los puntos de distribución de extracción y de la nube admiten muchas de estas mismas configuraciones, pero tienen limitaciones específicas de cada variación de punto de distribución.  


## <a name="distribution-point-groups"></a>Grupos de puntos de distribución

Los grupos de puntos de distribución son agrupaciones lógicas de puntos de distribución que pueden simplificar la distribución de contenido.  

Para obtener más información, vea [Administrar grupos de puntos de distribución](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).


## <a name="distribution-point-priority"></a>Prioridad de puntos de distribución

El valor de prioridad del punto de distribución se basa en cuánto tiempo se tardó en transferir las implementaciones anteriores en ese punto de distribución.  

- Este valor es de ajuste automático. Se establece en cada punto de distribución para ayudar a Configuration Manager a transferir el contenido más rápidamente a más puntos de distribución.  

- Cuando se distribuye contenido a varios puntos de distribución al mismo tiempo, o bien a un grupo de puntos de distribución, el sitio envía primero el contenido al servidor con la prioridad más alta. Después, envía el mismo contenido a un punto de distribución con una prioridad inferior.  

- La prioridad del punto de distribución no reemplaza a la prioridad de distribución de los paquetes. La prioridad del paquete sigue siendo el factor decisivo de cuándo envía el sitio otro contenido.  

Por ejemplo, tiene un paquete con una prioridad de paquete alta. Lo distribuye a un servidor con una prioridad de punto de distribución baja. Este paquete de prioridad alta siempre se transferirá antes que un paquete con una prioridad más baja. La prioridad de paquete se aplica incluso si el sitio distribuye paquetes de prioridad más baja a servidores con prioridades de punto de distribución más altas.

La prioridad alta del paquete garantiza que Configuration Manager distribuye el contenido a los puntos de distribución antes de que envíe paquetes con una prioridad de distribución inferior.  

> [!NOTE]  
> Los puntos de distribución de extracción también usan el concepto de prioridad para ordenar la secuencia de los puntos de distribución de origen.  
>
> - La prioridad de punto de distribución de las transferencias de contenido al servidor es distinta de la prioridad que usan los puntos de distribución de extracción. Los puntos de distribución de extracción usan su prioridad cuando buscan contenido de un punto de distribución de origen.  
> - Para más información, vea [Usar un punto de distribución de extracción con System Center Configuration Manager](use-a-pull-distribution-point.md).  


## <a name="fallback"></a>Reserva

Varios aspectos han cambiado con la rama actual de Configuration Manager relacionados con la forma en que los clientes buscan un punto de distribución que tiene contenido, incluida la reserva.

Los clientes que no encuentran contenido en un punto de distribución asociado a su grupo de límites actual usan como reserva ubicaciones de origen de contenido asociadas a grupos de límites vecinos. Para que se use como reserva, un grupo de límites vecino debe tener una relación definida con el grupo de límites actual del cliente. Esta relación incluye un tiempo configurado que debe transcurrir para que un cliente que no encuentra contenido localmente incluya los orígenes de contenido del grupo de límites vecino como parte de su búsqueda.

Ya no se usa el concepto de puntos de distribución preferidos, y la opción para **permitir el uso de ubicaciones de origen de reserva para el contenido** ya no está disponible ni se aplica.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](../../servers/deploy/configure/boundary-groups.md).


## <a name="network-bandwidth"></a>Ancho de banda de red

Para administrar la cantidad de ancho de banda de red usada al distribuir contenido, puede usar las opciones siguientes:  

- **Contenido preconfigurado**: transferencia de contenido a un punto de distribución sin distribuir el contenido a través de la red.  

- **Programación y limitación**: configuraciones con las que podrá controlar cuándo y cómo se distribuye el contenido en puntos de distribución.  

Para obtener más información, consulte [Administración del ancho de banda de red](manage-network-bandwidth.md).


## <a name="network-connection-speed-to-content-source"></a>Velocidad de conexión de red con el origen de contenido

Varios aspectos han cambiado con la rama actual de Configuration Manager relacionados con la forma en que los clientes buscan un punto de distribución que tiene contenido. Estos cambios incluyen la velocidad de red a un origen de contenido.

Ya no se usan las velocidades de conexión de red que definen un punto de distribución como **rápido** o **lento**. En su lugar, cada sistema de sitio asociado a un grupo de límites se trata de la misma manera.

Para obtener más información, consulte [Boundary groups (Grupos de límites)](../../servers/deploy/configure/boundary-groups.md).


## <a name="on-demand-content-distribution"></a>Distribución de contenido a petición

La distribución de contenido a petición es una opción para las implementaciones de aplicaciones y paquetes individuales. Esta opción permite la distribución de contenido a petición en los servidores preferidos.  

- Para habilitar esta opción para una implementación, habilite: **Distribuir el contenido de este paquete en puntos de distribución preferidos**.  

- Cuando se habilita esta opción para una implementación y un cliente pide ese contenido, pero el contenido no está disponible en ninguno de los puntos de distribución preferidos del cliente, Configuration Manager distribuye automáticamente ese contenido en los puntos de distribución preferidos del cliente.  

- Aunque esto hace que Configuration Manager distribuya automáticamente el contenido a los puntos de distribución preferidos del cliente, este puede obtener el contenido desde otros puntos de distribución antes de que los puntos de distribución preferidos del cliente reciban la implementación. Cuando se produce este comportamiento, el contenido estará presente en ese punto de distribución para que lo use el próximo cliente que busque esa implementación.  

Para obtener más información, consulte [Boundary groups (Grupos de límites)](../../servers/deploy/configure/boundary-groups.md).


## <a name="package-transfer-manager"></a>Administrador de transferencia de paquetes

El administrador de transferencia de paquetes es el componente de servidor de sitio que transfiere contenido a puntos de distribución de otros equipos.  

Para obtener más información, vea [Administrador de transferencia de paquetes](package-transfer-manager.md).  


## <a name="prestage-content"></a>Preconfigurar el contenido

Preconfigurar el contenido es un proceso de transferencia de contenido a un punto de distribución sin distribuirlo a través de la red.  

Para obtener más información, consulte [Administración del ancho de banda de red](manage-network-bandwidth.md).
