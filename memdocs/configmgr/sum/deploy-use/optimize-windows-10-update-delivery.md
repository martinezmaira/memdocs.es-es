---
title: Optimización de la distribución de actualizaciones de Windows 10
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar Configuration Manager para administrar el contenido de actualización para estar al día con Windows 10.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f7edd05a7b1ce105e81fd4f594d95c9dfb45f472
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771367"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Optimización de la distribución de actualizaciones de Windows 10 con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para muchos clientes, una buena forma de obtener las actualizaciones mensuales de Windows 10 y de estar al día con ellas empieza por disponer de una buena estrategia de distribución de contenido mediante Configuration Manager. El tamaño de las actualizaciones de calidad mensuales puede ser motivo de preocupación para las grandes organizaciones. Existen algunas tecnologías disponibles que están diseñadas para ayudar a reducir la carga de red y el ancho de banda para optimizar la distribución de actualizaciones. En este artículo se explican estas tecnologías, se comparan y se ofrecen recomendaciones para ayudarle a decidir cuál utilizar.  
 
Windows 10 proporciona varios tipos de actualizaciones. Para obtener más información, consulte [Tipos de actualizaciones en Windows Update para empresas](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). Este artículo se centra en las actualizaciones de *calidad* de Windows 10 con Configuration Manager. 


## <a name="express-update-delivery"></a>Distribución de actualizaciones rápidas

Las descargas de actualizaciones de calidad de Windows 10 pueden ser grandes. Cada paquete contiene todas las revisiones publicadas anteriormente para garantizar la coherencia y la simplicidad. Microsoft ha logrado reducir el tamaño del contenido de las actualizaciones de Windows 10 que cada cliente descarga gracias a una característica rápida. La característica rápida la usan millones de dispositivos que extraen actualizaciones directamente del servicio Windows Update y reduce significativamente el tamaño de descarga. Esta ventaja también está disponible para clientes cuyos clientes no descargan directamente desde el servicio Windows Update. 

Configuration Manager agregó compatibilidad para los [archivos de instalación rápida](manage-express-installation-files-for-windows-10-updates.md) de las actualizaciones de calidad de Windows 10 en la versión 1702. Sin embargo, para una mejor experiencia, se recomienda usar la versión 1802 o posteriores de Configuration Manager. Para optimizar el rendimiento en las velocidades de descarga, también se recomienda usar la versión 1703 o posteriores de Windows 10. 

> [!NOTE]  
> El contenido de la versión rápida es considerablemente más grande que el de la versión del archivo completo. Un archivo de instalación rápida contiene todas las variaciones posibles de cada archivo que se pretende actualizar. Como resultado, la cantidad necesaria de espacio en disco aumenta para las actualizaciones en el origen del paquete de actualización y en los puntos de distribución cuando se habilita la compatibilidad con la característica rápida en Configuration Manager. Aunque el requisito de espacio en disco en los puntos de distribución aumenta, se reduce el tamaño del contenido que los clientes descargan desde estos puntos de distribución. Los clientes solo descargan los bits que necesitan (diferencias), pero no la actualización completa.


## <a name="peer-to-peer-content-distribution"></a>Distribución de contenido punto a punto

Aunque los clientes descargan solo las partes del contenido que necesitan, acelere las actualizaciones de Windows en su entorno mediante el uso de la distribución de contenido punto a punto. El uso de elementos del mismo nivel como un origen de descarga de las actualizaciones de calidad puede resultar útil para entornos en que los puntos de distribución local no están presentes en las oficinas remotas. Este comportamiento evita la necesidad de que todos los clientes descarguen contenido desde un punto de distribución remoto mediante un vínculo WAN lento. El uso de elementos del mismo nivel también puede resultar beneficioso cuando los clientes reservan en el servicio Windows Update. Solo se necesita un elemento del mismo nivel para descargar contenido de actualización de la nube antes de que esté disponible para otros dispositivos.

Configuration Manager admite muchas tecnologías punto a punto, incluidas las siguientes:
- Optimización de distribución de Windows
- Caché del mismo nivel de Configuration Manager
- Windows BranchCache  

En las secciones siguientes se proporciona información adicional sobre estas tecnologías.

