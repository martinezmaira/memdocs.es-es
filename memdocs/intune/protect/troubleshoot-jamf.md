---
title: Solución de problemas de integración de Jamf Pro con Microsoft Intune
titleSuffix: Microsoft Intune
description: Sugerencias para solucionar algunos de los problemas más habituales a la hora de integrar dispositivos de Jamf Pro para Mac con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 335841a8642429e36c277673fd8a238d486366c9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350621"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>Solución de problemas de integración de Jamf Pro con Microsoft Intune

Este artículo ayuda a los administradores de Intune a comprender y solucionar problemas relacionados con la integración de dispositivos de Jamf Pro para macOS con Intune.

> [!TIP]  
> Gran parte de la información de este artículo aparecía originalmente en el artículo sobre [solución de problemas al integrar Jamf con Microsoft Intune](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) en support.microsoft.com.

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar a solucionar problemas, recopile información básica para aclarar el problema y reducir el tiempo para encontrar una solución. Por ejemplo, si encuentra un problema relacionado con la integración de Jamf-Intune, compruebe siempre que se cumplen todos los requisitos previos. Revise las consideraciones siguientes antes de empezar a solucionar problemas:

- Revise los requisitos previos de [integración de Jamf Pro con Intune](conditional-access-integrate-jamf.md#prerequisites).
- Todos los usuarios deben tener Microsoft Intune y licencias Premium P1 de Microsoft AAD 
- Debe disponer de una cuenta de usuario que tenga permisos de integración de Microsoft Intune en la consola de Jamf Pro.
- Debe disponerse de una cuenta de usuario que tenga permisos de administrador global en Azure.


Tenga en cuenta la siguiente información al investigar la integración de Jamf Pro con Intune: 
- ¿Cuál es el mensaje de error exacto?
- ¿Dónde está el mensaje de error?
- ¿Cuándo empezó el problema?  ¿Ha funcionado la integración de Jamf Pro con Intune?
- ¿Cuántos usuarios están afectados? ¿Todos los usuarios están afectados o solo algunos?
- ¿Cuántos dispositivos se ven afectados? ¿Todos los dispositivos se ven afectados o solo algunos?
 

## <a name="common-problems"></a>Problemas comunes 

La siguiente información puede ayudarle a identificar y resolver problemas comunes de los dispositivos después de configurar la integración de Intune y Jamf Pro.  

| Problema   | Más información                  |
|-----------------|--------------------------|
| **Los dispositivos se marcan como sin respuesta en Jamf Pro**  | [Los dispositivos no se pueden sincronizar con Jamf Pro ni con Azure AD](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Los dispositivos Mac solicitan el inicio de sesión de la cadena de claves al abrir dispositivos de aplicación que no se pueden registrar**  | [Se pide la contraseña a los usuarios para permitir que las aplicaciones se registren en Azure AD](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app). |
| **Los dispositivos no se pueden registrar**  | Pueden aplicarse las siguientes causas: <br> **-** [***Causa 1***: la aplicación Jamf Pro de Azure tiene permisos incorrectos](#cause-1) <br> **-** [***Causa 2***: hay un problema con el *Jamf Native macOS Connector* in Azure AD](#cause-2) <br> **-** [***Causa 3***: el usuario no tiene una licencia válida de Intune o Jamf](#cause-3) <br> **-** [***Causa 4***: el usuario no usó Jamf Self Service para iniciar la aplicación Portal de empresa](#cause-4) <br> **-** [***Causa 5***: la integración de Intune está desactivada](#cause-5) <br> **-** [***Causa 6***: el dispositivo se inscribió anteriormente en Intune o el usuario ha intentado registrar el dispositivo varias veces](#cause-6) <br> **-** [***Cause 7***: JamfAAD solicita acceso a una "clave de Workplace Join de Microsoft" de la cadena de claves de los usuarios](#cause-7) |
|  **El dispositivo Mac se muestra compatible con Intune pero no compatible en Azure** | [Problemas de registro de dispositivos](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **Aparecen entradas duplicadas en la consola de Intune para dispositivos Mac inscritos mediante Jamf** | [Varios registros del mismo dispositivo](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **La directiva de cumplimiento no puede evaluar el dispositivo** | [La directiva se dirige a grupos de dispositivos](#compliance-policy-fails-to-evaluate-the-device) |
| **No se pudo recuperar el token de acceso para Microsoft Graph API** | Pueden aplicarse las siguientes causas: <br> -[Permisos para la aplicación Jamf Pro en Azure](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Licencia expirada para Jamf o Intune](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [Los puertos no están abiertos](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>Los dispositivos se marcan como sin respuesta en Jamf Pro  

**Causa**: A continuación se indican las causas comunes que los dispositivos se marquen como *Sin respuesta*: en Jamf Pro:

- El dispositivo no se sincroniza con Jamf Pro.  
  Jamf Pro espera que los dispositivos se sincronicen cada 15 minutos. Los dispositivos se marcan como sin respuesta en Jamf cuando no se sincronizan durante 24 horas.  

- El dispositivo no se sincroniza con Azure AD.  
  Con el registro correcto en Azure AD, los dispositivos macOS reciben un token de Azure:
  - Este token se actualiza cada 12 horas.   
  - Cuando la actualización del token no se realiza durante 24 horas o más, Jamf Pro marca el dispositivo como sin respuesta.  
  - Si el token de Azure expira, se solicitará a los usuarios que inicien sesión en Azure para obtener un nuevo token. Un token de actualización para el acceso a Azure se genera cada siete días.

**Solución**  
Una vez que un dispositivo se marca como *Sin respuesta* en Jamf Pro, el usuario inscrito del dispositivo debe iniciar sesión para corregir el estado de falta de respuesta. Debe ser el usuario que ha unido el trabajo a la cuenta, ya que tiene la identidad de Intune en su cadena de inicio de sesión.



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Los dispositivos Mac solicitan el inicio de sesión de la cadena de claves al abrir una aplicación  

Después de configurar la integración de Intune y Jamf Pro e implementar directivas de acceso condicional, los usuarios de dispositivos administrados con Jamf Pro reciben solicitudes de contraseña al abrir aplicaciones de Microsoft Office 365, como Teams, Outlook y otras aplicaciones que requieren la autenticación Azure AD. 

Por ejemplo, cuando se abre Microsoft Teams, aparece un símbolo del sistema con texto similar al siguiente:

``` 
  Microsoft Teams wants to sign using key “Microsoft Workplace Join Key” in your keychain.  
  To allow this, enter the “login” keychain password 
```

**Causa**: Jamf Pro genera estos mensajes para cada aplicación que requiera el registro de Azure AD. 

**Solución**   
En el símbolo del sistema, el usuario debe proporcionar la contraseña del dispositivo para iniciar sesión en Azure AD. Las opciones son:
- **Denegar**: no se inicia sesión ni se usa la aplicación.
- **Permitir**: un inicio de sesión único. La próxima vez que se abra la aplicación, se le pedirá que vuelva a iniciar sesión.
- **Permitir siempre**: las credenciales de inicio de sesión se almacenan en la memoria caché de la aplicación. La próxima vez que se abra la aplicación, no se le pedirá que inicie sesión.  

Al seleccionar *Permitir siempre* para una aplicación, solo se aprueba esa aplicación para el inicio de sesión futuro. Las aplicaciones adicionales solicitan autenticación hasta que también se establecen en *Permitir siempre*. Otra aplicación no puede usar las credenciales almacenadas en caché para una aplicación.  

### <a name="devices-fail-to-register"></a>Los dispositivos no se pueden registrar  

Hay varias causas comunes para que no se puedan registrar dispositivos Mac.  

#### <a name="cause-1"></a>Causa 1  

**La aplicación empresarial de Jamf Pro en Azure tiene el permiso incorrecto o tiene más de un permiso**  

  Al crear la aplicación en Azure, debe quitar todos los permisos de API predeterminados y asignar a Intune un único permiso de *update_device_attributes*. 

  **Solución**  
  Repase y, si es necesario, corrija los permisos para la aplicación Jamf que creó en Azure AD. Consulte el procedimiento para [crear una aplicación para Jamf en Azure AD](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory). 

#### <a name="cause-2"></a>Causa 2  

**La aplicación de **conector de macOS nativo de Jamf** no se creó en su inquilino de Azure AD o el consentimiento del conector fue firmado por una cuenta que no tiene derechos de administrador global**  

  **Solución**  
  Consulte la sección sobre *configuración de la integración de Intune con macOS* del artículo sobre [integración con Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) en docs.jamf.com. 

#### <a name="cause-3"></a>Causa 3

**El usuario no tiene una licencia válida de Intune o Jamf**  

  La falta de una licencia válida puede generar el siguiente error, que indica que la licencia de Jamf ha expirado:  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **Solución**
  - Licencia de Jamf: Póngase en contacto con Jamf para obtener ayuda para obtener una nueva licencia para Jamf.  
  - Licencia de Intune: Asigne una licencia válida al usuario o póngase en contacto con Microsoft o con su partner para obtener información sobre cómo obtener una licencia actual.

#### <a name="cause-4"></a>Causa 4  

**El usuario no usó *Jamf Self Service* para iniciar la aplicación Portal de empresa**

Para que un dispositivo se inscriba correctamente y se registre con Intune a través de Jamf, el usuario debe usar Jamf Self Service para abrir el Portal de empresa de Intune. Si el usuario abre el portal de empresa manualmente, el dispositivo se inscribe y registra sin su conexión a Jamf.  

Para determinar qué servicio usó el dispositivo para inscribirse y registrarse, mire en la aplicación Portal de empresa en el dispositivo. Al registrarse a través de Jamf, debe recibir una notificación para abrir la aplicación de autoservicio para realizar cambios.

En la aplicación Portal de empresa, el usuario podría ver **`Not registered`** y podría aparecer una entrada similar a la del ejemplo siguiente en los registros de Portal de empresa:  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**Solución**  
Para cambiar el origen de registro de Intune a Jamf:
1. [Anule la inscripción del dispositivo macOS de Intune](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-macos). Para evitar otras complicaciones en los dispositivos que no se han quitado completamente de Intune, consulte la [*causa 6*](#cause-6) de esta lista de causas.  

2. En el dispositivo, use Jamf Self Service para abrir la aplicación Portal de empresa y después inscribir el dispositivo con Intune. Esta tarea requiere que se haya [usado Jamf para implementar la aplicación Portal de empresa para macOS](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) y se haya [creado una directiva en Jamf Pro que registre el dispositivo de los usuarios con Azure AD](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory).  

3. La primera pantalla que verá en la aplicación Portal de empresa le pedirá que inicie sesión. Uso de una cuenta profesional o educativa  

4. La aplicación Portal de empresa confirma la información de la cuenta y muestra los estados de Inscripción de dispositivos y Cumplimiento de dispositivos. Con triángulos de color amarillo se resaltan las acciones que debe emprender para proteger su dispositivo macOS para la escuela o el trabajo. Haga clic en Comenzar para iniciar la inscripción.  

5. Si se le pide, escriba la información de inicio de sesión del equipo.  
     
Puede que tarde unos minutos en inscribir el dispositivo en la administración. Durante este tiempo, puede realizar otras acciones en el dispositivo. Una vez haya completado la configuración de acceso de la empresa, recibirá un mensaje para informarle de que ya ha terminado.

#### <a name="cause-5"></a>Causa 5  

**La integración de Intune está desactivada**

Si la integración de Intune está desactivada, los usuarios reciben una ventana emergente en el Portal de empresa con el siguiente mensaje al intentar registrar un dispositivo:  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

Cuando la integración está desactivada, el servidor Jamf Pro envía un pulso a los servidores de Intune que indica a Intune que la integración está deshabilitada. 

**Solución**  
Vuelva a habilitar la integración de Intune dentro de Jamf Pro. Vea [Configurar la integración de Microsoft Intune en Jamf Pro](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro).


#### <a name="cause-6"></a><a name="cause-6"></a>Causa 6  

**El dispositivo se inscribió anteriormente en Intune o el usuario ha intentado registrar el dispositivo varias veces**

Si se anula la inscripción de un dispositivo de Jamf pero no se quita correctamente de Intune o se realizan varios intentos de registro, es posible que vea varias instancias del mismo dispositivo en el portal. Esto hace que la inscripción de Jamf no se realice.

**Solución**  
1. En el equipo Mac, inicie **Terminal**.
2. Ejecute **sudo JAMF removemdmprofile**.
3. Ejecute **sudo JAMF removeFramework**.
4. En el servidor de JAMF Pro, elimine el registro de inventario del equipo.
5. Elimine el dispositivo de Azure AD.
6. Si existen, elimine los siguientes archivos del dispositivo:
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Clave de transporte de sesión de Microsoft (claves públicas y privadas)
   - Clave de Microsoft Workplace Join (claves públicas y privadas)
7. Quite los elementos de la cadena de claves del dispositivo que hagan referencia a *Microsoft*, *Intune* o *Portal de empresa*, incluidos los certificados de DeviceLogin.microsoft.com. Quite las referencias de *JAMF*, excepto la clave pública y privada de JAMF. 
   > [!IMPORTANT]  
   > Al quitar la clave pública y privada se interrumpirá la inscripción del dispositivo.

8. Elimine cualquiera de las siguientes entradas que encuentre:  
   - Tipo: Contraseña de aplicación; Cuenta: com.microsoft.workplacejoin.thumbprint
   - Tipo: Contraseña de aplicación; Cuenta: com.microsoft.workplacejoin.registeredUserPrincipalName
   - Tipo: Certificado; Emitido por: MS-Organization-Access
   - Tipo: Preferencia de identidad; Nombre (dirección URL de STS de ADFS si está presente): https://adfs\<DNSName>.com/adfs/ls
   - Tipo: Preferencia de identidad; Nombre https://enterpriseregistration.windows.net
   - Tipo: Preferencia de identidad; Nombre https://enterpriseregistration.windows.net/  
9. Reinicie el equipo Mac.
10. Desinstale Portal de empresa del dispositivo.
11. Vaya a portal.manage.microsoft.com y elimine todas las instancias del dispositivo Mac. Espere al menos 30 minutos antes de ir al paso siguiente.
12. Vuelva a inscribir el dispositivo en JAMF Pro.
13. Vuelva a abrir Self Service e inicie la Directiva de registro.


#### <a name="cause-7"></a>Causa 7  

**JamfAAD solicita acceso a una "clave de Microsoft Workplace Join" desde la cadena de claves de los usuarios**

Durante el registro, el usuario de un dispositivo macOS recibe el siguiente mensaje para permitir el acceso de JamfAAD a una clave desde su cadena de claves: 

```
   JamfAAD wants to access key “Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the “login” keychain password
```

**Solución**  
Para registrar correctamente el dispositivo con Azure AD, Jamf requiere que el usuario proporcione su contraseña de cuenta y seleccione **Permitir**.

Esta solicitud es similar a la de [los dispositivos Mac que piden el inicio de sesión de cadena de claves al abrir una aplicación](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app), anteriormente en este artículo.  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>El dispositivo Mac se muestra compatible con Intune pero no compatible en Azure  

**Causa**: Las siguientes condiciones pueden hacer que un dispositivo se muestre como compatible en Intune, pero no en Azure:  
- El dispositivo no está registrado correctamente.  
- El dispositivo se registró varias veces sin la limpieza necesaria.

**Solución**  
Para resolver este problema, siga la solución de la [*causa 6*](#cause-6) para *Los dispositivos no se pueden registrar*, anteriormente en este artículo. 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>Aparecen entradas duplicadas en la consola de Intune para dispositivos Mac inscritos mediante Jamf  
 
**Causa**: Un dispositivo se registra varias veces en Intune, que normalmente se vuelve a registrar después de quitarse de Intune.  

Cuando se quita un dispositivo de la integración de Intune y Jamf Pro, pueden quedar algunos datos que pueden hacer que los registros sucesivos creen entradas duplicadas.  

**Solución**  
Para resolver este problema, siga la solución de la [*causa 6*](#cause-6) para *Los dispositivos no se pueden registrar*, anteriormente en este artículo. 

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>La directiva de cumplimiento no puede evaluar el dispositivo  

**Causa**: La integración de Jamf con Intune no es compatible con las directivas de cumplimiento que tienen como destino grupos de dispositivos. 

**Solución**  
Modifique la directiva de cumplimiento para que los dispositivos macOS se asignen a grupos de usuarios. 


### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>No se pudo recuperar el token de acceso para Microsoft Graph API

Recibe el siguiente error:

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

El origen de este error puede ser una de las causas siguientes: 

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Hay un problema de permisos con la aplicación Jamf Pro en Azure

Al registrar la aplicación Jamf Pro en Azure, se produjo una de las siguientes condiciones:  
- La aplicación recibió más de un permiso.
- No se seleccionó la opción **Conceder consentimiento de administrador para *\<la compañía>*** .  

**Solución**  
Consulte la solución de la causa 1 para [Los dispositivos no se pueden registrar](#devices-fail-to-register), anteriormente en este artículo.

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Ha expirado una licencia necesaria para la integración de Jamf-Intune

**Solución**: Consulte la solución para la causa 3 de [Los dispositivos no se pueden registrar](#devices-fail-to-register). 

#### <a name="the-required-ports-arent-open-on-your-network"></a>Los puertos necesarios no están abiertos en la red

**Solución**: Consulte la información sobre puertos de red en [Requisitos previos](conditional-access-integrate-jamf.md#prerequisites) para la integración de Jamf Pro con Intune.


## <a name="next-steps"></a>Pasos siguientes
Más información sobre la [integración de Jamf Pro con Intune](conditional-access-integrate-jamf.md)