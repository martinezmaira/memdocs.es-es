---
title: Jerarquías de origen de migración
titleSuffix: Configuration Manager
description: Configure una jerarquía de origen y sitios de origen para poder migrar datos al entorno de la rama actual de Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2e8e2ba57867b3c2a0929cfd670629296fdb9c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701783"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-configuration-manager-current-branch"></a>Configuración de jerarquías de origen y sitios de origen para la migración a la rama actual de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Para habilitar la migración de datos a la rama actual de Configuration Manager, debe configurar una jerarquía de origen de Configuration Manager compatible y uno o varios sitios de origen de esa jerarquía que contengan los datos que quiere migrar.  

> [!NOTE]  
>  Las operaciones de la migración se ejecutan en el sitio de nivel superior en la jerarquía de destino. Si configura la migración cuando use una consola de Configuration Manager conectada a un sitio primario secundario, debe dejar tiempo para que la configuración se replique en el sitio de administración central, para que se inicie y, luego, replicar el estado de vuelta al sitio primario al que está conectado.  

 Use la información y los procedimientos de las secciones siguientes para especificar la jerarquía de origen y para agregar sitios de origen adicionales. Después de completar estos procedimientos, puede crear trabajos de migración y empezar a migrar datos de la jerarquía de origen a la jerarquía de destino.  

