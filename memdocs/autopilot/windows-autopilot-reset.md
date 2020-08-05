---
title: Restablecimiento de Windows AutoPilot
description: El restablecimiento de Windows AutoPilot vuelve a poner el dispositivo en un estado listo para la empresa, lo que permite que el siguiente usuario inicie sesión y se haga productivo de forma rápida y sencilla.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 8388febead5953fd6c76e7e40571d3b2e1b91e4d
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757014"
---
# <a name="windows-autopilot-reset"></a>Restablecimiento de Windows AutoPilot

- Se aplica a: Windows 10, versión 1709 y versiones posteriores (restablecimiento local)
- Se aplica a: Windows 10, versión 1809 y versiones posteriores (restablecimiento remoto)

El restablecimiento de Windows AutoPilot quita los archivos personales, las aplicaciones y la configuración y vuelve a aplicar la configuración original de un dispositivo, manteniendo su conexión de identidad a Azure AD y su conexión de administración a Intune para que el dispositivo vuelva a estar listo para su uso. El restablecimiento de Windows AutoPilot vuelve a poner el dispositivo en un estado listo para la empresa, lo que permite que el siguiente usuario inicie sesión y se ponga en productividad de forma rápida y sencilla. 

El proceso de restablecimiento de Windows AutoPilot conserva automáticamente la información del dispositivo existente:
 
-   Establezca la región, el idioma y el teclado en los valores configurados originalmente.
-   Detalles de la conexión Wi-Fi.
-   Aprovisionar paquetes previamente aplicados al dispositivo, así como un paquete de aprovisionamiento presente en una unidad USB cuando se inicia el proceso de restablecimiento. 
-   Azure Active Directory la información de inscripción de dispositivos e MDM.

El restablecimiento de Windows AutoPilot impedirá al usuario el acceso al escritorio hasta que se restaure esta información, incluida la nueva aplicación de los paquetes de aprovisionamiento.  En el caso de los dispositivos inscritos en un servicio MDM, el restablecimiento de Windows AutoPilot también se bloqueará hasta que se complete una sincronización de MDM.  
Al usarse el restablecimiento de Autopilot en un dispositivo, se quitará el usuario primario del dispositivo. El próximo usuario que inicie sesión tras el restablecimiento se establecerá como usuario primario.
 
 
>[!NOTE]
>El restablecimiento de AutoPilot no es compatible con dispositivos Azure AD híbrido Unidos.

## <a name="scenarios"></a>Escenarios

El restablecimiento de Windows AutoPilot admite dos escenarios:

