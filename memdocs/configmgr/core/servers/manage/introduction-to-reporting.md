---
title: Introducción a los informes
titleSuffix: Configuration Manager
description: Obtenga información sobre el conjunto de herramientas y recursos disponibles para administrar los informes en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bfed31b820ac1f09b240122207b5bf27e432b10a
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607523"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Introducción a los informes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los informes de Configuration Manager proporcionan un conjunto de herramientas y recursos para usar las funciones avanzadas de informes de SQL Server Reporting Services en (SSRS) y Power BI Report Server. Ambas plataformas de creación de informes ofrecen una amplia experiencia de creación de informes personalizados. Los informes le ayudan a recopilar, organizar y presentar información sobre los abundantes datos de Configuration Manager de su organización. Configuration Manager proporciona numerosos informes predefinidos en Reporting Services que puede usar sin realizar ningún cambio. Puede duplicar y modificar los informes predeterminados de modo que satisfagan sus necesidades, o bien crear informes personalizados.

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services proporciona una gama completa de herramientas y servicios listos para usar que le ayudarán a crear, implementar y administrar informes para la organización. También cuenta con características de programación que permiten ampliar y personalizar la funcionalidad de informes. Reporting Services es una plataforma de creación de informes basada en servidor que proporciona exhaustivas funciones de informes para diferentes tipos de orígenes de datos.

Configuration Manager usa SQL Server Reporting Services como principal solución de informes. La integración con Reporting Services proporciona las siguientes ventajas:  

- Usa un sistema de informes estándar del sector para consultar la base de datos de Configuration Manager.  

- Muestra los informes mediante el Visor de informes de Configuration Manager o mediante el Administrador de informes, que es una conexión al informe basada en web.  

- Proporciona elevadas escalabilidad y disponibilidad y alto rendimiento.  

- Proporciona suscripciones a informes a las que pueden suscribirse los usuarios. Por ejemplo, un administrador puede suscribirse a un informe diario por correo electrónico en el que se detalla el estado de una implementación de actualización de software.

- Exporta informes en diferentes tipos de formatos conocidos.  

Para obtener más información, consulte [¿Qué es SQL Server Reporting Services (SSRS)?](/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports)

## <a name="power-bi-report-server"></a>Power BI Report Server

<!-- 3721603 -->

A partir de la versión 2002, puede integrar Power BI Report Server con los informes de Configuration Manager. Esta integración proporciona una visualización moderna y un mejor rendimiento. Además, la consola admite informes de Power BI de manera similar a como ya ocurre con SQL Server Reporting Services. Para obtener más información, vea [Integración con Power BI Report Server](powerbi-report-server.md).

Power BI Report Server es un servidor de informes local con un portal web en el que se muestran y se administran los informes. Incluye herramientas para crear informes de Power BI, informes paginados, informes móviles y KPI. Para obtener más información, vea [¿Qué es Power BI Report Server?](/power-bi/report-server/get-started)

## <a name="reporting-services-point"></a>Punto de servicios de informes

El punto de servicios de informes es un rol de sistema de sitio que se agrega a un servidor que ejecuta Microsoft SQL Server Reporting Services. El punto de servicios de informes realiza las funciones siguientes:

- Copia las definiciones de informe de Configuration Manager en Reporting Services.
- Crea carpetas de informes basadas en categorías de informe.
- Establece la directiva de seguridad en las carpetas de informes y los informes. Estas directivas se basan en los permisos basados en roles para los usuarios administrativos de Configuration Manager. En un intervalo de 10 minutos, el punto de servicios de informes se conecta con Reporting Services para volver a aplicar la directiva de seguridad si se ha cambiado.

Para obtener más información sobre cómo planear e instalar un punto de servicios de informes, consulte los artículos siguiente:

- [Planeación de informes](planning-for-reporting.md)

