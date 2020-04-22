---
title: Conector Mobile Threat Defense de Better Mobile con Intune
titleSuffix: Intune on Azure
description: Configure el conector Mobile Threat Defense de Better Mobile con Intune.
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
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "79353988"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Conector Mobile Threat Defense de Better Mobile con Intune

Puede controlar el acceso desde dispositivos móviles a recursos corporativos mediante el acceso condicional basado en la evaluación de riesgos efectuada por Better Mobile, una solución de Mobile Threat Defense (MTD) integrada en Microsoft Intune. El riesgo se evalúa en función de la telemetría recopilada de los dispositivos que ejecutan la aplicación Better Mobile.

Se pueden configurar directivas de acceso condicional según la evaluación de riesgos de Better Mobile habilitada mediante las directivas de cumplimiento de dispositivos de Intune para dispositivos inscritos, que se pueden usar para permitir o bloquear dispositivos que no cumplan los requisitos y, así, evitar que accedan a recursos corporativos en función de las amenazas detectadas. En el caso de los dispositivos no inscritos, puede usar directivas de protección de aplicaciones para aplicar un bloqueo o un borrado selectivo en función de las amenazas detectadas.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>¿Cómo ayudan Intune y Better Mobile a proteger los recursos de la empresa?

La aplicación móvil Better Mobile se instala y se ejecuta en dispositivos móviles. Esta aplicación captura el sistema de archivos, la pila de red, el dispositivo y la telemetría de aplicaciones cuando está disponible, y luego envía los datos al servicio en la nube de Better Mobile para evaluar el riesgo del dispositivo para las amenazas móviles.

- **Compatibilidad con los dispositivos inscritos**: la directiva de cumplimiento de dispositivos de Intune incluye una regla para Mobile Threat Defense (MTD), que puede usar la información de evaluación de riesgos de Better Mobile. Si la regla de MTD está habilitada, Intune evalúa la conformidad del dispositivo con la directiva que habilitó. Si se detecta que el dispositivo no cumple con la directiva, se bloqueará el acceso de los usuarios a los recursos corporativos, como Exchange Online y SharePoint Online. Los usuarios también reciben los pasos de la aplicación Better Mobile instalada en sus dispositivos para resolver el problema y volver a obtener acceso a los recursos corporativos. Para admitir el uso de Better Mobile con dispositivos inscritos:
  - [Incorpore aplicaciones MTD a los dispositivos](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md).
  - [Cree una directiva de cumplimiento de dispositivos compatible con MTD](../protect/mtd-device-compliance-policy-create.md).
  - [Habilite el conector de MTD en Intune](../protect/mtd-connector-enable.md).

- **Compatibilidad con dispositivos no inscritos**: Intune puede usar los datos de evaluación de riesgos de la aplicación de Better Mobile en los dispositivos no inscritos cuando se usan las directivas de protección de aplicaciones de Intune. Los administradores pueden usar esta combinación para facilitar la protección de los datos corporativos dentro de una [aplicación protegida de Microsoft Intune](../apps/apps-supported-intune-apps.md), así como emitir un bloqueo o un borrado selectivo para datos corporativos en esos dispositivos. Para admitir el uso de Better Mobile con dispositivos no inscritos:
  - [Incorpore la aplicación MTD a dispositivos no inscritos](../protect/mtd-add-apps-unenrolled-devices.md).
  - [Cree una directiva de protección de aplicaciones de Mobile Threat Defense](../protect/mtd-app-protection-policy.md).
  - [Habilite el conector de MTD en Intune para dispositivos no inscritos](../protect/mtd-enable-unenrolled-devices.md).

## <a name="supported-platforms"></a>Plataformas compatibles

- **Android 4.1 y versiones posteriores**

- **iOS 8.0 y versiones posteriores**

## <a name="prerequisites"></a>Requisitos previos

- Azure Active Directory Premium

- Suscripción a Microsoft Intune

- Suscripción a Mobile Threat Defense de Better Mobile

  - Para obtener más información, vea el [sitio web de Better Mobile](https://www.better.mobi/).

## <a name="sample-scenarios"></a>Escenarios de ejemplo

Estos son algunos casos más frecuentes.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Control del acceso basado en amenazas de aplicaciones malintencionadas

Cuando se detectan aplicaciones malintencionadas, como el malware, en los dispositivos, puede bloquear las siguientes acciones hasta resolver la amenaza:

- Conectarse al correo electrónico corporativo

- Sincronizar los archivos corporativos mediante la aplicación OneDrive para el trabajo

- Acceder a las aplicaciones de empresa

Bloqueo cuando se detectan aplicaciones malintencionadas:

![Imagen que muestra las aplicaciones malintencionadas detectadas](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

Se concede acceso tras la corrección:

![Aplicaciones malintencionadas detectadas y acceso concedido](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar el acceso basándose en amenazas en la red

Detecte amenazas para la red, por ejemplo, ataques de tipo **Man in the middle**, y proteja el acceso a las redes Wi-Fi según el riesgo del dispositivo.

Bloqueo del acceso de red a través de Wi-Fi:

![Bloquear el acceso de red a través de Wi-Fi](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

Se concede acceso tras la corrección:

![Imagen que muestra el acceso concedido tras la corrección](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar el acceso a SharePoint Online basándose en amenazas en la red

Detecte amenazas para la red, por ejemplo, ataques de tipo **Man in the middle**, y evite la sincronización de archivos corporativos según el riesgo del dispositivo.

Bloqueo de SharePoint Online cuando se detectan amenazas de red:

![Bloqueo de SharePoint Online cuando se detectan amenazas a la red](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Acceso concedido tras la solución:

![Acceso concedido tras la solución](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Control del acceso en dispositivos no inscritos basado en amenazas de aplicaciones malintencionadas

Cuando la solución BETTER Mobile Threat Defense considera que un dispositivo está infectado: ![La directiva de protección de aplicaciones realiza un bloqueo debido al malware detectado](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png).

Se concede acceso tras la corrección:

![Se concede acceso tras la corrección a la directiva de protección de aplicaciones.](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Pasos siguientes

- [Integrate Better Mobile with Intune](better-mobile-mtd-connector-integration.md) (Integración de Better Mobile con Intune)

- [Set up Better Mobile apps](mtd-apps-ios-app-configuration-policy-add-assign.md) (Configuración de aplicaciones de Better Mobile)

- [Create Better Mobile device compliance policy](mtd-device-compliance-policy-create.md) (Creación de la directiva de cumplimiento de dispositivos de Better Mobile)

- [Enable Better Mobile MTD connector](mtd-connector-enable.md) (Habilitación del conector de MTD de Better Mobile)

- [Creación de una directiva de protección de aplicaciones de MTD](mtd-app-protection-policy.md) 
