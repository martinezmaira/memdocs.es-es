---
title: Punto de distribución de extracción
titleSuffix: Configuration Manager
description: Obtenga información sobre las configuraciones y las limitaciones del uso de un punto de distribución de extracción con Configuration Manager.
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e88636d6854ed49e24a72518ba20ec7a1b50771
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703103"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Usar un punto de distribución de extracción con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


Cuando se distribuye contenido a un punto de distribución estándar en la consola de Configuration Manager, el servidor de sitio inserta el contenido en el punto de distribución. Un punto de distribución de extracción obtiene el contenido descargándolo desde una ubicación de origen, como un cliente.  

Cuando se distribuye contenido a muchos puntos de distribución, los puntos de distribución de extracción ayudan a reducir la carga de procesamiento en el servidor de sitio. También pueden acelerar a la transferencia de contenido a cada servidor. Normalmente el componente de administrador de distribución en el servidor de sitio envía contenido a cada punto de distribución. En su lugar, el sitio descarga el proceso de transferencia del contenido a los puntos de distribución de extracción.  

Puede configurar distintos puntos de distribución para que sean de extracción. Para cada punto de distribución de extracción, especifique uno o varios puntos de distribución de origen de los que puede obtener el contenido. Un punto de distribución de extracción solo puede descargar contenido de un punto de distribución que se especifique como punto de distribución de origen. 

Cuando se distribuye contenido a un punto de distribución de extracción en la consola, el servidor de sitio le envía una notificación. Después, el punto de distribución de extracción descarga el contenido de un punto de distribución de origen. Un punto de distribución de extracción administra la transferencia de contenido mediante la descarga desde un punto de distribución que ya tiene una copia del contenido.  

Los puntos de distribución de extracción admiten las mismas configuraciones y funcionalidad que los puntos de distribución normales. Por ejemplo, un punto de distribución de extracción admite lo siguiente: 
- Configuraciones de multidifusión y entorno PXE
- Validación de contenido
- Distribución de contenido a petición
- Comunicaciones HTTP o HTTPS desde los clientes
- Las mismas opciones de certificado que otros puntos de distribución
- Administración individual o como un miembro de un grupo de puntos de distribución  

Configure un punto de distribución de extracción cuando instale el punto de distribución. Después de crear un punto de distribución, puede configurarlo como un punto de distribución de extracción si modifica las propiedades de rol. Para obtener más información sobre cómo habilitar un punto de distribución como punto de distribución de extracción, vea [Punto de distribución de extracción](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull).  

Quite la configuración para que el punto de distribución deje de ser de extracción, mediante la edición de las propiedades del punto de distribución. Cuando se quita la configuración de punto de distribución de extracción, vuelve a su funcionamiento normal. El servidor de sitio administra las transferencias de contenido futuras al punto de distribución.  



### <a name="distribution-process"></a>Proceso de distribución

Al distribuir contenido a un punto de distribución de extracción, se produce la secuencia de eventos siguiente:

-   Una vez se distribuye el contenido a un punto de distribución de extracción en la consola, el componente de administrador de transferencia de paquetes en el servidor de sitio comprueba la base de datos del sitio para confirmar si el contenido está disponible en un punto de distribución de origen. Si no puede confirmar que el contenido está en un punto de distribución de origen para el punto de distribución de extracción, repite la comprobación cada 20 minutos hasta que el contenido esté disponible.  

-   Cuando el administrador de transferencia de paquetes confirma que el contenido está disponible, envía una notificación al punto de distribución de extracción para descargar el contenido. Si se produce un error en esta notificación, lo vuelve a intentar según lo establecido en **Configuración de reintento** del componente de distribución de software para los puntos de distribución de extracción. Cuando el punto de distribución de extracción recibe esta notificación, intenta descargar el contenido de sus puntos de distribución de origen.  

-   Mientras el punto de distribución de extracción descarga el contenido, el administrador de transferencia de paquetes sondea el estado según lo establecido en **Configuración del sondeo de estado** del componente de distribución de software para los puntos de distribución de extracción.  Cuando el punto de distribución de extracción completa la descarga del contenido, envía este estado a un punto de administración.  



