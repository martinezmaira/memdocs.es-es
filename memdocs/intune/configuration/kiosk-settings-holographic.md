---
title: 'Configuración de pantalla completa para Windows Holographic for Business en Microsoft Intune: Azure | Microsoft Docs'
description: Configure los dispositivos con Windows Holographic for Business como pantallas completas con una sola aplicación y con varias, personalice el menú Inicio, agregue aplicaciones, muestre la barra de tareas y configure un explorador web en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d54e02c7bb88354ec59a9a8ce780ff559377466
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556105"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Configuración de dispositivos con Windows Holographic for Business para ejecutarse como una pantalla completa en Intune

En los dispositivos con Windows Holographic for Business, puede configurar estos dispositivos para que se ejecuten en modo de pantalla completa con una sola aplicación o con varias. Algunas características no se admiten en Windows Holographic for Business.

En este artículo se enumeran y describen las distintas opciones de configuración que puede controlar en los dispositivos Windows Holographic for Business. Como parte de su solución de administración de dispositivos móviles (MDM), use estas opciones de configuración para configurar sus dispositivos Windows Holographic for Business para que se ejecuten en pantalla completa.

Como administrador de Intune, puede crear y asignar estas opciones de configuración a los dispositivos.

Para más información sobre la característica de pantalla completa de Windows en Intune, consulte la [configuración de las opciones de pantalla completa](kiosk-settings.md).

## <a name="before-you-begin"></a>Antes de comenzar

