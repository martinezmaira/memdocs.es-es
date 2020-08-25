---
title: Adición y asignación de la aplicación Portal de empresa de Windows 10 para dispositivos aprovisionados con Autopilot
titleSuffix: Microsoft Intune
description: Agregue y asigne la aplicación Portal de empresa de Windows 10 a Intune para dispositivos aprovisionados con Autopilot.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559528"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Adición y asignación de la aplicación Portal de empresa de Windows 10 para dispositivos aprovisionados con Autopilot

Para administrar dispositivos e instalar aplicaciones, los usuarios pueden usar la aplicación Portal de empresa. Puede asignar la aplicación Portal de empresa de Windows 10 directamente desde Intune. 

## <a name="prerequisites"></a>Requisitos previos

En el caso de los dispositivos Windows 10 aprovisionados con Autopilot, se recomienda asociar la cuenta de Microsoft Store para Empresas con Intune. Para obtener más información, vea [Administración de aplicaciones compradas por volumen en Microsoft Store para Empresas con Microsoft Intune](windows-store-for-business.md).

Puede optar por instalar la aplicación del **Portal de empresa (sin conexión)** mediante los pasos siguientes. La aplicación del Portal de empresa se instalará en el contexto del dispositivo cuando se asigne al grupo de Autopilot y se instalará en el dispositivo antes de que el usuario inicie sesión.

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>Configuración de las opciones de Store para mostrar la aplicación sin conexión

1. Inicie sesión en [Microsoft Store para Empresas](https://www.microsoft.com/business-store) con la cuenta de administrador.
2. Haga clic en la pestaña **Administrar**, situada cerca de la parte superior de la ventana.
3. En el panel de la izquierda, seleccione **Configuración**.
4. En **Experiencia de compra**, establezca **Mostrar aplicaciones sin conexión** en **Activado**.  
   Se muestran las aplicaciones con licencia sin conexión.

## <a name="get-the-offline-company-portal-app-from-the-store"></a>Obtención de la aplicación del Portal de empresa sin conexión de Store

1. Busque y seleccione la aplicación **Portal de empresa**.
2. Establezca **Tipo de licencia** en **Sin conexión**.
3. Seleccione **Obtener la aplicación** para adquirir y agregar la aplicación Portal de empresa sin conexión al inventario.
   Para que la aplicación aparezca en Intune, debe esperar a que se complete la programación de sincronización, o bien realizar una sincronización manual desde el Centro de administración de Microsoft Endpoint Manager.

## <a name="manually-sync-company-portal-app-with-intune"></a>Sincronización manual de la aplicación del Portal de empresa con Intune

1. Inicie sesión en el  [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431)  con la cuenta de administrador.
2. Seleccione **Administración de inquilinos** > **Conectores y tokens** > **Microsoft Store para Empresas**.
3. Haga clic en **Habilitar**.
4. Si aún no lo ha hecho, haga clic en el vínculo para registrarse en la Tienda Microsoft para Empresas y asocie la cuenta como se ha descrito anteriormente.
5. En la lista desplegable **Idioma**, seleccione el idioma en el que las aplicaciones de Microsoft Store para Empresas se muestran en Azure Portal. Independientemente del idioma en el que se muestren, se instalan en el idioma del usuario final si esa versión está disponible.
6. Haga clic en **Sincronizar** para que las aplicaciones que ha adquirido en la Microsoft Store aparezcan en Intune.

## <a name="assign-the-company-portal-app"></a>Asignación de la aplicación Portal de empresa

1. Inicie sesión en el  [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431)  con la cuenta de administrador.
2. Seleccione **Aplicaciones** > **Windows**.
3. En la lista de aplicaciones de Windows, seleccione **Portal de empresa (sin conexión)** .
4. [Asigne](apps-deploy.md) la aplicación del Portal de empresa como una aplicación necesaria a los grupos de dispositivos AutoPilot seleccionados.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener más información sobre cómo asignar aplicaciones, vea [Asignación de aplicaciones a grupos](apps-deploy.md).

