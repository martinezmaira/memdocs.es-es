---
title: Implementación de Windows AutoPilot para dispositivos existentes
description: La implementación de escritorio moderna con Windows AutoPilot permite implementar fácilmente la versión más reciente de Windows 10 en los dispositivos existentes.
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
ms.openlocfilehash: fc13a3a73e5e043d01bf5c7a3d310c496714caee
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908397"
---
# <a name="windows-autopilot-deployment-for-existing-devices"></a>Implementación de Windows AutoPilot para dispositivos existentes

**Se aplica a: Windows 10**

La implementación de escritorio moderna con Windows AutoPilot permite implementar fácilmente la versión más reciente de Windows 10 en los dispositivos existentes. Las aplicaciones que necesita para el trabajo se pueden instalar automáticamente. Su perfil de trabajo está sincronizado, por lo que puede continuar trabajando de inmediato.

En este tema se describe cómo convertir equipos Unidos a un dominio de Windows 7 o Windows 8.1 en dispositivos de Windows 10 Unidos a Azure Active Directory o Active Directory (Unión a Azure AD híbrido) mediante Windows AutoPilot.

>[!NOTE]
>Windows AutoPilot para dispositivos existentes solo admite perfiles de Azure Active Directory y Azure AD híbrido basados en el usuario. No se admiten los perfiles de implementación automática.

## <a name="prerequisites"></a>Requisitos previos

