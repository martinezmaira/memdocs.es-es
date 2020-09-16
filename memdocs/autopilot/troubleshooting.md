---
title: Solución de problemas de Windows AutoPilot
description: Obtenga información acerca de cómo solucionar los problemas que surjan durante el proceso de implementación de Windows AutoPilot.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
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
ms.openlocfilehash: 38f140717d256d6edd4e9bd6cd0a66b6bc853740
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574584"
---
# <a name="troubleshooting-windows-autopilot"></a>Solución de problemas de Windows AutoPilot

**Se aplica a: Windows 10**

Windows AutoPilot está diseñado para simplificar todas las partes del ciclo de vida de los dispositivos de Windows, pero siempre hay situaciones en las que pueden surgir problemas. Revise la información siguiente para obtener ayuda con los esfuerzos de solución de problemas.

## <a name="troubleshooting-process"></a>Proceso de solución de problemas

Tanto si va a realizar implementaciones controladas por el usuario como para implementar dispositivos de forma automática, el proceso de solución de problemas es el mismo. Resulta útil comprender el flujo de un dispositivo específico:

1. Se establece una conexión de red. La conexión puede ser una conexión inalámbrica (Wi-Fi) o cableada (Ethernet).
2. Se descarga el perfil de Windows AutoPilot. Cuando se usa una conexión cableada, o se establece manualmente una conexión inalámbrica, el perfil se descarga desde el servicio de implementación de AutoPilot en cuanto se realiza la conexión de red.
3. Se produce la autenticación del usuario. Al realizar una implementación controlada por el usuario, el usuario escribirá sus credenciales de Azure Active Directory, que se validarán.
4. Se produce Azure Active Directory combinación. En el caso de las implementaciones controladas por el usuario, el dispositivo se unirá a Azure AD con las credenciales de usuario especificadas. En el caso de los escenarios de auto-implementación, el dispositivo se unirá sin especificar ninguna credencial de usuario.
5. Se produce la inscripción automática de MDM. Como parte del proceso de unión de Azure AD, el dispositivo se inscribe en el servicio MDM configurado en Azure AD (por ejemplo, Microsoft Intune).
6. Se aplica la configuración. Si está configurada la [Página estado de inscripción](enrollment-status.md) , la mayoría de las opciones se aplicarán mientras se muestra la página estado de inscripción. Si no está configurado o disponible, se aplicará la configuración después de que el usuario haya iniciado sesión.

Para solucionar problemas, las actividades clave que se deben realizar son las siguientes:

