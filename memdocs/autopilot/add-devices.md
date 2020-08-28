---
title: Agregar dispositivos
ms.reviewer: ''
manager: laurawi
description: Cómo agregar dispositivos a Windows AutoPilot
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
ms.openlocfilehash: c0e4e0b2d440856f24199d89485ac521208964e8
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993239"
---
# <a name="adding-devices-to-windows-autopilot"></a>Agregar dispositivos a Windows AutoPilot

**Se aplica a**

- Windows 10

Antes de implementar un dispositivo con Windows AutoPilot, el dispositivo debe estar registrado con el servicio de implementación de Windows AutoPilot. Idealmente, esto lo llevaría a cabo el OEM, el revendedor o el distribuidor desde el que se compraron los dispositivos, pero esto también lo puede hacer la organización mediante la recopilación de la identidad de hardware y su carga manual.

## <a name="oem-registration"></a>Registro de OEM

Al adquirir dispositivos directamente desde un OEM, ese OEM puede registrar automáticamente los dispositivos con el servicio de implementación de Windows AutoPilot.  Para obtener la lista de OEM que actualmente admiten esto, consulte la sección sobre fabricantes y distribuidores de dispositivos participantes en la [Página de información de Windows AutoPilot](https://aka.ms/windowsautopilot).

Para que un OEM pueda registrar dispositivos en nombre de una organización, la organización debe conceder el permiso de OEM para hacerlo.  Este proceso lo inicia el OEM, con la aprobación concedida por un administrador global de Azure AD de la organización.  Consulte la sección "consentimiento del cliente" de la [Página de consentimiento del cliente](registration-auth.md#oem-authorization).

> [!Note]
> Aunque los hashes de hardware se generan como parte del proceso de fabricación de dispositivos OEM, no se deben proporcionar directamente a clientes o asociados de CSP.  En su lugar, el OEM debe registrar los dispositivos en nombre del cliente.  En los casos en los que los asociados de CSP están registrando dispositivos, los OEM pueden proporcionar información de PKID a esos asociados para que admitan el proceso de registro de dispositivos.

## <a name="reseller-distributor-or-partner-registration"></a>Reseller, distribuidor o registro de asociados

Los clientes pueden adquirir dispositivos de revendedores, distribuidores u otros asociados.  Siempre que estos revendedores, distribuidores y asociados formen parte del programa de [asociados de soluciones en la nube (CSP)](https://partner.microsoft.com/cloud-solution-provider), también pueden registrar dispositivos en nombre del cliente.  

Al igual que con los OEM, a los asociados de CSP se les debe conceder permiso para registrar dispositivos en nombre de una organización.  Esto sigue el proceso descrito en la [Página de consentimiento del cliente](registration-auth.md#csp-authorization).  El asociado de CSP inicia una solicitud para establecer una relación con la organización, con la aprobación concedida por un administrador global de la organización.  Una vez aprobado, los asociados de CSP agregan dispositivos mediante el [centro de Partners](https://partner.microsoft.com/pcv/dashboard/overview), ya sea directamente a través del sitio web o a través de las API disponibles que pueden automatizar las mismas tareas.

Windows AutoPilot no requiere permisos de administrador delegado al establecer la relación entre el asociado de CSP y la organización.  Como parte del proceso de aprobación que realiza el administrador global, el administrador global puede optar por desactivar la casilla "incluir permisos de administración delegada".

> [!Note]
> Aunque los revendedores, distribuidores o asociados podrían arrancar cada nuevo dispositivo de Windows para obtener el hash de hardware (con el fin de proporcionarles a los clientes o el registro directo del asociado), no se recomienda hacerlo.  En su lugar, estos asociados deben registrar los dispositivos con la información de PKID obtenida del empaquetado de dispositivos (código de barras) u obtenerse electrónicamente del OEM o del asociado ascendente (por ejemplo, el distribuidor).

## <a name="automatic-registration-of-existing-devices"></a>Registro automático de dispositivos existentes

Si un dispositivo existente ya está ejecutando una versión compatible del canal semianual de Windows 10 y está inscrito en un servicio MDM como Intune, el servicio MDM puede solicitar al dispositivo el identificador de hardware (también conocido como hash de hardware).  Una vez que lo tenga, puede registrar automáticamente el dispositivo con Windows AutoPilot.

Para obtener instrucciones sobre cómo hacerlo con Microsoft Intune, consulte la documentación sobre la [creación de un perfil de implementación de AutoPilot](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) que describe la configuración "convertir todos los dispositivos de destino en AutoPilot". 

Tenga en cuenta también que al usar el escenario [de Windows AutoPilot para dispositivos existentes](existing-devices.md) , no es necesario registrar previamente los dispositivos con Windows AutoPilot.  En su lugar, se usa un archivo de configuración (AutopilotConfigurationFile.jsen) que contiene todas las opciones de configuración del perfil de Windows AutoPilot. el dispositivo se puede registrar con Windows AutoPilot después del hecho mediante el mismo valor "convertir todos los dispositivos de destino en AutoPilot".

## <a name="manual-registration"></a>Registro manual

Para realizar el registro manual de un dispositivo, primero debe capturar su identificador de hardware (también conocido como hash de hardware).  Una vez completado este proceso, el identificador de hardware resultante se puede cargar en el servicio de Windows AutoPilot.  Dado que este proceso requiere el arranque del dispositivo en Windows 10 para obtener el identificador de hardware, esto está destinado principalmente a escenarios de prueba y evaluación.

> [!Note]
> Los clientes solo pueden registrar dispositivos con un hash de hardware.  Otros métodos (PKID, Tuple) están disponibles a través de los OEM o de los asociados de CSP, tal como se describe en las secciones anteriores.

## <a name="device-identification"></a>Identificación de dispositivos

Para definir un dispositivo para el servicio de implementación de Windows AutoPilot, es necesario capturar y cargar en el servicio un identificador de hardware único para el dispositivo. Aunque este paso es idóneo para el proveedor de hardware (OEM, Reseller o distribuidor), asociando automáticamente el dispositivo a una organización, también es posible hacerlo a través de un proceso de recopilación que recopila el dispositivo desde una instalación de Windows 10 en ejecución.

El identificador de hardware, también conocido comúnmente como hash de hardware, contiene varios detalles sobre el dispositivo, incluidos el fabricante, el modelo, el número de serie del dispositivo, el número de serie de la unidad de disco duro y muchos otros atributos que se pueden usar para identificar el dispositivo de forma exclusiva.

Tenga en cuenta que el hash de hardware también contiene detalles acerca de Cuándo se generó, por lo que cambiará cada vez que se genere. Cuando el servicio de implementación de Windows AutoPilot intenta coincidir con un dispositivo, tiene en cuenta los cambios como este, así como los cambios más importantes, como una nueva unidad de disco duro, y sigue pudiendo coincidir correctamente. Pero los cambios sustanciales en el hardware, como una sustitución de la placa base, no coincidirían, por lo que es necesario generar y cargar un nuevo hash.

### <a name="collecting-the-hardware-id-from-existing-devices-using-microsoft-endpoint-configuration-manager"></a>Recopilar el identificador de hardware de los dispositivos existentes mediante el punto de conexión de Microsoft Configuration Manager

El punto de conexión de Microsoft Configuration Manager recopila automáticamente los valores hash de hardware de los dispositivos Windows 10 existentes. Para obtener más información, consulte [recopilar información de Configuration Manager para Windows AutoPilot](/configmgr/comanage/how-to-prepare-win10#windows-autopilot). Puede extraer la información de hash de Configuration Manager en un archivo CSV.

> [!Note]
> Antes de cargar el archivo CSV en Intune, asegúrese de que la primera fila contiene el número de serie del dispositivo, el ID. de producto de Windows, el hash de hardware, la etiqueta de grupo y el usuario asignado. Si hay información de encabezado en la parte superior del archivo CSV, elimine esa información de encabezado. Vea los detalles en [inscribir dispositivos Windows en Intune](/intune/enrollment/enrollment-autopilot).

### <a name="collecting-the-hardware-id-from-existing-devices-using-powershell"></a>Recopilar el identificador de hardware de los dispositivos existentes mediante PowerShell

El identificador de hardware, o el hash de hardware, de un dispositivo existente está disponible a través de Instrumental de administración de Windows (WMI), siempre que el dispositivo ejecute una versión compatible del canal semianual de Windows 10. Para ayudar a recopilar esta información, así como el número de serie del dispositivo (útil para ver de un vistazo el equipo al que pertenece), se ha publicado un script de PowerShell llamado [Get-WindowsAutoPilotInfo.ps1 en el sitio web de galería de PowerShell](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo).

Para usar este script, puede descargarlo desde el Galería de PowerShell y ejecutarlo en cada equipo, o bien puede instalarlo directamente desde el Galería de PowerShell. Para instalarlo directamente y capturar el hash de hardware desde el equipo local, use los siguientes comandos desde un símbolo del sistema de Windows PowerShell con privilegios elevados:

```powershell
md c:\\HWID
Set-Location c:\\HWID
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

Los comandos también se pueden ejecutar de forma remota, siempre y cuando los permisos de WMI estén en vigor y se pueda tener acceso a WMI a través del firewall de Windows en ese equipo remoto. Vea la ayuda del script [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) (con "Get-Help Get-WindowsAutoPilotInfo.ps1") para obtener más información sobre la ejecución del script.

>[!IMPORTANT]
>No conecte dispositivos a Internet antes de capturar el identificador de hardware y crear un perfil de dispositivo AutoPilot. Esto incluye la recopilación del identificador de hardware, la carga de. CSV en MSfB o Intune, asignando el perfil y confirmando la asignación de perfil. La conexión del dispositivo a Internet antes de que se complete este proceso hará que el dispositivo Descargue un perfil en blanco que se almacena en el dispositivo hasta que se quite de forma explícita. En la versión 1809 de Windows 10, puede borrar el perfil almacenado en caché reiniciando OOBE. En versiones anteriores, la única manera de borrar el perfil almacenado es volver a instalar el sistema operativo, restablecer la imagen inicial del equipo o ejecutar **Sysprep/generalize/Oobe**. <br>
>Después de que Intune informe de que el perfil está listo, solo debe conectarse a Internet.

>[!NOTE]
>Si OOBE se reinicia demasiadas veces, puede entrar en un modo de recuperación y no ejecutar la configuración de AutoPilot. Puede identificar este escenario si OOBE muestra varias opciones de configuración en la misma página, incluidos el idioma, la región y la distribución del teclado. El archivo OOBE normal muestra cada uno de ellos en una página independiente. La clave de valor siguiente realiza un seguimiento del recuento de reintentos de OOBE: <br>
>**HKCU\SOFTWARE \\ Microsoft \\ Windows \\ CurrentVersion \\ UserOOBE** <br>
>Para asegurarse de que OOBE no se ha reiniciado demasiadas veces, puede cambiar este valor a 1.

## <a name="registering-devices"></a>Registro de dispositivos

<img src="./images/image2.png" width="511" height="249" alt="process" />


Una vez que se han capturado los identificadores de hardware de los dispositivos existentes, se pueden cargar a través de diversos medios. Consulte la documentación detallada para cada mecanismo disponible.

-   [Microsoft Intune](enrollment-autopilot.md).  Este es el mecanismo preferido para todos los clientes.
    - El centro de administración de Microsoft Endpoint Manager se usa para la inscripción de dispositivos de Intune.
-   [Centro de Partners](https://msdn.microsoft.com/partner-center/autopilot).  Los asociados de CSP lo usan para registrar los dispositivos en nombre de los clientes.
-   [Microsoft 365 empresa Premium](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa).  Normalmente, lo usan las pequeñas y medianas empresas (SMB) que administran sus dispositivos mediante Microsoft 365 Empresa Premium.
-   [Microsoft Store para la empresa](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles).  Es posible que ya esté usando MSfB para administrar las aplicaciones y la configuración.

A continuación se proporciona un resumen de las funcionalidades de cada plataforma.<br>
<br>
<table>
<tr>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Plataforma/portal</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">¿Registrar dispositivos?</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Crear o asignar perfil</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">DeviceID aceptable</font></td>
</tr>

<tr>
<td>API directa de OEM</td>
<td>SÍ-1000 a la hora máx.</td>
<td>No</td>
<td>Tupla o PKID</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/partner-center/autopilot">Centro de partners</a></td>
<td>SÍ-1000 a la hora máx.</td>
<td>SÍ<b><sup>34</sup></b></td>
<td>Tuple o PKID o 4K HH</td>
</tr>

<tr>
<td><a href="enrollment-autopilot.md">Intune</a></td>
<td>SÍ: 500 a una hora como máximo<b><sup>1</sup></b></td> 
<td>SÍ<b><sup>12</sup></b></td> 
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles">Microsoft Store para Empresas</a></td>
<td>SÍ-1000 a la hora máx.</td>
<td>SÍ<b><sup>4</sup></b></td>
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 Empresa Premium</a></td>
<td>SÍ-1000 a la hora máx.</td>
<td>SÍ<b><sup>3</sup></b></td>
<td>4K HH</td>
</tr>

</table>

><b><sup>1</sup></b> Plataforma recomendada de Microsoft para su uso<br>
><b><sup>2</sup></b> Licencia de Intune requerida<br>
><b><sup>3</sup></b> Las funcionalidades de características están limitadas<br>
><b><sup>4</sup></b> La asignación de Perfil de dispositivo se retirará de MSfB y del centro de Partners en los próximos meses<br>


Consulte también los temas siguientes para obtener más información acerca de los identificadores de dispositivo:
- [Identificación del dispositivo](#device-identification)
- [Instrucciones para dispositivos Windows AutoPilot](autopilot-device-guidelines.md)
- [Agregar dispositivos a una cuenta de cliente](/partner-center/autopilot)


## <a name="summary"></a>Resumen

Cuando se implementan nuevos dispositivos con Windows AutoPilot, son necesarios los siguientes pasos:

1.  [Registrar dispositivos](#registering-devices). Idealmente, este paso lo realiza el OEM, el revendedor o el distribuidor desde el que se compraron los dispositivos, pero también lo puede hacer la organización mediante la recopilación de la identidad de hardware y su carga manual.
2.  [Configure los perfiles de dispositivo](profiles.md)y especifique cómo se debe implementar el dispositivo y qué experiencia del usuario se debe presentar.
3.  Arranque el dispositivo. Cuando el dispositivo está conectado a una red con acceso a Internet, se pondrá en contacto con el servicio de implementación de Windows AutoPilot para ver si el dispositivo está registrado y, si es así, descargará la configuración del perfil, como la [Página estado de inscripción](enrollment-status.md), que se usa para personalizar la experiencia del usuario final.

## <a name="other-configuration-settings"></a>Otras opciones de configuración

- [Configuración de cifrado de BitLocker](bitlocker.md): puede configurar las opciones de cifrado de BitLocker que se aplicarán antes de que se inicie el cifrado automático.