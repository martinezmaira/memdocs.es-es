---
title: Compatibilidad con Windows 10
titleSuffix: Configuration Manager
description: Obtención de información sobre las versiones de Windows 10 que se admiten como clientes o para OSD con Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7241db0220bf4adf9b55341514afb03de33c2589
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688603"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Compatibilidad con Windows 10 en Configuration Manager  

*Se aplica a: Configuration Manager (rama actual)*

Obtenga información sobre las versiones de Windows 10 que admite Configuration Manager, incluidas:

- [Windows 10 como cliente de Configuration Manager](#windows-10-as-a-client)
- [Windows Assessment and Deployment Kit (ADK) para Windows 10](#windows-10-adk)

> [!Tip]
> Las compilaciones de Windows Server como cliente se admiten del mismo modo que la versión de Windows 10 asociada. Por ejemplo, Windows Server 2016 es la misma versión de compilación que Windows 10 LTSB 2016 y Windows Server versión 1803 es la misma versión de compilación que Windows 10 versión 1803.
>
> Para más información sobre Windows Server como sistema de sitios, vea [Sistemas operativos compatibles con servidores de sistema de sitio de Configuration Manager](supported-operating-systems-for-site-system-servers.md#bkmk_core).

## <a name="windows-10-as-a-client"></a>Windows 10 como cliente

Configuration Manager intenta proporcionar compatibilidad como cliente para cada versión nueva de Windows 10 tan pronto como es posible después de que se encuentre disponible. Como los productos tienen programaciones independientes de lanzamiento y desarrollo, la compatibilidad que Configuration Manager proporciona depende de cuándo se encuentra disponible cada una.

Una versión de Configuration Manager se quitará de la matriz después de que finalice la [compatibilidad con esa versión](../../servers/manage/current-branch-versions-supported.md). De forma similar, la compatibilidad con versiones de Windows 10 como Enterprise 2015 LTSB o 1511 se quitará de la matriz cuando se eliminen del soporte técnico.

- La última versión de la rama actual de Configuration Manager recibe las actualizaciones críticas y de seguridad, que pueden incluir correcciones para problemas con versiones de Windows 10. Cuando Microsoft publica una nueva versión de la rama actual de Configuration Manager, las versiones anteriores solo reciben actualizaciones de seguridad. Para más información, vea [Compatibilidad con versiones de la rama actual de System Center Configuration Manager](../../servers/manage/current-branch-versions-supported.md).  

    > [!Note]  
    > La mejor manera de tener Windows 10 actualizado es estar al día con Configuration Manager. Para saber más, vea [Configuration Manager y Windows como servicio](../../understand/configuration-manager-and-windows-as-service.md).  

- Esta información complementa a [Sistemas operativos compatibles con dispositivos y clientes](supported-operating-systems-for-clients-and-devices.md).  

- Si usa la rama de mantenimiento a largo plazo de Configuration Manager, vea [Configuraciones admitidas para la rama de mantenimiento a largo plazo](../../understand/supported-configurations-for-ltsb.md).  

En la tabla siguiente se enumeran las versiones de Windows 10 que puede usar como cliente con diferentes versiones de Configuration Manager.

| Versión de Windows 10 | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Enterprise 2015 LTSB** <!--10/14/2025-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| **Enterprise 2016 LTSB** <!--10/13/2026-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| **Enterprise LTSC 2019** <!--01/09/2029-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--04/14/2020-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![No compatible](media/Red_X.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/11/2021-->   | ![No compatible](media/Red_X.png) | ![No compatible](media/Red_X.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Para más información sobre el ciclo de vida de Windows, vea [Hoja de datos del ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

| Key |
|--|
| ![Compatible](media/green_check.png) = **Compatible**  |
| ![No compatible](media/Red_X.png) = **Not supported** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a> Notas sobre la compatibilidad con clientes de Windows 10

- En la compatibilidad para las versiones del Canal semianual de Windows 10, se incluyen las ediciones siguientes: Enterprise, Pro, Education y Pro Education.  

- A partir de la versión 1906, Configuration Manager admite Windows 10 Pro for Workstation.

- En la versión 1909 de Windows 10, el medio de implementación del sistema operativo muestra la versión como 10.0.18362.418.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a> Windows 10 en ARM64

Configuration Manager es compatible con el cliente en dispositivos ARM64 de Windows 10. No se admite la implementación del SO.<!-- 1353704 -->

A partir de la versión 2002,<!--5954175--> la plataforma **Todo Windows 10 (ARM64)** está disponible en la lista de versiones de sistema operativo admitidas en objetos con reglas de requisitos o listas de aplicabilidad.

> [!NOTE]
> Si previamente ha seleccionado la plataforma de nivel superior **Windows 10**, esta acción ha seleccionado automáticamente **Todo Windows 10 (64 bits)** y **Todo Windows 10 (32 bits)** . Esta nueva plataforma no se selecciona automáticamente. Si quiere agregar **Todo Windows 10 (ARM64)** , selecciónelo manualmente en la lista.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a> Compatibilidad con Windows Insider

A partir de la versión 1906 de Configuration Manager, puede [actualizar y mantener las compilaciones de Windows Insider](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB). Esta capacidad se proporciona para comodidad de los clientes. Aunque esta funcionalidad debería funcionar, la compatibilidad con ella es la mejor opción. Es posible que Configuration Manager no emita una revisión para esta funcionalidad si deja de funcionar.  

Para proporcionar comentarios sobre Windows Insider, use el [concentrador de comentarios](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback).

## <a name="windows-10-adk"></a>Windows 10 ADK

Cuando se implementan sistemas operativos con Configuration Manager, Windows ADK es una dependencia externa necesaria. Vea los siguientes artículos para más información:

- [Requisitos de infraestructura para la implementación del sistema operativo](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Descargar Windows ADK para Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > A partir de Windows 10 versión 1809, Windows PE es un instalador independiente. Aparte de esto, no hay ninguna diferencia funcional.
    >
    > Asegúrese de descargar **Windows ADK para Windows 10** y el **complemento de Windows PE para el ADK**.

En la tabla siguiente se enumeran las versiones de Windows 10 ADK que puede usar con diferentes versiones de Configuration Manager.

| Versión del ADK de Windows 10  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![No compatible](media/Red_X.png)   | ![No compatible](media/Red_X.png) | ![No compatible](media/Red_X.png) | ![No compatible](media/Red_X.png) | ![No compatible](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Compatible con versiones anteriores](media/blue_compat.png) | ![Compatible con versiones anteriores](media/blue_compat.png) | ![No compatible](media/Red_X.png) | ![No compatible](media/Red_X.png) | ![No compatible](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible con versiones anteriores](media/blue_compat.png) | ![Compatible con versiones anteriores](media/blue_compat.png) | ![No compatible](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![No compatible](media/Red_X.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) | ![Compatible.](media/green_check.png) |

|Key|
|--|
| ![Compatible](media/green_check.png) = **Compatible** <br/> En esta tabla solo se muestra la compatibilidad con Windows ADK en relación con la versión de Configuration Manager. Microsoft recomienda el uso de la versión de Windows ADK que coincida con la de Windows que va a implementar. Al implementar la versión más reciente de Windows 10, use la versión más reciente de Windows ADK. La versión más reciente de Windows ADK puede admitir la implementación de versiones anteriores del sistema operativo, como Windows 8.1.<!-- SCCMDocs issue 1229 --> Para obtener más información sobre la compatibilidad del componente Windows ADK, consulte [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) (Plataformas compatibles con DISM) y [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1) (Requisitos de USMT). |
| ![Compatible con versiones anteriores](media/blue_compat.png)  = **Compatible con versiones anteriores** <br/> Esta combinación no se ha probado pero debería funcionar. Informaremos de cualquier problema conocido o advertencia. |
| ![No compatible](media/Red_X.png) = **Not supported** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a> Notas sobre la compatibilidad de Windows 10 ADK

- Configuration Manager solo admite componentes x86 y amd64 de Windows 10 ADK. Actualmente no admite componentes ARM o ARM64.

- Las compilaciones de Windows Server tienen el mismo requisito de Windows ADK que la versión de Windows 10 asociada. Por ejemplo, Windows Server 2016 es la misma versión de compilación que Windows 10 LTSB 2016.