- Configuración: ¿Azure Active Directory y Microsoft Intune (o un servicio MDM equivalente) se han configurado según se especifica en [los requisitos de configuración de Windows AutoPilot](configuration-requirements.md)?
- Conectividad de red: ¿el dispositivo puede acceder a los servicios descritos en [requisitos de red de Windows AutoPilot](networking-requirements.md)?
- Comportamiento de la experiencia rápida (OOBE) del piloto automático: ¿se muestran las pantallas [Oobe esperadas](#troubleshooting-autopilot-oobe-issues) ? ¿Se ha personalizado la página de credenciales de Azure AD con detalles específicos de la organización?
- Problemas de Azure AD join: ¿el dispositivo puede [unirse Azure Active Directory](#troubleshooting-azure-ad-join-issues)?
- Problemas de inscripción de MDM: ¿el dispositivo puede [inscribirse en Microsoft Intune](#troubleshooting-intune-enrollment-issues) (o un servicio de MDM equivalente)?

## <a name="troubleshooting-autopilot-device-import"></a>Solución de problemas de importación de dispositivos AutoPilot

### <a name="clicking-import-after-selecting-csv-does-nothing-400-error-appears-in-network-trace-with-error-body-cannot-convert-the-literal-devicehash-to-the-expected-type-edmbinary"></a>Al hacer clic en importar después de seleccionar CSV no hace nada, aparece el error "400" en el seguimiento de red con el cuerpo del error **"no se puede convertir el literal" [DEVICEHASH] "al tipo esperado" EDM. binary ""**

Este error apunta al hash del dispositivo con un formato incorrecto. Cualquier cosa que dañe el hash recopilado puede producir este error. Una posibilidad es que el propio hash (incluso si es válido) no se pueda descodificar.

El hash del dispositivo es Base64. En el nivel de dispositivo, se codifican como Base64 sin rellenar, pero el piloto automático espera que los códigos base de Base64 estén rellenados. Normalmente, la carga no requiere relleno y el proceso funciona. Sin embargo, a veces, la carga no se alinea correctamente y es necesario el relleno. En este caso, obtendrá el error mostrado anteriormente. El descodificador de Base64 de PowerShell también espera que se rellene el código Base64, por lo que podemos usar este descodificador para validar que el hash está correctamente rellenado.

Los caracteres "A" al final del hash son datos realmente vacíos. Cada carácter de Base64 es de 6 bits, un en Base64 es de 6 bits igual a 0. La eliminación o adición de s al final no cambia los **datos de carga**reales.

Para corregir este problema, es necesario modificar el hash y, a continuación, probar el nuevo valor hasta que PowerShell sea correcto al descodificar el hash. El resultado es principalmente ilegible, que es correcto. Solo estamos buscando para no producir el error "longitud no válida para una matriz de caracteres de base 64 o cadena". 

Para probar Base64, puede usar el siguiente PowerShell:
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("DEVICE HASH"))
```

Por lo tanto, como ejemplo (esto no es un hash de dispositivo, pero no está alineado con base64 sin rellenar, por lo que es adecuado para pruebas):
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("Q29udG9zbwAAA"))
```

Ahora para las reglas de relleno. El carácter de relleno es "=". El carácter de relleno solo puede estar al final del hash y solo puede haber un máximo de dos caracteres de relleno. Esta es la lógica básica.

- ¿Se produce un error al descodificar el hash?
 - Sí: ¿son los dos últimos caracteres "="?
   - Sí: reemplace "=" por un solo carácter "A" e inténtelo de nuevo.
   - No: agregue otro carácter "=" al final e inténtelo de nuevo.
 - No: ese hash es válido

Al recorrer la lógica anterior en el hash de ejemplo anterior, se obtienen las siguientes permutaciones:
- Q29udG9zbwAAA
- Q29udG9zbwAAA =
- Q29udG9zbwAAA = =
- Q29udG9zbwAAAA
- Q29udG9zbwAAAA =
- **Q29udG9zbwAAAA = =** (este tiene un relleno válido)

Reemplace el hash recopilado por este nuevo hash rellenado e intente realizar de nuevo la importación.

## <a name="troubleshooting-autopilot-oobe-issues"></a>Solución de problemas de OOBE de AutoPilot

Cuando OOBE incluye un comportamiento inesperado de AutoPilot, resulta útil comprobar si el dispositivo ha recibido un perfil de AutoPilot. Si es así, Compruebe la configuración que contiene el perfil. Dependiendo de la versión de Windows 10, hay diferentes mecanismos disponibles para hacerlo.

### <a name="windows-10-version-1803-and-above"></a>Windows 10 versión 1803 y versiones posteriores

La versión 1803 y posteriores de Windows 10 agrega entradas del registro de eventos. Puede usar las entradas de OG para ver los detalles relacionados con la configuración del perfil de AutoPilot y el flujo de OOBE. Estas entradas se pueden ver mediante Visor de eventos. Revise la información en **registros de aplicaciones y servicios: > Microsoft – > Windows – > provisioning-Diagnostics-Provider – > AutoPilot** para las versiones anteriores a 1903. Para la versión 1903 y versiones posteriores, consulte **registros de aplicaciones y servicios: > Microsoft – > Windows – > ModernDeployment-Diagnostics-Provider – > AutoPilot**. Se pueden registrar los siguientes eventos, en función del escenario y de la configuración del perfil:

| Id. de evento | Tipo | Descripción |
|----------|------|-------------| 
| 100 | Advertencia | "No se encontró la Directiva de AutoPilot [nombre]." Este error suele ser un problema temporal, mientras que el dispositivo está esperando a que se descargue un perfil de AutoPilot. |
| 101 | Información | "AutopilotGetPolicyDwordByName Succeeded: nombre de la Directiva = [nombre de la configuración]; valor de Directiva = [valor]. " Este mensaje muestra la recuperación y el procesamiento automático de la configuración de OOBE. |
| 103 | Información | "AutopilotGetPolicyStringByName Succeeded: nombre de la Directiva = [nombre]; valor = [valor]. " Este mensaje muestra la recuperación y el procesamiento automático de cadenas de configuración de OOBE como el nombre del inquilino de Azure AD. |
| 109 | Información | "AutopilotGetOobeSettingsOverride Succeeded: configuración de OOBE [nombre de configuración]; Estado = [Estado]. " Este mensaje muestra la recuperación y el procesamiento automáticos de la configuración de OOBE relacionada con el estado. |
| 111 | Información | "AutopilotRetrieveSettings Succeeded". Este mensaje significa que la configuración almacenada en el perfil AutoPilot que controla el comportamiento de OOBE se ha recuperado correctamente. |
| 153 | Información | "AutopilotManager comunicó el Estado cambió de [estado original] a [nuevo estado]." Normalmente, este mensaje debería decir "ProfileState_Unknown" a "ProfileState_Available". Este caso indica que un perfil estaba disponible y se ha descargado para el dispositivo. Por lo tanto, el dispositivo está listo para realizar la implementación mediante AutoPilot. |
| 160 | Información | "AutopilotRetrieveSettings a partir de la adquisición". Este mensaje muestra que AutoPilot está listo para descargar la configuración de Perfil de AutoPilot necesaria. |
| 161 | Información | "AutopilotManager recuperar la configuración correctamente." El perfil AutoPilot se descargó correctamente. |
| 163 | Información | "No se requiere la descarga definida por AutopilotManager y el dispositivo ya está aprovisionado. Limpie o restablezca el dispositivo para cambiar esto ". Este mensaje indica que un perfil de AutoPilot está residente en el dispositivo; normalmente solo lo quitaría el proceso **Sysprep/generalize** . |
| 164 | Información | "AutopilotManager determinó que Internet está disponible para intentar la descarga de la Directiva". |
| 171 | Error | "AutopilotManager no pudo establecer la identidad de TPM confirmada. HRESULT = [código de error]. " Este mensaje indica un problema al realizar la atestación de TPM, necesario para completar el proceso del modo de implementación automática. | 
| 172 | Error | "AutopilotManager no pudo establecer el perfil de AutoPilot como disponible. HRESULT = [código de error]. " Este error suele estar relacionado con el ID. de evento 171. |

Además de las entradas del registro de eventos, el registro y las opciones de seguimiento de ETW funcionan con la versión 1803 y posteriores de Windows 10.

### <a name="windows-10-version-1709-and-above"></a>Windows 10 versión 1709 y versiones posteriores

La configuración del perfil de AutoPilot recibida del servicio de implementación de AutoPilot se almacena en el registro del dispositivo. Esta información puede encontrarse en **HKLM\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot**. Entre las entradas del registro disponibles se incluyen:

| Valor | Descripción |
|-------|-------------|
| AadTenantId | GUID del inquilino de Azure AD en el que el usuario inició sesión. El usuario recibe un error si esta entrada no coincide con el inquilino que se usó para registrar el dispositivo. |
| CloudAssignedTenantDomain | El Azure AD inquilino con el que se ha registrado el dispositivo, por ejemplo, "contosomn.onmicrosoft.com". Si el dispositivo no está registrado con AutoPilot, este valor estará en blanco. |
| CloudAssignedTenantId | GUID del inquilino de Azure AD con el que se registró el dispositivo. El GUID corresponde al dominio del inquilino del valor del registro CloudAssignedTenantDomain. Si el dispositivo no está registrado con AutoPilot, este valor estará en blanco.|
| IsAutopilotDisabled | Si se establece en 1, este valor del registro indica que el dispositivo no está registrado con AutoPilot. Este estado también puede indicar que no se pudo descargar el perfil AutoPilot debido a problemas de conectividad de red o de firewall, o a tiempos de espera de red. |
| TenantMatched | Esta entrada se establece en 1 si el identificador de inquilino del usuario coincide con el identificador de inquilino con el que se registró el dispositivo. Si el valor del registro es 0, se mostrará un error al usuario y se forzará a que se inicie de nuevo. |
| CloudAssignedOobeConfig | Un mapa de bits que muestra qué configuración de AutoPilot se configuró. Los valores incluyen: SkipCortanaOptIn = 1, OobeUserNotLocalAdmin = 2, SkipExpressSettings = 4, SkipOemRegistration = 8, SkipEula = 16 |

### <a name="windows-10-semi-annual-channel-supported-versions"></a>Versiones compatibles con el canal semianual de Windows 10

En los dispositivos que ejecutan una [versión compatible](/windows/release-information/) del canal semianual de Windows 10, puede usar el seguimiento de ETW para obtener información detallada de los componentes relacionados con el autopiloto y los relacionados. Los archivos de seguimiento de ETW se pueden ver mediante el analizador de rendimiento de Windows o herramientas similares. Para obtener más información, consulte [el blog de solución de problemas avanzada](/archive/blogs/mniehaus/troubleshooting-windows-autopilot-level-300400).

## <a name="troubleshooting-azure-ad-join-issues"></a>Solución de problemas de Azure AD join

El problema más común al unir un dispositivo a Azure AD está relacionado con Azure AD permisos. Asegúrese de que [la configuración correcta esté en vigor](configuration-requirements.md) para que los usuarios puedan unir dispositivos a Azure ad. También se pueden producir errores si el usuario supera el número de dispositivos que pueden unirse. Este límite se configura en Azure AD.

Después de la importación, se crea un dispositivo Azure AD. Es importante que este objeto no se elimine. El objeto actúa como delimitador de AutoPilot en Azure AD para la pertenencia a grupos y los destinos (incluido el perfil). La eliminación puede provocar errores de combinación. Si se elimina este objeto, puede corregir el problema eliminando y reimportando este hash de AutoPilot para que pueda volver a crear el objeto asociado.

El código de error 801C0003 normalmente se inscribirá en una página de error titulada "algo salió mal". Este error significa que se produjo un error en la combinación de Azure AD.

## <a name="troubleshooting-intune-enrollment-issues"></a>Solución de problemas de inscripción de Intune

Consulte [este artículo de Knowledge Base](https://support.microsoft.com/help/4089533/troubleshooting-windows-device-enrollment-problems-in-microsoft-intune) para obtener ayuda con los problemas de inscripción de Intune. Entre los problemas comunes se incluyen "
- licencias incorrectas o que faltan asignadas al usuario.
- demasiados dispositivos inscritos para el usuario.

El código de error 80180018 normalmente se inscribirá en una página de error titulada "algo salió mal". Este error significa que se produjo un error en la inscripción de MDM.

Si se produce un error al restablecer el piloto automático inmediatamente con el error **. Inicie sesión con una cuenta de administrador para ver por qué y restablecer manualmente**. para obtener más ayuda, consulte [solución de problemas de restablecimiento de AutoPilot](/education/windows/autopilot-reset#troubleshoot-autopilot-reset) .

## <a name="profile-download"></a>Descarga de perfiles

Cuando se inicia un dispositivo de Windows 10 conectado a Internet, intentará conectarse al servicio AutoPilot y descargar un perfil de AutoPilot. Nota: es importante que exista un perfil en esta fase para que un perfil en blanco no se almacene en caché localmente en el equipo. Para quitar el perfil local actualmente almacenado en caché en la versión 1803 y anteriores de Windows 10, es necesario volver a generalizar el sistema operativo con **Sysprep/generalize/Oobe**, volver a instalar el sistema operativo o volver a crear la imagen del equipo. En Windows 10 versión 1809 y versiones posteriores, puede recuperar un nuevo perfil reiniciando el equipo.

Cuando se descarga un perfil, depende de la versión de Windows 10 que se esté ejecutando en el equipo. Vea la siguiente tabla.

| Versión de Windows 10 | Comportamiento de descarga de perfiles |
| --- | --- |
| 1709 | El perfil se descarga después de la página de conexión de red de OOBE. Esta página no se muestra cuando se usa una conexión con cable. En este caso, el perfil se descarga antes de la pantalla de CLUF. |
| 1803 | El perfil se descarga lo antes posible. Si está conectado, se descarga al principio de OOBE. Si es inalámbrica, se descarga después de la página de conexión de red. |
| 1809 | El perfil se descarga lo antes posible (igual que 1803) y de nuevo después de cada reinicio. |

Si necesita reiniciar un equipo durante OOBE:
- Presione Mayús + F10 para abrir un símbolo del sistema.
- Escriba **shutdown/r/t 0** para reiniciarlo inmediatamente o **cierre/s/t 0** para cerrarlo inmediatamente.

Para más información, consulte [Opciones de la línea de comandos del programa de instalación de Windows](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

## <a name="related-topics"></a>Temas relacionados

[Windows AutoPilot: problemas conocidos](known-issues.md)<br>
[Diagnóstico de errores de MDM en Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>