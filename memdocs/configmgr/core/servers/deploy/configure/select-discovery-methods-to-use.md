---
title: Selección de los métodos de detección
titleSuffix: Configuration Manager
description: Consulte las consideraciones sobre qué métodos usar y en qué sitios ejecutarlos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f08ab44a11b48b4446a372c4f6065ea0d7c63e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700963"
---
# <a name="select-discovery-methods-to-use-for-configuration-manager"></a>Selección de los métodos de detección que se usarán en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para usar la detección en Configuration Manager de forma correcta y eficaz, debe tener en cuenta qué métodos usar y en qué sitios ejecutarlos.  

 Debido a que la detección puede generar un gran volumen de tráfico de red y los registros de datos de detección (DDR) resultantes pueden usar bastantes recursos de la CPU durante el procesamiento, use solo aquellos métodos de detección que necesite para lograr sus objetivos. Podría comenzar usando solo uno o dos métodos de detección y más tarde habilitar métodos adicionales de una manera controlada para ampliar el nivel de detección en su entorno. La información de este tema puede ayudarle a tomar decisiones informadas.  

 Para más información sobre los diferentes métodos de detección, vea [Acerca de los métodos de detección en Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Seleccionar métodos para detectar cosas diferentes  
 Para detectar posibles recursos de usuario o equipos cliente de Configuration Manager, debe habilitar los métodos de detección adecuados. Puede usar diferentes combinaciones de métodos de detección para localizar recursos diferentes y detectar información adicional sobre dichos recursos. Los métodos de detección que use determinan el tipo de recursos detectados y los agentes y servicios de Configuration Manager que se usan en el proceso de detección. También determinan el tipo de información acerca de los recursos que puede detectar.  

### <a name="discover-computers"></a>Detectar equipos   
Cuando quiera detectar equipos, puede usar la **detección de redes** o la **detección de sistemas de Active Directory**.  

 Por ejemplo, si quiere detectar recursos que puedan instalar el cliente de Configuration Manager antes de usar la instalación de inserción de cliente, puede ejecutar la detección de sistemas de Active Directory. Con este método, no solo detecta el recurso, sino que también detecta información básica (incluso información ampliada) sobre él de Active Directory Domain Services. Esta información puede ser útil en la creación de consultas complejas y recopilaciones que se utilizarán para la asignación de la configuración del cliente o la distribución de contenido.

Como alternativa, podría ejecutar la detección de redes y usar sus opciones para detectar el sistema operativo de los recursos (necesario para usar después la instalación de inserción de cliente). La detección de redes proporciona información sobre la topología de red que no puede adquirir con otros métodos de detección. En cambio, este método no proporciona información sobre el entorno de Active Directory.

 También hay un método denominado **detección de latidos**. Es posible usar únicamente la detección de latidos para forzar la detección de clientes que ha instalado mediante métodos distintos de la instalación de inserción de cliente. En cambio, a diferencia de otros métodos de detección, la detección de latidos no puede detectar equipos que no tengan un cliente de Configuration Manager activo. Devuelve un conjunto limitado de información, diseñada para mantener un registro de base de datos existente (y no para ser la base de ese registro). La información presentada por la detección de latidos podría no ser suficiente para crear consultas complejas o recopilaciones.  

 Si usa la **detección de grupos de Active Directory** para detectar la pertenencia a un grupo específico, puede detectar información del equipo o sistema limitada. Esto no sustituye a una detección completa de equipos, pero puede proporcionar información básica. Esta información no es suficiente para la instalación de inserción de cliente.  

### <a name="discover-users"></a>Detectar usuarios   
Cuando quiera obtener información sobre los usuarios, use la **detección de usuarios de Active Directory**. De manera similar a la detección de sistemas de Active Directory, este método detecta los usuarios de Active Directory. Incluye información básica, además de información ampliada de Active Directory. Puede utilizar esta información para crear consultas complejas y recopilaciones similares a las de los equipos.  

### <a name="discover-group-information"></a>Detectar información de grupo   
Cuando quiera obtener información sobre grupos y pertenencias a grupos, use la **detección de grupos de Active Directory**. Este método de detección crea registros de recursos para los grupos de seguridad.  

 Puede usar este método para buscar un grupo específico de Active Directory para identificar a los miembros de ese grupo, además de los grupos anidados dentro de ese grupo. También puede utilizar este método para buscar una ubicación de Active Directory para grupos y buscar de forma recursiva en cada contenedor secundario de esa ubicación en Servicios de dominio de Active Directory.  

 Este método de detección también puede buscar la pertenencia a grupos de distribución. Esto puede identificar las relaciones de grupo de usuarios y equipos.  

 Cuando se detecta un grupo, también puede detectar información limitada sobre sus miembros. En cambio, esto no reemplaza los métodos de detección de usuarios ni de sistemas de Active Directory. Normalmente no es suficiente para crear consultas y recopilaciones complejas o para servir como base de una instalación de inserción de cliente.  

### <a name="discover-infrastructure"></a>Detectar infraestructura   
Hay dos métodos que puede usar para detectar la infraestructura de red: la **detección de redes** y la **detección de bosques de Active Directory**.  

 Use la detección de bosques de Active Directory para buscar un bosque de Active Directory para obtener información sobre subredes y configuraciones de sitios de Active Directory. Después, estas configuraciones se pueden introducir de forma automática en Configuration Manager como ubicaciones de límite.  

 Cuando desee detectar la topología de red, utilice la detección de redes. Mientras otros métodos de detección devuelven información relacionada con Active Directory Domain Services y pueden identificar la ubicación de red actual de un cliente, no proporcionan información de infraestructura basada en las subredes y la topología del enrutador de la red.  

##  <a name="discovery-data-is-shared-among-sites"></a><a name="bkmk_shared"></a> Los datos de detección se comparten entre los sitios  
 Después de que Configuration Manager agregue los datos de detección a una base de datos, estos se comparten rápidamente entre todos los sitios de la jerarquía. Ya que detectar la misma información en varios sitios de la jerarquía no aporta normalmente ningún beneficio, es conveniente configurar una sola instancia de cada método de detección usado para que se ejecute en un único sitio. Se aconseja hacer esto en vez de ejecutar varias instancias de un único método en diferentes sitios.  

 En cambio, en algunos entornos, podría resultar útil asignar el mismo método de detección para que se ejecute en varios sitios, cada uno con una programación y una configuración independientes. Por ejemplo, al usar la detección de redes, puede dirigir cada sitio para detectar su red local, en lugar de intentar detectar todas las ubicaciones de red a través de una WAN.

Si configura varias instancias de los mismos métodos de detección para ejecutarse en diferentes sitios, planee la configuración de cada sitio cuidadosamente. No quiere tener dos o más sitios que detecten los mismos recursos de la red o de Active Directory. Esto puede consumir ancho de banda de red adicional y crear DDR duplicados.

En la tabla siguiente se identifica en qué sitios se pueden configurar los diferentes métodos de detección.  

|Método de detección|Ubicaciones admitidas|  
|----------------------|-------------------------|  
|Detección de bosques de Active Directory|Sitio de administración central<br /><br /> Sitio primario|  
|Detección de grupos de Active Directory|Sitio primario|  
|Detección de sistemas de Active Directory|Sitio primario|  
|Detección de usuario de Active Directory|Sitio primario|  
|Detección de latidos<sup>1</sup>|Sitio primario|  
|Detección de redes|Sitio primario<br /><br /> Sitio secundario|  

 <sup>1</sup> Los sitios secundarios no pueden configurar el método de detección de latidos, pero pueden recibir el DDR de latido de un cliente.  

 Cuando los sitios secundarios ejecutan la detección de redes o reciben DDR de detección de latidos, transfieren el DDR mediante la replicación basada en archivos a su sitio primario principal. Esto se debe a que solo los sitios primarios y los sitios de administración central pueden procesar los DDR. Para obtener más información sobre cómo se procesan los DDR, consulte [Acerca de los registros de datos de detección](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Consideraciones de los diferentes métodos de detección  
 Dado que cada entorno de red y cada servidor de sitio es diferente, se aconseja limitar las configuraciones iniciales para la detección. Luego, supervise detenidamente la capacidad de cada servidor de sitio de procesar los datos de detección generados.  

Cuando se usa un método de detección de **Active Directory** para sistemas, usuarios o grupos:  

-   Ejecute la detección en un sitio que tiene una conexión de red rápida con los controladores de dominio.  

-   Tenga en cuenta la topología de replicación de Active Directory para garantizar que la detección puede tener acceso a la información más reciente.  

-   Tenga en cuenta el ámbito de la configuración de detección y limite la detección únicamente a las ubicaciones y los grupos de Active Directory que se deban detectar.  

Si usa la **detección de redes**:  

-   Utilice una configuración inicial limitada para identificar la topología de la red.  

-   Después de identificar la topología de la red, configure la detección de redes para ejecutarse en sitios específicos que son fundamentales para las áreas de la red que quiera detectar plenamente.  

Habida cuenta de que la **detección de latidos** no se ejecuta en un sitio específico, no es necesario considerarla en la planificación general de dónde ejecutar la detección.  

##  <a name="best-practices-for-discovery"></a><a name="bkmk_best"></a> Procedimientos recomendados para la detección  
Para obtener mejores resultados con la detección, se recomienda lo siguiente:

- **Ejecución de la detección de sistemas de Active Directory y la detección de usuarios de Active Directory antes de ejecutar la detección de grupos de Active Directory.**  

  Cuando la detección de grupos de Active Directory identifica un usuario o equipo no detectado previamente como miembro de un grupo, trata de detectar los detalles básicos del usuario o el equipo. Habida cuenta de que la detección de grupos de Active Directory no está optimizada para este tipo de detección, este proceso puede dar lugar a que se ejecute con lentitud. Además, la detección de grupos de Active Directory identifica solo los detalles básicos sobre los usuarios y equipos que detecta, y no crea un registro de detección completo del usuario o el equipo. Al ejecutar la detección de sistemas de Active Directory y la detección de usuarios de Active Directory, se encontrarán disponibles también los atributos adicionales de Active Directory para cada tipo de objeto y, como resultado, la detección de grupos de Active Directory se ejecuta de manera más eficaz.  

- **Al configurar la detección de grupos de Active Directory, especifique solo los grupos que usa con Configuration Manager.**  

  Para controlar el uso que la detección de grupos de Active Directory hace de los recursos, especifique solo los grupos que use con Configuration Manager. Esto se debe a que la detección de grupos de Active Directory busca usuarios, equipos y grupos anidados de forma recursiva en cada grupo que detecta. La búsqueda de cada grupo anidado puede ampliar el ámbito de la detección de grupos de Active Directory y reducir el rendimiento. Además, al configurar la detección de diferencias para la detección de grupos de Active Directory, el método de detección supervisa los cambios de cada grupo. Esto reduce aún más el rendimiento cuando el método debe buscar grupos innecesarios.  

- **Configuración de métodos de detección con un intervalo más largo entre la detección completa y un período más frecuente de detección de diferencias.**  

  Habida cuenta de que la detección de diferencias consume menos recursos que un ciclo de detección completa, además de poder identificar recursos nuevos o modificados en Active Directory, se puede reducir la frecuencia de los ciclos de detección completa a una ejecución semanal (o incluso menos). La detección de diferencias para la detección de sistemas de Active Directory, la detección de usuarios de Active Directory y la detección de grupos de Active Directory identifica casi todos los cambios de los objetos de Active Directory y puede mantener datos de detección precisos sobre los recursos.  

- **Ejecución de métodos de detección de Active Directory en un sitio primario que tiene una ubicación de red más cercana al controlador de dominio de Active Directory.**  

  Para mejorar el rendimiento de la detección de Active Directory, se aconseja ejecutar la detección en un sitio primario que tenga una conexión de red rápida a los controladores de dominio. Si se ejecuta el mismo método de detección de Active Directory en varios sitios, configure cada método de detección para evitar superposiciones. A diferencia de las versiones anteriores de Configuration Manager, los datos de detección se comparten entre los sitios. Por lo tanto, no es necesario detectar la misma información en varios sitios. Para obtener más información, consulte [Los datos de detección se comparten entre los sitios](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Ejecución de la detección de bosques de Active Directory en un solo sitio cuando planee crear de forma automática los límites de los datos de detección.**  

  Si se ejecuta la detección de bosques de Active Directory en más de un sitio de una jerarquía, se aconseja habilitar solo las opciones para crear automáticamente los límites en un solo sitio. Esto se debe a que, cuando la detección de bosques de Active Directory se ejecuta en cada sitio y crea límites, Configuration Manager no puede combinar esos límites en un objeto de un solo límite. Al configurar la detección de bosques de Active Directory para crear de forma automática los límites en varios sitios, el resultado pueden ser objetos con límites duplicados en la consola de Configuration Manager.  
