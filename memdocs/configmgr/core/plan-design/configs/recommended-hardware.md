---
title: Hardware recomendado
titleSuffix: Configuration Manager
description: Obtenga recomendaciones de hardware que le ayudarán a ampliar su entorno de Configuration Manager más allá de una implementación básica.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d741e34325da859d4fe1f0af554544ce146a42f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702123"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Hardware recomendado para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Las siguientes recomendaciones son instrucciones para ayudarle a escalar un entorno de Configuration Manager de tal manera que admita más de una implementación básica de sitios, sistemas de sitios y clientes. No pretenden cubrir todas las configuraciones de jerarquía y sitios posibles.  

Use la información de las siguientes secciones como una guía para planear los componentes de hardware que pueden satisfacer las cargas de procesamiento de clientes y sitios que usan las características disponibles de Configuration Manager con las configuraciones predeterminadas.  



##  <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a> Sistemas de sitio  
En esta sección se proporcionan las configuraciones de hardware recomendadas para los sistemas de sitio de Configuration Manager en implementaciones que admiten el número máximo de clientes y usan todas o la mayoría de las características de Configuration Manager. Es posible que las implementaciones que admitan una cantidad inferior al número máximo de clientes y que no usen todas las características disponibles requieran menos recursos del equipo. En general, los factores clave que limitan el rendimiento del conjunto del sistema son los siguientes por su orden de incidencia:  

1.  Rendimiento de E/S del disco  

2.  Memoria disponible  

3.  CPU  

Para obtener el mejor rendimiento, use las configuraciones de RAID 10 para todas las unidades de datos y una red Ethernet de 1 Gbps.  

###  <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a> Servidores de sitio  

|Configuración del sitio|CPU (núcleos)|Memoria (GB)|Asignación de memoria para SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Servidor de sitio primario independiente con un rol de sitio de base de datos en el mismo servidor<sup>1</sup>|16|96|80|  
|Servidor de sitio primario independiente con una base de datos de sitio remoto|8|16|-|  
|Servidor de bases de datos remoto para un sitio primario independiente|16|72|90|  
|Servidor de sitio de administración central con un rol de sitio de base de datos en el mismo servidor<sup>1</sup>|20|128|80|  
|Servidor de sitio primario de administración central con una base de datos de sitio remoto|8|16|-|  
|Servidor de bases de datos remoto para un sitio de administración central|16|96|90|  
|Sitio primario secundario con un rol de sitio de base de datos en el mismo servidor|16|96|80|  
|Servidor de sitio primario secundario con una base de datos de sitio remoto|8|16|-|  
|Servidor de bases de datos remoto para un sitio primario secundario|16|72|90|  
|Servidor de sitio secundario|8|16|-|  

<sup>1</sup> Si el servidor de sitio y SQL Server están instalados en el mismo equipo, la implementación admite los [números de tamaño y escala](size-and-scale-numbers.md) máximos para sitios y clientes. Pero esta configuración puede limitar las [opciones de alta disponibilidad de Configuration Manager](../../servers/deploy/configure/high-availability-options.md), como el uso de un clúster de SQL Server. Además, debido a los mayores requisitos de E/S necesarios para admitir SQL Server y el servidor de sitio de Configuration Manager cuando ambos se ejecutan en el mismo equipo, es recomendable considerar el uso de una configuración con una máquina de SQL Server remota con implementaciones de mayor tamaño.  

###  <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> Servidores del sistema de sitio remoto  
Las instrucciones siguientes están destinadas para equipos que tienen un solo rol de sistema de sitio. Planee realizar ajustes al instalar varios roles de sistema de sitio en el mismo equipo.  

|Rol de sistema de sitio|CPU (núcleos)|Memoria (GB)|Espacio en disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Punto de administración|4|8|50|  
|Punto de distribución|2|8|Según sea necesario para el sistema operativo y para almacenar el contenido que implemente|  
|Punto de actualización de software<sup>1</sup>|8|16|Según sea necesario para el sistema operativo y para almacenar las actualizaciones que implemente|  
|Resto de roles del sistema de sitio|4|8|50|  

<sup>1</sup> El equipo que hospeda un punto de actualización de software requiere las siguientes configuraciones para los grupos de aplicaciones de IIS:  

- Aumente la **longitud de cola de WsusPool** a **2000**.  

- Cuadriplique el **límite de memoria privada de WsusPool** o establézcalo en **0** (ilimitado).  

###  <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> Espacio en disco para los sistemas de sitio  
La asignación de disco y la configuración inciden en el rendimiento de Configuration Manager. Dado que no todos los entornos de Configuration Manager son iguales, los valores que implemente pueden diferir de los indicados en estas instrucciones.  

Para lograr un rendimiento óptimo, ubique cada objeto en un volumen RAID dedicado independiente. Para todos los volúmenes de datos (Configuration Manager y sus archivos de base de datos), utilice RAID 10 para lograr un rendimiento óptimo.  

|Uso de datos|Espacio mínimo en disco|25.000 clientes|50.000 clientes|100.000 clientes|150.000 clientes|700 000 clientes (sitio de administración central)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Sistema operativo|Consulte las instrucciones para el sistema operativo.|Consulte las instrucciones para el sistema operativo.|Consulte las instrucciones para el sistema operativo.|Consulte las instrucciones para el sistema operativo.|Consulte las instrucciones para el sistema operativo.|Consulte las instrucciones para el sistema operativo.|  
|Archivos de registro y de aplicación de Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Archivo .mdf de la base de datos del sitio|75 GB por cada 25.000 clientes|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Archivo .ldf de la base de datos del sitio|25 GB por cada 25.000 clientes|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Archivos temporales de la base de datos (.mdf y .ldf)|Según sea necesario|Según sea necesario|Según sea necesario|Según sea necesario|Según sea necesario|Según sea necesario|  
|Contenido (recursos compartidos de punto de distribución)|Según sea necesario<sup>1</sup>|Según sea necesario<sup>1</sup>|Según sea necesario<sup>1</sup>|Según sea necesario<sup>1</sup>|Según sea necesario<sup>1</sup>|Según sea necesario<sup>1</sup>|  

