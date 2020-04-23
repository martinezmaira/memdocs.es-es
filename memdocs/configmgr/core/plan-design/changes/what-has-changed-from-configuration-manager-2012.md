---
title: Cambios con respecto a la versión de 2012
titleSuffix: Configuration Manager
description: Identifique los cambios y las nuevas funciones de Configuration Manager con respecto a System Center 2012 Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704443"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>Cambios desde System Center 2012 Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La rama actual de Configuration Manager presenta cambios importantes de System Center 2012 Configuration Manager. En este artículo se identifican los cambios más importantes y las nuevas funciones de la versión de línea base 1511 original de la rama actual de Configuration Manager. Para más información sobre los cambios incluidos en actualizaciones recientes de Configuration Manager, vea [Novedades de las versiones incrementales de Configuration Manager](whats-new-incremental-versions.md).

> [!NOTE]
> A partir de la versión 1910, Configuration Manager forma parte de Microsoft Endpoint Manager. Para más información, vea [Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem).

La versión de diciembre de 2015 (versión 1511) de Configuration Manager es la versión inicial del producto actual de Configuration Manager de Microsoft. Se conoce habitualmente como la rama actual de Configuration Manager. *Rama actual* indica que esta versión que actualizaciones incrementales para el producto. También proporciona una manera de distinguir entre esta versión y las versiones anteriores de Configuration Manager.  

La rama actual de Configuration Manager:  

- No usa un identificador de producto o de año en el nombre de producto, a diferencia de versiones anteriores como Configuration Manager 2007 o System Center 2012 Configuration Manager.  

- Admite actualizaciones incrementales desde el producto, que también se denominan versiones de actualización. La versión inicial era la 1511. Varias veces al año se publican versiones posteriores como actualizaciones en consola, como la versión 1910.  

- Se instala con una versión de línea base. Aunque 1511 era la versión original de línea de base, también se publican de vez en cuando nuevas versiones de línea de base, como la 2002. Las versiones de línea base se pueden usar para instalar un nuevo sitio o jerarquía de Configuration Manager, o para actualizar desde una versión compatible de System Center 2012 Configuration Manager.  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a> Actualizaciones en la consola

Configuration Manager usa un método de servicio en la consola denominado **Actualizaciones y mantenimiento** que facilita la ubicación e instalación de las actualizaciones recomendadas.  

Algunas versiones solo están disponibles como actualizaciones de los sitios existentes desde la consola de Configuration Manager. Estas actualizaciones no se pueden usar para instalar un nuevo sitio de Configuration Manager. Por ejemplo, la actualización 1910 solo está disponible en la consola de Configuration Manager. Se usa para actualizar un sitio que ya ejecuta una versión compatible de Configuration Manager.

Periódicamente, también se publica una versión de actualización como una nueva versión de *línea base*. Por ejemplo, la versión de actualización 2002 es también una línea base. Use una versión de línea base para instalar un nuevo sitio o jerarquía. No empiece con una versión de línea base anterior, como 1802, y actualice a la versión más reciente. Use siempre la línea base más reciente.

Vea los siguientes artículos para más información:

