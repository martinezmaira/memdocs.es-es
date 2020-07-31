---
title: Administración de actualizaciones de controladores de Surface
titleSuffix: Configuration Manager
description: Configuration Manager sincroniza las actualizaciones de controladores de Surface para implementarlos en dichos dispositivos.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: f276db618a2e67832ffa5575622e00eea02c7422
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438624"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>Administración de controladores de Surface con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

System Center Configuration Manager le permite sincronizar los controladores de Surface e implementarlos como una actualización de software. Esta funcionalidad le permite garantizar que los dispositivos Surface ejecutan los controladores disponibles más recientes. Esta sincronización se presentó por primera vez en la versión 1706 como una característica de versión preliminar y se convirtió en una característica en la 1710. <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>Requisitos previos para la sincronización de controladores de Surface

- Un punto de actualización de software de nivel superior conectado a Internet.
- Todos los puntos de actualización de software deben ejecutar Windows Server 2016 con la actualización acumulativa KB4025339 o posterior instalada.
- Configuration Manager no habilita esta característica opcional de forma predeterminada. Habilítela para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>Habilitación de la sincronización para controladores de Surface

Siga estos pasos para habilitar la sincronización de controladores de Surface:

1. Conecte la consola de Configuration Manager al servidor de sitio de nivel superior.
1. Vaya a **Administration** > **Configuración del sitio** > **Sitios** y, luego, haga clic en el sitio de nivel superior.
1. En la cinta de opciones, seleccione **Configuración** > **Configurar componentes de sitio** > **Punto de actualización de software**.
1. Haga clic en la pestaña **Clasificaciones** y, luego, haga clic en la casilla **Incluir actualizaciones de controladores y firmware de Microsoft Surface** y en **Aplicar**.

     ![Habilitación de los controladores de Surface desde las propiedades del punto de actualización de software](media/enable-surface-driver-sync.png)

