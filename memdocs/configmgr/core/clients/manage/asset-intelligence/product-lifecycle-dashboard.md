---
title: Panel de ciclo de vida del producto
titleSuffix: Configuration Manager
description: Vea la Directiva del ciclo de vida de Microsoft con el panel de ciclo de vida del producto en Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695173"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Administrar la directiva de ciclo de vida de Microsoft con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

A partir de la versión 1806, puede usar el panel de ciclo de vida del producto de Configuration Manager para ver la Directiva de ciclo de vida de Microsoft. El panel muestra el estado de la Directiva de ciclo de vida de Microsoft de los productos instalados en los dispositivos administrados con Configuration Manager. Además proporciona información sobre los productos de Microsoft del entorno, el estado de compatibilidad y la fechas de finalización del soporte técnico. Use el panel para conocer la disponibilidad del soporte técnico para cada producto. Esta información le ayuda a planear cuándo actualizar los productos de Microsoft que usa antes de que llegue el fin del soporte actual.  

Para más información, vea la [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle).

A partir de la versión 1810, el panel incluye información para System Center 2012 Configuration Manager y versiones posteriores.<!--1358702-->  



## <a name="prerequisites"></a>Requisitos previos 

 Para ver los datos en el panel del ciclo de vida del producto, se requieren los siguientes componentes:  

- Internet Explorer 9 o una versión posterior debe estar instalado en el equipo que ejecuta la consola de Configuration Manager.  

- Es necesario instalar y configurar un rol de punto de conexión de servicio. Para obtener actualizaciones de los datos de este panel, el punto de conexión de servicio debe estar en línea o sincronizarse regularmente en caso de que esté sin conexión. Para obtener más información, consulte [About the service connection point](../../../servers/deploy/configure/about-the-service-connection-point.md) (Sobre el punto de conexión del servicio).

- Un punto de servicios de informes es necesario para la funcionalidad de hipervínculo en el panel. Los informes de vínculos del panel para SQL Server Reporting Services (SSRS). Para obtener más información, vea [Introducción a los informes](../../../servers/manage/introduction-to-reporting.md).  

- El punto de sincronización de Asset Intelligence debe estar configurado y sincronizado. El panel usa el catálogo de Asset Intelligence como metadatos para los títulos de productos. Los metadatos se comparan con los datos de inventario en la jerarquía. Para obtener más información, consulte [Configurar Asset Intelligence en Configuration Manager](configuring-asset-intelligence.md).  
  - Si está configurando el punto de servicio de Asset Intelligence por primera vez, no olvide [habilitar las clases de inventario de hardware de Asset Intelligence](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). El panel de ciclo de vida depende de esas clases de inventario de hardware de Asset Intelligence. El panel no mostrará datos hasta que los clientes hayan analizado y devuelto el inventario de hardware.  
  - Para ver información acerca de las actualizaciones de seguridad extendidas (ESU) en este panel, habilite la clase de inventario de hardware **Producto de licencia de software: Asset Intelligence (SoftwareLicensingProduct)** . Para obtener más información, vea [Habilitar las clases de informes de inventario de hardware de Asset Intelligence](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>Uso del panel de ciclo de vida del producto

El panel mostrará información sobre todos los productos actuales en función de los datos de inventario que recopile el sitio de los dispositivos administrados. Sin embargo, la información mostrada para los sistemas operativos y SQL Server se limita a las siguientes versiones:

- Windows Server 2008 y versiones posteriores
- Windows XP y versiones posteriores
- SQL Server 2008 y versiones posteriores

Para tener acceso al panel de ciclo de vida, en la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Asset Intelligence** y seleccione el nodo **Ciclo de vida del producto**.

> [!NOTE]  
> Los datos del panel se basan en el sitio al que se conecta la consola de Configuration Manager. Si la consola se conecta a su sitio de nivel superior, verá datos en toda la jerarquía. Cuando se conecta a un sitio primario secundario, se mostrarán solamente los datos de ese sitio.

### <a name="product-lifecycle-dashboard"></a>Panel de ciclo de vida del producto

![Captura de pantalla del panel de ciclo de vida del producto en la consola](media/product-lifecycle-dashboard.png)

Cambie la vista seleccionando una de las siguientes opciones de la lista **Categoría de productos**:  
- **Todo**: ver todos los productos de forma conjunta  
- **Cliente de Windows**: ver las versiones del SO del cliente de Windows  
- **Windows Server**: ver las versiones del SO de Windows Server  
- **Base de datos**: ver las versiones de SQL Server  
- **Configuration Manager**: a partir de la versión 1810, ver las versiones de Configuration Manager 
- **Microsoft Office**: a partir de la versión 1902, vea la información de las versiones instaladas de Office 2003 a Office 2016 <!--3556026-->

El panel presenta los iconos siguientes:  

- **Cinco principales productos que han superado el fin de su ciclo de vida**: este icono es una vista de datos consolidados de productos que se encuentran en su entorno y cuyo fin de ciclo de vida se ha superado. El gráfico muestra el software instalado que ha expirado en comparación con el ciclo de vida de soporte técnico para sistemas operativos y productos de SQL server.  

- **Cinco principales productos que se aproximan al final de su ciclo de vida**: este icono es una vista de datos consolidados de productos que se encuentran en su entorno cuyo ciclo de vida finaliza en un plazo de 18 meses. El gráfico muestra el software instalado al que le quedan 18 meses en relación con el ciclo de vida de soporte técnico para sistemas operativos y productos de SQL Server.  

- **Datos del ciclo de vida de los productos instalados:** este icono proporciona una idea general de cuándo un producto cambia del estado admitido al estado expirado. El gráfico proporciona un desglose del número de clientes en los que está instalado el producto y el estado de disponibilidad del soporte técnico, junto con un vínculo para obtener más información acerca de los siguientes pasos que se deben realizar. En el gráfico se incluye la siguiente información:     
    - Tiempo de soporte técnico restante
    - Número en el entorno 
    - Fecha de finalización del soporte técnico estándar
    - Fecha de finalización del soporte técnico ampliado
    - Pasos siguientes  

> [!IMPORTANT]  
> La información que se muestra en este panel se proporciona para su comodidad y únicamente para el uso interno en su empresa. No debe confiar exclusivamente en esta información para comprobar el cumplimiento. Asegúrese de comprobar la exactitud de la información proporcionada, junto con la disponibilidad de la información de soporte técnico, en [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Generación de informes

También existen informes adicionales. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y expanda **Informes**. Se agregan los siguientes informes nuevos a la categoría **Asset Intelligence**:  

- **Ciclo de vida 01A (equipos con un producto de software específico)** : Vea una lista de equipos en los que se detecta un producto especificado.  

- **Ciclo de vida 02A (lista de equipos con productos que han expirado en la organización)** : Vea equipos que contienen productos expirados. Este informe se puede filtrar por nombre de producto.

- **Ciclo de vida 03A (lista de productos expirados que se han encontrado en la organización)** : Vea los detalles de productos de su entorno cuyo ciclo de vida ha expirado.  

- **Ciclo de vida 04A (información general del ciclo de vida de los productos)** : Vea una lista de los ciclos de vida de los productos. Filtre la lista por nombre de producto y los días para que expire.  

- **Ciclo de vida 05A (panel de ciclo de vida del producto)** : A partir de la versión 1810, este informe incluye información similar a la del panel de consola. Seleccione una categoría para ver el recuento de productos en su entorno y los días de soporte técnico que le quedan.  

Para obtener más información, vea [Lista de informes](../../../servers/manage/list-of-reports.md#asset-intelligence).<!--SCCMDocs issue 997-->  
