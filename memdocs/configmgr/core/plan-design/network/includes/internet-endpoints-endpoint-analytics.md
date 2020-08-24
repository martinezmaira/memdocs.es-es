---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126480"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Puntos de conexión necesarios para los dispositivos administrados por Configuration Manager

Los dispositivos administrados por Configuration Manager envían datos a Intune a través del conector en el rol de Configuration Manager y no necesitan acceder directamente a la nube pública de Microsoft.

| Punto de conexión  | Función  |
|-----------|-----------|
| `https://graph.windows.net` | Se usa para recuperar automáticamente la configuración al asociar la jerarquía a Análisis de puntos de conexión en el rol de servidor de Configuration Manager. Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Se usa para sincronizar la recopilación de dispositivos y los dispositivos con Análisis de puntos de conexión solo en el rol del servidor de Configuration Manager. Para más información, consulte [Configuración del proxy para un servidor de sistema de sitio](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="endpoints-required-for-intune-managed-devices"></a>Puntos de conexión necesarios para los dispositivos administrados por Intune

Para inscribir dispositivos en Análisis de puntos de conexión, se deben enviar los datos funcionales necesarios a la nube pública de Microsoft. El Análisis de puntos de conexión usa el componente Telemetría y experiencias del usuario conectado de Windows 10 y Windows Server (DiagTrack) para recopilar los datos de los dispositivos administrados por Intune. Asegúrese de que el servicio **Experiencia del usuario y telemetría asociadas** se ejecuta en el dispositivo.

| Punto de conexión  | Función  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Los dispositivos administrados por Intune lo usan para enviar los [datos funcionales necesarios](../../../../../analytics/data-collection.md#bkmk_datacollection) al punto de conexión de recopilación de datos de Intune. |
