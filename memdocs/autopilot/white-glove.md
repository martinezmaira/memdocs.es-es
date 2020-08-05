---
title: Implementación de Windows AutoPilot para la guante blanca
description: Implementación de Windows AutoPilot para la guante blanca
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, sin intervención del socio, msfb, Intune, aprovisionamiento previo
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itproF
manager: laurawi
ms.audience: itpro
author: greg-lindsay
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: e08c69412fef2149d71c684fed6b900b88c9cb60
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757038"
---
# <a name="windows-autopilot-for-white-glove-deployment"></a>Implementación de Windows AutoPilot para la guante blanca

**Se aplica a: Windows 10, versión 1903** 

Windows AutoPilot permite a las organizaciones aprovisionar fácilmente nuevos dispositivos: aprovechar la imagen de OEM preinstalada y los controladores con un proceso sencillo que puede realizar el usuario final para ayudar a que el dispositivo esté listo para la empresa.

 ![OEM](images/wg01.png)

Windows AutoPilot también puede proporcionar un servicio de la <I>guante de blanco</I> que permite a los asociados o al personal de ti aprovisionar previamente un equipo con Windows 10 para que esté completamente configurado y listo para la empresa. Desde la perspectiva del usuario final, la experiencia controlada por el usuario de Windows AutoPilot no cambia, pero la obtención de su dispositivo a un estado totalmente aprovisionado es más rápida.

Con la **implementación de Windows AutoPilot para la guante blanca**, se divide el proceso de aprovisionamiento. Las partes que requieren mucho tiempo se realizan por ti, asociados o OEM. El usuario final simplemente completa algunos valores y directivas necesarios y, a continuación, puede empezar a usar su dispositivo.

 ![OEM](images/wg02.png)

Habilitado con Microsoft Intune en Windows 10, versión 1903 y versiones posteriores, las capacidades de implementación de la guante de blanco se basan en los [escenarios](user-driven.md)existentes de Windows AutoPilot, que admiten tanto el modo controlado por el usuario para la combinación Azure Active Directory como el modo controlado por el usuario para escenarios de unión de Azure Active Directory híbridas.

## <a name="prerequisites"></a>Prerrequisitos

Además de [los requisitos de Windows AutoPilot](windows-autopilot-requirements.md), la implementación de Windows AutoPilot para la guante blanca agrega lo siguiente:

- Se requiere Windows 10, versión 1903 o posterior.
- Una suscripción de Intune.
- Dispositivos físicos que admiten TPM 2,0 y la atestación de dispositivo; no se admiten las máquinas virtuales.  El proceso de aprovisionamiento de la guante blanca aprovecha las capacidades de Autoimplementación de Windows AutoPilot, por lo tanto los requisitos de TPM 2,0.
- Dispositivos físicos con conectividad Ethernet; No se admite la conectividad Wi-Fi debido al requisito de elegir un idioma, una configuración regional y un teclado para realizar esa conexión Wi-Fi. Si lo hace en un proceso de aprovisionamiento previo, podría impedir que el usuario elegira su idioma, configuración regional y teclado cuando reciban el dispositivo.

>[!IMPORTANT]
>Dado que el OEM o el proveedor lleva a cabo el proceso de la guante blanca, <u>no requiere acceso a la infraestructura de dominio local del usuario final</u>. Esto no es lo mismo que un escenario híbrido típico de Azure AD Unidos porque se pospone el reinicio del dispositivo. El dispositivo se vuelve a sellar antes del momento en que se espera la conectividad con un controlador de dominio y se Contacta con la red del dominio cuando el usuario final vuelve a desempaquetar el dispositivo local.

## <a name="preparation"></a>Preparación

Los dispositivos programados para el aprovisionamiento de la guante blanca se registran para el piloto automático mediante el proceso de registro normal. 

Para estar listo para probar la implementación de Windows AutoPilot para la guante blanca, asegúrese de que primero pueda usar correctamente los escenarios existentes basados en el usuario de Windows AutoPilot:

- Combinación de Azure AD controlada por el usuario.  Los dispositivos se pueden implementar mediante Windows AutoPilot y estar Unidos a un inquilino de Azure Active Directory.
- Controlado por el usuario con Azure AD híbrido join.  Los dispositivos se pueden implementar mediante Windows AutoPilot y estar Unidos a un dominio de Active Directory local y, a continuación, registrarse con Azure Active Directory para habilitar las características de Azure AD híbrido join.

Si no se pueden completar estos escenarios, la implementación de Windows AutoPilot para la guante blanca tampoco se realizará correctamente, ya que se basa en estos escenarios.

Para habilitar la implementación en blanco de la guantera, el cliente o el administrador de TI debe configurar una configuración de perfil AutoPilot adicional a través de su cuenta de Intune, antes de comenzar el proceso de la guante blanca en la instalación del servicio de aprovisionamiento:

 ![permitir la guante blanca](images/allow-white-glove-oobe.png)

El proceso de aprovisionamiento previo de implementación de Windows AutoPilot para la guante blanca aplicará todas las directivas de destino de dispositivos de Intune.  Esto incluye los certificados, las plantillas de seguridad, la configuración, las aplicaciones, etc., todo ello dirigido al dispositivo.  Además, también se instalarán las aplicaciones (Win32 o LOB) que estén configuradas para instalarse en el contexto de dispositivo y destinadas al usuario que se ha asignado previamente al dispositivo AutoPilot. Asegúrese de no tener como destino aplicaciones de Win32 y LOB en el mismo dispositivo. 

> [!NOTE]
> Seleccione el modo de idioma como usuario especificado en perfiles de AutoPilot para garantizar un acceso sencillo en el modo de aprovisionamiento de la guante blanca. La fase de técnico de la guante blanca instalará todas las aplicaciones de destino del dispositivo, así como todas las aplicaciones de contexto de dispositivo que tengan como destino el usuario asignado. Si no hay ningún usuario asignado, solo instalará las aplicaciones de destino del dispositivo. No se aplicarán otras directivas de destino de usuario hasta que el usuario inicie sesión en el dispositivo. Para comprobar estos comportamientos, asegúrese de crear las aplicaciones y las directivas adecuadas para los dispositivos y los usuarios.

## <a name="scenarios"></a>Escenarios

La implementación de Windows AutoPilot para la guante blanca es compatible con dos escenarios distintos:
- Implementaciones controladas por el usuario con Azure AD join.  El dispositivo se unirá a un inquilino de Azure AD.
- Implementaciones controladas por el usuario con Unión a Azure AD híbrido.  El dispositivo se unirá a un dominio de Active Directory local y se registrará de forma independiente en Azure AD.
Cada uno de estos escenarios consta de dos partes, un flujo del técnico y un flujo de usuario.  En un nivel alto, estas partes son las mismas para Azure AD join y Azure AD híbrido join; el usuario final suele ver las diferencias en los pasos de autenticación.

### <a name="technician-flow"></a>Flujo del técnico

Una vez que el cliente o el administrador de ti ha dirigido todas las aplicaciones y la configuración que desean para sus dispositivos a través de Intune, el técnico de la guante blanca puede comenzar el proceso de la guante blanca.  El técnico podría ser miembro del personal de ti, de un asociado de servicios o de un OEM: cada organización puede decidir quién debe realizar estas actividades. Independientemente del escenario, el proceso que va a realizar el técnico es el mismo:
- Arranque el dispositivo (con las SKU de Windows 10 Pro, Enterprise o Education, versión 1903 o posterior).
- En la primera pantalla de OOBE (que podría ser una pantalla de selección de idioma o de configuración regional), no haga clic en **siguiente**.  En su lugar, presione la tecla de Windows cinco veces para ver un cuadro de diálogo de opciones adicionales.  En esa pantalla, elija la opción de **aprovisionamiento de Windows AutoPilot** y, a continuación, haga clic en **continuar**.

  ![choice](images/choice.png)