- [Configuración de informes](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Informes de Configuration Manager

Configuration Manager proporciona definiciones de informe para más de 400 informes en más de 50 carpetas de informes. Durante el proceso de instalación del punto de servicios de informes, los copia en la carpeta de informes raíz en SQL Server Reporting Services. La consola de Configuration Manager muestra los informes y los organiza en subcarpetas según la categoría de los informes.

Los informes no se propagan hacia arriba o hacia abajo en la jerarquía de Configuration Manager. Solo se ejecutan en la base de datos del sitio en el que se crean. Debido a que Configuration Manager replica los datos globales por toda la jerarquía, tendrá acceso a la información de toda ella en los informes. Cuando un informe recupera datos de la base de datos de un sitio, obtiene acceso a los datos del sitio tanto para el sitio actual como para los secundarios, y a los datos globales para todos los sitios de la jerarquía.

Al igual que otros objetos de Configuration Manager, los usuarios administrativos deben tener los permisos adecuados para ejecutar o modificar informes. Para ejecutar un informe, un usuario administrativo debe tener el permiso **Ejecutar informe** para el objeto. Para crear o modificar un informe, un usuario administrativo debe tener el permiso **Modificar informe** para el objeto.

### <a name="create-and-modify-reports"></a>Creación y modificación de informes

Para los informes basados en Reporting Services, Configuration Manager usa el Generador de informes de Microsoft SQL Server como herramienta exclusiva de creación y edición de informes tanto basados en modelo como basados en SQL. Al crear o editar un informe en la consola de Configuration Manager, se abrirá el Generador de informes. Para obtener más información, vea [Operaciones y mantenimiento de informes](operations-and-maintenance-for-reporting.md).

A partir de la versión 2002, para crear o editar informes de Power BI, la consola se integra con Power BI Desktop. Para obtener más información, vea [Creación de informes de Power BI](powerbi-report-server.md#create-power-bi-reports).

### <a name="run-reports"></a>Ejecutar informes

Si ejecuta un informe basado en Reporting Services en la consola de Configuration Manager, el Visor de informes se abre y se conecta a Reporting Services. Una vez que especifique los parámetros de informes requerido, Reporting Services recuperará los datos y mostrará los resultados en el visor. También puede conectarse a SQL Server Reporting Services, conectarse al origen de datos para el sitio y ejecutar informes.

A partir de la versión 2002, cuando se ejecuta un informe basado en Power BI, se abre en el explorador web.

### <a name="report-prompts"></a>Mensajes de informes

Puede configurar un mensaje de informe o un parámetro al crear o modificar un informe. Cree mensajes de informes para limitar o dirigir los datos que recupera un informe. Un informe puede contener más de un mensaje. Asegúrese de que los nombres de los mensajes sean exclusivos y solo contengan caracteres alfanuméricos que cumplan las normas de SQL Server para los identificadores.

Cuando se ejecuta un informe, el mensaje solicitará un valor para un parámetro necesario. En función del valor del parámetro, recuperará los datos del informe. Por ejemplo, el informe **Información de equipo sobre un equipo específico** solicita un nombre de equipo. Reporting Services pasa el valor especificado a una variable definida en la instrucción SQL del informe.

### <a name="report-links"></a>Vínculos de informes

Los vínculos de informes de Configuration Manager se usan en un informe de origen para proporcionar un acceso sencillo a datos adicionales. Por ejemplo, puede vincular a información más detallada sobre cada uno de los elementos del informe de origen. Si el informe de destino requiere uno o más mensajes para su ejecución, el informe de origen deberá contener una columna con los valores adecuados para cada mensaje.

El vínculo deberá especificar el número de columna con el valor para el mensaje. Por ejemplo:

- Hay un informe que muestra los equipos que el sitio ha detectado recientemente.
- Desde este, se vincula a otro informe que muestra los últimos mensajes que recibe el sitio para un equipo específico.
- Debe crear el vínculo y especificar que la columna `2` del informe de origen contiene el nombre del equipo. Este valor es un mensaje obligatorio para el informe de destino.
- Cuando ejecute el informe de origen, aparecerá un icono de vínculo a la izquierda de cada fila de datos.
- Cuando seleccione el icono de una fila, el Visor de informes pasará el valor de la columna especificada para dicha fila como valor de mensaje para el informe de destino.

Solo se puede configurar un vínculo para un informe, y dicho vínculo solo se puede conectar a un único informe de destino.

> [!WARNING]  
> Si mueve un informe de destino a otra carpeta de informes, cambiará la ubicación para el informe de destino. Configuration Manager no actualiza automáticamente el vínculo del informe de origen con la nueva ubicación, y el vínculo no funcionará en el informe de origen.

## <a name="report-folders"></a>Carpetas de informes

Las carpetas de informes proporcionan un método para ordenar y filtrar los informes que Configuration Manager almacena en Reporting Services. Las carpetas de informes son útiles si tiene muchos informes que administrar. Si instala un punto de servicios de informes, este copia los informes a Reporting Services y los organiza en más de 50 carpetas de informes. Las carpetas de informes son de sólo lectura. No se pueden modificar en la consola de Configuration Manager.

## <a name="report-subscriptions"></a>Suscripciones a informes

Una suscripción de informe en Reporting Services es una solicitud recurrente para entregar un informe a una hora específica o en respuesta a un evento. En la suscripción se especifica un formato de archivo de aplicación. Las suscripciones proporcionan una alternativa a ejecutar un informe a petición. Los informes a petición requieren que seleccione activamente el informe cada vez que desee verlo. Por el contrario, las suscripciones se pueden utilizar para programar y, a continuación, automatizar la entrega de un informe.

Puede administrar suscripciones a informes en la consola de Configuration Manager. El servidor de informes procesa las suscripciones y las distribuye mediante el uso de las extensiones de entrega que están implementadas en el servidor. De forma predeterminada, puede crear suscripciones que envíen informes a una carpeta compartida o a una dirección de correo electrónico.

Para obtener más información, vea [Administrar suscripciones a informes](operations-and-maintenance-for-reporting.md#bkmk_subscription).

## <a name="report-builder"></a>Generador de informes

Para los informes basados en Reporting Services, Configuration Manager usa el Generador de informes de Microsoft SQL Server como herramienta exclusiva de creación y edición de informes tanto basados en modelo como basados en SQL. Al crear o editar un informe en la consola de Configuration Manager, se abrirá el Generador de informes. Al crear o modificar un informe por primera vez, el Generador de informes se instalará automáticamente. La versión del Generador de informes asociada con la versión instalada de SQL Server se abre cuando se ejecutan o editan informes.  

 La instalación del Generador de informes agrega compatibilidad para más de 20 idiomas. Cuando se ejecuta el Generador de informes, muestra los datos en el idioma del sistema operativo del equipo local. Si el Generador de informes no es compatible con el idioma, mostrará los datos en inglés. El Generador de informes es compatible con todas las funciones de SQL Server Reporting Services, que incluyen las funcionalidades siguientes:

- Ofrece un entorno de creación de informes intuitivo, con un aspecto similar a Aplicaciones de Microsoft 365.  

- Ofrece el diseño de informes flexible del lenguaje RDL (Report Definition Language) de SQL Server.  

- Proporciona diversas formas de visualización de datos, incluidos gráficos e indicadores.  

- Proporciona cuadros de texto con formato enriquecido.  

- Exporta a formato de Microsoft Word.  

También puede abrir el Generador de informes directamente desde SQL Server Reporting Services.

## <a name="report-models-in-sql-server-reporting-services"></a>Modelos de informes en SQL Server Reporting Services

SQL Reporting Services usa modelos de informes para ayudarle a seleccionar elementos de la base de datos de Configuration Manager e incluirlos en informes basados en modelos. Cuando genera un informe, los modelos de informes solo exponen las vistas y elementos especificados para elegir entre ellos. Para crear informes basados en modelos, al menos un modelo de informes debe estar disponible.

Los modelos de informes tienen las siguientes características:

- Proporcionan nombres empresariales lógicos a los campos y las vistas de base de datos. Para generar informes, no es necesario conocer la estructura de base de datos de Configuration Manager.

- Agrupan los elementos lógicamente.  

- Definen relaciones entre los elementos.  

- Protegen los elementos del modelo para que los usuarios administrativos solo puedan ver los datos que tienen permiso para ver.

Aunque Configuration Manager proporciona modelos de informes de ejemplo, también puede definir modelos de informes para satisfacer los requisitos empresariales. Para obtener más información sobre cómo crear modelos de informes, consulte [Creación de modelos de informes personalizados](creating-custom-report-models-in-sql-server-reporting-services.md).

## <a name="next-steps"></a>Pasos siguientes

[Planeación de informes](planning-for-reporting.md)