1. En las propiedades del componente Punto de actualización de software, haga clic en la pestaña **Productos**. Para más información, consulte las secciones [Productos para controladores de Surface](#bkmk_prod) y [Modelos de Surface](#bkmk_models).
1. Seleccione los productos para cada versión de Windows 10 para la que quiera admitir controladores de Surface. Observará que hay dos versiones diferentes de cada uno de los productos para los controladores:

   - Windows 10, *versión* **Update and later Servicing Drivers**
   - Windows 10, *versión* **Update and later Upgrade & Servicing Drivers**

     ![Lista de productos de controladores de versiones de Windows 10](media/surface-driver-products-sup.png)

1. Cuando haya terminado de seleccionar los productos, haga clic en **Aceptar**.
1. [Sincronice el punto de actualización de software](../get-started/synchronize-software-updates.md) para incorporar los controladores de Surface a Configuration Manager.
1. Una vez que los controladores de Surface están sincronizados, impleméntelos de la misma manera que se implementan otras actualizaciones.

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a> Productos para controladores de Surface

La mayoría de los controladores pertenecen a los siguientes grupos de productos:

- Windows 10 and later version drivers
- Windows 10 and later Upgrade & Servicing Drivers
- Windows 10 Anniversary Update and Later Servicing Drivers
- Windows 10 Anniversary Update and Later Upgrade & Servicing Drivers
- Windows 10 Creators Update and Later Servicing Drivers
- Windows 10 Creators Update and Later Upgrade & Servicing Drivers
- Windows 10 Fall Creators Update and Later Servicing Drivers
- Windows 10 Fall Creators Update and Later Upgrade & Servicing Drivers
- Windows 10 S and Later Servicing Drivers
- Windows 10 S Version 1709 and Later Servicing Drivers for testing
- Windows 10 S Version 1709 and Later Upgrade & Servicing Drivers for testing
- Windows 10 S Version 1803 and Later Servicing Drivers
- Windows 10 S Version 1803 and Later Upgrade & Servicing Drivers
- Windows 10 S version 1809 and later, Servicing Drivers
- Windows 10 S version 1809 and later, Upgrade & Servicing Drivers
- Windows 10 S version 1903 and later, Servicing Drivers
- Windows 10 S version 1903 and later, Upgrade & Servicing Drivers
- Windows 10 Version 1803 and Later Servicing Drivers
- Windows 10 Version 1803 and Later Upgrade & Servicing Drivers
- Windows 10 version 1809 and later, Servicing Drivers
- Windows 10 Version 1809 and later, Upgrade & Servicing Drivers
- Windows 10 version 1903 and later, Servicing Drivers
- Windows 10 Version 1903 and later, Upgrade & Servicing Drivers

> [!NOTE]
> La mayoría de los controladores de Surface pertenecen a varios grupos de productos de Windows 10. Es posible que no tenga que seleccionar todos los productos que se enumeran aquí. Para reducir el número de productos que forman parte del catálogo de actualizaciones, se recomienda seleccionar solo aquellos que se necesiten en el entorno para la sincronización.

## <a name="surface-models"></a><a name="bkmk_models"></a> Modelos Surface

La tabla siguiente contiene los modelos Surface y las versiones de Windows 10 en las que se pueden instalar controladores con Configuration Manager. Las actualizaciones de controladores de Surface no están disponibles en Configuration Manager el mismo día en que se publican en el catálogo de Microsoft Update. Configuration Manager mantiene su propia lista de controladores de Surface que se importarán. Se indican los dispositivos que necesitan productos de Windows 10 S. Microsoft tiene la intención de agregar los controladores de Surface a la lista de permitidos el segundo martes de cada mes con el fin de facilitarlos para la sincronización con Configuration Manager. Para más información, consulte [Preguntas más frecuentes](#bkmk_faq).

</br>

|Modelo Surface|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|Sí| Sí| Sí |Sí|Sí|
|Surface Pro 4|Sí| Sí| Sí |Sí|Sí|
|Surface Pro 6|No aplicable| Sí| Sí |Sí|Sí|
|Surface Pro 7|No aplicable| No aplicable| No aplicable |Sí|Sí|
|Surface Pro X|No aplicable| No aplicable| No aplicable |Sí|Sí|
|Surface Book|Sí| Sí| Sí |Sí|Sí|
|Surface Book 2|Sí| Sí| Sí |Sí|Sí|
|Surface Book 3|No aplicable| No aplicable| No aplicable |Sí|Sí|
|Surface Laptop|Sí, con el producto "Windows 10 S version 1709 and later Servicing drivers" seleccionado| Sí, con el producto "Windows 10 S version 1803 and later Servicing drivers" seleccionado|Sí, con el producto "Windows 10 S version 1809 and later Upgrade & Servicing drivers" seleccionado|Sí, con el producto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" seleccionado|Sí, con el producto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" seleccionado|
|Surface Laptop 2|No aplicable| Sí |Sí|Sí|Sí|
|Surface Laptop 3|No aplicable| No aplicable|No aplicable|Sí |Sí|
|Surface Go|No aplicable| Sí, con el producto "Windows 10 S version 1803 and later Servicing drivers" seleccionado|Sí, con el producto "Windows 10 S version 1809 and later Upgrade & Servicing drivers" seleccionado|Sí, con el producto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" seleccionado|Sí, con el producto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" seleccionado|
|Surface Go 2|No aplicable| No aplicable| Sí |Sí|Sí, con el producto "Windows 10 S version 1903 and later Upgrade & Servicing drivers" seleccionado|
|Surface Studio|Sí| Sí| Sí |Sí|Sí|
|Surface Studio 2|No aplicable| Sí| Sí |Sí|Sí|

## <a name="verify-the-configuration"></a>Comprobación de la configuración

Para comprobar que el punto de actualización de software está configurado correctamente, use los archivos **WsyncMgr.log** y **WCM.log**.

1. Abra WsyncMgr.log y busque la siguiente entrada del registro:

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. Si se ha registrado alguna de las siguientes entradas en **WsyncMgr.log**, compruebe que haya seleccionado la opción **Include Microsoft Surface drivers and firmware updates** (Incluir actualización de controladores y firmware de Microsoft Surface) en las propiedades del punto de actualización de software:
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. Abra **WCM. log** y busque elementos similares a las siguientes entradas:
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   Esta entrada es un elemento XML que enumera el grupo y la clasificación de productos que están sincronizados actualmente por el servidor del punto de actualización de software. Si no encuentra los productos que ha seleccionado, compruebe que se hayan guardado los productos para el punto de actualización de software.
1. También puede esperar a que finalice la siguiente sincronización. Luego, compruebe si las actualizaciones de controladores y de firmware de Surface aparecen en las actualizaciones de software de la consola de Configuration Manager. Por ejemplo, la consola podría mostrar la siguiente información: ![Controladores de Surface sincronizados en la consola de Configuration Manager](media/synchronized-surface-drivers.png)

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> Preguntas más frecuentes

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>Aunque he seguido los pasos de este artículo, los controladores de mi dispositivo Surface siguen sin sincronizarse. ¿Por qué?

Si realiza la sincronización desde un servidor de Windows Server Update Services (WSUS) ascendente, y no desde Microsoft Update, asegúrese de que dicho servidor esté configurado para admitir y sincronizar las actualizaciones de controladores de Surface. Todos los servidores descendentes se limitan a las actualizaciones que se encuentran en la base de datos del servidor WSUS ascendente.

Hay más de 68 000 actualizaciones que se clasifican como controladores en WSUS. Para evitar que los controladores no relacionados con Surface se sincronicen con Configuration Manager, Microsoft filtra la sincronización de controladores con una lista de permitidos. Después de publicar e incorporar la nueva lista de permitidos a Configuration Manager, los nuevos controladores se agregan a la consola después de la siguiente sincronización. Microsoft tiene la intención de agregar los controladores de Surface a la lista de permitidos el segundo martes de cada mes con el fin de facilitarlos para la sincronización con Configuration Manager.

Si el entorno de Configuration Manager es sin conexión, se importa una nueva lista de permitidos cada vez que se importan [actualizaciones de servicio](../../core/servers/manage/use-the-service-connection-tool.md) a Configuration Manager. También tendrá que importar un [nuevo catálogo de WSUS](../get-started/synchronize-software-updates-disconnected.md) que contenga los controladores antes de que las actualizaciones se muestren en la consola de Configuration Manager. Dado que un entorno de WSUS independiente contiene más controladores que un SUP de Configuration Manager, se recomienda establecer un entorno de Configuration Manager que tenga funcionalidades en línea y configurarlo para sincronizar los controladores de Surface. Con esto se consigue una exportación de WSUS más pequeña que se asemeja en gran medida al entorno sin conexión.

Si el entorno de Configuration Manager está en línea y puede detectar nuevas actualizaciones, recibirá actualizaciones de la lista automáticamente. Si no ve los controladores esperados, compruebe que los archivos WCM.log y WsyncMgr.log no tengan errores de sincronización.

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>El entorno de Configuration Manager está sin conexión, ¿puedo importar manualmente los controladores de Surface en WSUS?

No. Incluso si la actualización se importa en WSUS, no se importará en la consola de Configuration Manager para la implementación si no aparece en la lista de permitidos. Debe usar la [herramienta de conexión de servicio](../../core/servers/manage/use-the-service-connection-tool.md) para importar las actualizaciones de servicio a Configuration Manager a fin de actualizar la lista de permitidos.

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>¿Qué métodos alternativos tengo para implementar las actualizaciones de controladores y de firmware de Surface?

Puede encontrar información sobre cómo implementar las actualizaciones de los controladores y del firmware de Surface mediante canales alternativos en [Administrar actualizaciones de los controladores y del firmware de Surface](https://docs.microsoft.com/surface/manage-surface-driver-and-firmware-updates). Si quiere descargar el archivo .msi o .exe y, luego, realizar la implementación mediante los canales de implementación de software tradicionales, consulte [Mantenimiento de la actualización del firmware de los dispositivos Surface con Configuration Manager](https://docs.microsoft.com/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager).

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre los controladores de Surface, consulte los artículos siguientes:

- [Consideraciones sobre Surface y System Center Configuration Manager](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Historial de actualizaciones de Surface](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Descarga del firmware y de los controladores más recientes para dispositivos Surface](/surface/manage-surface-driver-and-firmware-updates)
