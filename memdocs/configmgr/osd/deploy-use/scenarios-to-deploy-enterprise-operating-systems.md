---
title: Escenarios para implementar sistemas operativos de empresa
titleSuffix: Configuration Manager
description: Obtenga información sobre distintos escenarios para implementar sistemas operativos de empresa con Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07e8623928cbfe0bcd562d3d6efdf3a9ceee85ae
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708393"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Escenarios para implementar sistemas operativos de empresa con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Los siguientes escenarios de implementación de sistema operativo están disponibles en Configuration Manager:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Actualizar Windows a la versión más reciente
Este escenario actualiza el sistema operativo en equipos que ejecutan actualmente Windows 7, Windows 8.1 o Windows 10. El proceso de actualización conserva las aplicaciones, la configuración y los datos de usuario en el equipo. No hay dependencias externas, como Windows ADK. Este proceso puede ser más rápido y resistente que las implementaciones de SO tradicionales.  

Para más información, consulte [Actualizar Windows a la versión más reciente](upgrade-windows-to-the-latest-version.md).


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot para dispositivos existentes
<!--3607717, fka 1358333-->
A partir de la versión 1810, Windows Autopilot para dispositivos existentes está disponible con Windows 10, versión 1809 o posteriores. Esta característica permite crear una imagen y aprovisionar un dispositivo de Windows 7 para el modo controlado por el usuario de Windows Autopilot mediante una única secuencia de tareas de Configuration Manager.

Para obtener más información, consulte [Windows Autopilot para dispositivos existentes](windows-autopilot-for-existing-devices.md).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Actualizar un equipo existente con una nueva versión de Windows
Este escenario realiza la partición y formatea (borra) un equipo existente, e instala un sistema operativo nuevo en el equipo. Puede migrar la configuración y los datos de usuario después de instalar el sistema operativo.  

Para obtener más información, consulte [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)
Este escenario instala un sistema operativo en un equipo nuevo. Se trata de una instalación nueva del sistema operativo y no incluye los valores de configuración ni la migración de datos de usuario.  

Para obtener más información, consulte [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Reemplazar un equipo existente y transferir la configuración
Este escenario instala un sistema operativo en un equipo nuevo. Opcionalmente, puede migrar la configuración y los datos de usuario del equipo antiguo al nuevo.  

Para obtener más información, consulte [Reemplazar un equipo existente y transferir la configuración](replace-an-existing-computer-and-transfer-settings.md).


