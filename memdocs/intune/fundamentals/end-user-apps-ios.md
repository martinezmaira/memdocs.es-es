---
title: Cómo obtienen sus aplicaciones los usuarios de iOS/iPadOS
description: Métodos para hacer que las aplicaciones iOS/iPadOS estén disponibles para los usuarios finales
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "79344095"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>Cómo obtienen sus aplicaciones los usuarios de iOS/iPadOS

Lea esta información para comprender cómo y dónde obtienen los usuarios finales las aplicaciones que se distribuyen a través de Microsoft Intune.

**Aplicaciones obligatorias**: son las aplicaciones que exige el administrador y que se instalan en el dispositivo con intervención mínima del usuario, según la plataforma.

**Aplicaciones disponibles**: son las aplicaciones que se proporcionan en la lista de aplicaciones de portal de empresa y que un usuario puede instalar si quiere.

**Aplicaciones administradas**: son aplicaciones que se pueden administrar mediante directivas y que se han "encapsulado" con Intune o se han creado con el kit de desarrollo de software (SDK) para aplicaciones de Intune. Estas aplicaciones pueden administrarse mediante Intune y las directivas de protección de aplicaciones pueden aplicarse a estas.

**Aplicaciones no administradas**: las aplicaciones que los usuarios pueden descargar desde el App Store de iOS/iPadOS que no están integradas con el SDK para aplicaciones de Intune. Intune no tiene ningún control sobre la distribución, la administración o el borrado selectivo de estas aplicaciones.  

Los usuarios inscritos obtienen sus aplicaciones tocando en los iconos siguientes de la pantalla de aplicaciones de la aplicación del Portal de empresa:

- **Todas las aplicaciones** apunta a una lista de todas las aplicaciones en la pestaña TODO del [sitio web del Portal de empresa](https://portal.manage.microsoft.com).

- **Las aplicaciones destacadas** llevarán a los usuarios a la pestaña DESTACADOS del sitio web del Portal de empresa.

- **Categorías** apunta a la pestaña CATEGORÍAS del sitio web del Portal de empresa.

![Pantalla de aplicaciones del Portal de empresa de iOS](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

Para más información sobre cómo agregar aplicaciones, vea [Agregar una aplicación a Microsoft Intune](../apps/apps-add.md).

## <a name="app-management-takeover"></a>Toma de control de la administración de aplicaciones
Si una aplicación ya está instalada en el dispositivo de un usuario final, el dispositivo iOS o iPadOS muestra una alerta para permitir la administración de la aplicación por parte de su organización. El usuario final debe permitir que la organización asuma la administración de la aplicación para de que se puedan aplicar las configuraciones de aplicaciones en un dispositivo administrado. Si el usuario cancela la alerta, la alerta aparecerá periódicamente mientras el dispositivo se administre y la aplicación se asigne.  


![Imagen de la alerta de cambio de la administración de aplicaciones donde se muestran opciones para cancelar y administrar](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>Vea también  

[Cómo obtienen sus aplicaciones los usuarios de Android](end-user-apps-android.md)

[Cómo obtienen sus aplicaciones los usuarios de Windows](end-user-apps-windows.md)
