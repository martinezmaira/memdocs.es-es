---
title: Conector de Lookout MTD con Microsoft Intune
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo integrar Intune con Lookout Mobile Threat Defense (MTD) para controlar el acceso de los dispositivos móviles a los recursos corporativos.
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
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17b120faa0021a1fc044d7831b4b81ea88f404a7
ms.sourcegitcommit: bbb63f69ff8a755a2f2d86f2ea0c5984ffda4970
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2020
ms.locfileid: "79526587"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Conector de Lookout Mobile Endpoint Security con Intune

Puede controlar el acceso del dispositivo móvil a recursos corporativos según la evaluación del riesgo que realice Lookout, una solución Mobile Threat Defense integrada con Microsoft Intune. El riesgo se evalúa basándose en la telemetría recopilada de dispositivos mediante el servicio de Lookout que incluye:
- Vulnerabilidades del sistema operativo
- Aplicaciones malintencionadas instaladas
- Perfiles de red malintencionados

Se pueden configurar directivas de acceso condicional según la evaluación de riesgos de Lookout habilitada mediante las directivas de cumplimiento de Intune para dispositivos inscritos, que se pueden usar para permitir o bloquear dispositivos que no cumplan los requisitos y, así, evitar que accedan a recursos corporativos en función de las amenazas detectadas. En el caso de los dispositivos no inscritos, puede usar directivas de protección de aplicaciones para aplicar un bloqueo o un borrado selectivo en función de las amenazas detectadas.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>¿Cómo contribuye Lookout Mobile Threat Defense a proteger los recursos de la empresa?

La aplicación móvil Lookout, **Lookout for Work**, está instalada y se ejecuta en dispositivos móviles. Esta aplicación captura el sistema de archivos, la pila de red y la telemetría de aplicaciones y dispositivos cuando está disponible, después lo envía al servicio en la nube de Lookout para evaluar el riesgo del dispositivo para las amenazas móviles. Puede cambiar la clasificación del nivel de riesgo de las amenazas en la consola de Lookout para satisfacer sus requisitos.

- **Compatibilidad con los dispositivos inscritos**: la directiva de cumplimiento de dispositivos de Intune incluye una regla para Mobile Threat Defense (MTD), que puede usar la información de evaluación de riesgos de Lookout for Work. Si la regla de MTD está habilitada, Intune evalúa la conformidad del dispositivo con la directiva que habilitó. Si se detecta que el dispositivo no cumple con la directiva, se bloqueará el acceso de los usuarios a los recursos corporativos, como Exchange Online y SharePoint Online. Los usuarios también reciben instrucciones de la aplicación Lookout for Work instalada en sus dispositivos para resolver el problema y recuperar el acceso a los recursos corporativos. Para admitir el uso de Lookout for Work con dispositivos inscritos:
  - [Incorpore aplicaciones MTD a los dispositivos](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md).
  - [Cree una directiva de cumplimiento de dispositivos compatible con MTD](../protect/mtd-device-compliance-policy-create.md).
  - [Habilite el conector de MTD en Intune](../protect/mtd-connector-enable.md).

- **Compatibilidad con dispositivos no inscritos**: Intune puede usar los datos de evaluación de riesgos de la aplicación de Lookout for Work en los dispositivos no inscritos cuando se usan las directivas de protección de aplicaciones de Intune. Los administradores pueden usar esta combinación para facilitar la protección de los datos corporativos dentro de una [aplicación protegida de Microsoft Intune](../apps/apps-supported-intune-apps.md), así como emitir un bloqueo o un borrado selectivo para datos corporativos en esos dispositivos. Para admitir el uso de Lookout for Work con dispositivos no inscritos:
  - [Incorpore la aplicación MTD a dispositivos no inscritos](../protect/mtd-add-apps-unenrolled-devices.md).
  - [Cree una directiva de protección de aplicaciones de Mobile Threat Defense](../protect/mtd-app-protection-policy.md).
  - [Habilite el conector de MTD en Intune para dispositivos no inscritos](../protect/mtd-enable-unenrolled-devices.md).

## <a name="supported-platforms"></a>Plataformas compatibles

Las siguientes plataformas son compatibles con Lookout cuando se inscriben en Intune:

- **Android 4.1 y versiones posteriores**  
- **iOS 8 y versiones posteriores**  

Para información adicional sobre la compatibilidad de lenguaje y plataforma, visite el [sitio web de Lookout](https://personal.support.lookout.com/hc/articles/114094140253).  

## <a name="prerequisites"></a>Requisitos previos

- Suscripción de empresa a Lookout Mobile Endpoint Security  
- Suscripción a Microsoft Intune
- Azure Active Directory Premium
- Enterprise Mobility and Security (EMS) E3 o E5, con licencias asignadas a los usuarios.  

Para obtener más información, consulte [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).

## <a name="sample-scenarios"></a>Escenarios de ejemplo

Estos son los escenarios comunes cuando se usa Mobile Endpoint Security con Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Control del acceso basado en amenazas de aplicaciones malintencionadas

Cuando las aplicaciones malintencionadas como malware se detectan en dispositivos, puede bloquear los dispositivos de la siguiente manera hasta que la amenaza se resuelva:

- Conectarse al correo electrónico corporativo
- Sincronizar los archivos corporativos mediante la aplicación OneDrive para el trabajo
- Acceder a las aplicaciones de empresa

*Bloquear cuando se detectan aplicaciones malintencionadas:*

> [!div class="mx-imgBorder"]
> ![Imagen conceptual de directiva que bloquea el acceso por contener aplicaciones malintencionadas](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Acceso concedido tras la corrección:*

> [!div class="mx-imgBorder"]
> ![Imagen conceptual que muestra el acceso que se concede a los dispositivos después de la corrección](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar el acceso basándose en amenazas en la red

Detecte amenazas para la red como ataques de tipo "Man in the middle" y proteja el acceso a las redes Wi-Fi según el riesgo del dispositivo.

*Bloquear el acceso de red a través de Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Imagen que muestra el bloqueo de acceso de Wi-Fi basándose en amenazas de red](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Acceso concedido tras la corrección:*

> [!div class="mx-imgBorder"]
> ![Imagen conceptual del acceso condicional que permite el acceso después de la corrección](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar el acceso a SharePoint Online basándose en amenazas en la red

Detecte amenazas en la red como ataques de tipo "Man in the middle" e impida la sincronización de archivos corporativos en función del riesgo del dispositivo.

*Bloqueo de SharePoint Online cuando se detectan amenazas a la red:*

> [!div class="mx-imgBorder"]
> ![Imagen conceptual de bloqueo del acceso a SharePoint Online](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Acceso concedido tras la corrección:*

> [!div class="mx-imgBorder"]
> ![Imagen conceptual que muestra cómo se permite el acceso tras la corrección de la amenaza de red](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Control del acceso en dispositivos no inscritos basado en amenazas de aplicaciones malintencionadas

Cuando la solución Lookout Mobile Threat Defense considera que un dispositivo está infectado:
> [!div class="mx-imgBorder"]
> ![La directiva de protección de aplicaciones realiza un bloqueo debido al malware detectado](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png).

Se concede acceso tras la corrección:

> [!div class="mx-imgBorder"]
> ![Se concede acceso tras la corrección a la directiva de protección de aplicaciones](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png).

## <a name="next-steps"></a>Pasos siguientes

Aquí se muestran los pasos principales que debe realizar para implementar esta solución:

- [Configurar la integración a Lookout](lookout-mtd-connector-integration.md)
- [Habilitar el conector Mobile Threat Defense en Intune](mtd-connector-enable.md)
- [Agregar y asignar la aplicación Lookout for Work](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Crear la directiva de cumplimiento de dispositivos de Lookout](mtd-device-compliance-policy-create.md)
- [Creación de una directiva de protección de aplicaciones de MTD](mtd-app-protection-policy.md)
