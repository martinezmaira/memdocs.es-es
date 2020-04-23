---
title: Aspectos básicos de sitios y jerarquías
titleSuffix: Configuration Manager
description: Obtenga información básica sobre los sitios y jerarquías de Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707033"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>Aspectos básicos de sitios y jerarquías de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Una implementación de Configuration Manager debe instalarse en un dominio de Active Directory. La base de esta implementación incluye uno o varios sitios de Configuration Manager que forman una jerarquía de sitios. Desde un único sitio hasta una jerarquía de varios sitio, el tipo y la ubicación de los sitios que instale proporcionan la capacidad de escalar verticalmente (expandir) su implementación cuando sea necesario y ofrecer servicios clave a los usuarios y dispositivos administrados.

## <a name="hierarchies-of-sites"></a>Jerarquías de sitios
Al instalar Configuration Manager por primera vez, el primer sitio de Configuration Manager que se instale determina el ámbito de la jerarquía. El primer sitio de Configuration Manager es la base desde la que se administran los dispositivos y los usuarios de la empresa. Este primer sitio debe ser un sitio de administración central o un sitio primario independiente.  

 Un *sitio de administración central* es adecuado para implementaciones a gran escala, proporciona un punto central de administración y la flexibilidad necesaria para admitir dispositivos distribuidos por la infraestructura de red global. Después de instalar un sitio de administración central, tendrá que instalar uno o varios sitios primarios como sitios secundarios. Esta configuración es necesaria dado que un sitio de administración central no admite directamente la administración de dispositivos, que es la función de un sitio primario. Un sitio de administración central admite varios sitios primarios secundarios. Los sitios primarios secundarios se usan para administrar dispositivos y controlar el ancho de banda de red cuando los dispositivos administrados estén en distintas ubicaciones geográficas.  

 Un *sitio primario independiente* es adecuado para implementaciones más pequeñas, y puede usarse para administrar dispositivos sin tener que instalar sitios adicionales. Aunque un sitio primario independiente puede limitar el tamaño de la implementación, admite un escenario para expandir la jerarquía posteriormente mediante la instalación de un nuevo sitio de administración central. Con este escenario de expansión del sitio, su sitio primario independiente se convierte en un sitio primario secundario y, de este modo, podrá instalar sitios primarios secundarios adicionales por debajo de su nuevo sitio de administración central. Después, es posible ampliar la implementación inicial para el crecimiento futuro de la empresa.  

> [!TIP]  
>  En realidad, un sitio primario independiente y un sitio primario secundario son el mismo tipo de sitio: un sitio primario. La diferencia en el nombre se basa en la relación jerárquica que se crea cuando también se usa un sitio de administración central. Esta relación jerárquica también puede limitar la instalación de determinados roles de sistema de sitio que amplían la funcionalidad de Configuration Manager. Esta limitación de roles se produce dado que determinados roles de sistema de sitio solo pueden instalarse en el sitio de nivel superior de la jerarquía, un sitio de administración central o un sitio primario independiente.  

 Después de instalar el primer sitio, puede instalar sitios adicionales. Si el primer sitio era un sitio de administración central, puede instalar uno o varios sitios primarios secundarios. Después de instalar un sitio primario (independiente o primario secundario), puede instalar uno o varios sitios secundarios.  

 Un *sitio secundario* solo puede instalarse como tal debajo de uno primario. Este tipo de sitio extiende el alcance de un sitio primario para administrar dispositivos en ubicaciones que tienen una conexión de red lenta con el sitio primario. Aunque un sitio secundario extienda el sitio primario, el sitio primario administra todos los clientes. El sitio secundario proporciona compatibilidad para los dispositivos en la ubicación remota. Proporciona compatibilidad mediante la compresión y la posterior administración de la transferencia de información a través de la red que envíe (implemente) a los clientes, y que los clientes envíen de nuevo al sitio.  

 Los siguientes diagramas muestran algunos ejemplos de diseños de sitios.  

 ![Ejemplos de jerarquía](media/Hierarchy_examples.png)  

 Para obtener más información, consulte los temas siguientes:  

-   [Introducción a Configuration Manager](../../core/understand/introduction.md)  

-   [Diseñar una jerarquía de sitios para Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Instalación de sitios de Configuration Manager](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>Servidores de sistema de sitio y roles de sistema de sitio  
 Cada sitio de Configuration Manager instala *roles del sistema de sitio* que admiten operaciones de administración. Los siguientes roles se instalan de forma predeterminada al instalar un sitio:

-   El rol de servidor de sitio se asigna al equipo donde se instala el sitio.

-   El rol de servidor de base de datos de sitio se asigna al servidor SQL que hospeda la base de datos del sitio.

Otros roles de sistema de sitio son opcionales y solo se usan cuando se quiere usar las funciones activas en un rol de sistema de sitio. Cualquier equipo que hospede un rol de sistema de sitio se conoce como servidor de sistema de sitio.  

 Para una implementación más pequeña de Configuration Manager, es preferible que ejecute inicialmente todos los roles de sistema de sitio directamente en el equipo del servidor de sitio. Después, a medida que crezcan el entorno administrado y las necesidades, se podrán instalar servidores de sistema de sitio adicionales para hospedar roles de sistema de sitio adicionales a fin de mejorar la eficiencia del sitio en la provisión de servicios a más dispositivos.  

 Para más información sobre los distintos roles de sistema de sitio, vea [Roles de sistema de sitio](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) en [Planeamiento de servidores y roles de sistema de sitio para Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publicación de información de sitio en Active Directory Domain Services  
 Para simplificar la administración de Configuration Manager, puede extender el esquema de Active Directory para admitir los detalles usados por Configuration Manager y, después, hacer que los sitios publiquen su información clave en Active Directory Domain Services (AD DS). Después, los equipos que quiera administrar pueden recuperar de forma segura la información relacionada con el sitio de la fuente de confianza de AD DS. La información que los clientes pueden recuperar identifica los sitios disponibles, los servidores de sistema de sitio y los servicios que proporcionan dichos servidores.  

 *La extensión del esquema de Active Directory* se realiza solo una vez por bosque y puede hacerse antes o después de instalar Configuration Manager.   Al extender el esquema, debe crear un nuevo contenedor de Active Directory denominado System Management en cada dominio. El contenedor contiene un sitio de Configuration Manager que publicará datos para que los clientes los busquen. Para más información, vea [Preparar Active Directory para la publicación de sitios](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 *La publicación de datos del sitio* mejora la seguridad de su jerarquía de Configuration Manager y reduce la sobrecarga administrativa, pero no se necesita para las funciones básicas de Configuration Manager.  
