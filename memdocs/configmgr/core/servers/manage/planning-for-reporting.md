---
title: Planeamiento de informes
titleSuffix: Configuration Manager
description: Desde la información de instalación hasta la seguridad y el ancho de banda de red, es importante planear los informes en Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694373"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Planear la elaboración de informes en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los informes de Configuration Manager proporcionan un conjunto de herramientas y recursos para usar funciones avanzadas de informes de SQL Server Reporting Services en Power BI Report Server. Use las siguientes secciones para planear informes en Configuration Manager.

## <a name="where-to-install-the-reporting-services-point"></a>Decidir la ubicación de la instalación del punto de servicios de informes

Cuando ejecuta informes de Configuration Manager en un sitio, los informes tienen acceso a la información en la base de datos del sitio al que se conectan. Utilice las secciones siguientes para decidir la ubicación de la instalación del punto de servicios de informes y el origen de datos que se debe usar.

> [!NOTE]
> Para obtener más información sobre la planeación de sistemas de sitio en Configuration Manager, consulte [Add site system roles](../deploy/configure/add-site-system-roles.md) (Agregar roles de sistema de sitio).

### <a name="supported-site-system-servers"></a>Servidores de sistema de sitio admitidos

Puede instalar el punto de servicios de informes en un sitio de administración central (CAS) y en un sitio primario. Funciona en varios sistemas de sitio en un sitio, y en otros sitios de la jerarquía. Configuration Manager no es compatible con el punto de servicios de informes en los sitios secundarios. El primer punto de servicios de informes en un sitio está establecido como el servidor de informes predeterminado. Puede agregar más puntos de servicios de informes en un sitio, pero los informes de Configuration Manager usan activamente el servidor de informes predeterminado de cada sitio. Instale el punto de servicios de informes en un servidor de sitio o en un sistema de sitio remoto. Para un rendimiento óptimo, utilice SQL Server Reporting Services en un servidor de sistema de sitio remoto.

### <a name="data-replication-considerations"></a>Consideraciones de replicación de datos

Tenga en cuenta los factores siguientes para determinar la ubicación de la instalación de los puntos de servicios de informes:

- Un punto de servicios de informes con la base de datos del sitio de administración central (CAS) como origen de datos de informes tiene acceso a todos los datos globales y datos de sitio en la jerarquía de Configuration Manager. Si necesita informes que contengan datos de sitio para varios sitios en una jerarquía, considere la posibilidad de instalar el punto de servicios de informes en un sistema de sitio en el CAS. Después, use su base de datos como origen de datos de informes.

- Un punto de servicios de informes con una base de datos de sitio primario secundario como origen de datos de informes tiene acceso a los datos globales y a los datos de sitio solo del sitio primario local y de los sitios secundarios. Los datos de sitio de otros sitios primarios de la jerarquía de Configuration Manager no se replican en este sitio primario. Reporting Services no puede tener acceso a los datos del sitio para otros sitios primarios. Si precisa informes que contengan datos de sitio de un determinado sitio primario o datos globales y no quiere que el usuario tenga acceso a los datos de sitio de otros sitios primarios, instale un punto de servicios de informes en un sistema de sitio en el sitio primario y use la base de datos del sitio primario como origen de datos de informes. Después, use la base de datos de sitio primario como origen de datos de informes.

