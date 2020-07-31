---
title: Supervisión de la integración de Advanced Threat Protection (ATP) de Microsoft Defender en Microsoft Intune - Azure | Microsoft Docs
description: Supervise Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) con Intune, incluido el estado de incorporación y cumplimiento de los dispositivos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264570"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>Supervisión del estado del dispositivo al integrar ATP de Microsoft Defender con Intune

Al integrar Microsoft Intune y Advanced Threat Protection (ATP) de Microsoft Defender, puede ver información sobre el cumplimiento de los dispositivos y su incorporación en el centro de administración de Microsoft Endpoint Manager.

## <a name="monitor-device-compliance"></a>Supervisión del cumplimiento del dispositivo

Supervise el estado de los dispositivos que tienen la directiva de cumplimiento de ATP de Microsoft Defender.

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Supervisar** > **Cumplimiento de directiva**.

3. Busque la directiva de ATP de Microsoft Defender en la lista y vea qué dispositivos son compatibles o no compatibles.

También puede usar el informe *Operativo* en dispositivos no conformes desde la misma ubicación:

- Seleccione **Dispositivos** > **Monitor** > **Dispositivos no conformes**.

Para más información sobre los informes, consulte [Informes de Intune](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Ver estado de incorporación

Para ver el estado de incorporación de todos los dispositivos administrados por Intune, vaya a **Seguridad de punto de conexión** > **ATP de Microsoft Defender**. En esta página, también puede crear un perfil de configuración de dispositivos para incorporar más dispositivos a ATP de Microsoft Defender.

## <a name="next-steps"></a>Pasos siguientes

[Aplicación del cumplimiento de ATP de Microsoft Defender con acceso condicional en Intune](../protect/advanced-threat-protection.md)
