---
title: Windows Autopilot para dispositivos existentes
titleSuffix: Configuration Manager
description: Use una secuencia de tareas de Configuration Manager para crear una imagen y aprovisionar un dispositivo de Windows 7 para el modo controlado por el usuario de Windows Autopilot.
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709023"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot para dispositivos existentes
<!--3607717, fka 1358333-->

*Se aplica a: Configuration Manager (rama actual)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) proporciona una manera para que las organizaciones envíen dispositivos Windows 10 nuevos e intactos directamente al usuario final y definan el flujo de aprovisionamiento por el que pasa el usuario para obtener un dispositivo Windows 10 seguro y productivo. El dispositivo está registrado en el servicio de Windows Autopilot, por lo que puede asignar el perfil de Windows Autopilot necesario. Este perfil define la configuración rápida del dispositivo. 

[Windows Autopilot para los dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponible con Windows 10, versión 1809 o posterior. Esta característica permite volver a crear una imagen y aprovisionar un dispositivo de Windows 7 para el [modo controlado por el usuario de Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) mediante una única secuencia de tareas nativa de Configuration Manager. 



## <a name="prerequisites"></a>Requisitos previos

- Adquiera el soporte de instalación para Windows 10, versión 1809 o posterior. Después cree una imagen del sistema operativo de Configuration Manager. Para más información, vea [Administrar imágenes de SO](../get-started/manage-operating-system-images.md).

- En Microsoft Intune, cree perfiles de Windows Autopilot. Para obtener más información, consulte [Inscripción de dispositivos Windows en Intune con Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- Un dispositivo no está registrado todavía con el servicio de Windows Autopilot. Si el dispositivo ya está registrado, el perfil asignado tendrá prioridad. El perfil de Autopilot para dispositivos existentes solo se aplica en caso de que expire el perfil en línea.



## <a name="create-the-configuration-file"></a>Creación del archivo de configuración

1. En un dispositivo Windows con conectividad a internet, abra una ventana de comandos de PowerShell administrativa y ejecute los siguientes comandos:  

    1. Instale los módulos necesarios y acepte las indicaciones para continuar.  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Inicie sesión en Intune con credenciales de administrador.  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Recupere todos los perfiles de Windows Autopilot asociados con su inquilino de Intune.  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Cree un archivo de configuración para cada perfil. Los archivos reciben un nombre acorde con el nombre para mostrar del perfil y se guardan en el escritorio del usuario actual.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > El archivo de configuración solo puede contener un perfil. Cada perfil debe estar dentro de llaves `{}`.  

2. Guarde uno de los perfiles en un archivo con codificación ANSI denominado **AutopilotConfigurationFile.json**. Guárdelo en una ubicación adecuada como un origen del paquete de Configuration Manager.  

    > [!Tip]  
    > Si usa el cmdlet de PowerShell **Out-File** para redirigir la salida JSON a un archivo, se usa la codificación Unicode de forma predeterminada. Este cmdlet también puede truncar las líneas largas. Use el cmdlet **Set-Content** con el parámetro `-Encoding ASCII` para establecer la codificación de texto adecuada.   
    > 
    > El Bloc de notas de Windows usa la codificación ANSI de manera predeterminada.  

3. Cree un paquete de Configuration Manager que contenga este archivo. No requiere un programa. Para más información, vea [Creación de un paquete](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program).  

    > [!NOTE]  
    > Windows requiere que este archivo se denomine **AutopilotConfigurationFile.json**. Para utilizar más de un perfil de Autopilot, cree paquetes independientes de Configuration Manager.  



## <a name="create-the-task-sequence"></a>Creación de la secuencia de tareas

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y seleccione el nodo **Secuencias de tareas**. Seleccione **Crear secuencia de tareas** en la cinta de opciones.  

2. En la página **Crear nueva secuencia de tareas**, seleccione la opción de **Implementar Windows Autopilot para los dispositivos existentes**.  

3. En la página **Información de secuencia de tareas**, especifique un nombre, opcionalmente agregue una descripción y seleccione una imagen de arranque. Para más información sobre las versiones compatibles de la imagen de arranque, vea [Compatibilidad con Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).  

4. En la página **Instalar Windows**, seleccione el **paquete de la imagen** de Windows 10. Luego, configure las siguientes opciones:  

    - **Índice de imagen**: Seleccione Enterprise, Education o Professional, según lo requiera la organización.  

    - Habilite la opción de **Particionar y formatear el equipo de destino antes de instalar el sistema operativo**.  

    - **Configurar secuencia de tareas para su uso con BitLocker**: Si habilita esta opción, la secuencia de tareas incluye los pasos necesarios para habilitar Bitlocker.  

    - **Clave de producto**: Si tiene que especificar una clave de producto para la activación de Windows, escríbala aquí.  

    - Seleccione una de las siguientes opciones para configurar la cuenta de administrador local en Windows 10:  
        - **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas (recomendado)**
        - **Habilitar la cuenta y especificar la contraseña de administrador local**

5. En la página **Configurar red**, seleccione la opción de **unirse a un grupo de trabajo**. Esta secuencia de tareas usa la herramienta de preparación del sistema de Windows (sysprep). Si el dispositivo está unido a un dominio, sysprep genera un error.  

6. En la página **Instalar Configuration Manager**, agregue las propiedades de instalación necesarias para su entorno.  

    > [!Tip]  
    > La secuencia de tareas solo necesita esta información si se necesitan los componentes de cliente de Configuration Manager durante la secuencia de tareas antes de que se ejecute sysprep. Por ejemplo, para instalar las actualizaciones de software o aplicaciones. Si no va a realizar estas acciones, el cliente no es necesario. Se desinstala antes de que la secuencia de tareas ejecute sysprep.  

7. En la página **Incluir actualizaciones**, se selecciona de forma predeterminada la opción para **No instalar ninguna actualización de software**.  

    > [!Tip]  
    > Utilice el mantenimiento de imágenes sin conexión para mantener la imagen actualizada con las últimas actualizaciones de calidad de Windows 10. Para más información, vea [Aplicación de actualizaciones de software a una imagen de sistema operativo](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).  

8. Puede seleccionar aplicaciones para instalarlas durante la secuencia de tareas en la página **Instalar aplicaciones**. Sin embargo, Microsoft recomienda reflejar el enfoque de la imagen de firma con este escenario. Una vez aprovisionado el dispositivo con Autopilot, aplique todas las aplicaciones y configuraciones de la administración conjunta de Microsoft Intune o Configuration Manager. Este proceso proporciona una experiencia coherente entre los usuarios que reciben los nuevos dispositivos y aquellos que usan Windows Autopilot para los dispositivos existentes.  

8. En la página **Preparación del sistema**, seleccione el paquete que incluye el archivo de configuración de Autopilot. De forma predeterminada, la secuencia de tareas reinicia el equipo después de ejecutar Sysprep de Windows. También puede seleccionar la opción de **Apagar el equipo cuando se complete esta secuencia de tareas**. Esta opción permite preparar un dispositivo y luego entregarlo a un usuario para una experiencia coherente de Autopilot.  

9. Complete el asistente.  

Si edita la secuencia de tareas, es similar a la secuencia de tareas predeterminada para aplicar una imagen del sistema operativo existente. Esta secuencia de tareas incluye los siguientes pasos adicionales:  

- **Aplicar configuración de Windows Autopilot**: Este paso aplica el archivo de configuración de Autopilot desde el paquete especificado. No es un nuevo tipo de paso, es un paso de **Ejecutar línea de comandos** para copiar el archivo.  

- **Preparar Windows para la captura**: Este paso ejecuta sysprep de Windows y tiene la configuración para **apagar el equipo después de ejecutar esta acción**. Para obtener más información, consulte [Preparar Windows para la captura](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

La secuencia de tareas de Windows Autopilot para dispositivos existentes da como resultado un dispositivo unido a Azure Active Directory (Azure AD). 

> [!NOTE]  
> Con la versión 1903 y la versión 1909 de Windows 10, AutoPilot tiene un problema conocido en el que Sysprep elimina el archivo **AutopilotConfigurationFile.json**. Si usa este método para implementar la versión 1903 o 1909 de Windows 10, edite esta secuencia de tareas y realice los cambios siguientes:
>
> 1. Deshabilite el paso **Preparar Windows para la captura**.
> 2. Inmediatamente después del paso deshabilitado **Preparar Windows para la captura**, agregue un nuevo paso **Ejecutar línea de comandos**. Configúrelo para ejecutar la siguiente línea de comandos: `c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> Para más información, vea [Windows Autopilot: problemas conocidos](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues).

Use la opción de [mover carpetas conocidas](https://docs.microsoft.com/onedrive/redirect-known-folders) de OneDrive para la Empresa para asegurarse de que se hace una copia de seguridad de los datos del usuario antes de la actualización de Windows 10.



## <a name="next-steps"></a>Pasos siguientes

Use la administración conjunta para mejorar las características de administración de los dispositivos Windows 10. La segunda ruta hacia la administración conjunta pasa a través del aprovisionamiento moderno con Windows Autopilot. Vea los siguientes artículos para más información:

- [¿Qué es administración conjunta?](../../comanage/overview.md)
- [Rutas hacia la administración conjunta](../../comanage/quickstart-paths.md)
- [Windows Autopilot con administración conjunta](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>Vea también

- [Inscripción de dispositivos Windows en Intune con Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)
