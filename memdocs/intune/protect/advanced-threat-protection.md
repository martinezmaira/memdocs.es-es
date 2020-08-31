---
title: Uso de ATP de Microsoft Defender en Microsoft Intune (Azure) | Microsoft Docs
description: Use Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) con Intune. Puede instalar, configurar e incorporar ATP en sus dispositivos de Intune, y usar una evaluación de riesgos de ATP de dispositivos con las directivas de cumplimiento y acceso condicional de los dispositivos de Intune para proteger los recursos de red.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f54bf7f281fca65e01d839e926200bc68c49765
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663454"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Aplicación del cumplimiento de ATP de Microsoft Defender con acceso condicional en Intune

Puede integrar Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) con Microsoft Intune como solución de Mobile Threat Defense. Esta integración puede ayudarle a evitar infracciones de seguridad y a limitar su impacto en una organización.

ATP de Microsoft Defender funciona con dispositivos que ejecutan Windows 10 o una versión posterior y con dispositivos Android.

Para que funcione correctamente, usará las siguientes tareas de configuración de manera conjunta:

- **Establecer una conexión de servicio a servicio entre Intune y ATP de Microsoft Defender**. Esta conexión permite que ATP de Microsoft Defender recopile datos sobre el riesgo de la máquina de los dispositivos compatibles que se administran con Intune.
- **Usar un perfil de configuración de dispositivo para incorporar dispositivos con ATP de Microsoft Defender**. Los dispositivos se incorporan para configurarlos y que se comuniquen con ATP de Microsoft Defender y para proporcionar datos que ayuden a evaluar su nivel de riesgo.
- **Usar una directiva de cumplimiento de dispositivos para establecer el nivel de riesgo que quiere permitir**. ATP de Microsoft Defender notifica los niveles de riesgo. Los dispositivos que superan el nivel de riesgo permitido se identifican como no compatibles.
- **Usar una directiva de acceso condicional** para impedir que los usuarios accedan a los recursos corporativos desde dispositivos no compatibles.

Al integrar Intune con ATP de Microsoft Defender, puede aprovechar las ventajas de Threat & Vulnerability Management (TVM) de ATP y [usar Intune para corregir las debilidades de los puntos de conexión que ha identificado TVM](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Ejemplo de uso de ATP de Microsoft Defender con Intune

En el siguiente ejemplo se explica cómo funcionan conjuntamente estas soluciones para ayudar a proteger la organización. En este ejemplo, ATP de Microsoft Defender e Intune ya están integrados.

Considere el caso en que alguien envía datos adjuntos de Word con código malintencionado insertado a un usuario de la organización.

- El usuario abre los datos adjuntos y habilita el contenido.
- Se inicia un ataque con privilegios elevados y un atacante desde una máquina remota tiene derechos de administrador al dispositivo de la víctima.
- Después, el atacante, accede remotamente a otros dispositivos del usuario. Esta infracción de seguridad puede afectar a toda la organización.

ATP de Microsoft Defender puede ayudar a resolver eventos de seguridad como el de este escenario.

- En nuestro ejemplo, ATP de Microsoft Defender detecta que el dispositivo ejecutó código anómalo, experimentó una elevación de privilegios de proceso, inyectó código malintencionado y emitió un shell remoto sospechoso.
- En función de estas acciones del dispositivo, ATP de Microsoft Defender [clasifica el dispositivo como de alto riesgo](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) e incluye un informe detallado de actividad sospechosa en el portal de Security Center de Microsoft Defender.

Puede integrar Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) con Microsoft Intune como solución de Mobile Threat Defense. Esta integración puede ayudarle a evitar infracciones de seguridad y a limitar su impacto en una organización.

Como tiene una directiva de cumplimiento de dispositivos de Intune para clasificar los dispositivos con un nivel de riesgo *Medio* o *Alto* como no compatibles, el dispositivo en peligro se clasifica como no compatible. Esta clasificación permite que se inicie la directiva de acceso condicional y que bloquee el acceso a los recursos corporativos desde ese dispositivo.

En el caso de los dispositivos que ejecutan Android, puede usar la directiva de Intune para modificar la configuración de ATP de Microsoft Defender en Android. Para obtener más información, consulte [Protección web de ATP de Microsoft Defender](../protect/advanced-threat-protection-manage-android.md).

## <a name="prerequisites"></a>Requisitos previos

Para usar ATP de Microsoft Defender con Intune, asegúrese de que tiene configurados los siguientes requisitos previos y listos para su uso:

- Inquilino con licencia para Enterprise Mobility + Security E3 y Windows E5 (o Microsoft 365 Enterprise E5)
- Entorno de Microsoft Intune, con dispositivos Windows 10 [administrados por Intune](../enrollment/windows-enroll.md) o dispositivos Android que también estén unidos a Azure AD.
- Entorno de [ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) que le proporcionará acceso al Centro de seguridad de Microsoft Defender (portal de ATP).

> [!NOTE]
> ATP de Microsoft Defender no es compatible con las directivas de protección de aplicaciones de Intune de iOS/iPadOS y Android.

## <a name="next-steps"></a>Pasos siguientes

- Para conectar ATP de Microsoft Defender a Intune, incorporar dispositivos y configurar directivas de acceso condicional, consulte [Configuración de ATP de Microsoft Defender en Intune](../protect/advanced-threat-protection-configure.md).

Obtenga más información en la documentación de Intune:

- [Uso de tareas de seguridad con la administración de vulnerabilidades de ATP para corregir problemas de los dispositivos](atp-manage-vulnerabilities.md)
- [Introducción a las directivas de cumplimiento de dispositivos de Intune](device-compliance-get-started.md)

Obtenga más información en la documentación de ATP de Microsoft Defender:

- [Acceso condicional de ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Panel de riesgo de ATP de Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
