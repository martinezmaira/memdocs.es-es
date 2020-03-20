---
title: 'Configuración de educación de Windows 10 en Microsoft Intune: Azure | Microsoft Docs'
description: Vea una lista de todas las configuraciones de educación para dispositivos Windows 10. Use estas configuraciones en un perfil de configuración de dispositivo con la aplicación Hacer un examen, elija cómo los usuarios o alumnos inician sesión, supervise la pantalla durante el examen y mucho más en Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39f881b05c9698a8560fe009331fac3389b35bde
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364297"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Configuración de la aplicación Hacer un examen en dispositivos Windows 10 con Microsoft Intune

La aplicación Hacer un examen permite administrar de forma segura las pruebas en línea en los dispositivos Windows 10 de su aula. Para configurar la aplicación Hacer un examen, se deberá crear un perfil de configuración de dispositivo en Intune y configurar las opciones de evaluación segura. En este artículo se describe la configuración que encontrará para la aplicación Hacer un examen. 

Una vez configurado el perfil, asígnelo a los alumnos e impleméntelo. 

[La aplicación Hacer un examen de Intune](education-settings-configure.md) proporciona más información sobre esta característica.

## <a name="before-you-begin"></a>Antes de comenzar

[Cree un perfil de configuración de dispositivo](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Configuración de Hacer un examen
Después de crear un perfil de configuración de dispositivo, vaya a **Tipo de perfil** y seleccione **Evaluación segura (Educación)** . Encontrará la configuración de aplicación Hacer un examen siguiente. 


- **Tipo de cuenta**: elija cómo los usuarios inician sesión en el examen. Las opciones son:
  - Cuenta de Azure AD
  - Cuenta de dominio
  - Cuenta local
  - Cuenta de invitado local: solo disponible en dispositivos que ejecuten Windows 10, versión 1903 y posteriores.    
- **Nombre de usuario de la cuenta**: especifique el nombre del usuario de la cuenta que utiliza con Hacer un examen. Puede especificar cuentas en el siguiente formato:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Nombre de la cuenta**: para configurar un tipo de cuenta de invitado local, escriba el nombre de la cuenta que se usa con la aplicación Hacer un examen. El nombre de la cuenta aparecerá como un icono en la pantalla de inicio de sesión. Los alumnos deben hacer clic en el icono para iniciar el examen.  
- **Dirección URL de evaluación**: especifique la dirección URL del examen que desea que los usuarios realicen. Para más información sobre cómo obtener la dirección URL, vea la [documentación de Hacer un examen](https://docs.microsoft.com/education/windows/take-tests-in-windows-10).
- **Conexión de impresora**: elija **Requerir** para permitir solo el acceso a la aplicación Hacer un examen desde dispositivos que estén conectados a una impresora. Esta opción también hace que el botón Imprimir de la aplicación esté disponible para los alumnos que van a realizar el examen. **No configurado** permite a los alumnos tener acceso a la aplicación desde dispositivos que no están conectados a una impresora.  
- **Supervisión de pantalla**: elija **Permitir** para supervisar la actividad de la pantalla mientras los usuarios realizan una prueba. **No configurada** impide la supervisión de la pantalla durante el examen.
- **Sugerencias de texto**: elija **Permitir** para que los que hacen el examen puedan ver sugerencias de texto. **No configurada** bloquea las sugerencias de texto mientras los usuarios realizan un examen.

## <a name="next-steps"></a>Pasos siguientes

Asegúrese de [asignar el perfil](device-profile-assign.md) y [supervise su estado](device-profile-monitor.md).
