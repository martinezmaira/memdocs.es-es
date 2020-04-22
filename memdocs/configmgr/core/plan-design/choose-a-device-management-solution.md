---
title: Elegir una solución de administración de dispositivos
titleSuffix: Configuration Manager
description: Obtenga información sobre las soluciones que ofrece Microsoft para administrar equipos, servidores y dispositivos.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d36e29f0f915c0f2a35070c667525853e5981564
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702273"
---
# <a name="choose-a-device-management-solution"></a>Elegir una solución de administración de dispositivos

Microsoft ofrece diferentes soluciones para la administración de equipos, servidores y dispositivos. Estas soluciones están disponibles en el entorno local o en la nube, o en ambas ubicaciones. Elija la solución más adecuada para los requisitos empresariales de la organización. en función de su decisión sobre las plataformas de dispositivos que necesita administrar y la funcionalidad de administración que necesita.

## <a name="overview"></a>Introducción

Hay varias soluciones de Microsoft que funcionan mejor para usted en diferentes escenarios. No es necesario que elija solo uno.

- Si se trata de una organización pequeña, una herramienta como Windows Admin Center puede ser una gran elección.
- Aproximadamente, el 75 % de las organizaciones de TI usan Configuration Manager para administrar sus dispositivos.
- Microsoft Azure ofrece varias soluciones de la nube o locales con Azure Stack destinadas principalmente a la administración de servidores.
- Microsoft Intune proporciona la administración de clientes en la nube.
- Puede combinar Configuration Manager y Intune con la administración conjunta.

Use la siguiente tabla para ayudar a comparar estas tecnologías de administración:

|  | Solo nube | Conectado a la nube | Local | Desconectada |
|---------|---------|---------|---------|---------|
| **Host de Hyper-V** | No disponible | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager |
| **Windows Server** | - Administración de Azure<br/> - Configuration Manager | - Administración de Azure<br/> - Configuration Manager | - Administración de Azure<br/> - Configuration Manager | Configuration Manager |
| **Servidor Linux** | Administración de Azure | Administración de Azure | Administración de Azure |  |
| **Windows 10** | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | Configuration Manager |
| **Windows 7 o 8.1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows Virtual Desktop** | Configuration Manager | No disponible | No disponible | No disponible |

Vea los siguientes artículos para más información:

- [¿Qué es Azure Stack?](https://docs.microsoft.com/azure-stack/operator/azure-stack-overview)
- [¿Qué es Windows Admin Center?](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/what-is)
- [¿Qué es Virtual Machine Manager?](https://docs.microsoft.com/system-center/vmm/overview)
- [Productos de administración de Azure](https://docs.microsoft.com/azure/)
- [¿Qué es Windows Virtual Desktop?](https://docs.microsoft.com/azure/virtual-desktop/overview)

Para más información sobre las soluciones Configuration Manager y Intune, continúe con la siguiente sección.

## <a name="client-management"></a>Administración de cliente

En esta sección se comparan las cuatro soluciones de administración de clientes siguientes:

- [Cliente de Configuration Manager](#bkmk_sccm)
- [Administración de dispositivos móviles (MDM) local con Configuration Manager](#bkmk_opmdm)
- [Administración conjunta con Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

Puede usar estas soluciones de forma independiente o en combinación con otras. Por ejemplo, use el enfoque de administración basada en cliente para administrar los equipos y los servidores de la organización y, además, use la administración conjunta para administrar equipos portátiles basados en Internet. Al combinar los enfoques de esta manera, puede cubrir todas las necesidades de administración del dispositivo.  

También hay dos tablas que comparan las soluciones de administración por los siguientes factores:

- [Comparación por plataformas admitidas](#bkmk_comp1)
- [Comparación por funcionalidad de administración](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> Cliente de Configuration Manager  

Esta opción requiere la instalación del cliente de Configuration Manager en dispositivos. Proporciona la mayoría de las características para administrar equipos, servidores y otros dispositivos del entorno.

Para obtener más información, vea [Métodos de instalación de cliente en System Center Configuration Manager](../clients/deploy/plan/client-installation-methods.md).  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> MDM local  

Esta opción usa las funcionalidades de administración de dispositivos integradas en Windows 10. Aunque no incluye tantas características como la administración basada en cliente, MDM local proporciona un enfoque más ligero para la administración. Usa recursos locales de Configuration Manager para administrar dispositivos.  

Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a> Administración conjunta con Microsoft Intune

La administración conjunta es una de las principales formas de asociar la implementación existente de Configuration Manager a la nube de Microsoft 365. Le permite administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune. La administración conjunta le permite asociar a la nube su inversión existente en Configuration Manager mediante la incorporación de nuevas funcionalidades.

Para más información, vea [What is co-management?](../../comanage/overview.md) (¿Qué es la administración conjunta?).  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Microsoft Exchange  

Esta opción usa el conector de Exchange Server para conectar varios servidores de Exchange con Configuration Manager. Centraliza la administración de los dispositivos que pueden conectarse a Exchange ActiveSync. Puede configurar características de administración de dispositivos móviles de Exchange desde la consola de Configuration Manager. Entre las características de ejemplo se incluyen el borrado remoto de dispositivos y el control de configuración para varios servidores de Exchange.

Para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> Comparación de soluciones por plataformas admitidas  

|Plataforma|Cliente de Configuration Manager|MDM local|Configuration Manager con Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Sí| Sí |
|iOS| | |Sí| Sí |
|Mac OS X|Sí| |Sí| Sí |
|Windows 10|Sí|Sí|Sí| Sí |
|Windows 10 Móvil| |Sí|Sí| Sí |
|Windows (versiones anteriores)|Sí| |Sí|  |
|Windows Server|Sí| |Sí|  |
|Windows Embedded|Sí| | |  |

Para obtener una lista completa de plataformas compatibles, vea los siguientes artículos:

- [Sistemas operativos compatibles con dispositivos y clientes de Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)
- [Configuraciones compatibles con Intune](https://docs.microsoft.com/intune/supported-devices-browsers)

Microsoft recomienda usar Intune para administrar dispositivos móviles Android, iOS y Windows 10. Para más información, vea [¿Qué es Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a> Comparación de soluciones por funcionalidad de administración  

|Funcionalidad de administración|Cliente de Configuration Manager|MDM local|Configuration Manager con Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Autenticación mutua basada en certificados|Sí|Sí| |
|Instalación de cliente|Sí| | |
|Soporte técnico a través de Internet|Sí| | |
|Detección|Sí| |Sí|
|Inventario de hardware|Sí|Sí|Sí|
|Inventario de software|Sí| |Sí|
|Configuración|Sí|Sí|Sí|
|Implementación de software|Sí|Sí| |
|Administración de actualizaciones de software|Sí| | |
|Implementación del sistema operativo|Sí| | |
|Bloqueo desde Configuration Manager|Sí|Sí| |
|Cuarentena y bloqueo desde Exchange Server (y Configuration Manager)| | |Sí|
|Borrado remoto| |Sí|Sí|
