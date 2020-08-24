---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 2ae953f6fb01f42c8140407c551ddeb3a9f39c70
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692693"
---
### <a name="server-connectivity-endpoints"></a>Puntos de conexión de conectividad del servidor

El punto de conexión del servicio debe comunicarse con los puntos de conexión siguientes:

| Punto de conexión  | Función  |
|-----------|-----------|
| `https://aka.ms` | Se usa para ubicar el servicio |
| `https://graph.windows.net` | Se usa para recuperar automáticamente la configuración como CommercialId al asociar la jerarquía a Análisis de escritorio (en el rol de servidor de Configuration Manager). Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Se usa para sincronizar las pertenencias de la recopilación de dispositivos, los planes de implementación y el estado de preparación del dispositivo con Análisis de escritorio (solo en el rol de servidor Configuration Manager). Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://dc.services.visualstudio.com` | Para obtener datos de diagnóstico del conector del servicio local a fin de extraer conclusiones sobre el estado de los servicios conectados a la nube.<!--7541816--> |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Puntos de conexión de experiencia del usuario y componente de diagnóstico

Los dispositivos cliente necesitan comunicarse con los puntos de conexión siguientes:

| Punto de conexión  | Función  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Punto de conexión de experiencia del usuario y componente de diagnóstico asociados. Lo usan los dispositivos que ejecutan la versión 1809 o posterior de Windows 10 o la versión 1803 con la actualización acumulativa 2018-09 o posterior instalada. |
| `https://v10.events.data.microsoft.com` | Punto de conexión de experiencia del usuario y componente de diagnóstico asociados. Lo usan los dispositivos que ejecutan la versión 1803 de Windows 10 _sin_ la actualización acumulativa 2018-09 instalada. |
| `https://v10.vortex-win.data.microsoft.com` | Punto de conexión de experiencia del usuario y componente de diagnóstico asociados. Lo usan los dispositivos que ejecutan la versión 1709 o anterior de Windows 10. |
| `https://vortex-win.data.microsoft.com` | Punto de conexión de experiencia del usuario y componente de diagnóstico asociados. Lo usan los dispositivos que ejecutan Windows 7 y Windows 8.1. |

### <a name="client-connectivity-endpoints"></a>Puntos de conexión de conectividad de cliente

Los dispositivos cliente necesitan comunicarse con los puntos de conexión siguientes:

| Índice | Punto de conexión  | Función  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Permite la actualización de compatibilidad para enviar datos a Microsoft. |
| 2 | `http://adl.windows.com` | Permite que la actualización de compatibilidad reciba los datos de compatibilidad más recientes de Microsoft. |
| 3 | `https://watson.telemetry.microsoft.com` | [Informe de errores de Windows (WER)](/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1803 o anterior de Windows 10. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Informe de errores de Windows (WER)](/windows/win32/wer/windows-error-reporting). Es necesario para los informes de estado de dispositivos de la versión 1809 o posterior de Windows 10. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Informe de errores de Windows (WER)](/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Informe de errores de Windows (WER)](/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Informe de errores de Windows (WER)](/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Informe de errores de Windows (WER)](/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Informe de errores de Windows (WER)](/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Informe de errores de Windows (WER)](/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Análisis de volcado de memoria de bloqueos (OCA)](/windows/win32/dxtecharts/crash-dump-analysis). Es necesario para los informes de estado de dispositivos de la versión 1809 o posterior de Windows 10. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Análisis de volcado de memoria de bloqueos (OCA)](/windows/win32/dxtecharts/crash-dump-analysis). Es necesario para supervisar el estado de implementación de la versión 1803 o anterior de Windows 10. |
| 13 | `https://login.live.com` | Es necesario para proporcionar una identidad de dispositivo más confiable para Análisis del escritorio. <br> <br>Para deshabilitar el acceso a la cuenta Microsoft del usuario final, use la configuración de directiva en lugar de bloquear este punto de conexión. Para más información, consulte [La cuenta de Microsoft en la empresa](/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Punto de conexión de experiencia del usuario y componente de diagnóstico asociados. |