## <a name="configure-site-component-settings"></a>Configurar opciones de componentes de sitio

Cuando use un punto de distribución de extracción, revise y configure las siguientes opciones de componente de sitio:  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2.  Seleccione el sitio. En la cinta, haga clic en **Configurar componentes de sitio** y seleccione **Distribución de software**.  

3. Cambie a la pestaña **Punto de distribución de extracción**.  

4.  En el grupo **Configuración de reintento**, revise los valores siguientes:  

    -   **Número de reintentos**: número de veces que el administrador de transferencia de paquetes intenta notificar al punto de distribución de extracción que descargue el contenido. Después de intentarlo este número de veces, el Administrador de transferencia de paquetes cancela la transferencia. Este valor es 30 de forma predeterminada.  

    -   **Retraso antes de cada reintento (minutos)** : número de minutos que el administrador de transferencia de paquetes espera entre cada intento. Este valor es 20 de forma predeterminada.  

5.  En la lista **Configuración del sondeo de estado**, revise los valores siguientes:  

    -   **Número de sondeos**: número de veces que el Administrador de transferencia de paquetes establece el contacto con el punto de distribución de extracción para recuperar el estado del trabajo. Si intenta este número de veces antes de que se complete el trabajo, el Administrador de transferencia de paquetes cancela la transferencia. Este valor es 72 de forma predeterminada.   

    -   **Retraso antes de cada reintento (minutos)** : número de minutos que el administrador de transferencia de paquetes espera entre cada intento. Este valor es 60 de forma predeterminada.   
    
    > [!NOTE]  
    >  Cuando el Administrador de transferencia de paquetes cancela un trabajo porque supera el número de reintentos de sondeo, el punto de distribución de extracción continúa con la descarga del contenido. Cuando termina, el punto de distribución de extracción envía el mensaje de estado adecuado y el estado nuevo se refleja en la consola.  
    


## <a name="limitations"></a>Limitaciones 

-   No se puede configurar un punto de distribución de nube como un punto de distribución de extracción.  

-   No se puede configurar el rol de punto de distribución de un servidor del sitio como un punto de distribución de extracción.  