-   [Especificar una jerarquía de origen para la migración](#BKBM_ConfigSrcHierarchy)  

-   [Identificar sitios de origen adicionales de la jerarquía de origen](#BKBM_ConfigSrcSites)  

##  <a name="specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a> Especificar una jerarquía de origen para la migración  
 Para migrar datos a la jerarquía de destino, debe especificar una jerarquía de origen compatible que contenga los datos que quiere migrar. De forma predeterminada, el sitio de nivel superior de esa jerarquía se convierte en un sitio de origen de la jerarquía de origen. Si migra desde una jerarquía de Configuration Manager 2007, puede configurar sitios de origen adicionales para la migración después recopilar los datos del sitio de origen inicial. Si migra desde una jerarquía de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, no tiene que configurar sitios de origen adicionales para migrar datos desde la jerarquía de origen. Esto se debe a que estas versiones de Configuration Manager usan una base de datos compartida que está disponible en el sitio de nivel superior de la jerarquía de origen. La base de datos compartida contiene toda la información que puede migrar.  

 Use los procedimientos siguientes para especificar una jerarquía de origen para la migración y para identificar sitios de origen adicionales en una jerarquía de Configuration Manager 2007.  

 Realice este procedimiento con una consola de Configuration Manager que esté conectada a la jerarquía de destino:  

### <a name="to-configure-a-source-hierarchy"></a>Para configurar una jerarquía de origen   

1. En la consola de Configuration Manager, haga clic en **Administración**.  

2. En el área de trabajo **Administración** , expanda **Migración**y, a continuación, haga clic en **Jerarquía de orígenes**.  

3. En la pestaña **Inicio** , en el grupo **Migración** , haga clic en **Especificar la jerarquía de origen**.  

4. En el cuadro de diálogo **Especificar la jerarquía de origen** para **Jerarquía de origen**, seleccione **Nueva jerarquía de origen**.  

5. En **Servidor de sitio de Configuration Manager de nivel superior**, especifique el nombre o la dirección IP del sitio de nivel superior de una jerarquía de origen admitida.  

6. Especifique cuentas de acceso del sitio de origen que tengan los siguientes permisos:  

   - Cuenta de sitio de origen: permiso **Leer** del proveedor de SMS para el sitio de nivel superior especificado en la jerarquía de origen. Las actualizaciones y el uso compartido de puntos de distribución requieren los permisos **Modificar** y **Eliminar** para el sitio en la jerarquía de origen.

   - Cuenta de base de datos del sitio de origen: permisos **Leer** y **Ejecutar** de la base de datos de SQL Server para el sitio de nivel superior especificado en la jerarquía de origen.  

     Si especifica el uso de la cuenta de equipo, Configuration Manager usa la cuenta de equipo del sitio de nivel superior de la jerarquía de destino. Para esta opción, asegúrese de que esta cuenta sea miembro del grupo de seguridad **Usuarios COM distribuidos** en el dominio en el que reside el sitio de nivel superior de la jerarquía de origen.  

7. Para compartir puntos de distribución entre las jerarquías de origen y de destino, active la casilla **Habilitar uso compartido del punto de distribución para el servidor de sitio de origen** . Si no habilita el uso compartido del punto de distribución en este momento, podrá hacerlo mediante la edición de las credenciales del sitio de origen una vez completada la recopilación de datos.  

8. Haga clic en **Aceptar** para guardar la configuración. Se abrirá el cuadro de diálogo **Estado de obtención de datos** y la recopilación de los datos se iniciará automáticamente.  

9. Cuando finalice la obtención de datos, haga clic en **Cerrar** para cerrar el cuadro de diálogo **Estado de obtención de datos** y complete la configuración.  

##  <a name="identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a> Identificar sitios de origen adicionales de la jerarquía de origen  
 Cuando se configura una jerarquía de origen compatible, el sitio de nivel superior de esa jerarquía se configura automáticamente como un sitio de origen y se recopilan datos automáticamente de ese sitio. La siguiente acción que realice depende de la versión de Configuration Manager que ejecute la jerarquía de origen:  

-   En una jerarquía de origen de Configuration Manager 2007, puede comenzar la migración desde ese sitio de origen inicial o configurar sitios de origen adicionales desde la jerarquía de origen después finalizar la recopilación de datos del sitio de origen inicial. Para migrar datos que solo estén disponibles en un sitio secundario, configure sitios de origen adicionales para una jerarquía de Configuration Manager 2007. Por ejemplo, puede configurar sitios de origen adicionales para recopilar datos sobre el contenido que quiere migrar cuando ese contenido se crea en un sitio secundario en la jerarquía de origen y no está disponible en el sitio superior de la jerarquía de origen.  

-   En una jerarquía de origen de System Center 2012 Configuration Manager o de la rama actual de Configuration Manager, no es necesario configurar sitios de origen adicionales. Esto se debe a que estas versiones de Configuration Manager usan una base de datos compartida que está disponible en el sitio de nivel superior de la jerarquía de origen. La base de datos compartida contiene toda la información que puede migrar desde todos los sitios de esa jerarquía de origen. Esto hace que los datos que se pueden migrar estén disponibles desde el sitio de nivel superior de la jerarquía de origen.  

Cuando configure sitios de origen adicionales para una jerarquía de origen de Configuration Manager 2007, deberá configurar los sitios de origen adicionales desde la parte superior de la jerarquía de origen hasta la parte inferior. Debe configurar un sitio primario como un sitio de origen antes de configurar cualquiera de sus sitios secundarios como sitios de origen.  

Use el siguiente procedimiento para configurar sitios de origen adicionales para jerarquías de origen de Configuration Manager 2007:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Para identificar sitios de origen adicionales en la jerarquía de origen 

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Migración**y, a continuación, haga clic en **Jerarquía de orígenes**.  

3.  Seleccione el sitio que quiere configurar como un sitio de origen.  

4.  En la pestaña **Inicio** , en el grupo **Sitio de origen** , haga clic en **Configurar**.  

5.  En el cuadro de diálogo **Credenciales del sitio de origen** , para las cuentas de acceso del sitio de origen, especifique las cuentas que tengan los permisos siguientes:  

    -   Cuenta de sitio de origen: permiso **Leer** del proveedor de SMS para el sitio de nivel superior especificado en la jerarquía de origen. Las actualizaciones y el uso compartido de puntos de distribución requieren los permisos **Modificar** y **Eliminar** para el sitio en la jerarquía de origen.  

    -   Cuenta de base de datos del sitio de origen: permisos **Leer** y **Ejecutar** de la base de datos de SQL Server para el sitio de nivel superior especificado en la jerarquía de origen.  

    Si especifica el uso de la cuenta de equipo, Configuration Manager usa la cuenta de equipo del sitio de nivel superior de la jerarquía de destino. Para esta opción, asegúrese de que esta cuenta sea miembro del grupo de seguridad **Usuarios COM distribuidos** en el dominio en el que reside el sitio de nivel superior de la jerarquía de origen.  

6.  Para compartir puntos de distribución entre las jerarquías de origen y de destino, active la casilla **Habilitar uso compartido del punto de distribución para el servidor de sitio de origen** . Si no habilita el uso compartido del punto de distribución en este momento, podrá hacerlo mediante la edición de las credenciales del sitio de origen una vez completada la recopilación de datos.  

7. Haga clic en **Aceptar** para guardar la configuración. Se abrirá el cuadro de diálogo **Estado de obtención de datos** y la recopilación de los datos se iniciará automáticamente.  

8.  Cuando termine la recopilación de datos, haga clic en **Cerrar** para completar la configuración.  
