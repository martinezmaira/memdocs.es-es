---
title: Configuración de la red cableada 802.1x para dispositivos macOS en Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Cree o agregue un perfil de configuración de dispositivos de red cableada para dispositivos y equipos de escritorio macOS. Vea las diferentes configuraciones, agregue certificados, elija un tipo de EAP y seleccione un método de autenticación en Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095803"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>Adición y uso de la configuración de redes cableadas en dispositivos macOS en Microsoft Intune

Muchas organizaciones usan redes cableadas para proporcionar acceso de red a los equipos de escritorio. Microsoft Intune incluye configuraciones integradas que se pueden implementar en los usuarios y dispositivos macOS de la organización. Este grupo de configuración se denomina "perfil". En el perfil, puede incluir valores de configuración comunes, como la interfaz de red, los tipos de EAP aceptados y la configuración de confianza de servidor.

Cuando el perfil está listo, se puede asignar a usuarios y grupos diferentes. Una vez asignado, los usuarios acceden a la red cableada de la organización sin tener que configurarla ellos mismos.

Como parte de la solución de administración de dispositivos móviles (MDM), use esta característica para crear perfiles de 802.1x con el fin de administrar redes cableadas. Después, implemente estas redes cableadas en los dispositivos macOS.

Esta característica se aplica a:

- macOS

Por ejemplo, tiene una red cableada denominada **Red cableada de Contoso**. Quiere configurar todos los dispositivos de escritorio macOS de modo que se conecten a esta red. Este es el proceso:

1. Cree un perfil de red cableada que contenga la configuración para conectarse a la **red cableada de Contoso**.
2. Asigne el perfil a un grupo que incluya todos los usuarios de equipos de escritorio macOS. Para obtener recomendaciones sobre el uso de tipos de grupos, vea [Grupos de usuarios y grupos de dispositivos](device-profile-assign.md#user-groups-vs-device-groups).
3. En los dispositivos de escritorio, los usuarios encontrarán la **red cableada de Contoso** en la lista de redes. Pueden conectarse a ella fácilmente con el método de autenticación de su elección.

En este artículo se enumeran los pasos para crear un perfil de red cableada. También se incluye un vínculo que describe las distintas configuraciones.

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
3. Escriba las propiedades siguientes:

    - **Plataforma**: seleccione **macOS**.
    - **Perfil**: seleccione **Red cableada**.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. Asígnele un nombre a los perfiles para que pueda identificarlos de manera sencilla más adelante. Por ejemplo, un buen nombre de perfil sería **Perfil de red cableada para toda la empresa en dispositivos macOS**.
    - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.
7. En **Opciones de configuración**, seleccione la interfaz de red y elija el tipo de Protocolo de autenticación extensible (EAP). Para una lista de todas las configuraciones, y lo que hacen, consulte:

    - [macOS](wired-network-settings-macos.md)

8. Seleccione **Siguiente**.
9. En **Asignaciones**, seleccione los grupos de usuarios o de dispositivos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](device-profile-assign.md).

    Seleccione **Siguiente**.

10. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

> [!TIP]
> Si usa la autenticación basada en certificados para el perfil de red cableada, implemente el perfil de red cableada, el de certificado y el perfil raíz de confianza en los mismos grupos. Esta implementación garantiza que cada dispositivo pueda reconocer la legitimidad de la entidad de certificación. Para obtener más información, vea [Configuración de certificados con Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Pasos siguientes

El perfil se crea, pero puede que no haga nada. Asegúrese de [asignar el perfil](device-profile-assign.md) y [supervisar el estado](device-profile-monitor.md).