-   La configuración del contenido preconfigurado reemplaza la del punto de distribución de extracción. Si se activa la opción **Habilitar este punto de distribución para contenido preconfigurado** en un punto de distribución de extracción, espera al contenido. No extrae el contenido del punto de distribución de origen. Al igual que un punto de distribución estándar habilitado para contenido preconfigurado, no recibe contenido del servidor de sitio. Para obtener más información, vea [Contenido preconfigurado](manage-network-bandwidth.md#BKMK_PrestagingContent).  

-   Un punto de distribución de extracción no usa las configuraciones de límite de frecuencia o de programación. Cuando se configura un punto de distribución instalado previamente para que sea un punto de distribución de extracción, las configuraciones de límites de frecuencia y de programación se guardan, pero no se usan. Si después quita la configuración del punto de distribución de extracción, las configuraciones de límites de frecuencia y de programación se implementan tal y como se configuraron anteriormente.  

    > [!NOTE]  
    >  Las pestañas **Programación** y **Límites de frecuencia** no son visibles en las propiedades del punto de distribución.  

-   Los puntos de distribución de extracción no usan la configuración de la pestaña **General** de **Propiedades del componente de distribución de software** para cada sitio. Estas opciones incluyen **Configuración de distribución simultánea** y **Configuración de reintento de multidifusión**.  

-   Para transferir contenido de un punto de distribución de origen en un bosque remoto, instale el cliente de Configuration Manager en el punto de distribución de extracción. Además, configure una cuenta de acceso a la red con acceso al punto de distribución de origen. A partir de la versión 1806, si habilita la opción del sitio **Usar los certificados generados por Configuration Manager para sistemas de sitios HTTP**, no necesita una cuenta de acceso a la red.<!--1358228-->  

-   Si el punto de distribución de extracción también es un cliente de Configuration Manager, la versión del cliente debe ser la misma que la del sitio de Configuration Manager que instala el punto de distribución de extracción. El punto de distribución de extracción usa CCMFramework, que es común al punto de distribución de extracción y al cliente de Configuration Manager.  



## <a name="about-source-distribution-points"></a>Acerca de los puntos de distribución de origen  

Al configurar el punto de distribución de extracción, especifique uno o varios puntos de distribución de origen:  

-   El asistente solo muestra los puntos de distribución que pueden ser puntos de distribución de origen.  

-   Un punto de distribución de extracción puede especificarse como punto de distribución de origen para otro punto de distribución de extracción.  

-   Solo los puntos de distribución compatibles con HTTP se pueden especificar como puntos de distribución de origen cuando se usa la consola de Configuration Manager.  

-   Use el SDK de Configuration Manager para especificar un punto de distribución de origen configurado para HTTPS. Para usar un punto de distribución de origen configurado para HTTPS, instale el cliente de Configuration Manager en el punto de distribución de extracción.  

-   A partir de la versión 1806, si sus oficinas remotas tienen una mejor conexión a Internet o si quiere reducir la carga en los vínculos a WAN, use como origen un [punto de distribución de nube](use-a-cloud-based-distribution-point.md) en Microsoft Azure. El punto de distribución de extracción necesita acceso a Internet para comunicarse con Microsoft Azure. El contenido debe distribuirse al punto de distribución de nube de origen.<!--1321554-->  

    > [!Note]  
    > Esta característica no genera gastos por almacenamiento de datos y salida de red en la suscripción de Azure. Para obtener más información, vea [Costo de la utilización de la distribución basada en la nube](use-a-cloud-based-distribution-point.md#bkmk_cost).  


> [!Tip]  
> Cuando un punto de distribución de extracción descarga contenido desde un punto de distribución de origen, ese punto de distribución de extracción se cuenta como un cliente en la columna **Cliente accedido (único)** del informe **Resumen de uso de los puntos de distribución** .  


### <a name="source-priorities"></a>Prioridades de origen

-   Asigne una prioridad diferente a cada punto de distribución de origen, o bien asigne varios puntos de distribución de origen a la misma prioridad.  

-   La prioridad determina el orden en que el punto de distribución de extracción solicita contenido de sus puntos de distribución de origen.  

-   Los puntos de distribución de extracción establecen contacto inicialmente con el punto de distribución de origen que tenga la prioridad más baja. Si hay varios puntos de distribución de origen con la misma prioridad, el punto de distribución de extracción selecciona de forma aleatoria uno de los orígenes con la misma prioridad.  

-   Si el contenido no está disponible en el origen seleccionado, el punto de distribución de extracción intenta descargarlo desde otro punto de distribución con la misma prioridad.  

-   Si ninguno de los puntos de distribución con una prioridad determinada tiene el contenido, el punto de distribución de extracción intenta descargarlo desde un punto de distribución de origen con el nivel de prioridad siguiente. Esta búsqueda continúa hasta que el contenido se encuentra.   

- Si ninguno de los puntos de distribución de origen asignados tiene el contenido, el punto de distribución de extracción espera durante 30 minutos y, después, inicia el proceso de nuevo.  



## <a name="inside-the-pull-distribution-point"></a>Dentro del punto de distribución de extracción 

-   Para administrar la transferencia de contenido, los puntos de distribución de extracción usan el componente **CCMFramework**. El cliente de Configuration Manager incluye este componente.  

-   Cuando se habilita el punto de distribución de extracción, el sitio instala **pulldp.msi**. Este instalador también agrega el componente CCMFramework. El marco no requiere el cliente de Configuration Manager.  

-   Después de instalar el punto de distribución de extracción, para funcionar usa principalmente el servicio **CCMExec**.  

-   Cuando el punto de distribución de extracción transfiere contenido, usa el **Servicio de transferencia inteligente en segundo plano** (BITS) integrado en Windows. Un punto de distribución de extracción no requiere que se instale la extensión BITS para el servidor IIS.<!--sms.503672 -Clarified BITS use-->

-  Para obtener los detalles operativos, vea los siguientes archivos de registro en el punto de distribución de extracción:  
    - **DataTransferService.log**
    - **PullDP.log**



## <a name="see-also"></a>Vea también  
 [Conceptos básicos de la administración de contenido](fundamental-concepts-for-content-management.md)   
