---
title: Problemas conocidos de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Infórmese sobre los problemas conocidos que pueden producirse durante la implementación de Windows AutoPilot.
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
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
ms.openlocfilehash: 4ad59d2891a94147a81450ee3c7157281b24d3df
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908013"
---
# <a name="windows-autopilot---known-issues"></a>Windows AutoPilot: problemas conocidos

**Se aplica a**

- Windows 10

<table>
<th>Incidencia<th>Más información

<tr><td>Las aplicaciones de bloqueo especificadas en un perfil de estado de inscripción dirigido al usuario se omiten durante el ESP del dispositivo.</td>
<td>Los servicios responsables de determinar la lista de aplicaciones que deben bloquearse durante el ESP del dispositivo no pueden determinar el perfil ESP correcto que contiene la lista de aplicaciones porque no conocen la identidad del usuario. Como solución alternativa, habilite el perfil ESP predeterminado (que tiene como destino a todos los usuarios y dispositivos) y coloque la lista de aplicaciones de bloqueo allí. En el futuro, será posible establecer como destino el perfil ESP en grupos de dispositivos para evitar este problema.</tr>

<tr><td>Ese nombre de usuario tiene el mismo aspecto que pertenece a otra organización. Intente iniciar sesión de nuevo o vuelva a empezar con una cuenta diferente.</td>
 <td>Confirme que toda la información sea correcta en HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Provisioning\Diagnostics\AutoPilot. Para obtener más información, consulte <a href="troubleshooting.md#windows-10-version-1709-and-above">solución de problemas de Windows AutoPilot</a>.</td></tr>

<tr><td>Las implementaciones de Azure AD híbrido de Windows AutoPilot basadas en el usuario no conceden derechos de administrador a los usuarios, ni siquiera cuando se especifican en el perfil de Windows AutoPilot.</td>
<td>Este problema se produce cuando hay otro usuario en el dispositivo que ya tiene derechos de administrador. Por ejemplo, un script o una directiva de PowerShell puede crear una cuenta local adicional que sea miembro del grupo administradores. Para asegurarse de que funciona correctamente, no cree una cuenta adicional hasta que finalice el proceso de Windows AutoPilot.</tr>

<tr><td>El aprovisionamiento de dispositivos de Windows AutoPilot puede producir errores con atestación de TPM o tiempos de espera de ESP en los dispositivos en los que el reloj en tiempo real está desactivado durante un período de tiempo considerable (por ejemplo, varios minutos o más).</td>
<td>Para corregir este problema: <ol><li>Arranque el dispositivo al principio de la experiencia rápida (OOBE).
<li>Establecer una conexión de red (cableada o inalámbrica).
<li>Ejecute el comando <b>W32tm/Resync/Force</b> para sincronizar la hora con el servidor horario predeterminado (Time.Windows.com).</ol>
</tr>

<tr><td>Windows AutoPilot para dispositivos existentes no funciona para Windows 10, versión 1903 o 1909; verá pantallas que ha deshabilitado en su perfil de Windows AutoPilot, como la pantalla del contrato de licencia de Windows 10.
<br>&nbsp;<br>
Este problema se produce porque Windows 10, versión 1903 y 1909 elimina el AutopilotConfigurationFile.jsen el archivo.
<td>Para corregir este problema: <ol><li>Edite la secuencia de tareas Configuration Manager y deshabilite el paso <b>preparar Windows para la captura</b> .
<li>Agregue un nuevo paso <b>Ejecutar línea de comandos</b> que ejecute <b>c:\windows\system32\sysprep\sysprep.exe/Oobe/reboot</b>.</ol>
<a href="https://oofhours.com/2019/09/19/a-challenge-with-windows-autopilot-for-existing-devices-and-windows-10-1903/">Más información</a></tr>
 
<tr><td>Se produce un error en la atestación de TPM en Windows 10 1903 debido a que falta la extensión AKI en el certificado EK. (Se ha agregado una validación adicional en Windows 10 1903 para comprobar que los certificados de TPM EK tenían los atributos adecuados de acuerdo con las especificaciones de TCG descubiertas que no se revelaron para que se eliminara la validación).
<td>Descargue e instale la <a href="https://support.microsoft.com/help/4517211/windows-10-update-kb4517211">actualización de KB4517211</a>.
<tr><td>Los siguientes problemas conocidos se resuelven mediante la instalación de la actualización del 30 de agosto de 2019 KB4512941 (compilación del sistema operativo 18362,329):

- La característica de Windows AutoPilot para dispositivos existentes no elimina correctamente la página "actividades" durante OOBE. (Debido a este problema, verá la página adicional durante OOBE).
- Sysprep/generalize no borra el estado de la atestación de TPM, lo que produce un error en la atestación de TPM durante el flujo de OOBE posterior. (Esto no es un problema especialmente común, pero podría encontrarlo mientras realiza pruebas si está ejecutando Sysprep/generalize y, a continuación, reinicie o vuelva a crear la imagen del dispositivo para volver a través de un escenario de inspección automática o de una guante en blanco autopiloto).
- Se puede producir un error en la atestación de TPM si el dispositivo tiene un certificado de AIK válido pero no un certificado de EK. (este problema está relacionado con el elemento anterior).
- Si se produce un error en la atestación de TPM durante el proceso de la guante en blanco de Windows AutoPilot, la página de aterrizaje parece estar bloqueada. (Básicamente, la página de aterrizaje de la guante blanca, donde se hace clic en "aprovisionamiento" para comenzar el proceso de la guante blanca, no informa correctamente de los errores).
- Se produce un error en la atestación de TPM en los TPM de Infineon más recientes (versión de firmware > 7,69). (Antes de esta corrección, solo se aceptó una lista específica de versiones de firmware).
- Las plantillas de nomenclatura de dispositivos pueden truncar el nombre del equipo con 14 caracteres en lugar de 15.
- Las directivas de acceso asignadas provocan un reinicio, que puede interferir con la configuración de los dispositivos de pantalla completa de una sola aplicación.
<td>Descargue e instale la <a href="https://support.microsoft.com/help/4512941">actualización de KB4512941</a>. <br><br>Vea la sección: <b>Cómo obtener esta actualización</b> para obtener información sobre canales de versión específicos que puede usar para obtener la actualización.
<tr><td>Los siguientes problemas conocidos se resuelven mediante la instalación de la actualización del 26 de julio de 2019 KB4505903 (compilación del sistema operativo 18362,267):

