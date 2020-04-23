---
title: Aspectos básicos de la administración basada en roles
titleSuffix: Configuration Manager
description: Use la administración basada en roles para controlar el acceso administrativo a Configuration Manager y a los objetos que administra.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 62faf2fd736f9751e8b33e821cb814f527a1197c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707093"
---
# <a name="fundamentals-of-role-based-administration-for-configuration-manager"></a>Aspectos básicos de la administración basada en roles de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Con Configuration Manager, la administración basada en roles sirve para proteger el acceso que se necesita para administrar Configuration Manager. Además, protege el acceso a los objetos que administra, como las recopilaciones, implementaciones y sitios. Una vez que comprenda los conceptos presentados en este artículo, podrá [configurar la administración basada en roles para Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 El modelo de administración basada en roles define y administra de manera centralizada la configuración de acceso de seguridad de la totalidad de la jerarquía para todos los sitios y sus configuraciones, mediante los elementos siguientes:  

- Los *roles de seguridad* se asignan a los usuarios administrativos para proporcionar a dichos usuarios (o grupos de usuarios) permisos de diferentes objetos de Configuration Manager. Por ejemplo, permiso para crear o cambiar la configuración del cliente.  

- Los *ámbitos de seguridad* se usan para agrupar instancias específicas de objetos que un usuario administrativo se encarga de administrar, como una aplicación que instala Microsoft Office 2010.  

- Las *recopilaciones* se usan para especificar grupos de recursos de usuarios y de dispositivos que el usuario administrativo puede administrar.  

  Con la combinación de roles de seguridad, ámbitos de seguridad y recopilaciones, proporciona las asignaciones administrativas que cumplen los requisitos de su organización. Si se usan conjuntamente, definen el ámbito administrativo de un usuario, que es lo que el usuario puede ver y administrar en su implementación de Configuration Manager.  

## <a name="benefits-of-role-based-administration"></a>Ventajas de la administración basada en roles  

- Los sitios no se usan como límites administrativos.  
- Puede crear usuarios administrativos para una jerarquía y solo es necesario asignarles la seguridad una vez.  
- Todas las asignaciones de seguridad se replican y están disponibles en toda la jerarquía.  
- Existen roles de seguridad integrados que se usan para asignar las tareas de administración habituales. Cree sus propios roles de seguridad personalizados para satisfacer sus requisitos empresariales específicos.  
- Los usuarios administrativos solo ven los objetos que tienen permisos para administrar.  
- Puede auditar las acciones de seguridad administrativa.  

Al diseñar e implementar la seguridad administrativa de Configuration Manager, se usa lo siguiente para crear un *ámbito administrativo* para un usuario administrativo:  

