---
title: Conector MTD de Zimperium con Intune
titleSuffix: Intune on Azure
description: Obtenga información sobre cómo integrar Intune con Zimperium Mobile Threat Defense para controlar el acceso de los dispositivos móviles a los recursos corporativos.
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
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed623abeb602e599866af7b7249756edd87d5a29
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349204"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Conector Mobile Threat Defense de Zimperium con Intune

Puede controlar el acceso desde dispositivos móviles a recursos corporativos mediante el acceso condicional basado en la evaluación de riesgos efectuada por Zimperium, una solución de defensa contra amenazas móviles (MTD) integrada en Microsoft Intune. El riesgo se evalúa en función de la telemetría recopilada de los dispositivos que ejecutan la aplicación Zimperium.

Se pueden configurar directivas de acceso condicional según la evaluación de riesgos de Zimperium habilitada mediante las directivas de cumplimiento de dispositivos de Intune para dispositivos inscritos, que se pueden usar para permitir o bloquear dispositivos que no cumplan los requisitos y, así, evitar que accedan a recursos corporativos en función de las amenazas detectadas. En el caso de los dispositivos no inscritos, puede usar directivas de protección de aplicaciones para aplicar un bloqueo o un borrado selectivo en función de las amenazas detectadas.

## <a name="supported-platforms"></a>Plataformas compatibles

- **Android 4.1 y versiones posteriores**

- **iOS 8 y versiones posteriores**

## <a name="prerequisites"></a>Requisitos previos

- Azure Active Directory Premium

- Suscripción a Microsoft Intune

- Suscripción a Mobile Threat Defense de Zimperium

  - Para más información, consulte el [sitio web de Zimperium](https://www.zimperium.com/zips-mobile-ips).

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>¿Cómo ayudan Intune y Zimperium a proteger los recursos de la empresa?

La aplicación Zimperium para iOS/iPadOS y Android captura telemetría del sistema de archivos, la pila de red, el dispositivo y las aplicaciones cuando está disponible. Después, envía los datos de telemetría al servicio en la nube de Zimperium para evaluar el riesgo del dispositivo frente a las amenazas móviles.

- **Compatibilidad con los dispositivos inscritos**: la directiva de cumplimiento de dispositivos de Intune incluye una regla para Mobile Threat Defense (MTD), que puede usar la información de evaluación de riesgos de Zimperium. Si la regla de MTD está habilitada, Intune evalúa la conformidad del dispositivo con la directiva que habilitó. Si se detecta que el dispositivo no cumple con la directiva, se bloqueará el acceso de los usuarios a los recursos corporativos, como Exchange Online y SharePoint Online. Los usuarios también reciben los pasos de la aplicación Zimperium instalada en sus dispositivos para resolver el problema y volver a obtener acceso a los recursos corporativos. Para admitir el uso de Zimperium con dispositivos inscritos:
  - [Incorpore aplicaciones MTD a los dispositivos](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md).
  - [Cree una directiva de cumplimiento de dispositivos compatible con MTD](../protect/mtd-device-compliance-policy-create.md).
  - [Habilite el conector de MTD en Intune](../protect/mtd-connector-enable.md).

- **Compatibilidad con dispositivos no inscritos**: Intune puede usar los datos de evaluación de riesgos de la aplicación de Zimperium en los dispositivos no inscritos cuando se usan las directivas de protección de aplicaciones de Intune. Los administradores pueden usar esta combinación para facilitar la protección de los datos corporativos dentro de una [aplicación protegida de Microsoft Intune](../apps/apps-supported-intune-apps.md), así como emitir un bloqueo o un borrado selectivo para datos corporativos en esos dispositivos. Para admitir el uso de Zimperium con dispositivos no inscritos:
  - [Incorpore la aplicación MTD a dispositivos no inscritos](../protect/mtd-add-apps-unenrolled-devices.md).
  - [Cree una directiva de protección de aplicaciones de Mobile Threat Defense](../protect/mtd-app-protection-policy.md).
  - [Habilite el conector de MTD en Intune para dispositivos no inscritos](../protect/mtd-enable-unenrolled-devices.md).
  
## <a name="sample-scenarios"></a>Escenarios de ejemplo

Vea a continuación algunos escenarios de integración de Zimperium con Intune:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Control del acceso basado en amenazas de aplicaciones malintencionadas

Cuando se detectan aplicaciones malintencionadas, como malware, en los dispositivos, puede bloquearlos de la siguiente manera hasta que la amenaza se resuelva:

- Conectarse al correo electrónico corporativo

- Sincronizar los archivos corporativos mediante la aplicación OneDrive para el trabajo

- Acceder a las aplicaciones de empresa

*Bloquear cuando se detectan aplicaciones malintencionadas:*

> [!div class="mx-imgBorder"]
> ![Imagen conceptual de aplicaciones malintencionadas detectadas](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Acceso concedido tras la corrección:*

> [!div class="mx-imgBorder"]
> ![Imagen conceptual del acceso concedido tras la corrección](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar el acceso basándose en amenazas en la red

Detecte amenazas para la red, como **ataques de tipo Man-in-the-middle**, y proteja el acceso a las redes Wi-Fi según el riesgo del dispositivo.

*Bloquear el acceso de red a través de Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Bloquear el acceso de red a través de Wi-Fi](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*Acceso concedido tras la corrección:*

> [!div class="mx-imgBorder"]
> ![Acceso concedido tras la corrección](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar el acceso a SharePoint Online basándose en amenazas en la red

Detecte amenazas para la red, como **ataques de tipo Man-in-the-middle**, y evite la sincronización de archivos corporativos según el riesgo del dispositivo.

*Bloqueo de SharePoint Online cuando se detectan amenazas a la red:*

> [!div class="mx-imgBorder"]
> ![Bloqueo de SharePoint Online cuando se detectan amenazas de red](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Acceso concedido tras la corrección:*

> [!div class="mx-imgBorder"]
> ![Acceso concedido tras la corrección para el ejemplo de SharePoint](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Control del acceso en dispositivos no inscritos basado en amenazas de aplicaciones malintencionadas

Cuando la solución Mobile Threat Defense de Zimperium considera que un dispositivo está infectado:

> [!div class="mx-imgBorder"]
> ![La directiva de protección de aplicaciones realiza un bloqueo debido al malware detectado](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png).

Se concede acceso tras la corrección:

> [!div class="mx-imgBorder"]
> ![Se concede acceso tras la corrección a la directiva de protección de aplicaciones](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png).

## <a name="next-steps"></a>Pasos siguientes

- [Integrar Zimperium con Intune](zimperium-mtd-connector-integration.md)

- [Configurar aplicaciones Zimperium](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Crear una directiva de cumplimiento de dispositivos de Zimperium](mtd-device-compliance-policy-create.md)

- [Habilitar el conector MTD de Zimperium](mtd-connector-enable.md)

- [Creación de una directiva de protección de aplicaciones de MTD](../protect/mtd-app-protection-policy.md)
