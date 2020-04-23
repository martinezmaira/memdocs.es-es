---
title: Configurar sitios y jerarquías
titleSuffix: Configuration Manager
description: Consulte esta lista de comprobación para asegurarse de tener en cuenta las configuraciones más comunes que afectan a los sitios y las jerarquías.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704683"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Configurar sitios y jerarquías para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de instalar el primer sitio de Configuration Manager o de agregar sitios adicionales a la jerarquía, use esta lista de comprobación para asegurarse de tener en cuenta las configuraciones más comunes que afectan tanto a los sitios como a las jerarquías.  

Las notas de configuración siguientes se aplican a la mayoría de las implementaciones:  

- Algunas opciones se basan en otras (por ejemplo, la Detección de bosques de Active Directory, los límites y los grupos de límites).  

- Varias configuraciones tienen valores predeterminados que se usan sin cambios de configuración, al menos al principio.  

- Otras, como los grupos de límites y los grupos de puntos de distribución, se deben configurar antes de usarlas.  

| Acción | Detalles |  
|------------|-------------|  
| Configurar la administración basada en roles | Separe las asignaciones administrativas para controlar qué usuarios administrativos pueden ver y administrar los distintos objetos y datos de su entorno de Configuration Manager.<br /><br /> Las configuraciones de la administración basada en roles se comparten con todos los sitios de una jerarquía.   <br/><br/>Para obtener más información, vea [Configurar la administración basada en roles](configure-role-based-administration.md). |  
| Publicar datos del sitio en Active Directory Domain Services | Permita que los clientes encuentren fácilmente servicios y que usen de manera eficiente los recursos del sitio.<br /><br /> En primer lugar, [extienda el esquema de Active Directory](../../../plan-design/network/extend-the-active-directory-schema.md). Después, configure cada sitio de forma individual para [publicar datos del sitio](publish-site-data.md). |  
| Configurar un punto de conexión de servicio | Planee la instalación y configuración del punto de conexión de servicio en el sitio de nivel superior de la jerarquía. Para obtener más información, consulte [About the service connection point](about-the-service-connection-point.md) (Sobre el punto de conexión del servicio). |  
| Agregar roles de sistema de sitio | Instale uno o varios roles de sistema de sitio adicionales para sitios individuales. Para obtener más información, vea [Agregar roles del sistema de sitio](add-site-system-roles.md). |  
| Configurar límites de sitio y grupos de límites | Especifique límites que definan ubicaciones de red de la intranet que puede contener los dispositivos que quiere administrar. Después, configure los grupos de límites para que los clientes en esas ubicaciones de red puedan encontrar recursos de Configuration Manager. Para obtener más información, vea [Definir los límites del sitio y los grupos de límites](define-site-boundaries-and-boundary-groups.md). |  
| Configurar grupos de puntos de distribución | Configure grupos lógicos de puntos de distribución para facilitar la administración de las implementaciones. Para obtener más información, vea [Administrar grupos de puntos de distribución](install-and-configure-distribution-points.md#bkmk_manage). |  
| Ejecutar la detección | Ejecute la detección para buscar recursos en la red, incluidos los usuarios, los dispositivos y la infraestructura de red.<br /><br /> Para obtener más información, vea [Ejecutar la detección](run-discovery.md). |  
| Agregar redundancia y capacidad para los administradores | Puede instalar proveedores de SMS adicionales y consolas de Configuration Manager para expandir la capacidad de los administradores para administrar la infraestructura:<br /><br /> **Instale proveedores de SMS adicionales** para proporcionar redundancia para la consola y las conexiones de API al sitio. Para obtener más información, vea [Administración del proveedor de SMS](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).<br /><br /> **Instale consolas de Configuration Manager adicionales** para proporcionar acceso a otros usuarios administrativos. Para obtener más información, consulte [Instalar la consola de System Center Configuration Manager](../install/install-consoles.md). |  
| Configurar componentes de sitio | Puede configurar componentes de sitio en cada sitio para modificar el comportamiento de los roles de sistema de sitio y los informes de estado de sitio. Para obtener más información, vea [Componentes de sitio](site-components.md). |  
| Crear recopilaciones personalizadas | Con la información que el sitio detecta sobre los dispositivos y usuarios, cree colecciones personalizadas de objetos para simplificar las tareas de administración futuras. Para obtener más información, vea [Creación de recopilaciones](../../../clients/manage/collections/create-collections.md). |  
| Configurar opciones para administrar implementaciones de alto riesgo | Configure opciones en un sitio para avisar a los administradores cuando creen una implementación de alto riesgo. Para obtener más información, consulte [Settings to manage high-risk deployments](../../manage/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo). |  
| Configurar réplicas de bases de datos para puntos de administración | Configure una réplica de base de datos para reducir la carga del procesador que los puntos de administración colocan en el servidor de base de datos del sitio al atender las solicitudes de servicio de los clientes. Para obtener más información, vea [Réplicas de bases de datos para puntos de administración ](database-replicas-for-management-points.md). |  
| Configurar un grupo de disponibilidad de SQL Server Always On | Configure grupos de disponibilidad como soluciones de alta disponibilidad y recuperación ante desastres para hospedar la base de datos del sitio en sitios primarios y en el sitio de administración central. Para obtener más información, vea [SQL Server Always On para una base de datos de sitio de alta disponibilidad](sql-server-alwayson-for-a-highly-available-site-database.md). |  
| Modificar la replicación entre sitios | Vea [Transferencias de datos entre sitios](../../../plan-design/hierarchy/data-transfers-between-sites.md) para obtener más información sobre los temas siguientes:<br /><br /> Configurar la [replicación basada en archivos](../../../plan-design/hierarchy/file-based-replication.md) entre sitios secundarios<br /><br /> Configurar [vínculos de replicación de base de datos](../../../plan-design/hierarchy/database-replication.md)<br /><br /> Configurar [vistas distribuidas](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) |  
| Configurar los servidores de sitio en modo pasivo | A partir de la versión 1806, configure un servidor de sitio en modo pasivo para cada sitio primario y el sitio de administración central. Esta característica proporciona un servidor de sitio de alta disponibilidad. Para obtener más información, vea [Alta disponibilidad de servidor de sitio](site-server-high-availability.md). |  
