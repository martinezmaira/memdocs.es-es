---
title: Escenarios de instalación
titleSuffix: Configuration Manager
description: Aprenda técnicas para instalar una nueva jerarquía de Configuration Manager mientras efectúa una actualización de un sitio.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a63667faf9590f647c01565f1425081e53bdfc97
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700603"
---
# <a name="scenarios-to-streamline-your-installation-of-configuration-manager"></a>Escenarios para simplificar la instalación de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Con el lanzamiento de las versiones de actualización de la rama actual de Configuration Manager, existen nuevos escenarios que simplifican la instalación de una nueva jerarquía en una versión de actualización (como la actualización 1610) y para actualizar desde Microsoft System Center 2012 Configuration Manager.

Entre los escenarios admitidos se incluyen:  

**Instalación de una nueva jerarquía de la rama actual de Configuration Manager** que ejecuta una versión actualizada.  

-   Instale solo el sitio de nivel superior; luego, instale inmediatamente una instalación para que el sitio esté actualizado con la versión de actualización que va a usar. Luego puede instalar sitios adicionales directamente en esa versión de actualización.  
-   En este escenario, omite el proceso de instalar sitios adicionales en un nivel de línea base y luego actualizarlos a la versión de actualización que quiera usar.  
-   En este escenario, omite el proceso de instalar los clientes en una versión de línea base y luego volver a instalarlos al actualizarlos a una versión posterior.  

**Actualización de una infraestructura de Microsoft System Center 2012 Configuration Manager** a una versión de actualización de Configuration Manager.  

-   Actualice manualmente el sitio de administración central y cada sitio primario a una versión de línea base (como la versión 1606) antes de instalar una versión de actualización (como la versión 1610).  
-   No actualice sitios secundarios desde Microsoft System Center 2012 Configuration Manager hasta que los sitios primarios ejecuten la versión de actualización que se va a usar.  
-   No actualice clientes desde Microsoft System Center 2012 Configuration Manager hasta que los sitios primarios ejecuten la versión de actualización que se va a usar.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Escenario: instalación de una nueva jerarquía en una versión de actualización  
En este escenario de ejemplo, instale el primer sitio de una jerarquía mediante una versión de línea base de Configuration Manager, como la versión 1610. Luego, instale la actualización 1610 antes de implementar sitios o clientes adicionales.  

-   Como tiene pensado usar una versión de actualización (como la versión 1610) y no permanecer en una versión de línea base (como la versión 1606), no es necesario instalar sitios adicionales y luego actualizarlos. Esto también se aplica a los clientes.  
-   No instale sitios secundarios con la versión 1606 ni los actualice después a la versión 1610. En vez de eso, instale sitios secundarios después de que los sitios primarios ejecuten la versión 1610.  

Siga esta secuencia:  

1. **Instale un sitio de nivel superior para su nueva jerarquía** usando los medios de línea base.  

   -   Puede usar los medios de línea base únicamente para instalar el primer sitio de una nueva jerarquía.  
   -   Por ejemplo, instale un sitio de nivel superior con la versión de línea base de 1606. Para obtener más información, consulte [Use the Setup Wizard to install sites](use-the-setup-wizard-to-install-sites.md) (Usar el asistente para instalación para instalar sitios).  

   Después de este paso, el sitio de nivel superior ejecuta la versión 1606.  

2. **Use actualizaciones integradas en la consola para actualizar el sitio de nivel superior a una versión posterior.**  

   -   Antes de instalar los clientes o los sitios secundarios, actualice el sitio de nivel superior a la versión de actualización que tiene pensado usar.  
   -   Por ejemplo, puede actualizar el sitio de nivel superior que ejecuta la versión 1606 a la versión 1610. Para obtener más información, vea [Actualizaciones para Configuration Manager](../../../../core/servers/manage/updates.md).  

   Después de este paso, el sitio de nivel superior ejecuta la versión 1610.  