Para obtener más información sobre los datos globales y de sitio, vea [Tipos de datos](../../plan-design/hierarchy/database-replication.md#types-of-data).

### <a name="network-bandwidth-considerations"></a>Consideraciones de ancho de banda de red

En función de la configuración del sitio, los sistema de sitio en el mismo sitio se comunican entre ellos mediante el uso del protocolo de bloque de mensajes del servidor (SMB), HTTP o HTTPS. Configuration Manager no administra esta comunicación. Puede producirse en cualquier momento sin control de ancho de banda de red. Revise el ancho de banda de red disponible antes de instalar el rol de punto de servicios de informes en un sistema de sitio.

Para obtener más información sobre la planeación de sistemas de sitio, consulte [Add site system roles](../deploy/configure/add-site-system-roles.md) (Agregar roles de sistema de sitio).

## <a name="plan-for-role-based-administration"></a>Planear la administración basada en roles

La seguridad de los informes es como la de otros objetos en Configuration Manager: puede asignar roles y permisos de seguridad a los usuarios administrativos. Los usuarios administrativos solo pueden ejecutar y modificar informes para los que tengan los derechos de seguridad apropiados. Para ejecutar informes en la consola de Configuration Manager, los usuarios deben tener derechos de **Lectura** para el permiso de **Sitio** y los permisos configurados para los objetos correspondientes.

A diferencia de otros objetos en Configuration Manager, los derechos de seguridad que configure para usuarios administrativos en la consola de Configuration Manager también se configuran en Reporting Services. Cuando configura los derechos de seguridad en la consola de Configuration Manager, el punto de servicios de informes se conecta a Reporting Services y configura los permisos adecuados para los informes.

Por ejemplo, el rol de seguridad **Administrador de actualizaciones de software** tiene los permisos **Ejecutar informe** y **Modificar informe**. Los usuarios con el rol de **Administrador de actualizaciones de software** solo pueden ejecutar y modificar informes de actualizaciones de software. La consola de Configuration Manager no muestra informes para otros objetos a este rol. Como excepción a esta regla, algunos informes no están asociados a ningún objeto protegible de Configuration Manager específico. Para estos informes, el usuario administrativo debe tener el derecho de **Leer** para que el permiso **Sitio** ejecute informes, y el derecho **Modificar** para que el permiso **Sitio** modifique informes.  

> [!IMPORTANT]
> Debe existir una relación de confianza bidireccional establecida entre los dos dominios para los usuarios de un dominio distinto al de la cuenta de punto de servicios de informes, para la correcta ejecución de los informes.

Los informes están totalmente habilitados para la administración basada en roles. Configuration Manager filtra los datos de todos los informes incluidos en función de los permisos del usuario que ejecuta el informe. Los usuarios con roles específicos solo pueden ver la información definida para sus roles.

Para obtener más información sobre los derechos de seguridad de los informes, consulte [Configure reporting](configuring-reporting.md) (Configurar los informes).

Para obtener más información sobre la administración basada en roles en Configuration Manager, consulte [Configurar la administración basada en roles](../deploy/configure/configure-role-based-administration.md).

## <a name="reporting-recommendations"></a>Recomendaciones de informes

Tenga en cuenta las siguientes recomendaciones y sugerencias para la creación de informes en Configuration Manager:

- Para un rendimiento óptimo, instale el punto de servicios de informes en un sistema de sitio remoto. Aunque puede instalarlo en el servidor de sitio, el punto de servicios de informes funciona mejor cuando se instala en un sistema de sitio remoto. Cuando este rol realiza el procesamiento en segundo plano, puede competir por los recursos del sistema con otros roles. Hay muchas variables que se deben tener en cuenta con el rendimiento de los roles y del sitio, pero, en general, esta configuración mejora los informes y el rendimiento general del sitio.

- Optimizar consultas de SQL Server Reporting Services. Normalmente, los retrasos de los informes se deben al tiempo que se tarda en ejecutar consultas y recuperar los resultados. Algunas herramientas de Microsoft SQL Server, como el analizador de consultas y el generador de perfiles (Profiler), pueden ayudarle a optimizar las consultas.

- Programar el procesamiento de la suscripción de informes para que se ejecute fuera del horario de oficina estándar. Siempre que sea posible, el procesamiento de suscripciones durante las horas de inactividad puede minimizar el procesamiento de la CPU en el servidor de bases de datos de sitio de Configuration Manager. Esta práctica también mejora la disponibilidad de solicitudes de informes imprevistas.

- Las actualizaciones del sitio conservan los informes integrados. Si modifica un informe estándar, cuando el sitio se actualice, el nombre del informe se cambiará por un prefijo de subrayado (`_`). Este comportamiento garantiza que la actualización del sitio no sobrescriba el informe modificado por el informe estándar.

## <a name="security-and-privacy"></a>Seguridad y privacidad

Los informes de Configuration Manager muestran información recopilada durante operaciones de administración estándar de Configuration Manager. Por ejemplo, puede mostrar un informe con información recopilada por Configuration Manager a partir de un proceso de detección o inventario. Los informes también pueden contener la información de estado actual de las operaciones de administración de cliente, tales como la implementación de software y la comprobación de cumplimiento de normas.

Para más información sobre las recomendaciones de seguridad e información de privacidad de las operaciones de Configuration Manager que pueden generar datos que se pueden ver en informes, vea [Seguridad y privacidad de Configuration Manager](../../plan-design/security/security-and-privacy.md).  

## <a name="next-steps"></a>Pasos siguientes

[Requisitos previos de los informes](prerequisites-for-reporting.md)
