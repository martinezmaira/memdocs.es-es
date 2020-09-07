---
title: Configuración de la seguridad móvil de Wandera con Intune
titleSuffix: Intune on Azure
description: Procedimientos para configurar la seguridad móvil de Wandera con Microsoft Intune para controlar el acceso de los dispositivos móviles a los recursos corporativos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/2/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c0911ff9250fb1b2832df4b7e269f192ee8cda
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057528"
---
# <a name="wandera-mobile-threat-defense-connector-with-intune"></a>Conector Wandera Mobile Threat Defense con Intune  

Controle el acceso desde dispositivos móviles a recursos corporativos mediante el acceso condicional en función de la evaluación de riesgos efectuada por Wandera. Wandera es una solución Mobile Threat Defense (MTD) que se integra con Microsoft Intune.  El riesgo se evalúa basándose en la telemetría recopilada de dispositivos mediante el servicio de Wandera que incluye:
- Vulnerabilidades del sistema operativo
- Aplicaciones malintencionadas instaladas
- Perfiles de red malintencionados
- Cryptojacking

Puede configurar directivas de *acceso condicional* basadas en la evaluación de riesgos de Wandera, habilitada mediante las directivas de cumplimiento de dispositivos de Intune. La directiva de evaluación de riesgos puede permitir o bloquear el acceso de dispositivos no compatibles a recursos corporativos en función de las amenazas detectadas.  

## <a name="how-do-intune-and-wandera-mobile-threat-defense-help-protect-your-company-resources"></a>¿Cómo contribuyen Wandera Mobile Threat Defense e Intune a proteger los recursos de la empresa?  

La aplicación móvil de Wandera se instala sin problemas con Microsoft Intune. Esta aplicación captura el sistema de archivos, la pila de red y la telemetría del dispositivo y de la aplicación (cuando están disponibles). Esta información se sincroniza con el servicio en la nube de Wandera para evaluar el riesgo del dispositivo de amenazas móviles. Estas clasificaciones de nivel de riesgo se pueden configurar para adaptarse a sus necesidades en la consola de Wandera, RADAR.

La directiva de cumplimiento de Intune incluye una regla para MTD basada en la evaluación de riesgos de Wandera. Cuando esta regla está habilitada, Intune evalúa la conformidad del dispositivo con la directiva que habilitó.

Para los dispositivos que no son compatibles, puede bloquearse el acceso a recursos como Microsoft 365. Los usuarios de dispositivos bloqueados reciben instrucciones de la aplicación de Wandera para resolver el problema y volver a obtener acceso.

Wandera actualizará Intune con el nivel de amenaza más reciente de cada dispositivo (seguro, bajo, medio o alto) cada vez que dicho nivel cambie. Wandera Security Cloud calcula continuamente este nivel de amenaza en función del estado del dispositivo, la actividad de la red y un gran número de fuentes de inteligencia sobre amenazas móviles que tienen en cuenta varias categorías de amenazas.

Estas categorías y sus niveles de amenaza asociados se pueden configurar en la consola RADAR de Wandera, lo que permite personalizar el nivel de amenaza total calculado de cada dispositivo según los requisitos de seguridad de su organización. Teniendo en cuenta el nivel de amenaza, hay dos tipos de directivas de Intune que usan esta información para administrar el acceso a los datos corporativos:

* Mediante las **directivas de cumplimiento de dispositivos** con acceso condicional, los administradores establecen directivas para marcar automáticamente un dispositivo administrado como "fuera de cumplimiento" según el nivel de amenaza notificado por Wandera. Esta marca de cumplimiento controla posteriormente las directivas de acceso condicional para permitir o denegar el acceso a las aplicaciones que usan la autenticación moderna.  Para obtener detalles sobre la configuración, consulte [Creación de directiva de cumplimiento de dispositivos de Mobile Threat Defense (MTD) con Intune](../protect/mtd-device-compliance-policy-create.md).

* Mediante el uso de **directivas de protección de aplicaciones** con el inicio condicional, los administradores pueden establecer directivas que se aplican en el nivel de aplicación nativa (por ejemplo, aplicaciones de SO iOS/iPad y Android como Outlook, OneDrive, etc.), en función del nivel de amenaza notificado por Wandera.  Estas directivas también se pueden usar con dispositivos no administrados (MAM-WE) para proporcionar una directiva uniforme en todas las plataformas de dispositivos y modos de propiedad. Para obtener detalles sobre la configuración, consulte [Creación de una directiva de protección de aplicaciones de Mobile Threat Defense con Intune](../protect/mtd-app-protection-policy.md).