- [Actualizaciones para Configuration Manager](../../servers/manage/updates.md)
- [Versiones de línea de base y versiones de actualización](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a> Punto de conexión de servicio  

La rama actual de Configuration Manager incluye un nuevo rol de sistema de sitio, el **punto de conexión de servicio**:  

- Es un punto de contacto para muchas características habilitadas para la nube.

- Descarga actualizaciones relacionadas con el sitio.

- Carga datos de diagnóstico y de uso sobre el sitio en el servicio de nube de Microsoft.

Este rol de sistema de sitio admite los modos de funcionamiento en línea y sin conexión. Para obtener más información, consulte [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md) (Sobre el punto de conexión del servicio).  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a> Datos de diagnóstico y de uso

Configuration Manager recopila datos de diagnóstico y de uso de los sitios y la infraestructura. Esta información se compila y se envía al servicio de nube de Microsoft mediante el punto de conexión de servicio. Configuration Manager necesita estos datos para descargar las actualizaciones correspondientes al entorno. Al configurar el punto de conexión de servicio, se puede especificar el nivel de los datos que se recopilan y si enviar los datos de manera automática (en línea) o manual (sin conexión).

Para obtener más información, vea [Diagnósticos y datos de uso](../diagnostics/diagnostics-and-usage-data.md).  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a> Característica en desuso  

Algunas características, como los equipos nativos basados en la [Compatibilidad con la Tecnología de administración activa (AMT) de Intel](#bkmk_AMT), se quitan de la consola de Configuration Manager. Otras características, como la Protección de acceso a redes, se quitan completamente. Además, algunos productos de Microsoft anteriores como Windows Vista, Windows Server 2008 y SQL Server 2008, ya no son compatibles.  

Para una lista de las características en desuso, consulte el artículo [Elementos eliminados y en desuso](deprecated/removed-and-deprecated.md).  

Para información detallada sobre productos, sistemas operativos y configuraciones compatibles, consulte [Configuraciones admitidas](../configs/supported-configurations.md).  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Compatibilidad para la Tecnología de administración activa (AMT) Intel  

La rama actual de Configuration Manager quita la compatibilidad nativa con equipos basados en AMT desde la consola de Configuration Manager. Los equipos basados en AMT siguen estando totalmente administrados cuando se usa el [complemento Intel SCS para Microsoft Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). El complemento permite el acceso a las funciones más recientes para administrar AMT, a la vez que elimina las limitaciones introducidas hasta que Configuration Manager pudo incorporar esos cambios.  

La eliminación de AMT integrada para Configuration Manager incluye la administración fuera de banda. El rol de sistema de sitio del punto de administración fuera de banda ya no está disponible.  

> [!Note]
> Este cambio no afecta a la administración fuera de banda en System Center 2012 Configuration Manager.

## <a name="changes-in-functionality"></a>Cambios en la funcionalidad

En las siguientes secciones se resumen algunos de los cambios significativos realizados en las áreas de características entre System Center 2012 R2 Configuration Manager y la versión 1511 de la rama actual de Configuration Manager. Para más información sobre los cambios más recientes en la funcionalidad, vea [Novedades de las versiones incrementales](whats-new-incremental-versions.md).

### <a name="client-deployment"></a>Implementación de cliente  

Configuration Manager presenta una nueva característica para probar las nuevas versiones de cliente de Configuration Manager antes de actualizar el resto del sitio con el nuevo software. Puede configurar una recopilación de preproducción en la que realizar un piloto en un cliente nuevo. Una vez que esté satisfecho con el nuevo software cliente de preproducción, puede promover el cliente para actualizar automáticamente el resto del sitio con la nueva versión.  

Para más información sobre cómo probar los clientes, consulte [Cómo probar las actualizaciones de cliente en una recopilación de preproducción](../../clients/manage/upgrade/test-client-upgrades.md).  

### <a name="os-deployment"></a>Implementación del sistema operativo  

Tenga en cuenta los siguientes cambios en la implementación del sistema operativo:

- En el Asistente para crear secuencia de tareas, hay disponible un nuevo tipo de secuencia de tareas: **Actualización de un sistema operativo desde un paquete de actualización**. Crea los pasos para actualizar equipos Windows 7 o Windows 8.1 a Windows 10. Para más información, consulte [Actualizar Windows a la versión más reciente](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- El almacenamiento en caché de Windows PE ya está disponible al implementar sistemas operativos. Los equipos que ejecutan una secuencia de tareas para implementar un sistema operativo pueden usar el almacenamiento en caché del mismo nivel de Windows PE para obtener contenido a partir de un origen de caché del mismo nivel, en lugar de descargar contenido desde un punto de distribución. Este comportamiento minimiza el tráfico WAN en escenarios de sucursales donde no existe un punto de distribución local. Para obtener más información, consulte [Preparar el almacenamiento en caché del mismo nivel de Windows PE para reducir el tráfico WAN](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

- Ahora puede ver el estado de Windows como un servicio de su entorno. También puede crear planes de mantenimiento para formar anillos de implementación y garantizar que los equipos de la rama actual de Windows 10 se mantengan actualizados cuando se presenten nuevas compilaciones. Además, puede ver alertas cuando los clientes de Windows 10 estén cerca del final del soporte técnico de su compilación. Para obtener más información, consulte [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md) (Administrar Windows como servicio).  

### <a name="application-management"></a>Administración de aplicaciones  

Tenga en cuenta los siguientes cambios en la administración de aplicaciones:

- Configuration Manager le permite implementar aplicaciones de Plataforma universal de Windows (UWP) para dispositivos que ejecutan Windows 10 y versiones posteriores. Para más información, consulte [Creación de aplicaciones Windows](../../../apps/get-started/creating-windows-applications.md).  

- El Centro de software tiene un aspecto renovado y moderno. Las aplicaciones disponibles para el usuario que antes solo aparecían en el catálogo de aplicaciones ahora se incluyen en la pestaña Aplicaciones del Centro de software. Este comportamiento hace que estas implementaciones sean más reconocibles y que los usuarios no necesiten consultar el catálogo de aplicaciones por separado. Además, ya no hace falta un explorador habilitado para Silverlight. Para obtener más información, consulte [Planear y configurar la administración de aplicaciones en Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

- El nuevo tipo de aplicación Windows Installer a través de MDM le permite crear e implementar aplicaciones basadas en Windows Installer para los equipos inscritos que ejecutan Windows 10. Para más información, consulte [Creación de aplicaciones Windows](../../../apps/get-started/creating-windows-applications.md).  

- En Configuration Manager 2012, para especificar un vínculo a una aplicación de la Tienda Windows, se podía especificar el vínculo directamente o buscar un equipo remoto que tuviese instalada la aplicación. En la rama actual de Configuration Manager, también se puede escribir el vínculo directamente, pero ahora, en lugar de buscar un equipo de referencia, puede examinar la tienda de la aplicación directamente desde la consola de Configuration Manager.  

### <a name="software-updates"></a>Actualizaciones de software  

Tenga en cuenta los siguientes cambios en las actualizaciones de software:

- Configuration Manager ahora puede detectar la diferencia entre los métodos de administración de actualización de software en los equipos. Concretamente, puede diferenciar entre un equipo Windows 10 que se conecta a Windows Update for Business (WUfB) y un equipo conectado a WSUS. El atributo **UseWUServer** es nuevo y especifica si el equipo se administra con WUfB. Puede usar esta configuración en una recopilación para quitar estos equipos de la administración de actualizaciones de software. Para obtener más información, consulte [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md) (Integración con Windows Update for Business en Windows 10).  

- Ahora ya puede programar y ejecutar la tarea de limpieza de WSUS desde la consola de Configuration Manager. En las propiedades **Componente de punto de actualización de software**, cuando seleccione ejecutar la tarea de limpieza de WSUS, se ejecutará en la siguiente sincronización de actualizaciones de software. Las actualizaciones de software expiradas se establecen en un estado rechazado en el servidor de WSUS y el agente de Windows Update de los equipos ya no las examinará. Para obtener más información, consulte [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md) (Programar y ejecutar la tarea de limpieza de WSUS).  

### <a name="compliance-settings"></a>Configuración de cumplimiento  

Tenga en cuenta los siguientes cambios en la configuración de cumplimiento:

- Configuration Manager mejora el flujo de trabajo para crear elementos de configuración. Ahora, cuando cree un elemento de configuración y seleccione las plataformas admitidas, solo están disponible las opciones relevantes para esa plataforma. Consulte [Introducción a la configuración de cumplimiento](../../../compliance/get-started/get-started-with-compliance-settings.md).  

- El Asistente para **crear elemento de configuración** ahora facilita la elección del tipo de elemento de configuración que quiere crear. Además, hay elementos de configuración nuevos y actualizados que están disponibles para los siguientes dispositivos:  

    - Dispositivos Windows 10 administrados con el cliente de Configuration Manager  

    - Dispositivos Mac OS X administrados con el cliente de Configuration Manager  

    - Equipos de escritorio y servidores de Windows administrados con el cliente de Configuration Manager  

    - Dispositivos Windows 8.1 y Windows 10 administrados sin el cliente de Configuration Manager  

    Para más información, consulte [Cómo crear elementos de configuración](../../../compliance/deploy-use/create-configuration-items.md).  

- Compatibilidad para administrar la configuración en equipos Mac OS X administrados sin el cliente de Configuration Manager.

### <a name="on-premises-mobile-device-management"></a>Administración local de dispositivos móviles  

Ahora puede administrar dispositivos móviles con la infraestructura local de Configuration Manager. La totalidad de los dispositivos y los datos de administración se controla localmente y no forma parte de Microsoft Intune ni de otros servicios en la nube. Este tipo de administración de dispositivos no necesita software cliente. Configuration Manager administra los dispositivos con una funcionalidad integrada en el sistema operativo del dispositivo.  

Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

## <a name="next-steps"></a>Pasos siguientes

[Novedades de versiones incrementales](whats-new-incremental-versions.md)
