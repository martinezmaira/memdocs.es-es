---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: ff48e8117437e45be42551ebffff7cdcf5bce184
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820311"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
Los siguientes perfiles se admiten en los dispositivos que se administran con la versión 2006 o posteriores de la rama actual de Configuration Manager, mediante el escenario de asociación de inquilinos:
<!--The following profiles are supported for devices you manage with Configuration Manager Technical Preview 2007 or later, through the tenant attach scenario:-->

- Plataforma: **Windows 10 y Windows Server**

  - Perfil: **Directiva de Antivirus de Microsoft Defender (ConfigMgr)**
  
    Administre la [configuración de la directiva de antivirus para dispositivos de Configuration Manager](../../protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md), cuando se use la asociación de inquilinos.

    Este perfil es compatible con dispositivos que están asociados a un inquilino y se ejecuta en las siguientes plataformas:
    - Windows 10 y versiones posteriores (x86, x64, ARM64)
    - Windows 8.1 (x84, x64)
    - Windows Server 2019 y versiones posteriores (x64)
    - Windows Server 2016 (x64)
    - Windows Server 2012 R2 (x64)
    - Windows Server 2008 R2 SP1 (x64)