- En la pantalla **configuración de Windows AutoPilot** , se mostrará información sobre el dispositivo:
    - El perfil AutoPilot asignado al dispositivo.
    - El nombre de la organización para el dispositivo.
    - Usuario asignado al dispositivo (si hay alguno).
    - Un código QR que contiene un identificador único para el dispositivo, útil para buscar el dispositivo en Intune para realizar los cambios necesarios en la configuración (por ejemplo, asignar un usuario, agregar el dispositivo a los grupos adicionales necesarios para la aplicación o el destinatario de la Directiva).
    - **Nota**: los códigos QR se pueden analizar mediante una aplicación complementaria, que también configurará el dispositivo para especificar a quién pertenece.  El equipo de AutoPilot ha publicado en GitHub un [ejemplo de código abierto de la aplicación complementaria](https://github.com/Microsoft/WindowsAutopilotCompanion) que se integra con Intune mediante el Graph API.
- Valide la información que se muestra.  Si se necesitan cambios, haga clic en **Actualizar** para volver a descargar los detalles del perfil AutoPilot actualizado.

  ![destino](images/landing.png)

- Haga clic en **aprovisionar** para comenzar el proceso de aprovisionamiento.

Si el proceso de aprovisionamiento previo se completa correctamente:
- Se mostrará una pantalla de estado verde con información sobre el dispositivo, incluidos los mismos detalles presentados anteriormente (por ejemplo, el perfil AutoPilot, el nombre de la organización, el usuario asignado, el código QR), así como el tiempo transcurrido para los pasos previos al aprovisionamiento.
 ![blanco-guante-resultado](images/white-glove-result.png)
- Haga clic en volver a **sellar** para apagar el dispositivo.  En ese momento, el dispositivo puede enviarse al usuario final.

>[!NOTE]
>El flujo de técnicos hereda el comportamiento del [modo de auto-implementación](self-deploying.md). Según la documentación del modo de auto-implementación, se usa la página estado de inscripción para almacenar el dispositivo en un estado de aprovisionamiento y evitar que el usuario continúe con el escritorio después de la inscripción, pero antes de que se realice la aplicación del software y la configuración. Por lo tanto, si la página estado de inscripción está deshabilitada, el botón volver a sellar puede aparecer antes de que el software y la configuración se aplique, lo que le permite pasar al flujo de usuario antes de que se complete el aprovisionamiento del flujo de técnicos. La pantalla verde valida que la inscripción se ha realizado correctamente, no que el flujo del técnico se ha completado necesariamente.

Si se produce un error en el proceso de aprovisionamiento previo:
- Se mostrará una pantalla de estado rojo con información sobre el dispositivo, incluidos los mismos detalles presentados anteriormente (por ejemplo, el perfil AutoPilot, el nombre de la organización, el usuario asignado, el código QR), así como el tiempo transcurrido para los pasos previos al aprovisionamiento.
- Los registros de diagnóstico se pueden recopilar desde el dispositivo y, a continuación, se pueden restablecer para volver a iniciar el proceso.

### <a name="user-flow"></a>Flujo de usuario

Si el proceso de aprovisionamiento previo se ha completado correctamente y el dispositivo se ha resellado, se puede entregar al usuario final para completar el proceso normal controlado por el usuario de Windows AutoPilot.  Realizarán un conjunto estándar de pasos:

- Encienda el dispositivo.
- Seleccione el idioma, la configuración regional y la distribución del teclado adecuados.
- Conectarse a una red (si se usa Wi-Fi).  Siempre se requiere acceso a Internet.  Si usa Unión a Azure AD híbrido, también debe haber conectividad con un controlador de dominio.
- En la pantalla de inicio de sesión con marca, escriba las credenciales del Azure Active Directory del usuario.
- Si usa Unión a Azure AD híbrido, el dispositivo se reiniciará; después del reinicio, escriba las credenciales del Active Directory del usuario.
- Las directivas y las aplicaciones adicionales se entregarán en el dispositivo, tal y como realiza el seguimiento de la página de estado de inscripción (ESP).  Una vez completado, el usuario podrá tener acceso al escritorio.

## <a name="related-topics"></a>Temas relacionados

[Vídeo de la guante blanca](https://youtu.be/nE5XSOBV0rI)
