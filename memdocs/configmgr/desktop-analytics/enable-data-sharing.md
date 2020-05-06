---
title: Habilitación del uso compartido de datos
titleSuffix: Configuration Manager
description: Guía de referencia para compartir datos de diagnóstico con Análisis de escritorio.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7610b0e60f3ea02918c9dd98858a3b2bfd7c712
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708203"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Habilitación del uso compartido de datos en Análisis de escritorio

Para inscribir dispositivos en Análisis de escritorio, deben enviar datos de diagnóstico a Microsoft. Si su entorno usa un servidor proxy, utilice esta información para configurar el proxy.

## <a name="diagnostic-data-levels"></a>Niveles de datos de diagnóstico

![Diagrama de niveles de datos de diagnóstico de Análisis de escritorio](media/diagnostic-data-levels.png)

Al integrar Configuration Manager con Análisis de escritorio, también lo usa para administrar el nivel de datos de diagnóstico en los dispositivos. Para obtener la mejor experiencia, use Configuration Manager.

> [!Important]  
> En la mayoría de los casos, use solo Configuration Manager para definir estos valores. No aplique también esta configuración en los objetos de directiva de grupo de dominio. Para más información, consulte [Resolución de conflictos](enroll-devices.md#conflict-resolution).

La funcionalidad básica de Análisis de escritorio funciona en el [nivel de datos de diagnóstico](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels) **Básico**. Si no configura el nivel **Mejorado (limitado)** en Configuration Manager, no obtendrá las siguientes características de Análisis de escritorio:

- Uso de la aplicación
- [Información adicional de la aplicación](compat-assessment.md#additional-insights)
- Código de estado de implementación
- Datos de supervisión de estado

Microsoft recomienda habilitar el nivel de datos de diagnóstico **Mejorado (limitado)** con Análisis de escritorio para maximizar las ventajas que obtiene de él.

> [!Tip]
> El valor **Mejorado (limitado)** de Configuration Manager es el mismo valor que la directiva **Limitar los datos de diagnóstico mejorado al mínimo que necesita Windows Analytics.** disponible en los dispositivos que ejecutan la versión 1709 y posterior de Windows 10.
>
> Los dispositivos que ejecutan la versión 1703 y anterior de Windows 10, Windows 8.1 o Windows 7 no tienen esta configuración de directiva. Al configurar el valor **Mejorado (limitado)** de Configuration Manager, estos dispositivos retroceden al nivel **Básico**.
>
> Los dispositivos que ejecutan la versión 1709 de Windows 10 tienen esta configuración de directiva. Sin embargo, cuando se configura el valor **Mejorado (limitado)** de Configuration Manager, estos dispositivos también retroceden al nivel **Básico**.

Para más información sobre los datos de diagnóstico que se comparten con Microsoft con el nivel de datos de diagnóstico **Mejorado (limitado)** , consulte [Eventos y campos de datos de diagnóstico de nivel mejorado de Windows 10](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!Important]
> Microsoft está firmemente comprometido a proporcionar las herramientas y los recursos que le sitúan al mando de su privacidad. Como resultado, aunque Análisis de escritorio admite dispositivos Windows 8.1, Microsoft no recopila datos de diagnóstico de Windows de dispositivos Windows 8.1 ubicados en países europeos (EEE y Suiza).

Para más información, consulte [Privacidad de Análisis de escritorio](privacy.md).

Los artículos siguientes son también buenos recursos para comprender mejor los niveles de datos de diagnóstico de Windows:

- [Windows 10 y GDPR: información para administradores de TI y toma de decisiones](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Los clientes configurados para limitar los datos de diagnóstico mejorados enviarán aproximadamente 2 MB de datos a la nube de Microsoft en el examen completo inicial. La diferencia diaria varía entre 250 y 400 KB al día.
>
> El examen de diferencias diarias se produce a las 3:00 a. m. (hora local del dispositivo). Algunos eventos se envían en la primera hora disponible a lo largo del día. Estas horas no se pueden configurar.
>
> Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Puntos de conexión

Para habilitar el uso compartido de datos, configure el servidor proxy para permitir los siguientes puntos de conexión de Internet.

> [!Important]  
> De cara a la privacidad y la integridad de los datos, Windows comprueba si hay un certificado SSL de Microsoft (asignación de certificados) al comunicarse con los puntos de conexión de datos de diagnóstico. No es posible la interceptación y la inspección de SSL. Para usar Análisis de escritorio, excluya estos puntos de conexión de la inspección de SSL.<!-- BUG 4647542 -->

A partir de la versión 2002, si el sitio de Configuration Manager no se puede conectar a los puntos de conexión necesarios para un servicio en la nube, genera un mensaje de estado crítico con el identificador 11488. Si no se puede conectar al servicio, el estado del componente SMS_SERVICE_CONNECTOR cambia a crítico. Consulte el estado detallado en el nodo [Estado del componente](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) de la consola de Configuration Manager.<!-- 5566763 -->

### <a name="server-connectivity-endpoints"></a>Puntos de conexión de conectividad del servidor

El punto de conexión del servicio debe comunicarse con los puntos de conexión siguientes:

| Punto de conexión  | Función  |
|-----------|-----------|
| `https://aka.ms` | Se usa para ubicar el servicio |
| `https://graph.windows.net` | Se usa para recuperar automáticamente la configuración como CommercialId al asociar la jerarquía a Análisis de escritorio (en el rol de servidor de Configuration Manager). Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Se usa para sincronizar las pertenencias de la recopilación de dispositivos, los planes de implementación y el estado de preparación del dispositivo con Análisis de escritorio (solo en el rol de servidor Configuration Manager). Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

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
| 3 | `https://watson.telemetry.microsoft.com` | [Informe de errores de Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1803 o anterior de Windows 10. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Informe de errores de Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Es necesario para los informes de estado de dispositivos de la versión 1809 o posterior de Windows 10. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Informe de errores de Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Informe de errores de Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Informe de errores de Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Informe de errores de Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Informe de errores de Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Informe de errores de Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Es necesario para supervisar el estado de implementación de la versión 1809 o posterior de Windows 10. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Análisis de volcado de memoria de bloqueos (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Es necesario para los informes de estado de dispositivos de la versión 1809 o posterior de Windows 10. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Análisis de volcado de memoria de bloqueos (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Es necesario para supervisar el estado de implementación de la versión 1803 o anterior de Windows 10. |
| 13 | `https://login.live.com` | Es necesario para proporcionar una identidad de dispositivo más confiable para Análisis del escritorio. <br> <br>Para deshabilitar el acceso a la cuenta Microsoft del usuario final, use la configuración de directiva en lugar de bloquear este punto de conexión. Para más información, consulte [La cuenta de Microsoft en la empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Punto de conexión de experiencia del usuario y componente de diagnóstico asociados. |

## <a name="proxy-server-authentication"></a>Autenticación del servidor proxy

Si su organización usa la autenticación de servidor proxy para el acceso a Internet, asegúrese de que no bloquee los datos de diagnóstico debido a la autenticación. Si el proxy no permite que los dispositivos envíen estos datos, no se mostrarán en Análisis de escritorio.

### <a name="bypass-recommended"></a>Desviar (recomendado)

Configure los servidores proxy para que no exijan la autenticación proxy del tráfico que entra en los puntos de conexión de datos de diagnóstico. Esta opción es la solución más completa. Funciona en todas las versiones de Windows 10.  

### <a name="user-proxy-authentication"></a>Autenticación proxy del usuario

Configure los dispositivos para que usen el contexto del usuario con sesión iniciada para la autenticación proxy. Este método requiere las siguientes configuraciones:

- Los dispositivos tienen la actualización de calidad actual para una versión compatible de Windows.

- Configure el proxy de nivel de usuario (proxy de WinINET) en **Configuración de proxy** en el grupo Red e Internet de la configuración de Windows. También puede usar el panel de control heredado de Opciones de Internet.

- Asegúrese de que los usuarios tengan permiso de proxy para comunicarse con los puntos de conexión de datos de diagnóstico. Esta opción requiere que los dispositivos tengan usuarios de consola con permisos de proxy, de forma que no puede usar este método con dispositivos sin periféricos.

> [!IMPORTANT]
> El enfoque de autenticación proxy del usuario no es compatible con el uso de Azure Advanced Threat Protection de Microsoft Defender. Este comportamiento se debe a que esta autenticación se basa en la clave del Registro **DisableEnterpriseAuthProxy** establecida en `0`, mientras que ATP de Microsoft Defender requiere que se establezca en `1`. Para obtener más información, consulte [Configurar el proxy del equipo y la configuración de conectividad de Internet en ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### <a name="device-proxy-authentication"></a>Autenticación proxy del dispositivo

Este enfoque admite los escenarios siguientes:

- Dispositivos sin periféricos, donde ningún usuario inicia sesión o los usuarios del dispositivo no tienen acceso a Internet

- Servidores proxy autenticados que no usan la Autenticación integrada de Windows

- Uso conjunto con Protección contra amenazas avanzada de Microsoft Defender

Este enfoque es el más complejo porque requiere las siguientes configuraciones:

- Asegúrese de que los dispositivos puedan comunicarse con al servidor proxy a través de WinHTTP en el contexto del sistema local. Use una de las siguientes opciones para configurar este comportamiento:

  - Línea de comandos `netsh winhttp set proxy`

  - Protocolo de detección automática de proxy web (WPAD)

  - Proxy transparente

  - Configure el proxy WinINET para todo el dispositivo mediante la siguiente configuración de directiva de grupo: **Configuración de proxy por equipo y no por usuario** (ProxySettingsPerUser = `1`)

  - Conexión enrutada o que use la traducción de direcciones de red (NAT)

- Configure los servidores proxy para permitir que las cuentas de equipo de Active Directory tengan acceso a los puntos de conexión de datos de diagnóstico. Esta configuración requiere que los servidores proxy admitan la autenticación integrada de Windows.  
