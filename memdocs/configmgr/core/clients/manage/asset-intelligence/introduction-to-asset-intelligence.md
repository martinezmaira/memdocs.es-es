---
title: Introducción a Asset Intelligence
titleSuffix: Configuration Manager
description: Use Asset Intelligence en Configuration Manager para inventariar y administrar el uso de licencias de software en toda la empresa.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695093"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Introducción a Asset Intelligence en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede inventariar y administrar el uso de licencias de software en toda la empresa mediante el catálogo Asset Intelligence. Asset Intelligence agrega clases de inventario de hardware para mejorar la amplitud de la información que recopila Configuration Manager. Esta información incluye los títulos de software y hardware que se usan en el entorno. Más de 60 informes presentan esta información con un formato fácil de usar. Muchos de estos informes vinculan a otros más específicos, en los que puede consultar información general y profundizar para obtener información más detallada. 

Puede agregar información personalizada al catálogo Asset Intelligence, como categorías de software personalizadas, familias de software, etiquetas de software y requisitos de hardware. Si quiere actualizar dinámicamente el catálogo Asset Intelligence con la información más reciente disponible, conéctelo con Microsoft Cloud. 

No dude en usar Asset Intelligence para ayudar a conciliar el uso de licencias de software empresarial. Importe la información de licencias de software en la base de datos del sitio de Configuration Manager para verla con el software que se está usando.  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a> Catálogo Asset Intelligence  

El catálogo Asset Intelligence es un conjunto de tablas de base de datos almacenadas en la base de datos del sitio. Dichas tablas contienen información de categorización e identificación de más de 300 000 títulos y versiones de software También se usan para administrar requisitos de hardware de títulos de software concretos.  

Asset Intelligence ofrece información de licencias de software de los títulos de software que se usan, tanto de Microsoft como de otros fabricantes. Hay disponible un conjunto predefinido de requisitos de hardware de títulos de software en el catálogo Asset Intelligence y puede crear nueva información de requisitos de hardware definida por el usuario para cumplir requisitos personalizados. Además, puede personalizar la información en el catálogo Asset Intelligence y cargar información de títulos de software en Microsoft Cloud para su categorización.  

Las actualizaciones del catálogo Asset Intelligence que incluyen software de reciente publicación están disponibles para su descarga periódicamente a fin de realizar actualizaciones masivas del catálogo. También se puede actualizar dinámicamente mediante el uso del punto de sincronización de Asset Intelligence.  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Categorías de software  

Las categorías de software de Asset Intelligence se usan para categorizar en líneas generales los títulos de software inventariado y como agrupaciones de alto nivel de familias de software más específicas. Por ejemplo, una categoría de software podría ser empresas de energía, y una familia de software dentro de esa categoría de software podría ser petróleo y gas o hidroeléctrica. Existen muchas categorías de software predefinidas en el catálogo Asset Intelligence. Además, se pueden crear categorías definidas por el usuario para definir adicionalmente el software inventariado. El estado de validación de todas las categorías de software predefinidas es siempre **Validado**, mientras que la información de categorías de software personalizadas que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**. 