- La guante blanca de Windows AutoPilot no funciona para un sistema operativo que no sea en inglés y aparece una pantalla roja con el mensaje "correcto".
- Windows AutoPilot informa de un error AUTOPILOTUPDATE durante OOBE después de Sysprep, Reset u otras variaciones. Este problema suele ocurrir si se restablece el sistema operativo o se usa una imagen de preparada con Sysprep personalizada.
- El cifrado de BitLocker no está configurado correctamente. Por ejemplo: BitLocker no recibió una notificación esperada después de aplicar las directivas para comenzar el cifrado.
- No puede instalar aplicaciones para UWP desde el Microsoft Store, lo que provoca errores durante la fase piloto de Windows. Si va a implementar Portal de empresa como una aplicación de bloqueo durante el AutoPilot de Windows, es probable que vea este error.
- A un usuario no se le conceden derechos de administrador en el escenario de Azure AD híbrido combinación controlado por el usuario de Windows AutoPilot. Este es otro problema del sistema operativo que no está en inglés.
<td>Descargue e instale la <a href="https://support.microsoft.com/help/4505903">actualización de KB4505903</a>. <br><br>Vea la sección: <b>Cómo obtener esta actualización</b> para obtener información sobre canales de versión específicos que puede usar para obtener la actualización.
<tr><td><a href="self-deploying.md">El modo de Autoimplementación de</a> Windows AutoPilot produce un error con un código:
<td><table>
<tr><td>0x800705B4<td>Se trata de un error general que indica un tiempo de espera. Una causa común de este error en el modo de auto-implementación es que el dispositivo no es compatible con TPM 2,0 (por ejemplo: una máquina virtual). Los dispositivos que no son compatibles con TPM 2,0 no se pueden usar con el modo de implementación automática.
<tr><td>0x801c03ea<td>Este error indica que se produjo un error en la atestación de TPM, lo que provoca un error al unir Azure Active Directory con un token de dispositivo.
<tr><td>0xc1036501<td>El dispositivo no puede realizar una inscripción automática de MDM porque hay varias configuraciones de MDM en Azure AD. Vea <a href="https://oofhours.com/2019/10/01/inside-windows-autopilot-self-deploying-mode/">dentro del modo de Autoimplementación de Windows AutoPilot</a>.
</table>
<tr><td>La guante blanca proporciona una pantalla roja y el registro de eventos de <b>registro/administración de dispositivos Microsoft-Windows-usuario</b> muestra el <b>código de error HRESULT 0x801C03F3</b><td>Este problema puede producirse si Azure AD no encuentra un objeto de dispositivo de Azure AD para el dispositivo que está intentando implementar. Este problema se producirá si elimina manualmente el objeto. Para corregirlo, quite el dispositivo de Azure AD, Intune y AutoPilot y, a continuación, vuelva a registrarlo con AutoPilot, que volverá a crear el objeto de dispositivo Azure AD.<br> 
<br>Para obtener los registros de solución de problemas, use: <b> área deMdmdiagnosticstool.exe AutoPilot; TPM: c:\autopilot.cabCAB </b>
<tr><td>La guante blanca proporciona una pantalla roja<td>La guante blanca no es compatible con una máquina virtual.
<tr><td>Error al importar dispositivos Windows AutoPilot desde un archivo. csv<td>Asegúrese de que no ha editado el archivo. csv en Microsoft Excel o un editor que no sea el Bloc de notas. Algunos de estos editores pueden introducir caracteres adicionales que hacen que el formato de archivo no sea válido. 
<tr><td>Windows AutoPilot para dispositivos existentes no sigue la experiencia de OOBE de AutoPilot.<td>Asegúrese de que el archivo de perfil JSON se guarda en formato <b>ANSI/ASCII</b> , no Unicode o UTF-8.
<tr><td>Aparece <b>un error</b> en la página durante la Oobe.<td>Es probable que el cliente no pueda tener acceso a todas las direcciones URL requeridas relacionadas con Azure AD/MSA. Para obtener más información, consulte [requisitos de red](networking-requirements.md).
<tr><td>El uso de un paquete de aprovisionamiento en combinación con Windows AutoPilot puede producir problemas, especialmente si el PPKG contiene información de combinación, inscripción o nombre de dispositivo.<td>No se recomienda usar PPKGs en combinación con Windows AutoPilot.
</table>

## <a name="related-topics"></a>Temas relacionados

[Diagnóstico de errores de MDM en Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Solución de problemas de Windows AutoPilot](troubleshooting.md)