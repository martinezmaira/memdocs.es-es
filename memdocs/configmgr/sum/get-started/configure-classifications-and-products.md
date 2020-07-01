---
title: Configurar las clasificaciones y los productos
titleSuffix: Configuration Manager
description: Haga lo siguiente para configurar los productos y clasificaciones de actualización de software que se van a sincronizar en la consola de Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 4f13ff305ba5fc2b5c5080bafb6fed2412ff8366
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84614077"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>Configurar las clasificaciones y los productos que va a sincronizar  

*Se aplica a: Configuration Manager (rama actual)*

Los metadatos de las actualizaciones de software se recuperan durante el proceso de sincronización en Configuration Manager según la configuración que especifique en las propiedades de componente de punto de actualización de software. Después de sincronizar las actualizaciones de software por primera vez o cuando se publiquen nuevos productos y clasificaciones, debe ir a las propiedades para seleccionar los nuevos elementos. Utilice el siguiente procedimiento para configurar las clasificaciones y los productos para sincronizar.  

> [!NOTE]  
> Utilice el procedimiento de esta sección solo en el sitio de nivel superior.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Para configurar las clasificaciones y los productos para sincronizar  

1. En la consola de **Configuration Manager**, vaya a **Administración** > **Configuración del sitio** > **Sitios**.

2. Seleccione el sitio de administración central o el sitio primario independiente.  

3. En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y, a continuación, haga clic en **Punto de actualización de software**.

