---
title: Configuración de Windows Information Protection en Microsoft Intune
titleSuffix: Microsoft Intune
description: Obtenga información sobre la configuración de Microsoft Intune que puede usar para administrar Windows Information Protection.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18f353a6888ee30af2371ebb5a7f705ac0c060f0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349347"
---
# <a name="how-to-configure-windows-information-protection-in-microsoft-intune"></a>Configuración de Windows Information Protection en Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Con el aumento de los dispositivos propiedad de los empleados en la empresa, también aumenta el riesgo de pérdidas de datos accidentales a través de aplicaciones y servicios, como el correo electrónico, las redes sociales y la nube pública, que están fuera del control de la empresa. Por ejemplo, un empleado envía las imágenes de ingeniería más recientes desde una cuenta de correo electrónico personal, copia y pega la información del producto en un tweet o guarda un informe de ventas en curso en un almacenamiento en la nube pública.

**Windows Information Protection** ayuda a proporcionar protección ante esta pérdida potencial de datos sin interferir como contrapartida en la experiencia de empleado. También ayuda a proteger los datos y aplicaciones empresariales ante las pérdidas de datos accidentales en dispositivos propiedad de la empresa y personales que los empleados llevan al trabajo sin necesidad de realizar cambios en su entorno u otras aplicaciones.

Esta directiva de Intune administra la lista de aplicaciones protegidas por Windows Information Protection, las ubicaciones de red de la empresa, el nivel de protección y la configuración de cifrado.

>[!NOTE]
> Para usar la aplicación Portal de empresa de Windows 10 con Windows Information Protection, debe agregar la aplicación Portal de empresa en el modo **Exento** de Windows Information Protection. 

Para obtener más información, vea:
- [Protege los datos de tu empresa con Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
- [Crear una directiva de Windows Information Protection (WIP) con Microsoft Intune](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune)
- [Crear una directiva Windows Information Protection (WIP) con MDM usando el portal de Azure de Microsoft Intune](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune-azure)
- [Crear una directiva Windows Information Protection (WIP) con MAM usando el portal de Azure de Microsoft Intune](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure)
