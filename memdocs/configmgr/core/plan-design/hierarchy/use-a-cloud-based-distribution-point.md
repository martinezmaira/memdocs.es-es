---
title: Punto de distribución de nube
titleSuffix: Configuration Manager
description: Planee y diseñe la distribución de contenido de software mediante Microsoft Azure con puntos de distribución de nube en Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7a14b79a9e7fd91b6470836b4271a669725065bd
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771168"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Usar un punto de distribución de nube en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

> [!Important]  
> Ha cambiado la implementación para compartir contenido de Azure. Use una puerta de enlace de administración de la nube habilitada para el contenido al habilitar la opción de **Permitir a CMG funcionar como un punto de distribución de nube y servir contenido desde Azure Storage**. Para obtener más información, vea [Modify a CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg) (Modificar una instancia de CMG).
>
> No podrá crear un punto de distribución en la nube tradicional en el futuro. Para más información, consulte [Características en desuso y eliminadas](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Un punto de distribución de nube es un punto de distribución de Configuration Manager que se hospeda como plataforma como servicio (PaaS) en Microsoft Azure. El servicio admite los escenarios siguientes:  

- Proporcionar contenido de software a clientes basados en Internet sin una infraestructura local adicional.  

- Habilitar su sistema de distribución de contenido para la nube.  

- Reducir la necesidad de usar puntos de distribución tradicionales.  

En este artículo, obtendrá información sobre el punto de distribución de nube, cómo planear su uso y cómo diseñar su implementación. Se incluyen las secciones siguientes:

- [Características y ventajas](#bkmk_features)
- [Diseño de topología](#bkmk_topology)
- [Requirements](#bkmk_requirements)
- [Especificaciones](#bkmk_spec)
- [Costo](#bkmk_cost)
- [Rendimiento y escalabilidad](#bkmk_perf)
- [Puertos y flujo de datos](#bkmk_dataflow)
- [Certificados](#bkmk_certs)
- [Preguntas más frecuentes](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a> Características y ventajas

### <a name="features"></a>Funciones

Los puntos de distribución de nube admiten varias características que también se ofrecen en puntos de distribución locales:  

- Se pueden administrar puntos de distribución de nube individualmente o como miembros de grupos de puntos de distribución.  

- Usan un punto de distribución de nube como ubicación de contenido de reserva.  

- Son compatibles con clientes basados en intranet y en Internet.  

### <a name="benefits"></a>Ventajas

Un punto de distribución de nube proporciona las siguientes ventajas adicionales:  

- El sitio cifra el contenido antes de enviarlo al punto de distribución de nube en Azure.  

- Para cumplir con las demandas variables de solicitudes de contenido que realicen los clientes, escale de forma manual el servicio en la nube en Azure. Para realizar esta acción, no es necesario que instale ni aprovisione puntos de distribución adicionales en Configuration Manager.  

- Admite la descarga de contenido de clientes configurados para otras tecnologías de contenido, como Windows BranchCache y proveedores de contenido alternativos.  

- A partir de la versión 1806, use puntos de distribución de nube como ubicaciones de origen para los puntos de distribución de extracción.  


## <a name="topology-design"></a><a name="bkmk_topology"></a> Diseño de topología

La implementación y el funcionamiento del punto de distribución de nube están formados por los componentes siguientes:  

- Un **servicio en la nube** en Azure. El sitio distribuye contenido a este servicio, que lo almacena en el almacenamiento en la nube de Azure. El punto de administración proporciona a los clientes esta ubicación de contenido en la lista de orígenes disponibles, según corresponda.  

- El rol de sistema de sitio del **punto de administración** atiende las solicitudes de cliente de manera normal.  

    - Los clientes locales suelen usar un punto de administración local.  

    - Los clientes basados en Internet pueden usar una [instancia de Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) o un [punto de administración basado en Internet](../../clients/manage/plan-internet-based-client-management.md).  

- El punto de distribución de nube usa un servicio web **HTTPS basado en certificados** para proteger la comunicación de red con los clientes. Los clientes tienen que confiar en este certificado.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
A partir de la versión 1806, cree un punto de distribución de nube con una **implementación de Azure Resource Manager**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) es una moderna plataforma para administrar todos los recursos de la solución como una única entidad, denominada [grupo de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Al implementar un punto de distribución de nube con Azure Resource Manager, el sitio usa Azure Active Directory (Azure AD) para autenticar y crear los recursos necesarios en la nube. Esta implementación modernizada no requiere el certificado de administración de Azure clásico.  

> [!Note]  
> Esta característica no habilita la compatibilidad de los proveedores de servicios en la nube (CSP) de Azure. La implementación de puntos de distribución de nube con Azure Resource Manager continúa usando el servicio en la nube clásico, que no es compatible con los proveedores de servicios en la nube. Para obtener más información, consulte [Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services) (Servicios de Azure disponibles en los proveedores de servicios en la nube de Azure).  

A partir de la versión 1902 de Configuration Manager, Azure Resource Manager es el único mecanismo de implementación para instancias nuevas del punto de distribución de nube. Las implementaciones existentes seguirán funcionando.<!-- 3605704 -->

En la versión 1810 y versiones anteriores de Configuration Manager, el asistente del punto de distribución de nube seguirá proporcionando la opción de una **implementación del servicio clásico** mediante un certificado de administración de Azure. Para simplificar la implementación y administración de recursos, use el modelo de implementación de Azure Resource Manager para todos los puntos de distribución de nube nuevos. Si es posible, vuelva a implementar los puntos de distribución de nube a través de Resource Manager.

> [!Important]  
> A partir de la versión 1810, la implementación del servicio clásico de Azure ya no se usa en Configuration Manager. Esta versión es la última que admite la creación de estas implementaciones de Azure. Esta funcionalidad se quitará en una edición futura de Configuration Manager.<!--SCCMDocs-pr issue #2993-->  

Configuration Manager no migra los puntos de distribución de nube clásicos existentes al modelo de implementación de Azure Resource Manager. Cree nuevos puntos de distribución de nube con las implementaciones de Azure Resource Manager y luego quite los puntos de distribución de nube clásicos.

### <a name="hierarchy-design"></a>Diseño de jerarquía

La ubicación donde creará el punto de distribución de nube depende de los clientes que necesiten acceder al contenido. A partir de la versión 1806, hay tres tipos de puntos de distribución de nube:  

- Implementación de Azure Resource Manager: cree este tipo en un sitio primario o en el sitio de administración central.  

- Implementación de servicio clásico : cree este tipo solo en un sitio primario.  

- La instancia de Cloud Management Gateway también puede servir contenido a los clientes. Esta funcionalidad reduce los certificados necesarios y el costo de máquinas virtuales de Azure. Para obtener más información, consulte [Plan for cloud management gateway (Plan para la puerta de enlace de administración en la nube)](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!--1358651-->  

Para determinar si se incluyen los puntos de distribución de nube en los grupos de límites, tenga en cuenta los comportamientos siguientes:  

- Los clientes basados en Internet no usan grupos de límites. Solo usan puntos de distribución accesibles desde Internet o puntos de distribución de nube. Si solo usa puntos de distribución de nube para dar servicio a estos tipos de clientes, no necesita incluirlos en grupos de límites.  

- Si quiere que los clientes de la red interna usen un punto de distribución de nube, necesita estar en el mismo grupo de límites que los clientes. Los clientes dan prioridad a los últimos puntos de distribución de nube de su lista de orígenes de contenido, ya que existe un costo asociado con la descarga de contenido desde Azure. Por lo tanto, un punto de distribución de nube suele usarse como un origen de reserva para los clientes basados en intranet. Si quiere usar un diseño que dé prioridad a la nube, diseñe los grupos de límites para adaptarse a este requisito empresarial. Para obtener más información, vea [Configuración de grupos de límites](../../servers/deploy/configure/boundary-groups.md).  

Aunque instale puntos de distribución de nube en regiones específicas de Azure, los clientes no conocen las regiones de Azure. Seleccionan de forma aleatoria un punto de distribución de nube. Si instala puntos de distribución de nube en varias regiones y un cliente recibe más de uno en la lista de ubicaciones de contenido, puede que el cliente no use un punto de distribución de nube de la misma región de Azure.  

### <a name="backup-and-recovery"></a>Copia de seguridad y recuperación  

Al usar un punto de distribución de nube en su jerarquía, use esta información para planear las operaciones de copia de seguridad y recuperación:  

- Si usa la tarea de mantenimiento **Copia de seguridad del servidor del sitio**, Configuration Manager incluye de forma automática las configuraciones para el punto de distribución de nube.  

- Realice una copia de seguridad del certificado de autenticación de servidor. Si usa una implementación clásica del servicio en Azure, realice también una copia de seguridad del certificado de administración de Azure. Al restaurar el sitio primario de Configuration Manager en otro servidor, tendrá que volver a importar los certificados.  


## <a name="requirements"></a><a name="bkmk_requirements"></a> Requisitos

- Para hospedar el servicio, necesita una **suscripción de Azure**.  

    - Es necesario que un **administrador de Azure** participe en la creación inicial de determinados componentes, en función del diseño. Este rol no necesita permisos en Configuration Manager.  

- El servidor de sitio necesita **acceso a Internet** para implementar y administrar el servicio en la nube.  

- Si usa el método de implementación de **Azure Resource Manager**, integre Configuration Manager con [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) para **Cloud Management**. La *detección de usuarios* de Azure AD no es necesaria.  

- Un **certificado de autenticación de servidor**. Para obtener más información, vea la sección [Certificados](#bkmk_certs) a continuación.  

    - Para reducir la complejidad, use un proveedor de certificados públicos para el certificado de autenticación del servidor. Al hacerlo, también necesita un **alias de CNAME de DNS** para que los clientes puedan resolver el nombre del servicio en la nube.  

- En la versión 1810 o anteriores de Configuration Manager, si se usa el método de implementación clásico de Azure, necesitará un **certificado de automatización de Azure**. Para obtener más información, vea la sección [Certificados](#bkmk_certs) a continuación.  

    > [!TIP]  
    > A partir de la versión 1806 de Configuration Manager, le recomendamos que use el modelo de implementación de **Azure Resource Manager**. No necesita este certificado de administración.  
    >
    > El método de implementación clásico está en desuso desde la versión 1810.  

- Establezca la opción del cliente **Permitir el acceso a puntos de distribución de nube** en **Sí** en el grupo **Cloud Services**. De forma predeterminada, este valor está establecido como **No**.  

- Los dispositivos cliente necesitan **conectividad a Internet** y tienen que usar **IPv4**.  


## <a name="specifications"></a><a name="bkmk_spec"></a> Especificaciones

- El punto de distribución de nube es compatible con todas las versiones de Windows que se indican en [Sistemas operativos compatibles de clientes y dispositivos](../configs/supported-operating-systems-for-clients-and-devices.md).  

- Un administrador distribuye los siguientes tipos de contenido de software admitido:  
  - Aplicaciones
  - Paquetes
  - Paquetes de actualización del sistema operativo
  - Actualizaciones de software de terceros  

    > [!Important]  
    > - Cuando la consola de Configuration Manager no impide la distribución de actualizaciones de software de Microsoft en un punto de distribución de nube, pagará costos de Azure para almacenar el contenido que los clientes no usen. Los clientes basados en Internet siempre obtienen el contenido de actualización de software de Microsoft del servicio en la nube de Microsoft Update. No distribuya actualizaciones de software de Microsoft en un punto de distribución de nube.
    > - Cuando se usa CMG para el almacenamiento de contenido, el contenido de las actualizaciones de terceros no se descarga en los clientes si está habilitada la [configuración de cliente](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Descarga de contenido diferencial cuando esté disponible**. <!--6598587--> 

- A partir de la versión 1806, configure un punto de distribución de extracción para que use un punto de distribución de nube como origen. Para más información, consulte [Información sobre los puntos de distribución de origen](use-a-pull-distribution-point.md#about-source-distribution-points).<!--1321554-->  

### <a name="deployment-settings"></a>Configuración de implementación

- Al implementar una secuencia de tareas con la opción **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas**, en el punto de administración no se incluye un punto de distribución de nube como una ubicación de contenido. Implemente la secuencia de tareas con la opción **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas** para que los clientes usen un punto de distribución de nube.  

- Un punto de distribución de nube no admite implementaciones de paquetes con la opción **Ejecutar programa desde el punto de distribución.** Use la opción de implementación **Descargar contenido desde el punto de distribución y ejecutar localmente**.  

### <a name="limitations"></a>Limitaciones  

- No se puede usar un punto de distribución de nube con implementaciones habilitadas para un entorno PXE o implementaciones de multidifusión.  

- Un punto de distribución de nube no admite las aplicaciones de streaming de App-V.  

- No se puede [preconfigurar contenido](manage-network-bandwidth.md#BKMK_PrestagingContent) en un punto de distribución de nube. El Administrador de distribución del sitio primario que administra el punto de distribución de nube transfiere todo el contenido al punto de distribución.  

- No se puede configurar un punto de distribución de nube como un punto de distribución de extracción.  


## <a name="cost"></a><a name="bkmk_cost"></a> Costo

<!--501018-->
> [!IMPORTANT]  
> La siguiente información sobre los costos se indica solo con fines de estimación. Su entorno puede tener otras variables que afecten al costo general del uso del punto de distribución de nube.  

Configuration Manager incluye las opciones siguientes para ayudar a controlar los costos y supervisar el acceso a datos:  

- Puede controlar y supervisar la cantidad de contenido que se almacena en un servicio en la nube. Para obtener más información, vea [Supervisar puntos de distribución de nube](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Puede configurar Configuration Manager para que le avise cuando los umbrales de las descargas de cliente alcancen o superen el límite mensual. Para obtener más información, vea [Alertas de umbral de transferencia de datos](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts).

- Para reducir el número de transferencias de datos desde puntos de distribución de nube que realizan los clientes, use una de las siguientes tecnologías de caché de sistemas del mismo nivel:  
  - Caché del mismo nivel de Configuration Manager
  - Windows BranchCache
  - Optimización de entrega de Windows 10  

    Para obtener más información, consulte [Fundamental concepts for content management](fundamental-concepts-for-content-management.md) (Conceptos fundamentales de la administración de contenido).  

### <a name="components"></a>Componentes

Un punto de distribución de nube usa los siguientes componentes de Azure, que conllevan cargos en la cuenta de suscripción de Azure:  

> [!Tip]  
> A partir de la versión 1806, la instancia de Cloud Management Gateway también puede servir contenido a los clientes. Esta función reduce el costo al consolidar las VM de Azure. Para obtener más información, vea [Costo de Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost).  

#### <a name="virtual-machine"></a>Máquina virtual

- El punto de distribución de nube usa Azure Cloud Services como plataforma como servicio (PaaS). Este servicio usa máquinas virtuales (VM) que conllevan costos de proceso.  

- Cada servicio de punto de distribución de nube usa dos VM estándar A0.  

- Vea la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) para determinar los costos potenciales.

    > [!NOTE]  
    > Los costos de máquina virtual varían según la región.

#### <a name="outbound-data-transfer"></a>Transferencia de datos de salida

- Todos los flujos de datos enviados a Azure son gratuitos (entrada o carga). La distribución de contenido desde el sitio al punto de distribución de nube se realiza mediante la carga en Azure.  

- Los cargos se basan en los datos que fluyen fuera de Azure (salida o descarga). Los flujos de datos del punto de distribución de nube desde Azure están formados por el contenido de software que descargan los clientes.  

- Para obtener más información, vea [Supervisar puntos de distribución de nube](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Vea [Detalles de precios de ancho de banda de Azure](https://azure.microsoft.com/pricing/details/bandwidth/) para determinar los costos potenciales. Los precios de la transferencia de datos se organizan por plan de tarifa. Cuanto más uso haga, menos pagará por gigabyte.  

#### <a name="content-storage"></a>Almacenamiento de contenido

- Los clientes basados en Internet obtienen contenido de actualizaciones de software de Microsoft desde el servicio en la nube de Microsoft Update sin costo adicional. No distribuya paquetes de implementación de actualizaciones de software con actualizaciones de software de Microsoft en un punto de distribución de nube. De lo contrario, se producirían costos de almacenamiento de datos por el contenido que los clientes no usen.  

- Los puntos de distribución de nube usan el siguiente almacenamiento de blobs estándar según el modelo de implementación:  

    - Una implementación de Azure Resource Manager usa almacenamiento con redundancia local (LRS) de Azure. Este cambio reduce el costo de la cuenta de almacenamiento. La implementación clásica no usaba las características adicionales de GRS. Para más información, consulte [Almacenamiento con redundancia local](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

    - Una implementación clásica con la versión 1810 o anteriores de Configuration Manager usa el almacenamiento con redundancia geográfica (GRS) de Azure. Para obtener más información, vea [Almacenamiento con redundancia geográfica](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

#### <a name="other-costs"></a>Otros costos

- Todos los servicios en la nube tienen una dirección IP dinámica. Cada punto de distribución de nube usa una nueva dirección IP dinámica. Agregar VM adicionales por servicio en la nube no aumenta estas direcciones.  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a> Puertos y flujo de datos

Existen dos flujos de datos primarios para el punto de distribución de nube:  

- El servidor de sitio se conecta a Azure para configurar el servicio del punto de distribución de nube.  

- Un cliente se conecta al punto de distribución de nube para descargar contenido.  

### <a name="site-server-to-azure"></a>Servidor de sitio a Azure

No es necesario abrir ningún puerto de entrada a la red local. El servidor de sitio inicia todas las comunicaciones con Azure y el punto de distribución de nube para implementar, actualizar y administrar el servicio en la nube. El servidor de sitio debe crear conexiones salientes a la nube de Microsoft. Esta acción es equivalente a la instalación del rol del sistema de sitio de punto de distribución en un determinado sitio.  

### <a name="client-to-cloud-distribution-point"></a>Cliente a punto de distribución de nube

No es necesario abrir ningún puerto de entrada a la red local. Los clientes basados en Internet se comunican directamente con el servicio de Azure. Los clientes en la red interna que usan un punto de distribución de nube necesitan conectarse a la nube de Microsoft.

Para obtener más información sobre la prioridad de ubicación de contenido y conocer cuándo los clientes basados en intranet usan un punto de distribución de nube, vea [Prioridad de origen de contenido](fundamental-concepts-for-content-management.md#content-source-priority).

Cuando un cliente usa un punto de distribución de nube como una ubicación de contenido:  

1. El punto de administración proporciona al cliente un token de acceso, además de la lista de orígenes de contenido. Este token es válido durante 24 horas y permite al cliente acceder al punto de distribución de nube.  

2. El punto de administración responde a la solicitud de ubicación del cliente con el **FQDN del servicio** del punto de distribución de nube. Esta propiedad es la misma que el nombre común del certificado de autenticación de servidor.  

    Si usa su propio nombre de dominio (por ejemplo, WallaceFalls.contoso.com), el cliente primero intentará resolver este FQDN. Necesita un alias de CNAME en la configuración DNS accesible desde Internet de dominio para que los clientes puedan resolver el nombre del servicio de Azure. Por ejemplo, WallaceFalls.cloudapp.net.  

3. Después, el cliente resuelve el nombre del servicio de Azure (por ejemplo, WallaceFalls.cloudapp.net) a una dirección IP válida. La configuración DNS de Azure necesita procesar esta respuesta.  

4. El cliente se conectará al punto de distribución de nube. La carga de Azure equilibra la conexión a una de las instancias de VM. El cliente se autentica con el token de acceso.  

5. El punto de distribución de nube autentica el token de acceso del cliente y, después, proporciona al cliente la ubicación de contenido exacta en Azure Storage.  

6. Si el cliente confía en los puntos de distribución de nube del certificado de autenticación de servidor, se conectará a Azure Storage para descargar el contenido.


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a> Rendimiento y escalabilidad

<!--494872-->

Al igual que con cualquier diseño de punto de distribución, tenga en cuenta los factores siguientes:  

- Número de conexiones de cliente simultáneas
- El tamaño del contenido que descargan los clientes
- La duración de tiempo permitida para adaptarse a sus requisitos empresariales

Según su [diseño de topología](#bkmk_topology), si los clientes pueden usar más de un punto de distribución de nube para cualquier contenido específico, usarán aleatoriamente esos servicios en la nube. Si solo distribuye una parte específica del contenido a un único punto distribución de la nube y, además, un número elevado de clientes intenta descargar este contenido al mismo tiempo, esta actividad pondrá una mayor carga en ese único punto de distribución de nube. Al agregar un punto de distribución de nube, también se incluye un servicio independiente de Azure Storage. Para obtener más información sobre cómo el cliente se comunica con los componentes del punto de distribución de nube y descarga contenido, vea [Puertos y flujo de datos](#bkmk_dataflow).  

El punto de distribución de nube usa dos VM de Azure como el front-end para Azure Storage. Esta implementación predeterminada se adapta a las necesidades de la mayoría de los clientes. En algunas circunstancias extremas, con un gran número de conexiones de cliente simultáneas (por ejemplo, 150 000 clientes), la capacidad de procesamiento de las VM de Azure no será suficiente para las solicitudes de cliente. No se puede cambiar el tamaño de las VM de Azure usadas para el punto de distribución de nube. Aunque no se puede configurar el número de instancias de VM para el punto de distribución de nube el Configuration Manager, si es necesario, puede volver a configurar el servicio en la nube en Azure Portal. Puede agregar más instancias de VM de forma manual, o bien puede configurar el servicio para que se escale automáticamente.

> [!Important]  
> Al actualizar Configuration Manager, el sitio volverá a implementar el servicio en la nube. Si vuelve a configurar de forma manual el servicio en la nube en Azure Portal, el número de instancias se restablecerá al valor predeterminado de dos.  

El servicio Azure Storage admite 500 solicitudes por segundo para un único archivo. Las pruebas de rendimiento de un único punto de distribución de nube admiten la distribución de un único archivo de 100 MB a 50 000 clientes en un período de 24 horas.<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a> Certificados  

Según el diseño de punto de distribución de nube, necesitará uno o más certificados digitales.  

### <a name="general-information"></a>Información general

<!--SCCMDocs issue #779-->
Los certificados para puntos de distribución de nube admiten las siguientes configuraciones:  

- Longitud de clave de 4096 bits

- Certificados de la versión 3. Para obtener más información, consulte [Introducción a los certificados CNG](../network/cng-certificates-overview.md).  

- A partir de la versión 1802, al configurar Windows con la siguiente directiva: **Criptografía de sistema: usar algoritmos que cumplan la norma FIPS para cifrado, aplicación de algoritmo hash y firma**.  

- A partir de la versión 1802, es compatible con TLS 1.2. Para más información, vea [Referencia técnica de controles criptográficos](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities).  

### <a name="server-authentication-certificate"></a>Certificado de autenticación de servidor

*Este certificado es necesario para todas las implementaciones de puntos de distribución de nube.*

Para obtener más información, vea [Certificado de autenticación de servidor de CMG](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth) y las subsecciones siguientes, según sea necesario:  

- Certificado raíz de confianza de CMG para clientes
- Certificado de autenticación de servidor emitido por un proveedor público
- Certificado de autenticación de servidor emitido por una PKI de empresa

El punto de distribución de nube usa este tipo de certificado de la misma forma que una instancia de Cloud Management Gateway. Los clientes también necesitan confiar en este certificado. Para reducir la complejidad, Microsoft le recomienda que use un certificado emitido por un proveedor público.

Excepto si usa un certificado de comodín, no reutilice el mismo certificado. Cada instancia del punto de distribución de nube y de la instancia de Cloud Management Gateway necesita un único certificado de autenticación de servidor.

Para obtener más información sobre cómo crear este certificado a partir de una PKI, vea [Implementar el certificado del servicio para puntos de distribución de nube](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).  

### <a name="azure-management-certificate"></a>Certificado de administración de Azure

*Este certificado es necesario para las implementaciones del servicio clásico. No se necesita para las implementaciones de Azure Resource Manager.*

> [!Important]  
> A partir de la versión 1806 de Configuration Manager, le recomendamos que use el modelo de implementación de **Azure Resource Manager**. No necesita este certificado de administración.  
>
> El método de implementación clásico está en desuso desde la versión 1810.  
>
> A partir de la versión 1902 de Configuration Manager, Azure Resource Manager es el único mecanismo de implementación para instancias nuevas del punto de distribución de nube. Este certificado no es necesario en la versión 1902 o posteriores de Configuration Manager.<!-- 3605704 -->

Si se usa el método de implementación clásico con la versión 1810 o anteriores de Configuration Manager, necesitará un **certificado de administración de Azure**. Para obtener más información, vea la sección [Certificado de administración de Azure](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt) del artículo sobre certificados de instancias de Cloud Management Gateway. El servidor de sitio de Configuration Manager usa este certificado para autenticarse con Azure con el fin de crear y administrar la implementación clásica.  

Para reducir la complejidad, use el mismo certificado de administración de Azure para todas las implementaciones clásicas de puntos de distribución de nube e instancias de Cloud Management Gateway en todas las suscripciones de Azure y en todos los sitios de Configuration Manager.


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> Preguntas más frecuentes

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>¿Necesita un cliente un certificado para descargar contenido desde un punto de distribución de nube?

No se necesita un certificado de autenticación del cliente. El cliente no necesita confiar en el certificado de autenticación de servidor usado por el punto de distribución de nube. Si este certificado es emitido por un proveedor de certificados públicos, en la mayoría de los dispositivos Windows ya se incluyen certificados raíz de confianza para estos proveedores. Si ha emitido un certificado de autenticación de servidor desde el PKI de su organización, sus clientes necesitarán confiar en los certificados emitidos en toda la cadena. En esta cadena, se incluye la entidad de certificación raíz y todas las entidades de certificación intermedias. Según su diseño de PKI, este certificado puede introducir una mayor complejidad en la implementación del punto de distribución de nube. Para evitar esta complejidad, Microsoft le recomienda que use un proveedor de certificados públicos en el que ya confíen sus clientes.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>¿Pueden mis clientes locales usar un punto de distribución de nube?

Sí. Si quiere que los clientes de la red interna usen un punto de distribución de nube, necesita estar en el mismo grupo de límites que los clientes. Los clientes dan prioridad a los últimos puntos de distribución de nube de su lista de orígenes de contenido, ya que existe un costo asociado con la descarga de contenido desde Azure. Por lo tanto, un punto de distribución de nube suele usarse como un origen de reserva para los clientes basados en intranet. Si quiere usar un diseño que dé prioridad a la nube, diseñe sus grupos de límites en consecuencia. Para obtener más información, vea [Configuración de grupos de límites](../../servers/deploy/configure/boundary-groups.md).  

### <a name="do-i-need-azure-expressroute"></a>¿Necesito Microsoft Azure ExpressRoute?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) permite ampliar la red local a la nube de Microsoft. Para el punto de distribución de nube de Configuration Manager, no se necesita ExpressRoute ni otras conexiones de red virtual de este tipo.  

Si su organización usa ExpressRoute, aísle la suscripción de Azure para el punto de distribución de nube de la suscripción que use ExpressRoute. Esta configuración garantiza que el punto de distribución de nube no se conecte por error de esta forma.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>¿Es necesario mantener las máquinas virtuales de Azure?

No se requiere ningún mantenimiento. El diseño del punto de distribución de nube usa la plataforma como servicio (PaaS) de Azure. Mediante la suscripción que se proporciona, Configuration Manager crea las máquinas virtuales (VM) necesarias, el almacenamiento y las redes. Azure protege y actualiza la máquina virtual. Estas máquinas virtuales no forman parte del entorno local, como sucede con la infraestructura como servicio (IaaS). El punto de distribución de nube es una PaaS que extiende el entorno de Configuration Manager a la nube. Para obtener más información, vea [Ventajas de seguridad de un modelo de servicio en la nube de PaaS](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>¿Usa el punto de distribución de nube la red CDN de Azure?

La red de entrega de contenido de Azure (CDN) es una solución global para entregar rápidamente contenido con un ancho de banda elevado al almacenar en caché el contenido en nodos físicos repartidos de forma estratégica por todo el mundo. Para obtener más información, vea [¿Qué es la red CDN de Azure?](https://docs.microsoft.com/azure/cdn/cdn-overview)

El punto de distribución de nube de Configuration Manager no es compatible actualmente con la red CDN de Azure.


## <a name="next-steps"></a>Pasos siguientes

[Instalación de puntos de distribución de nube](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
