---
title: Estrategia de jerarquía de origen
titleSuffix: Configuration Manager
description: Configure una jerarquía de origen y recopile datos de un sitio de origen antes de configurar un trabajo de migración de Configuration Manager.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28960753da06058ef181f94a5d11d9f2327ebf56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702863"
---
# <a name="plan-a-source-hierarchy-strategy-in-configuration-manager"></a>Planeación de una estrategia de jerarquía de origen en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Antes de configurar un trabajo de migración en el entorno de Configuration Manager, debe configurar una jerarquía de origen y recopilar datos de, al menos, un sitio de origen en esa jerarquía. Las secciones siguientes le ayudarán a planear la configuración de jerarquías de origen, la configuración de sitios de origen y a determinar cómo Configuration Manager recopila información de sitios de origen en la jerarquía de origen. 

##  <a name="source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a> Jerarquías de origen  
Una jerarquía de origen es una jerarquía de Configuration Manager que tiene los datos que quiere migrar. Cuando se configura la migración y se especifica una jerarquía de origen, se especifica el sitio de nivel superior de la jerarquía de origen. Este sitio también se denomina sitio de origen. Los sitios adicionales desde los cuales puede migrar datos en la jerarquía de origen también se denominan sitios de origen.  

-   Cuando se configura un trabajo de migración para migrar datos de una jerarquía de origen de Configuration Manager 2007, se configura para migrar datos de uno o más sitios de origen específicos en la jerarquía de origen.  

-   Cuando se configura un trabajo de migración para migrar datos de una jerarquía de origen que ejecuta System Center 2012 Configuration Manager o versiones posteriores, solo hay que especificar el sitio de nivel superior.  

Solo se puede configurar una jerarquía de origen cada vez.  

-   Si se configura una nueva jerarquía de origen, esa jerarquía se convierte automáticamente en la jerarquía de origen actual que sustituye a la jerarquía de origen anterior.  

-   Cuando se configura una jerarquía de origen debe especificar el sitio de nivel superior de la jerarquía de origen y las credenciales de Configuration Manager que se van a usar al conectarse a la base de datos del proveedor de SMS y la base de datos de sitio de ese sitio de origen.  

-   Configuration Manager usa estas credenciales para ejecutar la recopilación de datos para recuperar información sobre los objetos y puntos de distribución del sitio de origen.  

-   Como parte de los procesos de recopilación de datos, se identifican los sitios secundarios en la jerarquía de origen.  

-   Si la jerarquía de origen es una jerarquía de Configuration Manager 2007, puede configurar esos sitios adicionales como sitios de origen con credenciales independientes para cada sitio de origen.  

Aunque puede configurar varias jerarquías de origen en sucesión, la migración está activa solo para una jerarquía de origen a la vez.  

-   Si configura una jerarquía de origen adicional antes de completar la migración desde la jerarquía de origen actual, Configuration Manager cancela todos los trabajos de migración activos y pospone cualquier trabajo de migración programado para la jerarquía de origen actual.  

-   La jerarquía de origen recién configurada se convierte en la jerarquía de origen actual y la jerarquía de origen original ahora está inactiva.  

-   Después puede configurar credenciales de conexión, sitios de origen adicionales y trabajos de migración para la nueva jerarquía de origen.  

Si restaura una jerarquía de origen inactiva y no usó anteriormente **Limpiar datos de migración**, puede ver los trabajos de migración configurados previamente para esa jerarquía de origen. No obstante, antes de poder continuar con la migración desde esa jerarquía, debe volver a configurar las credenciales para establecer la conexión con los sitios de origen aplicables en la jerarquía y, a continuación, volver a programar todos los trabajos de migración que no se completaron.  

> [!CAUTION]  
>  Si migra datos de más de una jerarquía de origen único, cada jerarquía de origen adicional debe contener un conjunto de códigos de sitio único.  
> Las jerarquías de origen y destino también requieren un conjunto diferente de códigos de sitio.

