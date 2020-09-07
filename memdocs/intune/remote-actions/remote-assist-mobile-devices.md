---
title: Asistencia remota para dispositivos móviles administrados por Intune
description: Puede usar cuatro opciones diferentes para asistir de forma remota a los usuarios acerca de sus dispositivos móviles.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b501ab979d87461067018f789d6d096020d3819e
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057426"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Asistencia remota para dispositivos móviles administrados por el Administrador de puntos de conexión de Microsoft

Hay cuatro opciones disponibles para administrar de forma remota los dispositivos administrados por el Administrador de puntos de conexión de Microsoft:

- [Microsoft Teams](https://products.office.com/microsoft-teams/) es el centro para el trabajo en equipo en el que puede conversar, reunirse y colaborar con independencia de dónde se encuentre.
- [Asistencia rápida](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) es una aplicación de Windows 10 que permite a dos personas compartir un dispositivo a través de una conexión remota.
- [TeamViewer](https://www.teamviewer.com/) es un programa de terceros que se adquiere por separado. Proporciona un conjunto completo de funciones de acceso remoto y soporte técnico. La integración de Intune y [TeamViewer](teamviewer-support.md) habilita la compatibilidad remota mediante TeamViewer y el conector se administra directamente en Intune.
- El [control remoto](/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) se incluye en Microsoft Endpoint Configuration Manager. Se usa para administrar, proporcionar asistencia o ver cualquier equipo de grupo de trabajo o equipo unido a un dominio de forma remota.

| Características, plataformas, licencias | **Teams** | Asistencia rápida | TeamViewer (Intune) | Control remoto (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Vista y control remotos |![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Chat |![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Transferencia de archivos |![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Acceso de administrador elevado |||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Acceso desatendido |||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Control remoto simultáneo |![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Compatibilidad con varios usuarios |||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Acciones remotas ||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Compatibilidad por Internet |![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Informes de auditoría |![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Compatibilidad con todas las plataformas (Windows, iOS, Android, macOS) |![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Integrado con Windows 10: no se requiere ninguna aplicación adicional ||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Requiere que el dispositivo sea administrado conjuntamente por Configuration Manager e Intune ||||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Requiere licencias adicionales\* |![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)||![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|![Marca de verificación](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Teams requiere licencias de Microsoft 365. El uso de TeamViewer e Intune requiere una licencia de TeamViewer y de Intune. El control remoto es una característica de Configuration Manager y requiere licencias de Configuration Manager.
