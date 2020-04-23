---
title: Procedimientos recomendados para las actualizaciones de software
titleSuffix: Configuration Manager
description: Use estos procedimientos recomendados para actualizaciones de software en Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: dc0d416fdd186dbbeb4c61d48b688072bb830485
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708713"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Procedimientos recomendados para actualizaciones de software en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo incluye procedimientos recomendados para actualizaciones de software en Configuration Manager. La información se ordena en procedimientos recomendados para la instalación inicial y para las operaciones en curso.  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a> Procedimientos recomendados de instalación  

Use los procedimientos recomendados siguientes cuando instale actualizaciones de software en Configuration Manager.  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a> Usar una base de datos WSUS compartida para los puntos de actualización de software  

Cuando instale más de un punto de actualización de software en un sitio primario, utilice la misma base de datos de WSUS para cada punto de actualización de software del mismo bosque de Active Directory. Si se comparte la misma base de datos, se mitiga significativamente (aunque no se elimina por completo) el impacto sobre el rendimiento de la red y el cliente que podría experimentarse cuando los clientes cambian a un nuevo punto de actualización de software. Cuando un cliente cambia a un nuevo punto de actualización de software que comparte una base de datos con el punto de actualización de software anterior, se sigue produciendo un examen de diferencias, pero es mucho menor que si el servidor WSUS tuviera su propia base de datos. Para obtener más información sobre el cambio del punto de actualización de software, vea [Cambio de punto de actualización de software](plan-for-software-updates.md#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Cuando se utiliza una base de datos WSUS compartida para los puntos de actualización de software, comparta también las carpetas locales de contenido de WSUS.  

Para obtener más información sobre el uso compartido de la base de datos WSUS, consulte las siguientes entradas de blog:  

- [How to implement a shared SUSDB for Configuration Manager software update points (Cómo implementar un SUSDB compartido para los puntos de actualización de software de Configuration Manager)](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Consideraciones para varias instancias WSUS que comparten una base de datos de contenido cuando se usa Configuration Manager](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/)  


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a> Si Configuration Manager y WSUS usan el mismo servidor SQL Server, configure uno para que use una instancia con nombre y el otro para que use la instancia predeterminada  

Si las bases de datos de Configuration Manager y WSUS comparten la misma instancia de SQL Server, no podrá determinar fácilmente el uso de recursos entre las dos aplicaciones. Use diferentes instancias de SQL Server para Configuration Manager y WSUS. Esta configuración facilita diagnosticar y solucionar problemas del uso de recursos que pudieran producirse en cada aplicación.  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a> Especificar la configuración de "Guardar actualizaciones localmente"  

Cuando instale WSUS, seleccione la opción de **Guardar actualizaciones localmente**. Esta configuración hace que WSUS descargue los términos de licencia que están asociados con las actualizaciones de software. Descarga los términos durante el proceso de sincronización y los almacena en la unidad de disco duro local para el servidor WSUS. Si no selecciona esta opción, los equipos cliente pueden producir un error de análisis de cumplimiento para actualizaciones de software que tengan términos de licencia. El componente **Administrador de sincronización de WSUS** del punto de actualización de software comprueba que esta configuración se habilita cada 60 minutos, de forma predeterminada.  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a> Procedimientos recomendados de uso  

Siga las recomendaciones siguientes al usar las actualizaciones de software:  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a> Limitar las actualizaciones de software a 1000 en una única implementación de actualización de software  

Limite el número de actualizaciones de software a 1000 en cada implementación de actualización de software. Cuando cree una regla de implementación automática, compruebe que los criterios especificados no den como resultado más de 1000 actualizaciones de software. Si implementa manualmente las actualizaciones de software, no seleccione más de 1000 actualizaciones.  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a> Crear un nuevo grupo de actualizaciones de software cada vez que se ejecuta una ADR para "Patch Tuesday" y para la implementación general  

Hay un límite de 1000 actualizaciones de software en una implementación. Cuando cree una regla de implementación automática (ADR), especifique si quiere utilizar un grupo de actualización existente o crear un nuevo grupo de actualización cada vez que se ejecute la regla. Si especifica criterios en una ADR que resulte en varias actualizaciones de software y la regla se ejecuta en una programación recurrente, cree un nuevo grupo de actualizaciones de software cada vez que se ejecute la regla. Este comportamiento evita que se sobrepase el límite de 1000 actualizaciones de software por implementación.  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a> Usar un grupo de actualizaciones de software existente para las ADR para actualizaciones de definiciones de Endpoint Protection  

Si usa una ADR para implementar las actualizaciones de definiciones de Endpoint Protection con frecuencia, use siempre un grupo de actualizaciones de software existente. De lo contrario, con el paso del tiempo, la ADR puede crear cientos de grupos de actualizaciones de software. Por lo general, los publicadores de actualizaciones de definición establecerán la caducidad de estas actualizaciones cuando sean reemplazadas por cuatro actualizaciones más recientes. Por lo tanto, el grupo de actualizaciones de software que se crea mediante la ADR nunca contendrá más de cuatro actualizaciones de definiciones para el publicador: una activa y tres obsoletas.  



## <a name="see-also"></a>Consulte también  
 [Planear las actualizaciones de software](plan-for-software-updates.md)