Para más información sobre cómo configurar una jerarquía de origen, vea [Configurar jerarquías de origen y sitios de origen para la migración a la rama actual de Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

##  <a name="source-sites"></a><a name="BKMK_Source_Sites"></a> Sitios de origen  
 Los sitios de origen son los sitios en la jerarquía de origen que tienen los datos que se van a migrar. El sitio de nivel superior de la jerarquía de origen siempre es el primer sitio de origen. Cuando la migración recopila los datos del primer sitio de origen de una nueva jerarquía de origen, detecta información acerca de los sitios adicionales en dicha jerarquía.  

 Una vez que la recopilación de datos se completa para el sitio de origen inicial, las acciones que el usuario deba realizar a continuación dependen de la versión del producto de la jerarquía de origen.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Sitios de origen que ejecutan Configuration Manager 2007 SP2  
 Después de recopilar los datos del sitio de origen inicial de la jerarquía de Configuration Manager 2007 SP2, no es necesario configurar sitios de origen adicionales para crear trabajos de migración. Pero, antes de poder migrar datos desde otros sitios, debe configurar esos sitios como sitios de origen, y Configuration Manager debe recopilar datos de esos sitios correctamente.  

 Para recopilar datos de sitios adicionales, configure individualmente cada sitio como sitio de origen. Para ello, debe especificar las credenciales para que Configuration Manager se conecte con el proveedor de SMS y con la base de datos de cada sitio de origen. Después de configurar las credenciales para un sitio de origen, comienza el proceso de recopilación de datos para ese sitio.  

 Si configura sitios de origen adicionales en una jerarquía de origen de Configuration Manager 2007 SP2, debe configurar sitios de origen de arriba hacia abajo, lo que significa que debe configurar los sitios del nivel inferior en último lugar. Puede configurar los sitios de origen de una rama de la jerarquía en cualquier momento, pero debe configurar un sitio como sitio de origen antes de configurar cualquiera de sus sitios secundarios como sitios de origen.  

> [!NOTE]  
>  Solo se admiten para la migración los sitios primarios de una jerarquía de Configuration Manager 2007 SP2.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Sitios de origen que ejecutan System Center 2012 Configuration Manager o versiones posteriores  
 Después de recopilar los datos del sitio de origen inicial de la jerarquía de System Center 2012 Configuration Manager o posterior, no es necesario configurar sitios de origen adicionales en esa jerarquía de origen. Esto se debe a que, a diferencia de Configuration Manager 2007, estas versiones de Configuration Manager usan una base de datos compartida, que permite identificar y luego migrar todos los objetos disponibles desde el sitio de origen inicial.  

 Cuando configure las cuentas de acceso para recopilar datos, es posible que necesite otorgar el acceso de **Cuenta de proveedor de SMS de origen** a varios equipos de la jerarquía de origen. Esto podría ser necesario si el sitio de origen admite varias instancias del proveedor de SMS, cada una en un equipo diferente. Cuando se inicia la recopilación de datos, el sitio de nivel superior de la jerarquía de destino se pone en contacto con el sitio de nivel superior de la jerarquía de origen para identificar las ubicaciones del proveedor de SMS para ese sitio. Se identifica únicamente la primera instancia de proveedor de SMS. Si el proceso de recopilación de datos no puede acceder al proveedor de SMS en la ubicación que identifica, el proceso genera un error y no intenta conectarse con otros equipos que ejecuten una instancia del proveedor de SMS para ese sitio.  

##  <a name="data-gathering"></a><a name="BKMK_Data_Gathering"></a> Recopilación de datos  
 Inmediatamente después de especificar una jerarquía de origen, de configurar las credenciales para cada sitio de origen adicional en una jerarquía de origen o de compartir los puntos de distribución para un sitio de origen, Configuration Manager comienza a recopilar datos del sitio de origen.  

 Luego, el proceso de recopilación de datos se repite según una programación simple para mantener la sincronización con todos los cambios que se produzcan en los datos del sitio de origen. De forma predeterminada, el proceso se repite cada cuatro horas. Puede cambiar la programación para este ciclo mediante la edición de las **Propiedades** del sitio de origen. El proceso inicial de recopilación de datos debe revisar todos los objetos de la base de datos de Configuration Manager y puede tardar mucho tiempo en finalizar. Los procesos de recopilación de datos subsiguientes identifican solo los cambios en los datos y requieren menos tiempo para completarse.  

 Para recopilar los datos, el sitio de nivel superior de la jerarquía de destino se conecta con el proveedor de SMS y con la base de datos del sitio de origen para recuperar una lista de objetos y puntos de distribución. Estas conexiones utilizan las cuentas de acceso del sitio de origen. Para más información sobre las configuraciones necesarias para la recopilación de datos, vea [Requisitos previos para la migración](../../core/migration/prerequisites-for-migration.md).  

 Puede iniciar y detener el proceso de recopilación de datos mediante **Obtener datos ahora** y **Detener la recopilación de datos** en la consola de Configuration Manager.  

 Después de usar **Detener la recopilación de datos** para un sitio de origen por la razón que fuese, debe volver a configurar las credenciales para el sitio para poder recopilar datos de ese sitio nuevamente. Hasta que vuelva a configurar el sitio de origen, Configuration Manager no podrá identificar objetos nuevos o cambios en los objetos migrados anteriormente en ese sitio.  

> [!NOTE]  
>  Antes de expandir un sitio primario independiente en una jerarquía con un sitio de administración central, debe detener todas las recopilaciones de datos. Puede volver a configurar la recopilación de datos una vez que se complete la expansión del sitio.  

### <a name="gather-data-now"></a>Obtener datos ahora  
 Después de que se ejecuta el proceso de recopilación de datos inicial para un sitio, este proceso se repite para identificar los objetos que se han actualizado desde el último ciclo de recopilación de datos. También puede usar la acción **Obtener datos ahora** en la consola de Configuration Manager para iniciar el proceso inmediatamente y para restablecer la hora de inicio del ciclo siguiente.  

 Una vez que un proceso de recopilación de datos se completa correctamente para un sitio de origen, puede compartir los puntos de distribución del sitio de origen y configurar trabajos de migración para migrar datos desde ese sitio. La recopilación de datos es un proceso repetitivo de migración y continúa realizándose hasta que se cambia la jerarquía de origen o se usa **Detener la recopilación de datos** para finalizar el proceso de recopilación de datos para ese sitio.  

### <a name="stop-gathering-data"></a>Detener la recopilación de datos  
 Puede usar **Detener la recopilación de datos** para finalizar el proceso de recopilación de datos para un sitio de origen si ya no quiere que Configuration Manager identifique los objetos nuevos o modificados de ese sitio. Esta acción también evita que Configuration Manager ofrezca a los clientes de la jerarquía de destino puntos de distribución compartidos del origen como ubicaciones de contenido para el contenido migrado.  

 Para detener la recopilación de datos de cada sitio de origen, debe ejecutar **Detener la recopilación de datos** en los sitios de origen del nivel inferior y, después, repetir el proceso en cada sitio primario. El sitio de nivel superior de la jerarquía de origen debe ser el último sitio en el que se detenga la recopilación de datos. Debe detener la recopilación de datos en cada sitio secundario antes de realizar esta acción en un sitio primario. Normalmente, solo debe detener la recopilación de datos cuando esté listo para completar el proceso de migración.  

 Una vez que se detiene la recopilación de datos para un sitio de origen, la información recopilada previamente sobre los objetos y recopilaciones de ese sitio permanece disponible para usarse en la configuración de nuevos trabajos de migración. Pero no verá ningún objeto ni recopilaciones nuevas, ni los cambios realizados a los objetos existentes. Si vuelve a configurar el sitio de origen y comienza a recopilar datos de nuevo, verá la información y el estado de los objetos migrados anteriormente.  