-   [Restablecimiento local](#reset-devices-with-local-windows-autopilot-reset) Iniciado por el personal de ti u otros administradores de la organización.
-   El personal de ti inicia de forma remota el [restablecimiento remoto](#reset-devices-with-remote-windows-autopilot-reset) a través de un servicio MDM como Microsoft Intune.

Se aplican requisitos adicionales y detalles de configuración con cada escenario; Vea los vínculos detallados anteriores para obtener más información.

## <a name="reset-devices-with-local-windows-autopilot-reset"></a>Restablecimiento de dispositivos con restablecimiento de Windows AutoPilot local 

**Se aplica a: Windows 10, versión 1709 y versiones posteriores**

El rol de administrador de servicios de Intune es necesario para realizar esta tarea.  Para más información, vea [Adición de usuarios y concesión de permiso administrativo a Intune](https://docs.microsoft.com/intune/users-add).

Los administradores de TI pueden realizar un restablecimiento de Windows AutoPilot local para quitar rápidamente los archivos personales, las aplicaciones y la configuración, y restablecer los dispositivos de Windows 10 desde la pantalla de bloqueo en cualquier momento y aplicar la configuración original y la inscripción de administración (Azure Active Directory y administración de dispositivos) para que los dispositivos estén listos para usarse. Una vez que se restablece el AutoPilot local, los dispositivos se devuelven a un estado de aprobado totalmente configurado o conocido.

Para habilitar el restablecimiento local del AutoPilot en Windows 10:

1. [Habilitación de la Directiva para la característica](#enable-local-windows-autopilot-reset)
2. [Desencadenar un restablecimiento para cada dispositivo](#trigger-local-windows-autopilot-reset)

### <a name="enable-local-windows-autopilot-reset"></a>Habilitar restablecimiento de Windows AutoPilot local

Para habilitar un restablecimiento de Windows AutoPilot local, debe configurarse la directiva **DisableAutomaticReDeploymentCredentials** . Esta Directiva se documenta en el [CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-credentialproviders)de la Directiva, **CredentialProviders/DisableAutomaticReDeploymentCredentials**. De forma predeterminada, Windows AutoPilot local está deshabilitado. Esto garantiza que no se desencadene un restablecimiento local del AutoPilot por accidente.

Puede establecer la Directiva con uno de estos métodos:

- Proveedor de MDM

    - Al usar Intune, puede crear un nuevo perfil de configuración de dispositivo, especificando "Windows 10 o posterior" para la plataforma, "restricciones de dispositivos" para el tipo de perfil y "general" para la categoría de configuración.  La configuración de **reimplementación automática** debe establecerse en **permitir**.  Implemente esta opción en todos los dispositivos en los que se permita un restablecimiento local.
    - Si usa un proveedor de MDM distinto de Intune, consulte la documentación del proveedor de MDM para obtener información sobre cómo establecer esta Directiva. 

- Diseñador de configuración de Windows

    Puede [usar el diseñador de configuración de Windows](https://docs.microsoft.com/windows/configuration/provisioning-packages/provisioning-create-package) para establecer la configuración de tiempo de **ejecución > las directivas > CredentialProviders > DisableAutomaticReDeploymentCredentials** en 0 y, a continuación, crear un paquete de aprovisionamiento.

- Configuración de la aplicación School PCs

    La versión más reciente de la aplicación configurar equipos escolares admite el restablecimiento de Windows AutoPilot local.

### <a name="trigger-local-windows-autopilot-reset"></a>Desencadenar restablecimiento de Windows AutoPilot local

La realización de un restablecimiento local de Windows AutoPilot es un proceso de dos pasos: desencadenarlo y autenticarse. Una vez que haya realizado estos dos pasos, puede permitir que el proceso se ejecute y, una vez hecho, el dispositivo esté de nuevo preparado para su uso. 

**Para desencadenar un restablecimiento de AutoPilot local**

1. En la pantalla de bloqueo del dispositivo Windows, escriba la pulsación de tecla **Ctrl + ![ tecla Windows ](images/windows_glyph.png) + R**. 

    ![Escriba CTRL + Tecla Windows + R en la pantalla de bloqueo de Windows](images/autopilot-reset-lockscreen.png)

    Se abrirá una pantalla de inicio de sesión personalizada para el restablecimiento del AutoPilot local. La pantalla sirve para dos propósitos:
    1. Confirmar o comprobar que el usuario final tiene el derecho a desencadenar el restablecimiento local del piloto automático
    2. Notificar al usuario en caso de que se use un paquete de aprovisionamiento creado mediante el diseñador de configuración de Windows, como parte del proceso.

    ![Pantalla de inicio de sesión personalizada para el restablecimiento local de AutoPilot](images/autopilot-reset-customlogin.png)

2. Inicie sesión con las credenciales de la cuenta de administrador. Si ha creado un paquete de aprovisionamiento, conecte la unidad USB y desencadene el restablecimiento del AutoPilot local.

    Una vez que se desencadena el restablecimiento del AutoPilot local, se inicia el proceso de restablecimiento. Una vez completado el aprovisionamiento, el dispositivo vuelve a estar listo para su uso.

## <a name="reset-devices-with-remote-windows-autopilot-reset"></a>Restablecimiento de dispositivos con restablecimiento remoto de Windows AutoPilot

**Se aplica a: Windows 10, versión 1809 o posterior**

Al realizar un restablecimiento remoto de Windows AutoPilot, se puede usar un servicio MDM como Microsoft Intune para iniciar el proceso de restablecimiento, evitando la necesidad de que el personal de ti u otros administradores visiten cada equipo para iniciar el proceso.

Para habilitar un dispositivo para un restablecimiento remoto de Windows AutoPilot, el dispositivo debe estar administrado por MDM y estar unido a Azure AD. Esta característica no se admite en los dispositivos que se inscribieron mediante el [modo de Autoimplementación AutoPilot](self-deploying.md).

### <a name="triggering-a-remote-windows-autopilot-reset"></a>Desencadenar un restablecimiento remoto de Windows AutoPilot

Para desencadenar un restablecimiento remoto de Windows AutoPilot a través de Intune, siga estos pasos:
 
-   Vaya a la pestaña **dispositivos** en la consola de Intune. 
-   En la vista **todos los dispositivos** , seleccione los dispositivos de restablecimiento de destino y haga clic en **más** para ver las acciones de dispositivo. 
-   Seleccione **AutoPilot restablecer** para iniciar la tarea de restablecimiento. 

>[!NOTE]
>La opción de restablecimiento de AutoPilot no se habilitará en Microsoft Intune para dispositivos que no ejecuten la compilación 17672 o posterior de Windows 10.

>[!IMPORTANT]
>La característica de restablecimiento de AutoPilot permanecerá atenuada, **a menos** que se restablezca el dispositivo mediante el AutoPilot (ya sea mediante el restablecimiento de nuevos o manualmente el dispositivo).

Una vez completado el restablecimiento, el dispositivo vuelve a estar listo para su uso.
 


## <a name="troubleshooting"></a>Solución de problemas

El restablecimiento de Windows AutoPilot requiere que el [entorno de recuperación de Windows (WinRE)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) esté configurado y habilitado correctamente en el dispositivo. Si no está configurado y habilitado, se informará de un error como `Error code: ERROR_NOT_SUPPORTED (0x80070032)` .

Para asegurarse de que WinRE está habilitado, use la [herramienta deREAgentC.exe](https://docs.microsoft.com/windows-hardware/manufacture/desktop/reagentc-command-line-options) para ejecutar el siguiente comando:

```
reagentc /enable
```

Si se produce un error en el restablecimiento de Windows AutoPilot después de habilitar WinRE, o si no puede habilitar WinRE, póngase en contacto con [soporte técnico de Microsoft](https://support.microsoft.com) para obtener ayuda.
