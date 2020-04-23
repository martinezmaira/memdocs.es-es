---
title: Proteger los datos y la infraestructura del sitio
titleSuffix: Configuration Manager
description: Aprenda a proteger los recursos de la organización frente a exposiciones o ataques malintencionados con Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708603"
---
# <a name="protect-data-and-site-infrastructure"></a>Proteger los datos y la infraestructura del sitio

*Se aplica a: Configuration Manager (rama actual)*

Quiere que los usuarios accedan de forma segura a los recursos de su organización. Proteja la infraestructura y los datos frente a la exposición o los ataques malintencionados. Use Configuration Manager para habilitar el acceso y ayudar a proteger los recursos de su organización.  

- [Endpoint Protection](../deploy-use/endpoint-protection.md) le permite administrar las siguientes directivas de Microsoft Defender para equipos cliente:

  - Antimalware de Microsoft Defender
  - Firewall de Microsoft Defender
  - Protección contra amenazas avanzada de Microsoft Defender
  - Protección contra vulnerabilidades de seguridad de Microsoft Defender
  - Protección de aplicaciones de Microsoft Defender
  - Control de aplicaciones de Microsoft Defender

  > [!TIP]
  > Para administrar Endpoint Protection en dispositivos Windows 10 de administración conjunta con el servicio en la nube de Microsoft Endpoint Manager, cambie la [carga de trabajo de **Endpoint Protection**](../../comanage/workloads.md#endpoint-protection) a Intune. Para obtener más información, vea [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

- Proteja los datos almacenados en clientes de Windows locales con cifrado de unidad BitLocker (BDE). Configuration Manager ofrece una administración completa del ciclo de vida de BitLocker que puede sustituir el uso de Microsoft BitLocker Administration and Monitoring (MBAM). Para más información, vea [Planeación de la administración de BitLocker](../plan-design/bitlocker-management.md).

- En lugar de las contraseñas tradicionales, habilite métodos de inicio de sesión alternativos en dispositivos Windows 10 con Windows Hello para empresas. Para más información, vea [Configuración de Windows Hello para empresas](../deploy-use/windows-hello-for-business-settings.md).

- Minimice los esfuerzos de los usuarios para conectarse a recursos mediante la conectividad VPN con perfiles de VPN. Para obtener más información, vea [Perfiles de VPN](../deploy-use/vpn-profiles.md).  

- Los perfiles de Wi-Fi proporcionan un conjunto de herramientas y recursos para ayudarle a administrar la configuración de red inalámbrica en los dispositivos de su organización. Al implementar estas opciones, se minimiza el esfuerzo de los usuarios finales para conectarse a redes inalámbricas. Para más información, consulte [Perfiles de Wi-Fi](../deploy-use/create-wifi-profiles.md).  

- Aprovisione los dispositivos con los certificados que los usuarios necesitan para conectarse a los recursos. Para obtener más información, consulte [Introduction to certificate profiles in System Center Configuration Manager](../deploy-use/introduction-to-certificate-profiles.md) (Introducción a perfiles de certificado en Configuration Manager).  