- [Roles de seguridad](#bkmk_Planroles)  

- [Recopilaciones](#bkmk_planCol)  

- [Ámbitos de seguridad](#bkmk_PlanScope)  

 El ámbito administrativo controla los objetos que un usuario administrativo ve en la consola de Configuration Manager y controla los permisos que el usuario tiene en dichos objetos. Las configuraciones de administración basada en roles se replican en cada sitio en la jerarquía como datos globales y, a continuación, se aplican a todas las conexiones administrativas.  

> [!IMPORTANT]  
> Los retrasos de replicación entre sitios pueden impedir que un sitio reciba los cambios de la administración basada en roles. Para más información sobre cómo supervisar la replicación de base de datos entre sitios, vea el tema [Transferencias de datos entre sitios](../plan-design/hierarchy/data-transfers-between-sites.md).  

##  <a name="security-roles"></a><a name="bkmk_Planroles"></a> Roles de seguridad

 Use roles de seguridad para conceder permisos de seguridad a usuarios administrativos. Los roles de seguridad son grupos de permisos de seguridad que se asignan a usuarios administrativos para que puedan realizar sus tareas administrativas. Estos permisos de seguridad definen las acciones administrativas que un usuario administrativo puede realizar y los permisos que se conceden para determinados tipos de objetos. Como medida de seguridad recomendada, asigne roles de seguridad que proporcionen el menor nivel de permisos.  

 Configuration Manager dispone de varios roles de seguridad integrados para admitir las agrupaciones habituales de tareas administrativas. Puede crear sus propios roles de seguridad para satisfacer sus requisitos empresariales. Ejemplos de roles de seguridad integrados:  

- *Administrador total* concede todos los permisos en Configuration Manager.  

- *Administrador de activos* concede permisos para administrar el punto de sincronización de Asset Intelligence, las clases de notificaciones, el inventario de software, el inventario de hardware y las reglas de disponibilidad.  

- *Administrador de actualizaciones de software* concede permisos para definir e implementar actualizaciones de software. Los usuarios administrativos asociados a este rol pueden crear recopilaciones, grupos de actualizaciones de software, implementaciones y plantillas.  

- El *administrador de seguridad* concede permiso para agregar y quitar los usuarios administrativos y asociar estos usuarios con roles de seguridad, recopilaciones y ámbitos de seguridad. Los usuarios administrativos que están asociados con este rol también pueden crear, modificar y eliminar los roles de seguridad y sus recopilaciones y ámbitos de seguridad asignados.

> [!TIP]  
> Puede ver la lista de los roles de seguridad integrados y los roles de seguridad personalizados que crea, y sus descripciones, en la consola de Configuration Manager. Para ver los roles, en el área de trabajo **Administración**, expanda **Seguridad** y, después, seleccione **Roles de seguridad**.  

 Cada rol de seguridad tiene determinados permisos para distintos tipos de objetos. Por ejemplo, el rol de seguridad *Administrador de aplicaciones* tiene los permisos siguientes para las aplicaciones: Aprobar, Crear, Eliminar, Modificar, Modificar carpeta, Mover objeto, Leer, Ejecutar informe y Establecer ámbito de seguridad.

 No puede cambiar los permisos de los roles de seguridad integrados, pero puede copiar el rol, realizar cambios y, a continuación, guardar estos cambios como un nuevo rol de seguridad personalizado. También puede importar roles de seguridad que ha exportado desde otra jerarquía, por ejemplo, de una red de prueba. Revise los roles de seguridad y sus permisos para determinar si usará los roles de seguridad integrados o si debe crear sus propios roles de seguridad personalizados.  

### <a name="to-help-you-plan-for-security-roles"></a>Para ayudarle a planear los roles de seguridad  

1. Identifique las tareas que los usuarios administrativos realizan en Configuration Manager. Estas tareas pueden estar relacionadas con uno o más grupos de tareas de administración, como la implementación de aplicaciones y paquetes, la implementación de sistemas operativos y configuraciones para el cumplimiento, la configuración de sitios y seguridad, la realización de auditorías, el control remoto de equipos y la recopilación de datos de inventario.  

2. Asigne estas tareas administrativas a uno o varios roles de seguridad integrados.  

3. Si algunos de los usuarios administrativos realiza las tareas de varios roles de seguridad, asigne dichos roles de seguridad a estos usuarios administrativos en vez de crear un nuevo rol de seguridad que combine las tareas.  

4. Si las tareas que identificó no se ajustan a los roles de seguridad integrados, cree y pruebe nuevos roles de seguridad.  

Para más información sobre cómo crear y configurar roles de seguridad para la administración basada en roles, vea [Crear roles de seguridad personalizados](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) y [Configurar roles de seguridad](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) en el artículo [Configurar la administración basada en roles para Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

##  <a name="collections"></a><a name="bkmk_planCol"></a> Recopilaciones

 Las recopilaciones especifican los recursos de usuario y equipo que los usuarios administrativos pueden ver o administrar. Por ejemplo, para que los usuarios administrativos puedan implementar aplicaciones o ejecutar el control remoto, deben estar asignados a un rol de seguridad que conceda acceso a la recopilación que contiene dichos recursos. Puede seleccionar recopilaciones de usuarios o dispositivos.  

 Para más información sobre las recopilaciones, vea [Introducción a las recopilaciones](../../core/clients/manage/collections/introduction-to-collections.md).  

 Antes de configurar la administración basada en roles, compruebe si tiene que crear nuevas recopilaciones por cualquiera de las siguientes razones:  

- Organización funcional. Por ejemplo, separar recopilaciones de servidores y estaciones de trabajo.  
- Alineación geográfica. Por ejemplo, separar recopilaciones de Europa y América del Norte.  
- Requisitos de seguridad y procesos empresariales. Por ejemplo, separar las recopilaciones para equipos de prueba y producción.  
- Alineación de la organización. Por ejemplo, separar recopilaciones para cada unidad de negocio.  

Para más información sobre cómo configurar recopilaciones para la administración basada en roles, vea [Configurar recopilaciones para administrar la seguridad](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) en el artículo [Configurar la administración basada en roles para Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="security-scopes"></a><a name="bkmk_PlanScope"></a> Ámbitos de seguridad

 Use los ámbitos de seguridad para proporcionar acceso a objetos protegibles para los usuarios administrativos. Un ámbito de seguridad es un conjunto de objetos protegibles asignados a usuarios administrativos como un grupo. Todos los objetos protegibles deben estar asignados a uno o más ámbitos de seguridad. Configuration Manager tiene dos ámbitos de seguridad integrados:  

- El ámbito de seguridad integrado *Todo* concede acceso a todos los ámbitos. No se pueden asignar objetos a este ámbito de seguridad.  

- El ámbito de seguridad integrado *Predeterminado* se usa para todos los objetos de manera predeterminada. Cuando se instala inicialmente Configuration Manager, todos los objetos se asignan a este ámbito de seguridad.  

Si desea restringir los objetos que los usuarios administrativos pueden ver y administrar, debe crear y utilizar sus propios ámbitos de seguridad personalizados. Los ámbitos de seguridad no admiten estructuras jerárquicas y no se pueden anidar. Los ámbitos de seguridad pueden contener uno o varios tipos de objetos, como los siguientes:  

- Suscripciones de alerta  
- Aplicaciones  
- Imágenes de arranque  
- Grupos de límites  
- Elementos de configuración  
- Configuraciones personalizadas de cliente  
- Puntos de distribución y grupos de puntos de distribución  
- Paquetes de controladores
- Carpetas (a partir de la versión 1906) <!--3600867-->
- Condiciones globales  
- Trabajos de migración
- Imágenes de sistema operativo
- Paquetes de instalación de sistema operativo  
- Paquetes  
- Consultas  
- Sitios  
- Reglas de disponibilidad de software  
- Grupos de actualizaciones de software  
- Paquetes de actualizaciones de software  
- Paquetes de secuencias de tareas  
- Paquetes y elementos de configuración de dispositivos Windows CE  

También hay algunos objetos que no se incluyen en los ámbitos de seguridad ya que solo se pueden proteger mediante roles de seguridad. El acceso administrativo a estos objetos no se puede limitar a un subconjunto de los objetos disponibles. Por ejemplo, puede tener un usuario administrativo que crea grupos de límites que se utilizan en un determinado sitio. Ya que el objeto de límite no admite ámbitos de seguridad, no puede asignar al usuario un ámbito de seguridad que solo proporciona acceso a los límites que puedan estar asociados a ese sitio. Como los objetos de límite no pueden estar asociados a un ámbito de seguridad, cuando asigna un rol de seguridad que incluye el acceso a objetos de límite a un usuario, el usuario puede obtener acceso a todos los límites de la jerarquía.  

Entre los objetos que no están limitados por ámbitos de seguridad se incluyen los siguientes:  

- Bosques de Active Directory  
- Usuarios administrativos  
- Alertas  
- Directivas antimalware  
- Límites  
- Asociaciones de equipos  
- Configuración de cliente predeterminada  
- Plantillas de implementación  
- Controladores de dispositivo  
- Conector de Exchange Server  
- Asignaciones de sitio a sitio de migración  
- Perfiles de inscripción de dispositivo móvil  
- Roles de seguridad  
- Ámbitos de seguridad  
- Direcciones de sitios  
- Roles de sistema de sitio  
- Títulos de software  
- Actualizaciones de software  
- Mensajes de estado  
- Afinidades de dispositivo de usuario  

Cree ámbitos de seguridad si tiene que limitar el acceso a instancias independientes de objetos. Por ejemplo:  

- Un grupo de usuarios administrativos tiene que poder ver las aplicaciones de producción pero no tiene que poder ver aplicaciones de prueba. Cree un ámbito de seguridad para las aplicaciones de producción y otro para las aplicaciones de prueba.  

- Los distintos usuarios administrativos requieren un determinado acceso a algunas instancias de un tipo de objeto. Por ejemplo, un grupo de usuarios administrativos requiere el permiso de lectura en determinados grupos de actualizaciones de software, y otro grupo de usuarios administrativos requiere el permiso Modificar y Eliminar para otros grupos de actualizaciones de software. Cree distintos ámbitos de seguridad para estos grupos de actualizaciones de software.  

Para más información sobre cómo configurar ámbitos de seguridad para la administración basada en roles, vea [Configurar ámbitos de seguridad para un objeto](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) en el artículo [Configurar la administración basada en roles para Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="next-steps"></a>Pasos siguientes

[Configuración de la administración basada en roles para Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