### <a name="windows-delivery-optimization"></a>Optimización de distribución de Windows

La [Optimización de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) es la tecnología de descarga y el método de distribución punto a punto principales integrados en Windows 10. Los clientes de Windows 10 pueden obtener contenido de otros dispositivos de su red local que descargan las mismas actualizaciones. Con el uso de las [opciones de Windows disponibles para la Optimización de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options), puede configurar los clientes en grupos. Esta agrupación permite a la organización identificar los dispositivos que posiblemente son los mejores candidatos para responder a las solicitudes punto a punto. La Optimización de distribución reduce significativamente el ancho de banda general utilizado para mantener los dispositivos actualizados, al mismo tiempo que acelera el tiempo de descarga.

> [!NOTE]  
> La Optimización de distribución es una solución administrada en la nube. El acceso al servicio en la nube Optimización de distribución a través de Internet es un requisito para utilizar su funcionalidad punto a punto. Para obtener información sobre los puntos de conexión de Internet necesarios, vea [Preguntas más frecuentes sobre Optimización de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). 

Para obtener los mejores resultados, puede que tenga que establecer el [modo de descarga](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode) de la Optimización de distribución en **Grupo (2)** y definir los *identificadores de grupo*. En el modo de grupo, el emparejamiento puede cruzar subredes internas entre los dispositivos que pertenecen al mismo grupo, incluidos los dispositivos de las oficinas remotas. Use la [opción Id. de grupo](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids) para crear su propio grupo personalizado con independencia de los dominios y los sitios de AD DS. El modo de descarga en grupo es la opción recomendada para la mayoría de las organizaciones que tratan de conseguir la máxima optimización del ancho de banda con la Optimización de distribución.

La configuración manual de estos identificadores de grupo resulta complicada cuando los clientes usan un perfil itinerante entre diferentes redes. Configuration Manager 1802 agregó una nueva característica para simplificar la administración de este proceso mediante la [integración de los grupos de límites con la Optimización de distribución](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). Cuando un cliente se activa, se comunica con su punto de administración para obtener directivas y ofrece su información de red y de grupo de límites. Configuration Manager crea un identificador único para cada grupo de límites. El sitio usa la información de ubicación del cliente para configurar automáticamente el identificador de grupo de la Optimización de distribución del cliente con el identificador de límites de Configuration Manager. Cuando el cliente usa un perfil itinerante en otro grupo de límites, se comunica con su punto de administración y se reconfigura automáticamente con un nuevo identificador de grupo de límites. Con esta integración, la Optimización de distribución puede utilizar la información del grupo de límites de Configuration Manager para encontrar un elemento del mismo nivel desde el que descargar las actualizaciones.

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a> Optimización de entrega a partir de la versión 1910
<!--4699118-->
A partir de la versión 1910 de Configuration Manager, puede usar Optimización de distribución para la distribución de todo el contenido de Windows Update en clientes que ejecutan la versión 1709 o posterior de Windows 10, no solo los archivos de instalación rápida.

