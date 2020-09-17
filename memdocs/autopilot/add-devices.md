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
ms.openlocfilehash: 776cc47865853ae9b52218c0b2257840aea09219
ms.sourcegitcommit: 2339c927b6576db8878f34f167a9a45c5dc9f58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2020
ms.locfileid: "90689336"
---
# <a name="adding-devices-to-windows-autopilot"></a>Agregar dispositivos a Windows AutoPilot

**Se aplica a**

- Windows 10

Antes de implementar un dispositivo con Windows AutoPilot, el dispositivo debe estar registrado con el servicio de implementación de Windows AutoPilot. Idealmente, este registro lo realiza el OEM, el revendedor o el distribuidor desde el que se compraron los dispositivos. Sin embargo, el registro también se puede realizar en la organización mediante la recopilación de la identidad de hardware y su carga manual.

## <a name="oem-registration"></a>Registro de OEM

Al adquirir dispositivos de un OEM, ese OEM puede registrar automáticamente los dispositivos con Windows AutoPilot. Para obtener la lista de OEM que admiten el registro, consulte la sección sobre fabricantes y distribuidores de dispositivos participantes en la [Página de Windows AutoPilot](https://aka.ms/windowsautopilot).

Para que un OEM pueda registrar dispositivos para una organización, la organización debe conceder el permiso de OEM para hacerlo. El OEM inicia este proceso, con la aprobación concedida por un Azure AD administrador global de la organización. Consulte la sección "consentimiento del cliente" de la [Página de consentimiento del cliente](registration-auth.md#oem-authorization).

> [!Note]
> Aunque los hash de hardware (también conocidos como identificadores de hardware) se generan como parte del proceso de fabricación de dispositivos OEM, no se deben proporcionar directamente a clientes o asociados de CSP. En su lugar, el OEM debe registrar los dispositivos en nombre del cliente. En los casos en los que los asociados de CSP están registrando dispositivos, los OEM pueden proporcionar información de PKID a esos asociados para que admitan el proceso de registro de dispositivos.

## <a name="reseller-distributor-or-partner-registration"></a>Reseller, distribuidor o registro de asociados

Los clientes pueden adquirir dispositivos de revendedores, distribuidores u otros asociados. Siempre que estos revendedores, distribuidores y asociados formen parte del programa de [asociados de soluciones en la nube (CSP)](https://partner.microsoft.com/cloud-solution-provider), también pueden registrar los dispositivos del cliente. 

Al igual que con los OEM, a los asociados de CSP se les debe conceder permiso para registrar dispositivos para una organización. Puede usar el proceso que se describe en la [Página de consentimiento del cliente](registration-auth.md#csp-authorization). El asociado de CSP solicita una relación con la organización. El administrador global de la organización aprueba la solicitud. Después de la aprobación, los asociados de CSP agregan dispositivos mediante el [centro de Partners](https://partner.microsoft.com/pcv/dashboard/overview), ya sea directamente a través del sitio web o a través de las API disponibles que pueden automatizar las mismas tareas.

En el caso de los dispositivos Surface, Soporte técnico de Microsoft puede ayudar con el registro de dispositivos.  Para obtener más información, consulte [compatibilidad con el registro de Surface para Windows AutoPilot](https://docs.microsoft.com/surface/surface-autopilot-registration-support).

Windows AutoPilot no requiere permisos de administrador delegado al establecer la relación entre el asociado de CSP y la organización. Como parte del proceso de aprobación del administrador global, pueden optar por desactivar la casilla "incluir permisos de administración delegada".

> [!Note]
> Aunque los revendedores, distribuidores o asociados podrían arrancar cada nuevo dispositivo de Windows para obtener el hash de hardware (con el fin de proporcionarles a los clientes o el registro directo del asociado), no se recomienda. En su lugar, estos asociados deben registrar los dispositivos con la información de PKID obtenida del empaquetado de dispositivos (código de barras) u obtenerse electrónicamente del OEM o del asociado ascendente (por ejemplo, el distribuidor).

## <a name="automatic-registration-of-existing-devices"></a>Registro automático de dispositivos existentes

Puede registrar automáticamente un dispositivo existente si es:
- ejecutar una versión compatible del canal semianual de Windows 10.
- inscritos en un servicio MDM como Intune.

En el caso de los dispositivos que cumplen ambos requisitos, el servicio MDM puede pedir al dispositivo el hash de hardware. Una vez que lo tenga, puede registrar automáticamente el dispositivo con Windows AutoPilot.

Para obtener instrucciones sobre cómo hacerlo con Microsoft Intune, consulte la documentación sobre la [creación de un perfil de implementación de AutoPilot](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) que describe la configuración "convertir todos los dispositivos de destino en AutoPilot". 

Puede convertir automáticamente estos dispositivos en Windows mediante la configuración **convertir todos los dispositivos de destino en el piloto automático** de Intune. Para más información, vea [Crear un perfil de implementación de Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile). 

Al usar el escenario [de Windows AutoPilot para dispositivos existentes](existing-devices.md) , no es necesario registrar previamente los dispositivos con Windows AutoPilot. En su lugar, se usa un archivo de configuración (AutopilotConfigurationFile.jsen) que contiene todos los valores de configuración del perfil de Windows AutoPilot. Después, el dispositivo se puede registrar con Windows AutoPilot con la misma configuración "convertir todos los dispositivos de destino en AutoPilot".

## <a name="manual-registration"></a>Registro manual

Para registrar manualmente un dispositivo, primero debe capturar su hash de hardware. Una vez completado este proceso, el hash de hardware resultante se puede cargar en el servicio de Windows AutoPilot. Dado que este proceso requiere el arranque del dispositivo en Windows 10 para obtener el hash de hardware, el registro manual está destinado principalmente a escenarios de prueba y evaluación.

> [!Note]
> Los clientes solo pueden registrar dispositivos con un hash de hardware. Otros métodos (PKID, Tuple) están disponibles a través de los OEM o de los asociados de CSP, tal como se describe en las secciones anteriores.

## <a name="device-identification"></a>Identificación de dispositivos

Para identificar un dispositivo con Windows AutoPilot, el hash de hardware único del dispositivo se debe capturar y cargar en el servicio. Este paso es ideal para que el proveedor de hardware (OEM, Reseller o distribuidor) asocie automáticamente el dispositivo a una organización. También es posible identificar un dispositivo con un proceso de recopilación que recopile el dispositivo desde una instalación de Windows 10 en ejecución.

El hash de hardware contiene detalles sobre el dispositivo:
- fabricante
- model
- número de serie del dispositivo
- número de serie de la unidad de disco duro
- detalles sobre cuándo se generó el identificador
- muchos otros atributos que se pueden usar para identificar el dispositivo de forma única

El hash de hardware cambia cada vez que se genera porque incluye detalles sobre cuándo se generó. Cuando el servicio de implementación de Windows AutoPilot intenta coincidir con un dispositivo, tiene en cuenta los cambios similares. También tiene en cuenta los cambios grandes, como una nueva unidad de disco duro, y sigue pudiendo coincidir correctamente. Sin embargo, los cambios grandes en el hardware, como el reemplazo de la placa base, no coinciden, por lo que es necesario generar y cargar un nuevo hash.

### <a name="collecting-the-hardware-hash-from-existing-devices-using-microsoft-endpoint-configuration-manager"></a>Recopilación del hash de hardware de los dispositivos existentes mediante el punto de conexión de Microsoft Configuration Manager

El punto de conexión de Microsoft Configuration Manager recopila automáticamente los valores hash de hardware de los dispositivos Windows 10 existentes. Para obtener más información, consulte [recopilar información de Configuration Manager para Windows AutoPilot](/configmgr/comanage/how-to-prepare-win10#windows-autopilot). Puede extraer la información de hash de Configuration Manager en un archivo CSV.

> [!Note]
> Antes de cargar el archivo CSV en Intune, asegúrese de que la primera fila contiene el número de serie del dispositivo, el ID. de producto de Windows, el hash de hardware, la etiqueta de grupo y el usuario asignado. Si hay información de encabezado en la parte superior del archivo CSV, elimine esa información de encabezado. Vea los detalles en [inscribir dispositivos Windows en Intune](/intune/enrollment/enrollment-autopilot).

### <a name="collecting-the-hardware-hash-from-existing-devices-using-powershell"></a>Recopilación del hash de hardware de dispositivos existentes con PowerShell

El hash de hardware de un dispositivo existente está disponible a través de Instrumental de administración de Windows (WMI), siempre que el dispositivo ejecute una versión compatible del canal semianual de Windows 10. Puede usar un script de PowerShell ([Get-WindowsAutoPilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)) para obtener el número de serie y el hash de hardware de un dispositivo. El número de serie es útil para ver rápidamente a qué dispositivo pertenece el hash de hardware.

Para usar este script, puede usar cualquiera de los métodos siguientes:
- Descárguelo del Galería de PowerShell y ejecútelo en cada equipo.
- instálelo directamente desde el Galería de PowerShell.

Para instalarlo directamente y capturar el hash de hardware desde el equipo local, use los siguientes comandos desde un símbolo del sistema de Windows PowerShell con privilegios elevados:

```powershell
md c:\\HWID
Set-Location c:\\HWID
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

Puede ejecutar los comandos de forma remota si se cumplen las dos condiciones siguientes:
- Se han implementado los permisos de WMI
- Se puede tener acceso a WMI a través del firewall de Windows en el equipo remoto.

Para obtener más información sobre cómo ejecutar el script, vea la ayuda del script [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) mediante "Get-Help Get-WindowsAutoPilotInfo.ps1".

>[!IMPORTANT]
>No conecte dispositivos a Internet antes de capturar el hash de hardware y crear un perfil de dispositivo AutoPilot. Esto incluye la recopilación del hash de hardware, la carga de. CSV en MSfB o Intune, asignando el perfil y confirmando la asignación de perfil. La conexión del dispositivo a Internet antes de que se complete este proceso hará que el dispositivo Descargue un perfil en blanco que se almacena en el dispositivo hasta que se quite de forma explícita. En la versión 1809 de Windows 10, puede borrar el perfil almacenado en caché reiniciando OOBE. En versiones anteriores, la única manera de borrar el perfil almacenado es volver a instalar el sistema operativo, restablecer la imagen inicial del equipo o ejecutar **Sysprep/generalize/Oobe**. <br>
>Después de que Intune informe de que el perfil está listo, solo debe conectarse a Internet.

>[!NOTE]
>Si OOBE se reinicia demasiadas veces, puede entrar en un modo de recuperación y no ejecutar la configuración de AutoPilot. Puede identificar este escenario si OOBE muestra varias opciones de configuración en la misma página, incluidos el idioma, la región y la distribución del teclado. El archivo OOBE normal muestra cada uno de ellos en una página independiente. La clave de valor siguiente realiza un seguimiento del recuento de reintentos de OOBE: <br>
>**HKCU\SOFTWARE \\ Microsoft \\ Windows \\ CurrentVersion \\ UserOOBE** <br>
>Para asegurarse de que OOBE no se ha reiniciado demasiadas veces, puede cambiar este valor a 1.

## <a name="registering-devices"></a>Registro de dispositivos

<img src="./images/image2.png" width="511" height="249" alt="process" />


Una vez que se han capturado los hash de hardware de los dispositivos existentes, se pueden cargar de cualquiera de las maneras siguientes:

- [Microsoft Intune](enrollment-autopilot.md). Este es el mecanismo preferido para todos los clientes.
  - El centro de administración de Microsoft Endpoint Manager se usa para la inscripción de dispositivos de Intune.
- [Centro de Partners](https://msdn.microsoft.com/partner-center/autopilot). Los asociados de CSP lo usan para registrar los dispositivos en nombre de los clientes.
- [Microsoft 365 Empresa & administrador de Office 365](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa). Normalmente, lo utilizan las pequeñas y medianas empresas (SMB) que administran sus dispositivos mediante Microsoft 365 Empresa.
- [Microsoft Store para la empresa](/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles). Es posible que ya esté usando MSfB para administrar las aplicaciones y la configuración.

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

Para obtener más información acerca de los identificadores de dispositivo, consulte los temas siguientes:
- [Identificación del dispositivo](#device-identification)
- [Instrucciones para dispositivos Windows AutoPilot](autopilot-device-guidelines.md)
- [Agregar dispositivos a una cuenta de cliente](/partner-center/autopilot)


## <a name="summary"></a>Resumen

Cuando se implementan nuevos dispositivos con Windows AutoPilot, son necesarios los siguientes pasos:

1. [Registrar dispositivos](#registering-devices). Idealmente, este paso lo realiza el OEM, el revendedor o el distribuidor desde el que se compraron los dispositivos. Sin embargo, la organización también puede realizar el registro mediante la recopilación de la identidad de hardware y su carga manual.
2. [Configure los perfiles de dispositivo](profiles.md). Especifique cómo se debe implementar el dispositivo y qué experiencia del usuario se debe presentar.
3. Arranque el dispositivo. Si el dispositivo está conectado a una red con acceso a Internet, se pondrá en contacto con el servicio de implementación de Windows AutoPilot para ver si el dispositivo está registrado. Si se registra, se descargará la configuración del perfil, como la [Página estado de inscripción](enrollment-status.md), que se usa para personalizar la experiencia del usuario final.

## <a name="next-steps"></a>Pasos siguientes

[Configuración de cifrado de BitLocker](bitlocker.md): puede configurar las opciones de cifrado de BitLocker que se aplicarán antes de que se inicie el cifrado automático.
