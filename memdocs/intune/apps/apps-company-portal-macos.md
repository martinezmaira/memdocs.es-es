---
title: Adición de la aplicación Portal de empresa para macOS
titleSuffix: Microsoft Intune
description: Agregue la aplicación Portal de empresa de macOS.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1eb64f8ed2bc67b4800a4583010dea150ade421d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914164"
---
# <a name="add-the-macos-company-portal-app"></a>Adición de la aplicación Portal de empresa de macOS

Para administrar dispositivos, instalar aplicaciones opcionales y obtener acceso a recursos protegidos con acceso condicional en dispositivos macOS con afinidad de usuario, los usuarios deben instalar e iniciar sesión en la aplicación Portal de empresa. Puede proporcionar instrucciones a los usuarios para que instalen el Portal de empresa para macOS o en dispositivos ya inscritos directamente desde Intune.

Puede usar cualquiera de las opciones siguientes para instalar la aplicación Portal de empresa para macOS:
- [Instrucciones para que los usuarios descarguen e instalen el Portal de empresa](#instruct-users-to-download-and-install-company-portal)
- [Instalación del Portal de empresa para macOS como aplicación de LOB para macOS](#install-company-portal-for-macos-as-a-macos-lob-app)
- [Instalación del Portal de empresa para macOS mediante un script de shell de macOS](#install-company-portal-for-macos-by-using-a-macos-shell-script)

Para ayudar a mantener las aplicaciones más seguras y actualizadas una vez instaladas, la aplicación Portal de empresa incluye Microsoft AutoUpdate (MAU).

> [!NOTE]
> La aplicación Portal de empresa solo se puede instalar automáticamente en dispositivos con Intune que ya están inscritos mediante la inscripción directa, o bien la automatizada. En el caso de los dispositivos personales o la inscripción manual, se debe descargar e instalar la aplicación Portal de empresa para iniciar la inscripción. Consulte [Instrucciones para que los usuarios descarguen e instalen el Portal de empresa](#instruct-users-to-download-and-install-company-portal).
## <a name="instruct-users-to-download-and-install-company-portal"></a>Instrucciones para que los usuarios descarguen e instalen el Portal de empresa

Puede indicar a los usuarios que descarguen, instalen e inicien sesión en el Portal de empresa para macOS. Para obtener instrucciones sobre cómo descargar, instalar e iniciar sesión en el Portal de empresa, consulte [Inscripción de un dispositivo macOS con Portal de empresa](../user-help/enroll-your-device-in-intune-macos-cp.md).

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>Instalación del Portal de empresa para macOS como aplicación de LOB para macOS

El Portal de empresa para macOS se puede descargar e instalar mediante la característica [Aplicaciones de LOB para macOS](lob-apps-macos.md). La versión descargada es la que siempre se instalará, y puede que tenga que actualizarse periódicamente para garantizar que los usuarios obtengan la mejor experiencia durante la inscripción inicial.

1. Descargue el Portal de empresa para macOS desde https://go.microsoft.com/fwlink/?linkid=853070. 

2. Siga las instrucciones para crear una aplicación de LOB para macOS en [Aplicaciones de LOB para macOS](lob-apps-macos.md).

> [!NOTE]
> Una vez instalada, la aplicación Portal de empresa para macOS se actualizará automáticamente con Microsoft AutoUpdate (MAU).
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>Instalación del Portal de empresa para macOS mediante un script de shell de macOS

La aplicación Portal de empresa para macOS se puede descargar e instalar con la característica [Scripts de shell de macOS](macos-shell-scripts.md). Esta opción siempre instalará la versión actual del Portal de empresa para macOS, pero no le proporcionará los informes de instalación de aplicaciones a los que pueda estar acostumbrado al implementar aplicaciones con [Aplicaciones de LOB para macOS](lob-apps-macos.md).

1. Descargue un script de ejemplo para instalar el Portal de empresa para macOS desde [Ejemplos de script de shell de Intune: Portal de empresa](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal).

2. Siga las instrucciones para implementar el script de shell de macOS con [scripts de shell de macOS](macos-shell-scripts.md). 
    - Establezca **Ejecutar el script como usuario que inició sesión** en **No** para que se ejecute en el contexto del sistema.
    - Establezca el **número máximo de reintentos en caso de error del script** en **3**.

> [!NOTE]
> El script necesitará acceso a Internet cuando se ejecute para descargar la versión actual del Portal de empresa para macOS. 
## <a name="next-steps"></a>Pasos siguientes
- Para obtener más información sobre cómo asignar aplicaciones, vea [Asignación de aplicaciones a grupos](apps-deploy.md).
- Para obtener más información sobre cómo configurar la inscripción de dispositivo automatizada, consulte [Inscripción automática de dispositivos macOS con Apple Business Manager o Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md).
- Para obtener más información sobre cómo configurar las opciones de Microsoft AutoUpdate en macOS, consulte el artículo sobre [actualizaciones para Mac](/windows/security/threat-protection/microsoft-defender-atp/mac-updates).