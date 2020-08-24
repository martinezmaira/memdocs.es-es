---
title: Compatibilidad con la virtualización
titleSuffix: Configuration Manager
description: Los requisitos para instalar los roles de sistema de sitio y el cliente de Configuration Manager en un entorno de virtualización.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d2977fc34e9c398e9e266cbc9b223ea74a1dd18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700238"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Compatibilidad con entornos de virtualización con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Configuration Manager admite la instalación de los roles de sistema de sitio y de cliente en sistemas operativos compatibles que se ejecutan como una máquina virtual (VM) en determinados entornos de virtualización. Esta compatibilidad existe incluso cuando el host virtual (entorno de virtualización) no se admita como cliente o servidor de sitio.

Por ejemplo, puede usar Microsoft Hyper-V Server 2016 para hospedar una máquina virtual que ejecuta Windows Server 2019. Puede instalar los roles de cliente y de sistema de sitio en la máquina virtual que ejecuta Windows Server 2019. El cliente no se puede instalar en el host que ejecuta Microsoft Hyper-V Server 2016.

## <a name="virtualization-environments"></a>Entornos de virtualización

- Windows Server 2019  
- Windows Server 2016 <sup>[Note 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Note 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager no admite la [virtualización anidada](/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), que es nueva en Windows Server 2016.

### <a name="virtualization-environment-support"></a>Compatibilidad del entorno de virtualización

Cada equipo virtual tiene los mismos o mayores requisitos de hardware y software que se usarían para un equipo de Configuration Manager físico.

Para validar que Configuration Manager admita el entorno de virtualización, use el Programa de validación de virtualización del servidor. Incluye un Asistente para directivas de compatibilidad del programa de virtualización en línea. Para más información, consulte [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx) (Programa de validación de virtualización del servidor de Windows).

Configuration Manager no puede administrar máquinas virtuales sin conexión. El cliente de Configuration Manager del equipo host no puede administrar una imagen de máquina virtual sin conexión. Por ejemplo, no puede instalar actualizaciones de software ni recopilar inventario de hardware.

En general, Configuration Manager no otorga ninguna consideración especial a las máquinas virtuales. Por ejemplo, si detiene una máquina virtual y no guarda su estado, es posible que Configuration Manager no determine si se tiene que volver a instalar una actualización de software.

Para contribuir al rendimiento del cliente de Configuration Manager en entornos virtuales que admiten varias sesiones de usuario, se deshabilita la directiva de usuario de forma predeterminada. A partir de la versión 1910, puede habilitar la directiva de usuario en este escenario. Para más información, consulte [Acerca de la configuración de cliente: Habilitar la directiva de usuario para varias sesiones de usuario](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions).

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a> Máquinas virtuales de Microsoft Azure

Configuration Manager puede ejecutarse en máquinas virtuales de Azure y localmente dentro del centro de datos. Use Configuration Manager con máquinas virtuales de Azure en los escenarios siguientes:

- **Escenario 1**: Ejecutar Configuration Manager en una máquina virtual de Azure. Úselo para administrar clientes en otras máquinas virtuales de Azure.

- **Escenario 2**: Ejecutar Configuration Manager en una máquina virtual de Azure. Úselo para administrar clientes que no se ejecuten en Azure.

- **Escenario 3**: Ejecutar distintos roles de sistema de sitio de Configuration Manager en máquinas virtuales de Azure. Ejecute otros roles en el centro de datos local que está conectado correctamente a Azure.

Los mismos requisitos de Configuration Manager para redes, configuraciones admitidas y requisitos de hardware también se aplican a las máquinas virtuales de Azure.

Para más información, consulte [Configuration Manager en Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]
> Los sitios y clientes de Configuration Manager que se ejecutan en máquinas virtuales de Azure están sujetos a los mismos requisitos de licencia que las instalaciones locales.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Windows Virtual Desktop](/azure/virtual-desktop/) es un servicio de virtualización de escritorio y aplicaciones que se ejecuta en Microsoft Azure. A partir de la versión 1906, use Configuration Manager para administrar estos dispositivos virtuales que ejecutan Windows en Azure. Para más información, vea [Sistemas operativos compatibles con clientes y dispositivos](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="next-steps"></a>Pasos siguientes

[Administración de clientes de Configuration Manager en una infraestructura de escritorio virtual (VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)