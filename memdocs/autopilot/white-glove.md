---
title: Implementación de Windows AutoPilot para la guante blanca
description: Implementación de Windows AutoPilot para la guante blanca
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, sin intervención del socio, msfb, Intune, aprovisionamiento previo
ms.prod: w10
ms.technology: windows
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itproF
manager: laurawi
ms.audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 61bddf4ffcb844a997e19ad4d954b2e2a8ec6b45
ms.sourcegitcommit: dc2cca9eb70aef15037e8f7d18d671c513bfde85
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2020
ms.locfileid: "90081714"
---
# <a name="windows-autopilot-for-white-glove-deployment"></a>Implementación de Windows AutoPilot para la guante blanca

**Se aplica a: Windows 10, versión 1903** 

Windows AutoPilot ayuda a las organizaciones a aprovisionar fácilmente nuevos dispositivos mediante la imagen y los controladores OEM preinstalados. Esto permite a los usuarios finales obtener sus dispositivos listos para la empresa mediante un proceso sencillo.

 ![proceso de OEM](images/wg01.png)

Windows AutoPilot también puede proporcionar un servicio de la <I>guante de blanco</I> que ayuda a los asociados o al personal de ti a aprovisionar previamente un equipo con Windows 10 preparado para el negocio y totalmente configurado. Desde la perspectiva del usuario final, la experiencia controlada por el usuario de Windows AutoPilot no cambia, pero la obtención de su dispositivo a un estado totalmente aprovisionado es más rápida.

Con la **implementación de Windows AutoPilot para la guante blanca**, se divide el proceso de aprovisionamiento. Las partes que requieren mucho tiempo se realizan por ti, asociados o OEM. El usuario final simplemente completa algunos valores y directivas necesarios y, a continuación, puede empezar a usar su dispositivo.

 ![Proceso de OEM con asociado](images/wg02.png)

Las implementaciones de la guante blanca usan Microsoft Intune en Windows 10, versión 1903 y posteriores. Estas implementaciones se basan en escenarios de Windows AutoPilot existentes basados en [el usuario](user-driven.md) y admiten escenarios de modo controlado por el usuario para dispositivos Azure Active Directory Unidos e híbridos Unidos Azure Active Directory.

## <a name="prerequisites"></a>Prerrequisitos

Además de [los requisitos de Windows AutoPilot](software-requirements.md), la implementación de Windows AutoPilot para la guante blanca también requiere:

