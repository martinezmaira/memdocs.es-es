---
title: Administración de las opciones de reducción de la superficie expuesta a ataques con directivas de seguridad de puntos de conexión en Microsoft Intune | Microsoft Docs
description: Configure e implemente directivas para los dispositivos administrados con opciones de directiva de reducción de la superficie expuesta a ataques en Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 20c8cc73e8037c0f394547b64d562cf75271240c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431454"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Directiva de reducción de la superficie expuesta a ataques para la seguridad de puntos de conexión en Intune

Si hace uso del antivirus de Defender en los dispositivos Windows 10, puede usar las directivas de seguridad de puntos de conexión de Intune para reducir la superficie de ataque y administrar esas opciones en los dispositivos.

Las directivas de reducción de la superficie expuesta a ataques ayudan a disminuir las superficies de ataque, ya que reducen la cantidad de lugares en los que la organización es vulnerable a ciberamenazas y ataques. Para más información, vea [Información general sobre la reducción de la superficie expuesta a ataques]( https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) en la documentación de protección contra amenazas de Windows.

Encontrará las directivas de seguridad de puntos de conexión correspondientes a la reducción de la superficie expuesta a ataques en *Administrar*, en el nodo **Seguridad de los puntos de conexión** del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Cada *perfil* de reducción de la superficie expuesta a ataques administra las opciones de un área concreta de un dispositivo Windows 10.

Vea cuáles son las [opciones de los perfiles de reducción de la superficie expuesta a ataques](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>Requisitos previos de los perfiles de reducción de la superficie expuesta a ataques

- Windows 10 o posterior
- Antivirus de Defender como antivirus principal del dispositivo

## <a name="attack-surface-reduction-profiles"></a>Perfiles de reducción de la superficie expuesta a ataques

**Perfiles de Windows 10**:

- **Aislamiento de aplicaciones y navegador**: administre las opciones de Protección de aplicaciones de Windows Defender como parte de ATP de Defender. Protección de aplicaciones ayuda a evitar ataques antiguos y recientes, y permite aislar sitios definidos por la empresa como de no confianza y, al mismo tiempo, definir qué sitios, recursos en la nube y redes internas sí son de confianza.

  Para más información, vea [Protección de aplicaciones](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) en la documentación de ATP de Microsoft Defender.

- **Protección web**: las opciones de protección web que se pueden administrar en ATP de Microsoft Defender configuran la protección de red para proteger los equipos de amenazas web. Gracias a la integración con Microsoft Edge y los navegadores de terceros más conocidos, como Chrome y Firefox, la protección web detiene las amenazas web sin necesidad de un proxy web, y los equipos se pueden proteger tanto de forma remota como local. La protección web impide el acceso a lo siguiente:
  - Sitios de suplantación de identidad (phishing)
  - Vectores de malware
  - Sitios de vulnerabilidad de seguridad
  - Sitios que no son de confianza o de baja reputación
  - Sitios bloqueados en la lista de indicadores personalizados

  Para más información, vea [Protección web](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) en la documentación de ATP de Microsoft Defender.

- **Control de aplicaciones**: las opciones de control de aplicaciones ayudan a mitigar las amenazas de seguridad restringiendo las aplicaciones que los usuarios pueden ejecutar y el código que se ejecuta en el núcleo del sistema (kernel). Administre las opciones que pueden bloquear archivos MSI y scripts sin firmar, y restrinja Windows PowerShell para que se ejecute en modo de lenguaje restringido.

  Para más información, vea [Control de aplicaciones](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) en la documentación de ATP de Microsoft Defender.

- **Reglas de reducción de la superficie expuesta a ataques**: configure las opciones de las reglas de reducción de la superficie expuesta a ataques dirigidas a acabar con los comportamientos que el malware y las aplicaciones malintencionadas suelen manifestar para infectar equipos, por ejemplo:
  - Archivos ejecutables y scripts usados en aplicaciones de Office, o correo electrónico web que intenta descargar o ejecutar archivos
  - Scripts confusos o sospechosos
  - Comportamientos que las aplicaciones no suelen iniciar durante el trabajo cotidiano habitual Reducir la superficie de ataque significa conseguir que los atacantes tengan menos formas de llevar a cabo ataques.

  Para más información, vea [Reglas de reducción de la superficie expuesta a ataques](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) en la documentación de ATP de Microsoft Defender.

- **Control de dispositivos**: con las opciones de control de dispositivos, los dispositivos se pueden configurar con un método por niveles para proteger los medios extraíbles. ATP de Microsoft Defender proporciona varias características de supervisión y control que ayudan a evitar que las amenazas de periféricos no autorizados pongan en peligro sus dispositivos.

  Para más información, vea [Cómo controlar dispositivos USB y otros medios extraíbles usando ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/device-control/control-usb-devices-using-intune) en la documentación de ATP de Microsoft Defender.

- **Protección contra vulnerabilidades**: las opciones de protección contra vulnerabilidades puede ayudar a protegerse del malware que usa vulnerabilidades para infectar dispositivos y propagarse. La protección contra vulnerabilidades se compone de una serie de mitigaciones que se pueden aplicar al sistema operativo o a aplicaciones individuales.

  Para más información, vea [Habilitar la protección contra vulnerabilidades](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) en la documentación de ATP de Microsoft Defender.

## <a name="next-steps"></a>Pasos siguientes

[Configuración de directivas de seguridad de puntos de conexión](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