4. En la pestaña **Clasificaciones** , especifique las clasificaciones de actualización de software para las que desea sincronizar las actualizaciones de software.  

    Cada actualización de software se define con una clasificación de actualización que facilita la organización de los distintos tipos de actualizaciones. Durante el proceso de sincronización, se sincronizan los metadatos de las actualizaciones de software para las clasificaciones especificadas. Configuration Manager ofrece la posibilidad de sincronizar actualizaciones de software con las siguientes clasificaciones de actualización:  

     - **Actualizaciones críticas**: especifica una corrección de amplia distribución para un problema específico que permite solucionar un error crítico no relacionado con la seguridad.  
     - **Actualizaciones de definiciones**: especifica una actualización de software frecuente y de amplia distribución que contiene adiciones a la base de datos de definiciones de un producto.  
     - **Paquetes de características**: especifica la nueva función del producto que se distribuye fuera de una versión del producto y que normalmente se incluye en la siguiente versión del producto completo.  
     - **Actualizaciones de seguridad**: especifica una corrección de amplia distribución para una vulnerabilidad relacionada con la seguridad de un producto específico.  
     - **Service Packs**: especifica un conjunto acumulativo y probado de todas las revisiones, actualizaciones de seguridad, actualizaciones críticas y actualizaciones que se aplican en un producto. Además, los Service Pack pueden contener correcciones adicionales para problemas que se han identificado internamente desde la publicación del producto.  
     - **Herramientas**: especifica una utilidad o característica que ayuda a realizar una o varias tareas.  
     - **Paquetes acumulativos de revisiones**: especifica un conjunto acumulativo y probado de revisiones, actualizaciones de seguridad, actualizaciones críticas y actualizaciones que se incluyen en un producto de forma conjunta para facilitar su implementación. Un paquete acumulativo de actualizaciones suele relacionarse, por lo general, con un área específica (por ejemplo, un componente del producto o de la seguridad).  
     - **Actualizaciones**: especifica una corrección de amplia distribución para un problema específico. Una actualización proporciona una solución para un error de código no crítico y no relacionado con la seguridad.  
     - **Actualización**: especifica una actualización para las características y funciones de Windows 10. Los sitios y los puntos de actualización de software tienen que ejecutar como mínimo WSUS 6.2 con la [revisión 3095113](https://support.microsoft.com/kb/3095113) para obtener la clasificación **Actualización**. Para obtener más información sobre la instalación de esta actualización, y otras, para las **actualizaciones**, vea [Requisitos previos para las actualizaciones de software en Configuration Manager](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012).
    
    > [!NOTE]
    > Puede activar la casilla **Incluir actualizaciones de controladores y firmware de Microsoft Surface** para sincronizar los controladores de Microsoft Surface.<!--1098490--> Todos los puntos de actualización de software deben ejecutar Windows Server 2016 o versiones posteriores para sincronizar correctamente los controladores de Surface. Si habilita un punto de actualización de software en un equipo que ejecuta Windows Server 2012 después de habilitar a los controladores de Surface, los resultados del examen de las actualizaciones de controladores no serán precisos. Esto genera datos de cumplimiento incorrectos que se muestran en la consola y en los informes de Configuration Manager. Para más información, consulte [Administración de controladores de dispositivos Surface con Configuration Manager](../deploy-use/surface-drivers.md).

5. En la pestaña **Productos** , especifique los productos para los que desea sincronizar las actualizaciones de software y, a continuación, haga clic en **Cerrar**.  

    - Configuration Manager almacena una lista de productos y familias de productos entre los que puede elegir cuando instala por primera vez el punto de actualización de software. Es posible que los productos y las familias de productos lanzados después del lanzamiento de Configuration Manager no estén disponibles para seleccionar hasta que se complete la sincronización de las actualizaciones de software, lo cual actualiza la lista de productos y familias de productos disponibles para seleccionar.  

    - Los metadatos para cada actualización de software definen los productos para los que la actualización es aplicable. Un producto es una edición específica de un sistema operativo o una aplicación, por ejemplo, Windows Server 2012. Una familia de productos es el sistema operativo o la aplicación de base de los cuales se derivan los productos individuales. Un ejemplo de una familia de productos es Windows, de la cual Windows Server 2012 forma parte. Puede especificar una familia de productos o productos individuales dentro de una familia de productos. Cuantos más productos seleccione, más tiempo tomará sincronizar las actualizaciones de software.  

    - Cuando las actualizaciones de software son aplicables a varios productos y se seleccionó al menos uno de ellos para sincronización, todos los productos aparecerán en la consola de Configuration Manager, aunque algunos no se hayan seleccionado. Por ejemplo, si Windows Server 2012 es el único sistema operativo que ha seleccionado y si una actualización de software se aplica a Windows 8 y Windows Server 2012, la consola de Configuration Manager mostrará ambos productos.  

    > [!NOTE]  
    > **Windows 10, versión 1903 y posteriores** se ha agregado a Microsoft Update como un producto propio en lugar de formar parte del producto **Windows 10** como en las versiones anteriores. Este cambio le obligaba a realizar una serie de pasos manuales para asegurarse de que los clientes veían estas actualizaciones. Se ha intentado reducir el número de pasos manuales que debe seguir para el nuevo producto en Configuration Manager, versión 1906. <!--4682946-->
    >
    > Cuando actualice a la versión 1906 de Configuration Manager y tenga seleccionado el producto **Windows 10** para la sincronización, las siguientes acciones tendrán lugar de forma automática:
    > - El producto **Windows 10, versión 1903 y posteriores** se agrega para la sincronización.
    > - Las [reglas de implementación automática](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) que contienen el producto **Windows 10** se actualizarán para incluir **Windows 10, versión 1903 y versiones posteriores**.
    > - Los [planes de mantenimiento](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) se actualizan para incluir el producto **Windows 10, versión 1903 y posteriores**.


## <a name="configuring-products-for-versions-of-windows-10"></a>Configuración de productos para versiones de Windows 10

### <a name="windows-10-version-1909"></a>Windows 10, versión 1909

Windows 10, versión 1909 comparte un sistema operativo básico común con Windows 10, versión 1903. El mantenimiento de ambas versiones es mediante las mismas actualizaciones acumulativas. Para obtener más información sobre Windows 10, versión 1909, la entrada de blog sobre [Opciones de entrega de Windows 10, versión 1909](https://aka.ms/1909mechanics).

Para asegurarse de que los clientes de Windows 10 versión 1909 y Windows 10, versión 1903 instalan actualizaciones desde Configuration Manager:

- Apruebe las actualizaciones para las versiones 1909 y 1903 de Windows 10.
  - Las actualizaciones tienen distintos títulos y reglas de aplicabilidad para cada versión del sistema operativo.
  - La aprobación de cada actualización por versión y arquitectura del sistema operativo mantiene el proceso de aprobación normal para los administradores.
- Los archivos de instalación de la actualización acumulativa son los mismos para las versiones 1909 y 1903 de Windows 10.
  - Configuration Manager solo descargará los archivos de origen de la actualización una vez.

#### <a name="feature-updates-for-windows-10-version-1909"></a>Actualizaciones de características para Windows 10, versión 1909

Cuando se aprueban las actualizaciones de características para Windows 10, versión 1909, observará algunas opciones diferentes:

- A los clientes de Windows 10, versión 1903 se les ofrece un [paquete de habilitación](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package), publicado el 12 de noviembre de 2019.
  - El paquete de habilitación es un archivo pequeño y rápido de instalación que activa las características de Windows 10, versión 1909 y reinicia el dispositivo.
  - Los requisitos previos para el paquete de habilitación incluyen:
    - Una actualización acumulativa mínima de [KB 4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389), publicada el 8 de octubre de 2019.
    - Una actualización mínima de la pila de servicio de [KB 4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390), publicada el 24 de septiembre de 2019.
  - Esta actualización, al igual que cualquier otra actualización de características, no está disponible para su importación desde `https:\\catalog.update.microsoft.com`.
  - La actualización se sincronizará automáticamente con WSUS si tiene el producto **Windows 10, versión 1903 y versiones posteriores,** y la clasificación de **actualizaciones** está seleccionada para la sincronización.
  - En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Mantenimiento de Windows 10** y seleccione el nodo **Todas las actualizaciones de Windows 10**. Busque los términos "habilitación" o "4517245".

    > [!TIP]
    > Dado que se trata de actualizaciones de características, no se encuentran en el nodo **Todas las actualizaciones de software**.

- Windows 10, versión 1809 y los clientes anteriores se actualizan con una única actualización directa de características,
  - al igual que ocurre con las demás instalaciones anteriores de actualizaciones de características que haya realizado para Windows 10.

> [!NOTE]
> Tanto el paquete de habilitación como la actualización de características tradicional de Windows 10, versión 1909, se mostrarán como "instalados" en los informes, independientemente de la ruta de acceso que se haya usado para instalarlo.

### <a name="windows-10-version-1903-and-later"></a>Windows 10, version 1903 and later

**Windows 10, versión 1903 y posteriores** se ha agregado a Microsoft Update como un producto propio en lugar de formar parte del producto **Windows 10** como en las versiones anteriores. Este cambio le obligaba a realizar una serie de pasos manuales para asegurarse de que los clientes veían estas actualizaciones. Se ha intentado reducir el número de pasos manuales que debe seguir para el nuevo producto en Configuration Manager, versión 1906. <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10, versión 1903 y versiones posteriores con Configuration Manager, versión 1906
Cuando actualice a la versión 1906 de Configuration Manager y tenga seleccionado el producto **Windows 10** para la sincronización, las siguientes acciones tendrán lugar de forma automática:
- El producto **Windows 10, versión 1903 y posteriores** se agrega para la sincronización.
- Las [reglas de implementación automática](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) que contienen el producto **Windows 10** se actualizarán para incluir **Windows 10, versión 1903 y versiones posteriores**.
- Los [planes de mantenimiento](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) se actualizan para incluir el producto **Windows 10, versión 1903 y posteriores**.

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10, versión 1903 y versiones posteriores con Configuration Manager, versión 1902
Si usa Configuration Manager 1902 con los clientes de la versión 1903 de Windows 10, deberá hacer lo siguiente:
- Seleccione el producto **Windows 10, versión 1903 y posteriores** para sincronización.
- Actualice las [reglas de implementación automática](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) para los clientes de Windows 10, versión 1903.
- Actualice los [planes de mantenimiento](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) para los clientes de Windows 10, versión 1903.

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a> Programa Windows Insider
<!--3556023-->
A partir de septiembre de 2019, puede atender y actualizar los dispositivos que ejecutan las compilaciones de Windows Insider Preview con Configuration Manager. Este cambio significa que puede administrar estos dispositivos sin cambiar los procesos normales ni habilitar Windows Update para empresas. Puede descargar actualizaciones de características y actualizaciones acumulativas para las compilaciones de Windows Insider Preview en Configuration Manager igual que cualquier otra actualización de Windows 10. Para obtener más información, vea la entrada de blog [Publicación de actualizaciones de características de Windows 10 en la versión preliminar de WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054).

Para obtener más información sobre la compatibilidad de Windows Insider en Configuration Manager, vea [Compatibilidad con Windows 10](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support).

### <a name="prerequisites"></a>Requisitos previos

- Configuration Manager, versión 1906 o posterior, configurada para la [administración de actualización de software](../plan-design/plan-for-software-updates.md).
- Dispositivos Windows 10 que ejecutan la [compilación de Windows Insider Preview](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started).
- Colección que contiene los dispositivos de Windows Insider.

### <a name="enable-windows-insider-upgrades-and-updates"></a>Habilitación de actualizaciones de Windows Insider

Debe habilitar los productos y las clasificaciones para las actualizaciones de Windows Insider. Las actualizaciones de características, las actualizaciones acumulativas y otras actualizaciones para Windows Insider se encuentran en la categoría de producto **Versión preliminar de Windows Insider**.

1. En la consola de **Configuration Manager**, vaya a **Administración** > **Configuración del sitio** > **Sitios**.
2. Seleccione el sitio de administración central o el sitio primario independiente.  
3. En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y, a continuación, haga clic en **Punto de actualización de software**.
4. En la pestaña **Productos**, asegúrese de seleccionar los siguientes productos para la sincronización:
    - Versión preliminar de Windows Insider
    - Windows 10, version 1903 and later
5. En la pestaña **Clasificaciones**, asegúrese de seleccionar las siguientes clasificaciones para la sincronización:
    - Actualizaciones
    - Actualizaciones de seguridad
    - Actualizaciones (opcional)
6. Haga clic en **Aceptar** para cerrar **Propiedades de componente de punto de actualización de software**.

### <a name="upgrading-windows-insider-devices"></a>Actualización de dispositivos de Windows Insider

Cuando se hayan sincronizado las actualizaciones de Windows Insider, podrá verlas desde **Biblioteca de Software** > **Mantenimiento de Windows 10** > **Todas las actualizaciones de Windows 10**.

![Actualizaciones de características de Windows Insider para el mantenimiento de Windows 10](media/3556023-windows-insiders-pre-release-feature-update.png)

Implemente las actualizaciones de características para Windows Insider en la recopilación de destino, al igual que cualquier otra actualización. Pero deberá tener en cuenta los siguientes elementos al implementar estas actualizaciones de características:

- Estas actualizaciones se aplicarán a todos los clientes de Windows 10, versión 1903 o versiones anteriores, con la misma arquitectura, edición e idioma.
- Hay términos de licencia que debe aceptar para poder instalar la implementación.
- Considere la posibilidad de utilizar la [prioridad del subproceso en la configuración de cliente](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority).
- La actualización dinámica instala automáticamente las actualizaciones críticas, incluida la actualización acumulativa más reciente, directamente desde Microsoft Update. Este comportamiento comenzó con las actualizaciones de características para Windows 10, versión 1903. 
  - Puede deshabilitar explícitamente la [actualización dinámica en la configuración de cliente](../../core/clients/deploy/about-client-settings.md#bkmk_du) o usando un [archivo setupconfig.ini](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options). 
  - Para obtener más información, vea la entrada de blog [Actualización dinámica de Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847).

Para obtener más información sobre cómo implementar actualizaciones, vea [Administración de Windows como servicio](../../osd/deploy-use/manage-windows-as-a-service.md).


### <a name="keeping-insider-devices-up-to-date"></a>Mantenimiento de los dispositivos internos actualizados

Las actualizaciones acumulativas para Windows Insider estarán disponibles para WSUS y, por extensión, para Configuration Manager. Estas actualizaciones acumulativas se lanzarán con una frecuencia similar a la de las actualizaciones acumulativas de Windows 10, versión 1903. Las actualizaciones acumulativas de Windows Insider se encuentran en la categoría de producto **Versión preliminar de Windows Insider** y se clasifican como **Actualizaciones de seguridad** o **Actualizaciones**. Puede implementar las actualizaciones acumulativas para Windows Insider mediante el proceso de actualización de software habitual, como mediante [reglas de implementación automática](../deploy-use/automatically-deploy-software-updates.md) o [implementaciones por fases](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> Actualizaciones de seguridad extendida y Configuration Manager

El programa de [actualizaciones de seguridad extendida (ESU) ](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) es una opción de último recurso para aquellos clientes que necesitan ejecutar determinados productos de Microsoft heredados más allá del final del soporte técnico. Incluye actualizaciones de seguridad críticas o importantes (tal y como se define en el [Centro de respuestas de seguridad de Microsoft [MSRC]](https://www.microsoft.com/msrc)) durante un máximo de tres años después del final de la fecha de soporte extendido del producto.

Los productos que están fuera de su ciclo de vida de soporte no se pueden usar con Configuration Manager. Esto incluye todos los productos que se incluyen en el programa ESU. Por ejemplo, Windows 7. Las actualizaciones de seguridad publicadas en el programa ESU se publicarán en Windows Server Update Services (WSUS). Estas actualizaciones se mostrarán en la consola de Configuration Manager. Mientras que los productos que se incluyen en el programa ESU ya no se admiten para su uso con Configuration Manager, se puede usar la [versión más reciente publicada de la rama actual de Configuration Manager](../../core/servers/manage/updates.md#version-details) para implementar e instalar actualizaciones de seguridad de Windows publicadas en el programa. También se puede usar la última versión de lanzamiento para implementar Windows 10 en dispositivos que ejecutan Windows 7.

Las características de administración de cliente no relacionadas con la administración de actualizaciones de software de Windows o la implementación de SO dejarán de estar probadas en los sistemas operativos que se incluyen en el programa ESU y no garantizamos que sigan funcionando. Se recomienda encarecidamente actualizar o migrar a una versión actual de los sistemas operativos lo antes posible para recibir compatibilidad con la administración de clientes.


## <a name="next-steps"></a>Pasos siguientes

Inicie la sincronización de las actualizaciones de software para recuperar actualizaciones de software en función de los nuevos criterios. Para más información, vea [Sincronizar actualizaciones de software](synchronize-software-updates.md).
