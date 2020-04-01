---
title: 'Inicio rápido: Creación de un perfil de dispositivo de correo para dispositivos iOS/iPadOS'
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo usar Microsoft Intune para crear un perfil de dispositivo de correo para que los dispositivos iOS/iPadOS se puedan conectar de forma segura al correo de la empresa.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af7657eb89df14e8429a81616e76d81a5a9ac5c1
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327422"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>Inicio rápido: Creación de un perfil de dispositivo de correo para iOS/iPadOS

En este inicio rápido, aprenderá a crear un perfil de dispositivo de correo para dispositivos iOS/iPadOS. Este perfil especifica la configuración necesaria para que la aplicación de correo integrada en el dispositivo iOS/iPadOS se conecte al correo de la empresa. Con los perfiles de dispositivo de correo, puede estandarizar la configuración para todos los dispositivos y permitir a los usuarios finales acceder al correo de la empresa desde sus dispositivos personales sin necesidad de ninguna configuración por su parte. Para proteger aún más su correo, puede usar un perfil de correo electrónico para determinar si los dispositivos son compatibles y, después, establecer el acceso condicional para permitir que solo puedan acceder al correo los dispositivos que sean compatibles. Para más detalles sobre los perfiles de correo, vea [Configuración del correo electrónico en Microsoft Intune](email-settings-configure.md).

Si no dispone de ninguna suscripción a Intune, [regístrese para obtener una cuenta de evaluación gratuita](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Iniciar sesión en Intune

Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) como administrador global o administrador de servicios de Intune. Si ha creado una suscripción de prueba de Intune, la cuenta con la que creó la suscripción es el administrador global.

## <a name="create-an-iosipados-email-profile"></a>Creación de un perfil de correo electrónico para iOS/iPadOS

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione y vaya a **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
   ![Creación de un perfil de correo para iOS/iPadOS en Intune](./media/quickstart-email-profile/ios-create-profile.png)

3. Escriba las propiedades siguientes:
   - **Plataforma**: seleccione **iOS/iPadOS**.
   - **Perfil**: seleccione **Correo electrónico**.
  
4. Seleccione **Crear**.

5. En **Básico**, escriba las propiedades siguientes:
   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil. En este ejemplo, escriba **iOS necesita correo electrónico de trabajo**.
   - **Descripción**: escriba **Requiere que los dispositivos iOS/iPadOS usen correo electrónico del trabajo**.


        ![Creación de un perfil de correo electrónico para usarlo con dispositivos iOS/iPadOS en Intune](./media/quickstart-email-profile/ios-email-profile-name.png)

6. Seleccione **Siguiente**.

7. En **Opciones de configuración**, establezca estos valores (deje los demás valores predeterminados):
   - **Servidor de correo electrónico**: para este inicio rápido, escriba **outlook.office365.com**. Esta configuración especifica la ubicación de Exchange (dirección URL) del servidor de correo electrónico que usará la aplicación de correo electrónico de iOS/iPadOS para conectarse al correo electrónico.
   - **Nombre de la cuenta**: Escriba el **Correo electrónico de la empresa**.
   - **Atributo de nombre de usuario de AAD**: este nombre es el atributo que Intune obtiene de Azure Active Directory (Azure AD). Intune usa este nombre para generar dinámicamente el nombre de usuario para este perfil. Para este inicio rápido, suponemos que queremos que se use **Nombre principal de usuario** como nombre de usuario para el perfil (por ejemplo, user1@contoso.com).
   - **Atributo de dirección de correo electrónico de AAD**: esta configuración es la dirección de correo electrónico de Azure AD que se usará para iniciar sesión en Exchange. Para este inicio rápido, seleccione **Nombre principal de usuario**.
   - **Método de autenticación**: para este inicio rápido, seleccione **Nombre de usuario y contraseña**. También puede elegir **Certificado** si ya ha configurado un certificado para Intune.

8. Seleccione **Siguiente**.

9. En **Etiquetas de ámbito** (opcional), seleccione **Siguiente**. No usaremos una etiqueta de ámbito para este perfil.

10. En **Asignaciones**, use la lista desplegable para **Asignar a** y seleccione **Todos los usuarios y dispositivos**.  A continuación, seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. 

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no piensa usar el perfil que creó para otros tutoriales o pruebas, puede eliminarlo ahora.

1. En Intune, seleccione **Dispositivos** > **Configuración de dispositivos**.
2. Seleccione el perfil de prueba que ha creado, **iOS/iPadOS necesita correo electrónico de trabajo**, y seleccione **Eliminar**. 

## <a name="next-steps"></a>Pasos siguientes

En este inicio rápido, ha creado un perfil de correo electrónico para dispositivos iOS/iPadOS. Ya puede usar este perfil para determinar si un dispositivo iOS/iPadOS es compatible; para ello, solo tiene que crear una directiva de cumplimiento que marque como no compatibles aquellos dispositivos iOS/iPadOS que no coincidan con el perfil. Para lograr una mayor protección, puede crear una directiva de acceso condicional que bloquee el acceso al correo electrónico para todos aquellos dispositivos iOS/iPadOS que no sean compatibles. Para obtener más información sobre las directivas de cumplimiento de dispositivos, consulte la [introducción a las directivas de cumplimiento de dispositivos en Intune](../protect/device-compliance-get-started.md).

> [!div class="nextstepaction"]
> [Tutorial: Protección del correo electrónico de Exchange Online en dispositivos administrados](../protect/tutorial-protect-email-on-enrolled-devices.md)
