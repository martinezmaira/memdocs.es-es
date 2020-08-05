---
title: Modo controlado por el usuario de Windows AutoPilot
description: El modo controlado por el usuario de Windows AutoPilot permite que los dispositivos se implementen en un estado listo para su uso sin necesidad de ayuda del personal de ti.
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
ms.openlocfilehash: b5e7c88272f8da386d25e7e7bca1973026f4407a
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757062"
---
# <a name="windows-autopilot-user-driven-mode"></a>Modo controlado por el usuario de Windows Autopilot

**Se aplica a: Windows 10, versión 1809 o posterior**

El modo controlado por el usuario de Windows AutoPilot está diseñado para permitir que los nuevos dispositivos de Windows 10 se transformen de su estado de fábrica inicial en un estado listo para usar sin necesidad de que el personal de ti toque el dispositivo.  El proceso se ha diseñado para ser sencillo para que cualquier persona pueda completarlo, lo que permite que los dispositivos se envíen o distribuyan directamente al usuario final con instrucciones sencillas:

- Vuelva a aplicar la conversión unboxing del dispositivo, conéctelo y enciéndalo.
- Elija un idioma (solo es necesario cuando se instalan varios idiomas), configuración regional y teclado.
- Conéctelo a una red inalámbrica o cableada con acceso a Internet.  Si usa la red inalámbrica, el usuario debe establecer el vínculo de Wi-Fi.  
- Especifique la dirección de correo electrónico y la contraseña de la cuenta de la organización.

Después de completar estos sencillos pasos, se automatiza el resto del proceso, con el dispositivo unido a la organización, inscrito en Intune (u otro servicio MDM) y configurado completamente según lo definido por la organización.  Cualquier solicitud adicional durante la ejecución rápida (OOBE) se puede suprimir. consulte [configuración de perfiles de AutoPilot](profiles.md) para ver las opciones disponibles.