Para obtener más información sobre cómo administrar las categorías de software, vea [Configurar Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> La información de categorías de software predefinidas que se almacena en el catálogo Asset Intelligence es de solo lectura y no se puede cambiar ni eliminar. Los usuarios administrativos pueden agregar, modificar o eliminar categorías de software definidas por el usuario.  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a> Familias de software  

Las familias de software de Asset Intelligence se usan para definir los títulos de software inventariado dentro de las categorías de software. Existen muchas familias de software predefinidas en el catálogo Asset Intelligence. Además, se pueden crear categorías definidas por el usuario para definir adicionalmente el software inventariado. El estado de validación de todas las familias de software predefinidas es siempre **Validado**, mientras que la información de familias de software personalizadas que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**. 

Para obtener más información sobre cómo administrar las familias de software, vea [Configurar Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> La información de las familias de software predefinidas es de solo lectura y no se puede cambiar. Los usuarios administrativos pueden agregar, modificar o eliminar familias de software definidas por el usuario.  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a> Etiquetas de software  

Las etiquetas de software personalizadas de Asset Intelligence permiten crear filtros para agrupar los títulos de software y para verlos en informes de Asset Intelligence. Puede usar etiquetas de software para crear grupos definidos por el usuario de títulos de software que compartan un atributo común. Por ejemplo, podría crear una etiqueta de software denominada Shareware, asociarla con títulos de shareware inventariados y ejecutar un informe para mostrar todos los títulos de software con esa etiqueta. No hay ninguna etiqueta predefinida. El estado de validación de las etiquetas de software siempre es **Definido por el usuario**. 

Para obtener más información sobre cómo administrar las etiquetas de software, vea [Configurar Asset Intelligence](configuring-asset-intelligence.md).  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  

Use la información de requisitos de hardware para comprobar que los equipos cumplan los requisitos de hardware de los títulos de software antes de que se destinen a implementaciones de software. Puede administrar los requisitos de hardware de títulos de software en el área de trabajo **Assets and Compliance** (Activos y compatibilidad), en el nodo **Requisitos de hardware**, en el nodo **Asset Intelligence**. 

Existen muchos requisitos de hardware predefinidos en el catálogo Asset Intelligence. Además, puede crear información de requisitos de hardware definidos por el usuario para cumplir requisitos personalizados. El estado de validación de todos los requisitos de hardware predefinidos es siempre **Validado**, mientras que la información de requisitos de hardware definidos por el usuario que se hayan agregado al catálogo Asset Intelligence es **Definido por el usuario**. 

Para obtener más información sobre cómo administrar los requisitos de hardware, vea [Configurar Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Los requisitos de hardware que se muestran en la consola de Configuration Manager se recuperan desde el catálogo Asset Intelligence y no se basan en información de títulos de software inventariado de clientes. 
> 
> La información de requisitos de hardware no se actualiza como parte del proceso de sincronización con Microsoft. 
> 
> Puede crear requisitos de hardware definidos por el usuario para software inventariado que no tenga requisitos de hardware asociados.  

De forma predeterminada, se muestra la siguiente información por cada requisito de hardware de la lista:  

- **Título de software**: título de software asociado con el requisito de hardware.  

- **CPU mínima (MHz)** : velocidad del procesador mínima, en megahercios (MHz), que requiere el título de software.  

- **RAM mínima (KB)** : memoria RAM mínima, en kilobytes (KB), que requiere el título de software.  

- **Espacio en disco mínimo (KB)** : espacio disponible en disco duro mínimo, en KB, que requiere el título de software.  

- **Tamaño del disco mínimo (KB)** : tamaño de disco duro mínimo, en KB, que requiere el título de software.  

- **Estado de validación**: estado de validación del requisito de hardware.  

Los requisitos de hardware predefinidos almacenados en el catálogo Asset Intelligence son de solo lectura y no se pueden eliminar. Los usuarios administrativos pueden agregar, modificar o eliminar requisitos de hardware definidos por el usuario de títulos de software que no se almacenan en el catálogo Asset Intelligence.  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a> Títulos de software inventariado  

Para ver la información de títulos de software inventariado en la consola de Configuration Manager, vaya al área de trabajo **Assets and Compliance** (Activos y compatibilidad), expanda el nodo **Asset Intelligence** y seleccione el nodo **Software inventariado**. El Agente de inventario de hardware recopila la información de software inventariado de clientes de Configuration Manager basada en los títulos de software que se almacenan en el catálogo Asset Intelligence.  

> [!Note]  
> El Agente de inventario de hardware recopila inventario en función de las clases de informes de inventario de hardware de Asset Intelligence que habilite. Para obtener más información sobre cómo habilitar las clases de informes, vea [Configurar Asset Intelligence](configuring-asset-intelligence.md).  

De forma predeterminada, se muestra la siguiente información por cada título de software inventariado:  

- **Nombre**: especifica el nombre del título de software inventariado.  

- **Proveedor**: nombre del proveedor que ha desarrollado el título de software inventariado.  

- **Versión**: versión de producto del título de software inventariado.  

- **Categoría**: categoría de software que está asignada actualmente al título de software inventariado.  

- **Familia**: familia de software que está asignada actualmente al título de software inventariado.  

- **Etiqueta** [**1**, **2** y **3**]: etiquetas personalizadas asociadas con el título de software. Los títulos de software inventariado pueden tener hasta tres etiquetas personalizadas asociadas a ellos.  

- **Recuento**: número de clientes de Configuration Manager que han inventariado el título de software.  

- **Estado**: estado de validación del título de software inventariado.  

> [!NOTE]  
> Puede cambiar la información de categorización del software inventariado únicamente en el sitio de nivel superior de la jerarquía. Esta información incluye el nombre de producto, proveedor, categoría de software y familia de software. Después de modificar la información de categorización de software predefinido, el estado de validación del software cambia de **Validado** a **Definido por el usuario**.  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a> Punto de sincronización de Asset Intelligence  

El punto de sincronización de Asset Intelligence es un rol de sistema de sitio de Configuration Manager. Se usa para conectarse a la nube de Microsoft mediante el puerto TCP 443 para administrar las actualizaciones de información del catálogo dinámico. Instale este rol de sitio únicamente en el sitio de nivel superior de la jerarquía. Debe configurar todas las personalizaciones del catálogo Asset Intelligence mediante una consola de Configuration Manager conectada al sitio de nivel superior. 

Aunque todas las actualizaciones se configuran en el sitio de nivel superior, la información del catálogo se replica en los demás sitios de la jerarquía. El rol de sitio permite solicitar sincronización del catálogo a petición con Microsoft o programar una sincronización del catálogo automática. Además de descargar la nueva información del catálogo, el punto de sincronización de Asset Intelligence puede cargar la información de títulos de software personalizado en Microsoft para su categorización. Microsoft trata todos los títulos de software cargados como información pública. Asegúrese de que los títulos de software personalizado no incluyen información confidencial o de propiedad.  

Después de enviar un título de software sin categoría, Microsoft no lo revisa hasta que haya al menos cuatro solicitudes de categorización de clientes para el mismo título de software. Después, los investigadores de Microsoft identifican, categorizan y ponen la información de categorización del título de software a disposición de todos los clientes que usan el servicio en línea. Los títulos de software que tengan la mayoría de solicitudes de categorización reciben la mayor prioridad para la categorización. El software personalizado y las aplicaciones de línea de negocio no suelen recibir una categoría. No envíe estos títulos de software a Microsoft para su categorización.  

Es necesario punto de sincronización de Asset Intelligence para conectarse a Microsoft Cloud. Para obtener información sobre cómo instalar el rol, vea [Configurar Asset Intelligence](configuring-asset-intelligence.md).  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Página principal de Asset Intelligence  

El nodo **Asset Intelligence** del área de trabajo **Assets and Compliance** (Activos y compatibilidad) es la página principal de Asset Intelligence en Configuration Manager. En esta página principal se muestra una vista de panel de resumen para obtener información sobre el catálogo Asset Intelligence.  

> [!NOTE]  
> La página principal de **Asset Intelligence** no se actualiza automáticamente mientras se está visualizando.  

La página principal de **Asset Intelligence** incluye las siguientes secciones:  

- **Sincronización de catálogos**: ofrece información sobre si Asset Intelligence está habilitada y sobre el estado actual del punto de sincronización de Asset Intelligence.  

    > [!NOTE]  
    > Esta sección se muestra en la página principal únicamente cuando se instala un punto de sincronización de Asset Intelligence.  

    En la sección también se proporciona la siguiente información:  

    - Programación de sincronización  

    - Si se ha importado una declaración de licencias de cliente   

    - Última actualización de estado  

    - Hora de la siguiente actualización programada  

    - Número de cambios después de instalar el punto de sincronización de Asset Intelligence   

- **Estado de software inventariado**: ofrece el recuento y porcentaje de software inventariado, categorías de software y familias de software que identifica Microsoft o un administrador, están pendientes de identificación en línea, o no tienen identificación y no están pendientes de ella. La información que se muestra en formato de tabla muestra el recuento de cada uno, y la información mostrada en el gráfico muestra el porcentaje de cada una.  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Informes de Asset Intelligence  

Los informes de Asset Intelligence se encuentran en la consola de Configuration Manager, en el área de trabajo **Supervisión**, en el nodo **Informes** de la carpeta **Asset Intelligence**. Los informes ofrecen información sobre el hardware, la administración de licencias y el software. Para obtener más información sobre los informes en Configuration Manager, consulte [Introducción a los informes](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
> La precisión de la cantidad de títulos de software instalados y la información de licencias que se muestra en los informes de Asset Intelligence puede diferir del número real de títulos de software instalados o licencias que se usan en el entorno. Esta diferencia se debe a las complejas dependencias y limitaciones relacionadas con la información de licencia de software de los títulos de software que están instalados en entornos empresariales. No use los informes de Asset Intelligence como única fuente para determinar el cumplimiento de licencias de software adquirido.  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a> Informes de hardware  

Los informes de hardware de Asset Intelligence ofrecen información sobre los recursos de hardware de la organización. Gracias a la información de inventario de hardware, como la velocidad, la memoria y los dispositivos periféricos, los informes de hardware de Asset Intelligence pueden presentar información sobre dispositivos USB, sobre hardware que debe actualizarse e incluso sobre los equipos que no estén preparados para una actualización de software concreta.  

> [!NOTE]  
> Algunos datos de usuario de los informes de hardware de Asset Intelligence se recopilan del registro de eventos de seguridad de Windows. Para conseguir una mayor precisión en los informes, borre este registro cuando se reasigne un equipo a un nuevo usuario.  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a> Informes de administración de licencias  

Los informes de administración de licencias de Asset Intelligence ofrecen datos sobre las licencias que se están usando. En el informe de **contabilidad de licencias** se muestra una lista de las aplicaciones de Microsoft instaladas en un formato coherente con la Declaración de licencias de Microsoft (MLS). Este formato ofrece un método práctico para hacer coincidir licencias adquiridas con licencias usadas. Otros informes de administración de licencias ofrecen información sobre los equipos que actúan como servidores que ejecutan el Servicio de administración de claves (KMS) para las estadísticas de activaciones de Windows.  

> [!IMPORTANT]  
> Varios de los informes de administración de licencias de Asset Intelligence presentan información sobre la función de KMS, un método de administración de licencias por volumen. Si no ha implementado un servidor KMS, es posible que algunos informes no devuelvan datos.  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a> Informes de software  

Los informes de software de Asset Intelligence ofrecen información sobre familias de software, categorías y títulos de software concretos que están instalados en equipos de la organización. Los informes de software presentan información como los objetos auxiliares de explorador y el software que se inicia automáticamente. Estos informes se pueden usar para identificar adware, spyware y otro malware. También se pueden usar para identificar la redundancia de software, a fin de ayudar a agilizar la adquisición de software y el soporte técnico.  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a> Informes de etiquetas de identificación de software  

Los informes de etiquetas de identificación de software de Asset Intelligence proporcionan información sobre el software que contiene una etiqueta de identificación de software que sea compatible con ISO/IEC 19770-2. Las etiquetas de identificación de software proporcionan información autorizada que se usa para identificar el software instalado. Si habilita la clase de informes de inventario de hardware **SMS_SoftwareTag**, Configuration Manager recopila información sobre el software con etiquetas de identificación de software. 

En los informes siguientes se ofrece información sobre el software:  

- **Software 14A - Búsqueda de software con etiqueta de identificación de software habilitada**: recuento de software instalado con una etiqueta de identificación de software habilitada.  

- **Software 14B - Equipos con etiqueta de identificación de software específica habilitada instalada**: todos los equipos que tienen software instalado con una etiqueta de identificación de software habilitada especificada.  

- **Software 14C - Software instalado con etiqueta de identificación de software habilitada en un equipo específico**: todo el software instalado con una etiqueta de identificación de software específica habilitada en un equipo específico.  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a> Limitaciones de los informes  

Los informes de Asset Intelligence pueden ofrecer grandes cantidades de información sobre los títulos de software instalado y las licencias de software adquiridas que se están usando. No use esta información como única fuente para determinar el cumplimiento de licencias de software adquirido.  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Dependencias de ejemplo  
La precisión de la cantidad mostrada en los informes de Asset Intelligence para los títulos de software instalados y la información de licencia puede diferir de las cantidades reales que se usan actualmente. Esta diferencia se debe a las complejas dependencias relacionadas con la información de licencia de software de los títulos de software que se usan en entornos empresariales. En los ejemplos siguientes se muestran las dependencias relacionadas con el inventario del software instalado en la empresa mediante el uso de Asset Intelligence que podrían afectar a la precisión de los informes de Asset Intelligence:  

- **Dependencias del inventario de hardware del cliente**: los informes del software instalado de Asset Intelligence se basan en datos que se recopilan de clientes de Configuration Manager mediante la ampliación del inventario de hardware para habilitar los informes de Asset Intelligence. Debido a esta dependencia de los informes de inventario de hardware, los informes de Asset Intelligence reflejan solo los datos de clientes que completen correctamente los procesos de inventario de hardware con las clases de informes de WMI de Asset Intelligence habilitadas. Como los clientes de Configuration Manager realizan procesos de inventario de hardware según una programación definida por el usuario administrativo, puede producirse un retraso en los informes de datos que afecte a la precisión de los informes de Asset Intelligence. 

    Por ejemplo, un título de software con licencia inventariado podría desinstalarse después de que el cliente finalice un ciclo de inventario de hardware correcto. En los informes de Asset Intelligence el título del software se muestra como instalado hasta el siguiente ciclo de informes de inventario de hardware del cliente programado.  

- **Dependencias de paquetes de software**: Los informes de Asset Intelligence se basan en datos de títulos de software instalados que se recopilan mediante procesos estándares de inventario de hardware de cliente de Configuration Manager. Algunos datos de títulos de software podrían no recopilarse correctamente. Ejemplos que provocarían informes inexactos de Asset Intelligence:  

    - Instalaciones de software que no cumplen los procesos de instalación estándar  

    - Instalaciones de software que se cambiaron antes de la instalación   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Limitaciones legales  
La información que se muestra en los informes de Asset Intelligence está sujeta a numerosas limitaciones. La información mostrada no supone asesoramiento legal, contable ni profesional. La información que proporcionan los informes de Asset Intelligence es meramente informativa. No la use como única fuente para determinar el cumplimiento del uso de licencias de software.  

Las siguientes limitaciones son ejemplos de un uso de Asset Intelligence que podría afectar a la precisión de los informes:  

- **Limitaciones de cantidad de usos de las licencias de Microsoft**:  

    - La cantidad de licencias de software de Microsoft adquiridas se basa en la información que facilitan los administradores. Debe revisarla con cuidado para asegurarse de que se ofrece el número correcto de licencias de software.  

    - La cantidad de licencias de software de Microsoft que se muestra en el informe solo contiene información sobre licencias de software de Microsoft adquiridas a través de programas de licencias por volumen. No refleja la información de licencias de software adquiridas a través de minoristas, OEM u otros canales de ventas de licencias de software.  

    - Las licencias de software adquiridas en los últimos 45 días podrían no incluirse en la cantidad de licencias de software de Microsoft que se muestra en el informe, debido a las programaciones y los requisitos de informes de los distribuidores de software.  

    - Las transferencias de licencias de software de las fusiones o adquisiciones entre compañías podrían no reflejarse en las cantidades de licencias de software de Microsoft.  

    - Los términos y condiciones no estándares de un acuerdo de Programas de Licencias por Volumen de Microsoft (MVLS) podrían afectar al número de licencias de software que aparecen en el informe. Podría ser necesario que un representante de Microsoft realizara revisiones adicionales.  

- **Limitaciones de cantidades de títulos de software instalados**: Los clientes de Configuration Manager deben completar correctamente los ciclos de informes de inventario de hardware de los informes de Asset Intelligence para notificar con exactitud la cantidad de títulos de software instalados. Podría producirse un retraso entre la instalación o desinstalación de un título de software con licencia después de un ciclo de informes de inventario de hardware correcto. Esta acción podría no reflejarse en los informes de Asset Intelligence que se ejecutaron antes de que el cliente informe del siguiente inventario de hardware programado.  

- **Limitaciones de conciliación de licencias**: la conciliación entre la cantidad de títulos de software instalados y la cantidad de licencias de software adquiridas se calcula mediante una comparación entre la cantidad de licencias que especifica el administrador y el número de títulos de software instalados, recopilados de los inventarios de hardware de los clientes de Configuration Manager, según la programación establecida por el administrador. Esta comparación no representa una conclusión final de Microsoft sobre las situaciones de las licencias. La posición de licencia depende de los derechos licencias y el uso de título determinado software concedidos por los términos de licencia.  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a> Estados de validación de Asset Intelligence  

Los estados de validación de Asset Intelligence representan el origen y el estado de validación actual de la información del catálogo Asset Intelligence. En la tabla siguiente se muestran los posibles estados de validación de Asset Intelligence y las acciones de administrador que pueden provocarlos.  

| Estado | Definición | Acción del administrador | Comentario |  
|---------------|--------------------|------------------------------|-----------------|  
|**Validado**|Los investigadores de Microsoft han definido el elemento del catálogo.|Ninguno|Mejor estado.|  
|**Definido por el usuario**|Los investigadores de Microsoft no han definido el elemento del catálogo.|Personalice la información del catálogo local.|Este estado se muestra en los informes de Asset Intelligence.|  
|**Pendiente**|Los investigadores de Microsoft no han definido el elemento de catálogo, pero el elemento se ha enviado a Microsoft para su categorización.|Ninguna otra acción tras solicitar la categorización.|El elemento del catálogo permanece en este estado hasta que los investigadores de Microsoft categoricen el elemento y se sincronice el catálogo Asset Intelligence.|  
|**Actualizable**|Microsoft ha categorizado de forma diferente un elemento de catálogo definido por el usuario durante una sincronización del catálogo.|Use la acción **Resolver conflicto** para decidir si quiere usar la nueva información de categorización o el valor definido por el usuario anterior. Para obtener más información sobre cómo resolver conflictos, vea [Cómo usar Asset Intelligence](operations-for-asset-intelligence.md).|Después de resolver un conflicto de categorización, el elemento no se valida de nuevo como en conflicto a menos que haya actualizaciones de categorización posteriores que introduzcan nueva información sobre el elemento.|  
|**Sin categoría**|Los investigadores de Microsoft no han definido el elemento del catálogo, el elemento no se ha enviado a Microsoft para su categorización y el administrador no ha asignado un valor de categorización definido por el usuario.|Solicite categorización o personalice la información del catálogo local. Para obtener más información, vea [Cómo usar Asset Intelligence](operations-for-asset-intelligence.md).|Ninguno|  

> [!NOTE]  
> Los elementos del catálogo enviados a Microsoft para su categorización tienen un estado de validación **Pendiente** en un sitio de administración central, pero se siguen mostrando con un estado de validación **Sin categoría** en los sitios primarios secundarios.  

Para obtener ejemplos de cuándo puede pasar un estado de validación de un estado a otro, vea [Ejemplo de transiciones de estado de validación de Asset Intelligence ](example-validation-state-transitions-for-asset-intelligence.md).  
