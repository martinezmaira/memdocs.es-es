---
title: Modo controlado por el usuario de Windows AutoPilot
description: Con el modo controlado por el usuario de Windows AutoPilot, puede configurar los dispositivos para que se implementen en un estado listo para usar sin necesidad de ayuda del personal de ti.
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
ms.openlocfilehash: 09632eccf99774d4170fe60f51b6703cd8b90fed
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907923"
---
# <a name="windows-autopilot-user-driven-mode"></a>Modo controlado por el usuario de Windows Autopilot

**Se aplica a: Windows 10, versión 1809 o posterior**

El modo controlado por el usuario de Windows AutoPilot le permite configurar nuevos dispositivos Windows 10 para que los transformen automáticamente desde su estado de fábrica hasta un estado listo para usar. Este proceso no requiere que el personal de ti toque el dispositivo.

El proceso es sencillo para que cualquier persona pueda completarlo. Los dispositivos se pueden enviar o distribuir al usuario final directamente con instrucciones sencillas:

1. Vuelva a aplicar la conversión unboxing del dispositivo, conéctelo y enciéndalo.
2. Elija un idioma (solo es necesario cuando se instalan varios idiomas), configuración regional y teclado.
3. Conéctelo a una red inalámbrica o cableada con acceso a Internet. Si usa la red inalámbrica, el usuario debe establecer el vínculo de Wi-Fi. 
4. Especifique la dirección de correo electrónico y la contraseña de la cuenta de la organización.

El resto del proceso se automatiza, como el dispositivo:
1. Se une a la organización.
2. Inscribe en Intune (u otro servicio MDM)
3. Está configurado según la definición de la organización.

Cualquier solicitud adicional durante la ejecución rápida (OOBE) se puede suprimir. consulte [configuración de perfiles de AutoPilot](profiles.md) para ver las opciones disponibles.

El modo controlado por el usuario de Windows AutoPilot admite dispositivos Azure Active Directory e híbridos Unidos Azure Active Directory. Para obtener más información sobre estas dos opciones de combinación, consulte [¿Qué es una identidad de dispositivo](/azure/active-directory/devices/overview)?

El flujo de proceso completado durante el proceso controlado por el usuario es el siguiente:

1. Después de conectarse a una red, el dispositivo descarga un perfil de Windows AutoPilot. El perfil define la configuración utilizada para el dispositivo. Por ejemplo, defina los mensajes suprimidos durante OOBE.
2. Windows 10 comprueba las actualizaciones de OOBE críticas. Si hay actualizaciones disponibles, se instalan automáticamente (si es necesario, se reinician).
3. Se solicita al usuario Azure Active Directory credenciales. Esta experiencia de usuario personalizada muestra el nombre del inquilino Azure AD, el logotipo y el texto de inicio de sesión.
4.  El dispositivo se une Azure Active Directory o Active Directory, en función de la configuración del perfil de Windows AutoPilot.
5. El dispositivo se inscribe en Intune (u otros servicios MDM configurados). En función de las necesidades de la organización, se produce esta inscripción:
    - durante el proceso de Unión Azure Active Directory mediante la inscripción automática de MDM
    - o antes del proceso de unión de Active Directory.
6. Si está configurado, se mostrará la [Página de estado de inscripción](enrollment-status.md) (ESP).
7. Una vez completadas las tareas de configuración del dispositivo, el usuario inicia sesión en Windows 10 con las credenciales proporcionadas anteriormente. (Si el dispositivo se reinicia durante el proceso de ESP del dispositivo, el usuario debe volver a escribir sus credenciales, ya que estos detalles no se conservan en los reinicios).
8. Después del inicio de sesión, se muestra la página estado de inscripción para las tareas de configuración de destino del usuario.

Si se detecta algún problema durante este proceso, consulte la documentación de [solución de problemas de Windows AutoPilot](troubleshooting.md) .

Para obtener más información sobre las opciones de combinación disponibles, vea las siguientes secciones:

- [Azure Active Directory combinación](#user-driven-mode-for-azure-active-directory-join) está disponible si no es necesario que los dispositivos estén Unidos a un dominio de Active Directory local.
- La [Unión híbrida Azure Active Directory](#user-driven-mode-for-hybrid-azure-active-directory-join) está disponible para los dispositivos que deben estar unidos a Azure Active Directory y al dominio de Active Directory local.

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Modo basado en el usuario para Azure Active Directory join

Para completar una implementación controlada por el usuario mediante Windows AutoPilot, siga estos pasos de preparación:

1. Asegúrese de que los usuarios que van a realizar implementaciones en modo controlado por el usuario pueden unir dispositivos a Azure Active Directory. Para obtener más información, consulte [Configure Device Settings](/azure/active-directory/device-management-azure-portal#configure-device-settings) en la documentación de Azure Active Directory.
2. Cree un perfil de AutoPilot para el modo controlado por el usuario con la configuración deseada. En Microsoft Intune, este modo se elige explícitamente al crear el perfil. Con Microsoft Store para la empresa y el centro de Partners, el modo controlado por el usuario es el valor predeterminado y no es necesario seleccionarlo.
3. Si usa Intune, cree un grupo de dispositivos en Azure Active Directory y asigne el perfil de AutoPilot a ese grupo.

Estos pasos adicionales son necesarios para cada dispositivo que se va a implementar mediante la implementación controlada por el usuario:

- Asegúrese de que el dispositivo se ha agregado a Windows AutoPilot. La adición de un dispositivo a Windows AutoPilot puede realizarse de dos maneras:
  - Automáticamente por un OEM o un asociado en el momento en que se adquiere el dispositivo
  - Recopilación manual, como se describe en [Agregar dispositivos a Windows AutoPilot](add-devices.md).
- Asegúrese de que se ha asignado un perfil de AutoPilot al dispositivo:
 - Si usa Intune y Azure Active Directory grupos de dispositivos dinámicos, esta asignación puede realizarse automáticamente.
 - Si usa Intune y Azure Active Directory grupos de dispositivos estáticos, agregue manualmente el dispositivo al grupo de dispositivos.
 - Si usa otros métodos (por ejemplo, Microsoft Store para la empresa o el centro de Partners), asigne manualmente un perfil AutoPilot al dispositivo.


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>Modo controlado por el usuario para la Unión de Azure Active Directory híbrida

Windows AutoPilot requiere que los dispositivos estén Azure Active Directory Unidos. Si tiene un entorno de Active Directory local, puede unir dispositivos a su dominio local. Para unirse a los dispositivos, debe configurar los dispositivos AutoPilot para que estén [Unidos a Azure Active Directory (Azure ad)](/azure/active-directory/devices/hybrid-azuread-join-plan). 

### <a name="requirements"></a>Requisitos

Para realizar una implementación híbrida orientada a Azure AD basada en el usuario mediante Windows AutoPilot:

- Se debe crear un perfil de Windows AutoPilot para el modo controlado por el usuario y 
 - **Azure ad híbrido** join debe especificarse como la opción seleccionada en **unirse a Azure ad como** en el perfil de AutoPilot.
- Si usa Intune, debe existir un grupo de dispositivos en Azure Active Directory con el perfil de Windows AutoPilot asignado a ese grupo.
- El dispositivo debe ejecutar Windows 10, versión 1809 o posterior.
- El dispositivo debe tener acceso a un controlador de dominio de Active Directory. Debe estar conectado a la red de la organización. Debe ser capaz de resolver los registros DNS para el dominio de AD y el controlador de dominio de AD. Debe ser capaz de comunicarse con el controlador de dominio para autenticar al usuario.
- El dispositivo debe poder tener acceso a Internet, según los [requisitos de red de Windows AutoPilot documentados](networking-requirements.md).
- Se debe instalar el conector de Intune para Active Directory.
 - Nota: el conector de Intune realizará una Unión a AD local. Por lo tanto, los usuarios no necesitan el permiso AD-join local. Se supone que el conector está [configurado para realizar esta acción](/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) en nombre del usuario. 
- Si utiliza el proxy, la opción de configuración del proxy WPAD debe estar activada y configurada.

**Azure ad Unión de dispositivos**: el proceso híbrido de unión a Azure ad utiliza el contexto del sistema para realizar la combinación de Azure ad de dispositivos. No se ve afectado por la configuración de permisos de unión de Azure AD basada en el usuario. Todos los usuarios pueden unir dispositivos a Azure AD de forma predeterminada.

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>Modo controlado por el usuario para la Unión de Azure Active Directory híbridos con compatibilidad con VPN

Los dispositivos Unidos a Active Directory requieren conectividad con un controlador de dominio Active Directory para muchas actividades. Estas actividades incluyen el inicio de sesión de usuario (validación de las credenciales del usuario) y directiva de grupo aplicación. Como resultado, el proceso de Unión a Azure AD híbrido de Windows AutoPilot controlado por el usuario validaría que el dispositivo pueda ponerse en contacto con un controlador de dominio de Active Directory haciendo ping a dicho controlador de dominio.

Además de la compatibilidad con VPN para este escenario, puede configurar el proceso de Unión a Azure AD híbrido para omitir la comprobación de conectividad. Esto no elimina la necesidad de comunicarse con un controlador de dominio de Active Directory. En su lugar, para permitir la conexión a la red de la organización, Intune proporciona la configuración de VPN necesaria antes de que el usuario intente iniciar sesión en Windows. 


### <a name="requirements"></a>Requisitos

Para Unión a Azure AD híbrido con compatibilidad con VPN, se aplican los siguientes requisitos adicionales:

- Una versión compatible de Windows 10:
 - Actualización acumulativa de Windows 10 1903 + 10 de diciembre (KB4530684, compilación de SO 18362,535) o superior 
 - Actualización acumulativa de Windows 10 1909 + 10 de diciembre (KB4530684, compilación de SO 18363,535) o superior 
 - Windows 10 2004 o posterior 
- Habilite la nueva alternancia "Omitir comprobación de conectividad de dominio" en el perfil de AutoPilot de Unión a Azure AD híbrido.
- Una configuración de VPN que:
  - se puede implementar con Intune y permite al usuario establecer manualmente una conexión VPN desde la pantalla de inicio de sesión de Windows.
  - uno que establece automáticamente una conexión VPN según sea necesario. 

La configuración de VPN específica necesaria depende del software de VPN y de la autenticación que se use. En el caso de las soluciones VPN de terceros (que no sean de Microsoft), esto normalmente implicaría la implementación de una aplicación Win32 (que contenía el software cliente de VPN en sí y cualquier información de conexión específica, por ejemplo: nombres de host de punto de conexión de VPN) a través de las extensiones de administración de Intune. Consulte la documentación del proveedor de VPN para obtener detalles de configuración específicos de ese proveedor.

> [!NOTE]
> Los requisitos de VPN no son específicos de Windows AutoPilot. Por ejemplo, si ya ha implementado una configuración de VPN para habilitar los restablecimientos de contraseñas remotos, en los que un usuario necesita iniciar sesión en Windows con una nueva contraseña cuando no está en la red de la organización, se puede usar la misma configuración con Windows AutoPilot. Una vez que el usuario ha iniciado sesión para almacenar en caché sus credenciales, los intentos de inicio de sesión posteriores no necesitan conectividad, ya que se pueden usar las credenciales almacenadas en caché. 

En los casos en los que el software de VPN requiere autenticación de certificado, el certificado de equipo necesario también debe implementarse a través de Intune. Esta implementación se puede realizar mediante las funcionalidades de inscripción de certificados de Intune, que se dirigen a los perfiles de certificado para el dispositivo.

No se admiten certificados de usuario porque no se pueden implementar hasta que el usuario inicia sesión. Además, dado que no se instalan hasta que el usuario inicia sesión, no se admiten los complementos VPN de UWP de Microsoft entregados desde la tienda Windows.

### <a name="validation"></a>Validación

Antes de intentar una Unión híbrida Azure AD mediante VPN, es importante confirmar que se puede realizar un proceso de Unión a Azure AD híbrido controlado por el usuario en la red de la organización. Esta confirmación simplifica la solución de problemas asegurándose de que el proceso principal funciona antes de agregar la configuración de VPN adicional necesaria.

A continuación, compruebe que la configuración de VPN (aplicación Win32, certificados y cualquier otro requisito) se puede implementar con Intune en un dispositivo existente que ya se ha unido Azure AD híbrido. Por ejemplo, algunos clientes VPN crean una conexión VPN por equipo como parte del proceso de instalación. Por lo tanto, puede validar la configuración mediante pasos como estos:

- En PowerShell, compruebe que se ha creado al menos una conexión VPN por equipo mediante el comando "Get-VpnConnection-AllUserConnection".
- Intente iniciar manualmente la conexión VPN con el comando: RASDIAL.EXE "ConnectionName"
- Cierre la sesión y compruebe que el icono de "conexión VPN" se puede ver en la página de inicio de sesión de Windows.
- Mueva el dispositivo fuera de la red corporativa e intente establecer la conexión con el icono de la página de inicio de sesión de Windows. Inicie sesión en una cuenta que no tenga credenciales almacenadas en caché.

En el caso de las configuraciones de VPN que se conectan automáticamente, los pasos de validación pueden ser diferentes.

> [!NOTE]
> Se puede usar Always On VPN para este escenario. Para obtener más información, consulte la documentación de [implementación de Always on VPN](/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) . Tenga en cuenta que Intune aún no puede implementar el perfil de VPN por equipo necesario. 

Para validar el proceso, asegúrese de que se ha instalado la actualización acumulativa de Windows 10 necesaria en Windows 10 1903 o Windows 10 1909. Puede instalar manualmente la actualización durante OOBE descargando primero la versión acumulativa más reciente de https://catalog.update.microsoft.com . Siga estos pasos:

1. Presione Mayús + F10 para abrir un símbolo del sistema.
2. Inserte una clave USB que contenga la actualización descargada.
3. Instale la actualización con el comando (sustituyendo el nombre de archivo real): WUSA.EXE <filename> . msu/Quiet
4. Reinicie el equipo con el comando: shutdown.exe/r/t 0

O bien, puede iniciar Windows Update para instalar las actualizaciones más recientes:

1. Presione Mayús + F10 para abrir un símbolo del sistema.
2. Ejecute el comando "Start MS-Settings:"
3. Navegue hasta el nodo "actualizar seguridad de &" y compruebe si hay actualizaciones.
4. Reiniciar después de instalar las actualizaciones.

### <a name="step-by-step-instructions"></a>Instrucciones paso a paso

Consulte [implementar dispositivos híbridos Unidos a Azure ad mediante Intune y Windows AutoPilot](/intune/windows-autopilot-hybrid).