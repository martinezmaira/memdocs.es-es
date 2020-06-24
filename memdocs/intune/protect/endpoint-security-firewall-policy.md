---
title: Administración de las opciones de firewall con directivas de seguridad de puntos de conexión en Microsoft Intune | Microsoft Docs
description: Configure e implemente directivas para los dispositivos administrados con la directiva de firewall de seguridad de puntos de conexión en Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
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
ms.openlocfilehash: aa518036aa99d5de003fbc56f99748267f3cc87b
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776878"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Directiva de firewall para la seguridad de puntos de conexión en Intune

Use la directiva de firewall de seguridad de puntos de conexión de Intune para configurar un firewall integrado para los dispositivos que ejecutan macOS y Windows 10.

Aunque se puede establecer la misma configuración de firewall usando perfiles de Endpoint Protection de configuración de dispositivos, los perfiles de configuración de dispositivos incluyen más categorías de configuración que no guardan relación con los firewalls y que podrían entorpecer la tarea de establecer únicamente la configuración de firewall en el entorno.

Encontrará las directivas de seguridad de puntos de conexión de los firewalls en *Administrar*, en el nodo **Seguridad de los puntos de conexión** del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Vea la [ configuración de los perfiles de firewall](../protect/endpoint-security-Firewall-profile-settings.md).

## <a name="prerequisites-for-firewall-profiles"></a>Requisitos previos de los perfiles de firewall

- Windows 10 o posterior
- Cualquier versión compatible de macOS

## <a name="firewall-profiles"></a>Perfiles de firewall

**Perfiles de macOS**:

- **Firewall de macOS**: habilite y configure las opciones del firewall integrado en macOS.

**Perfiles de Windows 10**:

- **Firewall de Microsoft Dender**: configure las opciones del Firewall de Windows Defender con seguridad avanzada. El Firewall de Windows Defender proporciona la posibilidad de filtrar el tráfico de red bidireccional basado en host de un dispositivo, y puede bloquear el tráfico de red no autorizado que entra y sale del dispositivo local.

- **Reglas del Firewall de Microsoft Defender** *(versión preliminar)* : defina reglas del Firewall pormenorizadas, incluidos puertos, protocolos, aplicaciones y redes específicos, así como permitir o bloquear el tráfico de red. Cada instancia de este perfil admite hasta 150 reglas personalizadas.

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>Combinaciones de reglas del Firewall y conflictos de directivas

Planee aplicar directivas del Firewall a un dispositivo a través de solamente una directiva. Usar una única instancia de directiva y un único tipo de directiva contribuye a evitar que dos directivas independientes apliquen configuraciones diferentes a la misma opción, lo que crearía un conflicto. Cuando existe un conflicto entre dos instancias de directiva o dos tipos de directiva que administran la misma opción con valores diferentes, la opción no se envía al dispositivo.

- Esta forma de conflicto de directivas se aplica al perfil del **Firewall de Microsoft Defender**, lo que puede entrar en conflicto con otros perfiles del Firewall de Microsoft Defender o con una configuración de firewall que se entregue por medio de otro tipo de directiva, como la configuración del dispositivo.

  Los *perfiles del Firewall de Microsoft Defender* no entran en conflicto con los *perfiles de reglas del Firewall de Microsoft Defender*.

Cuando se usan perfiles de **reglas del Firewall de Microsoft Defender**, se pueden aplicar varios perfiles de reglas al mismo dispositivo, pero cuando existen reglas diferentes para la misma cosa con distintas configuraciones, ambas se envían al dispositivo y se crea un conflicto en ese dispositivo.

- Por ejemplo, si una regla bloquea *Teams.exe* a través del firewall y una segunda regla permite *Teams.exe*, ambas reglas se entregan al cliente. Este resultado es diferente de los conflictos creados a través de otras directivas de configuración del Firewall.

Cuando las reglas de varios perfiles de reglas no entran en conflicto entre sí, los dispositivos combinan las reglas de cada perfil para crear una configuración de reglas de firewall combinada en ese dispositivo. Este comportamiento permite implementar más de las 150 reglas que cada perfil individual admite en un dispositivo concreto.

- Por ejemplo, tenemos dos perfiles de reglas del Firewall de Microsoft Defender. El primer perfil permite *Teams.exe* a través del firewall, mientras que el segundo permite *Outlook.exe* a través del firewall. Cuando un dispositivo recibe ambos perfiles, el dispositivo se configura para permitir ambas aplicaciones a través del firewall.

## <a name="next-steps"></a>Pasos siguientes

[Configuración de directivas de seguridad de puntos de conexión](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