- [Cree un perfil de configuración de dispositivo VPN de Windows 10](kiosk-settings.md#create-the-profile).

  Al crear un perfil de configuración de dispositivo de quiosco de Windows 10, hay más opciones de configuración de las que se enumeran en este artículo. La configuración de este artículo es compatible con dispositivos Windows Holographic for Business.

- Este perfil de pantalla completa está directamente relacionado con el perfil de restricciones de dispositivo que se crea mediante la [Configuración de quiosco de Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser). En resumen:

  1. Cree este perfil de pantalla completa para ejecutar el dispositivo en pantalla completa.
  2. Cree el [perfil de restricciones de dispositivo](device-restrictions-windows-holographic.md#microsoft-edge-browser) y configure opciones y características específicas que se permiten en Microsoft Edge.

> [!IMPORTANT]
> Asegúrese de asignar este perfil de pantalla completa a los mismos dispositivos que su [perfil de Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>Pantalla completa con aplicación única

Solo se ejecuta una aplicación en el dispositivo. Cuando el usuario inicia sesión, se inicia una aplicación concreta. Este modo también evita que el usuario abra nuevas aplicaciones o modifique la aplicación en ejecución.

- **Tipo de inicio de sesión de usuario**: Seleccione el tipo de cuenta que ejecuta la aplicación. Las opciones son:

  - **Inicio de sesión automático (Windows 10, versión 1803 y versiones posteriores)** : no se admite en Windows Holographic for Business.
  - **Cuenta de usuario local**: escriba la cuenta de usuario local (en el dispositivo). O bien, escriba una cuenta Microsoft (MSA) asociada a la aplicación de pantalla completa. La cuenta que especifique inicia sesión en la pantalla completa.

    En el caso de quioscos en entornos de acceso público, se debe usar un tipo de usuario con privilegios mínimos.

- **Tipo de aplicación**: Seleccione **Agregar aplicación de Store**.

  - **Aplicación para ejecutar en modo de pantalla completa**: Seleccione una aplicación de la lista.

    ¿No aparece ninguna aplicación? Agregue algunas siguiendo los pasos descritos en [Aplicaciones cliente](../apps/apps-add.md).

## <a name="multi-app-kiosk"></a>Pantalla completa con varias operaciones

Las aplicaciones en este modo están disponibles en el menú Inicio. Estas aplicaciones son las únicas que el usuario puede abrir. Si una aplicación tiene una dependencia de otra, ambas deben estar incluidas en la lista de aplicaciones permitidas.

- **Destino de Windows 10 en dispositivos en modo S**: Seleccione **No**. El modo S no se admite en Windows Holographic for Business.

- **Tipo de inicio de sesión de usuario**: agregue una o varias cuentas de usuario que puedan usar las aplicaciones que agregue. Las opciones son:

  - **Inicio de sesión automático (Windows 10, versión 1803 y versiones posteriores)** : no se admite en Windows Holographic for Business.
  - **Cuentas de usuarios locales**: **añada** la cuenta de usuario local (en el dispositivo). La cuenta que especifique inicia sesión en la pantalla completa.
  - **Azure AD user or group (Windows 10, version 1803 and later)** [Usuario o grupo de Azure AD (Windows 10, versión 1803 y posteriores)]: se requieren credenciales de usuario para iniciar sesión en el dispositivo. Seleccione **Agregar** para elegir usuarios o grupos de Azure AD en la lista. Puede seleccionar varios usuarios y grupos. Elija **Seleccionar** para guardar los cambios.
  - **Visitante de HoloLens**: la cuenta de visitante es una cuenta de invitado que no requiere ninguna credencial de usuario ni autenticación, como se describe en [Conceptos del modo de equipo compartido](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Exploradores y aplicaciones**: agregue las aplicaciones que se van a ejecutar en el dispositivo de pantalla completa. Recuerde que puede agregar varias aplicaciones.

  - **Exploradores**
    - **Agregar Microsoft Edge**: se agrega Microsoft Edge a la cuadrícula de aplicaciones y todas las aplicaciones se pueden ejecutar en esta pantalla completa. Seleccione el Tipo de modo de quiosco de Microsoft Edge:

      - **Modo normal (versión completa de Microsoft Edge)** : Se ejecuta una versión completa de Microsoft Edge con todas las características de exploración. Los datos de usuario y el estado se guardan entre sesiones.
      - **Exploración pública (InPrivate)** : se ejecuta una versión de varias pestañas de InPrivate de Microsoft Edge con una experiencia adaptada a los quioscos que se ejecutan en modo de pantalla completa.

      Para más información sobre estas opciones, vea [Implementar la pantalla completa de Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Esta valor habilita el explorador de Microsoft Edge en el dispositivo. Para configurar opciones específicas de Microsoft Edge, cree un perfil de restricciones de dispositivos (**Dispositivos** > **Perfiles de configuración** > **Crear perfil** > **Windows 10** para la plataforma > **Restricciones de dispositivos** > **Explorador Microsoft Edge**). [Explorador de Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser) muestra y describe las opciones disponibles.

    - **Agregar explorador del Quiosco**: no se admite en Windows Holographic for Business.

  - **Aplicaciones**
    - **Agregar aplicación de la tienda**: Seleccione una aplicación existente que haya agregado o implementado en Intune como [Aplicaciones cliente](../apps/apps-add.md), incluidas las aplicaciones LOB. Si no tiene ninguna aplicación enumerada, Intune admite muchos [tipos de aplicación](../apps/apps-add.md) que el usuario [agrega a Intune](../apps/store-apps-windows.md).
    - **Agregar aplicación Win32**: no se admite en Windows Holographic for Business.
    - **Agregar por AUMID**: use esta opción para agregar aplicaciones de Windows de bandeja de entrada, como el Bloc de notas o la Calculadora. Escriba las siguientes propiedades:

      - **Nombre de la aplicación**: Necesario. Escriba un nombre para la aplicación.
      - **Identificador de modelo del usuario de la aplicación (AUMID)** : Necesario. Escriba el identificador de modelo de usuario de aplicación (AUMID) de la aplicación de Windows. Para obtener este identificador, vea [Find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) (Buscar el identificador de modelo de usuario de aplicación de una aplicación instalada).

    - **Inicio automático**: Opcional. Después de agregar las aplicaciones y el explorador, seleccione una aplicación o un explorador que se abra automáticamente cuando el usuario inicie sesión. Solo puede iniciarse automáticamente una única aplicación o explorador.
    - **Tamaño de icono**: Necesario. Después de agregar las aplicaciones, seleccione un tamaño de icono de aplicación pequeño, mediano, ancho o grande.

- **Usar diseño de inicio alternativo**: elija **Sí** para especificar un archivo XML que describa el modo en que las aplicaciones aparecen en el menú Inicio, incluido el orden de estas. Use esta opción si necesita personalizar más el menú Inicio. En [Personalizar y exportar el diseño de la pantalla Inicio](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens) se proporcionan algunas instrucciones y se incluye un archivo XML específico para dispositivos con Windows Holographic for Business.

- **Barra de tareas de Windows**: no se admite en Windows Holographic for Business.
- **Permitir acceso a la carpeta de descargas**: no se admite en Windows Holographic for Business.
- **Especificar una ventana de mantenimiento para los reinicios de aplicaciones**: no se admite en Windows Holographic for Business.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md).

También puede crear perfiles de pantalla completa para dispositivos [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) y [Windows 10 y versiones posteriores](kiosk-settings-windows.md).