El modo controlado por el usuario de Windows AutoPilot admite dispositivos Azure Active Directory e híbridos Unidos Azure Active Directory.  Para obtener más información sobre estas dos opciones de combinación, consulte [¿Qué es una identidad de dispositivo](https://docs.microsoft.com/azure/active-directory/devices/overview)?

Desde la perspectiva del flujo de proceso, las tareas realizadas durante el proceso controlado por el usuario son las siguientes:

- Una vez que se haya conectado a una red, el dispositivo descargará un perfil de Windows AutoPilot que especifique la configuración que se debe usar (por ejemplo, los mensajes que se deben suprimir durante la OOBE).
- Windows 10 comprobará si hay actualizaciones de OOBE críticas. Si hay actualizaciones disponibles, se instalarán automáticamente (si es necesario, se reiniciarán).
- Se solicitará al usuario Azure Active Directory credenciales, con una experiencia de usuario personalizada que muestre el Azure AD nombre de inquilino, el logotipo y el texto de inicio de sesión.
- El dispositivo se unirá Azure Active Directory o Active Directory, en función de la configuración del perfil de Windows AutoPilot.
- El dispositivo se inscribe en Intune (u otros servicios MDM configurados).  (Esta inscripción se produce como parte del proceso de Unión Azure Active Directory a través de la inscripción automática de MDM o antes del proceso de Unión Active Directory, según sea necesario).
- Si está configurado, se mostrará la [Página de estado de inscripción](enrollment-status.md) (ESP).
- Una vez que se hayan completado las tareas de configuración del dispositivo, el usuario iniciará sesión en Windows 10 con las credenciales proporcionadas anteriormente.  (Nota: Si el dispositivo se reinicia durante el proceso de ESP del dispositivo, el usuario tendrá que volver a escribir sus credenciales, ya que estos detalles no se conservan en los reinicios).
- Una vez que haya iniciado sesión, se mostrará de nuevo la página estado de inscripción para las tareas de configuración de destino del usuario.

Si se produce algún problema durante este proceso, consulte la documentación de [solución de problemas de Windows AutoPilot](troubleshooting.md) .

Para obtener más información sobre las opciones de combinación disponibles, vea las siguientes secciones:

- [Azure Active Directory combinación](#user-driven-mode-for-azure-active-directory-join) está disponible si no es necesario que los dispositivos estén Unidos a un dominio de Active Directory local.
- La [Unión híbrida Azure Active Directory](#user-driven-mode-for-hybrid-azure-active-directory-join) está disponible para los dispositivos que deben estar unidos a Azure Active Directory y al dominio de Active Directory local.

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Modo basado en el usuario para Azure Active Directory join

Para realizar una implementación controlada por el usuario mediante Windows AutoPilot, deben realizarse los siguientes pasos de preparación:

- Asegúrese de que los usuarios que van a realizar implementaciones en modo controlado por el usuario pueden unir dispositivos a Azure Active Directory.  Para obtener más información, consulte [Configure Device Settings](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal#configure-device-settings) en la documentación de Azure Active Directory.
- Cree un perfil de AutoPilot para el modo controlado por el usuario con la configuración deseada.  En Microsoft Intune, este modo se elige explícitamente al crear el perfil. Con Microsoft Store para la empresa y el centro de Partners, el modo controlado por el usuario es el valor predeterminado y no es necesario seleccionarlo.
- Si usa Intune, cree un grupo de dispositivos en Azure Active Directory y asigne el perfil de AutoPilot a ese grupo.

Estos pasos adicionales son necesarios para cada dispositivo que se va a implementar mediante la implementación controlada por el usuario:

- Asegúrese de que el dispositivo se ha agregado a Windows AutoPilot.  Esta adición la puede realizar automáticamente un OEM o un asociado en el momento en que se adquiere el dispositivo, o bien se puede realizar a través de un proceso de recopilación manual más adelante.  Para obtener más información, consulte [Agregar dispositivos a Windows AutoPilot](add-devices.md).
- Asegúrese de que se ha asignado un perfil de AutoPilot al dispositivo:
  - Si usa Intune y Azure Active Directory grupos de dispositivos dinámicos, esta asignación puede realizarse automáticamente.
  - Si usa Intune y Azure Active Directory grupos de dispositivos estáticos, agregue manualmente el dispositivo al grupo de dispositivos.
  - Si usa otros métodos (por ejemplo, Microsoft Store para la empresa o el centro de Partners), asigne manualmente un perfil AutoPilot al dispositivo.


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>Modo controlado por el usuario para la Unión de Azure Active Directory híbrida

Windows AutoPilot requiere que los dispositivos estén Azure Active Directory Unidos. Si tiene un entorno de Active Directory local y también quiere unir dispositivos a su dominio local, puede configurar dispositivos AutoPilot para que se [unan a Azure Active Directory (Azure ad)](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).  

### <a name="requirements"></a>Requisitos

Para realizar una implementación híbrida orientada a Azure AD basada en el usuario mediante Windows AutoPilot:

- Se debe crear un perfil de Windows AutoPilot para el modo controlado por el usuario y 
  - **Azure ad híbrido** join debe especificarse como la opción seleccionada en **unirse a Azure ad como** en el perfil de AutoPilot.
- Si usa Intune, debe existir un grupo de dispositivos en Azure Active Directory con el perfil de Windows AutoPilot asignado a ese grupo.
- El dispositivo debe ejecutar Windows 10, versión 1809 o posterior.
- El dispositivo debe tener acceso a un controlador de dominio de Active Directory, por lo que debe estar conectado a la red de la organización (donde puede resolver los registros DNS para el dominio de AD y el controlador de dominio de AD, y comunicarse con el controlador de dominio para autenticar al usuario).
- El dispositivo debe poder tener acceso a Internet, según los [requisitos de red de Windows AutoPilot documentados](windows-autopilot-requirements.md).
- Se debe instalar el conector de Intune para Active Directory.
  - Nota: el conector de Intune realizará una Unión AD local, por lo que los usuarios no necesitan el permiso AD-join local, suponiendo que el conector está [configurado para realizar esta acción](https://docs.microsoft.com/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) en nombre del usuario. 
- Si utiliza el proxy, la opción de configuración del proxy WPAD debe estar activada y configurada.

**Azure ad Unión de dispositivos**: el proceso híbrido de unión a Azure ad utiliza el contexto del sistema para realizar la unión de Azure ad de dispositivos, por lo que no se ve afectado por la configuración de permisos de combinación de Azure ad basada en el usuario. Además, todos los usuarios están habilitados para unir dispositivos a Azure AD de forma predeterminada.

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>Modo controlado por el usuario para la Unión de Azure Active Directory híbridos con compatibilidad con VPN

Los dispositivos que están Unidos a Active Directory requieren conectividad con un controlador de dominio Active Directory para una variedad de actividades, como el inicio de sesión de usuario (validar las credenciales del usuario) y directiva de grupo aplicación.  Como resultado, el proceso de Unión a Azure AD híbrido de Windows AutoPilot controlado por el usuario validaría que el dispositivo pueda ponerse en contacto con un controlador de dominio de Active Directory haciendo ping a dicho controlador de dominio.

Además de la compatibilidad con VPN para este escenario, ahora es posible especificar para omitir la comprobación de conectividad durante el Unión a Azure AD híbrido.  Esto no elimina la necesidad de comunicarse con un controlador de dominio de Active Directory, sino que permite preparar el dispositivo por primera vez con una configuración de VPN necesaria entregada a través de Intune antes de que el usuario intente iniciar sesión en Windows, lo que permite la conectividad a la red de la organización.

### <a name="requirements"></a>Requisitos

Para Unión a Azure AD híbrido con compatibilidad con VPN, se aplican los siguientes requisitos adicionales:

- Una versión compatible de Windows 10:
  - Actualización acumulativa de Windows 10 1903 + 10 de diciembre (KB4530684, compilación de SO 18362,535) o superior 
  - Actualización acumulativa de Windows 10 1909 + 10 de diciembre (KB4530684, compilación de SO 18363,535) o superior  
  - Windows 10 2004 o posterior 
- Habilite la nueva alternancia "Omitir comprobación de conectividad de dominio" en el perfil de AutoPilot de Unión a Azure AD híbrido.
- Una configuración de VPN que se puede implementar a través de Intune que permite al usuario establecer manualmente una conexión VPN desde la pantalla de inicio de sesión de Windows o una que establece automáticamente una conexión VPN según sea necesario.  

La configuración de VPN específica necesaria depende del software de VPN y de la autenticación que se use.  En el caso de las soluciones VPN de terceros (que no sean de Microsoft), esto normalmente implicaría la implementación de una aplicación de Win32 (que contenía el software cliente de VPN en sí, así como cualquier información de conexión específica, por ejemplo: nombres de host de punto de conexión de VPN) a través de las extensiones de administración de Intune.  Consulte la documentación del proveedor de VPN para obtener detalles de configuración específicos de ese proveedor.

> [!NOTE]
> Los requisitos de VPN no son específicos de Windows AutoPilot. Por ejemplo, si ya ha implementado una configuración de VPN para habilitar los restablecimientos de contraseñas remotos, en los que un usuario necesita iniciar sesión en Windows con una nueva contraseña cuando no está en la red de la organización, se puede usar la misma configuración con Windows AutoPilot.  Una vez que el usuario ha iniciado sesión para almacenar en caché sus credenciales, los intentos de inicio de sesión posteriores no necesitan conectividad, ya que se pueden usar las credenciales almacenadas en caché. 

En los casos en los que el software de VPN requiere autenticación de certificado, el certificado de equipo necesario también debe implementarse a través de Intune.  Esta implementación se puede realizar mediante las funcionalidades de inscripción de certificados de Intune, que se dirigen a los perfiles de certificado para el dispositivo.

Tenga en cuenta que no se admiten certificados de usuario porque estos certificados no se pueden implementar hasta que el usuario inicie sesión.  Además, los complementos VPN que no son de Microsoft que se entregan desde la tienda Windows tampoco se admiten, ya que estos complementos no se instalan hasta después de que el usuario inicie sesión.

### <a name="validation"></a>Validación

Antes de intentar una Unión híbrida Azure AD mediante VPN, es importante confirmar primero que se puede realizar un proceso de Unión a Azure AD híbrido controlado por el usuario en la red de la organización, antes de agregar los requisitos adicionales que se describen a continuación.  Esto simplifica la solución de problemas asegurándose de que el proceso principal funciona correctamente antes de agregar la configuración de VPN adicional necesaria.

Después, compruebe que la configuración de VPN (aplicación Win32, certificados y cualquier otro requisito) se puede implementar a través de Intune en un dispositivo existente que ya se ha unido Azure AD híbrido.  Por ejemplo, algunos clientes VPN crean una conexión VPN por equipo como parte del proceso de instalación, por lo que puede validar la configuración mediante pasos como los siguientes:

- En PowerShell, compruebe que se ha creado al menos una conexión VPN por equipo mediante el comando "Get-VpnConnection-AllUserConnection".
- Intente iniciar manualmente la conexión VPN con el comando: RASDIAL.EXE "ConnectionName"
- Cierre la sesión y compruebe que el icono de "conexión VPN" se puede ver en la página de inicio de sesión de Windows.
- Mueva el dispositivo fuera de la red corporativa e intente establecer la conexión con el icono de la página de inicio de sesión de Windows, iniciando sesión en una cuenta que no tenga credenciales almacenadas en caché.

En el caso de las configuraciones de VPN que se conectan automáticamente, los pasos de validación pueden ser diferentes.

> [!NOTE]
> Se puede usar Always On VPN para este escenario.  Consulte la documentación de [implementación de Always on VPN](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) para obtener más información.  Tenga en cuenta que Intune aún no puede implementar el perfil de VPN por equipo necesario. 

Para validar el proceso de un extremo a otro, asegúrese de que se ha instalado la actualización acumulativa de Windows 10 necesaria en Windows 10 1903 o Windows 10 1909. Esta actualización se puede realizar manualmente durante la instalación de OOBE; para ello, primero debe descargar la versión acumulativa más reciente de https://catalog.update.microsoft.com y, después, instalarla manualmente:

- Presione Mayús + F10 para abrir un símbolo del sistema.
- Inserte una clave USB que contenga la actualización descargada.
- Instale la actualización con el comando (sustituyendo el nombre de archivo real): WUSA.EXE <filename> . msu/Quiet
- Reinicie el equipo con el comando: shutdown.exe/r/t 0

Como alternativa, puede invocar Windows Update para instalar las últimas actualizaciones a través de este proceso:

- Presione Mayús + F10 para abrir un símbolo del sistema.
- Ejecute el comando "Start MS-Settings:"
- Navegue hasta el nodo "actualizar seguridad de &" y compruebe si hay actualizaciones.
- Reiniciar después de instalar las actualizaciones.

### <a name="step-by-step-instructions"></a>Instrucciones paso a paso

Consulte [implementar dispositivos híbridos Unidos a Azure ad mediante Intune y Windows AutoPilot](https://docs.microsoft.com/intune/windows-autopilot-hybrid).



