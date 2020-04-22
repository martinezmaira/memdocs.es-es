---
title: Información de privacidad adicional
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Microsoft recopila y usa datos de Configuration Manager.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6891a46050bb83e54fb34b97d9129fcb5873785
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701423"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Más información sobre la privacidad de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*


## <a name="updates-and-servicing"></a>Actualizaciones y mantenimiento

Configuration Manager usa un modelo de actualización que ayuda a mantener su entorno actual con las últimas actualizaciones y características. Esta característica utiliza un rol de sistema de sitio denominado punto de conexión de servicio. Elija el servidor donde instalar este rol. 

Para obtener más información acerca de la información recopilada y cómo se usa, consulte [Datos de uso](#usage-data).



## <a name="usage-data"></a>Datos de uso

Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo que Microsoft usa para mejorar la experiencia de instalación, la calidad y la seguridad de las versiones futuras.
Los datos de uso y diagnóstico están habilitados para cada jerarquía de Configuration Manager. Consta de las consultas de SQL Server que se ejecutan de forma semanal en cada sitio primario y en el sitio de administración central. Cuando la jerarquía usa un sitio de administración central, los datos de los sitios primario se replican en ese sitio. En el sitio de nivel superior de la jerarquía, el punto de conexión de servicio envía esta información cuando busca actualizaciones. Si el punto de conexión de servicio está en modo sin conexión, la información se transfiere mediante la herramienta de conexión de servicio.

Configuration Manager solamente recopila datos de la base de datos de SQL Server del sitio y no recopila datos directamente de los clientes ni de los servidores de sitios.

Los administradores pueden cambiar el nivel de datos recopilado en la sección **Datos de uso** de la consola de Configuration Manager.

Para más información sobre los niveles y la configuración de los datos de uso, vea [Diagnósticos y datos de uso](../diagnostics/diagnostics-and-usage-data.md).



## <a name="log-analytics-connector"></a>Conector de Log Analytics

El conector de Log Analytics sincroniza datos, como recopilaciones, de Configuration Manager al servicio en la nube de Azure. El identificador de suscripción de Azure y la clave secreta se almacenan en la base de datos de Configuration Manager cuando un administrador configura la característica. El secreto de cliente de Azure Active Directory y la clave compartida del área de trabajo de Azure se almacenan en la base de datos local de Configuration Manager. Todas las comunicaciones entre Configuration Manager y Azure usan HTTPS. No se proporciona a Microsoft ninguna información adicional sobre las recopilaciones más allá de datos de diagnóstico y uso aleatorios. 

Para obtener más información acerca de la información que recopila Log Analytics, consulte [Seguridad de datos de Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Asset Intelligence

Asset Intelligence permite a los administradores definir, realizar un seguimiento y administrar de manera proactiva la conformidad con los estándares de configuración. La medición y la creación de informes sobre la implementación y el uso de aplicaciones físicas y virtuales ayuda a las organizaciones a tomar mejores decisiones empresariales acerca de las licencias de software y el cumplimiento con los contratos de licencia. Después de recopilar datos de uso de los clientes de Configuration Manager, puede usar características distintas para ver los datos, incluidas las recopilaciones, las consultas y los informes.

Durante cada sincronización, se descarga un catálogo de software conocido de Microsoft. Puede enviar información de Microsoft acerca de los títulos de software sin categorizar detectados dentro de su organización que se van a investigar y agregar al catálogo. Antes de cargar esta información, un cuadro de diálogo muestra los datos que se van a cargar. Los datos cargados no se pueden recuperar. Asset Intelligence no envía información relativa a los usuarios y equipos o el uso de licencias a Microsoft.

Después de cargar un título de software, los investigadores de Microsoft identifican, categorizan y ponen ese conocimiento a disposición de los demás clientes que usan esta característica y de otros consumidores del catálogo. Cualquier título de software cargado se hace público. La aplicación y su categorización pasan a formar parte del catálogo y después se pueden descargar a otros consumidores del catálogo. Antes de configurar la recopilación de datos de Asset Intelligence y decidir si desea enviar información a Microsoft, tenga en cuenta los requisitos de privacidad de su organización.

Asset Intelligence no está habilitado de manera predeterminada en Configuration Manager. La carga de títulos sin categorizar nunca se produce automáticamente, y el sistema no está diseñado para automatizar esta tarea. Debe seleccionar manualmente y aprobar la carga de cada título de software.



## <a name="endpoint-protection"></a>Endpoint Protection

Microsoft Cloud Protection Service se conocía anteriormente como Microsoft Active Protection Service o MAPS.

Los productos válidos son System Center Endpoint Protection y la característica Endpoint Protection de Configuration Manager (para la administración de System Center Endpoint Protection y Windows Defender en Windows 10). Esta característica no está implementada para las versiones Linux y Mac de System Center Endpoint Protection.

La comunidad antimalware Microsoft Cloud Protection Service es una comunidad voluntaria internacional en línea que agrupa a los usuarios de System Center Endpoint Protection. Cuando se une a Microsoft Cloud Protection Service, System Center Endpoint Protection envía información automáticamente a Microsoft. Microsoft usa la información para determinar el software para investigar en busca de posibles amenazas y ayudar a mejorar la eficacia de System Center Endpoint Protection. Esta comunidad ayuda a detener la propagación de nuevas infecciones de software malintencionado. Si un informe de Microsoft Cloud Protection Service incluye detalles sobre malware u otro software potencialmente no deseado que el cliente de Endpoint Protection puede quitar, Microsoft Cloud Protection Service descarga la firma más reciente para proceder. Microsoft Cloud Protection Service también puede encontrar "falsos positivos" y corregirlos. (Los falsos positivos son elementos inicialmente identificados como malware de forma errónea que resultan no serlo). 

Los informes de Microsoft Cloud Protection Service incluyen información sobre posibles archivos de malware, como nombres de archivo, hash criptográfico, proveedor, tamaño y marcas de fecha. Además, Microsoft Cloud Protection Service podría recopilar direcciones URL completas para indicar el origen del archivo. Es posible que estas direcciones URL incluyan ocasionalmente información personal como términos de búsqueda o datos escritos en formularios. También es posible que los informes incluyan las acciones tomadas cuando Endpoint Protection notificó sobre el software no deseado. Los informes de Microsoft Cloud Protection Service incluyen esta información para ayudar a Microsoft a evaluar la eficacia de Endpoint Protection a la hora de detectar y quitar el malware y el software potencialmente no deseado y para intentar identificar nuevo malware.

Puede unirse a Microsoft Cloud Protection Service si tiene una suscripción básica o avanzada. Los informes de los miembros básicos tienen la información descrita anteriormente. Los informes para un miembro avanzado son más completos y pueden incluir detalles adicionales sobre el software detectado por Endpoint Protection, como la ubicación del software, nombres de archivos, cómo funciona el software y el impacto que ha tenido en el equipo. Estos informes y los de otros usuarios de Endpoint Protection que participan en Microsoft Cloud Protection Service, ayudan a los investigadores de Microsoft a detectar las nuevas amenazas con más rapidez. Posteriormente, se crean las definiciones de malware para programas que cumplen los criterios de análisis y las definiciones actualizadas se ponen a disposición de todos los usuarios a través de Microsoft Update.

Para que sea más fácil detectar y solucionar determinados tipos de infecciones de malware, el producto envía regularmente a Microsoft Cloud Protection Service información sobre el estado de seguridad del PC. Esta información incluye detalles sobre la configuración de seguridad del PC y archivos de registro que describen los controladores y otro software que se carga cuando arranca el PC.

También se envía un número que identifica al equipo de forma exclusiva. Además, Microsoft Cloud Protection Service podría recopilar las direcciones IP a las que se conectan los potenciales archivos de malware.

Los informes de Microsoft Cloud Protection Service se usan para mejorar el software y los servicios de Microsoft. También es posible usar los informes para estadísticas o con otros fines de pruebas o analíticos, y para generar definiciones. El acceso a los informes solo se proporciona a los empleados de Microsoft, los contratistas, los partners y los proveedores que tengan la necesidad empresarial de usarlos.

Microsoft Cloud Protection Service no recopila intencionadamente información personal. En la medida en que Microsoft Cloud Protection Service recopila información personal, Microsoft no usa dicha información para identificarle ni ponerse en contacto con usted.

Para obtener más información, vea [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Jerarquía del sitio – vista geográfica con Bing Maps

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, seleccione el nodo **Jerarquía de sitio** y cambie a la **Vista geográfica**. Esta visa le permite usar mapas proporcionados por Mapas de Bing de Microsoft para ver la topología del servidor físico de Configuration Manager. Para habilitar esta característica, se envía información de ubicación proporcionada por usted desde su servidor al servicio web de Mapas de Bing.

Microsoft utiliza la información para hacer funcionar y mejorar Microsoft Bing Maps y otros sitios y servicios de Microsoft. Para más información, vea la [Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkId=823548).

Puede elegir no utilizar la Vista geográfica para la Jerarquía del sitio. La vista Diagrama de jerarquía predeterminada le permite ver la jerarquía y no usa el servicio Mapas de Bing.