- Windows 10, versión 1903 o posterior.
- Una suscripción de Intune.
- Dispositivos físicos que admiten TPM 2,0 y la atestación de dispositivo. No se admiten las máquinas virtuales. El proceso de aprovisionamiento de la guante blanca usa las capacidades de Autoimplementación de Windows AutoPilot, por lo que se requiere TPM 2,0.
- Los dispositivos físicos con conectividad Ethernet son necesarios para realizar aprovisionamiento. No se admite la conectividad Wi-Fi debido al requisito de elegir un idioma, una configuración regional y un teclado para realizar esa conexión Wi-Fi. Aplicar este requisito en un proceso de aprovisionamiento previo podría impedir que el usuario elegira su idioma, configuración regional y teclado cuando reciban el dispositivo. Para obtener más información, consulte [uso de una conexión de red inalámbrica con la guante blanca de Windows AutoPilot](https://oofhours.com/2019/11/14/using-a-wireless-network-connection-with-windows-autopilot-white-glove/).

>[!IMPORTANT]
>Dado que el OEM o el proveedor lleva a cabo el proceso de la guante blanca, <u>no requiere acceso a la infraestructura de dominio local del usuario final</u>. Esto no es lo mismo que un escenario híbrido típico de Azure AD Unidos porque se pospone el reinicio del dispositivo. El dispositivo se vuelve a sellar antes del momento en que se espera la conectividad con un controlador de dominio y se Contacta con la red del dominio cuando el usuario final vuelve a desempaquetar el dispositivo local.

## <a name="preparation"></a>Preparación

Los dispositivos programados para el aprovisionamiento de la guante blanca se registran para el piloto automático mediante el proceso de registro normal. 

Para estar listo para probar la implementación de Windows AutoPilot para la guante blanca, asegúrese de que puede usar en primer lugar los escenarios existentes basados en el usuario de Windows AutoPilot:

- Combinación de Azure AD controlada por el usuario. Asegúrese de que puede implementar dispositivos con Windows AutoPilot y unirlos a un inquilino de Azure Active Directory.
- Controlado por el usuario con Azure AD híbrido join. Asegúrese de que puede implementar dispositivos con Windows AutoPilot, unirlos a un dominio de Active Directory local y registrarlos con Azure Active Directory para habilitar las características de Azure AD híbrido join.

Si no se pueden completar estos escenarios, la implementación de Windows AutoPilot para la guante blanca tampoco se realizará correctamente, ya que se basa en estos escenarios.

Antes de comenzar el proceso de la guante blanca en la instalación del servicio de aprovisionamiento, debe configurar una configuración de perfil AutoPilot adicional mediante su cuenta de Intune:

 ![permitir la guante blanca](images/allow-white-glove-oobe.png)

El proceso de aprovisionamiento previo de implementación de Windows AutoPilot para la guante blanca aplicará todas las directivas de destino de dispositivos de Intune. Esto incluye los certificados, las plantillas de seguridad, la configuración, las aplicaciones, etc., todo ello dirigido al dispositivo. Además, cualquier aplicación de Win32 o LOB se instalará si cumplen estas dos condiciones:
- configurado para instalar en el contexto del dispositivo.
- dirigido al usuario preasignado al dispositivo AutoPilot.

Asegúrese de no tener como destino aplicaciones de Win32 y LOB en el mismo dispositivo. 

> [!NOTE]
> Seleccione el modo de idioma como usuario especificado en perfiles de AutoPilot para garantizar un acceso sencillo en el modo de aprovisionamiento de la guante blanca. La fase de técnico de la guante blanca instalará todas las aplicaciones de destino del dispositivo y todas las aplicaciones de contexto de dispositivo específicas del usuario que tengan como destino el usuario asignado. Si no hay ningún usuario asignado, solo instalará las aplicaciones de destino del dispositivo. No se aplicarán otras directivas de destino de usuario hasta que el usuario inicie sesión en el dispositivo. Para comprobar estos comportamientos, asegúrese de crear las aplicaciones y las directivas adecuadas para los dispositivos y los usuarios.

## <a name="scenarios"></a>Escenarios

La implementación de Windows AutoPilot para la guante blanca es compatible con dos escenarios distintos:
- Implementaciones controladas por el usuario con Azure AD join. El dispositivo se unirá a un inquilino de Azure AD.
- Implementaciones controladas por el usuario con Unión a Azure AD híbrido. El dispositivo se unirá a un dominio de Active Directory local y se registrará de forma independiente en Azure AD.

Cada uno de estos escenarios consta de dos partes, un flujo del técnico y un flujo de usuario. En un nivel alto, estas partes son las mismas para Azure AD join y Azure AD híbrido join. El usuario final verá principalmente las diferencias en los pasos de autenticación.

### <a name="technician-flow"></a>Flujo del técnico

Una vez que el cliente o el administrador de ti ha dirigido todas las aplicaciones y la configuración que desean para sus dispositivos a través de Intune, el técnico de la guante blanca puede comenzar el proceso de la guante blanca. El técnico podría ser miembro del personal de ti, de un asociado de servicios o de un OEM: cada organización puede decidir quién debe realizar estas actividades. Independientemente del escenario, el proceso realizado por el técnico es el mismo:
- Arranque el dispositivo (con las SKU de Windows 10 Pro, Enterprise o Education, versión 1903 o posterior).
- En la primera pantalla de OOBE (que podría ser una pantalla de selección de idioma o de configuración regional), no haga clic en **siguiente**. En su lugar, presione la tecla de Windows cinco veces para ver un cuadro de diálogo de opciones adicionales. En esa pantalla, elija la opción de **aprovisionamiento de Windows AutoPilot** y, a continuación, haga clic en **continuar**.

 ![Opción de aprovisionamiento de Windows AutoPilot](images/choice.png)

- En la pantalla **configuración de Windows AutoPilot** , se mostrará información sobre el dispositivo:
 - El perfil AutoPilot asignado al dispositivo.
 - El nombre de la organización para el dispositivo.
 - Usuario asignado al dispositivo (si hay alguno).
 - Código QR que contiene un identificador único para el dispositivo. Puede usar este código para buscar el dispositivo en Intune. Puede que desee hacer esto para realizar cambios de configuración, como la asignación de un usuario o la adición del dispositivo a los grupos necesarios para la aplicación o la Directiva de destino.
 - **Nota**: los códigos QR se pueden analizar mediante una aplicación complementaria. La aplicación también configura el dispositivo para especificar a quién pertenece. El equipo de AutoPilot ha publicado en GitHub un [ejemplo de código abierto de la aplicación complementaria](https://github.com/Microsoft/WindowsAutopilotCompanion) que se integra con Intune mediante el Graph API.
- Valide la información que se muestra. Si se necesitan cambios, realice los cambios y, a continuación, haga clic en **Actualizar** para volver a descargar los detalles del perfil AutoPilot actualizado.

 ![Pantalla de configuración de Windows AutoPilot](images/landing.png)

- Haga clic en **aprovisionar** para comenzar el proceso de aprovisionamiento.

Si el proceso de aprovisionamiento previo se completa correctamente:
- Aparece una pantalla de estado verde con información sobre el dispositivo, incluidos los mismos detalles presentados anteriormente. Por ejemplo, perfil de AutoPilot, nombre de la organización, usuario asignado y código QR. También se proporciona el tiempo transcurrido para los pasos previos al aprovisionamiento.
 ![Pantalla de configuración verde](images/white-glove-result.png)
- Haga clic en volver a **sellar** para apagar el dispositivo. En ese momento, el dispositivo puede enviarse al usuario final.

>[!NOTE]
>El flujo de técnicos hereda el comportamiento del [modo de auto-implementación](self-deploying.md). Según la documentación del modo de auto-implementación, se usa la página estado de inscripción para almacenar el dispositivo en un estado de aprovisionamiento y evitar que el usuario continúe con el escritorio después de la inscripción, pero antes de que se realice la aplicación del software y la configuración. Por lo tanto, si la página estado de inscripción está deshabilitada, el botón volver a sellar puede aparecer antes de que el software y la configuración se aplique, lo que le permite pasar al flujo de usuario antes de que se complete el aprovisionamiento del flujo de técnicos. La pantalla verde valida que la inscripción se ha realizado correctamente, no que el flujo del técnico se ha completado necesariamente.

Si se produce un error en el proceso de aprovisionamiento previo:
- Aparece una pantalla de estado rojo con información sobre el dispositivo, incluidos los mismos detalles presentados previamente. Por ejemplo, perfil de AutoPilot, nombre de la organización, usuario asignado y código QR. También se proporciona el tiempo transcurrido para los pasos previos al aprovisionamiento.
- Los registros de diagnóstico se pueden recopilar desde el dispositivo y, a continuación, se pueden restablecer para volver a iniciar el proceso.

### <a name="user-flow"></a>Flujo de usuario

Si el proceso de aprovisionamiento previo se ha completado correctamente y el dispositivo se ha resellado, puede entregarlo al usuario final. El usuario final completará el proceso normal controlado por el usuario de Windows AutoPilot siguiendo estos pasos:

- Encienda el dispositivo.
- Seleccione el idioma, la configuración regional y la distribución del teclado adecuados.
- Conectarse a una red (si se usa Wi-Fi). Siempre se requiere acceso a Internet. Si usa Unión a Azure AD híbrido, también debe haber conectividad con un controlador de dominio.
- En la pantalla de inicio de sesión con marca, escriba las credenciales del Azure Active Directory del usuario.
- Si usa Unión a Azure AD híbrido, el dispositivo se reiniciará; después del reinicio, escriba las credenciales del Active Directory del usuario.
- Las directivas y las aplicaciones adicionales se entregarán en el dispositivo, tal y como realiza el seguimiento de la página de estado de inscripción (ESP). Una vez que haya finalizado, el usuario podrá acceder al escritorio.

## <a name="related-topics"></a>Temas relacionados

[Vídeo de la guante blanca](https://youtu.be/nE5XSOBV0rI)
