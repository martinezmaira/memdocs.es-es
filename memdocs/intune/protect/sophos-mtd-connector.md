---
title: Uso de Sophos Mobile con Intune
titleSuffix: Intune on Azure
description: Uso de la solución Sophos Mobile con Microsoft Intune para controlar el acceso de los dispositivos móviles a los recursos corporativos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 285f323f55d41edab5ccd450deb0244b6fbda874
ms.sourcegitcommit: bbb63f69ff8a755a2f2d86f2ea0c5984ffda4970
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2020
ms.locfileid: "79526451"
---
# <a name="sophos-mobile-threat-defense-connector-with-intune"></a>Conector Sophos Mobile Threat Defense con Intune
Puede controlar el acceso de los dispositivos móviles a los recursos corporativos mediante el acceso condicional basado en la evaluación de riesgos realizada por Sophos Mobile, una solución de Mobile Threat Defense (MTD) integrada en Microsoft Intune. El riesgo se evalúa en función de la telemetría recopilada de los dispositivos que ejecutan la aplicación Sophos Mobile.
Se pueden configurar directivas de acceso condicional según la evaluación de riesgos de Sophos Mobile habilitada mediante las directivas de cumplimiento de dispositivos de Intune. Esas directivas se pueden usar para permitir o bloquear los dispositivos que no cumplan los requisitos y evitar que accedan a recursos corporativos en función de las amenazas detectadas.

> [!NOTE]
> Este proveedor de Mobile Threat Defense no es compatible con dispositivos no inscritos.

## <a name="supported-platforms"></a>Plataformas compatibles

- Android 5.0 y versiones posteriores
- iOS 11.0 y versiones posteriores

## <a name="prerequisites"></a>Requisitos previos

- Azure Active Directory Premium
- Suscripción a Microsoft Intune
- Suscripción a Sophos Mobile Threat Defense

Para más información, vea el [sitio web de Sophos](https://www.sophos.com/products/mobile-control.aspx).

## <a name="how-do-intune-and-sophos-mobile-help-protect-your-company-resources"></a>¿Cómo ayudan Intune y Sophos Mobile a proteger los recursos de la empresa?

La aplicación Sophos Mobile para iOS/iPadOS y Android captura telemetría del sistema de archivos, la pila de red, los dispositivos y las aplicaciones si está disponible y, después, envía los datos de telemetría al servicio en la nube de Sophos Mobile para evaluar el riesgo del dispositivo frente a las amenazas móviles.

La directiva de cumplimiento de dispositivos de Intune incluye una regla para Sophos Mobile Threat Defense, que se basa en la evaluación de riesgos de Sophos Mobile. Cuando esta regla está habilitada, Intune evalúa la conformidad del dispositivo con la directiva que habilitó. Si se detecta que el dispositivo no cumple con la directiva, se bloqueará el acceso de los usuarios a los recursos corporativos, como Exchange Online y SharePoint Online. Los usuarios también reciben instrucciones de la aplicación Sophos Mobile instalada en sus dispositivos para resolver el problema y recuperar el acceso a los recursos corporativos.  

## <a name="sample-scenarios"></a>Escenarios de ejemplo

Estos son algunos casos más frecuentes.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Control del acceso basado en amenazas de aplicaciones malintencionadas

Cuando se detectan aplicaciones malintencionadas, como el malware, en los dispositivos, puede bloquear las siguientes acciones hasta resolver la amenaza:

- Conectarse al correo electrónico corporativo
- Sincronizar los archivos corporativos mediante la aplicación OneDrive para el trabajo
- Acceder a las aplicaciones de empresa

*Bloquear cuando se detectan aplicaciones malintencionadas*:

![Imagen conceptual de aplicaciones malintencionadas detectadas](./media/sophos-mtd-connector/sophos-malicious-apps-blocked.png)  

*Acceso concedido tras la corrección*:  
![Imagen conceptual del acceso concedido tras la corrección](./media/sophos-mtd-connector/sophos-malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar el acceso basándose en amenazas en la red

Detecte amenazas para la red, por ejemplo, ataques de tipo "Man in the middle", y proteja el acceso a las redes Wi-Fi según el riesgo del dispositivo.  

*Bloquear el acceso de red a través de Wi-Fi*:  
![Bloquear el acceso de red a través de Wi-Fi](./media/sophos-mtd-connector/sophos-network-wifi-blocked.png)

*Acceso concedido tras la corrección*:   
![Acceso concedido tras la corrección](./media/sophos-mtd-connector/sophos-network-wifi-unblocked.png)  

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar el acceso a SharePoint Online basándose en amenazas en la red

Detecte amenazas para la red, por ejemplo, ataques de tipo "Man in the middle", y evite la sincronización de los archivos corporativos según el riesgo del dispositivo.  

*Bloqueo de SharePoint Online cuando se detectan amenazas de red*:

![Bloqueo de SharePoint Online cuando se detectan amenazas a la red](./media/sophos-mtd-connector/sophos-network-spo-blocked.png)  

*Acceso concedido tras la corrección*:

![Acceso concedido tras la solución](./media/sophos-mtd-connector/sophos-network-spo-unblocked.png)  

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Sophos Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/sophos-mtd-connector/sophos-mobile-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/sophos-mtd-connector/sophos-mobile-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Pasos siguientes

- [Integración de Sophos con Intune](sophos-mtd-connector-integration.md)
- [Configuración de aplicaciones de Sophos](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Creación de la directiva de cumplimiento de dispositivos de Sophos](mtd-device-compliance-policy-create.md)
- [Habilitación del conector MTD de Sophos](mtd-connector-enable.md)
