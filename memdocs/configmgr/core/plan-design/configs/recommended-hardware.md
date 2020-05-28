---
title: Hardware recomendado
titleSuffix: Configuration Manager
description: Obtenga recomendaciones de hardware que le ayudarán a ampliar su entorno de Configuration Manager más allá de una implementación básica.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428779"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Hardware recomendado para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las siguientes recomendaciones son instrucciones para ayudarle a escalar un entorno de Configuration Manager de tal manera que admita más de una implementación básica de sitios, sistemas de sitios y clientes. No pretenden cubrir todas las configuraciones de jerarquía y sitios posibles.  

Utilice la información de las secciones siguientes como guía para planear el hardware. Asegúrese de que el hardware pueda satisfacer las cargas de procesamiento de los clientes y sitios que usan las características de Configuration Manager disponibles.

Para más información, consulte las [notas del producto sobre la guía de rendimiento y escalado de Configuration Manager](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a> Sistemas de sitio

En esta sección se ofrecen las configuraciones de hardware recomendadas para los sistemas de sitio de Configuration Manager. Use estas recomendaciones para admitir el número máximo de clientes y usar la mayoría o todas las características de Configuration Manager. Es posible que si el entorno admite una cantidad inferior al número máximo de clientes y no usa todas las características disponibles requiera menos recursos. En general, los factores clave siguientes limitan el rendimiento del conjunto del sistema:

1. Rendimiento de E/S del disco

2. Memoria disponible

3. CPU

Para obtener el mejor rendimiento, use las configuraciones de RAID 10 para todas las unidades de datos y una red Ethernet de 1 Gbps.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a> Servidores de sitio

|Configuración del sitio|CPU (núcleos)|Memoria (GB)|Asignación de memoria para SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Servidor de sitio primario independiente con un rol de sitio de base de datos en el mismo servidor <sup>[Nota 1](#bkmk_note1)</sup>|16|96|80|  
|Servidor de sitio primario independiente con una base de datos de sitio remoto|8|16|-|  
|Servidor de bases de datos remoto para un sitio primario independiente|16|72|90|  
|Servidor de sitio de administración central con un rol de sitio de base de datos en el mismo servidor <sup>[Nota 1](#bkmk_note1)</sup>|20|128|80|  
|Servidor de sitio primario de administración central con una base de datos de sitio remoto|8|16|-|  
|Servidor de bases de datos remoto para un sitio de administración central|16|96|90|  
|Sitio primario secundario con un rol de sitio de base de datos en el mismo servidor|16|96|80|  
|Servidor de sitio primario secundario con una base de datos de sitio remoto|8|16|-|  
|Servidor de bases de datos remoto para un sitio primario secundario|16|72|90|  
|Servidor de sitio secundario|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a> Nota 1: SQL combinado

Si el servidor de sitio y SQL Server se encuentran en el mismo equipo, la implementación admite los [números de tamaño y escala](size-and-scale-numbers.md) máximos para sitios y clientes. Esta configuración puede limitar [opciones de alta disponibilidad](../../servers/deploy/configure/high-availability-options.md), como el uso de un clúster de SQL Server. Si tiene un entorno mayor, debido a los mayores requisitos de E/S para admitir ambos roles en el mismo equipo, considere la posibilidad de usar un servidor SQL Server remoto.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> Servidores del sistema de sitio remoto

Las instrucciones siguientes están destinadas para equipos que tienen un solo rol de sistema de sitio. Planee realizar ajustes al instalar varios roles de sistema de sitio en el mismo equipo.

|Rol de sistema de sitio|CPU (núcleos)|Memoria (GB)|Espacio en disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Punto de administración|4|8|50|  
|Punto de distribución|2|8|Según sea necesario para el sistema operativo y para almacenar el contenido que se implemente|  
|Punto de actualización de software <sup>[Nota 2](#bkmk_note2)</sup>|8|16|Según sea necesario para el sistema operativo y para almacenar las actualizaciones que se implementen|  
|Resto de roles del sistema de sitio|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a> Nota 2: Configuraciones de WSUS

El equipo que hospeda un punto de actualización de software requiere las siguientes configuraciones para los grupos de aplicaciones de IIS:  

- Aumente la **longitud de cola de WsusPool** a **2000**.  

- Cuadriplique el **límite de memoria privada de WsusPool** o establézcalo en **0** (ilimitado).  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> Espacio en disco para los sistemas de sitio

La asignación de disco y la configuración inciden en el rendimiento de Configuration Manager. Dado que no todos los entornos de Configuration Manager son iguales, los valores que implemente pueden diferir de los indicados en estas instrucciones.

Para lograr un rendimiento óptimo, ubique cada objeto en un volumen RAID dedicado independiente. Para todos los volúmenes de datos de Configuration Manager y sus archivos de base de datos, utilice RAID 10 para lograr un rendimiento óptimo.

|Uso de datos|Espacio mínimo en disco|25.000 clientes|50.000 clientes|100.000 clientes|150.000 clientes|700 000 clientes (sitio de administración central)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Archivos de registro y de aplicación de Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Archivo .mdf de la base de datos del sitio|75 GB por cada 25.000 clientes|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Archivo .ldf de la base de datos del sitio|25 GB por cada 25.000 clientes|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Archivos temporales de la base de datos (.mdf y .ldf)|Según sea necesario|Según sea necesario|Según sea necesario|Según sea necesario|Según sea necesario|Según sea necesario|  

En cuanto al disco del sistema de Windows, consulte la guía de ajustes de tamaño para la versión del sistema operativo instalada.

En lo que respecta al contenido en los puntos de distribución, depende de las implementaciones. Esta guía no incluye el espacio en disco necesario para la biblioteca de contenido en el servidor de sitio o en los puntos de distribución. Para obtener más información, vea [La biblioteca de contenido](../../../core/plan-design/hierarchy/the-content-library.md).

Cuando planee los requisitos de espacio en disco, tenga en cuenta las siguientes directrices adicionales:

- Cada cliente requiere aproximadamente 5-10 MB de espacio en la base de datos. Este número depende del tipo de jerarquía, la configuración y el número de clientes. El tamaño suele ser menor en entornos de mayor tamaño. Los sitios más pequeños tienen un mayor uso de la base de datos por cliente.<!-- SCCMDocs#1048 -->

- Para la base de datos temporal del sitio primario, calcule un tamaño combinado del 25 al 30 % del archivo .mdf de la base de datos del sitio. El tamaño real puede ser menor o mayor. Depende del rendimiento del servidor del sitio y el volumen de datos de entrada tanto en períodos de tiempo breves como amplios.

  > [!NOTE]
  > Una vez que tenga 50 000 o más clientes en un sitio, planee usar cuatro o más archivos .mdf de base de datos temporal.

- El tamaño de la base de datos temporal para un sitio de administración central suele ser mucho menor que el de un sitio primario.

- Si usa SQL Server Express para la base de datos del sitio secundario, el tamaño de la base de datos se limita a 10 GB.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a> Clientes

Esta sección proporciona las configuraciones de hardware recomendadas para los equipos que se administran mediante el software de cliente de Configuration Manager.

### <a name="client-for-windows-computers"></a>Cliente para equipos Windows

A continuación se describen los requisitos mínimos para equipos basados en Windows que se administran con Configuration Manager, incluidas las ediciones insertadas:

- **Procesador y memoria:** Consulte los requisitos de RAM y procesador para el sistema operativo.

- **Espacio en disco:** 500 MB de espacio en disco disponible, con 5 GB recomendados para la memoria caché del cliente de Configuration Manager. Si se usa la configuración personalizada para instalar el cliente de Configuration Manager, se requiere menos espacio en disco.

  - Use la propiedad client.msi **SMSCACHESIZE** para establecer un archivo de caché más pequeño que el valor predeterminado de 5120 MB. El tamaño mínimo es 1 MB. En el ejemplo siguiente se crea una caché de 2 MB: `CCMSetup.exe SMSCACHESIZE=2`

    Para obtener más información, vea [Información sobre las propiedades de instalación de clientes](../../../core/clients/deploy/about-client-installation-properties.md).

    > [!TIP]
    > La instalación del cliente con espacio en disco mínimo es útil para dispositivos de Windows Embedded que suelen tener tamaños de disco más pequeños que los equipos de Windows estándar.

Los siguientes requisitos de hardware mínimos adicionales corresponden a la funcionalidad opcional en Configuration Manager:

- **Implementación del sistema operativo:** Al menos 384 MB de RAM

- **Centro de software:** Al menos un procesador de 500 MHz

- **Control remoto:** Para tener una experiencia óptima, se requiere como mínimo un Pentium 4 a 3 GHz con Hyper-Threaded (núcleo único) o CPU comparable, con al menos 1 GB de RAM.

### <a name="client-for-linux-and-unix"></a>Cliente para Linux y UNIX

Los siguientes requisitos mínimos corresponden a los servidores Linux y UNIX que se administran con Configuration Manager.

|Requisito|Detalles|  
|-----------------|-------------|  
|Procesador y memoria|Consulte los requisitos de procesador y RAM para el sistema operativo del equipo.|  
|Espacio en disco|500 MB de espacio en disco disponible, con 5 GB recomendados para la memoria caché del cliente de Configuration Manager.|  
|Conectividad de red|Los equipos cliente de Configuration Manager deben tener conectividad de red con los sistemas de sitio de Configuration Manager para habilitar la administración.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Consola de Configuration Manager

Los siguientes requisitos de hardware mínimos se aplican a cada equipo que ejecuta la consola de Configuration Manager:

- Intel i3 o CPU comparable  

- 2 GB de RAM  

- 2 GB de espacio en disco  

|Configuración de PPP|Resolución mínima|  
|-----------------|------------------------|  
|96/100 %|1024 x 768|  
|120/125 %|1280 x 960|  
|144/150 %|1600 x 1200|  
|196/200 %|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a> Implementaciones de laboratorio

Use las siguientes recomendaciones mínimas de hardware para implementaciones de laboratorio y pruebas de Configuration Manager. Estas recomendaciones se aplican a todos los tipos de sitio, hasta un máximo de 100 clientes:  

|Rol|CPU (núcleos)|Memoria (GB)|Espacio en disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Servidor de sitio y base de datos|2 - 4|8 - 12|100|  
|Servidor de sistema de sitio|1 - 4|2 - 4|50|  
|Cliente|1 - 2|1 - 3|30|  
