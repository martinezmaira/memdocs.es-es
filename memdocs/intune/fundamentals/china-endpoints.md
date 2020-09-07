---
title: 'Puntos de conexión de red para las implementaciones de China: Microsoft Intune'
titleSuffix: ''
description: Revise los puntos de conexión de China para Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd52b34b70b71874a42486cbdc87cd3d7d2f9037
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994249"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Puntos de conexión de China para Microsoft Intune

En esta página se enumeran los puntos de conexión de China necesarios para la configuración del proxy en las implementaciones de Intune.

Para administrar dispositivos que se encuentren detrás de firewalls y servidores proxy, debe habilitar la comunicación para Intune.

- El servidor proxy debe ser compatible con **HTTP (80)** y **HTTPS (443)** , ya que los clientes de Intune usan ambos protocolos.
- Para algunas tareas (como descargar actualizaciones de software), Intune necesita acceso de un servidor proxy no autenticado a manage.microsoft.com.

Puede modificar la configuración del servidor proxy en equipos cliente individuales. También puede usar la opción de directiva de grupo para cambiar la configuración de todos los equipos cliente que se encuentran detrás de un servidor proxy especificado.

Los dispositivos administrados requieren configuraciones que dejen acceder a **Todos los usuarios** a los servicios a través de firewalls.

Para más información sobre la inscripción automática de Windows 10 y el registro de dispositivos para clientes de la administración pública de China, consulte [Configuración de la inscripción para dispositivos Windows](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

En las siguientes tablas se enumeran los puertos y los servicios a los que accede el cliente de Intune:

|**Punto de conexión**|**Dirección IP**|
|---------------------|-----------|
|*.manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>Puntos de conexión designados por el cliente de Intune en China
- Azure Portal: https:\//portal.azure.cn/
- Microsoft 365: https:\//portal.partner.microsoftonline.cn/
- Portal de empresa de Intune: https:\//portal.manage.microsoftonline.cn/
- Centro de administración de Microsoft Endpoint Manager: https:\//endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>Puntos de conexión de partners

Intune ofrecido por 21Vianet depende de los siguientes puntos de conexión de servicio de partners:
- Servicio Sincronización de Azure AD: https:\//syncservice.partner.microsoftonline.cn/DirectoryService.svc
- Evo STS: https:\//login.chinacloudapi.cn/
- Azure AD Graph: https:\//graph.chinacloudapi.us
- MS Graph: https:\//microsoftgraph.chinacloudapi.cn
- ADRS: https:\//enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Pasos siguientes
[Más información sobre Intune ofrecido por 21Vianet en China](china.md)

