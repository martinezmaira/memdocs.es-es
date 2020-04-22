---
title: Preguntas más frecuentes sobre datos de uso y diagnóstico
titleSuffix: Configuration Manager
description: Preguntas frecuentes sobre los datos de diagnóstico y uso en Configuration Manager
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60634ed8e275ff8496a08969054aa912a81b9d07
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688483"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>Preguntas frecuentes acerca de datos de diagnóstico y uso

*Se aplica a: Configuration Manager (rama actual)*

En este artículo encontrará respuestas a preguntas frecuentes sobre datos de diagnóstico y uso en Configuration Manager.

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a> ¿Puedo desactivar los datos de diagnóstico y uso?

Para administrar cuándo el sitio envía datos, use el punto de conexión de servicio en el modo sin conexión. Después, utilice la herramienta de conexión de servicio para enviar los datos manualmente. Vea los siguientes artículos para más información:

- [Acerca del punto de conexión de servicio](../../servers/deploy/configure/about-the-service-connection-point.md)
- [Uso de la herramienta de conexión de servicio](../../servers/manage/use-the-service-connection-tool.md)

Para admitir la nuevas versiones de Windows 10 y servicios en la nube como Microsoft Intune, debe actualizar la rama actual de Configuration Manager de forma regular. Microsoft necesita como mínimo el nivel básico de datos de diagnóstico y uso. Estos datos sirven para mantener el producto actualizado, mejorar la experiencia de actualización y mejorar la calidad y la seguridad del producto.

Si el punto de conexión de servicio está en modo sin conexión, no se envía ningún dato. Al pasar al modo en línea o usar la herramienta de conexión de servicio, se envían datos al servicio para comprobar si hay alguna actualización disponible.

También puede elegir el nivel de datos que Configuration Manager recopila. Para obtener más información, consulte [Niveles de datos de uso y diagnóstico](levels-overview.md).

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> ¿Qué es el período de retención de datos?

Microsoft almacena los datos de diagnóstico y uso de Configuration Manager durante un año.

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a> ¿Se envían datos de diagnóstico y uso cuando se ejecuta la configuración?

No. Solo se envían datos de diagnóstico y uso una vez que el sitio está instalado y en funcionamiento.

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> ¿Con qué frecuencia se envían los datos?

Los procedimientos almacenados de SQL se ejecutan cada siete días desde la fecha en que haya instalado el sitio.

- En el modo en línea, el punto de conexión de servicio carga los datos después de ejecutar las consultas.

- En el modo sin conexión, se usa la herramienta de conexión de servicio para cargar los datos. Los datos no están disponibles inicialmente para su uso sin conexión hasta que transcurran siete días tras la instalación del sitio.  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> ¿Los datos se pueden usar para formar un mapa de red?

No. Estos datos no reflejan ningún detalle de red (como direcciones IP) o información geográfica detallada. Para obtener más información, vea [Niveles de datos de diagnóstico y uso](levels-overview.md#bkmk_versions) y obtendrá más detalles sobre la versión que está usando.

Los datos incluyen información sobre la zona horaria de cada sitio. Esto puede ofrecer información general sobre la geolocalización y la dispersión global de los sitios de una jerarquía.

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a> ¿Se pueden ver datos en tablas de SQL personalizadas?

No. Configuration Manager recopila datos de uso y diagnóstico a través de procedimientos almacenados de SQL. Estos procedimientos almacenados se ejecutan en tablas de productos predeterminadas de la base de datos. Todas estas tablas SQL tienen el prefijo **TEL_** . Como parte de la consulta de detección de esquemas SQL, a todos los nombres de tabla se les aplica un algoritmo hash para establecer comparaciones con los valores predeterminados conocidos. Este comportamiento determina que hay tablas personalizadas en la base de datos. La presencia de tablas personalizadas indica a Microsoft que usted ha extendido el esquema de la base de datos desde el valor predeterminado. No incluye ninguno de los datos almacenados en esas tablas.

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a> ¿Se pueden ver otras bases de datos?

No. Los procedimientos almacenados para recopilar los datos se limitan a la base de datos de sitio de Configuration Manager. Microsoft no puede ver los nombres de otras bases de datos ni ningún dato en otras bases de datos.

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a> ¿Se envía algún dato a otros servicios en la nube integrados?

Sí, al integrar estos servicios con Configuration Manager. Cuando se produce una interacción con cualquier servicio en la nube, Configuration Manager envía algunos datos a ese servicio. Estos datos son específicos de ese servicio en la nube e independientes de los datos de diagnóstico y uso de Configuration Manager. Para obtener más información sobre los datos específicos que se usan en la interacción con otro servicio en la nube, vea la documentación correspondiente al servicio en cuestión.

Por ejemplo, los siguientes servicios en la nube forman parte de Microsoft Endpoint Manager:

- [Privacidad de datos de Análisis de escritorio](../../../desktop-analytics/privacy.md)
- [Privacidad y datos personales en Intune](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Requisitos de Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a> ¿Configuration Manager recopila datos personales?

No. Configuration no recopila ni transfiere datos personales ni datos de cliente. Se trata de un producto local que el usuario implementa, administra y opera directamente. Los datos de diagnóstico y uso que Microsoft recopila mejoran la experiencia de instalación, la calidad y la seguridad de las versiones futuras.

Para obtener más información sobre los datos de Configuration Manager, vea [Niveles de datos de uso y diagnóstico](levels-overview.md).