3. **Instale nuevos sitios primarios secundarios debajo de un sitio de administración central.**  

   - Utilice los medios de instalación de la carpeta CD.Latest en el servidor de sitio de administración central para instalar sitios primarios secundarios. Para más información, vea [La carpeta CD.Latest para Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

     Estos medios de origen son necesarios para garantizar que los nuevos sitios secundarios coinciden con la versión del sitio de administración central.  

   Después de este paso, los nuevos sitios primarios secundarios ejecutan la versión 1610.  

4. **En cada sitio primario, utilice la opción integrada en la consola para instalar nuevos sitios secundarios.**  

   -   Como no ha instalado sitios secundarios mientras los sitios primarios estaban en la versión 1606, no será necesario actualizar los sitios secundarios.  
   -   En su lugar, instale nuevos sitios secundarios que ejecuten la versión 1610. Para obtener más información, consulte [Install a secondary site](use-the-setup-wizard-to-install-sites.md#bkmk_secondary) (Instalar un sitio secundario) en el tema [Use the Setup Wizard to install sites](use-the-setup-wizard-to-install-sites.md) (Uso del asistente para instalación para instalar sitios).  

   Después de este paso, se instalan nuevos sitios secundarios que ejecutan la versión 1610.  

5. **Instale nuevos clientes en el sitio primario.**  

   -   Como no ha instalado clientes mientras los sitios primarios estaban en la versión 1606, no será necesario actualizar los clientes de la versión 1606 a la versión 1610.  
   -   En su lugar, instale nuevos clientes que ejecuten la versión 1610. Para más información, vea [Cómo implementar clientes](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

   Después de este paso, se instalan nuevos clientes que ejecutan la versión 1610.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-configuration-manager-current-branch"></a>Escenario: actualización de System Center 2012 Configuration Manager a una versión de actualización de la rama actual de Configuration Manager  

En este escenario de ejemplo, actualizará la infraestructura de System Center 2012 Configuration Manager a una versión de actualización de la rama actual de Configuration Manager, como la versión 1610.  

-   El sitio de administración central y todos los sitios primarios se deben actualizar a la versión de línea base 1606 antes de instalar la actualización de la versión 1610.  
-   Los clientes y los sitios secundarios no instalan ni actualizan la versión 1606. En su lugar, pasan directamente de System Center 2012 Configuration Manager a la versión 1610 de la rama actual de Configuration Manager.  

Siga esta secuencia:  

1. **Actualice el sitio de nivel superior de System Center 2012 Configuration Manager** a una versión de línea base de la rama actual usando los medios de origen de Configuration Manager (por ejemplo, la versión 1606). Para obtener más información, consulte [Actualizar a System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

   -   Al igual que los escenarios de actualización tradicionales, actualice siempre primero el sitio de nivel superior de la jerarquía y luego los sitios secundarios.  

   Después de este paso, el sitio de nivel superior ejecuta la versión 1606.  

2. **Actualice cada sitio primario secundario de la jerarquía** a esa misma versión de línea de base.  

   -   Si actualiza desde Microsoft System Center 2012 Configuration Manager, debe actualizar manualmente cada sitio primario a una versión de línea de base de la rama actual.  
   -   En este momento, no actualizará los sitios secundarios.  

   Después de este paso, cada sitio primario ejecuta la versión 1606.  

3. **Establezca las ventanas de mantenimiento en los sitios primarios secundarios.** Después de actualizar todos los sitios primarios a la versión de línea base, planee configurar ventanas de mantenimiento para controlar cuándo esos sitios instalarán actualizaciones de la infraestructura. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md) (Uso de ventanas de mantenimiento en Configuration Manager).  (Las ventanas de mantenimiento se denominan *ventanas de servicio* en la versión 1606).  

   -   Un sitio primario secundario instala automáticamente las mismas actualizaciones que se instalan en un sitio de administración central.  
   -   Los sitios secundarios no instalan automáticamente las nuevas versiones. Debe actualizarlas manualmente desde la consola.  

   Después de este paso, al instalar actualizaciones en el sitio de administración central, los sitios primarios secundarios solo instalarán esa actualización cuando así se lo permita la ventana de mantenimiento.  

4. **Instale la versión de actualización en el sitio de nivel superior.** De esta forma se actualiza el sitio de nivel superior. Después de que un sitio de administración central instale la versión de actualización, cada sitio primario secundario instala automáticamente la actualización a menos que una ventana de mantenimiento bloquee la instalación.  

   -   Por ejemplo, puede actualizar el sitio de nivel superior de la versión 1606 a la versión 1610. Para obtener más información, vea [Actualizaciones para Configuration Manager](../../../../core/servers/manage/updates.md).  

   Después de este paso, el sitio de administración central y todos los sitios primarios ejecutan la versión 1610.  

5. **Actualice los sitios secundarios.** Después de que un sitio primario instale la actualización y ejecute la versión 1610, use la opción integrada en la consola para actualizar los sitios secundarios.  

   -   De esta forma, se actualizan los sitios secundarios directamente desde Microsoft System Center 2012 Configuration Manager a la versión de actualización instalada en el sitio primario.  
   -   Para más información sobre cómo actualizar un sitio secundario, vea [Actualizar sitios](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) en el tema [Actualizar a Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

6. **Actualice los clientes.** Para actualizar los clientes, use la información que se describe en [Actualizar clientes de equipos Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

   -   De esta forma, se actualizan los clientes directamente desde Microsoft System Center 2012 Configuration Manager a la versión de actualización instalada en el sitio primario.  

   Después de este paso, los clientes se actualizan a la versión 1610 sin actualizarse primero a la versión 1606.