Para usar Optimización de distribución para todos los archivos de instalación de Windows Update, habilite la [configuración de cliente para las actualizaciones de software](../../core/clients/deploy/about-client-settings.md#software-updates) siguiente:

- **Permitir que los clientes descarguen contenido diferencial cuando esté disponible** establecido en **Sí**.
- **Puerto que los clientes usan para recibir solicitudes para el contenido diferencial** establecido en 8005 (valor predeterminado) o en un número de puerto personalizado.

> [!IMPORTANT]
> - Optimización de entrega debe estar habilitada (opción predeterminada) y no se puede omitir. Para más información, consulte la referencia [Optimización de entrega de Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference).
> - Compruebe la [configuración de cliente para Optimización de distribución](../../core/clients/deploy/about-client-settings.md#delivery-optimization) al cambiar la [configuración de cliente para las actualizaciones de software](../../core/clients/deploy/about-client-settings.md#software-updates) para el contenido diferencial.
> - No se puede usar Optimización de entrega para las actualizaciones de cliente de Office 365 si Office COM está habilitado. Configuration Manager usa Office COM para administrar las actualizaciones de los clientes de Office 365. Puede anular el registro de Office COM para permitir el uso de Optimización de entrega para las actualizaciones de Office 365. Cuando Office COM está deshabilitado, la tarea programada de Actualizaciones automáticas de Office 2.0 predeterminada administra las actualizaciones de software para Office 365. Esto significa que Configuration Manager no dicta ni supervisa el proceso de instalación de las actualizaciones de Office 365. Configuration Manager seguirá recopilando información del inventario de hardware para rellenar el panel de administración de cliente de Office 365 en la consola. Para obtener información sobre cómo anular el registro de Office COM, consulte [Habilite los clientes de Office 365 para recibir actualizaciones desde la red CDN de Office en lugar de Configuration Manager](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).
> - Cuando se usa CMG para el almacenamiento de contenido, el contenido de las actualizaciones de terceros no se descarga en los clientes si está habilitada la [opción de cliente](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Descarga de contenido diferencial cuando esté disponible**. <!--6598587-->


### <a name="configuration-manager-peer-cache"></a>Caché del mismo nivel de Configuration Manager

La [Caché del mismo nivel](../../core/plan-design/hierarchy/client-peer-cache.md) de Configuration Manager permite a los clientes compartir contenido con otros clientes directamente desde su caché local de Configuration Manager. La Caché del mismo nivel no reemplaza el uso de otras soluciones de almacenamiento en caché del mismo nivel, como Windows BranchCache. Funcionan de forma conjunta para ofrecer más opciones para extender las soluciones tradicionales de implementación de contenido, como los puntos de distribución. La Caché del mismo nivel no depende de BranchCache. Si no habilita o usa BranchCache, la caché del mismo nivel sigue funcionando.

> [!NOTE]  
> Los clientes solo pueden descargar contenido desde los clientes de la Caché del mismo nivel que están en su actual grupo de límites.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) es una tecnología de optimización de ancho de banda de Windows. Cada cliente tiene una memoria caché y actúa como un origen alternativo para el contenido. Los dispositivos de la misma red pueden solicitar este contenido. [Configuration Manager puede usar BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) para permitir que los elementos del mismo nivel sean el origen de contenido entre sí en lugar de tener que contactar siempre con un punto de distribución. Con el uso de BranchCache, los archivos se almacenan en la memoria caché de cada cliente individual, y otros clientes pueden recuperarlos según sea necesario. Este enfoque distribuye la caché en lugar de tener un único punto de recuperación. Este comportamiento ahorra una cantidad importante de ancho de banda, al mismo tiempo que reduce el tiempo que tardan los clientes en recibir el contenido solicitado.



## <a name="selecting-the-right-peer-caching-technology"></a>Selección de la tecnología correcta de almacenamiento en caché del mismo nivel

La selección de la tecnología correcta de almacenamiento en la memoria caché de los archivos de instalación rápida depende de su entorno y sus requisitos. Aunque Configuration Manager admite todas las tecnologías punto a punto, debe usar la más conveniente para su entorno. Para la mayoría de los clientes, suponiendo que cumplen los requisitos de Internet para la Optimización de distribución, sería suficiente con el almacenamiento en caché del mismo nivel de Windows 10 integrado con la Optimización de distribución. Si los clientes no pueden satisfacer estos requisitos de Internet, considere la posibilidad de usar la característica de Caché del mismo nivel de Configuration Manager. Si actualmente usa BranchCache con Configuration Manager y satisface todas sus necesidades, entonces los archivos rápidos con BranchCache pueden ser la opción correcta en su caso. 

### <a name="peer-cache-comparison-chart"></a>Gráfico comparativo de la Caché del mismo nivel


| Funcionalidad  | Optimización de entrega  | Almacenamiento en caché del mismo nivel  | BranchCache  |
|---------|---------|---------|---------|
| Compatible entre subredes | Sí | Sí | No |
| Límite de ancho de banda | Sí (Nativo) | Sí (mediante BITS) | Sí (mediante BITS) |
| Compatibilidad de contenido parcial | Sí, para todos los tipos de contenido admitidos que aparecen en la siguiente fila de esta columna. | Solo para Office 365 y las actualizaciones rápidas | Sí, para todos los tipos de contenido admitidos que aparecen en la siguiente fila de esta columna. |
| Tipos de contenido admitidos | **Mediante ConfigMgr:** </br> - Actualizaciones rápidas </br> - Todas las actualizaciones de Windows (a partir de la versión 1910). Esto no incluye las actualizaciones de Office.</br> </br> **Mediante Microsoft Cloud:**</br> - Actualizaciones de Windows y de seguridad</br> - Controladores</br> - Aplicaciones de la Tienda Windows</br> - Aplicaciones empresariales de la Tienda Windows | Todos los tipos de contenido de ConfigMgr, incluidas las imágenes descargadas en [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) | Todos los tipos de contenido de ConfigMgr, salvo las imágenes |
| Control del tamaño en disco de la caché | Sí | Sí | Sí |
| Detección de un origen del mismo nivel | Automático | Manual (configuración de agente de cliente) | Automático |
| Detección de elemento del mismo nivel | Mediante el servicio en la nube Optimización de distribución (requiere acceso a Internet) | Mediante el punto de administración (basado en los grupos de límites del cliente) | Multidifusión |
| Generación de informes | Sí (mediante Análisis de escritorio) | Panel de orígenes de datos de cliente de ConfigMgr | Panel de orígenes de datos de cliente de ConfigMgr |
| Control del uso de WAN | Sí (nativo, puede controlarse mediante la configuración de la directiva de grupo) | Grupos de límites | Solo compatibilidad de subred |
| Administración mediante ConfigMgr | Parcial (configuración de agente de cliente) | Sí (configuración de agente de cliente) | Sí (configuración de agente de cliente) |



## <a name="conclusion"></a>Conclusión

Microsoft recomienda optimizar la distribución de actualizaciones de calidad de Windows 10 mediante Configuration Manager con los archivos de instalación rápida y una tecnología de almacenamiento en caché del mismo nivel, según sea necesario. Este enfoque debe solucionar los problemas asociados con los dispositivos Windows 10 que descargan contenido de gran volumen para instalar las actualizaciones de calidad. También se recomienda mantener actualizados los dispositivos Windows 10 mediante la implementación de actualizaciones de calidad cada mes. Esta práctica reduce la diferencia del contenido de actualizaciones de calidad que los dispositivos necesitan cada mes. Con la reducción de las diferencias de contenido, las descargas desde los puntos de distribución o desde los orígenes del mismo nivel tienen un tamaño inferior. 

Dada la naturaleza de los archivos de instalación rápida, el tamaño de su contenido es considerablemente mayor que el de los archivos independientes tradicionales. Este tamaño ralentiza los tiempos de descarga de las actualizaciones desde el servicio Windows Update en el servidor del sitio de Configuration Manager. También aumenta la cantidad de espacio en disco necesario tanto para el servidor de sitio como para los puntos de distribución. El tiempo total necesario para descargar y distribuir actualizaciones de calidad podría ser más largo. Sin embargo, las ventajas para el dispositivo deberían ser importantes durante la descarga e instalación de las actualizaciones de calidad en los dispositivos Windows 10. Para obtener más información, consulte el artículo sobre cómo [usar archivos de instalación rápida](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files).

Si los inconvenientes del servidor para las actualizaciones de mayor tamaño impiden la adopción de la compatibilidad de los archivos de instalación rápida, pero las ventanas en el dispositivo son fundamentales para su empresa y entorno, Microsoft recomienda usar [Windows Update para empresas](integrate-windows-update-for-business-windows-10.md) con Configuration Manager. Windows Update para empresas proporciona todas las ventajas de los archivos de instalación rápida sin necesidad de descargar, almacenar y distribuir los archivos de instalación rápida en todo el entorno. Los clientes descargan el contenido directamente del servicio Windows Update, por lo que pueden seguir usando la Optimización de distribución.



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Preguntas más frecuentes

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>¿Cómo funcionan las descargas rápidas de Windows con Configuration Manager?

El agente de Windows Update (WUA) primero solicita el contenido rápido. Si no puede instalar la actualización rápida, puede revertir a la actualización del archivo completo.  

1. El cliente de Configuration Manager indica a WUA que descargue el contenido de actualización. Cuando WUA inicia una descarga rápida, primero descarga un código auxiliar (por ejemplo, `Windows10.0-KB1234567-<platform>-express.cab`), que forma parte del paquete rápido.  

2. WUA pasa este código auxiliar al instalador de actualizaciones de Windows, un servicio basado en componentes (CBS). CBS usa el código auxiliar para realizar un inventario local, comparar las diferencias del archivo en el dispositivo con lo que se necesita para obtener la última versión del archivo que se ofrece.  

3. CBS pide entonces a WUA que descargue los rangos necesarios de uno o varios archivos .psf rápidos.  

4. La Optimización de distribución se coordina con Configuration Manager y descarga los rangos de un punto de distribución local o de elementos del mismo nivel, en caso de que estén disponibles. Si la Optimización de distribución está deshabilitada, se usa el Servicio de transferencia inteligente en segundo plano (BITS) de la misma forma con Configuration Manager en la coordinación de los orígenes de caché del mismo nivel. La Optimización de distribución o BITS pasan los rangos a WUA, que los pone a disposición de CBS para su aplicación e instalación.  


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>¿Por qué los archivos rápidos (.psf) son tan grandes cuando se almacenan en los orígenes del mismo nivel de Configuration Manager en la carpeta ccmcache?

Los archivos rápidos (.psf) son archivos dispersos. Para determinar el espacio real que el archivo va a ocupar en el disco, compruebe la propiedad **Size on disk** (Tamaño en disco) del archivo. La propiedad de tamaño en disco debe ser considerablemente inferior al valor de tamaño.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>¿Configuration Manager admite archivos de instalación rápida con las actualizaciones de características de Windows 10?

No, Configuration Manager actualmente solo admite archivos de instalación rápida con las actualizaciones de calidad de Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>¿Cuánto espacio en disco se necesita para las actualizaciones de calidad en el servidor de sitio y en los puntos de distribución?

Depende. Para cada actualización de calidad, tanto la versión rápida como la del archivo completo de la actualización se almacenan en los servidores. Las actualizaciones de calidad de Windows 10 son acumulativas, por lo que el tamaño de estos archivos aumenta cada mes. Planee un mínimo de 5 GN por actualización e idioma. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>¿Los clientes de Configuration Manager aún se benefician de los archivos de instalación rápida al revertir al servicio Windows Update?

Sí. Si usa la siguiente opción de implementación de actualizaciones de software, los clientes aún usarán las actualizaciones rápidas y la Optimización de distribución cuando reviertan al servicio en la nube:  

**Si las actualizaciones de software no están disponibles en un punto de distribución de los grupos actuales, vecinos o del sitio, descargar el contenido de Microsoft Update**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>¿Por qué no se descarga el contenido del archivo rápido de las actualizaciones existentes después de habilitar la compatibilidad con los archivos rápidos? 

Los cambios solo surten efecto para las nuevas actualizaciones sincronizadas e implementadas después de habilitar la compatibilidad.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>¿Hay alguna forma de ver cuánto contenido se descarga de los elementos del mismo nivel con la Optimización de distribución?
La versión 1703 y posteriores de Windows 10 incluyen dos nuevos cmdlets de PowerShell, **Get-DeliveryOptimizationPerfSnap** y **Get-DeliveryOptimizationStatus**. Estos cmdlets ofrecen más información de la Optimización de distribución y el uso de la caché. Para más información, consulte el artículo sobre la [optimización de entrega para actualizaciones de Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>¿Cómo se comunican los clientes con la Optimización de distribución a través de la red?
Para obtener más información sobre los puertos de red, los requisitos de proxy y los nombres de host para los firewalls, vea las [preguntas más frecuentes sobre la Optimización de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

## <a name="log-files"></a>Archivos de registro

Use los siguientes archivos de registro para supervisar las descargas diferenciales:

- WUAHandler.log
- DeltaDownload.log

## <a name="next-steps"></a>Pasos siguientes

- [Implementar actualizaciones de software](deploy-software-updates.md)
- [Implementar actualizaciones de software automáticamente](automatically-deploy-software-updates.md)
