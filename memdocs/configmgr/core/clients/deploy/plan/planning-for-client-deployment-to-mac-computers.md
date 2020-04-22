---
title: Planeamiento de la implementación del cliente en equipos Mac
titleSuffix: Configuration Manager
description: Planee la implementación de cliente en equipos Mac en Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693723"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Planeación de la implementación de clientes en equipos Mac en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Puede instalar el cliente de Configuration Manager en equipos Mac que ejecuten el sistema operativo Mac OS X y usen las siguientes capacidades de administración:  

- **Inventario de hardware**  

   Es posible usar el inventario de hardware de Configuration Manager para recopilar información sobre el hardware y las aplicaciones instaladas en los equipos Mac. Entonces, esta información puede verse en el explorador de recursos de la consola de Configuration Manager y usarse para crear recopilaciones, consultas e informes. Para obtener más información, vea [Cómo usar el Explorador de recursos para ver el inventario de hardware](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Configuration Manager recopila la siguiente información de hardware de los equipos Mac:  

  -   Procesador  

  -   Sistema de equipo  

  -   Unidad de disco  

  -   Partición de disco  

  -   Adaptador de red  

  -   Sistema operativo  

  -   Servicio  

  -   Proceso  

  -   Software instalado  

  -   Producto de sistema del equipo  

  -   Controladora USB  

  -   Dispositivo USB  

  -   Unidad de CD-ROM  

  -   Controladora de vídeo  

  -   Monitor de escritorio  

  -   Batería portátil  

  -   Memoria física  

  -   Impresora  

  > [!IMPORTANT]  
  >  No se puede extender la información del hardware que se recopila de equipos Mac durante el inventario de hardware.  

- **Configuración de cumplimiento**  

   Puede usar la configuración de cumplimiento de Configuration Manager para ver la compatibilidad y corregir la configuración de preferencias (.plist) de Mac OS X. Por ejemplo, puede aplicar la configuración para la página principal en el explorador web Safari o asegurarse de que el firewall de Apple está habilitado. También puede utilizar scripts de shell para supervisar y corregir la configuración en MAC OS X.  

- **Administración de aplicaciones**  

   Configuration Manager puede implementar software en equipos Mac. Es posible implementar los siguientes formatos de software en equipos Mac:  

  -   Imagen de disco Apple (.DMG)  

  -   Archivo de paquete Meta (.MPKG)  

  -   Paquete de instalador de Mac OS X (.PKG)  

  -   Aplicación de Mac OSX (.APP)  

  Al instalar el cliente de Configuration Manager en equipos Mac, no se pueden usar las siguientes capacidades de administración admitidas por el cliente de Configuration Manager en equipos basados en Windows:  

- Instalación de inserción de cliente  

- Implementación de sistema operativo  

- Actualizaciones de software  

  > [!NOTE]  
  >  Puede usar la administración de aplicaciones de Configuration Manager para implementar las actualizaciones de software de Mac OS X necesarias en equipos Mac. Además, puede utilizar la configuración de compatibilidad para asegurarse de que los equipos tengan las actualizaciones de software necesarias.  

- Ventanas de mantenimiento  

- Control remoto  

- Administración de energía  

- Comprobación y corrección de cliente del estado de cliente  

  Para más información sobre cómo instalar y configurar el cliente Mac de Configuration Manager, vea [Cómo implementar clientes en equipos Mac](../../../../core/clients/deploy/deploy-clients-to-macs.md).
