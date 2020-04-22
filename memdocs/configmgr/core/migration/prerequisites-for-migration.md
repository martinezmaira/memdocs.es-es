---
title: Requisitos previos de la migración
titleSuffix: Configuration Manager
description: Obtenga información sobre las versiones admitidas de Configuration Manager, los idiomas admitidos del sitio de origen y las configuraciones necesarias para llevar a cabo la migración.
ms.date: 05/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 229a8c7980933480a243278b2679d55f012490ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693423"
---
# <a name="prerequisites-for-migration-in-configuration-manager"></a>Requisitos previos para la migración en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para migrar desde una jerarquía de origen compatible, debe tener acceso a cada sitio de origen de Configuration Manager aplicable. También debe tener permisos en el sitio de destino de Configuration Manager para configurar y ejecutar operaciones de migración.  

 Use la información de las secciones siguientes para conocer las versiones de Configuration Manager compatibles con la migración y las configuraciones necesarias.  

-   [Versiones de Configuration Manager admitidas para la migración](#BKMK_SupportedMigrationVersions)  

-   [Idiomas del sitio de origen que se admiten para la migración](#BKMK_SorceSiteLanguage)  

-   [Configuraciones necesarias para la migración](#BKMK_Required_Configurations)  

##  <a name="versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a> Versiones de Configuration Manager admitidas para la migración  
 Puede migrar datos de una jerarquía de origen que ejecute cualquiera de las siguientes versiones de Configuration Manager:  

- Configuration Manager 2007 SP2 (para los efectos de la migración, Configuration Manager 2007 R2 o R3 en el sitio de origen no se tiene en cuenta. Si el sitio de origen ejecuta SP2, se admitirán los sitios que tengan instalado el complemento R2 o R3 para la migración a la rama actual de Configuration Manager).  

- System Center 2012 Configuration Manager SP2 o System Center 2012 R2 Configuration Manager SP1.  

  > [!TIP]  
  >  Además de la migración, puede usar una actualización local de los sitios que ejecutan System Center 2012 Configuration Manager a la rama actual de Configuration Manager.  

- Una jerarquía de Configuration Manager de la misma versión o una inferior de Configuration Manager.  

  Por ejemplo, si tiene una jerarquía de destino que ejecuta la versión 1606 de la rama actual de Configuration Manager, podría usar la migración para copiar datos de una jerarquía de origen que ejecute la versión 1606 o 1602. Sin embargo, no podría migrar datos de una jerarquía de origen que ejecuta la versión 1610.  


##  <a name="source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a> Idiomas del sitio de origen que se admiten para la migración  
 Cuando migra datos entre jerarquías de Configuration Manager, estos se almacenan en la jerarquía de destino en el formato independiente del idioma de Configuration Manager. Debido a que Configuration Manager 2007 no almacena datos en un formato neutral de idioma, el proceso de migración debe convertir los objetos a este formato durante la migración de Configuration Manager 2007. Por lo tanto, solo los sitios de origen de Configuration Manager 2007 que se instalan con los siguientes idiomas son compatibles con la migración:  

-   Inglés  

-   Francés  

-   Alemán  

-   Japonés  

-   Coreano  

-   Ruso  

-   Chino simplificado  

-   Chino tradicional  

Al migrar datos desde una jerarquía de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, no hay ninguna limitación en los idiomas del sitio de origen. Los objetos de la base de datos del sitio de origen ya están en un formato neutral de idioma.  

##  <a name="required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a> Configuraciones necesarias para la migración  
A continuación, se enumeran las configuraciones necesarias para el uso de la migración y las operaciones de migración:  

- **Para configurar, ejecutar y supervisar la migración en la consola de Configuration Manager:**  

   En el sitio de destino, su cuenta debe tener asignado el rol de seguridad de administración basada en roles de **Administrador de infraestructuras**. Este rol de seguridad concede permisos para administrar todas las operaciones de migración, lo que incluye la creación de trabajos de migración, limpieza, supervisión, y la acción de compartir y actualizar puntos de distribución.  

- **Recopilación de datos:**  

   Para permitir que el sitio de destino recopile datos, debe configurar las dos cuentas de acceso del sitio de origen siguientes para su uso con cada sitio de origen:  

  -   **Cuenta de sitio de origen:** esta cuenta se usa para acceder al proveedor de SMS del sitio de origen.  

      -   Para un sitio de origen de Configuration Manager 2007 SP2, esta cuenta necesita el permiso **Leer** para todos los objetos del sitio de origen.  

      -   En cuanto a un sitio de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, esta cuenta requiere el permiso **Leer** en todos los objetos del sitio de origen. Este permiso se concede a la cuenta mediante la administración basada en roles. Para más información sobre cómo usar la administración basada en roles, vea [Conceptos básicos de la administración basada en roles de Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

  -   **Cuenta de base de datos del sitio de origen:** esta cuenta se usa para tener acceso a la base de datos de SQL Server del sitio de origen y necesita los permisos **Conectar**, **Ejecutar** y **Seleccionar** para la base de datos del sitio de origen.  

  Puede configurar estas cuentas cuando configure una nueva jerarquía de origen, cuando configure la recopilación de datos para un sitio de origen adicional o cuando vuelva a configurar las credenciales para un sitio de origen. Estas cuentas pueden utilizar una cuenta de usuario de dominio, o puede especificar la cuenta de equipo del sitio de nivel superior de la jerarquía de destino.  

  > [!IMPORTANT]  
  >  Si usa la cuenta de equipo de Configuration Manager, asegúrese de que esta cuenta forma parte del grupo de seguridad **Usuarios COM distribuidos** en el dominio donde reside el sitio de origen.  

  Al recopilar datos, se utilizan los puertos y protocolos de red siguientes:  

  -   NetBIOS/SMB - 445 (TCP)  

  -   RPC (WMI) - 135 (TCP)  

  -   SQL Server - los puertos TCP que utilizan bases de datos de sitios de origen y de destino.  

- **Migrar actualizaciones de software:**  

   Antes de migrar actualizaciones de software, debe configurar la jerarquía de destino con un punto de actualización de software. Para obtener más información, consulte [Planeación de la migración de actualizaciones de software](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

- **Compartir puntos de distribución:**  

   Para compartir correctamente cualquier punto de distribución de un sitio de origen, al menos un sitio primario o el sitio de administración central de la jerarquía de destino debe usar los mismos números de puerto para las solicitudes de cliente que el sitio de origen. Para más información sobre los puertos de solicitud de cliente, vea [Configurar puertos de comunicación de cliente](../../core/clients/deploy/configure-client-communication-ports.md).  

   Para cada sitio de origen, solo se comparten los puntos de distribución que se instalan en los servidores del sistema de sitio que se configuran con un FQDN.  

   Además, para compartir un punto de distribución de un sitio de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, la **cuenta de sitio de origen** (que obtiene acceso al proveedor de SMS del servidor del sitio de origen) debe tener el permiso **Modificar** en el objeto **Sitio** del sitio de origen. Este permiso se concede a la cuenta mediante la administración basada en roles. Para más información sobre cómo usar la administración basada en roles, vea [Conceptos básicos de la administración basada en roles de Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


- **Actualizar o volver a asignar puntos de distribución:**  

   La **Cuenta de acceso del sitio de origen** configurada para recopilar datos del proveedor de SMS del sitio de origen debe tener los permisos siguientes:  

  - Para actualizar un punto de distribución de Configuration Manager 2007, la cuenta necesita los permisos **Leer**, **Ejecutar** y **Eliminar** en la clase **Sitio** en el servidor de sitio de Configuration Manager 2007 para quitar correctamente el punto de distribución del sitio de origen de Configuration Manager 2007.  

  - Para reasignar un punto de distribución de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, la cuenta debe tener el permiso **Modificar** en el objeto **Sitio** en el sitio de origen. Este permiso se concede a la cuenta mediante la administración basada en roles. Para más información sobre cómo usar la administración basada en roles, vea [Conceptos básicos de la administración basada en roles de Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    Para actualizar o reasignar correctamente un punto de distribución a una nueva jerarquía, los puertos que se configuran para solicitudes de clientes, en el sitio que administra el punto de distribución de la jerarquía de origen, deben coincidir con los puertos que se configuran para solicitudes de clientes en el sitio de destino que administrará el punto de distribución. Para más información sobre los puertos de solicitud de cliente, vea [Configurar puertos de comunicación de cliente](../../core/clients/deploy/configure-client-communication-ports.md).  