- Una versión compatible actualmente de Microsoft Endpoint Configuration Manager rama actual o rama de vista previa técnica. 
- [Windows ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) 1803 o posterior
    - Para obtener más información sobre la compatibilidad de Configuration Manager, consulte [compatibilidad con Windows 10 ADK](/configmgr/core/plan-design/configs/support-for-windows-10#windows-10-adk).
- Licencias de Microsoft Intune asignadas
- Azure Active Directory Premium
- Windows 10 versión 1809 o posterior importada en Configuration Manager como una imagen de sistema operativo
  - **Importante**: Consulte los [problemas conocidos](known-issues.md) si usa Windows 10 1903 con la plantilla de secuencia de tareas integrada de **Windows autopilot del dispositivo existente** de Configuration Manager. Actualmente, uno de los pasos de esta secuencia de tareas debe editarse para que funcione correctamente con la versión 1903 de Windows 10.

## <a name="procedures"></a>Procedimientos

### <a name="configure-the-enrollment-status-page-optional"></a>Configurar la página de estado de inscripción (opcional)

Si lo desea, puede configurar una [Página de estado de inscripción](enrollment-status.md) para AutoPilot con Intune.

Para habilitar y configurar la página inscripción y estado:

1. Abra [Intune en el Azure portal](https://aka.ms/intuneportal).
2. Acceder a **Intune > la inscripción de dispositivos > la inscripción de Windows** y [configurar una página de estado de inscripción](/intune/windows-enrollment-status). 
3. Acceder a **Azure Active Directory > Mobility (MDM y MAM) > Microsoft Intune** y [configurar la inscripción automática de MDM](/configmgr/mdm/deploy-use/enroll-hybrid-windows#enable-windows-10-automatic-enrollment) y configurar el ámbito de usuario de MDM para algunos o todos los usuarios. 

Vea los ejemplos siguientes:

![Página estado de inscripción](images/esp-config.png)<br><br>
![mdm](images/mdm-config.png)

### <a name="create-the-json-file"></a>Creación del archivo JSON 

>[!TIP]
>Para ejecutar los siguientes comandos en un equipo con Windows Server 2012/2012 R2 o Windows 7/8.1, primero debe descargar e instalar [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616).

1. En un servidor o equipo Windows conectado a Internet, abra una ventana de comandos de Windows PowerShell con privilegios elevados.
2. Escriba las líneas siguientes para instalar los módulos necesarios.

    #### <a name="install-required-modules"></a>Instalación de los módulos necesarios

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module AzureAD -Force
    Install-Module WindowsAutopilotIntune -Force
    Install-Module Microsoft.Graph.Intune -Force
    ```
    
3. Escriba las líneas siguientes y proporcione las credenciales administrativas de Intune.
   - Asegúrese de que la cuenta de usuario que especifique tiene derechos administrativos suficientes.

     ```powershell
     Connect-MSGraph
     ```
     El usuario y la contraseña de su cuenta se solicitarán mediante un formulario de Azure AD estándar. Escriba su nombre de usuario y contraseña y haga clic en **iniciar sesión**. 
     <br>Observe el ejemplo siguiente:

     ![Autenticación de Azure AD](images/pwd.png)

     Si es la primera vez que usa las API de grafos de Intune, también se le pedirá que habilite los permisos de lectura y escritura para Microsoft Intune PowerShell. Para habilitar estos permisos, siga estos pasos:
   - Seleccione **el consentimiento en nombre o en su organización**
   - Haga clic en **Accept** (Aceptar).

4. A continuación, recupere y muestre todos los perfiles de AutoPilot disponibles en el inquilino de Intune especificado en formato JSON:

    #### <a name="retrieve-profiles-in-autopilot-for-existing-devices-json-format"></a>Recuperar perfiles en el piloto automático para el formato JSON de los dispositivos existentes

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    ```

    Vea la siguiente salida de ejemplo: (use la barra de desplazamiento horizontal en la parte inferior para ver las líneas largas)
    <pre style="overflow-y: visible">
    PS C:\> Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    {
        "CloudAssignedTenantId":  "1537de22-988c-4e93-b8a5-83890f34a69b",
        "CloudAssignedForcedEnrollment":  1,
        "Version":  2049,
        "Comment_File":  "Profile Autopilot Profile",
        "CloudAssignedAadServerData":  "{\"ZeroTouchConfig\":{\"CloudAssignedTenantUpn\":\"\",\"ForcedEnrollment\":1,\"CloudAssignedTenantDomain\":\"M365x373186.onmicrosoft.com\"}}",
        "CloudAssignedTenantDomain":  "M365x373186.onmicrosoft.com",
        "CloudAssignedDomainJoinMethod":  0,
        "CloudAssignedOobeConfig":  28,
        "ZtdCorrelationId":  "7F9E6025-1E13-45F3-BF82-A3E8C5B59EAC"
    }</pre>

    Cada perfil se encapsula entre llaves **{}**. En el ejemplo anterior, se muestra un solo perfil.     

    Vea la tabla siguiente para obtener una descripción de las propiedades que se usan en el archivo JSON.


   |                          Propiedad                          |                                                                                                                                                                        Descripción                                                                                                                                                                         |
   |------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                 Versión (número, opcional)                 |                                                                                                                 El número de versión que identifica el formato del archivo JSON.  En Windows 10 1809, la versión especificada debe ser 2049.                                                                                                                  |
   |           CloudAssignedTenantId (GUID, obligatorio)           |                                                                                      IDENTIFICADOR del inquilino de Azure Active Directory que se debe usar.  Este es el GUID del inquilino y se puede encontrar en las propiedades del inquilino.  El valor no debe incluir llaves.                                                                                       |
   |        CloudAssignedTenantDomain (cadena, obligatorio)        |                                                                                                                                  El nombre del inquilino Azure Active Directory que se debe usar, por ejemplo: tenant.onmicrosoft.com.                                                                                                                                  |
   |         CloudAssignedOobeConfig (número, requerido)         |                                                                           Se trata de un mapa de bits que muestra qué configuración de AutoPilot se configuró. Los valores incluyen: SkipCortanaOptIn = 1, OobeUserNotLocalAdmin = 2, SkipExpressSettings = 4, SkipOemRegistration = 8, SkipEula = 16                                                                           |
   |      CloudAssignedDomainJoinMethod (número, requerido)      |                                                                                                                                    Esta propiedad especifica si el dispositivo debe unirse Azure Active Directory o Active Directory (Unión a Azure AD híbrido).  Los valores incluyen: Active AD join = 0, Unión a Azure AD híbrido = 1                                                        |
   |      CloudAssignedForcedEnrollment (número, requerido)      |                                                                                                                         Especifica que el dispositivo debe requerir la inscripción de AAD y la inscripción de MDM.  <br>0 = no es necesario, 1 = obligatorio.                                                                                                                         |
   |             ZtdCorrelationId (GUID, obligatorio)              | Un GUID único (sin llaves) que se proporcionará a Intune como parte del proceso de registro. ZtdCorrelationId se incluirá en el mensaje de inscripción como "OfflineAutoPilotEnrollmentCorrelator". Este atributo estará presente solo si la inscripción se realiza en un dispositivo registrado con un aprovisionamiento sin conexión táctil a través del registro sin conexión. |
   | CloudAssignedAadServerData (cadena JSON codificada, requerida) |                                                  Cadena JSON incrustada que se usa para la personalización de marca. Requiere la personalización de marca de AAD Corp habilitada. <br> Valor de ejemplo: "CloudAssignedAadServerData": "{ \" ZeroTouchConfig \" : { \" CloudAssignedTenantUpn \" : \" \" , \" CloudAssignedTenantDomain \" : \" tenant.onmicrosoft.com \" }}"                                                   |
   |         CloudAssignedDeviceName (cadena, opcional)         |                                                                          Nombre asignado automáticamente al equipo.  Esto sigue la Convención de modelo de nomenclatura que se puede configurar en Intune como parte del perfil AutoPilot o puede especificar un nombre explícito para usarlo.                                                                           |


5. El perfil AutoPilot debe guardarse como un archivo JSON en formato ASCII o ANSI. Windows PowerShell tiene como valor predeterminado el formato Unicode, por lo que si intenta redirigir la salida de los comandos a un archivo, también debe especificar el formato de archivo. Por ejemplo, para guardar el archivo en formato ASCII con Windows PowerShell, puede crear un directorio (p. ej., c:\Autopilot) y guardar el perfil, tal como se muestra a continuación: (use la barra de desplazamiento horizontal en la parte inferior si es necesario para ver la cadena de comandos completa)

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON | Out-File c:\Autopilot\AutopilotConfigurationFile.json -Encoding ASCII
    ```
    **Importante**: el nombre de archivo se debe denominar **AutopilotConfigurationFile.js** en, además de codificarse como ASCII/ANSI. 

    Si lo prefiere, puede guardar el perfil en un archivo de texto y editarlo en el Bloc de notas. En el Bloc de notas, al elegir **Guardar como** debe seleccionar Guardar como tipo: **todos los archivos** y elegir ANSI en la lista desplegable junto a **codificación**. Consulte el ejemplo siguiente.

    ![JSON de Bloc de notas](images/notepad.png)

    Después de guardar el archivo, mueva el archivo a una ubicación adecuada como punto de conexión de Microsoft Configuration Manager origen del paquete.

    >[!IMPORTANT]
    >Se pueden usar varios archivos de perfil JSON, pero cada uno debe tener el nombre **AutopilotConfigurationFile.js** en para que Oobe siga la experiencia de AutoPilot. El archivo también se debe codificar como ANSI. <br><br>**Guardar el archivo con codificación Unicode o UTF-8 o guardarlo con un nombre de archivo diferente hará que Windows 10 Oobe no siga la experiencia de AutoPilot**.<br>


### <a name="create-a-package-containing-the-json-file"></a>Crear un paquete que contenga el archivo JSON

1. En Configuration Manager, desplácese hasta **\Software Library\Overview\Application Management\Packages**
2. En la cinta de opciones, haga clic en **crear paquete** .
3. En el **Asistente para crear paquetes y programas** , escriba los detalles de los siguientes **paquetes** y **programas** :<br>
    - <u>Nombre</u>: **AutoPilot para la configuración de dispositivos existentes**
    - Active la casilla **este paquete contiene archivos de origen**
    - <u>Carpeta de origen</u>: haga clic en **examinar** y especifique una ruta de acceso UNC que contenga el AutopilotConfigurationFile.jsen el archivo. 
    - Haga clic en **Aceptar** y luego en **Siguiente**.
    - <u>Tipo de programa</u>: **no crear un programa**
4. Haga clic en **siguiente** dos veces y, a continuación, haga clic en **cerrar**.

**Nota**: Si cambia la configuración del perfil de AutoPilot controlado por el usuario en Intune más adelante, también debe actualizar el archivo JSON y redistribuir el paquete de Configuration Manager asociado.

### <a name="create-a-target-collection"></a>Crear una colección de destino

>[!NOTE]
>También puede optar por volver a usar una colección existente

1. Vaya a **colecciones \Assets y Compliance\Overview\Device**
2. En la cinta de opciones, haga clic en **crear** y luego en **crear recopilación de dispositivos** .
3. En el **Asistente para crear recopilación de dispositivos** , escriba los detalles **generales** siguientes:
   - <u>Nombre</u>: **AutoPilot para la recopilación de dispositivos existentes**
   - Comentario: (opcional)
   - <u>Restricción</u>de la recopilación: haga clic en **examinar** y seleccione **todos los sistemas** .

     >[!NOTE]
     >Opcionalmente, puede optar por usar una colección alternativa para la recopilación de restricción. El dispositivo que se va a actualizar debe ejecutar el agente de ConfigMgr en la colección que seleccione.

4. Haga clic en **siguiente**y escriba los siguientes detalles de las **reglas de pertenencia** :
   - Haga clic en **Agregar regla** y especifique una regla de recopilación directa o basada en consultas para agregar la prueba de destino dispositivos de Windows 7 a la nueva recopilación.
   - Por ejemplo, si el nombre de host del equipo que se va a borrar y recargar es PC-01 y quiere usar el nombre como atributo, haga clic en **Agregar regla > regla directa > (se abre el asistente) > siguiente** y, a continuación, escriba **PC-01** junto a **valor**. Haga clic en **siguiente**y, a continuación, seleccione **PC-01** en **recursos**. Vea los ejemplos siguientes:

     ![Llamado Resource1 ](images/pc-01a.png)
      ![ denominado resource2](images/pc-01b.png)

5. Continúe con la creación de la recopilación de dispositivos con la configuración predeterminada:
    - Usar actualizaciones incrementales para esta recopilación: no seleccionado
    - Programar una actualización completa en esta recopilación: predeterminada
    - Haga clic en **siguiente** dos veces y haga clic en **cerrar** .

### <a name="create-an-autopilot-for-existing-devices-task-sequence"></a>Crear una secuencia de tareas de AutoPilot para dispositivos existentes

>[!TIP]
>El procedimiento siguiente requiere una imagen de arranque para Windows 10 1803 o posterior. Revise las imágenes de arranque disponibles en el Configuration Manager consola en **software Library\Overview\Operating Systems\Boot images** y compruebe que la **versión del sistema operativo** es 10.0.17134.1 (Windows 10 versión 1803) o posterior.

1. En la consola de Configuration Manager, vaya a **\Software Library\Overview\Operating Systems\Task sequences**
2. En la cinta Inicio, haga clic en **crear secuencia de tareas** .
3. Seleccione **instalar un paquete de imágenes existente** y, a continuación, haga clic en **siguiente** .
4. En el Asistente para crear secuencia de tareas, escriba los detalles siguientes:
   - <u>Nombre de secuencia de tareas</u>: **AutoPilot para dispositivos existentes**
   - <u>Imagen de arranque</u>: haga clic en **examinar** y seleccione una imagen de arranque de Windows 10 (1803 o posterior).
   - Haga clic en **siguiente**y, en la página instalar Windows, haga clic en **examinar** y seleccione un **paquete de imágenes** de Windows 10 e índice de **imagen**, versión 1803 o posterior.
   - Active la casilla **partición y formatee el equipo de destino antes de instalar el sistema operativo** .
   - Active o desactive la casilla **configurar secuencia de tareas para usar con BitLocker** . Esto es opcional.
   - <u>Clave de producto</u> y <u>modo de licencia de servidor</u>: opcionalmente, escriba una clave de producto y el modo de licencia de servidor.
   - <u>Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas de soporte técnico (recomendado)</u>: opcional.
   - <u>Habilite la cuenta y especifique la contraseña de administrador local</u>: opcional.
   - Haga clic en **siguiente**y, en la página configurar red, elija **unirse a un grupo de trabajo** y especifique un nombre (por ejemplo, grupo de trabajo) junto a grupo de **trabajo**.

     > [!IMPORTANT]
     > La secuencia de tareas piloto automático para dispositivos existentes ejecutará la acción **preparar Windows para la captura** , que usa la herramienta de preparación del sistema (Sysprep). Se producirá un error en esta acción si el equipo de destino está unido a un dominio.
     
     >[!IMPORTANT]
     > La herramienta de preparación del sistema (Sysprep) se ejecutará con el parámetro/generalize, que, en las versiones 1903 y 1909 de Windows 10, eliminará el archivo de perfil AutoPilot y el equipo arrancará en la fase OOBE en lugar de la fase AutoPilot. Para solucionar este problema, consulte los [problemas conocidos de Windows AutoPilot](known-issues.md).

5. Haga clic en **siguiente**y, a continuación, vuelva a hacer clic en **siguiente** para aceptar la configuración predeterminada en la página instalar Configuration Manager.
6. En la página migración de estado, escriba los detalles siguientes:
   - Desactive la casilla **capturar archivos y configuración de usuario** .
   - Desactive la casilla **capturar configuración de red** .
   - Desactive la casilla **capturar configuración de Microsoft Windows** .
   - Haga clic en **Next**.

     >[!NOTE]
     >Dado que la secuencia de tareas AutoPilot para dispositivos existentes se completa en Windows PE, la migración de datos del kit de herramientas de migración de estado de usuario (USMT) no se admite, ya que no hay forma de restaurar el estado de usuario en el nuevo sistema operativo.  Además, el kit de herramientas de migración de estado de usuario (USMT) no admite dispositivos Unidos a Azure AD.

7. En la página incluir actualizaciones, elija una de las tres opciones disponibles. Esta selección es opcional.
8. En la página instalar aplicaciones, agregue aplicaciones si lo desea. Esto es opcional.
9. Haga clic en **siguiente**, confirme la configuración, haga clic en **siguiente**y, a continuación, haga clic en **cerrar**.
10. Haga clic con el botón derecho en la secuencia de tareas AutoPilot para dispositivos existentes y haga clic en **Editar**.
11. En el editor de secuencia de tareas, en el grupo **instalar sistema operativo** , haga clic en la acción **Aplicar configuración de Windows** .
12. Haga clic en **Agregar** y luego en **nuevo grupo**.
13. Cambie el **nombre** del grupo de **nuevo grupo** a **AutoPilot para configuración de dispositivos existentes**.
14. Haga clic en **Agregar**, seleccione **General**y, a continuación, haga clic en **Ejecutar línea de comandos**.
15. Compruebe que el paso **Ejecutar línea de comandos** está anidado en el grupo **de configuración AutoPilot para dispositivos existentes** .
16. Cambie el **nombre** al **archivo de configuración aplicar AutoPilot para dispositivos existentes** y pegue lo siguiente en el cuadro de texto **línea de comandos** y, a continuación, haga clic en **aplicar**:
    ```
    cmd.exe /c xcopy AutopilotConfigurationFile.json %OSDTargetSystemDrive%\windows\provisioning\Autopilot\ /c
    ```
    -  **AutopilotConfigurationFile.jsen** debe ser el nombre del archivo JSON presente en el paquete AutoPilot para dispositivos existentes creado anteriormente.

17. En el paso **aplicar el piloto automático para el archivo de configuración de dispositivos existentes** , active la casilla **paquete** y, a continuación, haga clic en **examinar**.
18. Seleccione el paquete **de configuración AutoPilot para dispositivos existentes** creado anteriormente y haga clic en **Aceptar**. Al final de esta sección se muestra un ejemplo.
19. En el grupo **sistema operativo de instalación** , haga clic en la tarea **instalar ventanas y Configuration Manager** .
20. Haga clic en **Agregar** y, a continuación, en **nuevo grupo**.
21. Cambiar **el nombre** del **nuevo grupo** para **preparar el dispositivo para el AutoPilot**
22. Compruebe que el grupo **preparar dispositivo para AutoPilot** es el último paso de la secuencia de tareas. Use el botón **bajar** si es necesario.
23. Con el grupo **preparar dispositivo para AutoPilot** seleccionado, haga clic en **Agregar**, seleccione **imágenes** y, a continuación, haga clic en **preparar cliente de Configuration Manager para la captura**.
24. Agregue un segundo paso; para ello, haga clic en **Agregar**, seleccione **imágenes**y haga clic en **preparar Windows para la captura**. Utilice la siguiente configuración en este paso:
    - <u>Generar automáticamente lista de controladores de almacenamiento masivo</u>: **no seleccionado**
    - No <u>restablecer la marca de activación</u>: **no seleccionado**
    - <u>Apagar el equipo después de ejecutar esta acción</u>: **opcional**

    ![Secuencia de tareas de AutoPilot](images/ap-ts-1.png)

25. Haga clic en **Aceptar** para cerrar el editor de secuencia de tareas.

> [!NOTE]
> En Windows 10 1903 y 1909, el paso **preparar Windows para la captura** elimina el **AutopilotConfigurationFile.jsactivado** . Consulte [problemas conocidos de Windows AutoPilot](known-issues.md) para obtener más información y una solución alternativa.

### <a name="deploy-content-to-distribution-points"></a>Implementar contenido en puntos de distribución

A continuación, asegúrese de que todo el contenido necesario para la secuencia de tareas se implementa en los puntos de distribución.

1. Haga clic con el botón derecho en la secuencia **de tareas piloto automático para dispositivos existentes** y haga clic en **distribuir contenido**.
2. Haga clic en **siguiente**, **Revise el contenido que desea distribuir**y, a continuación, haga clic en **siguiente**.
3. En la página especificar la distribución de contenido, haga clic en **Agregar** para especificar un **punto de distribución** o un grupo de **puntos de distribución**.
4. En el Asistente para agregar puntos de distribución o agregar grupos de puntos de distribución, especifique los destinos de contenido que permitirán recuperar el archivo JSON cuando se ejecute la secuencia de tareas.
5. Cuando haya terminado de especificar la distribución de contenido, haga clic en **siguiente** dos veces y haga clic en **cerrar**.

### <a name="deploy-the-os-with-autopilot-task-sequence"></a>Implementación del sistema operativo con la secuencia de tareas AutoPilot

1. Haga clic con el botón derecho en la secuencia **de tareas piloto automático para dispositivos existentes** y, a continuación, haga clic en **implementar**.
2. En el Asistente para implementar software, escriba los siguientes detalles **generales** y de **configuración de implementación** :
    - <u>Secuencia de tareas</u>:  **AutoPilot para dispositivos existentes**.
    - <u>Recopilación</u>: haga clic en **examinar** y seleccione **AutoPilot para recopilación de dispositivos existentes** (u otra colección que prefiera).
    - Haga clic en **siguiente** para especificar la **configuración de implementación**.
    - <u>Acción</u>: **instalar**.
    - <u>Propósito</u>: **disponible**. Opcionalmente, puede seleccionar **requerido** en lugar de **disponible**. Esto no se recomienda durante la prueba debido al posible impacto de las configuraciones involuntarias.
    - <u>Haga que esté disponible para lo siguiente</u>: **solo Configuration Manager clientes**. Nota: elija aquí la opción que sea relevante para el contexto de la prueba. Si el cliente de destino no tiene instalado el agente de Configuration Manager o Windows, deberá seleccionar una opción que incluya PXE o medios de arranque.
    - Haga clic en **siguiente** para especificar los detalles de la **programación** .
    - <u>Programar Cuándo estará disponible esta implementación</u>: opcional
    - <u>Programar Cuándo expirará esta implementación</u>: opcional
    - Haga clic en **siguiente** para especificar los detalles de la **experiencia del usuario** .
    - <u>Mostrar progreso</u>de la secuencia de tareas: seleccionado.
    - <u>Instalación de software</u>: no seleccionada.
    - <u>Reinicio del sistema (si es necesario para completar la instalación)</u>: no seleccionado.
    - <u>Confirmación modificada en la fecha límite o durante una ventana de mantenimiento (reinicio necesario)</u>: opcional.
    - <u>Permitir que la secuencia de tareas se ejecute para el cliente en Internet</u>: opcional
    - Haga clic en **siguiente** para especificar los detalles de **alertas** .
    - <u>Cree una alerta de implementación cuando el umbral sea mayor que el siguiente</u>: opcional.
    - Haga clic en **siguiente** para especificar los detalles de los **puntos de distribución** .
    - <u>Opciones de implementación</u>: **Descargue el contenido localmente cuando sea necesario mediante la secuencia de tareas en ejecución**.
    - <u>Cuando no hay ningún punto de distribución local disponible, use un punto de distribución remoto</u>: opcional.
    - <u>Permitir a los clientes usar puntos de distribución del grupo de límites de sitio predeterminado</u>: opcional.
    - Haga clic en **siguiente**, confirme la configuración, haga clic en **siguiente**y, a continuación, haga clic en **cerrar**.

### <a name="complete-the-client-installation-process"></a>Completar el proceso de instalación del cliente

1. Abra el centro de software en el equipo cliente de Windows 7 o Windows 8.1 de destino. Para ello, haga clic en Inicio y, a continuación, escriba **software** en el cuadro de búsqueda o escriba lo siguiente en Windows PowerShell o en el símbolo del sistema:

    ```
    C:\Windows\CCM\SCClient.exe
    ```

2. En la biblioteca de software, seleccione **AutoPilot para dispositivos existentes** y haga clic en **instalar**. Observe el ejemplo siguiente:

    ![Denominado resource2 ](images/sc.png) ![ denominado resource2](images/sc1.png)

La secuencia de tareas descargará el contenido, lo reiniciará, formateará las unidades e instalará Windows 10. Después, el dispositivo se preparará para el piloto automático. Una vez completada la secuencia de tareas, el dispositivo arrancará en OOBE y proporcionará una experiencia de AutoPilot.

![actualización-1 actualización- ](images/up-1.png)
 ![ 2 ](images/up-2.png)
 ![ actualización-3](images/up-3.png)

>[!NOTE]
>Si se unen dispositivos a Active Directory (Unión a Azure AD híbrido), es necesario crear un perfil de configuración de dispositivo de unión a un dominio que esté destinado a "todos los dispositivos" (ya que no hay ningún objeto de dispositivo Azure Active Directory para que el equipo realice la creación de destinatarios basada en grupos).  Vea [modo basado en el usuario para la Unión de Azure Active Directory híbridas](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join) para obtener más información.

### <a name="register-the-device-for-windows-autopilot"></a>Registrar el dispositivo para Windows AutoPilot

Los dispositivos aprovisionados a través de AutoPilot solo recibirán la experiencia guiada del piloto automático de OOBE en el primer arranque. Una vez que se haya actualizado a Windows 10, el dispositivo debe estar registrado para garantizar una experiencia de autopiloto continuada en caso de que se restablezca el equipo. Puede habilitar el registro automático para un grupo asignado mediante la configuración **convertir todos los dispositivos de destino en AutoPilot** . Para más información, vea [Crear un perfil de implementación de Autopilot](enrollment-autopilot.md#create-an-autopilot-deployment-profile).

Consulte también [Agregar dispositivos a Windows AutoPilot](add-devices.md).

## <a name="speeding-up-the-deployment-process"></a>Acelerar el proceso de implementación

Para quitar unos 20 minutos del proceso de implementación, consulte el blog de Michael Niehaus con instrucciones para [acelerar Windows AutoPilot para dispositivos existentes](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices).