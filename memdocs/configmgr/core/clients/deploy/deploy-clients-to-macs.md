---
title: Implementación de clientes Mac
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar clientes en equipos Mac con Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694033"
---
# <a name="how-to-deploy-clients-to-macs"></a>Cómo implementar clientes en equipos Mac

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se describe cómo implementar y mantener el cliente de Configuration Manager en equipos Mac. Para obtener información sobre qué se debe configurar antes de implementar clientes en equipos Mac, vea [Prepararse para implementar software cliente en equipos Mac](prepare-to-deploy-mac-clients.md).

Cuando instale un nuevo cliente para equipos Mac, es posible que tenga que instalar también actualizaciones de Configuration Manager para reflejar la nueva información de cliente en la consola de Configuration Manager.

En estos procedimientos, tiene dos opciones para instalar los certificados de cliente. Obtenga más información sobre los certificados de cliente para equipos Mac en [Prepararse para implementar software cliente en equipos Mac](prepare-to-deploy-mac-clients.md#certificate-requirements).  

- Usar la inscripción de Configuration Manager mediante la [herramienta CMEnroll](#bkmk_enroll). El proceso de inscripción no admite la renovación automática de certificados. Vuelva a inscribir el equipo Mac antes de que expire el certificado instalado.    

- [Usar una solicitud de certificado y un método de instalación independiente de Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> Para implementar el cliente en dispositivos que ejecutan macOS Sierra, configure correctamente el **nombre de asunto** del certificado de punto de administración. Por ejemplo, use el FQDN del servidor de punto de administración.



## <a name="configure-client-settings"></a>Configuración del cliente  

Use la [configuración de cliente predeterminada](about-client-settings.md) para configurar la inscripción de equipos Mac. No puede usar la configuración de cliente personalizada. Para solicitar e instalar el certificado, el cliente de Configuration Manager para Mac requiere la configuración de cliente predeterminada.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Seleccione el nodo **Configuración de cliente** y, después, haga clic en **Configuración de cliente predeterminada**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.  

3. Haga clic en la sección **Inscripción** y, luego, establezca la configuración siguiente:  

    1. **Permitir a los usuarios inscribir dispositivos móviles y equipos Mac**: **Sí**  

    2. **Perfil de inscripción:** seleccione **Establecer perfil**.  

4. En el cuadro de diálogo **Perfil de inscripción de dispositivo móvil**, seleccione **Crear**.  

5. En el cuadro de diálogo **Crear perfil de inscripción**, escriba un nombre para este perfil de inscripción. Después, configure el **Código del sitio de administración**. Seleccione el sitio primario de Configuration Manager que contiene los puntos de administración para estos equipos Mac.  

    > [!NOTE]  
    >  Si no puede seleccionar el sitio, asegúrese de que configura como mínimo un punto de administración en el sitio para admitir dispositivos móviles.  

6. Seleccione **Agregar**.  

7. En la ventana **Agregar entidad de certificación para dispositivos móviles**, seleccione el servidor de la entidad de certificación (CA) que emite certificados a equipos Mac.  

8. En el cuadro de diálogo **Crear perfil de inscripción**, seleccione la plantilla de certificado del equipo Mac que ha creado previamente.  

9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Perfil de inscripción** y en el cuadro de diálogo **Configuración de cliente predeterminada**.  

    > [!TIP]  
    > Si quiere cambiar el intervalo de directivas de cliente, use el **Intervalo de sondeo de directiva de cliente** en el grupo de configuración de cliente **Directiva de cliente**.  

La próxima vez que los dispositivos descarguen la directiva de cliente, Configuration Manager aplicará esta configuración a todos los usuarios. Para iniciar la recuperación de directivas para un solo cliente, vea [Iniciar la recuperación de directivas para un cliente de Configuration Manager](../manage/manage-clients.md#BKMK_PolicyRetrieval).  

Además de la configuración de cliente de inscripción, asegúrese de que ha configurado las siguientes opciones del dispositivo de cliente:  

- **Inventario de hardware**: habilite y configure esta característica si quiere recopilar el inventario de hardware desde equipos cliente Mac y Windows. Para obtener más información, vea [Cómo ampliar el inventario de hardware](../manage/inventory/extend-hardware-inventory.md).  

- **Configuración de cumplimiento**: habilite y configure esta característica si quiere evaluar y corregir la configuración en los equipos cliente Mac y Windows. Para obtener más información, consulte [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Planear y configurar la configuración de cumplimiento).  

Para obtener más información, vea [Cómo configurar el cliente](configure-client-settings.md).  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a> Descarga del cliente para macOS

1. Descargue el paquete de archivos del cliente macOS, [Microsoft Endpoint Configuration Manager: cliente macOS (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850). Guarde **ConfigmgrMacClient.msi** en un equipo que ejecute Windows. Este archivo no se encuentra en los medios de instalación de Configuration Manager.  

2. Ejecute el instalador en el equipo Windows. Extraiga el paquete de cliente Mac, **Macclient.dmg**, en una carpeta del disco local. La ruta de acceso predeterminada es `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`.  

3. Copie el archivo **Macclient.dmg** en una carpeta del equipo Mac.  

4. En el equipo Mac, ejecute **Macclient.dmg** para extraer los archivos en una carpeta del disco local.  

5. Asegúrese de que la carpeta contiene los archivos siguientes: 

    - **Ccmsetup**: instala el cliente de Configuration Manager en los equipos Mac mediante **CMClient.pkg**.  

    - **CMDiagnostics**: recopila información de diagnóstico relacionada con el cliente de Configuration Manager en los equipos Mac.  

    - **CMUninstall**: desinstala el cliente de los equipos Mac.  

    - **CMAppUtil**: convierte paquetes de aplicaciones de Apple en un formato que se pueda implementar como una aplicación de Configuration Manager.  

    - **CMEnroll**: solicita e instala el certificado de cliente para un equipo Mac, de modo que pueda instalar después el cliente de Configuration Manager.  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a> Inscribir el cliente de Mac  

Inscriba los clientes individuales con el [Asistente para inscripción de equipos Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Para automatizar la inscripción para muchos clientes, use la [herramienta CMEnroll](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Inscribir el cliente mediante el Asistente para inscripción de equipos Mac  

1. Después de instalar el cliente, se abre el Asistente para inscripción de equipos. Para iniciar manualmente el asistente, seleccione **Inscribir** en la página de preferencias de **Configuration Manager**.  

2. En la segunda página del asistente, especifique la siguiente información:  

   - **Nombre de usuario**: El nombre de usuario puede adoptar los siguientes formatos:  

     - `domain\name`. Por ejemplo: `contoso\mnorth`  

     - `user@domain`. Por ejemplo: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Cuando se usa una dirección de correo electrónico para rellenar el campo **Nombre de usuario**, Configuration Manager rellena automáticamente el campo **Nombre del servidor**. Usa el nombre predeterminado del servidor del punto de proxy de inscripción y el nombre de dominio de la dirección de correo electrónico. Si estos nombres no coinciden con el nombre del servidor del punto de proxy de inscripción, corrija el **nombre del servidor** durante la inscripción.  

       El nombre de usuario y la contraseña correspondiente deben coincidir con una cuenta de usuario de Active Directory con permisos de **lectura** e **inscripción** en la plantilla de certificado de cliente de Mac.  

   - **Nombre de servidor**: nombre del servidor del punto de proxy de inscripción.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automatización del cliente y el certificado con CMEnroll  

Use este procedimiento para automatizar la instalación del cliente y solicitar e inscribir certificados de cliente con la herramienta CMEnroll. Para ejecutar la herramienta, debe tener una cuenta de usuario de Active Directory.

1. En el equipo Mac, vaya a la carpeta en la que ha extraído el contenido del archivo **Macclient.dmg**.  

2. Escriba este comando: `sudo ./ccmsetup`  

3. Espere hasta que vea el mensaje de **instalación completada** . Aunque el instalador muestra un mensaje que indica que debe reiniciar ahora, no lo haga y continúe con el paso siguiente.  

4. En la carpeta **Tools** del equipo Mac, escriba el comando siguiente: `sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`.  

    Una vez instalado del cliente, se abrirá el asistente para inscripción de equipos Mac que lo ayudará a inscribir el equipo Mac. Para obtener más información, vea [Inscribir el cliente mediante el Asistente para inscripción de equipos Mac](#bkmk_enroll).  

     Ejemplo: si el servidor del punto de proxy de inscripción se denomina **server02.contoso.com** y ha concedido permisos **contoso\mnorth** para la plantilla de certificado de cliente Mac, escriba lo siguiente: `sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`.  

    > [!NOTE]  
    > Si el nombre de usuario incluye alguno de los siguientes caracteres, se producirá un error en la inscripción: `<>"+=,`. Use un certificado de fuera de banda con un nombre de usuario que no contenga estos caracteres.  
    >  
    > Para que la experiencia de usuario sea más sencilla, incluya los pasos de instalación en un script. Así, los usuarios solo tendrán que proporcionar su nombre de usuario y contraseña.  

5. Escriba la contraseña de la cuenta de usuario de Active Directory. Cuando escriba este comando, le pedirá dos contraseñas. La primera es para que la cuenta de superusuario ejecute el comando. La segunda es para la cuenta de usuario de Active Directory. Los mensajes de solicitud son idénticos, así que asegúrese de especificar las credenciales en la secuencia correcta.  

6. Espere hasta que vea el mensaje de **inscripción correcta** .  

7. Para limitar el certificado inscrito a Configuration Manager, en el equipo Mac, abra una ventana de terminal y realice los cambios siguientes:  

    1. Escriba el comando `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`.  

    2. En la ventana **Keychain Access** (Acceso a llaveros), en la sección **Llaveros**, seleccione **Sistema**. Después, en la sección **Categoría**, seleccione **Claves**.  

    3. Expanda los llaveros para ver los certificados de cliente. Busque el certificado con una clave privada que haya instalado y abra la clave.  

    4. En la pestaña **Control de acceso**, seleccione **Confirm before allowing access** (Confirmar antes de permitir el acceso).  

    5. Vaya a **/Library/Application Support/Microsoft/MCC**, elija **CCMClient** y, después, seleccione **Agregar**.  

    6. Seleccione **Guardar cambios** y cierre el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves).  

8. Reinicie el equipo Mac.  

Para comprobar que la instalación de cliente se ha realizado correctamente, abra el elemento **Configuration Manager** en **Preferencias del sistema** en el equipo Mac. También puede actualizar y ver la recopilación **Todos los sistemas** en la consola de Configuration Manager para confirmar que el equipo Mac aparece en esta recopilación como un cliente administrado.  

> [!TIP]  
> Para ayudar a solucionar problemas del cliente de Mac, emplee la herramienta **CMDiagnostics** que se incluye con el paquete de cliente Mac. Úsela para recopilar la información de diagnóstico siguiente:  
>   
> - Una lista de procesos en ejecución  
> - La versión del sistema operativo Mac OS X  
> - Informes de bloqueo de Mac OS X relacionados con el cliente de Configuration Manager, incluidos **CCM\*.crash** y **System Preference.crash**.  
> - El archivo de lista de materiales (L. Mat) y el archivo de lista de propiedades (.plist) creados por la instalación de cliente de Configuration Manager.  
> - El contenido de la carpeta **/Library/Application Support/Microsoft/CCM/Logs**.  
>   
> La información recopilada por CmDiagnostics se agrega a un archivo zip que se guarda en el escritorio del equipo con el nombre `cmdiag-<hostname>-<datetime>.zip`



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a> Administrar certificados externos a Configuration Manager

Puede usar una solicitud de certificado y un método de instalación independiente de Configuration Manager. Use el mismo proceso general, pero incluya los siguientes pasos adicionales: 

- Al instalar el cliente de Configuration Manager, use las opciones de línea de comandos **MP** y **SubjectName**. Escriba este comando: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. El nombre de asunto del certificado distingue mayúsculas de minúsculas, por tanto escríbalo tal como aparece en los detalles del certificado.  

     Ejemplo: el FQDN de Internet del punto de administración es **server03.contoso.com**. El certificado de cliente Mac tiene el FQDN **mac12.contoso.com** como nombre común en el asunto del certificado. Use el comando siguiente: `sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`.  

- Si tiene más de un certificado que contiene el mismo asunto, especifique el número de serie de certificado que quiere usar para el cliente de Configuration Manager. Use el comando siguiente: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Por ejemplo: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Renovar el certificado de cliente Mac  

Este procedimiento quita el SMSID. El cliente de Configuration Manager para Mac requiere un identificador nuevo para usar un certificado nuevo o renovado.  

> [!IMPORTANT]  
> Después de reemplazar el SMSID del cliente, cuando elimine el recurso antiguo de la consola de Configuration Manager, también eliminará el historial del cliente almacenado. Por ejemplo, el historial del inventario de hardware de ese cliente.  


1. Cree y rellene una recopilación de dispositivos para los equipos Mac que deben renovar los certificados de equipo.  

2. En el área de trabajo **Activos y compatibilidad** , inicie el **Asistente para crear elemento de configuración**.  

3. En la página **General** del asistente, especifique la siguiente información:  

    - **Nombre**: **Quitar el SMSID para Mac**  

    - **Tipo**: **Mac OS X**  

4. En la página **Plataformas admitidas**, seleccione todas las versiones de Mac OS X.  

5. En la página **Configuración**, seleccione **Nuevo**. En la ventana **Crear configuración**, especifique la siguiente información:  

    - **Nombre**: **Quitar el SMSID para Mac**  

    - **Tipo de configuración**: **Script**  

    - **Tipo de datos**: **Cadena**  

6. En la ventana **Crear configuración**, para **Script de detección**, seleccione **Agregar script**. Esta acción especifica un script para detectar equipos Mac configurados con un SMSID.  

7. En la ventana **Editar script de detección**, escriba el siguiente script de shell:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Haga clic en **Aceptar** para cerrar la ventana **Editar script de detección**.  

9. En la ventana **Crear configuración**, para **Script de corrección (opcional)** , seleccione **Agregar script**. Esta acción especifica un script para quitar el SMSID cuando se encuentra en los equipos Mac.  

10. En la ventana **Crear script de corrección**, escriba el siguiente script de shell:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Haga clic en **Aceptar** para cerrar la ventana **Crear script de corrección**.  

12. En la página **Reglas de cumplimiento**, seleccione **Nuevo**. Después, en la ventana **Crear regla**, especifique la siguiente información:  

    - **Nombre**: **Quitar el SMSID para Mac**  

    - **Configuración seleccionada**: haga clic en **Examinar** y seleccione el script de detección especificado previamente.  

    - En el campo **los siguientes valores**, escriba: **El dominio/par predeterminado (com.microsoft.ccmclient, SMSID) no existe**.  

    - Habilite la opción **Ejecutar el script de corrección especificado cuando esta configuración no sea compatible**.  

13. Complete el asistente.  

14. Creare una línea base de configuración que contenga este elemento de configuración. Implemente la línea base en la recopilación de destino.  

     Para obtener más información, vea [Crear líneas base de configuración](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Después de instalar un nuevo certificado en los equipos Mac a los que se ha quitado el SMSID, ejecute el siguiente comando para configurar el cliente para usar el nuevo certificado:  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Vea también

[Preparar la implementación de clientes en equipos Mac](prepare-to-deploy-mac-clients.md)

[Mantenimiento de clientes Mac](../manage/maintain-mac-clients.md)
