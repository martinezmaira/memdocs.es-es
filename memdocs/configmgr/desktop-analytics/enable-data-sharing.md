---
title: Habilitación del uso compartido de datos
titleSuffix: Configuration Manager
description: Guía de referencia para compartir datos de diagnóstico con Análisis de escritorio.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 999d8441e8c97f0a4b7ad4a92c8175300dcc4ead
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696453"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Habilitación del uso compartido de datos en Análisis de escritorio

Para inscribir dispositivos en Análisis de escritorio, deben enviar datos de diagnóstico a Microsoft. Si su entorno usa un servidor proxy, utilice esta información para configurar el proxy.

## <a name="diagnostic-data-levels"></a>Niveles de datos de diagnóstico

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="Diagrama de niveles de datos de diagnóstico de Análisis de escritorio":::

Al integrar Configuration Manager con Análisis de escritorio, también lo usa para administrar el nivel de datos de diagnóstico en los dispositivos. Para obtener la mejor experiencia, use Configuration Manager.

> [!IMPORTANT]
> En la mayoría de los casos, use solo Configuration Manager para definir estos valores. No aplique también esta configuración en los objetos de directiva de grupo de dominio. Para más información, consulte [Resolución de conflictos](enroll-devices.md#conflict-resolution).

La funcionalidad básica de Análisis de escritorio funciona en el [nivel de datos de diagnóstico](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels) **Requerido**. Si no configura el nivel **Opcional (limitado)** en Configuration Manager, no obtendrá las siguientes características de Análisis de escritorio:

- Uso de la aplicación
- [Información adicional de la aplicación](compat-assessment.md#additional-insights)
- [Datos de estado de implementación](deploy-prod.md#address-deployment-alerts)
- [Datos de supervisión de estado](health-status-monitoring.md)

Microsoft recomienda habilitar el nivel de datos de diagnóstico **Opcional (limitado)** con Análisis de escritorio para maximizar las ventajas que se obtienen de esta funcionalidad.

> [!TIP]
> El valor **Opcional (limitado)** de Configuration Manager es el mismo valor que la directiva **Limitar los datos de diagnóstico mejorado a la cantidad mínima requerida por Windows Analytics** disponible en los dispositivos que ejecutan la versión 1709 y posterior de Windows 10.
>
> Los dispositivos que ejecutan la versión 1703 y anterior de Windows 10, Windows 8.1 o Windows 7 no tienen esta configuración de directiva. Al configurar el valor **Opcional (limitado)** de Configuration Manager, estos dispositivos retroceden al nivel **Requerido**.
>
> Los dispositivos que ejecutan la versión 1709 de Windows 10 tienen esta configuración de directiva. Sin embargo, cuando se configura el valor **Opcional (limitado)** de Configuration Manager, estos dispositivos también retroceden al nivel **Requerido**.
>
> En Configuration Manager, versión 2002 y anteriores, los valores tenían nombres diferentes:<!-- 7363467 -->
>
> | Versión 2006 y posteriores | Versión 2002 y anteriores |
> |---------|---------|
> | Obligatorio | Básico |
> | Opcional (limitado) | Mejorado (limitado) |
> | N/D | Mejorada |
> | Opcional | Completo |
>
> Si configuró previamente algún dispositivo en el nivel **Mejorado**, al actualizar a la versión 2006, se revertirá a **Opcional (limitado)** . Como consecuencia, se envían menos datos a Microsoft. Este cambio no debe afectar a lo que se ve en Análisis de escritorio.

Para más información sobre los datos de diagnóstico que se comparten con Microsoft con el nivel de datos de diagnóstico **Opcional (limitado)** , consulte [Eventos y campos de datos de diagnóstico de nivel mejorado de Windows 10](/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!IMPORTANT]
> Microsoft está firmemente comprometido a proporcionar las herramientas y los recursos que le sitúan al mando de su privacidad. Como resultado, aunque Análisis de escritorio admite dispositivos Windows 8.1, Microsoft no recopila datos de diagnóstico de Windows de dispositivos Windows 8.1 ubicados en países europeos (EEE y Suiza).

Para más información, consulte [Privacidad de Análisis de escritorio](privacy.md).

Los artículos siguientes son también buenos recursos para comprender mejor los niveles de datos de diagnóstico de Windows:

- [Windows 10 y GDPR: información para administradores de TI y toma de decisiones](/windows/privacy/gdpr-it-guidance)  

- [Configurar los datos de diagnóstico de Windows en la organización](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!NOTE]
> Los clientes configurados para enviar datos de diagnóstico con el nivel **Opcional (limitado)** enviarán aproximadamente 2 MB de datos a la nube de Microsoft en el examen completo inicial. La diferencia diaria varía entre 250 y 400 KB al día.
>
> El examen de diferencias diarias se produce a las 3:00 a. m. (hora local del dispositivo). Algunos eventos se envían en la primera hora disponible a lo largo del día. Estas horas no se pueden configurar.
>
> Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Puntos de conexión

Para habilitar el uso compartido de datos, configure el servidor proxy para permitir los siguientes puntos de conexión de Internet.

> [!IMPORTANT]
> De cara a la privacidad y la integridad de los datos, Windows comprueba si hay un certificado SSL de Microsoft (asignación de certificados) al comunicarse con los puntos de conexión de datos de diagnóstico. No es posible la interceptación y la inspección de SSL. Para usar Análisis de escritorio, excluya estos puntos de conexión de la inspección de SSL.<!-- BUG 4647542 -->

A partir de la versión 2002, si el sitio de Configuration Manager no se puede conectar a los puntos de conexión necesarios para un servicio en la nube, genera un mensaje de estado crítico con el identificador 11488. Si no se puede conectar al servicio, el estado del componente SMS_SERVICE_CONNECTOR cambia a crítico. Consulte el estado detallado en el nodo [Estado del componente](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) de la consola de Configuration Manager.<!-- 5566763 -->

> [!NOTE]
> Para más información sobre los intervalos de direcciones IP de Microsoft, consulte [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602) (Espacio de direcciones IP públicas de Microsoft). Estas direcciones se actualizan periódicamente. No hay granularidad por servicio, por lo que se podría usar cualquier dirección IP dentro de estos intervalos.

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

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
> El enfoque de autenticación proxy del usuario no es compatible con el uso de Azure Advanced Threat Protection de Microsoft Defender. Este comportamiento se debe a que esta autenticación se basa en la clave del Registro **DisableEnterpriseAuthProxy** establecida en `0`, mientras que ATP de Microsoft Defender requiere que se establezca en `1`. Para obtener más información, consulte [Configurar el proxy del equipo y la configuración de conectividad de Internet en ATP de Microsoft Defender](/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

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