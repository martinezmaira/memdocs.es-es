---
title: 'Configuración de pantalla completa para dispositivos Windows y Holographic en Microsoft Intune: Azure | Microsoft Docs'
description: Configure los dispositivos con Windows 10 (y versiones posteriores) y Windows Holographic for Business como pantallas completas con una sola aplicación y con varias, personalice el menú Inicio, agregue aplicaciones, muestre la barra de tareas y configure un explorador web en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9be644a47a361cf29e7b7132b2c87a4921553ea
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989438"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Configuración de dispositivos con Windows 10 y Windows Holographic for Business para ejecutarse como una pantalla completa dedicada con Intune

En dispositivos con Windows 10, use Intune para ejecutar los dispositivos como una pantalla completa, lo que a veces se conoce como un dispositivo dedicado. Un dispositivo en pantalla completa puede ejecutar una aplicación o varias. Puede mostrar y personalizar un menú Inicio, agregar diferentes aplicaciones, incluidas las aplicaciones Win32, agregar una página principal específica a un explorador web y mucho más. 

Esta característica se aplica a:

- Windows 10 y versiones posteriores
- Windows Holographic for Business

Para crear perfiles de quiosco para otras plataformas, consulte [Administrador de dispositivos Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) y [iOS/iPadOS](device-restrictions-ios.md#kiosk).

Intune admite un perfil de quiosco por dispositivo. Si necesita varios perfiles de quiosco en un único dispositivo, puede usar un [OMA-URI personalizado](custom-settings-windows-10.md).

Intune usa "perfiles de configuración" para crear y personalizar estas configuraciones para las necesidades de su organización. Después de agregar estas características a un perfil, inserte o implemente estas configuraciones en grupos de la organización.

En este artículo se muestra cómo crear un perfil de configuración de dispositivo. Para una lista de todas las configuraciones, y lo que hacen, consulte [Windows 10 kiosk settings](kiosk-settings-windows.md) (Configuración de pantalla de Windows 10) y [Windows Holographic for Business kiosk settings](kiosk-settings-holographic.md) (Configuración de pantalla completa de Windows Holographic for Business).

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

   - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
   - **Perfil**: seleccione **Pantalla completa**.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil.
   - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.
7. En **Opciones de configuración** > **Seleccionar un modo de pantalla completa**, elija el tipo de pantalla completa compatible con la directiva. Las opciones son:

    - **Sin configurar** (valor predeterminado): Intune no cambia ni actualiza esta configuración. la directiva no habilita la pantalla completa.
    - **Pantalla completa con aplicación única**: el dispositivo se ejecuta como una cuenta de usuario único y la bloquea para una única aplicación de la Tienda. Así que cuando el usuario inicia sesión, se inicia una aplicación concreta. Este modo también evita que el usuario abra nuevas aplicaciones o modifique la aplicación en ejecución.
    - **Pantalla completa con varias aplicaciones**: el dispositivo ejecuta varias aplicaciones de la Tienda, aplicaciones Win32 o aplicaciones de Windows de bandeja de entrada mediante el identificador de modelo del usuario de la aplicación (AUMID). En el dispositivo solo están disponibles las aplicaciones agregadas.

        La ventaja de un quiosco con varias aplicaciones, o un dispositivo para un propósito fijo, es que proporciona una experiencia fácil de entender para los usuarios, ya que solo acceden a las aplicaciones que necesitan. Además, se quitan de la vista las aplicaciones que no necesitan.

    Para una lista de todas las configuraciones, y lo que hacen, consulte:

      - [Configuración de pantalla completa en Windows 10](kiosk-settings-windows.md)
      - [Configuración de pantalla completa en Windows Holographic for Business](kiosk-settings-holographic.md)

8. Seleccione **Siguiente**.

9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione los usuarios o el grupo de usuarios que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

La próxima vez que se registre cada dispositivo, se aplicará la directiva.

## <a name="next-steps"></a>Pasos siguientes

Después de [asignar el perfil](device-profile-assign.md), [supervise su estado](device-profile-monitor.md).

Puede crear perfiles de pantalla completa para dispositivos que ejecutan las siguientes plataformas:

- [Administrador de dispositivos Android](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)
- [Windows 10 y versiones posteriores](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