## <a name="supported-platforms"></a>Plataformas compatibles  

Las siguientes plataformas son compatibles con Wandera cuando se inscriben en Intune:

- Android 5.0 y versiones posteriores  
- iOS 10.2 y versiones posteriores 

Para obtener más información sobre la plataforma y el dispositivo, consulte el [sitio web de Wandera](https://www.wandera.com/mobile-threat-defense/).

## <a name="prerequisites"></a>Requisitos previos  

- Suscripción a Microsoft Intune  
- Azure Active Directory  
- Wandera Mobile Threat Defense (anteriormente Wandera Secure)  

Para obtener más información, consulte la sección sobre [seguridad móvil de Wandera](https://www.wandera.com/mobile-security/).
 
## <a name="sample-scenarios"></a>Escenarios de ejemplo

Estos son los escenarios comunes cuando se usa Wandera MTD con Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Control del acceso basado en amenazas de aplicaciones malintencionadas  

Cuando las aplicaciones malintencionadas como malware se detectan en dispositivos, puede bloquear estos a partir de herramientas comunes hasta que la amenaza se resuelva. Los bloques comunes incluyen:  
- Conectarse al correo electrónico corporativo  
- Sincronizar los archivos corporativos mediante la aplicación OneDrive para el trabajo  
- Acceder a las aplicaciones de empresa  

*Bloquear cuando se detectan aplicaciones malintencionadas*:

![Imagen conceptual de aplicaciones malintencionadas detectadas](./media/wandera-mtd-connector/wandera-malicious-apps-blocked.png)  

*Acceso concedido tras la corrección*: 

![Imagen conceptual de acceso concedido tras la corrección](./media/wandera-mtd-connector/wandera-malicious-apps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Controlar el acceso basándose en amenazas en la red  

Detecte amenazas para la red como ataques de tipo "Man in the middle" y proteja el acceso a las redes Wi-Fi según el riesgo del dispositivo.  

*Bloquear el acceso de red a través de Wi-Fi*:  

![Bloquear el acceso de red a través de Wi-Fi](./media/wandera-mtd-connector/wandera-network-wifi-blocked.png)

*Acceso concedido tras la corrección*:  

![Acceso concedido tras la corrección](./media/wandera-mtd-connector/wandera-network-wifi-unblocked.png)  

## <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar el acceso a SharePoint Online basándose en amenazas en la red

Detecte amenazas en la red como ataques de tipo "Man in the middle" e impida la sincronización de archivos corporativos en función del riesgo del dispositivo.

*Bloqueo de SharePoint Online cuando se detectan amenazas de red*:  

![Bloqueo de SharePoint Online cuando se detectan amenazas a la red](./media/wandera-mtd-connector/wandera-network-spo-blocked.png)  

*Acceso concedido tras la corrección*:  

![Acceso concedido tras la corrección para el ejemplo de SharePoint](./media/wandera-mtd-connector/wandera-network-spo-unblocked.png)  

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Control del acceso en dispositivos no inscritos basado en amenazas de aplicaciones malintencionadas

Cuando la solución Wandera Mobile Threat Defense considera que un dispositivo está infectado:

![La directiva de protección de aplicaciones realiza un bloqueo debido al malware detectado.](./media/wandera-mtd-connector/wandera-mobile-app-policy-block.png)

Se concede acceso tras la corrección:

![Se concede acceso tras la corrección a la directiva de protección de aplicaciones.](./media/wandera-mtd-connector/wandera-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Pasos siguientes

- [Integrate Wandera with Intune](wandera-mtd-connector-integration.md) (Integración de Wandera con Intune)
- [Agregar y asignar aplicaciones de Mobile Threat Defense (MTD) con Intune](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Creación de directiva de cumplimiento de dispositivos de Mobile Threat Defense (MTD) con Intune](mtd-device-compliance-policy-create.md)
- [Habilitar el conector Mobile Threat Defense en Intune](mtd-connector-enable.md)