<sup>1</sup> La guía de espacio en disco no incluye el espacio necesario para el contenido que se encuentra en la biblioteca de contenido en el servidor de sitio o en los puntos de distribución. Para obtener información sobre la planeación de la biblioteca de contenido, consulte [The content library](../../../core/plan-design/hierarchy/the-content-library.md) (La biblioteca de contenido).  

Además de las instrucciones anteriores, tenga en cuenta las siguientes directrices al planear los requisitos de espacio en disco:  

- Cada cliente requiere aproximadamente 5 MB de espacio.  

- Al planear el tamaño de la base de datos temporal para un sitio primario, calcule un tamaño combinado del 25 % al 30 % del archivo .mdf de la base de datos de sitio. El tamaño real puede ser significativamente menor o mayor, en función del rendimiento del servidor del sitio y el volumen de datos de entrada en períodos breves o amplios de tiempo.  

  > [!NOTE]  
  >  Una vez que tenga 50 000 o más clientes en un sitio, planee usar cuatro o más archivos .mdf de base de datos temporal.  

- El tamaño de la base de datos temporal para un sitio de administración central suele ser mucho menor que el de un sitio primario.  

- El tamaño de la base de datos del sitio secundario tiene las limitaciones de tamaño siguientes:  

  - SQL Server 2012 Express: 10 GB  

  - SQL Server 2014 Express: 10 GB  

##  <a name="clients"></a><a name="bkmk_ScaleClient"></a> Clientes  
Esta sección proporciona las configuraciones de hardware recomendadas para los equipos que se administran mediante el software de cliente de Configuration Manager.  

### <a name="client-for-windows-computers"></a>Cliente para equipos Windows  
A continuación se describen los requisitos mínimos para equipos basados en Windows que se administran con Configuration Manager, incluidos los sistemas operativos integrados:  

- **Procesador y memoria:** Consulte los requisitos de procesador y RAM para el sistema operativo del equipo.  

- **Espacio en disco:** 500 MB de espacio en disco disponible, con 5 GB recomendados para la memoria caché del cliente de Configuration Manager. Se requiere menos espacio en disco si se usa la configuración personalizada para instalar el cliente de Configuration Manager:  

    - Use la propiedad Client.msi SMSCACHESIZE para establecer un archivo de caché más pequeño que el valor predeterminado de 5120 MB. El tamaño mínimo es 1 MB. Por ejemplo, `CCMSetup.exe SMSCachesize=2` crea una memoria caché de 2 MB de tamaño.  

    Para más información sobre esta configuración de instalación de clientes, consulte [Acerca de las propiedades de instalación de clientes en System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    > La instalación del cliente con espacio en disco mínimo es útil para dispositivos de Windows Embedded que suelen tener tamaños de disco más pequeños que los equipos de Windows estándar.  

Los siguientes son los requisitos de hardware mínimos adicionales para la funcionalidad opcional en Configuration Manager.  

- **Implementación de sistema operativo:** 384 MB de RAM  

- **Centro de software:** Procesador de 500 MHz  

- **Control remoto:** Pentium 4 a 3 GHz con Hyper-Threaded (núcleo único) o CPU comparable, con al menos 1 GB de RAM para una experiencia óptima  

### <a name="client-for-linux-and-unix"></a>Cliente para Linux y UNIX  
Los siguientes son los requisitos mínimos para los servidores Linux y UNIX que se administran con Configuration Manager.  

|Requisito|Detalles|  
|-----------------|-------------|  
|Procesador y memoria|Consulte los requisitos de procesador y RAM para el sistema operativo del equipo.|  
|Espacio en disco|500 MB de espacio en disco disponible, con 5 GB recomendados para la memoria caché del cliente de Configuration Manager.|  
|Conectividad de red|Los equipos cliente de Configuration Manager deben tener conectividad de red con los sistemas de sitio de Configuration Manager para habilitar la administración.|  

##  <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Consola de Configuration Manager  
Los requisitos en la tabla siguiente se aplican a cada equipo que ejecuta la consola de Configuration Manager.  

**Configuración mínima del hardware:**  

- Intel i3 o CPU comparable  

- 2 GB de RAM  

- 2 GB de espacio en disco  

|Configuración de PPP|Resolución mínima|  
|-----------------|------------------------|  
|96/100 %|1024 x 768|  
|120/125 %|1280 x 960|  
|144/150 %|1600 x 1200|  
|196/200 %|2500 x 1600|  

**Compatibilidad con PowerShell:**  

Al instalar compatibilidad con PowerShell en un equipo que ejecuta la consola de Configuration Manager, puede ejecutar los cmdlets de PowerShell en ese equipo para administrar Configuration Manager.

- Se admite PowerShell 3.0 o posterior

Además de PowerShell, se admite Windows Management Framework (WMF) versión 3.0 o posterior.   


##  <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a> Implementaciones de laboratorio  
Use las siguientes recomendaciones mínimas de hardware para implementaciones de laboratorio y pruebas de Configuration Manager. Estas recomendaciones se aplican a todos los tipos de sitio, hasta un máximo de 100 clientes:  

|Rol|CPU (núcleos)|Memoria (GB)|Espacio en disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Servidor de sitio y base de datos|2 - 4|8 - 12|100|  
|Servidor de sistema de sitio|1 - 4|2 - 4|50|  
|Cliente|1 - 2|1 - 3|30|  
